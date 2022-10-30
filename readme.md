# KN MemoPad 機能追加版
[watamario15](https://github.com/watamario15) 氏制作の SHARP Brain 用テキストエディタ **KN MemoPad 機能追加版** をひろをー仕様にしたフォークです。既存機能はそのままですので、何かミスがなければ\*完全な上位互換として動作するはずです。

# 動作要件
これは **Windows CE (ARMv4I)** 用ソフトウェアです。一部 SHARP Brain 専用の機能があります。

**SHARP Brain PW-SH1 (Windows Embedded CE 6.0, ARMv5TEJ)** で動作確認を行っています。

# 文字コード切り替えについて
BOMの情報だけを基に文字コードの自動判別を行います。BOM無しファイル(Shift_JIS/BOM無しUTF-8)の場合は、判別できませんので予め **Tools -> Charset...** で選択してから開いてください(先に開いてから選択し、Reloadでも構いません)。なお、この機能は **Tools -> Charset... -> Auto Detect by BOM** から無効化も可能です。

Reload及びSaveは、その時点で選択されている文字コードで行われます。予め開きたいor保存したい文字コードに設定してからそれらの処理を行ってください(間違った文字コードで処理してしまっても、設定し直してからやり直せば大丈夫です。)。

ちなみに、UTF-8 のBOM有り・無しは読み込み時に判別されます。

## 自動判別の仕様
- 最初が「EF BB BF」ならUTF-8、「FF FE」ならUTF-16 LEとして読み込む。
- 違ったら、BOM無しと判断し、現在ユーザが設定している文字コードを見る。UTF-16 LE以外ならそのまま、UTF-16 LEならShift_JISに設定する。

# 改行コード処理について
[wstring中の改行コードを変換する - わびさびサンプルソース](https://www.wabiapp.com/WabiSampleSource/windows/convert_crlf_w.html)で提供されているコードを基に、カスタマイズして使用しています。

どの改行コードでも指定不要で読み込める他、バグなどで改行コードが混在したファイルでも、正常に読み込むことができます。

読み込んだ時、最も多かった改行コード種をそのファイルの改行コードと判断し、**Tools -> Newline Code...** に設定します。保存前に別の改行コードに設定すれば、その改行コードで保存されます。

# 行・列数表示について
wordwrap が無効であれば正しく表示されますが、有効になっていると折り返しも1行とカウントされてしまいます。行・列数表示を参考にする場合は、 wordwrap を無効化することをお勧めします。

(思い返せば Windows 標準のメモ帳でも、Windows 10 で改良される前まで wordwrap 有効時はステータスバーが無効になっていた。)

# ソースコードについて
**src** 内にあります。プロジェクトは **eMbedded Visual C++ 4.0** のものです。

# 使用上の注意
**製作者は、このプログラムの利用によって生じた、いかなる損害についても責任を負いません。**

# 著作権情報
オリジナル版が GNU General Public License v3.0 で配布されていますので、その規定に従い同じく **GNU General Public License v3.0** で配布します。

# 変更履歴
## v0.12 rev7+ (2022/6/23 ~ 2022/8/13)
[KN Memopad rev7](https://github.com/watamario15/kn-memopad/releases/tag/v0.12-rev7) にツールバーを[TMK](https://github.com/orgs/GenkaiSoft/people/TmkSoft777)が追加したバージョン。