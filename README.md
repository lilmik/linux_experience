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

```bash
conda install -c conda-forge libstdcxx-ng
```


### wsl强制使用n卡来驱动gazebo
其他需要显卡的加速的功能同样适用，测试使用的MX150显卡，OK
```bash
export MESA_D3D12_DEFAULT_ADAPTER_NAME=NVIDIA
```
可以添加到.bashrc文件中，自动生效
```bash
nano ~/.bashrc

export LIBGL_ALWAYS_INDIRECT=0
export MESA_D3D12_DEFAULT_ADAPTER_NAME=NVIDIA

source ~/.bashrc
```

### wsl强制调整GUI应用的dpi
先安装下面软件包
```bash
sudo apt install x11-xserver-utils
```
创建并编辑 ~/.Xresources 文件：
```bash
nano ~/.Xresources
```
添加以下内容来设置默认 DPI（字体大小），例如将 DPI 设置为 192：
```bash
Xft.dpi: 192
```
加载 ~/.Xresources 文件：
```bash
xrdb -merge ~/.Xresources
```
编辑 ~/.bashrc 
```bash
nano ~/.bashrc

xrdb -merge ~/.Xresources

source ~/.bashrc
```

### wsl强制优化调整QtCreator应用,执行路径|dpi
编辑 ~/.bashrc 
```bash
nano ~/.bashrc

# qtcreator
export PATH=$PATH:~/Qt/Tools/QtCreator/bin
export QT_SCALE_FACTOR=1.75  # 尝试 1.25、1.5 等值
export QT_SCALE_FACTOR_ROUNDING_POLICY=PassThrough  # 避免四舍五入导致的比例偏差

source ~/.bashrc
```

### linux qt程序适应高分屏,指定缩放比例
```c++
#include <QApplication>
#include <QWidget>

int main(int argc, char *argv[])
{
    // 设置高 DPI 缩放策略
    QApplication::setHighDpiScaleFactorRoundingPolicy(Qt::HighDpiScaleFactorRoundingPolicy::PassThrough);
    QApplication::setAttribute(Qt::AA_EnableHighDpiScaling);
    QApplication::setAttribute(Qt::AA_UseHighDpiPixmaps);

    // 设置缩放因子
    qputenv("QT_SCALE_FACTOR", "1.5");

    QApplication a(argc, argv);
    QWidget w;
    w.show();
    return a.exec();
}    
```
