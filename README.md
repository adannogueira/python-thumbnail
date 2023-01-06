<!--
title: 'Python Thumbnail'
description: 'This small project demonstrates how to deploy a Python function running on AWS Lambda using the traditional Serverless Framework.'
layout: Doc
framework: v3
platform: AWS
language: python
priority: 2
authorLink: 'https://github.com/adannogueira'
authorName: 'Adan Nogueira'
-->


# Serverless Framework AWS Python Thumbnail

This small project demonstrates how to deploy Python functions running on AWS Lambda using the traditional Serverless Framework. The deployed functions will show how to trigger a lambda on an s3 event, use lambdas as an API Gateway to list saved thumbnails, get a specific thumnail and also delete a thumbnail.

## Usage

### Deployment

In order to deploy the application, you need to run the following command:

```
$ serverless deploy
```

After running deploy, you should see output similar to:

```bash
Deploying python-thumbnail to stage dev (us-east-1)

✔ Service deployed to stack python-thumbnail-dev (97s)

endpoints:                                                                                                                                    
  GET - https://xxxxx.execute-api.us-east-1.amazonaws.com/dev/images/all
  GET - https://xxxxx.execute-api.us-east-1.amazonaws.com/dev/images/get/{id}
  DELETE - https://xxxxx.execute-api.us-east-1.amazonaws.com/dev/images/delete/{id}
functions:
  s3_thumbnail_generator: python-thumbnail-dev-s3_thumbnail_generator (2.1 MB)                                                                
  list: python-thumbnail-dev-list (2.1 MB)
  get: python-thumbnail-dev-get (2.1 MB)
  delete: python-thumbnail-dev-delete (2.1 MB)
```

### Invocation

After successful deployment, you can invoke the deployed function by using the following command:

```bash
serverless invoke --function s3_get_thumbnail_urls
```

Which should result in response similar to the following:

```json
{
    "statusCode": 200,
    "headers": {"Content-Type": "application/json"},
    "body": {
      "createdAt": "2022-12-29 11:54:14.003456",
      "id": "7e06fef0-4927-4f5e-9394-5351ac45d389",
      "url": "https://s3.amazonaws.com/python-thumbs/modelo_thumbnail.png",
      "approxReducedSize": "1.62869 KB",
      "updatedAt": "2022-12-29 11:54:14.003477"
    }
}
```

### Local development

You can invoke your function locally by using the following command:

```bash
serverless invoke local --function s3_get_thumbnail_urls
```

### Bundling dependencies

The application shows how to add dependency layers to the lambda functions, adding the plugin `serverless-python-requirements`. You can set it up by running the following command:

```bash
serverless plugin install -n serverless-python-requirements
```
