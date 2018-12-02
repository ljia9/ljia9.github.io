---
layout: post
title:  "Different Flavors of Fermat's Little Theorem"
date:   2017-04-03 15:31:00
categories: [math, notes]
---
I think when you study math in a formal setting it's easy to lose scope of what the actual point of what you're doing is. So you end up being absorbed in practicing computations or building the tools necessary to accomplish a single goal (like proving a theorem) or simply going through the motions of a class just because you have faith in fact that math is important and blindly studying it will make you smart.

Whenever that becomes the case, it's good to take a step back and reflect on what it is that truly motivates your studies and your foray into this very interesting but also very unique thing that is the mathematical experience. So here is a little lecture that helps remind me of not only the beauty of math but also the whole versitility of math and the fact that there is so much to explore.

I'd like to present 3 different proofs for the same statement with each proof being viewed under a different lens. The statement is the fact that an integer raised to a prime power modulo that prime will always be congruent to that integer. More formally this statement is: 

>a^p ≅ a (mod p) where p is a prime and a is an integer

This statement is called Fermat's Little Theorem (not to be confused with the historically significant result Fermat's Last Theorem), and for now I would like to examine the equivalent statement:

>a^(p-1) ≅ 1 (mod p) where p is a prime and a is an integer s.t. p does not divide a

Now this statement has the very impressive title of a Theorem but really it is an observation on how the integers behave under modular arithmetic. If you were to collect some data as to how numbers act when raised to different powers and modulo different numbers (a simple task given a calculator or better yet a computer and a programming language), you can easily guess a pattern. In fact, the pattern can be guessed with a simple sample like by taking the integers raised to any power modulo 7.

| a (mod 7) |  a  |  a^2  | a^3 | a^4 | a^5 | a^6 | a^7 |
| --------- | --- | :---: | :-: | :-: | :-: | :-: | :-: |
| 0         |  0  |   0   |  0  |  0  |  0  |  0  |  0  |
| 1         |  1  |   1   |  1  |  1  |  1  |  1  |  1  |
| 2         |  2  |   4   |  1  |  2  |  4  |  1  |  2  |
| 3         |  3  |   2   |  6  |  4  |  5  |  1  |  3  |
| 4         |  4  |   2   |  1  |  4  |  2  |  1  |  4  |
| 5         |  5  |   4   |  6  |  2  |  3  |  1  |  5  |
| 6         |  6  |   1   |  6  |  1  |  6  |  1  |  6  |

Notice how the last column is the same as the first column and that the second to last column is always 1 (except when a is 0). In fact, this observation holds whenever you modulo by any prime. However, if you try building a similar table with modulo a composite number the pattern will not hold. Well, this is exactly the criteria for our statement above and exactly the same results and so we have formulated Fermat's Little Theorem just by experiment and observation. We have taken quantitative evidence to guess a law which we theorize that all integers must follow, not just the sample data we have.

But this being math, we aren't quite done yet. We need more than the statement of a law. We need a proof to solidify, through logic, that beyond any doubt our statement is true.

Okay. Let's try then.

Seeing how we based both our statement and our data on modular arithemtic, it would follow that a good approach would be to try to prove this statement using modular arithmetic, and this is a perfectly reasonable approach. It takes some creativity and some effort but it definitely can be done, and in fact the proof is very commonly presented when introducing Fermat's Little Theorem since it practices elementary number theory techniques for a result that is largely used in elementary number theory. I'll sketch the idea for the proof below:

- First, claim that the set S_a = {a, 2a, 3a, ..., (p-1)a (mod p)} is equal to the set S = {1, 2, 3, ..., (p-1)}
- Prove this claim is true by showing S_a cannot have repeated elements. Do this by contradiction on p dividing the difference of the indices of this repeated element when we know 0 cannot be an element in S_a.
- Take the product of all the elements in S_a and set it equal to the product of all the elements in S (mod p).
- See we can cancel a factor of (p-1)! on both sides (this is a safe operation since p is prime and therefore p cannot divide (p-1)!
- What we have left is a^(p-1) ≅ 1 (mod p) and we are done. 

Q.E.D.

This proof follows a very direct line of reasoning that is typical of any proof. We have an idea of the type of objects we are interested in (in this case the residues of mod p) and we make some claims of how they act. Then we simply take our new observations on how the objects act and apply them to a familiar setting (like modular arithmetic) in hopes of arriving at some conclusion. With each step we are careful not to lose generality or make any unjust logical steps, and in doing so we build a rigorous proof. All is well.

Now for the sake of comparison, I would like to provide a proof of Fermat's Little Theorem using an entirely different approach. This proof uses the power of algebra, specifically using a result from group theory, and it comes as a very straightforward application.

While groups are fantastic fundamental objects for studying symmetry and real world objects, they also provide a strong insight into the properties of numbers themselves. In particular, we would like to examine integers modulo a prime under multiplication behave, that is how the familiar group (Z/pZ, x), sometimes written as U(p), behaves.

We recall one of the most useful theorems in group theory Lagrange's Theorem, which is really a statement on how cosets partition a group but it is more useful to think of it in terms of the relationship of the order of subgroups to the order of the original group.

>Given a finite group G and a subgroup H of G, then the order of H must divide the order of G

An immediate corollary to Lagrange's Theorem is that any element of a subgroup H raised to the order(G) power must the identity element e. This is shown by the fact that the order of an element a in H must divide order(G). So we now have the statement:

>a^order(G) = e

This is all we need to prove Fermat's Little Theorem, so let's go ahead.

Pf. Consider the group G = (Z/pZ, x). We know that order(G) will be p-1 just by counting and recalling that 0 is not in this group since it has no inverse. Now take an element a from G, so a is in the set {1, 2, ..., (p-1)}. By applying the corollary above, find that a^(p-1) = the identity of G which is 1. 

Q.E.D.

Wow that was straightforward. And really easy. 

In less than the couple of lines it took to even sketch out the proof using modular arithmetic (let alone outline the whole process for the proof) we have provided a complete proof in the same space. How was this possible exactly? Well the big difference is the tools we used. Instead of building up to our result through several fundamental claims using only the bare operations of arithmetic on integers, we borrowed the more powerful tools of group theory and applied them directly. However, the key difference between this proof and the first one is the methodology used to prove the statement. Rather than collecting data to form a pattern, generalizing this pattern into a formal statement, and using common proof techniques of contradiction and algebraic reduction, we simply applied a previous result to a specific example to arrive at the same result. That is instead of looking at the specific case and zooming out to find the general case, we inherited this great, powerful, general result and zoomed in for a specific case. We took a statement we know to be true about the nature of these abstract objects called groups and got the most out of it by discovering a related but useful statement about the integers themselves.

Now for one final comparison. I'd like to take the same Fermat's Little Theorem and prove it from a combinatorics approach.

Consider the following problem.

>A wheel is made of p spokes where p is prime. So the wheel will look something like the figure below (but pretend the ascii art has 11 spokes instead of 12). How many ways can we paint the spokes given k colors and given that we require any paint job to have at least two different colors? How manys ways can we paint the wheel uniquely, that is if we rotate the wheel, then the paint job must differ from any previous paint job from how it looked originally.

```
           __.-(__)-.__
          (__)  |   (__)
       __/  \   |   /   \__
      (__)   \  |  /    (__)
      J  `-.  \ | /  .-'  L
    .-+.____`-.\|/.-'____.+-.
    `-+'     .-/|\`-.    `+-'
      J_  .-' / | \  `-. _F
     (__)'   /  |  \    (__)
        `.__/   |   \__.'
         (__)   |_  (__)
            `-.(__)-'          
```

For the first question, we can consider each spoke individuially. For each spoke, we can choose one of the k possible colors to paint ththe spoke. So for each of the p number of spokes we have k colors, meaning a total of k^p ways to paint all the spokes. But we require that we use at least 2 colors so we just subtract k possibilities from our total (since there are k^1 uses of single color). This gives a final answer of: `k^p - k ways`

For the second question, we can take our answer to first question and tweek it just a little. So we see that this new condition regarding the unique paint jobs will reduce the total number of ways to paint the wheel; the question really is by how much. We know that there are really p rotations of the wheel (based on the p spokes) that could possibly change the paint job. However, if you try any one of these rotations then you will find that no one of the rotations will give the same painting. Formulated in group terms, no rotation of 2π/p radians will preserve symmetry since there are p elements thus no common divisor to provide a line of symmetry to rotate the wheel.

This fact implies that of the k^p-p total ways we originally had, each way can be mapped to (p-1) unique paint jobs. So we simply need to take away a factor p from the total number of possibilities and then we have our answer: `(k^p - k) / p ways`.

Now for the magic of the proof. We are working in the realm of discrete math, specifically in combinatorics. So the only quantities we are dealing with are whole numbers, not reals, factions, complex numbers, or anything else. There are only an integer quantity number of ways to count things in a problem like this. So no matter the p and k choosen, the result will always an integer; the number `(k^p - k) / p` will have to be an integer and so `p must divide (k^p - k) evenly`.

With a little substituting we can take this statement and turn it into a more familiar statement in number theory.

```python
p divides (k^p - k)
then k^p - k ≅ 0 (mod p)
then k^p ≅ k (mod p)
(now replace the integer k with the integer a)
=> a^p ≅ a (mod p)
```
Behold this is Fermat's Little Theorem as stated in its original form.

Q.E.D.

This proof method is quite different than the two previous ones, but nonetheless it works and is actually quite pretty. Unlike the two more traditional approaches outlined before, this proof is ingrained in a real world problem and applying its solution to the more abstract theory of numbers. The key step is in the fact that the solution must be an integer so this proof relies entirely on the field of math we are operating in. And we weren't so much applying a previous theorem to derive new consquences as we were simply extending the results of typical combinatorics problem to a more general statement of numbers themselves. That leap there is wonderfully creative and a great advertisement for the beauty of discrete math as a whole.

So there they are. 3 different proofs through 3 different proof techniques for the same statement. But the point here is that math really is exploring. It is useful to remember that all we are trying to do is learn about the mysterious language nature expresses herself in and that we can learn about that language through different means. If we like, we can take a more scientific apporach where we make informed guesses based on observation to generalize those observations. Or we can use direct logic and simply apply what we already know to a specific case. Otherwise, we can reduce some larger statement to a familiar and nicely wrapped problem that lets us explore how objects work in our own little playground.

In any case, we are just trying to find out a little more about how nature operates. And what is more, there is great beauty in the methodology used to explore nature. While the result or ultimate law which we uncover may be beautiful and useful and interesting and all sorts of things, the proof method has a beauty of its own. So enjoy as best as you can.

Note: It has to be mentioned that Fermat's Little Theorem is really just a special case of the more general Euler's Theorem which considers relatively prime numbers instead of just primes. It makes for a good challenge to slightly extend these proofs to encompass this more powerful theorem.
