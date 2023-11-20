---
name: GitHub Release
authors: Woodpecker Authors
icon: https://woodpecker-ci.org/img/logo.svg
description: Extend your .env file with additional variables like semver information.
tags: [github, publish, release]
containerImage: woodpeckerci/plugin-github-release
containerImageUrl: https://hub.docker.com/r/woodpeckerci/plugin-github-release
url: https://github.com/woodpecker-ci/plugin-github-release
---

Woodpecker plugin to publish files and artifacts to GitHub Release.

# Settings

- `api-key`: api key to access github api
- `files`: list of files to upload
- `file-exists`: what to do if file already exist (default: `overwrite`)
- `checksum`: generate specific checksums
- `checksum-file`: name used for checksum file. \"CHECKSUM\" is replaced with the chosen method (default: `CHECKSUMsum.txt`)
- `checksum-flatten`: include only the basename of the file in the checksum file
- `draft`: create a draft release
- `prerelease`: set the release as prerelease
- `discussion-category`: create a discussion in the given category
- `base-url`: api url, needs to be changed for ghe (default `https://api.github.com/`)
- `upload-url`: upload url, needs to be changed for ghe (default: `https://uploads.github.com/`)
- `title`: file or string for the title shown in the github release
- `note`: file or string with notes for the release (example: changelog)
- `overwrite`: force overwrite existing release informations e.g. title or note

# Example

```yaml
steps:
  extend-env:
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
