---
title: "aaaCommunication zabezpieczeń — narzędzie modelowania zagrożeń Microsoft - Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 667829c75123f4dbe0b383fdaf8cd899802f9b16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-communication-security--mitigations"></a>Ramka zabezpieczeń: Zabezpieczenia komunikacji | Środki zaradcze 
| Produktów i usług | Artykuł |
| --------------- | ------- |
| **Centrum zdarzeń platformy Azure** | <ul><li>[Bezpieczna komunikacja tooEvent Centrum przy użyciu protokołu SSL/TLS](#comm-ssltls)</li></ul> |
| **Dynamics CRM** | <ul><li>[Sprawdź uprawnienia i sprawdź, czy hello niestandardowych stron ASP.NET lub usługi przestrzegać CRM zabezpieczeń konta usługi](#priv-aspnet)</li></ul> |
| **Azure Data Factory** | <ul><li>[Użyj bramy zarządzania danymi podczas tooAzure na serwerze SQL — wersja Premium łączenia usługi fabryka danych](#sqlserver-factory)</li></ul> |
| **Tożsamości serwera** | <ul><li>[Upewnij się, że wszystkie tooIdentity ruchu serwera jest za pośrednictwem połączenia HTTPS](#identity-https)</li></ul> |
| **Aplikacja sieci Web** | <ul><li>[Sprawdź, czy połączenia SSL, TLS i DTLS tooauthenticate używane certyfikaty X.509](#x509-ssltls)</li><li>[Konfigurowanie certyfikatu SSL dla domen niestandardowych w usłudze Azure App Service](#ssl-appservice)</li><li>[Wymuś wszystkich tooAzure ruchu usługi App Service za pośrednictwem połączenia HTTPS](#appservice-https)</li><li>[Włącz zabezpieczenie Strict transportu HTTP (HSTS)](#http-hsts)</li></ul> |
| **Baza danych** | <ul><li>[Upewnij się, SQL server szyfrowania i certyfikatu sprawdzania poprawności połączenia](#sqlserver-validation)</li><li>[Wymuś zaszyfrowana komunikacja tooSQL serwera](#encrypted-sqlserver)</li></ul> |
| **Azure Storage** | <ul><li>[Upewnij się, że tooAzure komunikacji, jest magazynu za pośrednictwem protokołu HTTPS](#comm-storage)</li><li>[Sprawdzenie skrótu MD5 po pobraniu obiektów blob, jeśli nie można włączyć protokołu HTTPS](#md5-https)</li><li>[Użyj protokołu SMB 3.0 zgodny klient tooensure podczas przesyłania tooAzure szyfrowania danych udziałów plików](#smb-shares)</li></ul> |
| **Klientów urządzeń przenośnych** | <ul><li>[Implementowanie funkcji przypinania certyfikatu](#cert-pinning)</li></ul> |
| **WCF** | <ul><li>[Włącz protokół HTTPS - bezpieczny kanał transportu](#https-transport)</li><li>[WCF: TooEncryptAndSign poziomu ochrony zabezpieczeń zestawu wiadomości](#message-protection)</li><li>[Usługi WCF: Użyj toorun najmniej uprzywilejowane konto usługi WCF](#least-account-wcf)</li></ul> |
| **Interfejs API sieci Web** | <ul><li>[Wymuś wszystkich tooWeb ruchu interfejsów API za pośrednictwem połączenia HTTPS](#webapi-https)</li></ul> |
| **Azure Redis Cache** | <ul><li>[Upewnij się, że tooAzure komunikacji, jest pamięcią podręczną Redis za pośrednictwem protokołu SSL](#redis-ssl)</li></ul> |
| **Pole IoT bramy** | <ul><li>[Bezpieczna komunikacja bramy tooField urządzenia](#device-field)</li></ul> |
| **Brama chmury IoT** | <ul><li>[Zabezpieczanie tooCloud urządzenia bramy komunikacji przy użyciu protokołu SSL/TLS](#device-cloud)</li></ul> |

## <a id="comm-ssltls"></a>Bezpieczna komunikacja tooEvent Centrum przy użyciu protokołu SSL/TLS

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Centrum zdarzeń platformy Azure | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Uwierzytelnianie i zabezpieczenia modelu Omówienie usługi Event Hubs](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Kroki** | Secure HTTP lub protokołu AMQP tooEvent połączenia koncentratora, za pomocą protokołu SSL/TLS |

## <a id="priv-aspnet"></a>Sprawdź uprawnienia i sprawdź, czy hello niestandardowych stron ASP.NET lub usługi przestrzegać CRM zabezpieczeń konta usługi

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Dynamics CRM | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Sprawdź uprawnienia i sprawdź, czy hello niestandardowych stron ASP.NET lub usługi przestrzegać CRM zabezpieczeń konta usługi |

## <a id="sqlserver-factory"></a>Użyj bramy zarządzania danymi podczas tooAzure na serwerze SQL — wersja Premium łączenia usługi fabryka danych

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Azure Data Factory | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Typy połączonych usług - Azure i lokalnej |
| **Odwołania**              |[Przenoszenie danych między o lokalnej i fabryki danych Azure](https://azure.microsoft.com/documentation/articles/data-factory-move-data-between-onprem-and-cloud/#create-gateway), [brama zarządzania danymi](https://azure.microsoft.com/documentation/articles/data-factory-data-management-gateway/) |
| **Kroki** | <p>Narzędzie danych zarządzania bramy (DMG) Hello jest wymagana tooconnect toodata źródeł, które są chronione za corpnet lub zaporą.</p><ol><li>Blokowanie maszynę hello izoluje hello DMG narzędzia i uniemożliwia nieprawidłowo programy z uszkodzenia lub śledzenie na maszynie źródłowej hello danych. (Np. musi być zainstalowane najnowsze aktualizacje, Włącz minimalne wymagane porty, kontrolowanego kont inicjowania obsługi administracyjnej, inspekcji włączona, szyfrowanie dysków włączone itp.)</li><li>Klucz bramy danych jest obracana odstępach częste lub gdy hasło konta usługi DMG hello odnawia</li><li>Tranzytu danych za pośrednictwem łącza usługi musi być zaszyfrowany.</li></ol> |

## <a id="identity-https"></a>Upewnij się, że wszystkie tooIdentity ruchu serwera jest za pośrednictwem połączenia HTTPS

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Tożsamości serwera | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [IdentityServer3 - kluczy, podpisy i szyfrowania](https://identityserver.github.io/Documentation/docsv2/configuration/crypto.html), [IdentityServer3 — wdrożenia](https://identityserver.github.io/Documentation/docsv2/advanced/deployment.html) |
| **Kroki** | Domyślnie IdentityServer wymaga wszystkich toocome przychodzących połączeń za pośrednictwem protokołu HTTPS. Jest absolutnie obowiązkowe, że komunikacja z IdentityServer odbywa się za pośrednictwem tylko zabezpieczonych transportów. Brak niektórych scenariuszy wdrażania, takie jak odciążanie protokołu SSL gdzie to wymaganie można rozluźnić. Zobacz hello tożsamości serwera wdrażania strony w odwołaniach hello, aby uzyskać więcej informacji. |

## <a id="x509-ssltls"></a>Sprawdź, czy połączenia SSL, TLS i DTLS tooauthenticate używane certyfikaty X.509

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | <p>Certyfikaty X.509 hello hello jednostek, które łączą się z pełni należy sprawdzić, aplikacje używające protokołu SSL, TLS i DTLS. Obejmuje to weryfikacji hello certyfikatów dla:</p><ul><li>Nazwa domeny</li><li>Daty ważności (początku i na wygaśnięcie daty)</li><li>Stan odwołania</li><li>Sposób użycia (na przykład uwierzytelniania serwera dla serwerów, uwierzytelnianie klienta dla klientów)</li><li>Zaufania łańcucha. Certyfikaty muszą być powiązane tooa główny urząd certyfikacji (CA), który jest traktowany jako zaufany przez platformę hello lub jawnie skonfigurowane przez administratora hello</li><li>Długość klucza publicznego certyfikatu musi być > 2048 bitów</li><li>Algorytm wyznaczania wartości skrótu musi być SHA256 i powyżej. |

## <a id="ssl-appservice"></a>Konfigurowanie certyfikatu SSL dla domen niestandardowych w usłudze Azure App Service

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | EnvironmentType - Azure |
| **Odwołania**              | [Włącz protokół HTTPS dla aplikacji w usłudze aplikacji Azure](https://azure.microsoft.com/documentation/articles/web-sites-configure-ssl-certificate/) |
| **Kroki** | Domyślnie program Azure po już umożliwia HTTPS dla każdej aplikacji przy użyciu symboli wieloznacznych certyfikatu dla hello *. azurewebsites.net domeny. Jednakże, podobnie jak wszystkie domeny symboli wieloznacznych, nie jest należycie zabezpieczone za pomocą domeny niestandardowej z własnym certyfikatem [zobacz](https://casecurity.org/2014/02/26/pros-and-cons-of-single-domain-multi-domain-and-wildcard-certificates/). Zalecane jest tooenable protokołu SSL dla domeny niestandardowej hello będą uzyskiwać dostęp za pośrednictwem aplikacji hello wdrożony|

## <a id="appservice-https"></a>Wymuś wszystkich tooAzure ruchu usługi App Service za pośrednictwem połączenia HTTPS

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | EnvironmentType - Azure |
| **Odwołania**              | [Wymuszanie protokołu HTTPS z usługi aplikacji Azure] https://azure.microsoft.com/documentation/articles/web-sites-configure-ssl-certificate/#4-enforce-https-on-your-app) |
| **Kroki** | <p>Chociaż Azure umożliwia już HTTPS dla usług aplikacji Azure z certyfikatem symbolu wieloznacznego hello domeny *. azurewebsites.net, nie Wymuszaj HTTPS. Odwiedzający mogą nadal uzyskiwać dostęp do aplikacji hello przy użyciu protokołu HTTP, który może naruszyć bezpieczeństwo aplikacji hello i dlatego HTTPS ma toobe jawnie wymuszane. Aplikacje programu ASP.NET MVC, należy użyć hello [filtru RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) który wymusza niezabezpieczona toobe żądania HTTP wysyłane ponownie przy użyciu protokołu HTTPS.</p><p>Alternatywnie hello ponowne zapisywanie adresów URL moduł, który znajduje się w usłudze Azure App Service może być używane tooenforce HTTPS. Moduł ponowne zapisywanie adresów URL umożliwia deweloperzy toodefine reguł, które są stosowane tooincoming żądań przed żądań hello są przekazywane tooyour aplikacji. Ponowne zapisywanie adresów URL reguły są zdefiniowane w pliku web.config, przechowywane w katalogu głównym hello aplikacji hello</p>|

### <a name="example"></a>Przykład
Witaj poniżej przedstawiono przykład zawierający podstawowe reguły ponowne zapisywanie adresów URL, która wymusza cały ruch przychodzący toouse ruch protokołu HTTPS
```XML
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```
Ta zasada działa zwróciła kod stanu HTTP 301 (Stałe przekierowanie) po hello użytkownik zażąda strony przy użyciu protokołu HTTP. Hello 301 przekierowuje hello żądania toohello tego samego adresu URL jako obiekt odwiedzający hello wymagane, ale zastępuje hello HTTP część hello żądanie HTTPS. Na przykład HTTP://contoso.com będzie tooHTTPS://contoso.com przekierowane. 

## <a id="http-hsts"></a>Włącz zabezpieczenie Strict transportu HTTP (HSTS)

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Zabezpieczenia transportu Strict HTTP OWASP Ściągawka](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet) |
| **Kroki** | <p>Zabezpieczenia transportu HTTP ograniczeniami (HSTS) jest ulepszeniem opcjonalnych zabezpieczeń, określonym przez aplikację sieci web przy użyciu hello nagłówka odpowiedzi specjalnych. Kiedy obsługiwanej przeglądarki odbiera ten nagłówek przeglądarka uniemożliwi komunikację z są wysyłane za pośrednictwem protokołu HTTP toohello określonej domeny i zamiast tego wyśle cała komunikacja za pośrednictwem protokołu HTTPS. Uniemożliwia także kliknij HTTPS za pomocą monity w przeglądarkach.</p><p>tooimplement HSTS powitania po nagłówka odpowiedzi ma toobe skonfigurowana dla witryny sieci Web globalnie, kodu lub w pliku konfiguracyjnym. Strict —-TLS: maksymalny — wiek = 300; includeSubDomains HSTS adresy powitania po zagrożeniami:</p><ul><li>Użytkownik zakładki lub ręcznie typy http://example.com i jest atakująca man-in--middle tooa podmiotu: HSTS automatyczne przekierowanie tooHTTPS żądania HTTP dla domeny docelowej hello</li><li>Aplikacji, który jest zamierzone toobe czysto przypadkowo zawiera łącza HTTP lub HTTPS służy zawartości za pośrednictwem protokołu HTTP sieci Web: HSTS automatyczne przekierowanie tooHTTPS żądania HTTP dla domeny docelowej hello</li><li>Atakujący man-in--middle prób toointercept ruch od użytkownika ofiara przy użyciu nieprawidłowego certyfikatu i nadzieję hello użytkownika będzie akceptować zły certyfikat hello: HSTS nie zezwala na komunikat użytkownika toooverride hello nieprawidłowy certyfikat</li></ul>|

## <a id="sqlserver-validation"></a>Upewnij się, SQL server szyfrowania i certyfikatu sprawdzania poprawności połączenia

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Database (Baza danych) | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Usługi SQL Azure  |
| **Atrybuty**              | Wersja programu SQL — wersja 12 |
| **Odwołania**              | [Najlepsze rozwiązania dla pisma bezpiecznego parametry połączenia dla bazy danych SQL](http://social.technet.microsoft.com/wiki/contents/articles/2951.windows-azure-sql-database-connection-security.aspx#best) |
| **Kroki** | <p>Cała komunikacja między bazy danych SQL i aplikacją klienta są szyfrowane przy użyciu protokołu Secure Sockets Layer (SSL) przez cały czas. Baza danych SQL nie obsługuje połączeń niezaszyfrowanych. toovalidate certyfikatów przy użyciu kodu aplikacji lub narzędzi, jawnie żądania połączenia szyfrowanego i nie masz zaufania certyfikatów serwera hello. Jeśli z kodu aplikacji lub narzędzia połączenie szyfrowane nie jest żądanie, będzie nadal otrzymywał szyfrowanych połączeń</p><p>Jednak nie może zweryfikować certyfikaty serwera hello i w związku z tym będzie narażony zbyt atakami "man w środku hello". Ustaw toovalidate certyfikatów przy użyciu kodu aplikacji ADO.NET, `Encrypt=True` i `TrustServerCertificate=False` w parametrach połączenia hello bazy danych. Certyfikaty toovalidate przy użyciu programu SQL Server Management Studio, Otwórz okno dialogowe tooServer Connect hello. Kliknij przycisk połączenie Szyfruj na karcie właściwości połączenia hello</p>|

## <a id="encrypted-sqlserver"></a>Wymuś zaszyfrowana komunikacja tooSQL serwera

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Database (Baza danych) | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Lokalnego programu |
| **Atrybuty**              | MsSQL2014 wersji — MsSQL2012, wersja programu SQL — SQL wersja - MsSQL2016, SQL |
| **Odwołania**              | [Włącz połączenia szyfrowane toohello aparatu bazy danych](https://msdn.microsoft.com/library/ms191192)  |
| **Kroki** | Włączanie protokołu SSL szyfrowania zwiększa bezpieczeństwo hello danych przesyłanych w sieci między wystąpieniami programu SQL Server i aplikacji. |

## <a id="comm-storage"></a>Upewnij się, że tooAzure komunikacji, jest magazynu za pośrednictwem protokołu HTTPS

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Azure Storage | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Szyfrowanie na poziomie transportu usługi Azure Storage — przy użyciu protokołu HTTPS](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_encryption-in-transit) |
| **Kroki** | tooensure hello zabezpieczeń usługi Azure Storage danych podczas przesyłania, należy zawsze używać protokołu HTTPS hello podczas wywoływania hello interfejsów API REST lub uzyskiwanie dostępu do obiektów w magazynie. Ponadto sygnatury dostępu współdzielonego, które mogą być używane toodelegate dostępu tooAzure magazynu obiektów, obejmują toospecify opcji tego powitalne tylko protokołu HTTPS, można użyć w przypadku przy użyciu sygnatury dostępu współdzielonego, zapewniając każdy wysyłaniu łącza o tokeny sygnatury dostępu Współdzielonego zostanie Użyj hello odpowiedni protokół.|

## <a id="md5-https"></a>Sprawdzenie skrótu MD5 po pobraniu obiektów blob, jeśli nie można włączyć protokołu HTTPS

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Azure Storage | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | StorageType — obiekt Blob |
| **Odwołania**              | [Omówienie MD5 obiektów Blob platformy Azure dla systemu Windows](https://blogs.msdn.microsoft.com/windowsazurestorage/2011/02/17/windows-azure-blob-md5-overview/) |
| **Kroki** | <p>Usługa Windows Azure Blob zapewnia integralność danych tooensure mechanizmów zarówno w aplikacji hello i warstwy transportu. Jeśli z jakiegokolwiek powodu potrzebne toouse HTTP zamiast HTTPS, a użytkownik pracuje z blokowych obiektów blob, można użyć sprawdzanie MD5 toohelp Sprawdź spójność hello obiektów blob hello przesyłania</p><p>Pomoże to ochrony z sieci/transport layer błędów, ale niekoniecznie pośredniczące ataków. Jeśli używasz protokołu HTTPS, który zapewnia zabezpieczeń na poziomie transportu, następnie przy użyciu algorytmu MD5 sprawdzanie jest nadmiarowe i niepotrzebne.</p>|

## <a id="smb-shares"></a>Użyj systemu protokołu SMB 3.0 zgodny klient tooensure danych podczas przesyłania szyfrowania tooAzure który udziałów plików

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Klientów urządzeń przenośnych | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | StorageType — plik |
| **Odwołania**              | [Magazyn plików Azure](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/#comment-2529238931), [plików na platformę Azure magazynu SMB obsługę klientów systemu Windows](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/#_mount-the-file-share) |
| **Kroki** | Magazyn plików Azure obsługuje protokołu HTTPS, używając hello interfejsu API REST, ale jest najczęściej używany jako udział plików SMB dołączony tooa maszyny Wirtualnej. Protokół SMB 2.1 nie obsługuje szyfrowania, więc połączeń są dozwolone jedynie w ramach hello sam region platformy Azure. Jednak protokół SMB 3.0 obsługuje szyfrowanie i może być używany z systemem Windows Server 2012 R2, Windows 8, Windows 8.1 i Windows 10, umożliwiając między region dostępu, a nawet dostępu na pulpicie hello. |

## <a id="cert-pinning"></a>Implementowanie funkcji przypinania certyfikatu

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Azure Storage | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny, Windows Phone |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Certyfikat i przypinanie klucza publicznego](https://www.owasp.org/index.php/Certificate_and_Public_Key_Pinning#.Net) |
| **Kroki** | <p>Przypinanie certyfikatu defends przed atakami typu Man-In--Middle (MITM). Przypinanie jest proces hello kojarzenie hosta z ich oczekiwanej X509 certyfikatu lub klucza publicznego. Po certyfikatu lub klucza publicznego jest znana lub widoczny dla hosta, hello certyfikatu lub klucza publicznego jest skojarzony lub "przypiętych" toohello hosta. </p><p>W związku z tym gdy atakujący dokonuje próbuje toodo ataki MITM protokołu SSL podczas klucza hello Uzgadnianie SSL od osoby atakującej serwera będzie inny niż hello przypięty klucza certyfikatu i zostaną odrzucone żądania hello, uniemożliwiający certyfikatu MITM przypinanie można osiągnąć przez Implementowanie przez element ServicePointManager `ServerCertificateValidationCallback` delegowanie.</p>|

### <a name="example"></a>Przykład
```C#
using System;
using System.Net;
using System.Net.Security;
using System.Security.Cryptography;

namespace CertificatePinningExample
{
    class CertificatePinningExample
    {
        /* Note: In this example, we're hardcoding a hello certificate's public key and algorithm for 
           demonstration purposes. In a real-world application, this should be stored in a secure
           configuration area that can be updated as needed. */

        private static readonly string PINNED_ALGORITHM = "RSA";

        private static readonly string PINNED_PUBLIC_KEY = "3082010A0282010100B0E75B7CBE56D31658EF79B3A1" +
            "294D506A88DFCDD603F6EF15E7F5BCBDF32291EC50B2B82BA158E905FE6A83EE044A48258B07FAC3D6356AF09B2" +
            "3EDAB15D00507B70DB08DB9A20C7D1201417B3071A346D663A241061C151B6EC5B5B4ECCCDCDBEA24F051962809" +
            "FEC499BF2D093C06E3BDA7D0BB83CDC1C2C6660B8ECB2EA30A685ADE2DC83C88314010FFC7F4F0F895EDDBE5C02" +
            "ABF78E50B708E0A0EB984A9AA536BCE61A0C31DB95425C6FEE5A564B158EE7C4F0693C439AE010EF83CA8155750" +
            "09B17537C29F86071E5DD8CA50EBD8A409494F479B07574D83EDCE6F68A8F7D40447471D05BC3F5EAD7862FA748" +
            "EA3C92A60A128344B1CEF7A0B0D94E50203010001";


        public static void Main(string[] args)
        {
            HttpWebRequest request = (HttpWebRequest)WebRequest.Create("https://azure.microsoft.com");
            request.ServerCertificateValidationCallback = (sender, certificate, chain, sslPolicyErrors) =>
            {
                if (certificate == null || sslPolicyErrors != SslPolicyErrors.None)
                {
                    // Error getting certificate or hello certificate failed basic validation
                    return false;
                }

                var targetKeyAlgorithm = new Oid(certificate.GetKeyAlgorithm()).FriendlyName;
                var targetPublicKey = certificate.GetPublicKeyString();
                
                if (targetKeyAlgorithm == PINNED_ALGORITHM &&
                    targetPublicKey == PINNED_PUBLIC_KEY)
                {
                    // Success, hello certificate matches hello pinned value.
                    return true;
                }
                // Reject, either hello key or hello algorithm does not match hello expected value.
                return false;
            };

            try
            {
                var response = (HttpWebResponse)request.GetResponse();
                Console.WriteLine($"Success, HTTP status code: {response.StatusCode}");
            }
            catch(Exception ex)
            {
                Console.WriteLine($"Failure, {ex.Message}");
            }
            Console.WriteLine("Press any key tooend.");
            Console.ReadKey();
        }
    }
}
```

## <a id="https-transport"></a>Włącz protokół HTTPS - bezpieczny kanał transportu

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | WCF | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | NET Framework 3 |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [uzyskania zawartości Królestwo](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Kroki** | Konfiguracja aplikacji Hello powinien upewnić się, że HTTPS jest używany przez wszystkie informacje toosensitive dostępu.<ul><li>**Wyjaśnienie:** Jeśli aplikacja obsługuje poufne informacje i nie używa szyfrowania na poziomie wiadomości, a następnie go powinny być dozwolone tylko toocommunicate przez kanał zaszyfrowany transportu.</li><li>**ZALECENIA:** upewnij się, że transportu HTTP jest wyłączona, a zamiast tego włączyć transportu HTTPS. Na przykład zastąpić hello `<httpTransport/>` z `<httpsTransport/>` tagu. Nie należy polegać na tooguarantee konfiguracji (zapora) sieci, że aplikacja hello jest możliwy tylko za pośrednictwem bezpiecznego kanału. Z filozoficzne punktu widzenia aplikacji hello nie należy uwzględniać sieci hello jego zabezpieczeń.</li></ul><p>Z praktycznego punktu widzenia osób hello odpowiadające za bezpieczeństwo sieci hello nie zawsze Śledź hello wymagań w zakresie zabezpieczeń aplikacji hello ich ewolucji.</p>|

## <a id="message-protection"></a>WCF: TooEncryptAndSign poziomu ochrony zabezpieczeń zestawu wiadomości

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | WCF | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | .NET framework 3 |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [MSDN](https://msdn.microsoft.com/library/ff650862.aspx) |
| **Kroki** | <ul><li>**Wyjaśnienie:** gdy poziom ochrony jest ustawiona zbyt komunikatu "none" spowoduje wyłączenie jego ochrony. Poufność i integralności odbywa się z poziomu odpowiednie ustawienia.</li><li>**ZALECENIA:**<ul><li>gdy `Mode=None` — wyłącza ochronę wiadomości</li><li>gdy `Mode=Sign` -znaki, ale nie szyfruje wiadomość hello; jeśli ważne jest, integralność danych, należy użyć</li><li>gdy `Mode=EncryptAndSign` -znaki i szyfrowanie wiadomości powitania</li></ul></li></ul><p>Rozważ wyłączenie szyfrowania i tylko podpisywania wiadomości, gdy wystarczy toovalidate hello integralność informacji hello bez obaw poufności. Może to być przydatne w przypadku operacji lub zamówienia usługi, w którym należy toovalidate hello oryginalnego nadawcy, ale są przesyłane żadne dane poufne. Gdy obniżenia poziomu ochrony hello, należy zachować ostrożność, tę wiadomość hello nie zawiera żadnych informacji osobistych (dane osobowe).</p>|

### <a name="example"></a>Przykład
Konfigurowanie usługi hello i wiadomości powitania hello operacji tooonly logowania jest wyświetlany w hello następujące przykłady. Przykład kontraktu usługi `ProtectionLevel.Sign`: hello poniżej przedstawiono przykład użycia ProtectionLevel.Sign na poziomie kontraktu usługi hello: 
```
[ServiceContract(Protection Level=ProtectionLevel.Sign] 
public interface IService 
  { 
  string GetData(int value); 
  } 
```

### <a name="example"></a>Przykład
Przykład kontrakt operacji `ProtectionLevel.Sign` (Aby uzyskać szczegółową kontrolę): hello poniżej przedstawiono przykład użycia `ProtectionLevel.Sign` na powitania OperationContract poziomu:

```
[OperationContract(ProtectionLevel=ProtectionLevel.Sign] 
string GetData(int value);
``` 

## <a id="least-account-wcf"></a>Usługi WCF: Użyj toorun najmniej uprzywilejowane konto usługi WCF

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | WCF | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | .NET framework 3 |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [MSDN](https://msdn.microsoft.com/library/ff648826.aspx ) |
| **Kroki** | <ul><li>**Wyjaśnienie:** nie są uruchamiane usługi WCF w ramach administratora lub konta wysokiego poziomu uprawnień. w przypadku naruszenia zabezpieczeń usługi spowoduje duże znaczenie.</li><li>**ZALECENIA:** Użyj toohost najmniej uprzywilejowane konto usługi programu WCF, ponieważ go zmniejsza możliwości ataku aplikacji i zmniejszyć potencjalne szkody hello, jeśli są ataku. Jeśli konto usługi hello wymaga praw dodatkowe dostępu do zasobów infrastruktury, takich jak usługi MSMQ, hello dziennika zdarzeń, liczników wydajności i system plików hello, odpowiednich uprawnień, należy podać toothese zasobów, aby uruchomić usługę WCF hello pomyślnie.</li></ul><p>Jeśli usługa wymaga tooaccess określonych zasobów imieniu hello oryginalny obiekt wywołujący, użyj personifikacji i delegowania tooflow hello tożsamości obiektu wywołującego sprawdzanie autoryzacji podrzędne. W przypadku rozwoju korzystać hello sieci lokalnej usługi konta, które jest specjalnym kontem wbudowanych, który ma ograniczone uprawnienia. W środowisku produkcyjnym należy utworzyć domeny niestandardowej najmniej uprzywilejowane konta usługi.</p>|

## <a id="webapi-https"></a>Wymuś wszystkich tooWeb ruchu interfejsów API za pośrednictwem połączenia HTTPS

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Interfejs API sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | MVC5, MVC6 |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Wymuszanie protokołu SSL w kontrolerze interfejsu API sieci Web](http://www.asp.net/web-api/overview/security/working-with-ssl-in-web-api) |
| **Kroki** | Jeśli aplikacja ma HTTPS i powiązanie HTTP, klientów można nadal używać lokacji hello tooaccess HTTP. tooprevent, użyj tooensure filtru Akcja żądający tooprotected interfejsy API są zawsze przy użyciu protokołu HTTPS.|

### <a name="example"></a>Przykład 
Witaj poniższy kod przedstawia filtr uwierzytelniania interfejsu API sieci Web, który sprawdza, czy protokół SSL: 
```C#
public class RequireHttpsAttribute : AuthorizationFilterAttribute
{
    public override void OnAuthorization(HttpActionContext actionContext)
    {
        if (actionContext.Request.RequestUri.Scheme != Uri.UriSchemeHttps)
        {
            actionContext.Response = new HttpResponseMessage(System.Net.HttpStatusCode.Forbidden)
            {
                ReasonPhrase = "HTTPS Required"
            };
        }
        else
        {
            base.OnAuthorization(actionContext);
        }
    }
}
```
Dodaj ten filtr akcji interfejsu API sieci Web tooany, które wymagają protokołu SSL: 
```C#
public class ValuesController : ApiController
{
    [RequireHttps]
    public HttpResponseMessage Get() { ... }
}
```
 
## <a id="redis-ssl"></a>Upewnij się, że tooAzure komunikacji, jest pamięcią podręczną Redis za pośrednictwem protokołu SSL

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Azure Redis Cache | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Pomoc techniczna platformy Azure Redis protokołu SSL](https://azure.microsoft.com/documentation/articles/cache-faq/#when-should-i-enable-the-non-ssl-port-for-connecting-to-redis) |
| **Kroki** | Redis fabrycznej hello serwer nie obsługuje protokołu SSL, ale nie w pamięci podręcznej Redis Azure. Jeśli łączysz tooAzure pamięci podręcznej Redis i klient obsługuje protokół SSL, takich jak programie StackExchange.Redis, należy użyć protokołu SSL. Domyślnie port bez protokołu SSL jest wyłączona dla nowego wystąpienia pamięci podręcznej Redis Azure. Upewnij się, że hello bezpieczne ustawienia domyślne nie są zmieniane, chyba że istnieje zależność na obsługę protokołu SSL dla klientów pamięci podręcznej redis. |

Należy pamiętać, że Redis jest zaprojektowana toobe dostęp do zaufanych klientów w środowiskach zaufanych. Oznacza to, że zwykle nie jest dobra pomysł tooexpose hello Redis bezpośrednio wystąpienia toohello internet lub ogólnie rzecz biorąc, umożliwiający niezaufani klienci mogą bezpośrednio dostęp do środowiska tooan hello port Redis TCP lub gniazda systemu UNIX. 

## <a id="device-field"></a>Bezpieczna komunikacja bramy tooField urządzenia

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Pole IoT bramy | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Dla urządzeń na podstawie adresu IP protokół komunikacyjny hello można zwykle hermetyzowany w przesyłanych danych tooprotect kanału SSL/TLS. Dla innych protokołów, które nie obsługują protokołu SSL/TLS Sprawdź, czy istnieją bezpieczne wersje protokołu hello zapewniające zabezpieczeń w warstwie transportu lub wiadomości. |

## <a id="device-cloud"></a>Zabezpieczanie tooCloud urządzenia bramy komunikacji przy użyciu protokołu SSL/TLS

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Brama chmury IoT | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Wybierz użytkownika protokołu komunikacyjnego](https://azure.microsoft.com/documentation/articles/iot-hub-devguide/#messaging) |
| **Kroki** | Secure HTTP/AMQP lub protokołów MQTT przy użyciu protokołu SSL/TLS. |
