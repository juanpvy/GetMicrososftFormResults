# Get Micrososft Form results
Get quiz result from Microsoft Forms and save values in SharePoint file

# Description 
I this post I will show you how to get Evaluations Result from a Quiz(Microsoft Forms).

# Microsoft Forms

First we need a Microsoft Forms Quiz, we can use this link [Microsoft Forms](https://support.microsoft.com/en-us/office/create-a-quiz-with-microsoft-forms-a082a018-24a1-48c1-b176-4b3616cdc83d) to learn how to create a new one. 
The important point of a Quiz Form is the result, is a value from 0 to 100, like an Assessment or test.  
After that we need to know some key point.
* Form URL: https://forms.office.com  , is the base URL of this service
* Form ID: When you are editing a Form  this value is in the URL 
 <img width="1313" height="45" alt="image" src="https://github.com/user-attachments/assets/ce123a35-166f-4b3c-94c4-deb1d161eb66" />

* Excel Results: Is an excel file with all  quiz results, Microsoft forms has an URL https://forms.office.com/formapi/DownloadExcelFile.ashx?formid=[FORM_ID]

# Power Automate - Get Responses 
As you already know Power Automate has a Microsoft Forms Connector in order to read the responses but is not possible get the  Result(0 to 100) using this connector.

<img width="616" height="261" alt="image" src="https://github.com/user-attachments/assets/777bcabe-dcaa-470c-aeb2-b60499bde641" />

As an alternative we can use the URL (Download Excel File) and  read the content implementing the following Actions: 
* Create URL to the excel file
* HTTP Request to get the file
* Save the file content in SharePoint
* Read the excel and get the rows
* Send those values to another repository
<img width="542" height="979" alt="image" src="https://github.com/user-attachments/assets/ff56d226-a8df-4d0d-926b-bd413eb2dba6" />

## Create ULR to the excel file
This url will have the format https://forms.office.com/formapi/DownloadExcelFile.ashx?formid=[FORM_ID]

## HTTP Request to get the file
We have to use the Connector HTTP with Microsoft Entra ID (Preautorized), this connector is important because we can use almost any Microsoft Services without Administration consent(we need access to that specific resource ).
<img width="634" height="250" alt="image" src="https://github.com/user-attachments/assets/e11504e3-cc00-4b6c-8f17-45a91a885cc1" />

First we need configure the connection   
<img width="583" height="447" alt="image" src="https://github.com/user-attachments/assets/8903717b-7e8d-4293-81b0-4024f82093fc" />

Then  configure parameters

<img width="628" height="409" alt="image" src="https://github.com/user-attachments/assets/7bee213b-e3dd-49a1-8bf6-04a48de90d90" />

## Save the content in sharepoint
We must to save the file in SharePoint because we can not read its content directly

<img width="604" height="477" alt="image" src="https://github.com/user-attachments/assets/cf65dc85-45b6-4010-b0bb-d9e614aa5c04" />

## Read the excel & extract the rows
We use the connector "List rows present in  table"

<img width="639" height="452" alt="image" src="https://github.com/user-attachments/assets/e2936770-6043-44d5-b41d-c16bd8417b41" />

Select the important columns , in this case "Total Point" because this columnas Microsoft Form saves the result that we are looking for

<img width="628" height="336" alt="image" src="https://github.com/user-attachments/assets/7db6c35f-1e24-4408-b270-d3f663355062" />

## Send those values to other repository

In this step you can implement any action you need , in this case was joins all values and  use the action "Respond to Power Apps"
