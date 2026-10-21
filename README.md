# Bazel + Buildkite Test Engine Example

An example Buildkite pipeline making use of a patched `bktec` and `test-collector-buildkite-plugin` to invoke bazel tests with BKTEC and send the results to BKTE.

## Patches that enable this
- Minor changes to the official `tests` [plugin](https://github.com/buildkite-plugins/test-collector-buildkite-plugin/compare/main...zachgrayio:test-collector-buildkite-plugin:main) to pipe settings through to BKTEC
- Bigger changes to [BKTEC](https://github.com/zachgrayio/test-engine-client/compare/buildkite%3Atest-engine-client%3Amain...main) itself to add the bazel support

## Implementation Details

- The BKTEC binary is a bazel dependency that's built with bazel, and then used to run tests.
- The patched `bktec` binary includes support for parsing Bazel BEP proto files, and the forked plugin reuses `bktec` to process BEP files (without reimplementing proto handling again in the plugin)
