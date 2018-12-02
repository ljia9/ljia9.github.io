---
layout: post
title:  "Continued fractions for regular ratios"
date:   2016-08-11 09:31:00
categories: [math, python]
---
Just a quick follow up to my previous posts regarding continued fractions.

So in my previous posts I focused on talking about continued fractions for square roots because they are really interesting, but it should be noted that you can derive continued fractions for regular rational numbers too. That means that numbers like 2/5 or 41/13 can be represented as a continued fraction - just they won't be infinite like in the case of irrational numbers.

To find the continued fraction presentation of a ratio, you can keep reducing the fraction to lowest terms and then invert the lowest fraction term by dividing it by 1 over the fraction. You can keep doing this until you have a whole fraction in the inner most nested term, which means that no matter how much you try to invert it, you cannot continue the process of finding lower terms.

Interestingly, this process has a strong connection to the Euclidean algorithm for finding greatest common divisors where the multipliers to the factors in each iteration describe the integer that is included in the fraction. This makes for a very nice python program for finding the continued fraction form of ratios since the Euclidean algorithms is such a nice programming exercise.

```python
def continued_frac_form(a, b):
    """ find shorthand version of continued fraction from using euclidean algorithm """
    form = []
    if b < a:
        a, b = b, a
    else: 
        form.append(0)
    while a != 0:
        form.append(b / a)
        remainder = b % a
        b = a
        a = remainder

   # if form[len(form)-1] != 1:
   #     form[len(form)-1] = form[len(form)-1]-1
   #     form.append(1)
    return form
```

Note that this function returns the shorthand representation for continued fractions. We know that the numerator for each inner fraction is 1, so these integers in the list represent what numbers are added to the next nested fraction.

We can even go from continued fraction representation back to ratio form by simply reversing our original process. We read the contiued fraction from right to left and multiply the next left term with the denomenator and add the current numerator to find our new numerator.

```python
def continued_to_ratio(cont_frac):
    numer = 1
    denom = cont_frac[len(cont_frac)-1]
    b = 1
    for i in range(len(cont_frac)-2, -1, -1):
        a = numer
        numer = denom * cont_frac[i] + numer
        if b == 1:
            b = 2
        else:
            denom = a

    return [numer+cont_frac[len(cont_frac)-1], denom]
```
