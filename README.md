# This ibmprojects repository stores  project code Which i wrote in python language  when doing a cyber security related course in IBM
# Image-Based Message Encryption and Decryption

## Overview

This project provides a simple way to hide a secret message inside an image using the OpenCV library. The message is encrypted into the image and can later be decrypted with the correct password.

## Features

- Encrypt a secret message into an image
- Decrypt the message from the image using a password

## Requirements

- Python 3.x
- OpenCV library

## Installation

1. **Clone the repository**:
    ```bash
    git clone https://github.com/your-username/image-encryption.git
    cd image-encryption
    ```

2. **Install the required library**:
    ```bash
    pip install opencv-python
    ```

3. **Place your image**:
   - Save the image you want to use for encryption as `hehimg.png` in the same directory as the script.

## Usage

1. **Run the script**:
    ```bash
    python image_encryption.py
    ```

2. **Enter the secret message** when prompted.
3. **Enter a password** for encrypting the message.
4. The encrypted image will be saved as `encryptedImage.jpg` and opened automatically.
5. **Enter the password** when prompted for decryption to retrieve the original message.

## Code Explanation

### Imports and Initial Setup

```python
import cv2
import os
import string
```

### Load the Image and Take User Input

```python
img = cv2.imread("hehimg.png")
msg = input("Enter secret message:")
password = input("Enter a password:")
```

### Create Encoding and Decoding Dictionaries

```python
d = {}
c = {}

for i in range(255):
    d[chr(i)] = i
    c[i] = chr(i)
```

### Encrypt the Message into the Image

```python
n = 0
m = 0
z = 0

for i in range(len(msg)):
    img.itemset((n, m, z), d[msg[i]])
    n = n + 1
    m = m + 1
    z = (z + 1) % 3
cv2.imwrite("encryptedImage.jpg", img)
os.startfile("encryptedImage.jpg")
```

### Decrypt the Message from the Image

```python
message = ""
n = 0
m = 0
z = 0

pas = input("Enter passcode for decryption:")
if password == pas:
    for i in range(len(msg)):
        message = message + c[img[n, m, z]]
        n = n + 1
        m = m + 1
        z = (z + 1) % 3
    print("Decrypted message =", message)
else:
    print("You are not Authenticated")
```

## Notes

- Ensure the image `hehimg.png` is in the same directory as the script before running it.
- The encrypted message length must not exceed the image capacity.
- The script currently supports only 8-bit characters.


## Acknowledgements

- OpenCV library for image processing.

---

Feel free to modify and expand the project as needed. Contributions are welcome!
