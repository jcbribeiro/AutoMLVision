# AutoMLVision

## 1. Setting Up

### 1.1. Go to the Google Cloud Platform Console (https://console.cloud.google.com/) and activate your free trial to get 300$ credit to explore Google Cloud products.

*Important note:* Google asks for your credit card information when you sign up for the free trial to: verify your identity; distinguish actual customers from robots. Even though you set up a billing account, you won't be charged unless you upgrade to a paid account. You might notice a $0-1 transaction from Google after you sign up. This transaction: is an authorization request to validate your account, not a permanent charge; might be converted to local currency by your bank; might appear on your statement for up to a month. Contact your bank if you have questions about the authorization.
	
Tip: if do now own a credit card or don't feel comfortable sharing its information, you may create a "virtual" credit card with a small validity and limit using, for example, the "MB Way" app (wwww.mbway.pt)
	
More info: https://cloud.google.com/free/docs/gcp-free-tier

### 1.2. Create a Project. 

Go to the Manage Resources page of the Google Cloud Platform Console (https://console.cloud.google.com/cloud-resource-manager) and create a new project. 

Name it "workshop-vision", for example.

### 1.3. Make sure that Billing is enabled for your project. 

Go to the Google Cloud Platform Console (https://console.cloud.google.com/); open the console's left side menu; and select "Billing". You should already have a billing account (containing the free credits you were just awarded), and your project should be linked to this billing account.

More info: https://cloud.google.com/billing/docs/how-to/modify-project#enable_billing_for_a_project

### 1.4. Enable the necessary APIs for your project.

To enable the AutoML Vision APIs go to: https://console.cloud.google.com/flows/enableapi?apiid=storage-component.googleapis.com,automl.googleapis.com,storage-api.googleapis.com&redirect=https://console.cloud.google.com

### 1.5. Create a Service Account, and download a Key File.

Go to the Google Cloud Platform's APIs & Services page - Credentials tab (https://console.cloud.google.com/apis/credentials), click "Create credentials", and select "Service Account Key".

Name your service account "my-service-account", set the Role to "AutoML Admin", and set the Key type to JSON.

Save the generated Private Key File in a secure place. You'll need it later!

### 1.6. Add your new Service Account to the AutoML Editor IAM role.

Go to the Google Cloud Platform Console (https://console.cloud.google.com/) and click on the "Activate Cloud Shell" icon in top right hand corner of the header bar (use the Chrome browser if possible).

Enter the following commands into the Cloud Shell. Consider the Template below, and replace 
* project-id with the name of your GCP project (for example, "workshop-vision")
* service-account-name with the name of your new service account (for example, "my-service-account")
* your email as the user (for example, "workshopgdgleiria@gmail.com")

#### TEMPLATE
```
gcloud projects add-iam-policy-binding project-id --member="user:your-userid@your-domain" --role="roles/automl.admin"
gcloud projects add-iam-policy-binding project-id --member=serviceAccount:service-account-name@project-id.iam.gserviceaccount.com --role="roles/automl.editor"
```

#### EXAMPLE
```
gcloud projects add-iam-policy-binding workshop-vision --member="user:workshopgdgleiria@gmail.com" --role="roles/automl.admin"
gcloud projects add-iam-policy-binding workshop-vision --member=serviceAccount:my-service-account@workshop-vision.iam.gserviceaccount.com  --role="roles/automl.editor"
```

### 1.7. Finish Setup and make sure everything is ok.

Go to AutoML Vision's Homepage: https://cloud.google.com/automl/ui/vision

You will be prompted to finish setting up you Google Cloud project. Click the "Set Up Now Button" and, if everything goes well, you will proceed automatically to AutoML Vision's Dataset creation page.


## 3. Create an AutoML Vision-enabled Android app

### 3.1. Download the Sample Android Studio Project.

Download and open the Sample AutoML Vision Projet available at: https://github.com/jcbribeiro/AutoMLVision

### 3.2. Copy the Key File to you Android Studio project.

Find the Private Key File you you downloaded during the Setting Up process (step 5), and rename it to: ```workshopvision.json```

Copy the ```workshopvision.json``` file to the ```/res/raw``` folder of your Android Studio project.

### 3.3. Define the necessary constants in the ```MainActivity.java``` File.

Set the values of the ```COMPUTE_REGION```, ```PROJECT_ID``` and ```MODEL_ID``` in accordance to the information contained in the URL provided by the AutoML Vision's Website ("Predict" tab, under "Execute the request"). For example, for the following URL:

```
https://automl.googleapis.com/v1beta1/projects/workshop-vision/locations/us-central1/models/ICN293500301081240869:predict
```

These constants would be defined as follows:

```
private static final String COMPUTE_REGION = "us-central1";
private static final String PROJECT_ID = "workshop-vision";
private static final String MODEL_ID = "ICN293500301081240869";
```

Also, define the ```SCORE_THRESHOLD``` and the ```JSON_RAW_RESOURCE_ID``` in order to set the score threshold and the ID of the json Key File as follows:

```
private static final String SCORE_THRESHOLD = "0.7"
private static final Integer JSON_RAW_RESOURCE_ID = R.raw.workshopvision;
```
