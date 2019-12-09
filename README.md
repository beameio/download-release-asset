# download-gh-release-asset

GitHub action that downloads asset with given name from a given repo/release.

## Environment
Requires setting secrets.GITHUB_TOKEN (on any other custom token) to the env.GITHUB_TOKEN

## Inputs
### file
Required filename to download

### repo
Repository to download from, if not given, it'll default to the current repository
Setting to a different repository requires a custom GITHUB_TOKEN to be set.

### release_tag
Release tag to download the file from, if not give it'll default to the latest release

## Usage

Downloads asset named `asset-file-name.txt` from release assets into working directory with the same name.

```
name: "Fetch release asset"
on:
- release

jobs:
  asset_fetcher:
    runs-on: ubuntu-latest
    steps:
    - uses: beameio/download-release-asset@master
      with:
        file: asset-file-name.txt
        release_tag: v1
      env:
        GITHUB_TOKEN: "${{ secrets.GITHUB_TOKEN }}"
```

## Credits

- https://github.com/wyozi/download-gh-release-asset
- https://gist.github.com/maxim/6e15aa45ba010ab030c4
- https://github.com/JasonEtco/upload-to-release
