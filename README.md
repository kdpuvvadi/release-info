# release-info

[![Actions Status](https://github.com/kdpuvvadi/release-info/workflows/ci/badge.svg)](https://github.com/kdpuvvadi/release-info/actions)
[![Latest
release](https://img.shields.io/github/v/release/kdpuvvadi/release-info?include_prereleases)](https://github.com/abatilo/release-info-action/releases)
[![License](https://img.shields.io/github/license/kdpuvvadi/release-info)](https://github.com/kdpuvvadi/release-info/blob/main/LICENSE)

A GitHub Action which fetches information about GitHub releases for you to use.

Inputs:

| Name  | Description                   | Required? |
| ----- | ----------------------------- | --------- |
| owner | The user or org for this repo | true      |
| repo  | The name of the repo itself   | true      |

Outputs:

| Name                    | Description                                                                                                       |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------- |
| latest_tag              | The latest release version tag                                                                                    |
| latest_tag_published_at | The ISO8601 timestamp of when this version was released                                                           |
| target_commitish        | Specifies the commitish value that determines where the Git tag is created from. Can be any branch or commit SHA. |

Example step

```
- name: Get Latest Release
  id: latest_version
  uses: kdpuvvadi/release-info@v1.0.0
  with:
    owner: kdpuvvadi
    repo: release-info
```

No other setup is required to use this action.

Example Workflow

```yaml
on: push

name: Example
jobs:
  latest-version:
    name: Get Latest Release
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@main
      - name: Get Latest Release
        id: latest_version
        uses: kdpuvvadi/release-info@v1.0.0
        with:
          owner: kdpuvvadi
          repo: release-info
      - name: Example of consumption of the output
        env:
          LATEST: ${{ steps.latest_version.outputs.latest_tag }}
          LATEST_DATE: ${{ steps.latest_version.outputs.latest_tag_published_at }}
        run: |
          echo "Version $LATEST was released at $LATEST_DATE"
```

You can see an example of the invocation of this workflow by [clicking here](https://github.com/kdpuvvadi/release-info/actions?query=workflow%3AExample)
