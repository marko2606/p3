# Webpack Demo App

Dummy App that shows how to setup JS project and configure Webpack

## GIT branches
```
git branch

# checkout master to get latest version of complete demo
git checkout master

# checkout workshop1 to get version from firt workshop
git checkout workshop1
```

## Table of Contents
- [Requirements](##Requirements)
- [Basic information](#Basic information)
- [Creating project](#Creating project)
- [Get Started](#Get Started)
- [Links](#links)


## Requirements

You need to have NodeJS instaled.

## Basic information

Webpack is a tool to build JavaScript modules in your application. It simplifies your workflow by quickly constructing a dependency graph of your application and bundling them in the right order. webpack can be configured to customise optimisations to your code, to split vendor/css/js code for production, run a development server that hot-reloads your code without page refresh and many such cool features.

## Image?

### Configuration

All of the configuration information are stored in webpack.config.js file. Config file needs to export a JS object that holds the configuration of webpack. Use NodeJS sytax for exporting.

example of webpack.config.js file
```
module.exports = {
	entry: {
		// entry configuration
	},
	output: {
		// output configuration
	},
	module: {
        // module/loaders configuration
	},
	plugins: [
		// plugin configuration
	]
};

```

### 4 basic concepts for configuring webpack. 

1. Entry point 
2. Output point 
3. Module - Loaders 
4. Plugins 


These concepts are properties of a weback module.

1. Entry point
    - Instructs the webpack where to start bundling the files. There can be more that one entry point, and it can be in the format of a string, an object or an array.

    ```
    module.exports = {

        ...

        entry: './src/index.js'

        ...

    }
    
    ```
2. Output point
    - JS object where we configure what the output should look like, where to store it and what to name it. 
    - Use path property to tell webpack where to store the files. Define path using nodejs syntax at the beginning of the webpack.config.js file. Call path.resolve(__dirname, 'dist'). '__dirname' refers to current directory, second argument refers to subdirectory where we want to store out files. Why are we using the output path.resolve method? The output path needs to be an absolute path. Webpack needs to write something there, to create something.
    - To set the name of the file we want to create we use filename property.
    - Use publicPath to tell the webpack the location of where the files should be stored?
    ```

    var path = require('path');

    module.exports = {

        ...
        
        output: {
            path: path.resolve(__dirname, 'dist'),
            filename: 'bundle.js',
            publicPath: '/dist'
        }

        ...

    }

    ```
3. Modules - Loaders
    - Module needs some rules property to tell it how to behave with certain file types.
    - test property tells webpack what rules apply on what file types.
    - Loader property tells the webpack what loader should use for that file(s). In this case we are using babel loader so we can use es6 syntax.
    - When using multiple loaders order of that file in array is important because webpack will run your loaders in reverce order!


```
    module.exports = {

        ...

          module: {
            rules: [
                {
			test: /\.js$/,
			exclude: /node_modules/,
			use: {
				use: ['babel-loader'],
				options: {
				presets: ['env']
				}
			    }
		}
            ]
	    }

        ...

    }

```

4. Plugins
    - Similar to loaders. Plugin are applied to your bundle before it is outputted.
    - Usage: To minify the code, dinamicly put js/css/images to you html... 

```
    const HtmlWebpackPlugin = require('html-webpack-plugin');

    module.exports = {

        ...

          plugins: [
            new HtmlWebpackPlugin({
		template: config.HTML_ENTRY_POINT
		})
          ]

        ...

    }


```

## Creating a project

Initalize a package.json. -y answers all the questions with 'yes'

```
npm init -y
```

Install webpack

```
npm install --save-dev webpack
```

create a build script in package.json

```
"scirpt": {
    "build": "webpack src/index.js dist/bundle.js"
}
```

Adding html-webpack-plugin to attach bundle files to index.html

```
npm install --save-dev html-webpack-plugin
```

Create webpack.config.js file in root directory.

```
    var path = require('path');

    module.exports = {
        entry: './src/index.js',
        output: {
            path: path.resolve(__dirname, 'dist'),
            filename: 'bundle.js'
        }

    }
```

Add HtmlWebpackPlugin const to config file.

```
const HtmlWebpackPlugin = require('html-webpack-plugin');
```

Activate plugin

```
    const HtmlWebpackPlugin = require('html-webpack-plugin');
    module.exports = {

        ...

     plugins: [
          new HtmlWebpackPlugin({
              template: './src/index.html',
              title: 'Webpack Workshop'
          })
      ]

        ...

    }

```

Webpack will bundle our files into dist/bundle.js and also create a copy of index.html based on our configuration(Dinamicly change title from webpack);

run build
open index.html in dist



## Install rimraf for cleaning dist and adding npm script for clean
```
npm install --save-dev rimraf
npm run clean
```

## Adding css [link](https://webpack.js.org/loaders/css-loader/)
```
npm install --save-dev style-loader css-loader 
```

## Adding sass [link](https://webpack.js.org/loaders/sass-loader/)
```
npm install --save-dev sass-loader node-sass 
```

## Adding extract-text-webpack-plugin to extract CSS to bundle.css
```
npm install --save-dev extract-text-webpack-plugin
```

## Adding bootstrap
```
npm install --save-dev bootstrap-sass
npm install --save-dev file-loader
```

## Adding babel [link](https://webpack.js.org/loaders/babel-loader/)
```
npm install --save-dev babel-loader babel-core babel-preset-env 
```

## Build for production and adding to npm scripts
```
webpack -p
npm run build-prod
```

## Adding Webpack Dev Server [link](https://webpack.js.org/configuration/dev-server/)
```
npm install --save-dev webpack-dev-server
```


## Get Started [link](https://webpack.js.org/guides/get-started/)
```
npm install --save-dev webpack
webpack
```


## Links
- [NPM](https://www.npmjs.com)
- [Webpack](https://webpack.js.org)
- [Babel](https://babeljs.io)
- [Webpack 2: The Complete Developer's Guide](https://www.udemy.com/webpack-2-the-complete-developers-guide/learn/v4/overview)
