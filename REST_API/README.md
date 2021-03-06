# Steps for Setting Up REST API with API Gateway and Lambda Function
## REST API Accepts Binary Images (JPG) and Returns JSON Payload

The following blog post was a big help in setting up the SageMaker endpoint as a REST API, able to accept binary JPG files: 

[**AWS Compute Blog**: Binary Support for API Integrations with Amazon API Gateway](https://aws.amazon.com/blogs/compute/binary-support-for-api-integrations-with-amazon-api-gateway/) (Accessed on 4/24/2020)

### Create Resource and Method
1. Go to AWS API Gateway. Select **Create API**

![Create API](images/1_create_api.png)

2. Select **REST API**. Click Build.

3. Keep Defaults. Add Name and description.

4. Go to **Resources** (far left bar, under API). Make Sure **/** is highlighted in the **Resources** banner.

![Create Resource](images/2_create_resource.png)

5. Select **Actions > Create Resource**.
 
6. Enter Resource Name. Maintain all other defaults.

7. Ensure **Resources** is selected under __API: {Resource Name}__. In **Resources** left side banner ensure **/{Resource Name}** is highligthed. Select **Actions > Create Method**.

8. Select **POST** from drop-down. Click check mark.

### Configure Method
1. With **POST** highlighted, select:
* Integration type: Lambda Function
* Use Lambda Proxy Integration: NOT checked
* Lambda Region: Ensure region is consistent with Lambda we are connecting the API to.
* Lambda Function: Enter lambda function name
* Use Default Timeout: Remain checked.
* Clcik Save. Select OK to give API Gateway permission to invoke Lambda Function.

![Configure Method](images/3_configure_method.png)

2. Click on Integration Request

![Integration Request](images/4_integration_request.png)

3. Click **Mapping Templates** so that drop-down content is visible.

4. For **Request body passthrough**, select **When there are no templates defined (recommended)**.

5. Under Content-Type, click **Add mapping template**.

6. Add **image/jpg**. Click check mark.

7. Scroll Down. Enter the following in the empty template box.

![Mapping Templates](images/5-mapping_templates.png)

8. Select Save.

### Deploy API
1. Return to **API/Resources** page. Ensure under **Resources** side banner the method **POST** is highlighted. 

2. Click Actions. Select Deploy API.

3. For Deployment Stage, select **New Stage**.

4. Add **Stage Name**. Click **Deploy**.

![Deploy](images/6-deploy.png)

### API Request Tests
For API testing, we used Postman

1. Open Postman

2. Create new Request.

3. Set Request method to **POST**.

4. Insert API URL in the **Enter request URL** entry.

* The API URL can be found be going to **API > Stages** and selecting the **POST** under **{Resource Name}**. The URL will be listed as **Invoke URL** in the main windown.

![Invoke URL](images/7-invoke_url.png)

5. Go to **Headers**. Add the following header:
* KEY: Content-Type
* Value: image/jpg

![Postman Headers](8-postman_headers.png)

6. Go to **Body**. Select **binary**. Add a JPG image from your local machine.

7. Click **Send**. If established correctly, the expected return will be received as a JSON.
