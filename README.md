### Reactive forms vs template forms

##Reactive forms - 
  - Most of the form logis is driven by configuration in a component class file 
-more appropriate for complex forms
- exposes some aspects of the form to use as Rxjs obervables
- we have to wire up the "ReactiveFormsModule" to our App module to use them

##Template forms
 - Most of the form logic is driven by config in our component template file 
 -more appropriate for simple forms
 - harder to deal with dynamic forms (adding, removing form elements)
 - we have to wire up  "FormsModule" to our app module to use them
 
 ##to use it 
 Put this two line of codes in app.module
 
 ```
 import {ReactiveFormsModule} from './app.component';
 
 imports :[....,ReactiveFormsModule]
 ```
 
 ## Rest of the things should be done in component where we want to use reactive forms
 
   Import these 
   ```
   import {FormGroup,FormControl} from "@angular/forms";
   
   ```
 
 ## Create instance of FormGroup
 ```
cardForm = new formGroup ({   })
```
## Use form control 
```
cardForm = new formGroup ({  
name = new FormControl(' ')
})

```
## in html template , use FormGroup 

```
<form FormGroup="CardForm">
</form>
```
## use formControlName in input field
```
<form FormGroup="CardForm">
<input formControlName="name"/>
</form>
```

###HTML put some code to check status of form

```
<form [formGroup]="cardForm">
  <input formControlName="name" />
</form>
<div>Form content: {{cardForm.value | json}}

</div>
<div>Form status: {{cardForm.valid}}

</div>
```
