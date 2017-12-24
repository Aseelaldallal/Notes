
## LAZY LOADING

**Purpose**: Only load components when you need them.

1. In hoc folder, create asyncComponent folder and asyncComponent.js file.
2. Add the following code

```
import React, {Component} from 'react';

// Takes a function as input then executes it
const asyncComponent = (importComponent) => {

  return class extends Component {
  
    state = { component: null }
    
    componentDidMount() {
      importComponent()
        .then(cmp=> {
          this.setState({component: cmp.default});
         });
    }
    
    render() {
        const C = this.state.component;
        return C? <C {...this.props} /> : null;
    }

  }

}

export default asyncComponent;
```

3. In App.js (or wherever you're loading the component via <Route ..), import asyncComponent

4. Lets assume the component you want to load lazily is called Checkout. Add the following code

```
const asyncCheckout = asyncComponent(()=> {
  return import('[PATH TO COMPONENT YOU WANT TO LOAD LAZILY]');
});
```
