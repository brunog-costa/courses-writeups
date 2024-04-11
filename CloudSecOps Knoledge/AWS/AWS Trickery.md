
Read data from S3 with Python using lambda code:

```python
import json, boto3
s3 = boto3.resource("s3").Bucket("bucket")
json.load_s3 = lambda f: json.load(s3.Object(key=f).get()["Body"])
json.dump_s3 = lambda obj, f: s3.Object(key=f).put(Body=json.dumps(obj))
```
