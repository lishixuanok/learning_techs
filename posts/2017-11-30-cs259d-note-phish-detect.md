# Basic

|   layout   |    title   |
|:----------:|:----------:|
|   post     | 钓鱼网站识别 |

# Body

## 目的

身份验证，包括账户信息、登陆信息、身份信息。

## 攻击维度

貌似合法的网页

## 钓鱼特征

###  基于IP的URL

例如，http://192.168.0.1/paypal.cgi?fix account

* 特征：IP的url 

###  域名的使用年限

通常是短期注册的，通过WHOIS信息查询得到。

* 特征：域名生命周期小于60天

### 链接与名称不符的超链接标签

例如， <a href="badsite.com"> paypal.com</a> 

### 链接数

定义在<a>标签中的链接数

### 域名数量

1. 特征：http和https的数量

2. 特征：非顶级域名数量

3. 特征：不同的域名数量

### 小数点的数量

1. 非顶级域名的小数点数量多

www.subdomain.app.company.cn

2. 重定向域名的小数点数量多

例如，http://www.google.com/url?q=http://www.badsite.com

3. 特征：任一链接最大小数点

## 算法评估方法

### 10折交叉检验

### 随机森林-分类器

1. 10个决策树

2. 每个决定基于随机属性

### 公开的钓鱼检测网站

### 公开的钓鱼网站库

## TF-IDF

测量文档中词的重要性

TF: 文档中的词频

IDF: 测量词语在语料库中的流行度

## URL的健全性

1. 识别URL的词法特征

2. 使用TF-IDF选择特征词

## 算法

1. 计算TF-IDF的词语

2. 找到前五词语

3. 向google查询词语

4. 检查域名是否在Alexa top N名单中

5. 推测：钓鱼网站具有很低的网站评级

## 降低错误概率

在词法特征包括词法特征

## 其他特征

1. 域名年限

2. 知名商标

3. 可疑URL
...

# Refer

https://web.stanford.edu/class/cs259d/lectures/Session16.pdf


没看懂的

“Here” links to non-modal domain 


