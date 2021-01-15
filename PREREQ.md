# Prerequisites for Installing ownCloud on Linux

The downloaded archive of the ownCloud server will contain all of the necessary dependencies for installation and use. This document will guide users through the process for installing the PHP extensions that ownCloud requires.

----
**Note** This guide focuses on the required extensions for ownCloud. For additional but recommended extensions and prerequisites, see the [Recommended Prerequisites](https://doc.owncloud.org/server/10.6/admin_manual/installation/manual_installation/manual_installation_prerequisites.html#recommended-prerequisites) section of the Prerequisites for Manual Installation on Linux document.

----

This Quick Start Guide assumes users are comfortable using a Linux command line. With Linux, the following command can be used to detect if any of the extensions are already installed. Replace `<module_name>` with the extension name to check.

    php -m | grep -i <module_name>

## List of Required Extensions

The following is a list of the required PHP extensions. The installed PHP version should be at least 7.2, with 7.3 and 7.4 also supported.
### PHP Extensions
----

* **Ctype**: For character type checking
* **cURL**: Used for aspects of HTTP user authentication
* **DOM**: For operating on XML documents through the DOM API
* **GD**: For creating and manipulating image files in a variety of different image formats, including GIF, PNG, JPEG, WBMP, and XPM.
* **HASH Message Digest Framework**: For working with message digests (hash).
* **iconv**: For working with the iconv character set conversion facility.
* **intl**: Increases language translation performance and fixes sorting of non-ASCII characters
* **JSON**: For working with the JSON data-interchange format.
* **libxml**: This is required for the DOM, libxml, SimpleXML, and XMLWriter extensions to work. It requires that libxml2, version 2.7.0 or higher, is installed.
* **Multibyte String**: For working with multibyte character encoding schemes.
* **OpenSSL**: For symmetric and asymmetric encryption and decryption, PBKDF2, PKCS7, PKCS12, X509 and other crypto operations.
* **PDO**: This is required for the pdo_msql function to work.
* **Phar**: For working with PHP Archives (.phar files).
* **POSIX**: For working with UNIX POSIX functionality.
* **SimpleXML**: For working with XML files as objects.
* **XMLWriter**: For generating streams or files of XML data.
* **Zip**: For reading and writing ZIP compressed archives and the files inside them.
* **Zlib**: For reading and writing gzip (.gz) compressed files.

### Database Extensions
----

* **pdo_mysql**: For working with MySQL & MariaDB.
* **pgsql**: For working with PostgreSQL. It requires PostgreSQL 9.0 or above.
* **sqlite**: For working with SQLite. It requires SQLite 3 or above. This is, usually, not recommended for performance reasons.

### Required For Specific Apps
----

* **ftp**: For working with FTP storage
* **sftp**: For working with SFTP storage
* **imap**: For IMAP integration
* **ldap**: For LDAP integration
* **smbclient**: For SMB/CIFS integration