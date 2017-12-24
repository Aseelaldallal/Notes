
## UNIT TESTS FOR REACT APPS BUILT WITH CREATE-REACT-APP

Testing Tools:
- Test Runner: Executes tests and provides a validation library. 
-- Jest: Installed in apps created with create-react-app
- Testing Utilities: Simulates react app (moutns component, allows you to dig into the dom)
-- React Test Utils
-- Enzyme

Install:
 npm install --save enzyme react-test-renderer enzyme-adapter-react-16

Name your test file
component.test.js : .test.js is automatically picked up by create-react-app when we run a special command

The test uses jest by default, and jest gives us a couple of methods:

Example:

```

// Enzyme allows us to render NavigationItem without having to render the entire app
// shallow function: it renders the component with all its content, but the content isn't deeply
// rendered. I.e, NavigationItems has NavigationItem, but NavigationItem is "shallow"

import {configure, shallow} from 'enzyme';
import Adapter from 'enzyme-adapter-react-16';
import NavigationItems from './NavigationItems';
import NavigationItem from './NavigationItem/NavigationItem';
import React from 'react';

configure({adapter: new Adapter()});


describe('<Navigation />', ()=> {
    
    let wrapper;

    beforeEach(()=>{
        wrapper = shallow(<NavigationItems />);
    })

    it('should render two <NavigationItem/> elements if not authenticated', () => {
        expect(wrapper.find(NavigationItem)).toHaveLength(2);
    });

    it('should render three <NavigationItem/> elements if authenticated', () => {
        wrapper.setProps({isAuthenticated: true});
        expect(wrapper.find(NavigationItem)).toHaveLength(3);
    });

});

```

More here: https://facebook.github.io/jest/docs/en/api.html
More here: http://airbnb.io/enzyme/docs/api/
