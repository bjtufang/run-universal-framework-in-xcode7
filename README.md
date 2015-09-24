# run-universal-framework-in-xcode7


> Xcode7编译app主工程没有问题，但是使用XCode7编译之前bundle framework就会失败。

解决方案，需要操作两步。

+ ###第一步，运行附件中的python脚本

	+ 脚本文件路径
	
	```
	- auto_xcode_edit
  		- framework
  		- main.py  	
	```
	+ 具体操作方法
	
	    + 拷贝附件文件，解压缩到你的工程文件夹中
	    
	      比如下图是解压缩到sdwebimage工程，确认auto_xcode_edit文件夹和sdwebimage.xcodeproj一个路径下
	    
		+ cd 到工程路径
		  比如，cd到上图的sdwebimage目录下

		+ 运行python auto_xcode_edit/main.py
		
		> OK-- 第一步、工程中老的python脚本修复完毕
				
+ ###第二步，打开xxx工程名xxx.xcodeproj工程，在工程设置中Build Phases加入Run Script Phase，Shell脚本
	
	**脚本** 加入到Target Dependencies下面
	
	```
	# remove the last framework
	set -e
	set +u
	echo rm -rf "${BUILT_PRODUCTS_DIR}/${PRODUCT_NAME}.framework"
	rm -rf "${BUILT_PRODUCTS_DIR}/${PRODUCT_NAME}.framework"
	
	```
	
	
+ ###第三步，执行pod update，生成新的workspace
+ ###第四步最后把工程相关的修改提交到git
	