# Programming Assignment 1

## Concept
The general idea behind this assignment is as follows:
- When two ciphertexts encrypted with the same stream cipher key are XORed together, the key gets cancelled out, resulting in the XOR of the two plaintexts.
- In ASCII format, when two such texts are XORed, the chances of two `space`s being in the same place are low.
- An ASCII `space` has the value of 32, which is also the distance between a letter's uppercase and lowercase.
- Therefore, when XORing two plaintexts, the case of the text is flipped where a space meets a letter.
- We can obtain the key by XORing a ciphertext with its corresponding plaintext. By performing frequency analysis on the pairs of XORed ciphers, we can obtain parts of the key.

## Implementation
1. The script first XORs each cipher text with every other cipher text and stores these XORed strings in xored_list.
2. It then divides these XORed strings into “blocks”. Each block contains the characters at the same position in the XORed strings. For example, the first block contains the first characters of all the XORed strings, the second block contains the second characters, and so on. This is done for all positions up to 180 (the length of the longest cipher text).
3. Each block is then scored based on the likelihood of it being English text. If a block’s score is above a certain threshold (7 in this case), the script assumes that the corresponding character in the key is a space character (ASCII value 32, or “20” in hexadecimal). The key is then updated accordingly.

[Source code](./1.py)

## Result

**Key:**
```
[b'f', b'9', b'n', b'\x89', b'\xc9', b'\xdb', b'\xd8', b'\xcb', b'\x98', b't', b'8', b'*', b'\xcd', b'c', 48, b'\x10', b'.', b'\xaf', 48, b'x', b'\xaa', b'\x7f', b'\xed', b'(', b'\xa0', 48, 48, b'\xc9', b'\x8d', b')', b'\xc5', b'\x19', b'i', b'\xb0', 48, 48, b'\x19', b'\xf8', b'\xaa', 48, b'\x1a', b'\x9c', b'm', b'p', b'\x8f', b'\x80', b'\xc0', b'f', b'\xc7', b'c', b'\xfe', b'\xf0', b'\x12', b'1', 48, 48, 48, b'\xe8', b'\x02', b'\xd0', b'[', b'\xa9', b'\x87', 48, b'3', b']', 48, b'\xfc', b'\xec', 48, b'\x9c', b'C', b':', b'k', b'&', b'\x8b', b'`', b'\xbf', b'N', b'\xf0', b'<', b'\x9a', 48, b'\x10', b'\x98', b'\xbb', 48, b'\x9a', b'1', b'a', b'\xed', b'\xc7', 48, b'\x04', 48, 48, 48, b'\xcf', 48, 48, 48, 48, 48, 48, 48, b'n', b'\xdb', b'\xa8', b'\xc2', 48]
```
**Decrypted ciphertext:**
```
The secuet mes_age_is: Whtn using aa~tream cipher, never_use the key more than once
```

Message: `The secret message is: When using stream cipher, never use the key more than once`
