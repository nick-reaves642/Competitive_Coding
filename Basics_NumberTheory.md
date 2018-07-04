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

    int modInverse(int A,int M)
    {
        A=A%M;
        for(int B=1;B<M;B++)
          if((A*B)%M)==1)
              return B;
    }
_Time Complexity: O(M)_



> **Recommended approach**

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

```
**SOURCE: **Hackerearth.com
```

