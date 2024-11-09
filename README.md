# TOTP Code Generation and Keys Management

## 1. **Keys Management**
Keys are stored in a 2D array called `keys`. Each key is represented as an array with two elements:
- **index 0**: Stores information about the key (e.g., account name or label).
- **index 1**: Stores the key itself in Base32 format.

### Example:
```javascript
const keys = [
    ["Account 1", "BASE32SECRETKEY"],
    ["Account 2", "BASE32SECRETKEY"]
];
```
# TOTP Code Generation and Clipboard Copying

## 2. **TOTP Code Generation**
Every 30 seconds, the `generateTOTP` function calculates a new TOTP code for each key in the `keys` array. The process works as follows:

- The current timestamp (in seconds) is divided by 30 to form a time counter.
- The time counter is then converted to hexadecimal format.
- HMAC-SHA1 is used to hash the time counter with the key, resulting in a 6-digit OTP code.

## 3. **Clipboard Copying**
- Each TOTP code has a "Copy" button. When clicked, the TOTP code is copied to the clipboard, and a notification briefly appears confirming the copy.
- If you want to show the OTP you can edit index.html, delete comment on otpLine variable to become like this
```javascript
const otpLine = `
    <div class="totp-line" id="totpLine${i}">
        <p>${keys[i][0]}</p>
        <h1>${otp}</h1>
        <button class="copy-btn" id="copyBtn${i}" onclick="copyToClipboard('${otp}', ${i})">Copy</button>
    </div>
`;
```
![Demo](https://github.com/amryyahya/local-2fa-totp-generator/blob/main/demo.png?raw=true)

4. The **secret key file** is saved on your local machine. Ensure you only use it on your personal computer.
   For extra security, you can **encrypt `data.js`** using either GPG or a Python script:
   Example using GPG
   - **Using GPG**:
     1. Run this command to encrypt the file:
        ```bash
        gpg -c data.js
        ```
     2. This will create an encrypted file called `data.js.gpg`.
     3. To decrypt it later, use:
        ```bash
        gpg data.js.gpg
        ```