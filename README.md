<!-- start title -->

# GitHub Action:Upload a released helm chart to a git helm charts repository

<!-- end title -->
<!-- start description -->

Extracts a helm chart tgz file from a release, assumes the . This action is designed to be run on a release trigger, and to extract a packaged chart in .tgz format from a .tgz file such as chart.tgz.

<!-- end description -->
<!-- start contents -->
<!-- end contents -->
<!-- start usage -->

```yaml
- uses: catalystcommunity/action-upload-chart-registry@undefined
  with:
    # Release tag to fetch chart from
    # Default: ${{ github.event.release.tag_name }}
    tag: ""

    # the asset name containing the chart, must be a tar file
    # Default: chart.tgz
    release-asset-name: ""

    # the url of the helm registry to upload to
    helm-registry-url: ""

    # github token to use for the release, if you want this to trigger other workflows
    # such as flows on release created, pass in a PAT
    # Default: ${{ github.token }}
    token: ""
```

<!-- end usage -->
<!-- start inputs -->

| **Input**                | **Description**                                                                                                                  |              **Default**               | **Required** |
| :----------------------- | :------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------: | :----------: |
| **`tag`**                | Release tag to fetch chart from                                                                                                  | `${{ github.event.release.tag_name }}` |  **false**   |
| **`release-asset-name`** | the asset name containing the chart, must be a tar file                                                                          |              `chart.tgz`               |  **false**   |
| **`helm-registry-url`**  | the url of the helm registry to upload to                                                                                        |                                        |   **true**   |
| **`token`**              | github token to use for the release, if you want this to trigger other workflows such as flows on release created, pass in a PAT |         `${{ github.token }}`          |  **false**   |

<!-- end inputs -->
<!-- start outputs -->

No Outputs at this time

<!-- end outputs -->
<!-- start examples -->

### Example usage

```yaml
on: [push]

jobs:
  push_my_released_chart_tgz:
    runs-on: ubuntu-latest
    name: I will push my chart!
    steps:
      - name: Dump Context
        uses: crazy-max/ghaction-dump-context@v1
      - name: Whatever I Need to Do to Login
        # This is whatever actions I need to take to be logged in to my helm registry
        uses: fakeorg/action-login-to-registry@v7
        with:
          REGISTRY_USERNAME: somesecret
          REGISTRY_PASSWORD: somepasswordmaybealsofromsecrets
      - name: Push Chart
        uses: catalystcommunity/action-upload-chart-registry@v1
        with:
          tag: ${{ github.event.release.tag_name }}
          release-asset-name: "chartname-${{ github.event.release.tag_name }}.tar.gz"
          helm-registry-url: oci://domain.com/path
```

<!-- end examples -->
<!-- start [.github/ghdocs/examples/] -->
<!-- end [.github/ghdocs/examples/] -->
