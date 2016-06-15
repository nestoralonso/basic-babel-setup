# basic-babel-setup
Sin usar gulp o grunt (para gulp preguntarle a Nicolas, :smiley:) 

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

### Paso 4: poner un archivo de configuracion para babel
Crear un archivo .babelrc, en este se guarda la configuracion de babel, con el siguiente contenido
```json
{
  "presets": [ "es2015"]
}
```

### Paso 5: Correr el script para crear el bundle
```bash
npm run build
```