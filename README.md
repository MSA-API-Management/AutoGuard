# AutoGuard
AutoGuard is a tool that automatically detects breaking changes of REST APIs in services developed with the popular Java Spring Boot framework.


## GitHub action 
The action uses AutoGuard-spec (currently implemented with [AutoOAS](https://github.com/MSA-API-Management/AutoOAS-action)) and [AutoGuard-diff](https://github.com/MSA-API-Management/AutoGuard-diff-action) to find breaking REST API changes in Java Spring Boot web services.

### Usage
~~~yml
- uses: MSA-API-Management/AutoGuard@v1
  with:
    # Path to the Maven source directory
    # default: '${{github.workspace}}'
    mvn_src_path:
    # The branch, tag or commit SHA of the old API version
    # default: '${{github.base_ref}}' (Base branch reference of a pull request)
    base_ref:
    # The branch, tag or commit SHA of the old API version
    # default: '${{github.head_ref}}' (Head branch reference of a pull request)
    head_ref:
~~~

## GitLab template
The template implements the AutoGuard-spec (again implemented with [AutoOAS](https://github.com/MSA-API-Management/AutoOAS-action)) and AutoGuard-diff directly.

### Usage
~~~yml
include:
  - remote: 'https://raw.githubusercontent.com/MSA-API-Management/AutoGuard/refs/tags/v1/AutoGuard.gitlab-ci.yml'
    inputs:
        mvn_src_dir: "."

# Extend .autoGuard job to add configuration like a job rule or stage 
autoGuard:
  extends: .autoGuard
  rules:
    - if: $CI_PIPELINE_SOURCE == 'merge_request_event'
  stage: test
~~~

