# SecretMerge

SecretMerge is a fully offline browser tool that securely combines two password parts into one using XOR encryption with ASCII95 mapping. No server, no internet connection required — runs entirely in your browser as a single HTML file.

## The Concept

Storing a complete password in a single location is a security risk. SecretMerge is based on the idea of splitting your password into two separate parts and storing them independently. Only when both parts are combined does the final password emerge.

Example storage strategies:

- Part A written on a piece of paper kept in a safe or wallet, Part B stored in your password manager
- Part A memorized, Part B stored in your password manager
- Part A on a USB stick stored at home, Part B in your password manager
- Part A shared with a trusted person, Part B only known to you

This way, neither part alone reveals anything about the final password.

## How It Works

Enter Part A and Part B of your password. SecretMerge applies a byte-wise XOR operation across both inputs and maps the result to a 95-character printable ASCII character set, producing a deterministic, high-entropy output every time. The same two inputs will always produce the same result.

## Security Features

- Fully offline — `default-src 'none'` CSP header, zero network requests
- Blur protection — result is blurred by default, revealed only on hover
- Clipboard auto-clear — clipboard is wiped automatically after 15 seconds
- Memory cleanup — the merged result is cleared from JavaScript memory after use
- Hidden inputs — both password fields use `type="password"`
- Dark / Light mode — switchable via toggle
- Responsive — works on desktop and mobile

## Usage

1. Open `index.html` in your browser
2. Enter Part A and Part B
3. Click "Merge passwords"
4. Hover over the result to reveal it
5. Copy the result using the button
6. The clipboard clears automatically after 15 seconds

## Tips for Practical Use

- Write Part A on a piece of paper and store it somewhere safe. Do not store it digitally.
- Store Part B in your password manager of choice.
- When you need your full password, open SecretMerge, combine both parts, and copy the result directly into the login field.
- Never store the merged result permanently. Re-create it only when needed.

## Important Security Note

SecretMerge cannot protect against OS-level threats such as keyloggers or screenshot tools. To reduce risk, paste your password parts instead of typing them manually whenever possible.

## Tech Stack

Pure HTML, CSS, and JavaScript — no external libraries or frameworks. Font embedded as Base64. Works entirely client-side.

## License

GNU General Public License v3.0 — see [LICENSE](LICENSE)

Developed with assistance from Perplexity AI.
