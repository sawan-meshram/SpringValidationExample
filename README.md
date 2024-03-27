# SpringValidationExample

This project is used to demonstrate the spring validation on server side.

To apply the validation on server-side, there are fews annotation used on this project, such as 

- **@Valid**
- **@NotBlank**
- **@Size**
- **@Pattern**
- **@AssertTrue**

Also, I have used **`BindingResult`** class to bind the validation with front-end.

To show the validation on front-end, used **Thymeleaf** template.

There are few thymeleaf tag expression to show validation from server-side. such as 

- **`${#fields.errors(var_name)}`**

	This expression is used to give the list of errors for `var_name` thrown at server-side.


- **`${#fields.hasErrors(var_name)}`**

	This expression is used to check if the given `var_name` throws any errors.


#### Add-on Thymeleaf tags

To validate the html form on server-side, there are few points to consider while validating on server-side.

- **th:action="@{/process}"**

	Here, `/process` is URL for requesting the form data to server. The tag is used to perform the action on html form.

- **th:object="${loginData}"**

	Here, `loginData` the object name defined on server-side controller class. The tag is used to receive the server-side response such as its data and validation like errors, etc.

- **`name="userName"`** 

	Used `name` property on `input` html tag. Here, `userName` is variable name of defined entity class. This property is used to pass the input value on server-side.

- **`th:classappend="class_name"`**

	It is used to add or give the css class name on html tag.
	
- **`th:each`**
	
	It is a thymeleaf tag, used to iterate the items.


#### Example

```
<form th:action="@{/process}" method="post" th:object="${loginData}">
	<h1 class="text-center">Login Here</h1>
	<div class="mb-3">
		<label for="exampleInputEmail1" class="form-label">UserName</label> 
		<input 
			type="text" 
			name ="userName" 
			th:value="${loginData.userName}"
			th:classappend="${#fields.hasErrors('userName')}? 'is-invalid': ''"
			class="form-control" 
			id="exampleInputEmail1" 
			aria-describedby="emailHelp" />
			
		<div th:each="e : ${#fields.errors('userName')}" th:text="${e}" class="invalid-feedback"></div>
	</div>
	<button type="submit" class="btn btn-primary">Submit</button>
</form>
```


