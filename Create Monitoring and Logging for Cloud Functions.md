
## CHANGE REGION FROM LAB


```
REGION=
```
### Task 1
```
export PROJECT_ID=$GOOGLE_CLOUD_PROJECT
gcloud services enable \
  artifactregistry.googleapis.com \
  cloudfunctions.googleapis.com \
  cloudbuild.googleapis.com \
  eventarc.googleapis.com \
  run.googleapis.com \
  logging.googleapis.com \
  pubsub.googleapis.com


gcloud config set compute/region $REGION
mkdir gcf_hello_world
cd gcf_hello_world
touch index.js
tee -a index.js <<EOF
/**
 * Responds to any HTTP request.
 *
 * @param {!express:Request} req HTTP request context.
 * @param {!express:Response} res HTTP response context.
 */
exports.helloWorld = (req, res) => {
  let message = req.query.message || req.body.message || 'Hello World!';
  res.status(200).send(message);
};
EOF

tee -a package.json <<EOF
{
  "name": "sample-http",
  "version": "0.0.1"
}
EOF
```
### Task 2
```
gcloud functions deploy helloWorld \
  --runtime nodejs20 \
  --entry-point helloWorld \
  --source . \
  --region $REGION \
  --trigger-http \
  --allow-unauthenticated \
  --max-instances 5
```

```
gcloud functions describe helloWorld --region $REGION
```

```
gcloud logging metrics create CloudFunctionLatency-Logs --description="Number of high severity log entries" \
--log-filter='resource.type="cloud_function"
resource.labels.function_name="helloWorld"
logName="projects/$GOOGLE_CLOUD_PROJECT/logs/cloudfunctions.googleapis.com%2Fcloud-functions"'
```
