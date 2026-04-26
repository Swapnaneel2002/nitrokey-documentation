Windows Active Directory Certificate Services (ADCS) with PKI Proxy
-------------------------------------------------------------------

This document describes the configuration of Windows Active Directory Certificate Services (ADCS) with PKI Proxy and NetHSM.

Prerequisits
============

- NetHSM
  - Provisioned
  - Access to generate or import keys and certificates
- PKI Proxy server
  - NetHSM PKCS#11 module installed and configured to use the NetHSM
- CA server (Windows Server)
  - ADCS role installed, but not configured
  - PKI Proxy client tools installed (not required if this server is the PKI Proxy server)

Root CA Key and Certificate
===========================

The following table lists the key algorithms, key length, together with the used hash function the Windows ADCS can use with NetHSM.

+---------------+------------+---------------------------------------------+
| Key Algorithm | Key Length | Hash function                               |
+---------------+------------+---------------------------------------------+
| RSA           | 512        | MD2, MD4, MD5, SHA1, SHA256, SHA384, SHA512 |
|               +------------+---------------------------------------------+
|               | 1024       | MD2, MD4, MD5, SHA1, SHA256, SHA384, SHA512 |
|               +------------+---------------------------------------------+
|               | 2048       | MD2, MD4, MD5, SHA1, SHA256, SHA384, SHA512 |
|               +------------+---------------------------------------------+
|               | 4096       | MD2, MD4, MD5, SHA1, SHA256, SHA384, SHA512 |
+---------------+------------+---------------------------------------------+
| ECDSA         | P256       | SHA1, SHA256, SHA385, SHA512                |
|               +------------+---------------------------------------------+
|               | P384       | SHA1, SHA256, SHA385, SHA512                |
|               +------------+---------------------------------------------+
|               | P521       | SHA1, SHA256, SHA385, SHA512                |
+---------------+------------+---------------------------------------------+

Generate a new Root CA Key and Certificate on Windows
+++++++++++++++++++++++++++++++++++++++++++++++++++++

#TODO

Generate a new Root CA Key on NetHSM and the Certificate on Windows
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

#TODO

Migrate existing Key and Certificate
++++++++++++++++++++++++++++++++++++

#TODO

NetHSM Configuration
====================

#TODO

PKI Proxy Server Configuration
==============================

On the PKI Proxy Server you must share the just added certificate from the NetHSM.
Please follow the steps in `Publish Certificates from the NetHSM <pkiproxy.html#publish-certificates-from-the-nethsm>`__ to learn more.

Windows ADCS Configuration
==========================

PKI Proxy Client Tools Configuration
++++++++++++++++++++++++++++++++++++

In the following we make the key and certificate available in the Windows local machine certificate store.

1. Open the **PKI Proxy Certificate Manager**.
2. Click the **Add...** button.
3. Fill the required fields.
   * Location, e.g. ``https://localhost:9266``
   * Authentication
   * User
   * Secret Key/Password/SPN
   * Certificate Store: ``Local Maschine\My``
   Confirm the configuration with the **OK** button.
   ->Back to prior window.
4. The list under **Certificate Management** in the **PKI Proxy Certificate Manager** should now show the just added certificate.

You can now verify that the certificate is available in the local machine certificate store.

1. Open the **Run** dialog, either by right clicking on the Windows **Start Menu** and choosing **Run** or pressing **Windows Key + R** on your keyboard.
2. In the **Run** dialog enter ``certlm.msc`` and confirm with pressing **Enter** on your keyboard or by clicking **OK**.
3. In the appearing certificate manager navigate in the tree structure on the left to **Certificates - Local Computer → Personal → My**.
4. Now you should see in the list on the right the published certificate.
   You can check the certificate properties by double-clicking on the certificate.

Windows ADCS Configuration
++++++++++++++++++++++++++

1. Run the configuration assisstant for the ADCS role. #TODO
2. Follow the instructions
   * Credentials
   * Role Services
   * Setup Type

     Select **Enterprise CA** or **Standalone CA** depending on your environment.

   * CA Type

     Select **Root CA**

   * Private Key

     Check the radio button next to **Select a certificate and use its associated private keys**.

   * Finish the assisstant
