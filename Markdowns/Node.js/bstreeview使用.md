## Bootstrap 5 TreeView 使用

github地址：  https://github.com/chniter/bstreeview



### 基本使用
```js
// 节点
var tree = [
  {
    text: "Node 1",
    icon: "fa fa-folder",
    nodes: [
      {
        text: "Sub Node 1",
        icon: "fa fa-folder",
        nodes: [
          {
            id:    "sub-node-1",
            text:  "Sub Child Node 1",
            icon:  "fa fa-folder",
            class: "nav-level-3",
            href:  "https://google.com"
          },
          {
            text: "Sub Child Node 2",
            icon: "fa fa-folder"
          }
        ]
      },
      {
        text: "Sub Node 2",
         icon: "fa fa-folder"
      }
    ]
  },
  {
    text: "Node 2",
    icon: "fa fa-folder"
  }];
// Example: initializing the bstreeview
$('#tree').bstreeview({
  data: data,
  expandIcon: 'fa fa-angle-down fa-fw', // 展开图标
  collapseIcon: 'fa fa-angle-right fa-fw', // 折叠图标
  indent: 1.25, // 缩进
  parentsMarginLeft: '1.25rem', // 父节点的左边缘值
  openNodeLinkOnNewTab: true // Open node link on new browser Tab
});
```


### 结合 JSON API

```js
let xmlhttp;
if (window.XMLHttpRequest) { // code for IE7+, Firefox, Chrome, Opera, Safari
    xmlhttp = new XMLHttpRequest();
} else { // code for IE6, IE5
    xmlhttp = new ActiveXObject("Microsoft.XMLHTTP");
}

xmlhttp.onreadystatechange = function () {
    if (xmlhttp.readyState === XMLHttpRequest.DONE) {
        if (xmlhttp.status === 200) {
            $('#tree').bstreeview({
                data: JSON.parse(xmlhttp.responseText),
                indent: 2,
                parentsMarginLeft: '1.25rem',
                openNodeLinkOnNewTab: false
            });
        } else {
            alert('There was a problem with the request.');
        }
    }
};
xmlhttp.onerror = function (e) {
    console.log(e);
};
xmlhttp.open("GET", "api/essays/getmarkdownlist", true);
xmlhttp.setRequestHeader('content-type', 'application/json; charset=utf-8');
xmlhttp.send();
```

### 全开合使用 折叠展开

```js
// 展开
function ExpandAllTreeView() {
  // 获取所有没展开的
    var collapseElementList = Array.prototype.slice.call(document.querySelectorAll('#tree .collapse:not(.show)'));
  // 执行动作
    var collapseList = collapseElementList.map(function (collapseEl) {
        return new bootstrap.Collapse(collapseEl);
    });
  // 文件夹展开动作
    var nodes = document.querySelectorAll('#tree .fa-angle-right');
    for (let i = 0; i < nodes.length; i++) {
        nodes[i].classList.remove('fa-angle-right');
        nodes[i].classList.add('fa-angle-down');
    }
}

function CollapseAllTreeView() {
    var collapseElementList = Array.prototype.slice.call(document.querySelectorAll('#tree .collapse.show'));
    var collapseList = collapseElementList.map(function (collapseEl) {
        return new bootstrap.Collapse(collapseEl);
    });

    var nodes = document.querySelectorAll('#tree .fa-angle-down');
    for (let i = 0; i < nodes.length; i++) {
        nodes[i].classList.remove('fa-angle-down');
        nodes[i].classList.add('fa-angle-right');
    }
}
```