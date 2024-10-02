# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.
## Answer
In the mystery function we have a base case of $n <= 1$. In this case the function returns which is constant time.
- $T(1) = O(1)$

In the recurrsive case the function makes 3 recursive calls to $mystery(n/3)$.

There is also a triple nested for loop which is executed.
- In the nested loops we have the outer middle and inner $for$ loops.
- Outer loop runs $n^{2}$ times
- Middle loop runs $n$ times
- Inner loop runs $n^{2}$ times

The total number of run for the loops is $n^{5}$

Now we can See that the the recurrance relation of the mystery funtion is
- $T(n) = 3T\left(\frac{n}{3}\right) + O(n^{5})$

Now we can use the recurence relation to find the asymtotic time complexity.
   
$T(n) = 3T\left(\frac{n}{3}\right) + O(n^{5})$

From this we can determine:
    
$T\left(\frac{n}{3}\right) = 3T\left(\frac{n}{9}\right) + \left(\frac{n}{3}\right)^{5}$

We can now place this into our recurrance relation:

$T(n) = 3\left(3T\left(\frac{n}{9}\right) + \left(\frac{n}{3}\right)^{5}\right) + n^{5}$

This can be simplied:

$T(n) = 9T\left(\frac{n}{9}\right) + \left(\frac{n^{5}}{3^4}\right) + n^{5}$

This step can be repeated for the next recursive call:

$T\left(\frac{n}{9}\right) = 3T\left(\frac{n}{27}\right) + \left(\frac{n}{9}\right)^{5}$

Place it back into out recurrence relation:

$T(n) = 9\left(3T\left(\frac{n}{27}\right) + \left(\frac{n}{9}\right)^{5}\right) + n^{5}$

We can again simplify this expression:

$T(n) = 27T\left(\frac{n}{27}\right) + \frac{n^{5}}{9^{4}} + \frac{n^{5}}{3^{4}} + n^{5}$

We can see a pattern where the recursive portion of the recurence relation increases by a factor of 3
and the non-recursive portion decreases We can see by adding the decreasing portion we are using a geometric series.

So, now we can find the amount of times the recursion will occur until we reach out base case.

$\frac{n}{3^i} = 1$

This gives us:

$i = \log_{3}(n)$

From here we can substitue it into our expression:

$T(n) = 3^{\log_{3}(n)}T\left(\frac{n}{3^{\log_{3}(n)}}\right) + \sum_{i=0}^{\log_{3}(n)}\left(\frac{n^{5}}{3^{4i}}\right)$

Which leads us to:

$T(n) = n + n^{5} \cdot \sum_{i=0}^{\log_{3}(n)}\left(\frac{1}{3^{4}}\right)^{i}$

Now we can take the geometric series from the non-recursive part and find the sum using the geometric series formula:

$\sum_{i=0}^{n}a^{i} = \frac{a^{n+1} - 1}{a - 1}$

For our case:

$n = log_{3}(n)$

$a = \frac{1}{3^{4}}$

Now we have:

$\frac{ \left(\frac{1} {3^{4}}\right)^{\log_{3}(n) + 1} - 1}{ \frac{1} {3^{4}} -1}$

If we simplify the exponent in the numerator and simplfy the denomenator:

$\frac{\frac{n^{4}}{81} - 1}{-\frac{80}{81}}$

Now we factor back in our coeffiecient $n^{5}$

$\frac{\frac{n}{81} - n^{5}}{\frac{80}{81}}$

With this we now have 

$T(n) = n + \frac{\frac{n}{81} -n^{5}}{-\frac{80}{81}}$

With this we can see that as $n$ grows to infinity $n^{5}$ is the dominant term 
Giveing us the asymptotic complexity of $T(n) \in O(n^{5})$

I recalled much of this problem from having previously worked on it. I remember spending a fair amount of time on it. There were still a few sections I stumbled with. Analyzing the mystery function came pretty easily. I knew I had to find the pattern and use the geometric series to solve the recurrence relation. The area that gave me a lot a trouble was the the recursive section, finding and placing the proper value in correct set of parentheses. I think the way I wrote my answer out this time is much more clear. I did take a look at my previous repository. Mostly to check work and find the formula for the geometric series.  

https://github.com/COSC3020/recurrence-analysis-swilso59-1


“I certify that I have listed all sources used to complete this exercise, including the use
of any Large Language Models. All of the work is my own, except where stated
otherwise. I am aware that plagiarism carries severe penalties and that if plagiarism is
suspected, charges may be filed against me without prior notice.”






