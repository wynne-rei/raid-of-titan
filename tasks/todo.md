# PvP → 協力プレイ（PvE）化 + 雷の国削除

## 概要
- 4国FFA → **3国PvE協力**（火・氷・土）
- プレイヤーの国: 最大4人プレイヤー + 無制限ダイバー
- 敵2国: AI制御

## Step 1: 雷の国を削除（3国に戻す）
- [ ] JS定数: FACTIONS, FACTION_IDS, FACTION_KING_TINT, FACTION_PALETTES, CARD_FACTIONS, AUTO_SPAWN_CARDS
- [ ] HTML: 国選択の雷カード、GDPバー、タイトルボタン
- [ ] CSS: --clr-lightning等

## Step 2: プレイヤー構成変更
- [ ] NUM_PLAYERS=3, PLAYER_NAMES, PLAYER_CHARACTER_MAP, PLAYER_POSITIONS

## Step 3: buildTowers() 3国用リライト
- [ ] Player0=人間, Player1,2=AI敵

## Step 4: 協力プレイヤー動的追加
- [ ] addCoopPlayer() / removeCoopPlayer()

## Step 5: 「プレイヤーとして戦う」導線変更
- [ ] 「新しく始める」or「ルームコードで参加」選択ダイアログ

## Step 6: ネットワーク協力プレイヤー対応
- [ ] ホスト側: join/move/spawn/chestコマンド処理
- [ ] 参加者側: initCoopNetworking(), HUD, カメラ

## Step 7: テレイン・拠点調整
- [ ] 雷拠点削除、3国用調整

## Step 8: エリクサー・デッキ
- [ ] 個別エリクサー、協力プレイヤー用デッキ初期化
