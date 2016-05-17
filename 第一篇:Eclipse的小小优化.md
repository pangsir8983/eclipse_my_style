## `开天辟地篇` : 打造专属开发工具Eclipse篇

#### 一.eclipse.ini和sts.ini`[基于8G内存]`
```ini
-startup
plugins/org.eclipse.equinox.launcher_1.3.100.v20150511-1540.jar
--launcher.library
plugins/org.eclipse.equinox.launcher.win32.win32.x86_64_1.1.300.v20150602-1417
-product
org.eclipse.epp.package.jee.product
--launcher.defaultAction
openFile
--launcher.XXMaxPermSize
256M
;注释系统自带的界面
;-showsplash
org.eclipse.platform
--launcher.XXMaxPermSize
256m
--launcher.defaultAction
openFile
--launcher.appendVmargs
;一定需要放置到-vmargs的前面
-vm
E:\java-tools\Java\JDK8_64\jdk1.8.0_77\bin
-vmargs
;配置自己的动画,只是支持bmp图片
-Dosgi.splashLocation=C:/hp.bmp
-XstartOnFirstThread
-Dosgi.requiredJavaVersion=1.7
-Declipse.p2.unsignedPolicy=allow
-Dcom.sun.management.jmxremote
-Dorg.eclipse.swt.internal.carbon.smallFonts
-Xincgc
-Xss8m
-Xms700m
-Xmx2048m
-XX:NewSize=16m
-XX:PermSize=128m
-XX:MaxPermSize=400m
-XX:MaxPermSize=1048m
-XX:MaxPermHeapExpansion=20m
-XX:+UseConcMarkSweepGC
-XX:CMSInitiatingOccupancyFraction=70
-XX:+UseCMSInitiatingOccupancyOnly
-XX:+UseParNewGC
-XX:+CMSConcurrentMTEnabled
-XX:ConcGCThreads=2
-XX:ParallelGCThreads=2
-XX:+CMSIncrementalPacing
-XX:CMSIncrementalDutyCycleMin=0
-XX:CMSIncrementalDutyCycle=5
-XX:GCTimeRatio=49
-XX:MaxGCPauseMillis=20
-XX:GCPauseIntervalMillis=1000
-XX:+UseCMSCompactAtFullCollection
-XX:+CMSClassUnloadingEnabled
-XX:+DoEscapeAnalysis
-XX:+UseCompressedOops
-XX:+ExplicitGCInvokesConcurrentAndUnloadsClasses
;参数来跳过jvm对class文件的校验，以此提升eclipse的启动速度，但这是很不安全的
-Xverify:none
-Dorg.eclipse.swt.browser.IEVersion=10001
```
#### 二. 全面优化Eclipse
1. 动画很酷，但如果可以的话，我总是在所有的工具中禁用动画。所以classic或者window classic主题是我最常用的主题 , 简简单单的挺好!
> `执行路径` Window -> Preferences -> General -> Appearance -> Uncheck 'Enable animations' 默认选项就是没有选择  

![优化操作,选择主题](https://app.yinxiang.com/shard/s32/res/66f88941-5007-438b-9f7a-f8cdb4bfa1bc/%E5%BF%AB%E7%85%A71.jpg)

2. 自动补全操作
有时在性能较差的机器上，或者当你有很多类的时，自动补全功能性能就会很差。一个很小的优化是减少自动补全的proposal。我仅保留了Java Proposals和Template Proposals：
> `执行路径` Window -> Preferences -> Java -> Editor -> Content Assist -> Advanced 根据自己的机器情况弄,有的时候显示太多的提示,很烦人!
  
  ![这步看情况吧!](https://app.yinxiang.com/shard/s32/res/463a8819-3f18-4b47-a8a7-45e2df09c850/%E5%BF%AB%E7%85%A74.jpg)

3. 验证的设置
推荐方案1 : 如下图所示,第一列保持不变,第二列就保留一项即可!
推荐方案2 : 如果对自己很自信就全部禁用,哈哈~~
> `执行路径` Window -> Preferences -> Validation  
  
  
![验证器设置](https://app.yinxiang.com/shard/s32/res/4d7b90ba-8808-420c-9b46-8b1ac869581b/%E5%BF%AB%E7%85%A77.jpg)
4. 关闭不使用的工程
如果你仅开发部分eclipse中的工程，那你最好把其他功能关闭掉。他们不会出现在eclipse索引中。你可以在workspace中手动关闭不相关的工程（Close unrelated projects）。
> `执行路径`Right Click on Project -> Close unrelated projects  

	网络中有人推荐使用Working Set，你可以添加多个工程到一个Working Set中，这样就可以快速的在Working Set件切换`STS中没有该项选择`。
> `执行路径` Right Click on Project -> Assign Working Sets.. 不喜欢  

5. 关闭编辑器中不用的tab
编辑中太多的tab会导致eclipse性能下降，可以这样控制下tab的个数：
> `执行路径`Window -> Preferences -> General -> Editors  

	勾选 Close editors automatically 并设置 Number of opened tabs 为10 , 如图所示:
![Alt text](https://app.yinxiang.com/shard/s32/res/767b5423-0595-41be-a452-a80a69d6bb68/%E5%BF%AB%E7%85%A78.jpg)
6. 禁用拼写检查
胖先生的英语不好,你还是个程序员吗？我觉得没有任何理由需要拼写检查功能。
取消这个鸡肋的功能:
> `执行路径`Window -> Preferences -> General -> Editors -> Text Editors -> Spelling -> Uncheck 'Enable spell checking'  

![Alt text](https://app.yinxiang.com/shard/s32/res/0c74de33-b12d-4a7a-aebd-af4150009c05/%E5%BF%AB%E7%85%A79.jpg)
7. 禁用auto build `对于这项,各位同学,根据自己的熟练程度来弄`
> `执行路径` Window -> Preferences -> Java -> Compiler -> Building -> Uncheck 'Scrub output folders when cleaning'  
  
  
> `执行路径` Window -> Preferences -> Java -> Compiler -> Building -> Uncheck 'Rebuild class files modified by others'  
  
  
![Alt text](https://app.yinxiang.com/shard/s32/res/17a8db7e-aaa5-4c89-a857-13cf784cebcc/%E5%BF%AB%E7%85%A711.jpg)

8. 取消过多的启动项加载
很多启动项对开始的我们并没有卵用,多有移除最好!打造干净的运行
![Alt text](https://app.yinxiang.com/shard/s32/res/e961152b-5618-444c-8dc8-55a78dc9a640/%E5%BF%AB%E7%85%A712.jpg)
9. 设置工作空间的编码格式
![Alt text](https://app.yinxiang.com/shard/s32/res/fd66a7e6-9a47-4110-a7e5-6f8979acdeed/%E5%BF%AB%E7%85%A714.jpg)
10. 修改文件的编码格式,个人全部使用UTF-8的编码
> `执行路径` Window -> Preferences -> General -> Editors -> Content Types  
  
  设置Text为` UTF-8 `编码格式
  ![Alt text](./快照9.jpg)
  展开Text,修改java properties的编码格式为` UTF-8 `点击Update
  ![Alt text](./快照11.jpg)
  展开Text,修改JSP的编码格式为` UTF-8 `点击Update
  ![Alt text](./快照12.jpg)
11. 设置新建JSP时的默认编码格式为UTF-8
![Alt text](https://app.yinxiang.com/shard/s32/res/fd66a7e6-9a47-4110-a7e5-6f8979acdeed/%E5%BF%AB%E7%85%A714.jpg)

----
	        后续 : 设置Tomcat和JDK,简单修改JSP模版   -  作者: 刘文铭

