# FOX-PIN-DEPS - what the Playwright fork is built from (WINGSCRUM-639, decision 1, 26 Nov 2026)

Our own file. No upstream file is edited. Build output (lib/, dist/, node_modules/) is ignored by their .gitignore.

## The pins
| what | pinned to |
|---|---|
| upstream source | microsoft/playwright `81f9852` (v1.66.0-next), branch `fox/provenance` |
| Node | v24.22.0 (fnm, `/Users/clawdbot/.fnm/node-versions/v24.22.0`) - their floor is >=20 |
| npm | 11.19.1 (ships with that Node) |
| registry | https://registry.npmjs.org/ only |
| lockfile | `package-lock.json` v3, sha256 `289491570e78577e94789444b0ee9e27016a40c1c86dd1fa4775152a6c8d8400` |
| outside packages | 671, every one resolved from registry.npmjs.org with an sha512 integrity hash; 0 git or URL deps |
| browsers | NONE downloaded. `PLAYWRIGHT_SKIP_BROWSER_DOWNLOAD=1`, install scripts off, build with `--disable-install`. It drives his installed Chrome. |

## The build, exactly
```
export PLAYWRIGHT_SKIP_BROWSER_DOWNLOAD=1 npm_config_registry=https://registry.npmjs.org/
npm ci --ignore-scripts                # installs exactly the lockfile; fails if package.json disagrees
node node_modules/esbuild/install.js   # the ONE install script we run: checks the locked esbuild binary
node utils/build/build.js --disable-install
```
Install scripts in the lockfile and what we do with them: `esbuild` RUN (binary check), `fsevents` SKIPPED, `packages/playwright-browser-chromium` SKIPPED, `packages/playwright-browser-firefox` SKIPPED, `packages/playwright-browser-webkit` SKIPPED, `packages/playwright-chromium` SKIPPED, `packages/playwright-firefox` SKIPPED, `packages/playwright-webkit` SKIPPED.

## Direct build dependencies (root package.json), with the locked version
| package | asks for | locked |
|---|---|---|
| @actions/core | 3.0.1 | 3.0.1 |
| @actions/github | 9.1.1 | 9.1.1 |
| @babel/core | 7.29.7 | 7.29.7 |
| @babel/helper-plugin-utils | 7.29.7 | 7.29.7 |
| @babel/parser | 7.29.7 | 7.29.7 |
| @babel/plugin-proposal-decorators | 7.29.7 | 7.29.7 |
| @babel/plugin-syntax-async-generators | 7.8.4 | 7.8.4 |
| @babel/plugin-syntax-import-attributes | 7.29.7 | 7.29.7 |
| @babel/plugin-syntax-json-strings | 7.8.3 | 7.8.3 |
| @babel/plugin-syntax-object-rest-spread | 7.8.3 | 7.8.3 |
| @babel/plugin-syntax-optional-catch-binding | 7.8.3 | 7.8.3 |
| @babel/plugin-transform-class-properties | 7.29.7 | 7.29.7 |
| @babel/plugin-transform-class-static-block | 7.29.7 | 7.29.7 |
| @babel/plugin-transform-explicit-resource-management | 7.29.7 | 7.29.7 |
| @babel/plugin-transform-export-namespace-from | 7.29.7 | 7.29.7 |
| @babel/plugin-transform-logical-assignment-operators | 7.29.7 | 7.29.7 |
| @babel/plugin-transform-modules-commonjs | 7.29.7 | 7.29.7 |
| @babel/plugin-transform-nullish-coalescing-operator | 7.29.7 | 7.29.7 |
| @babel/plugin-transform-numeric-separator | 7.29.7 | 7.29.7 |
| @babel/plugin-transform-optional-chaining | 7.29.7 | 7.29.7 |
| @babel/plugin-transform-private-methods | 7.29.7 | 7.29.7 |
| @babel/plugin-transform-private-property-in-object | 7.29.7 | 7.29.7 |
| @babel/plugin-transform-react-jsx | 7.29.7 | 7.29.7 |
| @babel/preset-typescript | 7.29.7 | 7.29.7 |
| @duckdb/node-api | 1.5.4-r.1 | 1.5.4-r.1 |
| @eslint/compat | 2.1.0 | 2.1.0 |
| @eslint/eslintrc | 3.3.5 | 3.3.5 |
| @eslint/js | 9.39.4 | 9.39.4 |
| @jest/expect-utils | 30.4.1 | 30.4.1 |
| @modelcontextprotocol/sdk | 1.32.0 | 1.32.0 |
| @stylistic/eslint-plugin | 5.10.0 | 5.10.0 |
| @types/babel__core | 7.20.5 | 7.20.5 |
| @types/babel__helper-plugin-utils | 7.10.3 | 7.10.3 |
| @types/babel__traverse | 7.28.0 | 7.28.0 |
| @types/chrome | 0.2.0 | 0.2.0 |
| @types/codemirror | 5.60.17 | 5.60.17 |
| @types/debug | 4.1.13 | 4.1.13 |
| @types/diff | 7.0.2 | 7.0.2 |
| @types/formidable | 2.0.6 | 2.0.6 |
| @types/ini | 4.1.1 | 4.1.1 |
| @types/istanbul-lib-instrument | 1.7.8 | 1.7.8 |
| @types/node | 20.19.43 | 20.19.43 |
| @types/pngjs | 6.0.5 | 6.0.5 |
| @types/progress | 2.0.7 | 2.0.7 |
| @types/proxy-from-env | 1.0.4 | 1.0.4 |
| @types/react | 19.2.17 | 19.2.17 |
| @types/react-dom | 19.2.3 | 19.2.3 |
| @types/retry | 0.12.5 | 0.12.5 |
| @types/source-map-support | 0.5.10 | 0.5.10 |
| @types/ws | 8.18.1 | 8.18.1 |
| @types/xml2js | 0.4.14 | 0.4.14 |
| @types/yauzl | 3.4.0 | 3.4.0 |
| @types/yazl | 3.3.1 | 3.3.1 |
| @typescript-eslint/eslint-plugin | 8.62.0 | 8.62.0 |
| @typescript-eslint/parser | 8.62.0 | 8.62.0 |
| @typescript-eslint/utils | 8.62.0 | 8.62.0 |
| @vitejs/plugin-basic-ssl | 2.3.0 | 2.3.0 |
| @vitejs/plugin-react | 6.0.3 | 6.0.3 |
| @zip.js/zip.js | 2.7.73 | 2.7.73 |
| chokidar | 4.0.3 | 4.0.3 |
| chromium-bidi | 159.0.8154-9 | 159.0.8154-9 |
| colors | 1.4.0 | 1.4.0 |
| commander | 15.0.0 | 15.0.0 |
| cross-env | 10.1.0 | 10.1.0 |
| debug | 4.4.3 | 4.4.3 |
| diff | 9.0.0 | 9.0.0 |
| dotenv | 17.4.2 | 17.4.2 |
| electron | 42.11.16 | 42.11.16 |
| enquirer | 2.4.1 | 2.4.1 |
| esbuild | 0.28.1 | 0.28.1 |
| eslint | 9.39.4 | 9.39.4 |
| eslint-plugin-import | 2.32.0 | 2.32.0 |
| eslint-plugin-notice | 1.0.0 | 1.0.0 |
| eslint-plugin-react | 7.37.5 | 7.37.5 |
| eslint-plugin-react-hooks | 5.2.0 | 5.2.0 |
| formidable | 2.1.5 | 2.1.5 |
| get-east-asian-width | 1.6.0 | 1.6.0 |
| get-stream | 9.0.1 | 9.0.1 |
| graceful-fs | 4.2.11 | 4.2.11 |
| https-proxy-agent | 9.1.0 | 9.1.0 |
| ini | 7.0.0 | 7.0.0 |
| istanbul-lib-instrument | 6.0.3 | 6.0.3 |
| jest-matcher-utils | 30.4.1 | 30.4.1 |
| jest-message-util | 30.4.1 | 30.4.1 |
| jpeg-js | 0.4.4 | 0.4.4 |
| json5 | 2.2.3 | 2.2.3 |
| mime | 4.1.0 | 4.1.0 |
| minimatch | 10.2.5 | 10.2.5 |
| open | 11.0.0 | 11.0.0 |
| pngjs | 7.0.0 | 7.0.0 |
| progress | 2.0.3 | 2.0.3 |
| proxy-from-env | 2.1.0 | 2.1.0 |
| react | 19.2.7 | 19.2.7 |
| react-dom | 19.2.7 | 19.2.7 |
| retry | 0.13.1 | 0.13.1 |
| signal-exit | 4.1.0 | 4.1.0 |
| socks-proxy-agent | 10.1.0 | 10.1.0 |
| source-map-support | 0.5.21 | 0.5.21 |
| ssim.js | 3.5.0 | 3.5.0 |
| typescript | 6.0.3 | 6.0.3 |
| vite | 8.1.6 | 8.1.6 |
| vite-plugin-static-copy | 3.4.0 | 3.4.0 |
| ws | 8.21.0 | 8.21.0 |
| xml2js | 0.6.2 | 0.6.2 |
| yaml | 2.9.0 | 2.9.0 |
| yauzl | 3.4.0 | 3.4.0 |
| yazl | 3.3.1 | 3.3.1 |
| zod | 4.6.7 | 4.6.7 |
| zod-to-json-schema | 3.25.2 | 3.25.2 |

## Dependencies of the workspace packages (outside ones only), with the locked version
| package | locked | used by |
|---|---|---|
| @browser-logos/chrome | 2.0.0 | dashboard |
| @browser-logos/chrome-beta | 3.0.0 | dashboard |
| @browser-logos/chrome-canary | 2.0.0 | dashboard |
| @browser-logos/chrome-dev | 3.0.0 | dashboard |
| @browser-logos/chromium | 2.0.1 | dashboard |
| @browser-logos/edge | 2.0.7 | dashboard |
| @browser-logos/firefox | 3.0.10 | dashboard |
| @browser-logos/firefox-beta | 4.1.4 | dashboard |
| @browser-logos/firefox-nightly | 3.0.6 | dashboard |
| @browser-logos/safari | 2.1.0 | dashboard |
| @xterm/addon-fit | 0.10.0 | web |
| @xterm/xterm | 5.5.0 | web |
| codemirror | 5.65.18 | web |
| yaml | 2.9.0 | recorder, trace-viewer, web |

The other 549 entries are transitive and pinned the same way: exact version plus integrity in the lockfile.

## Check
`docs/spike/639/playwright-check.mjs` in ~/fox: pin is an ancestor, only FOX-*.md differ, tree clean, every installed package matches its locked version and hash, no browser downloaded, core loads, extension built, a by-name click in Chrome on a throwaway profile.

## Moving the pin (standing rule, 26 Nov)
Every now and then: fetch upstream, map the upstream diff (Graphify now; Understand Anything when run), decide, move the pin, rerun the build and the check, update this file.

## Proved after the independent check (26 Nov 07:05)
- **Offline build:** `npm ci --ignore-scripts --offline --userconfig=/dev/null` and the build with `npm_config_offline=true` both pass. Nothing comes from outside the lockfile, and his `~/.npmrc` has no say.
- **esbuild:** the platform binary `@esbuild/darwin-arm64` is 0.28.1, from the lockfile; its install check downloads nothing.
- **Node:** the binary in use (sha256 `b468fb9c67427c9d3aec07ee1105e63020923a631a9a2a00beb71a7ba3768bfd`) is byte-identical to the one in the official `node-v24.22.0-darwin-arm64.tar.gz`, whose sha256 `6a9724d9...26d5` matches nodejs.org's SHASUMS256.txt.
- **fsevents:** install script skipped; its prebuilt `fsevents.node` sha256 `40f2f51199e4f5fc46fa6b985fb3461bb63e6cd86c62bfa9bcee45ed4438d5fb`.
- **Build outputs:** hashed per folder in `FOX-BUILD-HASHES.md`; the check compares them, instead of comparing npm's own copy of the lockfile to the lockfile.

## Named exception: Chrome
Playwright drives HIS everyday Chrome through the extension - that is the point. Chrome updates itself and is not pinned. Version on 26 Nov: **Google Chrome 158.0.8127.37**. The check prints the version each run, so a change is seen.

## The extension
- Built to `packages/extension/dist` (Playwright Extension 0.6.0). Its manifest carries the store key, so loaded unpacked it gets the store ID `mmlmfjhmonkocbjadbfplnigmagldckm`; Playwright's connect step relies on that ID.
- No `update_url` in the manifest: it never updates itself from the store.
- The store copy must NOT also be installed (same ID). Checked 26 Nov: not installed in any of his Chrome profiles.
