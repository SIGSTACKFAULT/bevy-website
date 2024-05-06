+++
title = "Custom Queries"
# insert_anchor_links = "right"
[extra]
weight = 9
status = 'hidden'
+++

{% todo() %}
* steal from [bevy/examples/custom_query_param.rs](https://github.com/bevyengine/bevy/blob/main/examples/ecs/custom_query_param.rs)
* recommend `duplicate` crate for impling for the ro and rw version of a custom query
* think of a good example
{% end %}

Ever find yourself writing out the same dozen systems parameters, over and over? Fear not! **Custom Queries** are here to save you.

<details>
<summary>Some Components We'll Use</summary>

```rs
/// our game happens on on a grid; another system updates the Transform
struct Position(IVec2);

/// health component; shared between players and enemies
struct Health(u32);

/// the player is the only thing with an inventory, XP, or levels
struct Player {
    inventory: Vec<Item>,
    exp: u32,
    level: u32,
};

/// marker for enemies
struct Enemy;
```
</details>

Now, let's write our very own custom query!

```rs
use bevy::prelude::*;
use bevy::ecs::query::{QueryData, QueryFilter};

#[derive(QueryData)]
struct PlayerQuery {
    player: Player,
    position: Position,
    health: Health,
}
```
