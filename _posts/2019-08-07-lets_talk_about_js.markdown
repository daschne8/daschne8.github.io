---
layout: post
title:      "Lets talk about JS"
date:       2019-08-07 20:51:06 +0000
permalink:  lets_talk_about_js
---


From my current, albeit, limited understanding I've come to the conclusion that JS is like the English of programming languages.  It's a convoluted mishmash of other languages grammer and syntax not always in a sensible order but it's one of the most ubiquitous (being the language of the web browser) and almost every programmer will have at least been around it.

Don't belive me just look at [typescript](https://www.typescriptlang.org/),[coffeescript](https://coffeescript.org/#introduction) and [babel](https://babeljs.io/).  All ways to introduce functionality or clean up JS in a way people feel it should behave.  

Below I will breifly describe 2 things that caused me trouble when first starting JS in the hopes anyone reading can avoid my headaches.

### Scope
if i were to run
```
var alpha = 'a'
if(true){
var alpha = 1
beta = 'b'
}
console.log(alpha) // 1
console.log(beta) // b
```
Alpha would print `b` not `a` and `beta` becomes a global variable even though it's declared inside a function. `var` is not block-scoped so some advice, never use it, use `let` or `const` instead, those declarations are block-scoped and would throw an error(you also shouldn't reuse variable names but i digress). 

### Arrow functions and this
```
class Person {
  constructor(name){
	  this.name = name
      this.greeting = this.greeting.bind(this)
	}
  greeting(){
    return "hello " + this.name
 }
}

let carl = new Person('carl')
console.log(carl.greeting()) // "hello carl"
```
using regular functions in order to get any class variables one must use `bind` however using the arrow function the same code can be simplified to 
`class Person {
  constructor(name){
	  this.name = name
	}
  greeting = () => {
    return "hello " + this.name
 }
}
let carl = new Person('carl')
console.log(carl.greeting()) // "hello carl"
`




