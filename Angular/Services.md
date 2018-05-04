# Services

File Type: name.services.ts

## Creating Services via CLI

```ng g s log```
creates log.services.ts in root folder by default

## Dependency Injection

Let's say we create a service, starWarsService, and we want to use it in ItemComponent.

###Step 1: Pass Service Into Constructor**

```

import { StarWarsService } from '../starwars.service';

export class ItemComponent implements OnInit {
star
	constructor(swService : StarWarsService) {
	}

}
```

They type assignment (swService: StarWarsService) is important. We need to make sure that we tell angular what type of argument we want to get. Why Angular? Because angular is instantiating components. Since angular is instantiating component classes, it is responsible for providing right arugments to the constructor. FI you request it to give you an argument which os of type StarWarsService, it is angular's job to do that. This is called **DEPENDENCY INJECTION**. Angular analyzes dependencies (arguments in constructors) and injects instances of them. 

### Step 2: Save constructor Argument

```
import { StarWarsService } from '../starwars.service';

export class ItemComponent implements OnInit {
	
	swService: StarWarsService
	constructor(swService : StarWarsService) {
		this.swService = swService;
	}

}
```

Now you can access it anywhere in the class via this.swService

### Step 3: Tell Angular how to create StarWarsService Object


**METHOD 1: Create a new Instance of the service in each component**

By default, Angular doesn't know how to create StarWarsService, we have to tell it. To do that, you add a provider array in @Component.

```
import { StarWarsService } from '../starwars.service';

@Component({
   ...
   providers: [StarWarsService] // and any other services you need
});
export class ItemComponent implements OnInit {
	
	swService: StarWarsService
	constructor(swService : StarWarsService) {
		this.swService = swService;
	}

}
```

Note: If you don't specify providers, you'll get an error "No Provider" in console.

Note: If you have another component, and you do the same thing as above, the other component and this ItemComponent WILL NOT be using the same StarWarsService instance - they're disconnected.


**METHOD 2: Let Child Components Share the Same Instance with Parent Component**


Say ItemComponent and ChickenComponent were child components of AppComponent. Then, instead of adding the StarWarsService in the provider array of each of the child components, you would add it to the providers array of the AppComponent.

**METHOD 3: Let ENTIRE App use the SAME instance**

This happens in app.module.ts

```javascript
import {StarWarsService} from ....;

@NgModule({
...
providers: [StarWarsService],
...
})
```


## Injecting Services into Services



Assume we have a service called LogService and we want to inject it into StarwarsService (i.e we want to use it in StarWarsService).


### Step 1:

```
import LogService from '....'

export class StarWarsService {
	
	private logServ;
	
	constructor(logServ : LogService) {
		this.logServ = logServ
	}

}
```

Now you can use this.logServ in the code

### Step 2: 

We have to PROVIDE log service. Services can only receive services as dependencies if you provie them in app.module.ts.

### Step 3:

If you inject Service A into Service B, YOU MUST add @injectable() decorator to Service A.

```
import { Injectable } from '@angular/core'

@injectable()

export class LogService {
...
}
```

