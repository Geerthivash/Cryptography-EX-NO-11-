# EX-NO-11-ELLIPTIC-CURVE-CRYPTOGRAPHY-ECC
```
GEERTHIVASH J.D. - 212223060067
```
## Aim:
To Implement ELLIPTIC CURVE CRYPTOGRAPHY(ECC)


## ALGORITHM:

1. Elliptic Curve Cryptography (ECC) is a public-key cryptography technique based on the algebraic structure of elliptic curves over finite fields.

2. Initialization:
   - Select an elliptic curve equation \( y^2 = x^3 + ax + b \) with parameters \( a \) and \( b \), along with a large prime \( p \) (defining the finite field).
   - Choose a base point \( G \) on the curve, which will be used for generating public keys.

3. Key Generation:
   - Each party selects a private key \( d \) (a random integer).
   - Calculate the public key as \( Q = d \times G \) (using elliptic curve point multiplication).

4. Encryption and Decryption:
   - Encryption: The sender uses the recipient’s public key and the base point \( G \) to encode the message.
   - Decryption: The recipient uses their private key to decode the message and retrieve the original plaintext.

5. Security: ECC’s security relies on the Elliptic Curve Discrete Logarithm Problem (ECDLP), making it highly secure with shorter key lengths compared to traditional methods like RSA.

## Program:
```
#include <stdio.h>
typedef struct {
int x;
int y;
} Point;
// Function to calculate modular inverse
int modInverse(int a, int p) {
a = a % p;
for (int x = 1; x < p; x++) {
if ((a * x) % p == 1)
return x;
}
return -1; // no inverse
}
// Function to perform point addition on elliptic curve
Point pointAdd(Point P, Point Q, int a, int p) {
Point R;
int lambda;
if (P.x == Q.x && P.y == Q.y) {
// Point doubling
int num = (3 * P.x * P.x + a) % p;
int den = (2 * P.y) % p;
lambda = (num * modInverse(den, p)) % p;
} else {
// Point addition
int num = (Q.y - P.y + p) % p;
int den = (Q.x - P.x + p) % p;
lambda = (num * modInverse(den, p)) % p;
}
R.x = (lambda * lambda - P.x - Q.x + p + p) % p;
R.y = (lambda * (P.x - R.x) - P.y + p + p) % p;
return R;
}
// Function for scalar multiplication (d * G)
Point scalarMultiply(Point G, int d, int a, int p) {
Point R = G;
for (int i = 1; i < d; i++) {
R = pointAdd(R, G, a, p);
}
return R;
}
int main() {
// Example curve: y^2 = x^3 + ax + b over field p
int a = 2;
int b = 2;
int p = 17; // prime
// Base point G
Point G;
G.x = 5;
G.y = 1;
printf("Elliptic Curve: y^2 = x^3 + %dx + %d (mod %d)\n", a, b, p);
printf("Base point G = (%d, %d)\n", G.x, G.y);
// Private key (randomly chosen)
int d = 7;
printf("\nPrivate Key d = %d\n", d);
// Public key Q = d * G
Point Q = scalarMultiply(G, d, a, p);
printf("Public Key Q = (%d, %d)\n", Q.x, Q.y);
return 0;
}
```


## Output:

<img width="678" height="400" alt="image" src="https://github.com/user-attachments/assets/342a8463-01d4-4664-a59c-4a9a0b721f8b" />

## Result:
The program is executed successfully

