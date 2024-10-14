# Ex 10 - Diffie-Hellman Key Exchange Algorithm
## Aim
To implement the Diffie-Hellman key exchange algorithm in C to securely generate a shared secret key between two users using public key cryptography.

## Algorithm
### Input two prime numbers p and g:

p: A large prime number that serves as the modulus.

g: A primitive root of p, used as the base.

### Choose private keys for both users:

Each user selects a private key a and b (for User A and User B) randomly.

### Generate public keys:

User A calculates A = g^a % p and sends A to User B.

User B calculates B = g^b % p and sends B to User A.

### Compute the shared secret:

User A computes the shared secret K = B^a % p.

User B computes the shared secret K = A^b % p.

Both users now share the same secret key K.
## Program
```
#include <stdio.h>
#include <math.h>

long long power_mod(long long base, long long exp, long long mod) {
    long long result = 1;
    base = base % mod;
    while (exp > 0) {
        if (exp % 2 == 1)
            result = (result * base) % mod;
        exp = exp >> 1;
        base = (base * base) % mod;
    }
    return result;
}

int main() {
    long long p, g, a, b, A, B, keyA, keyB;
    printf("Ex 10 - Diffie Hellman Key Exchange Algorithm by Preethi M\n");
    printf("Enter a large prime number (p): ");
    scanf("%lld", &p);
    printf("Enter a primitive root of p (g): ");
    scanf("%lld", &g);

    printf("Enter private key for User A: ");
    scanf("%lld", &a);
    A = power_mod(g, a, p);
    printf("Public key of User A: %lld\n", A);

    printf("Enter private key for User B: ");
    scanf("%lld", &b);
    B = power_mod(g, b, p);
    printf("Public key of User B: %lld\n", B);

    keyA = power_mod(B, a, p);  // User A's shared secret key
    keyB = power_mod(A, b, p);  // User B's shared secret key

    printf("Shared secret key for User A: %lld\n", keyA);
    printf("Shared secret key for User B: %lld\n", keyB);

    if (keyA == keyB)
        printf("Key exchange successful! Shared secret: %lld\n", keyA);
    else
        printf("Key exchange failed!\n");

    return 0;
}
```
## Output
![image](https://github.com/user-attachments/assets/128a78ad-7eb8-4676-b97a-4094067be782)

## Result
Thus Diffie-Hellman key exchange algorithm in C to securely generate a shared secret key between two users using public key cryptography has been successfully implemented.
