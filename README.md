# Nextflow template for non-nf-core pipelines

This repository contains a configuration file and parameters template for
running Nextflow pipelines on Sasquatch. If you are using an nf-core pipeline,
you should not use the instructions in this repository, but should instead use
[`-profile seattlechildrens`](https://nf-co.re/configs/seattlechildrens/).
(See [nf-core_vetted_pipelines](https://ea-bitbucket-prod.childrens.sea.kids/projects/RP/repos/nf-core_vetted_pipelines/browse)
for some specific information on individual pipelines that we have tested on
Sasquatch.) Otherwise, if you are building your own pipeline or using one that
you found on GitHub, you can use the files from this repository to get it
running on Sasquatch.

1. Copy `conf/sasquatch.config` to the `conf` folder in your workflow. You might
consider modifying the `workDir` or `cacheDir` directories if you want to have
pipeline-specific directories.

2. Edit `nextflow.config` to add the line `includeConfig "./conf/sasquatch.config"`

3. If using a params file to pass in parameters (highly recommended so you don't
have to further edit `nextflow.config`) you can use `params/params.yml` as a
starting point. Alternatively you can define the `assoc` parameter in your own
params or config file.

4. The code below can be modified for running your pipeline.

``` bash
mamba activate nextflow

DATE=$(date +%F)
PREFIX="pipelinereport_${DATE}"

nextflow -log "reports/${PREFIX}_nextflow.log" \
    -c nextflow.config \
    run main.nf \
    -profile sasquatch \
    -params-file params/<PARAMS.yml> \
    -work-dir <WORKDIR> \
    -resume
```
