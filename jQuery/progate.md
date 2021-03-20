#### jQueryの構文
```
$(セレクタ).メソッド(引数)
```

#### hide
要素を非表示にする
```
$('h1').hide();
```
#### show
cssで指定されてdisplayプロパティnoneをblockへ変更する
```
$('img').show();
```
#### fadeOut
要素をアニメーション付きで非表示にする  
薄くなって消える
```
$('h1').fadeOut();
$('h1').fadeOut(1500);
```
#### fadeIn
要素を表示させる  
徐々に
```
$(#'title').fadeOut();
$(#'title').fadeOut(1500);
```

#### slideUp
要素をアニメーション付きで非表示にする  
上方向に消える
```
$('h1').slideUp();
$('h1').slideUp('slow');
```

#### slideUp
要素をアニメーション付きで非表示にする  
下方向に表示
```
$('h1').slideDown();
$('h1').slideDown('slow'));
```

#### セレクタはidでいいならidを使用する
そのほうが処理が速いため

#### イベント構文
```
$('セレクタ').イベント名(function(){
   //処理 
});
```

#### clickイベント
```
$('#hide-text').click(function(){
    $('#text').hide();
});
```

#### cssメソッド
cssを変更できるメソッド
```
$('セレクタ').css('プロパティ名','値');
```

#### 色を変更する
```
$('p').css('color','red');
```
#### 表示、非表示
```
$('p').css('display','none');
$('p').css('display','blocj');
```

#### HTMLを変更する
```
$('p').text('こんばんは');
$('p').html(<span>こんばんは</span>);
```
#### this構文
イベントの中で起こった要素を取得することができる  
```
$('li').click(function(){
    $(this).css('color','red');
});
```

#### 変数
jqeryの変数宣言はわかりやすいように慣例として頭に$をつける
```
const $s = $('div');
$s.css('color','red');
$s.html('jQuery');
```

#### メソッドチェーン
メソッドはつなげることができる
```
const $s = $('div');
s.css('color','red').html('jQuery');
```
#### find
指定したセレクタのをもつ要素を全て取得する
```
$(#warapper).find('a').css('color','red');
```
#### children
指定したセレクタの持つ子要素の中から指定したセレクタに合致した要素を取得するとき使用する
```
$('wrapper').children('a').css('color','red');
```

#### hover
マウスが乗った時だけ処理
```
  $('#language-wrapper').hover(
      function(){
        $('.language-text').fadeIn();
      },
      function(){
        $('.language-text').fadeOut();
      }
    );
```

#jQueryの読み込み
bodyの終了タグの直前で読み込むとwebページの表示速度が上がる




