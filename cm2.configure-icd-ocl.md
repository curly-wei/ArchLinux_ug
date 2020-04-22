# CM2. Configure icd-ocl

## 1.Windows

### 1-1. Install your VGA driver

### 1-2. Install WDK

[download_WDK](https://docs.microsoft.com/en-us/windows-hardware/drivers/download-the-wdk)

### 1-3. Download opencl-headers

```bash
git clone https://github.com/KhronosGroup/OpenCL-Headers.git
```

### 1-4. Build opencl-ICD

#### 1-4-1. Download ocl-icd

```bash
git clone https://github.com/KhronosGroup/OpenCL-ICD-Loader.git
```

#### 1-4-2. Copy opencl-headers to ocl-icd source-code dir\(OpenCL-ICD-Loader\)

```bash
cp -r ~/Downloads/OpenCL-Headers-master/CL ~/Downloads/OpenCL-ICD-Loader-master/loader
```

#### 1-4-3. cd to dir && create dir for build

```text
 cd OpenCL-ICD-Loader
 mkdir build
 cd build
```

#### 1-4-4. Configure cmake and build

```text
cmake.exe -DBUILD_TESTING=OFF -G "Visual Studio 16 2019" -A x64 ..
```

```text
MSBuild.exe OpenCL.sln /property:Configuration=Release /property:Platform=x64
```

#### 1-4-5. Create dir for package this SDK

```bash
mkdir ~/Downloads/ocl-icd/bin
mkdir ~/Downloads/ocl-icd/lib
mkdir ~/Downloads/ocl-icd/include
cp -r ~/Downloads/OpenCL-ICD-Loader-master/build/Release/OpenCL.dll ~/Downloads/ocl-icd/bin
cp -r ~/Downloads/OpenCL-ICD-Loader-master/build/Release/OpenCL.lib ~/Downloads/ocl-icd/lib
cp -r~/Downloads/OpenCL-Headers-master/CL  ~/Downloads/ocl-icd/include
```

#### 1-4-6. Create OpenCLConfig.cmake

```text
set(OpenCL_ROOT_DIR ${CMAKE_CURRENT_LIST_DIR})

find_path(OpenCL_INCLUDE_DIR NAMES CL/cl.h PATHS "${OpenCL_ROOT_DIR}/include")
mark_as_advanced(OpenCL_INCLUDE_DIR)
find_library(OpenCL_LIBRARY NAMES OpenCL.lib PATHS "${OpenCL_ROOT_DIR}/lib")
mark_as_advanced(OpenCL_LIBRARY)
set(OpenCL_INCLUDE_DIRS "${OpenCL_INCLUDE_DIR}")
set(OpenCL_LIBRARIES ${OpenCL_LIBRARY})

message(STATUS "Found OpenCL, version is: ${OpenCL_VERSION}")
message(STATUS "OpenCL Include dir. is: ${OpenCL_INCLUDE_DIR}")
message(STATUS "OpenCL Libs is: ${OpenCL_LIBRARY}")
```

Copy OpenCLConfig.cmake to `~/Downloads/ocl-icd`

#### 1-4-7. Create OpenCLConfigVersion.cmake

```text
set(OpenCL_VERSION 2.2)
set(PACKAGE_VERSION ${OpenCL_VERSION})

set(PACKAGE_VERSION_EXACT False)
set(PACKAGE_VERSION_COMPATIBLE False)

if(PACKAGE_FIND_VERSION VERSION_EQUAL PACKAGE_VERSION)
  set(PACKAGE_VERSION_EXACT True)
  set(PACKAGE_VERSION_COMPATIBLE True)
endif()

if(PACKAGE_FIND_VERSION_MAJOR EQUAL 2
   AND PACKAGE_FIND_VERSION VERSION_LESS PACKAGE_VERSION)
  set(PACKAGE_VERSION_COMPATIBLE True)
endif()
```

Copy OpenCLConfigVersion.cmake to `~/Downloads/ocl-icd`
