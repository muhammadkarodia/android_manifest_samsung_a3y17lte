# LineageOS 18.1

Before starting check [hardware requirement](https://source.android.com/setup/build/requirements).

### Installing dependencies and Repo
This is for informational purposes only, without any guarantee, you may need extra packages.

The following is from [CrDroid README](https://github.com/crdroidandroid/android).
Some complements can be found [here](https://source.android.com/setup/build/initializing) too.

```bash
# Several packages are needed in order to build LineageOS & CrDroid
$ sudo apt install bc bison build-essential ccache curl flex g++-multilib gcc-multilib git gnupg gperf imagemagick lib32ncurses5-dev lib32readline-dev lib32z1-dev liblz4-tool libncurses5 libncurses5-dev libsdl1.2-dev libssl-dev libwxgtk3.0-gtk3-dev libxml2 libxml2-utils lzop pngcrush rsync schedtool squashfs-tools xsltproc zip zlib1g-dev
# You also need to install git-lfs

# Install Repo tool
# Make a directory where Repo will be stored and add it to the path
$ mkdir ~/bin
$ PATH=~/bin:$PATH

# Download Repo itself
$ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo

# Make Repo executable
$ chmod a+x ~/bin/repo
```

### How to build ###

```bash
# Create dirs
$ mkdir lineage18 ; cd lineage18

# Init repo
$ repo init --depth=1 -u https://github.com/LineageOS/android.git -b lineage-18.1

# Clone my local repo
$ git clone https://github.com/debie-A320FL/android_manifest_samsung_a3y17lte.git -b lineage-18.1-oss_bsp-vndk .repo/local_manifests

# Sync official Github repo
$ repo sync --no-repo-verify -c --force-sync --no-clone-bundle --no-tags --optimized-fetch --prune -j`nproc`
# You need to use git-lfs to handle large files (like chromium webview) since repo doesn't support it out of the box.
$ repo forall -c 'git lfs pull'

# Build
# For 16GB RAM or more
$ . build/envsetup.sh && lunch lineage_a3y17lte-userdebug && mka clean && mka bacon -j`nproc`

# For 8GB RAM (workaround)
$ . build/envsetup.sh && lunch lineage_a3y17lte-userdebug && mka clean && mka api-stubs-docs && mka hiddenapi-lists-docs && mka system-api-stubs-docs && mka test-api-stubs-docs && mka bacon -j`nproc`
```


### How to pass Safetynet ###

You need to modify the android_framework_base repo and use my commits from August 10 2023 share [here](https://github.com/debie-A320FL/android_frameworks_base/commits/59f008284014286b0d534310688ad946a96633b4).

### Extra features ###

Additionnal features such as Signature Spoofing support are set in a android_X repo. Check my personnal repositories to find them ;).

## Credits
2019 @Astrako

2020 @Martin

2021-22 @debie @gonic

2023 @debie @FlominatorGD

## Contact
Telegram support group : https://t.me/debieLineageOS
