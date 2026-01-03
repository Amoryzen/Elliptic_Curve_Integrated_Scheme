# ECIES from Scratch (C Implementation)

A production-ready, pure C implementation of the **Elliptic Curve Integrated Encryption Scheme (ECIES)** built from scratch. This library assumes zero external dependencies, providing custom implementations for all cryptographic primitives including Big Integer arithmetic, Elliptic Curve operations, SHA-256 for Key Derivation, and AES-128-CTR for symmetric encryption.

## Motivation

This project serves as a comprehensive educational resource and a standalone library for understanding and implementing ECIES without relying on heavy external libraries like OpenSSL. It demonstrates the full stack of cryptographic operations required for secure public-key encryption on the **secp256k1** curve.

## Key Features

-   **Zero External Dependencies**: Pure C implementation logic.
-   **Custom BigInt Library**: Handles 256-bit integer arithmetic (`bigint256_t`).
-   **Elliptic Curve Arithmetic**: Efficient point addition, doubling, and scalar multiplication over $y^2 = x^3 + 7$ (secp256k1).
-   **Integrated KDF**: Custom SHA-256 implementation for key derivation.
-   **Symmetric Encryption**: AES-128 in CTR (Counter) mode for secure payload encryption.
-   **Performance Profiling**: Includes a test driver to profile decryption performance.

## Tech Stack

-   **Language**: C (C99 standard or later recommended)
-   **Compiler**: GCC / Clang / MSVC
-   **Architecture**: Optimized for 64-bit systems.

## Project Structure

```bash
.
├── include/        # Header files
│   ├── aes.h       # AES encryption definitions
│   ├── bigint.h    # Big Integer structure and ops
│   ├── ec.h        # Elliptic curve point definitions
│   └── sha256.h    # SHA-256 context and functions
├── src/            # Source implementation
│   ├── aes.c
│   ├── bigint.c
│   ├── ec.c
│   ├── sha256.c
│   └── main.c      # Demo and profiling entry point
├── ecies_test.exe  # Compiled binary (Windows)
└── .gitignore
```

## Installation & Usage

### Prerequisites

-   A C compiler (GCC, Clang, etc.)

### Build Instructions

To compile the project, run the following command from the root directory:

```bash
gcc src/*.c -I include -o ecies_test
```

### Running the Demo

Execute the compiled binary:

```bash
# On Windows
./ecies_test.exe

# On Linux/macOS
./ecies_test
```

### Example Usage (from `main.c`)

The `main.c` file demonstrates a full encryption flow:
1.  **Bob** generates a static public/private key pair.
2.  **Alice** generates an ephemeral key pair.
3.  **Alice** derives a shared secret using ECDH.
4.  **Alice** encrypts a message ("Hello Bob!...") using AES-128-CTR with a derived key.
5.  **Bob** receives the ephemeral public key and ciphertext, derives the same secret, and decrypts the message.

## Testing & Verification

The included `main.c` runs a functional test of the encryption/decryption cycle. It also performs a profiling run, executing the decryption process 10,000 times to verify stability and performance.

## License

This project is open-source and available under the MIT License.
