---
title: CSS WorkFlow
date: 2020-08-06 22:25:09
tags: Doc
comments: true

---

## CSS预处理器

处理特定格式源文件到目标css的处理程序

### 预处理器的变革

1. CSS中使用后端模版变量统一处理CSS重复的值
2. sass/less/stylus 
3. 直接书写css



### 预处理器有哪些规范

1. 变量
2. 混合（Mixin)Extend
3. 嵌套规则
4. 运算
5. 函数
6. Namespaces & Accessors
7. Scope
8. 注释

### CSS后处理器

1. CSS压缩 CLEAN-CSS
2. 自动添加浏览器前缀Autoprefixer
3. CSS更加美观顺序 CSScomb
4. Rework取代Stylus后处理器发热
5. 前后通吃PostCSS (预处理器和后处理器)



### 老式处理过程

Source => Parser => AST(类CSS) => Interpreter => AST(纯CSS) => Translator => CSS

#### 新型的处理过程 （共享AST,最后生成CSS)

Source => Parser => AST(纯CSS) => Plugin system [post-simple-vars, post-mixins, PostNested, post-custom...]  => AST(纯CSS) => Translator => CSS

抽象语法树（Abstract Syntax Tree, AST)作为程序的一种中间表示形式

## PostCSS

**Use tomorrow’s CSS syntax, today.**  今天使用未来的CSS语法

#### cssnext （此库已经弃用）

官网介绍：https://cssnext.github.io/

#### [特性](https://cssnext.github.io/features/)

- [automatic vendor prefixes](https://cssnext.github.io/features/#automatic-vendor-prefixes)
- [custom properties & `var()`](https://cssnext.github.io/features/#custom-properties-var) 
- [custom properties set & `@apply`](https://cssnext.github.io/features/#custom-properties-set-apply) 
- [reduced `calc()`](https://cssnext.github.io/features/#reduced-calc)
- [custom media queries](https://cssnext.github.io/features/#custom-media-queries)
- [media queries ranges](https://cssnext.github.io/features/#media-queries-ranges)
- [custom selectors](https://cssnext.github.io/features/#custom-selectors)
- [nesting](https://cssnext.github.io/features/#nesting)
- [`image-set()` function](https://cssnext.github.io/features/#image-set-function)
- [`color()` function](https://cssnext.github.io/features/#color-function)
- [`hwb()` function](https://cssnext.github.io/features/#hwb-function)
- [`gray()` function](https://cssnext.github.io/features/#gray-function)
- [`#rrggbbaa` colors](https://cssnext.github.io/features/#rrggbbaa-colors)
- [`rgba` function (`rgb` fallback)](https://cssnext.github.io/features/#rgba-function-rgb-fallback) 
- [`rebeccapurple` color](https://cssnext.github.io/features/#rebeccapurple-color)
- [`font-variant` property](https://cssnext.github.io/features/#font-variant-property)
- [`filter` property](https://cssnext.github.io/features/#filter-property) (svg fallback)
- [`initial` value](https://cssnext.github.io/features/#initial-value)
- [`rem` unit](https://cssnext.github.io/features/#rem-unit-px-fallback) (`px` fallback)
- [`:any-link` pseudo-class](https://cssnext.github.io/features/#any-link-pseudo-class)
- [`:matches` pseudo-class](https://cssnext.github.io/features/#matches-pseudo-class)
- [`:not` pseudo-class](https://cssnext.github.io/features/#not-pseudo-class) (to l.3)
- [`::`pseudo syntax](https://cssnext.github.io/features/#pseudo-syntax-fallback) (`:` fallback)
- [`overflow-wrap` property](https://cssnext.github.io/features/#overflow-wrap-property-word-wrap-fallback) (`word-wrap` fallback)
- [attribute case insensitive](https://cssnext.github.io/features/#attribute-case-insensitive)
- [`rgb()` function](https://cssnext.github.io/features/#rgb-function-functional-notation) (functional-notation)
- [`hsl()` function](https://cssnext.github.io/features/#hsl-function-functional-notation) (functional-notation)
- [`system-ui` font-family](https://cssnext.github.io/features/#system-ui-font-family) (font-family fallback)

#### 提供书写前和书写的案例

https://cssnext.github.io/playground/

#### 注意

cssnext已经被弃用，可以迁移至[`postcss-preset-env`](http://preset-env.cssdb.org/)

弃用库的原因可查看地址：https://moox.io/blog/deprecating-cssnext/



#### post-preset-env

官网地址：http://preset-env.cssdb.org/

####  W3C标准的实现

1. 变量

   ```css
   :root {
     --main-bg-color: gray;
     --x: 0.5;
     --y: 0.5;
   }
   ```

2. 使用CSS变量

   ```css
   body {
     backgorund: var(--main-bg-color);
   }
   ```

3. CSS变量结合calc计算公式

   ```css
   left: calc(100px * var(--x));
   ```

4. 使用CSS变量的默认值

   ```css
   right: calc(100px * var(--x, 0.1));
   ```

5. Javascript给CSS变量赋值

   ```javascript
   var el = document.documentElement;
   document.addEventListener("mousemove", ({ clientX, clientY}) => {
     let x = clientX / innerWidth;
     let y = clientY / innerHeight;
     el.style.setProperty("--x", x);
     el.style.setProperty("--y", y);
   })
   ```



#### POSTCSS 插件

1. [postcss-custom-properties](https://github.com/postcss/postcss-custom-properties) 允许使用自定义属性，运行时的变量
2. [postcss-simple-vars ](https://github.com/postcss/postcss-simple-vars) 可以在值和选择器中使用变量与scss一致变量实现
3. [postcss-mixins](https://github.com/postcss/postcss-mixins) 实现类似SASS的@mixin功能
4. [postcss-extend](https://github.com/travco/postcss-extend) 实现类似SASS的继承功能
5. [postcss-import](https://github.com/postcss/postcss-import) 实现类似SASS功能的@import 
6. Cssnext 面向未来 CSSGrace修复过去



