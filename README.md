# Meticulus's Android Bin Tools

## Description
Various tools and prebuilts I use in the course of developing and build android roms on UbuntuMate 14.04 LTS.

### Patch System
The patch system works by having a patchset in the $devicetree/patches. In this folder is a "common" folder and various "$rom" folders. Each recreates the directory structure from the "$TOP" of the AOSP source with corresponding patches inside. The "patcher" tool will find all these patches and apply them to the correct repo. Other tools are there to help make it easy to create and modifiy patches quickly. Each "$rom" folder should hold patches that are specific to that rom. I.E. lineage folder for lineage and slim for slim. The "common" folder is used for patches that apply to all roms. This makes it possible to build several AOSP based ROMs using the same branch of the same tree.

EXAMPLE: https://github.com/Meticulus/android_device_huawei_hi6250/tree/master/patches

NOTE: All patches should be cleared before repo sync'ing. Use "clearpatches". Then "patcher" to re-apply after repo sync'ing.


## License
Any tools written by me are subject to the AGPL. Other prebuilt tools are subject to their own licenses.

## Setup
I keep these in ~/bin and add them to the PATH variable.
```bash
git clone https://github.com/Meticulus/android_bintools -b master ~/bin
```

Add ~/bin to the PATH variable.
```bash
echo PATH=~/bin:$PATH
```

For a more permanent solution:
```bash
echo "PATH=~/bin:\$PATH" >> ~/.bashrc
```

## Session Setup
Before using these tools you should have the typical build android build environment setup.
```bash
. build/envsetup.sh
lunch your_buildtarget-buildvariant
```

## Workflow

### Create a patch
cd to the repo you wish to patch and clear the repo of all patches first.
```bash
clearrepo
```

Make your modifications and then create the patch
```bash
makepatch
```

Re-patch the repo including the patch you just created
```bash
patchrepo
```

### Fix a patch
cd to the repo you wish to patch and clear the repo of all patches first.
```bash
clearrepo
```
Select the broken patch and type its number. Then type 0 for "Work on it"
```bash
listpatch
```

Use git status to see the .rej files and make the appropriate changes. Then use listpatch to replace the old one with the new.
Type 1 for "Replace it".
```bash
listpatch
```

Re-patch the repo including the patch you just created
```bash
patchrepo
```
