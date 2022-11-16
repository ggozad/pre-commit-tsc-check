# Pre-commit hook for typescript type checking

This is a hook for [pre-commit](https://github.com/pre-commit/pre-commit) checking that the typescript compiler can process with no errors a file.

### Usage

- To use this you first need to install pre-commit.
- Then create a pre-commit config file in the root of your project.
- Run `pre-commit install` from the root of your project

Finally add this to your `.pre-commit-config.yaml`:

```yaml
- repo: git://github.com/ggozad/tsc-check
  rev: "" # Use the sha or tag you want to point at
  hooks:
    - id: tsc-check
```

Now everytime you commit a ts file `tsc` will run on the file.

By default, the `--noEmit` options is passed as argument. You can customize arguments that you pass to `tsc` by adding a `args` key to the hook configuration. For example if you want to run `tsc` on some other folder where your `tsconfig.json` is located you can do:

```yaml
- repo: git://github.com/ggozad/tsc-check
  rev: "" # Use the sha or tag you want to point at
  hooks:
    - id: tsc-check
      args: [--noEmit, -p, haiku-bots/tsconfig.json]
      pass_filenames: false
```

Note how we set `pass_filenames` to `false` since we cannot pass individual files *and* set `tsconfig.json`.
