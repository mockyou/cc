```bash
aws configure
```

Fill in the prompts using the **Access key** and **Secret key** from AWS Console:

```
AWS Access Key ID [None]: <YOUR-ACCESS-KEY-ID>
AWS Secret Access Key [None]: <YOUR-SECRET-ACCESS-KEY>
Default region name [None]: us-east-1
Default output format [None]: json
```

---

### 🟩 4. **Check Current Users (needs IAM permission)**

```bash
aws iam list-users
```

> 🔐 If you get **AccessDenied**, it means this IAM user lacks `iam:ListUsers`. Add it via the console or attach `IAMFullAccess`.

---

### 🟩 5. **Create a New IAM User**

```bash
aws iam create-user --user-name new_user_name
```

---

### 🟩 6. **List IAM Users Again (Verification)**

```bash
aws iam list-users
```

---

### 🟩 7. **Grant S3 Full Access to New User**

Attach `AmazonS3FullAccess` policy:

```bash
aws iam attach-user-policy \
  --user-name new_user_name \
  --policy-arn arn:aws:iam::aws:policy/AmazonS3FullAccess
```

✅ Now `new_user_name` has full S3 access.

---

### 🟩 8. **Generate Access Key for New User (Login Info)**

```bash
aws iam create-access-key --user-name new_user_name
```

Save the output:

```json
{
  "AccessKey": {
    "AccessKeyId": "AKIA....",
    "SecretAccessKey": "...."
  }
}
```

---

### 🟩 9. **Log in as the New User**

```bash
aws configure
```

Enter the **AccessKeyId / SecretAccessKey** from Step 8.

---

### 🟩 10. **Create an S3 Bucket**

```bash
aws s3 mb s3://your-unique-bucket-name
```


---

### 🟩 11. **Create a Test File**

```bash
echo "akjnrwsd" > test.txt
```

---

### 🟩 12. **Upload File to S3 Bucket**

```bash
aws s3 cp test.txt s3://your-unique-bucket-name/
```
