---
title:  "Analisis de performance web continuo, Lighthouse - CI,"
date:   2023-02-07 09:15:07 -0300
tags: software bestPractices performance continousIntegration
categories: software
toc: true
---
Análisis de performance de sitios web de forma continua, para evaluar en cada cambio como evolucionan los indicadores mas importantes de performance hacie nuestros usuarios.

Cuando trabajamos con sitios web abiertos a internet, landing pages, sitios con usuarios casuales, que son encontrados por nuestrs usuarios a traves de campañas o buscadores.
Es muy importante que tengamos en cuenta ciertos indicadores de performance que van a influir mucho en la retencion de esos usuarios. 
Si el sitio es lento, tarda en renderizar, tarda en ser interactivo, es mucho mas  probable que los usuarios nos abandonden.

Para poder controlar estos indicadores de forma continua puede ser util agregar un paso en nuestra integracion continua que nos permita ver el impacto de cada cambio que hacemos en los indicadores basicos de perfomance. 

Asi como controlamos la cobertura de unit test, cantidad de code smells o simplemente si nuestro sistema compila ante cada cambio. Podemos usar la integracion continua para verificar la perfomance de los sitios web.


## Reportes de lightouse
Lighthouse es una herramienta automatizada [open-source](https://github.com/GoogleChrome/lighthouse) de google para verificar y diagnosticar la corrección, performance y calidad los sitios web.

![Lighthouse en Chrome]({{ site.baseurl }}/assets/screenshots/lighthouse/lighthouse-screen1.png)


Lightouse corre una serie de pruebas y mediciones y genera un reporte con indicadores clave y problemas. Esta incorporada en chrome en las herramientas de inspección y medicion.

![Reporte Lighthouse]({{ site.baseurl }}/assets/screenshots/lighthouse/lighthouse-screen2.png)

## Indicadores clave
Lighthouse divide sus indicadores en 5 categorías

+ Performance
+ Accesibilidad
+ PWA
+ Buenas Prácticas
+ SEO

En un enfoque de mejora continua deberíamos mejorar, o aunque sea no empeorar, los indicadores ante cada cambio que hagamos en nuestro sitio. 

Cuando los indicadores clave no estén en los valores predeterminados como aceptables por google, lighthouse nos va dar recomendaciones muy valiosas para mejorarlos. 

## Lighthouse CI
Es una herramienta que nos permite obtener reportes de lighthouse en el contexto de un servidor de Integración Continua (CI)

Primero necesitamos contar con un sistema de integración continua, puede ser github actions, azure devops, un esquema basado en jenkins o cualquier otro. 
Incluyendo un VCS como github, bitbucket o azure generalmente basado en git.

> *Integración continua* consiste en una práctica de desarrollo de software donde los miembros de un equipo integran sus cambios de forma frecuente y automatizada, como minimo diariamente.
> Cada integración se verifica de manera automatizada incluyendo tests, compilaciones y analisis estatico para detectar problemas.

Para agregar soporte para lighthouse-ci con las configuraciones por defecto debemos agregar un archivo 

**lighthouserc.js**

```js
module.exports = {
  ci: {
    upload: {
      target: 'temporary-public-storage',
    },
  },
};
```

Con esto vamos a poder trackear los resultados de lighthouse en un almacenamiento público y temporal proporcionado por google. 

Corriendo el comando ´lhci autorun´ lighthouse va a tratar de encontrar todos los archivos estaticos y correr el reporte por cada uno de ellos.

El siguiente paso es configurar nuestro servidor de CI para que este comando corra despues de cada pull request o de cada commit a master

### Ej: con github actions

**.github/workflows/ci.yml**

```yaml
name: CI
on: [push]
jobs:
  lhci:
    name: Lighthouse
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Use Node.js 16.x
        uses: actions/setup-node@v1
        with:
          node-version: 16.x
      - name: npm install, build
        run: |
          npm install
          npm run build
      - name: run Lighthouse CI
        run: |
          npm install -g @lhci/cli@0.8.x
          lhci autorun
```

Existen varias opciones de configuración dependiendo del tipo de servidor del sitio web, si es un sitio estatico, dinamico, si tenemos diferentes ambientes, etc.
para esto podemos ver la guia de configuración de [lighthouse-ci](https://github.com/GoogleChrome/lighthouse-ci/blob/main/docs/getting-started.md)

En mi caso estoy usando este enfoque en un sitio [Next.js](https://nextjs.org/) y mediante github actions corremos las pruebas sobre el entorno de desarrollo 
Además generamos un comentario en el pull request de github que muestra el estado del análisis de lighthouse.

Para eso tenemos un script que genera un comentario. Una vez que corre lighthouse uso la información que deja en el action para generar un comentario con un script custom les dejo el snipeet

Los análisis los corremos sobre un deploy temporal que vive mientras esta vivo el Pull Request
Pero se podría correr sobre el ambiente de dev y hacerlo una vez que el PR esta mergeado y deployado. 

Los snippets

**.github/workflows/pr.yml** 

```yaml
.....
      - name: Audit URLs using Lighthouse
        uses: treosh/lighthouse-ci-action@v9
        id: LHCIAction
        with:
          urls: |
            https://dev-site.com
          uploadArtifacts: false # save results as an action artifacts
          temporaryPublicStorage: true # upload lighthouse report to the temporary storage
      - name: Format Lighthouse comment
        id: LHCICommentFormat
        uses: actions/github-script@v6
        with:
          script: |
            const lighthouseCommentMaker = require('./.github/formatComment.js')
            const lighthouseOutputs = {
                        manifest: ${{ steps.LHCIAction.outputs.manifest }},
                        links: ${{ steps.LHCIAction.outputs.links }}
                      };
            const comment = lighthouseCommentMaker({ lighthouseOutputs });
            core.setOutput("comment", comment);
      - name: comment lighthouse PR
        uses: unsplash/comment-on-pr@master
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          msg: ${{ steps.LHCICommentFormat.outputs.comment }}
          check_for_duplicate_msg: false # OPTIONAL
....
```

**.github/formatComment.js**

```js
const formatScore = (/** @type { number } */ score) => Math.round(score * 100)
const emojiScore = (/** @type { number } */ score) =>
  score >= 0.8 ? '🟢' : score >= 0.5 ? '🟠' : '🔴'

const scoreRow = (
  /** @type { string } */ label,
  /** @type { number } */ score
) => `| ${emojiScore(score)} ${label} | ${formatScore(score)} |`

const scoreSpan = (
  /** @type { string } */ label,
  /** @type { number } */ score
) => `${label}: ${emojiScore(score)} ${formatScore(score)}`
/**
 * @param {LighthouseOutputs} lighthouseOutputs
 */
function makeComment(lighthouseOutputs) {
  const { summary } = lighthouseOutputs.manifest[0]
  const [[testedUrl, reportUrl]] = Object.entries(lighthouseOutputs.links)

  const comment = `## ⚡️🏠 Lighthouse   ${scoreSpan(
    'Performance',
    summary.performance
  )}, ${scoreSpan('Best practices', summary['best-practices'])}, ${scoreSpan(
    'SEO',
    summary.seo
  )}
### [Complete Report](${reportUrl}).
| Category | Score |
| -------- | ----- |
${scoreRow('Performance', summary.performance)}
${scoreRow('Accessibility', summary.accessibility)}
${scoreRow('Best practices', summary['best-practices'])}
${scoreRow('SEO', summary.seo)}
${scoreRow('PWA', summary.pwa)}
*Lighthouse ran against [${testedUrl}](${testedUrl})*
`

  return comment
}

module.exports = ({ lighthouseOutputs }) => {
  return makeComment(lighthouseOutputs)
}
```

Con eso podemos obtener un comentario parecido a este:

![Comentario en github]({{ site.baseurl }}/assets/screenshots/lighthouse/lighthouse-screen3.png)

## Links

+ [Lighthouse CI](https://github.com/GoogleChrome/lighthouse-ci)
+ [Guia de uso](https://developer.chrome.com/docs/lighthouse/overview/)
+ [Demistyfing speed tools](https://www.youtube.com/watch?v=mLjxXPHuIJo)
