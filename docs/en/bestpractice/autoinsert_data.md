# Ad Customizers feature (Data Assignment)
## What is “Ad Customizers”?
Ad Customizers is a function of changing the title and descriptions of the Sponsored Search ads in dynamic.<br>
It can automatically insert the ad title and description flexibly. And 'COUNTDOWN' function will enable the feature to count down remaining minutes on discount sale.<br>

## How to operate from Sponsored Search API
To display ads by using Ad Customizers feature, use the three services below from Sponsored Search API.

##### 1.	FeedFolderService 
FeedFolderService can retrieve and add/update/delete the FeedFolder information. <br>
FeedFolder is a component to store Data Assignment List which added data to be inserted to ads.
  
##### 2.	FeedItemService  
FeedItemService can add/update/delete data to/from each Data Assignment List in FeedFolder information.

##### 3.	AdGroupAdService
AdGroupAdService can create the ads which is inserted the data already added to the list (ads using a function to insert data).

## Examples
Company A is planning to add the data list below by Sponsored Search API for the promotion.
  
##### Sale product list
<table class="standard">
                <tr>
                    <th valign="top" >
                        <p>Product (String)</p>
                    </th>
                    <th valign="top" >
                        <p>Price (Price)</p>
                    </th>
                    <th valign="top">
                        <p>Final sale date (Date)</p>
                    </th>
                    <th valign="top" >
                        <p>CampaignId</p>
                    </th>
                    <th valign="top" >
                        <p>AdGroupId</p>
                    </th>
                </tr>
                <tr>
                    <td valign="top">
                        <p>Product 101</p>
                    </td>
                    <td valign="top">
                        <p>100</p>
                    </td>
                    <td valign="top">
                        <p>20151231 000000</p>
                    </td>
                    <td valign="top">
                        <p>500001</p>
                    </td>
                    <td valign="top">
                        <p>600001</p>
                    </td>
                </tr>
                <tr>
                    <td valign="top">
                        <p>Product 102</p>
                    </td>
                    <td valign="top">
                        <p>300</p>
                    </td>
                    <td valign="top">
                        <p>20151231 000000</p>
                    </td>
                    <td valign="top">
                        <p>500001</p>
                    </td>
                    <td valign="top">
                        <p> </p>
                    </td>
                </tr>
                <tr>
                    <td valign="top">
                        <p>Product 103</p>
                    </td>
                    <td valign="top">
                        <p>1,000</p>
                    </td>
                    <td valign="top">
                        <p>20151231 000000</p>
                    </td>
                    <td valign="top">
                        <p>500002</p>
                    </td>
                    <td valign="top">
                        <p> </p>
                    </td>
                </tr>
</table>
*Setting CampaignId and AdGroupId will enable to specify campaign and ad group to be used for the data line. Cbr>
Can leave the setting blank, if specifying is not necessary.

#### 1.	Adding FeedFolder
Add Feed Folder to Sponsored Search account using FeedFolderService. <br>
For this example, "Sale product list" will be added to the account of company A (ID: 100000001).

##### Request Sample
```xml
<?xml version="1.0" encoding="UTF-8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://ss.yahooapis.jp/V6">
   <soapenv:Header>
      <ns1:RequestHeader>
         <ns1:license>XXXX-XXXX-XXXX-XXXX</ns1:license>
         <ns1:apiAccountId>XXXX-XXXX-XXXX-XXXX</ns1:apiAccountId>
         <ns1:apiAccountPassword>passwd</ns1:apiAccountPassword>
         <ns1:accountId>100000001</ns1:accountId>
         <ns1:onBehalfOfAccountId>XXXXX-XXXX-XXXXX-XXXX</ns1:onBehalfOfAccountId>
         <ns1:onBehalfOfPassword>passwd2</ns1:onBehalfOfPassword>
      </ns1:RequestHeader>
   </soapenv:Header>
   <soapenv:Body>
      <ns1:mutate>
         <ns1:operations>
            <ns1:operator>ADD</ns1:operator>
            <ns1:accountId>100000001</ns1:accountId>
            <ns1:operand>
               <ns1:accountId>100000001</ns1:accountId>
               <ns1:feedFolderName>Sale product list</ns1:feedFolderName>
               <ns1:feedAttribute>
                  <ns1:feedAttributeName>Product</ns1:feedAttributeName>
                  <ns1:placeholderField>AD_CUSTOMIZER_STRING</ns1:placeholderField>
               </ns1:feedAttribute>
               <ns1:feedAttribute>
                  <ns1:feedAttributeName>Price</ns1:feedAttributeName>
                  <ns1:placeholderField>AD_CUSTOMIZER_PRICE</ns1:placeholderField>
               </ns1:feedAttribute>
               <ns1:feedAttribute>
                  <ns1:feedAttributeName>Last sale date</ns1:feedAttributeName>
                  <ns1:placeholderField>AD_CUSTOMIZER_DATE</ns1:placeholderField>
               </ns1:feedAttribute>
               <ns1:placeholderType>AD_CUSTOMIZER</ns1:placeholderType>
            </ns1:operand>
         </ns1:operations>
      </ns1:mutate>
   </soapenv:Body>
</soapenv:Envelope>
```

##### Response Sample
```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://ss.yahooapis.jp/V6">
   <SOAP-ENV:Header>
      <ns1:ResponseHeader>
         <ns1:service>FeedFolderService</ns1:service>
         <ns1:remainingQuota>-1</ns1:remainingQuota>
         <ns1:quotaUsedForThisRequest>-1</ns1:quotaUsedForThisRequest>
         <ns1:timeTakenMillis>1.2862</ns1:timeTakenMillis>
      </ns1:ResponseHeader>
   </SOAP-ENV:Header>
   <SOAP-ENV:Body>
      <ns1:mutateResponse>
         <ns1:rval>
            <ns1:ListReturnValue.Type>FeedFolderReturnValue</ns1:ListReturnValue.Type>
            <ns1:Operation.Type>ADD</ns1:Operation.Type>
            <ns1:values>
               <ns1:operationSucceeded>true</ns1:operationSucceeded>
               <ns1:feedFolder>
                  <ns1:accountId>100000001</ns1:accountId>
                  <ns1:feedFolderId>20001</ns1:feedFolderId>
                  <ns1:feedFolderName>Sale product list</ns1:feedFolderName>
                  <ns1:feedAttribute>
                     <ns1:feedAttributeId>1</ns1:feedAttributeId>
                     <ns1:feedAttributeName>Product</ns1:feedAttributeName>
                     <ns1:placeholderField>AD_CUSTOMIZER_STRING</ns1:placeholderField>
                  </ns1:feedAttribute>
                  <ns1:feedAttribute>
                     <ns1:feedAttributeId>2</ns1:feedAttributeId>
                     <ns1:feedAttributeName>Price</ns1:feedAttributeName>
                     <ns1:placeholderField>AD_CUSTOMIZER_PRICE</ns1:placeholderField>
                  </ns1:feedAttribute>
                  <ns1:feedAttribute>
                     <ns1:feedAttributeId>3</ns1:feedAttributeId>
                     <ns1:feedAttributeName>Last sale date</ns1:feedAttributeName>
                     <ns1:placeholderField>AD_CUSTOMIZER_DATE</ns1:placeholderField>
                  </ns1:feedAttribute>
                  <ns1:placeholderType>AD_CUSTOMIZER</ns1:placeholderType>
               </ns1:feedFolder>
            </ns1:values>
         </ns1:rval>
      </ns1:mutateResponse>
   </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

#### 2.	Adding FeedItem
Next, use FeedItemService to set data to be inserted or to be set to the FeedFolder that was created earlier.

##### Request Sample
```xml
<?xml version="1.0" encoding="UTF-8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://ss.yahooapis.jp/V6">
   <soapenv:Header>
      <ns1:RequestHeader>
         <ns1:license>XXXX-XXXX-XXXX-XXXX</ns1:license>
         <ns1:apiAccountId>XXXX-XXXX-XXXX-XXXX</ns1:apiAccountId>
         <ns1:apiAccountPassword>passwd</ns1:apiAccountPassword>
         <ns1:accountId>100000001</ns1:accountId>
         <ns1:onBehalfOfAccountId>XXXXX-XXXX-XXXXX-XXXX</ns1:onBehalfOfAccountId>
         <ns1:onBehalfOfPassword>passwd2</ns1:onBehalfOfPassword>
      </ns1:RequestHeader>
   </soapenv:Header>
   <soapenv:Body>
      <ns1:mutate>
         <ns1:operations>
            <ns1:operator>ADD</ns1:operator>
            <ns1:accountId>100000001</ns1:accountId>
            <ns1:placeholderType>AD_CUSTOMIZER</ns1:placeholderType>
            <ns1:operand>
               <ns1:accountId>100000001</ns1:accountId>
               <ns1:feedFolderId>20001</ns1:feedFolderId>
               <ns1:feedItemAttribute>
                  <ns1:placeholderField>AD_CUSTOMIZER_STRING</ns1:placeholderField>
                  <ns1:feedAttributeId>1</ns1:feedAttributeId>
                  <ns1:feedAttributeValue>Product 101</ns1:feedAttributeValue>
               </ns1:feedItemAttribute>
               <ns1:feedItemAttribute>
                  <ns1:placeholderField>AD_CUSTOMIZER_PRICE</ns1:placeholderField>
                  <ns1:feedAttributeId>2</ns1:feedAttributeId>
                  <ns1:feedAttributeValue>100</ns1:feedAttributeValue>
               </ns1:feedItemAttribute>
               <ns1:feedItemAttribute>
                  <ns1:placeholderField>AD_CUSTOMIZER_DATE</ns1:placeholderField>
                  <ns1:feedAttributeId>3</ns1:feedAttributeId>
                  <ns1:feedAttributeValue>20151231 000000</ns1:feedAttributeValue>
               </ns1:feedItemAttribute>
               <ns1:placeholderType>AD_CUSTOMIZER</ns1:placeholderType>
               <ns1:targetingCampaign>
                  <ns1:targetingCampaignId>500001</ns1:targetingCampaignId>
               </ns1:targetingCampaign>
               <ns1:targetingAdGroup>
                  <ns1:targetingAdGroupId>600001</ns1:targetingAdGroupId>
               </ns1:targetingAdGroup>
            </ns1:operand>
            <ns1:operand>
               <ns1:accountId>100000001</ns1:accountId>
               <ns1:feedFolderId>20001</ns1:feedFolderId>
               <ns1:feedItemAttribute>
                  <ns1:placeholderField>AD_CUSTOMIZER_STRING</ns1:placeholderField>
                  <ns1:feedAttributeId>1</ns1:feedAttributeId>
                  <ns1:feedAttributeValue>Product 102</ns1:feedAttributeValue>
               </ns1:feedItemAttribute>
               <ns1:feedItemAttribute>
                  <ns1:placeholderField>AD_CUSTOMIZER_PRICE</ns1:placeholderField>
                  <ns1:feedAttributeId>2</ns1:feedAttributeId>
                  <ns1:feedAttributeValue>300</ns1:feedAttributeValue>
               </ns1:feedItemAttribute>
               <ns1:feedItemAttribute>
                  <ns1:placeholderField>AD_CUSTOMIZER_DATE</ns1:placeholderField>
                  <ns1:feedAttributeId>3</ns1:feedAttributeId>
                  <ns1:feedAttributeValue>20151231 000000</ns1:feedAttributeValue>
               </ns1:feedItemAttribute>
               <ns1:placeholderType>AD_CUSTOMIZER</ns1:placeholderType>
               <ns1:targetingCampaign>
                  <ns1:targetingCampaignId>500001</ns1:targetingCampaignId>
               </ns1:targetingCampaign>
            </ns1:operand>
            <ns1:operand>
               <ns1:accountId>100000001</ns1:accountId>
               <ns1:feedFolderId>53161</ns1:feedFolderId>
               <ns1:feedItemAttribute>
                  <ns1:placeholderField>AD_CUSTOMIZER_STRING</ns1:placeholderField>
                  <ns1:feedAttributeId>1</ns1:feedAttributeId>
                  <ns1:feedAttributeValue>Product 103</ns1:feedAttributeValue>
               </ns1:feedItemAttribute>
               <ns1:feedItemAttribute>
                  <ns1:placeholderField>AD_CUSTOMIZER_PRICE</ns1:placeholderField>
                  <ns1:feedAttributeId>2</ns1:feedAttributeId>
                  <ns1:feedAttributeValue>1,000</ns1:feedAttributeValue>
               </ns1:feedItemAttribute>
               <ns1:feedItemAttribute>
                  <ns1:placeholderField>AD_CUSTOMIZER_DATE</ns1:placeholderField>
                  <ns1:feedAttributeId>3</ns1:feedAttributeId>
                  <ns1:feedAttributeValue>20151231 000000</ns1:feedAttributeValue>
               </ns1:feedItemAttribute>
               <ns1:placeholderType>AD_CUSTOMIZER</ns1:placeholderType>
               <ns1:targetingCampaign>
                  <ns1:targetingCampaignId>500001</ns1:targetingCampaignId>
               </ns1:targetingCampaign>
            </ns1:operand>
         </ns1:operations>
      </ns1:mutate>
   </soapenv:Body>
</soapenv:Envelope>
```

##### Response Sample
```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://ss.yahooapis.jp/V6">
   <SOAP-ENV:Header>
      <ns1:ResponseHeader>
         <ns1:service>FeedItemService</ns1:service>
         <ns1:remainingQuota>-1</ns1:remainingQuota>
         <ns1:quotaUsedForThisRequest>-1</ns1:quotaUsedForThisRequest>
         <ns1:timeTakenMillis>1.5086</ns1:timeTakenMillis>
      </ns1:ResponseHeader>
   </SOAP-ENV:Header>
   <SOAP-ENV:Body>
      <ns1:mutateResponse>
         <ns1:rval>
            <ns1:ListReturnValue.Type>FeedItemReturnValue</ns1:ListReturnValue.Type>
            <ns1:Operation.Type>ADD</ns1:Operation.Type>
            <ns1:values>
               <ns1:operationSucceeded>true</ns1:operationSucceeded>
               <ns1:feedItem>
                  <ns1:accountId>100000001</ns1:accountId>
                  <ns1:feedFolderId>20001</ns1:feedFolderId>
                  <ns1:feedItemId>30001</ns1:feedItemId>
                  <ns1:approvalStatus>REVIEW</ns1:approvalStatus>
                  <ns1:feedItemAttribute>
                     <ns1:placeholderField>AD_CUSTOMIZER_STRING</ns1:placeholderField>
                     <ns1:feedAttributeId>1</ns1:feedAttributeId>
                     <ns1:feedAttributeValue>Product 101</ns1:feedAttributeValue>
                  </ns1:feedItemAttribute>
                  <ns1:feedItemAttribute>
                     <ns1:placeholderField>AD_CUSTOMIZER_PRICE</ns1:placeholderField>
                     <ns1:feedAttributeId>2</ns1:feedAttributeId>
                     <ns1:feedAttributeValue>100</ns1:feedAttributeValue>
                  </ns1:feedItemAttribute>
                  <ns1:feedItemAttribute>
                     <ns1:placeholderField>AD_CUSTOMIZER_DATE</ns1:placeholderField>
                     <ns1:feedAttributeId>4</ns1:feedAttributeId>
                     <ns1:feedAttributeValue>20151231 000000</ns1:feedAttributeValue>
                  </ns1:feedItemAttribute>
                  <ns1:placeholderType>AD_CUSTOMIZER</ns1:placeholderType>
                  <ns1:targetingCampaign>
                     <ns1:targetingCampaignId>868992</ns1:targetingCampaignId>
                  </ns1:targetingCampaign>
                  <ns1:targetingAdGroup>
                     <ns1:targetingAdGroupId>308006520</ns1:targetingAdGroupId>
                  </ns1:targetingAdGroup>
               </ns1:feedItem>
            </ns1:values>
            <ns1:values>
               <ns1:operationSucceeded>true</ns1:operationSucceeded>
               <ns1:feedItem>
                  <ns1:accountId>100000001</ns1:accountId>
                  <ns1:feedFolderId>20001</ns1:feedFolderId>
                  <ns1:feedItemId>30001</ns1:feedItemId>
                  <ns1:approvalStatus>REVIEW</ns1:approvalStatus>
                  <ns1:feedItemAttribute>
                     <ns1:placeholderField>AD_CUSTOMIZER_STRING</ns1:placeholderField>
                     <ns1:feedAttributeId>1</ns1:feedAttributeId>
                     <ns1:feedAttributeValue>Product 102</ns1:feedAttributeValue>
                  </ns1:feedItemAttribute>
                  <ns1:feedItemAttribute>
                     <ns1:placeholderField>AD_CUSTOMIZER_PRICE</ns1:placeholderField>
                     <ns1:feedAttributeId>2</ns1:feedAttributeId>
                     <ns1:feedAttributeValue>300</ns1:feedAttributeValue>
                  </ns1:feedItemAttribute>
                  <ns1:feedItemAttribute>
                     <ns1:placeholderField>AD_CUSTOMIZER_DATE</ns1:placeholderField>
                     <ns1:feedAttributeId>4</ns1:feedAttributeId>
                     <ns1:feedAttributeValue>20151231 000000</ns1:feedAttributeValue>
                  </ns1:feedItemAttribute>
                  <ns1:placeholderType>AD_CUSTOMIZER</ns1:placeholderType>
                  <ns1:targetingCampaign>
                     <ns1:targetingCampaignId>868992</ns1:targetingCampaignId>
                  </ns1:targetingCampaign>
               </ns1:feedItem>
            </ns1:values>
            <ns1:values>
               <ns1:operationSucceeded>true</ns1:operationSucceeded>
               <ns1:feedItem>
                  <ns1:accountId>100000001</ns1:accountId>
                  <ns1:feedFolderId>20001</ns1:feedFolderId>
                  <ns1:feedItemId>30001</ns1:feedItemId>
                  <ns1:approvalStatus>REVIEW</ns1:approvalStatus>
                  <ns1:feedItemAttribute>
                     <ns1:placeholderField>AD_CUSTOMIZER_STRING</ns1:placeholderField>
                     <ns1:feedAttributeId>1</ns1:feedAttributeId>
                     <ns1:feedAttributeValue>Product 103</ns1:feedAttributeValue>
                  </ns1:feedItemAttribute>
                  <ns1:feedItemAttribute>
                     <ns1:placeholderField>AD_CUSTOMIZER_PRICE</ns1:placeholderField>
                     <ns1:feedAttributeId>2</ns1:feedAttributeId>
                     <ns1:feedAttributeValue>1,000</ns1:feedAttributeValue>
                  </ns1:feedItemAttribute>
                  <ns1:feedItemAttribute>
                     <ns1:placeholderField>AD_CUSTOMIZER_DATE</ns1:placeholderField>
                     <ns1:feedAttributeId>3</ns1:feedAttributeId>
                     <ns1:feedAttributeValue>20151231 000000</ns1:feedAttributeValue>
                  </ns1:feedItemAttribute>
                  <ns1:placeholderType>AD_CUSTOMIZER</ns1:placeholderType>
                  <ns1:targetingCampaign>
                     <ns1:targetingCampaignId>868993</ns1:targetingCampaignId>
                  </ns1:targetingCampaign>
               </ns1:feedItem>
            </ns1:values>
         </ns1:rval>
      </ns1:mutateResponse>
   </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

#### 3.	Adding AdGroupAd
Then, use AdGroupAdService to create ads to be inserted added data to.<br>
In this example, two of different ads are created since Ad Customizer requires to enable ordinary ads and ads to be inserted data automatically.<br>
*Cannot use BulkService to submit ads.<br>
[Tips]<br>
Using 'COUNTDOWN' feature will enable to display remaining minutes of discount sales and campaign within the ad. And ad delivery can be paused at the same time as the end of countdown. <br>



##### Request Sample
```xml
<?xml version="1.0" encoding="UTF-8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:ns1="http://ss.yahooapis.jp/V6">
   <soapenv:Header>
      <ns1:RequestHeader>
         <ns1:license>XXXX-XXXX-XXXX-XXXX</ns1:license>
         <ns1:apiAccountId>XXXX-XXXX-XXXX-XXXX</ns1:apiAccountId>
         <ns1:apiAccountPassword>passwd</ns1:apiAccountPassword>
         <ns1:accountId>100000001</ns1:accountId>
         <ns1:onBehalfOfAccountId>XXXXX-XXXX-XXXXX-XXXX</ns1:onBehalfOfAccountId>
         <ns1:onBehalfOfPassword>passwd2</ns1:onBehalfOfPassword>
      </ns1:RequestHeader>
   </soapenv:Header>
   <soapenv:Body>
      <ns1:mutate>
         <ns1:operations>
            <ns1:operator>ADD</ns1:operator>
            <ns1:accountId>100000001</ns1:accountId>
            <!--1 or more repetitions:-->
            <ns1:operand>
               <ns1:accountId>100000001</ns1:accountId>
               <ns1:campaignId>1001</ns1:campaignId>
               <ns1:adGroupId>10001</ns1:adGroupId>
               <ns1:adName>Best Practice Ad</ns1:adName>
               <ns1:userStatus>ACTIVE</ns1:userStatus>
               <ns1:ad xsi:type="ns1:TextAd2">
                  <ns1:type>TEXT_AD2</ns1:type>
                  <ns1:url>http://www.example.jp</ns1:url>
                  <ns1:displayUrl>www.example.jp</ns1:displayUrl>
                  <ns1:headline>人気の{=Sale product list.Product}が大特価</ns1:headline>
                  <ns1:description>{=Sale product list.Price}円で販売。</ns1:description>
                  <ns1:description2>終了まであと{=COUNTDOWN(Sale product list.Last sale date,"ja")}</ns1:description2>
               </ns1:ad>
            </ns1:operand>
            <ns1:operand>
               <ns1:accountId>100000001</ns1:accountId>
               <ns1:campaignId>1002</ns1:campaignId>
               <ns1:adName>Best Practice Normal Ad</ns1:adName>
               <ns1:userStatus>ACTIVE</ns1:userStatus>
               <ns1:ad xsi:type="ns1:TextAd2">
                  <ns1:type>TEXT_AD2</ns1:type>
                  <ns1:url>http://www.example.jp</ns1:url>
                  <ns1:displayUrl>www.example.jp</ns1:displayUrl>
                  <ns1:headline>人気の商品が大特価</ns1:headline>
                  <ns1:description>期間限定特別価格で販売。</ns1:description>
                  <ns1:description2>１２月３１日まで</ns1:description2>
               </ns1:ad>
            </ns1:operand>
         </ns1:operations>
      </ns1:mutate>
   </soapenv:Body>
</soapenv:Envelope>
```

##### Response Sample
```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://ss.yahooapis.jp/V6" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
   <SOAP-ENV:Header>
      <ns1:ResponseHeader>
         <ns1:service>AdGroupAdService</ns1:service>
         <ns1:remainingQuota>1</ns1:remainingQuota>
         <ns1:quotaUsedForThisRequest>2</ns1:quotaUsedForThisRequest>
         <ns1:timeTakenMillis>1.1128</ns1:timeTakenMillis>
      </ns1:ResponseHeader>
   </SOAP-ENV:Header>
   <SOAP-ENV:Body>
      <ns1:mutateResponse>
         <ns1:rval>
            <ns1:ListReturnValue.Type>AdGroupAdReturnValue</ns1:ListReturnValue.Type>
            <ns1:Operation.Type>ADD</ns1:Operation.Type>
            <ns1:values>
               <ns1:operationSucceeded>true</ns1:operationSucceeded>
               <ns1:adGroupAd>
                  <ns1:accountId>100000001</ns1:accountId>
                  <ns1:campaignId>1001</ns1:campaignId>
                  <ns1:campaignName>Best Practice Campaign</ns1:campaignName>
                  <ns1:adGroupId>10001</ns1:adGroupId>
                  <ns1:adGroupName>Best Practice AdGroup</ns1:adGroupName>
                  <ns1:adId>100001</ns1:adId>
                  <ns1:adTrackId>0</ns1:adTrackId>
                  <ns1:adName>Best Practice Ad</ns1:adName>
                  <ns1:userStatus>ACTIVE</ns1:userStatus>
                  <ns1:approvalStatus>REVIEW</ns1:approvalStatus>
                  <ns1:ad xsi:type="ns1:TextAd2">
                     <ns1:type>TEXT_AD2</ns1:type>
                     <ns1:url>http://www.example.jp</ns1:url>
                     <ns1:displayUrl>www.example.jp</ns1:displayUrl>
                     <ns1:headline>人気の{=Sale product list.Product}が大特価</ns1:headline>
                     <ns1:description>{=Sale product list.Price}円で販売。</ns1:description>
                     <ns1:description2>終了まであと{=COUNTDOWN(Sale product list.Last sale date,"ja")}</ns1:description2>
                  </ns1:ad>
                  <ns1:feedFolderId>20001</ns1:feedFolderId>
               </ns1:adGroupAd>
            </ns1:values>
            <ns1:values>
               <ns1:operationSucceeded>true</ns1:operationSucceeded>
               <ns1:adGroupAd>
                  <ns1:accountId>100000001</ns1:accountId>
                  <ns1:campaignId>1002</ns1:campaignId>
                  <ns1:campaignName>Best Practice Campaign</ns1:campaignName>
                  <ns1:adGroupId>10001</ns1:adGroupId>
                  <ns1:adGroupName>Best Practice AdGroup</ns1:adGroupName>
                  <ns1:adId>100001</ns1:adId>
                  <ns1:adTrackId>0</ns1:adTrackId>
                  <ns1:adName>Best Practice Normal Ad</ns1:adName>
                  <ns1:userStatus>ACTIVE</ns1:userStatus>
                  <ns1:approvalStatus>REVIEW</ns1:approvalStatus>
                  <ns1:ad xsi:type="ns1:TextAd2">
                     <ns1:type>TEXT_AD2</ns1:type>
                     <ns1:url>http://www.example.jp</ns1:url>
                     <ns1:displayUrl>www.example.jp</ns1:displayUrl>
                     <ns1:headline>人気の商品が大特価</ns1:headline>
                     <ns1:description>期間限定特別価格で販売。</ns1:description>
                     <ns1:description2>１２月３１日まで</ns1:description2>
                  </ns1:ad>
               </ns1:adGroupAd>
            </ns1:values>
         </ns1:rval>
      </ns1:mutateResponse>
   </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

#### 4.	Change of FeedItem
Since some price changes occurred after creating ads, following data revision is required.<br>
Ad Customizers can change ad creatives automatically only with data updates, using FeedItemService.

##### Sale product list (After the change)
<table class="standard">
                <tr>
                    <th valign="top" >
                        <p>Product (String)</p>
                    </th>
                    <th valign="top" >
                        <p>Price (Price)</p>
                    </th>
                    <th valign="top">
                        <p>Final sale date (Date)</p>
                    </th>
                    <th valign="top" >
                        <p>CampaignId</p>
                    </th>
                    <th valign="top" >
                        <p>AdGroupId</p>
                    </th>
                </tr>
                <tr>
                    <td valign="top">
                        <p>Product 101</p>
                    </td>
                    <td valign="top">
                        <p>90</p>
                    </td>
                    <td valign="top">
                        <p>20151231 000000</p>
                    </td>
                    <td valign="top">
                        <p>500001</p>
                    </td>
                    <td valign="top">
                        <p>600001</p>
                    </td>
                </tr>
                <tr>
                    <td valign="top">
                        <p>Product 102</p>
                    </td>
                    <td valign="top">
                        <p>350</p>
                    </td>
                    <td valign="top">
                        <p>20151231 000000</p>
                    </td>
                    <td valign="top">
                        <p>500001</p>
                    </td>
                    <td valign="top">
                        <p> </p>
                    </td>
                </tr>
                <tr>
                    <td valign="top">
                        <p>Product 103</p>
                    </td>
                    <td valign="top">
                        <p>1,000</p>
                    </td>
                    <td valign="top">
                        <p>20151231 000000</p>
                    </td>
                    <td valign="top">
                        <p>500002</p>
                    </td>
                    <td valign="top">
                        <p> </p>
                    </td>
                </tr>
</table>

##### Request Sample
```xml
<?xml version="1.0" encoding="UTF-8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://ss.yahooapis.jp/V6">
   <soapenv:Header>
      <ns1:RequestHeader>
         <ns1:license>XXXX-XXXX-XXXX-XXXX</ns1:license>
         <ns1:apiAccountId>XXXX-XXXX-XXXX-XXXX</ns1:apiAccountId>
         <ns1:apiAccountPassword>passwd</ns1:apiAccountPassword>
         <ns1:accountId>100000001</ns1:accountId>
         <ns1:onBehalfOfAccountId>XXXXX-XXXX-XXXXX-XXXX</ns1:onBehalfOfAccountId>
         <ns1:onBehalfOfPassword>passwd2</ns1:onBehalfOfPassword>
      </ns1:RequestHeader>
   </soapenv:Header>
   <soapenv:Body>
      <ns1:mutate>
         <ns1:operations>
            <ns1:operator>SET</ns1:operator>
            <ns1:accountId>100000001</ns1:accountId>
            <ns1:placeholderType>AD_CUSTOMIZER</ns1:placeholderType>
            <ns1:operand>
               <ns1:accountId>100000001</ns1:accountId>
               <ns1:feedFolderId>200001</ns1:feedFolderId>
               <ns1:feedItemId>300001</ns1:feedItemId>
               <ns1:feedItemAttribute>
                  <ns1:placeholderField>AD_CUSTOMIZER_PRICE</ns1:placeholderField>
                  <ns1:feedAttributeId>2</ns1:feedAttributeId>
                  <ns1:feedAttributeValue>90</ns1:feedAttributeValue>
               </ns1:feedItemAttribute>
               <ns1:placeholderType>AD_CUSTOMIZER</ns1:placeholderType>
               <ns1:targetingCampaign>
                  <ns1:targetingCampaignId>500001</ns1:targetingCampaignId>
               </ns1:targetingCampaign>
               <ns1:targetingAdGroup>
                  <ns1:targetingAdGroupId>600001</ns1:targetingAdGroupId>
               </ns1:targetingAdGroup>
            </ns1:operand>
            <ns1:operand>
               <ns1:accountId>100000001</ns1:accountId>
               <ns1:feedFolderId>200001</ns1:feedFolderId>
               <ns1:feedItemId>300001</ns1:feedItemId>
               <ns1:feedItemAttribute>
                  <ns1:placeholderField>AD_CUSTOMIZER_PRICE</ns1:placeholderField>
                  <ns1:feedAttributeId>2</ns1:feedAttributeId>
                  <ns1:feedAttributeValue>350</ns1:feedAttributeValue>
               </ns1:feedItemAttribute>
               <ns1:placeholderType>AD_CUSTOMIZER</ns1:placeholderType>
               <ns1:targetingCampaign>
                  <ns1:targetingCampaignId>500001</ns1:targetingCampaignId>
               </ns1:targetingCampaign>
            </ns1:operand>
            <ns1:operand>
               <ns1:accountId>100000001</ns1:accountId>
               <ns1:feedFolderId>200001</ns1:feedFolderId>
               <ns1:feedItemId>300001</ns1:feedItemId>
               <ns1:placeholderType>AD_CUSTOMIZER</ns1:placeholderType>
               <ns1:targetingCampaign>
                  <ns1:targetingCampaignId>500001</ns1:targetingCampaignId>
               </ns1:targetingCampaign>
            </ns1:operand>
         </ns1:operations>
      </ns1:mutate>
   </soapenv:Body>
</soapenv:Envelope>
```

##### Response Sample
```xml
<?xml version="1.0" encoding="UTF-8"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:ns1="http://ss.yahooapis.jp/V6">
   <SOAP-ENV:Header>
      <ns1:ResponseHeader>
         <ns1:service>FeedItemService</ns1:service>
         <ns1:remainingQuota>9993</ns1:remainingQuota>
         <ns1:quotaUsedForThisRequest>3</ns1:quotaUsedForThisRequest>
         <ns1:timeTakenMillis>1.1774</ns1:timeTakenMillis>
      </ns1:ResponseHeader>
   </SOAP-ENV:Header>
   <SOAP-ENV:Body>
      <ns1:mutateResponse>
         <ns1:rval>
            <ns1:ListReturnValue.Type>FeedItemReturnValue</ns1:ListReturnValue.Type>
            <ns1:Operation.Type>SET</ns1:Operation.Type>
            <ns1:values>
               <ns1:operationSucceeded>true</ns1:operationSucceeded>
               <ns1:feedItem>
                  <ns1:accountId>100000001</ns1:accountId>
                  <ns1:feedFolderId>200001</ns1:feedFolderId>
                  <ns1:feedItemId>300001</ns1:feedItemId>
                  <ns1:approvalStatus>APPROVED_WITH_REVIEW</ns1:approvalStatus>
                  <ns1:feedItemAttribute>
                     <ns1:placeholderField>AD_CUSTOMIZER_STRING</ns1:placeholderField>
                     <ns1:feedAttributeId>1</ns1:feedAttributeId>
                     <ns1:feedAttributeValue>Product 101</ns1:feedAttributeValue>
                  </ns1:feedItemAttribute>
                  <ns1:feedItemAttribute>
                     <ns1:placeholderField>AD_CUSTOMIZER_PRICE</ns1:placeholderField>
                     <ns1:feedAttributeId>2</ns1:feedAttributeId>
                     <ns1:feedAttributeValue>90</ns1:feedAttributeValue>
                  </ns1:feedItemAttribute>
                  <ns1:feedItemAttribute>
                     <ns1:placeholderField>AD_CUSTOMIZER_DATE</ns1:placeholderField>
                     <ns1:feedAttributeId>3</ns1:feedAttributeId>
                     <ns1:feedAttributeValue>20151231 000000</ns1:feedAttributeValue>
                  </ns1:feedItemAttribute>
                  <ns1:placeholderType>AD_CUSTOMIZER</ns1:placeholderType>
                  <ns1:targetingCampaign>
                     <ns1:targetingCampaignId>500001</ns1:targetingCampaignId>
                  </ns1:targetingCampaign>
                  <ns1:targetingAdGroup>
                     <ns1:targetingAdGroupId>600001</ns1:targetingAdGroupId>
                  </ns1:targetingAdGroup>
               </ns1:feedItem>
            </ns1:values>
            <ns1:values>
               <ns1:operationSucceeded>true</ns1:operationSucceeded>
               <ns1:feedItem>
                  <ns1:accountId>100000001</ns1:accountId>
                  <ns1:feedFolderId>200001</ns1:feedFolderId>
                  <ns1:feedItemId>300001</ns1:feedItemId>
                  <ns1:approvalStatus>APPROVED_WITH_REVIEW</ns1:approvalStatus>
                  <ns1:feedItemAttribute>
                     <ns1:placeholderField>AD_CUSTOMIZER_STRING</ns1:placeholderField>
                     <ns1:feedAttributeId>1</ns1:feedAttributeId>
                     <ns1:feedAttributeValue>Product 102</ns1:feedAttributeValue>
                  </ns1:feedItemAttribute>
                  <ns1:feedItemAttribute>
                     <ns1:placeholderField>AD_CUSTOMIZER_PRICE</ns1:placeholderField>
                     <ns1:feedAttributeId>2</ns1:feedAttributeId>
                     <ns1:feedAttributeValue>350</ns1:feedAttributeValue>
                  </ns1:feedItemAttribute>
                  <ns1:feedItemAttribute>
                     <ns1:placeholderField>AD_CUSTOMIZER_DATE</ns1:placeholderField>
                     <ns1:feedAttributeId>3</ns1:feedAttributeId>
                     <ns1:feedAttributeValue>20151231 000000</ns1:feedAttributeValue>
                  </ns1:feedItemAttribute>
                  <ns1:placeholderType>AD_CUSTOMIZER</ns1:placeholderType>
                  <ns1:targetingCampaign>
                     <ns1:targetingCampaignId>500001</ns1:targetingCampaignId>
                  </ns1:targetingCampaign>
               </ns1:feedItem>
            </ns1:values>
            <ns1:values>
               <ns1:operationSucceeded>true</ns1:operationSucceeded>
               <ns1:feedItem>
                  <ns1:accountId>100000001</ns1:accountId>
                  <ns1:feedFolderId>200001</ns1:feedFolderId>
                  <ns1:feedItemId>300001</ns1:feedItemId>
                  <ns1:approvalStatus>APPROVED_WITH_REVIEW</ns1:approvalStatus>
                  <ns1:feedItemAttribute>
                     <ns1:placeholderField>AD_CUSTOMIZER_STRING</ns1:placeholderField>
                     <ns1:feedAttributeId>1</ns1:feedAttributeId>
                     <ns1:feedAttributeValue>Product 103</ns1:feedAttributeValue>
                  </ns1:feedItemAttribute>
                  <ns1:feedItemAttribute>
                     <ns1:placeholderField>AD_CUSTOMIZER_PRICE</ns1:placeholderField>
                     <ns1:feedAttributeId>2</ns1:feedAttributeId>
                     <ns1:feedAttributeValue>1,000</ns1:feedAttributeValue>
                  </ns1:feedItemAttribute>
                  <ns1:feedItemAttribute>
                     <ns1:placeholderField>AD_CUSTOMIZER_DATE</ns1:placeholderField>
                     <ns1:feedAttributeId>3</ns1:feedAttributeId>
                     <ns1:feedAttributeValue>20151231 000000</ns1:feedAttributeValue>
                  </ns1:feedItemAttribute>
                  <ns1:placeholderType>AD_CUSTOMIZER</ns1:placeholderType>
                  <ns1:targetingCampaign>
                     <ns1:targetingCampaignId>500001</ns1:targetingCampaignId>
                  </ns1:targetingCampaign>
               </ns1:feedItem>
            </ns1:values>
         </ns1:rval>
      </ns1:mutateResponse>
   </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```
