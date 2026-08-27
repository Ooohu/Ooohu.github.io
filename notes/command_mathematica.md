---
layout: page
title: "Mathematica"
permalink: /notes/command_math/
---

## 👹Typing Shortcut
`Crtl-2` add a square root box to select text

`CTRL+6` type superscript

`CTRL+/` type fraction.


## 👹General
Drop a nested list:
`Drop[List,{i},{j}]`
means, modify List, remove ith element in first layer, then drop jth element of each element in the second layer.

Use [Part](https://reference.wolfram.com/language/ref/Part.html) to filter your list.

## 👹Special Characters Usage
See [Functional Operators](https://reference.wolfram.com/language/tutorial/FunctionalOperations.html#17469)

## Percentage %
It refers to the result of the previous calculations

```
In: 1
Out: 1
In: %+1
Out: 2
```

## Hash \#
\# is a place holder.
```
#	the first variable in a pure function
#n	the n th variable in a pure function
#	the sequence of all variables in a pure function
#n	the sequence of variables starting with the n th one
```

## Map /@
See [map](https://reference.wolfram.com/language/ref/Map.html)

```
Map[f, {a, b, c, d, e}]    Apply function f to elements
f /@ {a, b, c, d, e}        Same, in short input forms.
```

## Function \&
See [Function](https://reference.wolfram.com/language/ref/Function.html)

```
Function[u, 3 + u][x]    calculate 3+u, with u=x
(3 + #) &[x]    Same, in short input forms.
(#1^2 + #2^4) &[x, y]    Can take inputs from an order pair.
```

## Part [[]]
See [part](https://reference.wolfram.com/language/ref/Part.html)
```
Part[{a, b, c, d, e, f}, -2]    Return the last two argument
{a, b, c, d, e, f}[[-2]]    Same. but in short inputs form.
Table[[All; 2 ;; 50]]    Show elements from 2-50
Table[[All, 12]]    Show every 12th element of each vector, 1st layer of the table.
Table[[All, 16 ;;17]]    Show every 16th - 17th elements as a list of each vector.
Table[[All, 16 ;;]]    Show every 16th - last elements as a list of each vector.
Table[[ ;; ;; n]] Get every nth elements

```

