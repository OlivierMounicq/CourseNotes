## Javascript: Getting Started


```console
git clone https://github.com/pluralsight/web-dev-starter.git
```

 ```console
 npm insall
 npm run start
 ```


### 1/ Variables

#### 1.1/ Declare variable and constant

```js
//To declare a variable:
let total = 149.99;

//To declare a constant
const pi = 3.1426
```

#### 1.2/ Former method to declre a variable

The former way to declare a variable is to use __var__. This is deprecated.  
The main difference between __var__ and __let__ is the error management:

When we execute this code, no error is raised !

```js
showMessage(price);
var price =25;
```

But when we execute this code, an explicite error is raised:

```js
showMessage(price);
let price =25;
```

If you open the Chrome console, an error appears:

```log
Uncaught ReferenceError : cannot access 'price' before initialization
```



