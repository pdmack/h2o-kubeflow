# H2O + OpenShift

Populate `config/config.toml` with whatever changes required.

Obtain `license.sig` from H2O and place in the `config` directory.

If you will be using an NVIDIA GPU-enabled host, you will need to set the persistence mode otherwise the DAI server inside the pod will not fully complete its startup

`sudo nvidia-smi -pm 1`

Create a new project 

`oc new-project h2o`

Create a ConfigMap to store the license file and config

`oc create configmap driverless --from-file=config/`

Give the default SA in the new project privileged capability 

`oc adm policy add-scc-to-user privileged -z default`

Set up a local hostPath model storage. This step and the following may be modified to suit available PV or StorageClass options.

`mkdir -p /tmp/h2oai-storage && chmod 777 /tmp/h2oai-storage`

Create a PV and PVC for the storage. The default setting is for 2Gi but you may need or want more storage.

`oc create -f h2oai-volume.json`

`oc create -f h2oai-claim.json`

Launch the deployment

`oc create -f h2oai-driverlessai.json`
