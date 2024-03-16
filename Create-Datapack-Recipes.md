# Create Data Pack Recipes

| Machine            | Recipe Name                                  | ID                           |
| ------------------ | -------------------------------------------- | ---------------------------- |
| Encased Fan        | [Bulk Haunting](#Bulk-Haunting)              | `create:haunting`            |
| \                  | [Bulk Washing](#Bulk-Washing)                | `create:splashing`           |
| Millstone          | [Milling](#Milling)                          | `create:milling`             |
| Crushing Wheel     | [Crushing](#Crushing)                        | `create:crushing`            |
| Mechanical Press   | [Compacting](#Compacting)                    | `create:compacting`          |
| \                  | [Pressing](#Pressing)                        | `create:pressing`            |
| Mechanical Mixer   | [Mixing](#Mixing)                            | `create:mixing`              |
| Item Drain         | [Item Draining](#Item-Draining)              | `create:emptying`            |
| Spout              | [Filling by Spout](#Filling-by-Spout)        | `create:filling`             |
| Mechanical Saw     | [Sawing](#Sawing)                            | `create:cutting`             |
| Deployer           | [Deploying](#Deploying)                      | `create:deploying`           |
| Hand               | [Manual Item Application](#Item-Application) | `create:item_application`    |
| Sand Paper         | [Sandpaper Polishing](#Sandpaper-Polishing)  | `create:sandpaper_polishing` |
| Mechanical Crafter | [Mechanical Crafting](#Mechanical-Crafting)  | `create:mechanical_crafting` |
| *                  | [Recipe Sequence](#Recipe-Sequence)          | `create:sequenced_assembly`  |

## Recipe Types

### Bulk Haunting

Related Blocks
- `create:encased_fan`
- `#create:fan_processing_catalysts/haunting`

```json
{
  "type": "create:haunting",
  "ingredients:": Ingredients<Item>[],
  "result": Result<Item>[]
}
```

:::spoiler example
```json
{
  "type": "create:haunting",
  "ingredients": [
    {
      "tag": "forge:cobblestone"
    }
  ],
  "results": [
    {
      "item": "minecraft:blackstone"
    }
  ]
}
```
:::

### Bulk Washing

Related Blocks
- `create:encased_fan`
- `#create:fan_processing_catalysts/washing`

```json
{
  "type": "create:splashing",
  "ingredients:": Ingredients<Item>[],
  "result": Result<Item>[]
}
```

:::spoiler example
```json
{
  "type": "create:splashing",
  "ingredients": [
    {
      "item": "minecraft:black_concrete_powder"
    }
  ],
  "results": [
    {
      "item": "minecraft:black_concrete"
    }
  ]
}
```
:::

### Milling

Related Blocks
- `create:milling_stone`

```json
{
  "type": "create:milling",
  "ingredients:": Ingredients<Item>[],
  "result": Result<Item>[],
  "processingTime": GameTick // optional
}
```

:::spoiler example
```json
{
  "type": "create:milling",
  "ingredients": [
    {
      "item": "minecraft:andesite"
    }
  ],
  "results": [
    {
      "item": "minecraft:cobblestone"
    }
  ],
  "processingTime": 200
}
```
:::

### Crushing

Related Blocks
- `create:crushing_wheel`

```json
{
  "type": "create:crushing",
  "ingredients:": Ingredients<Item>[],
  "result": Result<Item>[],
  "processingTime": GameTick // optional
}
```

:::spoiler example
```json
{
  "type": "create:crushing",
  "ingredients": [
    {
      "item": "minecraft:amethyst_block"
    }
  ],
  "results": [
    {
      "item": "minecraft:amethyst_shard",
      "count": 3
    },
    {
      "item": "minecraft:amethyst_shard",
      "chance": 0.5
    }
  ],
  "processingTime": 150
}
```
:::

### Compacting

Related Blocks
- `create:mechanical_press`
- `create:basin`

```json
{
  "type": "create:compacting",
  "ingredients:": Ingredients<Item,Fluid>[],
  "result": Result<Item,Fluid>[],
  "heatRequirement": "superheated"|"heated"|"none" // optional
}
```

:::spoiler example
```json
{
  "type": "create:compacting",
  "ingredients": [
    {
      "item": "minecraft:flint"
    },
    {
      "item": "minecraft:flint"
    },
    {
      "item": "minecraft:gravel"
    },
    {
      "fluid": "minecraft:lava",
      "amount": 100,
      "nbt": {}
    }
  ],
  "results": [
    { "item": "minecraft:andesite" }
  ]
}
```
:::

### Pressing

Related Blocks
- `create:mechanical_press`
- `create:depot` / `create:belt_connector`

```json
{
  "type": "create:pressing",
  "ingredients:": Ingredients<Item>[],
  "result": Result<Item,Fluid>[]
}
```

:::spoiler example
```json
{
  "type": "create:pressing",
  "ingredients": [
    {
      "tag": "forge:ingots/brass"
    }
  ],
  "results": [
    {
      "item": "create:brass_sheet"
    }
  ]
}
```
:::

### Mixing

Related Blocks
- `create:mechanical_mixer`
- `create:basin`

```json
{
  "type": "create:",
  "ingredients:": SpecialIngredients<Item,Fluid>[],
  "result": Result<Item,Fluid>[],
  "heatRequirement": "superheated"|"heated"|"none" // optional
}
```

#### [Ingredients](#objectltIngredientgt)&lt;SpecialIngredients&gt;

- `return_chance`: number = 1 (Optional)
  1.0 = 100%

:::spoiler example
```json
{
  "type": "create:mixing",
  "ingredients": [
    {
      "item": "minecraft:andesite"
    },
    {
      "tag": "forge:nuggets/iron"
    }
  ],
  "results": [
    {
      "item": "create:andesite_alloy"
    }
  ]
}
```
:::

### Item Draining

Related Blocks
- `create:item_drain`

```json
{
  "type": "create:emptying",
  "ingredients:": Ingredients<Item>[],
  "result": [Result<Item>, Result<Fluid>]
}
```

:::spoiler example
```json
{
  "type": "create:emptying",
  "ingredients": [
    {
      "item": "create:builders_tea"
    }
  ],
  "results": [
    {
      "item": "minecraft:glass_bottle"
    },
    {
      "amount": 250,
      "fluid": "create:tea"
    }
  ]
}
```
:::

### Filling by Spout

Related Blocks
- `create:spout`
- `create:depot` / `create:belt_connector`

```json
{
  "type": "create:filling",
  "ingredients:": [Ingredients<Item>, Ingredients<Fluid>],
  "result": Result<Item>[]
}
```

:::spoiler example
```json
{
  "type": "create:filling",
  "ingredients": [
    {
      "item": "create:blaze_cake_base"
    },
    {
      "fluid": "minecraft:lava",
      "amount": 250,
      "nbt": {}
    }
  ],
  "results": [
    {
      "item": "create:blaze_cake"
    }
  ]
}
```
:::

### Sawing

Related Blocks
- `create:mechanical_saw`

```json
{
  "type": "create:cutting",
  "ingredients:": Ingredients<Item>[],
  "result": Result<Item>[],
  "processingTime": GameTick // optional
}
```

:::spoiler example
```json
{
  "type": "create:cutting",
  "ingredients": [
    {
      "item": "minecraft:acacia_log"
    }
  ],
  "results": [
    {
      "item": "minecraft:stripped_acacia_log"
    }
  ],
  "processingTime": 50
}
```
:::

### Deploying

Related Blocks
- `create:deployer`
- `create:depot` / `create:belt_connector`

```json
{
  "type": "create:deploying",
  "ingredients:": Ingredients<Item>[],
  "result": Result<Item>[]
}
```

:::spoiler example
```json
{
  "type": "create:deploying",
  "ingredients": [
    {
      "item": "create:shaft"
    },
    {
      "tag": "minecraft:planks"
    }
  ],
  "results": [
    { "item": "create:cogwheel" }
  ]
}
```
:::

### Sandpaper Polishing

Related Items
- `create:sand_paper` / `create:red_sand_paper`

```json
{
  "type": "create:sandpaper_polishing",
  "ingredients:": Ingredients<Item>[],
  "result": Result<Item>[]
}
```

:::spoiler example
```json
{
  "type": "create:sandpaper_polishing",
  "ingredients": [
    {
      "item": "create:rose_quartz"
    }
  ],
  "results": [
    {
      "item": "create:polished_rose_quartz"
    }
  ]
}
```
:::

### Item Application

```json
{
  "type": "create:item_application",
  "ingredients:": [Ingredients<Block>, Ingredients<Item>],
  "result": Result<Item>[]
}
```

:::spoiler example
```json
{
  "type": "create:sandpaper_polishing",
  "ingredients": [
    {
      "item": "create:rose_quartz"
    }
  ],
  "results": [
    {
      "item": "create:polished_rose_quartz"
    }
  ]
}
```
:::

### Mechanical Crafting

Related Blocks
- `create:mechanical_crafter`

```json
{
  "type": "create:mechanical_crafting",
  "key": object<string, Ingredients<Item>>
  "pattern": string[][],
  "result": Result<Item>[],
  "acceptMirrored": boolean // optional
}
```

:::spoiler example
```json
{
  "type": "create:mechanical_crafting",
  "key": {
    "A": {
      "item": "create:andesite_alloy"
    },
    "P": {
      "tag": "minecraft:planks"
    },
    "S": {
      "tag": "forge:stone"
    }
  },
  "pattern": [
    " AAA ",
    "AAPAA",
    "APSPA",
    "AAPAA",
    " AAA "
  ],
  "result": {
    "item": "create:crushing_wheel"
    "count": 2,
  },
  "acceptMirrored": false
}
```
:::

### Recipe Sequence

Related Blocks
- `create:belt_connector`
- `create:deployer` (When using `deploying` recipe)
- `create:mechanical_press` (When using `pressing` recipe)
- `create:mechanical_saw` (When using `sawing` recipe)
- `create:spout` (When using `filling by spout` recipe)

```json
{
  "type": "create:sequenced_assembly",
  "ingredients:": Ingredients<Item>,
  "sequence": SequenceRecipe[],
  "result": Result<Item>[],
  "loops": number,
  "translationItem": Ingredients<Item> // optional
}
```

:::spoiler example
```json
{
  "type": "create:sequenced_assembly",
  "ingredient": {
    "tag": "forge:plates/gold"
  },
  "loops": 5,
  "results": [
    {
      "chance": 120.0,
      "item": "create:precision_mechanism"
    },
    {
      "chance": 8.0,
      "item": "create:golden_sheet"
    },
    {
      "chance": 8.0,
      "item": "create:andesite_alloy"
    },
    {
      "chance": 5.0,
      "item": "create:cogwheel"
    },
    {
      "chance": 3.0,
      "item": "minecraft:gold_nugget"
    },
    {
      "chance": 2.0,
      "item": "create:shaft"
    },
    {
      "chance": 2.0,
      "item": "create:crushed_raw_gold"
    },
    {
      "item": "minecraft:iron_ingot"
    },
    {
      "item": "minecraft:clock"
    }
  ],
  "sequence": [
    {
      "type": "create:deploying",
      "ingredients": [
        {
          "item": "create:incomplete_precision_mechanism"
        },
        {
          "item": "create:cogwheel"
        }
      ],
      "results": [
        {
          "item": "create:incomplete_precision_mechanism"
        }
      ]
    },
    {
      "type": "create:deploying",
      "ingredients": [
        {
          "item": "create:incomplete_precision_mechanism"
        },
        {
          "item": "create:large_cogwheel"
        }
      ],
      "results": [
        {
          "item": "create:incomplete_precision_mechanism"
        }
      ]
    },
    {
      "type": "create:deploying",
      "ingredients": [
        {
          "item": "create:incomplete_precision_mechanism"
        },
        {
          "tag": "forge:nuggets/iron"
        }
      ],
      "results": [
        {
          "item": "create:incomplete_precision_mechanism"
        }
      ]
    }
  ],
  "transitionalItem": {
    "item": "create:incomplete_precision_mechanism"
  }
}
```
:::

---

## Data Classes

### object&lt;`Ingredient`&gt;

- `nbt`: object = {} (Optional)  
  NBT filter
- `chance`: number = 1 (Optional)

#### &lt;Item&gt;

- `item|tag`: string  
  Item id or tag, must be a ResourceLocation

#### &lt;Block&gt;

- `item|tag`: string  
  Block id or tag, must be a ResourceLocation

#### &lt;Fluid&gt;

- `fluid|fluidTag`: string  
  Fluid id or tag, must be a ResourceLocation
- `amount`: number = 1 (Optional)  
  Amount of the fluid/fluidTag

### object&lt;`Result`&gt;

- `nbt`: object = {} (Optional)  
  NBT filter
- `chance`: number = 1 (Optional)

#### &lt;Item&gt;

- `item`: string  
  Item id or tag, must be a ResourceLocation
- `count`: number = 1 (Optional)  
  Count of the item/tag

#### &lt;Block&gt;

- `item|tag`: string  
  Block id or tag, must be a ResourceLocation

#### &lt;Fluid&gt;

- `fluid`: string  
  Fluid id or tag, must be a ResourceLocation
- `amount`: number = 1 (Optional)  
  Amount of the fluid/fluidTag

### number&lt;`GameTick`&gt;

20 game tick = 1 second

---

<small>Copyright © 2022~ Mango Minecraft Notes. All rights reserved.</small>

{%hackmd @lumynou5/dark-theme %}
<!-- the theme made by Luminous-Coder -->