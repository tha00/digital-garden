---
title: Installing JDKs on MacOS
draft: false
tags:
---
Search for available versions:
```bash
> brew search --formulae openjk
openjdk ✔     openjdk@11 ✔  openjdk@17    openjdk@21 ✔  openjdk@8
```
(`openjdk` without `@xx` refers to the latest version, in this case 22)

Install a particular version
```bash
brew install openjdk@17
```

Brew installs packages into `/usr/local/Cellar` (Intel) or `/opt/homebrew/Cellar` (M1), but MacOS searches for Java under `/Library/Java/JavaVirtualMachines/`.

The required link is not created by brew ("keg-only"), so we need to add it:
```bash
sudo ln -sfn /usr/local/opt/openjdk@17/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-17.jdk
```

List installed Java versions by running
```bash
> /usr/libexec/java_home -V
17.0.5 (x86_64) "Eclipse Adoptium" - "OpenJDK 17.0.5" /Library/Java/JavaVirtualMachines/temurin-17.jdk/Contents/Home
```

For convenience, set environment variables pointing to the different `JAVA_HOME` locations:
```bash
export JAVA_HOME_11=$(/usr/libexec/java_home -v "11")
export JAVA_HOME_17=$(/usr/libexec/java_home -v "17")
export JAVA_HOME=$JAVA_HOME_17
```