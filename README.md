# Buildalon Upload Meta Quest Build

[![Discord](https://img.shields.io/discord/939721153688264824.svg?label=&logo=discord&logoColor=ffffff&color=7389D8&labelColor=6A7EC2)](https://discord.gg/VM9cWJ9rjH)

A GitHub Action for [uploading a Meta Quest app to the Meta Quest store](https://developer.oculus.com/resources/publish-reference-platform-command-line-utility/#upload-quest).

## How to use

* [Get Credentials](https://developer.oculus.com/resources/publish-reference-platform-command-line-utility/#credentials)
* Set repo secrets
  * `META_APP_ID`
  * `META_APP_SECRET`

### workflow

```yaml
steps:
    # setup ovr platform util
  - uses: buildalon/setup-ovr-platform-util@v1
    # upload meta quest build
  - uses: buildalon/upload-meta-quest-build@v2
    id: upload
    with:
      appId: ${{ secrets.META_APP_ID }}
      appSecret: ${{ secrets.META_APP_SECRET }}
      apkPath: 'path/to/apk'
    # use uploaded meta quest build id
  - run: 'echo ${{ steps.upload.build_id }}'
```

### inputs

[Oculus Platform Utility docs](https://developer.oculus.com/resources/publish-reference-platform-command-line-utility/)

| Name | Description | Default | Required |
| ---- | ----------- | ------- |----------|
| `ageGroup` | Age group of the build. This can be `TEENS_AND_ADULTS`, `MIXED_AGES`, or `CHILDREN`. | | Yes |
| `appId` | Your App ID from the meta store | | Yes |
| `appSecret` | Your App secret from the meta store | | Must provide appSecret or token |
| `token` | The App ID from the meta store | | Must provide appSecret or token |
| `apkPath` | Path to the APK to upload | | Yes |
| `obbPath` | Path to an obb file to upload | | No |
| `assetsDir` | DLC Content to upload | | No |
| `releaseChannel` | Which release channel to upload the apk to | `ALPHA` | No |
| `releaseNotes` | Release notes to upload | | No |
| `assetFilesConfig` | DLC Config | | No |
| `languagePacksDir` | Additional languages | | No |
| `debugSymbolsDir` | Path to the folder that contains the debug symbol file(s) | | No |
| `debugSymbolsPattern` | Specifies a file pattern that matches the files names of all debug symbol files | | No |

### outputs

* `build_id`: The uploaded build id.
