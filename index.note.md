## 自己紹介
- 時間が足りなくなることが判明しまして
- 結構削ってますがそれでも足りません
- サクサク行きます


## はじめに
### 導入
- 今回、React と CSS を中心に話をさせて頂くわけですが
- [ ] React 使われますか
- Web で JS やってたら無関係ではないんじゃないか
- 全てがグローバルスコープ
- そのスコープ、有効範囲を制限しよう

- 全てをネームスペースだけで解決してきました
- フロントエンド意外お断りの世界
- そんな CSS も...

### 事例2
- Web Components で Shadow DOM を使ってこのように書くと `.title` クラスの有効範囲はこの `div` 中だけに制限され
- 外の `.title` クラスからの影響は受けない
- Mozilla は `style` タグに `scoped` と付けると同じようなことができる
- Web Components でいいじゃんてなって採用はされなかったけど

- 先日リリースされた Angular2
- 2通りの CSS カプセル化の実装を持ちます
- Emulated
  - デコレータでスタイルとテンプレートを渡すと
  - HTML はこうなって
  - Style にも名前がつく
  - Angular がコンポーネント単位にユニークな名前を付けてカプセル化してくれる
- Native
- Shadow DOM そのもの

- Riot の場合
- Riot もコアで Scoped CSS の実装を持っていて
- Mozilla 風にカスタムタグ内に `Style` を書くと
- タグ名で擬似カプセル化してくれる
  - 但し外部からの影響は受ける

- Vue.js は Angular2 と Riot の Mix


## React の場合
- 今現場で使いたいので、Shadow DOM は一旦忘れましょう
  - React が策定前の Web Components 採用はありえない
  - Shadow DOM も最近 Polymer で Shady DOM とかやっててまだ固まらない
- 全てのクラス・スタイルをカプセル化する必要はありません
- React は Soped CSS の実装を持たない → 組み合わせが必要


## 可能性1: CSS in JS
- React 使っていれば誰もが聞いたことあると思います
- JS の オブジェクトキーバリューに CSS プロパティを記述して
- HTML の Style プロパティに突っ込む
- 意外に古く2014年から広まり始めた

- Material UI など大御所コンポーネントがこぞって採用しています
- が、... と言う形で真っ二つに割れました
- 問題点としてよく上がるのが...
- Radium で解決はした
- それでもダウンサイドはある
- 因みにぼくが Material UI のスタイルで Prop 渡せない部分をどうしても変更しないといけないことがあり


## 可能性2: CSS Modules
- CSS Modules による Scoped CSS
- 特徴
- 普通に SCSS を書いて
- React Component 側から styles オブジェクトにインポートする
- オブジェクト内にはクラス名が格納
- Render メソッドで JSX の ClassName に styles オブジェクトからクラス名を与えていく
- `ファイル名__クラス名__ハッシュの` クラスができる
- Angular2 の Emulated に近い


## 可能性2.5: React CSS Cmodules
- React CSS Modules によると CSS Module は
- React CSS Modules なら
- 同じように import して
- Render メソッドで `styleName` にクラス名を書く
- HOC の要領で Export かます
- CSS Module と同じ出力が得られる


## 可能性3: Custom Element 風
- Riot が取る手法
- 結論: React では不可能
- ただし、配布コンポーネントでは是非使いたい
- 冒頭に挙げた React Components の巨匠意外、CSS は利用時側で好きに取り扱ってスタイルが多い
- `react-select` とか4千スターあって有名
- loader を改造しないとだめなので
- 現状 scss とかそっち側で書かないといけない
- ダウンサイドはそれなりにあるけど
- 配布するコンポーネントでは切に使いたい


## まとめ
