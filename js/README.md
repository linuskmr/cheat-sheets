# Javascript / Typescript

## Private class attributes and methods

Attribute and function names starting with a `#` are private.

```js
class Person {
    name = "";
    #age = 0;
    constructor(name, age){
      this.name = age;
      this.#name = age;
    }
    
    set #age(newAge) {
      age = newAge
    }
}
```

[^8-new-js-features]

## Static class variables ans static blocks

```js
class Person {
  static id = 0
  static {
    // Gets executed when the class gets created
    console.log("Hi")
  }
}
```

[^8-new-js-features]

## Exception with cause

```js
throw new Error('Error message', { cause: errorCause });
```

[^8-new-js-features]


[^8-new-js-features]: https://www.infoworld.com/article/3665748/8-new-javascript-features-to-start-using-today.html
