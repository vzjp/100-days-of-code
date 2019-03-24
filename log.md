# 100 Days Of Code - Log

### Day 3: March  23-24, 2019 

**Today's Progress**: 図書情報館での情報収集（２３日）とturbolinksの適用（２４日）。turbolinksが適用されていた場合、ページのリロードが行われないため、jQueryの`$(function(){ 処理 });`が効かなかった。そこで、`$(document).on('turbolinks:load', function(){ 処理 });`で解決。

**Thoughts:**  javascriptの実行されるタイミングをよく理解していない。

**Link to work:**

**refer [Rails5でjqueryを動かす方法](https://qiita.com/hiroyayamamo/items/b258acbaa089d9482c8a)


### Day 2: March  20, 2019 

**Today's Progress**: rails migrationで新規のcolumnを追加。
```rails generate migration add_altitude_to_area_blocks lower_alt:integer upper_alt:integer```

**Thoughts:** 

**Link to work:**

**refer [vimでのマクロ操作](https://qiita.com/Go-zen-chu/items/5464fb6b9e6b38c958bd)


### Day 1: March  19, 2019 

**Today's Progress**: Ruby on Rails のviewで、json出力する場合のテンプレートを作成。 => json出力する時はcontrollerで出力することが多いよう。主処理をhelperに渡して、controllerでjsonを出力する方向で。

**Thoughts:** 

**Link to work:**

**refer 


### Day 0: March  18, 2019 

**Today's Progress**: Ruby on RailsのFixtureが少し使えるようになった。fixtureの中でtestデータを作って他のモデルを参照した場合でその先のモデルにそのfixtureを用意していなかった時は、``undefined method xxx for nil:NilClass``となった。また、`dependent :destroy`で関連付けしたものに対するテストでは、test内で関連付けたものと、fixture内で関連づけられたものが消えたから`assert different`は`-2`となるべきところ、よく理解せず`-1`としていたため、テストが通らず苦労した。

**Thoughts:** testがあれば自身を持てる。これからも面倒臭がらずテストを書こう。

**Link to work:** 
