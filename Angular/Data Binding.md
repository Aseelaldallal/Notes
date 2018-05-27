# Data Binding

![DataBinding](https://i.imgur.com/YAPcE2k.png "")


## String Interpolation

```
@Component({
  selector: 'app-user',
  template: `
    <p>Hello {{ name }} </p>
    <p>I'm the user component</p>`
})
export class UserComponent {
  name = 'Aseel';
}
```

Three Requirements:
- Whatever is in between {{ }} has to return a string.
- You CANT add Multiline Expressions
- You CAN use ternary expressions
