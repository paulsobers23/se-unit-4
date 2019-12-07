# Unit 4 Lesson 1 Practice Set
## Function Execution Context

1. In the browser, what serves as the global object?
Answer: In the browser the `window` object serves as the global object.

2. In the Node.js environment, what serves as the global object?
Answer: In the Node.js environment `global` serves as the global object. `globalthis` could also be serves because it works on all environment except some old browsers.

3. In the browser environment, what does the following log?
      ```javascript
      a = 10;

      console.log(window.a);
      ```     
Answer: In the browser environment, this code log 10 because `window` serves as a global object that look for the variable `a` and return `a` value.
4. What does the following code log? Why?
      ```javascript
      var b = 100;

      console.log(window.b);
      ```
Answer: In the browser environment, this code log 10 because `window` serves as a global object that look for the variable `b` and return `b` value.

5. What does the following code log? Why?
      ```javascript
      let c = 9;
      const d = 11;

      console.log(window.c);
      console.log(window.d);
      ```
Answer: This code logs `undefined` and `undefined` because only the variables declared with `var` becomes the propeties of the global object. So window object can only grab the values of `c` and `d` if they were declared with `var`.   

6. What does the following code log? Why?
      ```javascript
      function func() {
        var b = 1;
      }

      func();

      console.log(b);
      ```
Answer: This logs a reference error because `b` was declared in a function scope.

7. What does the following code log? Why?
      ```javascript
      function func() {
        b = 1;
      }

      func();

      console.log(b);
      ```
Answer: This logs 1 because `b` was not declared with a key word but initialized so it was but it was added  on the global object as a property so `console.log` was able to log the value of `b` value `1`;

8. What does the following code log? Why?
      ```javascript
      function func() {
        return this;
      }

      let context = func();

      console.log(context);
      ```
Answer: This code logs the window object because ` this` refers to  `window` object in the browser environment. So when we passed the value of the `func` to `context` we just passed the value of `this` to `context`.

9. What will the code below output? Explain the difference, if any, between this output and that of problem 8.
      ```javascript
      const obj = {
        func: function() {
          return this;
        },
      };

      let context = obj.func();

      console.log(context);
      ```
Answer: The code below logged the object that hold a method `func`. `func` is invoked as a method in and its execution context refer to `obj` which contain the property that has a value of a function.

10. What will the following code produce? Why? 
      ```javascript
      var a = 10;
      var b = 10;
      var c = {
        a: -10,
        b: -10,
      };

      function add() {
        return this.a + b;
      }

      c.add = add;

      console.log(add());
      console.log(c.add());
      ```
Answer: The following code produce `20` and `0` .

11. In the code below, use `call` to invoke `add` as a method on `bar` but with `foo` as execution context. What will this return?
      ```javascript
      const foo = {
        a: 1,
        b: 2,
      };

      const bar = {
         a: 'abc',
         b: 'def',
         add: function() {
           return this.a + this.b;
         },
      };
      ```
Answer: The code return 3 because since we invoking `call` on `add.bar` already. Supplying the object `foo` as the context for `call` the propeties `a` and `b` that lives in `foo` will be referred to instead of `bar` `a` and `b` and `add` property that lives within bar will add `1` + `2` returning 3.

12. What does the `Function.prototype.bind()` method return?
Answer: The `bind()` method creates a new function. When executed `this` keyword set to the provided value.

13. What does the following code log to the console?
      ```javascript
      var obj = {
        message: 'JavaScript',
      };

      function foo() {
        console.log(this.message);
      }

      foo.bind(obj);
      ```
Answer: The `bind` method does not invoke the function `foo` instead it returns a new function that is bound permanently to the function context argument.

14. What will the following code produce and why? 
      ```javascript
      const obj1 = {
        a: 2,
        b: 3,
      };

      const obj2 = {
        a: 20,
        b: 30,
      };

      function foo() {
        return this.a + this.b;
      }

      let bar = foo.bind(obj1);
      console.log(bar());

      console.log(foo.call(obj2));
      ```
Answer: The code produce 5 and 50 because on line 15 we declared the variable `bar` and assigned it a value of a function. When the `bind` method was invoked on the function `foo` it created a new function and bind `this` to the object `obj1` and ran `foo` function context on `obj1` property `a` and `b` which has a value of 2 and 3 and added it which return 5 .
On line 18 we use the `call` method on the function `foo` and passed `obj2` propeties as arguments individually and added it together using `foo` function context and return 50.

15. What will the following code log? Why?
      ```javascript
      const obj = {
        a: 'Amazebulous!',
      };
      const otherObj = {
        a: "That's not a real word!",
      };

      function foo() {
        console.log(this.a);
      }

      let bar = foo.bind(obj);

      bar.call(otherObj);
      ```
The code log Amazebulous because on line 12 we use the `bind` method on the object `obj` and permanently bound the context of `foo` and cannot be changed even tho we tried to `call` on `otherObj`.

16. What does this point to in the code below?

      ```javascript
      function whatIsMyContext() {
        return this;
      }
      ```
Answer: We won't know until function execution time. We don't know the context until we run the function.

17. What does this point to in the code below?
      ```javascript
      function whatIsMyContext() {
        return this;
      }

      whatIsMyContext();
      ```
Answer: This points to the `window` object because when we invoke the function on line 5 `this` refer the context to the global object.

18. What does this point to in the code below?
      ```javascript
      const obj = {
        count: 2,
        method: function() {
          return this.count;
        },
      };

      obj.method();
      ```
Answer: We call `method` on the `obj` object and `this` referred to `obj`.

19. What does the following code log? Why?
      ```javascript
      window.a = 1;

      function bar() {
        console.log(this.a);
      }

      const obj = {
        a: 2,
        foo: bar,
      };

      obj.foo();
      ```
Thr following code log 2 because we are calling the `foo` method that lives as a property in the `obj` object that has a value of the function `bar` which context changed `this` from referring to the `window` object and referred it to the `obj` object and logged the `a` property that lives within `obj`.

20. **Bonus:** We expect the following code to log `34000` but instead we are getting `35000`. What is the bug and how can we fix it?
      ```javascript
      const computer = {
        price: 30000,
        shipping: 2000,
        total: function() {
          var tax = 3000;
          function specialDiscount() {
            if (this.price > 20000) {
              return 1000;
            } else {
              return 0;
            }
          }

          return this.price + this.shipping + tax - specialDiscount();
        }
      };

      console.log(computer.total());
      ```

Answer: The following code logged 35000 because when we declared the function `specialDiscount` the `this` in our if statement didn't referred to price which is supposed to be `35000` , which is actually supposed to be `34000` if our statement was true and line 14 would've executed and return `34000`. To fix this we have to lexically bind `this` to the context of our object. In shorter `this` changes its context because of the function declartion on line 6. 
```javascript

  const computer = {
        price: 30000,
        shipping: 2000,
        total: function() {
          var tax = 3000;
          const specialDiscount= () => {
            if (this.price > 20000) {
              return 1000;
            } else {
              return 0;
            }
          }

          return this.price + this.shipping + tax - specialDiscount();
        }
      };

      console.log(computer.total());
      ```