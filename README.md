# steg
steg - Store and extract files hidden within images

Inspired by:
* http://www.pythonchallenge.com/
* http://puzzling.stackexchange.com/

These are puzzle websites that commonly use ciphers and steganography to hide clues and 
solutions within images. 

## Description
These tools take files, convert them to raw binary (steg1), or raw octal (steg2) data and insert this data into the least-signficant-digit of an image's pixel rgb-data.

Image types officially supported: .jpg, .png

## Tools/Differences
* steg1 - uses binary (3 bits of information per pixel)
* steg2 - uses octal  (9 bits of information per pixel) (recommended)

## Comparison
> [I Have a Dream, by Martin Luther King, Jr. (August 28, 1963)](http://www.textfiles.com/etext/NONFICTION/)

| `duck.png`(raw image)           | `dreamy_duck.png` (Storing MLK's Speech)  |
|:------------------------------- |:----------------------------------------- |
| ![](steg2/test_images/duck.png) | ![](steg2/test_images/dreamy_duck.png)    |

## How it works
* data.txt: "Hi" 
* Binary data: **01001000 01101001** 
* Octal data:  **44151**

| raw-pixels   | steg1-pixels             | steg2-pixels             |
| ------------ | -------------------------| ------------------------ |
| (100, 10, 1) | (10**0**, 1**1**, **0**) | (10**4**, 1**4**, **1**) |
| (100, 10, 1) | (10**0**, 1**1**, **0**) | (10**5**, 1**1**, **8**) |
| (100, 10, 1) | (10**0**, 1**0**, **0**) | (10**9**, 10, 1)         |
| (100, 10, 1) | (10**1**, 1**1**, **0**) |                          |
| (100, 10, 1) | (10**1**, 1**0**, **0**) |                          |
| (100, 10, 1) | (10**1**, 1**8**, **9**) |                          |
* **Bolded Numbers** represent stored data
* **8** is the "separator" digit between file1, file2, .. (we have only 1 in this case)
* **9** is the "end" digit that signifies the end of data

## Dependencies
* Both steg1/steg2 require Pillow (tested with version 5.4.1) 
```pip
pip install pillow
```
* Python 3.0+
* Tested on ArchLinux

## Usage
* For steg1 see [README](steg1/README.md)
* For steg2 see [README](steg2/README.md)
