# basic-babel-setup
This tutorial covers how to use es6 modules in the browser.

### Intro
Although browsers like Chrome and Webkit are almost 100% percent compatible with es6, the one little bit that has not been implemented yet is es6 modules (aka import and export). One of the easiest tools for dealing with this problem is browserify, its approach is to concat all the files in a single bundle that can be included in the web page. In combination with babel can translate features from es7 that hasn't been shipped yet.

### Step 0
You must already have installed nodejs. 

### Step 1: create folders
```bash
mkdir src 
mkdir dist
```
In the *src* folder create a file *main.js* with this content:
```javascript
import { sum, mult } from './math-utils';

var res = sum(2, 3);
console.log('res= ' + res);

res = mult(2, 6);
console.log('res= ' + res);
```
and a file named *math-utils.js* with:
```javascript
export function sum(x, y) {
    return x + y;
}

export function mult(x, y) {
    return x * y;
}
```
### Step 1: Create an empty package.json file

Initialize an npm project using this line:
```bash
npm init -y
```
### Step 2: Install the development dependencies
Install *babel*, *browserify* and *babelify* and the es2015 preset:
 ```bash
npm install --save-dev babel-core babel-preset-es2015 browserify babelify 
```
the --save-dev flag saves the development dependencies section of the package.json file 

### Step 3: Test and save the setup
To use browserify you must specify an entry point, a transformation and an output destination, you can test the setup using:
```bash
node_modules/.bin/browserify src/main.js -t [ babelify --presets [ es2015 ] ] --outfile dist/bundle.js
```
In this case the entry is *main.js*, the transformation is *babelify* and the destination is *bundle.js*, note the presets section, from babel version 6 and up you must specifiy which plugins you will use, the es2015 preset contains all the plugins necesary to use es6 or es2015, if you use features from es7 or above you must specify the plugins in a .babelrc file. If the command work you should see a file bundle.js in the dist folder containing the all the function definitions and their invocations.

To avoid the retyping you can save the command to the scripts section of package.json like this:
```javascript
...
 "scripts": {
    "build": "browserify src/main.js -t [ babelify --presets [ es2015 ] ]  --outfile dist/bundle.js",
 }
...
```
To run the above script you simply type:
```bash
    npm run build
```