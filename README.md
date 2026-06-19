# @ryo/eslint-config

Strict ESLint configuration for TypeScript backend projects.

Built on top of [`typescript-eslint`](https://typescript-eslint.io/) `strictTypeChecked` + `stylisticTypeChecked` presets, with additional rules for code quality and consistency.

## Requirements

- ESLint >= 9.0.0
- TypeScript >= 5.0.0
- typescript-eslint >= 8.0.0


## What's included

### Presets

The following presets from `typescript-eslint` are applied automatically. See the [typescript-eslint docs](https://typescript-eslint.io/users/configs) for the full list of rules they include.

| Preset | Key rules included |
|---|---|
| `strictTypeChecked` | `await-thenable`, `no-floating-promises`, `no-explicit-any`, `no-unsafe-*`, `only-throw-error`, `unbound-method`, etc. |
| `stylisticTypeChecked` | `prefer-nullish-coalescing`, `prefer-optional-chain`, `prefer-includes`, `prefer-string-starts-ends-with`, etc. |

### Additional rules

Rules explicitly configured on top of the presets.

#### @typescript-eslint

| Rule | Config | Description |
|---|---|---|
| `class-methods-use-this` | error | Enforces converting class methods that don't use `this` to static methods |
| `consistent-type-exports` | fixMixedExportsWithInlineTypeSpecifier: true | Requires `export type` for type-only exports; mixed exports are fixed with inline type specifiers |
| `consistent-type-imports` | fixStyle: "separate-type-imports" | Requires the `type` keyword on type-only imports; auto-fix uses top-level `import type { Foo }` form |
| `default-param-last` | error | Requires default parameters to be placed last in the parameter list |
| `explicit-member-accessibility` | accessibility: "no-public" | Requires explicit accessibility modifiers; `public` is omitted as redundant |
| `member-ordering` | error | Enforces a consistent ordering of class members (static before instance, fields before constructor before methods, etc.) |
| `method-signature-style` | "property" | Requires interface method signatures to use property style: `method: () => void` |
| `naming-convention` | multiple selectors | Enforces naming conventions: catch-all default → camelCase / types → PascalCase / enum members → PascalCase or UPPER_CASE / imports → camelCase or PascalCase / variables and parameters → camelCase (leading `_` allowed) / global const variables → camelCase or UPPER_CASE / quoted names (requiresQuotes) → unrestricted |
| `no-import-type-side-effects` | error | Disallows `import { type Foo, type Bar }` (all-type inline imports) and requires `import type { Foo, Bar }` instead, so transpilers that don't understand the inline `type` keyword will still elide the entire import |
| `no-loop-func` | error | Disallows function declarations inside loops that close over loop variables |
| `no-shadow` | error | Disallows variable declarations that shadow variables from outer scopes |
| `no-unused-private-class-members` | error | Disallows unused `private` class members |
| `no-unused-vars` | args/vars/caughtErrors: all, `^_` exempted | Disallows unused variables; names prefixed with `_` are treated as intentionally unused |
| `no-use-before-define` | error | Disallows the use of variables, functions, and classes before they are defined |
| `no-useless-empty-export` | error | Disallows `export {}` when there are other exports in the file |
| `parameter-properties` | error | Disallows constructor parameter property shorthand (`constructor(public x: string)`) |
| `prefer-destructuring` | VariableDeclarator object only | Requires `const { x } = obj` over `const x = obj.x` for variable declarations with objects |
| `prefer-enum-initializers` | error | Requires explicit initializers on all enum members to avoid implicit numeric dependencies |
| `prefer-promise-reject-errors` | allowEmptyReject: true | Requires an `Error` object to be passed to `Promise.reject()`; empty rejects are allowed |
| `prefer-readonly` | error | Requires class properties that are never reassigned to be marked `readonly` |
| `promise-function-async` | error | Requires any function that returns a Promise to be declared `async` |
| `require-array-sort-compare` | ignoreStringArrays: true | Requires a comparison function to be passed to `Array.sort()`; string arrays are exempt |
| `return-await` | "always" | Requires `return await promise` in async functions for better stack traces and reliable `try/catch` error handling |
| `strict-void-return` | allowReturnAny: false | Disallows returning a value from a function typed to return `void`; `any` is also disallowed |
| `switch-exhaustiveness-check` | allowDefaultCaseForExhaustiveSwitch: false, considerDefaultExhaustiveForUnions: false, requireDefaultForNonUnion: true | Requires exhaustive switch coverage; union types must handle all variants explicitly (no `default` shortcut allowed), and non-union types must have a `default` |

#### Core ESLint

| Rule | Config | Description |
|---|---|---|
| `accessor-pairs` | error | Disallows setters that have no corresponding getter; getter-only (read-only) properties are allowed |
| `array-callback-return` | checkForEach: true | Requires `return` in callbacks of `map`, `filter`, `reduce`, etc.; also warns when a `forEach` callback returns a value (since `forEach` ignores return values) |
| `curly` | error | Requires braces `{}` for all `if`, `for`, `while`, etc. blocks |
| `default-case-last` | error | Requires the `default` case to appear last in `switch` statements |
| `eqeqeq` | always, null exempted | Requires `===`; `==` is only allowed for `null` comparisons |
| `grouped-accessor-pairs` | error | Requires getter and setter pairs to be defined adjacent to each other |
| `guard-for-in` | error | Requires a `hasOwnProperty` check (or similar) inside `for...in` loops |
| `logical-assignment-operators` | "always" | Requires logical assignment operators (`\|\|=`, `&&=`, `??=`) instead of `a = a \|\| b` |
| `new-cap` | newIsCap: true, capIsNew: false, properties: true | Requires constructor functions called with `new` to start with a capital letter; calling capitalized functions without `new` is allowed; also checks property accessors |
| `no-await-in-loop` | error | Disallows `await` inside loops; use `Promise.all` instead |
| `no-caller` | error | Disallows `arguments.caller` and `arguments.callee` |
| `no-cond-assign` | "always" | Disallows all assignments in conditional expressions |
| `no-constructor-return` | error | Disallows returning a value from constructors; bare `return;` for early exit is allowed |
| `no-duplicate-imports` | allowSeparateTypeImports: true | Disallows duplicate imports from the same module; separate type imports are allowed |
| `no-else-return` | allowElseIf: false | Disallows `else` / `else if` blocks after an `if` block that ends with `return` |
| `no-eval` | error | Disallows `eval()` |
| `no-extend-native` | error | Disallows extending native object prototypes |
| `no-extra-bind` | error | Disallows unnecessary `.bind()` calls |
| `no-implicit-coercion` | error | Disallows implicit type coercions such as `!!x`, `+x`, or `"" + x` |
| `no-iterator` | error | Disallows the `__iterator__` property (non-standard SpiderMonkey extension, never adopted into ECMAScript; use `Symbol.iterator` instead) |
| `no-labels` | error | Disallows labeled statements |
| `no-lone-blocks` | error | Disallows unnecessary `{}` blocks |
| `no-lonely-if` | error | Requires `else if` instead of a bare `if` as the only statement inside an `else` block |
| `no-multi-assign` | error | Disallows chained assignments like `a = b = c` |
| `no-multi-str` | error | Disallows multiline string literals using backslash continuation |
| `no-nested-ternary` | error | Disallows nested ternary expressions |
| `no-new` | error | Disallows `new` solely for side effects (result not used) |
| `no-new-func` | error | Disallows `new Function()` (equivalent risk to `eval`) |
| `no-new-wrappers` | error | Disallows `new String()`, `new Number()`, and `new Boolean()` |
| `no-octal-escape` | error | Disallows octal escape sequences in string literals (e.g. `\251`) |
| `no-promise-executor-return` | error | Disallows returning a value from a Promise executor; bare `return;` for early exit is allowed |
| `no-proto` | error | Disallows `__proto__`; use `Object.getPrototypeOf` instead |
| `no-restricted-exports` | bans `then` | Disallows a named export called `then` to avoid confusion with Promises |
| `no-restricted-globals` | `isFinite`, `isNaN` | Disallows the global `isFinite` and `isNaN`; use `Number.isFinite` and `Number.isNaN` instead |
| `no-restricted-properties` | `isFinite`, `isNaN`, `__defineGetter__`, etc. | Disallows specific property accesses: global `isFinite`/`isNaN` and deprecated `__defineGetter__` etc. |
| `no-restricted-syntax` | `const enum`, `TSExportAssignment` | Disallows `const enum` (bundler incompatibility) and `export =` (CommonJS style) |
| `no-return-assign` | "always" | Disallows all assignments inside `return` statements |
| `no-self-compare` | error | Disallows comparing a value to itself (`x === x`) |
| `no-sequences` | error | Disallows the comma operator (`a, b`) |
| `no-template-curly-in-string` | error | Disallows `${var}` inside regular strings; use template literals instead |
| `no-unassigned-vars` | error | Disallows variables that are declared but never assigned a value |
| `no-undef-init` | error | Disallows redundant `let x = undefined` initializations |
| `no-unmodified-loop-condition` | error | Disallows loop conditions where the tested variable is never modified inside the loop |
| `no-unneeded-ternary` | defaultAssignment: false | Disallows ternary expressions that can be simplified (e.g. `x ? x : y` → `x \|\| y`) |
| `no-unsafe-optional-chaining` | disallowArithmeticOperators: true | Disallows using the result of optional chaining (`?.`) in arithmetic operations |
| `no-useless-assignment` | error | Disallows assignments to variables that are never read after the assignment |
| `no-useless-call` | error | Disallows unnecessary `.call()` and `.apply()` |
| `no-useless-computed-key` | error | Disallows unnecessary computed property keys like `{ ['foo']: 1 }` |
| `no-useless-concat` | error | Disallows concatenation of string literals that could be merged |
| `no-useless-rename` | error | Disallows renaming imports/exports to the same name (`import { a as a }`) |
| `no-useless-return` | error | Disallows unnecessary `return;` at the end of a function |
| `object-shorthand` | "always" | Requires object shorthand: `{ x }` instead of `{ x: x }` |
| `one-var` | initialized: "never" | Requires one declaration per initialized variable (`let a = 1, b = 2` is disallowed) |
| `operator-assignment` | "always" | Requires compound assignment operators: `x += 1` instead of `x = x + 1` |
| `prefer-arrow-callback` | error | Requires arrow functions for callbacks |
| `prefer-const` | destructuring: "all" | Requires `const` for variables that are never reassigned; destructuring requires all variables to be non-reassigned |
| `prefer-exponentiation-operator` | error | Requires `x ** y` instead of `Math.pow(x, y)` |
| `prefer-numeric-literals` | error | Requires numeric literals (`0b11`) instead of `parseInt('0b11', 2)` |
| `prefer-object-has-own` | error | Requires `Object.hasOwn(obj, key)` instead of `Object.prototype.hasOwnProperty.call(obj, key)` |
| `prefer-object-spread` | error | Requires `{ ...obj }` instead of `Object.assign({}, obj)` |
| `prefer-regex-literals` | disallowRedundantWrapping: true | Requires regex literals (`/foo/`) instead of `new RegExp('foo')` |
| `prefer-template` | error | Requires template literals instead of string concatenation |
| `radix` | error | Requires a radix argument to be passed to `parseInt()` |
| `semi` | error | Requires semicolons at the end of statements |
| `symbol-description` | error | Requires a description string to be passed to `Symbol()` |
| `use-isnan` | enforceForIndexOf: true | Disallows direct comparisons with `NaN`; also requires `Number.isNaN` in `indexOf` etc. |
| `valid-typeof` | requireStringLiterals: true | Restricts `typeof` comparisons to string literals to prevent typos |
| `yoda` | never, exceptRange: true | Disallows yoda conditions (`'foo' === x`); range checks (`0 < x && x < 10`) are allowed |

## License

MIT
