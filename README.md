# Bazel Test Engine Example

An example Buildkite pipeline making use of a patched `bktec` and `test-collector-buildkite-plugin` to invoke bazel tests with BKTEC and send the results to BKTE.

## Implementation Details

- The BKTEC binary is a bazel dependency that's built with bazel, and then used to run tests.
- The patched `bktec` binary includes support for parsing Bazel BEP proto files, and the forked plugin reuses `bktec` to process BEP files (without reimplementing proto handling again in the plugin)

