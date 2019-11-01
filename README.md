# Cognitive Container Sample

Azure Cognitive Services are a powerful set of tools that perform Cognitive functions ranging from speech recognition, translation, generation to image processing.

These are made available as a series of APIs that are provisioned in the Azure portal. These are essentially multi-tenant services - that is they are shared between the different Azure customers. For many customers, this is adequate.

Some customers want to use Cognitive Services, but also want much tighter control on the service itself, whilst others want to be able to run these Cognitive services offline.

## Cognitive Services in a Container
To allow customers a higher degree of control, some Cognitive services will be deployable inside container technologies such as Azure Kubernetes Service (AKS) or Azure Container Instances (ACI). 

![alt text](https://github.com/jometzg/cognitive-container-sample/blob/master/cognitive-container.png "Cognitive Speech in a container")

The above diagram shows a function app interacting with Cognitive Speech in a container. The function app takes some inbound audio either from an MP3 file and processes it so that the speech transcription service can perform the transcription. This is just one sample configuration.

This is currently a preview feature and there is a process where some developers can request access to an Azure Container Registry (ACR) that contains these preview Docker images.

There is some documentation [here](https://docs.microsoft.com/en-gb/azure/cognitive-services/speech-service/speech-container-howto) that shows you how to configure Cognitive Services in a simple container.

It should also be noted that to allow Microsoft to bill you for the use of these Cognitive Services, you need to configure the container with the URL and API key of an existing normal PaaS Cognitive Services account. It should be noted that this account will only be used for billing purposes - when clients of Cognitive Services are configured to call a container-based instance, then the cognitive requests will only go the the container, but your PaaS Cognitive Service will receive the billing requests.

## Coding against the container-based version
Fundamentally the coding model for the container-based version is identical to that of the existing SDKs. But the main change that needs to be made to the code is how the connection is made from the SDK to the container-based cognitive services. This is discussed in detail [here](https://docs.microsoft.com/en-us/azure/cognitive-services/speech-service/speech-container-howto#query-the-containers-prediction-endpoint).

In summary, the connection code must be changed from:
```c#
var config = SpeechConfig.FromSubscription("YourSubscriptionKey", "YourServiceRegion");
```
to use a container endpoint:
```c#
var config = SpeechConfig.FromEndpoint(
    new Uri("ws://<container-ip-address>:5000/speech/recognition/dictation/cognitiveservices/v1"),
    "YourSubscriptionKey");
```
The starting point for any coding is best taken from the [Speech SDK](https://github.com/Azure-Samples/cognitive-services-speech-sdk)

This [sample](https://github.com/Azure-Samples/cognitive-services-speech-sdk/tree/master/samples/csharp/dotnetcore/console) is the starting point for any test changes that can be made to point to a container-based Cognitive Services speech demonstration.

**It should be noted that this container does not support the [batch REST API](https://docs.microsoft.com/en-us/azure/cognitive-services/speech-service/batch-transcription) that my [cognitive-speech](https://github.com/jometzg/cognitive-speech) sample uses. Therefore this demonstation has to use the SDK rather than pure HTTP REST calls.**

## The demonstration
This section will detail what the demonstration will do in non-technical terms. This could be the same as the other cognitive speech demonstration, but a slightly different demonstration may be best.

**Watch this space**
