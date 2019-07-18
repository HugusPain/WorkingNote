This document is a guide to implement WOGAA tracking code on your website. 

We are constantly improving this guide. If you have any feedback, please email to us at wogaa@tech.gov.sg

> WARN: Do not reshare this document with anyone unless they need to implement WOGAA tracking on their websites.

- [Getting Started](#getting-started)
- [1. Requirement of WOGAA Codes](#1-requirement-of-wogaa-codes)
- [2. Base Code v2](#2-base-code-v2)
- [3. Event Trigger Codes](#3-event-trigger-codes)
- [4. Code Verification](#4-code-verification)
  - [4a. Verify Base Code](#4a-to-verify-base-code)
  - [4a. Verify Event Trigger Codes](#4b-to-verify-event-trigger-codes)
- [Content Security Policies](#content-security-policies)
- [Previous Implementation of the Base Code - Base Code v1](#previous-implementation-of-the-base-code---base-code-v1)
  - [Base Code v1](#base-code-v1)
  - [Migrating of Base Code v1 to Base Code v2](#migrating-of-base-code-v1-to-base-code-v2)
- [Sentiments](#sentiments)
  - [Onboarding of Sentiments](#onboarding-of-sentiments)
  - [Verification of Sentiments](#verification-of-sentiments)

---

# Getting Started

> :exclamation: If your website is currently using Adobe Launch, Adobe DTM or Adobe Analytics, please do not proceed with the rest of the instruction in this page. Please contact WOGAA Team at wogaa@tech.gov.sg and we will be happy to assist you.

- [Step 1: Register your Informational Service (IS) and Transactional Service (TS) on WOGAA website](#step-1-register-your-informational-service-is-and-transactional-service-ts-on-wogaa-website)
- [Step 2: Embed the base code on your website to start tracking Informational Service](#step-2-embed-the-base-code-on-your-website-to-start-tracking-informational-service)
- [Step 3: Verify that the base code has been embedded properly](#step-3-verify-that-the-base-code-has-been-embedded-properly)
- [Step 4: Embed the event trigger code on your website to start tracking Transactional Service](#step-4-embed-the-event-trigger-code-on-your-website-to-start-tracking-transactional-service)
- [Step 5: Verify that the event trigger code has been embedded properly](#step-5-verify-that-the-event-trigger-code-has-been-embedded-properly)


## Step 1: Register your Informational Service (IS) and Transactional Service (TS) on WOGAA website

If you haven't done so, please go to https://wogaa.sg to register your IS and TS. This step is required to track IS and TS.

## Step 2: Embed the base code on your website to start tracking Informational Service

In order for us to track web analytics data about your IS, we will need you to add the base code to your website.

Please see [Base code v2](#2-base-code-v2) for implementation details.

If you encounter any error related to CSP after embedding the code, please refer to [Content Security Policies](#content-security-policies) to resolve it

## Step 3: Verify that the base code has been embedded properly

When the page that has the base code embedded is loaded, it will collect web analytics data and send it to Adobe Analytics.

Please refer to [4a. Verify Base Code](#4a-to-verify-base-code) to verify if the base code has been embedded correctly.

If you do not have any transactional services for your website, you can stop at this step.

## Step 4: Embed the event trigger code on your website to start tracking Transactional Service

After you have registered your TS on [WOGAA website](https://wogaa.sg), a unique tracking ID is generated for each of your TS.

You will have to embed the event trigger code with the TS tracking ID on your website to start tracking them

- When the transactional service is started, it should invoke the event trigger code 
```javascript
window.wogaaCustom.startTransactionalService("<tracking_id>")
```

When the transactional service is completed, it should invoke the event trigger code 
```javascript
window.wogaaCustom.completeTransactionalService("<tracking_id>")
```

Please see [Event Trigger Codes](#3-event-trigger-codes) for implementation details.

## Step 5: Verify that the event trigger code has been embedded properly
When the event trigger code is called, it will send data to Adobe Analytics.

Please refer to [4b. Verify Event Trigger Codes](#4a-to-verify-base-code) to verify if the base code has been embedded correctly.

---

# 1. Requirement of WOGAA Codes

### Both Informational and Transactional pages
For all pages that are to be tracked by WOGAA, the base code needs to be embedded to enable basic web analytics tracking, e.g. Page Views, Browser Types, Visits. Please see [Base code v2](#2-base-code-v2) for implementation details.

### Transactional Service pages only
In addition to the Base Code, these codes needs to be embedded on Transactional Service services. These codes will identify Transactional Services so that completion rates can be measured accurately. Please see [Event Trigger codes](#3-event-trigger-codes) for implementation details.

The implementation of the above is detailed in the following sections.

---

# 2. Base Code v2

> :exclamation: For websites that has the script inserted before 15 November 2018, please read [Previous Implementation of the Base Code v1](#previous-implementation-of-the-base-code-v1)


Insert the following code into the `<head>` of every page of your website, before other scripts.

  - Staging Environment
  ```html
  <script src="https://assets.dcube.cloud/scripts/wogaa.js"></script>
  ```

  - Production Environment
  ```html
  <script src="https://assets.wogaa.sg/scripts/wogaa.js"></script>
  ```

  - Example

  ```html
  <html>
    <head>
      ...
      [Insert Staging / Production Base Code]
    </head>
    ...
  </html>
  ```

> :exclamation: For websites that has the script inserted before 15 November 2018 date, please read [Previous Implementation of the Base Code v1](#previous-implementation-of-the-base-code-v1)

---

# 3. Event Trigger codes
> Please note that for this to work, you would need to switch to the new [Base code v2](#2-base-code-v2).

Event trigger codes help to track your transactional services. 

We understand that different websites have different structure and way of tracking website analytics, thus we provide event trigger codes for website owner to call at their own convenience.

Once you embed the event trigger code for your transactional services, you will be able to track the completion rate of each transaction. 

There are 2 event trigger codes for you to use
1. Event trigger code to start tracking the transactional services
```javascript
window.wogaaCustom.startTransactionalService('<tracking_id>')
```
2. Event trigger code to end tracking the transactional services
```javascript
window.wogaaCustom.completeTransactionalService('<tracking_id>')
```

> :exclamation: Please ensure that new [Base code v2](#2-base-code-v2) is loaded before invoking the event trigger codes. 

The correct tracking ID should be passed to `startTransactionalService` and `completeTransactionalService`. If the tracking ID passed to either of the event trigger code doesn't belong to your website, event trigger code will not work.

### How to get the tracking_id of the transactional services
1. Login to WOGAA and go to `My Digital Services`
2. Click on the information service that the transactional services belong to
3. Click on `GET CODE`
4. A CSV file of transactional services and its tracking_id will be emailed to you

### Example

*Transactional service belonging to Example Website (`www.example.gov.sg`)*

| Name of Transactional service  | Tracking ID           |
| ------------------------------ | --------------------- |
| Creation of user               | `example-1`           |
| Apply for approval             | `example-2`           |


##### When to invoke `startTransactionalService` and `completeTransactionalService`
`window.wogaaCustom.startTransactionalService('example-1')` should be invoked when the website user starts the transactional service `Creation of user`

`window.wogaaCustom.completeTransactionalService('example-1')` should be invoked when the website user completes the transactional service `Creation of user`

##### Argument to pass to `startTransactionalService` and `completeTransactionalService`
Invoking `window.wogaaCustom.startTransactionalService('example-1')` will work since the Example Webite `www.example.gov.sg` has tracking ID `example-1` tagged under it.

Invoking `window.wogaaCustom.startTransactionalService('testing-1')` will not work since the Example Webite `www.example.gov.sg` doesn't have tracking ID `testing-1` tagged under it.

### Ensures that `wogaa.js` and `datalayer.js` is loaded before invoking the Event Trigger Codes
`datalayer.js` will expose the function `startTransactionalService()` and `completeTransactionalService()` on the window object. 

You will have to ensure that `datalayer.js` is loaded before invoking the event trigger codes.

##### How to check that `datalayer.js` is loaded
1. Open Chrome
2. Go to Developer Tools
3. Click on the `Network` tab
4. Filter by `JS`
5. Refresh the page
6. Check if there's a file called `datalayer.min.js`


##### Invoking `startTransactionalService()` and `completeTransactionalService()` when page loads
Likewise, you will have to ensure `datalayer.js` is loaded before invoking the function.

The code snippets below are just some example on how can you ensure that `startTransactionalService()` and `completeTransactionalService()` is invoked when page loads. More examples can be found [here](https://developer.mozilla.org/en-US/docs/Web/Events/load). You don't necessarily have to follow the example below.

```javascript
  window.addEventListener("load", function(event) {
    window.wogaaCustom.startTransactionalService('<tracking_id>')
  });
```

```javascript
  window.addEventListener("load", function(event) {
    window.wogaaCustom.startTransactionalService('<tracking_id>')
    window.wogaaCustom.completeTransactionalService('<tracking_id>')
  });
```

---

# 4. Code Verification

Use the Chrome extension [Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) to verify if the base code and event trigger codes are working
* Install [Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj)
* Follow the steps below to verify base code and event trigger codes

### 4a. To verify base code

1. Navigate to the website with the base code.
2. Open the Adobe Experience Cloud Debugger extension.
3. Navigate to the `Analytics` tab in the `Adobe Experience Cloud Debugger` and clicks on `Clear All Requests`.
4. Refresh the website and check if there is any data in the `Hits` section.
5. If the implementation is correct, there should be 2 sets of data.
6. Expand both set of data and screen capture them.
7. Send the image to WOGAA NCS Support at `wog.aa.support@ncs.com.sg`, indicating the environment the screen capture is for (Staging or Production)

![image](https://user-images.githubusercontent.com/43952553/48483821-7521a600-e84f-11e8-869a-9cad2222484e.png)

### 4b. To verify event trigger codes

##### For startTransactionalService()
1. Open the Adobe Experience Cloud Debugger extension.
2. Navigate to the `Analytics` tab in the `Adobe Experience Cloud Debugger` and clicks on `Clear All Requests`.
3. Navigate to the page where the Event Trigger code `startTransactionalService()` is fired.
4. If the implementation is correct, you should be able to see data on the Experience Cloud Debugger, with a value set for `eVar16`
5. Take a screenshot of the data
6. Send the image to WOGAA NCS Support at `wog.aa.support@ncs.com.sg`, indicating the environment the screen capture is for (Staging or Production)

![starttransactionss](https://user-images.githubusercontent.com/43952553/50443599-0b60e580-093f-11e9-831c-398bba26e787.png)

##### For completeTransactionalService()
1. Open the Adobe Experience Cloud Debugger extension.
2. Navigate to the `Analytics` tab in the `Adobe Experience Cloud Debugger` and clicks on `Clear All Requests`.
3. Navigate to the page where the Event Trigger code `completeTransactionalService()` is fired.
4. If the implementation is correct, you should be able to see data on the Experience Cloud Debugger, with a value set for `eVar16` and `eVar17`
5. Take a screenshot of the data
6. Send the image to WOGAA NCS Support at `wog.aa.support@ncs.com.sg`, indicating the environment the screen capture is for (Staging or Production)

![completetransactionss](https://user-images.githubusercontent.com/43952553/50443702-83c7a680-093f-11e9-8472-a97da7760e99.png)

---

# Content Security Policies

If you are using a default CSP, just adding the following should be sufficient.

## Production CSP
```
default-src 'self' https://*.wogaa.sg https://*.demdex.net/ https://cm.everesttech.net/ https://wogadobeanalytics.sc.omtrdc.net/;
script-src 'self' 'unsafe-inline' 'unsafe-eval' https://*.wogaa.sg https://assets.adobedtm.com/;
img-src 'self' data: https://wogadobeanalytics.sc.omtrdc.net/ https://cm.everesttech.net/ https://dpm.demdex.net/;
connect-src 'https://*.wogaa.sg';
style-src 'self' 'unsafe-inline' https://assets.wogaa.sg/fonts/;
font-src 'self' data: https://assets.wogaa.sg/fonts/;
```

## Staging CSP
``` 
default-src 'self' https://*.dcube.cloud/ https://*.demdex.net/ https://cm.everesttech.net/ https://wogadobeanalytics.sc.omtrdc.net/;
script-src 'self' 'unsafe-inline' 'unsafe-eval' https://*.dcube.cloud https://assets.adobedtm.com/;
img-src 'self' data: https://wogadobeanalytics.sc.omtrdc.net/ https://cm.everesttech.net/ https://dpm.demdex.net/;
connect-src 'https://*.dcube.cloud';
style-src 'self' 'unsafe-inline' https://assets.dcube.cloud/fonts/;
font-src 'self' data: https://assets.dcube.cloud/fonts/;
```

---

# Previous Implementation of the Base Code - Base Code v1

Base Code v1 is deprecated. Please use [Base code v2](#2-base-code-v2)


### Base Code v1

1. Insert the following code into the `<head>` of every page of your website, before other scripts.

Staging Environment
```html
<script src="//assets.adobedtm.com/a63ef04a8a06d4763abe9b28a8d967e7e749d199/satelliteLib-db3891214175cc48594c242657d262be8297f3d8-staging.js"></script>
```

Production Environment
```html
<script src="//assets.adobedtm.com/a63ef04a8a06d4763abe9b28a8d967e7e749d199/satelliteLib-db3891214175cc48594c242657d262be8297f3d8.js"></script>
```

2. Insert the following code into the `<body>` of every page of your website, just before the closing `</body>` tag

Staging and Production Environment
```html
<script type="text/javascript">_satellite.pageBottom();</script>
```

### Migrating of Base Code v1 to Base Code v2
1. Remove `<script type="text/javascript">_satellite.pageBottom();</script>`
2. Update `<script src="//assets.adobedtm.com/a63ef04a8a06d4763abe9b28a8d967e7e749d199/satelliteLib-db3891214175cc48594c242657d262be8297f3d8.js"></script>` to `<script src="https://assets.wogaa.sg/scripts/wogaa.js"></script>`

| Position                                                  | Environment            | Base code v1 | Base code v2 |
|-----------------------------------------------------------|------------------------|--------------|--------------|
| `<head>` of every page                                    | Staging                | <script src="//assets.adobedtm.com/a63ef04a8a06d4763abe9b28a8d967e7e749d199/satelliteLib-db3891214175cc48594c242657d262be8297f3d8-staging.js"></script> | <script src="https://assets.dcube.cloud/scripts/wogaa.js"></script> |
|                                                           | Production             | <script src="//assets.adobedtm.com/a63ef04a8a06d4763abe9b28a8d967e7e749d199/satelliteLib-db3891214175cc48594c242657d262be8297f3d8.js"></script> | <script src="https://assets.wogaa.sg/scripts/wogaa.js"></script> |
| `<body>` of every page, just before the closing `</body>` | Staging and Production | <script type="text/javascript">_satellite.pageBottom();</script> | *empty* |

---

# Additional Detail
When the base code v2 is loaded on the website, it will load 3 more JavaScript files
1. Adobe Launch `//assets.adobedtm.com/launch-ENaf340d988e354d18ba897b99e3538f23.min.js`
2. Adobe Analytics `https://assets.adobedtm.com/extensions/EPb3826f174b534354aaa5a9e9f1dab55d/AppMeasurement.min.js`
3. Data Layer `https://ujs.wogaa.sg/datalayer.min.js`

---

# Sentiments

## Onboarding of Sentiments
If you wish to onboard Sentiments, just send us an email and we will be happy to help.

## Verification of Sentiments 

### Verification of Sentiments on Informational Services
1. Go to your website that has Sentiments onboarded
2. Check if there's a Sentiments Icon on the bottom left of your screen

### Verification of Sentiments on Transactional Services
1. Go to your transactional services that has Sentiments onboarded
2. Check if there's no Sentiments Icon on the bottom left of your screen
3. Open your browser developer console
4. Enter `wogaaCustom.startTransactionalService("<tracking-id>")`
5. Enter `wogaaCustom.completeTransactionalService("<tracking-id>")`
6. Check if sentiments appear