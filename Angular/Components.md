## Components

**app.component.html**

Angular transforms .html file to .js file and then renders it.


**App.component.ts:**

whatever.component.ts

To inform angular to treat a typescript class as a component (this changes what angular does with it behind the scenes), you have to attach the @Component decorator. 

**App.module.ts**

You have to declare every single component that you use. 


### Decorators:

Decorators allows you to attach extra information to the class.

```javacript
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
```


**selector**: css selector by which angular will identify this whenever it encounters it in html code. See index.html, you'll see <app-root></app-root>

Good idea: For selectors, prefix elements with app- , just to not confuse with native html elements


**templateUrl**: What to render? This file holds the content of the file that should be rendered when selector is found


**styleUrls**: CSS to ONLY be applied to this component




### Adding Custom Components

You have to export a class

```javacript
import {Component} from '@angular/core';

@Component({
  selector: 'app-user',
  template: `
    <p>Hello!</p>
    <p>I'm the user component</p>`
})
export class UserComponent {};
```

You can use an inline template, as above. Now add the component to app.module.ts.

```javascript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { UserComponent} from './user.component';

@NgModule({
  declarations: [
    AppComponent,
    UserComponent
  ],
  imports: [
    BrowserModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

Now you can use the component in the app.component.html file

### String Interpolation

```javascript
@Component({
  selector: 'app-user',
  template: `
    <p>Hello {{ name }} </p>
    <p>I'm the user component</p>`
})
export class UserComponent {
  name = 'Aseel';
}
```

### Listening to Events

```javacript
@Component({
  selector: 'app-user',
  template: `
    <input type="text" (input)="onUserInput($event)">
    <p>Hello {{ name }} </p>
    <p>I'm the user component</p>`
})
export class UserComponent {
  name = 'Aseel';
  onUserInput(event) {
      this.name = event.target.value;
  }
}
```

Basically,
```javascript
 <input type="text" (input)="onUserInput($event)">
```

Note: $event is a reserved name

### Binding

**Property Binding**

Example: 

```javascript
<input type="text" (input)="onUserInput($event)" [value]="name">
```

Basically,
[property]="whatever" binds the variable whatever to that property.

**Set the value attribute of the html element to some text**

```javascript
<input type="text" (input)="onUserInput($event)" value={{name}}>
```

Sometimes you don't have an attribute, so the first syntax becomes important.

#### Two way Binding

**Event binding:** (input)="onUserInput($event)"

**Property Binding:** [value]="name"

**Shorten:** 
Listen to input event, and set the value
```javascript
<input type="text" [(ngModel)]="name">
```

Angular will now manage the binding in two directions. I.e, ngModel directive enables *two way binding*. It listens to the input event, and binds the value. Thus,
you can ONLY use it on an element that has a value property it can bind to.

For ngModel to work, we need to add a new module to app.module.ts:

So,

```javascript
import { FormsModule } from '@angular/forms'
...
@NgModule({
...
imports: [
	...,
	FormsModule
]
...
})
```


### Summary

4 Ways to Bind:

* String Interpolation to output text
* Property Binding to pass data into a property
* Event Binding to listen to an event
* Two way binding to do event binding and property binding simultaneously (as long as we're talking about  the input event, and the value property)


### Binding Component Properties

What if you wanted to pass data in from the outside? 

```
<app-user [name]="'Max'"> <app-user>
```

Note the single quotes around Max, this is so that it is interpreted as a string. 

This isn't enough. By default, name can't be set from outside. To do this, you need to add a decorator.

Go into user.component.ts, and add the following:

```
import { Component, Input } from '@angular/core';

export class UserComponent{
	@Input() name;
	...
}
```

@Input is the decorator (all decorators are just functions). 

### Listening to Custom Events

**app.component.html**:

```
<app-user [name]="rootName" (nameChanged)="onNameChanged($event)"></app-user>
```

**app.component.ts**:

```
export class AppComponent {
  title = 'app';
  rootName = 'Aseel';
  onNameChanged(newName) {
    this.rootName = newName;
  }
}
```

**user.component.html**:

```
  <input type="text" (input)="onUserInput($event)" [value]="name">
```
  
**user.component.ts**:

```javascript
import { ..., Output, EventEmitter} from '@angular/core';

@Component({
  selector: 'app-user',
  template: 'user.component.html'
 })
 
 export class UserComponent {
  @Input() name;
  @Output() nameChanged = new EventEmitter<string>();
  onUserInput(event) {
    this.nameChanged.emit(event.target.value);
  }
}
```


### Multiple Components and Using the CLI for Component Generation

**Command**:

n generate component <component name>
	
n g c <component name>

This will create a new folder in app folder named 'component name'.

Note: In app.module.ts, you'll see everything automatically added once you run the above.

