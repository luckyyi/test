- 安装ElasticSearch

  - https://www.elastic.co/downloads/elasticsearch
  
  从上面的地址下载安装，Past release中选择2.3.x [2|3], 5.x的插件安装老是失败。
  - 下载.zip文件，解压，进入bin目录，直接启动，或用命令安装成service.
  然后用localhost:9200查看，成功。
  - 安装插件
  ` plugin -install mobz/elasticsearch-head ` 有可能只是head
  - 输入plugin list 查看已安装插件  
  - http://localhost:9200/_plugin/head
  
- marvel插件
 - 先安装Kibana v4.6.x
 - https://www.elastic.co/downloads/kibana
 - 下载zip文件解压后，进入kibana/bin目录，启动kibana
 - http://localhost:5601
 
 - 在kibana中安装mervel插件
 
 ` kibana plugin --install elasticsearch/marvel/latest `
 
 在kibana的Settings菜单后面有个九宫格，点击，进入相应的插件。 
 
 安装Sense
 ` kibana plugin --install elastic/sense `
  
  
  
