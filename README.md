# Autokey Cipher — Python Implementation

A Python implementation of the classical **Autokey Cipher**, one of the most elegant polyalphabetic substitution ciphers in cryptographic history — described by Blaise de Vigenère in 1586.

## Background

The Autokey Cipher belongs to a family of ciphers where the key is derived from the plaintext itself. Its earliest form was described by **Girolamo Cardano**, who used the plaintext as its own keystream — a clever but flawed approach since it required no secret key.

The more secure version, described by **Blaise de Vigenère in 1586**, improved on this by prepending a secret keyword to the plaintext before forming the keystream — making it significantly harder to crack than the Atbash or Trithemius Ciphers, and superior to the standard Vigenère Cipher.

## How It Works

### Encryption

1. Generate the keystream by prepending the keyword to the plaintext
2. Use a **Tabula Recta** — align the keystream letter across the top and the plaintext letter down the left
3. The intersection gives the ciphertext letter

**Example:** Encrypting `"meet me at the corner"` with keyword `king`

| Plaintext  | m | e | e | t | m | e | a | t | t | h | e |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Keystream  | k | i | n | g | m | e | e | t | m | e | a |
| Ciphertext | W | M | R | Z | Y | I | E | M | F | L | E |

### Decryption

1. Start with the keyword as the initial keystream
2. For each letter: find the key letter column in the Tabula Recta, locate the ciphertext letter in that column, read the plaintext letter from the left
3. **Append each recovered plaintext letter to the keystream** — this is what makes it "auto"

**Example:** Decrypting `"QNXEPKMAEGKLAAELDTPDLHN"` with keyword `queen`

> Each decrypted letter extends the keystream, allowing the next letter to be decoded — a self-feeding mechanism.

## Features

- Full **encryption** and **decryption** of alphabetic text
- Keyword-based keystream generation
- Handles uppercase and lowercase input
- Ignores non-alphabetic characters (spaces, punctuation)
- Clean CLI interface

## Tech Stack

- **Language** — Python 3
- No external dependencies — pure standard library

## Project Structure

```
autokey-cipher/
├── autokey.py        # Core encryption & decryption logic
├── tabula_recta.py   # Tabula Recta generation helper
├── main.py           # CLI entry point
└── README.md
```

## Usage

```bash
python main.py
```

**Encrypt:**
```bash
Enter mode (encrypt/decrypt): encrypt
Enter plaintext: meet me at the corner
Enter keyword: king
Ciphertext: WMRZYIEMFLE...
```

**Decrypt:**
```bash
Enter mode (encrypt/decrypt): decrypt
Enter ciphertext: QNXEPKMAEGKLAAELDTPDLHN
Enter keyword: queen
Plaintext: ...
```

## Key Concept: Why Autokey Is Stronger Than Vigenère

| Feature | Vigenère | Autokey |
|---|---|---|
| Keystream length | Repeats (fixed key) | Never repeats (plaintext-fed) |
| Vulnerable to Kasiski? | Yes | No |
| Key dependency | Static keyword | Keyword + plaintext |

The repeating key of the Vigenère Cipher makes it vulnerable to frequency analysis via the **Kasiski examination**. Autokey eliminates this by making the keystream as long as the message itself — never cycling.

## Historical Note

This cipher is often misattributed as the "Vigenère Cipher," but the cipher Vigenère himself considered his masterwork was this Autokey variant. The standard Vigenère Cipher was actually described earlier by Giovan Battista Bellaso in 1553.

## Course

Implemented as part of a cryptography/security study — classical cipher series.

---

> *"A cipher is only as strong as its keystream."*
