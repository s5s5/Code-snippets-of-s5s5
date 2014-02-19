代码片断@s5s5
=====================

这里是一些s5s5经常用到的代码片断，欢迎拍砖。

***

##HTML

HTML文档声明

    <!DOCTYPE html>

HTML编码使用utf-8，放置于&lt;head&gt;区最上方 （文件保存时存为 utf-8 无BOM）

    <meta charset="utf-8">

强制IE系浏览器用最新渲染模式渲染

    <meta http-equiv="X-UA-Compatible" content="edge">

多终端设备访问时自动缩放到屏幕宽度

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

Meta 值是SEO优化的关键

    <meta name="description" content="" />
    <meta name="keywords" content=""/>

Title 部分更是SEO优化的关键

    <title></title>

-----------------------

##CSS

文件编码必须使用utf-8（无BOM），且必须有汉语系字符

    @charset "utf-8";
    /* ワンピース */

必须使用CSS Reset，减少不同浏览器的表现差异

    html, body, div, span, applet, object, iframe,
    h1, h2, h3, h4, h5, h6, p, blockquote, pre,
    a, abbr, acronym, address, big, cite, code,
    del, dfn, em, img, ins, kbd, q, s, samp,
    small, strike, strong, sub, sup, tt, var,
    b, u, i, center,
    dl, dt, dd, ol, ul, li,
    fieldset, form, label, legend,
    table, caption, tbody, tfoot, thead, tr, th, td,
    article, aside, canvas, details, embed,
    figure, figcaption, footer, header, hgroup,
    menu, nav, output, ruby, section, summary,
    time, mark, audio, video {
        margin: 0;
        padding: 0;
        border: 0;
        font-size: 100%;
        font: inherit;
        vertical-align: baseline;
    }
    /* HTML5 display-role reset for older browsers */
    article, aside, details, figcaption, figure,
    footer, header, hgroup, menu, nav, section {
        display: block;
    }
    body {
        line-height: 1;
    }
    ol, ul {
        list-style: none;
    }
    blockquote, q {
        quotes: none;
    }
    blockquote:before, blockquote:after,
    q:before, q:after {
        content: '';
        content: none;
    }
    table {
        border-collapse: collapse;
        border-spacing: 0;
    }

禁止使用 * 选择器

    * {
        margin:0;
    }

禁止使用expression

    .some_element {
        width: expression((documentElement.clientWidth < 725) ? "725px" : "auto" );
    }

最终发布样式避免使用@import

    @import url('a.css');

尽量避免使用 ID 选择器，为了提升样式重用性以及与页面的耦合性

    #id {
        margin:0;
    }

尽量避免使用 !important，为了减少后续工作复杂度

    .some_element{
        color:red !important;
    }

禁用 outline:none 或 outline:0，为了帮助使用我们产品有障碍的人士（如：盲人）

    a {
        outline: none;
    }
    a {
        outline: 0;
    }

值为0时不需要任何单位

    .some_element {
        padding:0 5px;
    }

避免使用多类选择符，IE6以及更古老的浏览器对类似 .some.element 的多类选择符解析不正确

    .some.element {
        color:red;
    }

移除空的css规则

    .some_element {
    }

正确使用display的属性，由于display的作用，某些样式组合会无效，徒增样式体积的同时也影响解析性能

    .some_element {
        display:inline //后不应该再使用 width 、 height 、 margin 、 margin-top 、 margin-bottom 以及 float
        display:inline-block //后不应该再使用 float
        display:block //后不应该再使用 vertical-align
        display:table-* //后不应该再使用 margin 或者 float
    }

隐藏文字用text-indent: -999方法时，要指定单位和文字方向

    .some_element {
        direction: ltr;
        text-indent: -999em;
    }

filter：应该尽量避免使用 AlphaImageLoader，可以适当在投影、发光、渐变、去色方面上使用

    .some_element {
        background  : url(image.png);
        _background : none;
        _filter     : progid:DXImageTransform.Microsoft.AlphaImageLoader(src='image.png', sizingMethod='crop');
    }

禁止重复属性

    .some_element {
        width: 100px;
        width: 120px;
    }

不滥用web字体，web fonts通常体积庞大，而且一些浏览器在下载web fonts时会阻塞页面渲染损伤性能。

    @media screen {
        @font-face {
            font-family: 'Flavors';
            font-style: normal;
            font-weight: 400;
            src: local('Flavors'), local('Flavors-Regular'), url('http://themes.googleusercontent.com/static/fonts/flavors/v1/7ed-D3MQicPNqc0ZKJ1T1Q.woff') format('woff');
        }
    }

标准化各种浏览器前缀，将浏览器前缀置于前面，将标准样式属性置于最后

    .some_element {
        -webkit-box-shadow: 4px 5px 6px #789;
           -moz-box-shadow: 4px 5px 6px #789;
                box-shadow: 4px 5px 6px #789;
    }

使用CSS渐变等高级特性，需指定所有浏览器的前缀

    .some_element {
        background: -moz-linear-gradient(top,  #1e5799 0%, #7db9e8 100%);
        background:     -webkit-gradient(linear, left top, left bottom, color-stop(0%,#1e5799), color-stop(100%,#7db9e8));
        background: -webkit-linear-gradient(top,  #1e5799 0%,#7db9e8 100%);
        background:     -ms-linear-gradient(top,  #1e5799 0%,#7db9e8 100%);
        background:      -o-linear-gradient(top,  #1e5799 0%,#7db9e8 100%);
    }

rgba(), hsl(), hsla()只现代浏览器支持，使用时还要加上备用色

    .some_element {
        color: red;
        color: rgba(255, 0, 0, 0.5);
    }

使用CSS3圆角时，添加background-clip，以防止某些浏览器显示不正常

    .some_element {
      -webkit-border-radius: 12px;
         -moz-border-radius: 12px;
              border-radius: 12px;
       -moz-background-clip: padding; -webkit-background-clip: padding-box; background-clip: padding-box;
    }

-----------------------

##OTHER

常用HACK

    .all-IE { property:value\9; }
    :root .IE-9 { property:value\0/; }
      .gte-IE-8 { property:value\0; }
      .lte-IE-7 {  *property:value; }
          .IE-7 {  +property:value; }
          .IE-6 { _property:value; }
      .not-IE {  property//:value;}
    @-moz-document url-prefix () { .firefox { property:value; } }
    @media all and (-webkit-min-device-pixel-ratio:0) { .webkit { property:value; } }
    @media all and (-webkit-min-device-pixel-ratio:10000), not all and (-webkit-min-device-pixel-ratio:0) { .opera { property:value; } }
    @media screen and (max-device-width: 480px) { .iphone-or-mobile-s-webkit { property:value; } }

PNG32透明(IE6)

    .some_element {
        background  : url(image.png);
        _background : none;
        _filter     : progid:DXImageTransform.Microsoft.AlphaImageLoader(src='image.png', sizingMethod='crop');
    }

透明

    .some_element {
        opacity: 0.5;
        filter:alpha(opacity=50);
    }

超长截字

    .some_element {
        display: block;
        width: 200px;
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
    }

文本强制换行

    .some_element {
        word-wrap:break-wrod;
        word-break:break-all;
        table-layout:fixed; /* TABLE类还要加这个 */
    }

变灰（IE）

    .some_element {
        filter:gray;
        color:gray;
    }

禁止使用输入法（IE）

    .some_element {
        ime-mode:disabled;
    }

滚动条颜色（IE）

    .some_element {
        scrollbar-3d-light-color:#FF0000;
        scrollbar-arrow-color:#FF0000;
        scrollbar-Base-color:#000000;
        scrollbar-track-color:#000000;
        scrollbar-dark-shadow-color:#330000;
        scrollbar-face-color:#000000;
        scrollbar-highlight-color:#FF0000;
        scrollbar-shadow-color:#990000;
    }

垂直/水平居中 （设定宽度和高度，父节点为 position:relative;）

    .some_element {
        position:absolute;
        left:50%;
        top:50%;
        margin-left:-250px; /* 元素自身宽度的一半 */
        margin-top:-250px; /* 元素自身高度的一半 */
        width:500px;
        height:500px;
    }

自定义鼠标路径要用绝对路径，不然不显示

    .some_element {
        cursor:url("http://www.url.com/cursor.cur")
    }

IE下iframe的设置透明

    <iframe src="about:blank" allowTransparency="true"></iframe>
