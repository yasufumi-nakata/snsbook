# 3.1 ホジキン・ハクスレーモデルのシミュレーション

## ファイル一覧
- `hh.c`: ホジキン・ハクスレーモデル (リスト3.1)
- `hh1.c`: リスト3.1を修正して、図3.2を作成するときに使ったもの
- `fr.c`: リスト3.1を修正して、図3.3を作成するときに使ったもの
- `sfa.c`: 発火頻度適応のモデル
- `ia.c`: Type Iニューロンのモデル (コナー・スティーブンスモデル)
- `Makefile`: Makefile
- `README-ja.md`: 日本語の説明 (このファイル)

## コンパイル方法
テキスト通りにコンパイルするか、もしくは`make`すると全て自動的にコンパイルされる。`make`
した場合は実行も自動的に行われる。`fr`の実行は少し時間がかかるが心配しなくてよい。

## 実行方法
`hh`はテキスト通りに実行すればよい。結果をファイルに出力した後、[0:1000]ミリ秒間の膜電位を
プロットすれば図3.1aが、[900:1000]ミリ秒間の膜電位をプロットすれば図3.1bがそれぞれ得られる。

`hh1`は
```
node00:~/snsbook/code/part1/hh$ ./hh1 > hh1.dat
```
としてファイルに出力した後、[-5:25]ミリ秒間の数値をプロットすればよい。ファイルの
フォーマットは
```
t V m h n
```
なので、例えばgnuplotでは
```
gnuplot> plot [-5:25] 'hh1.dat' using 1:2 title 'V' with lines
```
で膜電位がプロットされ、
```
gnuplot> plot [-5:25] 'hh1.dat' using 1:3 title 'm' with lines, 'hh1.dat' using 1:4 title 'h' with lines, 'hh1.dat' using 1:5 title 'n' with lines
```
でm, h, nの値が重ねてプロットされる。表示をうまくまとめると図3.2が得られる。

`fr`はテキストには説明はないが、実行すると外部電流の強度を変えながら発火頻度を計算していく。
出力のフォーマットは、
```
電流強度(\mu A / cm^2) 発火頻度(spikes/s)
```
である。これをプロットすると図3.3が得られる。

`sfa`は`hh`と同様に実行すればよい。結果をファイルに出力した後、[0:100]ミリ秒間の膜電位を
プロットすれば図3.4aが、[900:1000]ミリ秒間の膜電位をプロットすれば図3.4bがそれぞれ得られる。

`ia`も`hh`と同様に実行すれば良い。外部電流の強度はコード内で
```
double I_ext = 8.60941453; // micro A / cm^2
```
と定義しているので、この値を変えてシミュレーションを行えば、図3.5a, bが得られる。また、`fr.c`を
参考にして、強度を変えながら発火頻度を計算すれば、図3.6が得られる。

`make`した場合は、実行結果がそれぞれ`hh.dat`, `hh1.dat`, `fr.dat`, `sfa.dat`, `ia.dat`に出力される
ので、それらをプロットすればよい。

一通り試して見た後は、
```
make distclean
```
とすると、作成されたファイルを全て削除し、初期状態に戻すことができる (全てのシミュレーションで共通)。