---
title: "aaaSchema aktualizuje sierpnia-1-2015 preview — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Utworzenie definicji JSON dla usługi Azure Logic Apps z wersji schematu 2015-08-01-preview"
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 0d03a4d4-e8a8-4c81-aed5-bfd2a28c7f0c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 05/31/2016
ms.author: LADocs; stepsic
ms.openlocfilehash: 950cd18a27aa1859c4f0b6116de3fb8699d746c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a><span data-ttu-id="bda5c-103">Aktualizacje schematu dla usługi Azure Logic Apps - 1 sierpnia 2015 preview</span><span class="sxs-lookup"><span data-stu-id="bda5c-103">Schema updates for Azure Logic Apps - August 1, 2015 preview</span></span>

<span data-ttu-id="bda5c-104">Tego nowego schematu i interfejsu API w wersji dla usługi Azure Logic Apps zawiera kluczowe ulepszenia lepiej aplikacje logiki niezawodnych i łatwiejsze toouse:</span><span class="sxs-lookup"><span data-stu-id="bda5c-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier toouse:</span></span>

*   <span data-ttu-id="bda5c-105">Witaj **APIApp** typ akcji jest zaktualizowane tooa nowe [ **APIConnection** ](#api-connections) typ akcji.</span><span class="sxs-lookup"><span data-stu-id="bda5c-105">hello **APIApp** action type is updated tooa new [**APIConnection**](#api-connections) action type.</span></span>
*   <span data-ttu-id="bda5c-106">**Powtórz** jest zmieniana zbyt[**Foreach**](#foreach).</span><span class="sxs-lookup"><span data-stu-id="bda5c-106">**Repeat** is renamed too[**Foreach**](#foreach).</span></span>
*   <span data-ttu-id="bda5c-107">Witaj [ **odbiornik HTTP** aplikacji interfejsu API](#http-listener) nie jest już wymagane.</span><span class="sxs-lookup"><span data-stu-id="bda5c-107">hello [**HTTP Listener** API App](#http-listener) is no longer required.</span></span>
*   <span data-ttu-id="bda5c-108">Wywoływanie podrzędnego przepływy pracy używa [nowego schematu](#child-workflows).</span><span class="sxs-lookup"><span data-stu-id="bda5c-108">Calling child workflows uses a [new schema](#child-workflows).</span></span>

<a name="api-connections"></a>
## <a name="move-tooapi-connections"></a><span data-ttu-id="bda5c-109">Przenieś tooAPI połączeń</span><span class="sxs-lookup"><span data-stu-id="bda5c-109">Move tooAPI connections</span></span>

<span data-ttu-id="bda5c-110">Zmiana największych Hello jest, że nie masz już toodeploy API Apps do Twojej subskrypcji platformy Azure, aby można było używać interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="bda5c-110">hello biggest change is that you no longer have toodeploy API Apps into your Azure subscription so you can use APIs.</span></span> <span data-ttu-id="bda5c-111">Poniżej przedstawiono sposoby hello użyć interfejsów API:</span><span class="sxs-lookup"><span data-stu-id="bda5c-111">Here are hello ways that you can use APIs:</span></span>

* <span data-ttu-id="bda5c-112">Zarządzane interfejsy API</span><span class="sxs-lookup"><span data-stu-id="bda5c-112">Managed APIs</span></span>
* <span data-ttu-id="bda5c-113">Niestandardowych interfejsów API sieci Web</span><span class="sxs-lookup"><span data-stu-id="bda5c-113">Your custom Web APIs</span></span>

<span data-ttu-id="bda5c-114">Każdego sposób różni się nieznacznie, ponieważ ich zarządzania i modele obsługi są różne.</span><span class="sxs-lookup"><span data-stu-id="bda5c-114">Each way is handled slightly differently because their management and hosting models are different.</span></span> <span data-ttu-id="bda5c-115">Jedną z zalet tego modelu jest jest już ograniczone tooresources, które są wdrożone w grupie zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bda5c-115">One advantage of this model is you're no longer constrained tooresources that are deployed in your Azure resource group.</span></span> 

### <a name="managed-apis"></a><span data-ttu-id="bda5c-116">Zarządzane interfejsy API</span><span class="sxs-lookup"><span data-stu-id="bda5c-116">Managed APIs</span></span>

<span data-ttu-id="bda5c-117">Firma Microsoft zarządza niektórych interfejsów API w Twoim imieniu, takie jak usługi Office 365, Salesforce, Twitter i FTP.</span><span class="sxs-lookup"><span data-stu-id="bda5c-117">Microsoft manages some APIs on your behalf, such as Office 365, Salesforce, Twitter, and FTP.</span></span> <span data-ttu-id="bda5c-118">Można użyć niektóre zarządzane interfejsy API jako — jest, takich jak Bing tłumaczenia, a inne wymagają konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bda5c-118">You can use some managed APIs as-is, such as Bing Translate, while others require configuration.</span></span> <span data-ttu-id="bda5c-119">Ta konfiguracja jest nazywana *połączenia*.</span><span class="sxs-lookup"><span data-stu-id="bda5c-119">This configuration is called a *connection*.</span></span>

<span data-ttu-id="bda5c-120">Na przykład gdy używasz usługi Office 365, możesz utworzyć połączenie, które zawiera token logowania usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="bda5c-120">For example, when you use Office 365, you must create a connection that contains your Office 365 sign-in token.</span></span> <span data-ttu-id="bda5c-121">Token ten jest bezpiecznie przechowywane i odświeżania, dzięki czemu aplikację logiki zawsze można wywołać interfejsu API usługi Office 365 hello.</span><span class="sxs-lookup"><span data-stu-id="bda5c-121">This token is securely stored and refreshed so that your logic app can always call hello Office 365 API.</span></span> <span data-ttu-id="bda5c-122">Alternatywnie Chcąc tooconnect tooyour SQL lub serwer FTP, należy utworzyć połączenie, które ma hello parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="bda5c-122">Alternatively, if you want tooconnect tooyour SQL or FTP server, you must create a connection that has hello connection string.</span></span> 

<span data-ttu-id="bda5c-123">W tej definicji, te akcje są nazywane `APIConnection`.</span><span class="sxs-lookup"><span data-stu-id="bda5c-123">In this definition, these actions are called `APIConnection`.</span></span> <span data-ttu-id="bda5c-124">Oto przykład połączenia, które wywołuje toosend usługi Office 365 wiadomości e-mail:</span><span class="sxs-lookup"><span data-stu-id="bda5c-124">Here is an example of a connection that calls Office 365 toosend an email:</span></span>

```
{
    "actions": {
        "Send_Email": {
            "type": "ApiConnection",
            "inputs": {
                "host": {
                    "api": {
                        "runtimeUrl": "https://msmanaged-na.azure-apim.net/apim/office365"
                    },
                    "connection": {
                        "name": "@parameters('$connections')['shared_office365']['connectionId']"
                    }
                },
                "method": "post",
                "body": {
                    "Subject": "Reminder",
                    "Body": "Don't forget!",
                    "To": "me@contoso.com"
                },
                "path": "/Mail"
            }
        }
    }
}
```

<span data-ttu-id="bda5c-125">Witaj `host` obiekt jest część danych wejściowych jest unikatowy tooAPI połączeń, która zawiera części tow: `api` i `connection`.</span><span class="sxs-lookup"><span data-stu-id="bda5c-125">hello `host` object is portion of inputs that is unique tooAPI connections, and contains tow parts: `api` and `connection`.</span></span>

<span data-ttu-id="bda5c-126">Witaj `api` ma środowiska uruchomieniowego hello znajduje się adres URL gdzie, która zarządza interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="bda5c-126">hello `api` has hello runtime URL of where that managed API is hosted.</span></span> <span data-ttu-id="bda5c-127">Widać hello wszystkie dostępne zarządzanych interfejsów API, wywołując `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span><span class="sxs-lookup"><span data-stu-id="bda5c-127">You can see all hello available managed APIs by calling `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span></span>

<span data-ttu-id="bda5c-128">Jeśli korzystasz z interfejsu API hello interfejsu API może lub nie może mieć dowolną *parametry połączenia* zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="bda5c-128">When you use an API, hello API might or might not have any *connection parameters* defined.</span></span> <span data-ttu-id="bda5c-129">Jeśli nie hello interfejsu API, nie *połączenia* jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="bda5c-129">If hello API doesn't, no *connection* is required.</span></span> <span data-ttu-id="bda5c-130">Jeśli nie hello interfejsu API, należy utworzyć połączenie.</span><span class="sxs-lookup"><span data-stu-id="bda5c-130">If hello API does, you must create a connection.</span></span> <span data-ttu-id="bda5c-131">Hello utworzone połączenie ma nazwę hello, którą wybierzesz.</span><span class="sxs-lookup"><span data-stu-id="bda5c-131">hello created connection has hello name that you choose.</span></span> <span data-ttu-id="bda5c-132">Następnie odwoływać się nazwy hello w hello `connection` obiektu wewnątrz hello `host` obiektu.</span><span class="sxs-lookup"><span data-stu-id="bda5c-132">You then reference hello name in hello `connection` object inside hello `host` object.</span></span> <span data-ttu-id="bda5c-133">toocreate połączenia w grupie zasobów, rozmów:</span><span class="sxs-lookup"><span data-stu-id="bda5c-133">toocreate a connection in a resource group, call:</span></span>

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

<span data-ttu-id="bda5c-134">Z hello następującej treści:</span><span class="sxs-lookup"><span data-stu-id="bda5c-134">With hello following body:</span></span>

```
{
  "properties": {
    "api": {
      "id": "/subscriptions/{subid}/providers/Microsoft.Web/managedApis/azureblob"
    },
    "parameterValues": {
        "accountName": "{hello name of hello storage account -- hello set of parameters is different for each API}"
    }
  },
  "location": "{Logic app's location}"
}
```

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a><span data-ttu-id="bda5c-135">Wdrażanie zarządzanych interfejsów API w szablonie usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bda5c-135">Deploy managed APIs in an Azure Resource Manager template</span></span>

<span data-ttu-id="bda5c-136">Można utworzyć pełne zastosowanie szablonu usługi Azure Resource Manager tak długo, jak interakcyjnego logowania nie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="bda5c-136">You can create a full application in an Azure Resource Manager template as long as interactive sign-in isn't required.</span></span>
<span data-ttu-id="bda5c-137">Jeśli logowanie jest wymagana, można skonfigurować wszystkie elementy z szablonem usługi Azure Resource Manager hello, ale nadal masz toovisit hello portalu tooauthorize hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="bda5c-137">If sign-in is required, you can set up everything with hello Azure Resource Manager template, but you still have toovisit hello portal tooauthorize hello connections.</span></span> 

```
    "resources": [{
        "apiVersion": "2015-08-01-preview",
        "name": "azureblob",
        "type": "Microsoft.Web/connections",
        "location": "[resourceGroup().location]",
        "properties": {
            "api": {
                "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
            },
            "parameterValues": {
                "accountName": "[parameters('storageAccountName')]",
                "accessKey": "[parameters('storageAccountKey')]"
            }
        }
    }, {
        "type": "Microsoft.Logic/workflows",
        "apiVersion": "2015-08-01-preview",
        "name": "[parameters('logicAppName')]",
        "location": "[resourceGroup().location]",
        "dependsOn": ["[resourceId('Microsoft.Web/connections', 'azureblob')]"
        ],
        "properties": {
            "sku": {
                "name": "[parameters('sku')]",
                "plan": {
                    "id": "[concat(resourceGroup().id, '/providers/Microsoft.Web/serverfarms/',parameters('svcPlanName'))]"
                }
            },
            "definition": {
                "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2015-08-01-preview/workflowdefinition.json#",
                "actions": {
                    "Create_file": {
                        "type": "apiconnection",
                        "inputs": {
                            "host": {
                                "api": {
                                    "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/azureblob"
                                },
                                "connection": {
                                    "name": "@parameters('$connections')['azureblob']['connectionId']"
                                }
                            },
                            "method": "post",
                            "queries": {
                                "folderPath": "[concat('/', parameters('containerName'))]",
                                "name": "helloworld.txt"
                            },
                            "body": "@decodeDataUri('data:, Hello+world!')",
                            "path": "/datasets/default/files"
                        },
                        "conditions": []
                    }
                },
                "contentVersion": "1.0.0.0",
                "outputs": {},
                "parameters": {
                    "$connections": {
                        "defaultValue": {},
                        "type": "Object"
                    }
                },
                "triggers": {
                    "recurrence": {
                        "type": "Recurrence",
                        "recurrence": {
                            "frequency": "Day",
                            "interval": 1
                        }
                    }
                }
            },
            "parameters": {
                "$connections": {
                    "value": {
                        "azureblob": {
                            "connectionId": "[concat(resourceGroup().id,'/providers/Microsoft.Web/connections/azureblob')]",
                            "connectionName": "azureblob",
                            "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
                        }

                    }
                }
            }
        }
    }]
```

<span data-ttu-id="bda5c-138">Widać w tym przykładzie połączeń hello są tylko zasoby, które znajdują się w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="bda5c-138">You can see in this example that hello connections are just resources that live in your resource group.</span></span> <span data-ttu-id="bda5c-139">Odwołujących się do hello zarządzane interfejsy API tooyou dostępne w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="bda5c-139">They reference hello managed APIs available tooyou in your subscription.</span></span>

### <a name="your-custom-web-apis"></a><span data-ttu-id="bda5c-140">Niestandardowych interfejsów API sieci Web</span><span class="sxs-lookup"><span data-stu-id="bda5c-140">Your custom Web APIs</span></span>

<span data-ttu-id="bda5c-141">Jeśli używasz własnych interfejsów API, z nich nie zarządzany przez firmę Microsoft, Użyj wbudowanych hello **HTTP** toocall akcji je.</span><span class="sxs-lookup"><span data-stu-id="bda5c-141">If you use your own APIs, not Microsoft-managed ones, use hello built-in **HTTP** action toocall them.</span></span> <span data-ttu-id="bda5c-142">Nadaje się doskonale środowisko powinny ujawniać punktu końcowego struktury Swagger dla interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="bda5c-142">For an ideal experience, you should expose a Swagger endpoint for your API.</span></span> <span data-ttu-id="bda5c-143">Ten punkt końcowy włącza hello projektanta aplikacji logiki toorender hello w danych wejściowych i danych wyjściowych dla interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="bda5c-143">This endpoint enables hello Logic App Designer toorender hello inputs and outputs for your API.</span></span> <span data-ttu-id="bda5c-144">Bez struktury Swagger Projektant hello można tylko wyświetlić hello wejściami i wyjściami jako nieprzezroczyste obiektów JSON.</span><span class="sxs-lookup"><span data-stu-id="bda5c-144">Without Swagger, hello designer can only show hello inputs and outputs as opaque JSON objects.</span></span>

<span data-ttu-id="bda5c-145">Oto przykład przedstawiający hello nowe `metadata.apiDefinitionUrl` właściwości:</span><span class="sxs-lookup"><span data-stu-id="bda5c-145">Here is an example showing hello new `metadata.apiDefinitionUrl` property:</span></span>

```
{
   "actions": {
        "mycustomAPI": {
            "type": "http",
            "metadata": {
              "apiDefinitionUrl": "https://mysite.azurewebsites.net/api/apidef/"  
            },
            "inputs": {
                "uri": "https://mysite.azurewebsites.net/api/getsomedata",
                "method": "GET"
            }
        }
    }
}
```

<span data-ttu-id="bda5c-146">Jeśli na serwerze sieci Web interfejsu API w usłudze Azure App Service interfejsu API sieci Web automatycznie zostanie wyświetlony hello listę dostępnych w Projektancie hello akcji.</span><span class="sxs-lookup"><span data-stu-id="bda5c-146">If you host your Web API on Azure App Service, your Web API automatically appears in hello list of actions available in hello designer.</span></span> <span data-ttu-id="bda5c-147">Jeśli nie masz toopaste w adresie URL hello bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="bda5c-147">If not, you have toopaste in hello URL directly.</span></span> <span data-ttu-id="bda5c-148">punktu końcowego struktury Swagger Hello musi być nieuwierzytelnione toobe w hello projektanta aplikacji logiki, mimo że można zabezpieczyć hello interfejsu API się z dowolnej metody, które obsługuje struktury Swagger.</span><span class="sxs-lookup"><span data-stu-id="bda5c-148">hello Swagger endpoint must be unauthenticated toobe usable in hello Logic App Designer, although you can secure hello API itself with whatever methods that Swagger supports.</span></span>

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a><span data-ttu-id="bda5c-149">Wywołaj wdrożonej aplikacji interfejsu API za pomocą 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="bda5c-149">Call deployed API apps with 2015-08-01-preview</span></span>

<span data-ttu-id="bda5c-150">Jeśli wdrożono aplikację interfejsu API można wywołać aplikacji hello z hello **HTTP** akcji.</span><span class="sxs-lookup"><span data-stu-id="bda5c-150">If you previously deployed an API App, you can call hello app with hello **HTTP** action.</span></span>

<span data-ttu-id="bda5c-151">Na przykład, jeśli pliki toolist Dropbox Twoje **2014-12-01-preview** definicji wersji schematu może mieć wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="bda5c-151">For example, if you use Dropbox toolist files, your **2014-12-01-preview** schema version definition might have something like:</span></span>

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2014-12-01-preview/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token": {
            "defaultValue": "eyJ0eX...wCn90",
            "type": "String",
            "metadata": {
                "token": {
                    "name": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token"
                }
            }
        }
    },
    "actions": {
        "dropboxconnector": {
            "type": "ApiApp",
            "inputs": {
                "apiVersion": "2015-01-14",
                "host": {
                    "id": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector",
                    "gateway": "https://avdemo.azurewebsites.net"
                },
                "operation": "ListFiles",
                "parameters": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

<span data-ttu-id="bda5c-152">Można utworzyć hello równoważne akcji HTTP, tak jak ten przykład sekcji parametrów hello hello definicję aplikacji logiki pozostaje bez zmian:</span><span class="sxs-lookup"><span data-stu-id="bda5c-152">You can construct hello equivalent HTTP action like this example, while hello parameters section of hello Logic app definition remains unchanged:</span></span>

```
{
    "actions": {
        "dropboxconnector": {
            "type": "Http",
            "metadata": {
              "apiDefinitionUrl": "https://avdemo.azurewebsites.net/api/service/apidef/dropboxconnector/?api-version=2015-01-14&format=swagger-2.0-standard"  
            },
            "inputs": {
                "uri": "https://avdemo.azurewebsites.net/api/service/invoke/dropboxconnector/ListFiles?api-version=2015-01-14",
                "method": "POST",
                "body": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

<span data-ttu-id="bda5c-153">Instruktaż te właściwości jeden po drugim:</span><span class="sxs-lookup"><span data-stu-id="bda5c-153">Walking through these properties one-by-one:</span></span>

| <span data-ttu-id="bda5c-154">Właściwość Action</span><span class="sxs-lookup"><span data-stu-id="bda5c-154">Action property</span></span> | <span data-ttu-id="bda5c-155">Opis</span><span class="sxs-lookup"><span data-stu-id="bda5c-155">Description</span></span> |
| --- | --- |
| `type` |<span data-ttu-id="bda5c-156">`Http`Zamiast`APIapp`</span><span class="sxs-lookup"><span data-stu-id="bda5c-156">`Http` instead of `APIapp`</span></span> |
| `metadata.apiDefinitionUrl` |<span data-ttu-id="bda5c-157">toouse tej akcji w hello projektanta aplikacji logiki, obejmują punktu końcowego metadanych hello, który jest tworzony z:`{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span><span class="sxs-lookup"><span data-stu-id="bda5c-157">toouse this action in hello Logic App Designer, include hello metadata endpoint, which is constructed from: `{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span></span> |
| `inputs.uri` |<span data-ttu-id="bda5c-158">Utworzone na podstawie:`{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14`</span><span class="sxs-lookup"><span data-stu-id="bda5c-158">Constructed from: `{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14`</span></span> |
| `inputs.method` |<span data-ttu-id="bda5c-159">Zawsze`POST`</span><span class="sxs-lookup"><span data-stu-id="bda5c-159">Always `POST`</span></span> |
| `inputs.body` |<span data-ttu-id="bda5c-160">Parametry aplikacji identyczne toohello interfejsu API</span><span class="sxs-lookup"><span data-stu-id="bda5c-160">Identical toohello API App parameters</span></span> |
| `inputs.authentication` |<span data-ttu-id="bda5c-161">Identyczne toohello uwierzytelniania aplikacji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="bda5c-161">Identical toohello API App authentication</span></span> |

<span data-ttu-id="bda5c-162">Ta metoda powinna działać dla wszystkich akcji w aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="bda5c-162">This approach should work for all API App actions.</span></span> <span data-ttu-id="bda5c-163">Należy jednak pamiętać, że tych poprzedniej aplikacji interfejsu API nie są już obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="bda5c-163">However, remember that these previous API Apps are no longer supported.</span></span> <span data-ttu-id="bda5c-164">Dlatego należy przenieść tooone hello dwóch innych poprzedniej opcji zarządzanego interfejsu API lub hosting niestandardowego interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="bda5c-164">So you should move tooone of hello two other previous options, a managed API or hosting your custom Web API.</span></span>

<a name="foreach"></a>
## <a name="renamed-repeat-tooforeach"></a><span data-ttu-id="bda5c-165">Zmieniono jego nazwę, powtórz too'foreach "</span><span class="sxs-lookup"><span data-stu-id="bda5c-165">Renamed 'repeat' too'foreach'</span></span>

<span data-ttu-id="bda5c-166">Dla wcześniejszych wersji schematu hello Otrzymaliśmy dużo opinie klientów który **Powtórz** było trudne i poprawnie nie przechwytywania, który **Powtórz** jest rzeczywiście dla każdej pętli.</span><span class="sxs-lookup"><span data-stu-id="bda5c-166">For hello previous schema version, we received much customer feedback that **Repeat** was confusing and didn't properly capture that **Repeat** was really a for-each loop.</span></span> <span data-ttu-id="bda5c-167">W rezultacie firma Microsoft zmieniono `repeat` zbyt`foreach`.</span><span class="sxs-lookup"><span data-stu-id="bda5c-167">As a result, we have renamed `repeat` too`foreach`.</span></span> <span data-ttu-id="bda5c-168">Na przykład wcześniej piszesz:</span><span class="sxs-lookup"><span data-stu-id="bda5c-168">For example, previously you would write:</span></span>

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "repeat": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{repeatItem()}"
            }
        }
    }
}
```

<span data-ttu-id="bda5c-169">Teraz możesz zapisać:</span><span class="sxs-lookup"><span data-stu-id="bda5c-169">Now you would write:</span></span>

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "foreach": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{item()}"
            }
        }
    }
}
```

<span data-ttu-id="bda5c-170">Witaj funkcja `@repeatItem()` został poprzednio tooreference hello bieżący element jest iterowane za pośrednictwem.</span><span class="sxs-lookup"><span data-stu-id="bda5c-170">hello function `@repeatItem()` was previously used tooreference hello current item being iterated over.</span></span> <span data-ttu-id="bda5c-171">Ta funkcja jest teraz uproszczone zbyt`@item()`.</span><span class="sxs-lookup"><span data-stu-id="bda5c-171">This function is now simplified too`@item()`.</span></span> 

### <a name="reference-outputs-from-foreach"></a><span data-ttu-id="bda5c-172">Odwołanie do danych wyjściowych ze "foreach"</span><span class="sxs-lookup"><span data-stu-id="bda5c-172">Reference outputs from 'foreach'</span></span>

<span data-ttu-id="bda5c-173">Dla uproszczenia hello danych wyjściowych ze `foreach` akcje nie są ujęte w nazwie obiektu `repeatItems`.</span><span class="sxs-lookup"><span data-stu-id="bda5c-173">For simplification, hello outputs from `foreach` actions are not wrapped in an object called `repeatItems`.</span></span> <span data-ttu-id="bda5c-174">Gdy hello danych wyjściowych z poprzednich hello `repeat` zostały przykładzie:</span><span class="sxs-lookup"><span data-stu-id="bda5c-174">While hello outputs from hello previous `repeat` example were:</span></span>

```
{
    "repeatItems": [
        {
            "name": "pingBing",
            "inputs": {
                "uri": "https://www.bing.com/search?q=0",
                "method": "GET"
            },
            "outputs": {
                "headers": { },
                "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
            }
            "status": "Succeeded"
        }
    ]
}
```

<span data-ttu-id="bda5c-175">Teraz te dane wyjściowe są:</span><span class="sxs-lookup"><span data-stu-id="bda5c-175">Now these outputs are:</span></span>

```
[
    {
        "name": "pingBing",
        "inputs": {
            "uri": "https://www.bing.com/search?q=0",
            "method": "GET"
        },
        "outputs": {
            "headers": { },
            "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
        }
        "status": "Succeeded"
    }
]
```

<span data-ttu-id="bda5c-176">Wcześniej tooget toohello treść hello akcji podczas odwoływania się do tych danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="bda5c-176">Previously, tooget toohello body of hello action when referencing these outputs:</span></span>

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "repeat": "@outputs('pingBing').repeatItems",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@repeatItem().outputs.body"
            }
        }
    }
}
```

<span data-ttu-id="bda5c-177">Teraz można wykonać zamiast tego:</span><span class="sxs-lookup"><span data-stu-id="bda5c-177">Now you can do instead:</span></span>

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "foreach": "@outputs('pingBing')",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@item().outputs.body"
            }
        }
    }
}
```

<span data-ttu-id="bda5c-178">Wprowadzone zmiany hello funkcji `@repeatItem()`, `@repeatBody()`, i `@repeatOutputs()` są usuwane.</span><span class="sxs-lookup"><span data-stu-id="bda5c-178">With these changes, hello functions `@repeatItem()`, `@repeatBody()`, and `@repeatOutputs()` are removed.</span></span>

<a name="http-listener"></a>
## <a name="native-http-listener"></a><span data-ttu-id="bda5c-179">Natywny odbiornika HTTP</span><span class="sxs-lookup"><span data-stu-id="bda5c-179">Native HTTP listener</span></span>

<span data-ttu-id="bda5c-180">Witaj możliwości są obecnie wbudowane w odbiornik HTTP.</span><span class="sxs-lookup"><span data-stu-id="bda5c-180">hello HTTP Listener capabilities are now built in.</span></span> <span data-ttu-id="bda5c-181">Nie należy więc toodeploy aplikacji interfejsu API odbiornika HTTP.</span><span class="sxs-lookup"><span data-stu-id="bda5c-181">So you no longer need toodeploy an HTTP Listener API App.</span></span> <span data-ttu-id="bda5c-182">Zobacz [hello pełne szczegóły na temat toomake Twojego logiki aplikacji punktu końcowego można wywołać tutaj](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="bda5c-182">See [hello full details for how toomake your Logic app endpoint callable here](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<span data-ttu-id="bda5c-183">Wprowadzone zmiany, firma Microsoft usunęła hello `@accessKeys()` funkcji, która możemy zastąpione hello `@listCallbackURL()` funkcja uzyskania hello punktu końcowego, gdy jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="bda5c-183">With these changes, we removed hello `@accessKeys()` function, which we replaced with hello `@listCallbackURL()` function for getting hello endpoint when necessary.</span></span> <span data-ttu-id="bda5c-184">Ponadto teraz należy zdefiniować co najmniej jeden wyzwalacz w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="bda5c-184">Also, you must now define at least one trigger in your logic app.</span></span> <span data-ttu-id="bda5c-185">Jeśli chcesz zbyt`/run` hello przepływu pracy, musi mieć jeden z tych wyzwalaczy: `manual`, `apiConnectionWebhook`, lub `httpWebhook`.</span><span class="sxs-lookup"><span data-stu-id="bda5c-185">If you want too`/run` hello workflow, you must have one of these triggers: `manual`, `apiConnectionWebhook`, or `httpWebhook`.</span></span>

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a><span data-ttu-id="bda5c-186">Wywołania podrzędne przepływy pracy</span><span class="sxs-lookup"><span data-stu-id="bda5c-186">Call child workflows</span></span>

<span data-ttu-id="bda5c-187">Wcześniej wywoływania podrzędnego przepływów pracy wymagane będzie toohello przepływu pracy, uzyskiwanie hello token dostępu i token hello wklejanie w definicji aplikacji logiki hello miejscu toocall podrzędny przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="bda5c-187">Previously, calling child workflows required going toohello workflow, getting hello access token, and pasting hello token in hello logic app definition where you want toocall that child workflow.</span></span> <span data-ttu-id="bda5c-188">Hello nowego schematu aplikacji logiki hello aparat automatycznie generuje sygnaturę dostępu Współdzielonego w czasie wykonywania dla hello podrzędny przepływ pracy, nie ma zbyt wklejania żadnych kluczy tajnych w definicji hello.</span><span class="sxs-lookup"><span data-stu-id="bda5c-188">With hello new schema, hello Logic Apps engine automatically generates a SAS at runtime for hello child workflow so you don't have too paste any secrets into hello definition.</span></span> <span data-ttu-id="bda5c-189">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="bda5c-189">Here is an example:</span></span>

```
"mynestedwf": {
    "type": "workflow",
    "inputs": {
        "host": {
            "id": "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName": "myendpointtrigger"
        },
        "queries": {
            "extrafield": "specialValue"
        },
        "headers": {
            "x-ms-date": "@utcnow()",
            "Content-type": "application/json"
        },
        "body": {
            "contentFieldOne": "value100",
            "anotherField": 10.001
        }
    },
    "conditions": []
}
```

<span data-ttu-id="bda5c-190">Drugi poprawy jest udostępniamy możliwość sprawowania podrzędnych hello przychodzące żądanie toohello pełny dostęp przepływów pracy.</span><span class="sxs-lookup"><span data-stu-id="bda5c-190">A second improvement is we are giving hello child workflows full access toohello incoming request.</span></span> <span data-ttu-id="bda5c-191">Oznacza to, że można przekazywać parametrów w hello *zapytania* sekcji w hello *nagłówki* obiekt i który pełni można zdefiniować hello całej treści.</span><span class="sxs-lookup"><span data-stu-id="bda5c-191">That means that you can pass parameters in hello *queries* section and in hello *headers* object and that you can fully define hello entire body.</span></span>

<span data-ttu-id="bda5c-192">Na koniec są wymagane zmiany toohello podrzędny przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="bda5c-192">Finally, there are required changes toohello child workflow.</span></span> <span data-ttu-id="bda5c-193">Podczas wcześniej można bezpośrednio wywołać podrzędny przepływ pracy, teraz należy zdefiniować punkt końcowy wyzwalacza w przepływie pracy powitania dla hello toocall nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="bda5c-193">While you could previously call a child workflow directly, now you must define a trigger endpoint in hello workflow for hello parent toocall.</span></span> <span data-ttu-id="bda5c-194">Ogólnie rzecz biorąc, należy dodać wyzwalacz, który ma `manual` typu, a następnie użyj tego wyzwalacza w definicji nadrzędnej hello.</span><span class="sxs-lookup"><span data-stu-id="bda5c-194">Generally, you would add a trigger that has `manual` type, and then use that trigger in hello parent definition.</span></span> <span data-ttu-id="bda5c-195">Uwaga hello `host` właściwość specjalnie ma `triggerName` ponieważ należy zawsze określić, której wyzwalacz wywoływania.</span><span class="sxs-lookup"><span data-stu-id="bda5c-195">Note hello `host` property specifically has a `triggerName` because you must always specify which trigger you are invoking.</span></span>

## <a name="other-changes"></a><span data-ttu-id="bda5c-196">Inne zmiany</span><span class="sxs-lookup"><span data-stu-id="bda5c-196">Other changes</span></span>

### <a name="new-queries-property"></a><span data-ttu-id="bda5c-197">Nowe właściwości "zapytania"</span><span class="sxs-lookup"><span data-stu-id="bda5c-197">New 'queries' property</span></span>

<span data-ttu-id="bda5c-198">Wszystkie typy akcji obsługują teraz nowe dane wejściowe o nazwie `queries`.</span><span class="sxs-lookup"><span data-stu-id="bda5c-198">All action types now support a new input called `queries`.</span></span> <span data-ttu-id="bda5c-199">Obiektu strukturalnego, zamiast ponownego ciąg hello tooassemble ręcznie, może być tych danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="bda5c-199">This input can be a structured object, rather than you having tooassemble hello string by hand.</span></span>

### <a name="renamed-parse-function-toojson"></a><span data-ttu-id="bda5c-200">Zmieniona "parse()" Funkcja too'json() "</span><span class="sxs-lookup"><span data-stu-id="bda5c-200">Renamed 'parse()' function too'json()'</span></span>

<span data-ttu-id="bda5c-201">Dodajemy więcej zawartości typy wkrótce, dlatego firma Microsoft zmieniona hello `parse()` funkcji zbyt`json()`.</span><span class="sxs-lookup"><span data-stu-id="bda5c-201">We are adding more content types soon, so we renamed hello `parse()` function too`json()`.</span></span>

## <a name="coming-soon-enterprise-integration-apis"></a><span data-ttu-id="bda5c-202">Wkrótce: interfejsy API integracji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="bda5c-202">Coming soon: Enterprise Integration APIs</span></span>

<span data-ttu-id="bda5c-203">Nie mamy zarządzanej wersji jeszcze hello interfejsów API integracji przedsiębiorstwa, takich jak AS2.</span><span class="sxs-lookup"><span data-stu-id="bda5c-203">We don't have managed versions yet of hello Enterprise Integration APIs, like AS2.</span></span> <span data-ttu-id="bda5c-204">W tym samym czasie możesz użyć istniejących wdrożonej BizTalk interfejsów API za pomocą hello akcji HTTP.</span><span class="sxs-lookup"><span data-stu-id="bda5c-204">Meanwhile, you can use your existing deployed BizTalk APIs through hello HTTP action.</span></span> <span data-ttu-id="bda5c-205">Aby uzyskać więcej informacji, zobacz "Używanie już raz wdrożonej aplikacji interfejsu API" w hello [plan integracji](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span><span class="sxs-lookup"><span data-stu-id="bda5c-205">For details, see "Using your already deployed API apps" in hello [integration roadmap](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span></span> 
