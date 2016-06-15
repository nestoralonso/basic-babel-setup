# basic-babel-setup
Sin usar gulp o grunt (para gulp preguntarle a Nicolas, :smiley:) 

### Intro
Si bien Chrome y Webkit ya son casi 100% compatibles con es6, la parte que aún no esta implementada en los browsers es la de imports y exports. Babel sirve para pegar todos los fuentes en un bundle que puede ser incluido en la pagina y que contiene todos los archivos fuentes, además puede transpilar features de es7, es6 a es5 para hacerlo compatible con navegadores como Internet Explorer o versiones anteriores de Chrome.

### Paso 00
Previamente se debe tener instalado nodejs. nodejs incluye una herramienta llamada npm que sirve para instalar dependencias y ejecutar comandos.

#### Paso 0: Crear una carpeta src y una dist para los fuentes y para el bundle (archivo con todo incluido)
```bash
mkdir src 
mkdir dist
```
en la carpeta *src* crear un *main.js* con este contenido
```javascript
import { suma, multiplicacion } from './matematicas';

var res = suma(2, 3);
console.log('res= ' + res);

res = multiplicacion(2, 6);
console.log('res= ' + res);
```
y un *matematicas.js* con el siguiente contenido
```javascript
export function suma(x, y) {
    return x + y;
}

export function multiplicacion(x, y) {
    return x * y;
}
```

### Paso 1: Crear un proyecto vacio de npm

La siguiente línea crea un archivo llamado *package.json* en donde se guardan las dependencias externas del proyecto

```bash
npm init -y
```

### Paso 2: Instalar dependencias 
Instala *babel*, *browserify*, *babelify* y el preset por defecto de es2015 (aka es6), el --save-dev es para que lo guarde en *package.json*
```bash
npm install --save-dev babel babel-preset-es2015 browserify babelify 
```

### Paso 3: editar package.json
Ahora editar el *package.json* generado y añadir esta línea en la sección de scripts
```javascript
"build": "browserify src/main.js -t babelify --outfile dist/bundle.js"
```
El archivo deberia quedar algo asi
```json
{
  "name": "basic-babel-setup",
  "version": "1.0.0",
  "description": "Sin usar gulp o grunt",
  "main": "index.js",
  "scripts": {
    "build": "browserify src/main.js -t babelify --outfile dist/bundle.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/nestoralonso/basic-babel-setup.git"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/nestoralonso/basic-babel-setup/issues"
  },
  "homepage": "https://github.com/nestoralonso/basic-babel-setup#readme",
  "devDependencies": {
    "babel": "^6.5.2",
    "babel-preset-es2015": "^6.9.0",
    "babelify": "^7.3.0",
    "browserify": "^13.0.1"
  }
}
```

### Paso 4: poner un archivo de configuracion para babel ** importante **
Crear un archivo *.babelrc*, en este se guarda la configuracion de babel, con el siguiente contenido
```json
{
  "presets": [ "es2015"]
}
```
Babel necesita configuración porque puede hacer un gran variedad de cosas como transpilar es6, es7, o el lenguaje loco de react que se llama JSX ( q es como JS + HTML ), entonces dependiendo de lo que se quiera se pueden incluir otros presets o plugins dependiendo de los features que se quieran usar como *generators* o el *object spread operator* que aún no son standarden EcmaScript.

### Paso 5: Correr el script para crear el bundle
```bash
npm run build
```
Este paso genera un *bundle.js* en la carpeta dist, este se puede jecutar directamente en node on si es para una página incluirlo en la sección de scripts

### Qué leer después

La función básica de *npm* es bajar dependencias, pero también sirve para automatizar  tareas como:
- Estar pendiente de cambios en los fuentes, compilar y recargar automaticamente el browser.
- correr preprocesadores como sass (css en esteroides), less (es como sass pero distinto ```¯\_(ツ)_/¯``` ). 
- correr linters (estos revisan el código y alertan de posibles errores como falta de puntos y comas o indentación incorrecta)
- correr test automatizados (ver jasmine o mocha)
 
*npm*, *grunt* y *gulp* son comparables a herramientas como *make* o como se llame el *make* de java.

 Ver [npm as a build tool](http://blog.keithcirkel.co.uk/how-to-use-npm-as-a-build-tool/) 

**Nota**: hay veces para empezar es bueno bajar *boilerplates* que son esqueletos de proyecto que ahorran mucho trabajo, como por ejemplo este [boilerplate](https://github.com/gruberb/angular-boilerplate) de angular (q no he probado, es solo un ejemplo), aunque hay veces estos incluyen demasiadas cosas que realmente uno no usa o no entiende.

### Alternativas
Otras herramientas populares para correr tareas son *grunt.js* y *gulp.js* (más nuevo), en estos las tareas se hacen en javascript. Otros setups avanzados incluyen *webpack*.

Para bajar dependencias a veces también se usa *bower* (deps de browser como jquery o angular) o *jspm*.