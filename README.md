# 神奈川県社会人サッカーリーグ1部 2026 データボード

鎌倉インターナショナルFCの3位入りを軸に、2026シーズンの1部リーグを可視化した非公式のファンメイドサイトです。

## ページ

| ファイル | 内容 |
|---|---|
| `index.html` | トップ。現在順位と主要指標、各ページへのリンク |
| `trend.html` | 第1節からの勝ち点推移（折れ線・クラブ別オンオフ）＋全90試合の星取表 |
| `simulator.html` | 残り試合の結果を入れると3位到達パターンが消えていくシミュレーター |
| `fixtures.html` | 3〜7位の残り日程難易度マップ（期待勝ち点・前回対戦・ホーム/アウェイ） |
| `dads.css` | 全ページ共通のスタイル（デジタル庁デザインシステム準拠のトークン・タブヘッダー） |

各ページは `dads.css` と Google Fonts（Noto Sans JP）だけを参照します。ビルド不要で、そのまま GitHub Pages に置けます。

## デザイン

[デジタル庁デザインシステム](https://design.digital.go.jp/)に準拠しています。

- **カラー**：公式デザイントークン `@digital-go-jp/design-tokens` v2.0.1 の Primitive / Semantic カラーをそのまま使用（Primary = Blue-900 `#0017c1`、テキスト = Solid Gray 900/700/536、Success = Green-600、Error = Red-800）
- **書体**：Noto Sans JP、ウェイトは 400 / 700 の2段階のみ。本文16px以上、最小14px（DADS のタイポグラフィ規定）
- **角丸・影**：DADS の border-radius スケール（4/8/12/16px）
- **グラフの系列色**：DADS の Primitive カラーから8系統を抽出。隣接ペアについて色覚多様性シミュレーション（P/D/T型）での色差を検証済み（OKLab ΔE×100 で最小15.0／ダーク10.6、目標値8以上）。全系列に直接ラベルを併記しているため、色のみに依存しません

## 公開手順（GitHub Pages）

1. GitHub で新しいリポジトリを作成（Public）
2. この4つのHTMLと README.md をアップロード（ドラッグ&ドロップで可）
3. リポジトリの **Settings → Pages** を開く
4. **Source** を `Deploy from a branch`、**Branch** を `main` / `/ (root)` にして Save
5. 1〜2分後に `https://<ユーザー名>.github.io/<リポジトリ名>/` で公開

## データ更新のしかた

各ページの先頭付近にある JavaScript のデータ定義を書き換えるだけです。

- `simulator.html` … `const SCORES = {...}` に `フィクスチャ番号: [ホーム得点, アウェイ得点]` を追記
- `trend.html` … `const DATA = {...}`（勝ち点推移）と `const MX = {...}`（星取表）
- `fixtures.html` … `const D = [...]`
- `index.html` … `const T = [...]`（順位表）

## データ出典

[一般社団法人神奈川県サッカー協会 社会人部会](https://fakj-shakaijin.com/standings/leaguediv1/)（順位表 / 日程・結果）

順位決定方法：勝点 → 得失点差 → 総得点 → 直接対決

## 注意

- 期待勝ち点・到達確率は、各クラブの得点/失点実績からポアソン分布で試合結果を生成する簡易モデルによる参考値で、公式なものではありません。
- 「3位以内の可能性あり」は数学的に到達可能という意味で、確率ではありません。
