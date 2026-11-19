# Vault-Money-Manager

name: Build Vault APK

on:
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Java
        uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '17'

      - name: Setup Gradle
        uses: gradle/actions/setup-gradle@v4
        with:
          gradle-version: '8.9'

      - name: Extract and Build APK
        run: |
          unzip Vault_Android_Project.zip -d extracted
          cd extracted/VaultAndroid
          gradle assembleDebug

      - name: Upload APK
        uses: actions/upload-artifact@v4
        with:
          name: Vault-Android-APK
          path: extracted/VaultAndroid/app/build/outputs/apk/debug/app-debug.apk
