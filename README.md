

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

    "scripts": {
    "web": "webpack-dev-server --config webpack.config.js --hot --inline"
  }

13. The next 4 files and src folder are all added next to the package.json in the src folder.
13. Add a tsconfig.json file with the following.

    {
  "compilerOptions": { 
    "target": "es5",
    "module": "commonjs",  
    "lib": [ "es6", "dom" ],
    
    "experimentalDecorators": true    
  }
}

14. Add a webpack.config.json file with the following.
15. Add a index.html with the following.
16. Add a site.scss with the following.
17. Add the src folder.
18. The next 3 and 2 folders files are added in the newly create src folder.
19. Add a main.ts with the following.
20. Add a app.ts with the following.
21. Add a app.html with the following.
22. Add the home folder.
23. Add the shared folder.
24. The next 2 files are added to home folder.
25. Add the home.ts with the following.
26. Add the home.html with the following.
27. The next 2 files are added to the shared folder.
28. Add a main-nav.html with the following.
29. Add a footer-nav.html with the following.
30. In the terminal run *webpack* to check webpack transpiles correctly.
31. In the terminal *run npm run web*.
32. Open your browser to http://localhost:8000.
33. Enjoy!
