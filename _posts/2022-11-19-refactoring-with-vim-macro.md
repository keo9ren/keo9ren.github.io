---
layout: post
title: Refactoring with Vim Macro - Vimspired Series 1
--- 
Let's say you have this code, which is Angular unittest code, and you have many more lines like this.
You want to refactor this, to make it more try like in Example 2. Then typing it all, is not very efficient, but that's when (Idea-)Vims Makro come in handy.

Example 1
```typescript
function getSubmitHarness() {
  return loader.getHarness(MatButtonHarness.with({selector: '[data-id="submit"]'}));
}

function getUsernameHarness() {
  return loader.getHarness(MatInputHarness.with({selector: '[data-id="username"]'}));
}

function getPasswordHarness() {
  return loader.getHarness(MatInputHarness.with({selector: '[data-id="password"]'}));
}
```

Example 2
```typescript
function dataId(name: string) {
    return {
        selector: `[data-id="${name}]"`
    }
}

function getSubmitHarness() {
    return loader.getHarness(MatButtonHarness.with(dataId('submit')));
}

function getUsernameHarness() {
    return loader.getHarness(MatInputHarness.with(dataId('username')));
}

function getPasswordHarness() {
    return loader.getHarness(MatInputHarness.with(dataId('password')));
}
```

Let's see how it works in a small gif first before, explaining the solution.

<video muted autoplay controls>
    <source src="/images/refactoring-vim-dataid/refactor-with-vim.mp4" type="video/mp4">
</video>

[Fullscreen](/images/refactoring-vim-dataid/refactor-with-vim.mp4)

The Commands
=====
1. Place your cursor on a line top the first loader word
2. Record macro `qx` (`x` is just one possible macro register, you can use others to)
3. Search for loader `/loader` and jump there (ENTER)
4. Jump to `{` on the same line by typing `f` followed by `{`
5. Enter visual mode `v` and jump to `"` using `f"`
6. Press `s` for substitute (you're in input mode now) type `dataId('`
7. Leave input mode and jump to next `"` with `f"`
8. Enter visual mode and jump to `}` by `vf}`
9. Press `s` (substitute) and enter the text `')`
10. Goto normal mode
11. Stop macro record with `q`
12. Replay macro n-times typing `@x` 
13. Or jump to all occurrence of loader by typing `n` and use `@@` to repeat last macro 
14. Equipped with this, you can go through your files and refactor many occurrences in no time


