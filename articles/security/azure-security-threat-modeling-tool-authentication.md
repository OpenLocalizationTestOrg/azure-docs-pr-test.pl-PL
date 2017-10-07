---
title: "aaaAuthentication — narzędzie modelowania zagrożeń Microsoft - Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 06c1b1aebab25e6fb5b666d24ecd9d86085d656c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-authentication--mitigations"></a>Ramka zabezpieczenia: Uwierzytelnianie | Środki zaradcze 
| Produktów i usług | Artykuł |
| --------------- | ------- |
| **Aplikacja sieci Web**    | <ul><li>[Należy rozważyć użycie uwierzytelniania standardowego tooWeb tooauthenticate mechanizm aplikacji](#standard-authn-web-app)</li><li>[Aplikacje muszą obsługiwać bezpiecznie scenariusze uwierzytelniania nie powiodło się](#handle-failed-authn)</li><li>[Włącz zwiększenia lub adaptacyjną uwierzytelniania](#step-up-adaptive-authn)</li><li>[Upewnij się, że interfejsy administracyjne są odpowiednio zablokowana](#admin-interface-lockdown)</li><li>[Implementowanie bezpiecznie nie pamiętasz hasła funkcji](#forgot-pword-fxn)</li><li>[Upewnij się, że są wykonywane zasad haseł i kont](#pword-account-policy)</li><li>[Wdrożenie kontroli tooprevent username wyliczenia](#controls-username-enum)</li></ul> |
| **Baza danych** | <ul><li>[Jeśli to możliwe, należy używać uwierzytelniania systemu Windows do łączenia tooSQL serwera](#win-authn-sql)</li><li>[Jeśli to możliwe Użyj uwierzytelniania usługi Azure Active Directory dla tooSQL łączenie bazy danych](#aad-authn-sql)</li><li>[Gdy używany jest tryb uwierzytelniania SQL, upewnij się, że konto i hasło zasady są wymuszane na serwerze SQL](#authn-account-pword)</li><li>[Nie należy używać uwierzytelniania SQL w zawartych baz danych](#autn-contained-db)</li></ul> |
| **Centrum zdarzeń platformy Azure** | <ul><li>[Użyj na tokeny sygnatury dostępu współdzielonego poświadczenia uwierzytelniania urządzenia](#authn-sas-tokens)</li></ul> |
| **Granic zaufania Azure** | <ul><li>[Włącz uwierzytelnianie wieloskładnikowe platformy Azure dla administratorów usługi Azure](#multi-factor-azure-admin)</li></ul> |
| **Granic zaufania sieci szkieletowej usług** | <ul><li>[Ogranicz dostęp anonimowy tooService klastra sieci szkieletowej](#anon-access-cluster)</li><li>[Upewnij się, że certyfikat klienta do węzła sieci szkieletowej usług różni się od certyfikatu węzła do węzła](#fabric-cn-nn)</li><li>[Za pomocą usługi AAD tooauthenticate klientów tooservice sieci szkieletowej klastrów](#aad-client-fabric)</li><li>[Upewnij się, że certyfikaty sieci szkieletowej usług są uzyskiwane z zatwierdzonych certyfikatu urzędu certyfikacji](#fabric-cert-ca)</li></ul> |
| **Tożsamości serwera** | <ul><li>[Standardowe uwierzytelnianie scenariusze obsługiwane przez serwer tożsamości użycia](#standard-authn-id)</li><li>[Zastąpienie hello domyślne tożsamości serwera pamięci podręcznej tokenu z alternatywnymi skalowalne](#override-token)</li></ul> |
| **Granic zaufania maszyny** | <ul><li>[Upewnij się, że pliki binarne wdrożonej aplikacji są podpisane cyfrowo](#binaries-signed)</li></ul> |
| **WCF** | <ul><li>[Włączenie uwierzytelniania podczas łączenia tooMSMQ kolejki programu WCF](#msmq-queues)</li><li>[Czy WCF nie jest ustawiony toonone clientCredentialType wiadomości](#message-none)</li><li>[Czy WCF nie jest ustawiony toonone clientCredentialType transportu](#transport-none)</li></ul> |
| **Interfejs API sieci Web** | <ul><li>[Upewnij się, że techniki standardowe uwierzytelnianie używane toosecure interfejsów API sieci Web](#authn-secure-api)</li></ul> |
| **Azure AD** | <ul><li>[Użyj uwierzytelniania standardowego scenariusze obsługiwane przez usługę Azure Active Directory](#authn-aad)</li><li>[Zastąpienie hello domyślny token pamięci podręcznej biblioteki ADAL z alternatywnymi skalowalne](#adal-scalable)</li><li>[Upewnij się, że TokenReplayCache jest używane tooprevent hello powtórzeń tokenów uwierzytelniania ADAL](#tokenreplaycache-adal)</li><li>[Korzystaj z bibliotek ADAL toomanage token żąda od tooAAD klientów OAuth2 (lub lokalnej usługi AD)](#adal-oauth2)</li></ul> |
| **Pole IoT bramy** | <ul><li>[Uwierzytelnianie urządzeń nawiązujących połączenie toohello pola bramy](#authn-devices-field)</li></ul> |
| **Brama chmury IoT** | <ul><li>[Upewnij się, że urządzeń nawiązujących połączenie bramy tooCloud są uwierzytelniane](#authn-devices-cloud)</li><li>[Użyj poświadczeń uwierzytelniania na urządzenie](#authn-cred)</li></ul> |
| **Azure Storage** | <ul><li>[Upewnij się, że ten hello tylko wymagane kontenery i obiekty BLOB są podane anonimowy dostęp do odczytu](#req-containers-anon)</li><li>[Przyznać ograniczony dostęp tooobjects w magazynie Azure za pomocą sygnatury dostępu Współdzielonego lub SAP](#limited-access-sas)</li></ul> |

## <a id="standard-authn-web-app"></a>Należy rozważyć użycie uwierzytelniania standardowego tooWeb tooauthenticate mechanizm aplikacji

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| Szczegóły | <p>Uwierzytelnianie to proces hello jednostki, w przypadku gdy okaże się swoją tożsamość, zwykle za pomocą poświadczeń, takie jak nazwa użytkownika i hasło. Brak dostępnych wiele protokołów uwierzytelniania, które mogą być uważane za. Poniżej wymieniono niektóre z nich:</p><ul><li>Certyfikaty klienta</li><li>Systemem Windows</li><li>Na podstawie formularzy</li><li>Federacyjna - usług AD FS</li><li>Federacyjna — usługi Azure AD</li><li>Federacyjna - tożsamości serwera</li></ul><p>Należy rozważyć użycie uwierzytelniania standardowego mechanizmu tooidentify hello źródła procesu</p>|

## <a id="handle-failed-authn"></a>Aplikacje muszą obsługiwać bezpiecznie scenariusze uwierzytelniania nie powiodło się

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| Szczegóły | <p>Aplikacje, które jawnie uwierzytelnianie użytkowników musi obsługiwać uwierzytelnianie nie powiodło się scenariusze, które muszą securely.hello mechanizmu uwierzytelniania:</p><ul><li>Odmowa dostępu tooprivileged zasobów, jeśli uwierzytelnianie nie powiedzie się</li><li>Wyświetl ogólny komunikat o błędzie po uwierzytelnieniu nie powiodło się i występuje odmowa dostępu</li></ul><p>Testowanie:</p><ul><li>Ochrona zasobów uprzywilejowanych po zakończonych niepowodzeniem prób zalogowania</li><li>Ogólny komunikat o błędzie jest wyświetlany na uwierzytelnianie nie powiodło się i zdarzenia odmowa dostępu</li><li>Konta są wyłączone po nadmiernej liczby nieudanych prób</li><ul>|

## <a id="step-up-adaptive-authn"></a>Włącz zwiększenia lub adaptacyjną uwierzytelniania

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| Szczegóły | <p>Sprawdź aplikacji hello ma dodatkowe autoryzacji (takie jak wzmocnić lub adaptacyjną uwierzytelniania, za pośrednictwem usługi Multi-Factor authentication, takie jak wysyłanie SMS, wiadomości e-mail itd. lub monitowanie o ponowne uwierzytelnianie OTP), użytkownik hello jest wezwał przed przyznaniem dostępu informacje o toosensitive. Ta zasada ma zastosowanie również do wprowadzania zmian krytyczne tooan konta lub akcji</p><p>Tym również oznacza, że dostosowania hello uwierzytelniania ma toobe zaimplementowana w taki sposób, że aplikacja hello poprawnie wymusza kontekstowa autoryzacji jako toonot pozwalają na nieautoryzowany manipulowania za pomocą klasy w przykładzie parametr naruszeniu</p>|

## <a id="admin-interface-lockdown"></a>Upewnij się, że interfejsy administracyjne są odpowiednio zablokowana

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| Szczegóły | Pierwsze rozwiązanie Hello jest toogrant dostęp tylko z niektórych IP zakresu toohello administracyjne interfejs źródłowy. Jeśli rozwiązania nie jest możliwe, nie zawsze jest zalecane tooenforce wzrostu lub adaptacyjną uwierzytelniania do logowania do interfejsu administracyjnego hello |

## <a id="forgot-pword-fxn"></a>Implementowanie bezpiecznie nie pamiętasz hasła funkcji

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| Szczegóły | <p>Hello jest po pierwsze tooverify, który zapomniał się, że hasło i innych ścieżek odzyskiwania wysłać łącze w tym czas aktywacji token, a nie hello samego hasła. Dodatkowe uwierzytelnianie oparte na tokeny elastyczne (np. programu SMS tokenu, natywnych aplikacji dla urządzeń przenośnych, itp.) może być wymagana również przed wysłaniem za pośrednictwem łącza hello. Drugie użytkownik powinien nie zablokowania hello użytkowników konta podczas procesu hello oznaczające wprowadzenie nowego hasła jest w toku.</p><p>Zawsze, gdy osoba atakująca decyduje toointentionally blokady hello użytkownikom atak zautomatyzowane, może to spowodować tooa odmowa usługi. Trzecie zawsze, gdy nowe żądanie hasła hello została ustawiona w toku, wiadomość hello, którą można wyświetlić powinien uogólniony w kolejności tooprevent username wyliczenia. Czwarty zawsze nie zezwalaj na używanie hello starego hasła i wdrożenie zasad silne hasło.</p> |

## <a id="pword-account-policy"></a>Upewnij się, że są wykonywane zasad haseł i kont

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| Szczegóły | <p>Powinny zostać wdrożone zasady haseł i kont zgodność z zasadami organizacyjnymi i najlepsze rozwiązania.</p><p>toodefend przed metodą siłową i słownik na podstawie odgadnięcie: zasady silne hasło musi być zaimplementowany tooensure, że użytkownicy tworzyć złożone hasło (np. minimalna długość 12 znaków, alfanumeryczne i znaki specjalne).</p><p>Zasady blokowania konta może być wdrażana w powitania po sposób:</p><ul><li>**Elastyczne blokady:** może to być dobre rozwiązanie do ochrony przed atakami siłowymi użytkowników. Na przykład zawsze, gdy użytkownik hello wprowadzi nieprawidłowe hasło aplikacji hello trzy razy może zablokować hello konta w ciągu minuty w kolejności tooslow dół hello proces wymuszanie hasła, dzięki czemu mniej zyski tooproceed atakująca hello metodą siłową. Jeśli zostały tooimplement twardych przeciwdziałanie blokady w ramach tego przykładu może osiągnąć "DOS" przez trwale blokowania kont. Możesz też aplikacji może wygenerować OTP (jedno hasło czasu) i wysłać go poza pasmem (za pośrednictwem poczty e-mail, sms itp.) toohello użytkownika. Innym rozwiązaniem może być tooimplement CAPTCHA, po osiągnięciu wartości progowej liczby nieudanych prób.</li><li>**Twarde blokady:** powinien być zastosowany ten typ blokady, za każdym razem wykryć użytkownika aplikacji do zaatakowania i licznika go za pomocą trwale zablokowania jego konta, dopóki zespół miał toodo czas ich dowodowe. Po wykonaniu tego procesu można zdecydować toogive hello ponownie użytkownika, jego konto lub podjęcia dalszych działań prawnych względem niego. Takiego podejścia zapobiega atakująca hello dalsze przechodzące przez aplikacji i infrastruktury.</li></ul><p>toodefend przed atakami na domyślnym i przewidywalne kont, sprawdź, czy wszystkie klucze i hasła są wymienne i są generowane lub zastąpiony po godzinie instalacji.</p><p>Jeśli aplikacja hello ma tooauto-generowania haseł, upewnij się, że hasła hello generowane są losowe i mieć wysokiej entropii.</p>|

## <a id="controls-username-enum"></a>Wdrożenie kontroli tooprevent username wyliczenia

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Wszystkie komunikaty o błędach powinny uogólniony w kolejności tooprevent username wyliczenia. Również czasami nie można pominąć informacje przeciek w funkcje, takie jak strona rejestracji. W tym miejscu należy toouse metody limitów szybkości, takie jak tooprevent CAPTCHA atak automatycznych przez osobę atakującą. |

## <a id="win-authn-sql"></a>Jeśli to możliwe, należy używać uwierzytelniania systemu Windows do łączenia tooSQL serwera

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Database (Baza danych) | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Lokalnego programu |
| **Atrybuty**              | Wersja programu SQL — wszystkie |
| **Odwołania**              | [SQL Server — wybierz tryb uwierzytelniania](https://msdn.microsoft.com/library/ms144284.aspx) |
| **Kroki** | Uwierzytelnianie systemu Windows używa protokołu zabezpieczeń Kerberos, zapewnia wymuszanie zasad haseł, z uwzględnieniem toocomplexity weryfikacji silnych haseł, zapewnia obsługę blokady konta oraz obsługuje wygasanie haseł.|

## <a id="aad-authn-sql"></a>Jeśli to możliwe Użyj uwierzytelniania usługi Azure Active Directory dla tooSQL łączenie bazy danych

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Database (Baza danych) | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Usługi SQL Azure |
| **Atrybuty**              | Wersja programu SQL — wersja 12 |
| **Odwołania**              | [Łączenie tooSQL bazy danych przy użyciu usługi Azure uwierzytelnianie usługi Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/) |
| **Kroki** | **Minimalna wersja:** bazy danych SQL Azure V12 wymagane tooallow bazy danych SQL Azure toouse uwierzytelniania w usłudze AAD przed hello Directory firmy Microsoft |

## <a id="authn-account-pword"></a>Gdy używany jest tryb uwierzytelniania SQL, upewnij się, że konto i hasło zasady są wymuszane na serwerze SQL

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Database (Baza danych) | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Zasady haseł programu SQL Server](https://technet.microsoft.com/library/ms161959(v=sql.110).aspx) |
| **Kroki** | Podczas korzystania z uwierzytelniania programu SQL Server, logowania są tworzone w programie SQL Server, które nie są oparte na kontach użytkowników systemu Windows. Hello nazwa użytkownika i hasło hello są tworzone za pomocą programu SQL Server i przechowywane w programie SQL Server. Program SQL Server można użyć mechanizmów zasad haseł systemu Windows. Stosuje hello same zasady złożoności i wygaśnięcia używane w toopasswords systemu Windows używane w programie SQL Server. |

## <a id="autn-contained-db"></a>Nie należy używać uwierzytelniania SQL w zawartych baz danych

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Database (Baza danych) | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Lokalnego, programu SQL Azure |
| **Atrybuty**              | Wersja - MSSQL2012, wersja programu SQL - SQL w wersji 12 |
| **Odwołania**              | [Najlepsze rozwiązania z zawartych baz danych](http://msdn.microsoft.com/library/ff929055.aspx) |
| **Kroki** | Hello braku zasad haseł wymuszone mogą zwiększyć prawdopodobieństwo hello słabe poświadczenia ustanowiono w zawartej bazie danych. Wykorzystywanie uwierzytelniania systemu Windows. |

## <a id="authn-sas-tokens"></a>Użyj na tokeny sygnatury dostępu współdzielonego poświadczenia uwierzytelniania urządzenia

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Centrum zdarzeń platformy Azure | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Uwierzytelnianie i zabezpieczenia modelu Omówienie usługi Event Hubs](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Kroki** | <p>model zabezpieczeń usługi Event Hubs Hello jest oparta na kombinacji tokenów dostępu sygnatury dostępu Współdzielonego i wydawców zdarzeń. Nazwa wydawcy Hello reprezentuje hello DeviceID, który odbiera hello token. Umożliwi to skojarzenie tokeny hello wygenerowane z odpowiednich urządzeń hello.</p><p>Wszystkie komunikaty są oznaczane nadawca po stronie usługi, umożliwiając wykrywanie pochodzenia — jest ładunku fałszowania prób. Podczas uwierzytelniania urządzenia, generowanie na wydawcy unikatowy tooa zakresie tokenu sygnatury dostępu współdzielonego urządzenia.</p>|

## <a id="multi-factor-azure-admin"></a>Włącz uwierzytelnianie wieloskładnikowe platformy Azure dla administratorów usługi Azure

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Granic zaufania Azure | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Co to jest usługa Multi-Factor Authentication platformy Azure?](https://azure.microsoft.com/documentation/articles/multi-factor-authentication/) |
| **Kroki** | <p>Uwierzytelnianie wieloskładnikowe (MFA) jest metoda uwierzytelniania, która wymaga więcej niż jednej metody weryfikacji i dodaje kluczową drugą warstwę logowania toouser zabezpieczeń i transakcji. Działania, gdyż dowolne dwa lub więcej hello następujące metody weryfikacji:</p><ul><li>Coś znasz (zwykle hasła)</li><li>Coś (zaufanych urządzeń, który nie jest łatwo zduplikowany, takich jak telefon)</li><li>Coś jest (biometria)</li><ul>|

## <a id="anon-access-cluster"></a>Ogranicz dostęp anonimowy tooService klastra sieci szkieletowej

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Granic zaufania sieci szkieletowej usług | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Środowisko — Azure  |
| **Odwołania**              | [Scenariusze zabezpieczeń klastra sieci szkieletowej usług](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security) |
| **Kroki** | <p>Klastry powinna być zawsze użytkowników zabezpieczonych tooprevent nieautoryzowany łączenie tooyour klastra, szczególnie w przypadku, gdy ma na nim uruchomione obciążeń produkcyjnych.</p><p>Podczas tworzenia klastra sieci szkieletowej usług, upewnij się, że ten tryb zabezpieczeń hello jest ustawiony za "bezpiecznej" i skonfiguruj certyfikat serwera X.509 hello wymagane. Tworzenie klastra "niebezpieczne" umożliwi tooit tooconnect dowolnego konta użytkownika anonimowego Jeśli eksponuje toohello punkty końcowe zarządzania publicznej sieci Internet.</p>|

## <a id="fabric-cn-nn"></a>Upewnij się, że certyfikat klienta do węzła sieci szkieletowej usług różni się od certyfikatu węzła do węzła

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Granic zaufania sieci szkieletowej usług | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Środowisko — Azure, środowisko — autonomiczny |
| **Odwołania**              | [Zabezpieczenia certyfikatów klienta do węzła sieci szkieletowej usług](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#_client-to-node-certificate-security), [Connect tooa bezpiecznego klastra przy użyciu certyfikatu klienta](https://azure.microsoft.com/documentation/articles/service-fabric-connect-to-secure-cluster/) |
| **Kroki** | <p>Węzeł klient certyfikat zabezpieczeń jest skonfigurowany podczas tworzenia klastra hello za pośrednictwem hello portalu Azure, szablonów usługi Resource Manager lub szablonu JSON w autonomicznej, określając administracyjnej certyfikatu klienta i/lub certyfikatu klienta użytkownika.</p><p>powitania klienta i użytkownika certyfikatów klienta administracyjnego przez użytkownika powinna być inna niż certyfikatów głównych i dodatkowych hello określone dla zabezpieczeń węzła do węzła.</p>|

## <a id="aad-client-fabric"></a>Za pomocą usługi AAD tooauthenticate klientów tooservice sieci szkieletowej klastrów

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Granic zaufania sieci szkieletowej usług | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Środowisko — Azure |
| **Odwołania**              | [W scenariuszach zabezpieczeń — zalecenia dotyczące zabezpieczeń klastra](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#security-recommendations) |
| **Kroki** | Klastry z systemem Azure można również bezpieczny dostęp do punktów końcowych zarządzania toohello przy użyciu usługi Azure Active Directory (AAD), z wyjątkiem certyfikatów klienta. W przypadku klastrów platformy Azure zaleca się korzystać klienci tooauthenticate zabezpieczeń usługi AAD i certyfikaty zabezpieczeń węzła do węzła.|

## <a id="fabric-cert-ca"></a>Upewnij się, że certyfikaty sieci szkieletowej usług są uzyskiwane z zatwierdzonych certyfikatu urzędu certyfikacji

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Granic zaufania sieci szkieletowej usług | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Środowisko — Azure |
| **Odwołania**              | [Certyfikaty X.509 i sieci szkieletowej usług](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#x509-certificates-and-service-fabric) |
| **Kroki** | <p>Sieć szkieletowa usług używa certyfikatów X.509 w celu uwierzytelniania węzłów i klientów.</p><p>Kilka ważnych rzeczy tooconsider podczas korzystania z certyfikatów w sieci szkieletowej usług:</p><ul><li>Certyfikatów używanych w klastrach z systemem obciążeń produkcyjnych powinna być utworzony przy użyciu poprawnie skonfigurowanej usługi certyfikatów systemu Windows Server lub uzyskane z zatwierdzonych certyfikatu urzędu certyfikacji. Witaj urzędu certyfikacji może być zatwierdzone zewnętrznego urzędu certyfikacji lub właściwie zarządzane wewnętrznej infrastruktury kluczy publicznych (PKI)</li><li>Nigdy nie używaj żadnych tymczasowej lub certyfikaty testów w środowisku produkcyjnym, które są tworzone za pomocą narzędzi, takich jak MakeCert.exe</li><li>Można użyć certyfikatu z podpisem własnym, ale powinien tylko zrobić dla klastrów testowych, a nie w środowisku produkcyjnym</li></ul>|

## <a id="standard-authn-id"></a>Standardowe uwierzytelnianie scenariusze obsługiwane przez serwer tożsamości użycia

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Tożsamości serwera | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [IdentityServer3 - hello duży obraz](https://identityserver.github.io/Documentation/docsv2/overview/bigPicture.html) |
| **Kroki** | <p>Poniżej przedstawiono hello typowe interakcje obsługiwane przez serwer tożsamości:</p><ul><li>Przeglądarki komunikacji z aplikacjami sieci web</li><li>Aplikacje sieci Web komunikować się z interfejsów API sieci web (czasami samodzielnie, czasami w imieniu użytkownika)</li><li>Aplikacje oparte na przeglądarce komunikować się z interfejsów API sieci web</li><li>Natywnych aplikacji komunikować się z interfejsów API sieci web</li><li>Aplikacje oparte na serwerze komunikować się z interfejsów API sieci web</li><li>Interfejsy API sieci Web komunikować się z interfejsów API sieci web (czasami samodzielnie, czasami w imieniu użytkownika)</li></ul>|

## <a id="override-token"></a>Zastąpienie hello domyślne tożsamości serwera pamięci podręcznej tokenu z alternatywnymi skalowalne

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Tożsamości serwera | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Wdrażanie serwera tożsamości — buforowanie](https://identityserver.github.io/Documentation/docsv2/advanced/deployment.html) |
| **Kroki** | <p>IdentityServer ma prosty wbudowanych w pamięci podręcznej. Jest to dobra dla natywnych aplikacji małą skalę, skalowaniu mid aplikacji warstwy i wewnętrznej bazy danych dla hello z następujących powodów:</p><ul><li>Te aplikacje są dostępne przez wielu użytkowników jednocześnie. Zapisywanie wszystkich tokenów dostępu w hello tego samego magazynu tworzy problemy izolacji i przedstawia problemy podczas działania na dużą skalę: w przypadku wielu użytkowników, każda z dowolną liczbę tokenów jako zasoby hello hello uzyskuje dostęp do aplikacji w ich imieniu może oznaczać dużych liczb i bardzo kosztowna wyszukiwania operacje</li><li>Te aplikacje są zwykle wdrażane dotyczących topologii rozproszonej, w której wiele węzłów musi mieć dostęp toohello tej samej pamięci podręcznej</li><li>Tokeny pamięci podręcznej musi być odporny odtwarza proces i deactivations</li><li>Dla wszystkich hello powyżej ze względu na podczas wdrażania aplikacji sieci web zalecane jest toooverride hello domyślne tożsamości serwera pamięci podręcznej tokenu z skalowalne alternatywne, takie jak pamięć podręczna Azure Redis</li></ul>|

## <a id="binaries-signed"></a>Upewnij się, że pliki binarne wdrożonej aplikacji są podpisane cyfrowo

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Granic zaufania maszyny | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Upewnij się, że pliki binarne wdrożonej aplikacji są podpisane cyfrowo, dzięki czemu można zweryfikować integralność plików binarnych hello hello|

## <a id="msmq-queues"></a>Włączenie uwierzytelniania podczas łączenia tooMSMQ kolejki programu WCF

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | WCF | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny, NET Framework 3 |
| **Atrybuty**              | Nie dotyczy |
| **Odwołania**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx) |
| **Kroki** | Program nie powiedzie się uwierzytelnianie tooenable podczas łączenia z kolejek tooMSMQ, osoba atakująca może anonimowo przesyłania wiadomości toohello kolejki w celu przetworzenia. Jeśli uwierzytelnianie nie jest używane tooconnect tooan MSMQ kolejkę toodeliver program tooanother wiadomości, osoba atakująca może przesłać anonimowe komunikat o błędzie jest złośliwe.|

### <a name="example"></a>Przykład
Witaj `<netMsmqBinding/>` element hello pliku konfiguracji usługi WCF poniżej nakazuje WCF toodisable uwierzytelniania podczas łączenia tooan kolejki usługi MSMQ w celu dostarczania komunikatów.
```
<bindings>
    <netMsmqBinding>
        <binding>
            <security>
                <transport msmqAuthenticationMode=""None"" />
            </security>
        </binding>
    </netMsmqBinding>
</bindings>
```
Skonfiguruj uwierzytelnianie domeny systemu Windows lub certyfikat toorequire usługi MSMQ przez cały czas jakiekolwiek komunikaty przychodzące lub wychodzące.

### <a name="example"></a>Przykład
Witaj `<netMsmqBinding/>` element hello pliku konfiguracji usługi WCF poniżej nakazuje WCF tooenable certyfikatu uwierzytelniania podczas łączenia tooan kolejki usługi MSMQ. powitania klienta jest uwierzytelniany przy użyciu certyfikatów X.509. certyfikat klienta na powitania musi występować w magazynie certyfikatów hello powitania serwera.
```
<bindings>
    <netMsmqBinding>
        <binding>
            <security>
                <transport msmqAuthenticationMode=""Certificate"" />
            </security>
        </binding>
    </netMsmqBinding>
</bindings>
```

## <a id="message-none"></a>Czy WCF nie jest ustawiony toonone clientCredentialType wiadomości

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | WCF | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | .NET framework 3 |
| **Atrybuty**              | Typ poświadczeń klienta - brak |
| **Odwołania**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [uzyskania zawartości](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Kroki** | Brak Hello uwierzytelniania oznacza Wszyscy jest możliwe tooaccess tej usługi. Usługa, która nie uwierzytelnia klientów zezwala na dostęp użytkowników tooall. Skonfiguruj tooauthenticate aplikacji hello względem poświadczeń klienta. Można to zrobić przez ustawienie tooWindows clientCredentialType wiadomość hello lub certyfikatu. |

### <a name="example"></a>Przykład
```
<message clientCredentialType=""Certificate""/>
```

## <a id="transport-none"></a>Czy WCF nie jest ustawiony toonone clientCredentialType transportu

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | WCF | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny, .NET Framework 3 |
| **Atrybuty**              | Typ poświadczeń klienta - brak |
| **Odwołania**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [uzyskania zawartości](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Kroki** | Brak Hello uwierzytelniania oznacza Wszyscy jest możliwe tooaccess tej usługi. Usługa, która nie uwierzytelnia klientów umożliwia wszystkich użytkowników tooaccess jego funkcjonalność. Skonfiguruj tooauthenticate aplikacji hello względem poświadczeń klienta. Można to zrobić przez ustawienie tooWindows clientCredentialType transportu hello lub certyfikatu. |

### <a name="example"></a>Przykład
```
<transport clientCredentialType=""Certificate""/>
```

## <a id="authn-secure-api"></a>Upewnij się, że techniki standardowe uwierzytelnianie używane toosecure interfejsów API sieci Web

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Interfejs API sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Uwierzytelnianie i autoryzacja w składniku ASP.NET Web API](http://www.asp.net/web-api/overview/security/authentication-and-authorization-in-aspnet-web-api), [zewnętrznych usług uwierzytelniania z interfejsu API sieci Web platformy ASP.NET (C#)](http://www.asp.net/web-api/overview/security/external-authentication-services) |
| **Kroki** | <p>Uwierzytelnianie to proces hello jednostki, w przypadku gdy okaże się swoją tożsamość, zwykle za pomocą poświadczeń, takie jak nazwa użytkownika i hasło. Brak dostępnych wiele protokołów uwierzytelniania, które mogą być uważane za. Poniżej wymieniono niektóre z nich:</p><ul><li>Certyfikaty klienta</li><li>Systemem Windows</li><li>Na podstawie formularzy</li><li>Federacyjna - usług AD FS</li><li>Federacyjna — usługi Azure AD</li><li>Federacyjna - tożsamości serwera</li></ul><p>Łącza w sekcji odwołań hello zapewniają szczegółów niskiego poziomu, w jak każdy hello schematy uwierzytelniania może być zaimplementowany toosecure interfejs API sieci Web.</p>|

## <a id="authn-aad"></a>Użyj uwierzytelniania standardowego scenariusze obsługiwane przez usługę Azure Active Directory

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Azure AD | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Scenariusze uwierzytelniania dla usługi Azure AD](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/), [Azure Active Directory przykłady kodu](https://azure.microsoft.com/documentation/articles/active-directory-code-samples/), [przewodnik dewelopera usługi Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-developers-guide/) |
| **Kroki** | <p>Azure Active Directory (Azure AD) ułatwia uwierzytelniania dla deweloperów, zapewniając tożsamości jako usługa, z obsługą standardowych protokołów, takich jak OAuth 2.0 i OpenID Connect. Poniżej przedstawiono hello pięć scenariuszy głównej aplikacji obsługiwanych przez usługę Azure AD:</p><ul><li>Przeglądarka tooWeb aplikacji w sieci Web: użytkownik musi toosign w tooa aplikacji sieci web chronionej przez usługę Azure AD</li><li>Jednej strony aplikacji JEDNOSTRONICOWEJ: Użytkownik musi toosign w tooa jednostronicowej aplikacji chronionej przez usługę Azure AD</li><li>Natywny tooWeb aplikacji interfejsu API: aplikacji natywnej działającym na telefonie, tablecie lub tooauthenticate potrzeb PC tooget użytkownika zasobów z interfejsu API sieci web chronionej przez usługę Azure AD</li><li>Interfejs API tooWeb aplikacji sieci Web: aplikacja sieci web wymaga zasobów tooget ze składnika web API zabezpieczone przez usługę Azure AD</li><li>TooWeb demon lub serwera aplikacji interfejsu API: aplikację demona lub serwera bez interfejsu użytkownika sieci web wymaga zasobów tooget ze składnika web API zabezpieczone przez usługę Azure AD</li></ul><p>Szczegółowe informacje niskiego poziomu implementacji zawiera łącza toohello w sekcji odwołań hello</p>|

## <a id="adal-scalable"></a>Zastąpienie hello domyślny token pamięci podręcznej biblioteki ADAL z alternatywnymi skalowalne

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Azure AD | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Nowoczesne uwierzytelnianie w usłudze Azure Active Directory dla aplikacji sieci Web](https://blogs.msdn.microsoft.com/microsoft_press/2016/01/04/new-book-modern-authentication-with-azure-active-directory-for-web-applications/), [przy użyciu Redis jako pamięci podręcznej tokenu ADAL](https://blogs.msdn.microsoft.com/mrochon/2016/09/19/using-redis-as-adal-token-cache/)  |
| **Kroki** | <p>Witaj domyślne podręcznej używa biblioteki ADAL (Active Directory Authentication Library) w pamięci podręcznej, używający statycznych magazynu, dostępne dla procesu. Gdy działa natywnych aplikacji, skalowaniu mid aplikacji warstwy i wewnętrznej bazy danych dla hello z następujących powodów:</p><ul><li>Te aplikacje są dostępne przez wielu użytkowników jednocześnie. Zapisywanie wszystkich tokenów dostępu w hello tego samego magazynu tworzy problemy izolacji i przedstawia problemy podczas działania na dużą skalę: w przypadku wielu użytkowników, każda z dowolną liczbę tokenów jako zasoby hello hello uzyskuje dostęp do aplikacji w ich imieniu może oznaczać dużych liczb i bardzo kosztowna wyszukiwania operacje</li><li>Te aplikacje są zwykle wdrażane dotyczących topologii rozproszonej, w której wiele węzłów musi mieć dostęp toohello tej samej pamięci podręcznej</li><li>Tokeny pamięci podręcznej musi być odporny odtwarza proces i deactivations</li></ul><p>Dla wszystkich hello powyżej ze względu na podczas wdrażania aplikacji sieci web zaleca się toooverride hello domyślny token pamięci podręcznej biblioteki ADAL z skalowalne alternatywne, takie jak pamięć podręczna Azure Redis.</p>|

## <a id="tokenreplaycache-adal"></a>Upewnij się, że TokenReplayCache jest używane tooprevent hello powtórzeń tokenów uwierzytelniania ADAL

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Azure AD | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Nowoczesne uwierzytelnianie w usłudze Azure Active Directory dla aplikacji sieci Web](https://blogs.msdn.microsoft.com/microsoft_press/2016/01/04/new-book-modern-authentication-with-azure-active-directory-for-web-applications/) |
| **Kroki** | <p>Właściwość TokenReplayCache Hello umożliwia deweloperom toodefine pamięci podręcznej powtórzeń tokenów, magazynu, który może służyć do zapisywania tokeny hello w celu sprawdzenia, czy token nie może zostać użyty więcej niż raz.</p><p>Jest to miara przed atakiem wspólne, hello aptly o nazwie ataku powtórzeń tokenów: osoba atakująca przechwytywaniu token hello wysyłane podczas logowania, spróbuj toosend go ponownie toohello aplikacji ("" Odtwórz je ponownie) do utworzenia nowej sesji. Np. W OIDC kodu grant przepływu, po uwierzytelnieniu użytkownika powiodło się żądanie zbyt "/ signin-oidc" punkt końcowy hello jednostki uzależnionej staje się z "w żądaniu", "code" i "stanu" Parametry.</p><p>Jednostka uzależniona Hello weryfikuje tego żądania i ustanawia nowej sesji. Jeśli atakujący dokonuje przechwytuje tego żądania i odtwarzaniem go, on ustanowić sesji pomyślnie i fałszywe hello użytkownika. obecność Hello nonce hello w OpenID Connect można ograniczyć, ale całkowicie wyeliminować hello okoliczności, w których atak powitania można pomyślnie przyjęte. tooprotect swoich aplikacji, deweloperzy mogą zapewniać implementację ITokenReplayCache i przypisz tooTokenReplayCache wystąpienia.</p>|

### <a name="example"></a>Przykład
```C#
// ITokenReplayCache defined in ADAL
public interface ITokenReplayCache
{
bool TryAdd(string securityToken, DateTime expiresOn);
bool TryFind(string securityToken);
}
```

### <a name="example"></a>Przykład
Oto przykładowe zastosowanie hello ITokenReplayCache interfejsu. (Należy dostosować i implementowanie framework buforowania z określonego projektu)
```C#
public class TokenReplayCache : ITokenReplayCache
{
    private readonly ICacheProvider cache; // Your project-specific cache provider
    public TokenReplayCache(ICacheProvider cache)
    {
        this.cache = cache;
    }
    public bool TryAdd(string securityToken, DateTime expiresOn)
    {
        if (this.cache.Get<string>(securityToken) == null)
        {
            this.cache.Set(securityToken, securityToken);
            return true;
        }
        return false;
    }
    public bool TryFind(string securityToken)
    {
        return this.cache.Get<string>(securityToken) != null;
    }
}
```
pamięć podręczna Hello zaimplementowana ma toobe, do którego odwołuje się opcje OIDC za pośrednictwem właściwości "TokenValidationParameters" hello w następujący sposób.
```C#
OpenIdConnectOptions openIdConnectOptions = new OpenIdConnectOptions
{
    AutomaticAuthenticate = true,
    ... // other configuration properties follow..
    TokenValidationParameters = new TokenValidationParameters
    {
        TokenReplayCache = new TokenReplayCache(/*Inject your cache provider*/);
    }
}
```

Należy należy pamiętać, tym skuteczności hello tootest tej konfiguracji, zaloguj się do lokalnych aplikacji chronionej przez OIDC i przechwytywania żądania hello zbyt`"/signin-oidc"` punktu końcowego w narzędziu fiddler. Gdy ochrona powitalnych nie znajduje się w miejscu, odtwarzanie tego żądania w narzędziu fiddler ustawi nowego pliku cookie sesji. Gdy Żądanie hello jest odtwarzany po dodaniu hello TokenReplayCache ochrony, aplikacja hello spowoduje zgłoszenie wyjątku w następujący sposób:`SecurityTokenReplayDetectedException: IDX10228: hello securityToken has previously been validated, securityToken: 'eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ1......`

## <a id="adal-oauth2"></a>Korzystaj z bibliotek ADAL toomanage token żąda od tooAAD klientów OAuth2 (lub lokalnej usługi AD)

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Azure AD | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [ADAL](https://azure.microsoft.com/documentation/articles/active-directory-authentication-libraries/) |
| **Kroki** | <p>tooeasily deweloperzy aplikacji Hello Azure AD authentication Library (ADAL) umożliwia klienta uwierzytelniania użytkowników toocloud lub lokalnej usługi Active Directory (AD), a następnie uzyskać tokeny dostępu dla zabezpieczanie interfejsu API.</p><p>Biblioteka ADAL oferuje wiele funkcji uwierzytelniania upewnij łatwiejsze dla deweloperów, takie jak obsługa komunikacji asynchronicznej, można skonfigurować tokenu pamięci podręcznej, która przechowuje tokenów dostępu i tokenów odświeżania, automatyczne odświeżanie tokenu po wygaśnięciu tokenu dostępu i token odświeżania jest dostępny, i więcej.</p><p>Dzięki obsłudze większość złożoności hello, ADAL można zawęzić dewelopera na logice biznesowej w aplikacjach i łatwo zabezpieczenia zasobów bez konieczności ekspertem w zakresie zabezpieczeń. Oddzielne biblioteki są dostępne dla platformy .NET, JavaScript (klient i Node.js), iOS, Android i Java.</p>|

## <a id="authn-devices-field"></a>Uwierzytelnianie urządzeń nawiązujących połączenie toohello pola bramy

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Pole IoT bramy | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Upewnij się, że każde urządzenie jest uwierzytelniany przez hello bramy pola przed zaakceptowaniem z nich danych oraz przed ułatwienia nadrzędnego komunikację z hello bramy chmury. Upewnij się również, że z łączyć się urządzenia na urządzeniu poświadczeń, dzięki czemu można jednoznacznie zidentyfikować poszczególnych urządzeń.|

## <a id="authn-devices-cloud"></a>Upewnij się, że urządzeń nawiązujących połączenie bramy tooCloud są uwierzytelniane

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Brama chmury IoT | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny, C#, Node.JS,  |
| **Atrybuty**              | Nie dotyczy — wybór bramy - Centrum IoT Azure |
| **Odwołania**              | Nie dotyczy — [Centrum Azure IoT z platformą .NET](https://azure.microsoft.com/documentation/articles/iot-hub-csharp-csharp-getstarted/), [wprowadzenie o Centrum IoT i Node JS](https://azure.microsoft.com/documentation/articles/iot-hub-node-node-getstarted), [zabezpieczanie IoT z sygnatury dostępu Współdzielonego i certyfikaty](https://azure.microsoft.com/documentation/articles/iot-hub-sas-tokens/), [repozytorium Git](https://github.com/Azure/azure-iot-sdks/tree/master/node) |
| **Kroki** | <ul><li>**Ogólny:** urządzenia hello uwierzytelniania przy użyciu zabezpieczeń TLS (Transport Layer) lub protokołu IPSec. Infrastruktura powinna obsługiwać przy użyciu klucza wstępnego (PSK) na tych urządzeniach, które nie może obsłużyć pełnej asymetrycznego kryptografii. Korzystaj z usługi Azure AD, Oauth.</li><li>**C#:** podczas tworzenia wystąpienia DeviceClient, domyślnie, hello metody Create tworzy wystąpienie DeviceClient, która używa toocommunicate protokołu AMQP hello z Centrum IoT. Witaj toouse protokołu HTTPS, za pomocą zastąpienia hello hello Tworzenie metody, która umożliwia toospecify hello protokołu. Jeśli używasz hello protokołu HTTPS, należy również dodać hello `Microsoft.AspNet.WebApi.Client` NuGet pakietu tooyour projektu tooinclude hello `System.Net.Http.Formatting` przestrzeni nazw.</li></ul>|

### <a name="example"></a>Przykład
```C#
static DeviceClient deviceClient;

static string deviceKey = "{device key}";
static string iotHubUri = "{iot hub hostname}";

var messageString = "{message in string format}";
var message = new Message(Encoding.ASCII.GetBytes(messageString));

deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey("myFirstDevice", deviceKey));

await deviceClient.SendEventAsync(message);
```

### <a name="example"></a>Przykład
**Node.JS: uwierzytelnianie**
#### <a name="symmetric-key"></a>Klucz symetryczny
* Tworzenie Centrum IoT na platformie azure
* Utwórz wpis w rejestrze tożsamości urządzeń hello
    ```javascript
    var device = new iothub.Device(null);
    device.deviceId = <DeviceId >
    registry.create(device, function(err, deviceInfo, res) {})
    ```
* Utworzyć symulowane urządzenie
    ```javascript
    var clientFromConnectionString = require('azure-iot-device-amqp').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    var connectionString = 'HostName=<HostName>DeviceId=<DeviceId>SharedAccessKey=<SharedAccessKey>';
    var client = clientFromConnectionString(connectionString);
    ```
#### <a name="sas-token"></a>Token sygnatury dostępu Współdzielonego
* Pobiera zostały wygenerowane wewnętrznie przy użyciu klucza symetrycznego, ale można wygenerować i używają go jawnie także
* Zdefiniuj protokół:`var Http = require('azure-iot-device-http').Http;`
* Utwórz token sygnatury dostępu współdzielonego:
    ```javascript
    resourceUri = encodeURIComponent(resourceUri.toLowerCase()).toLowerCase();
    var deviceName = "<deviceName >";
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    var toSign = resourceUri + '\n' + expires;
    // using crypto
    var decodedPassword = new Buffer(signingKey, 'base64').toString('binary');
    const hmac = crypto.createHmac('sha256', decodedPassword);
    hmac.update(toSign);
    var base64signature = hmac.digest('base64');
    var base64UriEncoded = encodeURIComponent(base64signature);
    // construct authorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "%2fdevices%2f"+deviceName+"&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
    ```
* Połącz przy użyciu tokenu sygnatury dostępu współdzielonego: 
    ```javascript
    Client.fromSharedAccessSignature(sas, Http); 
    ```
#### <a name="certificates"></a>Certyfikaty
* Generowanie self X509 podpisanego certyfikatu przy użyciu dowolnego narzędzia takie jak toogenerate biblioteki OpenSSL .cert .key pliki toostore hello certyfikat i hello klucz i odpowiednio
* Udostępnić urządzenia, który akceptuje połączenia zabezpieczonego za pomocą certyfikatów.
    ```javascript
    var connectionString = '<connectionString>';
    var registry = iothub.Registry.fromConnectionString(connectionString);
    var deviceJSON = {deviceId:"<deviceId>",
    authentication: {
        x509Thumbprint: {
        primaryThumbprint: "<PrimaryThumbprint>",
        secondaryThumbprint: "<SecondaryThumbprint>"
        }
    }}
    var device = deviceJSON;
    registry.create(device, function (err) {});
    ```
* Podłącz urządzenie przy użyciu certyfikatu
    ```javascript
    var Protocol = require('azure-iot-device-http').Http;
    var Client = require('azure-iot-device').Client;
    var connectionString = 'HostName=<HostName>DeviceId=<DeviceId>x509=true';
    var client = Client.fromConnectionString(connectionString, Protocol);
    var options = {
        key: fs.readFileSync('./key.pem', 'utf8'),
        cert: fs.readFileSync('./server.crt', 'utf8')
    }; 
    // Calling setOptions with hello x509 certificate and key (and optionally, passphrase) will configure hello client //transport toouse x509 when connecting tooIoT Hub
    client.setOptions(options);
    //call fn tooexecute after hello connection is set up
    client.open(fn);
    ```

## <a id="authn-cred"></a>Użyj poświadczeń uwierzytelniania na urządzenie

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Brama chmury IoT  | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Wybór bramy - Centrum IoT Azure |
| **Odwołania**              | [Tokeny zabezpieczające Centrum IoT Azure](https://azure.microsoft.com/documentation/articles/iot-hub-sas-tokens/) |
| **Kroki** | Użycie na tokeny sygnatury dostępu współdzielonego poświadczenia uwierzytelniania urządzenia na podstawie klucza urządzenia lub certyfikat klienta, zamiast poziomie Centrum IoT udostępnionych zasad dostępu. Zapobiega to ponowne użycie hello tokeny uwierzytelniania jednego pola lub urządzenia bramy przez inną |

## <a id="req-containers-anon"></a>Upewnij się, że ten hello tylko wymagane kontenery i obiekty BLOB są podane anonimowy dostęp do odczytu

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Azure Storage | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | StorageType — obiekt Blob |
| **Odwołania**              | [Zarządzanie toocontainers anonimowy dostęp do odczytu i obiekty BLOB](https://azure.microsoft.com/documentation/articles/storage-manage-access-to-resources/), [sygnatury dostępu współdzielonego, część 1: zrozumienie hello SAS modelu](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/) |
| **Kroki** | <p>Domyślnie kontener i wszystkie obiekty BLOB w nim mogą być używane tylko przez właściciela hello hello konta magazynu. kontener tooa uprawnienia do odczytu użytkowników anonimowych toogive i jego obiektów blob, jeden ustawiony dostępu publicznego tooallow hello kontenera uprawnienia. Użytkownicy anonimowi mogą odczytywać obiekty BLOB w kontenerze publicznie bez uwierzytelniania hello żądania.</p><p>Kontenery zawierają hello następujące opcje zarządzania dostęp do kontenera:</p><ul><li>Pełne publiczny dostęp do odczytu: obiektów blob i kontenera danych mogą być odczytywane za pomocą żądania od użytkowników anonimowych. Klientów można wyliczyć obiektów blob w kontenerze hello za pomocą żądania od użytkowników anonimowych, ale nie można wyliczyć kontenery w ramach konta magazynu hello.</li><li>Dostęp do obiektów blob tylko odczytu publicznego: dane obiektów Blob w tym kontenerze mogą być odczytywane za pomocą żądania od użytkowników anonimowych, ale nie są dostępne dane kontenera. Klienci nie można wyliczyć obiektów blob w kontenerze hello za pomocą żądań anonimowych</li><li>Dostęp do odczytu żadnego elementu publicznego public: obiektów blob i kontenera danych może zostać odczytany przez hello tylko właściciel konta</li></ul><p>Dostęp anonimowy jest najlepsze w przypadku scenariuszy, w którym niektórych obiektów blob zawsze powinny być dostępne dla anonimowego dostępu do odczytu. Precyzyjny system kontroli, można utworzyć sygnatury dostępu współdzielonego, co umożliwia dostęp ograniczony toodelegate przy użyciu różnych uprawnień i w określonym przedziale czasu. Upewnij się, że kontenerów i obiektów blob, które potencjalnie mogą zawierać poufne dane, nie otrzymują dostęp anonimowy przypadkowo</p>|

## <a id="limited-access-sas"></a>Przyznać ograniczony dostęp tooobjects w magazynie Azure za pomocą sygnatury dostępu Współdzielonego lub SAP

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Azure Storage | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy |
| **Odwołania**              | [Współużytkowanych sygnatur dostępu, część 1: Opis modelu sygnatur dostępu Współdzielonego hello](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/), [sygnatury dostępu współdzielonego, część 2: tworzenie i używanie sygnatury dostępu Współdzielonego z magazynem obiektów Blob](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-2/), [jak toodelegate dostępu tooobjects w za pomocą konta Sygnatury dostępu współdzielonego i zasad dostępu przechowywane](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_how-to-delegate-access-to-objects-in-your-account-using-shared-access-signatures-and-stored-access-policies) |
| **Kroki** | <p>Przy użyciu sygnatury dostępu współdzielonego (SAS) to wydajny sposób toogrant ograniczony dostęp tooobjects magazynu konta tooother klientów, bez konieczności klucz dostępu do konta tooexpose. Identyfikator URI, który obejmuje w jego parametrów zapytania jest Hello SAS hello informacje niezbędne do uwierzytelniony dostęp tooa zasobów magazynu. tooaccess zasoby pamięci masowej z hello SAS powitania klienta musi tylko toopass hello SAS toohello odpowiedniego konstruktora lub metody.</p><p>Sygnatury dostępu Współdzielonego można używać, gdy chce tooprovide tooresources dostępu w sieci klienta tooa konta magazynu nie może być kluczem konta hello zaufanych. Klucze konta magazynu obejmują zarówno podstawowego i pomocniczego klucza, które przyznać dostęp administracyjny tooyour konta i wszystkie zasoby hello w nim. Udostępnianie jednej z Twoich kluczy konta otwiera możliwości toohello Twojego konta złośliwego lub brak dbałości o ich użycia. Sygnatury dostępu współdzielonego zapewnić bezpieczne alternatywne, który umożliwia innym klientom tooread, zapisu i usuwania danych na koncie magazynu, zgodnie z toohello uprawnienia, które zostały przyznane i bez potrzeby hello klucz konta.</p><p>Jeśli masz logiczne zestaw parametrów, które są podobne za każdym razem, przy użyciu przechowywanych zasad dostępu (SAP) jest lepiej zrozumieć. Ponieważ przy użyciu sygnatury dostępu Współdzielonego uzyskane z zasad dostępu do przechowywanych umożliwia toorevoke możliwości hello czy SAS, jest ona hello zalecane najlepsze praktyki tooalways Użyj przechowywane zasad dostępu, gdy jest to możliwe.</p>|
