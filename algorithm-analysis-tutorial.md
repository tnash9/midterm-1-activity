# Algorithm Analysis
## Tutorial by Tanner Nash

<br>
We will be using Val's 5 Step Algorithm Analysis plan for nonrecursive functions. The steps are listed below.

### Step 1: Decide on a parameter indicating the algorithm's input size

### Step 2: Identify the algorithm's basic operation

### Step 3: Determine whether the number of times that the basic operation is executed is dependent only on input size

### Step 4: Set up a sum to express the number of times that the basic operation is executed

### Step 5: Using standard formulas and rules for sum manipulation, establish the algorithm's order of growth

<br><br>
For our tutorial, we will be analyzing a simple sorting algorithm step by step. Take a minute to check out the function below.

```javascript
function sort(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < i; j++) {
      if (arr[j] > arr[i]) {
        const temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
      }
    }
  }

  return arr;
}
```

<br>

#### Step 1:

Our algorithm takes in an array, sorts it, and returns the sorted array. It seems obvious that our parameter `n`, which will indicate the algorithm's input size, will be related somehow to our array. 

As you may have already determined, we will say `n = arr.length`. In nearly all algorithms that work with arrays or similar data structures, the size of our input will be the length.

Now that we've determined our input size, we can move on to establishing a basic operation.

<br>

#### Step 2:

In step 2, we need to determine which operation(s) to use as our basic operation. This is the operation that actually does the work of our algorithm, and is generally located in the inner-most loop. 

In looking at our sorting algorithm, we have a couple of options for the basic operation. The main things that are happening are we are comparing two values, and then *potentially* swapping those values. We could use either of these actions as our basic operation, but because the comparison (line 4) happens *every* time our inner loop executes, we'll choose that as our basic operation.

We have now established an input size and a basic operation. At this point, we can move into the more complicated stages of algorithm analysis.

<br>

#### Step 3:

This step involves some deeper thinking than the previous two. We are going to whether the number of times that our basic operation executes is dependent only on the size of our input, or if other factors contribute to how many times we execute our basic operation.

Essentially, what we are doing in step 3 is determining if we can assess our algorithm only once, or if we need to investigate the best, worst, and average cases.

Let's think of some factors that could affect how many times we need to execute our basic operation. The main thing that comes to mind for me is whether we're given an array that's already sorted. For example, would `[1, 2, 3, 4, 5]` require fewer basic operations than `[3, 5, 1, 4, 2]`?

Had our basic operation been swaps rather than comparisons, we would have to evaluate our algorithm for multiple cases, because a sorted array would have zero swaps, while a random array would obviously have some number of swaps. Since we chose comparisons, however, our basic operation is dependent only on the size of our array. Even if the array is already sorted, we will still *compare* our elements every time we reach that line of code.

We have now completed all of the setup for our algorithm analysis and can finally find a sum to express the number of times our basic operation executes.

<br>

#### Step 4:

I hope you're as excited as I am to finally get into the meat of algorithm analysis. We have finally gotten to the point where we can set up our sum, which will allow us to determine our algorithm's order of growth in our final step.

Recall from step 2 that we determined our basic operation to be the comparison on line 4. Keeping this in mind, we now need to figure out an equation to represent how many times this comparison happens when we run our algorithm on an array of length `n`.

A natural place to start is with our outer loop. The loop executes from 0 to n - 1, meaning that it will execute n times. Now, we want to figure out how many times the inner loop––which contains our basic operation––executes. Note that the inner loop executes from 0 to i. What this tells us is that on the first execution of the outer loop, our inner loop executes 1 time. On the second execution of the outer loop, the inner loop executes 2 times, and so on until the outer loop has completed.

We now need to come up with a way to take what we just covered and represent it as a summation. We will execute our summation from i = 1 to n since our outer loop executes n times. All that's left to do in this step is to decide what goes inside the summation. As we determined above, our inner loop executes one additional time for every time our outer loop executes, so our inner loop will look something like this: `(1 + 2 + ... + n)`.

Finally, we compile all of the information we've gathered to create our actual summation. As you may have figured out by now, it is: 
$$\sum_{i=1}^{n} i$$
Now we're finally ready to figure out our algorithm's order of growth!

<br>

#### Step 5:

The final step in algorithm analysis is to determine the order of growth of our algorithm––the whole reason we analyzed it in the first place! We'll use the formulas and rules of sum manipulation to get our final answer, so it may be helpful to have your *Important Summation Formulas* sheet handy.

A quick glance at the sheet should make it apparent that it has exactly what we need. Formula 2 says the following:
$$\sum_{i=1}^{n} i = 1 + 2 + ... + n = \frac{n(n + 1)}{2} = \frac{1}{2}n^2-\frac{1}{2}n$$
This matches up exactly with the sumnation we found in step 4. All that's left now is to take $\frac{1}{2}n^2$, the most simplified form of the sumnation, and use it to determine our order of growth. 

As you may know, when determining the order of growth, we want to ignore all lower order terms, as the term with the highest order is the one that will ultimately determine our asymptotical runtime. This means we can drop $\frac{1}{2}n$, leaving us with $\frac{1}{2}n^2$.

We can also ignore leading constants for similar reasoning. This means we'll drop $\frac{1}{2}$, leaving us with just $n^2$. We've now simplified as far as we can and what we're left with is the order of growth for our algorithm.

This brings us to our final solution and the conclusion of our tutorial! The Big O of our sorting algorithm is $O(n^2)$.

Thank you for reading, I hope you were enlightened by my tutorial and that you were able to learn something!
