# bung Debian packaging

## Introduction

This is the git repository for bung Debian packaging

The main git repository for bung is https://github.com/CharlesMAtkinson/bung

## Forking

When forking, please read tools/git-store-meta/README-for-bung.md

## Usage

### Initialisation: prepare to run debsign

Needs to be done once for each user.

Example

```
c@CW10:~$ diff /home/c/.gnupg/gpg-agent.conf{.org,}
0a1
> allow-preset-passphrase
2c3
< max-cache-ttl 999999
\ No newline at end of file
---
> max-cache-ttl 999999
c@CW10:~$ gpg-connect-agent reloadagent /bye
OK
c@CW10:~$ echo <redacted> | /usr/lib/gnupg/gpg-preset-passphrase --preset C334DC45900C011EB521763C8F12097C5A0BCA50
OK
``` 

### Prepare the source build tree

Ensure debian/source/include-binaries is current.  It only needs changing when the .odt file paths have changed

Copy the the upstream source tarball and run the update script

Example

- To be run in the root of the debian_packaging repository
- Assumes the upstream source tarball is in the parent directory

```
bung_version=3.2.2; package_version=3 
cp -p {..,source}/bung_$bung_version.orig.tar.gz 
tools/update_build_tree.sh -v $bung_version-$package_version
```

### Create the .deb etc.

```tools/build_deb.sh -v $bung_version-$package_version```
