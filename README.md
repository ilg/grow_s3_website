# grow + s3_website

[Docker Hub](https://hub.docker.com/r/ilg0/grow_s3_website/)

[grow](https://grow.io/) static site generator and [s3_website](https://github.com/laurilehmijoki/s3_website) utility together in one convenient image

![](https://img.shields.io/docker/automated/ilg0/grow_s3_website.svg)
![](https://img.shields.io/docker/build/ilg0/grow_s3_website.svg)

## Suggested Usage

### `bitbucket_pipelines.yml`

```yml
image: ilg0/grow_s3_website

pipelines:
  default:
    - step:
        script:
          - grow install
          - grow deploy --noconfirm --preprocess
          - s3_website push --dry-run
  branches:
    master:
      - step:
          script:
            - grow install
            - grow deploy --noconfirm --preprocess
            - s3_website push
```

### `podspec.yaml`

```yml
[…]

deployments:
  default:
    destination: local
    out_dir: _site
```

### `s3_website.yml`

```yml
[…]
exclude_from_upload:
  - .grow
[…]
```

### `.gitignore`

```
[…]
_site
[…]
```