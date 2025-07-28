Consiste en reemplazar el contenido del archivo por lo siguiente (corrigiendo el nombre por el del servicio que se va a migrar):

```yml
include:

- project: "fif/dx/configurable-pipelines/node-build-pipeline"

ref: v1

file: "pipeline.yml"

- project: "fif/canales-digitales/fif-tools/ci-templates/building/update-service-deploy-template"

ref: v1.1.6

file: "template.yml"

- project: "fif/canales-digitales/fif-tools/ci-templates/building/gitlab-tagging-template"

ref: v1.1.2

file: "template.yml"

  

variables:

IMAGE_NAME: hub.fif.tech/onboarding/mx-rewards-card-manager

PROJECT_NAME: mx-rewards-card-manager

DOCKER_FILE_PATH: ./dockerfiles/Dockerfile

CS_DOCKERFILE_PATH: $DOCKER_FILE_PATH

COVERAGE_SCRIPT: npm run coverage-table

DEPLOY_PLATFORM: "all"

INSTALL_DEPS_SCRIPT: npm i --legacy-peer-deps

RUN_COMPILE: false

DEPLOY_PROJECT_REF: &DEPLOY_PROJECT_REF fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-stack-deploy

DEPLOY_PROJECT_URL: "https://gitlab.falabella.tech/${DEPLOY_PROJECT_REF}.git"

LABEL_SERVICE: v_rewards_card_manager

TAG: v${CI_COMMIT_REF_SLUG}-${CI_COMMIT_SHORT_SHA}

MONOREPO: false

  

workflow:

rules:

- if: $CI_PIPELINE_SOURCE == "merge_request_event"

- if: $CI_COMMIT_REF_NAME =~ /^(chore|feature|fix|hotfix)\/.*$/ && $CI_OPEN_MERGE_REQUESTS

when: never

- if: $CI_COMMIT_REF_NAME =~ /^(chore|feature|fix|hotfix)\/.*$/

  

.rules:

deploy:

- if:

$CI_PIPELINE_SOURCE == "merge_request_event" && $CI_MERGE_REQUEST_TARGET_BRANCH_NAME == "master" &&

'$CI_COMMIT_REF_NAME =~ /^(feature|fix|hotfix)\/.*$/'

when: manual

  

stages:

- validtion

- convco

- dependencies

- test

- security

- compile

- build

- security-scan

- generate-changelog

- update-deploy-stack

- deploy-stack

  

stop-checking:

stage: validtion

script:

- echo "This branch name is not allowed to run. It must contain a 'feature/', 'fix/', 'hotfix/' or 'chore/' prefix."

- exit 1

rules:

- if: '$CI_COMMIT_REF_NAME =~ /^(chore|feature|fix|hotfix)\/.*$/'

when: never

- if: '$CI_PIPELINE_SOURCE == "merge_request_event"'

when: always

  

dependency-check-analysis:

allow_failure: true

  

.update_config_template: &update_config

extends: .update-deploy

stage: update-deploy-stack

variables:

TAG: $TAG

needs:

- docker-build

tags:

- fif-runner

  

allow_failure: true

  

.deploy_config_template: &deploy_config

stage: deploy-stack

inherit:

variables: false

trigger:

project: *DEPLOY_PROJECT_REF

branch: master

allow_failure: true

  

update-test:

<<: *update_config

variables:

SERVICE_ENV_FILE: ./deploy/services-test.env

rules:

- !reference [.rules, deploy]

  

deploy-test:

<<: *deploy_config

variables:

DEPLOY_ENV: test

rules:

- !reference [.rules, deploy]

  

update-qa:

<<: *update_config

variables:

SERVICE_ENV_FILE: ./deploy/services-qa.env

rules:

- !reference [.rules, deploy]

  

deploy-qa:

<<: *deploy_config

variables:

DEPLOY_ENV: qa

rules:

- !reference [.rules, deploy]

  

update-prod:

<<: *update_config

variables:

SERVICE_ENV_FILE: ./deploy/services-prod.env

rules:

- !reference [.rules, deploy]

  

deploy-prod:

<<: *deploy_config

variables:

DEPLOY_ENV: prod

rules:

- !reference [.rules, deploy]
```

#### MR de referencia
- Soporte para nullplatform: https://gitlab.falabella.tech/fif/canales-digitales/portafolio-ventas/onboarding/mexico/mx-onboarding-rewards-card-manager/-/merge_requests/39#bde78f313e5e4d0170c8da4a22e81290f67a0dd7