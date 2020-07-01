# Tesseract 
[![](https://img.shields.io/badge/Tesseract-v1.79.0-blue)](https://github.com/DanBloomberg/leptonica/releases/download/1.79.0/leptonica-1.79.0.tar.gz)  [![](https://img.shields.io/badge/pytesseract-v0.3.4-lightgrey)](https://pypi.org/project/pytesseract/)

In Conclusion, I did three kinds of languages including English, Simplified Chinese, and Traditional Chinese. We can know the performance not good for Chinese actually. In contrast, the performance of English samples are quite good if your font is not using irregular font that I think it can normally recognize them.

Please check the [Jupyter file](./pytesseract.ipynb) of what I did small tests. 

---
# Install `pytesseract`

Command:

```
sudo -H python3 -m pip install pytesseract
```

---
# Build the Tesseract from source
In these steps, I installed on my desktop. (Ubuntu system 18.04)

> Check here : 
> - https://tesseract-ocr.github.io/tessdoc/Compiling.html
> - https://github.com/tesseract-ocr/tesseract/wiki

So you can use the apt directly to install

```
sudo apt install tesseract-ocr
```

And you still need to install the some lib

```
sudo apt install libtesseract-dev 
```

If you install by git (Build from source.)
Please check here : https://tesseract-ocr.github.io/tessdoc/Compiling-%E2%80%93-GitInstallation.html

## Steps on my way:

```
sudo apt-get install automake ca-certificates g++ git libtool libleptonica-dev make pkg-config

sudo apt-get install libpango1.0-dev

git clone https://github.com/tesseract-ocr/tesseract.git
```

So we still need to install *Leptonica* package. (Check [here](https://github.com/DanBloomberg/leptonica))

I downloaded from here : https://github.com/DanBloomberg/leptonica/releases). 
* [Version 1.79.0](https://github.com/DanBloomberg/leptonica/releases/download/1.79.0/leptonica-1.79.0.tar.gz)
* Build the Leptonica : Here is the [README](http://www.leptonica.org/source/README.html)

```
./configure
make
sudo make install
sudo make check
```

There is an error.

```
============================================================================
See prog/test-suite.log
============================================================================
Makefile:4127: recipe for target 'test-suite.log' failed
make[3]: *** [test-suite.log] Error 1
make[3]: Leaving directory '/home/chieh/github/leptonica-1.79.0/prog'
Makefile:4233: recipe for target 'check-TESTS' failed
make[2]: *** [check-TESTS] Error 2
make[2]: Leaving directory '/home/chieh/github/leptonica-1.79.0/prog'
Makefile:5261: recipe for target 'check-am' failed
make[1]: *** [check-am] Error 2
make[1]: Leaving directory '/home/chieh/github/leptonica-1.79.0/prog'
Makefile:520: recipe for target 'check-recursive' failed
make: *** [check-recursive] Error 1
```

Then we come back to Tesseract folder.

```
cd tesseract
./autogen.sh
./configure
make
sudo make install
sudo ldconfig
```

To build the training tool.
```
make training
sudo make training-install
```

---
# Download the dataset

```
git clone https://github.com/tesseract-ocr/tessdata.git 

sudo mv * /usr/local/share/tessdata
```

Add this line in your `bashrc` or `zshrc`

```
# Tesseract 
export TESSDATA_PREFIX=/usr/local/share/tessdata/
```