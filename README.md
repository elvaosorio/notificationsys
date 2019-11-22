# notificationsys
Send push notifications to apple and android.
FCM PUSH NOTIFICATION

DESCRIPTION
The FCM Push Notification service is a project that allows users to send push notifications to android devices.

WHY IT’S NEEDED
When the socket server fails to send push notifications, that’s when the FCM push notification takes control and sends push notifications.

TECHNICAL DESCRIPTION
The API/fcm.go receives variables from the env file that may change over time; like the authentication key, server, or certificates. In the Postman API, when you insert the values to the variables in the Body/raw/application/json file, the API/fcm.go file reads the values and inserts them into a payload that is then read by  a function called SendPushToAndroid in service/fcm.go. The RequestHandler function returns whether or not the notification was sent as a boolean.

POSTMAN API
In Postman, you should have a json file in the Body. That should look similar to this:
{
    "id": "<REQUEST_ID>",
    "module_name": <FCM_OR_APNS>,
    "token": "DEVICE_TOKEN",
    "message": "MESSAGE",
    "retry": true,
    "max_retry": 3
}
The REQUEST_ID is an identification given to each pushed notification. The FCM_OR_APNS should tell the program whether the phone receiving the notification is apple or android. The DEVICE_TOKEN is the device’s identification. 
REQUEST_ID, MESSAGE, and a device response should all be inputted into the database.

The API in Postman should have three keys with the following values:
KEY			VALUE
Content-Type		application/json
Authorization		key=<FCM_SERVER_KEY>
Accept			application/json

HOW TO SEND PUSH NOTIFICATION
SendPushToAndroid is a function that works with the API directly by setting the Headers, taking the payload, and sending the request in POST. If SendPushToAndroid doesn’t work, then it should return false.

The model/fcm_notification.go sets the structure of the json file in the Postman API. It should all run and a notification should be sent when SendPushToAndroid is called.

“If you’d like to use the apns version, it works the same way, except with different function names, but all functions do the same thing.”

