## Fuzzy A-PIR Verification Suite (`half-tuple.m`)

This repository includes a standalone verification script (`half-tuple.m`) for the **Fuzzy A-PIR** protocol, implemented in the Magma Computational Algebra System. 

All performance benchmarks and algebraic checks can be executed directly in the public **Magma Online Calculator**, ensuring instant and license-free reproducibility.

### Protocol Highlights

- **Curve & Field Engine**: Instantiates the Base-3 homomorphic XOR pipeline over Curve25519 with byte-level packing (η = 8).
- **Half-Tuple Optimization**: Caches the ephemeral ElGamal blinding components (`C1` and decryption mask) once per query vector, allowing the server to evaluate responses by updating only the second ciphertext component (`C2'`). This eliminates redundant scalar multiplications and speeds up the pipeline by **35.5x** compared to full-tuple re-encryption.
- **Extended RS Code [256, 192, 65]₂₅₆** : Constructs non-systematic Reed-Solomon codewords over GF(256) via message scrambling (`S`), encodes a cyclic [255, 192, 64]₂₅₆ core, and appends an overall parity-check symbol (`c256 = ∑ c_i = f(0)`).

### Performance Benchmarks (Magma Online Calculator)

* **Domain Setup (O(1) LUT for N = 6560 points)**: `0.090 sec`
* **Half-Tuple Homomorphic Pipeline (n = 256 bytes)**: `0.060 sec` (~0.23 ms per byte)
* **Blind Syndrome Decoding & Parity Verification (ℵ = 31 errors, avg over 10,000 runs)**: `1,837,839` CPU cycles (~0.55 ms)

### Running the Script

1. Open the [Magma Online Calculator](http://magma.maths.usyd.edu.au/calc/).
2. Copy and paste the contents of `half-tuple.m`.
3. Execute to verify protocol correctness, Half-Tuple throughput, and payload integrity.
