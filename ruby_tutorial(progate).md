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

#### クラスの定義方法
クラスに情報を持たせる場合は
`attr_accessor シンボル`
とする。
[attr_accessorリファレンス](https://docs.ruby-lang.org/ja/latest/method/Module/i/attr_accessor.html)
つなげて書くこともできる
``` ruby
class menu
    attr_accessor :name :price
end
```

#### インスタンスの生成、使用方法
生成
``` ruby
menu1 = Menu.new
```
インスタンス変数への代入
``` ruby
menu1.name = "すし"
puts menu1.name
#すし
```
#### クラスの中でのインスタンスメソッド定義、呼び出し
``` ruby
class menu
    attr_accessor :name :price
    def show
        puts "私はすしです"
    end
end
menu1 = menu.new
menu1.show
#私はすしです
```
引数も戻り値も普通に使える
``` ruby
class menu
    attr_accessor :name :price
    def show(data)
        return "わたしは#{data}です"
    end
end
menu1 = menu.new
puts menu1.show("すし")
#私はすしです
```
インスタンスメソッド内で
`self.変数名`
とすることで呼び出したインスタンス自身を使える。
``` ruby
class menu
    attr_accessor :name :price
    def show
        puts "私は#{self.menu}です"
    end
end
menu1 = menu.new
menu1.name = "すし"
puts menu1.show
#私はすしです
```
#### initializeメソッド
インスタンス生成時に呼び出されるメソッド
``` ruby
class menu
    attr_accessor :name :price
    def initialize
        self.name = "すし"
    end
end
menu1 = menu.new
puts "わたしは#{menu1.name}です"
#私はすしです
```
initializeメソッドにも引き数を渡せる
newするときに渡せばOK
``` ruby
class menu
    attr_accessor :name :price
    def initialize(name:,price:)
        self.name = name
        self.price = price
    end
end
menu1 = menu.new(name:"すし",price:"800")
puts "私は#{menu1.name}です。#{menu1.price}円です"
#私はすしです。800円です
```

#### クラス定義を呼び出す(外部ファイルを呼びだす)
requireを使う
(importではない)
``` ruby
#./menu.rbを呼び出す。.rbは省略できる
require "./menu"
```
#### インスタンスの配列
生成したインスタンスは配列に入れることができる
``` ruby
require "./menu"
menu1 = Menu.new(name:"りんご", price:100")
menu2 = Menu.new(name:"ごりら", price:200)
menues = [menu1,menu2]

menus.each do|menu|
    puts menu.info
end
```

#### 継承
めっちゃ簡単<て書くだけ
``` ruby
class Menu
    attr_accessor :name
    attr_accessor :price
end
class Food < Menu
    attr_accessor :calorie
    def calorie_info 
        puts "800カロリー"
    end
end
Food.calorie_info
```
#### オーバーライド
親クラスにあるメソッドを子クラスで定義すると上書きできる
子クラスのインスタンスは親ではなく子クラスのインスタンスを呼ぶようになる。
``` ruby
class Menu
    attr_accessor :name
    attr_accessor :price
    def info 
        self.name = "すし"
        self.price = 800
    end
end
class Food < Menu
    attr_accessor :calorie
    def info 
        self.calorie = 500
    end
end
Food.name
#すし
```
#### initializeもオーバーライドできる
``` ruby
class Menu
    attr_accessor :name
    attr_accessor :price
    def initialize(name:,price:)
        self.name = "わかめ"
        self.price = 500
    end
end
class Food < Menu
    attr_accessor :calorie
    def initialize(name:,price:,calorie:) 
        self.name = name
        self.price = price
        self.calorie = calorie
    end
end
Food1 = Food.new(name:"すし",price:300,calorie:500)
puts Food1.price
#300
puts Food1.calorie
#500
```
#### super
オーバーライドしたメソッドの中でsuperとすると、親クラスの同名メソッドを呼び出すことができる
子クラス（sub）に同名メソッドがあっても親クラス(super)のメソッドを呼び出せる
``` ruby
class Menu
    attr_accessor :name
    attr_accessor :price
    def initialize(name:,price:)
        self.name = "わかめ"
        self.price = 500
    end
end
class Food < Menu
    attr_accessor :calorie
    def initialize(name:,price:,calorie:) 
        super(name:name,price:price)
        self.calorie = calorie
    end
end
Food1 = Food.new(name:"すし",price:300,calorie:500)
puts Food1.price
#300
puts Food1.calorie
#500
```

#### Dateクラス
標準クラスの読み込み
``` ruby
require "date"
date1 = Date.new(2021,03,15)
puts date1
#2021-03-15
puts date.sunday?#インスタンスメソッドの使用
# false
```
dateクラスではDate.todayとすることによって
インスタンスを生成することもできる
``` ruby 
require "date"
date1 = Date.today
purs date1
# 2021/03/15
```
上記で使用した
`Date.today`
はクラスメソッドという
インスタンスメソッドとの違いは、クラスに対して呼び出すか
インスタンスに対して呼び出すかの違い、、、らしい

#### クラスメソッドの定義とよびだし
インスタンスメソッドの定義との違いは
メソッド名の前にクラス名を書く必要があること
呼び出し方法は定義時と同じようにクラス名+メソッド名
* クラスメソッドの定義
``` ruby
class Menu
    def Menu.is_discount_day?
        #処理
    end
end
puts Menu.is_discount_day?
```
* インスタンスメソッドの定義
``` ruby
class Menu
    def is_discount_day?
        #処理
    end
end
Menu1 = Menu.new
puts Menu1.is_discount_day?
```
クラスメソッドはnewしなくていいのが利点？

