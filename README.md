
## sidecred 🤖

Sidecred handles the lifecycle of your credentials "on the side". It supports multiple credential providers and secret store, and handles the lifecycle from creation, to rotations and eventual deletion.


## Development

### Local

```bash
# Enable the STS provider
export AWS_REGION=eu-west-1
export SIDECRED_STS_PROVIDER_ENABLED=true
export SIDECRED_STS_PROVIDER_SESSION_DURATION=20m

# Enable the Github provider
export SIDECRED_GITHUB_PROVIDER_ENABLED=true
export SIDECRED_GITHUB_PROVIDER_KEY_ROTATION_INTERVAL=20m

# Chose a secret store and configure it
export SIDECRED_SECRET_STORE_BACKEND=ssm
export SIDECRED_SSM_STORE_PATH_TEMPLATE="/sidecred/{{ .Namespace }}/{{ .Name }}"

# Chose a state backend and configure it
export SIDECRED_STATE_BACKEND=file

# Enable debug logging
export SIDECRED_DEBUG=true
```

After setting the above you can execute `sidecred` as follows:

```bash
# The Github App credentials (integration ID and private key) and AWS STS credentials
# should be populated using e.g. vaulted or aws-vault:
go run ./cmd/sidecred --namespace e2e --config ./cmd/sidecred/testdata/config.yml
```
