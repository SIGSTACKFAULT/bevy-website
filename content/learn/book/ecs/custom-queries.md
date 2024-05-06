+++
title = "Custom Query Parameters"
insert_anchor_links = "right"
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

Now, let's write our very own custom query! We'll use some components defined earlier in [Entites Have Components](../entities-components#defining-components)

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

Unlike [`Query`](../systems-queries) arguments which are regular old references, in a custom query we write `&'static`. This is just a contrivance to avoid having to constantly write lifetime parameters on any function that uses. [Read more about why below.](#why-the-static)



## Why the `&'static`?

{% todo() %}
Rewrite this into something more docs-y with examples and such. james.obrien on discord very helpfully explained it and this writer is too dumb to re-explain it: https://discordapp.com/channels/691052431525675048/749335865876021248/1236859745944600698

> Ah, in order to have a reference inside a struct in rust you need to either mark it as 'static or give it a lifetime. The  lifetime would have to then be a generic on the struct and you would have to add it everywhere you use it.
> This also applies recursively to the surround scope, if you were to add a lifetime generic to `WorldQuery` you would then need to either specify it in your system function definition as `'static` or supply another generic lifetime you would then have to add to the system etc. etc.
> In the end `&T` in a query type definition is only a marker to say "I want a reference to T here", the lifetime on the reference in the type is irrelevant as the lifetime is constrained by the borrow on the query
{% end %}
