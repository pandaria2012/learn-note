# solr 配置 mmseg4j 分词器

    solr6.0.0
    mmseg4j-solr-2.4.0.jar
    mmseg4j-core-1.10.0.jar
    solr 以 jetty 方式部署 (非tomcat)
    
    mmseg4j [GitHub地址](https://github.com/chenlb/mmseg4j-solr)
    
    # 将 mmseg4j-solr-2.4.0.jar 和 mmseg4j-core-1.10.0.jar 放入到 solr 根目录下的 dist目录下
    
    # 在具体仓库根目录下的 solrconfig.xml 中 加入以下两行
    <lib dir="${solr.install.dir:../../../..}/dist/" regex="mmseg4j-core-\d.*\.jar" />
    <lib dir="${solr.install.dir:../../../..}/dist/" regex="mmseg4j-solr-\d.*\.jar" />
    
    # 然后编辑 具体仓库根目录下的 managed-schema 文件 加入以下几行(自定义字段域类型)
    # mode 有三种模式 complex simple max-word 
    <fieldType name="text_complex" class="solr.TextField" positionIncrementGap="100">  
        <analyzer>  
            <tokenizer class="com.chenlb.mmseg4j.solr.MMSegTokenizerFactory" mode="complex" />  
        </analyzer>  
    </fieldType>  

    <fieldType name="text_simple" class="solr.TextField" positionIncrementGap="100">  
        <analyzer>  
            <tokenizer class="com.chenlb.mmseg4j.solr.MMSegTokenizerFactory" mode="simple" />  
        </analyzer>  
    </fieldType>  

    <fieldType name="text_max_word" class="solr.TextField" positionIncrementGap="100">  
        <analyzer>  
            <tokenizer class="com.chenlb.mmseg4j.solr.MMSegTokenizerFactory" mode="max-word" />  
        </analyzer>  
    </fieldType> 
    
    # 然后相关字段 使用刚配置的字段与类型 即可
    <field name="name" type="text_max_word" indexed="true" stored="true" />
    
    
    
    
##### maven 打包 mmseg4j-solr-2.4.0 jar 包
    
    eclipse oxygen
    java8
    
    # pom.xml 文件
    <properties>
        <javadocExecutable>D:/dev/java/jdk/bin/javadoc</javadocExecutable>
        <JAVA_HOME>D:/dev/java/jdk</JAVA_HOME>
    </properties>
    
    <dependency>
        <groupId>jdk.tools</groupId>
        <artifactId>jdk.tools</artifactId>
        <version>1.7</version>
        <scope>system</scope>
        <systemPath>D:/dev/java/jdk/lib/tools.jar</systemPath>
    </dependency>
    
    # 注释掉
    maven-gpg-plugin 
    
    # 注意 maven 下载的 依赖 jar 包, 可能会有下载错误的情况, 删除掉相关的 jar, 重新下
    
    
    
    
    
    
    
    
    
    
    
    
    