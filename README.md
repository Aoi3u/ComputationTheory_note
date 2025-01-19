# 情報数学前半まとめ
情報数学A・Bのチューリング機械あたりまでの内容をまとめています。厳密な部分や証明には一切ふれておらず、また完全に自分用なので、わかりづらい部分があっても大目にみてください。（同値記号は誤った使い方をしている部分が多々あります。）間違っている部分があったらご指摘いただけると幸いです。

## 有限オートマトン・正則言語
### 決定性有限オートマトン DFA
<ul>
  <li>ルートが一意に決まる(決定性)。</li>
  <li>受理する文字列全体の集合を言語という。<br> → DFAが受理する言語を、正則（正規）言語という。</li>
  <li>言い換えると、DFAは正則言語を受理する（認識する）という。</li>
</ul>

### 非決定性有限オートマトン NFA
<ul>
  <li>ルートが一意ではない(非決定性)。</li>
  <li>ルートが分岐してる場合、全て並列に辿る。辿るルート先がない場合、そのルートはそこで終わり。最終的に、並列したルートのうち一つでも受理されれば、受理。</li>
  <li>εが書いているルートがある場合、入力文字列に関係なく、εのルートに進むルートとその場に留まるルートの2ルートに分岐する。</li>
  <li>ある言語をNFAが認識する⇔その言語は正則言語</li>
</ul>

### 正則表現
<ul>
  <li>正則言語を表現するための演算</li>
  <li>例: 0* </li>
</ul>

### 非正則言語
<ul>
  <li>dfa,nfaで認識できない言語</li>
  <li>例: B={0^n1^n|n≧0} </li>
  <li>↑0がいくつ現れたか記憶しなくてはならないので、無限個の可能性を記憶する必要がある。有限オートマトンではむり</li>
</ul>

**DFA、NFA、正則言語、正則表現で1グループのイメージ**
<br>

## プッシュダウンオートマトン・文脈自由言語
### 文脈自由文法・文脈自由言語
<ul>
  <li>文脈自由文法で生成できる言語が文脈自由言語</li>
  <li>正則言語では表せない再起的な言語も表せる</li>
  <li>例: 文脈自由文法が<br>
  A→0A1, A→B, B→# （変数A,B、終端記号0,1,#）<br>
  のとき、文脈自由言語は<br>
  {0^n#1^n|n≧0}</li>
  <li>上の例は A→0A1|B とも表せる</li>
</ul>

### チョムスキー標準形
生成規則がすべて <br>
A→BC（変数→変数二文字）<br>
または<br>
A→a（変数→終端一文字）<br>
または<br>
A→ε<br>

### グライバッハ標準形
生成規則がすべて<br>
A→aα（変数→終端一文字と任意の変数）<br>
または<br>
A→ε<br>

### プッシュダウンオートマトン PDA
<ul>
  <li>文脈自由言語を認識する</li>
  <li>dfaやnfaと違い、最後に入れたものが最初に出る、スタックという記憶装置を持つ</li>
  <li>状態遷移図で、「a,b→c」と書くとき、入力からaを読み出す時にスタックの先頭にある文字bをcに置き換える。という意味になる。</li>
  <li>a,b,cのいずれがεであってもよく、以下のように動作する
    <ul>
      <li>aがεの場合、入力から文字読み出さない</li>
      <li>bがεの場合、スタックから文字をポップしない</li>
      <li>cがεの場合、スタックに文字を書き込まない</li>
    </ul>
  </li>
  <li>スタック上に$をはじめに置くことで、それがポップした際スタックが空であることを検出できるようにしている。（遷移図の最初にε,ε→$がある）</li>
  <li>PDAがある言語を認識する⇔その言語は文脈自由言語</li>
</ul>

### 非文脈自由言語
<ul>
  <li>PDAで認識できない言語</li>
  <li>例: B={a^nb^nc^n|n≧0} </li>
</ul>

**PDA、文脈自由言語、文脈自由文法で1グループのイメージ**
<br>

## チューリング機械・チューリング認識可能言語
### チューリング機械
<ul>
  <li>無限大・無制約のメモリを持つ。</li>
  <li>実際の計算機が解ける問題全てを解ける。</li>
  <li>テープの読み込み、書き込みができる。</li>
  <li>δ(qi,b)=(qj,c,L)ならば <br>
u a qi b v → u qj a c v</li>
  <li>チューリング機械がある言語を認識する⇔その言語はチューリング認識可能言語（帰納的列挙可能言語）</li>
  <li>チューリング機械はループすると受理か拒否かわかりづらい　<br> →決してループしない機械が望ましい <br> →ループしない機械は常に受理か拒否か判定するため、判定装置という。</li>
  <li>判定装置がある存在する言語を判定可能言語という。</li>
  <li>「判定可能⇒チューリング認識可能」だが、逆は成り立たない。</li>
</ul>

### 複数テープチューリング機械
<ul>
  <li>チューリング機械の複数テープ版。</li>
  <li>δ(qi,a1,...,ak)=(qj,b1,...,bk,L,R,...,L)</li>
  <li>普通のチューリング機械と等価。</li>
</ul>

### 非決定性チューリング機械
<ul>
  <li>すべての非決定性チューリング機械に対し、それと等価な決定性チューリング機械が存在する。</li>
</ul>

**チューリング機械とチューリング認識可能言語で1セットのイメージ**

## 言語間の関係のイメージ
**正則言語 < 文脈自由言語 < チューリング認識可能言語 < 言語（形式言語）** <br>
（部分集合の関係）
