# Elasticsearch
## 查看所有的index:
` curl 'localhost:9200/_cat/indices?v' `
` curl 'localhost:9200/_alias/indexname

## 查询插件
```
http://qalocales01.intranet.theknot.com:9200/_plugin/marvel/sense/index.html 
GET storefront/profile/5f241487-52d8-4b6f-85ec-a6dc00ef6cf8
GET [index]/[document]/[id]
```
## API
https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-create-index.html

## C#
http://www.cnblogs.com/luxiaoxun/archive/2015/10/11/4869509.html

## Java
http://blog.csdn.net/u014039577/article/details/52439766

## Modidy Type
`
http://www.tuicool.com/articles/7nIbIz
`
## 新增字段
- 给admin[index]的account[type]添加两个字段，注意不要用自动生成的，那样没法search，可以用下面的插件去执行
http://localhost:9200/_plugin/marvel/sense/index.html
```
PUT admin/_mapping/account
{
  "properties":{
    "usernamessDenormalized": {
      "type": "string",
        "fields": {
           "substring": {
              "type": "string",
              "index_analyzer": "autocomplete",
              "search_analyzer": "standard"
           }
        }
      },
    "emailsDenormalized": {
    "type": "string",
      "fields": {
         "substring": {
            "type": "string",
            "index_analyzer": "autocomplete",
            "search_analyzer": "standard"
         }
      }
    }
  }
}
```
当看到 acknowledged true，说明新建成功了，然后查询一下。
```
GET admin/account/_mapping
```
或者用curl XPOST | XPUT执行。


# 相关文档
http://itindex.net/detail/54724-elasticsearch-mapping

