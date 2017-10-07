---
title: "aaaCloud zabezpieczeń odnajdywania aplikacji i zagadnienia dotyczące ochrony prywatności | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano hello zabezpieczeń i powiązane tooCloud zagadnienia dotyczące ochrony prywatności App Discovery."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 2fce5c82-d3de-4097-808f-40214768df9e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 33659e85bd2cf4294e443512e69a85401f7c53f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-security-and-privacy-considerations"></a>Cloud App Discovery zabezpieczeń i zagadnienia dotyczące ochrony prywatności
Firma Microsoft jest zatwierdzona tooprotecting prywatności i zabezpieczania danych, podczas dostarczania oprogramowania i usług, które ułatwiają zarządzanie hello zabezpieczeń organizacji.  
Wiemy, że podczas powierzyć tooothers Twojego danych, tej relacji zaufania wymaga inwestycje techniczne rygorystyczne zabezpieczeń i doświadczenia tooback go.
Microsoft toostrict zgodności i wytyczne dotyczące zabezpieczeń jest zgodna z bezpiecznego oprogramowania programowanie cyklu życia rozwiązania toooperating usługi.  
Zabezpieczenia i ochrona danych ma najwyższy priorytet w firmie Microsoft.

W tym temacie wyjaśniono, jak dane są zbierane, przetwarzane i zabezpieczane w ramach usługi Azure Active Directory Cloud App Discovery

## <a name="overview"></a>Omówienie
Usługa cloud App Discovery to funkcja usługi Azure AD i jest hostowana na platformie Microsoft Azure.  
Witaj Cloud App Discovery endpoint agent jest toocollect używanych danych odnajdywania aplikacji z IT zarządzanych komputerów.  
Witaj zebranych danych jest przesłane za pośrednictwem kanału szyfrowanego toohello usługi Azure AD Cloud App Discovery.  
Hello Cloud App Discovery danych organizacji będzie widoczne w portalu Azure hello. 

![Jak działa usługa Cloud App Discovery](./media/active-directory-cloudappdiscovery-security-and-privacy-considerations/cad01.png) 

Witaj poniższe sekcje wykonaj hello przepływu informacji i opisano, jak zabezpieczone przesyłane z usługą Cloud App Discovery toohello organizacji i ostatecznie toohello Cloud App Discovery portalu.

## <a name="collecting-data-from-your-organization"></a>Zbieranie danych z Twojej organizacji
W kolejności toouse usługi Azure Active Directory w aplikacji w chmurze odnajdowania funkcji tooget wgląd w aplikacji hello używanych przez pracowników w organizacji, należy toofirst wdrażanie hello Azure AD Cloud App Discovery endpoint agent toomachines w Twojej organizacji.

Administratorzy dzierżawy usługi Azure Active Directory hello (lub ich delegata) można pobrać pakiet instalacyjny agenta hello z hello portalu Azure. Hello agenta może być ręcznie zainstalowane lub zainstalowany na wielu komputerach w organizacji hello za pomocą programu SCCM lub zasad grupy.

Aby uzyskać dalsze instrukcje na temat opcji wdrażania, zobacz [Podręcznik wdrażania zasad grupy chmury aplikacji odnajdywania](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx).


### <a name="data-collected-by-hello-agent"></a>Dane zebrane przez agenta hello
Hello informacje opisane w poniższej listy hello zbieranych przez agenta powitania po nawiązaniu połączenia tooa aplikacji sieci Web. Witaj informacje są zbierane w przypadku aplikacji, czy administrator hello ma skonfigurowany w celu odnajdywania.  
Można edytować hello wykaz aplikacji w chmurze, które hello monitorów agenta za pomocą bloku Cloud App Discovery hello w hello Microsoft [portalu Azure](https://portal.azure.com/)w obszarze **ustawienia**->**danych Kolekcja**->**listy aplikacji kolekcji**. Aby uzyskać więcej informacji, zobacz [pobierania uruchomiona z Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)


**Informacje o kategorii**: informacje o użytkowniku  
**Opis elementu**:  
Nazwa użytkownika systemu Windows Hello hello procesu, który zgłosił żądanie toohello docelowej aplikacji sieci Web (np.: domena azwa_użytkownika) oraz hello identyfikatora zabezpieczeń systemu Windows (SID) użytkownika hello.

**Informacje o kategorii**: przetworzyć informacji  
**Opis elementu**:  
Nazwa Hello hello procesu, który zgłosił żądanie hello docelowej toohello aplikacji sieci Web (np.: "iexplore.exe")

**Informacje o kategorii**: informacje o komputerze  
**Opis elementu**:  
Nazwa NetBIOS komputera Hello na które hello jest zainstalowany agent.

**Informacje o kategorii**: informacje o aplikacji ruchu  
**Opis elementu**: 

Witaj, następujące informacje dotyczące połączenia:

* Źródło Hello (komputer lokalny) i docelowe adresy IP i numery portów
* Witaj publiczny adres IP hello organizacji za pomocą których hello trafia żądania.
* czas Hello hello żądania
* wielkość Hello ruch wysyłany i odbierany
* Wersja IP Hello (4 lub 6)
* Tylko w połączeniach TLS: Nazwa hosta docelowego hello hello rozszerzeń wskaźnika nazwy serwera lub certyfikatu serwera hello.

Witaj następujących informacji HTTP:

* — Metoda (GET, POST itp.)
* Protokół (HTTP/1.1, itp.)
* Ciąg agenta użytkownika
* Nazwa hosta
* Docelowy identyfikator URI (z wyłączeniem ciągu zapytania)
* Informacje o typie zawartości
* Adresy URL odwołania (z wyjątkiem ciągu zapytania)

> [!NOTE]
> Witaj HTTP powyższe informacje są zbierane dla wszystkich połączeń niezaszyfrowanych.
> Dla połączeń TLS te informacje są przechwytywane tylko po włączeniu ustawienia "Głęboka inspekcja" hello w portalu hello. Domyślnie ustawienie Hello jest "ON".
> Aby uzyskać więcej informacji, zobacz poniżej i [uzyskiwanie uruchomiona z Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)
> 
> 

Dodatkowo toohello danych agenta hello zbiera dane o działaniu sieci hello, ponadto zbiera anonimowe informacje o konfiguracji sprzętu i oprogramowania hello, raporty o błędach i informacje o sposobie używania hello agenta.


### <a name="how-hello-agent-works"></a>Jak działa hello agenta
Instalacja agenta Hello obejmuje dwa składniki:

* Składnik trybu użytkownika
* Składnik sterowników trybu jądra (driver platformy filtrowania systemu Windows)

Podczas pierwszej instalacji agenta hello przechowuje zaufanego certyfikatu komputera na maszynie hello które it używa tooestablish bezpiecznego połączenia z usługą Cloud App Discovery hello.  
Hello agent okresowo pobiera konfigurację zasad z hello usługi Cloud App Discovery za pośrednictwem tego bezpiecznego połączenia.  
zasady Hello zawierają informacje o które toomonitor aplikacje w chmurze i czy automatycznego aktualizowania powinno być włączone, między innymi.

Jak ruch w sieci Web są wysyłane i odbierane na komputerze hello w programie Internet Explorer i Chrome, agenta Cloud App Discovery hello analizuje ruch hello i wyodrębnia hello odpowiednie metadane (zobacz hello **danych zbieranych przez agenta hello** sekcji powyżej).  
Co minutę hello agenta przekazywania hello zebranych metadanych toohello usługi Cloud App Discovery za pośrednictwem kanału szyfrowanego.

Przechwytuje składnika sterownika Hello hello szyfrowanego ruchu sieciowego i umieszczony w strumieniu zaszyfrowanych hello. Więcej szczegółów w hello **przechwycenia danych z zaszyfrowanego połączenia (głęboka inspekcja)** poniższej sekcji.

### <a name="respecting-user-privacy"></a>Przestrzeganie zasady zachowania poufności użytkownika
Naszym celem jest tooprovide Administratorzy hello narzędzia tooset hello równowagi między szczegółowe światłowodowa do użycia i użytkownika prywatności aplikacji zależnie od potrzeb organizacji. końcowy toothat udostępniamy powitania po pokrętła na stronie ustawień hello w hello portalu:

* **Zbieranie danych**: Administratorzy mogą wybrać toospecify, które aplikacje lub mają tooget danych odnajdywania na kategorii aplikacji.
* **Głęboka inspekcja**: Administratorzy mogą wybrać toospecify Jeśli hello agent zbiera ruchu HTTP na potrzeby połączeń SSL/TLS (alias **"Głęboka inspekcja"**). Więcej informacji na temat to w następnej sekcji hello.
* **Zgoda opcje**: Administratorzy mogą używać portalu toochoose Cloud App Discovery hello Określa, czy użytkownicy toonotify hello zbierania danych przez agenta hello i czy użytkownik toorequire wyrazić zgodę przed rozpoczęciem powitalne agenta zbierania danych użytkownika.

Witaj Cloud App Discovery endpoint agent zbiera tylko hello informacje opisane w hello **danych zbieranych przez agenta hello** powyższej sekcji.

### <a name="intercepting-data-from-encrypted-connections-deep-inspection"></a>Przechwycenia danych z zaszyfrowanego połączenia (głęboka inspekcja)
Jak wspomniano wcześniej, Administratorzy mogą skonfigurować hello agenta toomonitor danych z zaszyfrowanego połączenia ("głęboka inspekcja"). TLS ([Transport Layer Security](https://msdn.microsoft.com/library/windows/desktop/aa380516%28v=vs.85%29.aspx)) jest jednym z hello najbardziej popularne protokoły używany na powitania Internet dzisiaj. Przez szyfrowania komunikacji z protokołem TLS, klient może ustanowić kanał bezpieczeństwo i prywatność komunikacji z serwerem sieci web; TLS zapewnia ochronę niezbędne do przekazywania poświadczeń uwierzytelniania i zapobiec hello ujawnienie poufnych informacji.

Podczas hello end-to-end bezpiecznego kanału szyfrowanego udostępniane przez protokoły TLS umożliwia ważne zabezpieczenia i ochrona prywatności, protokół hello jest często użyte do celów złośliwego lub nefarious. Zbyt duża, w rzeczywistości TLS jest często określane tooas hello "universal obejścia zapory protokół". główny Hello hello problemu są większość zapór komunikację TLS tooinspect ponieważ hello warstwy aplikacji dane są szyfrowane przy użyciu protokołu SSL. Wiedzy o to, osoby atakujące często wykorzystać TLS toodeliver złośliwe ładunków tooa użytkownika pewność, że nawet hello najbardziej inteligentnego warstwy aplikacji zapory są całkowicie ukryta tooTLS i po prostu musi przekazywać TLS komunikacji między hostami. Użytkownicy końcowi często korzystaj z kontroli dostępu toobypass TLS wymuszane przez ich firmowej zapory i serwery proxy, używają jej tooconnect toopublic proxy oraz tunelowania protokołów-TLS przez zaporę Windows hello, w przeciwnym razie może być zablokowany przez zasady.

Głęboka inspekcja pozwala tooact agenta Cloud App Discovery hello jako zaufany man-in--middle. Po wysłaniu żądania klienta jest tooaccess HTTPS chroniony zasób, sterownik Endpoint Agent hello przechwytuje hello połączenia i ustanawia nowego tooretrieves serwera docelowego toohello połączenia jego certyfikat SSL w imieniu klienta hello. Hello agent następnie sprawdza, czy certyfikat hello mogą być zaufane (przez sprawdzanie, czy nie został odwołany i wykonywania innych operacje sprawdzania certyfikatów) i jeśli te przekazać, hello Endpoint Agent hello informacje są kopiowane z certyfikatu serwera hello i tworzy własne certyfikat serwera — znany pod nazwą certyfikatu przechwytywaniu — za pomocą tych informacji. certyfikat przechwytywaniu Hello jest podpisem na bieżąco przez agenta endpoint hello za pomocą certyfikatu głównego, który jest instalowany w magazynie certyfikatów zaufanych Windows hello. Ten certyfikat główny z podpisem własnym jest oznaczony jako eksportowalny z systemem innym niż i listy kontroli dostępu jest miał tooadministrators. Jest zamierzone toonever pozostaw hello maszyny, na którym został utworzony. Aplikacja kliencka hello użytkownika końcowego odebrania hello przechwycenie certyfikatu go go ufa ponieważ można pomyślnie zweryfikować łańcucha certyfikatów hello wszystkich hello sposób toohello certyfikatu głównego. Ten proces jest przeważnie przezroczysty od użytkownika końcowego punktu widzenia z kilku zastrzeżeniami zgodnie z poniższym opisem.

Włączając głęboka inspekcja hello agenta Cloud App Discovery Endpoint Agent może odszyfrować i zbadaj komunikację TLS szyfrowane, umożliwiając szumu tooreduce usługi hello i szczegółowymi informacjami na temat hello użycie aplikacji w chmurze hello szyfrowane.

#### <a name="a-word-of-caution"></a>Wyraz Uwaga
Przed włączeniem głęboka inspekcja, zdecydowanie zaleca się komunikować się z tooyour zamiarach prawne i działu HR i uzyskać zgodę. Zapoznanie się użytkownika końcowego prywatnej szyfrowanie komunikacji może być poufnych podmiotu, oczywiste ze względu na. Przed produkcji wdrożenie głębokiej inspekcji należy pewność, że zabezpieczeń firmy i zostały zaktualizowane zasady dopuszczalnych działań będzie sprawdzana tooindicate szyfrowane komunikacji. Powiadomienie użytkownika i wykluczania witryn uznany za poufnych (np. bankowości i medyczne witryny) może być konieczne, jeśli konfigurujesz toomonitor Cloud App Discovery je. Jak wspomniano powyżej, Administratorzy mogą używać portalu toochoose Cloud App Discovery hello Określa, czy użytkownicy toonotify hello zbierania danych przez agenta hello i czy użytkownik toorequire wyrazić zgodę przed rozpoczęciem powitalne agenta zbierania danych użytkownika.

### <a name="known-issues-and-drawbacks"></a>Znane problemy i wady
Istnieje kilka przypadków, w którym zatrzymania protokołu TLS może mieć wpływ na środowisko użytkownika końcowego hello:

* Rozszerzonej weryfikacji zastosowanie certyfikatów renderowania hello paska adresu tooact zielony przeglądarki sieci web hello jako wizualny sygnał odwiedzają zaufanych witryn sieci web. Kontroli TLS nie może mieć takiej Weryfikacją w hello certyfikat, który wystawia toohello klienta, więc witryn sieci web, które korzystają z Weryfikacją certyfikatów będą działały normalnie, ale hello pasku adresu nie zostanie wyświetlony zielony.  
* Publicznego klucza przypinanie (określane również jako przypinania certyfikatu) zostały zaprojektowane toohelp chronić użytkowników przed atakami man-in--middle i nieautoryzowane urzędów certyfikacji. Gdy certyfikat główny hello przypiętych witryny nie pasuje do jednej z hello znana dobra urzędu certyfikacji, przeglądarki hello odrzuca hello połączenia z powodu błędu. Ponieważ zatrzymania protokołu TLS jest w rzeczywistości man-in--middle, te połączenia nie powiedzie się.
* Jeśli użytkownik kliknie ikonę blokady hello hello przeglądarki adres pasek przeglądarki tooinspect hello informacji o lokacji, nie zobaczy łańcuch końcówką hello urząd certyfikacji używany certyfikat witryny internetowej hello toosign, ale zamiast tego łańcucha certyfikatów kończąc hello systemu Windows magazynu zaufanych certyfikatów.

tooreduce hello wystąpienia tych problemów, firma Microsoft śledzić usługi w chmurze i aplikacje klienckie znane toouse rozszerzonej weryfikacji lub przypinanie klucza publicznego oraz poinstruuj tooavoid Endpoint Agent hello przechwytywaniu ryzyko połączenia. Nawet w takich przypadkach jednak nadal będą odbierane raporty hello korzystanie z tych aplikacji w chmurze i hello ilość danych przesyłanych jednak ponieważ nie są one głębokiej inspekcji, szczegóły używania aplikacji hello będą dostępne.

## <a name="sending-data-toocloud-app-discovery"></a>Wysyłanie danych tooCloud App Discovery
Gdy metadane zostały zebrane przez agenta hello, są buforowane na komputerze hello na potrzeby się tooone minutę lub dopóki hello buforowane dane osiągnie rozmiar to 5 MB. Następnie jest skompresowany i wysyłane za pośrednictwem bezpiecznego połączenia toohello usługi Cloud App Discovery.

Jeśli hello agent toocommunicate z hello usługi Cloud App Discovery jakiejkolwiek przyczyny, hello zebranych metadane są przechowywane w pamięci podręcznej z pliku lokalnego jest możliwy tylko przez użytkowników uprzywilejowanych hello maszyny (np. grupy Administratorzy hello).  
Hello agent automatycznie hello tooresend prób buforowane metadane do pomyślnie zostały odebrane przez usługę Cloud App Discovery hello.

## <a name="receiving-hello-data-at-hello-service-end"></a>Odbieranie danych hello na końcu usługi hello
agenci Hello uwierzytelniania toohello Cloud App Discovery usługi przy użyciu certyfikatu uwierzytelniania klienta właściwy maszyny hello powyżej i przekazuje dane za pośrednictwem kanału szyfrowanego.  
Usługa Cloud App Discovery Hello potoku analitycznego procesów metadanych dla każdego klienta oddzielnie logicznie podział na wszystkich etapach potoku analizy hello.
Witaj przeanalizowane metadanych dysków hello różne raporty w portalu hello.

Witaj nieprzetworzone metadanych i hello przeanalizowane metadane są przechowywane na potrzeby się too180 dni. Ponadto klienci mogą wybrać toocapture hello przeanalizowane metadanych dla konta magazynu obiektów blob platformy Azure ich wybrać.
Jest to przydatne w trybie offline analizy metadanych, a także dłużej przechowywania danych hello.

## <a name="accessing-hello-data-using-hello-azure-portal"></a>Uzyskiwanie dostępu do danych hello przy użyciu hello portalu Azure
W metadanych hello tookeep nakładu zbierane bezpieczny, domyślnie tylko administratorzy globalni hello dzierżawcy mają funkcji Cloud App Discovery toohello dostępu w hello portalu Azure.  
Jednak administratorzy mogą wybrać toodelegate tego dostępu tooother użytkowników lub grup.

> [!NOTE]
> Aby uzyskać więcej informacji, zobacz [pobierania uruchomiona z Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)
> 
> 


Podczas uzyskiwania dostępu do danych hello dowolnego użytkownika w portalu hello muszą mieć licencję z licencją Azure AD Premium.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Jak odnajdywać niezatwierdzone aplikacje w chmurze używanych mojej organizacji](active-directory-cloudappdiscovery-whatis.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)

