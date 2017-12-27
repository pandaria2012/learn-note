# solr 配置自动同步数据库数据(全量,增量)
    
    solr6.3.3
    mysql-connector-java-5.1.45-bin.jar
    
    * 1.将 mysql-connector-java-5.1.45-bin.jar 放到 ./dist下
    
    * 2. 修改数据仓库下的配置文件 ./collocation1/conf/solrconfig.xml
        在大约70行左右的范围 加入以下几行
        <lib dir="${solr.install.dir:../../../..}/dist/" regex="solr-dataimporthandler-.*\.jar"/>
        <lib dir="${solr.install.dir:../../../..}/dist/" regex="mysql-connector-java-\d.*\.jar" />
            <requestHandler name="/dataimport" class="org.apache.solr.handler.dataimport.DataImportHandler">
              <lst name="defaults">
                   <str name="config">data-config.xml</str>
              </lst>
        </requestHandler>
    
    * 3. 再在 ./collocation1/conf 创建 data-config.xml文件, 内容如下:
    
        <?xml version="1.0" encoding="UTF-8" ?>
        <dataConfig>
            <dataSource type="JdbcDataSource" name="test" driver="com.mysql.jdbc.Driver" url="jdbc:mysql://127.0.0.1:3306/test" user="root" password="1234"/>
                <document>
                    <entity 
                        pk="id" 
                        dataSource="test" 
                        name="t_product"  
                        query="select id,name,alias_name,old_product_id,top_product_id,type from t_product where status = '1' " 
                        deltaQuery="select id from t_product where update_dt > '${dataimporter.last_index_time}'"
                        deletedPkQuery="select id from t_product where status = 10"
                        deltaImportQuery="select id,name,alias_name,old_product_id,top_product_id,type from t_product where id='${dataimporter.delta.id}'"
                        >
                         <field name="id" column="id" />
                         <field name="name" column="name" />
                         <field name="alias_name" column="alias_name" />
                         <field name="old_product_id" column="old_product_id" />
                         <field name="top_product_id" column="top_product_id" />
                         <field name="type" column="type" />
                    </entity>
               </document>
        </dataConfig>
        
        # 同步数据语句 
        query="select id,name,alias_name,old_product_id,top_product_id,type from t_product where status = '1' "
        # 增量同步语句 只去 id 用于 只同步被修改的 根据 ${dataimporter.last_index_time}'
        # 这里注意时间 update_dt 为int, dataimporter.last_index_time为 timestamp
        deltaQuery="select id from t_product where FROM_UNIXTIME(update_dt , '%Y-%m-%d %H:%i:%S') > '${dataimporter.last_index_time}'"
        # 拉取 增量同步需要修改的数据
        deltaImportQuery="select id,name,alias_name,old_product_id,top_product_id,type from t_product where id='${dataimporter.delta.id}'"
        # 同步需要删除的数据
        deletedPkQuery="select id from t_product where status = 10"

    
    * 4. 在 ./bin 的 solr.in.sh 内 修改 solr 的默认时区为 PRC, 大约在 60+ 行
    
        # By default the start script uses UTC; override the timezone if needed
        SOLR_TIMEZONE="Asia/Shanghai"
        
        # 不生效的话 可以修改 ./bin/solr 
        vim solr
        搜索 /UTC/
        改为 Asia/Shanghai
    
    * 5. 定时脚本修复
    
        # 在索引之前先清除索引
        clean=true    
        # 无论做什么操作  都提交
        commit=true
        # 更新那个实体对应 的 配置文件中的 实体
        entity=t_product
        # 无论做什么操作 都优化
        optimize=false
        # 是否开启 debug
        debug=false
        # 是否阻塞所有请求
        synchronous=false
           
        # 增量更新数据
        http://localhost:8983/solr/collocation1/dataimport?command=delta-import&clean=true&commit=true&wt=json&indent=true&entity=t_product&verbose=false&optimize=false&debug=false&synchronous=false&id=1
        # 全量跟新数据
        http://localhost:8983/solr/collocation1/dataimport?command=full-import&clean=true&commit=true&wt=json&indent=true&entity=t_product&verbose=false&optimize=false&debug=false&synchronous=false
        # 重载配置
        http://localhost:8983/solr/collocation1/dataimport?command=reload-config
        # 查看运行的统计状态
        http://localhost:8983/solr/collocation1/dataimport?command=status
        # 查看配置
        http://localhost:8983/solr/collocation1/dataimport?command=show-config













    
    
    
