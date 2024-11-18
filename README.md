# EX.-NO-5-IMPLEMENTATION OF RSA
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
#include <stdlib.h>
int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;}
    return a; }
int mod_exp(int base, int exponent, int mod) {
    int result = 1;
    base = base % mod;
    while (exponent > 0) {
        if (exponent % 2 == 1) {
            result = (result * base) % mod;
        }
        exponent = exponent >> 1;
        base = (base * base) % mod;}
    return result;}
int mod_inverse(int e, int phi) {
    int t = 0, newt = 1;
    int r = phi, newr = e;
    while (newr != 0) {
        int quotient = r / newr;
        int temp = t;
        t = newt;
        newt = temp - quotient * newt;
        temp = r;
        r = newr;
        newr = temp - quotient * newr;}
    if (r > 1) {
        printf("e does not have an inverse mod phi\n");
        return -1;}
    if (t < 0) t = t + phi;
    return t;}
int main() {
    int p, q, n, phi, e, d, message;
    printf("Enter two prime numbers p and q: ");
    scanf("%d %d", &p, &q);
    n = p * q;
    phi = (p - 1) * (q - 1);
    for (e = 2; e < phi; e++) {
        if (gcd(e, phi) == 1) {
            break; }}
    printf("Public key (e, n) = (%d, %d)\n", e, n);
    d = mod_inverse(e, phi);
    if (d == -1) {
        return 1; }
    printf("Private key (d, n) = (%d, %d)\n", d, n);
    printf("Enter a message (integer) to encrypt: ");
    scanf("%d", &message);
    int encrypted_message = mod_exp(message, e, n);
    printf("Encrypted message: %d\n", encrypted_message);
    int decrypted_message = mod_exp(encrypted_message, d, n);
    printf("Decrypted message: %d\n", decrypted_message);
    return 0;}
```
## OUTPUT:
![image](https://github.com/user-attachments/assets/9ca3e60d-bbe8-4671-a972-a0e12d24e4be)
## RESULT:
  Thus the C program to implement RSA encryption technique had been implemented successfully
