# Cognitive Container Sample

Azure Cognitive Services are a powerful set of tools that perform Congitive functions ranging from speech recognition, translation, generation to image processing.

These are made available as a series of APIs that are provisioned in the Azure portal. These are essentially multi-tenant services - that is they are shared between the different Azure customers. For many customers, this is adequate.

Some customers want to use Cognitive Services, but also want much tighter control on the service itself, whilst others want to be able to run these Cognitive services offline.

## Cognitive Services in a Container
To allow customers a higher degree of control, some Cognitive services will be deployable inside container technologies such as Azure Kubernetes Service (AKS) or Azure Container Instances (ACI). 

This is currently a preview feature and there is a process where some developers can request access to an Azure Container Registry (ACR) that contains these preview Docker images.


