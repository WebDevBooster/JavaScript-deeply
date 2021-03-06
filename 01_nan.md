# An easy way to understand NaN in JavaScript

The `NaN` value in JavaScript is often a cause of confusion or claims that JavaScript is "weird" etc. But once you get to properly *understand* it, you'll realize that there's nothing "weird" about it. 

Here's an easy way to understand it: 

In every tutorial and every book that I've come across, the claim is always: 
> “NaN stands for not a number”

OK, genius, how then do you explain the following: 

```javascript
console.log(typeof(NaN));
number
```

In other words, if you ask JavaScript what is the type of `NaN`, it will clearly tell you: It's the type of number!

So, JavaScript clearly tells you that `NaN` ***is*** a number. And yet, everyone keeps telling you that... 

> “NaN stands for not a number”

And it is precisely that fact that everyone keeps telling you that `NaN` means "not a number"... it is this fact that makes things so confusing and contributes to the **myth** that "JavaScript is weird". 

Here's the only right and proper way to think about `NaN`: 

## NaN in JavaScript stands for "nonsense as a number"!

There you go! If you adjust your mental model to think about `NaN` as **nonsense expressed as a number**, then it becomes immediately obvious and logical why the output of 
```javascript
console.log(NaN == NaN);
```
is `false`.

If you try to calculate 
```javascript
console.log("JavaScript" / 42);
```
the result of that calculation will be nonsense.  
Nonsense expressed as a number i.e. NaN.
Because trying to divide a string by 42 is nonsense. 

But if you try to run `parseInt` on an empty string (empty string is what you get from an empty form field as an example)
```javascript
parseInt("");
```
then you'll also get `NaN` (nonsense expressed as a number) but it will be ***different*** kind of nonsense. 

## Nonsense is unique, unpredictable and random. 

That's why one piece of random nonsense cannot be equal to another piece of random nonsense. And that's the reason you get `false` for 
```javascript
console.log(NaN == NaN);
```
One piece of random nonsense expressed as a number cannot be the same as another piece of random nonsense expressed as a number. 

And because `NaN` expresses nonsense ***as a number*** it is very logical that `NaN` is of type `number`. 

Once you make this little shift in your mental model, everything about `NaN` becomes instanly crystal-clear and very logical. 

There's nothing "weird" or "quirky" about JavaScript once you grow a proper understanding of all the parts that comprise it. 

You could argue that thinking of `NaN` as "nonsense as a number" is just a mnemonic device and it is. After all, since ES2015 we have the `Object.is()` method which checks whether or not two values are the same value. And `Object.is(NaN, NaN)` does return `true` i.e. according to `Object.is()` the value of a `NaN` really does equal the value of any other `NaN` (consistent with what we normally expect with any normal numbers that look identical). 

We can probably all agree that the unexpected output when comparing `NaN` to `NaN` and when comparing `-0` to `0` with a strict equality operator (`===`) are just bugs in JavaScript that have to be kept for historical and backward compatibility reasons. And the newer `Object.is()` method is designed to fix that. 

It can be argued that `Object.is()` is more suitable for comparing two values that can be different. When it comes to `NaN`, we don't really want to compare two values i.e. we don't want to compare the result of our operation to `NaN`. We just want to know whether or not the result of our operation is `NaN`. And to answer that question, we should use the specialist method `isNaN()` or `Number.isNaN()` because that's specifically designed to answer that question. So, it makes more sense to use that. 

## Caution when dealing with `NaN` in arrays!

Because the `indexOf()` method in arrays uses the strict equality operator (`===`) when searching through the array, `_array.indexOf(NaN)` will always return `-1`, even if you do have `NaN` in the array i.e. JavaScript will say that `NaN` isn't there. 

To get around this, use `_array.includes(NaN)` because it returns `true` in case `NaN` is present in the array. 

To find the index/position of `NaN` in a JavaScript array, you can call the `findIndex()` method on that array with `Number.isNaN` as the callback like so:
```javascript
[2, 11, 42, NaN].findIndex(Number.isNaN)
```
