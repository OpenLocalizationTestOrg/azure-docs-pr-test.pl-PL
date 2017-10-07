---
title: aaaPublish-WebApplicationWebSite (skrypt programu Windows PowerShell) | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toopublish sieci web projektu tooan witryny sieci Web platformy Azure. Ten skrypt tworzy hello wymaganych zasobów w Twojej subskrypcji platformy Azure, jeśli nie istnieją."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d46904e30e3c2e040e57888fa31543e8e366527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a>Publikowanie WebApplicationWebSite (skrypt programu Windows PowerShell)
## <a name="syntax"></a>Składnia
Publikuje tooan projektu sieci web Azure witryny sieci Web. Witaj skrypt tworzy hello wymaganych zasobów w Twojej subskrypcji platformy Azure, jeśli nie istnieją.

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a>Konfiguracja
Witaj ścieżki toohello plik JSON konfiguracji opisujący szczegóły hello hello wdrożenia.

| Parametr | Wartość domyślna |
| --- | --- |
| Aliasy |Brak |
| Wymagana? |Wartość true |
| Stanowisko |o nazwie |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |wartość false |
| Akceptowanie symboli wieloznacznych? |wartość false |

## <a name="subscriptionname"></a>Nazwa subskrypcji
Nazwa Hello hello subskrypcji platformy Azure, który ma być toocreate hello witryny sieci Web.

| Parametr | Wartość domyślna |
| --- | --- |
| Aliasy |Brak |
| Wymagana? |wartość false |
| Stanowisko |o nazwie |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |wartość false |
| Akceptowanie symboli wieloznacznych? |wartość false |

## <a name="webdeploypackage"></a>WebDeployPackage
Witaj ścieżki toohello sieci web wdrożenia pakietu toopublish toohello witryny sieci Web. Ten pakiet można utworzyć za pomocą kreatora Publikowanie w sieci Web hello w programie Visual Studio. Aby uzyskać więcej informacji, zobacz [wprowadzenie do usług Azure Cloud Services i platformy ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).

| Parametr | Wartość domyślna |
| --- | --- |
| Aliasy |Brak |
| Wymagana? |wartość false |
| Stanowisko |o nazwie |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |wartość false |
| Akceptowanie symboli wieloznacznych? |wartość false |

## <a name="databaseserverpassword"></a>DatabaseServerPassword
Hello nazwy użytkownika i hasło dla bazy danych SQL hello na platformie Azure.

| Parametr | Wartość domyślna |
| --- | --- |
| Aliasy |Brak |
| Wymagana? |wartość false |
| Stanowisko |o nazwie |
| Wartość domyślna |Brak |
| Akceptowanie danych wejściowych potoku? |wartość false |
| Akceptowanie symboli wieloznacznych? |wartość false |

## <a name="sendhostmessagestooutput"></a>SendHostMessagesToOutput
Jeśli PRAWDA, drukowania wiadomości powitania skryptu toohello output strumienia.

| Parametr | Wartość domyślna |
| --- | --- |
| Aliasy |Brak |
| Wymagana? |wartość false |
| Stanowisko |o nazwie |
| Wartość domyślna |wartość false |
| Akceptowanie danych wejściowych potoku? |wartość false |
| Akceptowanie symboli wieloznacznych? |wartość false |

## <a name="remarks"></a>Uwagi
Pełny opis sposobu toouse hello skryptu toocreate deweloperów i środowisk testowych, zobacz [tooDev tooPublish przy użyciu skrypty programu Windows PowerShell i środowisk testowych](vs-azure-tools-publishing-using-powershell-scripts.md).

plik konfiguracji JSON Hello określa szczegóły hello co to jest toobe wdrożone. Zawiera informacje dotyczące hello podane podczas tworzenia projektu hello, takie jak nazwa hello i nazwa użytkownika dla witryny sieci Web hello. Obejmuje on też hello tooprovision bazy danych, jeśli istnieje. Witaj następującego kodu przedstawiono przykładowy plik konfiguracji JSON:

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

Co to jest wdrażany hello JSON konfiguracji pliku toochange można edytować. Sekcja witryny sieci Web jest wymagana, ale hello bazy danych sekcja jest opcjonalna.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji, zobacz [Publish-WebApplicationVM (skrypt programu Windows PowerShell)](vs-azure-tools-publish-webapplicationvm.md)

