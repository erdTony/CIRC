# TN1518 - Building OpenCV4 on Windows g++ for Qt6
Updated 08/14/24

## References

* [Github Gist](https://gist.github.com/demid5111/6faa590e4fc5813550dd95cc1c538893) 'Build OpenCV for Python and C++ from sources' section 
* [CV Tricks](https://cv-tricks.com/how-to/installation-of-opencv-4-1-0-in-windows-10-from-source/)
* [CarpeDiem UK](https://carpediemsystems.co.uk/2022/11/23/compiling-opencv-4-6-0-on-windows-11-vs2022/)
* [Medium](https://medium.com/csmadeeasy/opencv-c-installation-on-windows-with-mingw-c0fc1499f39)

## Prerequsites

* [ ] Qt v6.8.2 or later

* [ ] PATH:
  * C:\Qt\Tools\mingw1310_64\bin
  * C:\Qt\6.8.2\mingw_64\bin
  * C:\Qt\Tools\CMake_64\bin
  * C:\Qt\Tools\QtCreator\bin

* [ ] Environment

* [ ] gcc & Friends
  * copy c++.exe to cc.exe
  * Test with > `c++ --version`, `gcc --version`, `g++ --version`, Expect v13.1.0 or later
  * > `gdb --version` v11.2 or later

* [ ] CMake with Qt
  * Test with > `cmake --version`, Expect v3.29.3 or later

* [ ] Git for Windows, SmartGit, Github Desktop, TourtoiseGit as desired

* [ ] Java & JNI
  * From: `https://www.java.com/download/ie_manual.jsp`, Select [Offline Installer]
  * From: `https://www.java.com/en/download/windows_offline.jsp`, Press [Download]
  * When downloaded, Run `jre-8u441-windows-i586.exe` or later
    * Check Change Destination, Press [Install]
    * Press [Change], Install to `\Lang\Java\jre-1.8`, Press [Install], ..., Press [Close]
    

## Source Code

[ ] Either download or fork and clone repository:

### Download ZIP
  * From: [Github OpenCV Releases](https://github.com/opencv/opencv/releases/tag/4.5.1) or later
  * Download: [Source v4.5.1 Zip](https://github.com/opencv/opencv/archive/refs/tags/4.5.1.zip) or later
  * When download complete, extract to `\home\code\repo\opencv`

### Fork Repository
  * From: `https://github.com/opencv/opencv`
  * Select `New Fork`
    * ...
    * Uncheck `Save v4.x only`
    * Press [Create Fork]
  * Open CMD Console
    * > `cd \home\code\repo`
    * > `gh repo clone TonyZOtto/opencv`
    * _Note for iffy connections:_
      * Reference: [stackoverflow](https://stackoverflow.com/questions/3954852/how-to-complete-a-git-clone-for-a-big-project-on-an-unstable-connection)

### Repeat for opencv_contrib

## Initial Configuration

* [ ] Run > `cmake-gui`
  * [ ] Set source code to: `\code\repo\opencv`
  * [ ] Set binary build directory to: `\code\temp\OpenCV4[D]\build` _D for Debug_
  * [ ] Add `CMAKE_MAKE_PROGRAM` FILEPATH to `C:\Qt\Tools\mingw1310_64\bin\mingw32-make.exe`
  * [ ] Add `CMAKE_CUSTOM_LINKER` FILEPATH to `C:\Qt\Tools\mingw1310_64\bin\ld.exe`
  * [ ] Add `CMAKE_C_COMPILER` FILEPATH to `C:/Qt/Tools/mingw1310_64/bin/cc.exe`
  * [ ] Add `CMAKE_CXX_COMPILER` FILEPATH to `C:/Qt/Tools/mingw1310_64/bin/c++.exe`
  * [ ] Set `CMAKE_BUILD_TYPE` to `Debug` _Or Release_
  * Check `BUILD_DOCS`
  * Check `BUILD_EXAMPLES`
  * Check `BUILD_WITH_DEBUG_INFO` _Uncheck for Release_
  * Check `WITH_QT`
  * Specify `OPENCV_EXTRA_MODULES_PATH` as `/home/code/repo/opencv_contrib/modules` _Note: must be forward / slash_
  * Specify `QT_QMAKE_EXECUTABLE` as `\Qt\6.8.2\mingw_64\bin\qmake.exe`
  * Specify `Qt6_DIR` as `\Qt\6.8.2`
  * Specify `CMAKE_INSTALL_PREFIX` as `C:\code\temp\OpenCV4[D]\install` _Omit D for Release_
  * Uncheck `BUILD_JAVA`
  * Add `Java_JAVA_EXECUTABLE` PATH as `C:\Lang\java\jre\bin`
  * Specify `OPENCV_JAVA_SOURCE_VERSION` and `OPENCV_JAVA_TARGET_VERSION` to `1.8`
  * Check `INSTALL_BIN_EXAMPLES`, `INSTALL_C_EXAMPLES`, `INSTALL_TESTS`
  * Check `BUILD_DOCS`, `BUILD_EXAMPLES`, `BUILD_ZLIB`, `BUILD_TIFF`
  * Check `BUILD_JPEG`, `BUILD_PNG`, `BUILD_WITH_DEBUG_INFO` _Except Release_
  * Check `ENABLE_PRECOMPILED_HEADERS`, `CV_ENABLE_INTRINSICS`
  * Check ~~`WITH_CUDA`~~ _CUDA not available on FYH14X1 Laptop_
  * **Uncheck** `WITH_IPP` _IPP causes missing RunTmChk DLL_
  * **Uncheck** `INSTALL_PYTHON_EXAMPLES` _`pbsensor` compile error_
  * **Uncheck** `BUILD_opencv-videoio` _compile errors--for now_
  * Check `WITH_DIRECTX`, `WITH_EIGEN`, `WITH_OPENGL`
  * Press [Configure]
    * Select `MinGW Makefiles` and default `Use Native Compilers`
    * Press [Finish]
  * Pray for `Configuration Complete` with out errors, else fix and keep trying

## Generate

* In GUI:
  * Press [Generate]
  * Review `C:\code\temp\OpenCV4[D]/Build/CMakeFiles/CMakeOutput.log`, if present
  * Review `C:\code\temp\OpenCV4[D]/Build/CMakeFiles/CMakeError.log`
  * Fix anything fixable, Press [Generate]
 
## Build

* In CMD console:
  * > `cd \code\temp\OpenCV4D\build` _Omit D for Release_
  * > `mingw32-make -B` _Build all targets_
  * > Lotsa coffee

## Install
  * > `mingw32-make install`
  * `xcopy C:\code\temp\OpenCV4D\build\install\*.* C:\code\bin\3P\OpenCV-v4.10.0D /S` _Do this better above next time!_

## Integration

### useOCV4.pri

In /home/code/repo/INDIface6/src or ottozcode/src
```
# file: {repo}/src/useOCV.4.pri
INCLUDEPATH *= ../../../3rdParty/OpenCV-v4.8.0/include  # typical #include's specify opencv2
LIBS *= -L../../../3rdParty/OpenCV-v4.8.0/x64/mingw/bin

LIBS *= -lopencv_core480d         # if DEBUG
LIBS *= -lopencv_highgui480d
LIBS *= -lopencv_imageproc480d
LIBS *= -lopencv_objdetect480d

LIBS *= -lopencv_core480          # if RELEASE
LIBS *= -lopencv_highgui480
LIBS *= -lopencv_imageproc480
LIBS *= -lopencv_objdetect480
```
### CVMAJOR.pri

```
CVMAJOR = "CV0"
```

### **Repeat for Release**

SUCCESS!

# Listings

## Configure
```
Detected processor: AMD64
CMake Warning (dev) at cmake/OpenCVUtils.cmake:144 (find_package):
  Policy CMP0148 is not set: The FindPythonInterp and FindPythonLibs modules
  are removed.  Run "cmake --help-policy CMP0148" for policy details.  Use
  the cmake_policy command to set the policy and suppress this warning.

Call Stack (most recent call first):
  cmake/OpenCVDetectPython.cmake:64 (find_host_package)
  cmake/OpenCVDetectPython.cmake:271 (find_python)
  CMakeLists.txt:650 (include)
This warning is for project developers.  Use -Wno-dev to suppress it.

Could NOT find PythonInterp (missing: PYTHON_EXECUTABLE) (Required is at least version "2.7")
CMake Warning (dev) at cmake/OpenCVUtils.cmake:144 (find_package):
  Policy CMP0148 is not set: The FindPythonInterp and FindPythonLibs modules
  are removed.  Run "cmake --help-policy CMP0148" for policy details.  Use
  the cmake_policy command to set the policy and suppress this warning.

Call Stack (most recent call first):
  cmake/OpenCVDetectPython.cmake:64 (find_host_package)
  cmake/OpenCVDetectPython.cmake:280 (find_python)
  CMakeLists.txt:650 (include)
This warning is for project developers.  Use -Wno-dev to suppress it.

Could NOT find PythonInterp (missing: PYTHON_EXECUTABLE) (Required is at least version "3.2")
libjpeg-turbo: VERSION = 2.1.3, BUILD = opencv-4.8.0-dev-libjpeg-turbo-debug
libjpeg-turbo(SIMD): SIMD extensions disabled: could not find NASM compiler.  Performance will suffer.
Could NOT find OpenJPEG (minimal suitable version: 2.0, recommended version >= 2.3.1). OpenJPEG will be built from sources
OpenJPEG: VERSION = 2.5.0, BUILD = opencv-4.8.0-dev-openjp2-2.5.0-debug
OpenJPEG libraries will be built from sources: libopenjp2 (version "2.5.0")
Could not find OpenBLAS include. Turning OpenBLAS_FOUND off
Could not find OpenBLAS lib. Turning OpenBLAS_FOUND off
Could NOT find BLAS (missing: BLAS_LIBRARIES) 
Could NOT find LAPACK (missing: LAPACK_LIBRARIES) 
    Reason given by package: LAPACK could not be found because dependency BLAS could not be found.

VTK is not found. Please set -DVTK_DIR in CMake to VTK build directory, or to VTK install subdirectory with VTKConfig.cmake file
Module opencv_alphamat disabled because the following dependencies are not found: Eigen
freetype2:   NO
harfbuzz:    NO
Julia not found. Not compiling Julia Bindings. 
Module opencv_ovis disabled because OGRE3D was not found
No preference for use of exported gflags CMake configuration set, and no hints for include/library directories provided. Defaulting to preferring an installed/exported gflags CMake configuration if available.
Failed to find installed gflags CMake configuration, searching for gflags build directories exported with CMake.
Failed to find gflags - Failed to find an installed/exported CMake configuration for gflags, will perform search for installed gflags components.
Failed to find gflags - Could not find gflags include directory, set GFLAGS_INCLUDE_DIR to directory containing gflags/gflags.h
Failed to find glog - Could not find glog include directory, set GLOG_INCLUDE_DIR to directory containing glog/logging.h
Module opencv_sfm disabled because the following dependencies are not found: Eigen Glog/Gflags
Tesseract:   NO
Module opencv_ts disabled because opencv_videoio dependency can't be resolved!
Consider adding OPENCV_ALLOCATOR_STATS_COUNTER_TYPE=int/int64_t according to your build configuration
Excluding from source files list: modules/imgproc/src/imgwarp.lasx.cpp
Excluding from source files list: modules/imgproc/src/resize.lasx.cpp
Registering hook 'INIT_MODULE_SOURCES_opencv_dnn': C:/home/code/repo/opencv/modules/dnn/cmake/hooks/INIT_MODULE_SOURCES_opencv_dnn.cmake
opencv_dnn: filter out cuda4dnn source code
Excluding from source files list: <BUILD>/modules/dnn/layers/layers_common.rvv.cpp
Excluding from source files list: <BUILD>/modules/dnn/layers/layers_common.lasx.cpp
Excluding from source files list: <BUILD>/modules/dnn/int8layers/layers_common.lasx.cpp
Excluding from source files list: <BUILD>/modules/dnn/layers/cpu_kernels/conv_depthwise.rvv.cpp
Excluding from source files list: <BUILD>/modules/dnn/layers/cpu_kernels/conv_depthwise.lasx.cpp
Excluding from source files list: <BUILD>/modules/dnn/layers/cpu_kernels/fast_gemm_kernels.neon.cpp
Excluding from source files list: <BUILD>/modules/dnn/layers/cpu_kernels/fast_gemm_kernels.lasx.cpp
imgcodecs: OpenEXR codec is disabled in runtime. Details: https://github.com/opencv/opencv/issues/21326
highgui: using builtin backend: WIN32UI
rgbd: Eigen support is disabled. Eigen is Required for Posegraph optimization
Could NOT find Doxygen (missing: DOXYGEN_EXECUTABLE) 

General configuration for OpenCV 4.8.0-dev =====================================
  Version control:               4.8.0-347-g617d7ff575

  Extra modules:
    Location (extra):            C:/home/code/repo/opencv_contrib/modules
    Version control (extra):     4.9.0-55-g7e1b089c

  Platform:
    Timestamp:                   2024-04-10T23:48:56Z
    Host:                        Windows 10.0.22631 AMD64
    CMake:                       3.29.0-rc3
    CMake generator:             MinGW Makefiles
    CMake build tool:            C:/Qt/Tools/mingw1310_64/bin/mingw32-make.exe
    Configuration:               Debug

  CPU/HW features:
    Baseline:                    SSE SSE2 SSE3
      requested:                 SSE3
    Dispatched code generation:  SSE4_1 SSE4_2 FP16 AVX AVX2 AVX512_SKX
      requested:                 SSE4_1 SSE4_2 AVX FP16 AVX2 AVX512_SKX
      SSE4_1 (16 files):         + SSSE3 SSE4_1
      SSE4_2 (1 files):          + SSSE3 SSE4_1 POPCNT SSE4_2
      FP16 (0 files):            + SSSE3 SSE4_1 POPCNT SSE4_2 FP16 AVX
      AVX (8 files):             + SSSE3 SSE4_1 POPCNT SSE4_2 AVX
      AVX2 (36 files):           + SSSE3 SSE4_1 POPCNT SSE4_2 FP16 FMA3 AVX AVX2
      AVX512_SKX (5 files):      + SSSE3 SSE4_1 POPCNT SSE4_2 FP16 FMA3 AVX AVX2 AVX_512F AVX512_COMMON AVX512_SKX

  C/C++:
    Built as dynamic libs?:      YES
    C++ standard:                11
    C++ Compiler:                C:/Qt/Tools/mingw1310_64/bin/c++.exe  (ver 13.1.0)
    C++ flags (Release):         -fsigned-char -W -Wall -Wreturn-type -Wnon-virtual-dtor -Waddress -Wsequence-point -Wformat -Wformat-security -Wmissing-declarations -Wundef -Winit-self -Wpointer-arith -Wshadow -Wsign-promo -Wuninitialized -Wno-delete-non-virtual-dtor -Wno-comment -Wimplicit-fallthrough=3 -Wno-strict-overflow -fdiagnostics-show-option -Wno-long-long -fomit-frame-pointer -ffunction-sections -fdata-sections  -msse -msse2 -msse3 -fvisibility=hidden -fvisibility-inlines-hidden -O3 -DNDEBUG  -DNDEBUG -g1
    C++ flags (Debug):           -fsigned-char -W -Wall -Wreturn-type -Wnon-virtual-dtor -Waddress -Wsequence-point -Wformat -Wformat-security -Wmissing-declarations -Wundef -Winit-self -Wpointer-arith -Wshadow -Wsign-promo -Wuninitialized -Wno-delete-non-virtual-dtor -Wno-comment -Wimplicit-fallthrough=3 -Wno-strict-overflow -fdiagnostics-show-option -Wno-long-long -fomit-frame-pointer -ffunction-sections -fdata-sections  -msse -msse2 -msse3 -fvisibility=hidden -fvisibility-inlines-hidden -g  -O0 -DDEBUG -D_DEBUG
    C Compiler:                  C:/Qt/Tools/mingw1310_64/bin/gcc.exe
    C flags (Release):           -fsigned-char -W -Wall -Wreturn-type -Waddress -Wsequence-point -Wformat -Wformat-security -Wmissing-declarations -Wmissing-prototypes -Wstrict-prototypes -Wundef -Winit-self -Wpointer-arith -Wshadow -Wuninitialized -Wno-comment -Wimplicit-fallthrough=3 -Wno-strict-overflow -fdiagnostics-show-option -Wno-long-long -fomit-frame-pointer -ffunction-sections -fdata-sections  -msse -msse2 -msse3 -fvisibility=hidden -O3 -DNDEBUG  -DNDEBUG -g1
    C flags (Debug):             -fsigned-char -W -Wall -Wreturn-type -Waddress -Wsequence-point -Wformat -Wformat-security -Wmissing-declarations -Wmissing-prototypes -Wstrict-prototypes -Wundef -Winit-self -Wpointer-arith -Wshadow -Wuninitialized -Wno-comment -Wimplicit-fallthrough=3 -Wno-strict-overflow -fdiagnostics-show-option -Wno-long-long -fomit-frame-pointer -ffunction-sections -fdata-sections  -msse -msse2 -msse3 -fvisibility=hidden -g  -O0 -DDEBUG -D_DEBUG
    Linker flags (Release):      -Wl,--gc-sections  
    Linker flags (Debug):        -Wl,--gc-sections  
    ccache:                      NO
    Precompiled headers:         YES
    Extra dependencies:          pthread
    3rdparty dependencies:

  OpenCV modules:
    To be built:                 aruco bgsegm bioinspired calib3d ccalib core datasets dnn dnn_objdetect dnn_superres dpm face features2d flann fuzzy gapi hfs highgui img_hash imgcodecs imgproc intensity_transform line_descriptor mcc ml objdetect optflow phase_unwrapping photo plot quality rapid reg rgbd saliency shape signal stereo stitching structured_light superres surface_matching text tracking video videostab wechat_qrcode xfeatures2d ximgproc xobjdetect xphoto
    Disabled:                    python_bindings_generator python_tests videoio world
    Disabled by dependency:      ts
    Unavailable:                 alphamat cannops cudaarithm cudabgsegm cudacodec cudafeatures2d cudafilters cudaimgproc cudalegacy cudaobjdetect cudaoptflow cudastereo cudawarping cudev cvv freetype hdf java julia matlab ovis python2 python3 sfm viz
    Applications:                examples apps
    Documentation:               NO
    Non-free algorithms:         NO

  Windows RT support:            NO

  GUI:                           WIN32UI
    QT:                          NO
    Win32 UI:                    YES
    OpenGL support:              YES (opengl32 glu32)
    VTK support:                 NO

  Media I/O: 
    ZLib:                        build (ver 1.2.13)
    JPEG:                        build-libjpeg-turbo (ver 2.1.3-62)
      SIMD Support Request:      YES
      SIMD Support:              NO
    WEBP:                        build (ver encoder: 0x020f)
    PNG:                         build (ver 1.6.37)
    TIFF:                        build (ver 42 - 4.2.0)
    JPEG 2000:                   build (ver 2.5.0)
    OpenEXR:                     build (ver 2.3.0)
    HDR:                         YES
    SUNRASTER:                   YES
    PXM:                         YES
    PFM:                         YES

  Video I/O:
    DC1394:                      NO
    FFMPEG:                      YES (prebuilt binaries)
      avcodec:                   YES (58.134.100)
      avformat:                  YES (58.76.100)
      avutil:                    YES (56.70.100)
      swscale:                   YES (5.9.100)
      avresample:                YES (4.0.0)
    GStreamer:                   NO
    DirectShow:                  YES

  Parallel framework:            pthreads

  Trace:                         YES (built-in)

  Other third-party libraries:
    Lapack:                      NO
    Eigen:                       NO
    Custom HAL:                  NO
    Protobuf:                    build (3.19.1)
    Flatbuffers:                 builtin/3rdparty (23.5.9)

  OpenCL:                        YES (NVD3D11)
    Include path:                C:/home/code/repo/opencv/3rdparty/include/opencl/1.2
    Link libraries:              Dynamic load

  Python (for build):            NO

  Install to:                    C:/home/code/temp/OpenCV4/build/install
-----------------------------------------------------------------

Configuring done (8.1s)```

```

## Generate

```
Detected processor: AMD64
CMake Warning (dev) at cmake/OpenCVUtils.cmake:144 (find_package):
  Policy CMP0148 is not set: The FindPythonInterp and FindPythonLibs modules
  are removed.  Run "cmake --help-policy CMP0148" for policy details.  Use
  the cmake_policy command to set the policy and suppress this warning.

Call Stack (most recent call first):
  cmake/OpenCVDetectPython.cmake:64 (find_host_package)
  cmake/OpenCVDetectPython.cmake:271 (find_python)
  CMakeLists.txt:650 (include)
This warning is for project developers.  Use -Wno-dev to suppress it.

Could NOT find PythonInterp (missing: PYTHON_EXECUTABLE) (Required is at least version "2.7")
CMake Warning (dev) at cmake/OpenCVUtils.cmake:144 (find_package):
  Policy CMP0148 is not set: The FindPythonInterp and FindPythonLibs modules
  are removed.  Run "cmake --help-policy CMP0148" for policy details.  Use
  the cmake_policy command to set the policy and suppress this warning.

Call Stack (most recent call first):
  cmake/OpenCVDetectPython.cmake:64 (find_host_package)
  cmake/OpenCVDetectPython.cmake:280 (find_python)
  CMakeLists.txt:650 (include)
This warning is for project developers.  Use -Wno-dev to suppress it.

Could NOT find PythonInterp (missing: PYTHON_EXECUTABLE) (Required is at least version "3.2")
libjpeg-turbo: VERSION = 2.1.3, BUILD = opencv-4.8.0-dev-libjpeg-turbo-debug
libjpeg-turbo(SIMD): SIMD extensions disabled: could not find NASM compiler.  Performance will suffer.
Could NOT find OpenJPEG (minimal suitable version: 2.0, recommended version >= 2.3.1). OpenJPEG will be built from sources
OpenJPEG: VERSION = 2.5.0, BUILD = opencv-4.8.0-dev-openjp2-2.5.0-debug
OpenJPEG libraries will be built from sources: libopenjp2 (version "2.5.0")
Could not find OpenBLAS include. Turning OpenBLAS_FOUND off
Could not find OpenBLAS lib. Turning OpenBLAS_FOUND off
Could NOT find BLAS (missing: BLAS_LIBRARIES) 
Could NOT find LAPACK (missing: LAPACK_LIBRARIES) 
    Reason given by package: LAPACK could not be found because dependency BLAS could not be found.

VTK is not found. Please set -DVTK_DIR in CMake to VTK build directory, or to VTK install subdirectory with VTKConfig.cmake file
Module opencv_alphamat disabled because the following dependencies are not found: Eigen
freetype2:   NO
harfbuzz:    NO
Julia not found. Not compiling Julia Bindings. 
Module opencv_ovis disabled because OGRE3D was not found
No preference for use of exported gflags CMake configuration set, and no hints for include/library directories provided. Defaulting to preferring an installed/exported gflags CMake configuration if available.
Failed to find installed gflags CMake configuration, searching for gflags build directories exported with CMake.
Failed to find gflags - Failed to find an installed/exported CMake configuration for gflags, will perform search for installed gflags components.
Failed to find gflags - Could not find gflags include directory, set GFLAGS_INCLUDE_DIR to directory containing gflags/gflags.h
Failed to find glog - Could not find glog include directory, set GLOG_INCLUDE_DIR to directory containing glog/logging.h
Module opencv_sfm disabled because the following dependencies are not found: Eigen Glog/Gflags
Tesseract:   NO
Module opencv_ts disabled because opencv_videoio dependency can't be resolved!
Consider adding OPENCV_ALLOCATOR_STATS_COUNTER_TYPE=int/int64_t according to your build configuration
Excluding from source files list: modules/imgproc/src/imgwarp.lasx.cpp
Excluding from source files list: modules/imgproc/src/resize.lasx.cpp
Registering hook 'INIT_MODULE_SOURCES_opencv_dnn': C:/home/code/repo/opencv/modules/dnn/cmake/hooks/INIT_MODULE_SOURCES_opencv_dnn.cmake
opencv_dnn: filter out cuda4dnn source code
Excluding from source files list: <BUILD>/modules/dnn/layers/layers_common.rvv.cpp
Excluding from source files list: <BUILD>/modules/dnn/layers/layers_common.lasx.cpp
Excluding from source files list: <BUILD>/modules/dnn/int8layers/layers_common.lasx.cpp
Excluding from source files list: <BUILD>/modules/dnn/layers/cpu_kernels/conv_depthwise.rvv.cpp
Excluding from source files list: <BUILD>/modules/dnn/layers/cpu_kernels/conv_depthwise.lasx.cpp
Excluding from source files list: <BUILD>/modules/dnn/layers/cpu_kernels/fast_gemm_kernels.neon.cpp
Excluding from source files list: <BUILD>/modules/dnn/layers/cpu_kernels/fast_gemm_kernels.lasx.cpp
imgcodecs: OpenEXR codec is disabled in runtime. Details: https://github.com/opencv/opencv/issues/21326
highgui: using builtin backend: WIN32UI
rgbd: Eigen support is disabled. Eigen is Required for Posegraph optimization
Could NOT find Doxygen (missing: DOXYGEN_EXECUTABLE) 

General configuration for OpenCV 4.8.0-dev =====================================
  Version control:               4.8.0-347-g617d7ff575

  Extra modules:
    Location (extra):            C:/home/code/repo/opencv_contrib/modules
    Version control (extra):     4.9.0-55-g7e1b089c

  Platform:
    Timestamp:                   2024-04-10T23:48:56Z
    Host:                        Windows 10.0.22631 AMD64
    CMake:                       3.29.0-rc3
    CMake generator:             MinGW Makefiles
    CMake build tool:            C:/Qt/Tools/mingw1310_64/bin/mingw32-make.exe
    Configuration:               Debug

  CPU/HW features:
    Baseline:                    SSE SSE2 SSE3
      requested:                 SSE3
    Dispatched code generation:  SSE4_1 SSE4_2 FP16 AVX AVX2 AVX512_SKX
      requested:                 SSE4_1 SSE4_2 AVX FP16 AVX2 AVX512_SKX
      SSE4_1 (16 files):         + SSSE3 SSE4_1
      SSE4_2 (1 files):          + SSSE3 SSE4_1 POPCNT SSE4_2
      FP16 (0 files):            + SSSE3 SSE4_1 POPCNT SSE4_2 FP16 AVX
      AVX (8 files):             + SSSE3 SSE4_1 POPCNT SSE4_2 AVX
      AVX2 (36 files):           + SSSE3 SSE4_1 POPCNT SSE4_2 FP16 FMA3 AVX AVX2
      AVX512_SKX (5 files):      + SSSE3 SSE4_1 POPCNT SSE4_2 FP16 FMA3 AVX AVX2 AVX_512F AVX512_COMMON AVX512_SKX

  C/C++:
    Built as dynamic libs?:      YES
    C++ standard:                11
    C++ Compiler:                C:/Qt/Tools/mingw1310_64/bin/c++.exe  (ver 13.1.0)
    C++ flags (Release):         -fsigned-char -W -Wall -Wreturn-type -Wnon-virtual-dtor -Waddress -Wsequence-point -Wformat -Wformat-security -Wmissing-declarations -Wundef -Winit-self -Wpointer-arith -Wshadow -Wsign-promo -Wuninitialized -Wno-delete-non-virtual-dtor -Wno-comment -Wimplicit-fallthrough=3 -Wno-strict-overflow -fdiagnostics-show-option -Wno-long-long -fomit-frame-pointer -ffunction-sections -fdata-sections  -msse -msse2 -msse3 -fvisibility=hidden -fvisibility-inlines-hidden -O3 -DNDEBUG  -DNDEBUG -g1
    C++ flags (Debug):           -fsigned-char -W -Wall -Wreturn-type -Wnon-virtual-dtor -Waddress -Wsequence-point -Wformat -Wformat-security -Wmissing-declarations -Wundef -Winit-self -Wpointer-arith -Wshadow -Wsign-promo -Wuninitialized -Wno-delete-non-virtual-dtor -Wno-comment -Wimplicit-fallthrough=3 -Wno-strict-overflow -fdiagnostics-show-option -Wno-long-long -fomit-frame-pointer -ffunction-sections -fdata-sections  -msse -msse2 -msse3 -fvisibility=hidden -fvisibility-inlines-hidden -g  -O0 -DDEBUG -D_DEBUG
    C Compiler:                  C:/Qt/Tools/mingw1310_64/bin/gcc.exe
    C flags (Release):           -fsigned-char -W -Wall -Wreturn-type -Waddress -Wsequence-point -Wformat -Wformat-security -Wmissing-declarations -Wmissing-prototypes -Wstrict-prototypes -Wundef -Winit-self -Wpointer-arith -Wshadow -Wuninitialized -Wno-comment -Wimplicit-fallthrough=3 -Wno-strict-overflow -fdiagnostics-show-option -Wno-long-long -fomit-frame-pointer -ffunction-sections -fdata-sections  -msse -msse2 -msse3 -fvisibility=hidden -O3 -DNDEBUG  -DNDEBUG -g1
    C flags (Debug):             -fsigned-char -W -Wall -Wreturn-type -Waddress -Wsequence-point -Wformat -Wformat-security -Wmissing-declarations -Wmissing-prototypes -Wstrict-prototypes -Wundef -Winit-self -Wpointer-arith -Wshadow -Wuninitialized -Wno-comment -Wimplicit-fallthrough=3 -Wno-strict-overflow -fdiagnostics-show-option -Wno-long-long -fomit-frame-pointer -ffunction-sections -fdata-sections  -msse -msse2 -msse3 -fvisibility=hidden -g  -O0 -DDEBUG -D_DEBUG
    Linker flags (Release):      -Wl,--gc-sections  
    Linker flags (Debug):        -Wl,--gc-sections  
    ccache:                      NO
    Precompiled headers:         YES
    Extra dependencies:          pthread
    3rdparty dependencies:

  OpenCV modules:
    To be built:                 aruco bgsegm bioinspired calib3d ccalib core datasets dnn dnn_objdetect dnn_superres dpm face features2d flann fuzzy gapi hfs highgui img_hash imgcodecs imgproc intensity_transform line_descriptor mcc ml objdetect optflow phase_unwrapping photo plot quality rapid reg rgbd saliency shape signal stereo stitching structured_light superres surface_matching text tracking video videostab wechat_qrcode xfeatures2d ximgproc xobjdetect xphoto
    Disabled:                    python_bindings_generator python_tests videoio world
    Disabled by dependency:      ts
    Unavailable:                 alphamat cannops cudaarithm cudabgsegm cudacodec cudafeatures2d cudafilters cudaimgproc cudalegacy cudaobjdetect cudaoptflow cudastereo cudawarping cudev cvv freetype hdf java julia matlab ovis python2 python3 sfm viz
    Applications:                examples apps
    Documentation:               NO
    Non-free algorithms:         NO

  Windows RT support:            NO

  GUI:                           WIN32UI
    QT:                          NO
    Win32 UI:                    YES
    OpenGL support:              YES (opengl32 glu32)
    VTK support:                 NO

  Media I/O: 
    ZLib:                        build (ver 1.2.13)
    JPEG:                        build-libjpeg-turbo (ver 2.1.3-62)
      SIMD Support Request:      YES
      SIMD Support:              NO
    WEBP:                        build (ver encoder: 0x020f)
    PNG:                         build (ver 1.6.37)
    TIFF:                        build (ver 42 - 4.2.0)
    JPEG 2000:                   build (ver 2.5.0)
    OpenEXR:                     build (ver 2.3.0)
    HDR:                         YES
    SUNRASTER:                   YES
    PXM:                         YES
    PFM:                         YES

  Video I/O:
    DC1394:                      NO
    FFMPEG:                      YES (prebuilt binaries)
      avcodec:                   YES (58.134.100)
      avformat:                  YES (58.76.100)
      avutil:                    YES (56.70.100)
      swscale:                   YES (5.9.100)
      avresample:                YES (4.0.0)
    GStreamer:                   NO
    DirectShow:                  YES

  Parallel framework:            pthreads

  Trace:                         YES (built-in)

  Other third-party libraries:
    Lapack:                      NO
    Eigen:                       NO
    Custom HAL:                  NO
    Protobuf:                    build (3.19.1)
    Flatbuffers:                 builtin/3rdparty (23.5.9)

  OpenCL:                        YES (NVD3D11)
    Include path:                C:/home/code/repo/opencv/3rdparty/include/opencl/1.2
    Link libraries:              Dynamic load

  Python (for build):            NO

  Install to:                    C:/home/code/temp/OpenCV4/build/install
-----------------------------------------------------------------

Configuring done (8.1s)
Generating done (9.5s)
```
