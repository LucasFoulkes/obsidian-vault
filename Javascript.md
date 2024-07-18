## Objects
```Javascript
let person = {
	firstName:'Jhon',
	lastName: 'Smith',
	age: 50 ,
	cars : {
		car1: 'red'	,
		car2: 'blue',
	}
	fullname : function(){
	return this.firstName + lastName;
	}
}
```

## Constructors
``` Javascript
function Person(first, last, age, eye) {
  this.firstName = first;
  this.lastName = last;
  this.age = age;
  this.eyeColor = eye;
}
```

## Classes
