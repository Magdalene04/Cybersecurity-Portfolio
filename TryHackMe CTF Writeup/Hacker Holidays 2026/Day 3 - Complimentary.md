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




