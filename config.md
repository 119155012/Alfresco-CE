## Disable file thumbnails
```
vi /opt/bitnami/apache-tomcat/shared/classes/alfresco-global.properties

system.thumbnail.generate = false
```

---

## Disable file quickshare
```
vi /opt/bitnami/apache-tomcat/shared/classes/alfresco-global.properties

system.quickshare.enabled = false
```

---

## Disable document library page social(Favorite/Like/Comment) line
```
vi /opt/bitnami/apache-tomcat/webapps/share/WEB-INF/classes/alfresco/share-documentlibrary-config.xml

<!-- comment this line -->
<!-- <line index="50" id="social" view="detailed">{social}</line> -->
```

---

## Replace document preview to metadata and disable comments
```
vi /opt/bitnami/apache-tomcat/webapps/share/WEB-INF/classes/alfresco/templates/org/alfresco/document-details.ftl

<!-- replace id="web-preview" to id="document-metadata" -->
<div class="yui-gc"> 
         <div class="yui-u first"> 
            <#if (config.scoped['DocumentDetails']['document-details'].getChildValue('display-web-preview') == "true")> 
                    <@region id="document-metadata" scope="template"/>  
            </#if> 
            <!-- <@region id="comments" scope="template"/>  -->
         </div> 
```
