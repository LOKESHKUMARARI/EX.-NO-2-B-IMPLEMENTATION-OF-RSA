# EX.8-IMPLEMENTATION-OF-RSA

## AIM:
  To write a C program to implement the RSA encryption algorithm.
  
## ALGORITHM:

  STEP-1: Select two co-prime numbers as p and q.
  
  STEP-2: Compute n as the product of p and q.
  
  STEP-3: Compute (p-1)*(q-1) and store it in z.
  
  STEP-4: Select a random prime number e that is less than that of z.
  
  STEP-5: Compute the private key, d as e * mod-1(z).
  
  STEP-6: The cipher text is computed as messagee *
  
  STEP-7: Decryption is done as cipherdmod n.
  
  
## PROGRAM: 
```
#include <stdio.h>
#include <math.h>

// Function to calculate gcd
int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

// Function to find modular inverse of e under modulo φ(n)
int modInverse(int e, int phi) {
    int d = 1;
    while ((d * e) % phi != 1) {
        d++;
    }
    return d;
}

// Function to perform modular exponentiation
long long modExp(long long base, long long exp, long long mod) {
    long long result = 1;
    base = base % mod;
    while (exp > 0) {
        if (exp % 2 == 1) {
            result = (result * base) % mod;
        }
        exp = exp >> 1;
        base = (base * base) % mod;
    }
    return result;
}

int main() {
    // Message to be encrypted (plaintext in integer form)
    char plaintext[] = "LOKESH";
    long long encrypted[128];
    char decrypted[128];

    // Small primes p and q (normally these would be large primes)
    int p = 61;
    int q = 53;

    // Calculate n and φ(n)
    long long n = p * q;
    long long phi = (p - 1) * (q - 1);

    // Choose e such that 1 < e < φ(n) and gcd(e, φ(n)) = 1
    int e = 17;
    while (gcd(e, phi) != 1) {
        e++;
    }

    // Calculate d (modular inverse of e mod φ(n))
    int d = modInverse(e, phi);

    printf("Public Key: (%d, %lld)\n", e, n);
    printf("Private Key: (%d, %lld)\n", d, n);

    // Encrypt the plaintext
    int i;
    for (i = 0; plaintext[i] != '\0'; i++) {
        encrypted[i] = modExp(plaintext[i], e, n);
    }
    encrypted[i] = -1; // End of encrypted array

    // Print encrypted message
    printf("Encrypted text: ");
    for (i = 0; encrypted[i] != -1; i++) {
        printf("%lld ", encrypted[i]);
    }
    printf("\n");

    // Decrypt the ciphertext
    for (i = 0; encrypted[i] != -1; i++) {
        decrypted[i] = modExp(encrypted[i], d, n);
    }
    decrypted[i] = '\0'; // Null-terminate the string

    printf("Decrypted text: %s\n", decrypted);

    return 0;
}

```

## OUTPUT:

![image](https://github.com/user-attachments/assets/c7641bbe-8be9-4173-9af1-aa84982f880e)




## RESULT:
  Thus the C program to implement RSA encryption technique had been implemented successfully
