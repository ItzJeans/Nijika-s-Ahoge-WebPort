# Nijika's Ahoge — web-port package

A browser-port asset package for **Nijika's Ahoge**, prepared from the original Construct 3 HTML5 export ZIP supplied for this project. This package serves the original game runtime and assets; it does not recreate the game or substitute a demo.

## Original game and credits

The source game is the itch.io title **Nijika, whose ahoge can grow infinitely**. The original game interaction is to grab and drag Nijika's ahoge, with its original character interactions preserved.

Original game page: <https://tamanidamani.itch.io/nijikas-ahoge>

Credits listed on the original game page:

- Programmer: **塔打** (TamaniDamani)
- Artist: **ナコ** (nako775_)


## Package and CDN

- npm package: `nijikas-ahoge-assets-itzjeans`
- Asset version: `1.0.0`
- jsDelivr root: `https://cdn.jsdelivr.net/npm/nijikas-ahoge-assets-itzjeans@1.0.0/`
- Construct runtime folder: `https://cdn.jsdelivr.net/npm/nijikas-ahoge-assets-itzjeans@1.0.0/html-classic.itch.zone/html/7171745/`

The standalone launcher is pinned to this exact package version. It does not use `@latest`, GitHub Pages, or a local game-assets folder.

## How this port works

The game is a **Construct 3 HTML5 export**. Its source archive contains the Construct runtime (`scripts/c3runtime.js`), bootstrap (`scripts/main.js`), project data (`data.json`), image atlases, media files, WebAssembly binaries, and runtime worker scripts.

The source archive's `index.html` is empty (0 bytes), so there was no usable page bootstrap to reuse. The standalone launcher supplies the HTML page and starts the original Construct runtime. It loads `scripts/supportcheck.js`, sets a pinned jsDelivr runtime base URL, then loads `scripts/offlineclient.js` and `scripts/main.js` in the game's required startup order.

The only game-source code change is in `scripts/main.js`: the Construct `RuntimeInterface` initialization now receives `runtimeBaseUrl: window.C3_CDN_BASE_URL`. This lets Construct resolve the original data, images, media, worker scripts, engine scripts, and WASM relative to the npm/jsDelivr package. The original game folder hierarchy and filenames are retained.

The original `scripts/register-sw.js` file is retained but not loaded because it registers `sw.js`, which is not included in the uploaded source ZIP. `static.itch.io/htmlgame.js` is also retained, but its itch.io hotlink callback is not loaded by the standalone launcher.

## Launcher controls

The launcher uses the exact two PNG controls from the provided Heaven For Death reference ZIP, copied byte-for-byte into `launcher-ui/`:

- `launcher-ui/btn_github.png` — opens <https://github.com/ItzJeans> in a new tab.
- `launcher-ui/btn_fullscreen.png` — toggles fullscreen using the supplied `toggleFullScreen()` implementation, including standard and WebKit fullscreen methods and the conditional graphics refresh.

Their positions and hover effects follow the supplied reference. Both controls are separate from the game canvas and remain visible above it.

## How to publish and play

1. Extract the modified asset ZIP.
2. Open the extracted `nijikas-ahoge-assets-itzjeans` folder.
3. Double-click `PUBLISH_TO_NPM.bat` and follow npm's browser login / account verification steps if prompted.
4. The script checks the exact package version before publishing, runs `npm pack --dry-run`, checks the publish exit code, verifies the published version afterwards, and (when Windows `curl` is available) checks key resource URLs through jsDelivr. It stops if the version already exists or if npm cannot confirm it is unused.
5. After the package is successfully published, open `nijikas-ahoge.html` in a modern desktop browser.

Do not share npm passwords, one-time codes, recovery codes, or authentication tokens in chat. Enter any required authentication only in the official npm/browser flow.

## Browser requirements and controls

Use an up-to-date desktop browser with JavaScript modules, WebAssembly, WebGL, Web Workers, and `OffscreenCanvas` support. Chrome or Edge is recommended. The source game primarily uses mouse interaction; no touch controls or substitute controls have been added.

Use the mouse to grab and drag Nijika's ahoge. Original in-game interactions remain as implemented by the source project.

## Language and included assets

The source archive provides one Construct project data file (`data.json`) and no separate language packs or language-selection configuration. This port does not add an invented language selector. No separate font files or plugin packages were present in the supplied ZIP; bundled runtime dependencies and WASM files are kept.

## Troubleshooting

- **Launcher shows a loading error:** confirm the package has been published publicly and that `nijikas-ahoge-assets-itzjeans@1.0.0` is available through jsDelivr.
- **A file returns 404:** check exact path spelling, capitalization, extension, package name, and version. Do not replace the version with `@latest`.
- **WebGL is reported as missing:** update the browser and graphics drivers, enable hardware acceleration, and retry in a current Chrome/Edge desktop session.
- **Worker or WASM errors:** use HTTPS or a current browser with worker modules and WebAssembly enabled; inspect the browser console for the first failed request.
- **npm says the version already exists:** do not republish it. Increment the package version and update the launcher CDN version together.
- **Publishing is blocked:** the batch script reports npm authentication, registry, packing, publishing, and post-publish verification failures separately. It never reports success unless npm confirms the exact version.

## ItzJeans links

- Games website: <https://sites.google.com/view/danielsgxmes/games>
- GitHub: <https://github.com/ItzJeans>

## Fan-work and copyright notice

This browser port does not change the ownership of the original game, artwork, character designs, audio, or other intellectual property. The source game is a fan work involving material associated with *Bocchi the Rock!*; no affiliation with or endorsement by the franchise's rights holders is implied. The permission confirmation supplied for this port is not a transfer of ownership or a license to unrelated third-party material.
