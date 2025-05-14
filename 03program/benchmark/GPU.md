# CUDA

可以使用 NVIDIA Nsight Compute 来对程序的运行进行分析：
- 该软件可以在 windows 上安装，然后从 linux 上得到日志文件，将日志文件在 windows 上打开进行分析
- 官方网站：[Getting Started with Nsight Compute | NVIDIA Developer](https://developer.nvidia.com/tools-overview/nsight-compute/get-started)

同类型的还有 Nsight System
- 同样在 linux 上执行一个 `nsys` 的分析，然后产生一个文件
- 比较快，生成两个文件
- 可以下载文件在 windows 上分析，查看不同流的情况