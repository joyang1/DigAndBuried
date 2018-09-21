## 问题一: flink1.6.0中集成ES6遇到的问题
> 问题描述

在我们代码的运行过程(build时候没有问题)中会遇到一下error信息:

org.apache.flink.runtime.client.JobExecutionException: TimerException{java.lang.NoSuchMethodError: org.elasticsearch.action.bulk.BulkProcessor.add(Lorg/elasticsearch/action/ActionRequest;)Lorg/elasticsearch/action/bulk/BulkProcessor;}

> 解决方案

这个是flink1.6.0之前的bug，我们有两种方案可以解决:

`方案一`

This is due to a binary compatibility issue between the base module (which is compiled against a very old ES version and the current Elasticsearch version).

As a work around you can simply copy org.apache.flink.streaming.connectors.elasticsearch.BulkProcessorIndexer to your project. This should ensure that the class is compiled correctly. 

继续使用1.6.0之前的版本集成es6的话,在本地项目中新建package：org.apache.flink.streaming.connectors.elasticsearch，然后把BulkProcessorIndexer.java文件拷贝到这个package下面，程序即可正常运行

`方案二`

使用1.6.1之后的版本，flink开发维护人员解释如下

[jira](https://issues.apache.org/jira/browse/FLINK-10271)

[github issue](https://github.com/apache/flink/pull/6682#discussion_r217266494)

我遇到问题在github上提问的[issue](https://github.com/apache/flink/pull/6391)

