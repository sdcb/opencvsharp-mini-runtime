# 启动容器：
docker run -it --rm --name cvsharp-test-centos7 centos:7

# 安装dotnet 7
rpm -Uvh https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm
yum install dotnet-sdk-7.0 -y

# 安装相关OpenVINO依赖以及ca-certificates
yum install -y epel-release
yum install -y ca-certificates wget pugixml-devel

wget https://storage.openvinotoolkit.org/repositories/openvino/packages/2023.1/linux/l_openvino_toolkit_centos7_2023.1.0.12185.47b736f63ed_x86_64.tgz
mkdir /tbb-temp
tar -xvzf l_openvino_toolkit_centos7_2023.1.0.12185.47b736f63ed_x86_64.tgz -C /tbb-temp/
cp /tbb-temp/l_openvino_toolkit_centos7_2023.1.0.12185.47b736f63ed_x86_64/runtime/3rdparty/tbb/lib/libtbb.so.12.2 /lib64/libtbb.so.12
rm -f l_openvino_toolkit_centos7_2023.1.0.12185.47b736f63ed_x86_64.tgz
rm -rf /tbb-temp


mkdir /ocr-test && cd /ocr-test && dotnet new console
dotnet add package Sdcb.OpenVINO
dotnet add package Sdcb.OpenVINO.PaddleOCR
dotnet add package Sdcb.OpenVINO.PaddleOCR.Models.Online
dotnet add package Sdcb.OpenVINO.runtime.centos.7-x64
dotnet add package Sdcb.OpenCvSharp4.mini.runtime.centos.7-x64 -v 4.8.0.20230708-preview.2 -s https://proget.starworks.cc:88/nuget/test/v3/index.json

echo 'using OpenCvSharp;
using Sdcb.OpenVINO;
using Sdcb.OpenVINO.PaddleOCR;
using Sdcb.OpenVINO.PaddleOCR.Models;
using Sdcb.OpenVINO.PaddleOCR.Models.Online;

FullOcrModel model = await OnlineFullModels.ChineseV4.DownloadAsync();
using Mat src = Cv2.ImDecode(await new HttpClient().GetByteArrayAsync("https://io.starworks.cc:88/paddlesharp/ocr/samples/xdr5450.webp"), ImreadModes.Color);
using PaddleOcrAll all = new(model, new DeviceOptions("CPU"))
{
    Enable180Classification = true,
    AllowRotateDetection = true,
};
PaddleOcrResult result = all.Run(src);
Console.WriteLine($"检测结果：\n{result.Text}");
' > Program.cs
dotnet run
