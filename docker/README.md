# Docker

Create home directory for scm-manager.

```bash
mkdir home
chown 1000:1000 home
```

## Start container

```bash
docker run --name scm \
  -v $(pwd)/home:/var/lib/scm \
  -p 8080:8080 \
  cloudogu/scm-manager:latest
```

or with docker-compose:

```bash
docker-compose up
```

After start open url at http://localhost:8080

## Plugin installation

To install plugins to the container you have to download the **smp** files from the 2.x or 2.0.0 branches at  [oss.cloudogu.com](https://oss.cloudogu.com/jenkins/job/scm-manager/job/scm-manager-bitbucket/) and put them into home/plugins e.g.:

```bash
mkdir home/plugins
wget -O home/plugins/scm-script-plugin.smp https://oss.cloudogu.com/jenkins/job/scm-manager/job/scm-manager-bitbucket/job/scm-script-plugin/job/2.0.0/lastSuccessfulBuild/artifact/target/scm-script-plugin-2.0.0-SNAPSHOT.smp
```