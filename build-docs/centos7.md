# 在CentOS7上编译OpenCvSharp

# 安装较新的gcc版本：
yum install centos-release-scl -y && yum install devtoolset-9-gcc devtoolset-9-gcc-c++ devtoolset-9-binutils -y && source scl_source enable devtoolset-9

# 确认gcc版本是否提高了
gcc --version

# 安装cmake3、gcc9和其它必要东西
```bash
yum install epel-release -y && yum update -y && yum install -y \
  cmake3 \
  wget \
  unzip \
  ca-certificates \
  make \
  git
```

准备配置OpenCV：
```bash
OPENCV_VERSION=4.8.0
wget https://github.com/opencv/opencv/archive/${OPENCV_VERSION}.zip && \
    unzip ${OPENCV_VERSION}.zip && \
    rm -f ${OPENCV_VERSION}.zip && \
    mv opencv-${OPENCV_VERSION} opencv && \
    wget https://github.com/opencv/opencv_contrib/archive/${OPENCV_VERSION}.zip && \
    unzip ${OPENCV_VERSION}.zip && \
    rm -f ${OPENCV_VERSION}.zip && \
    mv opencv_contrib-${OPENCV_VERSION} opencv_contrib
cd opencv && mkdir build && cd build && \
    cmake3 \
    -D CMAKE_BUILD_TYPE=RELEASE \
    -D OPENCV_EXTRA_MODULES_PATH=/opencv_contrib/modules \
    -D BUILD_SHARED_LIBS=OFF \
    -D ENABLE_CXX11=ON \
    -D BUILD_EXAMPLES=OFF \
    -D BUILD_DOCS=OFF \
    -D BUILD_PERF_TESTS=OFF \
    -D BUILD_TESTS=OFF \
    -D BUILD_JAVA=OFF \
    -D BUILD_LIST=core,imgproc,imgcodecs \
    -D BUILD_PNG=ON \
    -D BUILD_TIFF=ON \
    -D WITH_GSTREAMER=OFF \
    -D WITH_ADE=OFF \
    -D WITH_FFMPEG=OFF \
    -D WITH_V4L=OFF \
    -D WITH_1394=OFF \
    -D WITH_GTK=OFF \
    -D WITH_OPENEXR=OFF \
    -D WITH_PROTOBUF=OFF \
    -D WITH_QUIRC=OFF \
    -D OPENCV_ENABLE_NONFREE=ON \
    ..
```

# 在默认的centos7-arm64中，webp编译不了，因为是gcc4，升级到gcc9试试 
# 编译OpenCV：
make -j$(nproc)

# 下载并准备OpenCvSharp
```bash
cd / && git clone https://github.com/shimat/opencvsharp.git && cd opencvsharp && git checkout 4.8.0.20230711
sed -i '42s/.*/ /;44,70s/.*/ /' /opencvsharp/src/OpenCvSharpExtern/include_opencv.h
sed -i '451,585s/.*/ /' /opencvsharp/src/OpenCvSharpExtern/std_vector.h
sed -i '12s/.*/file(GLOB OPENCVSHARP_FILES core*.cpp imgp*.cpp imgc*.cpp std*.cpp)/' /opencvsharp/src/OpenCvSharpExtern/CMakeLists.txt
mkdir /opencvsharp/make && cd /opencvsharp/make && \
cmake3 \
  -D CMAKE_INSTALL_PREFIX=/opencvsharp/make \
  -D OpenCV_DIR=/opencv/build \
    /opencvsharp/src
make -j$(nproc)
ls -l /opencvsharp/make/OpenCvSharpExtern/libOpenCvSharpExtern.so
strip /opencvsharp/make/OpenCvSharpExtern/libOpenCvSharpExtern.so
ls -l /opencvsharp/make/OpenCvSharpExtern/libOpenCvSharpExtern.so
ldd /opencvsharp/make/OpenCvSharpExtern/libOpenCvSharpExtern.so
```


# 从docker拷到外面来（从外面的机子运行）
```bash
mkdir ~/artifacts/cvsharp/centos7-arm64 && ~/artifacts/cvsharp/centos7-arm64
docker cp cvsharp-centos7:/opencvsharp/make/OpenCvSharpExtern/libOpenCvSharpExtern.so .
```

# 从新机子测试
```bash
docker run -it --rm --name cvsharp-centos7-test centos:7
yum update -y && yum install -y gcc
mkdir /mylib
```

## 然后将之前的libOpenCvSharpExtern.so拷到docker中：
docker cp libOpenCvSharpExtern.so cvsharp-centos7-test:/mylib/

## docker运行test.c
```bash
echo '#include <stdio.h>
int core_Mat_sizeof();
int main()
{
        int i = core_Mat_sizeof();
        printf("sizeof(Mat) = %d\n", i);
        return 0;
}' > /test.c
gcc test.c -L/mylib -lOpenCvSharpExtern -o test
./test # 由于没有链接到libOpenCvSharpExtern.so，所以肯定无法运行
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/mylib ./test # 可以运行，期望输出sizeof(Mat) = 96
```
