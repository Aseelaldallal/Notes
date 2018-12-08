**Those lifecycle methods are discouraged**

componentWillMount
componentWillUpdate
componentWillRecieveProps

**Use the new ones:**


getDervidedStateFromProps(nextProps, prevState) {
// you should return a new state or prevState (you can do something with props to change state and return new state)
}
//Called before render

getSnapshotBeforeUpdate() {
// gives you snapshot of Dom right before update. Good for saving current scrolling position of user. For example, you save scrolling position, then after update, you set the scrolling position after update
}


**Memo**

Previously you had to have a purecomponent (so container). But now you can turn functional components into "pure" componets by using memo.

Export default React.memo(cockpit)
So cockpit will only be rendered whenever the props it received really change
Props will be compared to the old props on a shallow level (if top level values change, that is checked)
So same as pure component now which previously needs
