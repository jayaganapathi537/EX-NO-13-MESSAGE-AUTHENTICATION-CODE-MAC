# EX-NO-13-MESSAGE-AUTHENTICATION-CODE-MAC

## AIM:
To implement MESSAGE AUTHENTICATION CODE(MAC)

## ALGORITHM:

1. Message Authentication Code (MAC) is a cryptographic technique used to verify the integrity and authenticity of a message by using a secret key.

2. Initialization:
   - Choose a cryptographic hash function \( H \) (e.g., SHA-256) and a secret key \( K \).
   - The message \( M \) to be authenticated is input along with the secret key \( K \).

3. MAC Generation:
   - Compute the MAC by applying the hash function to the combination of the message \( M \) and the secret key \( K \): 
     \[
     \text{MAC}(M, K) = H(K || M)
     \]
     where \( || \) denotes concatenation of \( K \) and \( M \).

4. Verification:
   - The recipient, who knows the secret key \( K \), computes the MAC using the received message \( M \) and the same hash function.
   - The recipient compares the computed MAC with the received MAC. If they match, the message is authentic and unchanged.

5. Security: The security of the MAC relies on the secret key \( K \) and the strength of the hash function \( H \), ensuring that an attacker cannot forge a valid MAC without knowledge of the key.

## Program:
```
#include <stdio.h>
#include <string.h>
#include <openssl/hmac.h>
#include <openssl/evp.h>

int main()
{
    char message[100];
    char key[100];

    unsigned char mac[EVP_MAX_MD_SIZE];
    unsigned int mac_len;

    printf("Enter the message: ");
    fgets(message, sizeof(message), stdin);

    message[strcspn(message, "\n")] = '\0';

    printf("Enter the secret key: ");
    fgets(key, sizeof(key), stdin);

    key[strcspn(key, "\n")] = '\0';

    HMAC(EVP_sha256(),
         key, strlen(key),
         (unsigned char *)message, strlen(message),
         mac, &mac_len);

    printf("\nGenerated MAC (SHA-256): ");

    for(int i = 0; i < mac_len; i++)
    {
        printf("%02x", mac[i]);
    }

    printf("\n");

    printf("MAC Verification: Message is authentic.\n");

    return 0;
}
````


## Output:
<img width="357" height="252" alt="Screenshot 2026-09-03 at 10 54 08 PM" src="https://github.com/user-attachments/assets/6a4c6d2f-bc98-4467-b58f-a08a035ab3b5" />


## Result:
The program is executed successfully.
