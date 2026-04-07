# PvP → 協力プレイ（PvE）化 + 雷の国削除

## 概要
- 4国FFA → **3国PvE協力**（火・氷・土）
- プレイヤーの国: 最大4人プレイヤー + 無制限ダイバー
- 敵2国: AI制御

## Step 1: 雷の国を削除（3国に戻す） ✅
- [x] JS定数: FACTIONS, FACTION_IDS, FACTION_KING_TINT, FACTION_PALETTES, CARD_FACTIONS, AUTO_SPAWN_CARDS
- [x] HTML: 国選択の雷カード、GDPバー、タイトルボタン、ローカル観戦パネル
- [x] CSS: lightning関連スタイル全削除
- [x] 3D: 雷の国拠点オブジェクト削除
- [x] テレイン象限分割を3国用に修正

## Step 2: プレイヤー構成変更 ✅
- [x] NUM_PLAYERS=3, PLAYER_NAMES, PLAYER_CHARACTER_MAP, PLAYER_POSITIONS

## Step 3: buildTowers() 3国用リライト ✅
- [x] Player0=人間, Player1,2=AI敵

## Step 4: 協力プレイヤー動的追加 ✅
- [x] addCoopPlayer() — キングタワー生成、デッキ初期化
- [x] removeCoopPlayer() — 切断時タワー削除

## Step 5: 「プレイヤーとして戦う」導線変更 ✅
- [x] 「新しく始める（ホスト）」or「ルームコードで参加」選択ダイアログ
- [x] openPlayerModeDialog(), startAsHost(), showCoopJoinInput()

## Step 6: ネットワーク協力プレイヤー対応 ✅
- [x] ホスト側: join/move/coopSpawnコマンド処理
- [x] 参加者側: initCoopNetworking(), キャラ選択→join送信
- [x] 切断時のタワー自動削除

## Step 7: テレイン・拠点調整 ✅
- [x] 雷拠点削除済み、3国用配置確認OK

## Step 8: エリクサー・デッキ ✅
- [x] 個別エリクサー回復（isRemoteプレイヤー対応）
- [x] 協力プレイヤー用デッキ初期化（自国カードからランダム配布）
- [x] serializeBattleState/restoreBattleStateにisHuman/isRemote追加
