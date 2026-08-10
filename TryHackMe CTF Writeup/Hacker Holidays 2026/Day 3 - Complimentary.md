# Hacker Holidays 2026 - Complimentary
Complimentary is a cloud security challenge room. The scenario centers on inspecting an unauthenticated wellness application that retrieves temporary AWS credentials behind the scenes via AWS Cognito, leading to misconfigured IAM permissions and unauthorized access to guest data stored in DynamoDB.

Here, first I have deployed the attackbox and then used the link provided to open the AWS dashboard. To my surprise, there is no page to create an account. Instead, it sets us up as a guest and it's telling it will have a wellness data about us after a first spa checkup.

<img width="1855" height="606" alt="image" src="https://github.com/user-attachments/assets/50b8a87b-efbb-4a8e-89b5-86d6b7f78506" />

So, to inspect the website, I opened the developer tool, to inspect the code written for this application. The application uses Javascript program.

<img width="1908" height="683" alt="image" src="https://github.com/user-attachments/assets/44bbff93-a769-4771-9cca-82f9b786e4ae" />

In this, under debugging tab, I see app.js under which we have three fields which are

* Identity-pool ID
* AWS_Region
* Table_Name

So, AWS's Identity Pool sometimes has this issue, to create guest accounts for users who have not created the accounts. But this happens when a user gets denied or chooses for a guest account. But, this happened now for us without us authorizing for it. Guest permissions are fine, until it follows the principle of least privilege.

Now, with the identity_pool_id identified, I will switch to the terminal. We will issue temporary credentials which will require an Identity ID which is tied to the pool. 

```
aws cognito-identity get-id \
  --region us-east-1 \
  --identity-pool-id "us-east-1:836c0949-292d-485b-b532-52d5ca7bb688"
```

This command will ask AWS cognito to generate a unique session identifier for an unauthenticated user, who is requesting access to the pool.

<img width="902" height="276" alt="image" src="https://github.com/user-attachments/assets/0f000faa-ba0f-4633-aae5-6ae544f7aca8" />

Now, I exchanged this identity id for a temporary AWS Credentials, for which I passed the IdentityID back to Cognito to receive the temporary security keys.

```
aws cognito-identity get-credentials-for-identity \
  --region us-east-1 \
  --identity-id "us-east-1:4d571309-b007-c7f4-3b37-4d939ba55c13"
```

<img width="1909" height="819" alt="image" src="https://github.com/user-attachments/assets/de6cf320-57d9-4d8e-b34e-7c6a67d40cbf" />

Next, I will load these temporary credentials into the terminal, exported as environment variables.

```














