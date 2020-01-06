# **第一章 MobiusPi Python开发快速入门**
MobiusPi是北京映翰通网络技术股份有限公司InGateway系列软硬件产品的代号。  <br/>InGateway系列产品包含两个大的产品系列，InGateway900和InGateway500系列。本文档以InGateway500系列产品为例为用户演示如何进行MobiusPi Python开发， 以下文档中将InGateway500简称为“IG500”。
## 第一节 搭建MobiusPi开发环境
### 1. 准备IG500硬件设备及其网络环境
#### 1.1 接通IG500电源并使用网线连接PC
接通IG500的电源并按照拓扑使用以太网线连接PC和IG500。  <br/>
![](./images/2019-11-29-15-54-55.png)
#### 1.2 设置LAN网络参数：在局域网访问IG500
- 步骤1：IG500的FE 0/1口的默认ip地址为192.168.1.1，设置PC的IP地址与FE 0/1口处于同一网段。  
  - 方法一：自动获取IP地址（推荐）  

     ![](./images/2019-11-07-10-36-47.png) <br/>
 &nbsp;


  - 方法二：使用固定IP地址  <br/>
    设置PC和IG500的FE 0/1口处于同一网段。选择“使用下面的IP地址”，输入IP地址（默认为192.168.1.2~192.168.1.254中任意值）；子网掩码（默认255.255.255.0）；默认网关（默认为192.168.1.1）以及DNS服务器地址，单击<确定>。  

    ![](./images/2019-11-29-16-00-56.png)   
<br/>

- 步骤2：打开浏览器，访问IG500的FE 0/1口IP地址并输入登录用户名和密码。设备出厂的用户名/密码默认为adm/123456。
![](./images/2019-12-02-09-53-06.png)   
 &nbsp;

- 步骤3：登录成功后，您可以看到如下图所示的网页。
![](./images/2019-12-02-10-00-22.png)   
 &nbsp;

- 步骤4：如需修改WEB管理界面的用户名和密码可进入“系统管理>>用户管理”页面设置新的用户名和密码。
![](./images/2019-12-02-10-03-42.png)   
&nbsp;

- 步骤5：如需修改FE 0/1口的IP地址可访问“网络>>以太网接口>>配置以太网0/1”页面进行修改。
![](./images/2019-12-02-10-04-14.png)   

#### 1.3 设置IG500连接Internet
- 步骤1：将SIM卡插入卡槽（注意：插拔SIM卡操作时，必须拔掉电源，以免造成数据丢失或设备损坏）。插入SIM卡后将4G LTE天线与ANT口连接，接通IG500的电源。

  ![](./images/2019-11-29-16-18-51.png) <br/>
 &nbsp;

- 步骤2：进入“网络>>网络接口>>蜂窝网>>配置蜂窝网”页面，勾选“启用拨号”并点击提交。
![](./images/2019-12-03-14-19-26.png)
&nbsp;

  待网络连接状态显示为“连接”并且显示已分配相应IP地址等状态时说明IG500已通过SIM卡联网。  
![](./images/2019-12-04-10-00-36.png)

#### 1.4 更新IG500软件版本
如需获取IG500产品最新软件版本及其功能特性信息，请联系客服。如需更新IG500的固件或Python SDK版本，请参考如下方法。
- 更新IG500固件版本  <br/>
  点击“系统管理>>固件升级”，选择相应的固件文件后点击“开始升级”。IG500升级完成后，会提示重启设备以应用新的固件。
![](./images/2019-12-02-10-07-32.png)
 &nbsp;

- 更新IG500 Python SDK版本  <br/>
进入“边缘计算>>Python边缘计算>>引擎”页面，勾选“Python边缘计算引擎”并选择相应的SDK文件点击“升级”，IG500会自动完成升级操作。
![](./images/2019-12-02-10-11-07.png)

#### 1.5 启用IG500的调试模式
开发过程中，为了在IG500上运行并调试Python代码，需要启用IG500的调试模式。在“边缘计算>>Python边缘计算>>引擎”页面中，勾选“启用调试模式”，启用后可通过VS Code对IG500进行开发。
![](./images/2019-12-02-10-13-05.png)
 &nbsp;

启用调试模式后，IG500启动一个SSH Server，监听LAN网络(默认IP地址192.168.1.1)的222端口。SSH Server的用户名和密码将被显示到上述网页中。为了提高安全性，每次开启调试模式或重启设备，都会重新随机生成新的密码。

### 2. 安装PC上需要的软件
#### 2.1 安装Python解释器
在开发过程中PC需具备Python2.7.X或3.7.X解释器（建议使用3.7.X解释器），您可以访问 https://www.python.org/downloads/ 下载相应的安装包并安装至PC。
![](./images/2019-11-08-16-03-16.png)

#### 2.2 安装Visual Studio Code软件
您可以访问：https://code.visualstudio.com/Download 获取相应的Visual Studio Code软件（以下简称VS Code）。
![](./images/2019-11-29-15-28-59.png)
 &nbsp;

下载完成后运行安装程序，安装成功后打开VS Code软件，软件页面如下图。
![](./images/2019-11-29-15-35-23.png)
### 3. 准备VS Code开发环境
#### 3.1 安装VS Code扩展插件
为了在IG500上开发并调试Python代码，您要在VS Code IDE的“Extensions”中安装以下必需的扩展插件：  
- `Python`：一个拥有丰富的功能特性的VS Code Python扩展插件，包括诸如IntelliSense、linting、调试、代码导航、代码格式化、Jupyter笔记本支持、重构、变量资源管理器、测试资源管理器、代码片段等功能！想要了解跟多详细信息，请访问该插件的[官方网页](https://code.visualstudio.com/docs/languages/python)。  
- `Project Templates`：一个支持基于自定义模板快速创建新项目的VS Code扩展插件。我们会发布若干Python App模板，您可以使用Project Templates导入模板，并快速初始化项目。  
- `SFTP`：您可以使用SFTP Sync插件将代码上传至IG500中。
![](./images/2019-12-02-10-29-45.png)
![](./images/2019-12-02-10-30-54.png)
![](./images/2019-12-02-10-28-49.png)  
 &nbsp;

至此，MobiusPi边缘计算平台开发所必需的插件安装完成。想要了解更多VS Code插件，请访问[Visual Studio Code官网](https://code.visualstudio.com/)。

#### 3.2 配置Python解释器版本
使用快捷键：`Ctrl+Shift+P`弹出命令面板，在命令面板中输入`>Python: select Interpreter`。
![](./images/2019-12-02-10-42-26.png)
 &nbsp;

根据需要选择相应的Python解释器，本教程使用3.7.X版本的Python解释器（所选择的Python解释器版本应同“边缘计算>>Python边缘计算>>引擎”页面的Python解释器一致）。选择后在VS Code左下角可以看到已选择的Python解释器版本。
![](./images/2019-12-02-10-45-42.png)

#### 3.3 配置工程模板
##### 3.3.1 使用映翰通标准工程模板
- 步骤1：请从[这里](https://github.com/inhandnet/MobiuspiProjectTemplates/releases)下载MobiusPi工程模板。  </br>
MobiusPi提供多种工程模板以方便您快速初始化工程目录。各工程模板的详细说明请参考[README.md](https://github.com/inhandnet/MobiuspiProjectTemplates)。本教程使用标准工程模板“helloworld-template”进行演示说明。  
![](images/2019-12-25-09-39-17.png)
 &nbsp;

- 步骤2：打开工程模板。  </br>
解压下载后的工程模板压缩包，使用VS Code打开解压文件夹中的helloworld-template文件夹，点击“文件>>打开文件夹”并选择的“helloworld-template”文件夹。
![](./images/2019-12-02-11-00-38.png)
 &nbsp;

  打开工程模板文件夹“helloworld-template”后如下图所示，工程模板中包含以下内容：
  - `.vscode`：VS Code配置文件夹
    - `sftp.json`:SFTP插件的配置文件，用于与IG500建立SFTP连接
  - `build`：APP发布包文件夹
  - `src`：APP源码文件夹
    - `main.py`：APP入口
    - `parse_config.py`:解析APP配置文件
  - `config.yaml`：APP配置文件
  - `setup.py`:APP版本、SDK版本等信息说明

  ![](images/2019-12-27-09-54-32.png)
 &nbsp;

- 步骤3：在命令面板中输入`>Project:Save Project as Template`命令以将当前工程文件存为模板。
![](images/2019-12-27-09-55-10.png)
 &nbsp;

  定义您模板的名称，如：helloworld-template。
![](images/2019-12-27-09-56-06.png)

##### 3.3.2 自定义工程模板
- 步骤1：新建一个工程模板文件夹，文件夹中必须包含以下内容。其他文件可根据您的实际情况自行添加
  - `.vscode`：VS Code配置文件夹（在VS Code的命令面板中输入`>SFTP:Config` 命令可快速创建.vscode文件夹和sftp.json文件）
    - `sftp.json`:SFTP插件的配置文件，用于与IG500建立SFTP连接
  - `build`：APP发布包文件夹
  - `src`：APP源码文件夹
    - `main.py`：APP入口
  - `config.yaml`：APP配置文件，内容可自定义
  - `setup.py`:APP版本、SDK版本等信息说明，建议参照标准模板定义
   &nbsp;

- 步骤2：打开工程模板。
  使用VS Code打开自定义工程模板文件夹，点击“文件>>打开文件夹”并选择的自定义工程模板文件夹。详细说明请参考第一节中的“3.3.1 使用映翰通标准工程模板”。
 &nbsp;

- 步骤3：在命令面板中输入`>Project:Save Project as Template`命令以将当前工程文件存为模板。详细说明请参考第一节中的“3.3.1 使用映翰通标准工程模板”。

## 第二节 编写第一个MobiusPi App：Hello World
本教程以开发一个“HelloWorld”APP为例说明如何通过VS Code实现IG500 Python APP的开发。该APP具备在IG500中每10秒打印一条“hello world!”日志以及导入配置文件修改日志内容的功能。
### 1. 使用模板创建工程
- 步骤1：使用VS Code打开Python APP的工程文件夹，打开后如下图所示：
![](./images/2019-12-02-14-30-58.png)
 &nbsp;

- 步骤2：在命令面板中输入 `>Project:Create Project From Template`命令以通过已有模板快速创建工程目录。
![](./images/2019-12-05-13-31-26.png)
 &nbsp;

- 步骤3：输入helloworld-template模板的名称并回车。
![](images/2019-12-27-09-57-58.png)
 &nbsp;

  选择模板后VS Code会自动在当前工程目录下增加模板中包含的文件。
![](images/2019-12-27-09-59-42.png)

### 2. 编码
标准工程模板“helloworld-template”已经实现了在IG500中每10秒打印一条“hello world!”日志以及导入配置文件修改日志内容的功能。如需修改APP名称，请您参考下图修改main. py和setup.py中的代码。<font color=#FF0000>注意：Python APP名称中不能包含空格。</font>
![](images/2019-12-27-09-44-32.png)
![](./images/2019-12-09-16-06-37.png)

### 3. 调试
#### 3.1 建立SFTP连接
远程调试代码时需要先将本地代码上传到远程服务器（即IG500）。上传本地代码前需要确认IG500的调试模式已启用，启用调试模式后如下图所示：
![](./images/2019-12-02-14-48-31.png)
 &nbsp;

- 步骤1：打开`sftp.json`文件  <br/>
  在命令面板中输入`>SFTP:Config` 命令后打开`sftp.json`文件。
![](./images/2019-12-05-10-45-59.png)
 &nbsp;

- 步骤2：配置SFTP连接  <br/>
  在`sftp.json`文件中根据IG500“边缘计算>>Python边缘计算>>引擎”页面的连接参数配置SFTP连接。
  <font color=#FF0000>注意：Python APP名称应与mian. py中的APP名称保持一致。</font>

  ![](images/2020-01-03-16-19-29.png)
 &nbsp;

- 步骤3：配置完成并保存后在命令面板中输入`>SFTP:Open SSH in Terminal`以连接远端的服务器。
![](./images/2019-12-05-10-43-46.png)
 &nbsp;

- 步骤4：输入后命令面板会提示您需要输入SFTP服务器的IP地址（即“host”项内容）。
![](./images/2019-12-05-10-44-51.png)
 &nbsp;

- 步骤5：首次连接时“终端”窗口会提示您是否要继续连接，此时输入“yes”并回车。随后再次在命令面板中输入`>SFTP:Open SSH in Terminal`和SFTP服务器的IP地址。
![](./images/2019-12-05-16-56-59.png)
 &nbsp;

- 步骤6：“终端”窗口会提示您需要输入密码，您只需要将`sftp.json`文件中“password”项复制粘贴到此处即可。
![](./images/2019-12-05-10-47-06.png)
 &nbsp;

  成功与IG500建立SFTP连接后如下图所示：
![](./images/2019-12-05-10-48-21.png)

#### 3.2 调试代码
- 步骤1：同步代码  
  SFTP连接成功后，在左侧空白处右键选择“Sync Local->Remote”将代码同步到远程服务器，同步成功后本地修改或者删除代码时都会自动和远端服务器同步。
![](./images/2019-12-02-17-33-03.png)
 &nbsp;

  可以在TERMINAL窗口查看远程服务器是否已接收到相应的APP代码。在TERMINAL窗口输入以下命令查看已上传的APP文件夹信息：
  ```
  cd app  
  ls -l
  ```
  ![](./images/2019-12-05-11-15-01.png)
 &nbsp;

- 步骤2：在终端窗口调试脚本  
  同步代码后在终端窗口输入如下命令在IG500中立即执行脚本，执行脚本后在终端窗口查看执行结果：打印“hello world!”。
  ```
  python -m ptvsd --host 192.168.1.1 --port 3000 HelloWorld/src/main.py 
  ```
  - `192.168.1.1`为IG500的FE 0/1口的IP地址
  - `3000`为建议的调试端口号
  - `HelloWorld/src/main.py`为mian. py的执行路径，请根据您的当前位置适当调整

  IG500的Python开发环境内置了ptvsd依赖库用于远程调试代码，想要了解更多ptvsd插件的用法，请访问[ptvsd使用说明](https://github.com/microsoft/ptvsd/)。
  ![](images/2019-12-23-14-59-40.png)
 &nbsp;

- 步骤3：调试完成后在终端使用`Ctrl + C`快捷键终止调试。
![](images/2019-12-23-15-53-14.png)

### 4. 构建APP发布包
调试完毕后可以构建APP发布包以便于将APP快速部署至其他IG500。
- 步骤1：构建APP发布包  <br/>
  在“终端”窗口执行`build_py_app.sh HelloWorld`命令构建APP发布包。（即build_py_app.sh 工程名称）
![](./images/2019-12-05-13-16-10.png)
 &nbsp;

- 步骤2：下载APP发布包  <br/>
  执行完成后在远程服务器的build目录下会自动生成APP发布包。右键本地的“build”文件夹并选择“Download Folder”将构建好的APP发布包下载到本地以便于后续部署。
![](./images/2019-12-05-13-17-42.png)
 &nbsp;

  下载完成后在build目录下可以看到HelloWorld APP发布包。
![](./images/2019-12-05-13-20-40.png)

### 5. 通过InGateway Web页面部署App
执行构建APP发布包命令后会自动在已连接的IG500上安装对应的APP。同时您还可以访问其他IG500的“边缘计算>>Python边缘计算>>应用>>配置”页面导入并上传APP发布包将APP部署到其他IG500上。部署方法如下：
- 步骤1：上传APP  <br/>
  在IG500的“边缘计算>>Python边缘计算>>应用>>配置”页面点击“添加”按钮。
![](./images/2019-12-04-13-15-46.png)
 &nbsp;

  选择“build”目录下的HelloWorld发布包。
![](./images/2019-12-04-13-14-57.png)
 &nbsp;

- 步骤2：启用APP  <br/>
  上传完成后勾选“启用”HelloWorld App并点击提交，启用后APP将在IG500中运行且每次开机自动运行。
![](./images/2019-12-04-13-17-45.png)
 &nbsp;

  在APP状态页面查看APP已成功运行在网关上，完成HelloWorld App的部署和运行。
![](./images/2019-12-05-13-45-24.png)

### 6. 查看APP运行状态
在IG500的“边缘计算>>Python边缘计算>>应用>>状态”页面可查看App的运行状态。
![](./images/2019-12-05-13-48-18.png)

点击“查看日志”可查看App的运行日志。
![](./images/2019-12-05-13-48-39.png)
![](./images/2019-12-05-14-54-03.png)
### 7. 为APP更新配置文件
- 步骤1：修改配置文件  <br/>
  将App的“config.yaml”中的配置```description: "hello world!"```修改为:```description: "hello inhand!"```  

  ![](./images/2019-12-05-14-54-34.png) <br/>
 &nbsp;

- 步骤2：导入配置文件并重启APP  <br/>
  在IG500的“边缘计算>>Python边缘计算>>应用”页面为“HelloWorld”APP导入修改后的配置文件并重启APP。  
![](./images/2019-12-05-14-55-24.png) 
![](./images/2019-12-05-14-55-43.png)
 &nbsp;

重启后“HelloWorld”APP将按照更新后的配置文件运行，即每10秒打印一条"hello inhand!"日志。

![](./images/2019-12-06-15-20-04.png)
### 8. 附录
#### 8.1 使用pip为APP安装第三方依赖库
使用pip为APP安装第三方依赖库时需启用IG500的调试模式并且接入互联网。
![](./images/2019-12-06-16-42-29.png)
![](./images/2019-12-04-10-00-36.png)
- 步骤1：使用VS Code与网关建立SFTP连接，详见第二节中的“3.1 建立SFTP连接”。
![](./images/2019-12-06-16-41-02.png)
 &nbsp;

- 步骤2：执行pip install + “依赖库名称” + “==版本号” + “-t” + “APP的lib文件夹路径”命令并回车以安装相应依赖库。（不加版本号时pip会自动安装最新版的依赖库） 
  ```
  pip install modbus_tk==1.1.0 -t /var/user/app/HelloWorld/lib/
  ```

  ![](images/2019-12-24-14-37-38.png)
 &nbsp;

- 步骤3：随后会自动下载并安装相应的依赖库，安装成功后如下图所示：
![](images/2019-12-24-14-39-13.png)
 &nbsp;

- 步骤4：使用`export`命令为APP设置环境变量。在终端窗口执行以下命令（“HelloWorld”项需要根据实际的APP名称调整）
  ```
  export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/var/user/app/HelloWorld/lib/  
  export PYTHONPATH=$PYTHONPATH:/var/user/app/HelloWorld/lib/
  ```
  ![](images/2019-12-24-14-42-58.png)
 &nbsp;

  为APP安装第三方依赖库后，调试前必须要为该APP配置相应的环境变量，否则APP将不能正常运行。当APP未在IG500中运行时APP的环境变量为初始环境变量；APP运行时会自动添加lib文件夹下的第三方依赖库的环境变量。<br/>
 &nbsp;

- 步骤5：运行代码以确认APP运行正常
  ![](images/2019-12-25-11-10-52.png)

#### 8.2 启用代码自动补全
为了提高编码效率，您可以通过Python扩展插件实现代码自动补全功能。
- 步骤1：点击“文件>>首选项>>设置”进入设置页面。
![](./images/2019-12-05-15-13-02.png)
 &nbsp;

- 步骤2：选择设置页面中的“扩展>>Python”项，找到“Auto Complete: Extra Paths”项并点击“在setting.json中编辑”。
![](./images/2019-12-05-15-17-34.png)
 &nbsp;

  在“settings.json”中增加如下配置项并保存（python.pythonPath为python解释器的安装路径）
  ```
  "python.linting.pylintEnabled":false,
  "python.linting.flake8Enabled":true,
  "python.jediEnabled":true,
  "terminal.integrated.rendererType":"dom",
  "explorer.confirmDelete":false,
  "python.pythonPath":"C:/Users/zn/AppData/Local/Programs/Python/Python37",
  ```
  ![](./images/2019-12-05-17-43-10.png)

#### 8.3 FAQ
- Q1:建立SFTP连接时提示远程主机标识更新，认证失败应该怎么办？
![](./images/2019-12-10-13-40-49.png)
 &nbsp;

  A1：出现此问题的原因是因为IG500的密钥更新了，但是PC上的密钥还未更新导致认证失败。此时您只需要删掉密钥文件中有冲突的那一行即可。(按住Ctrl并单击冲突项可以快速访问链接)
![](./images/2019-12-10-13-53-22.png)
 &nbsp;

  删除后再次使用`>SFTP:Open SSH in Terminal`命令即可成功建立SFTP连接。
![](./images/2019-12-10-13-54-57.png)
 &nbsp;

- Q2:建立SFTP连接后，在左侧空白处右键选择”Sync Local->Remote”将代码同步到远程服务器时提示“配置的身份验证方法失败”怎么解决？
![](images/2019-12-19-18-33-09.png)
 &nbsp;

  A2:确保“sftp.json”文件中的password项与IG500的密码一致。一致后重新建立SFTP连接并同步代码。
