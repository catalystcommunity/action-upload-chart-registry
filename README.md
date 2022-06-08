<!-- start title -->

# GitHub Action:Upload Chart to Registry

<!-- end title -->
<!-- start description -->

This just does a `helm push` to the URL after downloading the asset specified. Meaning that if you set the URL to be oci, it's going to use it. Uses Helm above 3.7.0 so no `helm chart` support is given, which if fine since this action installs the version of helm used.

<!-- end description -->
<!-- start contents -->
<!-- end contents -->
<!-- start usage -->

```yaml
- uses: catalystsquad/action-upload-chart-registry@v1
  with:
    # Release tag to fetch chart from
    # Default: ${{ github.event.release.tag_name }}
    tag: v2.0.1
    # The asset name containing the chart, must be a tar file
    # Default: "chart.tgz"
    release-asset-name: "${{ github.event.release.tag_name }}.tar.gz"
    # The Helm Registry URL for the chart
    # Required, no default given
    helm-registry-url: oci://domain.com/path

```

<!-- end usage -->
<!-- start inputs -->

| **Input**                | **Description**                    |  **Default**                                  | **Required** |
| :----------------------- | :--------------------------------- |  :----------------------------------------:   | :----------: |
| **`tag`**                | Release tag to fetch chart from    |     `${{ github.event.release.tag_name }}`    |  **false**   |
| :----------------------- | :--------------------------------- |  :----------------------------------------:   | :----------: |
| **`release-asset-name`** | Who to greet                       | `${{ github.event.release.tag_name }}.tar.gz` |  **false**   |
| :----------------------- | :--------------------------------- |  :----------------------------------------:   | :----------: |
| **`helm-registry-url`**  | The Helm Registry URL              |     N/A                                       |  **true**    |

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
        uses: catalystsquad/action-upload-chart-registry@v1
        with:
          tag: ${{ github.event.release.tag_name }}
          release-asset-name: "${{ github.event.release.tag_name }}.tar.gz"
          helm-registry-url: oci://domain.com/path
```

<!-- end examples -->
<!-- start [.github/ghdocs/examples/] -->
<!-- end [.github/ghdocs/examples/] -->
