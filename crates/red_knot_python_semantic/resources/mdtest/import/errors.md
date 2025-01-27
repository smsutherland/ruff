# Unresolved Imports

## Unresolved import statement

```py
import bar # error: "Cannot resolve import `bar`"
reveal_type(bar)  # revealed: Unknown
```

## Unresolved import from statement

```py
from bar import baz # error: "Cannot resolve import `bar`"
reveal_type(baz)  # revealed: Unknown
```

## Unresolved import from resolved module

```py path=a.py
```

```py
from a import thing # error: "Module `a` has no member `thing`"
reveal_type(thing)  # revealed: Unknown
```

## Resolved import of symbol from unresolved import

```py path=a.py
import foo as foo # error: "Cannot resolve import `foo`"
reveal_type(foo)  # revealed: Unknown
```

Importing the unresolved import into a second file should not trigger an additional "unresolved
import" violation:

```py
from a import foo
reveal_type(foo)  # revealed: Unknown
```

## No implicit shadowing

```py path=b.py
x: int
```

```py
from b import x

x = 'foo'  # error: [invalid-assignment] "Object of type `Literal["foo"]"
```
