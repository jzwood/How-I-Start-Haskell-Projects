# How to Start Haskell Project

## Prerequisites
- stack
    * `stack --version`


## New Project

    stack new my-new-project

This will create the following project structure
```
.
└── my-new-project
    ├── ChangeLog.md
    ├── LICENSE
    ├── README.md
    ├── Setup.hs
    ├── app
    │   └── Main.hs
    ├── my-new-project.cabal
    ├── package.yaml
    ├── src
    │   └── Lib.hs
    ├── stack.yaml
    └── test
        └── Spec.hs
```

## Replace Prelude

Pick a Prelude replacement from the [Aelve Guide](https://guide.aelve.com/haskell/alternative-preludes-zr69k1hc)

### Update Dependencies

If we picked **protolude** then we would open `package.yaml` and add `- protolude == 0.3.0` to dependencies list so it looks like:

    dependencies:
    - base >= 4.7 && < 5
    - protolude == 0.3.0

Any dependencies you want to add from (Hackage)[https://hackage.haskell.org/] should be added here.

### Build Executable

To install dependencies and build package(s)

    stack install

If you look in `my-new-project.cabal` you'll see that `protolude` is one of the build depends in library, executable, and test-suite. Note: this is a stack generated file so do not edit it directly, it will get overwritten.

### Disable Default Prelude

Above `dependencies:` in **package.yaml** add

     default-extensions: NoImplicitPrelude

If you run `stack install` or `stack build` now you'll get an error, `IO not in scope`.

add `import Protolude` to `Main.hs` and any Lib files it's using. You can now run `stack build` then run

    stack exec my-new-project-exe

or you can run `stack install` then

    my-new-project-exe
