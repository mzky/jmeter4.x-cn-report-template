## 将report-template目录替换apache-jmeter-4.0\bin\report-template目录即可


## 可以写个bat进行html报告生成，在apache-jmeter-4.0目录下创建ResultReport文件夹和bat文件

- 将以下内容写到bat中，知道获取当前时间来命名文件夹，即使同名的报告也不会覆盖

- 其中“jtl报告名称.jtl”需要改成报告实际名字

----------------------------------------
脚本20180710已改进为提示选择jtl文件
----------------------------------------
<# :: 生成html报告脚本 by mzky 20180710
@color 2f
@echo off
@set h=%time:~0,2%
@set h=%h: =0%
@set file=%date:~0,4%%date:~5,2%%date:~8,2%%h%%time:~3,2%%time:~6,2%
@echo 等待选择jtl文件...
@set jtlname=''
for /f "delims=" %%I in ('powershell -noprofile "iex (${%~f0} | out-string)"') do (
@set jtlname=%%~I
)
if exist  %jtlname% (
@echo 选择的文件：%jtlname%
@echo 生成报告中...
@md %CD%\ResultReport\%file%
@cd %CD%\bin\
@call jmeter -g %jtlname% -o %CD%\ResultReport\%file%\
@echo 生成的报告路径：%CD%\ResultReport\%file%\
)else (
@echo 已取消选择，如想再次选择，需要重新执行本脚本！
)
@pause
exit
#>

Add-Type -AssemblyName System.Windows.Forms
$f = new-object Windows.Forms.OpenFileDialog
$f.InitialDirectory = pwd
$f.Filter = "JTL Files (*.jtl)|*.jtl|All Files (*.*)|*.*"
$f.ShowHelp = $false
$f.Multiselect = $false
[void]$f.ShowDialog()
if ($f.Multiselect) { $f.FileNames } else { $f.FileName }




## 汉化效果：https://www.jianshu.com/p/b9a1a43d3ffd
