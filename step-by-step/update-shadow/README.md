#### Ingredients
## Update Shadow <a id="title"></a>


This skill includes an Intent called ```CityIntent``` with a slot called ```city```, that is of type ```AMAZON.EUROPE_CITY```.

The user will say: ```go to London``` and the skill will update the IOT Device Shadow with the name of the city.

#### Instructions for deploying this sample skill
#### Ingredients
## 2. Create the Skill <a id="title"></a>
<hr />


1. Login to [developer.amazon.com](https://developer.amazon.com) and click Alexa, then Alexa Skills Kit.
1. Create a new Skill called **city browser** with invocation name ```city browser```.
1. Paste in the [IntentSchema.json](./speechAssets/IntentSchema.json) :

```
{
  "intents": [
    {
      "intent": "MyIntent",  "slots":[]
    },
    {
      "intent": "CityIntent",
      "slots":[
        {
          "name":"city",
          "type":"AMAZON.EUROPE_CITY"
      }
      ]
    },
    {
      "intent": "AMAZON.HelpIntent"
    },
    {
      "intent": "AMAZON.StopIntent"
    },
    {
      "intent": "AMAZON.CancelIntent"
    }
  ]
}

```

1. Paste in the [SampleUtterances.txt](speechAssets/SampleUtterances.txt) :

```
MyIntent hello
CityIntent go to {city}
CityIntent i am from {city}
```

Pause here and leave this browser tab open.

#### Continue to the next step

 * Part 3
#### Ingredients
## 3. Create the Lambda Function <a id="title"></a>
<hr />
*Leave the default values for any form inputs not described below.  To complete each page you will usually scroll down and find the blue button.*

1. Login to AWS and verify the region at the top right is set to either **Ireland** or **N. Virginia** Region region.
1. Click [Lambda](https://console.aws.amazon.com/lambda/home) and then **Create a Lambda function**  Do not select the default **Blank** blueprint.
1. Locate and click on the ```alexa-skill-kit-sdk-factskill``` skill template (hint: search for **fact** )
1. Click in the empty square and choose the trigger *Alexa Skills Kit* and click Next.
  + ![Alexa Skills Kit Trigger](https://m.media-amazon.com/images/G/01/cookbook/trigger._TTH_.png)
1. Give your function the name *HelloWorld*
1. Select all the existing Javascript code and delete it!
1. Paste in the source code from [src/index.js](./src/index.js)
1. Scroll down past the code editor and environment variables and find the **Role** dropdown.  Create a custom role or re-use an execution role, such as ```lambda_basic_execution```
1. Click Next and create the function.
1. Press the blue TEST button to begin a unit test.  Choose the event template called Alexa Start Session.
1. Notice Lambda ARN, shown near the top right, such as
 *  ``` arn:aws:lambda:us-east-1:333304287777:function:HelloWorld ```


#### Continue to the next step


 * Part 4 
#### Ingredients
## 4. Connect your skill to Lambda <a id="title"></a>
<hr />

Here is how to copy and paste your Lambda function ARN to the Skill endpoint.

1. Within the AWS Lambda function page, the ARN, or Amazon Resource Name, is shown near the top right, such as
 *  ``` arn:aws:lambda:us-east-1:333304287777:function:HelloWorld ```
1. Copy this ARN
 + ![Amazon Resource Name](https://m.media-amazon.com/images/G/01/cookbook/arn._TTH_.png)
1. Go to the browser tab at ```developer.amazon.com``` and navigate into your skill's Configuration page.
1. Click the radio button for Service Endpoint Type: AWS Lambda ARN
1. Pick a geographical region that is closest to your target customers
1. Click into the textbox that appears, and Paste.
1. Scroll down and click Save.
1. You should see a green checkbox next to the Configuration menu item.
1. If you get an error, confirm you have previously added an ASK Trigger to your Lambda function.



#### Add IOT permissions to your Lambda IAM Role

1. Within the AWS IAM console, locate and click on the role used by your Lambda function, such as ```lambda_basic_execution```
1. Click the blue button to add ```AWSIoTFullAccess``` policy. to this role.

```AWSIoTFullAccess``` will work fine for testing, however in a production setting, you would want to define a finer-grained set of limited permissions for your Lambda function role.

The following IAM Policy can be modified and attached to your Lambda function's IAM role to only allow updating a specific Thing.
See the [IAM Policies](../IAM_POLICIES.md) page for more details.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "iot:UpdateThingShadow"
      ],
      "Resource":["arn:aws:iot:eu-west-1:589662380000:thing/thing1"],
    }
  ]
}
```

 *You can learn more from the [Getting Started with AWS IOT](https://aws.amazon.com/iot-platform/getting-started/) documentation.*


#### Test your skill

* Open your skill and say 'hello'.  Verify the response is as expected.
* Say something like "reisen nach Frankfurt" or "go to Belfast" or "go to Berlin".


#### Add the dynamic web page
 * Create the single-page [webapp-thing](../webapp-thing/README.md#title)



<hr />
Back to the [Home Page](../../README.md#title)

<hr />
Back to the [Home Page](../../README.md#title)

<hr />
Back to the [Home Page](../../README.md#title)

<hr />
