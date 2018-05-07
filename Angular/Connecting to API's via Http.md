# Connecting to APIs via HTTP


## Injecting the Angular HTTP Service


Do it within the service you manage the data

**StarWarsService.ts:**

```javascript

import { Http } from '@angular/http';

export class StarWarsService {

	http: HTTP;
	
	constructor(..., http: Http) {
		this.http = http;
	}
	
	fetchCharacters() {
	}
	
}
```

Angular ships with its own http service that we can use. We can inject it. This http service can be used to send get/post requests.

For this http request to work, we need to add HttpModule

**app.module.ts**

```javascript

import { HttpModule } from '@angular/http';

@NgModule({

	import: [
		...,
		HttpModule
	]
})
```

If you inject http into a service, you need to add @Injectable to the service.

Note: You don't need to add HttpModule to providers. Just as with the router, the import HttpModule already takes care of it. 


## Sending a GET Request



**StarWarsService.ts:**

```javascript

import { Http } from '@angular/http';

export class StarWarsService {

	http: HTTP;
	
	constructor(..., http: Http) {
		this.http: Http;
	}
	
	fetchCharacters() {
		//this.http.get(<insert url>, {optional : headers})
		//this.http.post(<insert url>, <data to send>)
		
	}
	
}
```

``` this.http.get(<url>) ``` is NOT actually sending the request. This code simply sets up the get request but doesn't send it. Angular uses observables to manage this request, and the response we get back. As long as no one subscribes to this observable, angular is not going to send the request. This request will only be sent when we add subscribe. 

```javascript
	fetchCharacters() {
		this.http.get( url).subscribe( (response: Response) => {
			console.log(response); 
		});
	}
```

What if we want to transform the data we get back?

**StarWarsService.ts:**

```javascript

import { Http } from '@angular/http';
import 'rxjs/add/operator/map'; // unlocks map operator
export class StarWarsService {

	http: HTTP;
	
	constructor(..., http: Http) {
		this.http: Http;
	}
	
	fetchCharacters() {
		this.http.get(url)
			.map((response: Response) => {
				return response.json(); // extract the data and transform it from json to a js object
			}) 
			.subscribe( data => { // no longer a response
				console.log(data); 
			}); 
	}
```

So the map is the in between step. 


## Sending a POST Request

```javascriopt
	.	// Inside a method/ place where you want to send the request
	.	const myData = {description: 'Data I want to pass, could be any kind of data/ object'}
	.	this.http.post('https://my-api.com/endpoint', myData)
	.	    .map(
	.	        (response: Response) => {
	.	            // map() is totally optional, you just subscribe() without it!
	.	            return response.json(); // fetch the body of the response - this of course also works for post requests
	.	        }
	.	    )
	.	    .subscribe(
	.	        (transformedData: any) => {
	.	            // Use your response data here
	.	            console.log(transformedData);
	.	        }
	.	    );
```

