# Manually Installing ownCloud with the Linux Command Line

This guide details how to manually install ownCloud. This guide assumes that users have the required system configurations and permissions as detailed on the [**Prerequisites**](PREREQ.md) topic. This process is a manual path using the command line. For other methods of installing ownCloud, see the [**Alternative Installation Methods**](ALT-INSTALL.md) topic.

## 1 - Prepare the Server
----

Using an Ubuntu 18.04 LTS Server, ensure that the Apache Web Server and PHP are installed with the following command:

    sudo apt install php libapache2-mod-php apache2

Further considerations such as having multiple concurrent PHP versions as well as best practices can be found on the [**Server Preparation for Ubuntu 18.04**](https://doc.owncloud.org/server/10.6/admin_manual/installation/manual_installation/server_prep_ubuntu_18.04.html) document of the ownCloud Documentation.

## 2 - Install MariaDB
----

While a few options are supported for the choice of databases, the recommended option is MariaDB. For other database install options, see the [**Manual Installation Databases**](https://doc.owncloud.org/server/10.6/admin_manual/installation/manual_installation/manual_installation_db.html) guide.

For Ubuntu 18.04 LTS, add the MariaDB repository with the commands:
    sudo apt-get install software-properties-common

    sudo apt-key adv --fetch-keys 'https://mariadb.org/mariadb_release_signing_key.asc'

    sudo add-apt-repository 'deb [arch=amd64,arm64,ppc64el] https://ftp.osuosl.org/pub/mariadb/repo/10.5/ubuntu bionic main'

Once completed, update the package manager and install MariaDB with:

    sudo apt update

    sudo apt install mariadb-server

For other Linux distributions and versions of MariaDB, see the [**Setting up MariaDB Repositories**](https://downloads.mariadb.org/mariadb/repositories/#distro=Ubuntu&distro_release=bionic--ubuntu_bionic&mirror=osuosl&version=10.5) page on the MariaDB site.

## 3 - Configure the Apache Web Server
----

To configure on Debian and related distributions, simply create a owncloud.conf file at /etc/apache/sites-available with the following commands

     touch /etc/apache/sites-available/owncloud.conf

----
**NOTE:** This command assumes that the needed hierarchy is already created.

----

In this configuration file, add the following content:

    Alias /owncloud "/var/www/owncloud/"

    <Directory /var/www/owncloud/>

        Options +FollowSymlinks

         AllowOverride All

         <IfModule mod_dav.c>

             Dav off

         </IfModule>

    </Directory>

In the command line, create a symlink to the sites-enabled directory with:

    ln -s /etc/apache2/sites-available/owncloud.conf /etc/apache2/sites-enabled/owncloud.conf

For more information on optional Apache Configurations, see the [Configure Apache for Manual Installation on Linux](https://doc.owncloud.org/server/10.6/admin_manual/installation/manual_installation/manual_installation_apache.html) document.

## 4 - Downloading ownCloud
----

Before downloading the software, it is advised to change the command line directory to a temporary folder such as `/tmp.`

    cd /tmp

Go to the [**ownCloud download page**](https://owncloud.com/download-server/) and download the latest `.tar` file and the desired security hash file like `md5` as well as the `asc` PGP signature file. 

Once downloaded, run the md5sum command using the downloaded `md5` file with the `owncloud.tar.bz2` file. In the following commands, change the `x.y.z` value to match the value of the downloaded files which are in a `yyyymmdd` format.

    sudo md5sum -c owncloud-x.y.z.tar.bz2.md5 < owncloud-x.y.z.tar.bz2

If the sha256 has file was downloaded instead, use this command to verify the file.

    sudo sha256sum -c owncloud-x.y.z.tar.bz2.sha256 < owncloud-x.y.z.tar.bz2

Next, verify the PGP signature with this command:

    gpg --verify owncloud-complete-yyyymmdd.tar.bz2.asc owncloud-complete-yyyymmdd.tar.bz2

With the software downloaded and verified there are two paths to installation. The recommended path is using a script to install. This solution provides all the necessary permissions and component setups. To use the scripted installation, visit the [**Script Guided Installation**](https://doc.owncloud.org/server/10.6/admin_manual/installation/manual_installation/script_guided_install.html) document.

## 5 - Manual Installation with the Command Line
----

In the /tmp folder where the ownCloud download as well as the validation files are stored from the last step, extract the oWnCloud files with the following command:

    tar -xjf owncloud-complete-yyyymmdd.tar.bz2

Ensure that the `-xjf` extension is included since the tar file type is `bz2`. 

This extraction operation creates a single directory called `owncloud` containing the necessary files to run ownCloud. Copy this directory from the `/tmp` directory created in the previous step to the Apache web server document root. The default location for this root is `/var/www`, so the command is:

    cp -r owncloud /var/www

Before completing the installation, ownership roles and user permissions must be set. It is advised to use the scripted method to set these. This process is documented on the [**Script Guided Installation**](https://doc.owncloud.org/server/10.6/admin_manual/installation/manual_installation/script_guided_install.html) document.

## 6 - Finalizing the Installation via Command Line
----

Continuing with the command line process, the following command will add all the necessary credentials for the deployment.

    cd /var/www/owncloud/
    sudo -u www-data php occ maintenance:install \
       --database "mysql" \
       --database-name "owncloud" \
       --database-user "root"\
       --database-pass "password" \
       --admin-user "admin" \
       --admin-pass "password"

With this step, ownCloud is installed and configured. There are aditional recommended configurations that users may wish to configure. For inforamtion on these items, see the [**Post Installation Configuration**](https://doc.owncloud.org/server/10.6/admin_manual/installation/manual_installation/manual_installation.html#post-installation-configuration) section of the Detailed Installation Guide document.

[Back to Home](index.md).