# AddPermission<a name="API_AddPermission"></a>

Grants an AWS service or another account permission to use a function\. You can apply the policy at the function level, or specify a qualifier to restrict access to a single version or alias\. If you use a qualifier, the invoker must use the full Amazon Resource Name \(ARN\) of that version or alias to invoke the function\.

To grant permission to another account, specify the account ID as the `Principal`\. For AWS services, the principal is a domain\-style identifier defined by the service, like `s3.amazonaws.com` or `sns.amazonaws.com`\. For AWS services, you can also specify the ARN or owning account of the associated resource as the `SourceArn` or `SourceAccount`\. If you grant permission to a service principal without specifying the source, other accounts could potentially configure resources in their account to invoke your Lambda function\.

This action adds a statement to a resource\-based permission policy for the function\. For more information about function policies, see [Lambda Function Policies](https://docs.aws.amazon.com/lambda/latest/dg/access-control-resource-based.html)\. 

## Request Syntax<a name="API_AddPermission_RequestSyntax"></a>

```
POST /2015-03-31/functions/FunctionName/policy?Qualifier=Qualifier HTTP/1.1
Content-type: application/json

{
   "[Action](#SSS-AddPermission-request-Action)": "string",
   "[EventSourceToken](#SSS-AddPermission-request-EventSourceToken)": "string",
   "[Principal](#SSS-AddPermission-request-Principal)": "string",
   "[RevisionId](#SSS-AddPermission-request-RevisionId)": "string",
   "[SourceAccount](#SSS-AddPermission-request-SourceAccount)": "string",
   "[SourceArn](#SSS-AddPermission-request-SourceArn)": "string",
   "[StatementId](#SSS-AddPermission-request-StatementId)": "string"
}
```

## URI Request Parameters<a name="API_AddPermission_RequestParameters"></a>

The request requires the following URI parameters\.

 ** [FunctionName](#API_AddPermission_RequestSyntax) **   <a name="SSS-AddPermission-request-FunctionName"></a>
The name of the Lambda function, version, or alias\.  

**Name formats**
+  **Function name** \- `my-function` \(name\-only\), `my-function:v1` \(with alias\)\.
+  **Function ARN** \- `arn:aws:lambda:us-west-2:123456789012:function:my-function`\.
+  **Partial ARN** \- `123456789012:function:my-function`\.
You can append a version number or alias to any of the formats\. The length constraint applies only to the full ARN\. If you specify only the function name, it is limited to 64 characters in length\.  
Length Constraints: Minimum length of 1\. Maximum length of 140\.  
Pattern: `(arn:(aws[a-zA-Z-]*)?:lambda:)?([a-z]{2}(-gov)?-[a-z]+-\d{1}:)?(\d{12}:)?(function:)?([a-zA-Z0-9-_]+)(:(\$LATEST|[a-zA-Z0-9-_]+))?` 

 ** [Qualifier](#API_AddPermission_RequestSyntax) **   <a name="SSS-AddPermission-request-Qualifier"></a>
Specify a version or alias to add permissions to a published version of the function\.  
Length Constraints: Minimum length of 1\. Maximum length of 128\.  
Pattern: `(|[a-zA-Z0-9$_-]+)` 

## Request Body<a name="API_AddPermission_RequestBody"></a>

The request accepts the following data in JSON format\.

 ** [Action](#API_AddPermission_RequestSyntax) **   <a name="SSS-AddPermission-request-Action"></a>
The action that the principal can use on the function\. For example, `lambda:InvokeFunction` or `lambda:GetFunction`\.  
Type: String  
Pattern: `(lambda:[*]|lambda:[a-zA-Z]+|[*])`   
Required: Yes

 ** [EventSourceToken](#API_AddPermission_RequestSyntax) **   <a name="SSS-AddPermission-request-EventSourceToken"></a>
For Alexa Smart Home functions, a token that must be supplied by the invoker\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 256\.  
Pattern: `[a-zA-Z0-9._\-]+`   
Required: No

 ** [Principal](#API_AddPermission_RequestSyntax) **   <a name="SSS-AddPermission-request-Principal"></a>
The AWS service or account that invokes the function\. If you specify a service, use `SourceArn` or `SourceAccount` to limit who can invoke the function through that service\.  
Type: String  
Pattern: `.*`   
Required: Yes

 ** [RevisionId](#API_AddPermission_RequestSyntax) **   <a name="SSS-AddPermission-request-RevisionId"></a>
Only update the policy if the revision ID matches the ID that's specified\. Use this option to avoid modifying a policy that has changed since you last read it\.  
Type: String  
Required: No

 ** [SourceAccount](#API_AddPermission_RequestSyntax) **   <a name="SSS-AddPermission-request-SourceAccount"></a>
For AWS services, the ID of the account that owns the resource\. Use this instead of `SourceArn` to grant permission to resources that are owned by another account \(for example, all of an account's Amazon S3 buckets\)\. Or use it together with `SourceArn` to ensure that the resource is owned by the specified account\. For example, an Amazon S3 bucket could be deleted by its owner and recreated by another account\.  
Type: String  
Pattern: `\d{12}`   
Required: No

 ** [SourceArn](#API_AddPermission_RequestSyntax) **   <a name="SSS-AddPermission-request-SourceArn"></a>
For AWS services, the ARN of the AWS resource that invokes the function\. For example, an Amazon S3 bucket or Amazon SNS topic\.  
Type: String  
Pattern: `arn:(aws[a-zA-Z0-9-]*):([a-zA-Z0-9\-])+:([a-z]{2}(-gov)?-[a-z]+-\d{1})?:(\d{12})?:(.*)`   
Required: No

 ** [StatementId](#API_AddPermission_RequestSyntax) **   <a name="SSS-AddPermission-request-StatementId"></a>
A statement identifier that differentiates the statement from others in the same policy\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `([a-zA-Z0-9-_]+)`   
Required: Yes

## Response Syntax<a name="API_AddPermission_ResponseSyntax"></a>

```
HTTP/1.1 201
Content-type: application/json

{
   "[Statement](#SSS-AddPermission-response-Statement)": "string"
}
```

## Response Elements<a name="API_AddPermission_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 201 response\.

The following data is returned in JSON format by the service\.

 ** [Statement](#API_AddPermission_ResponseSyntax) **   <a name="SSS-AddPermission-response-Statement"></a>
The permission statement that's added to the function policy\.  
Type: String

## Errors<a name="API_AddPermission_Errors"></a>

 **InvalidParameterValueException**   
One of the parameters in the request is invalid\. For example, if you provided an IAM role for AWS Lambda to assume in the `CreateFunction` or the `UpdateFunctionConfiguration` API, that AWS Lambda is unable to assume you will get this exception\.  
HTTP Status Code: 400

 **PolicyLengthExceededException**   
The permissions policy for the resource is too large\. [Learn more](https://docs.aws.amazon.com/lambda/latest/dg/limits.html)   
HTTP Status Code: 400

 **PreconditionFailedException**   
The RevisionId provided does not match the latest RevisionId for the Lambda function or alias\. Call the `GetFunction` or the `GetAlias` API to retrieve the latest RevisionId for your resource\.  
HTTP Status Code: 412

 **ResourceConflictException**   
The resource already exists\.  
HTTP Status Code: 409

 **ResourceNotFoundException**   
The resource \(for example, a Lambda function or access policy statement\) specified in the request does not exist\.  
HTTP Status Code: 404

 **ServiceException**   
The AWS Lambda service encountered an internal error\.  
HTTP Status Code: 500

 **TooManyRequestsException**   
Request throughput limit exceeded\.  
HTTP Status Code: 429

## See Also<a name="API_AddPermission_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lambda-2015-03-31/AddPermission) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lambda-2015-03-31/AddPermission) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lambda-2015-03-31/AddPermission) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lambda-2015-03-31/AddPermission) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lambda-2015-03-31/AddPermission) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lambda-2015-03-31/AddPermission) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lambda-2015-03-31/AddPermission) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lambda-2015-03-31/AddPermission) 
+  [AWS SDK for Ruby V2](https://docs.aws.amazon.com/goto/SdkForRubyV2/lambda-2015-03-31/AddPermission) 