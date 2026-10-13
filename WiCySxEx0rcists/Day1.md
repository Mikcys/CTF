# 🖼️ A Picture Is Worth Two Fragments

## 🎯 Challenge Overview

- **Category:** Digital Forensics / Steganography
- **Challenge Name:** A Picture Is Worth Two Fragments
- **Tools Used:** Binwalk, Steghide, HexEd.it, `strings`, `exiftool`, `grep`

The challenge provided a ZIP file named `fragments-of-truth.zip`. After extracting it, I found two images: `school.jpg` and `WarAndPeace.png`.

The objective was to investigate both images and recover the two hidden fragments of the flag.

## 🔍 Step 1: Initial Analysis

After extracting the ZIP file,two images were found

<img width="442" height="195" alt="image" src="https://github.com/user-attachments/assets/ae739e2a-a258-4006-ae68-3cc552b00f54" />

I first analyzed `school.jpg` using the following commands:

```bash
strings school.jpg
grep
```
These initial checks did not reveal any useful clues.
While analyzing school.jpg using exiftool school.jpg, I discovered the keyword **taliban** in the image's metadata under the Comment field. This served as a potential clue during the initial investigation, although it did not directly reveal the flag.

<img width="622" height="485" alt="image" src="https://github.com/user-attachments/assets/f8caa0a3-9c6a-4b4d-a5f2-e5a8984fde63" />

## 🧩 Step 2: Finding the Hidden JPEG

I used **Binwalk** to analyze `school.jpg` and discovered that it contained two JPEG images embedded within the same file.

```bash
binwalk school.jpg
```
<img width="686" height="102" alt="image" src="https://github.com/user-attachments/assets/af8e6c4c-972b-4cfe-b1b1-06d1cdf0f005" />

The output revealed the second JPEG image starting at byte offset `90092`.

To extract the second image, I used:

```bash
tail -c +90093 school.jpg > hello
```

Here:
- `tail -c +90093` reads the file starting from byte 90093.
- `>` redirects the extracted data into a new file named `hello`.

The offset is `90093` because the `tail` command uses a 1-based byte position, while Binwalk reports offsets starting from zero.

<img width="392" height="225" alt="image" src="https://github.com/user-attachments/assets/c86ead2e-b421-4011-8e1b-d6298b6853f9" />

## 🔐 Step 3: Extracting the First Flag Fragment

After extracting the embedded JPEG into `hello`, I checked whether it contained hidden data using Steghide.

```bash
steghide info hello
```
The command indicated that a file was embedded inside the image.

<img width="467" height="170" alt="image" src="https://github.com/user-attachments/assets/61f95049-9586-41e0-9276-fd12489872eb" />

I then extracted the hidden file using:

```bash
steghide extract -sf hello
```
passphrase:taliban
After extracting and reading the file, I recovered the **first half of the flag**.

<img width="377" height="50" alt="image" src="https://github.com/user-attachments/assets/2c9f10a3-9726-4c7b-8725-bfbed8b622c8" />

## 🛠️ Step 4: Recovering the Second Flag Fragment

Next, I analyzed the second image, `WarAndPeace.png`.

Upon examining its hexadecimal contents, I discovered that the image was corrupted or incorrectly structured.

<img width="512" height="45" alt="image" src="https://github.com/user-attachments/assets/3fe1d780-c7d7-47c2-8525-f064619fec02" />

I opened the image in **HexEd.it** and inspected its hexadecimal data. By correcting the relevant bytes, I repaired the image data and recovered the **second half of the flag**.

<img width="504" height="662" alt="image" src="https://github.com/user-attachments/assets/963aabd0-dc6c-46ca-85f1-13a82c95f40a" />

## 🏁 Conclusion

The challenge required combining multiple digital forensics techniques to recover two separate flag fragments.

- **Binwalk** helped identify an embedded JPEG inside another image.
- **Tail** extracted the embedded JPEG using its byte offset.
- **Steghide** revealed and extracted the first hidden flag fragment.
- **HexEd.it** helped repair the corrupted image data and recover the second fragment.

The challenge demonstrated that image files can contain hidden data beyond their visible contents, and that inspecting file structure and hexadecimal data can reveal information that ordinary tools may miss.

