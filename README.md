# BTC Alert — PWA

GitHub Pages hosts the installable PWA shell. The dashboard, V1–V10 strategy evaluation, Google Sheets tracking, and Telegram notifications remain in Google Apps Script.

## URLs

- GitHub Pages: https://darwinlorenzana.github.io/btc-alert-app/
- Apps Script web app: https://script.google.com/macros/s/AKfycby9nLHo2IYaJb0bKSB9e3Oqr62OjL308YrAV1mQqVkbyA1-FhIZkq3vxjtmKEi7Tz4/exec

## Publish

1. Upload the contents of this folder to the root of the `btc-alert-app` repository.
2. In GitHub, open **Settings → Pages**.
3. Under **Build and deployment**, select **Deploy from a branch**.
4. Select branch `main` and folder `/(root)`, then save.
5. Wait for GitHub Pages to finish deploying, then open the Pages URL above.

## Apps Script iframe requirement

The GitHub Pages shell embeds the Apps Script web app in an iframe. In the Apps Script `doGet()` function, allow framing by the GitHub Pages origin. If your backend is currently using the default X-Frame-Options setting, change the return statement to include:

```javascript
function doGet() {
  return HtmlService.createHtmlOutputFromFile("Index")
    .setTitle("BTC Alert Control")
    .addMetaTag("viewport", "width=device-width, initial-scale=1, viewport-fit=cover")
    .setXFrameOptionsMode(HtmlService.XFrameOptionsMode.ALLOWALL);
}
```

Then save and **Deploy → Manage deployments → Edit** the existing web app deployment, select a new version, and deploy. Keep access settings appropriate for your account and test the URL directly before embedding it.

**Security note:** `ALLOWALL` permits other sites to frame the web app. Do not expose secrets in the HTML or GitHub repository. Keep Telegram tokens in Apps Script properties and keep paper trading enabled. The frontend iframe does not make the Apps Script backend public beyond the access permissions configured on the deployment.

## Install on Android

1. Open the GitHub Pages URL in Chrome.
2. Open Chrome's menu.
3. Choose **Install app** or **Add to Home screen**.

## Notes

- The service worker caches only the static PWA shell, not the Apps Script dashboard or trading data.
- The shell is not a replacement for `Code.gs` or `V10_EMA_Pullback.gs`.
- No live orders are implemented by this PWA shell.
