# AutoGuard
AutoGuard is a tool that automatically detects breaking changes of REST APIs in services developed with the popular Java Spring Boot framework. We published AutoGuard as a [tool paper](https://doi.org/10.1109/SANER64311.2025.00083).

We provide an example project with AutoGuard set up [on GitHub](https://github.com/MSA-API-Management/AutoGuard-example-project) and a demonstration video [on YouTube](https://www.youtube.com/watch?v=3qeWIVfMvWE).

## AutoGuard v1.2 now supports JAX-RS
Use `MSA-API-Management/AutoGuard@v1.2` to detect breaking changes of REST APIs developed with JAX-RS. 

## GitHub action 
The action uses AutoGuard-gen (currently implemented with [AutoOAS](https://github.com/MSA-API-Management/AutoOAS-action)) and [AutoGuard-diff](https://github.com/MSA-API-Management/AutoGuard-diff-action) to find breaking REST API changes in Java Spring Boot web services.

### Usage
~~~yml
- uses: MSA-API-Management/AutoGuard@v1
  with:
    # Path to the Maven source directory
    # default: '${{github.workspace}}'
    source_dir:
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
        source_dir: "."

# Extend .autoGuard job to add configuration like a job rule or stage 
autoGuard:
  extends: .autoGuard
  rules:
    - if: $CI_PIPELINE_SOURCE == 'merge_request_event'
  stage: test
~~~

## Academic Use
If you use this project in your academic work, please cite the following paper:

> A. Lercher, C. Bauer, C. Macho and M. Pinzger, "AutoGuard: Reporting Breaking Changes of REST APIs from Java Spring Boot Source Code," 2025 IEEE International Conference on Software Analysis, Evolution and Reengineering (SANER), Montreal, QC, Canada, 2025, pp. 814-818, doi: 10.1109/SANER64311.2025.00083.

```bibtex
@INPROCEEDINGS{10992426,
  author={Lercher, Alexander and Bauer, Clemens and Macho, Christian and Pinzger, Martin},
  booktitle={2025 IEEE International Conference on Software Analysis, Evolution and Reengineering (SANER)}, 
  title={AutoGuard: Reporting Breaking Changes of REST APIs from Java Spring Boot Source Code}, 
  year={2025},
  volume={},
  number={},
  pages={814-818},
  doi={10.1109/SANER64311.2025.00083}}
```
