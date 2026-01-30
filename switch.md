# Java `switch` — Complete Guide (From Basics to Modern Java)

This is a **from‑scratch to advanced** guide on Java `switch`, covering **classic switch**, **modern switch expressions**, **edge cases**, **performance**, and **best practices**.

---

## 1. What is `switch`?

`switch` is a **multi-branch conditional statement/expression** that executes code based on the value of a single expression.

Use it when:
- One variable decides the flow
- Possible values are fixed and known

---

## 2. Classic `switch` Syntax (Java ≤ 11)

```java
switch (expression) {
    case value1:
        // code
        break;
    case value2:
        // code
        break;
    default:
        // code
}
```

### Example

```java
int day = 3;

switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    case 3:
        System.out.println("Wednesday");
        break;
    default:
        System.out.println("Invalid day");
}
```

---

## 3. Importance of `break`

Without `break`, execution **falls through** to the next case.

```java
int x = 2;

switch (x) {
    case 1:
        System.out.println("One");
    case 2:
        System.out.println("Two");
    case 3:
        System.out.println("Three");
}
```

**Output**
```
Two
Three
```

---

## 4. Intentional Fall-through

Used when multiple cases share the same logic.

```java
switch (month) {
    case 12:
    case 1:
    case 2:
        System.out.println("Winter");
        break;
    case 3:
    case 4:
    case 5:
        System.out.println("Spring");
        break;
}
```

---

## 5. `default` Case

- Optional
- Executes when no case matches
- Best placed at the end

```java
switch (status) {
    default:
        System.out.println("Unknown status");
        break;
}
```

---

## 6. Supported Types in `switch`

### Allowed
- `byte`, `short`, `int`, `char`
- `enum`
- `String` (Java 7+)
- Wrapper types (auto-unboxing)

### Not Allowed
- `long`
- `float`, `double`
- `boolean`
- Arbitrary objects

---

## 7. `switch` with `String`

```java
String role = "ADMIN";

switch (role) {
    case "ADMIN":
        System.out.println("Full access");
        break;
    case "USER":
        System.out.println("Limited access");
        break;
    default:
        System.out.println("No access");
}
```

Notes:
- Case-sensitive
- `null` throws `NullPointerException`

---

## 8. `switch` with `enum` (Recommended)

```java
enum OrderStatus {
    NEW, PAID, SHIPPED, DELIVERED
}

switch (status) {
    case NEW:
        break;
    case PAID:
        break;
}
```

Advantages:
- Compile-time safety
- No magic strings
- Faster execution

---

## 9. Modern `switch` Expressions (Java 12+)

### Old (statement style)

```java
int result;
switch (x) {
    case 1:
        result = 10;
        break;
    case 2:
        result = 20;
        break;
    default:
        result = 0;
}
```

### New (expression style)

```java
int result = switch (x) {
    case 1 -> 10;
    case 2 -> 20;
    default -> 0;
};
```

Features:
- No `break`
- No fall-through
- Returns a value

---

## 10. Multiple Values per Case

```java
String type = switch (day) {
    case 1, 7 -> "Weekend";
    case 2, 3, 4, 5, 6 -> "Weekday";
    default -> "Invalid";
};
```

---

## 11. `yield` in Switch Expressions

Used for multi-line logic.

```java
int price = switch (category) {
    case "A" -> {
        int base = 100;
        yield base + 20;
    }
    case "B" -> {
        yield 200;
    }
    default -> 0;
};
```

---

## 12. Exhaustiveness with Enums

Compiler ensures all cases are handled.

```java
int priority = switch (status) {
    case NEW -> 1;
    case PAID -> 2;
    case SHIPPED -> 3;
    case DELIVERED -> 4;
};
```

No `default` required if all enum values are covered.

---

## 13. Null Handling

Classic `switch` does not handle `null`.

```java
if (str == null) {
    // handle null
} else {
    switch (str) {
        case "A" -> {}
    }
}
```

---

## 14. Performance Considerations

- Dense integer values → `tableswitch`
- Sparse values → `lookupswitch`
- Enum switches are fastest
- String switches use hash + equals

---

## 15. Common Mistakes

- Missing `break`
- Switching on `null`
- Overusing `String` instead of `enum`
- Complex logic inside `switch`

---

## 16. When NOT to Use `switch`

Avoid when:
- Conditions are ranges
- Logic is complex
- Behavior changes frequently

### Alternative

```java
Map<String, Runnable> actions = Map.of(
    "A", () -> doA(),
    "B", () -> doB()
);

actions.getOrDefault(key, () -> {}).run();
```

---

## 17. `switch` vs `if-else`

Use `switch` when:
- One variable
- Fixed values

Use `if-else` when:
- Ranges
- Multiple conditions

---

## 18. Key Takeaway

> Java `switch` has evolved from a fall-through statement to a powerful, safe expression with value returns, exhaustiveness, and cleaner syntax.

---
