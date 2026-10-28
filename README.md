# Team Signal: Capacitor app starter

A small interactive web app wrapped with Capacitor for Android. Use **Use this
template** to create your team's own repository; change the app ID in
`capacitor.config.json` and Android project before releasing your own app. A
button and counter are deliberately small enough to trace and change.

## Run and change

Install Node 24, then from the repository root:

```bash
npm ci
npm test
npm run build
```

Open `www/index.html` using a local web server, e.g. `npx serve www`, and click
**Send signal**. Change `src/logic.js` or the interface; rerun the checks. A
teammate can branch, commit, push and open a PR with a description and test
instructions. Actions uploads the `web` folder and an Android **debug APK**;
download an artifact from the run and test it. The APK is not a signed store
release.

## Codex cloud environment

Connect GitHub, create a new task and choose **Work in → Cloud → Select
environment → Create environment**, then choose your new repository. Ask Codex
to run `.codex/setup.sh` with Node 24; review setup output and changes, save and
**Publish**. Start a new task: “Change the message after a second tap and run
the tests.” Review its diff, run the app, and ask a teammate to review the PR.
The setup script configures the coding workspace. GitHub Actions uses separate
fresh runners. See [Codex environments](https://learn.chatgpt.com/docs/environments/cloud-environments).

## Android and iOS

For Android install JDK 21 and Android SDK, set `ANDROID_HOME`, then:

```bash
npm run android:sync
cd android && ./gradlew assembleDebug
```

The APK is in `android/app/build/outputs/apk/debug/`. GitHub Actions prepares
its own Android runner and uploads it without store credentials. A Play release
needs its own signing and store setup. iOS requires a Mac, Xcode, an Apple
developer account for distribution and a separately added iOS platform; see
[Capacitor environment setup](https://capacitorjs.com/docs/getting-started/environment-setup).
Electron desktop packaging is a separate wrapper; see
[Tetrilaunch's desktop workflow](https://github.com/venetanji/tetrilaunch/blob/main/.github/workflows/desktop.yml).

## Optional: deploy the web build

Create a Cloudflare account and a scoped Workers deployment API token. Under
GitHub **Settings → Secrets and variables → Actions**, add repository secrets
`CLOUDFLARE_API_TOKEN` and `CLOUDFLARE_ACCOUNT_ID`, and a repository variable
`CLOUDFLARE_WORKER_NAME` with your unique Worker name. Create a GitHub
`production` environment if using environment protection. Run **Deploy web
(manual)** in Actions, then open the Worker URL in the log. No deployment runs
on pull requests. The Cloudflare account may have usage limits or costs.
Do not put real secrets in source, screenshots, prompts, or the browser bundle:
anything shipped to the client is visible to users. Other providers have their
own destination, tokens and commands.
