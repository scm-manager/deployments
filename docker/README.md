# Docker

1. Create home directory for scm-manager

```bash
mkdir home
chown 1000:1000 home
```

2. Start container

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

3. Open URL http://localhost:8080

   

#### Plugin installation

To install plugins inside the scm-manager container do the following:

1. Download the **smp files** from the 2.x or 2.0.0 branches at  [oss.cloudogu.com](https://oss.cloudogu.com/jenkins/job/scm-manager/job/scm-manager-bitbucket/) 

2. Put them into `home/plugins`

   Example:

```bash
mkdir home/plugins
wget -O home/plugins/scm-script-plugin.smp https://oss.cloudogu.com/jenkins/job/scm-manager/job/scm-manager-bitbucket/job/scm-script-plugin/job/2.0.0/lastSuccessfulBuild/artifact/target/scm-script-plugin-2.0.0-SNAPSHOT.smp
```