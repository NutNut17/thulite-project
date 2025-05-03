---
title: "Cybersecurity"
description: ""
summary: ""

date: 2025-03-08T15:48:39+08:00
lastmod: 2025-03-08T15:48:39+08:00
draft: false
weight: 115
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

### Cryptography

Study of algorithms and methods for secure communication.

#### Hashing

Hashing is a one-way function (irreversible) that takes an input and produces an consistent output. It's very hard to break using brute force method.

**SHA-256**

SHA-256 is a cryptographic hash function that input any data and output a fixed 256-bit hash value. SHA-256 are quick to compute, it's suitable for integrity checks and digital signatures but are quick to break for password, so it's not suitable for password.

**Password-Based Key Derivation Function**

To store password securely in a database. In case database is hacked, the password is extremely hard to break. Example: bcrypt, argon2

Assume the connection between client and server are secure. Whent the client register, it sends a plaintext information and password to server. The server generates `1. A salt, unique random value per password to prevents identical passwords from having the same hash` and `2. A secure hash function configuration` and save a derived a hash value from the password, salt and configuration.

#### Asymmetric Key

An asymmetric key have public key and private key. These keys are mathematically related, what one key encrypts, the other can decrypt — but not vice versa with the same key. Asymmetric crypto lets you communicate securely without prior shared secrets. Example: RSA, ECDSA (Elliptic Curve Digital Signature Algorithm, faster, smaller keys), Ed25519 (Newer, ultra-fast and secure).

**Encryption & Decryption**

To send a secret message to Alice: Bob encrypts the message using Alice’s public key. Only Alice’s private key can decrypt it.

**Digital Signature**

To verify identity or data integrity, Alice signs data with her private key. Anyone can verify the signature using Alice’s public key, ensuring it was really her and the message wasn’t altered.

**E2EE (End-to-End Encryption)**

Uses assymetric key to encrypt and decrypt data. Adopted in modern messaging apps.

#### Symmetric Key

A same symmetric key algorithm can be used to encrypt and decrypt data quickly than assymetric key algorithm. It's hard to break the symmetric key using brute force method because it's not feasible on current computing power. Example: AES-256 (Algorithm iterates using keys to make a cipher).

#### Summary

Crypto algorithm keeps updating through mathematics and quantum physics discoveries. A brute force resistant algorithm is not discovered. The only thing we can do is slow down the brute force attack.

| Tool/Algorithm | Defense Mechanism |
| - | - |
| PBKDF2 | Increases CPU time per guess |
| bcrypt | Adds compute cost + some memory |
| scrypt | Adds memory + parallelism cost |
| Argon2id | Strongest — CPU, memory, threads |
| Rate limiting | Limits login attempts per user/IP |
| 2FA/MFA | Makes password-only attacks useless |
| Account lockout | CAPTCHA	Slows automated login attacks |
| Password managers | Encourage long, random, unique passwords |

### Cybersecurity Tech

#### SSH

SSH (Secure Shell) is a cryptographic network protocol that provides a secure tunnel to access and manage remote computers over an unsecured network. It's commonly used for remote logins, file transfers, and executing commands on other systems, offering a secure alternative to older protocols like Telnet and FTP. It uses asymmetric keys, similar to TLS but without a CA.

#### TLS

TLS (Transport Layer Security) is a cryptographic protocol that secures communication over a network. Successor to SSL. It authenticates the server (and optionally the client) and establishes an encrypted session using a symmetric key.

#### VPN (Virtual Private Network)

A secure connection that encrypts your internet traffic, masks your IP address, and allows you to browse the internet freely, privately and safely. It creates a secure tunnel between your device and a remote server.

#### HTTPS

**Before Connection Established**

The process of HTTPS handshake and connection is secure, but before handshake, it's not. As the TCP/IP is not encrypted, in public WiFi network, others can see your traffic. Mobile network is encrypted at radio wave, but network provider can still intercept your traffic. A VPN is safer, but in public WiFi, other can see your device connecting to a VPN server but have no idea what's going on.

If someone can spoof DNS, redirect you, or inject a fake cert, they might intercept traffic (man-in-the-middle) before the TLS kicks in.

**Establishing Connection**

HTTPS needs TLS certificate. A website make a private-public key, sign it's metadata (IP, domain, etc.) with it's private keys and sends the CSR (Certificate Signing Request) to a trusted CA (Certificate Authority). The CA validates the CSR and sends back a certificate. The website checks the certificate and acknowledges that the CA have validated CSR. The certificate is hold by the website and sent to client browser for HTTPS handshake so that the client browser can validate whether the domain name and other infomation matches through CA to establish secured HTTPS.

**Key Exchange**

???

**After Connection Established**

HTTPS ensures that you're connected to the right server and that your connection is secure, but some information is still visible. Symmetric key is secretly shared through secured communication using assymetric key (client and server) during handshake. The session use the symmetric key to encrypt and decrypt data efficiently and securely.

### Web Security Concepts

#### Practices

**Input validation & sanitization**

Never trust any input, sanitize everything to receive data instead of code. SQL injection changes the SQL query statements and cause damage.

**Authentication & Authorization**

`Authentication` is about making sure the user is who they say they are. `Authorization` decides what parts of the application are allowed to use. Use `JWTs`, `OAuth2`, and session management properly.

**Password Storage & Secret Management**

Never store plaintext passwords. Use `bcrypt` or `Argon2` with proper salting and cost factors. 

Don’t put secrets in source code. Use Vaults like HashiCorp Vault, AWS Secrets Manager.

**CSRF (Cross-Site Request Forgery)**

Exploits the browser’s automatic cookie sending. Attacker tricks a logged-in user’s browser into making an unwanted request. Protect state-changing requests with CSRF tokens or SameSite cookies.

**CORS (Cross-Origin Resource Sharing)**

Enforce cross-origin rules and how to set up CORS headers securely. Ensuring proper access of hosting server resource.

**XSS (Cross-Site Scripting)**

Malicious scripts that get injected into pages and run in other users' browsers. Use libraries like `DOMPurify`.

**Web Security Headers**

| Set HTTP header | Description |
| - | - |
| Content-Security-Policy | Mitigates XSS by limiting allowed scripts/resources |
| Strict-Transport-Security | Forces HTTPS only |
| X-Content-Type-Options | Prevents MIME sniffing |
| Referrer-Policy | Controls referrer header leakage |
| X-Frame-Options: DENY or SAMEORIGIN | Prevents clickjacking |
| X-Permitted-Cross-Domain-Policies | Prevents clickjacking |
| Permissions-Policy | Limits access to features like geolocation, camera, etc |

#### Malware Types

**Ransomware**

Malware that prevents you from accessing your device and the data stored on it, usually by encrypting your files.

**Phishing**

Trick individuals into revealing sensitive information by pretending to be a trusted source.

**Trojan Horse**

A malware that downloads onto a computer disguised as a legitimate program.

**Clickjacking**

Hides your site in an `<iframe>` and tricks users into clicking invisible buttons.

**Open Redirects**

A URL param is used to redirect users, and it’s not validated.

**Subdomain Takeover**

Attacker gains control over a subdomain of a target domain. Typically, this happens when the subdomain has a canonical name.

#### Infrastructure Level Security

It's bettere to implement Zero Trust Architecture, don’t trust anything inside or outside your network by default.

**Threat modeling**

STRIDE is a model for identifying computer security threats.

| Threat | Description | Desired Security Property |
| - | - | - |
| Spoofing | Spoofing is a type of MITM (Man-in-the-middle attack) attack where the attacker tries to impersonate another user. | Authentication |
| Tampering | Harmful alteration of information or systems | Integrity (Honesty) |
| Repudiation | The denial by a party of having performed a particular action | Non-repudation |
| Information Disclosure | Unintentionally reveals sensitive information to its users | Confidentiality |
| Denial of Service | Spam to a server until it becomes too busy to be available | Availability |
| Elevation of Privilege | Attacker exploits vulnerabilities to gain higher-level access | Authorization |

**Rate limiting & abuse protection**

Protect APIs from brute-force and scraping. Use IP rate limits, CAPTCHAs, etc.

**Security in CI/CD**

Secure your build pipeline. Secrets shouldn’t leak through envs or build logs. Signed commits and packages.

**Logging and Monitoring**

Don’t log secrets. Do log auth attempts, IPs, anomalies.

#### Advanced

- Try OWASP Juice Shop or HackTheBox for pen testing basics.
- Understand cloud security (IAM, security groups, S3 bucket policies).
- Use tools like Burp Suite or Wireshark for real testing.
- Look into Secure SDLC practices.
