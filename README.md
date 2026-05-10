# SecretMerge

SecretMerge is a fully offline, single-file browser tool that derives a strong, deterministic password from two separate parts using HKDF + PBKDF2 (600,000 iterations, SHA-256). No server, no internet connection required.

## The Concept

Storing a complete password in one place is a security risk. SecretMerge splits your password into two independent parts. Only when both are combined does the final password emerge.

**Example storage strategies:**
- Part A on paper in a safe — Part B in your password manager
- Part A memorized — Part B in your password manager
- Part A on a USB stick at home — Part B in your password manager
- Part A with a trusted person — Part B known only to you

Neither part alone reveals anything about the final password.

## How It Works

Enter Part A, Part B, and an optional service context (e.g. `github`, `email`). SecretMerge derives a 32-character, high-entropy password using:

1. **HKDF** (SHA-256) to extract and expand the combined key material
2. **PBKDF2** (SHA-256, 600,000 iterations) for computational hardening
3. **Rejection sampling** to map output to 94 printable ASCII characters (0x21–0x7E) without modulo bias

The same inputs always produce the same output. Different service contexts produce different passwords from the same parts.

> Part order matters — A+B and B+A produce different passwords. Always enter them in the same order.

## Security Features

- **Fully offline** — `default-src 'none'` CSP, zero network requests
- **DOM protection** — derived password never written to DOM in plaintext; masked by default
- **Click-to-reveal** — result shown only on explicit click
- **Clipboard auto-clear** — clipboard wiped after 15 seconds with visual countdown
- **WebCrypto only** — no custom crypto implementations; unsupported browsers receive a clear error message
- **Hidden inputs** — password fields use `type="password"`
- **Dark / Light mode** toggle
- **Responsive** — works on desktop and mobile

## Usage

1. Open `index.html` in your browser
2. Enter Part A and Part B
3. Optionally enter a service name (e.g. `github`)
4. Click **Merge Password**
5. Click the result field to reveal the password
6. Copy it — clipboard clears automatically after 15 seconds

## Tips for Practical Use

- Write Part A on paper and store it somewhere safe. Do not store it digitally.
- Store Part B in your password manager.
- Use the service context to derive different passwords for different services from the same two parts.
- Never store the merged result permanently. Re-derive it only when needed.

## Security Note

SecretMerge cannot protect against OS-level threats such as keyloggers. Paste your password parts instead of typing them manually whenever possible.

> Designed for local offline use. Do not deploy on a public web server without replacing `unsafe-inline` in the CSP with a nonce-based policy.

## v1 vs v2

| | v1 | v2 (current) |
|---|---|---|
| Algorithm | XOR + ASCII95 | HKDF + PBKDF2 (600k iter) |
| Bias | Modulo bias | Rejection sampling |
| DOM security | CSS blur only | Password never in DOM |
| Clipboard | Manual | Auto-wipe after 15s |
| Service context | No | Yes |
| Platform parity | No | Yes |

## Tech Stack

Pure HTML, CSS, and JavaScript. No external libraries or frameworks. Works entirely client-side.

## License

GPL-3.0 — Developed with assistance from Perplexity AI.
