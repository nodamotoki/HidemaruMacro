# HidemaruMacro

# 秀丸のキーアサインを Emacs 風にする

VS Code に Emacs Friendly Keymap という Extension を入れて Emacs 風の
キーマップにしたので、秀丸も Emacs Friendly Keymap に合わせてキーマップを変更した。あと自分用に少し追加。

## ダウンロード

[ぼくの秀丸マクロ](https://github.com/nodamotoki/HidemaruMacro)

* LittleEmacs.KEY ファイル
* kill-line.mac (C-k)
* open-line.mac (C-o)
* recenter-top-bottom.mac (C-l)
* delete-other-window.mac (C-x 1)
* comment-region.mac (C-c C-c)
* keyboard-quit.mac (C-g)
* tab-to-tabstop.mac (M-i)
* just-one-space.mac (M-space)
* delete-horizontal-space.mac (M-\)
* delete-blank-lines.mac (C-x C-o)
* other-window (C-x o)
* C-u.mac (C-u 7 2 = で = を72個挿入したりする)
* C-x_o.mac (C-x o と C-x C-o を切り分ける)
* C-x-experimental.mac (C-x.mac の実験用)

おまけ

* hr.mac 水平線ひく
* datetime.mac 日付挿入
* hr-and-datetime.mac.mac 水平線引いて日付挿入
* keycode.mac キーコードを表示 (C-x の実験用)
* todo.mac TODO管理用のツール
* today.mac 今日の日付と曜日を挿入 "04/23(木)" とか
* backtab.mac Shift+TAB でカーソルより後ろの空白を一つ前のタブ位置まで消す

## インストール

1. .mac ファイルを秀丸のマクロフォルダに入れる。メニューからツール＞マクロ用のフォルダ で開く。たぶんデフォルトではここ↓
    C:\Users\name\AppData\Roaming\Hidemaruo\Hidemaru\Macro
2. LittleEmacs.KEY を秀丸の設計ファイル置き場に置く。たぶんここ↓
    C:\Users\name\AppData\Roaming\Hidemaruo\Hidemaru\Settings
3. LittleEmacs.KEY ファイルを秀丸のメニュー＞その他＞キー割り当て＞読込み で読み込む。

## キーストローク

基本的に [Emacs Friendly Keymap Extension](https://github.com/SebastianZaha/vscode-emacs-friendly) と同じ。
いくつかのキーはうまく設定できなかった（後述）。

## 追加したキーストローク

いくつか、Emacs Fridndly Keymap にはない秀丸の機能をキーに割り当てたり、マクロを書いたりした。

| キーストローク | 機能 | メモ
|:-|:-|:-|
| C-k | カーソルより後ろをカット | kill-region.mac で一応対応。
| | | マクロ内の変数 #kill_whole_line が 1 なら行頭で C-k すると改行も切り取る。
| | | 0 なら Emacs のデフォルトの動作になる。
| C-g | キャンセル | keyboard-quit.mac で一応対応。秀丸で Esc 押すのと同じ。
| M-i | タブ | tab-to-tabstop.mac で対応。
| C-o | 空行を挿入。カーソル位置はそのまま | open-line.mac で対応。
| C-x i | カーソル位置へ読込み | insert-file.mac で対応。
| C-c C-c | 選択範囲をコメント | comment-region.mac でざっくり対応。
| | | Emacs では C-u C-c C-c でアンコメントだが C-c C-c でトグルします。
| | | 対応言語は C/C++/Java/C#/Swift/Go/html/css/javascript/
| | | TypeScript/PHP/perl/python/ruby/shell/
| | | 秀丸マクロ(mac)/bat を予定。
| | | 言語はファイルの拡張子で判断する。判断できないときは '#' をコメント用の行頭文字と見なす。
| | | C/C++ のコメント形式はデフォルトで // コメント。
| | | /* */ コメントにする場合はマクロ内の $comment_text_pre/post を変更する。
| | | 他の言語も同様。言語ごとに設定できるようにしてある。(すべての言語でテストはしてないけど)
| M-space | カーソルの周囲の空白を1つにする | just-one-space.mac で実現。
| M-\ | カーソルの周囲の空白を全部削除 | delete-horizontal-space.mac で実現
| C-x C-o | 空行を一つにする | delete-blank-lines.mac で実現。
| C-x C-x | 前のカーソル位置 | Emacs では exchange-point-and-mark.
| C-@ | 直前の操作の繰り返し | Emacs では C-x z zzz...
| C-x y | やり直しのやり直し | 元 Ctrl-y。 C-x u が Undo なのでその隣。
| C-_ | やり直しのやり直し | C-/ がやり直しなので隣のキーに設定。
| C-\ | やり直しのやり直し | C-/ がやり直しなのでBackslashに逆の意味を。
| M-l | 小文字変換 | 範囲選択後実施する
| M-u | 大文字変換 | これも範囲選択必要。
| M-y | 貼り付け＋履歴戻し | Emacs の M-y (yank-pop) とはやや動きが違うけれど少し似てる。そのうちマクロで yank-pop 同等にしたい。
|M-s u | TAB -> 空白変換 | よくやるのでキー割り当て。
|M-s t | 空白 -> TAB 変換 | よくやるのでキー割り当て。
|M-s s | すべての候補を選択 | 直近の検索文字列をすべて選択。VS Code の Ctrl-d に似た機能。
|M-s c | すべての候補を色つけ | 直近の検索文字列に色つけしてハイライト
|M-s l | すべての候補を一覧表示 | 直近の検索文字列にヒットする一覧
|M-s y | 引用符付き貼り付け | メールの返信で使いたい。

### 制限付きのキーストローク

| キーストローク | 機能 | メモ
|:-|:-|:-|
| C-x C-l | 英小文字へ変換 | 「大文字 ←→ 小文字変換」にした。これは一文字ずつしか変換できない。いまいちだったので、M-l, M-u に別途、小文字変換、大文字変換を設定した。
| C-x 1 | 画面分割を解除して1画面にする | 秀丸に分割解除の単独コマンドはないので左右分割を割り当てた。左右分割中にもう一度左右分割すると1つに戻るので。
| C-x 2 | 左右二分割 | 左右分割するが、最大2分割まで。もう一度左右分割すると1つに戻る。
| C-x 3 | 上下二分割 | 上下分割するが最大2分割まで。もう一度丈夫分割すると1つに戻る。
| C-x z | 全画面表示 | Emacs では操作の　repeat 機能。Emacs Friendly Keymap では Zenモード(動かないけど)。とりあえず秀丸では全画面表示を割り当てる。
| C-l | 最後の編集箇所へ移動 | Emacs ではカーソル位置を画面センターにする機能。秀丸にこの機能は無い様子。かわりにもともとアサインされていたままコマンドにしておく。
| C-Enter | 改行 | Emacs Friendly Keymap ではなにか置換ダイアログで1つ置換に使うらしいが改行にしとく。
| C-M-n | 対応する括弧に移動 | Emacs Friendly Keymap ではeditor.action.addSelectionToNextFindMatch(デフォルト Ctrl-d)だが、 Emacs では forward-list とかなので Emacs の動きに近い処理にする
| C-' (C-^) | 単語補間 | Intellisense は秀丸にはないので単語補間のリスト表示にした。
| C-M-Space | Toggle Sidebar Visivility | これは秀丸のファイルマネージャ枠表示の切替にしてみた。でもトグル動作してくれないなあ。

### 設定していないキーストローク

| キーストローク | 機能 | メモ
|:-|:-|:-|
| C-x C-u | 英大文字へ変換 | C-x u (Undo) とかぶるので設定不可。Emacs でも間違いやすいので disabled になっている。
| C-x C-k | タブを全部閉じる | Emacs Friendly Keymap 独自のキーアサイン。C-x k (ファイルを閉じる)と区別が付かないので設定不可。
| M-x | コマンド入力窓 | この機能は秀丸には無い。
| C-; | 行ごとにコメント | 取り合えす C-c C-c で代替
| M-; | 選択範囲をコメント | これも C-c C-c で代替


## 制限

* 秀丸は C-x s と C-x C-s とかの<s>区別が付かない。</s> 区別つく。`iskeydown(0x11)` でCtrlキーが押されているかどうか判定できた。
* C-x s とか C-x r t とか多段キーストロークで一つのコマンドを実行する機能は、秀丸ではユーザーメニューを C-x などのキーに割り当てて実現するが、ユーザーメニューは最大 8 枚しかない<s>のでせいぜい 2 ストロークまでかな。 3 ストロークの割り当てはできるけど数が限られる</s>。でも、マクロの中で `inputchar()` でキー入力を受け取ることが可能なためユーザーメニューを使わずに多段キーストロークに対応可能だった。そのとき、 `iskeydown(0x10)` でのShiftキー判定、`iskeydown(0x11)` のCtrlキー判定、`iskeydown(0x12)` のAltキー判定を組み合わせれば何でもできちゃいそう。たとえば C-x キーに`C-x.mac`マクロを割り当て、`C-x.mac` の中で`inputchar()`で次の入力を受け取って、 `r` が押されてたら Prefi Command だから再び `inputchar()` で次の入力を待ち合わせる・・・とかやれば、いくらでも多段キーストロークのコマンドがつくれそう。(但し `inputchar()` で読むと `r` と `C-r` は違うキーコードになるので、なんか汎用的に作るのはそれなりにたいへんそうな気がする）
* 当然ながら、用意されている機能は Emacs の機能とは違う。秀丸の機能をそのまま割り当てても Emacs と同じようには機能しない場合がある。
* 但し、いくつかは同じ動作になるようマクロを書いた。
* LittleEmacs.KEY には、ここに記載のないコマンドも登録されてたりするかも。普段使っていたキーマップに追加してしまったので。
