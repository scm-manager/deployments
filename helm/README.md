# Helm

Be sure you have a valid connection to your kubernetes and helm is installed.

```bash
helm install --name scm --image.tag=latest .
```

## Ingress

If you want to enable ingress, you can specify it with the ingress values of the chart e.g.:

```bash
helm install --name scm --set image.tag=latest --set ingress.enabled=true --set ingress.hosts="{scm-manager.local}" .
```

## Plugins

If you want to install plugins along with scm-manager, you should create your own values file e.g.: `local-value.yaml`:

```yaml
image:
  tag: version

service:
  type: ClusterIP
 
ingress:
  enabled: true
  hosts:
  - scm-manager.local

plugins:
 
 # urls are taken from https://oss.cloudogu.com/jenkins/job/scm-manager/job/scm-manager-bitbucket/

 - name: scm-gravatar-plugin
   url: https://oss.cloudogu.com/jenkins/job/scm-manager/job/scm-manager-bitbucket/job/scm-gravatar-plugin/job/2.x/lastSuccessfulBuild/artifact/target/scm-gravatar-plugin-2.0.0-SNAPSHOT.smp
 - name: scm-review-plugin
   url: https://oss.cloudogu.com/jenkins/job/scm-manager/job/scm-manager-bitbucket/job/scm-review-plugin/job/develop/lastSuccessfulBuild/artifact/target/scm-review-plugin-2.0.0-SNAPSHOT.smp
```

The example above will create an scm-manager 2 at `scm-manager.local` with `scm-gravatar-plugin` and `scm-review-plugin` pre installed. To create the instance with the created values file, just use the following command:

```bash
helm install --name scm --values local-values.yaml .
```

For more configuration options have a look at the `values.yaml`.