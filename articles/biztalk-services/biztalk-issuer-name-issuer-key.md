---
title: "aaaIssuer nazwy i klucza wystawcy usługi BizTalk Services | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooretrieve nazwy wystawcy i klucza wystawcy dla usługi Service Bus lub kontroli dostępu (ACS) w usługach BizTalk. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 067fe356-d1aa-420f-b2f2-1a418686470a
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: cc84c2820724ae3e7fc7c40ddbcd83a169add911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a>BizTalk Services: Issuer Name and Issuer Key (Usługa BizTalk Services: nazwa i klucz wydawcy)

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Azure usługi BizTalk Services używa hello Nazwa wystawcy magistrali usługi i klucza wystawcy i hello Nazwa wystawcy kontroli dostępu i klucza wystawcy. W szczególności:

| Zadanie | Która nazwa wystawcy i klucza wystawcy |
| --- | --- |
| Wdrażanie aplikacji w programie Visual Studio |Nazwa wystawcy kontroli dostępu i klucza wystawcy |
| Konfigurowanie hello Azure Portal usługi BizTalk |Nazwa wystawcy kontroli dostępu i klucza wystawcy |
| Tworzenie LOB przekaźników z hello BizTalk karty usług w programie Visual Studio |Nazwa wystawcy magistrali usługi i klucza wystawcy |

W tym temacie wymieniono hello kroki tooretrieve hello Nazwa wystawcy i klucza wystawcy. 

## <a name="access-control-issuer-name-and-issuer-key"></a>Nazwa wystawcy kontroli dostępu i klucza wystawcy
Hello Nazwa wystawcy kontroli dostępu i klucz wystawcy, są używane przez następujące hello:

* Aplikacja usługi BizTalk Azure utworzone w programie Visual Studio: toosuccessfully wdrażania aplikacji usługi BizTalk w Visual Studio tooAzure, należy wprowadzić hello Nazwa wystawcy kontroli dostępu i klucza wystawcy. 
* Portal usługi BizTalk Azure Hello: podczas tworzenia usługi BizTalk i otwórz hello Portal usługi BizTalk, nazwę wystawcy kontroli dostępu i klucza wystawcy, są automatycznie rejestrowane wdrożeń z hello takie same wartości kontroli dostępu.

### <a name="get-hello-access-control-issuer-name-and-issuer-key"></a>Pobierz hello Nazwa wystawcy kontroli dostępu i klucza wystawcy

Nazwa wystawcy i klucza wystawcy wartości hello ACS toouse uwierzytelniania i get, hello ogólne kroki obejmują:

1. Zainstaluj hello [poleceń cmdlet programu Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
2. Dodaj konto platformy Azure:`Add-AzureAccount`
3. Zwraca nazwę Twojej subskrypcji:`get-azuresubscription`
4. Wybierz subskrypcję:`select-azuresubscription <name of your subscription>` 
5. Tworzenie nowej przestrzeni nazw:`new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`

    Przykład:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`
      
5. Po utworzeniu przestrzeni nazw hello nowych usług ACS, (co może potrwać kilka minut), wartości nazwy wystawcy i klucza wystawcy hello są wymienione w ciągu połączenia hello: 

    ```
    Name                  : biztalksbnamespace
    Region                : South Central US
    DefaultKey            : abcdefghijklmnopqrstuvwxyz
    Status                : Active
    CreatedAt             : 10/18/2016 9:36:30 PM
    AcsManagementEndpoint : https://biztalksbnamespace-sb.accesscontrol.windows.net/
    ServiceBusEndpoint    : https://biztalksbnamespace.servicebus.windows.net/
    ConnectionString      : Endpoint=sb://biztalksbnamespace.servicebus.windows.net/;SharedSecretIssuer=owner;SharedSecretValue=abcdefghijklmnopqrstuvwxyz
    NamespaceType         : Messaging
    ```

toosummarize:  
Nazwa wystawcy = SharedSecretIssuer  
Klucz wystawcy = SharedSecretKey

Więcej informacji na temat hello [AzureSBNamespace nowy](https://msdn.microsoft.com/library/dn495165.aspx) polecenia cmdlet. 

## <a name="service-bus-issuer-name-and-issuer-key"></a>Nazwa wystawcy magistrali usługi i klucza wystawcy
Nazwa wystawcy magistrali usługi i klucza wystawcy, są używane przez usługi karty BizTalk. W projekcie usługi BizTalk Services w programie Visual Studio używasz hello usług karty BizTalk tooconnect tooan lokalnego — biznesowych (LOB) systemu. tooconnect, Utwórz hello LOB przekazywania i wprowadź swoje dane systemu LOB. W ten sposób można także wprowadzić hello Nazwa wystawcy magistrali usługi i klucza wystawcy.

### <a name="tooretrieve-hello-service-bus-issuer-name-and-issuer-key"></a>Witaj tooretrieve Nazwa wystawcy magistrali usługi i klucza wystawcy
1. Zaloguj się toohello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Wybierz w okienku nawigacji po lewej stronie powitania **usługi Service Bus**.
3. Wybierz obszar nazw. Na pasku zadań hello, wybierz **informacje o połączeniu**. Spowoduje to wyświetlenie hello **domyślne wystawcy** (Nazwa wystawcy) i **domyślny klucz** (klucza wystawcy). Można skopiować wartości.  

toosummarize:  
Nazwa wystawcy = wystawcy domyślne  
Klucz wystawcy domyślny klucz =

## <a name="next"></a>Następne kroki
Dodatkowe tematy usługi BizTalk Azure:

* [Instalowanie hello Azure zestawu SDK usługi BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [Samouczki: Usługi Azure BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [Jak mogę uruchomić przy użyciu hello Azure zestawu SDK usługi BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Usługi Azure BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a>Zobacz też
* [Porady: Użyj usługi Zarządzanie ACS tooConfigure tożsamości usługi](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [Usługi BizTalk Services: Developer, podstawowa, standardowa i Premium Edition wykresu](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [Usługi BizTalk Services: Klasyczny portal Azure przy użyciu inicjowania obsługi](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [BizTalk Services: Provisioning Status Chart (Usługa BizTalk Services: aprowizowanie wykresu stanu)](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [BizTalk Services: Dashboard, Monitor and Scale tabs (Usługa BizTalk Services: karty Pulpit nawigacyjny, Monitor i Skalowanie)](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [BizTalk Services: Backup and Restore (Usługa BizTalk Services: tworzenie kopii zapasowej i przywracanie)](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [BizTalk Services: Throttling (Usługa BizTalk Services: ograniczanie przepływności)](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

