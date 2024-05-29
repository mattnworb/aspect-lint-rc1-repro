# aspect-lint-v1.0.0-rc1 repro

This repo is to reproduce slow times running the `format_multirun` rule from
`rules_lint` v1.0.0-rc1 with a significant amount of Java source code.

**note:** see the `fix-disable_git_attribute_checks` branch for a fix / patch to
upstream

To reproduce, add any project containing a large amount of Java files into the
directory where this repo is cloned, with something like:

```
git subtree add --prefix guava git@github.com:google/guava.git master --squash
```

(I've not committed those files here to keep the repo size small)

and run

```
time run bazel format
```

additionally, note that the script hits an error if you try to pass
`--disable_git_attribute_checks`:

```
time bazel run format -- --disable_git_attribute_checks
...
... com/google/thirdparty/publicsuffix/TrieParser.java guava/refactorings/CharMatcherRewrite.java guava/refactorings/TraverserRewrite.java: File name too long
```

