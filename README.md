# download-release-asset

GitHub action that downloads an asset with a given name from a given repo/release.

This is particulary usefull as a way to host large test files - https://help.github.com/en/github/managing-large-files/distributing-large-binaries 

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

Downloads asset named `asset-file-name.txt` from v1 release into working directory with the same name.

```
name: "Fetch asset"
on: [push]
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


Download multiple assets from latest release into working directory with the same name.

```
name: "Run tests"
on: [push]
jobs:
  build:
    strategy:
      matrix:
        testFile: [test1, test2]
    runs-on: ubuntu-latest
    steps:
    - uses: beameio/download-release-asset@master
      with:
        file: "${{ matrix.testFile }}.zip"
        release_tag: v1
      env:
        GITHUB_TOKEN: "${{ secrets.GITHUB_TOKEN }}"
      run: |
        echo "## Running ${{ matrix.testFile }} ##"
        unzip "${{ matrix.testFile }}.zip"
        ls -al
```

## Credits

- https://github.com/wyozi/download-gh-release-asset
- https://gist.github.com/maxim/6e15aa45ba010ab030c4
- https://github.com/JasonEtco/upload-to-release
