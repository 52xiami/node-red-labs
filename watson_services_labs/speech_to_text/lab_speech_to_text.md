#Speech to Text

Note: To use the Speech To Text node we ran into some restrictions, which will be solved soon. This is why this lab is based on a stand-alone system.

Speech to Text service can be used anywhere voice-interactivity is needed. The service is great for mobile experiences, transcribing media files, call center transcriptions, voice control of embedded systems, or converting sound to text to then make data searchable. Supported languages include:
- US English 
- Spanish 
- Japanese 
- Brazilian Portuguese
- Mandarin. 

To use the Speech To Text service in Node-RED you first need to make this service available in a way Node-RED can connect to that service. 

You need to have a local instance of Node-RED with IBM nodes available. If you don't have that yet, you can go [here](../../node-RED_labs/lab_node-RED.md).
Then go to the Bluemix catalog and go to the Speech to Text service and click on it. Make sure that there is no app bound to this service and click 'Use"
Wait until this service is deployed and click on 'Show Credentials', you will need the username and the password later on in this lab.

In this lab an audio file will be transcribed. This audiofile is avilable [here](audio message.wav). 
In the following screenshots you can see how the nodes are configured.

The inject node:

