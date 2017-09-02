# App for Google Drive Publication workflow

## Contents
 * [Assets Storage Subdirectories Structure](#assets-storage-subdirectories-structure)
 * [Developer's Console](#developers-console)
 * [Chrome Web Store](#chrome-web-store)

## Assets Storage Subdirectories Structure
Assets
```text
--- cws                  - assets for Chrome Web Store
 |  |--- app-manifest    - App Manifest Pack
 |  \--- app-promo       - App Promo assets
 |
 \- src                  - assets source
    |--- cws             - for Chrome Web Store
    |    \--- app-promo  - for App Promo
    \--- ico-set         - icon set
```

## Integration and Publication

This section describes settings and workflow required to integrate
the app into google ecosystem and publish it with Chrome Web Store (CWS).

### Definitions

Some bits of information are used at multiple location therefore we
define here "variables" that will be referred to in the following sections.

The particular URLs are specific to this app.

```text
DEV_EMAIL   = oleksiy.rudenko@gmail.com

APP_NAME    = Link Manager for Google Drive
APP_DOMAIN  = https://oleksiyrudenko.github.io
APP_ROOT    = https://oleksiyrudenko.github.io/gd-linkman/

APP_DOC_PP  = APP_ROOT/#!/privacypolicy/
APP_DOC_TOS = APP_ROOT/#!/tos/

APP_DESCR_SHORT =
            Helps managing links to files and native Google documents stored on Google Drive.

APP_DESCR_LONG =
            Native sharing of files from Google Drive offers opening native Google documents or preview mode for other types of files.
            This tool integrates with Google Drive and offers:
             * convert-and-download direct links for native Google documents
             * direct download links for other types of files
            The tool doesn't take files content.

ICO_URL     = APP_ROOT + [dimensions.ext]
              - any image filename with dimensions specified
              - png? - means any image format
              - 120x120max - means max size of 120px x 120px
              Required ico dimensions:
              - web-site : favicon.ico
              - Google Drive UI Integration: png 256px, 128px, 64px, 32px, 16px

```

### Distribution

Make your app available at `APP_ROOT` (app default entry point).

### Developer's Console

Navigate to [Google Dev Console](https://console.developers.google.com/apis/dashboard)
 * Tap Button or Dropdown next to `Google APIs` logo and add a project
 * Complete the form

Go to [Credentials](https://console.developers.google.com/apis/credentials) and:
 * Create OAuth Client ID:
   - Name: `APP_NAME`
   - Authorized JS origins: `APP_DOMAIN`, `https://apis.google.com`
   - Authorized redirect URIs: `APP_ROOT`
 * OAuth Consent Screen:
   - use `DEV_EMAIL`, `APP_NAME`, `APP_ROOT`
   - logo URL: `ICO_URL/120x120max.png?`
 * Domain verification
   - [Verify domain](https://support.google.com/webmasters/answer/35179?hl=en)
     the app hosted at
   - Add verified domain `APP_DOMAIN`

Go to [Library](https://console.developers.google.com/apis/library)
 * Enable APIs `Google Drive API` (v2 at least) and `Google Apps Marketplace SDK`
   (check sections below for details)

Go to [Dashboard/Google Drive API/Drive UI Integration](https://console.developers.google.com/apis/api/drive.googleapis.com/drive_sdk)
 * Use `APP_NAME`, `APP_DESCR_SHORT`, `APP_DESCR_LONG`
 * Upload Application icons: 256px, 128px, 64px, 32px, 16px
 * Upload Document icons (optional): 256px, 128px, 64px, 32px, 16px
 * 


### Chrome Web Store
