# 100 Days Of Code - Log

### Day 4: March  27, 2019 

**Today's Progress**: 
- 今までgeojsonの生成をcontrollerで行なっていたが、MVCのポリシーからするとしっくりきていなかった。Ruby on Rails5アプリケーショんプログラミングで学び、viewで生成を行うように変更を行なった。

before:areas_controller.rb
```
def geojson
    @area = Area.find(params[:id])
    @area_blocks = @area.area_blocks
    geojson = { "type" => "FeatureCollection",
                "features" => [],
              }
    @area_blocks.each_with_index do |block, index|
      geojson["features"]<<{"type" => "Feature",
                            "properties" => {
                              "_color" => "#000000",
                              "_opacity" => 0.4980392156862745,
                              "_weight" => 3,
                              "_fillColor" => "#ff0000",
                              "_fillOpacity" => 0.4980392156862745
                              },
                            "geometry" => {
                              "type" => "Polygon",
                              "coordinates" => [],
                              }
                            }
      points = []
      block.boundary_points.order(:sequence).each do |point|
        points<<[point[:longitude], point[:latitude]]
      end
      geojson["features"][index]["geometry"]["coordinates"]<<points
      geojson["features"][index]["properties"]["name"] = block.area.icao_abbreviation.kanji_name
      unless Rails.env.production?
        geojson["features"][index]["properties"]["id"] = block.id
      end
      geojson["features"][index]["properties"]["upper_altitude"] = block.upper_alt
      geojson["features"][index]["properties"]["lower_altitude"] = block.lower_alt
    end
    render :json => geojson
  end
```
after:geojson.json.jbuilder
```
json.type "FeatureCollection"
json.features do
  json.array! @area.area_blocks do |block|
    json.type "Feature"
    json.properties do
      json._color       "#000000"
      json._opacity     0.4980392156862745
      json._weight      3
      json._fillColor   "#ff0000"
      json._fillOpacity 0.4980392156862745
      unless Rails.env.production?
        json.id block.id
      end
      json.name           block.area.icao_abbreviation.kanji_name
      json.upper_altitude block.upper_alt
      json.lower_altitude block.lower_alt
    end
    json.geometry do
      json.type "Polygon"
      points = []
      block.boundary_points.order(:sequence).each do |point|
        points<<[point[:longitude], point[:latitude]]
      end
      json.coordinates [points]
    end
  end
end
```

**Thoughts:**  便利なテンプレートを用いると、見た目もスッキリ、書きやすい。

**Link to work:**

**refer**



### Day 3: March  23-24, 2019 

**Today's Progress**: 
- 図書情報館での情報収集（２３日）とturbolinksの適用（２４日）。turbolinksが適用されていた場合、ページのリロードが行われないため、jQueryの`$(function(){ 処理 });`が効かなかった。そこで、`$(document).on('turbolinks:load', function(){ 処理 });`で解決。
- gitでログを見たい時はほとんどが`git log --oneline --all --graph`のため、アエリアスを設定した。

**Thoughts:**  javascriptの実行されるタイミングをよく理解していない。

**Link to work:**

**refer
- [Rails5でjqueryを動かす方法](https://qiita.com/hiroyayamamo/items/b258acbaa089d9482c8a)
- [gitで便利なエイリアス達](https://qiita.com/peccul/items/90dd469e2f72babbc106)


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
