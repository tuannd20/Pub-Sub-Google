# Pub-Sub-Google - Configure Real-time developer notifications
[Cloud Pub/Sub](https://cloud.google.com/pubsub/) is a fully-managed real-time messaging service that you can use to send and receive messages between independent applications. Google Play uses Cloud Pub/Sub to publish push notifications on topics to which you subscribe.
[Docs](https://developer.android.com/google/play/billing/getting-ready#configure-rtdn)

## Table of Contents
1. [**Step 1: Setup Cloud Pub/Sub.**](#step 1: Setup Cloud Pub/Sub.)
2. [**Step 2: Create a Pub/Sub subscription**](#Step 2: Create a Pub/Sub subscription)
3. [**Usage**](#usage)
4. [**Features**](#features)

## Step 1: Setup Cloud Pub/Sub.
Google Cloud Pub/Sub is a scalable message queuing service that ensures asynchronous and reliable messaging between various applications and services. It offers flexibility, supporting one-to-many, many-to-one, and many-to-many communication patterns. This service is designed to track changes in different applications and communicate these updates to diverse systems in real-time.
To begin using Google Cloud Pub/Sub, we must first configure and create a Google Cloud Pub/Sub instance. Here are the steps to do this:
- Login To [Google Cloud Console](https://console.cloud.google.com/)
    ![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/645a1340-65d3-460b-8ea2-94daf32cea50)
- After logging in, locate the Pub/Sub section in the left-hand menu or use the search bar
    ![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/2fed3728-d74a-45c2-ba93-7f7a5c30ce89)
- Next, create a new project. A project provides a logical grouping of resources, making it easier to manage and organize Google Cloud resources. Click on the CREATE PROJECT button to create one OR Select The project has been created available
- Return to the Pub/Sub page, and click on the CREATE TOPIC button. This action prompts a configuration interface where we can define crucial parameters for our topic.
    ![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/58b23dd8-24d8-4604-b9ab-82e8faad42bd)
- Input the topic name and click the CREATE button.
    ![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/dd972315-e894-47aa-9383-f00ff98213ed)
- This action will create our topic and a default subscription named will be automaticallygenerated since we left the Add default subscription box checked.
     ![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/f9fdb890-c082-4509-bf41-e5788b07a3b1)
  
  Subscriptions define how messages are delivered to subscribers, and specifying the delivery type is crucial for receiving real-time updates. Next, we will create two subscriptions with delivery types pull and push for our subscribers to connect with a topic.

## Step 2: Create a Pub/Sub subscription
Read the [Cloud Pub/Sub Subscriber Guide](https://cloud.google.com/pubsub/subscriber) to determine whether to configure the subscription as either a push subscription or a pull subscription.
  - A push subscription allows Cloud Pub/Sub to send notifications to your secure backend by issuing HTTPS requests.
  - A pull subscription requires your secure backend server to initiate requests to the Cloud Pub/Sub server to retrieve messages.
To create this custom subscription, click on CREATE SUBSCRIPTION button and create a pull or push subscriptions following the steps in the upcoming sections.
- Create a Pull Subscription
   ![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/9b1ea6b0-450f-45b2-b315-971f9d79c68b)
-  Enable Pub/Sub API for our project
   ![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/9a8779ee-954e-456c-a4c2-26f723700fbe)

   ![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/86befdf0-e253-420f-8a2b-558f73e9323a)

   ![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/93f8a5c0-75c4-43a9-92c3-fada1c9737ee)


# Step 3: Setting up a Service Account for Google Cloud Pub/Sub

Cloud Pub/Sub requires that you grant Google Play privileges to publish notifications to your topic.
[**In case there is Service Account**]
- Click to view permissions -> go to click button Add principal to grant new access.
    ![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/c4c57542-79de-4aff-97ec-e14c450d29db)

- Select account has been created previously and is already in use with the Google Play Console to input at Add principals section of image below.
- Example: with app drone have use service account [**goflyserviceaccount@go-fly-for-dji.iam.gserviceaccount.com**], so use this account to grant it the role of Pub/Sub Publisher and Enter this account in the input box of the Add principals section
    ![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/0cae95a0-0cd7-4273-9a2e-258307e92271)

- In Assign Roles -> select Pub/Sub Admin
    ![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/e03f60ac-67b3-46f3-94a1-91d5ff3267f9)


[**In case there is no Service Account**]
In the Google Cloud Console, go to the IAM & Admin section using the search bar.
  ![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/8d6985a0-e7a6-4572-ba67-314c7dec4ea6)

- Then click Create Service Account button.
  ![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/bd200cb4-1c4f-4aeb-b4d2-be3307837b69)

- Enter a service account name nodejs_app-pub-sub and description then click on the CREATE AND CONTINUE button
- Example: Add the service account google-play-developer-notifications@system.gserviceaccount.com, and grant it the role of Pub/Sub Publisher.
  ![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/474b76e6-81e3-40ca-a048-db6784f483e4)

- Next, to give us full access to topics and subscriptions, filter and assign the role Pub/Sub Admin to our service account nodejs_app-pub-sub. After that, click the Continue button.
   ![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/5fe41217-4045-4093-8d11-cb841c732fe9)

- We can skip the Grant users access to this service account option since we are not giving access to other users or groups in this article. Finally, click on the Done button.
- This should redirect us to the Service accounts page.
   ![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/7118945f-6646-48dd-b3f1-198b8e788fb8)

- Next, click to open the newly created service account and locate the key section.

- Click on Add Key, then select Create new Key, choose the JSON option, and [**download the JSON file**]. This file is essential for authentication within our Node.js project directory for our Pub/Sub setup.

  ![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/17b527c8-2e07-4261-83e0-8bd3c9085996)

# Step 4: Enable Real-time developer notifications for your app.
To enable Real-time developer notifications for your app, do the following:
1. Open the [Google Play Console](https://play.google.com/console/).
2. Select your app.
3. Go to Monetize > Monetization setup.
4. Scroll to the Real-time developer notifications section at the top of the page.

  ![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/88c5a657-488b-4730-918b-ddff7b159566)
  
5. Check Enable real-time notifications.
6. In the Topic name field, enter the full Cloud Pub/Sub topic name that you configured earlier. The topic name should be in the format of projects/{project_id}/topics/{topic_name} where project_id is the unique identifier for your project, and topic_name is the name of the topic created earlier.
7. Click Send Test Message to send a test message. Performing a test publish helps to ensure that everything is set up and configured properly. If the test publish succeeds, a message is displayed stating that the test publish was successful. If you have attached a subscription for this topic, you should receive the test message.
For a pull subscription, go to the subscription in Cloud Console, click View Messages, and proceed to pull messages. You should acknowledge any message you have pulled to avoid repeated delivery by Cloud Pub/Sub. For a push subscription, check if the test message is delivered to your push endpoint. A successful response code will serve as a message acknowledgement.
If the publish fails, an error is shown. Ensure that the topic name is correct and that the google-play-developer-notifications@system.gserviceaccount.com service account has Pub/Sub Publisher access to the topic.
8. Choose which notification types you'd like to receive.
- [Get notifications for subscriptions and all voided purchases - receive real-time developer notifications related to subscriptions and voided purchases. You won't receive notifications for one-time product purchases.]
- [Get all notifications for subscriptions and one-time products - receive notifications for all subscription and voided purchase events. You'll also receive one-time product purchase events, such as ONE_TIME_PRODUCT_PURCHASED and ONE_TIME_PRODUCT_CANCELED. See One-time purchase lifecycle to learn more about these purchase events.]
9. Click Save changes.
