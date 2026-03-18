# EX-NO:14-HASH-ALGORITHM
## AIM:
To implement HASH ALGORITHM

## ALGORITHM:

1. Hash Algorithm is used to convert input data (message) into a fixed-size string, typically a hash value, which uniquely represents the original data.

2. Initialization:
   - Choose a hash function \( H \) (e.g., SHA-256, MD5, etc.).
   - The message \( M \) to be hashed is input.

3. Message Preprocessing:
   - Break the message \( M \) into fixed-size blocks. If necessary, pad the message to make it compatible with the block size required by the hash function.
   - For example, in SHA-256, the message is padded to ensure that its length is a multiple of 512 bits.

4. Hash Calculation:
   - Process the message block by block, applying the hash function \( H \) iteratively to produce an intermediate hash value.
   - For SHA-256, each block is processed through a series of logical operations, bitwise manipulations, and modular additions.

5. Output:
   - After all blocks are processed, the final hash value (digest) is produced, which is a fixed-size output (e.g., 256-bit for SHA-256).
   - The resulting hash is unique to the input message, meaning even a small change in the message will result in a completely different hash.

6. Security: The strength of the hash algorithm lies in its collision resistance, ensuring that it is computationally infeasible to find two different messages that produce the same hash value.


## Program:
```c
#include <stdio.h>
#include <string.h>

int main()
{
    char str[100];
    int i, j, len;
    unsigned long hash = 5381; // initial value (like DJB2)

    printf("Enter message: ");
    scanf("%s", str);
    len = strlen(str);

    // Step 1: Basic Hashing
    for(i = 0; i < len; i++)
    {
        hash = ((hash << 5) + hash) + str[i]; // hash * 33 + char
    }
    // Step 2: Extra Mixing
    for(i = 0; i < len; i++)
    {
        hash = hash ^ (str[i] << (i % 8));
    }
    // Step 3: Reduce size
    hash = hash % 1000000;
    printf("Hash Value: %lu\n", hash);

    // Step 4: Simple Verification
    unsigned long verify = 5381;
    for(i = 0; i < len; i++)
    {
        verify = ((verify << 5) + verify) + str[i];
    }
    for(i = 0; i < len; i++)
    {
        verify = verify ^ (str[i] << (i % 8));
    }
    verify = verify % 1000000;

    if(hash == verify)
        printf("Hash Verified (Integrity Maintained)\n");
    else
        printf("Hash Mismatch (Data Changed)\n");

    return 0;
}
```

## Output:
<img width="512" height="276" alt="image" src="https://github.com/user-attachments/assets/8786a265-1ed7-450a-b6ac-0665b0df1c40" />

## Result:
The program is executed successfully.
