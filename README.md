# Azure-Deployment
Templates containing the permission to be assigned to the user for public azure resource Deployment.

Automation for Role Definition and Role Assignment Template in azure portal can be done with 2 options: (Permission to run these deployment - mostly preferred by admin)
1.  Template Specs Deployment --  For internal/organization purpose
	1. Allows ARM/Bicep template for resource creation with azure resource group.
2. Azure Deploy -- For public use case
	1. Bicep/ARM Template can be hosted to public git repo, terraform, azure blob storage
		a. Github - Compile the bicep using azure cli and store to public git repo into json format
			i. az bicep build --file <file-name>.bicep
			ii. Copy the json file raw url from the git
				1) https://raw.githubusercontent.com/PravarChaurasia/Azure-Deployment/refs/heads/main/netapp-role-deploy.json
			iii. Use deeplink generator tool -- Use AI tool (google) to avoid explicit encoding and generation
				1) Encode the github file raw url
				2) https://portal.azure.com/#create/Microsoft.Template/uri/ with your URL-encoded template URL. 
					a) https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FPravarChaurasia%2FAzure-Deployment%2Frefs%2Fheads%2Fmain%2Fnetapp-role-deploy.json
			iv. Open the above link
				1) Login to azure with specific tenant switch available and opting the subscrpition
		b. Azure blob storage -- Public to store the bicep
Terraform![Uploading image.png…]()

# Aws-Deployment

**CloudFormation Stack Deployment:** The user clicks your deep link to create the stack.
**EventBridge Monitoring:** An EventBridge rule listens for stack events on the default event bus.
**Trigger: **When the stack status changes to CREATE_COMPLETE, EventBridge triggers the Lambda function.
**Lambda Execution:** The Lambda function uses the AWS SDK (Boto3/Node.js) to describe the stack, extract the RoleARN from the Outputs, and proceed with your authentication logic.
