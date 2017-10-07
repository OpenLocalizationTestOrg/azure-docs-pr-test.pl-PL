---
title: "aaaCryptography — narzędzie modelowania zagrożeń Microsoft - Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: cab981bf116a0e76bbf44fe0f0a1a3650e4ab0f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-cryptography--mitigations"></a>Ramka zabezpieczeń: Kryptografia | Środki zaradcze 
| Produktów i usług | Artykuł |
| --------------- | ------- |
| **Aplikacja sieci Web** | <ul><li>[Użyj tylko zatwierdzone symetrycznego blok, szyfrowania i długości kluczy](#cipher-length)</li><li>[Użyj zatwierdzone tryby szyfrowania bloku i wektory inicjacji dla szyfrowania symetrycznego](#vector-ciphers)</li><li>[Użyj zatwierdzone asymetrycznych algorytmów, długości kluczy i uzupełniania](#padding)</li><li>[Użyj zatwierdzone losowych liczb generatory kodu](#numgen)</li><li>[Nie należy używać szyfrowania symetrycznego strumienia](#stream-ciphers)</li><li>[Użyj zatwierdzone algorytmy wyznaczania wartości skrótu MAC/HMAC/z kluczem](#mac-hash)</li><li>[Użyj tylko zatwierdzone funkcji skrótu kryptograficznego](#hash-functions)</li></ul> |
| **Baza danych** | <ul><li>[Użyj silnego szyfrowania algorytmów tooencrypt danych w bazie danych hello](#strong-db)</li><li>[Pakiety usług SSIS powinny być szyfrowane i podpisane cyfrowo](#ssis-signed)</li><li>[Dodaj zabezpieczanych obiektów bazy danych toocritical podpis cyfrowy](#securables-db)</li><li>[Użyj kluczy szyfrowania tooprotect EKM serwera SQL](#ekm-keys)</li><li>[Funkcja AlwaysEncrypted klucze szyfrowania nie powinny być ujawnione tooDatabase aparatu](#keys-engine)</li></ul> |
| **Urządzenia IoT** | <ul><li>[Bezpieczne przechowywanie kluczy szyfrowania na urządzeniu IoT](#keys-iot)</li></ul> | 
| **Brama chmury IoT** | <ul><li>[Wygeneruje losowy klucz symetryczny wystarczającej długości dla uwierzytelniania tooIoT Centrum](#random-hub)</li></ul> | 
| **Klienta mobilnego programu Dynamics CRM** | <ul><li>[Upewnij się, że zasady zarządzania urządzeniami jest, że wymagane jest użycie numeru PIN i umożliwia zdalne czyszczenie danych](#pin-remote)</li></ul> | 
| **Klient programu Outlook Dynamics CRM** | <ul><li>[Upewnij się, że zasady zarządzania urządzenia w miejscu, które wymaga blokady auto-kodu PIN/hasła i szyfruje wszystkie dane (np. funkcją Bitlocker)](#bitlocker)</li></ul> | 
| **Tożsamości serwera** | <ul><li>[Upewnij się, że klucze podpisywania są przetwarzane przy użyciu tożsamości serwera](#rolled-server)</li><li>[Upewnij się, że identyfikator klienta silną kryptograficznie, klucz tajny klienta są używane na serwerze tożsamości](#client-server)</li></ul> | 

## <a id="cipher-length"></a>Użyj tylko zatwierdzone symetrycznego blok, szyfrowania i długości kluczy

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | <p>Produkty należy używać tylko symetrycznego blok, szyfrowania i związanych z nimi długości klucza, które zostały jawnie zatwierdzone przez hello kryptograficznego Advisor w swojej organizacji. Zatwierdzone algorytmy symetryczne firmy Microsoft zawierają hello po blok, szyfrowania:</p><ul><li>Nowy kod AES-128, AES 192 i AES 256 są dozwolone</li><li>Zgodności z poprzednimi wersjami z istniejącego kodu jest dopuszczalne trzech klucz 3DES</li><li>Przy użyciu szyfrowania symetrycznego bloku produktów:<ul><li>Advanced Encryption (Standard AES) jest wymagany dla nowego kodu</li><li>Klucz trzech triple Data Encryption Standard (3DES) jest dozwolone w istniejącym kodzie zgodności z poprzednimi wersjami</li><li>Wszystkie inne bloku szyfrów, w tym RC2, DES 2 klucz 3DES, DESX i bonito, może być używana tylko w celu odszyfrowania starych danych i muszą zostać zastąpione, jeśli jest używany do szyfrowania</li></ul></li><li>Dla algorytmów szyfrowania symetrycznego bloku minimalną długość klucza 128 bitów jest wymagana. Witaj tylko algorytm szyfrowania bloku zalecane w przypadku nowego kodu jest AES (AES-128, AES 192 i AES 256 są wszystkie dozwolone)</li><li>Trzy klucz 3DES jest obecnie akceptowane, jeśli już używani w istniejącym kodzie; Zaleca się tooAES przejścia. DES, DESX RC2 i bonito są już uznawane za bezpieczne. Algorytmy te może być używana tylko w celu odszyfrowania istniejące dane dotyczące hello zapewnienia zgodności z poprzednimi wersjami, a dane powinny być ponownie szyfrowane, przy użyciu szyfrowania bloku zalecane</li></ul><p>Należy pamiętać, że wszystkie szyfrowania symetrycznego bloku musi być używany z trybu zatwierdzonych szyfrowania, który wymaga użycia wektora odpowiednie inicjowania (IV). Odpowiednie IV jest zwykle liczbę losową i nigdy nie wartością stałą</p><p>Hello starszej wersji lub w inny sposób niezatwierdzonych algorytmów kryptograficznych i długości kluczy mniejszych do odczytywania istniejących danych (jako nowe dane toowriting min.) dozwolone może być po Przejrzyj tablicy kryptograficznego w organizacji. Jednak należy pliku wyjątku względem tego wymagania. Ponadto w przedsiębiorstwach, produktów należy rozważyć Administratorzy ostrzeżenie w przypadku słabe algorytmy kryptograficzne używane tooread danych. Takie ostrzeżenia powinna być wyjaśniające i możliwością wykonania akcji. W niektórych przypadkach może być toohave odpowiednich zasad grupy kontroli hello użycie słabe algorytmy kryptograficzne</p><p>Dozwolone algorytmy .NET dla zarządzanych elastyczność usług kryptograficznych (w kolejności preferencji)</p><ul><li>AesCng (zgodny ze standardem FIPS)</li><li>AuthenticatedAesCng (zgodny ze standardem FIPS)</li><li>AESCryptoServiceProvider (zgodny ze standardem FIPS)</li><li>AESManaged (z systemem innym niż — zgodne ze standardem FIPS)</li></ul><p>Należy pamiętać, że żaden z tych algorytmów można określić za pomocą hello `SymmetricAlgorithm.Create` lub `CryptoConfig.CreateFromName` metody bez wprowadzania zmian toohello machine.config pliku. Zauważ również, czy nosi nazwę AES w wersjach wcześniejszych too.NET .NET 3.5 `RijndaelManaged`, i `AesCng` i `AuthenticatedAesCng` są > dostępna za pośrednictwem portalu CodePlex i wymagają CNG hello podstawowego systemu operacyjnego</p>

## <a id="vector-ciphers"></a>Użyj zatwierdzone tryby szyfrowania bloku i wektory inicjacji dla szyfrowania symetrycznego

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Wszystkie szyfrowania symetrycznego bloku musi być używana z trybu zatwierdzonych szyfrowania symetrycznego. tryby Hello tylko zatwierdzone są CBC i CTS. W szczególności należy unikać hello Kod elektroniczny książki (ECB) tryb działania. Użyj ECB wymaga wykonania przeglądu kryptograficznego tablicy w organizacji. Użycie wszystkich OFB, CFB, Ewidencyjne, CCM i GCM lub innych tryb szyfrowania musi zrecenzowane przez tablicy kryptograficznego w organizacji. Ponowne wykorzystywanie hello sam wektor inicjowania (IV) z bloku szyfrów w "przesyłania strumieniowego szyfrów trybach" takie jak Ewidencyjne, może spowodować ujawniony toobe zaszyfrowanych danych. Wszystkie szyfrowania symetrycznego bloku musi również z wektora odpowiednie inicjowania (IV). Odpowiednie IV jest kryptograficznie silne, liczbę losową i nigdy nie stałej wartości. |

## <a id="padding"></a>Użyj zatwierdzone asymetrycznych algorytmów, długości kluczy i uzupełniania

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | <p>Użyj Hello zabronione algorytmów kryptograficznych wprowadzono znaczące zagrożenie bezpieczeństwa tooproduct i należy unikać. Produktów należy używać tylko tych algorytmów kryptograficznych i skojarzone długości kluczy i wypełnieniem jawnie zatwierdzone przez kryptograficznego w organizacji.</p><ul><li>**RSA -** mogą być używane do szyfrowania, wymiana klucza i podpis. Szyfrowanie RSA, należy użyć tylko hello OAEP lub RSA KEM dopełnienie trybów. Tryb zgodności tylko uzupełniania w wersji 1.5 PKCS #1 może korzystać z istniejącego kodu. Użyj wartości null uzupełnienia jawnie jest niedozwolone. Klucze > = 2048 bitów jest wymagany dla nowego kodu. Istniejący kod może obsługiwać klucze < 2048 bitów tylko w przypadku wstecz zgodności po dokonaniu przeglądu przez kryptograficznego w organizacji. Klucze < 1024 bity może być używana tylko do odszyfrowywania weryfikowanie starych danych i muszą być zastąpiony, jeśli używane do operacji podpisywania lub szyfrowania</li><li>**ECDSA -** mogą służyć tylko podpis. ECDSA z > = klucze 256-bitowy jest wymagany dla nowego kodu. Na podstawie ECDSA podpisów muszą używać jednej z hello trzech krzywych NIST zatwierdzone (p-256, p-384 lub P521). Krzywe, które zostały przeanalizowane dokładnie może być używany tylko po dokonaniu przeglądu tablica kryptograficznego w organizacji.</li><li>**ECDH -** mogą służyć tylko wymiany kluczy. ECDH z > = klucze 256-bitowy jest wymagany dla nowego kodu. Na podstawie ECDH wymiany kluczy muszą używać jednej z hello trzech krzywych NIST, zatwierdzone (p-256, p-384 lub P521). Krzywe, które zostały przeanalizowane dokładnie może być używany tylko po dokonaniu przeglądu tablica kryptograficznego w organizacji.</li><li>**DSA -** można zaakceptować po przeglądu i zatwierdzania od tablicy kryptograficznego w organizacji. Skontaktuj się z Twojego tooschedule advisor zabezpieczeń przeglądu kryptograficznego tablicy w organizacji. Po zatwierdzeniu użytkowania DSA należy pamiętać, że konieczne będzie użycie kluczy tooprohibit mniej niż 2048 bitów długości. CNG obsługuje długości klucza 2048-bitowe i większa począwszy od systemu Windows 8.</li><li>**Diffie-Hellman -** może służyć do sesji tylko zarządzania kluczami. Długość klucza > = 2048 bitów jest wymagany dla nowego kodu. Istniejący kod może obsługiwać długości kluczy < 2048 bitów tylko dla zapewnienia zgodności po dokonaniu przeglądu przez kryptograficznego w organizacji. Klucze < 1024 bity nie mogą być używane.</li><ul>

## <a id="numgen"></a>Użyj zatwierdzone losowych liczb generatory kodu

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | <p>Produkty muszą używać zatwierdzonych generatory liczb losowych. Pseudolosowych funkcji, takich jak hello C runtime funkcji rand, klasy .NET Framework hello System.Random lub funkcji systemu, takich jak GetTickCount w związku z tym nigdy nie należy w taki kod. Witaj dwie krzywej eliptycznej generator (DUAL_EC_DRBG) algorytmu liczb jest zabronione</p><ul><li>**CNG -** BCryptGenRandom (użycie flagi BCRYPT_USE_SYSTEM_PREFERRED_RNG hello zalecane, chyba że obiekt wywołujący hello mogą zostać uruchomione w dowolnej IRQL większa niż 0 [czyli PASSIVE_LEVEL])</li><li>**CAPI -** cryptGenRandom</li><li>**Win32/64-** RtlGenRandom (Nowe implementacje powinny używać BCryptGenRandom lub CryptGenRandom) * rand_s — * SystemPrng (dla trybu jądra)</li><li>**. NET -** RNGCryptoServiceProvider lub RNGCng</li><li>**Aplikacje Sklepu Windows -** Windows.Security.Cryptography.CryptographicBuffer.GenerateRandom lub. GenerateRandomNumber</li><li>**Apple OS X (10.7+)/iOS(2.0+) -** int SecRandomCopyBytes (SecRandomRef losowych, liczba size_t, uint8_t *bajtów)</li><li>**Apple OS X (< 10,7)-** Użyj / tooretrieve dev/losowych liczb losowych</li><li>**Java(including Google Android Java Code) -** java.security.SecureRandom klasy. Dla systemu Android 4.3 (galaretki ziarna), deweloperzy musi wykonać hello Android zalecane rozwiązania i zaktualizować ich tooexplicitly aplikacji zainicjować hello PRNG z entropii z /dev/urandom lub /dev/random</li></ul>|

## <a id="stream-ciphers"></a>Nie należy używać szyfrowania symetrycznego strumienia

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Szyfry symetrycznego strumienia, takich jak RC4, nie mogą być używane. Zamiast szyfrowania symetrycznego strumienia produktów należy używać szyfrowania bloku, w szczególności AES z kluczem o długości co najmniej 128 bitów. |

## <a id="mac-hash"></a>Użyj zatwierdzone algorytmy wyznaczania wartości skrótu MAC/HMAC/z kluczem

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | <p>Produkty należy używać tylko zatwierdzone kod uwierzytelniania wiadomości (MAC) lub algorytmy kodu (HMAC) uwierzytelniania na podstawie wyznaczania wartości skrótu wiadomości.</p><p>Kod uwierzytelniania wiadomości (MAC) jest to część informacji tooa dołączony komunikat, który umożliwia jego odbiorcy tooverify zarówno autentyczności hello hello nadawcy i integralności hello wiadomość hello przy użyciu klucza tajnego. Witaj Użyj albo systemem skrótu MAC ([HMAC](http://csrc.nist.gov/publications/nistpubs/800-107-rev1/sp800-107-rev1.pdf)) lub [MAC z systemem szyfrowania bloku](http://csrc.nist.gov/publications/nistpubs/800-38B/SP_800-38B.pdf) jest dozwolone, dopóki wszystkie podstawowej skrótu lub algorytmów szyfrowania symetrycznego również zatwierdzone do użycia; aktualnie to obejmuje hello funkcje algorytmu SHA2 HMAC (HMAC SHA256, HMAC SHA384 i HMAC SHA512) i hello CMAC/OMAC1 i OMAC2 blokowania na podstawie szyfrowania Mac (są one oparte na AES).</p><p>HMAC SHA1 mogą być dopuszczalne zgodności platformy, ale będzie można toofile wymagane procedury toothis wyjątku i przechodzą przegląd usług kryptograficznych w organizacji. Obcięcie tooless HMAC niż 128 bitów nie jest dozwolone. Przy użyciu klienta metody toohash klucza i danych nie jest zatwierdzona i muszą zostać poddane toouse wcześniejszego przeglądu kryptograficznego tablicy w organizacji.</p>|

## <a id="hash-functions"></a>Użyj tylko zatwierdzone funkcji skrótu kryptograficznego

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | <p>Produkty muszą używać rodziny hello SHA-2 algorytmów wyznaczania wartości skrótu (SHA256, SHA384 i SHA512). Jeśli krótszą wyznaczania wartości skrótu jest potrzebny, takie jak długość 128-bitowego dane wyjściowe w kolejności toofit to struktura danych o krótszej skrótu MD5 hello pamiętać, zespoły produktu może obciąć jedną z wartości skrótu algorytmu SHA2 hello (zazwyczaj SHA256). Należy pamiętać, że SHA384 skrócona wersja SHA512. Obcięcie skróty kryptograficzne dla bezpieczeństwa celów tooless niż 128 bitów nie jest dozwolone. Nowy kod nie może używać hello MD2, MD4, MD5, SHA-0, algorytm SHA-1 lub RIPEMD algorytmów wyznaczania wartości skrótu. Kolizji wyznaczania wartości skrótu są wykonalne dla te algorytmy, które skutecznie dzieli je.</p><p>Dozwolone .NET algorytmów wyznaczania wartości skrótu dla zarządzanych elastyczność usług kryptograficznych (w kolejności preferencji):</p><ul><li>SHA512Cng (zgodny ze standardem FIPS)</li><li>SHA384Cng (zgodny ze standardem FIPS)</li><li>SHA256Cng (zgodny ze standardem FIPS)</li><li>SHA512Managed (z systemem innym niż — zgodne ze standardem FIPS) (Użyj SHA512 jako nazwa algorytmu tooHashAlgorithm.Create wywołania lub CryptoConfig.CreateFromName)</li><li>SHA384Managed (z systemem innym niż — zgodne ze standardem FIPS) (Użyj SHA384 jako nazwa algorytmu tooHashAlgorithm.Create wywołania lub CryptoConfig.CreateFromName)</li><li>SHA256Managed (z systemem innym niż — zgodne ze standardem FIPS) (Użyj SHA256 jako nazwa algorytmu tooHashAlgorithm.Create wywołania lub CryptoConfig.CreateFromName)</li><li>SHA512CryptoServiceProvider (zgodny ze standardem FIPS)</li><li>SHA256CryptoServiceProvider (zgodny ze standardem FIPS)</li><li>SHA384CryptoServiceProvider (zgodny ze standardem FIPS)</li></ul>| 

## <a id="strong-db"></a>Użyj silnego szyfrowania algorytmów tooencrypt danych w bazie danych hello

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Database (Baza danych) | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Wybieranie algorytmu szyfrowania](https://technet.microsoft.com/library/ms345262(v=sql.130).aspx) |
| **Kroki** | Algorytmy szyfrowania zdefiniuj przekształcenia danych, których nie można łatwo cofnąć przez nieautoryzowanych użytkowników. SQL Server umożliwia Administratorzy i deweloperzy toochoose spośród kilku algorytmy, w tym DES, Triple DES, TRIPLE_DES_3KEY, RC2, RC4, 128-bitowego szyfrowania RC4, DESX, AES 128-bitowego, 192-bitowego szyfrowania AES i AES 256-bitowy |

## <a id="ssis-signed"></a>Pakiety usług SSIS powinny być szyfrowane i podpisane cyfrowo

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Database (Baza danych) | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Zidentyfikuj hello źródła pakietów z podpisami cyfrowymi](https://msdn.microsoft.com/library/ms141174.aspx), [zagrożeń i zapobieganie luki w zabezpieczeniach (Integration Services)](https://msdn.microsoft.com/library/bb522559.aspx) |
| **Kroki** | Witaj źródła pakietu jest hello poszczególnych lub organizacji, która opracowała pakiet hello. Uruchamianie pakietu z nieznaną lub niezaufaną źródła może być ryzykowne. nieautoryzowany tooprevent modyfikowaniu pakietów SSIS podpisy cyfrowe powinny być używane. Poufność hello tooensure pakietów hello podczas przesyłania/magazynu, pakietów SSIS są także toobe szyfrowane |

## <a id="securables-db"></a>Dodaj zabezpieczanych obiektów bazy danych toocritical podpis cyfrowy

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Database (Baza danych) | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Dodaj podpis (Transact-SQL)](https://msdn.microsoft.com/library/ms181700) |
| **Kroki** | W przypadku których integralności hello krytyczne zabezpieczanego bazy danych ma toobe zweryfikowane można użyć podpisów cyfrowych. Zabezpieczanych obiektów bazy danych, takich jak procedury składowanej, funkcji, zestawu lub wyzwalacza mogą być podpisane cyfrowo. Poniżej przedstawiono przykładowy gdy może to być przydatne: Daj nam powiedzieć niezależnego dostawcy oprogramowania (niezależnego dostawcy oprogramowania) udostępnił tooone oprogramowania dostarczyć tooa obsługę klientów. Przed zapewnianie pomocy technicznej, hello niezależnego dostawcy oprogramowania mają tooensure zabezpieczanego w oprogramowaniu hello bazy danych nie została zmieniona przez pomyłkę lub przez złośliwe próby. Jeśli zabezpieczanego hello jest podpisany cyfrowo, hello niezależnego dostawcy oprogramowania można zweryfikować podpisu cyfrowego i sprawdzić poprawności integralności.| 

## <a id="ekm-keys"></a>Użyj kluczy szyfrowania tooprotect EKM serwera SQL

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Database (Baza danych) | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Rozszerzonego klucza zarządzania programu SQL Server (EKM)](https://msdn.microsoft.com/library/bb895340), [rozszerzonego zarządzania kluczami, za pomocą usługi Azure Key Vault (SQL Server)](https://msdn.microsoft.com/library/dn198405) |
| **Kroki** | Rozszerzone zarządzanie kluczami programu SQL Server umożliwia kluczy szyfrowania hello chroniących toobe pliki bazy danych hello przechowywane w urządzeniu wyłączone pole takie jak karty inteligentnej, urządzenie USB lub modułu EKM/HSM. Dzięki temu ochrony danych ze strony administratorów bazy danych (z wyjątkiem członków grupy sysadmin hello). Dane mogą być szyfrowane przy użyciu kluczy szyfrowania, że tylko hello bazy danych użytkownika ma dostęp tooon hello zewnętrznych EKM/modułu HSM. |

## <a id="keys-engine"></a>Funkcja AlwaysEncrypted klucze szyfrowania nie powinny być ujawnione tooDatabase aparatu

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Database (Baza danych) | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Lokalnego programu SQL Azure |
| **Atrybuty**              | MsSQL2016 - 12 SQL |
| **Odwołania**              | [Zawsze zaszyfrowane (aparat bazy danych)](https://msdn.microsoft.com/library/mt163865) |
| **Kroki** | Zawsze zaszyfrowane jest funkcja zaprojektowana tooprotect poufnych danych, takich jak numery kart kredytowych lub numerów identyfikacyjnych national (np. USA numerów ubezpieczenia społecznego), przechowywane w bazach danych usługi Azure SQL Database lub SQL Server. Zawsze zaszyfrowane umożliwia klientom tooencrypt poufnych danych w aplikacjach klienckich i nigdy nie podawaj toohello klucze szyfrowania hello aparatu bazy danych (bazy danych SQL lub SQL Server). W związku z tym zawsze zaszyfrowane zapewnia oddzielenie tych, którzy własnych danych hello (i można go wyświetlić) oraz tych, którzy zarządzają danymi hello (ale powinien nie mają dostępu) |

## <a id="keys-iot"></a>Bezpieczne przechowywanie kluczy szyfrowania na urządzeniu IoT

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Urządzenia IoT | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Urządzenie systemu operacyjnego — Windows IoT Core, łączność urządzeń - zestawy SDK urządzenia Azure IoT |
| **Odwołania**              | [Moduł TPM w systemie Windows IoT Core](https://developer.microsoft.com/windows/iot/docs/tpm), [Konfigurowanie modułu TPM w systemie Windows IoT Core](https://developer.microsoft.com/windows/iot/win10/setuptpm), [TPM zestawem SDK urządzenia IoT Azure](https://github.com/Azure/azure-iot-hub-vs-cs/wiki/Device-Provisioning-with-TPM) |
| **Kroki** | Klucze Symmetric lub prywatny certyfikatu bezpiecznie na sprzętu chronione magazynu, takich jak moduły TPM lub karty inteligentnej. Windows 10 IoT Core obsługuje hello użytkownika modułu TPM i istnieje kilka zgodne moduły TPM, które mogą być używane: https://developer.microsoft.com/windows/iot/win10/tpm. Jest zalecana toouse oprogramowania układowego lub odrębny modułu TPM. Moduł TPM oprogramowania należy używać tylko do programowania i testowania. Po modułu TPM jest dostępny, a klucze hello są udostępniane w nim, hello kod, który generuje hello token zapisywane bez twardych kodowania żadnych poufnych informacji w nim. | 

### <a name="example"></a>Przykład
```
TpmDevice myDevice = new TpmDevice(0);
// Use logical device 0 on hello TPM 
string hubUri = myDevice.GetHostName(); 
string deviceId = myDevice.GetDeviceId(); 
string sasToken = myDevice.GetSASToken(); 

var deviceClient = DeviceClient.Create( hubUri, AuthenticationMethodFactory. CreateAuthenticationWithToken(deviceId, sasToken), TransportType.Amqp); 
```
Jak widać, klucz podstawowy hello urządzenie nie jest obecny w hello kodu. Zamiast tego jest ona przechowywana w hello modułu TPM na gniazda 0. Moduł TPM urządzenie wygeneruje krótkim okresie tokenu sygnatury dostępu Współdzielonego, który jest następnie używany toohello tooconnect Centrum IoT. 

## <a id="random-hub"></a>Wygeneruje losowy klucz symetryczny wystarczającej długości dla uwierzytelniania tooIoT Centrum

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Brama chmury IoT | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Wybór bramy - Centrum IoT Azure |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Centrum IoT zawiera urządzenia rejestru tożsamości i podczas inicjowania obsługi administracyjnej urządzeniu, automatycznie generuje losowe klucza symetrycznego. Zalecane jest toouse tej funkcji hello Azure IoT Hub tożsamości rejestru toogenerate hello klucz używany do uwierzytelniania. Centrum IoT umożliwia również toobe klucza, określić podczas tworzenia hello urządzenia. Jeśli klucz został wygenerowany poza Centrum IoT podczas inicjowania obsługi urządzeń, jest zalecane toocreate losowego klucza symetrycznego lub co najmniej 256 bitów. |

## <a id="pin-remote"></a>Upewnij się, że zasady zarządzania urządzeniami jest, że wymagane jest użycie numeru PIN i umożliwia zdalne czyszczenie danych

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Klienta mobilnego programu Dynamics CRM | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Upewnij się, że zasady zarządzania urządzeniami jest, że wymagane jest użycie numeru PIN i umożliwia zdalne czyszczenie danych |

## <a id="bitlocker"></a>Upewnij się, że zasady zarządzania urządzenia w miejscu, które wymaga blokady auto-kodu PIN/hasła i szyfruje wszystkie dane (np. funkcją Bitlocker)

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Klient programu Outlook Dynamics CRM | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Upewnij się, że zasady zarządzania urządzenia w miejscu, które wymaga blokady auto-kodu PIN/hasła i szyfruje wszystkie dane (np. funkcją Bitlocker) |

## <a id="rolled-server"></a>Upewnij się, że klucze podpisywania są przetwarzane przy użyciu tożsamości serwera

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Tożsamości serwera | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Tożsamość serwera — kluczy, podpisy i szyfrowania](https://identityserver.github.io/Documentation/docsv2/configuration/crypto.html) |
| **Kroki** | Upewnij się, że klucze podpisywania są przetwarzane przy użyciu tożsamości serwera. łącze Hello w sekcji odwołań hello wyjaśniono, jak to planowane bez powodowania przestojów tooapplications jednostki uzależnionej na serwerze tożsamości. |

## <a id="client-server"></a>Upewnij się, że identyfikator klienta silną kryptograficznie, klucz tajny klienta są używane na serwerze tożsamości

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Tożsamości serwera | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | <p>Upewnij się, że identyfikator klienta silną kryptograficznie, klucz tajny klienta są używane na serwerze tożsamości. podczas generowania identyfikator klienta i klucz tajny powinien być używany Hello następujące wytyczne:</p><ul><li>Generowanie losowy identyfikator GUID jako Identyfikatora klienta hello</li><li>Generuj kryptograficznie losowe 256-bitowego klucza jako hello klucza tajnego</li></ul>|
