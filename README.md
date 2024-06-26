# Pub-Sub-Google - Configure Real-time developer notifications
[Cloud Pub/Sub](https://cloud.google.com/pubsub/) is a fully-managed real-time messaging service that you can use to send and receive messages between independent applications. Google Play uses Cloud Pub/Sub to publish push notifications on topics to which you subscribe.
[Docs](https://developer.android.com/google/play/billing/getting-ready#configure-rtdn)

## Table of Contents
1. [**Step 1:Setup Cloud Pub/Sub.**]
2. [**Step 2: Create a Pub/Sub subscription.**]
3. [**Step 3: Setting up a Service Account for Topic of Google Cloud Pub/Sub.**]
4. [**Step 4: Enable Real-time developer notifications for your app.**]

## **Step 1**: Setup Cloud Pub/Sub.
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

## Step 2: Create a Pub/Sub subscription.
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


## Step 3: Setting up a Service Account for Topic of Google Cloud Pub/Sub.
Use account default: google-play-developer-notifications@system.gserviceaccount.com
1. select topic -> click on View permissions
![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/ab20c621-35e2-40f5-9135-0533bc6749e4)

2. In the sidebar click button Add Principals
![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/a12e9062-348d-4f51-9fc8-3f9609608be1)

3. Fill in the information in the acc box as shown below:
Enter the account as **google-play-developer-notifications@system.gserviceaccount.com**
![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/0d805149-e40c-428d-83bb-2f3af548b91c)

Select role for account is **Pub/Sub Publisher** -> then click button **SAVE**
![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/ad81c1c3-e673-47e2-bd28-9184db87102d) 


## Step 4: Enable Real-time developer notifications for your app.
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

# Check message After clicking send notification successfully
Sau khi gửi thành công test notification thì quay lại trang Pub/sub của google cloud. Chọn vào topic trước đó và chọn tiếp vào Subscription của topic đó.
![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/4d2a783e-4b61-4af7-aed4-248607047017)

Trong trang của Subscription này thì chọn qua tab MESSAGES và click vào button PULL để xem được thông báo vừa được gửi ở bên google play console.
![image](https://github.com/tuannd20/Pub-Sub-Google/assets/74279060/6a73f891-7a75-467f-8930-0b980084a730)
