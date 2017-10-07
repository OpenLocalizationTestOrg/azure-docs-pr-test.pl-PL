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
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a>Aktualizacje schematu dla usługi Azure Logic Apps - 1 sierpnia 2015 preview

Tego nowego schematu i interfejsu API w wersji dla usługi Azure Logic Apps zawiera kluczowe ulepszenia lepiej aplikacje logiki niezawodnych i łatwiejsze toouse:

*   Witaj **APIApp** typ akcji jest zaktualizowane tooa nowe [ **APIConnection** ](#api-connections) typ akcji.
*   **Powtórz** jest zmieniana zbyt[**Foreach**](#foreach).
*   Witaj [ **odbiornik HTTP** aplikacji interfejsu API](#http-listener) nie jest już wymagane.
*   Wywoływanie podrzędnego przepływy pracy używa [nowego schematu](#child-workflows).

<a name="api-connections"></a>
## <a name="move-tooapi-connections"></a>Przenieś tooAPI połączeń

Zmiana największych Hello jest, że nie masz już toodeploy API Apps do Twojej subskrypcji platformy Azure, aby można było używać interfejsów API. Poniżej przedstawiono sposoby hello użyć interfejsów API:

* Zarządzane interfejsy API
* Niestandardowych interfejsów API sieci Web

Każdego sposób różni się nieznacznie, ponieważ ich zarządzania i modele obsługi są różne. Jedną z zalet tego modelu jest jest już ograniczone tooresources, które są wdrożone w grupie zasobów platformy Azure. 

### <a name="managed-apis"></a>Zarządzane interfejsy API

Firma Microsoft zarządza niektórych interfejsów API w Twoim imieniu, takie jak usługi Office 365, Salesforce, Twitter i FTP. Można użyć niektóre zarządzane interfejsy API jako — jest, takich jak Bing tłumaczenia, a inne wymagają konfiguracji. Ta konfiguracja jest nazywana *połączenia*.

Na przykład gdy używasz usługi Office 365, możesz utworzyć połączenie, które zawiera token logowania usługi Office 365. Token ten jest bezpiecznie przechowywane i odświeżania, dzięki czemu aplikację logiki zawsze można wywołać interfejsu API usługi Office 365 hello. Alternatywnie Chcąc tooconnect tooyour SQL lub serwer FTP, należy utworzyć połączenie, które ma hello parametry połączenia. 

W tej definicji, te akcje są nazywane `APIConnection`. Oto przykład połączenia, które wywołuje toosend usługi Office 365 wiadomości e-mail:

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

Witaj `host` obiekt jest część danych wejściowych jest unikatowy tooAPI połączeń, która zawiera części tow: `api` i `connection`.

Witaj `api` ma środowiska uruchomieniowego hello znajduje się adres URL gdzie, która zarządza interfejsu API. Widać hello wszystkie dostępne zarządzanych interfejsów API, wywołując `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.

Jeśli korzystasz z interfejsu API hello interfejsu API może lub nie może mieć dowolną *parametry połączenia* zdefiniowane. Jeśli nie hello interfejsu API, nie *połączenia* jest wymagana. Jeśli nie hello interfejsu API, należy utworzyć połączenie. Hello utworzone połączenie ma nazwę hello, którą wybierzesz. Następnie odwoływać się nazwy hello w hello `connection` obiektu wewnątrz hello `host` obiektu. toocreate połączenia w grupie zasobów, rozmów:

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

Z hello następującej treści:

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

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a>Wdrażanie zarządzanych interfejsów API w szablonie usługi Azure Resource Manager

Można utworzyć pełne zastosowanie szablonu usługi Azure Resource Manager tak długo, jak interakcyjnego logowania nie jest wymagane.
Jeśli logowanie jest wymagana, można skonfigurować wszystkie elementy z szablonem usługi Azure Resource Manager hello, ale nadal masz toovisit hello portalu tooauthorize hello połączenia. 

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

Widać w tym przykładzie połączeń hello są tylko zasoby, które znajdują się w grupie zasobów. Odwołujących się do hello zarządzane interfejsy API tooyou dostępne w ramach subskrypcji.

### <a name="your-custom-web-apis"></a>Niestandardowych interfejsów API sieci Web

Jeśli używasz własnych interfejsów API, z nich nie zarządzany przez firmę Microsoft, Użyj wbudowanych hello **HTTP** toocall akcji je. Nadaje się doskonale środowisko powinny ujawniać punktu końcowego struktury Swagger dla interfejsu API. Ten punkt końcowy włącza hello projektanta aplikacji logiki toorender hello w danych wejściowych i danych wyjściowych dla interfejsu API. Bez struktury Swagger Projektant hello można tylko wyświetlić hello wejściami i wyjściami jako nieprzezroczyste obiektów JSON.

Oto przykład przedstawiający hello nowe `metadata.apiDefinitionUrl` właściwości:

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

Jeśli na serwerze sieci Web interfejsu API w usłudze Azure App Service interfejsu API sieci Web automatycznie zostanie wyświetlony hello listę dostępnych w Projektancie hello akcji. Jeśli nie masz toopaste w adresie URL hello bezpośrednio. punktu końcowego struktury Swagger Hello musi być nieuwierzytelnione toobe w hello projektanta aplikacji logiki, mimo że można zabezpieczyć hello interfejsu API się z dowolnej metody, które obsługuje struktury Swagger.

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a>Wywołaj wdrożonej aplikacji interfejsu API za pomocą 2015-08-01-preview

Jeśli wdrożono aplikację interfejsu API można wywołać aplikacji hello z hello **HTTP** akcji.

Na przykład, jeśli pliki toolist Dropbox Twoje **2014-12-01-preview** definicji wersji schematu może mieć wyglądać mniej więcej tak:

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

Można utworzyć hello równoważne akcji HTTP, tak jak ten przykład sekcji parametrów hello hello definicję aplikacji logiki pozostaje bez zmian:

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

Instruktaż te właściwości jeden po drugim:

| Właściwość Action | Opis |
| --- | --- |
| `type` |`Http`Zamiast`APIapp` |
| `metadata.apiDefinitionUrl` |toouse tej akcji w hello projektanta aplikacji logiki, obejmują punktu końcowego metadanych hello, który jest tworzony z:`{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard` |
| `inputs.uri` |Utworzone na podstawie:`{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14` |
| `inputs.method` |Zawsze`POST` |
| `inputs.body` |Parametry aplikacji identyczne toohello interfejsu API |
| `inputs.authentication` |Identyczne toohello uwierzytelniania aplikacji interfejsu API |

Ta metoda powinna działać dla wszystkich akcji w aplikacji interfejsu API. Należy jednak pamiętać, że tych poprzedniej aplikacji interfejsu API nie są już obsługiwane. Dlatego należy przenieść tooone hello dwóch innych poprzedniej opcji zarządzanego interfejsu API lub hosting niestandardowego interfejsu API sieci Web.

<a name="foreach"></a>
## <a name="renamed-repeat-tooforeach"></a>Zmieniono jego nazwę, powtórz too'foreach "

Dla wcześniejszych wersji schematu hello Otrzymaliśmy dużo opinie klientów który **Powtórz** było trudne i poprawnie nie przechwytywania, który **Powtórz** jest rzeczywiście dla każdej pętli. W rezultacie firma Microsoft zmieniono `repeat` zbyt`foreach`. Na przykład wcześniej piszesz:

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

Teraz możesz zapisać:

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

Witaj funkcja `@repeatItem()` został poprzednio tooreference hello bieżący element jest iterowane za pośrednictwem. Ta funkcja jest teraz uproszczone zbyt`@item()`. 

### <a name="reference-outputs-from-foreach"></a>Odwołanie do danych wyjściowych ze "foreach"

Dla uproszczenia hello danych wyjściowych ze `foreach` akcje nie są ujęte w nazwie obiektu `repeatItems`. Gdy hello danych wyjściowych z poprzednich hello `repeat` zostały przykładzie:

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

Teraz te dane wyjściowe są:

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

Wcześniej tooget toohello treść hello akcji podczas odwoływania się do tych danych wyjściowych:

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

Teraz można wykonać zamiast tego:

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

Wprowadzone zmiany hello funkcji `@repeatItem()`, `@repeatBody()`, i `@repeatOutputs()` są usuwane.

<a name="http-listener"></a>
## <a name="native-http-listener"></a>Natywny odbiornika HTTP

Witaj możliwości są obecnie wbudowane w odbiornik HTTP. Nie należy więc toodeploy aplikacji interfejsu API odbiornika HTTP. Zobacz [hello pełne szczegóły na temat toomake Twojego logiki aplikacji punktu końcowego można wywołać tutaj](../logic-apps/logic-apps-http-endpoint.md). 

Wprowadzone zmiany, firma Microsoft usunęła hello `@accessKeys()` funkcji, która możemy zastąpione hello `@listCallbackURL()` funkcja uzyskania hello punktu końcowego, gdy jest to konieczne. Ponadto teraz należy zdefiniować co najmniej jeden wyzwalacz w aplikacji logiki. Jeśli chcesz zbyt`/run` hello przepływu pracy, musi mieć jeden z tych wyzwalaczy: `manual`, `apiConnectionWebhook`, lub `httpWebhook`.

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a>Wywołania podrzędne przepływy pracy

Wcześniej wywoływania podrzędnego przepływów pracy wymagane będzie toohello przepływu pracy, uzyskiwanie hello token dostępu i token hello wklejanie w definicji aplikacji logiki hello miejscu toocall podrzędny przepływ pracy. Hello nowego schematu aplikacji logiki hello aparat automatycznie generuje sygnaturę dostępu Współdzielonego w czasie wykonywania dla hello podrzędny przepływ pracy, nie ma zbyt wklejania żadnych kluczy tajnych w definicji hello. Oto przykład:

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

Drugi poprawy jest udostępniamy możliwość sprawowania podrzędnych hello przychodzące żądanie toohello pełny dostęp przepływów pracy. Oznacza to, że można przekazywać parametrów w hello *zapytania* sekcji w hello *nagłówki* obiekt i który pełni można zdefiniować hello całej treści.

Na koniec są wymagane zmiany toohello podrzędny przepływ pracy. Podczas wcześniej można bezpośrednio wywołać podrzędny przepływ pracy, teraz należy zdefiniować punkt końcowy wyzwalacza w przepływie pracy powitania dla hello toocall nadrzędnego. Ogólnie rzecz biorąc, należy dodać wyzwalacz, który ma `manual` typu, a następnie użyj tego wyzwalacza w definicji nadrzędnej hello. Uwaga hello `host` właściwość specjalnie ma `triggerName` ponieważ należy zawsze określić, której wyzwalacz wywoływania.

## <a name="other-changes"></a>Inne zmiany

### <a name="new-queries-property"></a>Nowe właściwości "zapytania"

Wszystkie typy akcji obsługują teraz nowe dane wejściowe o nazwie `queries`. Obiektu strukturalnego, zamiast ponownego ciąg hello tooassemble ręcznie, może być tych danych wejściowych.

### <a name="renamed-parse-function-toojson"></a>Zmieniona "parse()" Funkcja too'json() "

Dodajemy więcej zawartości typy wkrótce, dlatego firma Microsoft zmieniona hello `parse()` funkcji zbyt`json()`.

## <a name="coming-soon-enterprise-integration-apis"></a>Wkrótce: interfejsy API integracji przedsiębiorstwa

Nie mamy zarządzanej wersji jeszcze hello interfejsów API integracji przedsiębiorstwa, takich jak AS2. W tym samym czasie możesz użyć istniejących wdrożonej BizTalk interfejsów API za pomocą hello akcji HTTP. Aby uzyskać więcej informacji, zobacz "Używanie już raz wdrożonej aplikacji interfejsu API" w hello [plan integracji](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/). 
