# solr 配置自动同步数据库数据(全量,增量)
    
    solr6.3.3
    mysql-connector-java-5.1.45-bin.jar
    
    * 1.将 mysql-connector-java-5.1.45-bin.jar 放到 ./dist下
    
    * 2. 修改数据仓库下的配置文件 ./collocation1/conf/solrconfig.xml
    在大约70行左右的范围 加上一下两行
    <lib dir="${solr.install.dir:../../../..}/dist/" regex="solr-dataimporthandler-.*\.jar"/>
    <lib dir="${solr.install.dir:../../../..}/dist/" regex="mysql-connector-java-\d.*\.jar" />
    
    


    
    
    
