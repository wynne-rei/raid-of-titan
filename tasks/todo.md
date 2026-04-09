# 実装計画: ドラゴン改善 + ユニットシステム変更

## Phase 1: ドラゴンメッシュ作り直し
- [x] `buildDragonMesh()` を全面書き直し
  - カラーバグ修正（mcBoxにMaterialを渡していた問題）
  - サイズ: dragonling 4倍 / firedrake 6倍 / frostdrake 6倍 / stonedrake 8倍 / elderdragon 12倍
  - 飛行型(dragonling/firedrake/frostdrake/elderdragon): 翼大きめ、高度25飛行
  - 地上型(stonedrake): 翼なし、脚太い、四足獣
- [x] `isFlying` → `fly` に修正（spawnDragon内）
- [x] DRAGON_DEFS の scale値をサイズ倍率に合わせて更新

## Phase 2: ドラゴンの攻撃演出（火吐き）
- [x] 飛行ドラゴンの攻撃時に火の玉プロジェクタイルを発射
  - firedrake: 赤い炎
  - frostdrake: 青い氷弾
  - dragonling: 小さい火の玉
  - elderdragon: 巨大な紫炎
- [x] stonedrake は近接攻撃（体当たり）のまま

## Phase 3: プレイヤーは施設のみ配置可能に
- [x] CHEST_TYPES から troop / spell を削除（structure / building のみ）
- [x] getRandomCard() が施設・建物カードのみ返すように
- [x] インベントリパネルからタブ削除（施設一覧のみ表示）
- [x] handCards系の処理を施設カード専用に整理
- [x] 初期ナイト2体（spawnInitialArmy）は維持
