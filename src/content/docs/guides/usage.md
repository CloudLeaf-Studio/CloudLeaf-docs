---
title: Usage
description: Bookmark upload, download, export/import, and preview mode usage guide
---

## Actions

After opening the CloudLeaf popup, you'll see four main action buttons: [`Upload Bookmarks`](#upload-bookmarks), [`Download Bookmarks`](#download-bookmarks), [`Export Bookmarks`](#export-bookmarks), and [`Import Bookmarks`](#import-bookmarks).

![popup](../../../assets/popup.png)

### Upload Bookmarks

Sync bookmarks from the current browser to the cloud.

1. Click `Upload Bookmarks`
2. CloudLeaf reads your local bookmarks and compares them with the cloud
3. If there are no conflicts, the upload completes automatically
4. If the **cloud is newer than local**, a confirmation dialog will ask whether to force overwrite

:::caution
Uploading will **overwrite** the cloud bookmarks.
:::

### Download Bookmarks

Restore bookmarks from the cloud to the current browser.

1. Click `Download Bookmarks`
2. CloudLeaf fetches bookmark data from your configured sync source
3. If **local is newer than cloud**, a confirmation dialog will ask whether to force overwrite
4. After download, the current browser's bookmarks will be replaced with the cloud content

:::caution
Downloading will **replace** all bookmarks in the current browser. You can check the content in [Preview Mode](#preview-mode) first.
:::

### Export Bookmarks

Save current bookmarks as a local JSON file (Chrome and Edge only).

1. Click `Export Bookmarks`
2. The file is saved to the browser's default download location as `CloudLeaf.json`

### Import Bookmarks

Restore bookmarks from a local JSON file (Chrome and Edge only).

1. Click `Import Bookmarks`
2. Select a previously exported JSON file
3. If local data is newer than the file, a confirmation dialog will appear

## Automatic Sync

Automatic sync is initialized only after a successful manual upload. Configure a sync source and complete this upload before enabling the automatic mode.

1. Open the popup and click `Upload Bookmarks` once
2. Open Settings and turn on `Auto Sync`
3. CloudLeaf schedules a sync about 5 seconds after bookmark changes settle
4. A background alarm also checks for changes every 15 minutes

You can use `Trigger Sync` in the settings page to start a check immediately. The status indicator shows whether sync is `Uninitialized`, `Ready`, or in `Conflict`. If the cloud target or its highest-priority source changes, upload manually again to establish a new baseline.

:::caution
Automatic sync does not start until the first manual `Upload Bookmarks` succeeds. When a conflict is detected, automatic sync pauses; resolve it manually by choosing an upload or download action.
:::

## Preview Mode

View your cloud bookmarks at any time without performing an upload or download.

1. Click the eye icon in the top-right corner
2. The side panel expands, displaying the folder tree of your cloud bookmarks
3. Browse the folder structure to see what bookmarks are stored in the cloud

![sidepanel](../../../assets/sidepanel.png)

:::tip
Preview mode is not only for checking content before syncing — you can also open the side panel anytime to use your cloud bookmarks directly.
:::

## Conflict Detection

CloudLeaf compares normalized bookmark content first, then uses the **local bookmark timestamp** and **cloud file timestamp** when the content differs:

- **In sync**: both normalized content hashes match
- **Local is newer**: when downloading if local is newer → prompts whether to force download
- **Cloud is newer**: when uploading if cloud is newer → prompts whether to force overwrite
- **Conflict**: content differs but both timestamps are equal; resolve manually before automatic sync can continue
