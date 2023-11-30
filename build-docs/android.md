# 编译（使用3800x上面的cv2容器）
cd /opencvsharp && mkdir make && cd make

## x86_64
cmake -D CMAKE_INSTALL_PREFIX=/opencvsharp/make   -DCMAKE_TOOLCHAIN_FILE=/android-ndk-r25c/build/cmake/android.toolchain.cmake   -DANDROID_ABI=x86_64   -DANDROID_PLATFORM=21   -DANDROID_STL=c++_static   -DOpenCV_DIR=/OpenCV-android-sdk/sdk/native/jni   -DCMAKE_MODULE_PATH=/opencv/cmake   /opencvsharp/src

make -j16

# 编译好之后确认
/android-ndk-r25c/toolchains/llvm/prebuilt/linux-x86_64/bin/llvm-readelf -d /opencvsharp/make/OpenCvSharpExtern/libOpenCvSharpExtern.so

# strip
/android-ndk-r25c/toolchains/llvm/prebuilt/linux-x86_64/bin/llvm-strip /opencvsharp/make/OpenCvSharpExtern/libOpenCvSharpExtern.so

# 拷到父级Linux：
## x64
docker cp cv2:/opencvsharp/make/OpenCvSharpExtern/libOpenCvSharpExtern.so ~/artifacts/cvsharp/android-x64
