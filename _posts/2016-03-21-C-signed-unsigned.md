---
layout: post
title: C Basic about signed unsigned
---

{{ page.title }}
================

<p class="meta">21 March 2016 - Beijing</p>
# C语言类型隐式转换
http://stackoverflow.com/questions/50605/signed-to-unsigned-conversion-in-c-is-it-always-safe
涉及C99 Standard
According to the C99 Standard:

6.3.1.8 Usual arithmetic conversions

If both operands have the same type, then no further conversion is needed.
Otherwise, if both operands have signed integer types or both have unsigned integer types, the operand with the type of lesser integer conversion rank is converted to the type of the operand with greater rank.
Otherwise, if the operand that has unsigned integer type has rank greater or equal to the rank of the type of the other operand, then the operand with signed integer type is converted to the type of the operand with unsigned integer type.
Otherwise, if the type of the operand with signed integer type can represent all of the values of the type of the operand with unsigned integer type, then the operand with unsigned integer type is converted to the type of the operand with signed integer type.
Otherwise, both operands are converted to the unsigned integer type corresponding to the type of the operand with signed integer type.
In your case, we have one unsigned int (u) and signed int (i). Referring to (3) above, since both operands have the same rank, your i will need to be converted to an unsigned integer.

6.3.1.3 Signed and unsigned integers

When a value with integer type is converted to another integer type other than _Bool, if the value can be represented by the new type, it is unchanged.
Otherwise, if the new type is unsigned, the value is converted by repeatedly adding or subtracting one more than the maximum value that can be represented in the new type until the value is in the range of the new type.
Otherwise, the new type is signed and the value cannot be represented in it; either the result is implementation-defined or an implementation-defined signal is raised.
Now we need to refer to (2) above. Your i will be converted to an unsigned value by adding UINT_MAX + 1. So the result will depend on how UINT_MAX is defined on your implementation. It will be large, but it will not overflow, because:

6.2.5 (9)

A computation involving unsigned operands can never overflow, because a result that cannot be represented by the resulting unsigned integer type is reduced modulo the number that is one greater than the largest value that can be represented by the resulting type.


# C语言有/无符号数区别

#include <stdio.h>

int main(void)
{
  unsigned int plus_one = 1;
  int minus_one = -1;

  if(plus_one < minus_one)
    printf("1 < -1");
  else
    printf("boring");

  return 0;
}
http://codepad.org/yPhYCMFO


# -1的表示法
http://stackoverflow.com/questions/809227/is-it-safe-to-use-1-to-set-all-bits-to-true#comment619894_809879
unsigned int flags = -1; is portable.
unsigned int flags = ~0; isn't portable because it relies on a two's-complement representation.
unsigned int flags = 0xffffffff; isn't portable because it assumes 32-bit ints.

you're confusing two operations. ~0 yields an int value with all bits set, of course. 
But assigning an int to an unsigned int does not necessarily result in the unsigned int having the same bit pattern as the signed bit pattern. Only 
with a 2's complement representation is this always the case. On a 1s' complement or sign-magnitude representation, assigning a negative int value 
to an unsigned int results in a different bit pattern. This is because the C++ standard defines signed -> unsigned conversion to be 
the modulo-equal value, not the value with the same bits

[Discuss this post on StackOverflow](http://stackoverflow.com/questions/50605/signed-to-unsigned-conversion-in-c-is-it-always-safe)
