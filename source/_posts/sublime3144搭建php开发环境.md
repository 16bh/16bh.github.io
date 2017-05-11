---
title: sublime3144版本搭建php开发环境
toc: true
date: 2016-07-11 17:36:35
categories: [Editor,sublime]
tags: [php,sublime]
---

> `sublime`是兼备美观、轻便、扩展性强为一身的最强大的编辑器之一（没有之一的话会被打的吧）

> 最新版的`sublime`自带的`GOTO`功能解决了`php`需要安装`ctags`插件才能进行跳转的不方便之处，无需手动生成`tags`文件即可跳转

> 配置环境为`mac`，部分内容可能不适合`windows`环境

> `sublime`虽然也支持`debug`功能，但肯定没有`phpstorm`好用，如果经常需要`debug`功能的，建议切换到`phpstorm`使用


<!--more-->

# sublime下载

直接从`sublime`的官网下载安装文件：https://www.sublimetext.com/


# 万物的起始:安装插件管理工具`package control`

使用`Ctrl`+`、`（数字1左边那个）快捷键或者通过`View`>`Show Console`菜单打开命令行

输入以下内容：

```
import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
```
按确认后即开始安装`package control`


>安装报错：No such file or directory: '/Users/jim/Library/Application Support/Sublime Text 3/Installed Packages/Package Control.sublime-package'
>参考`https://packagecontrol.io/installation`手动安装即可

>不能获取插件列表 Package Control：There are no packages available for installation错误解决方案：
> - cmd下输入ping sublime.wbond.net链接一下看下sublime.wbond.net这个域名的ip.
> - 打开`\etc\hosts`文件。在最后面加上例如50.116.34.243 sublime.wbond.net这样的对应关系，IP是上面测试的。
> - 然后请关闭Submine Text并重启，即不会再弹出更新提醒了。

# 配置和快捷键修改
进入`Sublime Text`>`Perferences`
可以看到`Settings - Default`系统设置、`Settings - User`用户设置、`Key Bindings - Default`系统快捷键、`Key Bindings - User`用户快捷键

不管是修改`Default`还是`User`都可以，但是，推荐的做法（也是为了以后备份的需要），是先将`Default`里的内容拷贝一份到`User`中，再在`User`中进行修改




# php开发插件推荐
插件安装的方法及其简便，`Command`+`Shift`+`P`唤出命令面板，输入`install`,选择`Package Control : Install Package`，确认后过一段时间加载出包安装界面，输入扩展的名称搜索，选中你想安装的扩展确认即可自动安装

如果一直无法加载出包安装界面，说明你的网络存在问题

以下是推荐安装的插件

- SideBarEnhancement  侧边栏增强插件
    必装插件，安装完该插件后，在侧边栏文件上右击即可看到效果
    
- Colorsublime    主题库插件
    Why we use sublime? beacuse it is Cool!
    安装`colorsublime`插件后，为自动为你下载近百套主题到本地，供你切换使用，你只需`Command`+`Shift`+`P`呼出控制面板，输入`install theme`，确认后出现主题列表，可以用上下键预览主题的效果，按确认键确定主题
    
    
- SideBarFolders    项目列表插件
    如果需要打开多个项目文件夹，切经常在多个项目之间切换工作空间，可以安装`SideBarFolders`插件，该插件在在菜单栏多出一个`Folders`选项，点击可查看所有项目文件夹

- AllAutocomplete    代码自动补全插件
    默认的补全只能根据当前文件进行补全，安装了`AllAutocomplete`插件后会根据你已经打开的标签文件进行补全

- BracketHignlighter    高亮配对的括号插件
![](http://o9xbyqajf.bkt.clouddn.com/images/1468233622657.png)


- SyncedSidevarBg插件    修改侧边栏颜色插件
    使用深色主题的时候，感觉白色的`Sublime Text`>`Perferences`侧边栏与之颜色不搭，可以使用`SyncedSidevarBg`插件
    该插件会使得侧边栏的颜色和编辑区背景颜色保持一致,配合主题切换插件使用效果更加

- Seti_UI    自带精美的文件图标的主题
    如图所示，会为侧边栏的文件生成不同样式的文件图标，同时不需要安装上面的`SyncedSidevarBg`插件也可以解决侧边栏颜色的问题
    ![](http://o9xbyqajf.bkt.clouddn.com/images/1468231624322.png)


安装完成后，修改配置文件（`Sublime Text`>`Perferences`>`Settings - User`），加入以下内容启用`Seti-UI`主题
```
{
    "theme": "Seti.sublime-theme"
}
```

- SideBarGit    在侧边栏显示文件的git状态的插件
![](http://o9xbyqajf.bkt.clouddn.com/images/1468233896575.png)


- SublimeLinter和SublimeLinter-php    php错误提示插件
![](http://o9xbyqajf.bkt.clouddn.com/images/1468477997880.png)


- Color Highlighter和ColorPicker    css颜色插件

见单独介绍部分：[sublime插件 - css颜色高亮与取色器
](http://jimxu.me/2016/07/06/sublime%E6%8F%92%E4%BB%B6-css%E9%A2%9C%E8%89%B2%E9%AB%98%E4%BA%AE%E4%B8%8E%E5%8F%96%E8%89%B2%E5%99%A8/)

- Markdown Preview和MarkdownEditing    Markdown编辑插件
见单独介绍部分:[sublime插件 - markdown编辑和预览](http://jimxu.me/2016/07/11/sublime%E6%8F%92%E4%BB%B6-markdown%E7%BC%96%E8%BE%91%E5%92%8C%E9%A2%84%E8%A7%88/)

- WakaTime    记录编程习惯
见单独介绍部分:[记录你的编程习惯 - 编辑器通用插件：WakaTime](http://jimxu.me/2016/07/11/%E8%AE%B0%E5%BD%95%E4%BD%A0%E7%9A%84%E7%BC%96%E7%A8%8B%E4%B9%A0%E6%83%AF-%E7%BC%96%E8%BE%91%E5%99%A8%E9%80%9A%E7%94%A8%E6%8F%92%E4%BB%B6%EF%BC%9AWakaTime/)

- AutoFileName    自动补全文件路径

- Clickable URLs    链接可以点击

- DashDoc    在`Dash`中查找光标所在的单词
- outline    显示函数列表



# 其他配置

## 显示所有已打开的文件
  `View` > `Side Bar` > `Show Open Files`
  ![](http://o9xbyqajf.bkt.clouddn.com/images/1468233445271.png)


## 配置php的编译环境
见单独介绍部分：[mac环境sublime配置php编译环境](http://jimxu.me/2016/06/28/mac%E7%8E%AF%E5%A2%83sublime%E5%A2%9E%E5%8A%A0php%E7%BC%96%E8%AF%91%E7%8E%AF%E5%A2%83/)

## 开启vim模式

`sublime`其实自带了`vim`的插件`Vintage`，但是被默认禁用了，只需要在配置文件中取消禁用即可

打开`Sublime Text`>`Perferences`>`Settings - User`

```
"ignored_packages": ["Vintage"],
```

修改为：

```
"ignored_packages": [],    //取消禁用Vintage模块
"vintage_ctrl_keys": true,     //在vim模式下支持ctrl快捷键的使用   
"vintage_start_in_command_mode": true,    //默认使用vim输入模式而不是插入模式
```
然后就可以欢快的像使用`vim`模式进行编辑了


## sublime个人配置

```

	"auto_find_in_selection": true,
	"bold_folder_labels": true,
	"color_scheme": "Packages/User/SublimeLinter/1337 (SL).tmTheme",
	"disable_tab_abbreviations": true,
	"draw_minimap_border": true,    //在小地图上显示当前代码的位置
	"draw_white_space": "all",    //显示不可见的空格字符
	"fade_fold_buttons": false,
	"font_size": 14,    //字体大小
	"highlight_line": true,    //高亮当前行
	"highlight_modified_tabs": true,    //高亮已修改的标签页
	"line_padding_bottom": 1,
	"line_padding_top": 1,
	"margin": 4,
	"save_on_focus_lost": true,    //自动保存
	"show_full_path": true,    //显示完成的文件目录
	"tab_size": 4,    //一个tab转4个空格
	"theme": "Seti.sublime-theme",
	"translate_tabs_to_spaces": true,    //tab键自动转空格
	"vintage_ctrl_keys": true,    //vim模式支持ctrl组合的快捷键
	"vintage_start_in_command_mode": true    //默认启动vim模式
```

## sublime个人热键设置

- 设置了跳转到方法以及返回的快捷键为`Command`+`[`,`Command`+`]`
- 参照`atom`的快捷键，设置了隐藏侧边栏为`Command`+`Shit`+`\`,在侧边栏中显示当前文件为`Command`+`\`
- 设置了预览在默认浏览器中预览`markdown`文件为`Option`+`M`
- 设置了在`Dash`中搜索光标所在词为`Option`+`D`

```
{ "keys": ["super+left"], "command": "jump_back" },
  { "keys": ["super+right"], "command": "goto_definition" },
  { "keys": ["super+shift+\\"], "command": "toggle_side_bar" },
  { "keys": ["super+\\"], "command": "reveal_in_side_bar"},
  { "keys": ["alt+m"], "command": "markdown_preview", "args": { "target": "browser"}},
   { "keys": ["alt+d"], "command": "dash_doc"},
``` 


## 备份sublime插件及设置

将`~/Library/Application Support/Sublime Text 3/Packages/User`文件夹备份到可同步的云盘文件夹，如`坚果云`，即可自动备份`sublime`中已安装的插件和设置

