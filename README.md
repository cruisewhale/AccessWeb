# AccessWeb
学习AccessWeb记录 
===========

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

