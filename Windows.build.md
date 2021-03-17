# Requirements

* [cmake](https://cmake.org/download)
* [Visual Studio Community](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=16)
* unzip (part of git for windows) or use [gui build-in solutions](https://support.microsoft.com/en-us/windows/zip-and-unzip-files-f6dde0a7-0fec-8294-e1d3-703ed85e7ebc)
* [git for windows](https://git-scm.com/download/win) (optional)
* (optional) [curl](https://curl.se/windows/) for downloading files from internet


# Tesseract Windows installation (64bit) in command line

Destination for installation:
```
    mkdir F:\win64
    set INSTALL_DIR=F:\win64
    set PATH=%PATH%;%INSTALL_DIR%\bin
```

Build tree:
```
    mkdir F:\Project & cd Project
    call "c:\Program Files (x86)\Microsoft Visual Studio\2019\Community\VC\Auxiliary\Build\vcvars64.bat" x64
```

## zlib build and instalation

```
    curl https://zlib.net/zlib1211.zip
    "c:\Program Files\Git\usr\bin\unzip.exe" zlib1211.zip
    cd zlib-1.2.11
    mkdir build.msvs && cd build.msvs
    cmake .. -DCMAKE_INSTALL_PREFIX=%INSTALL_DIR%
    "C:\Program Files\CMake\bin\cmake.exe"  --build . --config Release --target install
    cd ..\..
```

## libpng build and instalation

    curl https://vorboss.dl.sourceforge.net/project/libpng/libpng16/1.6.37/lpng1637.zip
    "c:\Program Files\Git\usr\bin\unzip.exe" lpng1637.zip
    cd lpng1637
    mkdir build.msvs && cd build.msvs
    "C:\Program Files\CMake\bin\cmake.exe" .. -DCMAKE_INSTALL_PREFIX=%INSTALL_DIR%
    "C:\Program Files\CMake\bin\cmake.exe"  --build . --config Release --target install
    cd ..\..

## leptonica build and instalation

    curl -L https://github.com/DanBloomberg/leptonica/archive/master.zip --output leptonica.zip
    "c:\Program Files\Git\usr\bin\unzip.exe" leptonica.zip
    cd leptonica-master

or

    "C:\Program Files\Git\cmd\git.exe" clone --depth 1 https://github.com/DanBloomberg/leptonica.git
    cd leptonica

Then:

    mkdir build.msvs && cd build.msvs
    "C:\Program Files\CMake\bin\cmake.exe" .. -DCMAKE_INSTALL_PREFIX=%INSTALL_DIR% -DCMAKE_PREFIX_PATH=%INSTALL_DIR% -DBUILD_PROG=OFF -DSW_BUILD=OFF -DBUILD_SHARED_LIBS=ON
    "C:\Program Files\CMake\bin\cmake.exe" --build . --config Debug --target install
    "C:\Program Files\CMake\bin\cmake.exe" --build . --config Release --target install
    cd ..\..


## tesseract build and instalation

    curl -L https://github.com/tesseract-ocr/tesseract/archive/4.1.1.zip --output tesseract.zip
    "c:\Program Files\Git\usr\bin\unzip.exe" tesseract.zip
    cd tesseract-4.1.1

or

    git clone -b 4.1.1 --depth 1 https://github.com/tesseract-ocr/tesseract.git
    cd tesseract

Then:

    "C:\Program Files\CMake\bin\cmake.exe" .. -DCMAKE_INSTALL_PREFIX=%INSTALL_DIR% -DCMAKE_PREFIX_PATH=%INSTALL_DIR% -DBUILD_TRAINING_TOOLS=OFF -DSW_BUILD=OFF -DBUILD_SHARED_LIBS=ON -DLeptonica_DIR=%INSTALL_DIR%\lib\cmake
    "C:\Program Files\CMake\bin\cmake.exe" --build . --config Release --target install
    cd ..\..

### Check

    %INSTALL_DIR%\bin\tesseract -v
    tesseract 4.1.1
     leptonica-1.81.0 (Mar 17 2021, 20:26:26) [MSC v.1928 LIB Release x64]
      libpng 1.6.37 : zlib 1.2.11
     Found AVX2
     Found AVX
     Found FMA
     Found SSE

# tesserocr

```
    git clone https://github.com/zdenop/tesserocr.git
    cd tesserocr
    git checkout window_build
```

```
SET VS90COMNTOOLS=%VS140COMNTOOLS%
SET INCLUDE=%INCLUDE%;%INSTALL_DIR%\include
SET LIBPATH=%LIBPATH%;%INSTALL_DIR%\lib

python setup.py build
```
