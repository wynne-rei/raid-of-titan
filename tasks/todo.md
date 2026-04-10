# リファクタ計画 (2026-04-10)

## 方針

- **単一HTMLは維持**（GitHub Pages配布の利便性を崩さない）
- **削除ではなく休眠フラグで保全**（将来復活させる機能はコードを残す）
- **見た目も挙動も変えない**（純粋に可読性とパフォーマンスの改善のみ）
- **1項目ずつ実装→動作確認→コミット**

## タスク

- [x] **Phase A**: `CONTINUOUS_WORLD_MODE` フラグ撤去（16箇所の分岐削除）
- [x] **Phase B**: 旧ウェーブHUDのDOM/CSS削除（`#wave-top-hud` `#wave-info` `#wave-number` `#cd-timer` `#timer-bar`）
- [x] **Phase C'**: レイドシステム休眠化（`RAID_SYSTEM_ENABLED = false`）
- [x] **Phase D'**: スパチャ/ストリームチャット/ギフト休眠化（`STREAM_MODE_ENABLED = false`）
- [x] **Phase F**: セクションコメント整理（Core / Dormantの分類・SYSTEM MAP追加）
- [x] 総合セルフデバッグ: JSエラー0件、全Core関数exist、SAVED BY / ダイバーHUD DOM確認済
- [x] git commit && push

## 成果

- `index.html`: 16,615行 → 16,490行（**125行削減**）
- diff: 86 insertions(+), 125 deletions(-)
- 分岐削減: `CONTINUOUS_WORLD_MODE` 16箇所 → 0箇所
- 休眠フラグ追加: `RAID_SYSTEM_ENABLED`, `STREAM_MODE_ENABLED`

## やらないこと

- ファイル分割（ES Modules化）
- 変数リネーム
- ビルドツール導入
- TypeScript化
- ボットAIの変更（現役で稼働中のため温存）

## 完了条件

1. 各Phase後にブラウザで動作確認してデグレなし
2. コンソールエラー0件
3. ドラゴン登場演出・SAVED BY・ダイバーカードが従来通り動く
4. git commit && push 完了
