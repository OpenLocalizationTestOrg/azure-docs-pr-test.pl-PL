---
title: "aaaPolicies w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate, edytować i konfigurowania zasad w usłudze API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 537e5caf-708b-430e-a83f-72b70af28aa9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 9ab0f884a655004cb10c05085034df1795f512e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="policies-in-azure-api-management"></a>Zasady w usłudze Azure API Management
W usłudze Azure API Management zasady są zaawansowanych możliwości hello system, który umożliwia zachowanie hello toochange hello interfejsu API za pomocą konfiguracji hello wydawcy. Zasady są zbiór instrukcji, które są wykonywane sekwencyjnie na powitania żądania lub odpowiedzi interfejsu API. Popularne instrukcje obejmują Konwersja formatu XML tooJSON i Wywołaj tempa ograniczania toorestrict hello ilość przychodzących od dewelopera. Wiele zasad są dostępne fabrycznej hello.

Zobacz hello [informacje o zasadach] [ Policy Reference] pełną listę deklaracji zasad i ich ustawienia.

Zasady są stosowane wewnątrz hello bramy, która znajduje się pomiędzy powitania klienta interfejsu API i hello zarządzanego interfejsu API. Hello Brama odbiera wszystkie żądania i zwykle przekazuje je niezmieniony toohello podstawowy interfejs API. Jednak zasady można zastosować zmian tooboth hello przychodzącego żądania i odpowiedzi wychodzących.

Wyrażenie zasad może służyć jako wartości atrybutu lub tekst w żadnym z zasad interfejsu API zarządzania hello, chyba że zasady hello Określa, w przeciwnym razie wartość. Niektóre zasady, takie jak hello [sterowania przepływem] [ Control flow] i [zmiennej zestaw] [ Set variable] zasady są oparte na wyrażeniach zasad. Aby uzyskać więcej informacji, zobacz [zaawansowane zasady] [ Advanced policies] i [wyrażenie zasad][Policy expressions].

## <a name="scopes"></a>Jak tooconfigure zasad
Zasady można skonfigurować globalnie lub w zakresie hello [produktu][Product], [interfejsu API] [ API] lub [operacji] [Operation]. tooconfigure zasadę, przejdź toohello edytora zasad w portalu wydawcy hello.

![Menu zasad][policies-menu]

Edytor zasad Hello składa się z trzech głównych sekcji: hello zasad zakresu (z góry), hello definicji zasad gdzie edycji zasad (lewych) i instrukcje hello listy (po prawej):

![Edytor zasad][policies-editor]

toobegin Konfigurowanie zasad, musisz najpierw wybrać zakres hello na powitania, które mają dotyczyć zasady. Zrzucie ekranu hello poniżej hello **Starter** produkt jest zaznaczony. Należy pamiętać, że w tym hello kwadratowy dalej toohello zasad nazwa symbolu wskazuje, że zasady jest już stosowane na tym poziomie.

![Zakres][policies-scope]

Ponieważ zasady zostały już zastosowane, konfiguracja hello jest wyświetlana w widoku definicji hello.

![Konfigurowanie][policies-configure]

zasady Hello są wyświetlane tylko do odczytu na początku. W kolejności tooedit definicji powitania kliknij hello **Konfiguruj zasady** akcji.

![Edytuj][policies-edit]

Definicja zasad Hello jest proste dokument XML, który opisuje sekwencji instrukcji dla ruchu przychodzącego i wychodzącego. Witaj XML można edytować bezpośrednio w oknie definicji hello. Lista instrukcje są podane toohello prawo i bieżącego zakresu toohello odpowiednie instrukcje są włączone i wyróżniony; jak dowodzą hello **Limit szybkości wywołać** instrukcji na powitania zrzucie ekranu pokazano powyżej.

Kliknięcie instrukcji włączone spowoduje dodanie hello odpowiednie XML w lokalizacji hello hello kursora w hello definicji widoku. 

> [!NOTE]
> Hello zasad, które mają tooadd nie jest włączona, upewnij się, że jesteś w hello poprawny zakres dla tej zasady. Każda instrukcja zasad jest przeznaczony do użytku w określonych zakresach i sekcje zasad. sekcje zasad hello tooreview i zakresy dla zasady, sprawdź hello **użycia** sekcji dla tej zasady w hello [informacje o zasadach][Policy Reference].
> 
> 

Pełna lista deklaracji zasad i ich ustawienia są dostępne w hello [informacje o zasadach][Policy Reference].

Na przykład tooadd nowe toorestrict instrukcji przychodzących żądań toospecified adresów IP, umieść kursor hello wewnątrz zawartości hello hello `inbound` XML hello element i kliknij przycisk **wywołującego Ogranicz adresów IP** instrukcji.

![Zasady ograniczeń][policies-restrict]

Spowoduje to dodanie toohello fragment kodu XML `inbound` element, który zawiera wskazówki dotyczące sposobu tooconfigure hello instrukcji.

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

toolimit ruchu przychodzącego żądania i zaakceptować tylko te z adresu IP 1.2.3.4 zmodyfikować hello XML w następujący sposób:

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Zapisz][policies-save]

Po zakończeniu konfigurowania instrukcje hello hello zasad, kliknij przycisk **zapisać** i hello zmiany zostaną propagowany toohello interfejsu API zarządzania bramy natychmiast.

## <a name="sections"></a>Opis zasad konfiguracji
Zasady zostaną serię instrukcji, które są wykonywane w kolejności na żądania i odpowiedzi. Konfiguracja Hello jest odpowiednio podzielone na `inbound`, `backend`, `outbound`, i `on-error` sekcjach przedstawiono, jak pokazano w powitania po konfiguracji.

```xml
<policies>
  <inbound>
    <!-- statements toobe applied toohello request go here -->
  </inbound>
  <backend>
    <!-- statements toobe applied before hello request is forwarded too
         hello backend service go here -->
  </backend>
  <outbound>
    <!-- statements toobe applied toohello response go here -->
  </outbound>
  <on-error>
    <!-- statements toobe applied if there is an error condition go here -->
  </on-error>
</policies> 
```

Jeśli występuje błąd podczas przetwarzania żądania hello, wszystkie pozostałe kroki w hello `inbound`, `backend`, lub `outbound` sekcje są pomijane i wykonywania w tę łódź toohello instrukcje w hello `on-error` sekcji. Zaznaczając deklaracji zasad hello `on-error` sekcji można przejrzeć hello błędu przy użyciu hello `context.LastError` właściwość, sprawdzić i dostosować przy użyciu hello odpowiedzi na błąd hello `set-body` zasad i skonfigurować, co się stanie w przypadku wystąpienia błędu. Brak kody błędów dla wbudowanych kroków i błędy, które mogą wystąpić podczas przetwarzania hello deklaracji zasad. Aby uzyskać więcej informacji, zobacz [obsługi błędów w zasad interfejsu API zarządzania](https://msdn.microsoft.com/library/azure/mt629506.aspx).

Ponieważ zasad można określić na różnych poziomach (globalne, produktu, interfejsu api i operacji) hello konfiguracji umożliwia dla Ciebie toospecify hello kolejność, w którym instrukcje definicji zasad hello wykonywane za pomocą zasad nadrzędnej toohello względem. 

Zakresy zasad są oceniane w następującej kolejności hello.

1. Globalne
2. Zakres produktu
3. Zakres interfejsu API
4. Operacja zakresu

Witaj instrukcje w nich są oceniane według położenia toohello hello `base` elementu, jeśli jest obecny. Globalne zasady ma żadnych zasad nadrzędny i przy użyciu hello `<base>` element w nim nie ma wpływu.

Na przykład jeśli masz zasady na poziomie globalnym hello i zasady skonfigurowane dla interfejsu API, następnie każdorazowe użycie tego konkretnego interfejsu API obie zasady zostaną zastosowane. Zarządzanie interfejsami API umożliwia deterministyczne kolejność deklaracji zasad połączonych za pośrednictwem hello base element. 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

W hello przykład definicji zasad powyżej, hello `cross-domain` instrukcji jest wykonywany przed wszystkie wyższej zasady, które z kolei, następować hello `find-and-replace` zasad. 

zasady hello toosee w bieżącym zakresie hello w edytorze zasad hello, kliknij polecenie **ponownie Oblicz skutecznych zasad dla wybranego zakresu**.

## <a name="next-steps"></a>Następne kroki
Zapoznaj się z następującego wideo na wyrażeniach zasad.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Policy Reference]: api-management-policy-reference.md
[Product]: api-management-howto-add-products.md
[API]: api-management-howto-add-products.md#add-apis 
[Operation]: api-management-howto-add-operations.md

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx

[policies-menu]: ./media/api-management-howto-policies/api-management-policies-menu.png
[policies-editor]: ./media/api-management-howto-policies/api-management-policies-editor.png
[policies-scope]: ./media/api-management-howto-policies/api-management-policies-scope.png
[policies-configure]: ./media/api-management-howto-policies/api-management-policies-configure.png
[policies-edit]: ./media/api-management-howto-policies/api-management-policies-edit.png
[policies-restrict]: ./media/api-management-howto-policies/api-management-policies-restrict.png
[policies-save]: ./media/api-management-howto-policies/api-management-policies-save.png
