---
title: "aaaAzure automatyzacji zasobów w rozwiązaniach pakietu OMS | Dokumentacja firmy Microsoft"
description: "Rozwiązania w OMS zazwyczaj uwzględnia elementów runbook w automatyzacji Azure tooautomate procesy, takie jak zbierania i przetwarzania danych monitorowania.  W tym artykule opisano sposób tooinclude elementów runbook i ich powiązane zasoby w rozwiązaniu."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 5281462e-f480-4e5e-9c19-022f36dce76d
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 82a156f89bf77ce25e52e5e4596261ec07a24dae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-automation-resources-tooan-oms-management-solution-preview"></a>Dodawanie usługi Automatyzacja Azure zasobów tooan OMS rozwiązania do zarządzania (wersja zapoznawcza)
> [!NOTE]
> To jest wstępna dokumentacji do tworzenia rozwiązań do zarządzania w OMS, które są obecnie w wersji zapoznawczej. Żadnego schematu opisanych poniżej jest toochange podmiotu.   


[Rozwiązania do zarządzania w OMS](operations-management-suite-solutions.md) zazwyczaj uwzględnia elementów runbook w automatyzacji Azure tooautomate procesy, takie jak zbierania i przetwarzania danych monitorowania.  Ponadto toorunbooks, kont automatyzacji zawiera zasoby, takie jak zmienne i harmonogramy obsługuje hello elementów runbook używane w rozwiązaniu hello.  W tym artykule opisano sposób tooinclude elementów runbook i ich powiązane zasoby w rozwiązaniu.

> [!NOTE]
> cześć przykłady w tym artykule Użyj parametry i zmienne, które są albo toomanagement wymagane lub typowych rozwiązań i opisane w [tworzenia rozwiązań do zarządzania w Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md) 


## <a name="prerequisites"></a>Wymagania wstępne
W tym artykule przyjęto założenie, że znasz już hello następujących informacji.

- Jak zbyt[tworzenie rozwiązania do zarządzania](operations-management-suite-solutions-creating.md).
- Witaj struktury [plik rozwiązania](operations-management-suite-solutions-solution-file.md).
- Jak zbyt[Tworzenie szablonów usługi Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)

## <a name="automation-account"></a>Konto usługi Automation
Wszystkie zasoby w automatyzacji Azure są zawarte w [konto automatyzacji](../automation/automation-security-overview.md#automation-account-overview).  Zgodnie z opisem w [OMS obszaru roboczego i konto automatyzacji](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello konta automatyzacji nie jest zawarty w rozwiązaniu do zarządzania hello, ale musi istnieć przed zainstalowaniem hello rozwiązania.  Jeśli nie jest dostępna, następnie hello rozwiązania instalacja zakończy się niepowodzeniem.

Nazwa Hello każdego zasobu automatyzacji zawiera nazwę hello jego konta automatyzacji.  Odbywa się w rozwiązaniu hello hello **accountName** parametru jak hello poniższy przykład zasobu elementu runbook.

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a>Elementy Runbook
Należy uwzględnić wszystkie elementy runbook używana przez rozwiązania hello w pliku rozwiązania hello, dzięki czemu są tworzone po zainstalowaniu hello rozwiązania.  Hello treści elementu runbook hello hello szablonu nie może zawierać jednak, należy opublikować hello runbook tooa lokalizacji publicznej gdzie jest dostępny przez dowolnego użytkownika instalowanie rozwiązania.

[Element runbook automatyzacji Azure](../automation/automation-runbook-types.md) zasoby mają typ **Microsoft.Automation/automationAccounts/runbooks** i mieć hello następujące struktury. W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów hello. 

    {
        "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
        "type": "Microsoft.Automation/automationAccounts/runbooks",
        "apiVersion": "[variables('AutomationApiVersion')]",
        "dependsOn": [
        ],
        "location": "[parameters('regionId')]",
        "tags": { },
        "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
                "uri": "[variables('Runbook').Uri]",
                "version": [variables('Runbook').Version]"
            }
        }
    }


w hello w poniższej tabeli opisano Hello właściwości dla elementów runbook.

| Właściwość | Opis |
|:--- |:--- |
| runbookType |Określa typy hello hello elementu runbook. <br><br> Skrypt — skrypt programu PowerShell <br>PowerShell — przepływ pracy programu PowerShell <br> GraphPowerShell - runbook skryptu PowerShell graficznego <br> GraphPowerShellWorkflow - PowerShell graficzny element runbook przepływu pracy |
| logProgress |Określa, czy [rekordy postępu](../automation/automation-runbook-output-and-messages.md) ma być generowany dla hello elementu runbook. |
| logVerbose |Określa, czy [rekordów pełnych](../automation/automation-runbook-output-and-messages.md) ma być generowany dla hello elementu runbook. |
| description |Opcjonalny opis hello elementu runbook. |
| publishContentLink |Określa hello zawartość elementu hello runbook. <br><br>Identyfikator URI - Uri toohello zawartość elementu hello runbook.  Są to plik .ps1 dla elementów runbook programu PowerShell i skryptów, a plik wyeksportowany element runbook graficzny element runbook wykresu.  <br> Wersja — wersji elementu runbook hello własne śledzenia. |


## <a name="automation-jobs"></a>Automatyzacja zadań
Po uruchomieniu elementu runbook w automatyzacji Azure tworzy zadanie usługi Automatyzacja.  Możesz dodać automatyzacji zadań zasobów tooyour rozwiązania tooautomatically start element runbook po zainstalowaniu hello rozwiązania do zarządzania.  Ta metoda jest najczęściej używanymi toostart elementy runbook, które służą do konfiguracji początkowej hello rozwiązania.  Utwórz toostart elementu runbook w regularnych odstępach czasu, [harmonogram](#schedules) i [harmonogram zadań](#job-schedules)

Zasoby zadanie ma typ **Microsoft.Automation/automationAccounts/jobs** i mieć hello następujące struktury.  W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów hello. 

    {
      "name": "[concat(parameters('accountName'), '/', parameters('Runbook').JobGuid)]",
      "type": "Microsoft.Automation/automationAccounts/jobs",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
      ],
      "tags": { },
      "properties": {
        "runbook": {
          "name": "[variables('Runbook').Name]"
        },
        "parameters": {
          "Parameter1": "[[variables('Runbook').Parameter1]",
          "Parameter2": "[[variables('Runbook').Parameter2]"
        }
      }
    }

w hello w poniższej tabeli opisano właściwości Hello automatyzacji zadań.

| Właściwość | Opis |
|:--- |:--- |
| Element runbook |Jedna nazwa jednostki o nazwie hello hello toostart elementu runbook. |
| parameters |Jednostki dla każdej wartości parametru wymagane przez element runbook hello. |

Witaj zadania obejmują hello nazwy elementu runbook i wszelkie toobe wartości parametru wysyłane toohello elementu runbook.  zadanie Hello powinien [są zależne od](operations-management-suite-solutions-solution-file.md#resources) hello elementu runbook, który jest uruchamiany od elementu runbook hello musi zostać utworzone przed hello zadania.  Jeśli masz wiele elementów runbook, który ma być uruchamiany przez zadanie, które są zależne od innych zadań, które powinny być uruchamiane w pierwszy można zdefiniować ich kolejność.

Nazwa zasobu zadania Hello musi zawierać identyfikator GUID, który zazwyczaj jest przypisywany przez parametr.  Więcej o parametrach identyfikatora GUID w [tworzenie rozwiązań w Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).  


## <a name="certificates"></a>Certyfikaty
[Certyfikaty automatyzacji Azure](../automation/automation-certificates.md) typu **Microsoft.Automation/automationAccounts/certificates** i mieć hello następujące struktury. W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów hello. 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
      "type": "Microsoft.Automation/automationAccounts/certificates",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "base64Value": "[variables('Certificate').Base64Value]",
        "thumbprint": "[variables('Certificate').Thumbprint]"
      }
    }



w hello w poniższej tabeli opisano Hello właściwości zasobów certyfikatów.

| Właściwość | Opis |
|:--- |:--- |
| base64Value |Wartość Base-64 hello certyfikatu. |
| Odcisk palca |Odcisk palca certyfikatu hello. |



## <a name="credentials"></a>Poświadczenia
[Poświadczenia usługi Automatyzacja Azure](../automation/automation-credentials.md) typu **Microsoft.Automation/automationAccounts/credentials** i mieć hello następujące struktury.  W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów hello. 


    {
      "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
      "type": "Microsoft.Automation/automationAccounts/credentials",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "userName": "[parameters('credentialUsername')]",
        "password": "[parameters('credentialPassword')]"
      }
    }

w hello w poniższej tabeli opisano Hello właściwości zasobów poświadczeń.

| Właściwość | Opis |
|:--- |:--- |
| Nazwa użytkownika |Nazwa użytkownika dla hello poświadczenia. |
| hasło |Hasło dla poświadczeń hello. |


## <a name="schedules"></a>Harmonogramy
[Harmonogramy automatyzacji Azure](../automation/automation-schedules.md) typu **Microsoft.Automation/automationAccounts/schedules** i mieć hello hello następujące struktury. W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów hello. 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
      "type": "microsoft.automation/automationAccounts/schedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Schedule').Description]",
        "startTime": "[parameters('scheduleStartTime')]",
        "timeZone": "[parameters('scheduleTimeZone')]",
        "isEnabled": "[variables('Schedule').IsEnabled]",
        "interval": "[variables('Schedule').Interval]",
        "frequency": "[variables('Schedule').Frequency]"
      }
    }

w hello w poniższej tabeli opisano Hello właściwości harmonogramu zasobów.

| Właściwość | Opis |
|:--- |:--- |
| description |Opcjonalny opis hello harmonogramu. |
| startTime |Określa czas rozpoczęcia harmonogramu hello jako obiekt typu DateTime. Jeśli może zostać przekonwertowany tooa można podać ciąg prawidłowy element DateTime. |
| IsEnabled |Określa, czy harmonogram hello jest włączone. |
| interval |Typ Hello Interwał harmonogramu hello.<br><br>dzień<br>godz. |
| frequency |Witaj harmonogram częstotliwości powinna wyzwalać w liczbie dni lub godzin. |

Harmonogramy musi mieć godzinę rozpoczęcia o wartości większej niż hello bieżącego czasu.  Nie można podać tę wartość za pomocą zmiennych, ponieważ czy nie ma możliwości wiedzy, gdy jest zainstalowany toobe będzie.

Użyj jednej z powitania po dwóch strategii, korzystając z harmonogramu zasobów w rozwiązaniu.

- Użyj parametru hello czas rozpoczęcia harmonogramu hello.  Monit hello użytkownika tooprovide wartość przy instalacji hello rozwiązania.  Jeśli masz wiele harmonogramów można używać wartości jeden parametr dla więcej niż jeden z nich.
- Utwórz harmonogramy hello przy użyciu elementu runbook, który rozpoczyna się, gdy rozwiązanie hello jest zainstalowane.  Spowoduje to usunięcie hello wymaganie toospecify użytkownika hello raz, ale nie może zawierać harmonogram hello w rozwiązaniu, dlatego zostanie usunięta po usunięciu hello rozwiązania.


### <a name="job-schedules"></a>Harmonogramy zadań
Zadania planowania zasobów powiązania elementu runbook z harmonogramem.  Mają one typu **Microsoft.Automation/automationAccounts/jobSchedules** i mieć hello hello następujące struktury.  W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów hello. 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
      "type": "microsoft.automation/automationAccounts/jobSchedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
        "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
      ],
      "tags": {
      },
      "properties": {
        "schedule": {
          "name": "[variables('Schedule').Name]"
        },
        "runbook": {
          "name": "[variables('Runbook').Name]"
        }
      }
    }


w hello w poniższej tabeli opisano właściwości Hello harmonogramy zadań.

| Właściwość | Opis |
|:--- |:--- |
| Nazwa harmonogramu |Pojedynczy **nazwa** jednostki o nazwie hello hello harmonogramu. |
| Nazwa elementu Runbook  |Pojedynczy **nazwa** jednostki o nazwie hello hello elementu runbook.  |



## <a name="variables"></a>Zmienne
[Zmienne automatyzacji Azure](../automation/automation-variables.md) typu **Microsoft.Automation/automationAccounts/variables** i mieć hello następujące struktury.  W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów hello.

    {
      "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
      "type": "microsoft.automation/automationAccounts/variables",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Variable').Description]",
        "isEncrypted": "[variables('Variable').Encrypted]",
        "type": "[variables('Variable').Type]",
        "value": "[variables('Variable').Value]"
      }
    }

w hello w poniższej tabeli opisano Hello właściwości zasobów zmiennej.

| Właściwość | Opis |
|:--- |:--- |
| description | Opcjonalny opis hello zmiennej. |
| isEncrypted | Określa, czy ma być szyfrowana zmienna hello. |
| type | Ta właściwość obecnie nie ma znaczenia.  Typ danych zmiennej hello Hello będzie określana przez wartość początkowa hello. |
| wartość | Wartość zmiennej hello. |

> [!NOTE]
> Witaj **typu** właściwości obecnie nie ma wpływu na powitania zmiennej tworzona.  Typ danych zmiennej hello Hello będzie określana przez wartość hello.  

Jeśli ustawisz hello początkowej wartości zmiennej hello musi być skonfigurowany jako hello prawidłowy typ danych.  Witaj w poniższej tabeli zawiera hello różne typy danych dopuszczalny i ich składni.  Należy pamiętać, że wartości w formacie JSON są oczekiwane tooalways być ujęte w cudzysłów z znaków specjalnych w cudzysłowy hello.  Na przykład wartość ciągu zostałaby określona przez stawiać cudzysłów wokół ciąg hello (przy użyciu znaku ucieczki hello (\\)) podczas zostałaby określona wartość liczbową z jednego zestawu znaków cudzysłowu.

| Typ danych | Opis | Przykład | Usuwa zbyt|
|:--|:--|:--|:--|
| Ciąg   | Wartość należy ująć w cudzysłów.  | "\"Hello world\"" | "Hello world" |
| numeryczne  | Wartość liczbowa z apostrofy.| "64" | 64 |
| Wartość logiczna  | **wartość true,** lub **false** w cudzysłowy.  Należy pamiętać, że ta wartość musi być litera. | wartość "prawda" | Wartość true |
| Data i godzina | Serializacji wartości typu date.<br>Tej wartości można użyć polecenia cmdlet ConvertTo-Json hello w toogenerate środowiska PowerShell dla określonej daty.<br>Przykład: get data "2017-5/24 13:14:57" \| ConvertTo-Json | "\\/Date(1495656897378)\\/" | 2017-05-24 13:14:57 |

## <a name="modules"></a>Moduły
Rozwiązania do zarządzania nie jest konieczne toodefine [modułów globalnych](../automation/automation-integration-modules.md) używany przez elementy runbook, ponieważ zawsze będzie dostępna na Twoim koncie automatyzacji.  Trzeba tooinclude zasobów dla innych modułu używany przez elementy runbook.

[Moduły integracji](../automation/automation-integration-modules.md) typu **Microsoft.Automation/automationAccounts/modules** i mieć hello następujące struktury.  W tym wspólnych zmiennych i parametrów, aby mogli skopiuj i wklej następujący fragment kodu w pliku rozwiązania i Zmień nazwy parametrów hello.

    {
      "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
      "type": "Microsoft.Automation/automationAccounts/modules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "dependsOn": [
      ],
      "properties": {
        "contentLink": {
          "uri": "[variables('Module').Uri]"
        }
      }
    }


w hello w poniższej tabeli opisano Hello właściwości zasobów modułu.

| Właściwość | Opis |
|:--- |:--- |
| contentLink |Określa zawartość hello hello modułu. <br><br>Identyfikator URI - identyfikator Uri zawartości toohello hello modułu.  Są to plik .ps1 dla elementów runbook programu PowerShell i skryptów, a plik wyeksportowany element runbook graficzny element runbook wykresu.  <br> Wersja — wersja modułu hello własne śledzenia. |

Hello runbook powinien zależą od hello modułu zasobów tooensure utworzony przed hello elementu runbook.

### <a name="updating-modules"></a>Aktualizowanie modułów
Aktualizacji rozwiązanie do zarządzania, które zawiera element runbook, który używa harmonogram, a nowej wersji hello rozwiązań ma nowy moduł używany przez ten element runbook, hello runbook może używać hello starą wersję hello modułu.  Należy uwzględnić następujące elementy runbook w rozwiązaniu hello i utworzyć toorun zadania je przed wszystkie inne elementy runbook.  Daje to pewność, że wszystkie moduły są aktualizowane jako wymagany przed powitalne elementy runbook są ładowane.

* [Aktualizacja ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) sprawdzi wszystkie moduły hello używany przez elementy runbook w rozwiązaniu hello najnowszej wersji.  
* [ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) zostanie ponownie zarejestrować wszystkie hello harmonogramu zasobów tooensure, że hello elementy runbook połączone toothem z modułami najnowsze hello użycia.




## <a name="sample"></a>Przykład
Poniżej przedstawiono przykładowe rozwiązanie obejmujące obejmuje hello następujące zasoby:

- Element Runbook.  To jest przykładowy element runbook, przechowywane w publicznych repozytorium GitHub.
- Zadanie usługi Automatyzacja rozpoczynającej się od elementu runbook hello rozwiązania hello jest zainstalowany.
- Harmonogram i zadania harmonogramu toostart hello runbook w regularnych odstępach czasu.
- Certyfikat.
- Poświadczenie.
- Zmienna.
- Moduł.  Jest to hello [modułu OMSIngestionAPI](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) do zapisywania danych tooLog Analytics. 

Witaj używa próbki [parametry standardowego rozwiązania](operations-management-suite-solutions-solution-file.md#parameters) zmiennych, które służy zwykle do rozwiązania jako przeciwieństwie wartości toohardcoding w definicjach zasobów hello.


    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "workspaceName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Log Analytics workspace."
          }
        },
        "accountName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Automation account."
          }
        },
        "workspaceregionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Log Analytics workspace."
          }
        },
        "regionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Automation account."
          }
        },
        "pricingTier": {
          "type": "string",
          "metadata": {
            "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account."
          }
        },
        "certificateBase64Value": {
          "type": "string",
          "metadata": {
            "Description": "Base 64 value for certificate."
          }
        },
        "certificateThumbprint": {
          "type": "securestring",
          "metadata": {
            "Description": "Thumbprint for certificate."
          }
        },
        "credentialUsername": {
          "type": "string",
          "metadata": {
            "Description": "Username for credential."
          }
        },
        "credentialPassword": {
          "type": "securestring",
          "metadata": {
            "Description": "Password for credential."
          }
        },
        "scheduleStartTime": {
          "type": "string",
          "metadata": {
            "Description": "Start time for shedule."
          }
        },
        "scheduleTimeZone": {
          "type": "string",
          "metadata": {
            "Description": "Time zone for schedule."
          }
        },
        "scheduleLinkGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello schedule link toorunbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello runbook job.",
            "control": "guid"
          }
        }
      },
      "variables": {
        "SolutionName": "MySolution",
        "SolutionVersion": "1.0",
        "SolutionPublisher": "Contoso",
        "ProductName": "SampleSolution",
    
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31",
    
        "Runbook": {
          "Name": "MyRunbook",
          "Description": "Sample runbook",
          "Type": "PowerShell",
          "Uri": "https://raw.githubusercontent.com/user/myrepo/master/samples/MyRunbook.ps1",
          "JobGuid": "[parameters('runbookJobGuid')]"
        },
    
        "Certificate": {
          "Name": "MyCertificate",
          "Base64Value": "[parameters('certificateBase64Value')]",
          "Thumbprint": "[parameters('certificateThumbprint')]"
        },
    
        "Credential": {
          "Name": "MyCredential",
          "UserName": "[parameters('credentialUsername')]",
          "Password": "[parameters('credentialPassword')]"
        },
    
        "Schedule": {
          "Name": "MySchedule",
          "Description": "Sample schedule",
          "IsEnabled": "true",
          "Interval": "1",
          "Frequency": "hour",
          "StartTime": "[parameters('scheduleStartTime')]",
          "TimeZone": "[parameters('scheduleTimeZone')]",
          "LinkGuid": "[parameters('scheduleLinkGuid')]"
        },
    
        "Variable": {
          "Name": "MyVariable",
          "Description": "Sample variable",
          "Encrypted": 0,
          "Type": "string",
          "Value": "'This is my string value.'"
        },
    
        "Module": {
          "Name": "OMSIngestionAPI",
          "Uri": "https://devopsgallerystorage.blob.core.windows.net/packages/omsingestionapi.1.3.0.nupkg"
        }
      },
      "resources": [
        {
          "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
          "location": "[parameters('workspaceRegionId')]",
          "tags": { },
          "type": "Microsoft.OperationsManagement/solutions",
          "apiVersion": "[variables('LogAnalyticsApiVersion')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
            "referencedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
            ],
            "containedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]"
            ]
          },
          "plan": {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
            "Version": "[variables('SolutionVersion')]",
            "product": "[variables('ProductName')]",
            "publisher": "[variables('SolutionPublisher')]",
            "promotionCode": ""
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
          "type": "Microsoft.Automation/automationAccounts/runbooks",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "location": "[parameters('regionId')]",
          "tags": { },
          "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
              "uri": "[variables('Runbook').Uri]",
              "version": "1.0.0.0"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').JobGuid)]",
          "type": "Microsoft.Automation/automationAccounts/jobs",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
          ],
          "tags": { },
          "properties": {
            "runbook": {
              "name": "[variables('Runbook').Name]"
            },
            "parameters": {
              "targetSubscriptionId": "[subscription().subscriptionId]",
              "resourcegroup": "[resourceGroup().name]",
              "automationaccount": "[parameters('accountName')]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
          "type": "Microsoft.Automation/automationAccounts/certificates",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "Base64Value": "[variables('Certificate').Base64Value]",
            "Thumbprint": "[variables('Certificate').Thumbprint]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
          "type": "Microsoft.Automation/automationAccounts/credentials",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "userName": "[variables('Credential').UserName]",
            "password": "[variables('Credential').Password]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
          "type": "microsoft.automation/automationAccounts/schedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Schedule').Description]",
            "startTime": "[variables('Schedule').StartTime]",
            "timeZone": "[variables('Schedule').TimeZone]",
            "isEnabled": "[variables('Schedule').IsEnabled]",
            "interval": "[variables('Schedule').Interval]",
            "frequency": "[variables('Schedule').Frequency]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
          "type": "microsoft.automation/automationAccounts/jobSchedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
          ],
          "tags": {
          },
          "properties": {
            "schedule": {
              "name": "[variables('Schedule').Name]"
            },
            "runbook": {
              "name": "[variables('Runbook').Name]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
          "type": "microsoft.automation/automationAccounts/variables",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Variable').Description]",
            "isEncrypted": "[variables('Variable').Encrypted]",
            "type": "[variables('Variable').Type]",
            "value": "[variables('Variable').Value]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
          "type": "Microsoft.Automation/automationAccounts/modules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "properties": {
            "contentLink": {
              "uri": "[variables('Module').Uri]"
            }
          }
        }
    
      ],
      "outputs": { }
    }




## <a name="next-steps"></a>Następne kroki
* [Dodaj rozwiązanie tooyour widoku](operations-management-suite-solutions-resources-views.md) toovisualize zbieranych danych.
