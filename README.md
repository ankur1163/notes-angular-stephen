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

###html put some code to check status of form

```diff
<form [formGroup]="cardForm">
  <input formControlName="name" />
</form>
+<div>Form content: {{cardForm.value | json}}

+</div>
+<div>Form status: {{cardForm.valid}}

+</div>
```
##lets add validation that input is "required field"

```diff
cardForm = new FormGroup({
+name: new FormControl("", [Validators.required])
  });
```
## add validation to check minimum length of characters and minimum number
```
 Validators.minLength(3)
```
```
 Validators.min(3)
```
## displaying errors for validations

```
<div> errors around name:{{cardForm.controls.name.errors |json}}</div>
```
## display message if there is error 
```diff
<form [formGroup]="cardForm">
  <input formControlName="name" />
!<div *ngIf="cardForm.controls.name.errors.required">
!value is required
!</div>
</form>
<div>Form content: {{cardForm.value | json}}

</div>
<div>Form status: {{cardForm.valid}}

</div>
<div> errors around name:{{cardForm.controls.name.errors |json}}</div>
```
## validation error - because angular throws null object 
### so when we use above code, and there is error , angular throws {required:true} , so if ### we use ngIf logic (required is true) it works, but when there is no error, angular 
### throws null . Then when ngIf tries to check required is true or false. It returns 
### error. So, we have to use one more ngIf to check whether that object with required 
### key exists or not. If we have 2 divs, it will mess up css styling. So Instead of div, ###we will use <ng-container>
  
