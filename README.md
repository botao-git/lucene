### Lucene学习

#### lucene 索引创建及检索部分



#### 一、 创建索引

##### 1、存储数字
```java
doc.add(new NumericField("attach",Field.Store.YES,true).setIntValue(attachs[i]));
```

##### 2、存储日期
```java
doc.add(new NumericField("date",Field.Store.YES,true).setLongValue(dates[i].getTime()));
```


#### 二、 删除索引

##### 1、通过writer来删除
```java
writer.deleteDocuments(new Term("id","1"));
writer.commit();
```

##### 2、通过reader来删除
```java
reader.deleteDocuments(new Term("id","1"));
reader.close();//如果用Reader来删除的话，当前reader对象可以判断出已删除的索引，但是如果希望其他reader也能识别出来，就需要commit
```

#### 三、 恢复删除的索引

##### 通过reader来进行恢复
```java
IndexReader reader = IndexReader.open(directory,false);
//恢复时，必须把IndexReader的只读(readOnly)设置为false
reader.undeleteAll();
reader.close();
```

#### 四、 更新索引

##### 更新索引的本质是：**删除索引再创建索引**
```java
Document doc = new Document();
doc.add(new Field("id","11",Field.Store.YES,Field.Index.NOT_ANALYZED_NO_NORMS));
doc.add(new Field("email",emails[0],Field.Store.YES,Field.Index.NOT_ANALYZED));
doc.add(new Field("content",contents[0],Field.Store.NO,Field.Index.ANALYZED));
doc.add(new Field("name",names[0],Field.Store.YES,Field.Index.NOT_ANALYZED_NO_NORMS));
writer.updateDocument(new Term("id","1"), doc);
```
