# Alternative Methods to Installing ownCloud
The following methods are supported as well. These provide a bit less configurations, but each requires their own dependencies and processes.

## Docker

Docker is a Product-as-a-service product that allows virtualization containers to run various applications. To use the Docker image, download it from the [**Docker Hub ownCloud site**](https://hub.docker.com/r/owncloud/server/tags?page=1&ordering=last_updated).

For a guide of all the configurations required for the Docker method, see the [**Installing with Docker**](https://doc.owncloud.org/server/10.6/admin_manual/installation/docker/) document.

## Linux Package Manager

With many package managers, ownCloud can be installed by using the `owncloud-files` package.

----
**NOTE** This only installs the bare-minimum ownCloud files. Users will need to configure Apache, their databases, and fulfill the PHP dependencies. For more information on what is required for ownCloud, see the Prerequisites topic. For the commands for different package managers, like Yum, APT, and Zypper, see the [**Linux Package Manager**](https://doc.owncloud.org/server/10.6/admin_manual/installation/linux_packetmanager_install.html) topic.

----

[Back to Home](index.md).