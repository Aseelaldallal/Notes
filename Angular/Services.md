## Services

File Type: name.services.ts

### Dependency Injection

Let's say we create a service, starWarsService, and we want to use it in ItemComponent.

####Step 1: Pass Service Into Constructor**

```

import { StarWarsService } from '../starwars.service';

export class ItemComponent implements OnInit {

	constructor(swService : StarWarsService) {
	}

}
```

They type assignment (swService: StarWarsService) is important. We need to make sure that we tell angular what type of argument we want to get. Why Angular? Because angular is instantiating components. Since angular is instantiating component classes, it is responsible for providing right arugments to the constructor. FI you request it to give you an argument which os of type StarWarsService, it is angular's job to do that. This is called **DEPENDENCY INJECTION**. Angular analyzes dependencies (arguments in constructors) and injects instances of them. 

#### Step 2: Save constructor Argument

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

#### Step 3: Tell Angular how to create StarWarsService Object


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




