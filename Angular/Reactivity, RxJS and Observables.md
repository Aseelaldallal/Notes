# Reactivity, RxJS and Observables



## Observables

Observables provide support for passing messages between publishers and subscribers in your application.

Example Observable: activatedRoute.params

Each observable is "subscribable". I.e, by subscribing to it, we get informed whenever something changes in that observable. 

In <observable>.subscribe, we can pass 3 parameters (3 functions):

1. The first function is called whenever the observable gives us a new value. For example, when using activatedRoute.params, and the parameter changes, angular internally pushes the new parameter as a value through the observable that our subscription triggers and so this function gets executed
2. Function to fetch errors --> arg: error
3. Function without arguments --> Execute any code whenever observable completes (i.e, when it will not emit more values in the future. Note this doesn't apply to activatedRoute.params because it never ends)


```javascript

import { Subject } from 'rxjs';

export class StarWarsService {

charactersChanged = new Subject<void>() // public


constructor() {}
```

Subject is just like EventEmitter. You can emit a value and you can subscribe to it. Its just a better practice from an architectural perspective to use Subject instead of angular EventEmitter. 

Subject is a generic type, so we have to define which type of value is this event eventually going to carry. Thus, the void.

StarWarsService:
```onSideChosoen(charInfo) {

	this.charactersChanged.next(); // we're emitting a new event
}

```

Now we need to subscribe to it. This has to be done where you eventually want to react to the event.

A good place is in ngOnInit

ListComponent.ts
```
loadedSide = 'all'
ngOnInit() {
	this.activatedRoute.params.subscribe( 
		params => {
			this.characters - this.swService.getCharacters(params.side);
			this.loadedSide = params.side;
		}
	}
	this.swService.charactersChanged.subscribe(() => {
		this.characters - this.swService.getCharacters(this.loadedSide);
	});
}
```

**UNSUBSCRIBING:**

For your own subjects (not angular observables), you NEED to unsubscribe, otherwise they'll stay in memory.

ListComponent.ts
```javascript
loadedSide = 'all'
subscription: Subscription; // import from rsjx
ngOnInit() {
	this.activatedRoute.params.subscribe( 
		params => {
			this.characters - this.swService.getCharacters(params.side);
			this.loadedSide = params.side;
		}
	}
	this.subscription = this.swService.charactersChanged.subscribe(() => {
		this.characters - this.swService.getCharacters(this.loadedSide);
	});
}
```

Now we need to unsubscribe whenever we don't need charactersChanged anymore. This happens whenever we navigate away from the list component. 

```javascript
import { ..., onDestroy } from '@angular/core';

loadedSide = 'all'
subscription: Subscription; // import from rsjx

ngOnInit() {
	this.activatedRoute.params.subscribe( 
		params => {
			this.characters - this.swService.getCharacters(params.side);
			this.loadedSide = params.side;
		}
	}
	this.subscription = this.swService.charactersChanged.subscribe(() => {
		this.characters - this.swService.getCharacters(this.loadedSide);
	});
}

ngOnDestroy() {
	this.subscription.unsubscribe();
}

```

Angular executes ngOnDestroy() whenever component is about to be destroyed. Here, we unsubscribe. 


