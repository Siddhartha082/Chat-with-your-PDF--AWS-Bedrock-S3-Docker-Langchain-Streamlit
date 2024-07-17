# Chat With PDF - Generative AI Application
## Built Using Amazon Bedrock, Langchain, Python, Docker, Amazon S3
## Models used:
    Amazon Titan Embedding G1 - Text
    Anthropic Claude 2.1

# PDF .. Loaded in this folder- https://www.versusarthritis.org/media/22726/what-is-arthritis-information-booklet.pdf

we will build a CHATBOT like application with AWS Amazon Bedrock, docker, python, Langchain, and Streamlit. We will use Retrieval-Augmented generation concept to provide context to the Large Language model along with user query to generate response from our Knowledgebase
I will demonstrate the following: - 
Architecture of the applications - Build 2 applications (ADMIN and USER) and create DOCKER images – 
ADMIN Application: - Build Admin Web application where AdminUser can upload the pdf. - The PDF text is split into chunks - Using the Amazon Titan Embedding Model, create the vector representation of the chunks - Using FAISS, save the vector index locally - Upload the index to Amazon S3 bucket (You can use other vector stores like OpenSearch, Pinecone, PgVector etc., but for this demo, I chose cost effective S3) – 

USER Application: - Build User Web application where users can query / chat with the pdf. - At the application start, download the index files from S3 to build local FAISS index (vector store) - Langchain's RetrievalQA, does the following: - Convert the User's query to vector embedding using Amazon Titan Embedding Model (Make sure to use the same model that was used for creating the chunk's embedding on the Admin side) - Do similarity search to the FAISS index and retrieve 5 relevant documents pertaining to the user query to build the context - Using Prompt template, provide the question and context to the Large Language Model. We are using Claude model from Anthropic. - Display the LLM's response to the user.


## Introduction
In this video we will build a CHATBOT like application with AWS Amazon Bedrock, docker, python, Langchain, and Streamlit. We will use Retrieval-Augmented generation concept to provide context to the Large Language model along with user query to generate response from our Knowledgebase.

In this hands-on tutorial, we will demonstrate the following:
- Architecture of the applications
- Build 2 applications (ADMIN and USER) and create DOCKER images


## Architecture
![image info](./Bedrock-ChatWithPdf.png)

## ADMIN Application:
    - Build Admin Web application where AdminUser can upload the pdf.
    - The PDF text is split into chunks
    - Using the Amazon Titan Embedding Model, create the vector representation of the chunks
    - Using FAISS, save the vector index locally
    - Upload the index to Amazon S3 bucket (You can use other vector stores like OpenSearch, Pinecone, PgVector etc., but for this demo, I chose cost effective S3)

### Docker Commands:

  Build Docker Image:
  `docker build -t pdf-reader-admin .`

  Run ADMIN application:
  `docker run -e BUCKET_NAME=<YOUR S3 BUCKET NAME> -v ~/.aws:/root/.aws -p 8083:8083 -it pdf-reader-admin`



## USER Application:
  - Build User Web application where users can query / chat with the pdf.
  - At the application start, download the index files from S3 to build local FAISS index (vector store)
  - Langchain's RetrievalQA, does the following:
     - Convert the User's query to vector embedding using Amazon Titan Embedding Model (Make sure to use the same model that was used for creating the chunk's embedding on the Admin side)
    - Do similarity search to the FAISS index and retrieve 5 relevant documents pertaining to the user query to build the context
    - Using Prompt template, provide the question and context to the Large Language Model. We are using Claude model from Anthropic.
   -  Display the LLM's response to the user.

### Docker Commands:

  Build Docker Image:
  `docker build -t pdf-reader-client .`

  Run ADMIN application:
  `docker run -e BUCKET_NAME=<YOUR S3 BUCKET NAME> -v ~/.aws:/root/.aws -p 8084:8084 -it pdf-reader-client`


#### Note: The docker volume mount is only needed in local. If you are running the container in ECS, or EKS, the iam role is used.

![image](https://github.com/user-attachments/assets/2eb669b9-dcba-4630-b14f-a2557c2a7d93)

![image](https://github.com/user-attachments/assets/a7a0ee05-9838-4915-b316-32ad1916e656)

![image](https://github.com/user-attachments/assets/079930df-76a8-420d-9b23-40064410e033)

![image](https://github.com/user-attachments/assets/c18de805-b015-44bf-be28-6f8d906a7cd4)

# Go to aws console -  s3-  create S3 bucket

![image](https://github.com/user-attachments/assets/cb31d68a-9314-4928-a5c3-15d88993ef8d)

![image](https://github.com/user-attachments/assets/b10faf1d-54e3-4bc4-8cf3-4fae1e3551fa)

![image](https://github.com/user-attachments/assets/7ae8cfbb-b79e-4554-a2e6-643f19c3dfaa)

![image](https://github.com/user-attachments/assets/fec83dc6-bbf3-4df3-88a1-5276e16bdddb)

![image](https://github.com/user-attachments/assets/a66fe9c6-11ad-4aea-8827-02a10fd08e50)

# Admin side

![image](https://github.com/user-attachments/assets/347346c6-526e-40ab-9985-e2bec772274a)

![image](https://github.com/user-attachments/assets/7ae8515d-2e82-4b2d-8ce9-62bfd9099cfd)

![image](https://github.com/user-attachments/assets/55aff578-9988-41d5-b0f0-0527f1d07124)

# user data - app.py

![image](https://github.com/user-attachments/assets/43f210d5-bdc5-41c1-887d-09c0e3ceac53)

![image](https://github.com/user-attachments/assets/a781e8d4-141e-44d5-b732-5d29168f589d)

![image](https://github.com/user-attachments/assets/955deb31-a006-4d48-9a20-258cd208f640)

# Loading APP
![image](https://github.com/user-attachments/assets/e67060e0-28c6-4077-b61c-50c5eceb1689)

# AWS Bedrock Base models

![image](https://github.com/user-attachments/assets/b85c5dcc-7626-4799-9d54-383498e92ef6)

![image](https://github.com/user-attachments/assets/34643fbe-4ec9-4baf-8507-e51e6a25115f)

# O/p Index is Ready

![image](https://github.com/user-attachments/assets/ad83a46e-2d0e-4c21-a50c-b3d41238a113)

![image](https://github.com/user-attachments/assets/d7e9bfe7-a62f-4b24-b741-cd2f5d1b6be9)

# # Ask question Outside  PDF File

![image](https://github.com/user-attachments/assets/0cec5ee5-6baa-44ba-a1bd-24ca7351efcf)




































