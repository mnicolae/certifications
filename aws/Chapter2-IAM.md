# IAM 101

## What is IAM?

Essentially, IAM allows you to manage users and their level of access to the AWS console. It is important to understand IAM and how it works, both for the exam and for administrating a company's AWS account in real life.

## What does IAM give you?

* Centralized control of your AWS account
* Shared Access to your AWS account
* Granular permissions
* Identity federation (including Active Directory, Facebook, LinkedIn, etc.)
* Multi-factor Authentication
* Provides temporary access for users/devices and services, as necessary
* Allows you to set up your own password retention policy
* Supports PCI DSS Compliance

## Critical Terms

* Users - End Users (think people)
* Groups - A collection of users under one set of permissions
* Roles - You create roles and then assign them to AWS resources
* Policies - A document that defines one (or more) permissions

# IAM summary

## What have we learned so far?

* IAM consists of the following:
* Users
* Groups (A way to group our users and apply policies to them collectively)
* Roles
* Policy documents

* `IAM is universal.` It does apply to regions at this time.
* The "root account" is simply the account created when first setup your AWS account. It has complete Admin access.
* New Users have `NO permissions` when first created.
* New Users are assigned `Access Key ID & Secret Access Keys` when first created.
* These are not the same as a password, and you cannot use the Access key ID & Secret Access Key to login to the AWS Management Console.
* You can use this to access AWS via the APIs and command-line, however.
* You only get to view Access key ID & Secret Access Key once. If you lose them, you have to regenerate them. So, save them in a secure location.
* Always setup MFA on your root account.
* You can always create and customise your own password rotation policies.
