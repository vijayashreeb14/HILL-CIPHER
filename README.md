# HILL CIPHER
HILL CIPHER
EX. NO: 3 AIM:
 

IMPLEMENTATION OF HILL CIPHER
 
## To write a C program to implement the hill cipher substitution techniques.

## DESCRIPTION:

Each letter is represented by a number modulo 26. Often the simple scheme A = 0, B
= 1... Z = 25, is used, but this is not an essential feature of the cipher. To encrypt a message, each block of n letters is  multiplied by an invertible n × n matrix, against modulus 26. To
decrypt the message, each block is multiplied by the inverse of the m trix used for
 
encryption. The matrix used
 
for encryption is the cipher key, and it sho
 
ld be chosen
 
randomly from the set of invertible n × n matrices (modulo 26).


## ALGORITHM:

STEP-1: Read the plain text and key from the user. STEP-2: Split the plain text into groups of length three. STEP-3: Arrange the keyword in a 3*3 matrix.
STEP-4: Multiply the two matrices to obtain the cipher text of length three.
STEP-5: Combine all these groups to get the complete cipher text.

## PROGRAM 
```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#define S 2
int K[S][S] = {{3,3},{2,5}};
int modInv(int a, int m) 
{
  a %= m;
  for (int x = 1; x < m; x++) if ((a * x) % m == 1) return x;
  return -1;
}
int det(int M[S][S]) { return (M[0][0]*M[1][1] - M[0][1]*M[1][0]) % 26; }
void invMat(int M[S][S], int I[S][S])
{
  int d = det(M); if (d < 0) d += 26;
  int di = modInv(d, 26); if (di == -1) exit(0);
  I[0][0] =  M[1][1]*di % 26;
  I[0][1] = -M[0][1]*di % 26;
  I[1][0] = -M[1][0]*di % 26;
  I[1][1] =  M[0][0]*di % 26;
  for (int i = 0; i < S; i++) for (int j = 0; j < S; j++)
    if (I[i][j] < 0) I[i][j] += 26;
}
void mult(int M[S][S], int in[], int out[]) 
{
  for (int i = 0; i < S; i++) 
  {
    out[i] = 0;
    for (int j = 0; j < S; j++) out[i] += M[i][j]*in[j];
    out[i] %= 26;
  }
}
void hill(char *in, char *out, int enc) 
{
  int len = strlen(in), V[S], R[S], KM[S][S];
  if (!enc) invMat(K, KM); else memcpy(KM, K, sizeof(K));
  for (int i = 0; i < len; i += S) 
  {
    for (int j = 0; j < S; j++) V[j] = in[i + j] - 'A';
    mult(KM, V, R);

    for (int j = 0; j < S; j++) out[i + j] = R[j] + 'A';
  }
  out[len] = 0;
}
int main() {
  char msg[] = "vijayashree", enc[100], dec[100];
  hill(msg, enc, 1); printf("Encrypted: %s\n", enc);
  hill(enc, dec, 0); printf("Decrypted: %s\n", dec);
}
```

## OUTPUT

![image](https://github.com/user-attachments/assets/82da1f7c-9473-4b50-b2d4-a666cd16657e)


## RESULT
The program executed successfully.
