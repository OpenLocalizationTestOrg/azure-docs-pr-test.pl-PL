---
title: "aaaAzure usługi Service Bus — często zadawane pytania (FAQ) | Dokumentacja firmy Microsoft"
description: "Odpowiedzi na niektóre często zadawane pytania dotyczące usługi Azure Service Bus."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: cc75786d-3448-4f79-9fec-eef56c0027ba
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 71fe9eac46647a3e4026dbcaf2196984dd4b6a44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-faq"></a>Service Bus — często zadawane pytania
Ten artykuł zawiera odpowiedzi na niektóre często zadawane pytania dotyczące usługi Microsoft Azure Service Bus. Możesz również odwiedzić hello [często zadawane pytania dotyczące obsługi Azure](http://go.microsoft.com/fwlink/?LinkID=185083) ogólne informacje Azure cennik i pomocy technicznej.

## <a name="general-questions-about-azure-service-bus"></a>Ogólne pytania dotyczące usługi Azure Service Bus
### <a name="what-is-azure-service-bus"></a>Co to jest Azure Service Bus?
[Usługa Azure Service Bus](service-bus-messaging-overview.md) asynchroniczne komunikatów platforma chmury, która umożliwia toosend danych między systemami rozdzielonymi. Firma Microsoft oferuje tej funkcji jako usługa, co oznacza, że nie ma potrzeby toohost którykolwiek element sprzętowy w kolejności toouse go.

### <a name="what-is-a-service-bus-namespace"></a>Co to jest obszar nazw usługi Service Bus?
A [przestrzeni nazw](service-bus-create-namespace-portal.md) zapewnia kontener zakresu na potrzeby adresowania zasobów usługi Service Bus w aplikacji. Utworzenie jest toouse niezbędne usługi Service Bus i są hello pierwszym krokiem wprowadzenie.

### <a name="what-is-an-azure-service-bus-queue"></a>Co to jest kolejki usługi Azure Service Bus?
A [kolejki usługi Service Bus](service-bus-queues-topics-subscriptions.md) to jednostka, w której są przechowywane wiadomości. Kolejki są szczególnie przydatne, jeśli masz wiele aplikacji lub wielu części aplikacji rozproszonej, które wymagają toocommunicate ze sobą. kolejki Hello jest podobne Centrum dystrybucji tooa w wielu produktów (wiadomości) są odebrane i następnie wysyłane z tej lokalizacji.

### <a name="what-are-azure-service-bus-topics-and-subscriptions"></a>Co to są tematy usługi Azure Service Bus i subskrypcje?
Tematu może zostać zwizualizowany jako kolejka i korzystając z wieloma subskrypcjami, staje się bardziej rozbudowane modelu obsługi komunikatów; zasadniczo narzędzie komunikacji jeden do wielu. Ten model publikowania/subskrypcji (lub *pub/sub*) umożliwia aplikacji, która wysyła komunikat tooa temat o wielu toohave subskrypcji ten komunikat odebrany przez wiele aplikacji.

### <a name="what-is-a-partitioned-entity"></a>Co to jest partycjonowane jednostki?
Konwencjonalne kolejka lub temat są obsługiwane przez brokera pojedynczej wiadomości i przechowywane w jeden Magazyn obsługi komunikatów. A [partycjonowanej kolejka lub temat](service-bus-partitioning.md) jest obsługiwany przez wiele brokerzy wiadomości i przechowywane w wiele magazynów obsługi komunikatów. Oznacza to, że hello ogólną przepustowość partycjonowanej kolejka lub temat nie jest już ograniczone przez wydajności hello brokera komunikatów pojedynczego lub magazynie obsługi komunikatów. Ponadto tymczasowego awaria magazynie obsługi komunikatów nie renderować partycjonowanej kolejka lub temat niedostępny.

Należy pamiętać, że porządkowania braku pewności, korzystając z partycjonowania jednostek. W przypadku hello, czy partycja jest niedostępny można nadal wysyłania i odbierania wiadomości z hello innych partycji.

## <a name="best-practices"></a>Najlepsze praktyki
### <a name="what-are-some-azure-service-bus-best-practices"></a>Jakie są najlepsze rozwiązania Azure Service Bus?
* [Najlepsze rozwiązania dotyczące poprawy wydajności przy użyciu usługi Service Bus] [ Best practices for performance improvements using Service Bus] — w tym artykule opisano, jak toooptimize wydajności podczas wymiany wiadomości.

### <a name="what-should-i-know-before-creating-entities"></a>Co należy wiedzieć przed rozpoczęciem tworzenia jednostek?
następujące właściwości kolejki i tematu Hello są niezmienne. Należy to brać pod uwagę podczas obsługi administracyjnej jednostki zgodnie z tym nie można modyfikować, bez tworzenia nowego obiektu zastąpienia.

* Rozmiar
* Partycjonowanie
* Sesje
* Wykrywanie duplikatów
* Jednostki ekspresowe

## <a name="pricing"></a>Cennik
Ta sekcja zawiera odpowiedzi na niektóre często zadawane pytania dotyczące strukturę cen usługi Service Bus hello.

Witaj [usługi Service Bus cennik i rozliczenia](service-bus-pricing-billing.md) wyjaśniono hello metod rozliczeń w usłudze Service Bus oraz informacje o cenach opcje usługi Service Bus, zobacz [szczegóły cennika usługi Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).

Możesz również odwiedzić hello [pomocy technicznej platformy Azure — często zadawane pytania](http://go.microsoft.com/fwlink/?LinkID=185083) Azure ogólne informacje o cenach. 

### <a name="how-do-you-charge-for-service-bus"></a>Jak można pobierać dla usługi Service Bus?
Aby uzyskać pełne informacje na temat cen usługi Service Bus, zobacz [szczegóły cennika usługi Service Bus][Pricing overview]. Ponadto ceny toohello zauważyć są naliczane transferów danych skojarzony za wyjście poza hello centrum danych, w którym aplikacja zostanie zainicjowana.

### <a name="what-usage-of-service-bus-is-subject-toodata-transfer-what-is-not"></a>Jakie użycia usługi Service Bus jest podmiotu toodata transferu? Co to jest?
Przekazanie danych w danym regionie Azure znajduje się bez żadnych opłat, jak również wszelkich transfer danych przychodzących. Transfer danych poza region jest podmiotu tooegress obciążenia, które można znaleźć [tutaj](https://azure.microsoft.com/pricing/details/bandwidth/).

### <a name="does-service-bus-charge-for-storage"></a>Usługa Service Bus obciążenia magazynu?
Nie, magistrali usług nie nalicza dla magazynu. Istnieje jednak przydziału ograniczającej hello maksymalną ilość danych, które mogą być utrwalanych w ciągu kolejki/tematu. Zobacz często Zadawanych hello.

## <a name="quotas"></a>Przydziały

Dla listy ograniczeń usługi Service Bus i przydziały hello [Omówienie zasobów usługi Service Bus][Quotas overview].

### <a name="does-service-bus-have-any-usage-quotas"></a>Usługa Service Bus ma wszelkie przydziały użycia?
Domyślnie wszystkie chmury usługi Microsoft ustawia agregacji miesięczne przydział użycia, która jest obliczana dla wszystkich subskrypcji klienta. Ponieważ rozumiemy, że może być konieczne więcej niż te limity, skontaktuj się z działem w dowolnym momencie, aby firma Microsoft jest zrozumienie potrzeb i odpowiednio dostosować te limity. Dla usługi Service Bus przydział użycia agregacji hello jest 5 mld wiadomości miesięcznie.

Gdy firma Microsoft zarezerwować hello prawo toodisable konta klienta, która przekroczyła przydziały jego użycia w danym miesiącu, firma Microsoft będzie udostępniają powiadomienia e-mail i wiele prób toocontact klienta przed podjęciem działania. Nadal będzie odpowiedzialny za opłat, które przekraczają przydziały hello klientów przekraczającej przydziałów.

Podobnie jak w przypadku innych usług Azure Service Bus wymusza zestaw określonych przydziały tooensure istnieje odpowiedni Obciążenie zasobów. Więcej informacji na temat te przydziały można znaleźć w hello [Omówienie zasobów usługi Service Bus][Quotas overview].

## <a name="troubleshooting"></a>Rozwiązywanie problemów
### <a name="what-are-some-of-hello-exceptions-generated-by-azure-service-bus-apis-and-their-suggested-actions"></a>Jakie są hello wyjątków generowanych przez interfejsów API usługi Azure Service Bus i ich sugerowane rozwiązania?
Aby uzyskać listę możliwych wyjątków usługi Service Bus, zobacz [omówienie wyjątki][Exceptions overview].

### <a name="what-is-a-shared-access-signature-and-which-languages-support-generating-a-signature"></a>Co to jest sygnaturę dostępu współdzielonego i języki, które obsługuje generowania podpisu?
Udostępniony sygnatur dostępu są oparte na SHA-256 bezpiecznego skrótów lub identyfikatorów URI mechanizmu uwierzytelniania. Aby uzyskać informacje na temat toogenerate własnych podpisów w węźle, PHP, Java i C\#, zobacz hello [sygnatury dostępu współdzielonego] [ Shared Access Signatures] artykułu.

## <a name="subscription-and-namespace-management"></a>Zarządzanie subskrypcją i przestrzeni nazw
### <a name="how-do-i-migrate-a-namespace-tooanother-azure-subscription"></a>Jak przeprowadzić migrację przestrzeni nazw tooanother subskrypcji platformy Azure?

Przestrzeń nazw można przenosić z jednego tooanother subskrypcji platformy Azure, przy użyciu albo hello [portalu Azure](https://portal.azure.com) lub poleceń programu PowerShell. W kolejności tooexecute hello operacji hello przestrzeni nazw musi być aktywne. użytkownika Hello wykonywania poleceń hello musi być administratorem na obu źródła hello i docelowych subskrypcji.

#### <a name="portal"></a>Portal

Witaj toouse subskrypcji tooanother przestrzeni nazw usługi Service Bus toomigrate portalu Azure, postępuj zgodnie ze wskazówkami hello [tutaj](../azure-resource-manager/resource-group-move-resources.md#use-portal). 

#### <a name="powershell"></a>PowerShell

Witaj następująca sekwencja poleceń programu PowerShell przenosi przestrzeni nazw z jednego tooanother subskrypcji platformy Azure. tooexecute tej operacji, hello przestrzeni nazw musi być już aktywne i hello użytkownik uruchamiający poleceń programu PowerShell hello, musisz być administratorem na obu hello subskrypcji źródłowej i docelowej.

```powershell
# Create a new resource group in target subscription
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move namespace from source subscription tootarget subscription
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat usługi Service Bus, zobacz następujące tematy hello.

* [Introducing Azure Service Bus w warstwie Premium (wpis w blogu)](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [Introducing Azure Service Bus w warstwie Premium (Channel9)](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [Omówienie usługi Service Bus](service-bus-messaging-overview.md)
* [Omówienie architektury usługi Azure Service Bus](service-bus-fundamentals-hybrid-solutions.md)
* [Wprowadzenie do kolejek usługi Service Bus](service-bus-dotnet-get-started-with-queues.md)

[Best practices for performance improvements using Service Bus]: service-bus-performance-improvements.md
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Pricing overview]: https://azure.microsoft.com/pricing/details/service-bus/
[Quotas overview]: service-bus-quotas.md
[Exceptions overview]: service-bus-messaging-exceptions.md
[Shared Access Signatures]: service-bus-sas.md
