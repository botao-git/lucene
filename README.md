# Lucene
## lucene 创建索引部分
### 1、存储数字
```java
doc.add(new NumericField("attach",Field.Store.YES,true).setIntValue(attachs[i]));
```

### 2、存储日期
```java
doc.add(new NumericField("date",Field.Store.YES,true).setLongValue(dates[i].getTime()));
```
