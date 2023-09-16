---
title: Unused private fields should be removed
---

# Unused private fields should be removed

Unused private fields constitute dead code and should therefore be removed.

tags: #java

```grit
language java

class_body($declarations) where {
    $declarations <: contains {
        field_declaration() as $field where {
            $field <: contains variable_declarator($name) where {
                $declarations <: not contains $name until field_declaration(),
                $field => .,
            }
        }
    }
}
```

## Removes unused fields and preserves used fields

```java
public class MyClass {
  private int foo = 42;
  private int bar = 24;

  public int compute(int a) {
    return a * bar + 42;
  }
}
```

```java
public class MyClass {
  
  private int bar = 24;

  public int compute(int a) {
    return a * bar + 42;
  }
}
```
