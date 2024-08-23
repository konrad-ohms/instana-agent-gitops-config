# instana-agent-gitops-config
Config repo to control updates to instana agents

See: https://www.ibm.com/docs/en/instana-observability/current?topic=agents-git-based-configuration-management

Install the host agent and configure this repo and branch main or test via the webui.

To manually force an update to the hosts, the API can be invoked directly as well which is especially interesting, if GitHub Actions is not an option.

This curl command forces an update to production instances and will reboot the agents
```!/bin/bash
INSTANA_API_TOKEN=xxx
INSTANA_API_ENDPOINT=xxx
curl \
    -v \
    --request POST \
    --header "authorization: apiToken ${INSTANA_API_TOKEN}" \
    "${INSTANA_API_ENDPOINT}/api/host-agent/configuration?query=entity.zone:konrad-gitops%20AND%20entity.tag:gitops_environment=prod"
```