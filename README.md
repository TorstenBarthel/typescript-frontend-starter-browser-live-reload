# typescript-frontend-starter-browser-live-reload

When setting up a Typescript frontend project from scratch it can be a bit of pain to set it all up correctly with browser reload on file change.
I just decided to write this entry in case someone needs to know since in the end it turned out to be a quiet simple setup but there are some distinct steps neccessary to make it work.

* **Install required packages:**
```
npm i typescript browser-sync gts --save-dev
```

* **Init Google Typescript gts to handle setup config and linters:**
Dont overwrite Typescript dependency if you want to stay with the newest version.
At the end you have a fully working typescript project with even a ./src folder and an index.ts file as starting point. There has also a package.json file been created with some useful npm scripts set up.
```
$ npx gts init
```
*  **Add following 'start:dev' command to package.json scripts:**

```
"scripts": {
    "start:dev": "browser-sync start --server './web-app' --watch -f ./src"
  },
```
* **Create basic folder structure:**

```
$ mkdir web-app
$ mkdir web-app/js
$ mkdir web-app/css
```
* **Create index.html file as starting point for our frontend web app:**
Create ./web-app/index.html with your favorite editor. I recommend Visual Studio Code for Typescript development.

* **Set up outDir in tsconfig.json:**
```
{
  "extends": "./node_modules/gts/tsconfig-google.json",
  "compilerOptions": {
    "rootDir": ".",
    "outDir": "web-app/js"
  },
  "include": [
    "src/**/*.ts",
    "test/**/*.ts"
  ]
}

```

* **Startup Typescript in watch mode:**
Open a new Terminal tab and  navigate to root folder of project.
```
$ npx tsc --watch
```

* **Add browser-sync  script to ./web-app/index.html:**
Directly before closing body tag.
```
<!-- browser-sync -->
    <script id="__bs_script__">//<![CDATA[
    document.write("<script async src='http://HOST:8080/browser-sync/browser-sync-client.js?v=2.27.11'><\/script>".replace("HOST", location.hostname));
//]]></script>
```

* **Use browser-sync npm script to start  development server that auto reloads browser on file change**
Open another Terminal tab and from root project folder run following command:
```
$ npm run start:dev
```
 Et Voila! From now on you just need two commands in two terminal tabs/windows to startup your development server: 
```
$ npx tsc --watch
$ npm run start:dev
```
If you edit some typescript files in ./src or html or css files in ./web-app/ the browser is reloaded.
The typescript compiler places the compiled Javascript files in ./web-app/js/src.

There are a lot of more options with brwoser-sync and there is also an UI spinned up. You have the abbillity to connect to remote devices for testing and more. Its worth taking a look into:
[browser-sync website](https://browsersync.io/)

For easy access I made a git repo with this complete Frontend/Web-App Typescript starter project. Just use it as starting point for your typescript web application.
In index.html there is still some example code since I am just starting to develop a basic game world with HTML and canvas rendering.
