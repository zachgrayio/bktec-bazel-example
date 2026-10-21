# Bazel + Buildkite Test Engine Example

An example Buildkite pipeline making use of a patched `bktec` and `test-collector-buildkite-plugin` to invoke bazel tests with BKTEC and send the results to BKTE.

## Patches that enable this
- Minor changes to the official `tests` [plugin](https://github.com/buildkite-plugins/test-collector-buildkite-plugin/compare/main...zachgrayio:test-collector-buildkite-plugin:main) to pipe settings through to BKTEC
- Bigger changes to [BKTEC](https://github.com/zachgrayio/test-engine-client/compare/buildkite%3Atest-engine-client%3Amain...main) itself to add the bazel support

## Implementation Details

- The BKTEC binary is a bazel dependency that's built with bazel, and then used to run tests.
- BKTEC handles the upload to BKTE itself now; since the `tests` plugin relies on this functionality, this works seamlessly
    - note that implementing this in the other [test collector plugin](https://github.com/buildkite-plugins/test-collector-buildkite-plugin) would require reusing the BEP and test xml parsing in `bktec`, but that's possible in theory, and I proved that out [here](https://github.com/buildkite-plugins/test-collector-buildkite-plugin/compare/main...zachgrayio:test-collector-buildkite-plugin:main) but against an older version of the `bktec` fork, and that standalone processing subcommand is now removed.
