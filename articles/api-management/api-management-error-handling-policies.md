---
title: "Obsługa w ramach zasad usługi Azure API Management aaaError | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toorespond tooerror warunki, które mogą wystąpić podczas hello przetwarzania żądań w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 3c777964-02b2-4f55-8731-8c3bd3c0ae27
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 002c65f21e763fd644da61b6a11685ffd97488c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="error-handling-in-api-management-policies"></a>Obsługa błędów w zasad interfejsu API zarządzania
Zarządzanie interfejsami API Azure umożliwia wydawców toorespond tooerror warunki, które mogą wystąpić podczas przetwarzania żądania toohello proxy hello zapewniając `ProxyError` obiektu. Witaj `ProxyError` obiekt jest dostępny za pośrednictwem hello [kontekstu. LastError](api-management-policy-expressions.md#ContextVariables) właściwości i mogą być używane przez zasady w hello `on-error` sekcji zasad. Ten temat zawiera odwołanie błędu hello możliwości obsługi w programie Azure API Management.  
  
## <a name="error-handling-in-api-management"></a>Obsługa błędów w zarządzanie interfejsami API  
 Zasady w usłudze Azure API Management są podzielone na `inbound`, `backend`, `outbound`, i `on-error` sekcjach przedstawiono, jak pokazano w hello poniższy przykład.  
  
```xml  
<policies>  
  <inbound>  
    <!-- statements toobe applied toohello request go here -->  
  </inbound>  
  <backend>  
    <!-- statements toobe applied before hello request is   
         forwarded toohello backend service go here -->  
    </backend>  
    <outbound>  
      <!-- statements toobe applied toohello response go here -->  
    </outbound>  
    <on-error>  
        <!-- statements toobe applied if there is an error   
             condition go here -->  
  </on-error>  
</policies>  
```  
  
 Podczas przetwarzania żądania hello, wbudowanych kroków wdrożeniowych wraz z żadnych zasad, które znajdują się w zakresie hello żądania. Jeśli wystąpi błąd, przetwarzania natychmiast przechodzi toohello `on-error` sekcji zasad. Witaj `on-error` sekcji zasad może być używany w żadnych zakresu i wydawców interfejsu API można skonfigurować zachowanie niestandardowych, takich jak rejestrowanie koncentratory tooevent błąd hello lub tworzenia nowych wywołującego toohello tooreturn odpowiedzi.  
  
> [!NOTE]
>  Witaj `on-error` sekcji nie jest obecny w zasady domyślne. Witaj tooadd `on-error` sekcji tooa zasad, przeglądanie toohello potrzeby zasad w edytorze zasad hello i dodać go. Aby uzyskać więcej informacji o konfigurowaniu zasad, zobacz [zasad w usłudze API Management](https://azure.microsoft.com/documentation/articles/api-management-howto-policies/).  
>   
>  W przypadku nie `on-error` sekcji wywołań będą otrzymywać wiadomości odpowiedzi HTTP 400 lub 500 Jeśli wystąpi błąd.  
  
### <a name="policies-allowed-in-on-error"></a>Zasady dozwolone na błąd  
 Witaj następujące zasady mogą być używane w hello `on-error` sekcji zasad.  
  
-   [Wybierz pozycję](api-management-advanced-policies.md#choose)  
  
-   [Ustaw zmienną](api-management-advanced-policies.md#set-variable)  
  
-   [Znajdź i Zamień](api-management-transformation-policies.md#Findandreplacestringinbody)  
  
-   [odpowiedź Return](api-management-advanced-policies.md#ReturnResponse)  
  
-   [set — nagłówek](api-management-transformation-policies.md#SetHTTPheader)  
  
-   [set, metoda](api-management-advanced-policies.md#SetRequestMethod)  
  
-   [Ustaw stan](api-management-advanced-policies.md#SetStatus)  
  
-   [Żądanie wysłania](api-management-advanced-policies.md#SendRequest)  
  
-   [sposób żądania, Wyślij co w-](api-management-advanced-policies.md#SendOneWayRequest)  
  
-   [dziennika do Centrum eventhub](api-management-advanced-policies.md#log-to-eventhub)  
  
-   [JSON do pliku xml](api-management-transformation-policies.md#ConvertJSONtoXML)  
  
-   [XML do formatu json](api-management-transformation-policies.md#ConvertXMLtoJSON)  
  
## <a name="lasterror"></a>LastError  
 Gdy wystąpi błąd i kontroli w tę łódź toohello `on-error` sekcji zasad błąd hello są przechowywane w [kontekstu. LastError](api-management-policy-expressions.md#ContextVariables) właściwość, która jest możliwy przy użyciu zasad w hello `on-error` sekcji i ma następujące właściwości hello.  
  
|Nazwa|Typ|Opis|Wymagane|  
|----------|----------|-----------------|--------------|  
|Element źródłowy|Ciąg|Element hello nazwy którym wystąpił błąd hello. Może być zasad lub nazwa kroku wbudowanej potoku.|Tak|  
|Przyczyna|Ciąg|Kod błędu przyjaznych dla komputera, który może służyć do obsługi błędów.|Nie|  
|Komunikat|Ciąg|Opis błędu zrozumiałą dla użytkownika.|Tak|  
|Zakres|Ciąg|Nazwa zakresu hello, gdzie wystąpił błąd hello i może być "globalne", "product", "interfejsu api" lub "operacji"|Nie|  
|Sekcja|Ciąg|Nazwa sekcji, w którym wystąpił błąd i może wynosić "ruchu przychodzącego", "zaplecze", "wychodzący" lub "on error".|Nie|  
|Ścieżka|Ciąg|Określa zagnieżdżonych zasad, np. "Wybierz [3] / po [2]".|Nie|  
|PolicyId|Ciąg|Wartość hello `id` atrybut, jeśli określony przez powitania klienta i zasad hello, w którym wystąpił błąd|Nie|  
  
> [!NOTE]
>  Wszystkie zasady mają opcjonalny `id` atrybut, który można dodać elementu głównego toohello hello zasad. Jeśli ten atrybut jest obecny w zasadach, gdy wystąpi błąd, można pobrać wartości hello hello atrybutu przy użyciu hello `context.LastError.PolicyId` właściwości.  
  
## <a name="predefined-errors-for-built-in-steps"></a>Wstępnie zdefiniowane błędów dla wbudowanych kroków  
 Witaj następujące błędy są wstępnie zdefiniowane warunki błędów, które mogą wystąpić podczas obliczania hello przetwarzania wbudowanych kroków.  
  
|Element źródłowy|Warunek|Przyczyna|Komunikat|  
|------------|---------------|------------|-------------|  
|konfiguracja|Identyfikator URI nie odpowiada, operacji lub tooany interfejsu Api|OperationNotFound|Toomatch przychodzącego żądania tooan operacji.|  
|Autoryzacji|Nie podano klucza subskrypcji|SubscriptionKeyNotFound|Odmowa powodu toomissing subskrypcji klucz dostępu. Upewnij się, że klucz subskrypcji tooinclude podczas wprowadzania toothis żądania interfejsu API.|  
|Autoryzacji|Wartość klucza subskrypcji jest nieprawidłowy|SubscriptionKeyInvalid|Odmowa powodu tooinvalid subskrypcji klucz dostępu. Upewnij się, że tooprovide prawidłowy klucz dla subskrypcji usługi active.|  
  
## <a name="predefined-errors-for-policies"></a>Błędy wstępnie zdefiniowane zasady  
 Witaj następujące błędy są wstępnie zdefiniowane warunki błędów, które mogą wystąpić podczas oceny zasad.  
  
|Element źródłowy|Warunek|Przyczyna|Komunikat|  
|------------|---------------|------------|-------------|  
|limit szybkości|Przekroczono limit szybkości|RateLimitExceeded|Przekroczono limit szybkości|  
|limit przydziału|Przekroczono przydział|QuotaExceeded|Poza limitem woluminu wywołania. Przydział zostanie uzupełniona w xx:xx:xx. - lub - limit przydziału przepustowości. Przydział zostanie uzupełniona w xx:xx:xx.|  
|Format jsonp|Nieprawidłowa wartość parametru wywołania zwrotnego (zawiera nieprawidłowe znaki)|CallbackParameterInvalid|Wartość parametru wywołania zwrotnego {-nazwy parametru wywołania zwrotnego-} nie jest prawidłowym identyfikatorem języka JavaScript.|  
|Filtr IP|IP wywołującego tooparse nie powiodło się z żądania|FailedToParseCallerIP|Nie powiodło się adres IP tooestablish hello obiektu wywołującego. Odmowa dostępu.|  
|Filtr IP|Obiekt wywołujący IP nie ma na liście listy dozwolonych|CallerIpNotAllowed|Adres IP wywołującego {adres ip} nie jest dozwolone. Odmowa dostępu.|  
|Filtr IP|Obiekt wywołujący adres IP należy do listy zablokowanych|CallerIpBlocked|Adres IP wywołującego jest zablokowany. Odmowa dostępu.|  
|Sprawdź — nagłówek|Brak wymaganego nagłówka nie przedstawione lub wartość|HeaderNotFound|Nie znaleziono nagłówka {Nazwa nagłówka} w żądaniu hello. Odmowa dostępu.|  
|Sprawdź — nagłówek|Brak wymaganego nagłówka nie przedstawione lub wartość|HeaderValueNotAllowed|Wartość nagłówka {Nazwa nagłówka} z {wartość nagłówka} nie jest dozwolona. Odmowa dostępu.|  
|Sprawdź poprawność jwt|W żądaniu brakuje tokenu Jwt|TokenNotFound|Nie można odnaleźć w żądaniu hello JWT. Odmowa dostępu.|  
|Sprawdź poprawność jwt|Nie można sprawdzić poprawności podpisu|TokenSignatureInvalid|< wiadomości z biblioteki jwt\>. Odmowa dostępu.|  
|Sprawdź poprawność jwt|Nieprawidłowi odbiorcy|TokenAudienceNotAllowed|< wiadomości z biblioteki jwt\>. Odmowa dostępu.|  
|Sprawdź poprawność jwt|Nieprawidłowy wystawca|TokenIssuerNotAllowed|< wiadomości z biblioteki jwt\>. Odmowa dostępu.|  
|Sprawdź poprawność jwt|Token wygasł|TokenExpired|< wiadomości z biblioteki jwt\>. Odmowa dostępu.|  
|Sprawdź poprawność jwt|Klucz podpisu nie został rozwiązany przez identyfikator|TokenSignatureKeyNotFound|< wiadomości z biblioteki jwt\>. Odmowa dostępu.|  
|Sprawdź poprawność jwt|Token brakuje wymaganego oświadczeń|TokenClaimNotFound|Brak tokenu JWT powitania po oświadczeń: < c1\>, < c2\>,... Odmowa dostępu.|  
|Sprawdź poprawność jwt|Niezgodność wartości oświadczeń|TokenClaimValueNotAllowed|Wartość oświadczenia {Nazwa oświadczenia} {wartość oświadczenia} nie jest dozwolona. Odmowa dostępu.|  
|Sprawdź poprawność jwt|Inne błędy sprawdzania poprawności|JwtInvalid|< wiadomości z biblioteki jwt\>|

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji, Praca z zasad, zobacz [zasad w usłudze API Management](api-management-howto-policies.md).  