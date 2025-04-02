
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
