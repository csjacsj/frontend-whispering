# .vue文件的style部分加入scoped的问题

在.vue文件中，编写的内容主要地分为3个部分，即template, script 和 style 标签的内容
其中的style标签可以加入scoped属性，其作用在vue-cli的样例项目中的注释已经表达了：
<!-- Add "scoped" attribute to limit CSS to this component only -->
这样，在编译.vue文件时会对本模板的内容自动加入一个系统生成的唯一id作为其增加的属性，例如：
<div data-v-56fd9caf class=“aa bb ...">
而相应地，在style中写好的css，也会在其class的基础上再添加上这个唯一属性名（以方括号括住）

以表明该css定义在匹配成功后，还需要匹配具有相同的属性名，方才生效，例如：
.title[data-v-56fd9caf] {
1.  color: #3c4050;
2.           ...
3. }
1. 
这一功能来自于CSS的属性选择器。其原理就是如此。

目前知道的scoped的问题有2个：

1、由于为组件下的所有表层元素添加了唯一属性名，导致文件体积一定程度上增大了（虽然大部分时候这只是不痛不痒的小事）；
2、当在结合element-ui使用时，遇到这样的问题，即对el-input组件，定义其内部的input的样式，由于内部的input，编译出来之后并没有加上唯一属性名，从而导致无法应用到其上；

针对这2个问题，如果用less的嵌套写法都可以解决：
1、首先给template下的顶层div设置一个class名
2、在style的less中，所有定义写到这个class内部
唯一的小问题就是所有定义都多了一层缩进





<< EOF

