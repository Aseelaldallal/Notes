## Lifecycle Hooks


### ngOnChanges

Called after a bound input property changes (i.e, when properties bound with @Input change)

```javascript
import { ... onChanges, SimpleChanges } from '@angular/core'
export class ServerElementComponent implements OnInit, OnChanges {
	ngOnChanges(changes: SimpleChanges) {
		console.log(changes)
	}
}
```

This is the only hook that receives an argument.

### ngOnInit

Called once the component is initialized (but before it's visible in the DOM)

### ngDoCheck

Called during every change detection run. Note that it runs to check IF something changed that requires it to update template. For example, when an event is fired, it runs to see if the event caused a changed.

Triggers: Event called, promise fulfilled

Don't put powerful code here, it'll cost you in performance

### ngAfterContentInit

Called after content (ng-content) has been projected into view (and initialized). So not the view of the component itself, the view of the parent component, especially the part that will get added to our component via ng-content.

### ngAfterContentChecked

Called every time the projected content has been checked (i.e when change detection checked the content we're projecting into our component)

### ngAfterViewInit

Called after the component's view (anc child views) has been initialized and rendered

### ngAfterViewChecked

Called every time the view (and child views) have been checked. I.e, once we're sure that all the changes that have to be done were displayed in the view, or no changes were detected by angular.

### ngOnDestroy

Called once the component is about to be destroyed

### Notes

Good Practice: If you want to use any of those lifecycle methods, implement the interface.

```javascript
import { ... onChanges } from '@angular/core'
export class ServerElementComponent implements OnInit, OnChanges {
	ngOnChanges(...) {
	}
}
```


