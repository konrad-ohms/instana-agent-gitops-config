# instana-agent-gitops-config
Config repo to control updates to instana agents

See: https://www.ibm.com/docs/en/instana-observability/current?topic=agents-git-based-configuration-management

```
# Please enter proper values for all --env arguments.
docker run \
    --detach \
    --name instana-agent \
    --volume /var/run:/var/run \
    --volume /run:/run \
    --volume /dev:/dev:ro \
    --volume /sys:/sys:ro \
    --volume /var/log:/var/log:ro \
    --privileged \
    --net=host \
    --pid=host \
    --env="INSTANA_AGENT_ENDPOINT=xxx.instana.io" \
    --env="INSTANA_AGENT_ENDPOINT_PORT=443" \
    --env="INSTANA_AGENT_KEY=xxx" \
    --env="INSTANA_DOWNLOAD_KEY=xxx" \
    --env="INSTANA_AGENT_ZONE=konrad-fyre" \
    --env="INSTANA_GIT_REMOTE_BRANCH=main" \
    --env="INSTANA_GIT_REMOTE_PASSWORD=xxx" \
    --env="INSTANA_GIT_REMOTE_REPOSITORY=https://github.com/xxx/instana-agent-gitops-config.git" \
    --env="INSTANA_GIT_REMOTE_USERNAME=xxx" \
    icr.io/instana/agent
```