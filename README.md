#tess-two
* * *

A fork of Tesseract Tools for Android ([tesseract-android-tools](http://code.google.com/p/tesseract-android-tools/)) that adds some 
additional functions. Tesseract Tools for Android is a set of Android APIs and
build files for the Tesseract OCR and Leptonica image processing libraries.

This project works with Tesseract v3.01. Source code for Tesseract 3.01 and
the other dependencies is included in the tess-two/external folder.

The tess-two subdirectory contains tools for compiling the Tesseract, Leptonica, and JPEG
libraries for use on the Android platform. It contains an Eclipse Android
[library project](http://developer.android.com/guide/developing/projects/projects-eclipse.html#SettingUpLibraryProject)
that provides a Java API for accessing natively-compiled Tesseract and Leptonica APIs.

This project adds the following methods on top of tesseract-android-tools r6 to enable retrieving 
bounding boxes for words and characters recognized using OCR:

* TessBaseAPI::GetRegions()
* TessBaseAPI::GetTextlines()
* TessBaseAPI::GetWords()
* TessBaseAPI::GetCharacters()

Note: GetTextlines(), GetWords() and GetCharacters() work well, but I have not gotten good 
results from Tesseract when calling GetRegions().

eyes-two
========

The eyes-two subdirectory contains a second, separate library project with additional image 
processing code copied from the [eyes-free project](http://code.google.com/p/eyes-free/) without 
modifications. It includes native functions for text detection, blurriness detection, optical flow 
detection, and thresholding. Building eyes-two is not necessary for using the Tesseract API.

While I haven't tested all the Eyes-two code, I've bundled it in this project alongside tess-two for
convenience due to its dependency on Leptonica. 

Build
=====

This project is set up to build on Android SDK Tools r16 and Android NDK r7. The build works on Ubuntu 11.04. It's been reported to not work on Ubuntu 11.10 (Issue #6).

To build tess-two, run the following commands in the terminal:

    git clone git://github.com/rmtheis/tess-two tess
    cd tess/tess-two
    ndk-build
    android update project --path .
    ant release

To build eyes-two, additionally run the following:

    cd ../eyes-two
    ndk-build
    android update project --path .
    ant release

After building, the tess-two and eyes-two projects can be imported into Eclipse using 
File->Import->Existing Projects into Workspace.

License
=======

This project is licensed under the [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0.html)

    /*
     * Copyright 2011 Robert Theis
     *
     * Licensed under the Apache License, Version 2.0 (the "License");
     * you may not use this file except in compliance with the License.
     * You may obtain a copy of the License at
     *
     *      http://www.apache.org/licenses/LICENSE-2.0
     *
     * Unless required by applicable law or agreed to in writing, software
     * distributed under the License is distributed on an "AS IS" BASIS,
     * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
     * See the License for the specific language governing permissions and
     * limitations under the License.
     */

 
This project contains third party software in "tess-two/external" with separate license agreements:

* Tesseract 3.01 (Modified to add TessBaseAPI::GetCharacters())
* Leptonica 1.68 (Unmodified)
* LibJPEG 6b (Unmodified)
