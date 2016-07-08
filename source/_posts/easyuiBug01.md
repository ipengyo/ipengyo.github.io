title: easyuiBug01
date: 2016-07-09 02:38:12
tags: 
  - easyui
---

----

# easyui-loader加载器的坑

* commbobox
在使用easyui loader 加载  combobox 的多选下拉列表组件时，使用的是easyLoader加载发现问题js控制台报错：

       ComboBox Uncaught TypeError: Cannot read property 'defaults' of undefined     
然后点进去发现是window找不到，后来深入发现easyui 的loader 加载器里面的配置依赖没有window
后来我把他后面的 ** dependencies ** 加上了 window依赖
        combobox:{js:"jquery.combobox.js",css:"combobox.css",dependencies:["combo","window"]
* valiBox
在使用easyui loader 加载 validBox验证组件的时候，发现验证后的提示文字不显示
看loader的源码后才得知，validBox的显示验证的样式是来源与tooltip的组件，而这个组件在源码竟然有2个，有一个竟然没有加载css所以导致没有显示easyui的验证提示
		tooltip:{js:"jquery.tooltip.js",css:"tooltip.css"}
* datetimebox 
同commbobox同样的问题，在loader找到这个对象的配置，在他后面的 ** dependencies ** 加上了 window依赖


>来源于：easyui版本1.43