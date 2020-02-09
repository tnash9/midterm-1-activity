#<p align="center">Recursion and Iteration<p>
##<p align="center">Guide by Tanner Nash<p>
<br>
<b>
In this guide we will cover some basics of recursion. The main topics covered will be converting between recursive/iterative functions and head vs tail recursion.

<br><br>
#### Iterative vs Recursive Functions
Anything that can be accomplished recursively can also be accomplished iteratively, but each format has unique advantages and disadvantages.

Recursive functions can be hard to reason with when it comes to initially writing them, however once written, they are generally very clean and concise. This generally makes recursive functions shorter and easier to digest than their iterative counterpart.

Though they can be easier to read, recursive functions run the risk of increased time complexity or space issues. Because a recursive function repeatedly calls itself, if you are trying to execute a particularly deep recursion you will run into stack overflow. This is because the return address of your function is pushed onto the call stack each time it's called, and eventually your computer will run out of space to store the stack. (Note: stack overflow can also occur if your function does not reach a base case and executes infinitely.)

There are absolutely cases that lend themselves to recursion, but in practice (at a real job), iterative solutions are typically preferred. As a general rule of thumb, if time complexity is the main concern, an iterative function will probably be your friend. If you're concerned, however, about the length and readability of your function, you should consider a recursive solution.

<br>
#### Iterative $\xleftrightarrow{}$ Recursive
Adapting Val's guidelines for translating recursive functions to iterative, I will lay out a simple, general guide for converting between iterative and recursive functions.
<br>
##### Step 1:
Regardless of the direction you're going, you need to determine your base case. This is pretty easy to spot in recursion, as you just look for the case that *isn't* the recursive case––this will typically be a conditional at the start of your function. If you're converting an iterative function to recursion, you'll have to be a little more observant to find your base case. It will probably have something to do with your loop condition. For example, if your loop looks like `while (x > 0)`, your base case will be `x = 0`.
<br>
##### Step 2:
Once you've found your base case, you'll essentially want to reverse our first step. If you're going from iteration to recursion, it's pretty simple. Take the base case you found in step one, and write a conditional for it at the top of your function. Continuing our example from above, this may look something like `if (n = 0): do base case`.

If you're going in the other direction, you'll take your recursive function's base case and find a way to execute your loop until that condition is met. This may be a while loop, as in the above example, but it could be any kind of iteration (while, for, do while, etc).
<br>
##### Step 3:
Now that we've set up our base case or loop condition, we need to work towards it. Going from iterative to recursive, we will take what is inside our loop and plop it into our recursive function. If we meet our base case, we want to do that, otherwise, we want to perform some kind of action and then recurse. If inside our loop we increment a count variable, `count += x` for example, our recursive function should look something like `return x + f(x - 1)`.

We follow a similar strategy when going from iterative to recursive, but instead of calling our function on our new value (`x - 1`), we want to send our value to the top of our loop. We can accomplish this by mimicking the behavior we applied to our value. What this means is because we passed `x - 1` to our recursive function, we want to make sure that next time our loop executes we have one less than x. This means that in our example we'll want to have `x--` or something similar at the end of our loop.


At this point, we have all the necessary knowledge to switch between iterative and recursive functions. Following these steps for the example we used throughout, our two functions should look something like this:

```javascript
function recursive(x) {
  if (x == 0) {
    return 0;
  }

  return x + recursive(x - 1);
}
```
```javascript
function iterative(x) {
  let count = 0;

  while (x > 0) {
    count += x;
    x--;
  }

  return count;
}
```
<br><br>
#### Head vs Tail Recursion
The last thing we will cover in our guide is head vs tail recursion. We will again be building upon Val's guide on the topic.

Essentially, head vs tail tells us where we recurse. Head recursion says recurse then work, while tail recursion is work then recurse. As a result of this, a major distinction to note is that head recursion tackles the smallest instance and works up, while tail recursion processes the largest instance and breaks off a subset of that instance to recurse on.

Tail recursion is generally better in terms of optimization, as most compilers will convert your function into an iterative solution, which, as we covered above, will likely prove to be a faster algorithm. However, we also want to avoid unnecessary input, using our arguments for *input* only, and not for *state*. If you are passing state information to a tail recursive function, converting to head recursion may alleviate the need for state arguments.

Finally, regardless of whether you are doing head or tail recursion, it is imperative to have a reachable base case. Having met that criteria, then follow the above guide to determine which kind of recursion your algorithm lends itself to.

<br><br>
Thank you for reading! I hope this guide proves useful in your algorithm writing process.