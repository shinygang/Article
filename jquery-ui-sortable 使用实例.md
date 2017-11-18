# jquery-ui sortable 使用实例
> 最近公司需要做任务看板，需要拖拽效果。[点击查看效果](https://task.clouderwork.com/project/xiang-mu-guan-li-ping-tai-dailybuild/kanban)。由于网站是基于vue的技术栈，最开始找了一个现成的vue封装的拖拽组件：[Vue.Draggable](https://github.com/SortableJS/Vue.Draggable)，该组件是基于sortable封装的。但是由于使用的原生html5的拖拽属性，导致拖拽过程有透明度，而且不能修改透明度和倾斜度，达不到产品的要求（产品要求模仿worktile的使用体验）。同时我也看了同行很多类似的看板效果，都有倾斜度和非透明，经研究，采用的jquery-ui的sortable。所以，死皮赖脸的选择jquery-ui的sortable来操作，其实是极不情愿的使用：因为基于jQuery的，jQuery占空间太大。但由于是pc端，也还可以接受。

在开发之前，可以先看[jquery-ui的sortable的官方文档](https://api.jqueryui.com/sortable/)和[国人整理的文档的一些实例](http://www.runoob.com/jqueryui/example-sortable.html)。

* 引入jquery库和jquery-ui库
```
// 引入样式文件
<link rel="stylesheet" href="https://static.clouderwork.com/task/static/js/jquery-ui.min.css">
// 引入jquery 库
<script src="https://static.clouderwork.com/task/static/js/jquery.min.js"></script>
// 引入jquery-ui库
<script src="https://static.clouderwork.com/task/static/js/jquery-ui.min.js"></script>
```
* 使用实例代码
```
// 初始化拖拽
initSort () {
      // 拖拽时开始滚动的间距
      var scrollingSensitivity = 20
      // 拖拽时滚动速度
      let scrollingSpeed = 20
      // 拖拽前的父级节点
      let dragBeforeParentNode = null
      // 初始化拖拽函数
      $('.task-lists').sortable({
	    // 自适应placeholder的大小
        forceHelperSize: true,
        // 拖拽时的鼠标形状
        cursor : '-webkit-grabbing',
        // 拖拽的父级节点(该节点一定要注意，配置错误会导致当前屏幕外的元素没法自动滚动拖拽，两列之间拖拽的滚动也会出问题)
        appendTo: '.drag-task',
        // 拖拽时的倾斜度
        rotate: '5deg',
        // 延迟时间(毫秒)，避免和click同时操作时出现的冲突
        delay: 150,
        // 以clone方式拖拽
        helper: 'clone',
        // 拖拽到边框出现滚动的间距，
        scrollSensitivity:scrollingSensitivity,
        // 应用于拖拽空白区域的样式
        placeholder: 'portlet-placeholder ui-state-highlight',
        // 允许拖拽预留空白区域
        forcePlaceholderSize: true,
        // 多个列表之间的拖拽的dom元素
        connectWith: '.task-lists',
        // 拖拽结束函数
        stop: (e, ui) => {
	      // 当前拽入的元素
          let item = $(ui.item)
          // 当前拽入元素的下标
          let index = item.index()
          let kid = ''
          // xxxx 这里面可以操作数据更新
        },
        // 开始拖拽时的函数
        start: (e, ui) => {
	      // 拖拽前的父级节点
          dragBeforeParentNode = ui.item[0].parentNode
          // 让placeholder和源高度一致
	       ui.placeholder.height(ui.helper[0].scrollHeight).width(258)
	       // xxxx  这里可以记录一些拖拽前的元素属性
        },
        // 处理两列滚动条问题
        sort:function(event, ui){
          var scrollContainer = ui.placeholder[0].parentNode
          // 跨列拖拽的情况
          if (dragBeforeParentNode && dragBeforeParentNode.id !== scrollContainer.id) {
            // 设置拽入的列表的滚动位置
            var overflowOffset = $(scrollContainer).offset()
            if((overflowOffset.top + scrollContainer.offsetHeight) - event.pageY < scrollingSensitivity) {
              scrollContainer.scrollTop = scrollContainer.scrollTop + scrollingSpeed
            } else if(event.pageY - overflowOffset.top < scrollingSensitivity) {
              scrollContainer.scrollTop = scrollContainer.scrollTop - scrollingSpeed
            }
          }
        }
      }).disableSelection()
```
==在开发的时候一定要多看文档，了解其属性的含义会事半功倍，顺延解决问题。==
下面给一个实例供参考：[jquery-ui-sortable 实例](http://www.shinygang.cn/jquery-ui-sortable/)， 源代码在github上面，[地址](https://github.com/shinygang/jquery-ui-sortable)


#### ` 如果对你有帮助，恳请给作者累积一个大保健的机会，欢迎扫码`
![](http://ww1.sinaimg.cn/large/79462090ly1flmcqgz0xwj21080q2anh.jpg)
