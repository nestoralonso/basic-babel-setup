# basic-babel-setup
Sin usar gulp o grunt


## Paso 1: Crear un proyecto vacio de npm
npm init -y

# Paso 2: Instala babel, browserify y el preset por defecto de es2015 (aka es6)
npm install -y browserify babel babel-preset-es2015

# Paso 3: editar package.json
Ahora editar el package.json generado y añadir esta línea en la sección de scripts
"build": "browserify src/main.js -t babelify --outfile dist/bundle.js"
