---
layout: splash
title: "NLP Information Extraction 自然语言处理 信息提取"
date:   2017-09-29 10:06:46 +0800
categories: text mining
comments: false
share: true
publish: true
---

# Python代码
https://github.com/shenshutao/Machine-Learning/blob/master/Text%20Mining/3-tag-stanford.py

# 前期准备
在这里我们使用了Stanford的NLP小组的一些工具，请从https://nlp.stanford.edu/software 下载。（当然大家不要局限于这个库，很多大公司像Google也有提供它的一套API）
- Stanford POS Tagger
- Stanford Named Entity Recognizer
- Stanford CoreNLP

# 待分析的句子
```
Professor Tan Eng Chye, NUS Deputy President and Provost, and Professor 
Menahem Ben-Sasson, President of HUJ signed the joint degree agreement at NUS, 
in the presence of Ambassador of Israel to Singapore Her Excellency Amira Arnon 
and about 30 invited guests, on July 03, 2013.
```

# 步骤一 Tokenize
Tokenize将会把句子(text)拆分成独立的有顺序的一个一个的字(words).    
句子(字符串）：Professor Tan Eng Chye, NUS Deputy President ...
Tokenize以后（数组）：'Professor' 'Tan' 'Chye' ',' 'NUS' 'Deputy' 'President' ...
```
word_tokenize(sent)
```

# 步骤二 POS(part-of-speech) Tagging
基于字的前后文，判断该字的类别,比如     
[('Professor', 'NNP'), ('Tan', 'NNP'), ('Eng', 'NNP'),('Chye', 'NNP'), (',', ','), ('NUS', 'NNP'), ('Deputy', 'NNP'), ('President', 'NNP'), ('and', 'CC'), ('Provost', 'NNP') ...      
分类介绍： https://catalog.ldc.upenn.edu/docs/LDC99T42/tagguid1.pdf
```
st_pos=StanfordPOSTagger(pos_model_path, pos_jar_path)
send_pos = st_pos.tag(word_tokenize(sent))
```

# 步骤三 NER(Named Entity Recognizer) Tagging
把这个步骤叫做步骤三也不准确，因为从代码上面来看，是直接从第一步就可以跳到NER tagging。    
不过，NER一般是基于POS tagging，然后根据一些上下文的Pattern，来判断该字的类别，如下代码会识别三种类型：PERSON, ORGANIZATION 和 LOCATION。
[('Professor', 'O'), ('Tan', 'PERSON'), ('Eng', 'PERSON'), ('Chye', 'PERSON'), (',', 'O'), ('NUS', 'ORGANIZATION'), ('Deputy', 'O'), ('President', 'O'), ('and', 'O'), ('Provost', 'O') ...      
```
... stanford-postagger-full-2017-06-09/models/english-bidirectional-distsim.tagger
st_ner = StanfordNERTagger(ner_model_path, ner_jar_path)
sent_ne = st_ner.tag(word_tokenize(sent))
```

如果使用7种类型的Tagger，可以识别7种类型：Person, Organization, Money, Percent, Date, Time.
```
... stanford-ner-2017-06-09/classifiers/english.muc.7class.distsim.crf.ser.gz
st_ner7 = StanfordNERTagger(ner7_model_path, ner_jar_path)
sent_ne7 = st_ner7.tag(word_tokenize(sent))
sent_ne7
```

# 步骤四 提取信息 Extract Information
可以把相邻的同类别信息连起来，可以得到以下信息：     
- PERSON       Tan Eng Chye
- ORGANIZATION NUS
- PERSON       Menahem Ben-Sasson
- ORGANIZATION HUJ
- ORGANIZATION NUS
- LOCATION     Israel
- ORGANIZATION Singapore Her Excellency Amira Arnon
- DATE         July 03 , 2013