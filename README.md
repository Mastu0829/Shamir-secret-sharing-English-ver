# Shamir-secret-sharing-English-ver
# Shamir's (k, n) Threshold Secret Sharing Scheme

A Python implementation of **Shamir's (k, n) Threshold Secret Sharing Scheme** over a finite field **GF(p)**.

This project demonstrates how a secret can be split into multiple shares, reconstructed from a threshold number of shares, and extended by adding new participants both with and without a trusted dealer.

---

## Features

- Secret sharing using Shamir's Secret Sharing Scheme
- Secret reconstruction using Lagrange interpolation
- Finite field arithmetic over GF(p)
- Addition of new participants without a dealer
- Addition of new participants with a dealer
- Fully documented educational implementation

---

## Background

Shamir's Secret Sharing Scheme divides a secret value **S** into **n shares** such that:

- Any **k or more** shares can reconstruct the secret.
- Any **k − 1 or fewer** shares cannot reconstruct the secret.

A random polynomial of degree **k − 1** is generated:

\[
f(x)=S+a_1x+a_2x^2+\cdots+a_{k-1}x^{k-1}
\]

where:

- **S** is the secret.
- The remaining coefficients are chosen randomly.

Since the secret is stored in the constant term,

\[
f(0)=S
\]

the secret can be recovered by reconstructing the polynomial and evaluating it at \(x=0\).

---

## Finite Field

All computations are performed in the finite field:

\[
GF(p)
\]

where **p** is a prime number.

In this implementation:

```python
PRIME = 101
```

is used for simplicity and educational purposes.

Since the x-coordinates are assumed to be public, each participant only needs to store \(y_i\). Therefore, the share size is approximately:

\[
\log_2(p)
\]

bits.

---

## Secret Sharing Workflow

1. Define a secret \(S\).
2. Generate a random polynomial.
3. Create shares for participants.
4. Collect at least \(k\) shares.
5. Reconstruct the secret using Lagrange interpolation.

---

## Example Parameters

```python
secret = 1
n = 7
k = 3
```

Meaning:

- 7 participants receive shares.
- Any 3 or more shares can reconstruct the secret.
- 2 or fewer shares cannot reconstruct the secret.

---

## Adding New Participants Without a Dealer

A new participant can be added without a trusted dealer.

Procedure:

1. Collect at least \(k\) valid shares.
2. Reconstruct the polynomial using Lagrange interpolation.
3. Choose a new x-coordinate.
4. Compute \(f(x)\) at that point.
5. Issue the resulting share to the new participant.

Characteristics:

- The secret remains unchanged.
- Existing shares remain unchanged.
- At least \(k\) shares are required.

---

## Adding New Participants With a Dealer

If the dealer retains the polynomial coefficients, new participants can be added directly.

Procedure:

1. Choose a new x-coordinate.
2. Evaluate \(f(x)\) using the stored polynomial.
3. Issue the resulting share.

Characteristics:

- The secret remains unchanged.
- Existing shares remain unchanged.
- No share collection is required.
- The dealer must securely retain the polynomial coefficients.

---

## Maximum Number of Participants

Each participant must have a unique x-coordinate in the finite field.

Since this implementation does not use \(x=0\), the maximum theoretical number of participants is:

\[
p - 1
\]

For:

```python
PRIME = 101
```

the maximum number of participants is:

```text
100 participants
```

If this limit is reached, a larger finite field must be selected and all shares must be regenerated.

---

## Example Output

```text
==============================================
Shamir's (k, n) Threshold Secret Sharing Scheme
==============================================
Secret S                : 1
Total participants n    : 7
Threshold k             : 3

Generated Shares
(1, 14, 57)
(2, 25, 83)
(3, 41, 12)
(4, 58, 91)
(5, 63, 44)
(6, 79, 65)
(7, 92, 38)

Recovered Secret: 1
Match: True
```

The actual share values vary because the polynomial coefficients and x-coordinates are randomly generated.

---

## Educational Purpose

This project is intended as a simple and readable implementation for learning:

- Shamir's Secret Sharing Scheme
- Finite field arithmetic
- Polynomial interpolation
- Threshold cryptography

It prioritizes clarity and explanation over performance or production-grade security.

---

## License

MIT License
