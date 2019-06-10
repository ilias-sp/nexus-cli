## About nexus_cli

This is a CLI tool written in PHP to interact with a Nexus Repository OSS that can assist you in certain tasks, mainly to provide the convenience of CLI for massively deleting images/artifacts.

![Sonatype logo](documentation/sonatype_logo.png)

The tool was inspired by another already existing one ([https://github.com/mlabouardy/nexus-cli](https://github.com/mlabouardy/nexus-cli)), which at the time of writing, doesn't support communication with Nexuses running on https and self signed certificates, which basically nullified it for my https enabled environments.


## Usage

```
USAGE: 
nexus_cli help 
nexus_cli configure 
nexus_cli image list 
nexus_cli image tags -name <component's name> 
nexus_cli image info -name <component's name> -tag <tag id> 
nexus_cli image tag delete -name <component's name> -tag <tag id> 
```


## Commands

To setup the details of the Nexus you want to interact with, run:
```
nexus_cli configure
```
Please inspect the generated `.config` file, as a few more configuration variables will be found in it.

To see all the components the Nexus hosts under the provided registry:
```
nexus_cli image list 
```

To see all the tags of a specific component:
```
nexus_cli image tags -name <component's name> 
```

To view info for a tag of a specific component:
```
nexus_cli image info -name <component's name> -tag <tag id> 
```

To delete a tag of a specific component:
```
nexus_cli image tag delete -name <component's name> -tag <tag id> 
```

Please note that to reclaim the FS space after Docker image deletions, you will need to run 2 admin tasks, as explained in this article: [https://help.sonatype.com/repomanager3/cleanup-policies](https://help.sonatype.com/repomanager3/cleanup-policies).


## Configuration file

After using the `configure` option, a `.config` file will be generated, with contents as below:

```
<?php

// Nexus details:
$config["nexus_host"] = "http:10.10.10.2:9090";
$config["nexus_username"] = "admin";
$config["nexus_password"] = "admin";
$config["nexus_repository"] = "docker-images";
$config["skip_certification_checks"] = TRUE;
// 
$config["DEBUG_MODE"] = FALSE;
```

Some more info besides the self-explanatory variables:

| Variable | Description |
| ----------------------- | ----------------------- |
| skip_certification_checks | is important when your Nexus is running on https and its certificate has to be ignored (untrusted, self-signed for example). by default is set to TRUE (skip certificate checks) |
| DEBUG_MODE |  can be set to TRUE to view information about the http requests and their responses when interacting with the Nexus server. |


## Links

here are a couple of links for further reading:

| Description | Link |
| ----------------------- | ----------------------- |
| Sonatype Nexus Repository OSS | [https://www.sonatype.com/nexus-repository-oss](https://www.sonatype.com/nexus-repository-oss) |
| Nexus-cli that inspired this tool | [https://github.com/mlabouardy/nexus-cli](https://github.com/mlabouardy/nexus-cli) |

