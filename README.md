# loadYoumiADquestion
今天接入有米广告碰到点问题
# loadYoumiADquestion
今天接入有米广告碰到点问题

先是看官方教程https://app.youmi.net/sdk/android/17/doc/701/6/cn/%E6%9C%89%E7%B1%B3AndroidSDK%E4%B9%8BUnity3d%E4%BD%BF%E7%94%A8%E6%95%99%E7%A8%8B%E6%96%87%E6%A1%A3.html
然后自己跟着做了做，发现缺斤少两...
后来查看下载好的sdk包是发现有demo...原谅我之前的无脑...
窃喜，打开demo（unity版本的sdk）
编译。。。咦？官方的包竟然报错了？
查原因...插件冲突导致的
在build.ground下：
官方包用的是2.2
dependencies {
		classpath 'com.android.tools.build:gradle:2.2.2'
	}
andriodstudio而自动提供的解决方案是升级。。。
升级...
于是改为了
dependencies {
		classpath 'com.android.tools.build:gradle:3.0.0'
	}
但是接着说自定义apk名称代码报错（Cannot set the value of read-only property 'outputFile'。。。 ）
百度了一波解决方案，查到了http://www.jb51.net/article/126933.htm
大神的经验果然丰富
结果一改？喵？
还是不对...
经检查发现，最后的方式有问题，官方读取用的是buildTime()，而大神的修改用成了runtime（）
so，最终修改为
android.applicationVariants.all { variant ->
		variant.outputs.all {
			outputFileName = "YoumiUnity3dDemo_${defaultConfig.versionName}_${buildTime()}.apk"
		}
	}
最后又一次提示升级api，升级后大功告成！