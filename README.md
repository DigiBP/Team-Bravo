# Pharma24

![grafik](https://user-images.githubusercontent.com/28628058/146903533-94a32bb1-032f-4acd-918a-29d08c6ecd33.png)
**Visit us online !** - https://sites.google.com/view/pharma24-digibp/home
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

### Delivery
![grafik](https://user-images.githubusercontent.com/28628058/147090897-4b02ddb7-2a04-4adc-81e8-51abb8580b95.png)

### Pick-up
![grafik](https://user-images.githubusercontent.com/28628058/147090923-d53f6056-0b14-47dd-a7c2-da49b4a6d4a8.png)

___
Towards the end, the digitized model did not quite reach the level of complexity of the model originally conceived. However, it is the first good prototype.

## Final model
![grafik](https://user-images.githubusercontent.com/28628058/147091178-49955f1e-9c78-4cdf-8e77-3acca63c83f5.png)

___

## Workflow

### 1. Prescription

A process instance, which is triggered via google forms, starts in the service department of Pharma24.

For this to happen, a doctor has to write a prescription to a patient.

**Form**
<img width="1091" alt="grafik" src="https://user-images.githubusercontent.com/28628058/147090115-fde8e143-74c2-435a-8cbf-55eb01b4d7db.png">

If a doctor now clicks on submit, this automatically triggers an integromat scenario. Fortunately, this is done immediately because the scenario is provided with a webhook.

**Integromat**
![grafik](https://user-images.githubusercontent.com/28628058/147089230-790fdbc9-87fc-4cd8-b68b-d924cfc6bc28.png)

Then the process instance continues to inform customer.

### 2. User information

Integromat
![grafik](https://user-images.githubusercontent.com/28628058/147089361-f2a2c17e-3b02-40e6-a454-0c1203c66f88.png)

Mail

### 3. User decision

Form
<img width="1090" alt="grafik" src="https://user-images.githubusercontent.com/28628058/147090147-75b790c5-8f48-4f59-86a0-4c50af21d0d1.png">

Integromat
![grafik](https://user-images.githubusercontent.com/28628058/147089281-b46f5cd7-e364-43e4-85c1-39dd013ef5a3.png)

### 4. Check stock

Integromat
![grafik](https://user-images.githubusercontent.com/28628058/147089325-d3e1ec36-69e0-42d2-a329-e0c34bacd956.png)

### 5. Send invoice

Integromat
![grafik](https://user-images.githubusercontent.com/28628058/147089389-a3439936-6a5e-4995-b13d-e5269535567c.png)
___
