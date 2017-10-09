---
title: "na podstawie aaaToken uwierzytelniania (HTTP/2) dla usługi APNS w usłudze Azure Notification Hubs | Dokumentacja firmy Microsoft"
description: "W tym temacie wyjaśniono, jak tooleverage hello nowy token uwierzytelniania dla usługi APNS"
services: notification-hubs
documentationcenter: .net
author: kpiteira
manager: erikre
editor: 
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 05/17/2017
ms.author: kapiteir
ms.openlocfilehash: 3353d7f16033ce0b68edec9ee9aeb98f47faa1fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="token-based-http2-authentication-for-apns"></a>Uwierzytelniania opartego na tokenie (HTTP/2) dla usługi APNS
## <a name="overview"></a>Omówienie
Ten artykuł zawiera szczegóły dotyczące sposobu uwierzytelniania opartego na toouse hello nowego APNS HTTP/2 protokołu z tokenem.

Witaj klucza przy użyciu nowego protokołu hello zalety:
-   Generowania tokenów jest stosunkowo proste wolnego (toocertificates porównaniu)
-   Nie więcej daty wygaśnięcia — są w formancie tokenów uwierzytelniania i ich odwołań
-   Ładunki można teraz się too4 KB
- Synchroniczne opinii
-   Możesz teraz najnowsze protokołu firmy Apple – certyfikaty nadal używać hello binarne protokołu, który jest oznaczony do amortyzacja

Za pomocą tego nowego mechanizmu może odbywać się w dwóch krokach za kilka minut:
1.  Uzyskaj hello niezbędne informacje z portalu Apple Developer konta hello
2.  Konfigurowanie Centrum powiadomień przy użyciu nowych informacji hello

Centra powiadomień jest teraz wszystkie zestaw toouse hello nowy system uwierzytelniania przy użyciu usługi APNS. 

Należy pamiętać, że po migracji z przy użyciu poświadczeń certyfikatu dla usługi APNS:
- właściwości tokenu Hello zastąpić certyfikat w naszym systemie
- ale aplikacji nadal bezproblemowo tooreceive powiadomienia.

## <a name="obtaining-authentication-information-from-apple"></a>Uzyskiwanie informacji o uwierzytelnianiu od firmy Apple
uwierzytelniania opartego na tokenach tooenable należy hello następujące właściwości z konta dewelopera firmy Apple:
### <a name="key-identifier"></a>Identyfikator klucza
Identyfikator klucza Hello można uzyskać ze strony "Klucze" hello na koncie deweloperów firmy Apple

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a>Identyfikator aplikacji i nazwy aplikacji
Nazwa aplikacji Hello jest dostępna za pośrednictwem strony identyfikatorów aplikacji hello hello konta dewelopera. 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

Identyfikator aplikacji Hello jest dostępna za pośrednictwem strony szczegółów członkostwa hello hello konta dewelopera.
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a>Token uwierzytelniania
można pobrać tokenu uwierzytelniania powitania po wygenerowaniu tokenu dla aplikacji. Aby uzyskać szczegółowe informacje o sposobie toogenerate to token, zobacz zbyt[dokumentacja dla deweloperów firmy Apple](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).

## <a name="configuring-your-notification-hub-toouse-token-based-authentication"></a>Konfigurowanie powiadomień Centrum toouse tokenów uwierzytelniania
### <a name="configure-via-hello-azure-portal"></a>Konfigurowanie za pomocą hello portalu Azure
tooenable token na podstawie uwierzytelniania w portalu hello logowania toohello portalu Azure, przejdź tooyour Centrum powiadomień > Usługi powiadomień > APNS panel. 

Brak nową właściwość — *tryb uwierzytelniania*. Wybranie Token umożliwia tooupdate koncentrator z wszystkie hello odpowiednie właściwości tokenu.

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- Wprowadź właściwości hello, pobierane z konta dewelopera firmy Apple 
- Wybierz tryb aplikacji (środowisko produkcyjne lub piaskownicy) 
- Kliknij przycisk Zapisz tooupdate swoje poświadczenia usługi APNS. 

### <a name="configure-via-management-api-rest"></a>Konfigurowanie za pomocą interfejsu API (REST) do zarządzania

Można użyć naszych [API zarządzania](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate notification hub toouse tokenów uwierzytelniania.
W zależności od tego, czy w przypadku konfigurowania aplikacji hello jest piaskownicy lub produkcji aplikacja (określone w danych konta dewelopera Apple) użyj jednej z odpowiednich punktów końcowych hello:

- Punkt końcowy piaskownicy: [https://api.development.push.apple.com:443/3/urządzenia](https://api.development.push.apple.com:443/3/device)
- Punkt końcowy produkcji: [https://api.push.apple.com:443/3/urządzenia](https://api.push.apple.com:443/3/device)

> [!IMPORTANT]
> Uwierzytelnianie na podstawie tokenu wymaga wersji interfejsu API: **2017 04 lub nowszym**.
> 
> 

Oto przykład tooupdate żądania PUT Centrum przy użyciu uwierzytelniania opartego na tokenie:


        PUT https://{namespace}.servicebus.windows.net/{Notification Hub}?api-version=2017-04
          "Properties": {
            "ApnsCredential": {
              "Properties": {
                "KeyId": "<Your Key Id>",
                "Token": "<Your Authentication Token>",
                "AppName": "<Your Application Name>",
                "AppId": "<Your Application Id>",
                "Endpoint":"<Sandbox/Production Endpoint>"
              }
            }
          }
        

### <a name="configure-via-hello-net-sdk"></a>Konfigurowanie za pomocą hello zestawu .NET SDK
Można skonfigurować swoją Centrum toouse uwierzytelniania na podstawie tokenu przy użyciu naszych [najnowszego klienta SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8). 

Oto przykładowy kod, pokazujący hello poprawne użycie:


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH tooYOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-toousing-certificate-based-authentication"></a>Trwa przywracanie toousing uwierzytelniania opartego na certyfikatach
Możesz przywrócić w żadnego uwierzytelniania opartego na certyfikatach toousing czasu przy użyciu dowolnego poprzedniego certyfikatu hello — metoda i przekazywanie zamiast hello tokenu właściwości. Akcja hello spowoduje zastąpienie wcześniej zapisanych poświadczeń.
