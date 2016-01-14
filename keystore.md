# Creating a KeyStore in JKS Format

## 1. Perform the following command.

```
keytool -keystore clientkeystore -genkey -alias client
```

## 2. Once prompted, enter the information required to generate a CSR. A sample key generation section follows.

```
Enter keystore password: javacaps
What is your first and last name?
[Unknown]: development.sun.com
What is the name of your organizational unit?
[Unknown]: Development
what is the name of your organization?
[Unknown]: Sun
What is the name of your City or Locality?
[Unknown]: Monrovia
What is the name of your State or Province?
[Unknown]: California
What is the two-letter country code for this unit?
[Unknown]: US
Is<CN=development.sun.com, OU=Development, O=Sun, L=Monrovia, ST=California, 
C=US> correct?
[no]: yes

Enter key password for <client>
    (RETURN if same as keystore password):
```

If the KeyStore password is specified, then the password must be provided for the adapter.

## 3. Press `RETURN` when prompted for the key password (this action makes the key password the same as the KeyStore password).

This operation creates a KeyStore file __clientkeystore__ in the current working directory. You must specify a fully qualified domain for the “first and last name” question. The reason for this use is that some CAs such as VeriSign expect this properties to be a fully qualified domain name.

There are CAs that do not require the fully qualified domain, but it is recommended to use the fully qualified domain name for the sake of portability. All the other information given must be valid. If the information cannot be validated, a CA such as VeriSign does not sign a generated CSR for this entry.

This KeyStore contains an entry with an alias of __client__. This entry consists of the generated private key and information needed for generating a CSR as follows:

```
keytool -keystore clientkeystore -certreq -alias client -keyalg rsa -file client.csr
```

This command generates a certificate signing request which can be provided to a CA for a certificate request. The file __client.csr__ contains the CSR in PEM format.

Some CA (one trusted by the web server to which the adapter is connecting) must sign the CSR. The CA generates a certificate for the corresponding CSR and signs the certificate with its private key. For more information, visit the following web sites:

[http://www.thawte.com](http://www.thawte.com)

or

[http://www.verisign.com](http://www.verisign.com)

If the certificate is chained with the CA’s certificate, perform step 4; otherwise, perform step 5 in the following list:

## 4. Perform the following command.

```
keytool -import -keystore clientkeystore -file client.cer -alias client
```

The command imports the certificate and assumes the client certificate is in the file __client.cer__ and the CA’s certificate is in the file __CARoot.cer__.

## 5. Perform the following command to import the CA’s certificate into the KeyStore for chaining with the client’s certificate.

```
keytool -import -keystore clientkeystore -file CARoot.cer -alias theCARoot
```

## 6. Perform the following command to import the client’s certificate signed by the CA whose certificate was imported in the preceding step.

```
keytool -import -keystore clientkeystore -file client.cer -alias client
```

The generated file __clientkeystore__ contains the client’s private key and the associated certificate chain used for client authentication and signing. The KeyStore and/or __clientkeystore__, can then be used as the adapter’s KeyStore.
