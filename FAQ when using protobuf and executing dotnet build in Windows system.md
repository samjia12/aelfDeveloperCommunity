# FAQ when using protobuf and executing dotnet build in Windows system

Thie file：

Operating Environment

```bash

 os：windows10 Family-Chinese version x64
 node：v10.15.1
 npm: 6.4.1
 dotnet-sdk: 2.2.300
```

Hardware Environment 

```bash

    CPU: Intel Core i5-8250U
    RAM: 8GB
    Disk：256GB
```

## Problem Description 

```bash
google/protobuf/timestamp.proto: File not found.
```
After download protobuf and decompress it, there are two folders in the protoc folder: ```bin``` and ```include```

IF we only place ```bin\protoc.exe```  to  ```C:\WINDOWS\```, it will not find the corresponding dependency of include, and it will report error "file not found error" . Copy and paste "include" folder will fix this error.


Note：

1. Windows will search for ```C:\WINDOWS\protoc``` first, and then look for protoc path configured in the environment variable.

2. Execute ```ps1``` in window10 requires additional operations.

AELF provides three simple solutions for everyone to use. The specific scripts and scenarios are as follows.

## 1. Install.ps1 Script

Run ```chain/scripts/install.ps1```

<!-- *有开发者反馈运行脚本后编译找不到proto文件，你可以通过另外两种方式运行，详情见 ```手动安装 protoc & unzip``` ```使用 install_protoc.ps1 脚本``` -->

<!-- 如果你不想自己手动安装protoc 也不想重新下载新的脚本文件，那么你可以通过编辑 install.ps1 脚本文件来实现环境的搭建 -->

```ps1
    [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12

    if(Test-Path C:\protoc\bin\protoc.exe) {
        cp C:\protoc\include C:\WINDOWS\;
        cp C:\protoc\bin\protoc.exe  C:\WINDOWS\;
        protoc --version;
        exit 100;
    }
    else {
        wget https://github.com/protocolbuffers/protobuf/releases/download/v3.7.0/protoc-3.7.0-win64.zip -OutFile C:\protoc-3.7.0-win64.zip;
        Expand-Archive -Path C:\protoc-3.7.0-win64.zip -DestinationPath C:\protoc;
        cp C:\protoc\include C:\WINDOWS\;  
        cp C:\protoc\bin\protoc.exe  C:\WINDOWS\;
        protoc --version;
        exit 0;
    };
```

<!-- 然后删除掉```C:\WINDOWS\``` 目录下的 protoc.exe 重新执行脚本即可。 -->

## 2. USe install_protoc.ps1 Script

You can find ```install_protoc.ps1``` script file in ```XXXXXXXXwill edit this laterXXXXXXXXXXXX``` Group Folder，Download it to any directory (full English path) and execute it. (Execution method is the same as ```install.ps1```)

Please make sure your ```C:\WINDOWS``` directory does not include any ```protoc.exe``` or ```include``` file，because windows will execute ```protoc``` in the ```C:\WINDOWS``` directory by default, it may cause your compilation to fail.

Note: The ```chain/scripts/install_choco.ps1``` script in the codebase is same as the script ```install_protoc.ps1``` script in the group folder; choco is the package management tool for windows.

## 3. Install protoc & unzip Manually

### 1. Download protoc Manually
 
Download Link: https://github.com/protocolbuffers/protobuf/releases/tag/v3.7.0

1. Download ```protoc-3.7.0-win64/32``` according to the system to determine which version to download

2. Decompress it to any directory (path needs to be all English)

3. Set environment variables (decompress directory /bin)

### 2. Download unzip Manually

Download Link: https://sourceforge.net/projects/gnuwin32/files/unzip/5.51-1/unzip-5.51-1.exe/download?use_mirror=nchc&download=

1. Install it to any directory (path needs to be all English)

2. Set environment variables Installation directory /bin

## 3. Compile project

1. Execution

```shell
    cd chain/src/AElf.Boilerplate.Launcher/
    dotnet build
```

If there is no error after compile is completed, it means the compilation is successful (yellow warning does not affect the program)

If it said ```xxx is not an internal command or an external command```
, check if your environment variable is correct.

If it said ```xxx is inaccessible by the process```, please close all ```dotnet``` programs in Task Manager and re-execute the above command.


```sell
    dotnet run bin/Debug/netcoreapp2.2/AElf.Boilerplate.Launcher
```

Executing this command, if there is no error reported which means your execution is successful 
