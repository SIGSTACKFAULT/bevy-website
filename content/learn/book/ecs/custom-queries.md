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

Now, let's write our very own custom query! We'll use some components defined on [Entites Have Components](../entities-components#defining-components)

```rs
use bevy::prelude::*;
use bevy::ecs::query::{QueryData, QueryFilter};

#[derive(QueryData)]
struct CombatantQuery {
    _marker: &'static Combatant,
    life: &'static Life,
    stats: &'static Stats,
    allegiance: &'static Allegiance,
    in_combat: Option<&'static InCombat>,
}
```

Unlike [`Query`] arguments which are regular old references, in a custom query we write `&'static`. This is because
{% todo() %}
I have no idea why.
{% end %}
