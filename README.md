

## A small tutorial to get going with Aurelia.
### This tutorial makes use of following bits and bobs: VS Code, NPM, Yarn, WebPack, Bootstrap (V4) and of course the mighty Aurelia.
1. Install VS Code from [here](https://code.visualstudio.com/) or Insider version [here](https://code.visualstudio.com/insiders).
2. Install NPM from [here](https://yarnpkg.com/lang/en/).
3. Install Yarn from [here](https://www.npmjs.com/get-npm?utm_source=house&utm_medium=homepage&utm_campaign=free%20orgs&utm_term=Install%20npm).
4. Create a project folder for your code.
5. Create a src folder for your source code.  
  a. I typically create test, docs folder next to the src, but not for this tutorial.
6. Open the project folder in VS Code.
7. Open a terminal in VS Code using *Ctrl+'* keystroke.
8. Change dir to src folder using *cd src*.
9. Initialise a project using *yarn init*.  
  a. This creates the package.json.
  b. Open the package.json in VS Code.
10. Add the dependencies using *yarn add aurelia-bootstrapper bootstrap@4.0.0-alpha.6 bootstrap-sass bootstrap-sass-loader*
11. Add the dev dependecies using *yarn add aurelia-webpack-plugin css-loader html-loader node-sass sass-loader style-loader ts-loader typescript webpack webpack-dev-server url-loader file-loader –dev*
12. Add to the package.json, after the devDependencies to following.
````
    "scripts": {
        "web": "webpack-dev-server --config webpack.config.js --hot --inline"
    }
````
13. The next 4 files and src folder are all added next to the package.json in the src folder.
14. . Add a tsconfig.json file with the following.
````
    {
      "compilerOptions": { 
        "target": "es5",
        "module": "commonjs",  
        "lib": [ "es6", "dom" ],        
        "experimentalDecorators": true    
      }
    }
````
14. Add a webpack.config.json file with the following.
````
    const path = require("path");
    const { AureliaPlugin } = require("aurelia-webpack-plugin");
    
    module.exports = {
      entry: "main",
    
      output: {
        path: path.resolve(__dirname, "dist"),
        publicPath: "/dist/",
        filename: "bundle.js",    
      },
      devtool: "eval-source-map",
      resolve: {
        extensions: [".ts", ".js"],
        modules: ["src", "node_modules"].map(x => path.resolve(x)),
      },
    
      module: {
        rules: [      
          { test: /\.scss$/i, use: ["style-loader", "css-loader", "sass-loader"] },
          { test: /\.ts$/i, use: "ts-loader" },
          { test: /\.html$/i, use: "html-loader" },
        ]
      },  
    
      plugins: [
        new AureliaPlugin({ includeAll: "src" })    
      ],
    };
````
15. Add a index.html with the following (note dodgy js references).
````
    <!DOCTYPE html>
    <html>
        <head>
            <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
        </head>
        <body>
            <div aurelia-app="main">
                <script src="/node_modules/jquery/dist/jquery.min.js"></script>
                <script src="/node_modules/bootstrap/dist/js/bootstrap.min.js"></script>
                <script src="/dist/bundle.js"></script>    
            </div>
        </body>
    </html>
16. Add a site.scss with the following.

     $primary-color: #8484ff;
    body{
        background-color: $primary-color;
    }
````
17. Add the src folder.
18. The next 3 and 2 folders files are added in the newly create src folder.
19. Add a main.ts with the following.
````
    import 'bootstrap/scss/bootstrap.scss';
    import '../site.scss';
    import 'aurelia-bootstrapper';
    import { Aurelia } from 'aurelia-framework';
    
    export function configure(aurelia: Aurelia){
        aurelia.use
            .standardConfiguration()
            .developmentLogging();        
        
        aurelia.start().then(() => aurelia.setRoot());
    }
````
20. Add a app.ts with the following.
````
    import { AppRouter, RouterConfiguration } from 'aurelia-router';

    export class App{
    
        testMessage: string;
        title: string;
        router: AppRouter;
    
        constructor(){
            this.testMessage = "Set in the constructor of App class";
            this.title = "TODO"
        }
    
        configureRouter(config: RouterConfiguration, router: AppRouter){
    
            this.router = router;
            config.title = this.title;
            config.map([
                {route: ['','home'], name: 'home', title: 'Home', moduleId: 'home/home', nav: true},
                //{route: 'about', name: 'about', title: 'About', moduleId: 'about/about', nav: true}
            ]);
        }
    }
````
21. Add a app.html with the following.
````
    <template>
        <require from="./shared/main-nav.html"></require>
        <require from="./shared/main-footer.html"></require> 
    
        <div class="container-fluid container-content-header">        
            <div class="container px-0">
                <main-nav router.bind="router" title.bind="title"></main-nav>            
            </div>
        </div>
        
        <div class="container-fluid">
            <div class="container container-content pt-3">
                <router-view></router-view>
            </div>
        </div>
        
        <div class="container-fluid">
            <div class="container container-content-footer">
                <main-footer></main-footer>
            </div>
        </div>    
    </template>
````
22. Add the home folder.
23. Add the shared folder.
24. The next 2 files are added to home folder.
25. Add the home.ts with the following.
````
    export class Home{
        testMessage: string;
        constructor(){
            this.testMessage = 'Home Placeholder';
        }
    }
````
26. Add the home.html with the following.
````
    <template>
        ${testMessage}
    </template>
````
27. The next 2 files are added to the shared folder.
28. Add a main-nav.html with the following.
````
    <template bindable="router,title">        
        <nav class="navbar navbar-main navbar-toggleable-md navbar-light bg-transparent py-0">
            <button class="navbar-toggler navbar-toggler-right" 
                    type="button" 
                    data-toggle="collapse" 
                    data-target="#navbarSupportedContent" 
                    aria-controls="navbarSupportedContent" 
                    aria-expanded="false" 
                    aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <a class="navbar-brand" href="#">${title}</a>
            <div class="collapse navbar-collapse" 
                 id="navbarSupportedContent">    
                <ul class="navbar-nav">
                    <li repeat.for="nav of router.navigation"
                        class="nav-item nav-item ${nav.isActive ? 'active' : ''}">
                        <a class="nav-link ${nav.isActive ? 'active' : ''}"
                           href.bind="nav.href">${nav.title}</a>
                    </li>
                </ul>
            </div>
        </nav>
    </template>
````
29. Add a footer-nav.html with the following.
````
    <template>
        <h3>placeholder for footer</h3>
    </template>
````
30. In the terminal run *webpack* to check webpack transpiles correctly.
31. In the terminal *run npm run web*.
32. Open your browser to http://localhost:8000.
33. Enjoy!
