# Spread Syntax & Rest Parameter

## SPREAD SYNTAX

The spread syntax "spreads" out a variable into multiple arguments, based on the context.  Let's talk about what that means.  

Let's say you have an array. Let's say you want to add some stuff to that array.  

```js
const lessArray = [1, 2, 3]

const moarArray = [...lessArray, 4, 5, 6]
```

What does `moarArray` give you in the console?

### Apply

Remember `.apply()`? No? Let's revisit.

```js
function introduceYourself(name, homeTown, favFood) {
  console.log("Hello! My name is " + name + ", I'm from " + homeTown + " and my favorite food is " + favFood + '!');
}
var args = ['Brenna', 'Minneapolis', 'lutefisk'];
introduceYourself.apply(null, args);
// => "Hello! My name is Brenna, I'm from Minneapolis and my favorite food is lutefisk!"
```

This feel weird for a couple different reasons.  
1. Sometimes you just don't want to deal with every argument in a list by index.  
2. Two, sometimes you don't care what `this` is, which is the first argument in the `apply()` method, and nobody likes to write `null` as a placeholder.   

With ES6, we can refactor the above function like so:

```js
const introduceYourself = (name, homeTown, favFood) => {
  console.log(`Hello! My name is ${name}, I'm from ${homeTown} and my favorite food is ${favFood}!`);
}

const args = ['Brenna', 'Minneapolis', 'lutefisk'];

introduceYourself(...args);
```

Note that spread operator can act as the entire set of arguments, or as a subset of arguments. In the above example, I could also have written:

```js
const args = ['Los Angeles', 'Men']
introduceYourself('Cher', ...args)
```

### Your Turn!

Use the spread operator to produce the following output given the provided information:

```js
const upcomingHolidayAdvice = (day, month, holiday, gift, location) => {
  console.log(`Today is ${day}, in the month of ${month}. Pretty soon, it will be ${holiday}. ${gift} are SO 2016. I'd suggest going to ${location}.`)
}

const dates = ['Wednesday', 'February']
const stuff = ['flowers', 'Paris']

=> "Today is Wednesday, in the month of February. Pretty soon, it will be Valentine's Day. Flowers are SO 2016. I'd suggest going to Paris."
```

### Making A Copy

Using the spread operator allows us to access all existing elements of a previously referenced array without modifying it. (Hence why it's so useful when updating state in React and Redux).

Let's say you have the following arrays:  

```js
const  days = ['Monday', 'Tuesday', 'Wednesday']
const moarDays = [...days]
```

What happens to `days` and `moarDays` when you run:  

* `moarDays.push('Thursday')`  

* `moarDays.concat(['Friday, Saturday'])`  

* `[...moarDays, 'Thursday', 'Friday', 'Saturday']`  

*Based on the above examples, what is a conclusion we can draw from using the Spread operator?*  

### Refactoring ".push()"

Previously, using only `push()` we'd combine two arrays like this:  

```js
var things = ['pineapple', 'apple', 'pen']
var colors = ['orange', 'yellow', 'purple']

Array.prototype.push.apply(things, colors);
```

Try refactoring the above code to eliminate the `Array.prototype` syntax.

## REST PARAMETER

Rest arguments COLLAPSE all remaining arguments of a function into a single array.

Before ES6, in order to grab a bunch of arguments and do something with them you'd have to do something like this:  

```js
function stringStuffTogether() {
  console.log(arguments)
  return Array.prototype.slice.call(arguments).join(' ');
}

stringStuffTogether('What', 'the', 'fudge', 'are', 'we', 'doing', '?')
// => 'What the fudge are we doing?'  
```  

Hmm..that seems weird. Why can't we just write `return arguments.join(' ')`?  

First of all, what is `arguments`?  

What does `'.join()'` need to manipulate?  

Using ES6, pop in Rest Parameters to simplify our lives.

```js
function stringStuffTogether(...whateverTheArgsAre) {
  return whateverTheArgsAre.join(' ');
}

stringStuffTogether('this', 'is', 'so', 'much', 'cleaner', 'WOOT!!!')
```

In review, what's really the difference here? It seems like both of them have three dots and make an array of things into an array of things.  [This blog post](https://rainsoft.io/how-three-dots-changed-javascript/) (also listed next to other cool resources below) said it best:  

> The REST OPERATOR is used to get the arguments list passed to a function. The SPREAD OPERATOR is used for array construction and destructuring.


### Resources  
* [Spread And Butter In Depth](https://ponyfoo.com/articles/es6-spread-and-butter-in-depth) ... confession. I stole the lesson name from this blog post. And maybe some of the material. Aka thanks Pony Foo.  
* [Spread Syntax Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)  
* [How Three Dots Changed JavaScript](https://rainsoft.io/how-three-dots-changed-javascript/)  
