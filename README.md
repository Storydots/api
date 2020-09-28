Welcome to the StoryDots API documentation. This API allows you to integrate [StoryDots](https://storydots.app) to your Shopping cart experience providing your clients with the possibillity to send virtual video greeting cards with their gifts, atttached to a physical QR Tag the receiving party can scan to see the video and engage in the experience.

For more information about this service and to purchase your API key with a pre-charged QR Tags quota, please contact sales@storydots.app.

In order to test, you will need to request a sandbox API Key needed to get Tag codes and QR Tags. If you already bought your API Key, please send us a note to hello@storydots.app.

This API should be integrated in your shopping cart and there are two simple steps you need to follow in order to do this:

1. You should get a Tag code once the purchase _is confirmed_ (This is important since every time you get a Tag code, it will be deducted from your balance) and store the _videoUrl_ since you will need to present it to the user so that he can upload his video. (you can do it on screen, via email or both)
2. You can use the Tag code to retrieve the QR Tag so that it can be printed and added to the gift's packaging.

## **Retrieving new Tag Codes**

- **URL**

  _/tag_

- **Method:**

  `GET` - retrieves a new Tag code

- **Query Params**

  <_There are no Query Params needed for this API endpoint_>

- **Request Headers**

  **x-api-key:** _Your API Key_

- **Success Response:**

  This method will return a new, unique Tag code associated with your API key. This code identifies an active StoryDots tag. Each time you call this method you will get a new code so the overall code balance will be deducted. Please be careful in calling this method and make sure the returned code is saved for later use.

  - **Code:** 200 <br />
    **Content:** `{ "statusCode": 200, "tagCode": "[NEW-TAG-CODE]" "videoUrl": "[ACTIVE-VIDEO-URL]" }`

- **Error Response:**

  - **Code:** 403 FORBIDDEN <br />
    **Content:** `{ "message": "Forbidden" }`

  - **Code:** 403 FORBIDDEN <br />
    **Content:** `{ "message": 'Out of tags, contact support' }`

- **Sample Call:**

  _`curl -X GET \`_  
  _`https://api.storydots.app/tag \`_  
  _`-H 'cache-control: no-cache' \`_  
  _`-H 'x-api-key: [YOUR-API-KEY]'`_

## **Retrieving QR Tag image**

- **URL**

  _/qr/[TAG-CODE]_

- **Method:**

  `GET` - retrieves a PNG image of the corresponding QR Tag

- **Path Params**

  **[TAG-CODE]:** _The Tag code you want to retrieve the QR Tag image from_

- **Request Headers**

  <_There are no Request Headers needed for this API endpoint_>

- **Success Response:**

  This method will return a PNG image with a QR code associated to the provided Tag code. You should print this QR Tag image and attach it to the gift's packaging.

  - **Code:** 200 OK<br />
    **Content:**
    `image/png with the binary PNG image in the body`

- **Error Response:**

  - **Code:** 404 NOT FOUND <br />
    **Content:** `{}`

- **Sample Call:**

  _`curl -X GET \`_  
  _`https://api.storydots.app/qr/[QR-CODE] \`_  
  _`-H 'cache-control: no-cache' \`_

- **Notes:**

  For any questions please send an email to hello@storydots.app
