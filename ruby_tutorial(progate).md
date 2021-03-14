## Rubyの基本的な書き方について
* progateにてやったことを書く

#### 変数展開
変数の値を文字列へ含める場合は文字列の中で
\#{変数名}とすることによって含めることができる。

``` ruby 
name = "purotoko"
puts "こんにちは#{name}さん"
#こんにちはpurotokoさん
```
ちなみに+でも連結できるが解説に出てきたのは一回だったので使われてないんだと思う。

また、シングルクォーテーションでくくった場合は展開されないので注意
``` ruby 
name = "purotoko"
puts 'こんにちは#{name}さん'
#こんにちは#{name}さん
```
#### if文の書き方

``` ruby
if 条件式
    #処理
elsif 条件式
    #処理
else
    #処理
end
```
大小比較、比較演算子はjsと同じ
!=とか==とか>=とか

#### eachの書き方
(変数をカウントするタイプのforとか使われていない感じなのかな？やっぱり、みずらくなるとかの理由?)
``` ruby
names = ["purotoko","usako","hara"]

names.each do|name|
    puts name
end
# purotoko
# usako
# hara
```
#### ハッシュの作り方
``` ruby
user = {"name" => "purotoko", "age" => 21}
```

また、ハッシュのキーには**シンボル**がよく使われるとのこと
``` ruby
user = {:name => "purotoko", :age => 21}
```

そして=>も省略できるみたいで最終的に以下のようにもできる
``` ruby
user = {name: "purotoko", age: 21}
```
**シンボルなんで左から右へ移動したん....?** 見やすいからこっちのほうがいいけれど

#### ハッシュの取り出し方
``` ruby
user = {"name" => "purotoko", "age" => 21}
puts user["name"]
```
これもシンボルが使える
``` ruby 
puts user[:name]
```
一般的にはシンボルなので、そのようにしていく

#### 配列の中のハッシュ
配列のなかにハッシュを入れることができる
``` ruby
users = [
    {name:"purotoko",age:27},
    {name:"usako",age:17}
]
puts users[1][:name]
#usako
```
##### eachもできる
``` ruby
users = [
    {name:"purotoko",age:27},
    {name:"usako",age:17}
]
users.each do|user|
    puts user[:name]
end
# purotoko
# usako
```


#### nilとは
nullみたいなもの。何もない状態をあらわす

##### if nil
falseを返すから結構つかえるとのこと
``` ruby
user = {name:"purotoko"}
if user[:age]
    puts "true"
else
    puts "false"
end
```

#### メソッドの使用方法
引数なし
``` ruby 
def sample
    puts "こんにちは"
end
sample
```

引数あり
``` ruby 
def sample(hello,name)
    puts hello + name
end
sample("こんにちは","purotoko")
```

戻り値ありのメソッド
returnをつける
また、 **真偽値を返すメソッドはメソッド名の末尾に?をつける慣習あり**
覚えておく
``` ruby 
def nave?(num)
    return num < 0
end
puts navi?(5)
#false
```
複数のreturnがある場合は最初のreturn優先

##### キーワード引数について
下記のようにキーワードをつけることができる
``` ruby 
def navi(num:,name:)
    puts "#{name}は#{num}才"
end
navi(num:5,name:"purotoko")
```

