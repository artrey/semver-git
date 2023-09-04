# Semver tool wit installed git

Original semver image: https://github.com/alpine-docker/multi-arch-libs/tree/master/semver

## Usage

```yml
Prepare:Version:
  stage: prepare
  image: artrey/semver-git
  before_script:
    - git fetch --tags
  script:
    - PREV_VERSION=$(git describe --tags --abbrev=0) || true
    - echo "VERSION=$(semver -c -i minor ${PREV_VERSION:-0.0.0})" > prepare.env
  after_script:
    - cat prepare.env
  artifacts:
    reports:
      dotenv: prepare.env
```
