# Routing


Note: If you navigate to a route that exists in angular, but not in your server, server throws 404. To get around this, you need to configure server to give index.html (holding angular app) when 404 is encountered. 

**app.module.ts:**

This is where you configure the router, and register application routes.

```javascript
import { RouterModule } from '@angular/router';

const routes = [
	{path: '', component: TabsComponent }, // this is the minimum configuration
	{path: 'new-character', component: CreateCharacterCompoent} // don't add slash to path
];

@ngModule({
	...
	imports: [ ..., 
		RouterModule.forRoot(routes) // sets up root routes of the applications, and registers our routes in the router module provided by angular
	]
})
```

**app.component.html**

We need to tell angular where to render these routes.

You have to explicitly provide a hook where angular will put the to be loaded content in. 

```html
<div class="container">
  <app-header></app-header>
  <hr>
  <router-outlet></router-outlet>
</div>
```

By adding router-outlet, we're telling angular that for the root routes (registered with forRoot), load them in the app component (in place of router-outlet).

## Links to Routes

Assume the below is a navbar.

```
<ul>
	<li><a routerLink="/">Star Wars Characters</a></li>
	<li><a routerLink='/new-character">New Character</a></li>
</ul>
```

These paths must match those in app.module.ts

**RouterLinkActive**

```
<ul>
	<li><a routerLink="/" routerLinkActive="activeClassName">Star Wars Characters</a></li>
	<li><a routerLink='/new-character" routerLinkActive="activeClassName">New Character</a></li>
</ul>
```

This directive configures which css class gets applied to the element you added the directive to if the link becomes active. 

In the case above, if you click Star wars Characters, then New Character, both elements will have class 'activeClassName'. This is because '/' is part of the url '/new-character'. We can override this behaviour by adding another property binding:


```
<ul>
	<li><a routerLink="/" routerLinkActive="activeClassName" [routerLinkActiveOptions]="{exact: true}">Star Wars Characters</a></li>
	<li><a routerLink='/new-character" routerLinkActive="activeClassName">New Character</a></li>
</ul>
```

Now, only attach active class if "/" is the full path, not just part of the path.


## Handling Unconfigured Routes


Add a catch all route to our routes.

**app.module.ts:**

```javascript
import { RouterModule } from '@angular/router';

const routes = [
	{path: '', component: TabsComponent }, 
	{path: 'new-character', component: CreateCharacterCompoent},
	{path: '**' , redirectTo: '/ }
	
];

@ngModule({
	...
	imports: [ ..., 
		RouterModule.forRoot(routes) 	]
})
```

Order is important, the catch all route has to be in the end.



## Using Child Routes and Route Parameters


Lets say we want child routes in the tabs component.


**app.module.ts:**

```javascript
const routes = [
	{ path: 'characters', 
	  component: TabsComponent, 
	  children: [ // the children are to be seen relative from 'characters' path
	  		{path: '', redirectTo: 'all', pathMatch: 'full'} // This will ensure that when you go to /characters it goes to /characters/all
	  		{path: ':side', component: ListComponent}
	  ]
	}, 
	{path: 'new-character', component: CreateCharacterCompoent},
	{path: '**' , redirectTo: '/characters' }	
];

```

```{path: '', redirectTo: 'all', pathMatch: 'full'}```
This says that the full path has to be '' to trigger this redirectTo

**tabs.component.html:**

We have to provide another router-outlet.

```html
<ul class="nav">

  <li class="nav-item">
    <a routerLink="/characters/all">All</a>
  </li>

  <li class="nav-item">
    <a routerLink="/characters/dark">Dark</a>
  </li>

  <li class="nav-item">
    <a routerLink="/characters/light">Light</a>
  </li>

</ul>

<router-outlet><router-outlet>
```

:side in app.module.ts will be replaced with all, dark, light.


## Extracting Route Parameters


```
import { ActivatedRoute } from '@angular/router';

activatedRoute : ActivatedRoute;

constructor(activatedRoute : ActivatedRoute) {
	this.activatedRoute = activatedRoute;
}

ngOnInit() { 
	
}
```

**ngOnInit** is executed whenever angular initializes a component. Here we want to initialize our route listener. You can do this in the constructor, but it's good practice to do complex tasks here. 


Now we can use this.activatedRoute.params to react to changes in them. Note: Component won't reload if you switch the URL. Only part of the URL changes, and therefore the parameter changes. Hence, we need to setup a listener in this component to react to these changes. We can do this on the params object, which is actually an **observable**.

**Observables:**

Construct that wrap async events. You can subscribe to observables to react to events. 


```javascript
import { ActivatedRoute } from '@angular/router';
import { StarWarsService } from '...';

starWarsService: StarWarsService;
activatedRoute : ActivatedRoute;

constructor(activatedRoute : ActivatedRoute, swService: StarWarsService) {
	this.activatedRoute = activatedRoute;
	this.starWarsServce = swService; 
}

ngOnInit() { 
	this.activatedRoute.params.subscribe(
		params => {
			this.characters = this.swService.getCharacters(params.side) // see app.module.ts -- we called the param side
		}
	);
}
```

