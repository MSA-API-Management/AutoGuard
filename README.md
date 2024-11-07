# AutoGuard
This action uses AutoOAS and OpenAPI-diff to find breaking API changes in Spring REST APIs.

# Usage
## GitHub
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
## GitLab 
~~~yml
include:
  - local: 'AutoGuard.gitlab-ci.yml'
    inputs:
        mvn_src_dir: "."

# Extend .autoGuard job to add configuration like a job rule or stage 
autoGuard:
  extends: .autoGuard
  rules:
    - if: $CI_PIPELINE_SOURCE == 'merge_request_event'
  stage: test
~~~

