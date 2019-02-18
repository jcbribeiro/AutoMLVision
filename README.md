# AutoMLVision

### Setting Up

### 1. Go to the Google Cloud Platform Console (https://console.cloud.google.com/) and activate your free trial to get 300$ credit to explore Google Cloud products.

*Important note:* Google asks for your credit card information when you sign up for the free trial to: verify your identity; distinguish actual customers from robots. Even though you set up a billing account, you won't be charged unless you upgrade to a paid account. You might notice a $0-1 transaction from Google after you sign up. This transaction: is an authorization request to validate your account, not a permanent charge; might be converted to local currency by your bank; might appear on your statement for up to a month. Contact your bank if you have questions about the authorization.
	
Tip: if do now own a credit card or don't feel comfortable sharing its information, you may create a "virtual" credit card with a small validity and limit using, for example, the "MB Way" app (wwww.mbway.pt)
	
More info: https://cloud.google.com/free/docs/gcp-free-tier

### 2. Create a Project. 

Go to the Manage Resources page of the Google Cloud Platform Console (https://console.cloud.google.com/cloud-resource-manager) and create a new project. 

Name it "workshop-vision", for example.

### 3. Make sure that Billing is enabled for your project. 

Go to the Google Cloud Platform Console (https://console.cloud.google.com/); open the console's left side menu; and select "Billing". You should already have a billing account (containing the free credits you were just awarded), and your project should be linked to this billing account.

More info: https://cloud.google.com/billing/docs/how-to/modify-project#enable_billing_for_a_project

### 4. Enable the necessary APIs for your project.

To enable the AutoML Vision APIs go to: https://console.cloud.google.com/flows/enableapi?apiid=storage-component.googleapis.com,automl.googleapis.com,storage-api.googleapis.com&redirect=https://console.cloud.google.com

### 5. Create a Service Account, and download a Key File.

Go to the Google Cloud Platform's APIs & Services page - Credentials tab (https://console.cloud.google.com/apis/credentials), click "Create credentials", and select "Service Account Key".

Name your service account "my-service-account", set the Role to "AutoML Admin", and set the Key type to JSON.

Save the generated Private Key File in a secure place. You'll need it later!

### 6. Add your new Service Account to the AutoML Editor IAM role.

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

### 7. Finish Setup and make sure everything is ok.

Go to AutoML Vision's Homepage: https://cloud.google.com/automl/ui/vision. You will be prompted to finish setting up you Google Cloud project. Click the "Set Up Now Button" and, if everything goes well, you will proceed automatically to AutoML Vision's Dataset creation page.
