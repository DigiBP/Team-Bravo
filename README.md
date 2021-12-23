# Pharma24

**Visit us online !** - https://sites.google.com/view/pharma24-digibp/home

![grafik](https://user-images.githubusercontent.com/28628058/147106419-0ce1ba43-9fdc-4660-9339-4c246ba9aea2.png)

___

## Project concept
Pharma24 is a platform connecting physicians, patients, and pharmacies. This platform offers patients more convenience to receive their prescribed medication issued by medical doctors. Furthermore, it leads to increased efficiency in the invoicing of medicines between pharmacies and insurance companies. 

## General Features

1.	Electronic prescription handling
2.	Automated status updates
3.	Product availability check

___

## First concept

The first attempt was to create a BPMN model that visualizes our process and because we want to digitize it in the future.

### Main process concept
![grafik](https://user-images.githubusercontent.com/28628058/147090848-07875e5e-4335-4a8d-b330-6ebcf7b2a6e1.png)

### Delivery sub-process
![grafik](https://user-images.githubusercontent.com/28628058/147090897-4b02ddb7-2a04-4adc-81e8-51abb8580b95.png)

### Pick-up sub-process
![grafik](https://user-images.githubusercontent.com/28628058/147090923-d53f6056-0b14-47dd-a7c2-da49b4a6d4a8.png)

___
Towards the end, the digitized model did not quite reach the level of complexity of the model originally conceived. However, it is the first good prototype.

## Final model

This is the final automated and used model with all of our automated steps, based on our first concept bpmn model.

![grafik](https://user-images.githubusercontent.com/28628058/147091178-49955f1e-9c78-4cdf-8e77-3acca63c83f5.png)

___

## Workflow

### 1. Prescription received

![1](https://user-images.githubusercontent.com/63347322/147220531-5cb04b07-6c5e-4bd1-aed6-7d0ce12b1e65.JPG)

A process instance, which is triggered via google forms, starts in the service department of Pharma24.

For this to happen, a doctor has to write a prescription to a patient.

**Form**

https://forms.gle/nwU7jvuPK3daM2337

<img width="1091" alt="grafik" src="https://user-images.githubusercontent.com/28628058/147090115-fde8e143-74c2-435a-8cbf-55eb01b4d7db.png">

If a doctor now clicks on submit, this automatically triggers an integromat scenario. Fortunately, this is done immediately because the scenario is provided with a webhook.

**Integromat**

After the webhook is triggered we are generating a unique random business key for our further processes.
![grafik](https://user-images.githubusercontent.com/28628058/147089230-790fdbc9-87fc-4cd8-b68b-d924cfc6bc28.png)

Then the process instance continues to inform the customer.

### 2. Inform customer

**Integromat**

![grafik](https://user-images.githubusercontent.com/28628058/147089361-f2a2c17e-3b02-40e6-a454-0c1203c66f88.png)

**Mail**

In the e-mail we inform the user about a newly available prescription. In the mail we provide him/her with a receipt ID and a link to a google form, where it is possible to choose the handover type.

![mail1](https://user-images.githubusercontent.com/63347322/147220894-c864bdac-65c3-457f-bf17-5ca873e2178c.JPG)


### 3. Customer decision

**Form**

In the form we collect the information such as ID, Name, Insurance Number as well as the handover type.

https://forms.gle/dvxPgpi6ZuCvMsKo8

<img width="1090" alt="grafik" src="https://user-images.githubusercontent.com/28628058/147090147-75b790c5-8f48-4f59-86a0-4c50af21d0d1.png">

**Integromat**

All of the provided information is stored in the request content and will be sent to the camunda application using a HTTP post request.

![grafik](https://user-images.githubusercontent.com/28628058/147089281-b46f5cd7-e364-43e4-85c1-39dd013ef5a3.png)

### 4. Check stock

Once we have stored the handover type, we check with an automated scenario, if there is enough of the ordered product on stock. A rourter combined with a filtering option is checking which path to use. If there is enough on stock, we handle the order and update the database, if not we inform our stock department to order more of the desired product. We do then wait for the stock to be available again by simulating a waiting time of 2-3 day with a 15sec waiting time and increasing our stock.

**Integromat**

![grafik](https://user-images.githubusercontent.com/28628058/147089325-d3e1ec36-69e0-42d2-a329-e0c34bacd956.png)

### 5. Send order

![4 7](https://user-images.githubusercontent.com/63347322/147221018-2b7f73d2-6e5f-492b-9307-8ba740044acd.JPG)


After checking if the product is available, a manual task has to be fullfilled, where a user needs to claim the job and check all of the provided user information and compare it to the information provided from the doctor. This manual task is introduced as a security option, to make shure everything is in order. In a further development step this taks could also be automated for a faster fullfillment process.

![4 8](https://user-images.githubusercontent.com/63347322/147221034-fe8c2135-a079-4c7f-a57b-d7ebd42409b2.JPG)


### 6. Send invoice

The invoice is generated based on a google sheets price list, where we have defined the prices per product. In the generated mail, the platform user is informed of the total price of the ordered product, showing the final bill which would be further sent to the insurance company in a real case scenario.

**Integromat**
![grafik](https://user-images.githubusercontent.com/28628058/147089389-a3439936-6a5e-4995-b13d-e5269535567c.png)

**Mail**
![mail3](https://user-images.githubusercontent.com/63347322/147220956-2824ba77-f11a-4473-b4ad-6b7573ea9582.JPG)

___

## Outlook

The process described has potential for many enhancements that will help to improve patient safety, increase the efficiency of Pharma24’s stakeholders, and reduce health care costs. As an example, the newly prescribed medications could be automatically checked for incompatibility with the existing medications. The medication warehouses of the individual pharmacies could be mapped into a single virtual warehouse. Price comparisons between drugs with same active ingredient could be offered to patients etc.
