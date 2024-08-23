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

Onboard a new host agent as test environment

```
curl -o setup_agent.sh https://setup.instana.io/agent && chmod 700 ./setup_agent.sh && sudo ./setup_agent.sh \
    -a xxx \
    -d xxx \
    -t dynamic \
    -e ingress-red-saas.instana.io:443 \
    -s \
    -g https://github.com/konrad-ohms/instana-agent-gitops-config.git \
    -b test
```

A reboot of the agent might be required after first connection to get the correct agent version.
