# Develop a REST API using ACE Toolkit to interact with MQ.

This article explains the steps need to create an Integration Flow developed with *ACE Toolkit* that uses the *REST API* functionality as well as the *MQ Nodes* to interact with an **MQ Queue Manager** using the latest version of the **ACE Integration Server Certified Container (ACEcc)** as part of the *IBM Cloud Pak for Integration (CP4I)*.

## Low Code / No Code Development with ACE Toolkit.

1. Open the Toolkit in your workstation and create a new REST API project as shown below.

![ACE Toolkit REST API with MQ Step 1](images/2022-06-28_12-23-53.png)

2. Give a name to your project, i.e. *MQAPI* and then select the option to *Import resources* since we will leverage a definition already created.

![ACE Toolkit REST API with MQ Step 2](images/2022-06-28_12-25-32.png)

3. In the wizard click *Browse* and navigate to the location where the OpenAPI file definition is located.

![ACE Toolkit REST API with MQ Step 3](images/2022-06-28_12-26-19.png)

4. Once the path is displayed in the *Location* field click *Finish*.

![ACE Toolkit REST API with MQ Step 4](images/2022-06-28_12-28-17.png)

5. The REST API will be displayed, scroll to the right if needed to open the sunflow operation as shown in the image to proceed to implement the API logic.

![ACE Toolkit REST API with MQ Step 5](images/2022-06-28_12-31-05.png)

6. The *Message Flow Editor* will be open with only the *Input* and *Output* terminals. Double click the tab to maximize the editor and work with the flow.

![ACE Toolkit REST API with MQ Step 6](images/2022-06-28_12-32-33.png)

7. Drag and drop the *Nodes* from the palette to implemeng the "logic". In this case we will use the following nodes:
  * Flow Order Node,
  * HTTP Header Node,
  * MQ Header Node,
  * MQ Output Node, and
  * Mapping Node.

    And you will proceed to wire them. The flow should look like the one below. Once you are done double click the tab again in order to access the properties for each node.
![ACE Toolkit REST API with MQ Step 7](images/2022-06-28_12-37-45.png)

8. Now we will configure each node, starting with the *HTTP Header Node*. Click on it to bring it to focus and then select the *HTTP Input* tab followed by the *Delete header* option as shown below.

![ACE Toolkit REST API with MQ Step 8](images/2022-06-28_12-40-26.png)

9. Now select the *MQ Header Node* and navigate to the *MQMD* tab enabling the *Add header* option. And selecting *MQMFT_STRING* for the *Format* field as shown below.

![ACE Toolkit REST API with MQ Step 9](images/2022-06-28_13-01-52.png)

10. Then select the *MQ Output Node* and in the *Basic* tab enter the name of the queue we will use to put the messages, in this case *CP4I.DEMO.API.Q*

![ACE Toolkit REST API with MQ Step 10](images/2022-06-28_13-04-48.png)

11. In the same *MQ Output Node* navigate to the *MQ Connection* tab enter the information to connect to the Queue Manager. The information is based on the configuration we used for MQ, and for simplicity is included below.

Property | Value
---------|-------
Connection | ***MQ client connection properties***
Destination queue manager name | ***QMGRDEMO***
Queue manager host name | ***qmgr-demo-ibm-mq***
Listener port number | ***1414***
Channel name | ***ACE.TO.MQ***

![ACE Toolkit REST API with MQ Step 11](images/2022-06-28_13-07-42.png)

12. Now double click the *Mapping Node*,

![ACE Toolkit REST API with MQ Step 12](images/2022-06-28_13-08-43.png)

13. In the wizard window simply click *Finish*.

![ACE Toolkit REST API with MQ Step 13](images/2022-06-28_13-09-14.png)

14. Expand the *JSON* section in both the input and output message assemblies and connect the *payload* as shown below.  

![ACE Toolkit REST API with MQ Step 14](images/2022-06-28_13-11-15.png)

15. Then *right click* the *code* field and select *Add Assign* from the menu.

![ACE Toolkit REST API with MQ Step 15](images/2022-06-28_14-45-30.png)

16. In the properties section enter ***CP4I0000*** in the *value* field.

![ACE Toolkit REST API with MQ Step 16](images/2022-06-28_14-46-24.png)

17. Repeat the same process for field *msg* and assign the value ***Request has been processed***

18. Do the same for field *time* but this time we will replace the *Assign* option with the *current-time* function as shown below.

![ACE Toolkit REST API with MQ Step 18](images/2022-06-28_14-47-50.png)

19. The integration flow is completed. Save your progress and close the *mapping* tab.

![ACE Toolkit REST API with MQ Step 19](images/2022-06-28_14-48-57.png)

20. Now we will generate the BAR file that we will use to deploy the Integration into CP4I. From the *File* menu select *New* and then *BAR file* as shown below.

![ACE Toolkit REST API with MQ Step 20](images/2022-06-28_14-50-45.png)

21. In the pop up window enter the name of the BAR file, in this case ***CP4IACEMQAPIPREM***. And then click *Finish*.

![ACE Toolkit REST API with MQ Step 21](images/2022-06-28_14-52-42.png)

22. Click *OK* in the confirmation window and the BAR file is ready to be deployed.

![ACE Toolkit REST API with MQ Step 22](images/2022-06-28_14-54-12.png)
