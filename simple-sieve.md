# Sieve of Eratosthenes

This algorithm is used to find all prime numbers upto n, where n cannot be larger than 10^7 roughly.
The algorithm is one of the most efficient ways to find prime numbers upto n.

# Algorithm


``` 
1. Create a list of consecutive integers from 2 to n: (2, 3, 4, …, n).
2. Initially, let p = 2 (the first prime number).
3. Starting from p, count up in increments of p and mark each of these numbers greater than p itself in the list. These numbers will be 2p, 3p, 4p, etc.(note that some of them may have already been marked.)
4. Find the first number greater than p in the list that is not marked. If there was no such number, stop. Otherwise, let p now equal this number (which is the next prime), and repeat from step 3.
```

# Analysis

Time Complexity:	O(NloglogN)
Space Complexity:      O(N)

#  C++ implementaion

```

#include <bits/stdc++.h>
using namespace std;
 
void SOE(int n)
{
    bool prime[n+1];
    memset(prime, true, sizeof(prime));
 
    for (int p=2; p*p<=n; p++)
    {
        if(prime[p] == true)
        {
            for (int i = p*2; i<=n; i += p)
                prime[i] = false;
        }
    }
 javascript:void(0)
    for (int i=2; i<=n; i++)
       if (prime[i])
          cout <<i<< " ";
}
 
int main()
{
    int n = 50;
    cout << "Prime number upto "<< n<<":"<<endl;
    SOE(n);
    return 0;
}


```

Output:
```
Prime number upto 50:
2 3 5 7 11 13 17 19 23 29 31 37 41 43 47
```