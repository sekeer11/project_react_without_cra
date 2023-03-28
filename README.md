# Proyecto de ejemplo
#### Creating a React Project witout using create-react-app

---
## 1.- Iniciar un proyecto de node 
En la carpeta del proyecto abrir una terminal y ejecutar el comando:
#### **_( npm init -y )_**
---
## 2. Instalar las dependencias de Babel
Babel es un compilador que convierte su JavaScript moderno en versiones compatibles con versiones anteriores para que sean compatibles con navegadores o entornos más antiguos.
Para instalar Bable y sus depencias ejecute el comando:
#### **_( npm install --save-dev @babel/core babel-loader @babel/cli @babel/preset-env @babel/preset-react )_**
---
## 3. Instalar dependencias de Webpack
Webpack es un paquete de módulos estáticos para aplicaciones JavaScript modernas. Puede tomar diferentes archivos y agruparlos en un solo archivo JavaScript. Para instarlo ejecute el comando:
#### **_( npm install --save-dev webpack webpack-cli webpack-dev-server )_**
---
## 4. Instalar HtmlWebpackPlugin
HtmlWebpackPlugin es el paquete que simplifica la creación de archivos HTML para servir sus paquetes Webpack. Para instarlo ejecute el comando:
#### **_( npm install --save-dev html-webpack-plugin )_**
---
## 5. Instalar las dependencias de React
React es una biblioteca de JavaScript para crear interfaces de usuario.
El paquete de React en sí contiene solo la funcionalidad necesaria para definir los componentes de React, por lo tanto, generalmente se usa junto con un renderizador de React react-dompara crear elementos para la web. reacty react-domson las principales dependencias que necesitamos para usar React en nuestras aplicaciones. Para instalar las dependencias de React ejecute el comando:
#### **_( npm install react react-dom  )_**
---
## 6. Agregue archivos React
1. Cree una carpeta `public` y en la carpeta creada cree un archivo `index.html`. En el body crea un div con id root.
2. Crea una carpeta `src` y en ella crea un archivo `App.js` y en este un componente de React.
3. Crea un archivo `index.js` que será la entrada la aplicacion y agregue el siguiente codigo:
```import React from 'react'
import  { createRoot }  from 'react-dom/client';
import App from './src/App.js'

const container = document.getElementById('root');
const root = createRoot(container);
root.render(<App/>);
```
---
## 7. Configure Babel
En la carpeta raíz, cree un archivo llamado `.babelrcy` agregue el siguiente código:
```
{
    "presets": ["@babel/preset-env","@babel/preset-react"]
}
```
---
## 8. Configurar el paquete web
Cree un archivo llamado `webpack.config.js` y agregue el siguiente código:
```
const HtmlWebpackPlugin = require('html-webpack-plugin');
const path = require('path');

module.exports = {
  entry: './index.js',
  mode: 'development',
  output: {
    path: path.resolve(__dirname, './dist'),
    filename: 'index_bundle.js',
  },
  target: 'web',
  devServer: {
    port: '5000',
    static: {
      directory: path.join(__dirname, 'public')
},
    open: true,
    hot: true,
    liveReload: true,
  },
  resolve: {
    extensions: ['.js', '.jsx', '.json'],
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /(node_modules|bower_components)/,
        loader: 'babel-loader',
        options: { presets: ['@babel/env','@babel/preset-react'] },
      },
    ],
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: path.join(__dirname, 'public', 'index.html')
    })
  ]
};
```
---
## 9. Agregue scripts en package.json
En el archivo package.json en los scripts de objetos de scripts que se usarán para ejecutar Webpack e iniciar nuestra aplicación agregue scripts como se menciona a continuación:
```
"scripts": {
    "start": "webpack-dev-server .",
    "build": "webpack ."
  }
```
## 10. Inicie su aplicación
Ejecute `npm start` para iniciar la aplicación