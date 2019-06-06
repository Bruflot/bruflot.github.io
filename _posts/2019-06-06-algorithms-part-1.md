---
layout: post
title: Advanced Algorithms&#58; part 1
mathjax: true
---
This series will function as an introduction to advanced algorithms. It is 
assumed that you have a basic level of understanding of algorithms and data 
structures, and some familiarity with time and space complexity. Implementation 
details will be kept to a minimum; it is expected that you have enough 
experience to infer the details and come up with the specifics yourself. The 
contents of this series was originally my class notes that I cleaned up and 
decided to publish. 

This article will cover the word-RAM model, van Emde Boas trees, x- and y-fast 
tries, and finally fusion trees.

Traditional sorting algorithms and trees have one thing in common: they operate 
on a comparison-based model. For every step, one integer is compared to another.
By relying on this principle, the best worst-case time complexity of any given 
algorithm is \(O(log(n))\). This is demonstrated in a variety of algorithms, 
such as mergesort and heapsort; similarly, querying and insertion in balanced 
BSTs are \(O(log(n))\).

Comparing one number to another is how humans would go about organizing lists, 
and is precisely the origin of such algorithms. However, that is not how 
computers work—in computers, integers fit into words on which you can perform 
bitwise operations like AND, OR, XOR, and so forth. To better optimize for this, 
the <i>word-RAM model</i> is introduced. 

<b>Word-RAM model</b><br>
In the word-RAM model, we establish a few assumptions:<br>
<ol>
    <li>
        The universe of integers is defined by the word size, $u = 2^w-1$.    
    </li>
    <li>
        Elements of the list are integers that fit into a single word, thus 
        $x \in \{0, \, 2^n-1\}$.
    </li>
    <li>
        Pointers fit into a single word, i.e $w \geq lg(space) \geq lg(n)$.
    </li>
</ol>
Following this, basic operations like comparison, arithmetic, and bitwise can be 
performed in $\Theta(1)$ time. For multiplication, we either have to use two 
words, or assume there is an overflow.

<b>van Emde Boas trees</b><br>
vEB trees offer a query time of $\Theta(lg(w)) = \Theta(lg(lg(u))$ at the 
expense of $\Theta(u)$ space.$^{[1]}$ Occupying the entire universe is of 
course something we never want to do—on a 64-bit machine, it would use $2^{64}$ 
space. It was later found that it could be made $\Theta(n)$ with 
randomization.$^{[2]}$ The change to linear space turned out to be trivial, 
which we will cover later.

show the initial solution, then show the improved one

Lastly, <u>here</u> is an example implementation of fusion trees written in 
Rust. Keep in mind this is my personal implementation and thus may contain bugs 
or mistakes.

<div id="references">
    <b>References</b>
    <ol>
        <li>van Emde Boas, P. (1977). Preserving Order in a Forest in Less Than Loagirthmic Time and Linear Space. <i>FOCS</i>, 75-84.</li>
        <li>Willard, D. E. (1983). Log-Logarithmic Worst-Case Range Queries are Possible in Space Theta(N). <i>Inf. Process. Lett.</i>, 17, 81-84.</li>
    </ol>
</div>