# Actualsales's pixel installation INSTRUCTIONS


### Step 1 - Get a Pixel
The first step to install a pixel on you website, is to have one! =D
You need to ask for a pixel code to an Actualsales's employee.


### Step 2 - Ways to fire a pixel
Normally, there are 3 ways to fire a pixel.
- [image](#imagePixel)
- [iFrame](#iframePixel)
- [Server](#serverPixel)

___


#### <a name="imagePixel"></a> How to fire image pixels
You should print the below HTML code on your page, at the correct moment, applying the necessary changes.

Ex: After the user clicked on the submit button and all form validations passed.

Note that you also need to replace the following parameters with the ones you've received on first step:
- cpnid = It will be on the URL of your pixel, you **do not** need to edit it. This number is generate by actualsales's systems.
- arg = You need to replace **XXX** with any **UNIQUE IDENTIFIER** of a lead. Ex: telephone, email, auto generated code etc.
- argmon = This parameter does not need to be replaced. Leave it as it is. 

```html
<!-- Firing image pixel -->
<img src="http://actualsalesdomainname.com/conv.php?cpnid=randomNumberIdentifyingTheCampaing&arg=XXX&argmon=YYY" width="1" height="1" alt="" title="" border="0" />
```
___


#### <a name="iframePixel"></a> How to fire iFrame pixels
You should print the below HTML code on your page, at the correct moment, applying the necessary changes.

Ex: After the user clicked on the submit button and all form validations passed.

Note that you also need to replace the following parameters with the ones you've received on first step:
- cpnid = It will be on the URL of your pixel, you **do not** need to edit it. This number is generate by actualsales's systems.
- arg = You need to replace **XXX** with any **UNIQUE IDENTIFIER** of a lead. Ex: telephone, email, auto generated code etc.
- argmon = This parameter does not need to be replaced. Leave it as it is. 

```html
<!-- Firing iframe pixel -->
<iframe src="http://actualsalesdomainname.com/conv.php?cpnid=randomNumberIdentifyingTheCampaing&arg=XXX&argmon=YYY" frameborder="0" width="1" height="1"></iframe>
```
___

#### <a name="serverPixel"></a> How to fire a pixel on server side.
The proccess to fire a pixel from server side is quite differente from the others above. It will depend on you server side structure and language.

Basically, you need to send a GET request to the **pixel's URL**, note that you should discard any HTML tags and use nothing but only the URL.

Note that you also need to replace the following parameters with the ones you've received on first step:
- cpnid = It will be on the URL of your pixel, you **do not** need to edit it. This number is generate by actualsales's systems.
- arg = You need to replace **XXX** with any **UNIQUE IDENTIFIER** of a lead. Ex: telephone, email, auto generated code etc.
- argmon = This parameter does not need to be replaced. Leave it as it is.

PHP Example:
```
//Variables
$url = 'http://actualsalesdomainname.com/conv.php?cpnid=12345678910&arg=XXX&argmon=YYY';
$userEmail = 'testuser@testdomain.com';

//Function to replace
function replaceParameters($leadUid, $url){
	return str_replace('XXX', $leadUid, $url);
}

// Get cURL resource
$curl = curl_init();

// Adjust the URL
$url = replaceParameters($userEmail, $url); // It will return http://actualsalesdomainname.com/conv.php?cpnid=12345678910&arg=testuser@testdomain.com&argmon=YYY 

curl_setopt_array($curl, array(
    CURLOPT_RETURNTRANSFER => 1,
    CURLOPT_URL => $url
));
// Send the request & save response to $resp
$resp = curl_exec($curl);
// Close request to clear up some resources
curl_close($curl);
```

### Checking if everything worked as expected.

If you used image or iFrame, you can check if it succeded by inspecting the network traffic on google chrome's developer console. Normally the pixel should return HTTP_CODE 200.

If you used server side method, you should also check the response code on your code right after the request.
