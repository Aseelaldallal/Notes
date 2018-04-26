## Debugging and Using 3rd Party Libraries


## Adding CSS Packages:

npm install bootstrap --save

Go to node modules, and find the path of bootstrap's css file.

**angular-cli.json** : 

```
"styles": [
	"../node_modules/bootstrap/dist/css/bootstrap.min.css"
	"styles.css"
]
```

You need to stop ng serve because you changed the configuration.


## Adding JavaScript Libraries:

**Example 1:**

Via angular-cli.json, in the scripts array

**Example 2:**

npm install --save lodash

Issue: We're using typescript. Most packages are in JavaScript.

```typescript
import 'lodash';

export class AppComponent {
  number = 0;
  onIncrease() {
    this.number = _.random(1,10);
  }
}
```

Error: TypeScript can't find "_" because it isn't a variable we defined. We know we have access to it via lodash library, but TypeScript doesn't. 

Thus add

```
declare var _: any; fine
```

This is telling TypeScript that we know it exists.

This works, but many JavaScript packages have *type definition files* you can use. These are translations from Javascript to TypeScript.

```
npm install --save @types/lodash
```

Now,

```javascript 
import { random } from 'lodash';
...
this.number = random(1, 10);
```




