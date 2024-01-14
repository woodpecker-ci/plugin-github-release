---
name: GitHub Release
author: Woodpecker Authors
icon: https://raw.githubusercontent.com/woodpecker-ci/plugin-github-release/main/github.svg
description: Add files and artifacts alongside a GitHub Release.
tags: [github, publish, release]
containerImage: woodpeckerci/plugin-github-release
containerImageUrl: https://hub.docker.com/r/woodpeckerci/plugin-github-release
url: https://github.com/woodpecker-ci/plugin-github-release
---

# woodpecker-github-release

Woodpecker plugin to add files and artifacts alongside a GitHub Release.

## Settings

- `api-key`: API key to access Github API
- `files`: list of files to upload
- `file-exists`: what to do if file already exist (default: `overwrite`)
- `checksum`: generate specific checksums
- `checksum-file`: name used for checksum file. \"CHECKSUM\" is replaced with the chosen method (default: `CHECKSUMsum.txt`)
- `checksum-flatten`: include only the basename of the file in the checksum file
- `draft`: create a draft release
- `prerelease`: mark the release as a pre-release
- `discussion-category`: create a discussion in the given category
- `base-url`: API url, needs to be changed for GHE (default `https://api.github.com/`)
- `upload-url`: upload url, needs to be changed for GHE (default: `https://uploads.github.com/`)
- `title`: file or string for the title shown in the GitHub release
- `note`: file or string with notes for the release (example: changelog)
- `overwrite`: force overwrite existing release information, e.g. title or note

## Example

```yaml
steps:
  release:
    image: woodpeckerci/plugin-github-release
    settings:
      files:
        - dist/*.tar.gz
        - dist/*.deb
        - dist/*.rpm
        - dist/checksums.txt
      title: ${CI_COMMIT_TAG##v}
      api-key:
        from_secret: github_token
```
