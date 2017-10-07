---
title: "aaaProtect interfejs API usługi Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooprotect interfejs API przydziały i ograniczenia przepustowości (limitów szybkości) zasady."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 450dc368-d005-401d-ae64-3e1a2229b12f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3113fd277d434da0c051b8b90fd629a102bf4867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a>Ochrona interfejsu API za pomocą ograniczania liczby wywołań przy użyciu usługi Azure API Management
Ten przewodnik przedstawia, jak łatwo jest tooadd ochronę interfejs API zaplecza przez skonfigurowanie zasad limitu i przydziału szybkość z usługą Azure API Management.

W tym samouczku utworzysz produkt "Bezpłatnej wersji próbnej" interfejsu API, który umożliwia deweloperom stosowanie toomake rozmowy too10 na minutę oraz tooa maksymalnie 200 wywołań na tydzień tooyour API przy użyciu hello [częstotliwość wywołań Limit subskrypcji](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) i [ Ustawianie użycie przydziału dla subskrypcji](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) zasad. Następnie zostanie publikowanie hello interfejsu API i testowania zasad limitu szybkości hello.

Bardziej zaawansowanych scenariuszy przy użyciu hello ograniczania [szybkość limit przez klucz](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) i [limitu przydziału przez klucz](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) zasad, zobacz [Zaawansowane żądanie ograniczania z usługą Azure API Management](api-management-sample-flexible-throttling.md).

## <a name="create-product"></a>toocreate produktu
W tym kroku utworzysz produkt Bezpłatna wersja próbna, który nie wymaga zatwierdzania subskrypcji.

> [!NOTE]
> Jeśli już korzystasz z produktem skonfigurowane i chcesz toouse go w tym samouczku, można przejść dalej zbyt[Konfiguruj wywołać szybkość zasady, a limit przydziału] [ Configure call rate limit and quota policies] i postępuj zgodnie z samouczkiem hello stamtąd pomocą produktu zamiast hello bezpłatnej wersji próbnej produktu.
> 
> 

tooget pracę, kliknij przycisk **portal wydawcy** w hello portalu Azure usługi Zarządzanie interfejsami API.

![Portal wydawcy][api-management-management-console]

> Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [Zarządzanie pierwszy interfejs API usługi Azure API Management] [ Manage your first API in Azure API Management] samouczka.
> 
> 

Kliknij przycisk **produktów** w hello **zarządzanie interfejsami API** menu na powitania po lewej stronie toodisplay hello **produktów** strony.

![Dodawanie produktu][api-management-add-product]

Kliknij przycisk **produktu Dodaj** toodisplay hello **Dodaj nowy produkt** okno dialogowe.

![Dodawanie nowego produktu][api-management-new-product-window]

W hello **tytuł** wpisz **bezpłatnej wersji próbnej**.

W hello **opis** okno, hello typu następującego tekstu: **subskrybenci będą mogli toorun 10 wywołań/minutę w górę tooa maksymalnie 200 wywołania na tydzień po upływie którego dostęp jest zabroniony.**

Produkty w usłudze API Management mogą być chronione lub otwarte. Produkty chronione muszą być subskrybowanego toobefore, które mogą być używane. Produkty otwarte mogą być używane bez subskrypcji. Upewnij się, że **wymagają subskrypcji** jest wybrany toocreate chronionych produkt, który wymaga subskrypcji. To jest ustawienie domyślne hello.

Jeśli chcesz tooreview administratora i zaakceptuj lub Odrzuć subskrypcji prób toothis produktu, wybierz **wymagają zatwierdzenia subskrypcji**. Jeśli nie zaznaczono pola wyboru hello, prób subskrypcji zostaną automatycznie zatwierdzone. W tym przykładzie subskrypcje są automatycznie zatwierdzane, więc nie zaznaczaj pola hello.

Deweloper tooallow kont toosubscribe wielokrotnie toohello nowego produktu wybierz hello **zezwalać na wiele równoczesnych subskrypcji** pole wyboru. Ten samouczek nie wykorzystuje wielu jednoczesnych subskrypcji, więc pozostaw to pole niezaznaczone.

Po wprowadzeniu wszystkich wartości kliknij **zapisać** toocreate hello produktu.

![Dodany produkt][api-management-product-added]

Domyślnie nowe produkty są widoczne toousers w hello **Administratorzy** grupy. Zamierzamy tooadd hello **deweloperzy** grupy. Kliknij przycisk **bezpłatnej wersji próbnej**, a następnie kliknij przycisk hello **widoczność** kartę.

> W usłudze API Management grupy są używane toomanage widoczność hello toodevelopers produktów. Produkty Udziel toogroups widoczność i deweloperzy mogą wyświetlać i subskrybować toohello produktów, które są widoczne toohello grup, w których one należą. Aby uzyskać więcej informacji, zobacz [jak toocreate i użycie grup w usłudze Azure API Management][How toocreate and use groups in Azure API Management].
> 
> 

![Dodawanie grupy deweloperów][api-management-add-developers-group]

Wybierz hello **deweloperzy** pole wyboru, a następnie kliknij przycisk **zapisać**.

## <a name="add-api"></a>produktu toohello tooadd interfejsu API
W tym kroku samouczka hello dodamy hello Echo API toohello nowego bezpłatnej wersji próbnej produktu.

> Każde wystąpienie usługi API Management jest wstępnie skonfigurowany z użyciem interfejsu API Echo, które można tooexperiment używanych z i więcej informacji na temat interfejsu API zarządzania. Aby uzyskać więcej informacji, zobacz [Zarządzanie pierwszym interfejsem API w usłudze Azure API Management][Manage your first API in Azure API Management].
> 
> 

Kliknij przycisk **produktów** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij **bezpłatnej wersji próbnej** tooconfigure hello produktu.

![Konfigurowanie produktu][api-management-configure-product]

Kliknij przycisk **tooproduct dodać interfejsu API**.

![Dodaj tooproduct interfejsu API][api-management-add-api]

Wybierz interfejs **Echo API**, a następnie kliknij przycisk **Zapisz**.

![Dodawanie interfejsu Echo API][api-management-add-echo-api]

## <a name="policies"></a>tooconfigure wywołać szybkość zasady, a limit przydziału
Limity szybkości i przydziały są skonfigurowane w edytorze zasad hello. Witaj dwie zasady dodamy w tym samouczku są hello [częstotliwość wywołań Limit subskrypcji](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) i [przydział użycia zestawu na subskrypcję](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) zasad. Te zasady muszą być stosowane w zakresie produktu hello.

Kliknij przycisk **zasady** w obszarze hello **zarządzanie interfejsami API** menu po lewej stronie powitania. W hello **produktu** kliknij **bezpłatnej wersji próbnej**.

![Zasady produktu][api-management-product-policy]

Kliknij przycisk **Dodaj zasady** tooimport hello szablonu zasad i rozpocząć tworzenie hello szybkość zasad limitu i przydziału.

![Dodawanie zasad][api-management-add-policy]

Zasady, a limit przydziału szybkość są zasady ruchu przychodzącego, tak pozycji hello kursora w elemencie przychodzących hello.

![Edytor zasad][api-management-policy-editor-inbound]

Przewiń listę hello zasad i Znajdź hello **częstotliwość wywołań Limit subskrypcji** wpis zasad.

![Instrukcje zasad][api-management-limit-policies]

Po hello kursor znajduje się w hello **przychodzących** elementu zasad, kliknij strzałkę hello obok **częstotliwość wywołań Limit subskrypcji** tooinsert jego szablonu zasad.

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

Jak widać w hello fragment, zasad hello umożliwia ustawianie limitów interfejsów API i operacje hello produktu. W tym samouczku firma Microsoft nie używać tej funkcji, aby usunąć hello **interfejsu api** i **operacji** elementy z hello **limit szybkości** element, taki sposób, że tylko hello zewnętrzne **limit szybkości** element pozostaje, jak pokazano w hello poniższy przykład.

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

W hello bezpłatnej wersji próbnej produktu, szybkość maksymalna dopuszczalna wywołania hello jest 10 połączeń na minutę, wpisać **10** jako wartość hello hello **wywołania** atrybutu i **60** dla hello **okres odnawiania** atrybutu.

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

tooconfigure hello **przydział użycia zestawu na subskrypcję** zasad, pozycja kursora bezpośrednio pod hello nowo dodanych **limit szybkości** elementu w obrębie hello **przychodzących** element, a następnie odszukaj i kliknij hello Strzałka toohello lewej strony **przydział użycia zestawu na subskrypcję**.

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

Podobnie toohello **przydział użycia zestawu na subskrypcję** zasad, **przydział użycia zestawu na subskrypcję** zasad pozwala na ustawienie informacji o możliwościach dla interfejsów API i operacje hello produktu. W tym samouczku firma Microsoft nie używać tej funkcji, aby usunąć hello **interfejsu api** i **operacji** elementy z hello **przydziału** element, jak pokazano w hello poniższy przykład.

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

Przydziały może bazować na powitania liczba wywołań na interwał i przepustowości. W tym samouczku będziemy są nie ograniczania przepustowości na podstawie, więc usunięcie hello **przepustowości** atrybutu.

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

Hello bezpłatnej wersji próbnej produktu przydział hello jest wywołania 200 punktów w tygodniu. Określ **200** jako wartość hello hello **wywołania** atrybutu, a następnie określ **604800** jako wartość hello hello **okres odnawiania** atrybut.

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> Interwały zasad są określane w sekundach. Interwał powitania toocalculate na tydzień, należy pomnożyć hello liczbę dni (7) do hello liczbę godzin w ciągu dnia (24) hello liczbę minut w ciągu godziny (60) hello liczby sekund na minutę (60): 7 * 24 * 60 * 60 = 604800.
> 
> 

Po zakończeniu konfigurowania zasad hello powinna być zgodna hello poniższy przykład.

```xml
<policies>
    <inbound>
        <rate-limit calls="10" renewal-period="60">
        </rate-limit>
        <quota calls="200" renewal-period="604800">
        </quota>
        <base />

</inbound>
<outbound>

    <base />

    </outbound>
</policies>
```

Po hello potrzeby skonfigurowano zasad, kliknij przycisk **zapisać**.

![Zapisywanie zasad][api-management-policy-save]

## <a name="publish-product"></a> toopublish hello produktu
Witaj hello dodano interfejsy API i hello zasad są skonfigurowane, hello produktu musi zostać opublikowany, dzięki czemu mogą być używane przez deweloperów. Kliknij przycisk **produktów** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij **bezpłatnej wersji próbnej** tooconfigure hello produktu.

![Konfigurowanie produktu][api-management-configure-product]

Kliknij przycisk **publikowania**, a następnie kliknij przycisk **tak, przed opublikowaniem** tooconfirm.

![Publikowanie produktu][api-management-publish-product]

## <a name="subscribe-account"></a>toosubscribe produktu toohello konta dewelopera
Teraz tego produktu hello zostanie opublikowana, jest używane przez programistów tooand toobe dostępnych subskrypcji.

> Administratorzy wystąpienia interfejsu API zarządzania są automatycznie subskrybowanego tooevery produktu. W tym kroku samouczka firma Microsoft będzie subskrypcji jedną hello dewelopera z systemem innym niż administrator konta toohello bezpłatnej wersji próbnej produktu. Jeśli konta dewelopera jest częścią roli Administratorzy hello, następnie można wykonać wraz z tego kroku, nawet jeśli masz już subskrypcję.
> 
> 

Kliknij przycisk **użytkowników** na powitania **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij nazwę hello konta dewelopera. W tym przykładzie używamy hello **Gragg Borowik** konta dewelopera.

![Konfigurowanie konta dewelopera][api-management-configure-developer]

Kliknij przycisk **Dodaj subskrypcję**.

![Dodawanie subskrypcji][api-management-add-subscription-menu]

Wybierz produkt **Bezpłatna wersja próbna**, a następnie kliknij przycisk **Subskrybuj**.

![Dodawanie subskrypcji][api-management-add-subscription]

> [!NOTE]
> W tym samouczku wiele równoczesnych subskrypcji nie są włączone hello bezpłatnej wersji próbnej produktu. Jeśli były, jak pokazano w hello poniższy przykład użytkownik będzie zostanie wyświetlony monit o tooname hello subskrypcji.
> 
> 

![Dodawanie subskrypcji][api-management-add-subscription-multiple]

Po kliknięciu przycisku **Subskrybuj**, produktu hello jest wyświetlana w hello **subskrypcji** listę hello użytkownika.

![Dodana subskrypcja][api-management-subscription-added]

## <a name="test-rate-limit"></a>toocall operacji i testowania limit szybkości hello
Witaj bezpłatnej wersji próbnej produktu jest skonfigurowany, a opublikowana, firma Microsoft wywoływanie niektórych operacji i testowania zasad limitu szybkości hello.
Przełącznik toohello portalu dla deweloperów, klikając **portalu dla deweloperów** hello prawym górnym menu.

![Portal dla deweloperów][api-management-developer-portal-menu]

Kliknij przycisk **interfejsów API** w hello menu u góry, a następnie kliknij przycisk **Echo API**.

![Portal dla deweloperów][api-management-developer-portal-api-menu]

Kliknij operację **GET Resource** (pobieranie zasobu), a następnie kliknij przycisk **Wypróbuj**.

![Otwarta konsola][api-management-open-console]

Zachowaj hello domyślne wartości parametrów, a następnie wybierz klucz subskrypcji hello bezpłatnej wersji próbnej produktu.

![Klucz subskrypcji][api-management-select-key]

> [!NOTE]
> Jeśli masz wiele subskrypcji, należy się, że klucz hello tooselect dla **bezpłatnej wersji próbnej**, lub inne zasady hello, które zostały skonfigurowane w poprzednich krokach hello nie będzie obowiązywać.
> 
> 

Kliknij przycisk **wysyłania**, a następnie Wyświetl hello odpowiedzi. Uwaga hello **stanu odpowiedzi** z **200 OK**.

![Wyniki operacji][api-management-http-get-results]

Kliknij przycisk **wysyłania** szybkością większa niż hello polityka limit 10 połączeń na minutę. Po przekroczeniu zasad limitu szybkości hello stan odpowiedzi **429 zbyt wiele żądań** jest zwracany.

![Wyniki operacji][api-management-http-get-429]

Witaj **zawartości odpowiedzi** wskazuje hello pozostałych Interwał ponownych prób zakończy się pomyślnie.

Jeśli obowiązuje zasada limit szybkości hello 10 połączeń na minutę, kolejne wywołania zakończy się niepowodzeniem przed upływem 60 sekund od hello pierwszy hello 10 pomyślnych wywołań toohello produktu przed został przekroczony limit szybkości hello. W tym przykładzie hello pozostałych interwał to 54 sekund.

## <a name="next-steps"> </a>Następne kroki
* Obejrzyj pokaz ustawienia limitów szybkości i przydziały w powitania po wideo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-product-with-rules/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-product-with-rules/api-management-add-product.png
[api-management-new-product-window]: ./media/api-management-howto-product-with-rules/api-management-new-product-window.png
[api-management-product-added]: ./media/api-management-howto-product-with-rules/api-management-product-added.png
[api-management-add-policy]: ./media/api-management-howto-product-with-rules/api-management-add-policy.png
[api-management-policy-editor-inbound]: ./media/api-management-howto-product-with-rules/api-management-policy-editor-inbound.png
[api-management-limit-policies]: ./media/api-management-howto-product-with-rules/api-management-limit-policies.png
[api-management-policy-save]: ./media/api-management-howto-product-with-rules/api-management-policy-save.png
[api-management-configure-product]: ./media/api-management-howto-product-with-rules/api-management-configure-product.png
[api-management-add-api]: ./media/api-management-howto-product-with-rules/api-management-add-api.png
[api-management-add-echo-api]: ./media/api-management-howto-product-with-rules/api-management-add-echo-api.png
[api-management-developer-portal-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-menu.png
[api-management-publish-product]: ./media/api-management-howto-product-with-rules/api-management-publish-product.png
[api-management-configure-developer]: ./media/api-management-howto-product-with-rules/api-management-configure-developer.png
[api-management-add-subscription-menu]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-menu.png
[api-management-add-subscription]: ./media/api-management-howto-product-with-rules/api-management-add-subscription.png
[api-management-developer-portal-api-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-api-menu.png
[api-management-open-console]: ./media/api-management-howto-product-with-rules/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-product-with-rules/api-management-http-get.png
[api-management-http-get-results]: ./media/api-management-howto-product-with-rules/api-management-http-get-results.png
[api-management-http-get-429]: ./media/api-management-howto-product-with-rules/api-management-http-get-429.png
[api-management-product-policy]: ./media/api-management-howto-product-with-rules/api-management-product-policy.png
[api-management-add-developers-group]: ./media/api-management-howto-product-with-rules/api-management-add-developers-group.png
[api-management-select-key]: ./media/api-management-howto-product-with-rules/api-management-select-key.png
[api-management-subscription-added]: ./media/api-management-howto-product-with-rules/api-management-subscription-added.png
[api-management-add-subscription-multiple]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-multiple.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How toocreate and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers tooa product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API toohello product]: #add-api
[Publish hello product]: #publish-product
[Subscribe a developer account toohello product]: #subscribe-account
[Call an operation and test hello rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
