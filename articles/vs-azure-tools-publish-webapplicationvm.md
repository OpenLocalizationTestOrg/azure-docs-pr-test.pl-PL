---
title: aaaPublish WebApplicationVM | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toodeploy maszyny wirtualnej tooa aplikacji sieci web. Ten skrypt tworzy hello wymaganych zasobów w Twojej subskrypcji platformy Azure, jeśli nie istnieją."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: e4b52b620bebf44b87ddfc3b19c155bb65111814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a>Publikowanie WebApplicationVM (skrypt programu Windows PowerShell)
Wdraża maszynę wirtualną tooa aplikacji sieci web. Witaj skrypt tworzy hello wymaganych zasobów w Twojej subskrypcji platformy Azure, jeśli nie istnieją.

```
Publish-WebApplicationVM
–Configuration <configuration>
-SubscriptionName <subscriptionName>
-WebDeployPackage <packageName>
-VMPassword @{Name = "name"; Password = "password")
-DatabaseServerPassword @{Name = "name"; Password = "password"}
-SendHostMessagesToOutput
-Verbose
```

### <a name="configuration"></a>Konfiguracja
Witaj ścieżki toohello plik JSON konfiguracji opisujący szczegóły hello hello wdrożenia.

| Aliasy | Brak |
| --- | --- |
| Wymagana? |Wartość true |
| Stanowisko |o nazwie |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |wartość false |
| Akceptowanie symboli wieloznacznych? |wartość false |

### <a name="subscriptionname"></a>Nazwa subskrypcji
Nazwa Hello hello subskrypcji platformy Azure, w której ma zostać maszyny wirtualnej hello toocreate.

| Aliasy | Brak |
| --- | --- |
| Wymagana? |wartość false |
| Stanowisko |o nazwie |
| Wartość domyślna |Używa pierwszej subskrypcji hello w pliku subskrypcji hello |
| Akceptowanie danych wejściowych potoku? |wartość false |
| Akceptowanie symboli wieloznacznych? |wartość false |

### <a name="webdeploypackage"></a>WebDeployPackage
Witaj ścieżki toohello sieci web wdrożenia pakietu toopublish toohello maszyny wirtualnej. Ten pakiet można utworzyć za pomocą kreatora Publikowanie w sieci Web hello w programie Visual Studio. Zobacz [jak: utworzyć pakiet wdrożeniowy sieci Web w programie Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).

| Aliasy | Brak |
| --- | --- |
| Wymagana? |wartość false |
| Stanowisko |o nazwie |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |wartość false |
| Akceptowanie symboli wieloznacznych? |wartość false |

### <a name="allowuntrusted"></a>AllowUntrusted
Jeśli PRAWDA, Zezwól hello korzystanie z certyfikatów, które nie są podpisane przez zaufanego głównego urzędu.

| Aliasy | Brak |
| --- | --- |
| Wymagana? |wartość false |
| Stanowisko |o nazwie |
| Wartość domyślna |wartość false |
| Akceptowanie danych wejściowych potoku? |wartość false |
| Akceptowanie symboli wieloznacznych? |wartość false |

### <a name="vmpassword"></a>VMPassword
poświadczenia Hello hello konta maszyny wirtualnej. Przykład: - VMPassword @{nazwa = "admin"; Hasło = "password"}

| Aliasy | Brak |
| --- | --- |
| Wymagana? |wartość false |
| Stanowisko |o nazwie |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |wartość false |
| Akceptowanie symboli wieloznacznych? |wartość false |

### <a name="databaseserverpassword"></a>DatabaseServerPassword
poświadczenia Hello hello bazy danych SQL platformy Azure. Przykład: - DatabaseServerPassword @{nazwa = "admin"; Hasło = "password"}

| Aliasy | Brak |
| --- | --- |
| Wymagana? |wartość false |
| Stanowisko |o nazwie |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |wartość false |
| Akceptowanie symboli wieloznacznych? |wartość false |

### <a name="sendhostmessagestooutput"></a>SendHostMessagesToOutput
Jeśli PRAWDA, drukowania wiadomości powitania skryptu toohello output strumienia.

| Aliasy | Brak |
| --- | --- |
| Wymagana? |wartość false |
| Stanowisko |o nazwie |
| Wartość domyślna |wartość false |
| Akceptowanie danych wejściowych potoku? |wartość false |
| Akceptowanie symboli wieloznacznych? |wartość false |

## <a name="remarks"></a>Uwagi
Pełny opis sposobu toouse hello skryptu toocreate deweloperów i środowisk testowych, zobacz [tooDev tooPublish przy użyciu skrypty programu Windows PowerShell i środowisk testowych](vs-azure-tools-publishing-using-powershell-scripts.md).

plik konfiguracji JSON Hello określa szczegóły hello co to jest toobe wdrożone. Zawiera informacje dotyczące hello podane podczas tworzenia projektu hello, takie jak nazwa hello, grupy koligacji, obrazu wirtualnego dysku twardego i rozmiar maszyny wirtualnej hello. Także zawiera punkty końcowe hello na maszynie wirtualnej hello hello tooprovision baz danych, jeśli istnieje i parametry wdrażania w sieci web. Witaj następującego kodu przedstawiono przykładowy plik konfiguracji JSON:

```
{
    "environmentSettings": {
        "cloudService": {
            "name": "myvmname",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myvmname",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201404.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [
                    {
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [
            {
                "connectionStringName": "",
                "databaseName": "",
                "serverName": "",
                "user": "",
                "password": ""
            }
        ],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

Co to jest administracyjnie hello JSON konfiguracji pliku toochange można edytować. Maszyny wirtualne i usługi w chmurze są wymagane, ale hello bazy danych sekcja jest opcjonalna.

