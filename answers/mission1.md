# Mission 1: Python habits that break JavaScript security

## Evidence

Output of `npm run test:m1`, pasted or as a screenshot in `img/`:

```
24 passed, 0 failed 
```

## Connections: Python to JavaScript

For each check you implemented, write how you would do it in Python and how you did it in JavaScript.

| Rule | Python | JavaScript, as in my code |
|---|---|---|
| raw is a dictionary or object, not a list | `isinstance(raw, dict)` | `typeof raw === "object" && raw !== null && !Array.isArray(raw)` |
| name is a non-empty string after trimming | `isinstance(raw["name"], str) and raw["name"].strip() != ""` | `typeof raw.name === "string" && raw.name.trim().length > 0` |
| status is one of the allowed values | `raw["status"] in ["up", "degraded", "down"]` | `ALLOWED_STATUS.includes(raw.status)` |
| online is a real boolean | `isinstance(raw["online"], bool)` | `typeof raw.online === "boolean"` |
| latencyMs is a finite number ≥ 0 | `isinstance(raw["latencyMs"], (int, float)) and math.isfinite(raw["latencyMs"]) and raw["latencyMs"] >= 0` | `typeof raw.latencyMs === "number" && Number.isFinite(raw.latencyMs) && raw.latencyMs >= 0` |
| invalid JSON does not crash the program | `try: ... except:` | `try { ... } catch (error) { ... }` |

## Questions

1. Why is `latencyMs: 0` a trap for code such as `if (!raw.latencyMs) return null;`?

 > Because 0 is falsy in JavaScript, !raw.latencyMs would treat a valid latency of 0 as missing and reject it.

2. Your function builds a **new** object and ignores fields like `isAdmin`. Describe in two or three sentences what could go wrong later in an application that copied **every** field it received.

   > Copying every field could keep unsafe data like `isAdmin`. Using only the needed fields is safer.

## Documentation log 

| Page I used, with URL | One thing I learned from it |
|---|---|
| MDN Number.isFinite() - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/isFinite | I learned it checks if a number is finite. |


test