# gitlab-auto-cronjob

CronJob Chart

## gitlab-ci.yaml

```yaml
include:
  - template: Auto-DevOps.gitlab-ci.yml

.auto-deploy:
  image: "registry.gitlab.com/gitlab-org/cluster-integration/auto-deploy-image:v1.0.1"

variables:
  # AUTO_DEVOPS_DEPLOY_DEBUG: "true"
  STAGING_ENABLED: 1
  REVIEW_DISABLED: "true"
  TEST_DISABLED: "true"
  CODE_QUALITY_DISABLED: "true"
  LICENSE_MANAGEMENT_DISABLED: "true"
  PERFORMANCE_DISABLED: "true"
  POSTGRES_ENABLED: "false"
  ROLLOUT_STATUS_DISABLED: "true"
  DOCKERFILE_PATH: .gitlab/Dockerfile
  AUTO_DEVOPS_CHART_REPOSITORY: https://1mr.github.io/helm-charts
  AUTO_DEVOPS_CHART_REPOSITORY_NAME: gitlab-auto-cronjob

build:
  stage: build
  image:
    name: gcr.io/kaniko-project/executor:debug
    entrypoint: [""]
  script:
    - echo "{\"auths\":{\"$CI_REGISTRY\":{\"username\":\"$CI_REGISTRY_USER\",\"password\":\"$CI_REGISTRY_PASSWORD\"}}}" > /kaniko/.docker/config.json
    - /kaniko/executor --cache=true --context $CI_PROJECT_DIR --dockerfile $CI_PROJECT_DIR/$DOCKERFILE_PATH --destination $CI_REGISTRY_IMAGE/$CI_COMMIT_REF_NAME:$CI_COMMIT_SHA --destination $CI_REGISTRY_IMAGE:$CI_COMMIT_TAG

```
