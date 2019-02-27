# H2O + OpenShift

Populate `config/config.toml` with whatever changes required.

Obtain `license.sig` from H2O and place in the `config` directory.

`oc create configmap driverless --from-file=config/`

`oc create -f h2oai-driverlessai.json`
