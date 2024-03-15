# 7.4. The Law of Exclusivity

Another core memory feature of S++ to ensure safety is the enforcement of the Law of Exclusivity. This prevents
overlapping mutable borrows from being taken at the same time, as this could lead to data races and inconsistent memory
reads. As this is enforced at compile time, it is impossible to ever get a memory-related error concerning overlapping
borrows at runtime.

## The Laws

1. No more than one overlapping mutable borrows can exist at any given time.
2. Any number of immutable overlapping borrows can exist at any given time.
3. Rules `1` and `2` cannot occur at the same time.

## Overlapping

The laws apply to overlapping borrows. An overlap is where one of the two potentially conflicting borrows contains
the other borrow. A borrow contains another borrow if it starts with the same, or is the same, attribute /
identifier:

- `x` overlaps with `x`, because `x` contains `x`.
- `x.a` overlaps with `x`, because `x` contains `x.a`.
- `x.a` doesn't overlap with `x.b`, because `x.a` does not contain `x.b`.

Therefore, for example, a mutable borrow to `x.a` means that no other borrows to `x` or anything `x.a` contains can
be taken at the same time.

In the third example, `x.a` and `x.b` do not overlap. This is because the specific attribute is specified, and so only
from that attribute and inwards does the exclusivity apply. Because `x.a` and `x.b` do not overlap, they can be
mutably borrowed from at the same time.
