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
 
 

