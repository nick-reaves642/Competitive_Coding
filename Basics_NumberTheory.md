# **Number Theory**
## _Modular Arithmetic_

- [ ] (a + b) \% c = (a \% c + b \% c) \% c
- [ ] (a * b) \% c = ((a \% c) * (b \% c)) \% c
- [ ] (a - b) \% c = ((a \% c) - (b \% c) + c) \% c
- [ ] (a / b) \% c = ((a \% c) * (b<sup>-1</sup> \% c)) \% c

###### When are these properties used?
Assume that a = 10^18, b = 10^18, and c = 10^9 + 7. You have to find (a * b) \% c.
When you multiply a with b, the answer is 10^36, which does not conform with the standard integer data types. Therefore, to avoid this we used the properties.

> **Note:** b<sup>-1</sup> is known as multiplicative modulo inverse of b and c.

## Multiplicative Modulo Inverse

What is a multiplicative inverse? If A . B =1, you are required to find B such that it satisfies the equation. The solution is simple. The value of B is A<sup>-1</sup>. Here, B is the multiplicative inverse of A.

What is modular multiplicative inverse? If you have two numbers A and M, you are required to find B such it that satisfies the following equation:

(A . B) \% M =1

Here B is the modular multiplicative inverse of A under modulo M.

Formally, if you have two integers A and M, B is said to be modular multiplicative inverse of A under modulo M if it satisfies the following equation:

A . B = 1 (mod M), where B is in the range [1,M-1]

This equation is a formal representation of the equation discussed earlier.

Why is B in the range [1,M-1]?

(A * B) \% M = (A \% M * B \% M) \% M

Since we have B%M, the inverse must be in the range [0,M-1]. However, since 0 is invalid, the inverse must be in the range [1,M-1].

> **Naive Approach**

```cpp
int modInverse(int A,int M)
{
    A=A%M;
    for(int B=1;B<M;B++)
      if((A*B)%M)==1)
          return B;
}
```
_Time Complexity: O(M)_



> **Recommended approach**

Use this only if ```a``` and ```m``` are co-prime .i.e. their HCF is 1 (in most cases they are).

```cpp
void modInverse(int a, int m)
{
    int x, y;
    int g = gcdExtended(a, m, &x, &y);
    if (g != 1)
        cout << "Inverse doesn't exist";
    else
    {
        // m is added to handle negative x
        int res = (x%m + m) % m;
        cout << "Modular multiplicative inverse is " << res;
    }
}
```

```cpp
int gcdExtended(int a, int b, int *x, int *y)
{
    // Base Case
    if (a == 0)
    {
        *x = 0, *y = 1;
        return b;
    }
 
    int x1, y1; // To store results of recursive call
    int gcd = gcdExtended(b%a, a, &x1, &y1);
 
    // Update x and y using results of recursive
    // call
    *x = y1 - (b/a) * x1;
    *y = x1;
 
    return gcd;
}
```

> **EXPECTED OUTPUTS:** 
```
Inverse does not exist
```
   
   OR
   
   
   
```
Modular multiplicative inverse is [res]
```
_Time Complexity: O(log(max(A,M)))_


## _Modular exponentiation_
Exponentiation is a mathematical operation that is expressed as x<sup>n</sup> and computed as x<sup>n</sup>= x * x * x * . . . * x (_n times_)
 
> **Naive Approach**

```cpp
int recursivePower(int x,int n)
{
    if(n==0)
        return 1;
    return x*recursivePower(x,n-1);
}
```
_Time Complexity: O(n)_

OR 


```cpp
int binaryExponentiation(int x,int n)
{
    if(n==0)
        return 1;
    else if(n%2 == 0)        //n is even
        return binaryExponentiation(x*x,n/2);
    else                             //n is odd
        return x*binaryExponentiation(x*x,(n-1)/2);
}
```
_Time Complexity: O(log n)_

However, storing answers that are too large for their respective datatypes is an issue with this method. In some languages the answer will exceed the range of the datatype while in other languages it will timeout due to large number multiplications. In such instances, you must use modulus (%). Instead of finding x<sup>n</sup>, you must find (x<sup>n</sup>)%m.

For example, run the implementation of the method to find 2<sup>10<sup>9</sup></sup>. The O(n) solution will timeout, while the O(log n) solution will run in time but it will produce garbage values.

To fix this you must use the modulo operation i.e. % **_M_** in those lines where a temporary answer is computed.

> **Recommended approach**

> _RECURSIVE METHOD_
```cpp
int modularExponentiation(int x,int n,int M)
{
    if(n==0)
        return 1;
    else if(n%2 == 0)        //n is even
        return modularExponentiation((x*x)%M,n/2,M);
    else                             //n is odd
        return (x*modularExponentiation((x*x)%M,(n-1)/2,M))%M;
}
```
_Time complexity: O(log N)_

_Memory complexity: O(log N) because a function call consumes memory and log N recursive function calls are made_

> _ITERATIVE METHOD_

```cpp
int modularExponentiation(int x,int n,int M)
{
    int result=1;
    while(n>0)
    {
        if(power % 2 ==1)
            result=(result * x)%M;
        x=(x*x)%M;
        n=n/2;
    }
    return result;
}
```
_Time complexity: O(log N)_

_Memory complexity: O(1)_

## Greatest Common Divisor (GCD)

Always use euclidean algo to solve gcd problems.

**YOUTUBE VIDEO**

<a href="http://www.youtube.com/watch?feature=player_embedded&v=AJn843kplDw
" target="_blank"><img src="http://img.youtube.com/vi/AJn843kplDw/0.jpg" 
alt="IMAGE ALT TEXT HERE" width="240" height="180" border="10" /></a>

**Algorithm:**

```cpp
int GCD(int A, int B) {
    if(B==0)
        return A;
    else
        return GCD(B, A % B);
}
```


> **SOURCE**: Hackerearth.com


