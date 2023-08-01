## Policy for object storage browser

One of the ways to manage access rights to s3 storage is to use a bucket policy. It is a subset of the Amazon S3 policy language applied to buckets. It holds the policy rules of the bucket and all objects in it

### These keywords are used to define policies

- `"Version"` - date of version of the policy structure. Actual version is `"2012-10-17"`
- `"Statement"` - slice of statements of policy rules, each statement consists of:
    - `"Action"` - may be string or slice of strings with Action rules for each resource, such as `"s3:ListBucket"`, `"s3:GetObject"`, `"s3:PutObject"`, etc
    - `"Effect"` - it is a string with `"Allow"` or `"Deny"` command to take effect
    - `"Principal"` - specifies the user, account, service, or other entity that is allowed or denied access to a resource. It may be a string or a map of strings in special format. For more information, see [Principal](https://docs.aws.amazon.com/AmazonS3/latest/userguide/s3-bucket-user-policy-specifying-principal-intro.html)
    To grant permission to everyone, also referred as anonymous access, you can set the wildcard ("*") as the Principal value.

        Using 
        ```json
        "Principal": "*"
        ``` 
        with an `"Allow"` effect in a resource-based policy allows anyone, even if they’re not signed in to AWS, to access your resource

        Using 
        ```json
        "Principal" : { "AWS" : "*" }
        ```
        with an `"Allow"` effect in a resource-based policy allows any root user, IAM user, assumed-role session, or federated user in any account in the same partition to access your resource
        
        For anonymous users, these two methods are equivalent

    - `"Resource"` - Buckets and objects are resources for which you can allow or deny permissions. It may be string or slice of strings in special format.
    Amazon Resource Name (ARN) format identifies resources in AWS:
        ```json
        arn:partition:service:region:namespace:relative-id
        ```
        - __partition__ - `aws` - is a common partition name
        - __service__ - `s3`
        - __relative-id__ - `bucket_name` or `bucket_name/object_name`, or `bucket_name/*`, etc
    
    The ARN format for object storage resources reduces to the following:
    ```json
    arn:aws:s3:::bucket_name/obj_name
    ```
    For more information, see [Resource](https://docs.aws.amazon.com/AmazonS3/latest/userguide/s3-arn-format.html)
    - `"Condition"` - Conditions for when a policy is in effect. You can use AWS‐wide keys and Amazon S3‐specific keys to specify conditions in an object storage access policy. For more information, see [Condition key examples](https://docs.aws.amazon.com/AmazonS3/latest/userguide/amazon-s3-policy-keys.html)

### Template of policy structure for object storage browser we use

```json
{
  "Version":  "2012-10-17",
  "Statement":  [
    {
      "Action":  [
        "s3:ListBucket"
      ],
      "Effect":  "Allow",
      "Principal":  "*",
      "Resource":  [
        "arn:aws:s3:::{bucketName}"
      ]
    },
    {
      "Action":  [
        "s3:GetObject"
      ],
      "Effect":  "Allow",
      "Principal":  "*",
      "Resource":  [
        "arn:aws:s3:::{bucketName}/*"
      ]
    }
  ]
}
```

This template makes a bucket with name {bucketName} `public`

### Visibility states we use:

---

There are three states of visibility in our API

#### 1) `private`

- The default policy structure is empty and it means private access to resources.  
- Also, we have private access if a statement for needed resource is absent or present with `"Effect"`: `"Deny"`.
- If present two statements for one resource with `"Allow"` and `"Deny"` effects, `"Deny"` has more priority and the policy is `private`.

#### 2) `public`

we consider a resource `public` if:

- its name is present in statement with `"Allow"` effect and in `"Principal"` section present wildcard ("*") value.
- `"Action"`: `"s3:ListBucket"` is present for the checked bucket
- `"Action"`: `"s3:GetObject"` is present for the checked object or for the all objects in a bucket

#### 3) `custom`

we consider a resource `custom` if:

- `"Version"` of the policy structure not actual. Meen not `"2012-10-17"` or keyword `"Version"` is absent
- we did not recognize the ruleset as __private__ or __public__ for the given resource. It means that this resource may be as private and as public with using any other statements of policy.
