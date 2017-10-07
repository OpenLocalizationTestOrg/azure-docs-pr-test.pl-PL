---
title: "aaaException zarządzania — narzędzie modelowania zagrożeń Microsoft - Azure | Dokumentacja firmy Microsoft"
description: "środki zaradcze w przypadku zagrożeń w hello narzędzie modelowania zagrożeń"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 247096c10deeca94ebb9b19df7ba60e442ca1e4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-exception-management--mitigations"></a>Ramka zabezpieczeń: Zarządzanie wyjątkami | Środki zaradcze 
| Produktów i usług | Artykuł |
| --------------- | ------- |
| **WCF** | <ul><li>[Usługi WCF - nie zawiera węzła serviceDebug w pliku konfiguracji](#servicedebug)</li><li>[Usługi WCF - nie zawiera węzła serviceMetadata w pliku konfiguracji](#servicemetadata)</li></ul> |
| **Interfejs API sieci Web** | <ul><li>[Upewnij się, że odpowiednich wyjątków odbywa się w interfejsie API sieci Web ASP.NET](#exception)</li></ul> |
| **Aplikacja sieci Web** | <ul><li>[Nie ujawniaj szczegóły zabezpieczeń w komunikatach o błędach](#messages)</li><li>[Implementowanie obsługi strony błędów domyślne](#default)</li><li>[Ustaw tooRetail metody wdrażania w usługach IIS](#deployment)</li><li>[Wyjątki powinna zakończyć się niepowodzeniem bezpiecznie](#fail)</li></ul> |

## <a id="servicedebug"></a>Usługi WCF - nie zawiera węzła serviceDebug w pliku konfiguracji

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | WCF | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny, NET Framework 3 |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [uzyskania zawartości Królestwo](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Kroki** | Usług Windows Communication Framework (WCF) może być skonfigurowany tooexpose informacji o debugowaniu. Debugowanie informacji nie powinna być używana w środowisku produkcyjnym. Witaj `<serviceDebug>` tagów Określa, czy funkcja informacji o debugowaniu hello jest włączone dla usługi WCF. Jeśli includeExceptionDetailInFaults atrybutu hello ustawiono tootrue, informacje o wyjątku z aplikacji hello zostanie zwrócony tooclients. Osoby atakujące mogą korzystać z hello dodatkowe informacje, które będą mogli z debugowania dane wyjściowe toomount ataków ukierunkowanych hello framework, bazy danych lub innych zasobów używanych przez aplikację hello. |

### <a name="example"></a>Przykład
Witaj następujący plik konfiguracji zawiera hello `<serviceDebug>` tagu: 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
Wyłącz informacji o debugowaniu w usłudze hello. Można to zrobić przez usunięcie hello `<serviceDebug>` tagu z pliku konfiguracji aplikacji. 

## <a id="servicemetadata"></a>Usługi WCF - nie zawiera węzła serviceMetadata w pliku konfiguracji

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | WCF | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Ogólny, NET Framework 3 |
| **Odwołania**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [uzyskania zawartości Królestwo](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Kroki** | Publicznie udostępnianie informacji na temat usługi umożliwia atakującym cenny wgląd w sposób może wykorzystać hello usługi. Witaj `<serviceMetadata>` tag włącza funkcję publikowania hello metadanych. Metadane usługi mogą zawierać poufne informacje, które nie powinny być publicznie dostępne. Co najmniej umożliwiają tylko przez zaufanych użytkowników tooaccess hello metadanych i upewnij się, że niepotrzebnych informacji nie jest uwidaczniana. Jeszcze lepiej całkowicie wyłączyć hello możliwości toopublish metadanych. Bezpieczne konfiguracji usługi WCF nie będą zawierać hello `<serviceMetadata>` tagu. |

## <a id="exception"></a>Upewnij się, że odpowiednich wyjątków odbywa się w interfejsie API sieci Web ASP.NET

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Interfejs API sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | MVC 5, 6 MVC |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Obsługa wyjątków w ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [modelu weryfikacji w składniku ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api) |
| **Kroki** | Domyślnie większość nieprzechwyconych wyjątków w interfejsie API sieci Web platformy ASP.NET są przetłumaczyć z kodem stanu odpowiedzi HTTP`500, Internal Server Error`|

### <a name="example"></a>Przykład
Kod stanu hello toocontrol zwrócony przez hello interfejsu API, `HttpResponseException` można w sposób przedstawiony poniżej: 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        throw new HttpResponseException(HttpStatusCode.NotFound);
    }
    return item;
}
```

### <a name="example"></a>Przykład
Dla dalszego kontrolę nad hello wyjątek odpowiedzi, hello `HttpResponseMessage` klasa może być używana, jak pokazano poniżej: 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        var resp = new HttpResponseMessage(HttpStatusCode.NotFound)
        {
            Content = new StringContent(string.Format("No product with ID = {0}", id)),
            ReasonPhrase = "Product ID Not Found"
        }
        throw new HttpResponseException(resp);
    }
    return item;
}
```
toocatch nieobsługiwane wyjątki, które nie są typu hello `HttpResponseException`, filtry wyjątków mogą być używane. Filtry wyjątków zaimplementować hello `System.Web.Http.Filters.IExceptionFilter` interfejsu. Witaj najprostszy sposób toowrite filtra wyjątku jest tooderive z hello `System.Web.Http.Filters.ExceptionFilterAttribute` klasy i przesłonić metodę OnException hello. 

### <a name="example"></a>Przykład
Oto filtr, który konwertuje `NotImplementedException` wyjątków w kodzie stanu HTTP `501, Not Implemented`: 
```C#
namespace ProductStore.Filters
{
    using System;
    using System.Net;
    using System.Net.Http;
    using System.Web.Http.Filters;

    public class NotImplExceptionFilterAttribute : ExceptionFilterAttribute 
    {
        public override void OnException(HttpActionExecutedContext context)
        {
            if (context.Exception is NotImplementedException)
            {
                context.Response = new HttpResponseMessage(HttpStatusCode.NotImplemented);
            }
        }
    }
}
```

Istnieje kilka sposobów tooregister filtru wyjątków interfejsu API sieci Web:
- Przez akcję
- Kontroler
- Globalny

### <a name="example"></a>Przykład
Witaj tooapply Filtruj tooa określonej akcji, Dodaj filtr hello jako akcja toohello atrybutu: 
```C#
public class ProductsController : ApiController
{
    [NotImplExceptionFilter]
    public Contact GetContact(int id)
    {
        throw new NotImplementedException("This method is not implemented");
    }
}
```
### <a name="example"></a>Przykład
tooapply hello filtru tooall działania hello `controller`, Dodaj filtr hello jako atrybut toohello `controller` klasy: 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a>Przykład
tooapply hello filtrować globalnie tooall kontrolerów interfejsu API sieci Web, dodać wystąpienia toohello filtru hello `GlobalConfiguration.Configuration.Filters` kolekcji. Filtry wyjątków w tej kolekcji stosowanie akcji kontrolera interfejsu API sieci Web tooany. 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a>Przykład
Weryfikacja modelu hello stan modelu mogą być przekazywane metody tooCreateErrorResponse, jak pokazano poniżej: 
```C#
public HttpResponseMessage PostProduct(Product item)
{
    if (!ModelState.IsValid)
    {
        return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
    }
    // Implementation not shown...
}
```

Łącza hello wyboru w sekcji odwołań hello, aby uzyskać więcej informacji o obsługę wyjątkowych i sprawdzania poprawności modelu w interfejsie API sieci Web ASP.Net 

## <a id="messages"></a>Nie ujawniaj szczegóły zabezpieczeń w komunikatach o błędach

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | <p>Ogólne komunikaty o błędach są dostarczane bezpośrednio toohello użytkownika bez uwzględniania aplikacji poufnych danych. Przykłady danych poufnych:</p><ul><li>Nazwy serwerów</li><li>Parametry połączeń</li><li>Nazwy użytkowników</li><li>Hasła</li><li>Procedury SQL</li><li>Szczegóły błędów SQL dynamiczne</li><li>Ślad stosu i wiersze kodu</li><li>Zmiennych przechowywanych w pamięci</li><li>Dysk i folder lokalizacji</li><li>Punkty instalacji aplikacji</li><li>Ustawienia konfiguracji hosta</li><li>Inne szczegóły aplikacja wewnętrzna</li></ul><p>Generują pułapki wszystkich błędów w aplikacji i zapewnianie ogólne komunikaty o błędach, a także włączenie błędy niestandardowe w ramach usług IIS pomaga zapobiegać ujawnienie informacji. Bazy danych programu SQL Server i .NET obsługi wyjątków, między inny błąd obsługi architektury, są szczególnie pełne i bardzo przydatne tooa złośliwy użytkownik profilowania aplikacji. Czy nie bezpośrednio hello wyświetlana zawartość klasę pochodną klasy wyjątków .NET hello i sprawdź, czy mają odpowiednie wyjątków, dzięki czemu wystąpił nieoczekiwany wyjątek nie jest przypadkowo wywoływane bezpośrednio toohello użytkownika.</p><ul><li>Podaj ogólne komunikaty o błędach bezpośrednio toohello użytkownika, który abstrakcyjnej zadań bezpośrednio w wiadomości powitania błąd wyjątku/konkretne szczegółowe informacje</li><li>Wyświetlana zawartość hello wyjątku .NET bezpośrednio klasa toohello użytkownika</li><li>Pułapki wszystkie komunikaty o błędach i w razie potrzeby o hello użytkownika za pośrednictwem błąd rodzajowy komunikat wysłany toohello aplikacji klienta</li><li>Nie ujawniaj hello zawartość klasy wyjątku hello bezpośrednio toohello użytkowników, szczególnie hello wartością zwracaną z `.ToString()`, lub wartości hello hello właściwości wiadomości i ślad stosu. Bezpiecznego logowania tych informacji i wyświetlić więcej nieszkodliwe użytkownika toohello wiadomości</li></ul>|

## <a id="default"></a>Implementowanie obsługi strony błędów domyślne

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Edytuj okno dialogowe ustawień stron błędów ASP.NET](https://technet.microsoft.com/library/dd569096(WS.10).aspx) |
| **Kroki** | <p>Aplikacja ASP.NET nie powiedzie się i powoduje, że wystąpił wewnętrzny błąd serwera HTTP/1.x 500 lub Konfiguracja funkcji, (na przykład Filtrowanie żądań) zapobiega wyświetlaniu strony, zostanie wygenerowany komunikat o błędzie. Administratorzy mogą wybrać, czy aplikacja hello powinien być wyświetlany, przyjazny komunikat toohello klienta, szczegółowe informacje o błędzie komunikat toohello klienta lub tylko toolocalhost komunikat szczegółowe informacje o błędzie. Witaj <customErrors> znacznika w pliku web.config hello ma trzy tryby:</p><ul><li>**Na:** Określa, czy błędy niestandardowe są włączone. Jeśli zostanie określony bez atrybutu defaultRedirect, użytkownicy widzą błąd ogólny. błędy niestandardowe Hello są wyświetlane toohello klienci zdalni i toohello hosta lokalnego</li><li>**OFF:** Określa, czy błędy niestandardowe są wyłączone. Witaj szczegółowe błędy programu ASP.NET są wyświetlane toohello klienci zdalni i toohello hosta lokalnego</li><li>**RemoteOnly:** Określa, czy błędy niestandardowe są widoczne tylko toohello klienci zdalni i że błędy programu ASP.NET są pokazywane toohello hosta lokalnego. Jest to wartość domyślna hello</li></ul><p>Otwórz hello `web.config` dla witryny aplikacji hello i upewnij się, że hello tag ma `<customErrors mode="RemoteOnly" />` lub `<customErrors mode="On" />` zdefiniowane.</p>|

## <a id="deployment"></a>Ustaw tooRetail metody wdrażania w usługach IIS

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [wdrożenie — Element (schemat ustawień programu ASP.NET)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx) |
| **Kroki** | <p>Witaj `<deployment retail>` przełącznik jest przeznaczony dla systemów produkcyjnych serwerów usług IIS. Ten parametr jest toohelp używane aplikacje o najlepszej wydajności możliwe hello i najniższe możliwe informacji zabezpieczających wycieków wyłączając hello danych wyjściowych śledzenia toogenerate możliwości aplikacji na stronie wyłączenie toodisplay możliwości hello szczegóły błędu Użytkownicy tooend wiadomości i wyłączanie hello debugowania przełącznika.</p><p>Często, przełączniki i opcje, które są ukierunkowane developer, takie jak nie powiodło się żądanie śledzenia i debugowania, są włączane podczas opracowywania active. Zaleca się, że metoda wdrażania hello na dowolnym serwerze produkcyjnym można ustawić tooretail. Otwórz plik machine.config hello i upewnij się, że `<deployment retail="true" />` pozostanie wartość tootrue.</p>|

## <a id="fail"></a>Wyjątki powinna zakończyć się niepowodzeniem bezpiecznie

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Niepowodzenie bezpiecznego](https://www.owasp.org/index.php/Fail_securely) |
| **Kroki** | Aplikacja powinna zakończyć się niepowodzeniem bezpiecznie. Dowolnej metody, która zwraca wartość logiczną, oparte na następuje pewnych decyzji, powinien mieć dokładnie utworzyć bloku wyjątków. Istnieje wiele błędów logicznych powodu pełzanie problemy zabezpieczeń toowhich w po bloku wyjątków hello napisano zaniedbali.|

### <a name="example"></a>Przykład
```C#
        public static bool ValidateDomain(string pathToValidate, Uri currentUrl)
        {
            try
            {
                if (!string.IsNullOrWhiteSpace(pathToValidate))
                {
                    var domain = RetrieveDomain(currentUrl);
                    var replyPath = new Uri(pathToValidate);
                    var replyDomain = RetrieveDomain(replyPath);

                    if (string.Compare(domain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                    {
                        //// Adding additional check tooenable CMS urls if they are not hosted on same domain.
                        if (!string.IsNullOrWhiteSpace(Utilities.CmsBase))
                        {
                            var cmsDomain = RetrieveDomain(new Uri(Utilities.Base.Trim()));
                            if (string.Compare(cmDomain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                            {
                                return false;
                            }
                            else
                            {
                                return true;
                            }
                        }

                        return false;
                    }
                }

                return true;
            }
            catch (UriFormatException ex)
            {
                LogHelper.LogException("Utilities:ValidateDomain", ex);
                return true;
            }
        }
```
Hello powyżej metoda zawsze zwraca wartość PRAWDA, jeśli wystąpi wyjątek. Jeśli użytkownik końcowy hello zawiera źle sformułowany adres URL, który hello względem przeglądarki, ale hello `Uri()` Konstruktor nie, to spowoduje zgłoszenie wyjątku i ofiara hello zostaną wykonane toohello prawidłowe, ale źle sformułowany adres URL. 
