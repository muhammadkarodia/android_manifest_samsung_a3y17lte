# LineageOS 17.1

Before starting check [hardware requirement](https://source.android.com/setup/build/requirements).

### Installing dependencies and Repo
This is for informational purposes only, without any guarantee, you may need extra packages.

The following is from [CrDroid README](https://github.com/crdroidandroid/android).
Some complements can be found [here](https://source.android.com/setup/build/initializing) too.

```bash
# Several packages are needed in order to build LineageOS & CrDroid
$ sudo apt install bc bison build-essential ccache curl flex g++-multilib gcc-multilib git gnupg gperf imagemagick lib32ncurses5-dev lib32readline-dev lib32z1-dev liblz4-tool libncurses5 libncurses5-dev libsdl1.2-dev libssl-dev libwxgtk3.0-gtk3-dev libxml2 libxml2-utils lzop pngcrush rsync schedtool squashfs-tools xsltproc zip zlib1g-dev

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
$ mkdir lineage ; cd lineage

# Init repo
$ repo init --depth=1 -u https://github.com/LineageOS/android.git -b lineage-17.1

# Clone my local repo
$ git clone https://github.com/debie-A320FL/android_manifest_samsung_a3y17lte.git -b lineage .repo/local_manifests

# Sync
$ repo sync --no-repo-verify -c --force-sync --no-clone-bundle --no-tags --optimized-fetch --prune -j`nproc`

# Build
$ . build/envsetup.sh && lunch lineage_a3y17lte-userdebug && mka clean && mka bacon -j`nproc`
```


### How to pass Safetynet ###

In order to pass Google Safetynet, you need to set a build_fingerprint that match your android security patch as explain in the [MagiskHideProps Readme](https://github.com/Magisk-Modules-Repo/MagiskHidePropsConf/blob/master/README.md#matching-the-android-security-patch-date).
In practice, you need to change it to a Google Pixel device (it is what works with me). You can find some build_fingerprint in the [Nippon GSI Telegram Channel](https://t.me/nippongsi). Once you found the correct fingerprint, you need to edit the tree to update the buld_fingerprint used (like in [this commit](https://github.com/debie-A320FL/android_device_samsung_universal7870-common/commit/351c6a91a134319a86f42b6d7184a1e3dd0f7d7f)).

## Credits
2019 @Astrako

2020 @Martin

2021-22 @debie @gonic

## Contact
Telegram support group : https://t.me/+8qvqA0S2lmFiNGVk
