
# Project 2: API Development & Integration – Practical Data Science



## 1. What is an API and how does it work in the context of OpenAI?

An API (Application Programming Interface) acts as a bridge between different software applications. In the context of OpenAI, it allows developers to send prompts and receive model-generated responses programmatically. For instance, when using `curl` or a Python client like `openai`, you send a request (payload) to a specific endpoint, such as `https://api.openai.com/v1/chat/completions`, and get back a structured response.

Key aspects include:
- Sending queries as structured JSON payloads.
- Authenticating with an API key.
- Receiving JSON responses with content like text, images, or classification results.

## 2. What are common issues when making API calls and how do you troubleshoot them?

Common issues and their solutions include:
- **Missing packages**: Use `!pip install openai` to ensure dependencies are available.
- **Invalid or missing API keys**: The key must be securely added and correctly referenced, either via environment variables or notebooks (e.g., `os.environ["OPENAI_API_KEY"]`).
- **Rate limits and billing**: Monitor usage and token limits on the OpenAI dashboard. Running out of tokens or credit can cause calls to fail.
- **Free token restrictions**: Some accounts may not have active free credits; ensure you understand your billing setup.

Always check:
- Status codes (e.g., 200 for success).
- Error messages in the JSON response.
- Key structure (`choices[0].message.content` for completion responses).

## 3. How do you securely store and access your OpenAI API key in a notebook environment like Google Colab?

To manage secrets securely:
- Store keys using Colab’s built-in secret management under the “key” tab.
- Use the secret in code like this:
  ```python
  import os
  os.environ["OPENAI_API_KEY"] = user_data.get("my_key")
  ```
- Avoid hardcoding keys in code directly.
- Do not share or expose your notebook containing the actual API key value.

## 4. How can you create your own API using FastAPI locally?

Steps to create a local API:
1. Create a virtual environment: `python -m venv venv && source venv/bin/activate`
2. Install FastAPI and Uvicorn: `pip install fast api uvicorn`
3. Create a `main.py`:
   ```python
   from fastapi import FastAPI

   app = FastAPI()

   @app.get("/")
   def read_root():
       return {"Hello": "World"}

   @app.get("/items/{item_id}")
   def read_item(item_id: int, q: str = None):
       return {"item_id": item_id, "q": q}
   ```
4. Run with: `uvicorn main:app --reload`
5. Access it at `http://127.0.0.1:8000`

This is your own mini web server serving API endpoints.

## 5. How do you deploy an API on AWS using Lambda and API Gateway?

Deploying on AWS involves:
1. **Lambda Function**:
   - Write a handler in Python (e.g., `def lambda_handler(event, context):`)
   - Add logic to extract input, process it, and return JSON.

2. **Test Functionality**: Invoke with sample events to ensure it runs.

3. **API Gateway**:
   - Attach your Lambda to an HTTP endpoint.
   - Choose `REST API` or `HTTP API` depending on flexibility vs simplicity.
   - Ensure the payload format is correct (use `json.loads(event["body"])`).

4. **Deploy Stage**: Create a stage (e.g., "dev") and deploy the API.

5. **Test Public Endpoint**: Use `curl` or any browser to test the endpoint with payloads.

## 6. What is the difference between frontend and backend when working with APIs?

- **Frontend**: The interface or URL where a user sends data. This could be a browser, mobile app, or `curl` command sending a request to the API.
- **Backend**: The server or function (like a Lambda or FastAPI script) that processes incoming data and responds with results (e.g., JSON).

In the FastAPI demo:
- `http://localhost:8000/items/5?q=example` is the frontend.
- `main.py` with the logic to return the result is the backend.

In the AWS Lambda demo:
- The API Gateway URL is the frontend.
- The Lambda function with `event['body']` parsing is the backend.



