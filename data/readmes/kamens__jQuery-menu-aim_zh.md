jQuery-menu-aim
===============

`menu-aim` 是一个用于下拉菜单的 jQuery 插件，能够区分用户是仅仅悬停在某个菜单项上，还是准备导航进入子菜单的内容区域。

[尝试演示](https://rawgithub.com/kamens/jQuery-menu-aim/master/example/example.html)

![Amazon 截图](https://raw.github.com/kamens/jQuery-menu-aim/master/amazon.png)

该问题通常通过设置超时和延迟来解决。`menu-aim` 尝试通过检测用户鼠标的移动方向来优化这一体验。这可以让用户在菜单上下导航时获得更快的切换速度。希望使用体验能类似于 amazon.com 的“按部门购物”下拉菜单。

## 使用方法：

     $("#menu").menuAim({
         activate: $.noop,  // fired on row activation
         deactivate: $.noop  // fired on row deactivation
     });

……以便在菜单行被有意（激活或取消）时接收对应事件。

以下选项可传递给 `menuAim`。所有函数执行时，其上下文 (`this`) 均为对应行的 HTML 元素：

     .menuAim({
         // Function to call when a row is purposefully activated. Use this
         // to show a submenu's content for the activated row.
         activate: function() {},

         // Function to call when a row is deactivated.
         deactivate: function() {},

         // Function to call when mouse enters a menu row. Entering a row
         // does not mean the row has been activated, as the user may be
         // mousing over to a submenu.
         enter: function() {},

         // Function to call when mouse exits a menu row.
         exit: function() {},

         // Function to call when mouse exits the entire menu. If this returns
         // true, the current row's deactivation event and callback function
         // will be fired. Otherwise, if this isn't supplied or it returns
         // false, the currently activated row will stay activated when the
         // mouse leaves the menu entirely.
         exitMenu: function() {},

         // Selector for identifying which elements in the menu are rows
         // that can trigger the above events. Defaults to "> li".
         rowSelector: "> li",

         // You may have some menu rows that aren't submenus and therefore
         // shouldn't ever need to "activate." If so, filter submenu rows w/
         // this selector. Defaults to "*" (all elements).
         submenuSelector: "*",

         // Direction the submenu opens relative to the main menu. This
         // controls which direction is "forgiving" as the user moves their
         // cursor from the main menu into the submenu. Can be one of "right",
         // "left", "above", or "below". Defaults to "right".
         submenuDirection: "right"
     });

`menu-aim` 默认你的菜单结构为子菜单向右展开。当用户鼠标移入新的下拉项时，以及当该菜单项被有意悬停（即确认要进入）时，插件都会触发相应事件。

## 需要示例参考吗？

请查看 `example/example.html`，其中包含一个可供你自由体验的[完整下拉菜单示例](https://rawgithub.com/kamens/jQuery-menu-aim/master/example/example.html)：

![示例截图](https://raw.github.com/kamens/jQuery-menu-aim/master/example.png)<br>
_下载仓库后，打开 `example/example.html` 即可体验充满趣味猴子图片的上述示例。_

## FAQ

1. 许可证是什么？ [MIT](http://en.wikipedia.org/wiki/MIT_License)。
2. 是否支持水平菜单或向左展开的子菜单？是的。请参见上方的 `submenuDirection` 选项。
3. 我在一家大公司工作，使用此第三方代码前需要标注版本号。请问有版本号吗？有的，当前版本为：1.1
4. 我还是觉得不够无聊，还有其他内容吗？ [阅读关于本插件的创建过程](http://bjk5.com/post/44698559168/breaking-down-amazons-mega-dropdown)。