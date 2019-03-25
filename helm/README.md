# Helm

1. Make sure:
   - a valid connection to your kubernetes is available
   - helm is installed
2. Install SCM

```bash
helm install --name scm --image.tag=latest .
```

#### Ingress

If you want to enable ingress,  specify the ingress values of the chart within the installation step.

Example:

```bash
helm install --name scm --set image.tag=latest --set ingress.enabled=true --set ingress.hosts="{scm-manager.local}" .
```



#### Plugin installation

To install plugins along with scm-manager, create your own values file (e.g. `local-value.yaml`):

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

The example above will create:

- an scm-manager 2 at `scm-manager.local` 
- with `scm-gravatar-plugin` and `scm-review-plugin` pre installed



To create an instance with your values file, just use the following command:

```bash
helm install --name scm --values local-values.yaml .
```

For more configuration options have a look at the content of `values.yaml`.