# SQL
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

## 文字列の一部を抽出する関数
EX)口座テーブルから名義の1〜5文字目に「カワ」が含まれる<br>
SELECT * FROM 口座　WHERE SUBSTRING (名義,1,5)LIKE　’％カワ％’
  
  
  
  ## 3番目に高いものを取得
  SELECT 列名　　FROM テーブル名<br>
  ORDER BY 列名　LIMIT 1 OFFSET 2<br>
  （OFFSETは先頭から除外する行数）<br>
LENGTH (TRIM(000000)-1,2) -1は000000の後ろから1文字目ということ
  ## 列番号指定の並び替え
  * まず入金額で並び替え、同じ額については出金額で並び替え
  SELECT入金額,出金額　FROM 家計簿　ORDER BY 1 DESC
  
  ## 和集合
  SELECT  文1
  　UNION (ALL)
  SELECT 文2
  複数のテーブルから情報を取ってくる特
  
  ## 演算子
  同じ意味の演算子：NOT IN と　<>ALL 全ての値と一致しない<br>
  同じ意味の演算子IN と　=ANY いずれかの値と一致することを判定<br>
  文字列の|| 連結
  
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
