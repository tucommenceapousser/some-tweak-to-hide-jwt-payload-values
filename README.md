
  <summary>## 🌟 Some Tweak to Safeguard JWT Payload Values</summary>

[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2Fpassword123456%2Fsome-tweak-to-hide-jwt-payload-values&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false)](https://hits.seeyoufarm.com)

<p align="center">
  <a href="https://github.com/password123456/some-tweak-to-hide-jwt-payload-values"><img title="Version" src="https://img.shields.io/badge/Version-1.0.0-darkblue?style=for-the-badge&logo="></a>
  <a href="https://github.com/password123456/some-tweak-to-hide-jwt-payload-values/blob/main/LICENSE"><img title="License" src="https://img.shields.io/badge/License-MIT-darkblue?style=for-the-badge&logo=mit"></a>
  <a href=""><img title="Python" src="https://img.shields.io/badge/Python-3.9-blue?style=for-the-badge&logo=python"></a>
  <a href="https://github.com/password123456"><img title="Author" src="https://img.shields.io/badge/Author-password123456-blue?style=for-the-badge&logo=github"></a>
</p>

<details id="overview">
  <summary>## Overview</summary>

This repository explores innovative approaches to fortify the security of JSON Web Token (JWT) payload decoding. By dynamically altering the payload values, the decoded output remains unintelligible, thwarting attempts at unauthorized access.

</details>

<details id="what-is-a-jwt-token">
  <summary>## JWT Token</summary>

A JSON Web Token (JWT, pronounced "jot") is a compact and URL-safe way of passing a JSON message between two parties. It's a standard, defined in RFC 7519. The token is a long string, divided into parts separated by dots. Each part is base64 URL-encoded.

</details>

<details id="primary-objective-of-this-code-snippet">
  <summary>## Primary Objective of this Code Snippet</summary>

This code snippet offers a tweak perspective aiming to enhance the security of the payload section when decoding JWT tokens, where the stored keys are visible in plaintext. This code snippet provides a tweak perspective aiming to enhance the security of the payload section when decoding JWT tokens. Typically, the payload section appears in plaintext when decoded from the JWT token (base64). The main objective is to lightly encrypt or obfuscate the payload values, making it difficult to discern their meaning. The intention is to ensure that even if someone attempts to decode the payload values, they cannot do so easily.

</details>

<details id="userid">
  <summary>## User ID</summary>

- The code snippet targets the key named "userid" stored in the payload section as an example.
- The choice of "userid" stems from its frequent use for user identification or authentication purposes after validating the token's validity (e.g., ensuring it has not expired).

</details>

<details id="encryption">
  <summary>## Encryption</summary>

- The timestamp is hashed and then encrypted by performing a bitwise XOR operation with the user ID.
- XOR operation is performed using a symmetric key.
- The resulting value is then encoded using Base64.

</details>

<details id="decryption">
  <summary>## Decryption</summary>

- Encrypted data is decoded using Base64.
- Decryption is performed by XOR operation with the symmetric key.
- The original user ID and hashed timestamp are revealed in plaintext.
- The user ID part is extracted by splitting at the "|" delimiter for relevant use and purposes.

</details>

<details id="symmetric-key-for-xor-encoding">
  <summary>## Symmetric Key for XOR Encoding</summary>

- Various materials can be utilized for this key.
- It could be a salt used in conventional password hashing, an arbitrary random string, a generated UUID, or any other suitable material.
- However, this key should be securely stored in the database management system (DBMS).

</details>

<details id="notes">
  <summary>## Notes</summary>

- This code snippet is created for educational purposes and serves as a starting point for ideas rather than being inherently secure.
- It provides a level of security beyond plaintext visibility but does not guarantee absolute safety.

</details>

<details id="and">
  <summary>## And...</summary>

```python
# In the example, the key is shown as { 'userid': 'random_value' },
# making it apparent that it represents a user ID.

# However, this is merely for illustrative purposes.

# In practice, a predetermined and undisclosed name is typically used.
# For example, 'a': 'changing_random_value'
```

</details>

<details id="preview">
  <summary>## Preview</summary>

```bash
# Run the example
python3 main.py

- Current Unix Timestamp: 1709160368
- Current Unix Timestamp to Human Readable: 2024-02-29 07:46:08

- userid: 23243232
- XOR Symmetric key: b'generally_user_salt_or_hash_or_random_uuid_this_value_must_be_in_dbms'
- JWT Secret key: yes_your_service_jwt_secret_key

- Encoded UserID and Timestamp: VVZcUUFTX14FOkdEUUFpEVZfTWwKEGkLUxUKawtHOkAAW1RXDGYWQAo=
- Decoded UserID and Hashed Timestamp: 23243232|e27436b7393eb6c2fb4d5e2a508a9c5c

- JWT Token: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0aW1lc3RhbXAiOiIyMDI0LTAyLTI5IDA3OjQ2OjA4IiwidXNlcmlkIjoiVlZaY1VVRlRYMTRGT2tkRVVVRnBFVlpmVFd3S0VHa0xVeFVLYXd0SE9rQUFXMVJYREdZV1FBbz0ifQ.bM_6cBZHdXhMZjyefr6YO5n5X51SzXjyBUEzFiBaZ7Q
- Decoded JWT: {'timestamp': '2024-02-29 07:46:08', 'userid': 'VVZcUUFTX14FOkdEUUFpEVZfTWwKEGkLUxUKawtHOkAAW1RXDGYWQAo='}

# Run again
- Decoded JWT: {'timestamp': '2024-02-29 08:16:36', 'userid': '='}
- Decoded JWT
```

</details>
