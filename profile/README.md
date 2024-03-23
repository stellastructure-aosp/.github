# Stellastructure's AOSP Base

## What?

Stellastructure's AOSP Base, in short StructureAOSP or Stellastructure AOSP, is a simple project run by a college student named Stella Bloom that aims to make AOSP buildable by everyone!

## Why?

Because everyone wanting to mess with AOSP deserve the right to do so with no clutters whether if you're a...
* Buildbot wanting to make single-shot AOSP with no hassle.
* Device maintainer wanting to have pure AOSP experience with no hassle before diving right in.
* ROM maintainer wanting to have less hassle bringing your own source up.

## When?

This depends on context. Organization was created in September 25, 2022. First buildable source is available since March 23, 2024.

## How?

Basically getting just core patches to make AOSP buildable with common config and such **with proper authorships**. You can safely get these patches and submit to whatever ROM you want.

## Additional information

* StructureAOSP is, not to be confused, based straight on AOSP. This allows us to base on the latest stable AOSP tag with no hassle and waiting for another ROM to finish.
* StructureAOSP doesn't have a fixated official device listing/building unlike Stella's other project, Project Kasumi. It's always aimed as "owner's device first" basis.
* You can't submit patches to StructureAOSP unless it's critical for another device to operate. For example, you can submit a patch to adapt MTK IMS and it will be tested on both QCOM and MTK. But you can't submit a patch(set) to expose WiFi and mobile data tiles.
* StructureAOSP doesn't have a mailing list or anything you can submit patches through. You have to use GitHub PRs.
* StructureAOSP doesn't mirror anything to any other repos, and doesn't promote you do so.
* StructureAOSP doesn't promote any kinds of unauthorized changes to its sources (either locally, through sets of patches or straight up forks).
* StructureAOSP **IS NOT A GAMING ROM**!
* StructureAOSP doesn't ship, and doesn't provide support for, any kinds of Google apps. If you want a ROM that does so, you can give Pixel Experience a try. They ship all Google apps at once.
* StructureAOSP doesn't provide ROM-specific functions like `reposync` or `mka`. You're tied to AOSP functions only.

## Building guide

Initialize the repository;
```
repo init -u https://github.com/stellastructure-aosp/platform_manifest -b android-<version> --depth=1 --no-tags --no-clone-bundle --no-repo-verify
```

> You must replace `<version>` with the corresponding AOSP version you want to build - `android-12.1.0` for 12L or `android-13.0.0` for 13 for example.

Sync the repositories;
```
repo sync -c -jX --no-tags --no-clone-bundle --optimized-fetch --no-repo-verify --force-sync --prune
```

> You can omit `--force-sync` if you're not replacing any projects with your local manifests, in other words if your local manifest doesn't use `<remove-project />`.
>
> You can omit `--prune` if you're not planning to change project paths with your local manifests, in other words if you're not going to change `path=""` value in your local manifest entries.

Get common functions in and prepare shell for building;
```
source build/envsetup.sh
```

Set variables for your device;
```
lunch aosp_codename-release-variant
```

> Replace `codename` with your device codename, such as `rosemary`.
>
> Replace `release` with the AOSP release you want to build, such as `ap1a` for Android 14 QPR2.
>
> Replace `variant` with the build variant you want, such as `eng`.

Get to build process;
```
m otapackage
```

If you want to build fastboot images instead;
```
m
```

## Note for maintainers with existing device sources on AOSP

Google's device sources are already synced alongside! You don't have to replace anything here at all! If you patch things to fix/optimize stuff, open a GitHub PR at manifest to track your own fork of it! **DO NOT USE `<remove-project />` TO REPLACE AOSP'S DEVICE SOURCES WITH YOUR OWN!**

## Credits
- [LineageOS](https://github.com/LineageOS) for the build patches and custom prebuilts.
- [PixelExpetience](https://github.com/PixelExperience) for the initial vendor/aosp configuration.
- [halogenOS](https://git.halogenos.org/halogenOS) for plug-and-play vendor/custom.
