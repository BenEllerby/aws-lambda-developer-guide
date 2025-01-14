# AWS Lambda Features<a name="gettingstarted-features"></a>

AWS Lambda provides a management console and API for managing and invoking functions\. It provides runtimes that support a standard set of features so that you can easily switch between languages and frameworks depending on your needs\. In addition to functions, you can also create versions, aliases, layers and custom runtimes\.

**Topics**
+ [Programming Model](#gettingstarted-features-programmingmodel)
+ [Scaling](#gettingstarted-features-scaling)
+ [Deployment Package](#gettingstarted-features-package)
+ [Layers](#gettingstarted-features-layers)

## Programming Model<a name="gettingstarted-features-programmingmodel"></a>

Authoring specifics vary between runtimes, but all runtimes share a common programming model that defines the interface between your code and the runtime code\. You tell the runtime which method to run by defining a **handler** in the function configuration, and the runtime runs that method\. The runtime passes in objects to the handler that contain the invocation **event** and the **context**, such as the function name and request ID\.

The runtime captures **logging** output from your function and sends it to Amazon CloudWatch Logs\. You can use the standard logging functionality of your programming language\. If your function throws an **error**, the runtime returns that error to the client\.

**Note**  
Logging is subject to [CloudWatch Logs limits](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/cloudwatch_limits_cwl.html)\. Log data can be lost due to throttling or, in some cases, when the [execution context](running-lambda-code.md) is terminated\.

If your function exits without error, the runtime sends it another event\. The function's class stays in memory, so clients and variables declared outside of the handler method can be reused\. Your function also has access to local storage in the `/tmp` directory\.

Lambda scales your function by running additional instances of it as demand increases, and terminating instances as demand decreases\. Unless noted otherwise, incoming requests may be processed out of order or concurrently\. Store your application's state in other services, and don't rely on instances of your function being long lived\. Use local storage and class\-level objects to increase performance, but keep the size of your deployment package and the amount of data that you transfer onto the execution environment to a minimum\.

For a hands\-on introduction to the programming model in your preferred programming language, see the following chapters\.
+ [Building Lambda Functions with Node\.js](programming-model.md)
+ [Building Lambda Functions with Python](python-programming-model.md)
+ [Building Lambda Functions with Ruby](lambda-ruby.md)
+ [Building Lambda Functions with Java](java-programming-model.md)
+ [Building Lambda Functions with Go](go-programming-model.md)
+ [Building Lambda Functions with C\#](dotnet-programming-model.md)
+ [Building Lambda Functions with PowerShell](powershell-programming-model.md)

## Scaling<a name="gettingstarted-features-scaling"></a>

Lambda manages the infrastructure that runs your code, scaling automatically in response to incoming requests\. When your function is invoked more quickly than a single instance of your function can process events, Lambda scales up by running additional instances\. When traffic subsides, inactive instances are frozen or terminated\. You only pay for the time that your function code is actually processing events\.

For more information, see [AWS Lambda Function Scaling](scaling.md)

## Deployment Package<a name="gettingstarted-features-package"></a>

Your function's code consists of scripts or compiled programs and their dependencies\. When you author functions in the Lambda console or a toolkit, the client creates a ZIP archive of your code called a deployment package\. The client then sends the package to the Lambda service\. When you manage functions with the Lambda API, command line tools, or SDKs, you create the deployment package\. You also need to create a deployment package manually for compiled languages and to add dependencies to your function\.

For language specific instructions, see the following topics\.
+  [AWS Lambda Deployment Package in Node\.js](nodejs-create-deployment-pkg.md) 
+  [AWS Lambda Deployment Package in Python](lambda-python-how-to-create-deployment-package.md) 
+  [AWS Lambda Deployment Package in Ruby](ruby-package.md) 
+  [AWS Lambda Deployment Package in Java](lambda-java-how-to-create-deployment-package.md) 
+  [AWS Lambda Deployment Package in Go](lambda-go-how-to-create-deployment-package.md) 
+  [AWS Lambda Deployment Package in C\#](lambda-dotnet-how-to-create-deployment-package.md) 
+  [AWS Lambda Deployment Package in PowerShell](lambda-powershell-how-to-create-deployment-package.md) 

## Layers<a name="gettingstarted-features-layers"></a>

Lambda layers are a distribution mechanism for libraries, custom runtimes, and other function dependencies\. Layers let you manage your in\-development function code independently from the unchanging code and resources that it uses\. You can configure your function to use layers that you create, layers provided by AWS, or layers from other AWS customers\.

For more information, see [AWS Lambda Layers](configuration-layers.md)\.