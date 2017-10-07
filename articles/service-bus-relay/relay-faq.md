---
title: "aaaAzure przekazywania — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Uzyskaj odpowiedzi toosome przekazywania Azure — często zadawane pytania."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 886d2c7f-838f-4938-bd23-466662fb1c8e
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: ab14431e27df43287940e7d12ea37e4093638d21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-faqs"></a>Przekaźnik Azure — często zadawane pytania

Ten artykuł zawiera odpowiedzi niektóre często zadawane pytania (FAQ) o [przekazywania Azure](https://azure.microsoft.com/services/service-bus/). Ogólne Azure cennik i pomocy technicznej informacji można uzyskać [często zadawane pytania dotyczące obsługi Azure](http://go.microsoft.com/fwlink/?LinkID=185083).

## <a name="general-questions"></a>Pytania ogólne
### <a name="what-is-azure-relay"></a>Co to jest usługa Azure Relay?
Witaj [usługi przekazywania Azure](relay-what-is-it.md) ułatwia hybrydowych aplikacji, pomagając bardziej bezpieczne Uwidacznianie usług, które znajdują się w korporacyjnym środowisku chmury publicznej toohello sieci. Witaj usług mogą uwidaczniać bez konieczności otwierania połączenia zaporę i bez konieczności wprowadzania niepożądanych zmian tooa sieci firmowej infrastruktury.

### <a name="what-is-a-relay-namespace"></a>Co to jest obszar nazw przekazywania?
A [przestrzeni nazw](relay-create-namespace-portal.md) jest kontener zakresu, w której można tooaddress przekazywania zasobów w aplikacji. Należy utworzyć przestrzeń nazw toouse przekazywania. Jest to jedna z pierwszym krokiem hello wprowadzenie.

### <a name="what-happened-tooservice-bus-relay-service"></a>Jakie happened tooService przekaźnik magistrali usług?
poprzednia nazwa usługi Service Bus Relay Hello nosi teraz przekaźnika usługi WCF. Można kontynuować toouse tej usługi w zwykły sposób. Funkcja połączeń hybrydowych Hello jest zaktualizowana wersja usługi, która jest ponownie przeszczepione z usług Azure BizTalk. Przekaźnik usługi WCF i połączeń hybrydowych nadal toobe obsługiwane.

## <a name="pricing"></a>Cennik
Ta sekcja odpowiedzi niektóre często zadawane pytania dotyczące hello przekazywania cennik struktury. Również widoczne [pomocy technicznej platformy Azure — często zadawane pytania](http://go.microsoft.com/fwlink/?LinkID=185083) Azure ogólne informacje o cenach. Aby uzyskać pełne informacje o cenach przekazywania, zobacz [szczegóły cennika usługi Service Bus][Pricing overview].

### <a name="how-do-you-charge-for-hybrid-connections-and-wcf-relay"></a>Jak można pobierać połączeń hybrydowych i przekazywania WCF?
Aby uzyskać pełne informacje o cenach przekazywania, zobacz hello [połączeń hybrydowych i przekaźników WCF] [ Pricing overview] tabeli na stronie Szczegóły cen usługi Service Bus hello. Ponadto ceny toohello zauważyć na tej stronie są naliczane transferów danych skojarzony za wyjście poza hello centrum danych, w którym aplikacja zostanie zainicjowana.

### <a name="how-am-i-billed-for-hybrid-connections"></a>Jak m rozliczane dla połączenia hybrydowe?
Poniżej przedstawiono trzy przykładowe scenariusze rozliczeń dla połączeń hybrydowych było możliwe:

*   Scenariusz 1.
    *   Masz jeden odbiornik, takich jak wystąpienie hello Menedżera połączeń hybrydowych zainstalowane i pracujące przez cały miesiąc hello.
    *   3 GB danych są wysyłane za pośrednictwem połączenia hello w miesiącu hello. 
    *   Poziom naładowania całkowita jest wynosi 5.
*   Scenariusz 2.
    *   Masz jeden odbiornik, takich jak wystąpienie hello Menedżera połączeń hybrydowych zainstalowane i pracujące przez cały miesiąc hello.
    *   10 GB danych są wysyłane za pośrednictwem połączenia hello w miesiącu hello.
    *   Poziom naładowania całkowita jest 7.50 $. To 5 $ hello połączenia i pierwsze 5 GB + $2.50 dla hello dodatkowe 5 GB danych.
*   Scenariusz 3:
    *   Masz dwa wystąpienia, A i B hello Menedżera połączeń hybrydowych zainstalowane i pracujące przez cały miesiąc hello.
    *   3 GB danych są wysyłane za pośrednictwem połączenia A miesiącach hello.
    *   6 GB danych są wysyłane za pośrednictwem połączenia B w miesiącu hello.
    *   Poziom naładowania całkowita jest 10.50 $. To 5 $ połączenia A + $5 dla połączenia B wysokości 0,50 USD (dla hello szóstego gigabajt połączenia B).

Należy pamiętać, że hello ceny używana w przykładach hello są używane tylko podczas okresu zapoznawczego hello połączeń hybrydowych było możliwe. Ceny są toochange podmiotu po udostępnieniu wersji ogólnodostępnej połączeń hybrydowych.

### <a name="how-are-hours-calculated-for-relay"></a>Jak są obliczane godziny przekazywania?

Przekaźnik WCF jest dostępna tylko w przestrzeniach nazw warstwy standardowa. Cennik i [przydziały połączenia](../service-bus-messaging/service-bus-quotas.md) dla przekaźniki, w przeciwnym razie nie uległy zmianie. Oznacza to, że przekaźników kontynuowania toobe naliczane na podstawie liczby hello wiadomości (nie operacje) i przekazywania godzin. Aby uzyskać więcej informacji, zobacz hello ["Hybrydowego połączenia i przekaźników WCF"](https://azure.microsoft.com/pricing/details/service-bus/) tabeli na powitania cennik strony szczegółów.

### <a name="what-if-i-have-more-than-one-listener-connected-tooa-specific-relay"></a>Co zrobić, jeśli użytkownik ma więcej niż jeden odbiornik połączonych tooa konkretnego przekaźnika?
W niektórych przypadkach pojedynczego przekazywania może mieć wiele odbiorników połączonych. Przekaźnik jest uznawane za otwarte podczas przekazywania co najmniej jeden odbiornik jest tooit połączonych. Dodawanie odbiorników tooan przekazywania Otwórz wyniki w godzinach dodatkowe przekazywania. Witaj numer przekaźnika nadawców (klientów, które wywołują lub wysłania wiadomości toorelays), które są połączone tooa przekazywania nie wpływa na powitania obliczania godziny przekazywania.

### <a name="how-is-hello-messages-meter-calculated-for-wcf-relays"></a>Jak licznik wiadomości powitania jest obliczana dla przekaźników usługi WCF
(**Dotyczy tylko tooWCF przekaźników. Wiadomość nie jest koszt połączeń hybrydowych było możliwe.** )

Ogólnie rzecz biorąc, rozliczeniowy wiadomości dla przekaźniki są obliczane przy użyciu hello sama metoda, która jest używana dla obsługiwanych przez brokera jednostek (kolejki, tematy i subskrypcje) opisanych powyżej. Istnieje jednak kilka istotnych różnic.

Wysyłanie komunikatu przekaźnik usługi Service Bus tooa jest traktowana jako "pełnej za pośrednictwem" Wyślij toohello przekazywania odbiornika, który odbiera wiadomości powitania. Nie jest traktowana jako wysyłania operacji toohello przekaźnika usługi Service Bus, następuje odbiornik przekazywania toohello dostarczania. Styl wywołania usługi "żądanie-odpowiedź" (z too64 KB w górę) względem wyników odbiornika przekazywania w dwóch komunikatów rozliczeniowy: jeden komunikat rozliczeniowy hello żądania i jeden komunikat rozliczeń dla odpowiedzi hello (przy założeniu hello odpowiedzi jest także 64 KB lub mniejszy). To jest inny niż przy użyciu toomediate kolejki, między klientem a usługą. Jeśli używasz toomediate kolejki, między klientem a usługą hello tego samego wzorca "żądanie-odpowiedź" wymaga kolejki toohello wysyłania żądania, następuje kolejki/dostawy z hello kolejki toohello usługi. To jest następuje tooanother kolejki wysyłania odpowiedzi i kolejki/dostawy z tego klienta toohello kolejki. Przy użyciu hello rozmiaru takie same wartości domyślne w całej (up too64 KB), hello udziału kolejki powoduje wzorzec 4 rozliczeniowy wiadomości. Czy opłaty będą naliczane za dwukrotnie hello liczbę wiadomości tooimplement powitalne sam wzorca osiągnąć przy użyciu przekaźnika. Oczywiście istnieją korzyści toousing kolejek tooachieve tego wzorca, takie jak trwałości i wyrównywanie obciążenia. Tych korzyści mogą uzasadniać hello dodatkowych kosztów.

Przekaźniki otwieranych przy użyciu hello **netTCPRelay** wiązania WCF Traktuj wiadomości nie jako pojedyncze wiadomości, ale jako strumień danych przepływających przez hello system. Korzystając z tego powiązania, tylko hello nadawcy, jak i odbiornika mieć wgląd w ramek hello hello poszczególne wiadomości wysłanych i odebranych. Dla przekaźniki, które używają hello **netTCPRelay** powiązanie, wszystkie dane jest traktowane jako strumień obliczania rozliczeniowy wiadomości. W takim przypadku usługi Service Bus oblicza hello łączna ilość danych wysyłane lub odbierane za pośrednictwem każdej poszczególnych przekazywania na podstawie 5 minut. Następnie do dzielenia tego łączna ilość danych 64 KB toodetermine hello numer rozliczeniowy komunikatów dla tego przekazywania podczas tego okresu.

## <a name="quotas"></a>Przydziały
| Nazwa przydziału | Zakres | Typ | Zachowanie po przekroczeniu | Wartość |
| --- | --- | --- | --- | --- |
| Współbieżne odbiorników w przekaźnik |Jednostka |Statyczny |Kolejne żądania dla dodatkowych połączeń są odrzucane i wyjątek jest odbierany przez hello wywołanie kodu. |25 |
| Obiekty nasłuchujące równoczesnych przekazywania |Systemowe |Statyczny |Kolejne żądania dla dodatkowych połączeń są odrzucane i wyjątek jest odbierany przez hello wywołanie kodu. |2,000 |
| Połączeń współbieżnych przekazywania na wszystkich przekazywania punktów końcowych w przestrzeni nazw usługi |Systemowe |Statyczny |- |5,000 |
| Punkty końcowe przekazywania na przestrzeni nazw usługi |Systemowe |Statyczny |- |10 000 |
| Rozmiar komunikatu [NetOnewayRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.netonewayrelaybinding.aspx) i [NetEventRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.neteventrelaybinding.aspx) przekazuje |Systemowe |Statyczny |Wiadomości przychodzących, które przekraczają te przydziały są odrzucane i wyjątek jest odbierany przez hello wywołanie kodu. |64 KB |
| Rozmiar komunikatu [HttpRelayTransportBindingElement](https://msdn.microsoft.com/library/microsoft.servicebus.httprelaytransportbindingelement.aspx) i [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) przekazuje |Systemowe |Statyczny |- |Nieograniczona liczba |

### <a name="does-relay-have-any-usage-quotas"></a>Przekaźnik ma wszelkie przydziały użycia?
Domyślnie dla dowolnej usługi w chmurze firmy Microsoft ustawia agregacji miesięczne przydział użycia, która jest obliczana dla wszystkich subskrypcji klienta. Rozumiemy, że w czasie potrzeb może przekroczyć tych limitów. Tak możemy zrozumienie potrzeb i odpowiednio dostosować te limity można się z obsługą klienta w dowolnym momencie. Dla usługi Service Bus hello przydziały użycie agregacji są następujące:

* 5 miliardów komunikatów
* 2 miliony godzin przekazywania

Mimo że firma Microsoft zarezerwować hello prawo toodisable konta, które przekracza jego miesięcznego wykorzystania przydziały, firma Microsoft udostępnia powiadomienie e-mail, a wykonujemy wielu prób toocontact powitania klienta przed podjęciem działania. Klienci, którzy przekracza te przydziały nadal są odpowiedzialne za nadmiarowe opłat.

### <a name="naming-restrictions"></a>Ograniczenia nazewnictwa
Nazwa przestrzeni nazw przekazywania musi być od 6 do 50 znaków.

## <a name="subscription-and-namespace-management"></a>Zarządzanie subskrypcją i przestrzeni nazw
### <a name="how-do-i-migrate-a-namespace-tooanother-azure-subscription"></a>Jak przeprowadzić migrację przestrzeni nazw tooanother subskrypcji platformy Azure?

toomove przestrzeni nazw z jedną subskrypcją tooanother subskrypcji platformy Azure, możesz albo użyj hello [portalu Azure](https://portal.azure.com) lub użyć poleceń programu PowerShell. toomove subskrypcji tooanother przestrzeni nazw hello przestrzeni nazw musi już być aktywne. Użytkownik Hello hello polecenia musi być użytkownika Administrator dla obu hello subskrypcji źródłowych i docelowych.

#### <a name="azure-portal"></a>Azure Portal

Witaj toouse przestrzenie nazw przekaźnika usługi Azure toomigrate portalu Azure, z jedną subskrypcją tooanother subskrypcji, zobacz [przenoszenia zasobów tooa nową grupę zasobów lub subskrypcji](../azure-resource-manager/resource-group-move-resources.md#use-portal). 

#### <a name="powershell"></a>PowerShell

toomove PowerShell toouse przestrzeni nazw z jedną subskrypcją platformy Azure tooanother subskrypcji, użyj powitania po sekwencja poleceń. tooexecute tej operacji, hello przestrzeni nazw musi już być aktywne, a użytkownik hello uruchamianie poleceń programu PowerShell hello musi być użytkownika administratora dla subskrypcji źródłowej i docelowej zarówno hello.

```powershell
# Create a new resource group in hello target subscription.
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move hello namespace from hello source subscription toohello target subscription.
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="troubleshooting"></a>Rozwiązywanie problemów
### <a name="what-are-some-of-hello-exceptions-generated-by-azure-relay-apis-and-suggested-actions-you-can-take"></a>Jakie są hello wyjątków generowanych przez interfejsów API przekaźnika usługi Azure i sugerowanych akcji, które można wykonać?
Opis wyjątków typowe i wyświetlić sugerowane akcje można wykonać, zobacz [przekazywania wyjątki][Relay exceptions].

### <a name="what-is-a-shared-access-signature-and-which-languages-can-i-use-toogenerate-a-signature"></a>Co to jest sygnatury dostępu współdzielonego i języki, których można użyć toogenerate sygnaturę?
Udostępniony sygnatur dostępu (SAS) są mechanizmu uwierzytelniania na podstawie bezpiecznego wartości skrótu SHA-256 lub identyfikatorów URI. Aby uzyskać informacje o toogenerate własnych podpisów w węźle, PHP, Java, C i C#, zobacz temat [uwierzytelniania usługi Service Bus za pomocą sygnatur dostępu współdzielonego][Shared Access Signatures].

### <a name="is-it-possible-toowhitelist-relay-endpoints"></a>Jest to punkty końcowe przekazywania możliwe toowhitelist?
Tak. powitania klienta przekazywania umożliwia nawiązanie połączenia usługi Azure przekazywania toohello przy użyciu w pełni kwalifikowanych nazw domen. Klientów można dodać wpis dla `*.servicebus.windows.net` na zaporach, które obsługują listę dozwolonych podobnej DNS.

## <a name="next-steps"></a>Następne kroki
* [Tworzenie przestrzeni nazw](relay-create-namespace-portal.md)
* [Wprowadzenie do programu .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Wprowadzenie do programu Node](relay-hybrid-connections-node-get-started.md)

[Pricing overview]: https://azure.microsoft.com/pricing/details/service-bus/
[Relay exceptions]: relay-exceptions.md
[Shared access signatures]: ../service-bus-messaging/service-bus-sas.md