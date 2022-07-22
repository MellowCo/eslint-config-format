# @meoc/eslint-config-format

- 使用eslint取代prettier做代码格式化
- 单引号
- 自动修复格式
- 保证空格一致
- 最大连续空行数2行

## 用法

### 下载
``` 
pnpm add -D eslint @meoc/eslint-config-format
```

### .eslintrc
```js
{
  "extends": "@meoc/eslint-config-format"
}
```

# 规则
## rules
```js
  rules: {
    // 不允许连续空格
    "no-multi-spaces": "error",
    // 空2格 switch case
    "indent": ["error", 2, { "SwitchCase": 1 }],
    // 对象大括号空格 {   a:b   } => { a:b }
    "object-curly-spacing": ["error", "always"],
    // 括号去除空格 foo(   'bar'   ) =>  foo('bar');
    "space-in-parens": ["error", "never"],
    // 对象分号前后只有一个空格{ "foo"  :    42 } => { "foo": 42 };
    "key-spacing": ["error", { mode: "strict" }],
    // 逗号前后的空格  [1,     2,  3  ,4] => [1, 2, 4, 4]
    "comma-spacing": ["error", { "before": false, "after": true }],
    // 括号内使用空格 [ 1,2   ] => [ 1,2 ]
    "array-bracket-spacing": ["error", "always"],
    // if else 风格
    "brace-style": ["error", "1tbs"],
    // 函数调用空格 fn  () => fn()
    "func-call-spacing": ["error", "never"],
    // 函数左括号空格 function name         () {} => function name(){}
    "space-before-function-paren": ["error", "never"],
    // 语句块的空格 function name() {} => function name(){}
    "space-before-blocks": ["error", "never"],
    // 关键字前后空格 if  () => if()
    "keyword-spacing": ["error", {
      "overrides": {
        "if": { "after": false, before: false },
        "else": { "after": false, before: false },
      }
    }],
    // 对象取值不能有空格 obj  .  foo => obj.foo
    "no-whitespace-before-property": "error",
    // 最大连续空行数
    "no-multiple-empty-lines": ["error", { "max": 2, "maxEOF": 1, "maxBOF": 0 }],
    // 代码块中去除前后空行
    "padded-blocks": ["error", "never"],
    // ;前后空格 var foo   ;   var bar; => var foo;var bar;
    "semi-spacing": ["error", { "before": false, "after": false }],
    // 操作符是否空格 a=0 => a = 0
    "space-infix-ops": "error",
    // 操作符空格 + -
    "space-unary-ops": "error",
     // 箭头函数空格 ()=>{}  => () => {}
    "arrow-spacing": ["error", { "before": true, "after": true }],
    // 扩展运算符 {... f} => {...f}
    "rest-spread-spacing": "error",
    // 字符串拼接使用模版字符串 'hello' + world => `hello${world}`
    "prefer-template": "error",
    // 模版字符串中去除空格 `${ fo  }` =>${fo}
    "template-curly-spacing": ["error", "never"],
    // 链式调用换行
    "newline-per-chained-call": ["error", { "ignoreChainWithDepth": 1 }],
    // 禁止重复模块导入
    "no-duplicate-imports": "error",
    // 注释各一个 //a => // a
    "spaced-comment": ["error", "always"],
    // 使用单引号，字符串中包含了一个其它引号 允许"a string containing 'single' quotes"
    quotes: ["error", "single", { "avoidEscape": true }]
  },
``` 

## [no-multi-spaces](https://eslint.bootcss.com/docs/rules/no-multi-spaces)
```js
// 不允许连续空格
"no-multi-spaces": "error",
```

> 当配置某些空格规则，通常第二个参数，为`never`或`always`
* `never` 表示不需要空格
* `always` 表示需要1个或多个空格

```js
// 括号内使用空格 [ 1,2   ] => [ 1,2 ]
"array-bracket-spacing": ["error", "always"],
```
当单独使用`always`时，无法限定好空格的数量，只要空格大于`1`都可以通过`eslint`的校验
```js
const arr = [1, 2, 3] //false
const arr = [ 1, 2, 3 ] // true
const arr = [ 1, 2, 3    ] // true
```
搭配`no-multi-spaces`则可以限定空格的数量为`1`
```js
// 不允许连续空格
"no-multi-spaces": "error",
// 括号内使用空格 [ 1,2   ] => [ 1,2 ]
"array-bracket-spacing": ["error", "always"]

const arr = [1, 2, 3] //false
const arr = [ 1, 2, 3    ] // false
const arr = [ 1, 2, 3 ] // true
```

## [indent](https://eslint.bootcss.com/docs/rules/indent)
> 使用一致的缩进
```js
 // 空2格
 "indent": ["error", 2],
```

## [object-curly-spacing](https://eslint.bootcss.com/docs/rules/object-curly-spacing)
> 花括号中使用一致的空格
```js
// 对象大括号空格 {   a:b   } => { a:b }
"object-curly-spacing": ["error", "always"],
```

## [space-in-parens](https://eslint.bootcss.com/docs/rules/space-in-parens)
> 圆括号内的空格

```js
// 括号去除空格 foo(   'bar'   ) =>  foo('bar');
"space-in-parens": ["error", "never"],
```

## [key-spacing](https://eslint.bootcss.com/docs/rules/key-spacing)
> 对象分号前后的空格
第2个参数为对象类型，通过`beforeColon`和`afterColon`设置前后的空格
```js
"key-spacing": 
["error", { 
    "beforeColon": false|true, 
    "afterColon":false|true,"mode":
    "strict" | "minimum"
}]
```
* `"beforeColon": false (默认) | true`
    * `false`: 禁止存在空格
    * `true`: 要求至少有一个空格  
* `"afterColon": true (默认) | false`
    -   `true`: 要求至少有一个空格
    -   `false`: 禁止存在空格

- `"mode": "strict" (默认) | "minimum"`
    -   `"strict"`: 强制在冒号前后只有一个空格
    -   `"minimum"`: 要求在冒号前后最少有一个空格

```js
// 对象分号前后只有一个空格{ "foo"  :    42 } => { "foo": 42 };
"key-spacing": ["error", { mode: "strict" }],
```

## [comma-spacing](https://eslint.bootcss.com/docs/rules/comma-spacing)
> 逗号(，)周围的空格
通过`before`和`after`，设置前后空格
```js
// 逗号前后去除空格  [1,     2,  3  ,4] => [1, 2, 3, 4]
"comma-spacing": ["error", { "before": false, "after": true }]
```

## [array-bracket-spacing](https://eslint.bootcss.com/docs/rules/array-bracket-spacing)
> 在方括号[]内使用空格

```js
"array-bracket-spacing": ["error", "always"],
```

## [space-infix-ops](https://eslint.bootcss.com/docs/rules/space-infix-ops)

> 操作符周围空格
```js
 // 操作符是否空格 a=0 => a = 0
 "space-infix-ops": "error",
```

## [space-unary-ops](https://eslint.bootcss.com/docs/rules/space-unary-ops)
> 一元操作符空格 (`-` `+` `--`  `++`  `!`  `!!`)
```js
// 操作符空格 + -
"space-unary-ops": "error",
```

## [brace-style](https://eslint.bootcss.com/docs/rules/brace-style)
> 大括号风格要求
```js
function foo()         function foo() {
{                        return true;
  return true;   =>    }    
}                      



if (foo)           if (foo) {
{                     bar();
  bar();   =>      } else {
}                     baz();  
                   }
```

```js
// if else 风格
"brace-style": ["error", "1tbs"],
```

## [func-call-spacing](https://eslint.bootcss.com/docs/rules/func-call-spacing)
> 调用函数时的空格
```js
// 函数调用空格 fn   () => fn()
"func-call-spacing": ["error", "never"],
``` 

## [space-before-function-paren](https://eslint.bootcss.com/docs/rules/space-before-function-paren)

> 函数左括号空格

```js
// 函数左括号空格 function name     () {} => function name(){}
"space-before-function-paren": ["error", "never"],
```

## [space-before-blocks](https://eslint.bootcss.com/docs/rules/space-before-blocks)

> 语句块的空格 (简单理解，去除函数右括号空格)
```js
// 语句块的空格 function name()     {} => function name(){}
"space-before-blocks": ["error", "never"],
```

## [keyword-spacing](https://eslint.bootcss.com/docs/rules/keyword-spacing)
> 关键字周围空格 (if else from for ...)
```js
"keyword-spacing": ["error", {
  "overrides": {
    "if": { "after": false, before: false },
    "else": { "after": false, before: false },
  }
}]
```
## [no-whitespace-before-property](https://eslint.bootcss.com/docs/rules/no-whitespace-before-property)
> 对象取值空格
```js
// 对象取值空格 obj  .  foo => obj.foo
"no-whitespace-before-property": "error"
```

## [no-multiple-empty-lines](https://eslint.bootcss.com/docs/rules/no-multiple-empty-lines)
> 连续空行
* `max` 最大连续空行数
* `maxEOF` 文件末尾的最大连续空行数
* `maxBOF` 文件开始的最大连续空行数

```js
"no-multiple-empty-lines": ["error", { "max": 2, "maxEOF": 1, "maxBOF": 0 }],
```

## [padded-blocks](https://eslint.bootcss.com/docs/rules/padded-blocks)
> 代码块中空行
```js
// 代码块中去除前后空行
"padded-blocks": ["error", "never"],
```

## [semi-spacing](https://eslint.bootcss.com/docs/rules/semi-spacing)
> 分号前后空格
```js
// 前后空格 var foo   ;   var bar; => var foo;var bar;
"semi-spacing": ["error", { "before": false, "after": false }],
```

## [arrow-spacing](https://eslint.bootcss.com/docs/rules/arrow-spacing)
> 箭头函数的箭头空格
```js
 // 箭头函数空格 ()=>{}  => () => {}
"arrow-spacing": ["error", { "before": true, "after": true }],
```

## [rest-spread-spacing](https://eslint.bootcss.com/docs/rules/rest-spread-spacing)
> 扩展运算符(...)空格
```js
// 扩展运算符 {...   f} => {...f}
"rest-spread-spacing": "error"
```

## [prefer-template](https://eslint.bootcss.com/docs/rules/prefer-template)
> 使用模板字面量而非字符串连接
```js
// 字符串拼接使用模版字符串 'hello' + world => `hello${world}`
"prefer-template": "error",
```

## [template-curly-spacing](https://eslint.bootcss.com/docs/rules/template-curly-spacing)
> 模板字符串中空格
```js
// 模版字符串中去除空格 `${ fo  }` =>${fo}
"template-curly-spacing": ["error", "never"],
```

## [newline-per-chained-call](https://eslint.bootcss.com/docs/rules/newline-per-chained-call)
> 链式调用换行
```js
// 链式调用换行
// _.chain({}).map(foo).filter(bar).value();

// _
// .chain({})
// .map(foo)
// .filter(bar)
// .value();

"newline-per-chained-call": ["error", { "ignoreChainWithDepth": 1 }],
```

## [no-duplicate-imports](https://eslint.bootcss.com/docs/rules/no-duplicate-imports)
> 禁止重复导入
```js
// 禁止重复模块导入
"no-duplicate-imports": "error",
```

## [spaced-comment](https://eslint.bootcss.com/docs/rules/spaced-comment)
> 注释前有空白
```js
 // 注释空格 //a => // a
 "spaced-comment": ["error", "always"],
```

## [quotes](https://eslint.bootcss.com/docs/rules/quotes)
> 单引号
```js
// 使用单引号，字符串中包含了一个其它引号 允许"a string containing 'single' quotes"
quotes: ["error", "single", { "avoidEscape": true }]
```
