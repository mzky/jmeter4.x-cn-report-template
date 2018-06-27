将report-template目录替换apache-jmeter-4.0\bin\report-template目录即可


可以写个bat进行html报告生成，在apache-jmeter-4.0目录下创建ResultReport文件夹和bat文件

将以下内容写到bat中，知道获取当前时间来命名文件夹，即使同名的报告也不会覆盖

其中“jtl报告名称.jtl”需要改成报告实际名字

----------------------------------------

@echo 生成报告中...

@set h=%time:~0,2%

@set h=%h: =0%

@set file=%date:~0,4%%date:~5,2%%date:~8,2%%h%%time:~3,2%%time:~6,2%

@md ResultReport\%file%

%CD%\bin\jmeter -g %CD%\jtl报告名称.jtl -o %CD%\ResultReport\%file%\

----------------------------------------
