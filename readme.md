
## About
- This repo contains configurations for Fiddler's GCP marketplace k8s listing.

- The approach used on this branch is env-sub approach.

<br>
<br>

## How to build new deployer image

### Step 1: Clone the config repo:
```bash
git clone https://github.com/fiddler-labs/google-marketplace-integration
cd google-marketplace-integration
```

### Step 2: Modify the manifests template if needed.
The `manifests.yaml.template` is generated using `hem temlate` command and modifed to work with MP deployer scripts.

In this step you should modify the file as needed but it must comply with MP deployer scripts or otherwise it will fail to deploy.

### Step 3: Export all need variables:
```bash
export NAMESPACE=test
export REGISTRY=gcr.io/fiddler-public
export APP_NAME=fiddler
```

### Step 4: Delete old deployer image from local (if exists):
```bash
docker rmi $REGISTRY/$APP_NAME/deployer:24.4.1 && docker rmi $REGISTRY/$APP_NAME/deployer:24.4
```

### Step 5: Delete old deployer image from GCR:

link: https://console.cloud.google.com/gcr/images/fiddler-public/global/fiddler/deployer?project=fiddler-public

select the deployer image and click delete at top


### Step 6: Build and push new deployer images:
```bash
docker build --platform=linux/x86_64 --tag $REGISTRY/$APP_NAME/deployer:24.4.1 --tag $REGISTRY/$APP_NAME/deployer:24.4 . && docker push $REGISTRY/$APP_NAME/deployer:24.4.1 && docker push $REGISTRY/$APP_NAME/deployer:24.4
```
<br>
<br>

# Testing with mpdev tools

### Step 1: Installing mpdev tools:

To install  mpdev tools see https://github.com/GoogleCloudPlatform/marketplace-k8s-app-tools/blob/master/docs/mpdev-references.md



### Step 2: Running verify command:

```bash
mpdev verify --deployer=$REGISTRY/$APP_NAME/deployer:24.4 --parameters='{"name": "fiddler", "namespace": "test", "postgresHost":"10.227.0.2", "postgresUser":"root", "postgresPassword":"123", "hostName":"test", "domain":"bar.com"}'
```

Or if you want to write output to file:

```bash
mpdev verify --deployer=$REGISTRY/$APP_NAME/deployer:24.4 --parameters='{"name": "fiddler", "namespace": "test", "postgresHost":"10.227.0.2", "postgresUser":"root", "postgresPassword":"123", "hostName":"test", "domain":"bar.com"}' > OUTPUT
```

Explaination of variables:
- namespace: Where to deploy all resources.
- postgresHost: IP address of postgres CloudSQl db created by Terraform code.
- postgresUser: User name to access the db.
- postgresPassword: Password of the user to access the db.
- hostName: Required variable for Fiddler's app.
- domain: Required variable for Fiddler's app.


<br>
<br>

## Notes:

- All images must be taged with same tag, also need to use major tag like for example `24.4`
- `mpdev verify` command must give success before sumbiting for review. 
- If customer will pay for it's usage then a usage reporting agent must be integrated with any of the main images for Fiddler.


## Remaining Work:

- `mpdev verify` currently doesn't success due to pods are failing and this is because of removal of helm hooks.

- Integrating the usage reporting agent for biiling. See [here]( https://cloud.google.com/marketplace/docs/partners/kubernetes/create-app-package#billing-agent
) and [here](https://github.com/GoogleCloudPlatform/marketplace-k8s-app-tools/blob/64181befcb4d3a5417e84d4f59fea82b016988ab/docs/billing-integration.md
).