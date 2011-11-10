
 #--========================================================================
 #-- Organisation
 #--
 #--	Ce répertoire contient la key qui permet de décrypter les
 #--	strings encodés placés dans les mapfiles pour protéger les accès aux BD.
 #--
 #--========================================================================


ID serveur de production:
msencrypt -key ../usr/mspkey.txt user/password
{5ACE86C1C000C000B00C00000F00C6000B8D000000EB8A61}

msencrypt -key ../usr/mspkey.txt user/password@PRO6
{90AA22C3DA7E48B00000000000F007BA0FEC0F700A00BF25921BBAA87294491A9}

ID serveur de fonctionnel:
{5ACE86C1C000C937B00C000000F00C000E4B12F2BD4CF7618}




pour l'itilisation ... 

http://mapserver.gis.umn.edu/development/rfc/ms-rfc-18






Encryption key

In order to safely protect the encrypted information, an encryption key will be 
required by this mechanism. The key will NOT be stored in the mapfile: it will be stored 
in a separate file on the server and should be kept in a safe area by the server 
administrator (especially outside of the web server's document directories).

The location of the encryption key can be specified by two mechanisms, either by 
setting the environment variable MS_ENCRYPTION_KEY or using a CONFIG directive:

CONFIG MS_ENCRYPTION_KEY "/path/to/mykey.txt"

New "msencrypt" command-line utility

A "msencrypt" command-line utility will be provided to create an encryption key and 
to encrypt passwords (or any string) for use in a mapfile.

To create an encryption key:

msencrypt -keygen /path/to/mykey.txt

To encrypt a password or any string:

msencrypt -key /path/to/mykey.txt <string_to_encrypt>

If the MS_ENCRYPTION_KEY environment variable is set then the -key argument 
does not need to be specified.
Encoding of encrypted strings

Since the result of encryption is binary data that is not suitable for inclusion 
directly in a MapServer mapfile, hex encoding will be used for the encrypted strings 
in the mapfile as well as for storing the encryption key to disk.

The { and } characters will be used as delimiters for encrypted strings inside 
database CONNECTIONs. This will allow the use of either plain text or encrypted passwords 
in mapfiles without any backwards compatibility issues.


