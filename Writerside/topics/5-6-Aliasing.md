# 5.6. Aliasing

Aliasing in S++ allows for two things for renaming a type, that is possibly from another namespace too. This is useful
for when a type is used in multiple places, but the name of the type is too long to be used everywhere. Furthermore,
this allows for importing types from namespaces into the current namespace.

## Reducing the namespace of a type

Whilst all the following examples use namespaces to demonstrate the concept, it should be noted that namespaces are
syntactically optional for the `use` statement, explained in the [aliasing](#non-namespaced-aliasing) section.

### Reduction examples

#### Reduce single types

```
use some.long.namespace_a.{Type1}
use some.long.namespace_b.{Type2}
```

```
use some.long.{namespace_a.Type1, namespace_b.Type2}
```

#### Reduce multiple types

```
use some.long.namespace_a.{Type1, Type2}
use some.long.namespace_b.{Type3, Type4}
```

```
use some.long.{namespace_a.{Type1, Type2}, namespace_b.{Type3, Type4}}
```

#### Reduce all types

```
use some.long.namespace_a.*
use some.long.namespace_b.*
```

```
use some.long.{namespace_a.*, namespace_b.*}
```

## Aliasing

Aliasing can be done just like above, but with the `as` keyword as-well:

#### Examples

```
use some.long.namespace_a.{Type1 as T1}
use some.long.namespace_b.{Type2 as T2}
use some.long.namespace_c.{Type3 as T3, Type4 as T4}
use some.long.namespace_d.{Type5 as T5, Type6 as T6}
```

```
use some.long.{
    namespace_a.{Type1 as T1},
    namespace_b.{Type2 as T2},
    namespace_c.{Type3 as T3, Type4 as T4},
    namespace_d.{Type5 as T5, Type6 as T6}
}
```

### Non-namespaced aliasing

Because namespaces are optional, types from the current scope can be aliased too:

#### Example

```
use Type1 as T1
use {Type2 as T2, Type3 as T3}
```