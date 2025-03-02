AWS Generative AI Blog Project
Overview
This project uses AWS Bedrock and AWS Lambda to generate AI-powered blog content. The application takes a topic as input, generates a blog using AWS Bedrock, and stores the result in an Amazon S3 bucket. It is triggered via API Gateway, and logs are available in CloudWatch.

Technologies Used
AWS Bedrock – For AI-based blog generation (Meta Llama 3 70B model)
AWS Lambda – To handle API requests and execute blog generation
Amazon S3 – For storing generated blog content
Amazon API Gateway – To trigger the Lambda function via HTTP requests
Amazon CloudWatch – For logging function execution
Python – Backend processing
Boto3 – AWS SDK for Python
Installation & Setup
Prerequisites
An AWS account
AWS CLI installed and configured
Python 3.8+ installed
IAM permissions for AWS Bedrock, Lambda, S3, and API Gateway
Steps to Set Up
1. Clone the Repository
sh
Copy
Edit
git clone <your-repository-url>  
cd aws-generative-ai-blog  
2. Set Up a Virtual Environment (Optional, but recommended)
sh
Copy
Edit
python -m venv venv  
venv\Scripts\activate  # On Linux/macOS use: source venv/bin/activate  
3. Install Dependencies
sh
Copy
Edit
pip install boto3 botocore  
4. Configure AWS Credentials
sh
Copy
Edit
aws configure  
5. Deploy Lambda Function
Create a ZIP package for deployment:

sh
Copy
Edit
zip -r lambda_function.zip app.py  
Deploy to AWS Lambda:

sh
Copy
Edit
aws lambda create-function --function-name BlogGenerator --runtime python3.8 \
   --role <your-iam-role-arn> --handler app.lambda_handler \
   --zip-file fileb://lambda_function.zip  
6. Set Up API Gateway
Go to AWS API Gateway and create a new REST API
Create a POST method and link it to your Lambda function
Deploy the API and note down the invoke URL
Usage Guide
Step 1: Send a Request via API Gateway
Make a POST request to your API Gateway URL:

sh
Copy
Edit
curl -X POST https://your-api-gateway-url.com/generate \
     -H "Content-Type: application/json" \
     -d '{"blog_topic": "AI in Healthcare"}'  
Step 2: Check Logs in CloudWatch
To verify the function execution, check CloudWatch logs:

Go to AWS CloudWatch → Logs
Find the log group for your Lambda function (/aws/lambda/BlogGenerator)
Open the latest log stream to view execution details
Step 3: Retrieve Generated Blog from S3
Check your Amazon S3 bucket for the generated blog:

sh
Copy
Edit
aws s3 ls s3://genaibedrockdemo/blog-output/  
To download the latest blog:

sh
Copy
Edit
aws s3 cp s3://genaibedrockdemo/blog-output/<file-name>.txt .  
Example Prompts & Responses
Prompt:
"Write a blog post about the impact of AI in the education sector."

Response:
"Artificial Intelligence (AI) is transforming the education sector by personalizing learning experiences, automating administrative tasks, and enabling new teaching methodologies..."

Future Enhancements
Add a front-end UI for blog topic selection
Enable multi-model support for different content styles
Implement logging and monitoring improvements
Contributing
Contributions are welcome! Please submit a pull request with your changes.

Contact
For any questions or issues, feel free to reach out via:

GitHub Issues: Open an issue in this repository
Email: [sree68222@gmail.com] 
