#  Understanding API Calls — Class Session Summary

This file summarizes key concepts covered in the two-part YouTube video tutorial on API usage and development. Based entirely on the provided class recording and transcript.

---

## 1.  What is an API call (in your own words)?

An **API call** is when your program sends a request to an external service using a URL (called an endpoint) and gets a response back — often in JSON. Think of it like asking a website to do something on your behalf.

For example, using `curl` to access `google.com` is technically an API call. If the request is valid, the server responds with a `200` status and some data.

In the video, the instructor showed how to:
```bash
curl www.google.com
```
This is making a simple API call. Similarly, we made API calls to OpenAI’s endpoint using Python and `curl`.

---

## 2.  What is an example we discussed to create an API call *locally*?

We created a local API using **FastAPI** and ran it on `localhost:8000`.

Basic example from the video:
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

This was executed with:
```bash
uvicorn main:app --reload
```

We accessed it by visiting:
```
http://127.0.0.1:8000/items/5?q=blah
```
The response was:
```json
{"item_id": 5, "q": "blah"}
```

---

## 3.  What is an example we discussed to create an API call *on the cloud*?

We used **AWS Lambda** + **API Gateway**:

- A Python Lambda function was created and deployed.
- The handler looked like this:
```python
def lambda_handler(event, context):
    body = json.loads(event.get("body", "{}"))
    value = body.get("key1", "")
    return {
        "statusCode": 200,
        "body": json.dumps({"response": f"Received: {value}"})
    }
```
- We connected it to an API Gateway endpoint.
- After deployment, anyone could `POST` to the endpoint with a JSON payload like:
```json
{"key1": "hello"}
```
And receive a response like:
```json
{"response": "Received: hello"}
```

---

## 4.  What is the difference between FastAPI and creating API from AWS Gateway?

| FastAPI (Local) | AWS Lambda + API Gateway (Cloud) |
|-----------------|----------------------------------|
| Runs on your own machine | Runs on the cloud, publicly accessible |
| Great for testing and dev work | Great for production, real-world access |
| You control the server | AWS manages infrastructure |
| Only accessible from your machine | Can be accessed by anyone (if public) |

FastAPI is quick and flexible for prototyping. AWS Gateway is scalable and production-ready for real applications.

---

## 5.  In your own words, what are the main steps to create an API call on AWS Gateway?

As shown in the video:

1. **Create a Lambda function** in Python (e.g., `lambda_handler`).
2. Write logic that processes `event['body']` as JSON.
3. Test the function to ensure it responds correctly.
4. Go to **API Gateway** and create a **REST API**.
5. Connect your Lambda function to the API Gateway as a **trigger**.
6. Define method type (usually `POST`) and deploy to a new stage (e.g., `dev`).
7. You now get a URL you can `curl` or use from your app:
```bash
curl -X POST https://your-api-id.amazonaws.com/dev/endpoint \
-H "Content-Type: application/json" \
-d '{"key1": "hello"}'
```

---

## 6.  Professionally in the industry, how do developers ship products from one team to another? What's the usage of API here?

As mentioned in the video:

APIs are like **contracts** between teams. One team (like backend or ML) creates an API, and another team (like frontend or mobile) uses it without needing to know what’s inside.

> “You don’t necessarily see what the function is doing in the backend... you just send the request and get the response.”

APIs make it possible to:
- Share services between teams.
- Keep projects modular.
- Scale systems independently.

Whether it’s a machine learning model or a database service, developers expose logic through APIs so other teams can easily integrate them into larger systems.

