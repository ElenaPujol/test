![UOC Logo](/images/uoc_masterbrand_2linies_posititiu.jpg)

# Desenv. front-end amb framew. JavaScript - PEC4
#### by Elena Pujol Olmos (epujolo@uoc.edu)

<br><br>

## Ejercicio 2 – Hola Mundo con Angular (1.25 punto)

<br>

### Crea una carpeta PEC4_Ej_Prac, dentro crea un fichero Markdown que tenga como nombre PEC4_Ej2_respuestas_estructura.md y responde a cada uno de los siguientes puntos:

<br>

1. ### (0.75 puntos) ¿Qué comando debes utilizar para crear un nuevo proyecto Angular utilizando Angular CLI denominado ecommerce? (A las preguntas que te haga Angular CLI puedes contestar utilizando las opciones por defecto).<br><br>Con Angular Cli crea el proyecto angular ecommerce y explica brevemente la estructura y ficheros que ha generado Angular CLI:

    * Ficheros de configuración en la raíz del proyecto:
      * tsconfig.app.json
      * angular.json
      * package.json
      * .editorconfig
      * .gitignore
      * …
    * Directorio node_modules
    * Directorio src:
      * index.html
      * main.ts
      * styles.css
      * test.ts
      * polyfills.ts
      * Directorio environments
      * Directorio assets
      * Directorio app
        * Ficheros app.component.*
        * Fichero app.module.ts
  
    ### Respuesta:

    Para crear un nuevo proyecto Angular utilizando Angular CLI denominado ecommerce hay que usar el siguiente comando:

        $ ng new ecommerce

    La estructura y ficheros generados són:
      * Ficheros de configuración en la raíz del proyecto: para la configuración del compilador TypeScript (tsconfig.app.json), describir la aplicación Angular a las herramientas de creación de aplicaciones (angular.json), ejecutar la aplicación con npm (package.json), mantener la consistencia en los estilos de codificación (.editorconfig), ignorar ficheros en el repositorio GIT (.gitignore),...
      * Directorio node_modules: contiene los paquetes node.js que usa la aplicación.
      * Directorio src: contiene el código de la aplicación. La plantilla HTML (index.html), donde la aplicación comienza a ejecutarse (main.ts), donde se describe el estilo de la plantilla HTML (styles.css), donde se comienza a ejecutar el test unitario de la aplicación (test.ts), donde la aplicación se compatibiliza en diferentes navegadores (polyfills.ts), ...
      * Directorio environments: donde todas las configuraciones de la aplicación se mantienen en un entorno específico.
      * Directorio assets: donde todo lo que se guarde dentro de este directorio se vuelve público.
      * Directorio app: donde se guardan los archivos que se han creado para los componentes de la aplicación.

<br>

2. ### (0.25 puntos) Explica cada uno de los siguientes decoradores generados por Angular CLI, detallando cada una de las propiedades que se definen en:

    * app.module.ts - @NgModule (declarations, imports, providers, bootstrap).
    * app.component.ts - @Component (selector, templateUrl, styleUrls).

    ### Respuesta:

    P

<br>

3. ### (0.25 puntos) ¿Es posible poder inyectar el template y los estilos en línea de un componente sin necesidad de especificarlos en templateUrl, styleUrls? ¿Es recomendable hacer esto?
   
    ### Respuesta:

    P
  
