## TIL
- `git log` can show evolution of a function by its name using `-L:funcname:filename` format ([docs](https://git-scm.com/docs/git-log#Documentation/git-log.txt--Lltfuncnamegtltfilegt))
- JavaScript `every` method returns `true` for empty arrays because it acts as “for all” quantifier in mathematics. Because elements of an empty set satisfy any condition - a _bit_ counterintuitive, but well. Somehow I find it more intuitive that the `some` method always returns `false` for empty arrays. BTW, in Python there are `all` and `any` functions to implement the same behaviour.
- `sort` command supports `-h` parameter to sort by numeric parameters of the kind produced by `du -h`, which makes it possible to generate a listing of directory content based on the file/folder total size: `du -sh ./* | sort -h` (requires GNU Coreutils, which might be missing on an older  Mac OS and could be installed using `brew`) 
- TypeScript has this weird basic type [`never`](https://www.typescriptlang.org/docs/handbook/basic-types.html#never), which is not that weird if you think about it...
- `npm run` supports `--if-present` flag to avoid exiting with a non-zero exit code when the script is undefined
- There's [CSS Intrinsic & Extrinsic Sizing Module Level 3](https://www.w3.org/TR/css-sizing-3/) draft spec defining such keyword values of the `width`/`height` CSS properties as `min-content`, `max-content`, and `fit-content()`
- There's [preview mode](https://code.visualstudio.com/docs/getstarted/userinterface#_preview-mode) enabled in VS Code by default, but it's possible to disable it for `Quick Open` action with `workbench.editor.enablePreviewFromQuickOpen` property to open new files in new tab
- In some languages (e.g. Java) it is possible to access private members of a class from a different instance of the same class
- there is [`merge.conflictstyle`](https://git-scm.com/docs/merge-config) config option for `git`, that has a nice `zdiff3` value, that is even nicer than `diff3`
