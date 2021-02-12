# Modern CMake Buildsystem

This action portably builds, tests, and optionally installs
a modern CMake project.

It is based on [these commands](
https://gist.github.com/johelegp/65cbb2ffdb815c8ebce22ae847ab76b1
"How to portably build, test and install modern CMake projects").

It has no required input arguments.
It has no output arguments.
It uses no secrets.

It doesn't directly use environment variables,
though it may do so indirectly through the CMake commands.

## Optional inputs arguments

- `path-to-source`
  + Description: The top-level directory containing source files provided by the project.
  + Default: `"${{ github.workspace }}"`
- `path-to-build`
  + Description: The top-level directory in which buildsystem files and build output artifacts are to be stored.
  + Default: `"${{ github.workspace }}/build"`
- `generate-options`
  + Description: Options to generate a project buildsystem other than `-S` and `-B`.
- `build-options`
  + Description: Options to build a project other than `--build`.
- `test-options`
  + Description: Options to test a project.
- `install`
  + Description: Set to `true` to install the project. Requires CMake 3.15.
- `install-options`
  + Description: Options to install a project other than `--install`.

## Example

```yml
on: push
jobs:
  gcc-snapshot:
    runs-on: ubuntu-latest
    steps:
      - uses: johelegp/gcc-snapshot@v1
      - uses: actions/checkout@v2
      - uses: johelegp/modern-cmake-buildsystem@v1 # This action.
        with:
          generate-options: "--preset=test"
```
