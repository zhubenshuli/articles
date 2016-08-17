title: HTML2CANVAS插件对整个网页或者网页某一部分截图并保存为图片
date: 2015-04-07 14:21:00
categories: 文档教程
tags: [canvas]
description: HTML2CANVAS插件对整个网页或者网页某一部分截图并保存为图片...
---

html2canvas能够实现在用户浏览器端直接对整个或部分页面进行截屏。这个脚本将当前页面渲染成一个canvas图片，通过读取DOM并将不同的样式应用到这些元素上实现。它不需要来自服务器任何渲染，整张图片都是在客户端浏览器创建。当浏览器不支持Canvas时，将采用Flashcanvas或ExplorerCanvas技术代替实现。以下浏览器能够很好的支持该脚本：Firefox 3.5+, Google Chrome, Opera新的版本, IE9以上的浏览器。  

如果你想将网页的某一部分或者全部进行截图从而来生成图片保存，那么html2canvas将会是一个很好的选择！

<!--more-->

以下是html2canvas的使用教程：  
1. 使用jquery插件html2canvas对网页的某一部分截图（根据元素节点，比如id什么的）。  
2. 将截图到的canvas标签通过toDataURL()方法转成可以传输的base64编码post给后台服务器处理。  
3. 在后台服务器对传递过来的base64编码处理得到图像并保存。

代码：  
1.引用jquery插件
```
<script src="/js/html2canvas.js" type="text/javascript"></script>
```
2.截图通过ajax传输
```
<script type="text/javascript">
    function howuse(){
        html2canvas(document.getElementById('email_content'), {
            onrendered: function(canvas){
                var html_canvas = canvas.toDataURL();
                $.post('/report/send_rep_submit', {html_canvas:html_canvas}, function(json){

                }, 'json');
            }
        });
　　}
</script>
```
3.后台服务器处理
```
public function send_rep_submit() {
    $html_canvas = $this->input->post('html_canvas');
    $image = base64_decode(substr($html_canvas, 22));
    header('Content-Type: image/png');
    $filename = "images/report/" . $id . ".png";
    $fp = fopen($filename, 'w');
    fwrite($fp, $image);
    fclose($fp);
}
```