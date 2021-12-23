# Pharma24

**Visit us online !** - https://sites.google.com/view/pharma24-digibp/home

![grafik](https://user-images.githubusercontent.com/28628058/147106419-0ce1ba43-9fdc-4660-9339-4c246ba9aea2.png)

___

## Project concept
We are building a virtual Pharmacy store called Pharma24 that provides an
API for checking pharmaceutical products availability in a hospital.

In general, the hospital sends a prescription receipt via an API to Pharma24, where
the online pharmacy store checks the received information such as user data, product information and product availability / stock.

The products of the online pharmacy can be collected using a vending machine that checks the user information such as an invitation code, users’ identity and coverage of the insurance company.

## General Features

1.	User eligibility check
2.	Health insurance coverage check
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

### 1. Prescription

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

### 2. User information

**Integromat**

![grafik](https://user-images.githubusercontent.com/28628058/147089361-f2a2c17e-3b02-40e6-a454-0c1203c66f88.png)

**Mail**

In the e-mail we inform the user about a newly available prescription. In the mail we provide him/her with a receipt ID and a link to a google form, where it is possible to choose the handover type.

![grafik](https://user-images.githubusercontent.com/28628058/147098350-f8ed54af-2eb2-4699-bb88-ed17d2738ff2.png)

### 3. User decision

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

### 5. Send invoice

The invoice is generated based on a google sheets price list, where we have defined the prices per product. In the generated mail, the platform user is informed of the total price of the ordered product, showing the final bill which would be further sent to the insurance company in a real case scenario.

**Integromat**
![grafik](https://user-images.githubusercontent.com/28628058/147089389-a3439936-6a5e-4995-b13d-e5269535567c.png)

**Mail**
![grafik](https://user-images.githubusercontent.com/28628058/147098586-74bf52fb-0577-4467-a8c1-c43171cef206.png)
![grafik](https://user-images.githubusercontent.com/28628058/147098624-37eed108-097f-4004-b001-63d33a741cfa.png)

___
