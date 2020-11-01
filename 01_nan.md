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

Still, thinking of `NaN` as "nonsense as a number" allows to instantly eliminate confusion (and reduce bugs) when dealing with legacy code. Even in modern code, `Object.is()` has not yet universally replaced the use of the strict equality operator and who knows whether it will ever fully replace it. `===` is a whole lot easier to type than `Object.is()` and if you just shift your mental model a little (i.e. start thinking of `NaN` as "nonsense as a number"), you might not ever need to use `Object.is()` in your code. 

Plus, my mental model helps to remind you that `NaN` is of type number and it makes this fact to seem logical. 
