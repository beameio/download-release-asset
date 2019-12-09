# download-gh-release-asset

GitHub action that downloads asset with given name from a given GitHub release.
Usefull for downloading test files from the release assets

## Environment
Required set secrets.GITHUB_TOKEN to env.GITHUB_TOKEN

## Inputs
### file
Required upload file to release asset

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
        args: release_asset.dat
      env:
        GITHUB_TOKEN: "${{ secrets.GITHUB_TOKEN }}"
```

## Credits

- https://gist.github.com/maxim/6e15aa45ba010ab030c4
- https://github.com/JasonEtco/upload-to-release
- https://github.com/wyozi/download-gh-release-asset
