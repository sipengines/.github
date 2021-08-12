---
name: New releases check-list
about: Checklist for the Release Captain who is responsible for the next release
title: 'Release: x.x.x • MM/DD/YYYY'
labels: ''
assignees: ''

---

<!--- Please add the release version number and release date (not today's date in the title above and fill in details below) -->

This release includes the following surfaces:

- [ ] Android
- [ ] iOS
- [ ] Web

Version: <add_semantic_version_here>

---

###### Release process:

**Note:** if you are releasing both mobile and web you should only release web once the mobile version is **marked as complete** on shipit. The mobile release [updates the version](https://github.com/Shopify/inbox-client/blob/main/android/app/support/version), which will save you some work in the web release.

## Cut the release - Thursday Afternoon

1. Head to shipit-mobile for both mobile apps
   - [Android](https://shipit-mobile.shopifycloud.com/projects/73)
   - [iOS](https://shipit-mobile.shopifycloud.com/projects/74)
2. Click `Store Releases` (top row on left menu)
3. Click `New release` at the top of the list
4. Update the version number, if needed, under the `Regular release` section
5. Find the latest main branch you want to use for this release from the list (you may need to wait for CI to pass if its a recent commit)
6. Click the `Start release` button on the right. This will display an confirmation alert; click `Ok`
   - This will create the release and run CI again
7. After CI successfully passes, click the `Upload` button under the `Rollouts` section.
   - For iOS - click the button beside `App Store`. This will upload the build to app store connect
   - For Android - click the button beside `Google Play Store`. This will upload the build to the play console

- [ ] Release has been cut

Feel free to mention in #messaging-merchant-experiences-devs that the release has been cut

## Test the release candidate - Friday Morning (with next ATC)

When testing the release candidate, it is important to test new features from the [RELEASE NOTES](https://github.com/Shopify/inbox-client/wiki/Release-notes) as well as critical paths from the [tophat checklist](https://github.com/Shopify/inbox-client/blob/main/docs/TOPHAT_CHECKLIST.md) to ensure that the app is functioning properly.

**iOS**

1. Install `Shopify Inbox` from the App Store and log in to the app.
2. Install the `Testflight` build for the new release over the one from the App Store and ensure that the app does not crash on launch. This is testing regressions.
3. Test the app as indicated at the top of this section.

**Android**

1. Visit [shipit-mobile releases](https://shipit-mobile.shopifycloud.com/projects/73) to find the last release. Install the last version's APK onto your android device and log in to the app.
2. Go to the new release and download that APK and then install the new release's APK over the last one and ensure that the app does not crash on launch. This is testing regressions.
3. Test the app as indicated at the top of this section.

**Web**

1. Pull the branch for either the `Android` or the `iOS` release.
2. Build Inbox Web locally from this branch: `dev s`.
3. Test the app as indicated at the top of this section.

- [ ] Release candidate has been tested on all platforms and is ready for release

Feel free to mention in #messaging-merchant-experiences-devs that the release has been tested

NOTE: If a release-blocking issue has been discovered during this testing process, make sure to fix the issue before releasing. If the issue cannot be fixed we may have to delay or skip the release. If this is the case, make sure to communicate the issue with stakeholders (@runmad, @billdevine, etc.).

## Prepare the mobile release - Friday Afternoon

**iOS**

1. Login to [app store connect](https://appstoreconnect.apple.com/login) to start preparing the store release. If you don't have an account/permissions ask someone on the team with admin rights to [invite](https://appstoreconnect.apple.com/access/users) you (`@runmad`, `@jjjeeerrr111`, `@rkstar`)
   - NOTE: If any of the below steps are greyed-out, you may be missing some permissions
2. After logging in click [My Apps](https://appstoreconnect.apple.com/apps)
3. Find [Shopify Inbox](https://appstoreconnect.apple.com/apps/1301681854/appstore/ios/version/deliverable) in the apps list
4. Click the `+` symbol in the menu bar on the left hand side under the `iOS App` section
5. Make sure to enter the exact version number you created in `Shipit mobile` in the `New Version` popup
6. Scroll down to the `Phased Release for Automatic Updates` section and make sure the `using phased release` option is checked
7. Under the `Version Release` section select the `Automatically release this version after the App Review, no earlier than` option and enter next Mondays date at 9am
8. Check with `@billdevine`/`@jawsmartin` on slack to see if there should be any updates to the `Release notes`
9. If there are updates, paste the new notes in the `What's new in this version` section at the top of the page. If there aren't, copy the previous releases notes
10. Update any necessary metadata for this release. This includes things like screenshots, app description, etc
11. Under the `Build` section, add the build that was uploaded in the **Cut the release** step
12. Click `Save` then `Submit for review`

- [ ] iOS Release has been submitted for review

**Android**

1. Open [google play console](https://play.google.com/console/u/0/developers/8929232438554100687/app-list) to start preparing the store release. If you don't have an account/permissions ask someone on the team with admin rights to [invite](https://play.google.com/console/u/0/developers/8929232438554100687/users-and-permissions/invite) you (`@runmad`, `@jjjeeerrr111`, `@rkstar`)
2. From the app list in the google play console click on [Shopify Inbox](https://play.google.com/console/u/0/developers/8929232438554100687/app/4972610005982956193/app-dashboard?timespan=thirtyDays)
3. On the left hand side menu, find and click on `Releases overview`
4. Click on ['Release dashboard'](https://play.google.com/console/u/0/developers/8929232438554100687/app/4972610005982956193/tracks/production?tab=releaseDashboard) under the `Production` section
5. On the top right, click the `Create new release` button
6. Scroll down to the `Release details` section and update the `Release name` to the version you created in Shipit-mobile (from the **Cut the release** step)
7. Check with `@billdevine`/`@jawsmartin` on slack to see if there should be any updates to the `Release notes`
8. If there are updates, paste the new notes in the `Release notes` section. If there aren't, click the `Copy from a previous release` button and select the notes from the previous release
9. Update any necessary metadata for this release. This includes things like screenshots, app description, etc.
10. Under the `App bundles and APKs` click the `Add from library` button
11. Find the version that was uploaded in the **Cut the release** step, check the box on the left, and click the `Add to release` button
12. Click the `Save` button at the bottom right of the page

- [ ] Android release has been submitted for review

Feel free to mention in #messaging-merchant-experiences-devs that the release has been prepared

## Release the new version - Monday Morning

**iOS**

The new iOS version should be released automatically after App Review on Monday, based on **step 7** from the **Prepare the mobile release** step.

**Android**

1. The release is now ready to be reviewed. If this release is being prepared on a Friday, do not submit for review until Monday morning since it will go live immediately after approval.
2. When you are ready to submit for review, click the `Review release` button on the bottom right
3. Scroll all the way down to the `Staged roll-out` section and make sure that the `Roll-out percentage` is set to 7.5%
4. The Release Captain will need to come back and increase the rollout percentage 7.5% Monday, 30% Tuesday, 100% Wednesday
5. Click the `Start rollout to Production`, this will submit the app for review.
6. Once the app is approved it will be available on the Google play store.

**After releasing both mobile apps**

1. Head back to the shipit-mobile releases for both platforms and click `Complete release` at the top. This will create a release [here](https://github.com/Shopify/inbox-client/releases)
2. Grab our [release notes](https://github.com/Shopify/inbox-client/wiki/Release-notes) for this version and include them in the newly created releases from the previous step. (if you need an example of this just look at older releases)

- [ ] mobile app has been released

**Web**

1. In the `inbox-client` repo run `dev latest-release` - this will switch to the tag of the latest inbox-client release, ensuring mobile and web stay in sync, and allowing devs to continue merging changes to `main`
2. `dev deploy` - this will automatically create a PR and open your browser
3. Submit the PR and wait for CI to pass
4. Comment `/shipit` on the PR to complete the process

- [ ] web app has been released

Feel free to mention in #messaging-merchant-experiences-devs that the new version has been released
