---
title: component is v-bind
badges:
  - breaking
---

# {{ $frontmatter.title }} <MigrationBadges :badges="$frontmatter.badges" />

## Overview

- **BREAKING**: `v-bind="{ is: 'h1' }"` on `<component/>` is not supported.

## Introduction

When using `v-bind` on a `<component` without `:is`, the template compiler won't be to check if the javascript expression contains `:is`.

## 2.x Syntax

In 2.x, `v-bind` will be passed on the object props and it will render the component if `is` prop is passed

```html
<!-- template -->
<component v-bind="{ is: 'h1' }"></component>
<!-- result -->
<h1></h1>
```

## 3.x Syntax

In 3x, the template compiler will need an explicitly `is` prop to be able to optimize code

```html
<!-- template -->
<component v-bind="{ is: 'h1' }"></component>
<!-- result -->
<div is="h1"></div>

<!-- template -->
<div is="h1"></div>
<!-- result -->
<h1></h1>
```

## Migration Strategy

If you are relying on `v-bind` to pass `is`, we currently recommend ensuring that you are passing `is` outside of the bind.
