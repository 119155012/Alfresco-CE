 - ## Disable file thumbnails
```
vim /opt/bitnami/apache-tomcat/shared/classes/alfresco-global.properties

system.thumbnail.generate = false
```

---

 - ## Disable file quickshare
```
vim /opt/bitnami/apache-tomcat/shared/classes/alfresco-global.properties

system.quickshare.enabled = false
```

---

 - ## Disable document library page social(Favorite/Like/Comment) line
```
vim /opt/bitnami/apache-tomcat/webapps/share/WEB-INF/classes/alfresco/share-documentlibrary-config.xml

<!-- comment this line -->
<!-- <line index="50" id="social" view="detailed">{social}</line> -->
```

---

 - ## Replace document preview to metadata and disable comments
```
vim /opt/bitnami/apache-tomcat/webapps/share/WEB-INF/classes/alfresco/templates/org/alfresco/document-details.ftl

<!-- replace id="web-preview" to id="document-metadata" -->

<div class="yui-gc"> 
         <div class="yui-u first"> 
            <#if (config.scoped['DocumentDetails']['document-details'].getChildValue('display-web-preview') == "true")> 
                    <@region id="document-metadata" scope="template"/>  
            </#if> 
            <!-- <@region id="comments" scope="template"/>  -->
         </div>
```
```
/opt/bitnami/ctlscript.sh restart
```

---

 - ## Block non PDF file types upload
### Create a "block_type.js" below and upload to Repository / Data Dictionary / Scripts
```
function main() {
  var name = document.name;
  var siteName = document.siteShortName;
  var parent = document.parent;
  var ext = name.slice((name.lastIndexOf(".") - 1 >>> 0) + 2);

  if (ext !== 'pdf')
    throw "Unsupported file format. PDF and ZIP files are not supported at this time. File name:  " + name + ", Site Name: "  + siteName;
}

main();
```
### Select the target folder and click 'Manage Rules' then 'Create Rules'. Fill the options like below
![https://atechref.com/block-uploads-of-certain-file-type-to-sites-and-folders-in-alfresco-5-x/](https://user-images.githubusercontent.com/16496285/116969634-2ef38200-ace9-11eb-888e-002376d33531.png)

[https://atechref.com/block-uploads-of-certain-file-type-to-sites-and-folders-in-alfresco-5-x/](https://atechref.com/block-uploads-of-certain-file-type-to-sites-and-folders-in-alfresco-5-x/)

---

 - ## Customize title and logo of login page
```
Replace .svg in the path:
/opt/bitnami/apache-tomcat/webapps/share/themes/[depends_on_your_theme]/images/alfresco.svg
```
```
vim /opt/bitnami/apache-tomcat/webapps/share/WEB-INF/classes/alfresco/messages/slingshot_en.properties

app.name=DMS
app.community=
```

---

 - ## Customize background-color of login page
```
vim /opt/bitnami/apache-tomcat/webapps/share/themes/[depends_on_your_theme]/presentation.css

body.UNKNOWN
{
  background-color: #0c79bf;
}
```

---

 - ## Customize footer logo after login page
```
Replace .svg in the path:
/opt/bitnami/apache-tomcat/webapps/share/components/images/alfresco-logo.svg
```
