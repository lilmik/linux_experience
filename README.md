```

```

# linux_experience
ubuntu装完后一些使用技巧

### 修改英文系统下中文字体为首选样式

修改下列文件把,中文显示优先级放在日语字体优先级之前.

```bash
sudo gedit /etc/fonts/conf.avail/64-language-selector-prefer.conf
```

修改完成参考如下:

```xml
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
	<alias>
		<family>sans-serif</family>
		<prefer>
			<family>Noto Sans CJK SC</family>
			<family>Noto Sans CJK TC</family>
			<family>Noto Sans CJK HK</family>
			<family>Noto Sans CJK JP</family>
			<family>Noto Sans CJK KR</family>
			<family>Lohit Devanagari</family>
			<family>Noto Sans Sinhala</family>
		</prefer>
	</alias>
	<alias>
		<family>serif</family>
		<prefer>
			<family>Noto Serif CJK SC</family>
			<family>Noto Serif CJK TC</family>
			<family>Noto Serif CJK JP</family>
			<family>Noto Serif CJK KR</family>
			<family>Lohit Devanagari</family>
			<family>Noto Serif Sinhala</family>
		</prefer>
	</alias>
	<alias>
		<family>monospace</family>
		<prefer>
			<family>Noto Sans Mono CJK SC</family>
			<family>Noto Sans Mono CJK TC</family>
			<family>Noto Sans Mono CJK HK</family>
			<family>Noto Sans Mono CJK JP</family>
			<family>Noto Sans Mono CJK KR</family>
		</prefer>
	</alias>
</fontconfig>
```



### wps在英文系统下使用中文界面

启动完一次wps后修改配置文件

```bash
gedit  ~/.config/Kingsoft/Office.conf 
```

修改原有内容,如果原有内容没有相关内容,直接在文件末尾添加.

```xml
[General]
languages=zh_CN
PersistentStatus=0
```

### conda python环境报错

conda中提示libGL相关的问题

```bash
libGL error: MESA-LOADER: failed to open swrast: /usr/lib/dri/swrast_dri.so: cannot open shared object file: No such file or directory (search paths /usr/lib/x86_64-linux-gnu/dri:\$${ORIGIN}/dri:/usr/lib/dri, suffix _dri)
libGL error: failed to load driver: swrast
```

需要在conda对应的环境中安装补充包

```xml
conda install -c conda-forge libstdcxx-ng
```
