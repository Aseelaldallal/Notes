### Basics

Angular uses TypeScript as its primary language. 

### Setup

Install Angular CLI

npm install -g @angular/cli

ng new my-dream-app

cd my-dream-app

ng serve

***ng serve:*** 
Spins up development server which hosts our angular applications. 


### Project Structure

app.component.html -> The Main Page
angular-cli.json -> Settings
.editorconfig -> how the file should look in our editor
karma.conf.js -> manages testing
tsconfig.js -> typescript config
tslint.json -> linting - warns if we write code that works but doens't fit official angular style guide
e2e folder -> store end to end tests
environments -> environment variables

Index.html:
<app-root></app-root>

Main.ts:
Responsible for starting angular all

Polyfill.ts:
Allows our app to use features that aren't present in older browsers


### Index.html

This is the page that the server serves. 

```
<app-root></app-root>
```

Our workflow compiles and bundles our code, and injects import statements into index.html.



### Main.ts

Starts angular app. You can think of main.ts file holding the first code to be executed in your final main.bundle.js file.

Notice: 
platformBrowserDynamic().bootstrapModule(AppModule)

Go to app.module.ts -> It tells angular which features of angular this app actually uses (efficiency)


### Decorators

TypeScript Feature.

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})

Component comes from Angular. The @ comes from Typescript and is a decorator. Refers to what is after it immediately.


