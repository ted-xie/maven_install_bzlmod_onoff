# `maven_install` issues with lockfiles and bzlmod on/off

I would like to have a single source of truth for maven install artifacts. I would like the MODULE.bazel `maven.install()` artifact list to be the source of truth.

In this example, I specify the artifact list in MODULE.bazel, generate a lock file, and then in WORKSPACE read that lock file. My expectation is that `bazel build` commands with `--noenable_bzlmod` and `--enable_bzlmod` should work identically.

However, I get a `rules_jvm_external` error when building with bzlmod disabled:

```
$ bazelisk build :dummy --noenable_bzlmod

ERROR: An error occurred during the fetch of repository 'my_maven':
[...]

ERROR: An error occurred during the fetch of repository 'my_maven':
[...]
Error in fail: Cannot calculate input hash without artifacts or boms
```
