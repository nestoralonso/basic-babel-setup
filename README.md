# basic-babel-setup
Sin usar gulp o grunt

#### Paso 0: Crear una carpeta src y una dist para los fuentes y para el bundle (archivo con todo incluido)
```bash
mkdir src 
mkdir dist
```
en src crear un main.js con este contenido
```javascript
import { suma, multiplicacion } from './matematicas';

var res = suma(2, 3);
console.log('res= ' + res);

res = multiplicacion(2, 6);
console.log('res= ' + res);
```
y un matematicas.js con el siguiente contenido
```javascript
export function suma(x, y) {
    return x + y;
}

export function multiplicacion(x, y) {
    return x * y;
}
```

### Paso 1: Crear un proyecto vacio de npm
npm init -y

### Paso 2: Instalar dependencias 
Instala babel, browserify y el preset por defecto de es2015 (aka es6), el --save-dev es para que lo guarde en package.json
npm install --save-dev babel babel-preset-es2015 browserify babelify 

### Paso 3: editar package.json
Ahora editar el package.json generado y añadir esta línea en la sección de scripts
"build": "browserify src/main.js -t babelify --outfile dist/bundle.js"

### Paso 4: poner un archivo de configuracion para babel
Crear un archivo .babelrc, en este se guarda la configuracion de babel, con el siguiente contenido
```json
{
  "presets": [ "es2015"]
}
```

### Paso 5: Correr el script para crear el bundle
npm run build