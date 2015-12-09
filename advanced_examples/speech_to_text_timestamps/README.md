# Fetching word alignments from the Speech to Text service

Document creation is in progress

## Overview
The speech to text services allows time alignment for each word in the transcript to be returned. Unfortunately the 
speech to text node only returns the default transcript. If you need alternative transcripts or time alignment then
you will need to call the service using a HTTP Response node. This exercise shows how to retrieve the time alignments for 
each word in the default transcript. You should be able to adapt this flow, and by modifying the paramaters into the 
service modify the response. eg. Fetch confidence levels for each word. 

## Initial Form
The flow begins by showing a form.

![Upload both positive and negative examples](images/astt_show_form.png)

The entry point into the application is a HTTP Input configured to respond to a GET.

![HTTP GET Node](images/astt_application_get_node.png)

The switch node checks for a url.

![HTTP GET Node](images/astt_check_for_url_node.png)

The Template prompts the user to enter a url.

```
<h1>Speech to Text Demo on Node-RED</h1>
<h2>Enter a URL for the audio file</h2>
<form  action="{{req._parsedUrl.pathname}}">
    Url: <input type="text" name="url"/><br/>
    <input type="submit" value="recognize"/>
</form>
```

## Fetch the Audio
If a url has been provided, it should point to a wav 
file (eg. [Example Wav URL](http://www-mobile.ecs.soton.ac.uk/hth97r/links/Database/man1_wb.wav)
Use a function to setup a HTTP Request for the audio file

![HTTP GET Node](images/astt_function_prepare_audio.png)

The contents of which is:

```
audiourl = encodeURI(msg.payload.url)
msg.url=audiourl;
return msg;
```

Use a HTTP Response node,

![HTTP Response Node for Audio](images/astt_fetch_audio_request.png)

configured to return a binary buffer

![HTTP GET for Audio](images/astt_fetch_audio_node.png)


## Invoke Speech to text
Add a function that will take the returned audio file, and prepare the http headers and url to invoke 
the Speech to Text service

![Prepare for Speech to Text Service](images/astt_prepare_stt_request.png)


The url has parameters to fetch timestamps, and for the audio to be processed as a continous stream, ignoring
any speech pauses in the audio.

```
msg.headers = {'Content-Type' : 'audio/wav'};
msg.url="https://stream.watsonplatform.net/speech-to-text/api/v1/recognize?timestamps=true&continuous=true";
return msg;
```

A HTTP Request node is used to invoke the Speech to text service,

![HTTP Request for Speech to Text](images/astt_speech_to_text_request.png)


which needs to be configured to use basic authentication. Remember to enter Speech to Text service credentials which you can 
obtain from bluemix.

![HTTP Request Node for Speech to Text](images/astt_speech_to_text_post.png)


## Process the text
to be continued.

The completed flow is available at [Speech to Text Timestamps Flow](astt_speech_timestamps_flow.json)
