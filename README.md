# Release/Roll back repo

- Release/Roll Back CI workflow expects input( for instance v0.0.1) and has jobs:
    - build-images
        - ~~triggers each repo creating a new tag/release with tag's version~~
        - ~~azure registries(prod/dev)~~
        - ~~stage branch → build image:date-time~~
        - ~~Hot Fix → image:hot-fix-date~~
        - ~~show tag on website~~
        - ~~each repo is triggered~~
        ```bash
        on:
            push:
                tags:
                - 'v*'
        ```
        - ~~builds image using:~~
        ```bash
        - name: Extract version
            id: vars
            run: |
            echo "VERSION=${GITHUB_REF_NAME}" >> $GITHUB_OUTPUT
        ```
        - ~~pushes to artifact registry~~
        - ~~Release CI waits until all images are built~~
            ```bash
            docker manifest inspect myregistry/app-{1..3}:${{ steps.vars.outputs.VERSION }}
            ```
        - ~~Only when all images exist → move forward~~

    - maintenance mod(manually)
        - maintance mod on

    - deploy
        - ~~separate repo with charts and values.yaml~~
        - ~~helm diff to see changes~~
        - dev or stage build/deploy
        - ~~workflow is triggered based on branch name(hot-fix) to build/deploy a single svc~~
        - ~~Deploy with Helm passing: `--set image.tag=v0.0.1`~~
        - maintance mod off

    - roll back(optional; manually)