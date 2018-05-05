# Handling User Input

## Creating the Form

```
<form> 
</form>
```

Notice: We don't add action to the form element. This is because we don't want to submit the form to the server. Instead, we want to handle the form with angular.

## Two Ways of Handling Forms

### Template Driven Approach


**Step 1: Add ngModel to form Elements**

```javascript
<form>
	<input type="text" name="personTitle" ngModel>
</form>
```

Recall: the ngModel directive comes from @angular/forms. Thus, to use it you need to go to app.module.ts and add the following:

```
import { FormsModule } from '@angular/forms'
...
imports=[..., FormsModule]
```
By adding ngModel to a form element, we inform angular that this is a control it should  be aware of.

Notice: We're not using ngModel for two way binding here.

**Step 2: ngSubmit**

.html file: 
```javascript
<form (ngSubmit)="submitMyForm">
</form>
```

.ts file:
```
...
submitMyForm() {
\\ do stuff
}
```


By adding the directive ngSubmit:
1. We listen to form submission event
2. We prevent the default of submitting to server

**Step 3: Local References**

```javascript
<form (ngSubmit)="submitMyForm" #form="ngForm">
</form>
```

When we add #form, we bind the JS object angular created, which represents our form, to the variable "form". We can use that variable now anywhere in the template, but not in the .ts file. To use it in the .ts file, simply add

.html file:
```javascript
<form ngSubmit="submitMyForm(form)" #form="ngForm">
</form>
```

.ts file:
```javascript
onSubmit(form) {
// access form values via form.value
// For example form.value.personName for the value of input element with name personName
}
```

Now assume we want to access the input element

```
 <input type="text" id="name" name="name" class="form-control" ngModel required #nameCtrl="ngModel">
```

Now we can do things like

```
<span *ngIf="nameCtrol.invalid"> Blah </span>
```


#### Form Validation

Add required to input element

```
<input type="text" name="personTitle" ngModel required>
```

Angular has a directive called required that will override the normal html 5 required. Now, if the field is empty, angular marks the form as invalid. 

Also, you can style input elements based on validity because angular adds special css classes to inputs:
1. ng-touched
2. ng-valid
3. ng-dirty

Now in your .css file, you can add special styles to each of these



### Reactive Approach

Create angular form from scratch in typescript file

