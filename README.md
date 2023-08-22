# Create a single Concourse meta pipeline

## Benefits

- Improved traceability and discoverability of pipelines
- Pipelines automatically kept in sync with git repository
- Human & machine friendly format listing all pipelines
- Easily extensible for introducing more automations

## Cost

Less than a day if:

- Your pipelines already use Vault or any other CredManager (don't use hardcoded secrets)
- Your pipelines are written in static, standard Concourse syntax (no `ytt`, no `jsonnet`, etc)

Between 1 and 2 days if:

- Your pipelines rely on hardcoded secrets (that you need to replace with cred vars)
- Your pipelines require passing some static variables during `set-pipeline`.  
  In which case you need to extend the current `pipelines.yml` format to either:
  - [Allow passing a list of static variables to set-pipeline step](https://concourse-ci.org/set-pipeline-step.html#schema.set-pipeline.vars)
  - [Allow passing a single filepath to set-pipeline step](https://concourse-ci.org/set-pipeline-step.html#schema.set-pipeline.var_files)
- Your pipelines are generated or formatted dynamically using `ytt`, `jsonnet`, etc.  
  In which case you need to introduce a new step in `meta-ssh.yml` or `meta-https.yml` to preprocess your manifest to get the final YAML version on-the-fly.  
  Example: https://github.com/pivotal/cloud-service-broker-ci/blob/7834f75f57d4a69b46e17c7285c3a16021cf196e/aws-csb/pipeline.jsonnet#L517-L554

## Original idea

The following document includes additional suggestions on how to better track secrets, etc.

https://docs.google.com/document/d/1GeopEnKXppLwAYuLAGZGoCTdU0m76OxhtYLr8SeedCw/edit
