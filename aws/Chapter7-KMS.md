# AWS Key Management 101

## Managed
AWS Key Management Service (AWS KMS) is a managed service that makes it easy for you to create and control the encryption keys used to encrypt your data.

## Integrated

Seamlessly integrated with many AWS services to make encrypting data in these services as easy as checking a box.

## Simple

With KMS, it is simple to encrypt your data with encryption keys that you manage.

## AWS Key Management Service Exam Tips

The Customer Master Key:
* alias
* description
* key material (either customer provided or AWS provided)
* users, roles, admin permissions
* users, roles, usage permissions
* creation date
* key state
* stays inside KMS

Setup a Customer Master Key:
* Create Alias and Description
* Choose key material option
* Define Key Administrative Permissions: IAM users/roles that can administer (but not use) the key through the KMS API.
* Define Key Usage Permissions: IAM users/roles that can use the key to encrypt and decrypt data.

Key material options:
* Use KMS generated key material
* Your own key material


* AWS-Managed CMK: AWS-provided and AWS-managed CMK. Used on your behalf with the AWS services integrated with KMS.
* Customer-Managed CMK: You create, own and manage yourself.
* Data Key: Encryption keys that you can use to encrypt data, including large amounts of data. You can use a CMK to generate, encrypt, and decrypt data keys.

# KMS API Calls

## KMS API Calls Exam Tips

* aws kms encrypt: encrypts plaintext into ciphertext by using a CMK
* aws kms decrypt: decrypts ciphertext that was encrypted by an AWS KMS CMK
* aws kms re-encrypt: decrypts ciphertext and the re-encrypts it entirely with AWS KMS (e.g., when you change the CMK or manually rotate the CMK)
* aws kms enable-key-rotation: enables automatic key rotation every 365 days
* aws kms generate-data-key: uses the CMK to generate a data key to encrypt data > 4 KB

# KMS Envelope Encryption

## Envelope Encryption Exam Tips

Encrypting the key that encrypts our data.

The CMK is used to encrypt the data key (or envelope key).

The data key encrypts our data.

Used for encrypting anything over 4 KB.

Using envelope encryption avoids sending all your data into KMS over the network.

Remember the GenerateDataKey API call.
