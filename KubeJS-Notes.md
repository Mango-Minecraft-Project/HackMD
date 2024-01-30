# # KubeJS 筆記

以下資訊皆以KubeJS最新支援版本、Forge（NeoForge優先，LexForge次要）為主

[TOC]

---

## 腳本預處理參數 [KubeJS 6+]

可在腳本開頭使用預處理參數，如下

|名稱|用途|參數類別|說明|預設值|
|:-:|---|---|---|:-:|
|`priority`|載入優先度|整數(Number)|數字越大越先載入|`0`|
|`ignored`|忽略載入|布林(Boolean)|如果是true則跳過載入|`false`|
|`packmode`|模組包模式|字串(String)|若模組包模式不等於輸入值內則跳過載入|`default`|
|`requires`|命名空間需求|字串(String)|若未載入該命名空間則跳過載入|` ` (無)|
||||||

### 範例
```js
// priority: 100
// ignored: false
// packmode: dev
// requires: forge
// requires: create
```

## DamageSource 中 `immediate` 與 `actual` 的差異

`immediate` 回傳直接傷害者
`actual` 回傳傷害所有者

舉例來說，玩家拿弓箭射實體：
- `immediate` 回傳 `Arrow` (弓箭)
- `actual` 回傳 `Player` (玩家)

## 自製 KubeJS 用 VSCode Code Snippet

```json
{
  "event": {
    "scope": "javascript",
    "prefix": "$event",
    "body": ["(event) => {", "  $0", "}"]
  },
  "priority": {
    "scope": "javascript",
    "prefix": "$priority",
    "body": ["// priority: $1", "$0"]
  },
  "ignored": {
    "scope": "javascript",
    "prefix": "$ignored",
    "body": ["// ignored: ${1|true,false|}", "$0"]
  },
  "packmode": {
    "scope": "javascript",
    "prefix": "$packmode",
    "body": ["// packmode: $1", "$0"]
  },
  "requires": {
    "scope": "javascript",
    "prefix": "$requires",
    "body": ["// requires: $1", "$0"]
  },
  "todo": {
    "scope": "javascript",
    "prefix": "$todo",
    "body": ["// TODO", "$0"]
  },
  "license": {
    "scope": "javascript",
    "prefix": "$license",
    "body": ["/**", " * @author MangoJellyPudding", " */", "", ""]
  }
}
```

## 替換多個物品配方
```js=
ServerEvents.recipes((event) => {
  event.replaceInput(
    {
      output: new RegExp([
        "minecraft:diamond_axe",
        "minecraft:diamond_hoe",
        "minecraft:diamond_pickaxe",
        "minecraft:diamond_shovel",
        "minecraft:diamond_sword",
      ].join("|")),
    },
    "minecraft:diamond",
    "minecraft:emerald"
  );
});
```

## 將腳本自動同步到 Github

以下步驟皆以Prism Launcher為基礎

1. 備份 `.minecraft`；
2. 清空原有的 `.minecraft`；
3. 在 `.minecraft` 中輸入 `git clone "儲存庫網址" .`；
4. 將備份的 `.minecraft` 內的檔案放回 `.minecraft`，視情況選擇覆蓋舊有的或保留舊有的；
5. 新增以下檔案：
    - `.minecraft/.gitignore`
      ```
      *
      !.gitignore
      !kubejs/      
      ```
    - `.minecraft/kubejs/.gitignore`
      ```
      !*
      probe/
      ```

## 讀取任意模組的Json檔案

[pietro-lopes/read_json_from_mod.js](https://gist.github.com/pietro-lopes/1471e43c6acef411fd98f10908185fae)

## *Beans*

Kubejs 有一個名為 *beans* 的功能，可以讓腳本更易讀。
任何 `getXy()` 都可以用 `xy` 來獲取，任何 `setXy(value)` 都可以用 `xy = value` 來設置，任何 `isXy()` 都可以用 `xy` 來檢查。

這樣我們就可以縮短代碼！例如，要獲取所有在線玩家的列表，可以使用 `event.getServer().getPlayers()`。有了 *beans* ，這可以縮短為 `event.server.players`！

請注意，只有當方法沒有參數時，`get` 和 `is` 時 *beans* 才會起作用。這意味著像 `getHeldItem(InteractionHand hand)` 這樣的方法不能簡寫為 `heldItem`。
對於 `set` 方法，需要有一個參數。

## 實用模組（非KubeJS Addon為主）

### ProbeJS

|[![badge-curseforge]][probejs-curseforge]|[![badge-modrinth]][probejs-modrinth]|[![badge-mcmod]][probejs-mcmod]|[![badge-wiki]][probejs-wiki]|
|---|---|---|---|

> ProbeJS 的功能是收集你的模組包中的方塊/物品等資訊，供 VSCode 編輯器使用。

- tags: `vscode`, `code snippets`

### Lychee

|[![badge-curseforge]][lychee-curseforge]|[![badge-modrinth]][lychee-modrinth]|[![badge-mcmod]][lychee-mcmod]|[![badge-wiki]][lychee-wiki]|
|---|---|---|---|

> Lychee 是一個允許你使用 JSON 合成表和數據包定義自訂交互的模組。

- tags: `recipe`, `world intercation`

### Loquat🧩

<!-- |[![badge-curseforge]][loquat-curseforge]|[![badge-modrinth]][loquat-modrinth]|[![badge-mcmod]][loquat-mcmod]|[![badge-wiki]][loquat-wiki]|
|---|---|---|---| -->
|[![badge-curseforge]][loquat-curseforge]|[![badge-modrinth]][loquat-modrinth]|[![badge-wiki]][loquat-wiki]|
|---|---|---|

> Loquat🧩 為 Minecraft 地圖製作者提供的區域管理和結構生成模組。

- tags: `worldgen`, `structure`


### Custom Fluid Mixin

|[![badge-curseforge]][custom_fluid_mixin-curseforge]|[![badge-modrinth]][custom_fluid_mixin-modrinth]|[![badge-mcmod]][custom_fluid_mixin-mcmod]|[![badge-wiki]][custom_fluid_mixin-wiki]|
|---|---|---|---|

> 借助資料包，本模組允許你在流體（例如岩漿、水）流動時產生一個方塊（例如岩漿流動遇水時可以不再是產生黑曜石，能夠自訂任何方塊）、產生一陣爆炸或執行一個資料包函數。

- tags: `recipe`, `world intercation`

### Origins (Forge)

|[![badge-curseforge]][origins_forge-curseforge]|[![badge-modrinth]][origins_forge-modrinth]|[![badge-mcmod]][origins_forge-mcmod]|[![badge-wiki]][origins_forge-wiki]|
|---|---|---|---|

> 本模組可以讓你在遊戲開始之前選擇你的種族，它們特有的能力可以幫助你，也可能會妨礙你的正常生存！

可以透過禁用全部種族來讓此模組轉變成僅修改各種玩家屬性的模組

- tags: `player attributes`

### Custom Machinery

|[![badge-curseforge]][custom_machinery-curseforge]|[![badge-modrinth]][custom_machinery-modrinth]|[![badge-mcmod]][custom_machinery-mcmod]|[![badge-wiki]][custom_machinery-wiki]|
|---|---|---|---|

> 這個模組讓你使用資源包創建自己的機器並添加進遊戲中。

- tags: `multiblock`, `custom machine`

### Multiblocked

|[![badge-curseforge]][multiblocked-curseforge]|[![badge-mcmod]][multiblocked-mcmod]|[![badge-wiki]][multiblocked-wiki]|
|---|---|---|

<!-- |[![badge-curseforge]][multiblocked-curseforge]|[![badge-modrinth]][multiblocked-modrinth]|[![badge-mcmod]][multiblocked-mcmod]|[![badge-wiki]][multiblocked-wiki]|
|---|---|---|---| -->

> Multiblocked是一個極其靈活但具有原版風格的自訂多方塊模組。

- tags: `multiblock`, `custom machine`

### Lopy's More Materials

|[![badge-curseforge]][lopys_more_materials-curseforge]|[![badge-modrinth]][lopys_more_materials-modrinth]|[![badge-mcmod]][lopys_more_materials-mcmod]|
|---|---|---|

> 這是一個簡單的模組，它為模組/模組包作者添加了大量可供魔改配方的材料。
> 
> <img src="https://media.forgecdn.net/attachments/614/397/mmt_items.png" height="500">
  
## KubeJS Create 所提供的 `CreateEvents`

### 蒸氣鍋爐熱量源 - `boilerHeatHandler`

```js=
CreateEvents.boilerHeatHandler((event) => {
  //? 熱量等級說明：
  //? -1：此方塊不提供任何形式的熱量。
  //? 0 ：此方塊提供被動熱量。（例如未加燃料的烈焰燃燒器）
  //? 1 ：此方塊提供1單位的熱量（在狀態欄中顯示1個綠色條，例如加燃料的烈焰燃燒器）
  //? 2 ：此方塊提供2單位的熱量（例如烈焰蛋糕燃燒器）
  //? X ：此方塊提供X單位的熱量，狀態欄中顯示X個綠色條
  //?
  //? 注意，回調函數僅在鍋爐有更新信號時調用。
  //? 例如相鄰方塊的狀態變化、破壞或放置等。

  //? 添加單個方塊的加熱器。
  //? 回調函數的參數類型為 BlockContainerJS。
  event.add("minecraft:diamond_block", (block) => {
    return 2;
  });

  //? 添加方塊篩選器的加熱器。
  event.addAdvanced("#minecraft:logs", (block) => {
    if (block.id === "minecraft:oak_log") {
      return 1;
    } else {
      return 2;
    }
  });
});
```

### 管道流體效果 - `pipeFluidEffect`

```js=
CreateEvents.pipeFluidEffect((event) => {
  //? 添加液體處理器，支援 FluidIngredient。

  event.add(
    Fluid.water(), // 流體
    (pipe, fluid) => {
      const { world } = pipe;
      if (world.server.tickCount % 5 != 0) return;

      world.getEntitiesWithin(pipe.AOE).forEach((entity) => {
        if (entity.living) {
          entity.heal(5);
        }
      });
    }
  );
});
```

### 注液器注液方塊 - `spoutHandler`

```js=
CreateEvents.spoutHandler((event) => {
  //? 創建注液器處理器，需要提供 ID，因為這裡沒有辦法生成一個一致的 UUID。
  //?
  //? 注液器每個 tick 都會以 simulate = true 的方式調用處理器，如果返回值 > 0，則注液器將開始注液動畫，
  //? 動畫結束時，處理器將再次以 simulate = false 的方式調用。
  //?
  //? 返回的整數表示此操作應該消耗多少單位液體。
  //? 單位視模組載入器而不同，Forge = 1MB、Fabric = 1 unit
  //? 1 B（Bucket，桶） = 1000 MB（MiliBucket，千分之一桶） = 81000 unit（單位流體）

  event.add(
    "kubejs:obsidian", // ID
    "minecraft:lava", // 目標方塊
    (block, fluid, simulate) => {
    if (fluid.id === Fluid.water().id && fluid.amount >= 100) {
      if (!simulate) {
        block.set("minecraft:obsidian");
      }
      return 100;
    }
    return 0;
  });
});
```

## `ItemStack.weakNBT()` 與 `ItemStack.strongNBT()` 的差別

以 `Item.of("diamond_sword", "{damage:50}")` 舉例

- `.weakNBT()`
  若物品的nbt包含 `{damage:50}` 則可以使用
  舉例：
  - :o: `{damage:50}`
  - :o: `{damage:50, display:"Sword"}`
  - :x: `{display:"Sword"}`
- `.strongNBT()`
  若物品的nbt ==**僅**== 包含 `"{damage:50}"` 則可以使用
  舉例：
  - :o: `{damage:50}`
  - :x: `{damage:50, display:"Sword"}`
  - :x: `{display:"Sword"}`

## 合成時消耗物品耐久

![damage ingredient recipe](https://hackmd.io/_uploads/H1KHEFIca.png)

```js=
ServerEvents.recipes((event) => {
  const { kubejs } = event.recipes;

  kubejs
    .shapeless("stripped_oak_log", ["oak_log", "#minecraft:axes"])
    .damageIngredient("#minecraft:axes");
});
```
:::info
僅限 `kubejs:shaped` 和 `kubejs:shapeless` 配方可使用 `.damageIngredient`
:::

---

<!-- badge links -->
[badge-curseforge]: https://img.shields.io/badge/CurseForge-313338?style=for-the-badge&logo=CurseForge
[badge-modrinth]: https://img.shields.io/badge/Modrinth-313338?style=for-the-badge&logo=Modrinth
[badge-mcmod]: https://img.shields.io/badge/MC%E7%99%BE%E7%A7%91-313338?style=for-the-badge&logo=data%3Aimage%2Fpng%3Bbase64%2CiVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAAAIGNIUk0AAHomAACAhAAA%2BgAAAIDoAAB1MAAA6mAAADqYAAAXcJy6UTwAAAAGYktHRAD%2FAP8A%2F6C9p5MAAAUjSURBVFjDvZfbbxRVGMB%2F3zmzO6U3KAVKSwQBK8ViQsS7aI0YMIiCYjUmGkB88kkTH5RXk8Y%2FwRh9MNGkhoiEBzVqTBoVEEmEGC4WWmvvpS29bPcyt3N86O52tyzKA%2B2XTHZmznfm991nViiQto7WpcAh4BXgLkBx%2B%2BQf4GvgkyMtR4dyN6UA%2FgTwEbD5NkJLSZ9g3n6%2F5atj5Dxs62jdCpxYBDiK8I4I98u3vv9iF4C0dbRWAqeB5oWHB4RU0JN5jalwyzUh3OoALywevJzuzAES4Sa0JFcBbzjAvgWHS0Bgqvg7c5BEtBEt6dzSHgdoWli4T2Cq6c4cYibagJZM4fI6ByhfWM9r6MocJBndOR8O4DqAzV1ZbNGViFDQqRTr2eyaBRFknp7gkYlq6cocJm3WoElj7ayOzKlap3iTKlwkshFK5AY81qJEFxuUlSDyUBIRyRp6vAN4toGYeHlHYloIDRg7u8cBMNYQ12Xsb36Xitiy%2FMPODnzL2cFviOslc0aZkGc3vcWaqsY8tnfqIt9d%2BRhrDY2197OtYSdL4o2E1KDwi%2BCXrqf49MIIufg5c%2BFWrK5cT3lsaR62bc0uzg3%2FiMUiCKEJWFWxlq31O5CCKZ0MJvGiNNsadrFv8zvz0lGWP%2Fsn4XHs6jhBZHGUzEUgJ6EJioJdV3En9VUb6Z%2FuJKbiRMZn04qHi%2BC5fa522L52fx5%2BYTzFhBfmU5gMItr%2FGmPCC3D13P4iA3Iy7Y1TEV%2BKFod7Vj5G7%2BRFUDHieglNKx8CwItSYC2uUwHWx3EaqXTrATg9nODD3%2FuLC87OpqAQDjd52%2FVM%2FslQoguA5lXbqXRr8MM0DdWN1FWuB%2BDS6CmmvXEAUqaeAf91ROIA9M94GANLHEWZzh6OQsuNHVXSAC9M0jl2BoAqt5Z1S5vxojT31rUgCNYaLl77Jd8JGVOHZ5cDBgAtQglWSSlpgJYYl8ZOYWwEQNPKR6h0l3N37QMADM%2F0MJS4TEzHZsOMQYhujXhLBiiHkZkeBhNXAFi3rJn76ndS5dYCcHX8Z677dYS2uuRDreWWpaQBgiKMfM4P%2FQRAtbuCpza8DoAxCU4OTdLrHyay8ZJQVyvSkSEdlj5MgXLJLgBwdJyu63%2FghSlcp5y4nu3ni9cz%2FDbeQmW8Mht2hRIhEUQkA0OZVjzWUMVQcgWTXogqUQuXJ9JMZVt03iiW%2FK8WzURmhO6Jc2xe%2BWhe5%2BdBg2%2FKUIT5caMFpv2IXweneX7Dcpa5Dm9uqbtp2D84089YOoGr5f8%2FOs8P%2FwSEAMwEEedGE7jK5izOS1wJ7Z2j%2FNA7STL474IsTIG0dbR2g10vollVsRYtDqlgmon0MCJCTHx02auMBY%2FjRwF9CQ8ElAhrq%2BI4IqRCw2DSx1pLYCyry%2BPUlDncrBMHkj7pwCDCuJNzxVrDwHQnFotCo5WDlgzXggfpnroXwwxKLLFsUq21XJnIzOqLEFOCiOBqYTQdMJIKit6ShRJTKl8bTmEgHZWraosWj9FgO33efhxtswVX7FNcl%2F5ecPKV97%2FTSBxgpvienfXcf5I%2B%2F0WEEMlOuAWQtAIuFMM9Rvwd9Pn7FhoO8LcCjuXgSjyG%2Fafp9%2Fdmx%2BuCwgGOK%2BAE2N%2BVBAz7Oxnwn1sMzwF6gc%2FUkZajGUX02pD%2FzPCgt2ex4Eng1fbdTWMK4L2Wrzsnwy27EXtmEeCXgL3tu5tOwrw%2BefmbLlcRvAK8xOwf1arbBE0BV4HjwOftu5umcwv%2FAs4dLGlGxRDmAAAAJXRFWHRkYXRlOmNyZWF0ZQAyMDIzLTEyLTI5VDEwOjM2OjU1KzAwOjAwPlu%2B7wAAACV0RVh0ZGF0ZTptb2RpZnkAMjAyMy0xMi0yOVQxMDozNjo1NSswMDowME8GBlMAAAAodEVYdGRhdGU6dGltZXN0YW1wADIwMjMtMTItMjlUMTA6MzY6NTUrMDA6MDAYEyeMAAAAAElFTkSuQmCC
[badge-wiki]: https://img.shields.io/badge/Wiki-313338?style=for-the-badge&logo=wikipedia

<!-- 實用模組 -->
[probejs-curseforge]: https://curseforge.com/minecraft/mc-mods/probejs
[probejs-modrinth]: https://modrinth.com/mod/probejs
[probejs-mcmod]: https://mcmod.cn/class/6486
[probejs-wiki]: https://github.com/Prunoideae/ProbeJS/wiki/

[lychee-curseforge]: https://curseforge.com/minecraft/mc-mods/lychee
[lychee-modrinth]: https://modrinth.com/mod/lychee
[lychee-mcmod]: https://mcmod.cn/class/5559
[lychee-wiki]: https://lycheetweaker.readthedocs.io/en/latest/

[loquat-curseforge]: https://curseforge.com/minecraft/mc-mods/loquat
[loquat-modrinth]: https://modrinth.com/mod/loquat
<!-- [loquat-mcmod]: https://mcmod.cn/class/5559 -->
[loquat-wiki]: https://loquat.readthedocs.io/en/latest/

[custom_fluid_mixin-curseforge]: https://curseforge.com/minecraft/mc-mods/custom-fluid-mixin
[custom_fluid_mixin-modrinth]: https://modrinth.com/mod/custom-fluid-mixin
[custom_fluid_mixin-mcmod]: https://mcmod.cn/class/5942
[custom_fluid_mixin-wiki]: https://github.com/Insane96/CustomFluidMixin/wiki

[origins_forge-curseforge]: https://curseforge.com/minecraft/mc-mods/origins-forge
[origins_forge-modrinth]: https://modrinth.com/mod/origins-forge
[origins_forge-mcmod]: https://mcmod.cn/class/4032
[origins_forge-wiki]: https://origins.readthedocs.io/en/latest/

[custom_machinery-curseforge]: https://curseforge.com/minecraft/mc-mods/custom-machinery
[custom_machinery-modrinth]: https://modrinth.com/mod/custom-machinery
[custom_machinery-mcmod]: https://mcmod.cn/class/3903
[custom_machinery-wiki]: https://frinn.gitbook.io/custom-machinery-1.19/

[multiblocked-curseforge]: https://curseforge.com/minecraft/mc-mods/multiblocked
<!-- [multiblocked-modrinth]: https://modrinth.com/mod/multiblocked -->
[multiblocked-mcmod]: https://mcmod.cn/class/6191
[multiblocked-wiki]: https://github.com/Low-Drag-MC/Multiblocked/wiki

[lopys_more_materials-curseforge]: https://curseforge.com/minecraft/mc-mods/morematerials
[lopys_more_materials-modrinth]: https://modrinth.com/mod/morematerials
[lopys_more_materials-mcmod]: https://mcmod.cn/class/11835
<!-- [lopys_more_materials-wiki]: https://frinn.gitbook.io/custom-machinery-1.19/ -->

<!-- <style>
  .markdown-body {
      width: 50%;
      max-width: none;
  }
</style> -->

{%hackmd @lumynou5/dark-theme %}
<!-- {%hackmd @themes/dracula %} -->