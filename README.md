# SQL
UPDATE ...テーブル名<br>
SET...列名<br>
[WHERE]...<br>
whereがないと<strong>全件</strong>更新してしまう。

DELETE<br>
FROM...<br>
[WHERE]...<br>
whereがないと<strong>全件</strong>削除してしまう<br>
<strong><></strong> 左右が等しくない
  
  
  
  ## 3番目に高いものを取得
  SELECT 列名　　FROM テーブル名<br>
  ORDER BY 列名　LIMIT 1 OFFSET 2<br>
  （OFFSETは先頭から除外する行数）<br>
LENGTH (TRIM(000000)-1,2) -1は000000の後ろから1文字目ということ
  
  ##　和集合
  SELECT  文1
  　UNION (ALL)
  SELECT 文2
