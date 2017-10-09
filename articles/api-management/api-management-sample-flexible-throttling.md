---
title: "żądanie aaaAdvanced ograniczania z usługą Azure API Management"
description: "Dowiedz się, jak toocreate i stosować elastyczny przydział i szybkość ograniczenia zasad z usługą Azure API Management."
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: fc813a65-7793-4c17-8bb9-e387838193ae
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: ac87f83118a37bd587fddf044e5c2d6fc2af9031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-request-throttling-with-azure-api-management"></a>Zaawansowane żądanie ograniczania z usługą Azure API Management
Trwa toothrottle stanie przychodzących żądań jest kluczową rolę usługi Azure API Management. Przekazywane przez kontrolowanie hello współczynnika żądań lub hello całkowita liczba żądań/danych, umożliwia zarządzanie interfejsami API tooprotect dostawcy interfejsu API ich interfejsów API z nadużyć i utworzyć wartości dla różnych warstw produktu interfejsu API.

## <a name="product-based-throttling"></a>Ograniczanie produktu w oparciu
toodate, szybkość hello ograniczanie możliwości ma została ograniczona toobeing zakres tooa konkretnego produktu subskrypcji (zasadniczo klucza), zdefiniowane w hello API Management portal wydawcy. Jest to przydatne hello interfejsu API dostawcy tooapply limitów na powitania deweloperów, którzy utworzyli konto toouse ich interfejsu API, jednak nie pomaga, na przykład w ograniczania indywidualnych użytkowników końcowych z hello interfejsu API. Jest to możliwe, że dla pojedynczego użytkownika tooconsume aplikacji hello developer hello całego przydziału a następnie uniemożliwić innych klientów hello Deweloper aplikacji hello toouse stanie. Ponadto wielu klientów, którzy mogą generować dużą liczbę żądań może ograniczyć dostępu toooccasional użytkowników.

## <a name="custom-key-based-throttling"></a>Klucz niestandardowy na podstawie ograniczania przepustowości
Hello nowe [szybkość limit przez klucz](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) i [limitu przydziału przez klucz](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) udostępniają formantu tootraffic znacznie bardziej elastyczne rozwiązania. Te nowe zasady pozwalają toodefine wyrażenia tooidentify hello klucze, które będą używane tootrack ruchu użycia. działa to sposób Hello easiest przedstawiono przykład. 

## <a name="ip-address-throttling"></a>Ograniczenia adresów IP
Hello następujące zasady ograniczyć pojedynczy tooonly adres IP klienta 10 wywołuje co minutę, w sumie 1 000 000 wywołań i 10 000 kilobajtów przepustowości miesięcznie. 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

Jeśli wszyscy klienci na powitania Internet używany unikatowy adres IP, może to być efektywnym sposobem ograniczenia użycia przez użytkownika. Jednak jest bardzo prawdopodobne, że wielu użytkowników będzie udostępnianie jeden publiczny adres IP powodu toothem podczas uzyskiwania dostępu do hello Internet za pośrednictwem urządzenia translatora adresów Sieciowych. Mimo to dla interfejsów API, które umożliwia dostęp nieuwierzytelniony hello `IpAddress` może być hello najlepszym rozwiązaniem.

## <a name="user-identity-throttling"></a>Ograniczenie tożsamości użytkownika
Jeśli użytkownik jest uwierzytelniony, ograniczenie klucza mogą być generowane na podstawie informacji, który unikatowo identyfikuje, który użytkownik.

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

W tym przykładzie mamy wyodrębnić hello nagłówek autoryzacji, należy konwertować go za`JWT` obiekt i Użyj tematu hello hello tokenu tooidentify hello użytkownika i używać go jako szybkość hello ograniczenie klucza. Jeśli hello tożsamości użytkownika jest przechowywany w hello `JWT` zgodnie z jedną hello innych oświadczeń następnie czy można użyć wartości w jego miejscu.

## <a name="combined-policies"></a>Łączna zasad
Mimo że hello ograniczania nowe zasady zapewniają większą kontrolę niż hello istniejące zasady ograniczania przepustowości, występuje nadal łączenie możliwości obu wartości. Ograniczanie przez klucz produktu subskrypcji ([Limit szybkości wywołanie przez subskrypcji](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) i [przydział użycia zestawu subskrypcji](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) to dobry sposób tooenable monetizing interfejsu API, pobierając oparte na poziomy użycia. Witaj skuteczniejszą kontrolę ich stanie toothrottle przez użytkownika uzupełnia i zapobiega zachowanie jednego użytkownika pogorszenia jakości związku środowisko hello innego. 

## <a name="client-driven-throttling"></a>Klient zmiennych ograniczania przepustowości
Gdy hello ograniczania klucza jest definiowana za pomocą [wyrażenie zasad](https://msdn.microsoft.com/library/azure/dn910913.aspx), wówczas jest dostawcy hello interfejsu API, który jest wybór sposobu ograniczania hello ma zakres. Jednak może być deweloperem toocontrol jak szybkości ograniczyć własnych klientów. Może zostać włączona przez dostawcę interfejsu API hello dzięki zastosowaniu niestandardowy nagłówek tooallow hello dewelopera klienta aplikacji toocommunicate hello klucza toohello interfejsu API.

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

Dzięki temu deweloper powitania klienta aplikacji toochoose jak chcą szybkość hello toocreate ograniczenie klucza. Z niewielki ingenuity deweloperowi klienta można utworzyć własne warstwy stawki przydzielając zestawy kluczy toousers i obracanie hello użycia klucza.

## <a name="summary"></a>Podsumowanie
Zarządzanie interfejsami API Azure zapewnia szybkość i oferty ograniczania tooboth ochrony i Dodaj wartości tooyour interfejsu API usługi. Ograniczanie nowych zasad za pomocą reguł niestandardowych zakresu Hello zezwala na system można bardziej precyzyjną kontrolę nad tooenable tych zasad aplikacji jeszcze bardziej poprawić jakość toobuild klientów. Przykłady Hello w tym artykule przedstawiają hello stosowania tych nowych zasad przez współczynnik produkcyjnym ograniczanie klucze z adresów IP klientów, tożsamość użytkownika i wartości klientów wygenerowany. Istnieje jednak wiele innych części wiadomości powitania, które mogą zostać użyte, takich jak agent użytkownika, adres URL ścieżki fragmenty, rozmiar wiadomości.

## <a name="next-steps"></a>Następne kroki
Daj nam swoją opinię w wątku Disqus hello tego tematu. Jest bardzo toohear o innych potencjalnych wartości kluczy, które zostały logicznej wybór w swoim scenariuszu.

## <a name="watch-a-video-overview-of-these-policies"></a>Obejrzyj film poglądowy dotyczący tych zasad
Aby uzyskać więcej informacji na temat hello [szybkość limit przez klucz](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) i [limitu przydziału przez klucz](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) zasady omówione w tym artykule, obserwuj powitania po wideo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

