# Data Binding

![DataBinding](https://i.imgur.com/YAPcE2k.png "")

4 Ways to Bind:
	•	String Interpolation to output text
	•	Property Binding to pass data into a property
	•	Event Binding to listen to an event
	•	Two way binding to do event binding and property binding simultaneously (as long as we're talking about the input event, and the value property)


## String Interpolation

```
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

**Three Requirements:**
- Whatever is in between {{ }} has to return a string.
- You CANT add Multiline Expressions
- You CAN use ternary expressions

## Property Binding

**TypeScript**
```
export class ServersComponent implements onInit {

	allowNewServer = false;
	
	constructor() {
		setTimeout(() => {
			this.allowNewServer = true;
		},2000)
	}

}
```

**Template**
```
<button
	class="btn btn-primary"
	[disabled]="allowNewServer" 
>Add Server</button>
```

To make disabled functionality dynamic, we can bind to it by enclosing disabled in square brackets. Square brackets indicate to Angular that we're using property binding, and we want to dynamically bind. Here, we are binding to the native disabled property the button has. 

You can bind to any native html property. Disabled takes true or false (a boolean). Other html properties might expect other types.

### Property Binding vs String Interpolation

If you want to output text, use string interpolation. If you want to change some property, use property binding. 

Don't mix

### Custom Property Binding

**app.component.ts**
```javascript
export class AppComponent {
  serverElements = [{type: 'server', name: 'Testserver', content: 'Just a test'}];
}
```

**app.component.html**
```
      <app-server-element
        *ngFor="let serverElement of serverElements"
        [element]="serverElement">
      </app-server-element>
```

**server-element.component.ts**
```
import { Component, OnInit, Input } from '@angular/core';
export class ServerElementComponent implements OnInit {
  @Input() element: { type: string, name: string, content: string };
}
```

#### Alias

You can pass a property name as you want to have it outside of this component into Input. For example, lets say into server-element you wanted to refer to it as element, but in app you wanted to refer to it as srvElem. You'd have the following

**server-element.component.ts**
```@Input('srvElem') element: { type: string, name: string, content: string };```

**app.component.html**
```
      <app-server-element
        *ngFor="let serverElement of serverElements"
        [srvElem]="serverElement">
      </app-server-element>
```

## Event Binding

**TypeScript**
```
export class ServersComponent implements onInit {

	allowNewServer = false;
	serverCreationStatus = 'No Server';
	serverName ='';
	
	constructor() {
		setTimeout(() => {
			this.allowNewServer = true;
		},2000)
	}
	
	onCreateServer() {
		this.serverCreationStatus = 'Server was created';
	}
	
	onUpdateServerName(event: Event) {
		this.serverName = (<HTMLInputElement>event.target).value; 
	}

}
```

**Template**
```
<input
	type="text"
	(input)="onUpdateServerName($event)">
<button
	class="btn btn-primary"
	[disabled]="allowNewServer" 
	(click)="onCreateServer"
>Add Server</button>
<p> {[ serverName }}
```

Parentheses are the indicator that we are using event binding.

You can bind to all events made available by the html element. 

**$event** 
Reserved word which gives us access to event data. You can use it in the template when using Event Binding. $event is the data emitted with that event. Click event for example gives us an object with some information on what was clicked. 
event.target -> html element on which event occurred 

---
**How do you know to which Properties or Events of HTML Elements you may bind?**
You can basically bind to all Properties and Events - a good idea is to console.log()  the element you're interested in to see which properties and events it offers.

**Important:** For events, you don't bind to onclick but only to click (=> (click)).

The MDN (Mozilla Developer Network) offers nice lists of all properties and events of the element you're interested in. Googling for YOUR_ELEMENT properties  or YOUR_ELEMENT events  should yield nice results.

---


## Two Way Data Binding

We combine property and event binding.

**TypeScript**
```
export class ServersComponent implements onInit {

	allowNewServer = false;
	serverCreationStatus = 'No Server';
	serverName ='';
	
	constructor() {
		setTimeout(() => {
			this.allowNewServer = true;
		},2000)
	}
	
	onCreateServer() {
		this.serverCreationStatus = 'Server was created';
	}
	
	onUpdateServerName(event: Event) {
		this.serverName = (<HTMLInputElement>event.target).value; 
	}

}
```

**Template**
```
<input
	type="text"
	[(ngModel)]="serverName"
>
<button
	class="btn btn-primary"
	[disabled]="allowNewServer" 
	(click)="onCreateServer"
>Add Server</button>
<p> {[ serverName }}
```

**[(ngModel)] will:**
1. Trigger the onInput Event
2. Update the value of serverName in our component 
3. Update the value of the input element if we change serverName somewhere else

** FOR TWO WAY BINDING TO WORK, YOU NEED TO ENABLE THE NGMODEL DIRECTIVE BY ADDING THE FORMSMODULE TO THE IMPORTS ARRAY IN APPMODULE **

```
import { FormsModule } from '@angular/core'
```


