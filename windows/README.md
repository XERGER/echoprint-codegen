# Codegen windows compilation instructions

Using Visual Studio 2022 for x86_64 build

## Preliminary steps

1. Install CMake for the target architecture: https://cmake.org/download/
2. Download and install 7-Zip: http://www.7-zip.org/
3. Download zlib 1.2.12: https://www.zlib.net/zlib-1.2.12.tar.gz
4. Download taglib 1.7: https://taglib.org/releases/taglib-1.7.tar.gz
5. Download Boost 1_79_0: https://boostorg.jfrog.io/artifactory/main/release/1.79.0/source/boost_1_79_0.7z
6. Uncompress zlib, taglib and boost into the echoprint-codegen directory

## Dependencies

### Zlib

1. Load CMake
2. For Browse Source... and Browse Build... select the zlib directory you uncompressed
3. Click configure
4. Choose Visual Studio 17 2022 as the generator, and use default native compilers
5. Click generate
6. Load the generated zlib.sln
7. Make sure "Release" and "x64" is selected in the top bar (next to the play button)
8. In the solution explorer, right click on zlib project and select Build

### Taglib

1. Load CMake
2. For Browse Source... and Browse Build... select the taglib directory you uncompressed
3. Press configure
4. Choose Visual Studio 17 2022 as the generator, and use default native compilers
5. There will be an error saying "Could NOT find ZLIB". Click the Advanced checkbox.
6. Change the ZLIB_INCLUDE_DIR variable to the zlib directory, and ZLIB_LIBRARY_RELEASE variable to zlib-1.2.12\Release\zlib.lib
7. Click Generate
8. Load the generated taglib.sln
9. Make sure "Release" and "x64" is selected in the top bar (next to the play button)
10. In the solution explorer, right click on tag project and select Build

### FFmpeg

1. Download ffmpeg: https://github.com/BtbN/FFmpeg-Builds/releases/download/latest/ffmpeg-master-latest-win64-gpl.zip
2. Uncompress the archive and move it somewhere in your path

## Compiling codegen

1. Load codegen.sln from echoprint-codegen/windows directory
2. Retarget Project dialog will pop-up, select Windows SDK Version: 10.0 and Platform Toolset: Upgrade to v143
3. Open the Configuration Manager and under Active solution platform, add New -> Type: x64 and Copy settings from: Win32
4. Open project Properties window and change the versions for the following:
* C/C++ -> General -> Additional Include Directories: zlib-**1.2.12**, boost_**1_79_0**
* Linker -> General -> Additional Library Directories: zlib-**1.2.12**
5. Make sure "Release" and "x64" is selected in the top bar (next to the play button)
4. In the solution explorer, right click on tag project and select Build

 
## Running

Copy tag.dll and zlib.dll into the same directory as codegen.exe. Make sure that the ffmpeg is extracted and path to the ffmpeg.exe can be provided as the first argument.

    codegen.exe path_to_ffmpeg/ffmpeg example.mp3

## Credits

Zlib and Taglib compilation instructions from Lukáš Lalinský: http://oxygene.sk/lukas/2011/04/windows-binaries-for-taglib/
