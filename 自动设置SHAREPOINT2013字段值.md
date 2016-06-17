#使用URL通过 SPUtility.js 自动设置SHAREPOINT2013字段值或属性

参考文档及代码下载: http://sputility.codeplex.com/

做一个项目测试, 需要通过url直接打开SPS2013的一个文档库上传页面， 并自动将参数传递到这个文档库的字段

中，如：  /Lists/ProjectTasks/NewForm.aspx?projectID=523

SPUtility功能：

1. No server side code to deploy!

2. Hide a field from view Make a field read only

   1）设置字段值： SPUtility.GetSPField('Title').SetValue('Hello world!');

   2）设置字段只读：SPUtility.GetSPField('Title').SetValue('Hello world!').MakeReadOnly();

   3）隐藏字段：SPUtility.GetSPField('Complete').Hide();

3. Set or get field values in Document Libraries, all sorts of List forms (custom lists, issues, etc), and survey

这个脚本的使用很简单， 无需服务器部署。只要上传这个这个JS文件和JQUERY(当前版本推荐1.1x)以及用户的HTML文档到SPS的一个文档库, 目的是方便调用： 用户的HTML文档直接引用文档库中的SPUtility.js和 JQRERY.JS即可。在要使用这个功能的文档库或列表库的新建或修改页面， 插入Content editor webpart, 修改属性中的链接到之前上传到文档库的用户HTML。 具体按SPUtility中的安装说明操作即可。

在本项目中，通过Access Web App 调用 Sharepoint 2013的一个文档库的上传文档链接， 同时把参数传进文档库， 并存在一个字段中：

创建一个HTML文件， 存入以下代码, 这段代码作用是从URL的提取 ? 后的参数，并将值写入对应的字段中，

      <script src="http://pc3/testDocument/jquery-1.11.1.min.js"></script>
      <script src="http://pc3/testDocument/sputility.min.js"></script>
      <script>
      
       function getParameterByName(name, url) {
           if (!url) url = window.location.href;
           name = name.replace(/[\[\]]/g, "\\$&");
           var regex = new RegExp("[?&]" + name + "(=([^&#]*)|&|#|$)"),
              results = regex.exec(url);
           if (!results) return null;
           if (!results[2]) return '';
           return decodeURIComponent(results[2].replace(/\+/g, " "));
       }
      
       $(document).ready(function () {
           //alert('ssssss');
           try {
               //SPUtility.GetSPField('Title').SetValue(GetValueFromURL('title'));
               SPUtility.GetSPField('ProjectID').SetValue(getParameterByName('projectid'));
               //SPUtility.GetSPField('Name').SetValue(GetValueFromURL('name'));
               alert(getParameterByName('projectid'));
           } catch (ex) {
               alert(ex.toString());
           }
       });
      </script>
