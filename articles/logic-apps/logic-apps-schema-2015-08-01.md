---
title: "Schemat aktualizuje sierpnia-1-2015 preview — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 35d7a56d5607dcc18a4407c65b92962d3d0dcd1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a><span data-ttu-id="d7b8a-103">Aktualizacje schematu dla usługi Azure Logic Apps - 1 sierpnia 2015 preview</span><span class="sxs-lookup"><span data-stu-id="d7b8a-103">Schema updates for Azure Logic Apps - August 1, 2015 preview</span></span>

<span data-ttu-id="d7b8a-104">Ten nowy schemat i interfejsu API w wersji dla usługi Azure Logic Apps obejmuje klucza ulepszeniom aplikacje logiki bardziej niezawodne i łatwiejsze w:</span><span class="sxs-lookup"><span data-stu-id="d7b8a-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier to use:</span></span>

*   <span data-ttu-id="d7b8a-105">**APIApp** typ akcji jest aktualizowana do nowej [ **APIConnection** ](#api-connections) typ akcji.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-105">The **APIApp** action type is updated to a new [**APIConnection**](#api-connections) action type.</span></span>
*   <span data-ttu-id="d7b8a-106">**Powtórz** została zmieniona na [ **Foreach**](#foreach).</span><span class="sxs-lookup"><span data-stu-id="d7b8a-106">**Repeat** is renamed to [**Foreach**](#foreach).</span></span>
*   <span data-ttu-id="d7b8a-107">[ **Odbiornik HTTP** aplikacji interfejsu API](#http-listener) nie jest już wymagane.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-107">The [**HTTP Listener** API App](#http-listener) is no longer required.</span></span>
*   <span data-ttu-id="d7b8a-108">Wywoływanie podrzędnego przepływy pracy używa [nowego schematu](#child-workflows).</span><span class="sxs-lookup"><span data-stu-id="d7b8a-108">Calling child workflows uses a [new schema](#child-workflows).</span></span>

<a name="api-connections"></a>
## <a name="move-to-api-connections"></a><span data-ttu-id="d7b8a-109">Przenieś do połączenia interfejsu API</span><span class="sxs-lookup"><span data-stu-id="d7b8a-109">Move to API connections</span></span>

<span data-ttu-id="d7b8a-110">Największych zmiana jest, że nie masz już do wdrożenia aplikacji interfejsu API w Twojej subskrypcji platformy Azure, aby można było używać interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-110">The biggest change is that you no longer have to deploy API Apps into your Azure subscription so you can use APIs.</span></span> <span data-ttu-id="d7b8a-111">Poniżej przedstawiono sposoby używania interfejsów API:</span><span class="sxs-lookup"><span data-stu-id="d7b8a-111">Here are the ways that you can use APIs:</span></span>

* <span data-ttu-id="d7b8a-112">Zarządzane interfejsy API</span><span class="sxs-lookup"><span data-stu-id="d7b8a-112">Managed APIs</span></span>
* <span data-ttu-id="d7b8a-113">Niestandardowych interfejsów API sieci Web</span><span class="sxs-lookup"><span data-stu-id="d7b8a-113">Your custom Web APIs</span></span>

<span data-ttu-id="d7b8a-114">Każdego sposób różni się nieznacznie, ponieważ ich zarządzania i modele obsługi są różne.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-114">Each way is handled slightly differently because their management and hosting models are different.</span></span> <span data-ttu-id="d7b8a-115">Jedną z zalet tego modelu jest jest już ograniczona do zasobów, które zostały wdrożone w grupie zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-115">One advantage of this model is you're no longer constrained to resources that are deployed in your Azure resource group.</span></span> 

### <a name="managed-apis"></a><span data-ttu-id="d7b8a-116">Zarządzane interfejsy API</span><span class="sxs-lookup"><span data-stu-id="d7b8a-116">Managed APIs</span></span>

<span data-ttu-id="d7b8a-117">Firma Microsoft zarządza niektórych interfejsów API w Twoim imieniu, takie jak usługi Office 365, Salesforce, Twitter i FTP.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-117">Microsoft manages some APIs on your behalf, such as Office 365, Salesforce, Twitter, and FTP.</span></span> <span data-ttu-id="d7b8a-118">Można użyć niektóre zarządzane interfejsy API jako — jest, takich jak Bing tłumaczenia, a inne wymagają konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-118">You can use some managed APIs as-is, such as Bing Translate, while others require configuration.</span></span> <span data-ttu-id="d7b8a-119">Ta konfiguracja jest nazywana *połączenia*.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-119">This configuration is called a *connection*.</span></span>

<span data-ttu-id="d7b8a-120">Na przykład gdy używasz usługi Office 365, możesz utworzyć połączenie, które zawiera token logowania usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-120">For example, when you use Office 365, you must create a connection that contains your Office 365 sign-in token.</span></span> <span data-ttu-id="d7b8a-121">Token ten jest bezpiecznie przechowywane i odświeżenia, tak aby aplikację logiki zawsze można wywołać interfejsu API usługi Office 365.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-121">This token is securely stored and refreshed so that your logic app can always call the Office 365 API.</span></span> <span data-ttu-id="d7b8a-122">Alternatywnie Jeśli chcesz się połączyć z serwerem SQL lub FTP, należy utworzyć połączenie, które ma parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-122">Alternatively, if you want to connect to your SQL or FTP server, you must create a connection that has the connection string.</span></span> 

<span data-ttu-id="d7b8a-123">W tej definicji, te akcje są nazywane `APIConnection`.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-123">In this definition, these actions are called `APIConnection`.</span></span> <span data-ttu-id="d7b8a-124">Oto przykład połączenia, który wywołuje usługi Office 365, aby wysłać wiadomość e-mail:</span><span class="sxs-lookup"><span data-stu-id="d7b8a-124">Here is an example of a connection that calls Office 365 to send an email:</span></span>

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

<span data-ttu-id="d7b8a-125">`host` Obiekt jest część danych wejściowych jest unikatowy dla połączenia interfejsu API, która zawiera części tow: `api` i `connection`.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-125">The `host` object is portion of inputs that is unique to API connections, and contains tow parts: `api` and `connection`.</span></span>

<span data-ttu-id="d7b8a-126">`api` Ma środowisko uruchomieniowe znajduje się adres URL gdzie, która zarządza interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-126">The `api` has the runtime URL of where that managed API is hosted.</span></span> <span data-ttu-id="d7b8a-127">Widoczne wszystkie dostępne zarządzanych interfejsów API, wywołując `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-127">You can see all the available managed APIs by calling `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span></span>

<span data-ttu-id="d7b8a-128">Jeśli korzystasz z interfejsu API interfejsu API może lub nie może mieć dowolną *parametry połączenia* zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-128">When you use an API, the API might or might not have any *connection parameters* defined.</span></span> <span data-ttu-id="d7b8a-129">Jeśli interfejs API nie jest zaznaczone, nie *połączenia* jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-129">If the API doesn't, no *connection* is required.</span></span> <span data-ttu-id="d7b8a-130">Jeśli nie interfejsu API, należy utworzyć połączenie.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-130">If the API does, you must create a connection.</span></span> <span data-ttu-id="d7b8a-131">Utworzone połączenie ma nazwę, którą wybierzesz.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-131">The created connection has the name that you choose.</span></span> <span data-ttu-id="d7b8a-132">Następnie odwoływać się do nazwy w `connection` obiektów wewnątrz `host` obiektu.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-132">You then reference the name in the `connection` object inside the `host` object.</span></span> <span data-ttu-id="d7b8a-133">Aby utworzyć połączenie w grupie zasobów, należy wywołać:</span><span class="sxs-lookup"><span data-stu-id="d7b8a-133">To create a connection in a resource group, call:</span></span>

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

<span data-ttu-id="d7b8a-134">O następujących treści:</span><span class="sxs-lookup"><span data-stu-id="d7b8a-134">With the following body:</span></span>

```
{
  "properties": {
    "api": {
      "id": "/subscriptions/{subid}/providers/Microsoft.Web/managedApis/azureblob"
    },
    "parameterValues": {
        "accountName": "{The name of the storage account -- the set of parameters is different for each API}"
    }
  },
  "location": "{Logic app's location}"
}
```

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a><span data-ttu-id="d7b8a-135">Wdrażanie zarządzanych interfejsów API w szablonie usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d7b8a-135">Deploy managed APIs in an Azure Resource Manager template</span></span>

<span data-ttu-id="d7b8a-136">Można utworzyć pełne zastosowanie szablonu usługi Azure Resource Manager tak długo, jak interakcyjnego logowania nie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-136">You can create a full application in an Azure Resource Manager template as long as interactive sign-in isn't required.</span></span>
<span data-ttu-id="d7b8a-137">Jeśli logowanie jest wymagana, można skonfigurować wszystko przy użyciu szablonu usługi Azure Resource Manager, ale nadal jest konieczne można znaleźć w portalu w celu autoryzowania połączeń.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-137">If sign-in is required, you can set up everything with the Azure Resource Manager template, but you still have to visit the portal to authorize the connections.</span></span> 

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

<span data-ttu-id="d7b8a-138">Widać w tym przykładzie, że połączenia są tylko zasoby, które znajdują się w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-138">You can see in this example that the connections are just resources that live in your resource group.</span></span> <span data-ttu-id="d7b8a-139">Odwołujących się do zarządzanych interfejsów API dostępne w Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-139">They reference the managed APIs available to you in your subscription.</span></span>

### <a name="your-custom-web-apis"></a><span data-ttu-id="d7b8a-140">Niestandardowych interfejsów API sieci Web</span><span class="sxs-lookup"><span data-stu-id="d7b8a-140">Your custom Web APIs</span></span>

<span data-ttu-id="d7b8a-141">Jeśli używasz własnych interfejsów API, z nich nie zarządzany przez firmę Microsoft, użyj wbudowanej **HTTP** akcji do wywołania.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-141">If you use your own APIs, not Microsoft-managed ones, use the built-in **HTTP** action to call them.</span></span> <span data-ttu-id="d7b8a-142">Nadaje się doskonale środowisko powinny ujawniać punktu końcowego struktury Swagger dla interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-142">For an ideal experience, you should expose a Swagger endpoint for your API.</span></span> <span data-ttu-id="d7b8a-143">Ten punkt końcowy włącza projektanta aplikacji logiki do renderowania danych wejściowych i danych wyjściowych dla interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-143">This endpoint enables the Logic App Designer to render the inputs and outputs for your API.</span></span> <span data-ttu-id="d7b8a-144">Bez struktury Swagger Projektant można tylko wyświetlić wejściami i wyjściami jako nieprzezroczyste obiektów JSON.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-144">Without Swagger, the designer can only show the inputs and outputs as opaque JSON objects.</span></span>

<span data-ttu-id="d7b8a-145">Oto przykład przedstawiający nowy `metadata.apiDefinitionUrl` właściwości:</span><span class="sxs-lookup"><span data-stu-id="d7b8a-145">Here is an example showing the new `metadata.apiDefinitionUrl` property:</span></span>

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

<span data-ttu-id="d7b8a-146">Jeśli na serwerze sieci Web interfejsu API w usłudze Azure App Service, interfejs API sieci Web automatycznie zostanie wyświetlony na liście Akcje dostępne w projektancie.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-146">If you host your Web API on Azure App Service, your Web API automatically appears in the list of actions available in the designer.</span></span> <span data-ttu-id="d7b8a-147">Jeśli nie masz wkleić bezpośrednio w adresie URL.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-147">If not, you have to paste in the URL directly.</span></span> <span data-ttu-id="d7b8a-148">Musi być nieuwierzytelniony punktu końcowego struktury Swagger może być używany w Projektancie aplikacji logiki, mimo że można zabezpieczyć API z dowolnej metody, które obsługuje struktury Swagger.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-148">The Swagger endpoint must be unauthenticated to be usable in the Logic App Designer, although you can secure the API itself with whatever methods that Swagger supports.</span></span>

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a><span data-ttu-id="d7b8a-149">Wywołaj wdrożonej aplikacji interfejsu API za pomocą 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="d7b8a-149">Call deployed API apps with 2015-08-01-preview</span></span>

<span data-ttu-id="d7b8a-150">Jeśli wdrożono aplikację interfejsu API można wywołać w aplikacji przy użyciu **HTTP** akcji.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-150">If you previously deployed an API App, you can call the app with the **HTTP** action.</span></span>

<span data-ttu-id="d7b8a-151">Na przykład, jeśli używasz usługi Dropbox Aby wyświetlić listę plików z **2014-12-01-preview** definicji wersji schematu może mieć wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="d7b8a-151">For example, if you use Dropbox to list files, your **2014-12-01-preview** schema version definition might have something like:</span></span>

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

<span data-ttu-id="d7b8a-152">Odpowiednik akcji HTTP, tak jak ten przykład można utworzyć sekcji Parametry definicję aplikacji logiki pozostaje bez zmian:</span><span class="sxs-lookup"><span data-stu-id="d7b8a-152">You can construct the equivalent HTTP action like this example, while the parameters section of the Logic app definition remains unchanged:</span></span>

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

<span data-ttu-id="d7b8a-153">Instruktaż te właściwości jeden po drugim:</span><span class="sxs-lookup"><span data-stu-id="d7b8a-153">Walking through these properties one-by-one:</span></span>

| <span data-ttu-id="d7b8a-154">Właściwość Action</span><span class="sxs-lookup"><span data-stu-id="d7b8a-154">Action property</span></span> | <span data-ttu-id="d7b8a-155">Opis</span><span class="sxs-lookup"><span data-stu-id="d7b8a-155">Description</span></span> |
| --- | --- |
| `type` |<span data-ttu-id="d7b8a-156">`Http`Zamiast`APIapp`</span><span class="sxs-lookup"><span data-stu-id="d7b8a-156">`Http` instead of `APIapp`</span></span> |
| `metadata.apiDefinitionUrl` |<span data-ttu-id="d7b8a-157">Aby użyć tej akcji w Projektancie aplikacji logiki, obejmują punktu końcowego metadanych, który jest tworzony z:`{api app host.gateway}/api/service/apidef/{last segment of the api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span><span class="sxs-lookup"><span data-stu-id="d7b8a-157">To use this action in the Logic App Designer, include the metadata endpoint, which is constructed from: `{api app host.gateway}/api/service/apidef/{last segment of the api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span></span> |
| `inputs.uri` |<span data-ttu-id="d7b8a-158">Utworzone na podstawie:`{api app host.gateway}/api/service/invoke/{last segment of the api app host.id}/{api app operation}?api-version=2015-01-14`</span><span class="sxs-lookup"><span data-stu-id="d7b8a-158">Constructed from: `{api app host.gateway}/api/service/invoke/{last segment of the api app host.id}/{api app operation}?api-version=2015-01-14`</span></span> |
| `inputs.method` |<span data-ttu-id="d7b8a-159">Zawsze`POST`</span><span class="sxs-lookup"><span data-stu-id="d7b8a-159">Always `POST`</span></span> |
| `inputs.body` |<span data-ttu-id="d7b8a-160">Takie same jak parametry aplikacji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="d7b8a-160">Identical to the API App parameters</span></span> |
| `inputs.authentication` |<span data-ttu-id="d7b8a-161">Taki sam jak uwierzytelniania aplikacji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="d7b8a-161">Identical to the API App authentication</span></span> |

<span data-ttu-id="d7b8a-162">Ta metoda powinna działać dla wszystkich akcji w aplikacji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-162">This approach should work for all API App actions.</span></span> <span data-ttu-id="d7b8a-163">Należy jednak pamiętać, że tych poprzedniej aplikacji interfejsu API nie są już obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-163">However, remember that these previous API Apps are no longer supported.</span></span> <span data-ttu-id="d7b8a-164">Dlatego należy przenieść do jednej z dwóch innych poprzednie opcje zarządzanego interfejsu API lub hosting niestandardowego interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-164">So you should move to one of the two other previous options, a managed API or hosting your custom Web API.</span></span>

<a name="foreach"></a>
## <a name="renamed-repeat-to-foreach"></a><span data-ttu-id="d7b8a-165">Zmieniona "repeat" do "foreach"</span><span class="sxs-lookup"><span data-stu-id="d7b8a-165">Renamed 'repeat' to 'foreach'</span></span>

<span data-ttu-id="d7b8a-166">W poprzedniej wersji schematu Otrzymaliśmy dużo opinie klientów który **Powtórz** było trudne i poprawnie nie przechwytywania, który **Powtórz** jest rzeczywiście dla każdej pętli.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-166">For the previous schema version, we received much customer feedback that **Repeat** was confusing and didn't properly capture that **Repeat** was really a for-each loop.</span></span> <span data-ttu-id="d7b8a-167">W rezultacie firma Microsoft zmieniono `repeat` do `foreach`.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-167">As a result, we have renamed `repeat` to `foreach`.</span></span> <span data-ttu-id="d7b8a-168">Na przykład wcześniej piszesz:</span><span class="sxs-lookup"><span data-stu-id="d7b8a-168">For example, previously you would write:</span></span>

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

<span data-ttu-id="d7b8a-169">Teraz możesz zapisać:</span><span class="sxs-lookup"><span data-stu-id="d7b8a-169">Now you would write:</span></span>

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

<span data-ttu-id="d7b8a-170">Funkcja `@repeatItem()` był wcześniej używany do bieżącego elementu trwa iterowane przez odwołanie.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-170">The function `@repeatItem()` was previously used to reference the current item being iterated over.</span></span> <span data-ttu-id="d7b8a-171">Ta funkcja jest teraz uproszczona w celu `@item()`.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-171">This function is now simplified to `@item()`.</span></span> 

### <a name="reference-outputs-from-foreach"></a><span data-ttu-id="d7b8a-172">Odwołanie do danych wyjściowych ze "foreach"</span><span class="sxs-lookup"><span data-stu-id="d7b8a-172">Reference outputs from 'foreach'</span></span>

<span data-ttu-id="d7b8a-173">Dla uproszczenia, dane wyjściowe z `foreach` akcje nie są ujęte w nazwie obiektu `repeatItems`.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-173">For simplification, the outputs from `foreach` actions are not wrapped in an object called `repeatItems`.</span></span> <span data-ttu-id="d7b8a-174">Podczas gdy dane wyjściowe z poprzedniej `repeat` zostały przykładzie:</span><span class="sxs-lookup"><span data-stu-id="d7b8a-174">While the outputs from the previous `repeat` example were:</span></span>

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

<span data-ttu-id="d7b8a-175">Teraz te dane wyjściowe są:</span><span class="sxs-lookup"><span data-stu-id="d7b8a-175">Now these outputs are:</span></span>

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

<span data-ttu-id="d7b8a-176">Wcześniej Aby uzyskać dostęp do treści akcji podczas odwoływania się do tych danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="d7b8a-176">Previously, to get to the body of the action when referencing these outputs:</span></span>

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

<span data-ttu-id="d7b8a-177">Teraz można wykonać zamiast tego:</span><span class="sxs-lookup"><span data-stu-id="d7b8a-177">Now you can do instead:</span></span>

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

<span data-ttu-id="d7b8a-178">Wprowadzone zmiany funkcji `@repeatItem()`, `@repeatBody()`, i `@repeatOutputs()` są usuwane.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-178">With these changes, the functions `@repeatItem()`, `@repeatBody()`, and `@repeatOutputs()` are removed.</span></span>

<a name="http-listener"></a>
## <a name="native-http-listener"></a><span data-ttu-id="d7b8a-179">Natywny odbiornika HTTP</span><span class="sxs-lookup"><span data-stu-id="d7b8a-179">Native HTTP listener</span></span>

<span data-ttu-id="d7b8a-180">Odbiornik HTTP funkcji są obecnie wbudowane w.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-180">The HTTP Listener capabilities are now built in.</span></span> <span data-ttu-id="d7b8a-181">Dlatego nie należy wdrożyć aplikację interfejsu API odbiornika HTTP.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-181">So you no longer need to deploy an HTTP Listener API App.</span></span> <span data-ttu-id="d7b8a-182">Zobacz [szczegółowe instrukcje punkt końcowy aplikacji logiki można wywołać w tym miejscu](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="d7b8a-182">See [the full details for how to make your Logic app endpoint callable here](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<span data-ttu-id="d7b8a-183">Wprowadzone zmiany, firma Microsoft usunęła `@accessKeys()` funkcji, która możemy zastąpione `@listCallbackURL()` funkcja uzyskania punktu końcowego, gdy jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-183">With these changes, we removed the `@accessKeys()` function, which we replaced with the `@listCallbackURL()` function for getting the endpoint when necessary.</span></span> <span data-ttu-id="d7b8a-184">Ponadto teraz należy zdefiniować co najmniej jeden wyzwalacz w aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-184">Also, you must now define at least one trigger in your logic app.</span></span> <span data-ttu-id="d7b8a-185">Jeśli chcesz `/run` przepływu pracy, musi mieć jeden z tych wyzwalaczy: `manual`, `apiConnectionWebhook`, lub `httpWebhook`.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-185">If you want to `/run` the workflow, you must have one of these triggers: `manual`, `apiConnectionWebhook`, or `httpWebhook`.</span></span>

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a><span data-ttu-id="d7b8a-186">Wywołania podrzędne przepływy pracy</span><span class="sxs-lookup"><span data-stu-id="d7b8a-186">Call child workflows</span></span>

<span data-ttu-id="d7b8a-187">Wcześniej wywoływania podrzędnego przepływów pracy wymagane do przepływu pracy, pobierania tokenu dostępu i wklejania tokenu w definicji aplikacji logiki, którym chcesz się połączyć podrzędny przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-187">Previously, calling child workflows required going to the workflow, getting the access token, and pasting the token in the logic app definition where you want to call that child workflow.</span></span> <span data-ttu-id="d7b8a-188">Z nowym schematem aparat Logic Apps automatycznie generuje SAS w czasie wykonywania przepływu pracy podrzędny, dzięki czemu nie trzeba Wklej żadnych kluczy tajnych w definicji.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-188">With the new schema, the Logic Apps engine automatically generates a SAS at runtime for the child workflow so you don't have to paste any secrets into the definition.</span></span> <span data-ttu-id="d7b8a-189">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="d7b8a-189">Here is an example:</span></span>

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

<span data-ttu-id="d7b8a-190">Drugi poprawy jest udostępniamy możliwość sprawowania podrzędne przepływy pracy pełny dostęp do żądania przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-190">A second improvement is we are giving the child workflows full access to the incoming request.</span></span> <span data-ttu-id="d7b8a-191">Oznacza to, że można przekazać parametr w *zapytania* sekcji i w *nagłówki* obiekt i który pełni można zdefiniować całej treści.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-191">That means that you can pass parameters in the *queries* section and in the *headers* object and that you can fully define the entire body.</span></span>

<span data-ttu-id="d7b8a-192">Ponadto istnieją zmiany wymagane w celu podrzędny przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-192">Finally, there are required changes to the child workflow.</span></span> <span data-ttu-id="d7b8a-193">Gdy wcześniej można bezpośrednio wywołać podrzędny przepływ pracy, teraz należy zdefiniować punkt końcowy wyzwalacza w przepływie pracy nadrzędnego do wywołania.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-193">While you could previously call a child workflow directly, now you must define a trigger endpoint in the workflow for the parent to call.</span></span> <span data-ttu-id="d7b8a-194">Ogólnie rzecz biorąc, należy dodać wyzwalacz, który ma `manual` typu, a następnie użyj tego wyzwalacza w definicji nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-194">Generally, you would add a trigger that has `manual` type, and then use that trigger in the parent definition.</span></span> <span data-ttu-id="d7b8a-195">Uwaga `host` właściwość specjalnie ma `triggerName` ponieważ należy zawsze określić, której wyzwalacz wywoływania.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-195">Note the `host` property specifically has a `triggerName` because you must always specify which trigger you are invoking.</span></span>

## <a name="other-changes"></a><span data-ttu-id="d7b8a-196">Inne zmiany</span><span class="sxs-lookup"><span data-stu-id="d7b8a-196">Other changes</span></span>

### <a name="new-queries-property"></a><span data-ttu-id="d7b8a-197">Nowe właściwości "zapytania"</span><span class="sxs-lookup"><span data-stu-id="d7b8a-197">New 'queries' property</span></span>

<span data-ttu-id="d7b8a-198">Wszystkie typy akcji obsługują teraz nowe dane wejściowe o nazwie `queries`.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-198">All action types now support a new input called `queries`.</span></span> <span data-ttu-id="d7b8a-199">Tych danych wejściowych może być obiektu strukturalnego, zamiast konieczności ręcznie utworzyć ciąg.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-199">This input can be a structured object, rather than you having to assemble the string by hand.</span></span>

### <a name="renamed-parse-function-to-json"></a><span data-ttu-id="d7b8a-200">Zmieniono nazwę parse() funkcji "json()"</span><span class="sxs-lookup"><span data-stu-id="d7b8a-200">Renamed 'parse()' function to 'json()'</span></span>

<span data-ttu-id="d7b8a-201">Dodajemy więcej zawartości typy wkrótce, dlatego firma Microsoft zmieniona `parse()` funkcja `json()`.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-201">We are adding more content types soon, so we renamed the `parse()` function to `json()`.</span></span>

## <a name="coming-soon-enterprise-integration-apis"></a><span data-ttu-id="d7b8a-202">Wkrótce: interfejsy API integracji przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="d7b8a-202">Coming soon: Enterprise Integration APIs</span></span>

<span data-ttu-id="d7b8a-203">Nie mamy zarządzanej wersji jeszcze API integracji przedsiębiorstwa, takich jak AS2.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-203">We don't have managed versions yet of the Enterprise Integration APIs, like AS2.</span></span> <span data-ttu-id="d7b8a-204">W tym samym czasie możesz użyć istniejących wdrożonej BizTalk interfejsów API za pomocą akcji HTTP.</span><span class="sxs-lookup"><span data-stu-id="d7b8a-204">Meanwhile, you can use your existing deployed BizTalk APIs through the HTTP action.</span></span> <span data-ttu-id="d7b8a-205">Aby uzyskać więcej informacji, zobacz "Używanie już raz wdrożonej aplikacji interfejsu API" w [plan integracji](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span><span class="sxs-lookup"><span data-stu-id="d7b8a-205">For details, see "Using your already deployed API apps" in the [integration roadmap](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span></span> 
