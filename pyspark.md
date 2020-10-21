---
marp: true
_class: lead
theme: gaia
header: ''
footer: '@takap'

size: 16:9
page_number: true
paginate: false
style: |
    section.title * , h3{
        text-align: center;
    }
---

# **Pyspark** の初めの1歩

---

## アジェンダ
+ やること、やらないこと
+ Pysparkとは?
+ 使い方は?
+ 気を付けるべき点
+ まとめ

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>

---

## やること
+ spark sqlでcsvをSQL文で抽出するー!

---

## やらないこと
+ 難しいこと全部!

---

## Pysparkとは?

簡単に言えばApache SparkをPythonで使うよーって事!
Apache Spark(https://spark.apache.org/documentation.html)
現在はversion3.xまで出ている

そのため、Pysparkはなんなのかということは、sparkを理解すればOK！

---

## Apache Sparkとは?(wiki君より)

Apache Sparkとは**オープンソース**のクラスタコンピューティングフレームワークである。暗黙のデータ並列性と対象外性を備えたクラスタ全体をプログラミングできる(wiki参照)

...

......

wikiから見たのがいけないんだ!公式を見てみよう!

---

## Apache Sparkとは?(こーしき)

大規模なデータ処理のための統合分析エンジン。java, scale, PythonおよびRのAPIを提供!
また、SQLおよび構造化データ処理のためのSparkSQL,機械学習のためのMLlib、グラフ処理のためのGraphX、逐次計算およびストリーム処理のための構造化ストリーミングを含む高レベルの充実ツールがあるよ!

......

---

![ center](assets/strongword.jpg)

---
<!-- Scoped style -->
<style scoped>
li {
  font-size:30px;
}
</style>

## Apache Sparkとは?
+ 大量のデータを高速に処理したいときに使うよ
+ サーバを跨いだ並列処理が行えるよ
+ sparkは以下のプログラム言語から使用できるよ
  + java, Scala, Python, R
+ sparkは以下の機能が提供されてるよ
  + 構造化データを処理したいならSpark SQL
  + 機械学習を行いたいなら、アルゴリズムが用意されているMLlib
  + グラフを扱って計算とかしたいならGraphX
  + ストリームデータをリアルタイム処理したいならSpark Streaming

---

<!-- Scoped style -->
<style scoped>
section {
  font-size:20px;
}
</style>

![w:700 h:500 center](assets/image.png)

引用(https://speakerdeck.com/chie8842/pythondeda-liang-detachu-li-pysparkwoyong-itadetachu-li-tofen-xi-falsekihon?slide=14)


---

## 使い方

環境構築はいろいろとめんどそうだった(jdkいれて、spark入れてパス通してうんぬんかんぬん)ので、docker-hubで公開されている**jupyter公式**のイメージを拝借したいと思います

url(https://hub.docker.com/r/jupyter/pyspark-notebook)

```js
$ docker pull jupyter/pyspark-notebook
$ docker run -itdp 8888:8888 jupyter/pyspark-notebook
```

---

## Jupyterとは

データ分析、研究機構当でよく利用されています(知りませんでいた...)
ブラウザ上でコードを実行できたり、ドキュメントを作成できたり便利そう!


---

# まずはチュートリアル!

Sparkにあるクイックスタート(https://spark.apache.org/docs/latest/quick-start.html)



---

## 使い方(python api)

まずは公式が出してるpythonAPI(http://spark.apache.org/docs/latest/api/python/index.html)
うーん、いくつかみたことあるのが居ますねー

+ pyspark.SparkContext
  + これがないと始まらないメインエントリポイント
+ 

---


---

<!-- Scoped style -->
<style scoped>
section {
  font-size:30px;
}
</style>

```python
from pyspark.sql.types import *
from pyspark.context import SparkContext
from pyspark.sql.session import SparkSession

sc = SparkContext('local')
spark = SparkSession(sc)

struct = StructType([
  StructField('name', StringType(), False),
  StructField('type1', StringType(), False),
  StructField('type2', StringType(), True),
])

df = spark.read.csv('pokemon.csv', schema=struct)
df.show(5)
df.groupBy('type1').count().sort('count', ascending=False).show(5)

```

---
## 参考資料
apache spark(https://spark.apache.org/documentation.html)

pyspark(https://spark.apache.org/docs/latest/api/python/index.html)

Apache Sparkの初心者が環境構築とPySparkでのデータ集計までやってみる(https://qiita.com/mkyz08/items/0c1d8fa47179933c3a56)

---