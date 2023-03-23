# docker-build-and-push-action

## How to use

```
jobs:
  docker-build-and-push:
    needs: release
    if: github.event_name == 'push'
    runs-on: ubuntu-latest

    steps:
      - name: Check-out
        uses: actions/checkout@v3
        with:
          ref: "master"
          fetch-depth: 1

      - name: Release version
        id: semver
        shell: bash
        run: |
          semver=$(jq .version package.json | sed "s/\"//g")
          echo "semver=${semver}" >> $GITHUB_OUTPUT
          echo ${semver}

      - name: Docker build and push
        uses: wintero92/docker-build-and-push-action@v1
        with:
          package_version: ${{...}}
          GH_TOKEN: ${{secrets.GITHUB_TOKEN}}
```

## Inputs

See `action.yaml` for possible inputs.