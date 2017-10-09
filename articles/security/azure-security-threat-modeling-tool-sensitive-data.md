---
title: "aaaSensitive danych - Narzędzie modelowania zagrożeń Microsoft - Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 8a18f43af439241ba193ccf668971ddc4655355f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-sensitive-data--mitigations"></a>Ramka zabezpieczeń: Dane poufne | Środki zaradcze 
| Produktów i usług | Artykuł |
| --------------- | ------- |
| **Granic zaufania maszyny** | <ul><li>[Upewnij się, że pliki binarne są zaciemniona, jeśli zawierają one informacje poufne](#binaries-info)</li><li>[Należy rozważyć użycie System szyfrowania plików (EFS) jest używane tooprotect poufne dane specyficzne dla użytkownika](#efs-user)</li><li>[Upewnij się, że poufne dane przechowywane przez aplikację hello w systemie plików hello jest zaszyfrowany](#filesystem)</li></ul> | 
| **Aplikacja sieci Web** | <ul><li>[Upewnij się, poufnej zawartości nie jest buforowana na powitania przeglądarki](#cache-browser)</li><li>[Szyfrowanie sekcji pliki konfiguracji aplikacji sieci Web, które zawierają dane poufne](#encrypt-data)</li><li>[Jawnie Wyłącz atrybutu HTML autouzupełniania hello w formularzach poufnych i dane wejściowe](#autocomplete-input)</li><li>[Upewnij się, że poufne dane wyświetlane na ekranie użytkownika hello są wyświetlane jako znaki](#data-mask)</li></ul> | 
| **Baza danych** | <ul><li>[Implementowanie użytkowników maskowania ujawnienie danych poufnych toolimit z systemem innym niż uprzywilejowany danych dynamicznych](#dynamic-users)</li><li>[Upewnij się, że hasła są przechowywane w formacie solone wyznaczania wartości skrótu](#salted-hash)</li><li>[Upewnij się, że poufne dane w kolumnach bazy danych są szyfrowane](#db-encrypted)</li><li>[Upewnij się, że włączone jest szyfrowanie tej bazy danych na poziomie (funkcji TDE)](#tde-enabled)</li><li>[Upewnij się, że kopie zapasowe bazy danych są szyfrowane.](#backup)</li></ul> | 
| **Interfejs API sieci Web** | <ul><li>[Upewnij się, tym tooWeb odpowiednich danych poufnych, interfejsu API nie jest przechowywane w magazynie w przeglądarce](#api-browser)</li></ul> | 
| Dokumentów w usłudze Azure DB | <ul><li>[Szyfrowania poufnych danych przechowywanych w usłudze DocumentDB](#encrypt-docdb)</li></ul> | 
| **Maszyna wirtualna platformy Azure IaaS granicy zaufania** | <ul><li>[Używać szyfrowania dysków Azure tooencrypt dysków używanych przez maszyny wirtualne](#disk-vm)</li></ul> | 
| **Granic zaufania sieci szkieletowej usług** | <ul><li>[Szyfrowanie kluczy tajnych w aplikacji sieci szkieletowej usług](#fabric-apps)</li></ul> | 
| **Dynamics CRM** | <ul><li>[Wykonaj modelowania zabezpieczeń i użyć zespołów jednostki biznesowe w przypadku, gdy wymagane](#modeling-teams)</li><li>[Minimalizowanie funkcja tooshare dostępu na jednostkach krytyczne](#entities)</li><li>[Użytkownicy pociągu na powitania ryzyko związane z hello Dynamics CRM udziału funkcji i rozwiązań dobrze chroniony](#good-practices)</li><li>[Programowanie regułę standardy, proscribing konfiguracji ze szczegółowymi informacjami w Zarządzanie wyjątkami dołączania](#exception-mgmt)</li></ul> | 
| **Azure Storage** | <ul><li>[Użyj szyfrowanie usługi Magazyn Azure (SSE) dla danych magazynowanych (wersja zapoznawcza)](#sse-preview)</li><li>[Użyj szyfrowania po stronie klienta toostore poufnych danych w usłudze Azure Storage](#client-storage)</li></ul> | 
| **Klientów urządzeń przenośnych** | <ul><li>[Szyfrowanie liter lub dane osobowe danymi zapisywanymi toophones lokalnego magazynu](#pii-phones)</li><li>[Zasłaniają wygenerowanych plików binarnych przed rozpoczęciem dystrybuowania tooend użytkowników](#binaries-end)</li></ul> | 
| **WCF** | <ul><li>[Ustaw właściwość clientCredentialType tooCertificate lub systemu Windows](#cert)</li><li>[Nie jest włączony tryb zabezpieczeń programu WCF](#security)</li></ul> | 

## <a id="binaries-info"></a>Upewnij się, że pliki binarne są zaciemniona, jeśli zawierają one informacje poufne

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Granic zaufania maszyny | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Upewnij się, że pliki binarne są zaciemniona, jeśli zawierają one informacje poufne, takich jak tajemnice handlowe logiki biznesowej poufnych, które powinny nie wycofane. Jest to toostop odtwarzania zestawów. Narzędzi, takich jak `CryptoObfuscator` mogą być używane w tym celu. |

## <a id="efs-user"></a>Należy rozważyć użycie System szyfrowania plików (EFS) jest używane tooprotect poufne dane specyficzne dla użytkownika

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Granic zaufania maszyny | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Należy rozważyć użycie System szyfrowania plików (EFS) jest używane tooprotect poufne dane specyficzne dla użytkownika z atakujący z komputerem toohello fizyczny dostęp. |

## <a id="filesystem"></a>Upewnij się, że poufne dane przechowywane przez aplikację hello w systemie plików hello jest zaszyfrowany

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Granic zaufania maszyny | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Upewnij się, że poufne dane przechowywane przez aplikację hello w systemie plików hello są zaszyfrowane (np. przy użyciu DPAPI), jeśli nie można wymusić systemu szyfrowania plików |

## <a id="cache-browser"></a>Upewnij się, poufnej zawartości nie jest buforowana na powitania przeglądarki

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny, MVC6 MVC5, formularzy sieci Web |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Przeglądarki może przechowywać informacje na potrzeby buforowania i historii. Te buforowane pliki są przechowywane w folderze, takich jak hello folderu tymczasowych plików internetowych w przypadku hello programu Internet Explorer. Gdy te strony są określane ponownie, hello przeglądarki zostaną wyświetlone z pamięci podręcznej. Jeśli informacje poufne jest wyświetlanych toohello użytkownika (na przykład ich adres karty kredytowej, numer ubezpieczenia społecznego albo nazwa użytkownika), a następnie tych informacji może być przechowywane w pamięci podręcznej przeglądarki i w związku z tym można odzyskać badanie pamięci podręcznej przeglądarki hello lub po prostu naciskając przycisk "Wstecz", hello przeglądarki. Wartość nagłówka cache-control odpowiedzi nagłówka zbyt "no-store" dla wszystkich stron. |

### <a name="example"></a>Przykład
```XML
<configuration>
  <system.webServer>
   <httpProtocol>
    <customHeaders>
        <add name="Cache-Control" value="no-cache" />
        <add name="Pragma" value="no-cache" />
        <add name="Expires" value="-1" />
    </customHeaders>
  </httpProtocol>
 </system.webServer>
</configuration>
```

### <a name="example"></a>Przykład
Mogą to być wykonywane przez filtr. Może służyć następujący przykład: 
```C#
public override void OnActionExecuting(ActionExecutingContext filterContext)
        {
            if (filterContext == null || (filterContext.HttpContext != null && filterContext.HttpContext.Response != null && filterContext.HttpContext.Response.IsRequestBeingRedirected))
            {
                //// Since this is MVC pipeline, this should never be null.
                return;
            }

            var attributes = filterContext.ActionDescriptor.GetCustomAttributes(typeof(System.Web.Mvc.OutputCacheAttribute), false);
            if (attributes == null || **Attributes**.Count() == 0)
            {
                filterContext.HttpContext.Response.Cache.SetNoStore();
                filterContext.HttpContext.Response.Cache.SetCacheability(HttpCacheability.NoCache);
                filterContext.HttpContext.Response.Cache.SetExpires(DateTime.UtcNow.AddHours(-1));
                if (!filterContext.IsChildAction)
                {
                    filterContext.HttpContext.Response.AppendHeader("Pragma", "no-cache");
                }
            }

            base.OnActionExecuting(filterContext);
        }
``` 

## <a id="encrypt-data"></a>Szyfrowanie sekcji pliki konfiguracji aplikacji sieci Web, które zawierają dane poufne

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Porady: Szyfrowanie sekcji konfiguracyjnych w DPAPI za pomocą programu ASP.NET 2.0](https://msdn.microsoft.com/library/ff647398.aspx), [określenie dostawcę konfiguracji chronione](https://msdn.microsoft.com/library/68ze1hb2.aspx), [klucze tajne aplikacji tooprotect przy użyciu usługi Azure Key Vault](https://azure.microsoft.com/documentation/articles/guidance-multitenant-identity-keyvault/) |
| **Kroki** | Pliki konfiguracji, takich jak hello Web.config, appsettings.json są często używane toohold informacji poufnych, w tym nazwy użytkownika, hasła, parametry połączenia bazy danych i kluczy szyfrowania. Jeśli nie będzie chronić te informacje, aplikacja jest narażony tooattackers lub złośliwym użytkownikom uzyskania poufne informacje, takie jak nazwy kont i hasła, nazwy bazy danych i nazwy serwera. Oparte na powitania typ wdrożenia (azure/lokalnego), szyfrowanie hello poufnych sekcjami plików konfiguracji przy użyciu DPAPI lub usługi, takie jak usługi Azure Key Vault. |

## <a id="autocomplete-input"></a>Jawnie Wyłącz atrybutu HTML autouzupełniania hello w formularzach poufnych i dane wejściowe

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [MSDN: atrybut autocomplete](http://msdn.microsoft.com/library/ms533486(VS.85).aspx), [przy użyciu funkcji AutoComplete w formacie HTML](http://msdn.microsoft.com/library/ms533032.aspx), [luki w zabezpieczeniach ich oczyszczania HTML](http://technet.microsoft.com/security/bulletin/MS10-071), [Autocomplete., ponownie?](http://blog.mindedsecurity.com/2011/10/autocompleteagain.html) |
| **Kroki** | Atrybut autocomplete Hello Określa, czy formularza powinien mieć autouzupełniania lub wyłączyć. Po włączeniu funkcji autocomplete wartości automatycznie wykonania przeglądarki hello na podstawie wartości tego hello użytkownik wprowadził przed. Na przykład po wprowadzeniu nowej nazwy i hasła w postaci i przesłaniu formularza hello, przeglądarki hello pyta hello hasło ma zostać zapisany. Później, gdy zostanie wyświetlony formularz hello, hello nazwę i hasło są wypełniane automatycznie lub zakończeniu wprowadzoną hello nazwy. Osoba atakująca z dostępem do lokalnego może uzyskać hasła nieszyfrowanego hello z pamięci podręcznej przeglądarki hello. Funkcji autocomplete jest domyślnie włączona, a musi jawnie wyłączone. |

### <a name="example"></a>Przykład
```C#
<form action="Login.aspx" method="post " autocomplete="off" >
      Social Security Number: <input type="text" name="ssn" />
      <input type="submit" value="Submit" />    
</form>
```

## <a id="data-mask"></a>Upewnij się, że poufne dane wyświetlane na ekranie użytkownika hello są wyświetlane jako znaki

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Dane poufne, takie jak hasła, numery kart kredytowych, itp. SSN powinien maskowane, gdy wyświetlany na ekranie powitania. Jest to personel tooprevent nieautoryzowany dostęp do danych hello (np. hasła ramię przeglądanie, pomocy technicznej wyświetlanie SSN liczby użytkowników). Upewnij się, że te elementy danych nie są widoczne w postaci zwykłego tekstu i odpowiednio są ukryte. To ustawienie toobe podjęte ostrożność podczas akceptowania ich jako danych wejściowych (np.. wprowadzania type = "password") oraz wyświetlanie wstecz na ekranie powitania (np. wyświetlania tylko hello 4 ostatnie cyfry numeru karty kredytowej hello). |

## <a id="dynamic-users"></a>Implementowanie użytkowników maskowania ujawnienie danych poufnych toolimit z systemem innym niż uprzywilejowany danych dynamicznych

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Database (Baza danych) | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Lokalnego programu SQL Azure |
| **Atrybuty**              | MsSQL2016 wersji — w wersji 12, wersja programu SQL — SQL |
| **Odwołania**              | [Maskowanie danych dynamicznych](https://msdn.microsoft.com/library/mt130841) |
| **Kroki** | Celem Hello dynamicznego maskowania danych jest toolimit ujawnianie danych wrażliwych, co uniemożliwia użytkownikom, którzy nie powinni mieć dostęp do danych toohello go wyświetlać. Nie ma na celu tooprevent bazy danych użytkownikom bezpośrednie łączenie toohello bazy danych i uruchamiania wyczerpujący zapytań, które udostępniają fragmentów danych poufnych hello maskowania danych dynamicznych. Maskowanie danych dynamicznych jest tooother uzupełniające się funkcje zabezpieczeń programu SQL Server (inspekcji, szyfrowania, zabezpieczeń na poziomie wiersza...) i zdecydowanie zaleca się toouse tę funkcję w połączeniu z nimi również w kolejności toobetter chronią poufne dane hello w hello Baza danych. Należy pamiętać, że ta funkcja jest obsługiwana tylko przez program SQL Server w programie 2016 i bazy danych SQL Azure. |

## <a id="salted-hash"></a>Upewnij się, że hasła są przechowywane w formacie solone wyznaczania wartości skrótu

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Database (Baza danych) | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Hashing hasła przy użyciu interfejsów API architektury .NET kryptograficznego](http://docs.asp.net/en/latest/security/data-protection/consumer-apis/password-hashing.html) |
| **Kroki** | Hasła nie powinny być przechowywane w magazynie użytkownika niestandardowego w bazach danych. Hasła powinny być przechowywane wartości zaburzającej zamiast tego. Upewnij się, hello soli dla użytkownika hello jest zawsze unikatowa i zastosować b-crypt, s-crypt lub PBKDF2 przed przechowywanie hello hasła, minimalną pracy współczynnik iteracji liczba 150 000 pętli tooeliminate hello możliwości ukierunkowany wymuszania.| 

## <a id="db-encrypted"></a>Upewnij się, że poufne dane w kolumnach bazy danych są szyfrowane

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Database (Baza danych) | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Wersja programu SQL — wszystkie |
| **Odwołania**              | [Szyfrowania poufnych danych w programie SQL server](https://technet.microsoft.com/library/ff848751(v=sql.105).aspx), [porady: szyfrowanie kolumny danych w programie SQL Server](https://msdn.microsoft.com/library/ms179331), [Szyfruj certyfikatu](https://msdn.microsoft.com/library/ms188061) |
| **Kroki** | Dane poufne, takie jak numer karty kredytowej ma toobe szyfrowane w hello bazy danych. Dane mogą być szyfrowane za pomocą szyfrowania na poziomie kolumny lub funkcję aplikacji przy użyciu funkcji szyfrowania hello. |

## <a id="tde-enabled"></a>Upewnij się, że włączone jest szyfrowanie tej bazy danych na poziomie (funkcji TDE)

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Database (Baza danych) | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Opis programu SQL Server przezroczystego szyfrowania danych (funkcji TDE)](https://technet.microsoft.com/library/bb934049(v=sql.105).aspx) |
| **Kroki** | Funkcji przezroczystego szyfrowania danych (TDE) funkcji programu SQL server pomaga w szyfrowania poufnych danych w bazie danych i ochronę kluczy hello, które są używane tooencrypt hello danych przy użyciu certyfikatu. Zapobiega to osobom niemającym hello kluczy przy użyciu hello danych. Funkcji TDE chroni dane "magazynowane", co oznacza hello plików danych i dziennika. Zapewnia toocomply możliwości hello z wielu ustawowych, wykonawczych i wskazówkami w różnych branżach. |

## <a id="backup"></a>Upewnij się, że kopie zapasowe bazy danych są szyfrowane.

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Database (Baza danych) | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Lokalnego programu SQL Azure |
| **Atrybuty**              | MsSQL2014 wersji — w wersji 12, wersja programu SQL — SQL |
| **Odwołania**              | [Szyfrowanie kopii zapasowej bazy danych SQL](https://msdn.microsoft.com/library/dn449489) |
| **Kroki** | Serwer SQL ma hello możliwości tooencrypt hello danych podczas tworzenia kopii zapasowej. Określając hello algorytm szyfrowania i szyfrujący hello (certyfikatu lub klucza asymetrycznego) podczas tworzenia kopii zapasowej, można utworzyć zaszyfrowanego pliku kopii zapasowej. |

## <a id="api-browser"></a>Upewnij się, tym tooWeb odpowiednich danych poufnych, interfejsu API nie jest przechowywane w magazynie w przeglądarce

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Interfejs API sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | MVC 5, 6 MVC |
| **Atrybuty**              | Dostawca tożsamości dostawca — usługi AD FS, tożsamość — usługi Azure AD |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | <p>W niektórych implementacjach poufnych artefaktów tooWeb odpowiedniego interfejsu API uwierzytelniania są przechowywane w magazynie lokalnym w przeglądarce. Np. artefakty uwierzytelniania usługi Azure AD, takich jak adal.idtoken, adal.nonce.idtoken, adal.access.token.key, adal.token.keys, adal.state.login, adal.session.state, adal.expiration.key itp.</p><p>Wszystkie te artefakty są dostępne nawet po zakończeniu Wyloguj lub zamknięcie okna przeglądarki. Jeśli atakujący dokonuje uzyskuje dostęp artefakty toothese, jego późniejszego tooaccess hello chronione zasoby (API). Upewnij się, że wszystkich poufnych artefaktów pokrewne tooWeb interfejsu API nie są przechowywane w magazynie w przeglądarce. W przypadkach, gdy niezbędne jest magazynu po stronie klienta (np. jednej strony aplikacji JEDNOSTRONICOWEJ zwiększają przepływów niejawne OpenIdConnect/OAuth konieczne toostore tokenów dostępu lokalnie), użyj opcji magazynu z braku trwałości. np. preferowane SessionStorage tooLocalStorage.</p>| 

### <a name="example"></a>Przykład
Witaj poniższego fragmentu kodu JavaScript jest z biblioteki uwierzytelniania niestandardowego, której są przechowywane artefakty uwierzytelniania w magazynie lokalnym. Należy unikać takich implementacji. 
```javascript
ns.AuthHelper.Authenticate = function () {
window.config = {
instance: 'https://login.microsoftonline.com/',
tenant: ns.Configurations.Tenant,
clientId: ns.Configurations.AADApplicationClientID,
postLogoutRedirectUri: window.location.origin,
cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
};
```

## <a id="encrypt-docdb"></a>Szyfrowania poufnych danych przechowywanych w bazie danych rozwiązania Cosmos

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Dokumentów w usłudze Azure DB | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Szyfrowania poufnych danych na poziomie aplikacji przed przekazaniem dokumentu bazy danych lub przechowywać żadnych poufnych danych w innych rozwiązań pamięci masowej, takich jak usługi Azure Storage lub Azure SQL| 

## <a id="disk-vm"></a>Używać szyfrowania dysków Azure tooencrypt dysków używanych przez maszyny wirtualne

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Maszyna wirtualna platformy Azure IaaS granicy zaufania | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Przy użyciu szyfrowania dysków Azure dysków tooencrypt używany przez maszyny wirtualne](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines) |
| **Kroki** | <p>Szyfrowanie dysków Azure to nowa funkcja, która jest obecnie w przeglądzie. Ta funkcja umożliwia dysków systemu operacyjnego hello tooencrypt i dysków danych używanych przez maszyny wirtualne IaaS. W systemie Windows hello dyski są szyfrowane za pomocą technologii szyfrowania BitLocker standardowych. Dla systemu Linux dyski hello są szyfrowane za pomocą technologii hello DM-Crypt. To jest zintegrowany z usługą Azure Key Vault tooallow możesz toocontrol i zarządzać kluczami szyfrowania dysku hello. Witaj rozwiązania szyfrowania dysków Azure obsługuje hello następujących trzech scenariuszy szyfrowania:</p><ul><li>Włącz szyfrowanie dla nowych maszyn wirtualnych IaaS utworzone na podstawie szyfrowane przez klienta plików VHD i kluczy szyfrowania klienta, które są przechowywane w usłudze Azure Key Vault.</li><li>Włącz szyfrowanie dla nowych maszyn wirtualnych IaaS utworzone na podstawie hello Azure Marketplace.</li><li>Włącz szyfrowanie dla istniejących maszyn wirtualnych IaaS już uruchomione na platformie Azure.</li></ul>| 

## <a id="fabric-apps"></a>Szyfrowanie kluczy tajnych w aplikacji sieci szkieletowej usług

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Granic zaufania sieci szkieletowej usług | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Środowisko — Azure |
| **Odwołania**              | [Zarządzanie kluczy tajnych w aplikacji sieci szkieletowej usług](https://azure.microsoft.com/documentation/articles/service-fabric-application-secret-management/) |
| **Kroki** | Klucze tajne można poufne informacje, takie jak parametry połączenia magazynu, hasła lub inne wartości, które nie powinny być traktowane w postaci zwykłego tekstu. Użyj usługi Azure Key Vault toomanage kluczy i kluczy tajnych w aplikacji sieci szkieletowej usług. |

## <a id="modeling-teams"></a>Wykonaj modelowania zabezpieczeń i użyć zespołów jednostki biznesowe w przypadku, gdy wymagane

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Dynamics CRM | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Wykonaj modelowania zabezpieczeń i użyć zespołów jednostki biznesowe w przypadku, gdy wymagane |

## <a id="entities"></a>Minimalizowanie funkcja tooshare dostępu na jednostkach krytyczne

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Dynamics CRM | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Minimalizowanie funkcja tooshare dostępu na jednostkach krytyczne |

## <a id="good-practices"></a>Użytkownicy pociągu na powitania ryzyko związane z hello Dynamics CRM udziału funkcji i rozwiązań dobrze chroniony

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Dynamics CRM | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Użytkownicy pociągu na powitania ryzyko związane z hello Dynamics CRM udziału funkcji i rozwiązań dobrze chroniony |

## <a id="exception-mgmt"></a>Programowanie regułę standardy, proscribing konfiguracji ze szczegółowymi informacjami w Zarządzanie wyjątkami dołączania

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Dynamics CRM | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Obejmują reguły standardów programowanie proscribing konfiguracji ze szczegółowymi informacjami w Zarządzanie wyjątkami poza programowanie. Testowanie jako część przeglądy kodu lub okresowy.|

## <a id="sse-preview"></a>Użyj szyfrowanie usługi Magazyn Azure (SSE) dla danych magazynowanych (wersja zapoznawcza)

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Azure Storage | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | StorageType — obiekt Blob |
| **Odwołania**              | [Szyfrowanie usługi Magazyn Azure dla danych magazynowanych (wersja zapoznawcza)](https://azure.microsoft.com/documentation/articles/storage-service-encryption/) |
| **Kroki** | <p>Azure magazynu usługi szyfrowania (SSE) dla danych magazynowanych pomaga chronić i chronić Twoje toomeet danych organizacji bezpieczeństwa i zgodności zobowiązań. Przy użyciu tej funkcji usługi Azure Storage automatycznie szyfruje toostorage wcześniejsze toopersisting Twojego danych i odszyfrowuje tooretrieval wcześniejszych. Witaj szyfrowania, odszyfrowywania i klucz zarządzania toousers całkowicie przezroczysty. SSE stosuje tylko tooblock obiektów blob, stronicowe obiekty BLOB i uzupełnialnych obiektów blob. Witaj innych typów danych, w tym tabel, kolejek i plików, nie będą szyfrowane.</p><p>Szyfrowanie i odszyfrowywanie przepływu pracy:</p><ul><li>powitania klienta włącza szyfrowanie na powitania konta magazynu</li><li>Gdy powitania klienta zapisuje nowego magazynu tooBlob danych (umieszczanie obiektu Blob, umieść bloku, umieść stronę itp.); każdego zapisu jest szyfrowana przy użyciu szyfrowania AES 256-bitowego, jeden hello najwyższy bloku szyfrów dostępne</li><li>Gdy powitania klienta wymaga danych tooaccess (Pobierz obiekt Blob itp.), dane są automatycznie odszyfrowane przed zwróceniem toohello użytkownika</li><li>Jeśli szyfrowanie jest wyłączone, nowe zapisy nie są szyfrowane i zaszyfrowane dane pozostaną zaszyfrowane, dopóki nowy tekst hello użytkownika. Gdy włączone jest szyfrowanie, będą szyfrowane zapisy tooBlob magazynu. Stan Hello danych nie zmienia się z użytkownikiem hello przełączania się między włączenie/wyłączenie szyfrowania dla konta magazynu hello</li><li>Wszystkie klucze szyfrowania są przechowywane, szyfrowane i zarządzany przez firmę Microsoft</li></ul><p>Należy pamiętać, że w tej chwili hello klucze szyfrowania hello są zarządzane przez firmę Microsoft. Firma Microsoft generuje klucze hello pierwotnie i zarządzanie hello bezpiecznego magazynu kluczy hello, a także regularne obrotu hello zgodnie z definicją w wewnętrznych zasad firmy Microsoft. W przyszłości hello, klienci otrzymają toomanage możliwości hello własnych > klucze szyfrowania i podaj ścieżkę migracji z kluczy zarządzany przez firmę Microsoft toocustomer zarządzanych kluczy.</p>| 

## <a id="client-storage"></a>Użyj szyfrowania po stronie klienta toostore poufnych danych w usłudze Azure Storage

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Azure Storage | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Szyfrowanie po stronie klienta i usługi Azure Key Vault dla magazynu Microsoft Azure](https://azure.microsoft.com/documentation/articles/storage-client-side-encryption/), [samouczek: szyfrowanie i odszyfrowywanie obiektów blob w magazynie platformy Microsoft Azure przy użyciu usługi Azure Key Vault](https://azure.microsoft.com/documentation/articles/storage-encrypt-decrypt-blobs-key-vault/), [bezpieczne przechowywanie danych w magazynie obiektów Blob Azure z rozszerzeniami szyfrowania Azure](https://blogs.msdn.microsoft.com/partnercatalystteam/2015/06/17/storing-data-securely-in-azure-blob-storage-with-azure-encryption-extensions/) |
| **Kroki** | <p>Witaj biblioteki klienta magazynu Azure dla pakietu Nuget programu .NET obsługuje szyfrowanie danych w aplikacjach klienckich przed przekazaniem tooAzure magazynu i odszyfrowywania danych podczas pobierania toohello klienta. Biblioteka Hello obsługuje również integrację z usługą Azure Key Vault do zarządzania kluczami konta magazynu. Poniżej przedstawiono krótki opis działania szyfrowania po stronie klienta:</p><ul><li>powitania klienta usługi Azure Storage SDK generuje klucz szyfrowania zawartości (CEK), jest jeden jednorazowej użycia klucza symetrycznego</li><li>Dane klienta są zaszyfrowane za pomocą tego CEK</li><li>Witaj CEK jest następnie opakowane (zaszyfrowane) przy użyciu hello klucza szyfrowania klucza (KEK). Hello KEK jest identyfikowany przez identyfikator klucza i można parę klucza asymetrycznego lub klucza symetrycznego i może być zarządzane lokalnie lub przechowywane w usłudze Azure Key Vault. Witaj magazynu klienta nigdy nie ma dostępu toohello KEK. Wywołuje po prostu algorytm klucza zawijania hello są udostępniane przez usługi Key Vault. Klienci mogą wybrać toouse niestandardowych dostawców dla zawijania/odkodowywania chcący klucza</li><li>Witaj zaszyfrowane dane są następnie przekazywane toohello usługi Magazyn Azure. Sprawdź hello łącza w sekcji odwołań hello szczegółów niskiego poziomu wdrożenia.</li></ul>|

## <a id="pii-phones"></a>Szyfrowanie liter lub dane osobowe danymi zapisywanymi toophones lokalnego magazynu

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Klientów urządzeń przenośnych | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny, Xamarin  |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Zarządzanie ustawieniami i funkcjami na urządzeniach przy użyciu zasad usługi Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/manage-settings-and-features-on-your-devices-with-microsoft-intune-policies#create-a-configuration-policy), [Valet łańcucha kluczy](https://components.xamarin.com/view/square.valet) |
| **Kroki** | <p>Jeśli aplikacja hello zapisuje informacje poufne, na przykład PII użytkownika (poczty e-mail, numer telefonu, imię, nazwisko, preferencje itp.) — w systemie plików na telefon komórkowy, następnie go powinny być szyfrowane przed zapisaniem toohello lokalnego systemu plików. Jeśli aplikacja hello jest aplikacja przedsiębiorstwa, skorzystaj z możliwości hello publikowania aplikacji za pomocą usługi Windows Intune.</p>|

### <a name="example"></a>Przykład
Usługa Intune można skonfigurować za pomocą następujących zabezpieczeń zasady toosafeguard danych poufnych: 
```C#
Require encryption on mobile device    
Require encryption on storage cards
Allow screen capture
```

### <a name="example"></a>Przykład
Jeśli aplikacja hello nie jest aplikacją, a następnie użyj platformy podane magazynu kluczy, kluczy szyfrowania toostore pęki kluczy, przy użyciu których operacji kryptograficznych może być wykonana na powitania w systemie plików. Następujący kod fragment kodu przedstawia, jak tooaccess klucza z łańcucha kluczy za pomocą platformy xamarin: 
```C#
        protected static string EncryptionKey
        {
            get
            {
                if (String.IsNullOrEmpty(_Key))
                {
                    var query = new SecRecord(SecKind.GenericPassword);
                    query.Service = NSBundle.MainBundle.BundleIdentifier;
                    query.Account = "UniqueID";

                    NSData uniqueId = SecKeyChain.QueryAsData(query);
                    if (uniqueId == null)
                    {
                        query.ValueData = NSData.FromString(System.Guid.NewGuid().ToString());
                        var err = SecKeyChain.Add(query);
                        _Key = query.ValueData.ToString();
                    }
                    else
                    {
                        _Key = uniqueId.ToString();
                    }
                }

                return _Key;
            }
        }
```

## <a id="binaries-end"></a>Zasłaniają wygenerowanych plików binarnych przed rozpoczęciem dystrybuowania tooend użytkowników

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Klientów urządzeń przenośnych | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Zaciemnienie kryptograficznych dla platformy .net](http://www.ssware.com/cryptoobfuscator/obfuscator-net.htm) |
| **Kroki** | Wygenerowane dane binarne (zestawy w apk) powinna być zaciemnionego toostop odtwarzania zestawów. Narzędzi, takich jak `CryptoObfuscator` mogą być używane w tym celu. |

## <a id="cert"></a>Ustaw właściwość clientCredentialType tooCertificate lub systemu Windows

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | WCF | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | .NET framework 3 |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Uzyskania zawartości](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Kroki** | Przy użyciu UsernameToken za pomocą hasła w postaci zwykłego tekstu przez kanał niezaszyfrowany przedstawia hello tooattackers hasła, który można wyśledzić wiadomości powitania od protokołu SOAP. Dostawcy usług, używanego hello UsernameToken może zaakceptować wysyłania haseł w postaci zwykłego tekstu. Wysyłanie hasła w postaci zwykłego tekstu przez kanał niezaszyfrowany mogą uwidaczniać hello tooattackers poświadczeń, który można wyśledzić komunikatu protokołu SOAP hello. | 

### <a name="example"></a>Przykład
Witaj następującej konfiguracji dostawcy usług WCF używa hello UsernameToken: 
```
<security mode="Message"> 
<message clientCredentialType="UserName" />
``` 
Ustaw właściwość clientCredentialType tooCertificate lub systemu Windows. 

## <a id="security"></a>Nie jest włączony tryb zabezpieczeń programu WCF

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | WCF | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny, .NET Framework 3 |
| **Atrybuty**              | Zabezpieczenia trybu — transportu, trybu zabezpieczeń — komunikat |
| **Odwołania**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [uzyskania zawartości Królestwo](https://vulncat.fortify.com/en/vulncat/index.html), [Magazine kodu podstawowe informacje na temat zabezpieczeń programu WCF](http://www.codemag.com/article/0611051) |
| **Kroki** | Brak zabezpieczeń transportu lub komunikat został zdefiniowany. Aplikacje, które przesyłania komunikatów zabezpieczeń nie może zagwarantować hello integralności i poufności wiadomości powitania lub wiadomości bez transportu. Powiązanie zabezpieczeń WCF ustawiono tooNone, zabezpieczenia transportowe i wiadomości są wyłączone. |

### <a name="example"></a>Przykład
Witaj następujących zestawów konfiguracyjnych tooNone tryb zabezpieczeń hello. 
```
<system.serviceModel> 
  <bindings> 
    <wsHttpBinding> 
      <binding name=""MyBinding""> 
        <security mode=""None""/> 
      </binding> 
  </bindings> 
</system.serviceModel> 
```

### <a name="example"></a>Przykład
Tryb zabezpieczeń we wszystkich powiązań usługi są pięć tryby możliwe zabezpieczeń: 
* Brak. Wyłącza zabezpieczeń. 
* Transport. Używa transportu zabezpieczeń do wzajemnego uwierzytelniania i komunikat ochrony. 
* Komunikat. Używa zabezpieczeń wiadomości do wzajemnego uwierzytelniania i komunikat ochrony. 
* Oba. Umożliwia toosupply ustawienia dla transportu i zabezpieczenia na poziomie komunikatu (tylko usługi MSMQ obsługuje tę funkcję). 
* TransportWithMessageCredential. Poświadczenia są przekazywane z wiadomość hello i ochrony wiadomości i uwierzytelniania serwera są udostępniane przez warstwę transportu hello. 
* TransportCredentialOnly. Poświadczenia klienta są przekazywane z warstwy transportowej hello i stosowane jest Brak ochrony wiadomości. Użyj transportu i komunikat integralność hello tooprotect zabezpieczeń i poufności informacji. Konfiguracja Hello poniżej informuje hello usługi toouse TLS z poświadczeniami komunikatu.
```
<system.serviceModel>
  <bindings>
    <wsHttpBinding>
    <binding name=""MyBinding""> 
    <security mode=""TransportWithMessageCredential""/> 
    <message clientCredentialType=""Windows""/> 
    </binding> 
  </bindings> 
</system.serviceModel> 
```
