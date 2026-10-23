# Security update: 2026-10-23

Node.js 22.23.4 is selected in `.nvmrc` and `engines.node`. This includes the October 21 security patches. Application source behavior is unchanged except for required build integration configuration.

Source: [Node.js October security releases](https://nodejs.org/en/blog/vulnerability/october-2026-security-releases).

## Verification and limitations

Updated proxy tests: 98 pass and 15 fail. Baseline tests under patched Node: 45 pass and 8 fail. Legacy proxy tests require further compatibility review. Baseline dependencies already fail under patched Node; updated dependencies change failure patterns. This PR must remain a draft until proxy behavior is verified. Coveralls uses maintained @cypress/request through a targeted override to remove critical request/form-data findings.

Native npm audit: 0 critical, 2 high, 8 moderate, 1 low findings. Counts represent affected dependency packages, not unique CVEs.

Remaining findings are deferred to a separate compatibility/reachability review by 2026-10-30. High findings are not claimed fixed or harmless. Many are inherited from braces/micromatch, test tooling, development servers, or discontinued packages; runtime exposure must be assessed before release.

| Package | Severity | Remediation status | Advisory |
| --- | --- | --- | --- |
| `serialize-javascript` | high | Requires declared-range/major change | [Serialize JavaScript is Vulnerable to RCE via RegExp.flags and Date.prototype.toISOString()](https://github.com/advisories/GHSA-5c6j-r48x-rmvq); [Serialize JavaScript has CPU Exhaustion Denial of Service via crafted array-like objects](https://github.com/advisories/GHSA-qj8w-gfj5-8c6v) |
| `shelljs` | high | Requires declared-range/major change | [Improper Privilege Management in shelljs](https://github.com/advisories/GHSA-64g7-mvw6-v9qj); [Improper Privilege Management in shelljs](https://github.com/advisories/GHSA-4rq4-32rv-6wp6) |

## Verification scenario

Use the pinned Node version. Install from the authoritative lockfile with dependency scripts disabled first, review native/postinstall scripts, and run only those required by the package. Run the documented test/build commands. Repeat the native audit before release. In a preview, exercise the package's normal entry point and check browser/server errors. A successful build does not prove production integration.
