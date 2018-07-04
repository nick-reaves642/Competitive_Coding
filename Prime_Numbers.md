The concept of prime numbers is a very important concept in math. This article discusses the concept of prime numbers and related properties.

What are prime numbers and composite numbers?

Prime numbers are those numbers that are greater than 1 and have only two factors 1 and itself.

Composite numbers are also numbers that are greater than 1 but they have at least one more divisor other than 1 and itself.

For example, 5 is a prime number because 5 is divisible only by 1 and 5 only. However, 6 is a composite number as 6 is divisible by 1, 2, 3, and 6.

There are various methods to check whether a number is prime.

> **Naive approach**

Traverse all the numbers from 1 to N and count the number of divisors. If the number of divisors is equal to 2 then the given number is prime, else it is not.

```cpp
void checkprime(int N){
        int count = 0;
        for( int i = 1;i <= N;++i )
            if( N % i == 0 )
                count++;
        if(count == 2)
            cout << N << “ is a prime number.” << endl;
        else
            cout << N << “ is not a prime number.” << endl;
    }
```

> **Recommended approach**

If you have two positive numbers N and D, such that N is divisible by D and D is less than the square root of N.

- (N / D) must be greater than the square root of .
- N is also divisible by (N / D). If there is a divisor of N that is less than the square root of N, then there will be a divisor of N that is greater than square root of N. You will have to traverse till the square root of N.

> **Note:** You are generating all the divisors of N and if the count of divisors is greater than 2, then the number is composite.

For example, if N=50, sqrt(N)=7 (floor value). You will iterate from 1 to 7 and count the number of divisors of N. The divisors of N are 1, 50; 2, 25; 5,10. You have 6 divisors of 50, and therefore, it is not prime.

```cpp
bool checkprime(int N){
    for(int i=2 ; i<=int(sqrt(N)) ; i++)
        if (N % i == 0)
            return true;
    return false;
}
```
_Time Complexity= O(sqrt(N))_
