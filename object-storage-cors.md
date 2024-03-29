## CORS rules for bucket policy.

#### Template of CORS policy that we set
```json
{
	"CORSRules": [
		{
			"AllowedMethods": [
				"PUT",
				"POST"
			]
			"AllowedOrigins": [
				"DOMAIN_OF_CONSOLE" <!--console which used to send direct request to S3 storage-->
			],
			"AllowedHeaders": [
				"amz-sdk-invocation-id",
				"amz-sdk-request",
				"authorization",
				"content-type",
				"x-amz-content-sha256",
				"x-amz-date",
				"x-amz-user-agent"
			],
			"ExposeHeaders": [
				"ETag" <!-- needed to support multipart upload-->
			],
			"ID": "local.ventuscloud.eu:3000", <!-- this field is used to indicate which console initiates the rule creation and avoid rule duplicating -->
			"MaxAgeSeconds": 3600 <!-- specifies the time that your browser can cache the response for a preflight request 
		}
	],
	"ResultMetadata": {}
}
```

1. Setting this rule is necessary only for direct requests to the S3 bucket. We use it in object uploading
2. When the user tries to upload the object it's looking throw CORS-policy and checks each rule to find the one which will contain all of the necessary elements.
	- If the proper rule is found, the user can proceed to upload the object.
	- If the rule isn't found - it's asking if the user agrees will add a new rule (from the template) to the bucket policy
3. If a rule with our custom ID already exists, the new rule will NOT be appended (!) <!-- point to discuss -->

### In case CORS errors
1. Define the region where this bucket is placed
2. Using Postman send the request to get the actual CORS policy (needs credentials for S3 storage). To authorize - use Cookie 'gosassion', taken from another request to the backend from the console:

<img width="1031" alt="Screenshot 2023-07-31 at 15 21 16" src="https://github.com/iavorskyi/my-docs/assets/67505004/408e3707-a64f-41c5-8246-130425b69935">


`example of request data`

```json 
	path: "https://console.ventuscloud.eu/v1.0/invoke/gotham-eastern-switzerland-compute/method/a346f69b258c410b959ec8abb5b95bc1/buckets/bucket1/cors-policy"
	method: POST
	body:
				{
				"access_key": "7J5UUVtx3jFwful6ytK5fMoH44600jIN",
				"access_secret": "5KrFdP3T7QMGc3K0sy26STr2g9QKRl5F",
				"endpoint": "upper-austria-dev-2.ventuscloud.eu:8080"
				}
```

3. Check if there is a rule that aligns with all requirements:
	- AllowedMethods must contain at least: "PUT" and "POST" or "\*"
	- AllowedOrigins must contain the domain name of the console he uses to upload the file to bucket or wildcard "\*". For example: "console.ventuscloud.eu", "axpo.ventuscloud.eu", "\*"
	- AllowedHeaders must contain all of the headers below:
		- amz-sdk-invocation-id
		- amz-sdk-request
		- authorization
		- content-type
		- x-amz-content-sha256
		- x-amz-date
		- x-amz-user-agent
			or
		- "\*"
	- ExposeHeaders must contain at least: "ETag" or "\*"
3. Check for another rule with the same origin or "\*".  It could cause ambiguity and if this rule does not contain proper elements - the CORS errors could appear. 
4. To solve this issue we can:
	- modify this rule
	- delete the rule which causes the conflict with our one  
	- delete the whole policy and set our policy one more time

`example:`
```json
	path: "https://console.ventuscloud.eu/v1.0/invoke/gotham-eastern-switzerland-compute/method/a346f69b258c410b959ec8abb5b95bc1/buckets/bucket1/cors-policy"
	method: PUT
	body:
				{

					"credentials": {		
						"access_key": "7J5UUVtx3jFwful6ytK5fMoH44600jIQ",
						"access_secret": "5KrFdP3T7QMGc3K0sy26STr2g9QKRl5A",
						"endpoint": "eastern-switzerland.ventuscloud.eu:8080"
					},
					"policy": {
						"CORSRules": [
							{
							"AllowedMethods": [
								"GET",
								"PUT",
							],
							"AllowedOrigins": [
								"*"
							],
							"AllowedHeaders": [
								"*"
							],
							"ExposeHeaders": [
								"*"
							],
							"ID": "122",
							"MaxAgeSeconds": 3200
							}
						]
}
```
