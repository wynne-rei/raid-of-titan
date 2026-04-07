# 4人対戦化 + 雷の国追加 + 全FBXモデル実装

## 概要
- 64人対戦 → **4人対戦**（1プレイヤー + 3 BOT）
- 3国（火・氷・土）→ **4国（火・氷・土・雷）**
- 各プレイヤーに固有FBXキャラクター割り当て
- ユニットは全てヘッドレス巨人FBX

## キャラ割り当て
| プレイヤー | 国 | FBXモデル |
|-----------|-----|----------|
| Player 1（自分） | 選択制 | 選択したキャラ |
| Player 2（BOT） | 残り3国から | Scandinavian Man (knight) |
| Player 3（BOT） | 残り3国から | Medieval Soldier 1 (dwarfFemale) |
| Player 4（BOT） | 残り3国から | Medieval Soldier 2 (dwarfMale) |

※ プレイヤーのキャラ選択UIは維持（4種から選択）

## パフォーマンス見積もり
```
4キング × 45 DC = 180 DC
ユニット40体 × 1 DC = 40 DC
アリーナ固定 = 60 DC
合計 = 280 DC ← 300上限以内でOK
```

---

## Phase 1: 基盤（国・プレイヤー数） ✅ 完了
- [x] FACTIONSに雷の国を追加（名前・アイコン・カラー定義）
- [x] FACTION_IDSを4国に拡張
- [x] NUM_PLAYERSを64→4に変更
- [x] PLAYER_POSITIONSを4箇所に再配置（四方配置）
- [x] hardcoded {fire,ice,earth} オブジェクトを全て4国対応に修正
  - factionGDP, kingReviveCooldown, factionSpawnTimers, factionLevels, factionXP → initFactionMap()
  - getTotalGDP() → FACTION_IDS.reduce()
  - updateGDPDisplay() → Math.max(...FACTION_IDS.map())
  - startBattle() の初期化 → initFactionMap()
  - チュートリアル敵国選択 → FACTION_IDS.find()
- [x] FACTION_KING_TINT に lightning 追加
- [x] FACTION_PALETTES に lightning 追加
- [x] CARD_FACTIONS / AUTO_SPAWN_CARDS に lightning 追加
- [x] initFactionMap の TDZ問題修正（FACTION_IDS定義後に初期化）

## Phase 2: FBXモデル復元 ✅ 完了
- [x] CHARACTER_FBX_CONFIGに4キャラ全て復元（queen, knight, dwarfFemale, dwarfMale）
- [x] TEXTURE_MATERIAL_KEYWORDSの不足キーワード復元（dress, hair, boots, eyes, jacket, coat等）
- [x] PLAYER_CHARACTER_MAP定義（各プレイヤー→キャラモデル対応）
- [x] createTower()で全4プレイヤーにFBXを使用するよう変更
- [x] KING_MODEL_KEY廃止 → PLAYER_CHARACTER_MAP に置き換え

## Phase 3: マップ・ビジュアル ✅ 完了
- [x] テレインを4象限ゾーンに変更（十字分割: X=0, Z=0が国境）
- [x] 国境線を十字に変更（Z-strip → 4象限）
- [x] buildFactionBases()に雷の国拠点を追加（金属尖塔+コイル+台座）
- [x] 氷の国拠点を東（x > 0）に移動

## Phase 4: UI ✅ 完了
- [x] 国選択画面に雷の国カード追加（fs-card）
- [x] GDP表示バーに4国目追加（vp-row）
- [x] タイトル画面の国ボタンに雷追加（faction-btn, lobby-faction-btn）
- [x] 全CSS色定義に lightning 追加
- [x] fs-cards を flex-wrap: wrap に変更（4枚対応）

## Phase 5: ゲームロジック ✅ 完了
- [x] buildTowers()を4人用にリライト（1人1国、remainingFactions方式）
- [x] AUTO_SPAWN_CARDSに雷の国用デッキ追加
- [x] チュートリアルの敵国選択ロジック修正
- [x] CARD_FACTIONSに雷追加

## Phase 6: 検証
- [x] エラーなしで起動確認
- [x] 4国GDPバー表示確認
- [x] FBXモデル表示確認
- [ ] 4人対戦の本戦動作確認（チュートリアルスキップ後）
- [ ] 全4キャラのFBXが正しく表示されるか確認
- [ ] アニメーション（Idle/Walk）が機能するか確認
- [ ] パフォーマンス計測（300 DC以内か）
- [ ] 国選択→キャラ選択→バトル開始のフロー確認
