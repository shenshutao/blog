---
layout: splash
title: "Log Monitering System 日志实时监测分析系统 ElasticSearch"
date:   2017-09-22 12:06:46 +0800
categories: java
comments: false
share: true
publish: false
---

##用到的工具：
- [Beats: Filebeat](https://www.elastic.co/products/beats/filebeat)
- [Elasticsearch](https://www.elastic.co/products/elasticsearch)
- [Kibana](https://www.elastic.co/products/kibana)
- Tomcat： 用来生成log

##环境
目前测试环境为Mac

##步骤
1. 配置filebeat.yml    
> filebeat.prospectors:    
>     - type: log
>        paths:    
>        - /Users/shutao/Documents/apache-tomcat-8.5.24/logs/*        
> output.elasticsearch:    
>    hosts: ["localhost:9200"]  

2. 配置config/elasticsearch.yml
> http.port: 9200
 
3. 运行elasticsearch
```sh bin/elasticsearch```

4. 运行filebeat
``` ./filebeat -e -v -c filebeat.yml ```

5. 配置config/kibana.yml 
6. 运行kibana
```sh bin/kibana ```
打开浏览器 http://localhost:5601



