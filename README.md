# react-webpack-starter
a webpack config starter for react-apps with newest @babel v7

Since I was preparing and practicing to learn React and mostly Redux, Thunk, Webpack. I was setting up a basic project with webpack as an attempt to learn webpack, specifically the latest version, v4.

> Don't follow the flaw in article just yet, if you are directly looking for final conclusion with @babel7`, because I'm going to explain the error that I have encountered.

I followed Traversy Media's video on setting up webpack for react boiler plate projects and also read the Webpack's official docs just to understand the concepts.

First, I set up the repo with npm init and done all the basic checkmarks to which my package.json generated.

Then I installed all the basic npm libraries that I would need in my project with
```
npm install --save react react-dom react-router-dom react-redux redux
```
This generates a new object in our `package.json` file named as dependencies.
After which I would install all the dev dependencies, so since this is all about webpack so I first installed webpack and all its needed peripherals as following:

```
npm install --save-dev webpack webpack-cli webpack-dev-server
```

It creates another object in package.json named as "devDependencies" and stores all the development dependencies over there.

After that we need babel to transpile our ES6, ES7+ code to javascript that browsers understand i.e., ES5 ( correct me if I've misunderstood). So for that we need to install all the babel and dependencies related to it.

```
npm install --save-dev babel-core babel-loader babel-preset-react babel-preset-env
```

and after that I have configured my webpack.config.js in the root folder as follows:

```
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
   entry: './src/index.js',
   output: {
      path: path.join(__dirname, '/dist'),
      filename: 'index_bundle.js'
   },
   module:{
      rules: [
         {
            test: /\.js$/,
            exclude: /node_modules/,
            use: {
               loader: 'babel-loader'
            }
         }
      ],
   },
   plugins: [
      new HtmlWebpackPlugin({
         template: './src/index.html'
      })
   ]   
}

```
Also first don't forget to install html-webpack-plugin because it let's recognize webpack about the html template we are going to use which we will configure in a few minutes.

Now Webpack's basic flow goes something like this,
it has an entry` object where we define location to our index.js file which is where our react-app is going to be

then it has an output` which uses Node.js default path module to showcase the directory where our output bundled will be generated

then it has this modules in which we define our rule that which files are needs to be compiles and bundled when we build the application.
in which we use also define our babel-loader

at the end we can define all of our plug-ins in an array with their new` instances each time.

So after all this I set up my basic react-app in src/index.js` but it was just giving simple error of

```
ERROR in ./src/index.js
Module build failed (from ./node_modules/babel-loader/lib/index.js):
Error: Cannot find module 'babel-preset-env' from 'B:\Shall\Practice\mystarter'
- Did you mean "@babel/env"?
    at Function.module.exports [as sync] (B:\Shall\Practice\mystarter\node_modules\resolve\lib\sync.js:43:15)
    at resolveStandardizedName (B:\Shall\Practice\mystarter\node_modules\@babel\core\lib\config\files\plugins.js:101:31)
    at resolvePreset (B:\Shall\Practice\mystarter\node_modules\@babel\core\lib\config\files\plugins.js:58:10)
    at loadPreset (B:\Shall\Practice\mystarter\node_modules\@babel\core\lib\config\files\plugins.js:77:20)
    at createDescriptor (B:\Shall\Practice\mystarter\node_modules\@babel\core\lib\config\config-descriptors.js:154:9)
    at items.map (B:\Shall\Practice\mystarter\node_modules\@babel\core\lib\config\config-descriptors.js:109:50)
    at Array.map (<anonymous>)
    at createDescriptors (B:\Shall\Practice\mystarter\node_modules\@babel\core\lib\config\config-descriptors.js:109:29)
    at createPresetDescriptors (B:\Shall\Practice\mystarter\node_modules\@babel\core\lib\config\config-descriptors.js:101:10)
    at presets (B:\Shall\Practice\mystarter\node_modules\@babel\core\lib\config\config-descriptors.js:47:19)
 @ multi (webpack)-dev-server/client?http://localhost:8080 (webpack)/hot/dev-server.js ./src/index.js main[2]
```

And I was totally unable to understand that what is going on, so I kept asking about queries in Reactiflux Discord Server in #need-help. I started uninstalling babel, and then install it again, and then I did the ultimate try

```
rm -rf node_modules
```

and tried to install babel-loader again, but it was still giving the same error of not being able to find the babel-preset module.
Then I got to know that Babel has just released the newer version v7 in which the naming conventions has been changed and I need to first uninstall all of those

* babel-loader
* babel-core
* babel-preset-env
* babel-preset-react

and install them as follows with `@babel/core and @babel/preset-react`, etc.
After all this head banging I thought wow the newer version is going to handle all problems, but nope it still didn't.

Since the starting I had .babelrc setup as
but I need to change the presets with the newer version and naming convention such as

```
{
    "presets": ["@babel/env", "@babel/react"]
}
```

Thus once the webpack understand the loader with the newer versions of babel it would take care of the error itself. 


I learned a key thing from this that I guess no other articles online for @babel-7` had explained/shared.

> So I thought to share my learning from today this way. I hope this helps and I get to be the new pioneer star, though I would like to be a React-Redux star and not the babel for now, because jobs/work you know!


I know I daydream a lot in the previous sentence. But yeah this was a simple TIL @babel7`. Enjoy till next time when I understand more about Redux Middlewares and it's side effects.

Thank you for the read. Please correct, explain, guide me into more deep level details of this occurrence.
