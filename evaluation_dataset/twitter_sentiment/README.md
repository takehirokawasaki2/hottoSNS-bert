# Twitter日本語評判分析データセット：評価用
[Twitter日本語評判分析データセット](http://bigdata.naist.jp/~ysuzuki/data/twitter/)について，ツイート本文を復元した後，BERTモデル評価用に整形したもの

## 出典
* Twitter日本語評判分析データセット[Suzuki+, 2017]をクリーニング，分割したもの
* 以下のエントリを削除
  * 2つ以上の評判極性が付与されている
  * `pos,neg,neutral` 以外の評判極性が付与されている
* 残ったエントリを `train:dev:test = 8:1:1` に分割



## ファイル
* 本ディレクトリの格納ファイルは以下の通り
* 復元された評判分析コーパスは `train.tsv,dev.tsv.test.tsv` である

| ファイル名           | ファイル形式      | 説明                                                                                            |
|----------------------|-------------------|-------------------------------------------------------------------------------------------------|
| train.tsv | TSV，タブ区切り   | 学習用評判分析コーパス：データセットおよびツイートを統合したもの。Fine-Tuning時の学習用                                   |
| dev.tsv | TSV，タブ区切り   | 開発用評判分析コーパス：データセットおよびツイートを統合したもの。Fine−Tuning時の評価用                                   |
| test.tsv | TSV，タブ区切り   | 評価用評判分析コーパス：データセットおよびツイートを統合したもの。構築した評判分析モデルの評価用                                   |



## フォーマット
* `[train,dev,test].tsv` のフォーマットは以下の通り

| 列名        | 型       | 説明                                                                                                    |
|-------------|----------|---------------------------------------------------------------------------------------------------------|
| id          | str      | データ番号．Twitter日本語評判分析データセットにて採番されたもの                                         |
| category_id | str      | ジャンルID．詳細は[データセット説明](http://bigdata.naist.jp/~ysuzuki/data/twitter/)を参照              |
| status_id   | str      | ツイートID．ツイートの一意な識別子                                                                      |
| label_type  | str      | 評判極性ラベル，全5種類．詳細は[データセット説明](http://bigdata.naist.jp/~ysuzuki/data/twitter/)を参照 |
| created_at  | datetime | ツイートの投稿日時                                                                                      |
| user_id     | str      | 投稿者のID．Twitterユーザの一意な識別子                                                                 |
| screen_name | str      | 投稿者のスクリーン名                                                                                    |
| text        | str      | ツイート本文（改行コードを含む）                                                                        |

## 読み込み
* 読み込みには `pandas.read_csv()` methodを使用するとよい

```
import csv
import pandas as pd

# Python2
df_corpus = pd.read_csv(PATH, header=0, sep="\t", quoting=csv.QUOTE_NONE, encoding="utf-8", dtype=unicode, parse_dates=[4])
# Python3
df_corpus = pd.read_csv(PATH, header=0, sep="\t", quoting=csv.QUOTE_NONE, encoding="utf-8", dtype=str, parse_dates=[4])
```



以上