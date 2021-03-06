# SQL
教材：スッキリわかるSQL入門（中山清喬/飯田理恵子・著）<br>
間違えた問題を中心にまとめ<br>
ブラウザ上でSQLが実行できるサイトがあるのでそこで練習。
## データの更新
UPDATE ...テーブル名<br>
SET...列名<br>
[WHERE]...<br>
whereがないと<strong>全件</strong>更新してしまう。

## データの削除
DELETE<br>
FROM...<br>
[WHERE]...<br>
whereがないと<strong>全件</strong>削除してしまう<br>
<strong><></strong> 左右が等しくない

## 文字列関係
### 文字列の一部抽出
EX) 口座テーブルから更新日を抽出、更新日の形式を変える2021-01-01から2021年1月1日に<br>
SELECT SUBSTRING(CAST（更新日 AS VARCHAR）,1,4)|| '年'　|| SUBSTRING(CAST(更新日 AS VARCHAR),6,2)||'月'　SUBSTRING(CAST（更新日　AS VARCHAR）,9,2） || '日' AS 更新日<br>
FROM 口座

EX)口座テーブルから名義の1〜5文字目に「カワ」が含まれるものの抽出<br>
SELECT * <br>
FROM 口座　<br>
WHERE SUBSTRING (名義,1,5)LIKE　’％カワ％’
### 文字列の置き換え
(REPLACE(名義,' ',''))空白をなしにする

  
## 3番目に高いものを取得
  SELECT 列名　　FROM テーブル名<br>
  ORDER BY 列名　LIMIT 1 OFFSET 2<br>
  Q.11番目は…？？<br>
  
  
  （OFFSETは先頭から除外する行数）<br>
LENGTH (TRIM(000000)-1,2) -1は000000の後ろから1文字目ということ
  
  ## 並び替え
  ①で昇順、②で降順の場合<br>
  ORDER BY ①,②desc
  
  ## 列番号指定の並び替え
  ここでいう列番号は結果表に出てくる列番号。つまりSELECTした順番<br>
  まず入金額で並び替え、同じ額については出金額で並び替え<br>
  SELECT入金額,出金額　FROM 家計簿　ORDER BY 1 DESC<br>
  3列目で並び替え、3列目の数字が同じ場合は1列目で並び替える<br>
  ORDER BY 3、1
  
  ## 和集合
  SELECT  文1<br>
  　UNION (ALL)<br>
  SELECT 文2<br>
  複数のテーブルから情報を取ってくるとき
  
  ## 演算子
  同じ意味の演算子：NOT IN と　<>ALL 全ての値と一致しない<br>
  同じ意味の演算子IN と　=ANY いずれかの値と一致することを判定<br>
  <strong>[文字列の|| 連結]</strong><br>
  EX) 'カ）'　|| 名義　
  ## CASE 演算子
  railsでいうifみたいなもの<br>
  EX)費目に応じて変換<br>
  SELECT 費目, 出金額,<br>
    CASE 費目　WHEN '居住費'　THEN '固定費'<br>
  　　　　　WHEN　’水道光熱費’　THEN ’固定費’<br>
  　　　　　ELSE ’変動費’<br>
  END AS　出費の分類<br>
  FROM 家計簿　WHERE 出金額　0
  ## IN演算子
  IN 演算子で複数の値リストと比較<br>
　　　　WHERE 00 IN（値,値,値）
  
  
  ## 集計関数
  条件式を用いずにCOUNTする<br>
  EX) SELECT　COUNT（*） - COUNT(更新日) AS 更新日が登録されていない件数<br>
  FROM　口座
  
  
  ## テーブルの削除
  DROP TABLE テーブル
  ## テーブル定義の変更
  * 列の追加　ALTER TABLE テーブル名　ADD 列名　型　制約
  * 列の削除　ALTER TABLE テーブル名　DROP 列名　型　制約
  ## 正規化の順番
  * ①繰り返し列の排除
  * ②複合主キーの一部への関数従属（部分関数従属）
  * ③間接的な関数従属（推移関数従属）
  
  
  ## 関数
  * CAST関数……データ型の変更を行う関数<br>
  CAST (変換する値　AS 変換するデータ型)
  * TRUNC関数……指定行で切り捨てる関数<br>
  TRUNC(数値を表す列, 有効とする桁数)
  * CURRENT_DATE……現在の日付を表す
  * CURRENT_TIME……現在の時間を表す
  * COALESCE関数<br>
  <strong>COALESCE（引数1,引数2）……引数のうち最初に現れたNULLでない引数<br>
    NULLの場合の代替の値を入れるときに使うことが多いかも<br></strong>
  
  
  EX) 更新日が登録されていない場合は’設定なし’と表記する<br>
  SELECT COALESCE（CAST（更新日 AS VARCHAR）,'設定なし'）　AS 更新日　FROM　口座
  
  * ROUND関数……指定桁で四捨五入<br>
  ROUND（数値を表す列,有効とする桁数）
  ## テーブルの結合
  SELECT 選択列リスト<br>
  FROM テーブルA<br>
  JOIN テーブルB<br>
  ON 両テーブルの結合条件<br>
  * 同じカラム名がある場合は「テーブル名.カラム名」とすればよい
  ## 論理演算子の優先順位
  1. NOT
  2. AND
  3. OR
  
