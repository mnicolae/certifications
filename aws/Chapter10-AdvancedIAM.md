# Web Identity Federation Exam Tips

* Federation allows users to authenticate with a Web Identity Provider (Google, Facebook, Amazon).
* The user authenticates first with the Web ID Provider and receives an authentication token, which is exchanged for temporary AWS credentials allowing them to assume an IAM role.
* Cognito is an Identity Broker which handles interaction between your applications and the Web ID provider (You don't need to write your own code to do this).
* Provides sign-up, sign-in, and guest user access.
* Syncs user data for a seamless experience across your devices.
* Cognito is the AWS recommended approach for Web ID Federation particularly for mobile apps.

# Cognito User Pools Exam Tips

* Cognito uses User Pools to manage user sign-up and sign-in directly or via Web Identity Providers (Facebook, Amazon, etc.)
* Cognito acts as an Identity broker, handling all interaction with Web Identity Providers.
* Identity Pools provide AWS credentials to access AWS services.
* Cognito uses Push Synchronization to send a silent push notification of user data updates to multiple device types associated with a user ID.

# Inline Policies vs. Managed Policies vs. Custom Policies

Remember the 3 different types of IAM Policies:
* Managed Policy - AWS-managed default policies
* Customer Managed Policy - Managed by you
* Inline Policy - Managed by you and embedded in a single user, group, or role
* In most cases, AWS recommends using Managed Policies over Inline Policies.

# STS - AssumeRoleWithWebIdentity

* Part of the Security Token Service
* Allows users who have authenticated with a Web Identity provider to access AWS resources
* Once the user has authenticated, the application makes the `assume-role-with-web-identity` API call
* If successful, STS will return temporary credentials enabling access to AWS resources
* AssumedRoleUser ARN and AssumedRoleID - are used to programmatically  reference the temporary credentials - not an IAM role or user.

# Cross account access

# Security - Identity & Access Management content

[Best Practices for Choosing Identity Solutions for Applications](https://www.youtube.com/watch?v=-xTs4MmQOo4&secd_iam2)