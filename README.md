# Instamojo Opencart Payment Gateway Plugin


## Download:

Download the latest release from the [releases section](https://github.com/Instamojo/Instamojo-OpenCart-2.0/releases) or download it from the [OpenCart Extensions website](http://www.opencart.com/index.php?route=extension/extension/info&extension_id=21984).

For auto-installation rename the file to use the extension `ocmod.zip`, for example: `Instamojo-OpenCart-2.x.ocmod.zip`.

## Installation

#### Automatic Installation
1. Go to Extensions > Extension installer.
2. Click on upload and select Instamojo-OpenCart-2.x.ocmod.zip from your download directory
3. Click on Continue button. 
4. You will get the success notification if extension properly installed.

***Note: if automatic installation fails you can try further manual installation steps.***

***
#### Manual Installation:

1.  Copy the contents of `upload` directory(the folders inside upload directory in plugin) into your OpenCart installation root directory **(No files are going to be overwritten)**.

2. Navigate to Extensions > Payment from admin panel menu.
3. Look for the Instamojo in Payment List.
4. Click on green Install button(the button have + icon).
***

## Configuration

1. After installation click on edit button corresponding to Instamojo module(the button have pencil icon).
2. Fill the following details:

    - **Order Status :** This is the order of the status that you would like to set after a successful payment.

    -  **Checkout Label:** This is the label users will see during checkout, its default value is "Pay using Instamojo". You can change it to something more generic like "Pay using Credit/Debit Card or Online Banking".
      
    -  **Status:** This is the current status of the module. To use Instamojo during checkout make sure to change it to enabled.
     
    - **Client ID** and **Client Secret** - Client Secret And Client ID can be generated on the [Integrations page](https://www.instamojo.com/integrations/). Related support article: [How Do I Get My Client ID And Client Secret?](https://support.instamojo.com/hc/en-us/articles/212214265-How-do-I-get-my-Client-ID-and-Client-Secret-)
    
    - **Test Mode:** If enabled you can use our [Sandbox environment](https://test.instamojo.com) to test payments. Note that in this case you should use `Client Secret` and `Client ID` from the test account not production.

## Migrating from older version

If you were already using older version of our plugin then follow these steps:

1. Uninstall the old Instamojo extension first from `Extensions -> Payments`.
2. Now remove the following files:
   - admin/controller/payment/instamojo.php
   - admin/language/english/payment/instamojo.php
   - admin/view/template/payment/instamojo.tpl

   - catalog/controller/payment/instamojo.php
   - catalog/model/payment/instamojo.php
   - catalog/view/theme/default/template/payment/instamojo.tpl
=======
Instamojo-OpenCart for OpenCart versions 2.x
====
----
This module allows us to use [Instamojo](https://www.instamojo.com) as Payment Gateway in OpenCart 2.x
(**Note:** If you're using OpenCart version 1.5.x then use our other plugin: https://github.com/instamojo/Instamojo-OpenCart-1.5/)
###Installation
---
- Download the [zip file](https://github.com/instamojo/Instamojo-OpenCart-2.0/archive/master.zip) and paste the content of **upload** folder into your sites main directory, this is **public_html** is most cases. Note that inside **public_html** you will already have folders named **admin** and **catalog**, so you are supposed to merge the **admin** and **catalog** from our module to those folders.

- Now go the admin backend and there go to **Extensions -> Payments**:

![enter image description here](http://i.imgur.com/nO4E0yo.png)

This page will display all the Payment modules present along with **Instamojo Payment Method**.

![enter image description here](http://i.imgur.com/uuS1tgA.png)

Click on the button with **+** to install **Instamojo Payment Method**. After installation click on the edit  button:

![enter image description here](http://i.imgur.com/eg5QuBU.png) 

Click on **Edit** to configure the module.

Now you will see a form like this:

![enter image description here](http://i.imgur.com/2f5x4ER.png`)

---
I will explain **`Order Status`**, **`Checkout Label`** and **`Status`** here and rest of the fields are explained in next sections:  

- **Order Status**:  This is the order of the status that you would like to set after a **successful** payment.
- **Checkout Label**: This is the label users will see during checkout, its default value is **"Pay using Instamojo"**. You can change it to somethint more generic like **"Pay using Credit/Debit Card or Online Banking"**.
- **Status**:  This is the current status of the module. To use Instamojo during checkout make sure to change it to **enabled**.

### Creating a Product
----
In this section we will learn how to create a product along with how to get the required values for `Payment Link` and `Custom Field`.

- Create a product by clicking on **Add a Product** on your Instamojo dashboard and choose the category **Other**.

  Set the price to Rs. 10 and enable **"Pay what you want"**.  Under **Title** and **Description**, you may enter something that describes your business and the nature of the products being sold.

  Under **Advanced settings** of the same product there's a field **Custom Redirection URL**. Here if your website's url is **http://www.example.com** then use **http://www.example.com/index.php?route=payment/instamojo/callback** as **Custom Redirection URL**.

![enter image description here](http://i.imgur.com/mp2xipp.png)

 Click on **Add Product to Store** to save the product.
 
- Copy the product URL and paste this in **Payment Link** field. URL's format is usually: **https://www.instamojo.com/username/slug/**.
- On the product page go to **More options** and click on **Custom Fields**. Create a custom field called **Order ID** and mark it as **required**. Click on **Add Custom Field** to save this custom field. 

 ![enter image description here](http://i.imgur.com/0phw8JM.png)

 After the custom field has been created **Existing Custom Fields** section will appear. Copy the name shown under **Field ID** column, its format is **Field_xxxx**, where **xxxx** are some numbers(Note that this is case sensitive!). In this example the value is **Field_11828**.

![enter image description here](http://i.imgur.com/5G3yiWs.png)

Enter this value in the **Custom field** field of the Instamojo module configuration page in OpenCart.

### Auth
---
In this section we will learn how to get the values of fields  `API Key`,  `Auth token` and `Private salt`.

Go the [Instamojo developers](https://www.instamojo.com/developers/) page, if your are not logged in already then login first and then you'll see the value of `API Key`,  `Auth token`,  `Private salt` there on the bottom left side of the page.

Simply copy and paste their values in the configuration form in their respective fields.

---

Now your form will look something like this:

![enter image description here](http://i.imgur.com/Dvsi61j.png)

Now simply click on **save**(button with floppy icon) to save these setting and now the **Pay using DB/CC or Online banking**<sup>*</sup> option will show up on the checkout page.

![enter image description here](http://i.imgur.com/3RKx7j5.png)

### Logs
---

This module will everything to a file named **imojo.log** under **system/logs**. Share it with us if you're facing some issue while making a transaction using this module. Our support email id is: support@instamojo.com

---
<sub>`*` This may be different for your **Checkout Label** is different.</sub>

### Support
---

If you're facing some issue with plugin integration then open an ticket at http://support.instamojo.com/. Please do include a **screenshot of the settings** you've done for the plugin in your admin backend as well as the **URL of the Instamojo payment link** you're using with the plugin.
