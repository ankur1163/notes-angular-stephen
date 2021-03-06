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
#### so when we use above code, and there is error , angular throws {required:true} , so if ### we use ngIf logic (required is true) it works, but when there is no error, angular 
### throws null . Then when ngIf tries to check required is true or false. It returns 
### error. So, we have to use one more ngIf to check whether that object error is present 
### . If we have 2 divs, it will mess up css styling. So Instead of div, ###we will use 
```
<ng-container *ngIf="cardForm.controls.name.errors">
    <div *ngIf="cardForm.controls.name.errors.required">
      value is required
    </div>
    <div *ngIf="cardForm.controls.name.errors.minlength">
      Value you entered is
      {{cardForm.controls.name.errors.minlength.actualLength}}
      characters long, but it must be at least
      {{cardForm.controls.name.errors.minlength.requiredLength}}
    </div>

  </ng-container>
  ```
  
### add conditional css class 

```
<input 
[ngClass]="{is-danger':control.dirty && control.touched && control.errors }" . />
```
### submit form
<form (ngSubmit) = "onSubmit()"

### disabled button till form is valid
<button [disabled]="cardForm.invalid"

#### Template forms

## first create a model 

- signupstudent.ts
```
export class signupStudent {
    constructor (
        public Fullname: string,
        public email :string,
        public password : string,
        public confirmPassword: string,
    ){

    }
}
```
-Then go inside the component and inside signup-page.component.ts 
```
constructor() { }
  studentSignupInfo = new signupStudent("ank sh","er@gmail.com","houseon","houseon")
```
-then in component's html 

```


<div   class="signupbox" >
    <div   fxLayout="column" fxLayoutAlign="center center">
        
          
        <h1>Sign up here</h1>
            <form class="signupdiv">
         
                <div class="field">
                    <label class="label is-large"> Full Name</label>
                    <div class="control">
                      <input class="form-control input is-primary is-large" type="text"  required 
                      [(ngModel)]="studentSignupInfo.Fullname" 
                      //this is coming from component class 
                      name="name" 
                      //we are giving name to this input field. when it goes to api, it will put "name" :"value"
                      #Fullname="ngModel">
                      //we need to give name to this field and tie up with ngModel which holds all angular classes
                    </div>
                    <div [hidden]="Fullname.valid || Fullname.pristine">
                      This is required
                    </div>
                   
                  </div>

                  <div class="field">
                    <label class="label is-large"> Email</label>
                    <div class="control">
                      <input class="form-control input is-primary is-large" type="text" required 
                      [(ngModel)]="studentSignupInfo.email"
                      name="email"
                      #email="ngModel"
                       >
                    </div>
                    <div [hidden]="email.valid || email.pristine">
                        Email is required
                    </div>
                  </div>

                  <div class="field">
                    <label class="label is-large"> Password</label>
                    <div class="control">
                      <input class="form-control input  is-primary is-large" type="password"
                      required
                      [(ngModel)]="studentSignupInfo.password"
                      name="password"
                      #password= "ngModel"
                      >
                    </div>
                    <div [hidden]="password.valid || password.pristine">
                        Password is required
                    </div>
                  </div>

                  <div class="field">
                    <label class="label is-large"> Confirm  Password</label>
                    <div class="control">
                      <input class="form-control input  is-primary is-large" type="password"
                      required
                      [(ngModel)]="studentSignupInfo.confirmPassword"
                      name="confirmPassword"
                      #confirmPassword="ngModel"
                      >
                    </div>
                    <div [hidden]="confirmPassword.valid || confirmPassword.pristine">
                        Confirm password is required
                    </div>
                  </div>
                  
                  
                 <div class="tentopmargin field is-grouped">
                    <div class="control">
                      <button class="button is-large is-link">Submit</button>
                    </div>
                    <div class="control">
                      <button class="button is-large is-link is-light">Cancel</button>
                    </div>
                  </div>
                
               
              
            </form>
       </div>
</div>
```
