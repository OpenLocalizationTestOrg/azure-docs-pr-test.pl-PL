---
title: "aaaAzure zaawansowane wykrywanie zagrożeń | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat ochrony tożsamości i jego możliwości."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: 63e2c541fd4ce2c571af9d5845c9a9bd4b03b2a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-advanced-threat-detection"></a>Wykrywanie zagrożeń zaawansowane Azure
## <a name="introduction"></a>Wprowadzenie

### <a name="overview"></a>Omówienie

Firma Microsoft opracowała szereg oficjalne dokumenty, omówienie zabezpieczeń najlepsze rozwiązania i listy kontrolne tooassist Azure hello klientów dotyczące różnych funkcji zabezpieczeń dostępnych w i otaczającego hello platformy Azure. Tematy Hello zakresu pod względem szerokości i głębokość i są okresowo aktualizowane. Ten dokument jest częścią tej serii, zgodnie z opisem w powitania po sekcji abstrakcyjny.

### <a name="azure-platform"></a>Platformy Azure

Azure to platforma usługi chmury publicznej, która obsługuje hello wybór najszerszych systemów operacyjnych, programowania języków, struktury, narzędzia, baz danych i urządzeń.
Obsługuje następujące języki programowania hello:
-   Uruchom kontenery Linux z integracją rozwiązania Docker.
-   Tworzenie aplikacji za pomocą języka JavaScript, Python, .NET, PHP, Java i Node.js
-   Kompilacja zapleczy dla systemu iOS, Android i Windows urządzeń.

Usługi w chmurze publicznej Azure obsługuje hello już polegać na tej samej technologii miliony deweloperów i specjalistów IT i zaufania.

Podczas migrowania tooa chmury publicznej w organizacji, ta organizacja jest odpowiedzialny tooprotect danych i podaj zabezpieczeń i nadzór nad wokół hello systemu.

Zaprojektowano infrastruktury platformy Azure z tooapplications zakładzie hello jednocześnie hostingu miliony klientów i zapewnia foundation godne zaufania, na którym firmy mogą ich potrzeb zabezpieczeń. Azure oferuje szeroką gamę opcji tooconfigure i dostosować toomeet hello wymagań w zakresie zabezpieczeń stanu wdrożenia aplikacji. Ten dokument pomaga spełnić te wymagania.

### <a name="abstract"></a>Abstrakcyjny

Microsoft Azure oferuje wbudowane funkcje wykrywania advanced threat za pośrednictwem usług, takich jak Azure Active Directory, Azure Operations Management Suite (OMS) i Centrum zabezpieczeń Azure. Ta kolekcja usług zabezpieczeń i możliwości zapewnia toounderstand proste i szybkie sposób działania wykonywane w ramach wdrożeń platformy Azure.

Ten dokument zawiera informacje pomocne hello "Microsoft Azure podejścia" kierunku luki w zabezpieczeniach w przypadku zagrożenia diagnostycznych i analizy hello ryzyko związane z złośliwe działania hello przeznaczone dla serwerów i innych zasobów platformy Azure. Dzięki temu można tooidentify hello metod identyfikacji i luk w zabezpieczeniach zarządzania za pomocą zoptymalizowana rozwiązań hello platformy Azure i usług zabezpieczeń umożliwiających dostęp klienta i technologii.

Ten dokument koncentruje się na powitania technologii platformy Azure i kontrolek skierowane do klienta, a nie będzie podejmował tooaddress SLA cennik modeli i zagadnienia dotyczące praktyki DevOps.

## <a name="azure-active-directory-identity-protection"></a>Ochrona tożsamości w usłudze Azure Active Directory

![Ochrona tożsamości w usłudze Azure Active Directory](./media/azure-threat-detection/azure-threat-detection-fig1.png)


[Azure Active Directory Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection) jest funkcją hello [Azure AD Premium P2](https://docs.microsoft.com/azure/active-directory/active-directory-editions) edition, który umożliwia przegląd zdarzeń o podwyższonym ryzyku hello i potencjalne luki w organizacji tożsamości. Microsoft ma zostały zabezpieczających tożsamości opartej na chmurze za pośrednictwem dekadę i Azure AD Identity Protection, Microsoft jest wprowadzenie tych samych systemów ochrony klientów tooenterprise dostępne. Identity Protection korzysta z możliwości wykrywania anomalii istniejącej usługi Azure AD w dostępne za pośrednictwem [raporty dotyczące usługi Azure AD nietypowych działań](https://docs.microsoft.com/azure/active-directory/active-directory-view-access-usage-reports#anomalous-activity-reports)i wprowadza nowe typy zdarzeń ryzyka, które umożliwia wykrywanie anomalii w czasie rzeczywistym.

Identity Protection korzysta z algorytmów uczenia maszynowego adaptacyjną i anomalie toodetect Algorytm heurystyczny i zdarzenia ryzyka, które mogą wskazywać, że naruszono tożsamości. Przy użyciu tych danych, ochrona tożsamości generuje raporty i alerty, które pozwalają tooinvestigate te zdarzenia o podwyższonym ryzyku i podejmowanie odpowiednich działań korygujących lub migracji.

Ale Azure Active Directory Identity Protection jest większa niż przy użyciu narzędzi monitorowania i raportowania. Oparte na zdarzenia o podwyższonym ryzyku, Identity Protection oblicza poziom ryzyka użytkownika, dla każdego użytkownika, co pozwala chronić tooautomatically zasady oparte na ryzyko tooconfigure hello tożsamości organizacji.

Te zasady na podstawie ryzyka, w tooother dodanie [kontroli dostępu warunkowego](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) udostępniane przez usługi Azure Active Directory i [EMS](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access), można automatycznie blokować lub akcji korygowania adaptacyjną, które obejmują ofert Resetowanie haseł i wymuszania uwierzytelnianie wieloskładnikowe.

### <a name="identity-protections-capabilities"></a>Funkcje ochrony tożsamości

Azure Active Directory Identity Protection jest większa niż monitorowania i raportowania narzędzia. tooprotect tożsamości organizacji, można skonfigurować zasady stosowane na podstawie ryzyka odpowiadające automatycznie toodetected problemów, gdy zostanie osiągnięty poziom ryzyka określony. Te zasady dodatkowo tooother warunkowy dostęp do formantów zapewniane przez usługę Azure Active Directory i EMS, można automatycznie blokować lub zainicjować akcji korygowania adaptacyjną tym resetowanie haseł i wymuszania uwierzytelnianie wieloskładnikowe.

Przykłady niektórych metod hello Azure Identity Protection pomaga zabezpieczyć swoje konta i tożsamości obejmują:

[Wykrywanie zdarzenia o podwyższonym ryzyku i ryzykowne kont:](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#detection)
-   Wykrywanie sześć typów zdarzeń ryzykiem przy użyciu uczenia maszynowego i reguł heurystyczne
-   Obliczanie poziomów ryzyka użytkownika
-   Udostępnia zalecenia niestandardowych tooimprove ogólny stan zabezpieczeń przez wyróżnianie luk w zabezpieczeniach

[Badanie zdarzenia ryzyka:](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#investigation)
-   Wysyłanie powiadomienia o zdarzeniach ryzyka
-   Badania ryzyka zdarzeń za pomocą odpowiednich i kontekstowych informacji
-   Zapewnienie podstawowych przepływów pracy dochodzenia tootrack
-   Zapewniając łatwy dostęp tooremediation akcji, takich jak Resetowanie hasła

[Zasady dostępu warunkowego opartego na ryzyka:](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#risky-sign-ins)
-   Zasady toomitigate ryzykowne logowania przez blokowanie logowania lub wymaganie uwierzytelniania wieloskładnikowego wyzwania.
-   Zasady tooblock lub kont użytkowników ryzykowne bezpieczne
-   Zasady toorequire użytkowników tooregister uwierzytelnianie wieloskładnikowe

### <a name="azure-ad-privileged-identity-management-pim"></a>Usługa Azure AD Privileged Identity Management (PIM)

Z [usługi Azure Active Directory (AD) Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure),

![Azure AD Privileged Identity Management](./media/azure-threat-detection/azure-threat-detection-fig2.png)

Możesz zarządzanie, sterowanie i monitorowanie dostępu w organizacji. Obejmuje to tooresources dostępu w usłudze Azure AD i innych usług online firmy Microsoft, takich jak usługi Office 365 lub Microsoft Intune.

Azure AD Privileged Identity Management pomaga:

-   Alert zostanie wygenerowany i raport dotyczący administratorów usługi Azure AD i "just in time" tooMicrosoft dostępu administracyjnego usług Online, takich jak usługi Office 365 i Intune

-   Uzyskaj raporty dotyczące historii dostępu administratora i zmian w przypisaniach administratora

-   Uzyskiwanie alertów dotyczących ról uprzywilejowanych tooa dostępu

## <a name="microsoft-operations-management-suite-oms"></a>Microsoft Operations Management Suite (OMS)

[Microsoft Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) firmy Microsoft w chmurze IT rozwiązanie do zarządzania ułatwiające zarządzanie i ochrona lokalnej infrastruktury w chmurze. Ponieważ oprogramowanie OMS jest zaimplementowane jako usługa w chmurze, może być dostępne szybko przy minimalnym poziomie inwestycji w usługi infrastruktury. Nowe funkcje zabezpieczeń są przeprowadzane automatycznie, zapisywanie rutynowej konserwacji i zaktualizuj kosztów.

Ponadto tooproviding cenne usług na własną, OMS można zintegrować z składników programu System Center takich jak [System Center Operations Manager](https://blogs.technet.microsoft.com/cbernier/2013/10/23/monitoring-windows-azure-with-system-center-operations-manager-2012-get-me-started/) tooextend z dotychczasowych inwestycji zarządzania zabezpieczeń do hello w chmurze. System Center i OMS mogą współdziałać ze sobą tooprovide zarządzania pełne hybrydowego.

### <a name="holistic-security-and-compliance-posture"></a>Kompleksowe zabezpieczeń i stan zgodności

Hello [OMS zabezpieczeń i inspekcji pulpitu nawigacyjnego](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) daje szczegółowy wgląd w Twojej organizacji IT stan zabezpieczeń z wbudowaną zapytania dotyczące godne uwagi problemy wymagające uwagi. pulpit nawigacyjny zabezpieczeń i inspekcji Hello jest hello ekranu głównego dla wszystkich powiązanych toosecurity w OMS. Zawiera ogólne wgląd w stan zabezpieczeń hello komputerów. Obejmuje on też hello możliwości tooview wszystkie zdarzenia z hello poza 24 godzin, 7 dni lub innych niestandardowych przedziale czasu.

OMS pomocy pulpitów nawigacyjnych można szybko i łatwo zrozumieć hello ogólny stan zabezpieczeń innych środowiskach, w kontekście hello operacji IT, w tym: oceny aktualizacji oprogramowania, oceny ochrony przed złośliwym oprogramowaniem i linie bazowe konfiguracji. Ponadto danych dziennika zabezpieczeń jest łatwo dostępny toostreamline hello zabezpieczeń i zgodności inspekcji procesów.

pulpit nawigacyjny OMS zabezpieczeń i inspekcji Hello jest podzielone na cztery główne kategorie:

![Pulpit nawigacyjny Zabezpieczenia i inspekcja w pakiecie OMS](./media/azure-threat-detection/azure-threat-detection-fig3.jpg)

-   **Zabezpieczeń domeny:** w tym obszarze będą mogli toofurther Eksploruj rekordy zabezpieczeń w czasie, dostęp do oceny złośliwego oprogramowania, aktualizacji oceny, zabezpieczenia sieci, informacje o tożsamości i dostępu, komputery ze zdarzeniami zabezpieczeń oraz szybko pulpit nawigacyjny Centrum zabezpieczeń tooAzure dostępu.

-   **Godne uwagi problemy:** ta opcja umożliwia tooquickly określenie hello liczby aktywnych problemów i hello ważności tych problemów.

-   **Wykryć (wersja zapoznawcza):** umożliwia wzorców ataków tooidentify przez wizualizacja alerty zabezpieczeń, zgodnie z ich odbywać się z zasobami.

-   **Analizy zagrożeń:** umożliwia wzorców ataków tooidentify przez wizualizacja hello całkowita liczba serwery z wychodzącym ruchem złośliwego oprogramowania IP, typ złośliwe oprogramowanie hello i mapy, pokazujący, gdzie pochodzą z tych adresów IP.

-   **Typowe zapytania zabezpieczeń:** ta opcja zapewnia możesz listę najczęściej zabezpieczeń hello wysyła zapytanie do używania toomonitor środowiska. Po kliknięciu w jednym z tych zapytań zostanie otwarty blok wyszukiwania hello z hello wyników dla tego zapytania.

### <a name="insight-and-analytics"></a>Wgląd w dane i analizy
W środku hello [analizy dzienników](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) hello OMS repozytorium, która jest hostowana w hello chmury Azure.

![Wgląd w dane i analizy](./media/azure-threat-detection/azure-threat-detection-fig4.png)

Dane są zbierane w repozytorium hello z połączonych źródeł Konfigurowanie źródeł danych i dodawania subskrypcji tooyour rozwiązania.

![subskrypcja](./media/azure-threat-detection/azure-threat-detection-fig5.png)

Źródła danych i rozwiązania spowoduje utworzenie różnych typów rekordów własnych zbiór właściwości, które mogą być analizowane razem w repozytorium toohello zapytania. Dzięki temu hello toouse tego samego narzędzia i metody toowork z różnych rodzajów danych zbieranych przez różnych źródeł.


W większości współpracy z analizy dzienników jest za pośrednictwem portalu OMS hello, który jest uruchamiany w dowolnej przeglądarce i udostępnia ustawienia tooconfiguration dostępu i wielu narzędzi tooanalyze i ustawy o zebranych danych. Z hello portalu, możesz użyć [dziennika wyszukiwania](https://docs.microsoft.com/azure/log-analytics/log-analytics-log-searches) w przypadku, gdy tworzenia zapytań tooanalyze zebranych danych, [pulpity nawigacyjne](https://docs.microsoft.com/azure/log-analytics/log-analytics-dashboards), który można dostosować za pomocą graficznego widoków najbardziej przydatne wyszukiwania i [rozwiązań](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions), które zapewniają dodatkowe narzędzia funkcjonalność i analizy.

![narzędzia do analizy](./media/azure-threat-detection/azure-threat-detection-fig6.png)

Rozwiązania Dodaj funkcje tooLog Analytics. Przede wszystkim uruchamiania w chmurze hello i podaj analizy danych zebranych w repozytorium OMS hello. Mogą również określić nowe toobe typy rekordów zbierane z dziennika wyszukiwania lub przy użyciu interfejsu użytkownika dodatkowe podane przez rozwiązanie hello na pulpicie nawigacyjnym OMS hello umożliwia analizowanie.
Hello zabezpieczeń i inspekcji to przykład tego rodzaju rozwiązań.



### <a name="automation--control-alert-on-security-configuration-drifts"></a>Automatyzacja i kontrola: drifts alertu w konfiguracji zabezpieczeń

Automatyzacja Azure pozwala zautomatyzować procesów administracyjnych z elementami runbook, które są oparte na programie PowerShell i uruchom w hello chmury Azure. Elementy Runbook mogą być również wykonywane na serwerze w danych lokalnych zasobów lokalnych toomanage Centrum. Usługi Automatyzacja Azure umożliwia zarządzanie konfiguracją w usłudze Konfiguracja DSC środowiska PowerShell (konfiguracji żądanego stanu).

![Azure Automation](./media/azure-threat-detection/azure-threat-detection-fig7.png)

Można tworzyć i zarządzanie zasobami DSC hostowana na platformie Azure i zastosować je toocloud i lokalnymi toodefine systemów i automatycznie wymuszać ich konfiguracji lub Pobierz raporty na kilka toohelp ułatwieniu zapewnienia pozostawienie konfiguracjach zabezpieczeń w ramach zasad.

## <a name="azure-security-center"></a>Azure Security Center

Centrum zabezpieczeń Azure ułatwia ochronę zasobów platformy Azure. Zapewnia zabezpieczenia zintegrowane monitorowanie i zarządzanie zasadami subskrypcji platformy Azure. W ramach usługi hello jesteś w stanie toodefine zasady nie tylko z subskrypcjami platformy Azure, ale także przed [grup zasobów](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal), dlatego może być bardziej szczegółowego.

![Azure Security Center](./media/azure-threat-detection/azure-threat-detection-fig8.png)

Microsoft security pracowników naukowo-badawczych są stale na powitania poszukaj zagrożeń. Mają one zestaw obszernej tooan dostępu dane telemetryczne uzyskane na podstawie obecności globalnego firmy Microsoft w chmurze hello i lokalnych. Ta kolekcja osiągnięcia całej i różnych zestawów danych umożliwia Microsoft toodiscover nowe ataku wzorce i trendy między jego produkty konsumenckie i korporacyjne lokalnie, a także jej usług online.

W związku z tym Centrum zabezpieczeń można szybko aktualizować algorytmy wykrywania, ponieważ osoby atakujące wersji nowy, coraz bardziej zaawansowany luki w zabezpieczeniach. Takie podejście ułatwia sprostać środowisku przenoszenia fast zagrożeń.

![Security Center](./media/azure-threat-detection/azure-threat-detection-fig9.jpg)

Wykrywanie zagrożeń Centrum zabezpieczeń polega na automatyczne zbieranie informacji o zabezpieczeniach z zasobów platformy Azure, hello sieci i rozwiązań partnerskich połączonych.  Te informacje korelowanie informacji z wielu źródeł, zagrożenia tooidentify analizę.
Alerty zabezpieczeń mają pierwszeństwo w Centrum zabezpieczeń wraz z zaleceniami w sposób tooremediate hello zagrożeń.

Usługa Security Center wykorzystuje zaawansowane narzędzia analizy zabezpieczeń, które wykraczają daleko poza metody bazujące na sygnaturze. Osiągnięć w danych big data i [uczenia maszynowego](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) technologii są zdarzenia tooevaluate używanych w sieci szkieletowej chmury całego hello — wykrywanie zagrożeń, które mogą być niemożliwe tooidentify przy użyciu metod ręcznych i prognozowanie hello rozwój ataków. Te analizy zabezpieczeń obejmuje następujące hello.

### <a name="threat-intelligence"></a>Analiza zagrożeń

Firma Microsoft dysponuje ogromną ilością danych do globalnej analizy zagrożeń.
Dane telemetryczne przechodzi w z wielu źródeł, takich jak Azure, Office 365, Microsoft CRM online, Microsoft Dynamics AX, outlook.com, MSN.com, hello Microsoft jednostki ds. przestępstw cyfrowych (DCU) i Microsoft Security odpowiedzi Center (MSRC).

![Analiza zagrożeń](./media/azure-threat-detection/azure-threat-detection-fig10.jpg)

Pracownicy naukowo-badawczy również odbierać informacje analizy zagrożeń współużytkowany dostawcom usług w chmurze głównych i subskrybuje toothreat analizy źródeł innych firm. Centrum zabezpieczeń Azure można użyć tego tooalert informacji należy toothreats ze znanych nieupoważnione osoby. Oto niektóre przykłady:

-   **Wykorzystanie hello zasilania Machine Learning -** Centrum zabezpieczeń Azure ma dostęp tooa ogromnych ilości danych o aktywność w chmurze sieci, które mogą być używane zagrożenia toodetect przeznaczonych dla platformy Azure wdrożeń. Na przykład:

-   **Atak wykryć Force -** Machine learning to używane toocreate historycznych wzorzec prób dostępu zdalnego, co umożliwia toodetect ataków siłowych wobec portów SSH, RDP i SQL.

-   **Wychodzące DDoS i wykrywania Botnet** — typowe celem ataków przeznaczonych dla zasobów w chmurze jest moc obliczeniową hello toouse z tych zasobów tooexecute inne ataki.

-   **Nowe serwery analizy behawioralnej i maszyn wirtualnych -** po serwera lub maszyny wirtualnej zostanie naruszony, osoby atakujące stosować różnych technik tooexecute złośliwego kodu w tym systemie podczas unikanie wykrywania, zapewnienia trwałości i jak Opcje zabezpieczeń.

-   **Wykrywanie zagrożeń bazy danych Azure SQL -** wykrywanie zagrożeń bazy danych SQL Azure, który identyfikuje nietypowe działania bazy danych wskazujący nietypowe i potencjalnie szkodliwe prób tooaccess lub wykorzystać baz danych.

### <a name="behavioral-analytics"></a>Analiza behawioralna

Analizy behawioralnej to technika, która analizuje i porównuje zbierania danych tooa wzorców znane. Wzorce te nie są jednak prostymi sygnaturami. Są one określone za pomocą algorytmów uczenia maszynowego złożonych, które są stosowane toomassive zestawów danych.

![Analiza behawioralna](./media/azure-threat-detection/azure-threat-detection-fig11.jpg)


Są one również określane przez specjalistów od analizy, którzy dokonują dokładnej analizy złośliwych zachowań. Centrum zabezpieczeń Azure można użyć analizy behawioralnej tooidentify naruszony zasoby oparte na analizie dzienników maszyny wirtualnej, dzienniki urządzeń sieci wirtualnej, dzienniki sieci szkieletowej, zrzuty awaryjne i innych źródeł.

Ponadto jest korelacji z innych toocheck sygnałów do obsługi dowód powszechnie kampanii. Ta korelacja pomaga tooidentify zdarzenia, które są zgodne z ustalonych wskaźniki naruszenia.

Oto niektóre przykłady:
-   **Wykonanie procesu podejrzane:** osoby atakujące stosować kilka technik tooexecute złośliwego oprogramowania bez wykrywania. Na przykład osoba atakująca może nadać hello złośliwego oprogramowania tych samych nazw co wiarygodnego systemu plików, ale umieścić te pliki w innej lokalizacji, użyj nazwy, która jest bardzo podobna niegroźne pliku lub rozszerzenie true maska hello pliku. Centrum zabezpieczeń modeli procesów zachowania i monitory procesu wartości odstających toodetect wykonaniami takie.

-   **Ukryte przed złośliwym oprogramowaniem i wykorzystywania prób:** zaawansowane złośliwego oprogramowania można uniknięcia produktów tradycyjnych ochrony przed złośliwym kodem przy użyciu nigdy nie zapisywania toodisk lub szyfrowania składników oprogramowania przechowywane na dysku. Jednak takie złośliwego oprogramowania mogą być wykrywane przy użyciu analizy pamięci, jak złośliwe oprogramowanie hello musi pozostać dane śledzenia w pamięci toofunction. W przypadku awarii oprogramowania zrzutu awaryjnego przechwytuje część pamięci w czasie hello hello awarii (Crash). Analizując hello pamięci hello zrzutu awaryjnego, Centrum zabezpieczeń Azure można wykryć techniki stosowane tooexploit luk w zabezpieczeniach oprogramowania, dostęp do poufnych danych i utrwalić ukryty sposób na maszynie z naruszonymi zabezpieczeniami bez wpływu na wydajność hello tego komputera.

-   **Penetracji przepływu i Rekonesans wewnętrzny:** toopersist w złamany sieci i zlokalizuj zbiorów cennych danych, osoby atakujące często usiłują toomove bok z hello złamane tooothers maszyny w hello tej samej sieci. Centrum zabezpieczeń monitoruje proces i toodiscover działań logowania próbuje tooexpand stopień osoba atakująca w ramach sieci hello, takie jak zdalne wykonywanie polecenia, sondowanie sieci i wyliczania kont.

-   **Złośliwych skryptów środowiska PowerShell:** PowerShell mogą posłużyć osobom atakującym tooexecute złośliwego kodu na docelowych maszyn wirtualnych do różnych celów. Usługa Security Center sprawdza działanie programu PowerShell w poszukiwaniu dowodów na podejrzaną aktywność.

-   **Wychodzące ataków:** osoby atakujące często docelowych zasobów w chmurze z celem hello przy użyciu tych zasobów toomount dodatkowe ataków. Zagrożonych maszyn wirtualnych, na przykład może być używane toolaunch ataków siłowych wobec innych maszyn wirtualnych, wysyłania wiadomości-ŚMIECI lub skanowania otwartych portów i inne urządzenia na powitania Internet. Stosując machine learning toonetwork ruchu, Centrum zabezpieczeń może wykryć komunikacji sieciowej wychodzącego przekracza normy hello. Podczas wysyłania SPAMU, Centrum zabezpieczeń również są powiązane z ruchu nietypowe wiadomości e-mail z informacjami z usługi Office 365 toodetermine czy prawdopodobnie wiadomości powitania nefarious lub wynik hello kampanii uzasadnionych poczty e-mail.

### <a name="anomaly-detection"></a>Wykrywanie anomalii

Centrum zabezpieczeń Azure używa również zagrożenia tooidentify wykrywania anomalii. W module toobehavioral analiz kontrast, (która zależy od znane wzorce pochodzące z dużych zestawów danych) wykrywania anomalii jest bardziej "spersonalizowane" i koncentruje się na linie bazowe, które są określone tooyour wdrożeń. Machine learning to normalne działanie toodetermine zastosowanych wdrożeń, a następnie reguły zostaną wygenerowane toodefine odstające warunki, które może reprezentować zdarzeń zabezpieczeń. Oto przykład:

-   **Ruchu przychodzącego protokołu RDP/SSH ataków siłowych:** wdrożeń może być zajęta maszyn wirtualnych z wielu logowania do każdego dnia i innych maszyn wirtualnych, które mają niektórych lub żadnych uprawnień do logowania. Centrum zabezpieczeń Azure można ustalić aktywność logowania linii bazowej dla tych maszyn wirtualnych i używać machine learning toodefine wokół hello logowania normalnego działania. W przypadku niezgodności z linią bazową hello zdefiniowane dla skojarzone z logowaniem właściwości, a następnie można wygenerować alert. To uczenie maszynowe określa co jest istotne.

### <a name="continuous-threat-intelligence-monitoring"></a>Analizy zagrożeń ciągłego monitorowania

Centrum zabezpieczeń Azure działa z zabezpieczeń zespoły badawczo -danych nauki Witaj świecie które na stałe monitorowanie zmian w hello zagrożeń. Obejmuje to następujące inicjatyw hello:

-   **Monitorowanie analizy zagrożeń:** zagrożeń analizy zawiera mechanizmy, wskaźników, wpływ i możliwością porady dotyczące istniejących lub nowych zagrożeń. Te informacje są udostępniane w branży zabezpieczeń hello i Microsoft stale monitoruje źródła analizy zagrożeń wewnętrznych i zewnętrznych źródeł.

-   **Udostępnianie sygnału:** wgląd w dane dotyczące zabezpieczeń zespołów całej szerokie oferty firmy Microsoft w chmurze i lokalnych usług, serwerów i klientów urządzeń programu endpoint są udostępniane i przeanalizowane.

-   **Specjalistów zabezpieczeń firmy Microsoft:** trwającą interakcji użytkowników z zespołów przez Microsoft działające w polach zabezpieczeń specjalnych, takich jak danych dowodowych i wykrywanie ataków w sieci web.

-   **Dostrajanie wykrywania:** algorytmy są uruchamiane w odniesieniu do zestawów danych rzeczywistych klienta i bezpieczeństwa pracowników naukowo-badawczych pracy z wynikami hello toovalidate klientów. Wartość TRUE i false alarmów są algorytmów uczenia maszynowego toorefine używane.

Te połączonych działań kulminacyjny w wykryć nowe i ulepszone, które mogą korzystać z natychmiast — nie akcji dla tootake użytkownik.

## <a name="advanced-threat-detection-features---other-azure-services"></a>Funkcje wykrywania Advanced Threat — innymi usługami platformy Azure

### <a name="virtual-machine-microsoft-antimalware"></a>Maszyna wirtualna: Microsoft chroniące przed złośliwym kodem

[Microsoft Antimalware](https://docs.microsoft.com/azure/security/azure-security-antimalware) Azure to rozwiązanie jednego agenta do aplikacji i środowisk dzierżawy, zaprojektowany toorun w tle hello bez udziału człowieka. Można wdrożyć ochrony na podstawie potrzeb hello obciążeń aplikacji, z albo podstawowe secure domyślnie lub Zaawansowane Konfiguracja niestandardowa, w tym monitorowania ochrony przed złośliwym oprogramowaniem. Azure ochrony przed złośliwym kodem jest opcja zabezpieczeń dla maszyn wirtualnych platformy Azure i jest automatycznie instalowany na wszystkich maszynach wirtualnych Azure PaaS.

**Funkcje platformy Azure toodeploy i enable Antimalware firmy Microsoft dla aplikacji**

#### <a name="microsoft-antimalware-core-features"></a>Funkcje podstawowe ochrony przed złośliwym oprogramowaniem firmy Microsoft

-   **Ochrona w czasie rzeczywistym -** monitoruje aktywność usług w chmurze i maszyn wirtualnych toodetect i blokowanie wykonywania złośliwego oprogramowania.

-   **Zaplanowane skanowanie -** okresowo przesyła docelowe skanowania toodetect złośliwe oprogramowanie, w tym aktywnie uruchomione programy.

-   **Korygowania złośliwego oprogramowania -** automatycznie pobiera wykrytego złośliwego oprogramowania, takich jak usuwanie lub poddawania złośliwych plików i czyszczenie wpisy rejestru złośliwych działań.

-   **Aktualizacje podpisu —** automatycznie instaluje hello najnowsze ochrony podpisów (definicje wirusów) tooensure ochrona jest aktualne na wstępnie określoną częstotliwością.

-   **Aktualizacje aparatu ochrony przed złośliwym kodem —** automatycznie aktualizacje hello aparat Antimalware firmy Microsoft.

-   **Aktualizacje platformy ochrony przed złośliwym kodem —** automatycznie aktualizacje hello platformy Microsoft Antimalware.

-   **Active protection -** raporty metadanych dane telemetryczne dotyczące wykrytych zagrożeń i zasoby podejrzane tooMicrosoft Azure tooensure szybką odpowiedź toohello rozwijającymi zagrożeń i włączanie dostarczania w czasie rzeczywistym synchroniczne podpisu za pomocą Witaj systemu Microsoft Active Protection (MAPS).

-   **Przykłady raportowanie —** dostępnych i raportów przykłady toohelp usługi Microsoft Antimalware toohello uściślić hello usługi i Włącz rozwiązywania problemów.

-   **Wykluczenia —** aplikacji i tooconfigure administratorów usługi niektóre pliki, procesów i dyski tooexclude je z ochrony i skanowania dla wydajności i/lub innych powodów.

-   **Zbieranie zdarzeń ochrony przed złośliwym kodem —** rejestruje hello ochrony przed złośliwym kodem usługi kondycji, podejrzanych działań i korygowania akcje wykonywane w dzienniku zdarzeń systemu operacyjnego hello i zbiera je do konta magazynu Azure powitania klienta.

### <a name="azure-sql-database-threat-detection"></a>Wykrywanie zagrożeń bazy danych Azure SQL

[Wykrywanie zagrożeń bazy danych w usłudze Azure SQL](https://azure.microsoft.com/blog/azure-sql-database-threat-detection-your-built-in-security-expert/) to nowa funkcja analizy zabezpieczeń wbudowane hello usługi baza danych SQL Azure. Obchodzić hello zegara toolearn, profilu i wykrywa nietypowe działania bazy danych, wykrywanie zagrożeń bazy danych SQL Azure identyfikuje potencjalne zagrożenia toohello w bazie danych.

Funkcjonariusze lub innych administratorów wyznaczonych można uzyskać natychmiastowego wysłania powiadomienia o bazy danych podejrzanych działaniach miarę ich występowania. Każde powiadomienie zawiera szczegółowe informacje o podejrzanych działaniach hello i zaleca się, jak toofurther zbadać i uniknięcie hello zagrożenia.

Obecnie wykrywanie zagrożeń bazy danych SQL Azure wykrywa potencjalnych luk w zabezpieczeniach i ataki i wzorce dostępu nietypowych bazy danych.

Po otrzymaniu powiadomienia e-mail wykrywania zagrożeń, użytkownicy są możliwe toonavigate i widoku hello odpowiednich rekordów inspekcji przy użyciu hello głębokie łącze w wiadomości powitania, otwartym podgląd inspekcji i/lub wstępnie skonfigurowane inspekcji szablon programu Excel, pokazujący hello odpowiednich inspekcji rejestruje zdarzenie podejrzane hello zgodnie z następujących toohello hello czasie zbliżonym do:
-   Magazyn danych inspekcji dla powitania serwera bazy danych/z hello nietypowe działania bazy danych

-   Odpowiednie inspekcji magazynu tabeli, która została użyta w czasie hello dziennika inspekcji toowrite zdarzeń hello

-   Inspekcja rekordów powitania po godzinę, ponieważ hello zdarzenie.

-   Rekordy inspekcji podobne zdarzenia o identyfikatorze w czasie hello hello zdarzenia (opcjonalny w przypadku niektórych detektory)

Detektory zagrożeń bazy danych SQL, użyj jednej z hello następujące metody wykrywania:

-   **Wykrywanie deterministyczne —** wykrywa podejrzanych wzorców (na podstawie reguły) w zapytaniach powitania klienta SQL, zgodne znane ataki. Tej metody ma wykrywania wysoki i niski wynik fałszywie dodatni, jednak ograniczony zakres, ponieważ znajduje się w kategorii "wykryć atomic" hello.

-   **Wykrywanie zachowań —** wady nietypowych działań, które jest nietypowe zachowanie hello bazy danych, która nie była widoczna podczas hello ostatnich 30 dni.  Przykład nietypowych działań klienta SQL mogą być kolekcji nieudanych logowań/kwerendy, dużą liczbę wyodrębniania danych, nietypowe canonical zapytania i nieznane IP adresy używane tooaccess hello bazy danych

### <a name="application-gateway-web-application-firewall"></a>Zapora aplikacji sieci Web bramy aplikacji

[Zapora aplikacji sieci Web](https://docs.microsoft.com/azure/app-service-web/app-service-app-service-environment-web-application-firewall) jest funkcją [Azure Application Gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-webapplicationfirewall-overview) który zapewnia ochronę aplikacji tooweb, które używają bramy aplikacji dla standardowej [formant dostarczania aplikacji](https://kemptechnologies.com/in/application-delivery-controllers) funkcji. Zapora aplikacji sieci Web dzieje się tak, aby chronić je przed większość hello [OWASP pierwszych 10 znanych luk w sieci web](https://www.owasp.org/index.php/Top_10_2010-Main)

![Firewally aplikacji sieci Web bramy aplikacji](./media/azure-threat-detection/azure-threat-detection-fig13.png)

-   Ochrona przed atakami polegającymi na iniekcji SQL

-   Ochrona przed atakami z użyciem skryptów wykorzystywanych w obrębie wielu witryn

-   Częste ataki w ramach sieci Web polegające na iniekcji poleceń, przemycaniu żądań HTTP, rozdzielaniu odpowiedzi HTTP i zdalnym dołączaniu plików

-   Ochrona przed naruszeniami protokołu HTTP

-   Ochrona przed nieprawidłowościami protokołu HTTP, takimi jak brakujące powiązania agenta i użytkownika hosta oraz akceptowanie nagłówków

-   Zapobieganie atakom z użyciem robotów, przeszukiwarek i skanerów

-   Wykrycie typowych błędów konfiguracji aplikacji (czyli Apache usług IIS, itp.)

Konfigurowanie zapory aplikacji sieci Web w aplikacji bramy zapewnia następujące korzyści tooyou hello:

-   Ochrona aplikacji sieci web przed atakami bez modyfikacji kodu toobackend i luk w zabezpieczeniach sieci web.

-   Ochrona wielu sieci web aplikacji hello sam czas za bramy aplikacji. Brama aplikacji w obsługuje hosting się too20 witryn sieci Web za jednym bramy, która może być wszystkie chronione przed atakami opartymi na sieci web.

-   Monitorowanie aplikacji sieci Web pod kątem ataków przy użyciu raportu w czasie rzeczywistym generowanego przez dzienniki zapory aplikacji sieci Web bramy aplikacji.

-   Niektóre formanty zgodności wymagają wszystkich internetowy toobe punktów końcowych chronionych przez rozwiązanie zapory aplikacji sieci Web. Korzystając z bramy aplikacji z zaporą aplikacji sieci Web, można spełnić te wymagania zgodności.

### <a name="anomaly-detection--an-api-built-with-azure-machine-learning"></a>Wykrywanie anomalii — interfejs API skompilowanej za pomocą usługi Azure Machine Learning

Wykrywanie anomalii to interfejs API skompilowanej za pomocą usługi Azure Machine Learning jest przydatne w przypadku wykrywania różnych typów nietypowe wzorce w danych serii czasu. Witaj interfejsu API przypisuje anomalii wynik tooeach punkt hello szeregów czasowych, która może służyć do generowania alertów, monitorowanie za pomocą pulpitów nawigacyjnych lub nawiązać połączenie z systemu obsługi biletów.

Witaj [API wykrywania anomalii](https://docs.microsoft.com/azure/machine-learning/machine-learning-apps-anomaly-detection-api) może wykrywać następujące typy anomalii na czas serii danych hello:

-   **Wzrósł i DIP:** na przykład podczas monitorowania liczby hello usługi tooa błędy logowania lub liczbę wyewidencjonowań w witrynie handlu elektronicznego, nietypowych wzrostów DIP może wskazywać ataki lub zakłócenia w świadczeniu usługi.

-   **Dodatnie i ujemne trendów:** podczas monitorowania użycia pamięci w przypadku komputerów, na przykład zmniejszanie rozmiaru wolnej pamięci jest wskaźnikiem potencjalny wyciek pamięci; podczas monitorowania usługi długość kolejki, trwałe tendencję może wskazywać podstawowej problem z oprogramowaniem.

-   **Poziom zmiany i dynamicznych spoza zakresu:** na przykład poziom zmiany w opóźnienia usługi po usługi uaktualniania lub niższe poziomy wyjątków, po uaktualnieniu może być interesujące toomonitor.

uczenie maszynowe Hello oparte interfejsu API umożliwia:

-   **Wykrywanie elastyczna i niezawodna:** modeli wykrywania anomalii hello użytkownicy tooconfigure czułości ustawienia i wykrywania anomalii między zestawami danych okresach i okresach. Użytkownik może zmienić model wykrywania anomalii hello toomake wykrywania hello interfejsu API mniej lub bardziej poufnego zgodnie z tootheir wymaga. Oznacza to, czy wykrywanie hello mniej lub więcej anomalii widoczne w danych z włączonymi i wyłączonymi okresach wzorce.

-   **Skalowalna i odpowiednim wykrywania:** hello tradycyjny sposób monitorowania z progami obecne określone przez ekspertów wiedzy domeny są kosztowne i nie jest skalowalna toomillions zmieniających się dynamicznie zestawów danych. modele wykrywania anomalii Hello w tym interfejsie API są rozpoznawane i modele są automatycznie dopasowane dane historyczne jak w czasie rzeczywistym.

-   **Aktywne i można wykonać wykrywania:** trend powolne i wykrywania zmiany poziomu mogą być stosowane do wczesnego wykrywania anomalii. Hello wczesne sygnały nietypowe wykryto można tooinvestigate ludzi toodirect używane i działają na powitania obszarów problemów.  Ponadto Przyczyna modeli analizy i alertów narzędzia mogą być opracowane na podstawie to wykrywanie anomalii usługi interfejsu API.

wykrywanie anomalii Hello interfejsu API to rozwiązanie wydajny i efektywny dla szerokiego zakresu scenariuszy, takich jak kondycja usługi & kluczowego wskaźnika wydajności monitorowania IoT, monitorowanie wydajności i monitorowanie ruchu sieciowego. Poniżej przedstawiono kilka scenariuszy popularnych, w którym ten interfejs API może być przydatna:
- Działy IT muszą zdarzenia tootrack narzędzi, kod błędu dziennika użycia i wydajności (Procesora, pamięci i tak dalej) w odpowiednim czasie.

-   Witryn handlu online mają działania klienta tootrack, wyświetleń strony, kliknięć i tak dalej.

-   Narzędzie firmach tootrack zużycia wody, gazu, energii elektrycznej i innych zasobów.

-   Zakładzie/budynku usług zarządzania, która ma toomonitor temperatury, wilgotności, ruchu i tak dalej.

-   IoT/producentów mają toouse danych czujnika w czasie serii toomonitor przepływu pracy, jakości i tak dalej.

-   Dostawcy usług, takie jak biura obsługi muszą trend żądanie usługi toomonitor, liczba zdarzeń, poczekaj długość kolejki i tak dalej.

-   Grupy analiza biznesowa ma toomonitor biznesowe wskaźniki KPI (takie jak sprzedaż, opinie klientów, cennik) nietypowe ruchu w czasie rzeczywistym.

### <a name="cloud-app-security"></a>Usługa cloud App Security

[Cloud App Security](https://docs.microsoft.com/cloud-app-security/what-is-cloud-app-security) jest składnikiem krytycznym hello Microsoft Cloud Security stosu. To kompleksowe rozwiązanie, które mogą pomóc Twojej organizacji, jak przenieść tootake zalet promise hello aplikacji w chmurze, ale można przechowywać w kontroli dzięki ulepszonemu wglądowi w działanie. Pomaga również zwiększenia hello ochrony kluczowych danych w aplikacjach w chmurze.

Z narzędzia, które ułatwiają odkrywanie tle IT, ocenie ryzyka egzekwowanie zasad, badaniu działań i zatrzymywaniu zagrożeń organizacji bardziej bezpiecznie przenieść toohello chmury przy zachowaniu kontroli danych o kluczowym znaczeniu.

<table style="width:100%">
 <tr>
   <td>Wykrywanie</td>
   <td>Odkrywanie tle działu informatycznego dysponujące Cloud App Security. Zyskaj widoczność przez odnajdywanie aplikacji, działań, użytkowników, danych i plików w środowisku chmury. Odnajdywanie aplikacji innych firm, które są połączone tooyour chmury.</td>
 </tr>
 <tr>
   <td>Zbadaj</td>
   <td>Zbadaj aplikacji w chmurze przy użyciu chmury dowodowe narzędzia toodeep szczegółowo w ryzykowne aplikacje, konkretnych użytkowników i plików w sieci. Znajdź wzorce hello danych zebranych z chmury. Generowanie raportów toomonitor chmury.</td>

 </tr>
 <tr>
   <td>Formant</td>
   <td>Ogranicz ryzyko przez skonfigurowanie zasad i alertów tooachieve maksymalną kontrolę ruchu sieciowego w chmurze. Użyj toomigrate Cloud App Security toosafe Twojego użytkowników, chmury oficjalnie zaakceptowanych aplikacji alternatyw.</td>

 </tr>
 <tr>
   <td>Ochrona</td>
   <td>Użyj toosanction Cloud App Security lub Zabroń używania aplikacji, wymuszać zapobieganie utracie danych, uprawnienia kontroli i udostępniania i generować raporty niestandardowe i alerty.</td>

 </tr>
 <tr>
   <td>Formant</td>
   <td>Ogranicz ryzyko przez skonfigurowanie zasad i alertów tooachieve maksymalną kontrolę ruchu sieciowego w chmurze. Użyj toomigrate Cloud App Security toosafe Twojego użytkowników, chmury oficjalnie zaakceptowanych aplikacji alternatyw.</td>

 </tr>
</table>


![Usługa cloud App Security](./media/azure-threat-detection/azure-threat-detection-fig14.png)

Usługa cloud App Security integruje widoczności z chmurą przez

-   Przy użyciu funkcji Cloud Discovery toomap oraz identyfikację środowiska chmury i hello organizacja korzysta z aplikacji w chmurze.


-   Oficjalne akceptowanie lub zabronienia aplikacji w chmurze.



-   Używanie łączników łatwa do wdrożenia aplikacji, które korzystają z dostawcy interfejsów API, widoczność i ładu aplikacji łączących się z.

-   Pomaga ma ciągła kontrola ustawienie i stałe dostrajanie, zasad.

Na zbieranie danych z tych źródeł, Cloud App Security uruchamia zaawansowane analizy na powitania danych. Natychmiast go ostrzega tooanomalous działań i umożliwia dokładną widoczność w środowisku chmury. Możesz skonfigurować zasady w usłudze Cloud App Security i użyć go tooprotect wszystko w środowisku chmury.

## <a name="third-party-atd-capabilities-through-azure-marketplace"></a>Możliwości ATD innej firmy za pomocą portalu Azure Marketplace

### <a name="web-application-firewall"></a>Zapora aplikacji sieci Web

Zapora aplikacji sieci Web sprawdza sieci web dla ruchu przychodzącego ruchu i bloki iniekcji SQL, Cross-Site skryptów, złośliwego oprogramowania przekazywania & aplikacji przed atakami DDoS oraz inne ataki celem aplikacji sieci web. Sprawdza również hello odpowiedzi z serwerów sieci web zaplecza powitania dla zapobiegania utracie danych (DLP). Aparat kontroli dostępu zintegrowane Hello włącza zasady kontroli dostępu szczegółowego toocreate Administratorzy dla uwierzytelniania, autoryzacji i Ewidencjonowanie, która umożliwia organizacjom silnego uwierzytelniania i kontroli użytkownika.

**Najważniejsze funkcje:**
-   Wykrywa i blokuje SQL iniekcji, skryptów krzyżowych, przekazywanie złośliwego oprogramowania, aplikacji przed atakami DDoS lub inne ataki aplikacji.

-   Uwierzytelnianie i kontrola dostępu.

-   Skanuje dane poufne toodetect ruch wychodzący i można zamaskować lub blokowania informacji hello wyciek.

-   Przyspiesza hello dostarczania zawartości aplikacji sieci web, za pomocą funkcji, takich jak pamięci podręcznej, kompresji i inne optymalizacje ruchu.

Poniżej przedstawiono przykład dostępne w usłudze Azure rynek zapory aplikacji sieci Web:

[Zapora aplikacji sieci Web barracuda, Zapora Brocade do aplikacji wirtualnych sieci Web (Brocade vWAF), Imperva SecureSphere i hello ThreatSTOP IP zapory.](https://azure.microsoft.com/marketplace/partners/brocade_communications/brocade-virtual-web-application-firewall-templatevtmcluster/)

## <a name="next-steps"></a>Następne kroki

- [Funkcje wykrywania usługi Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities)

Możliwości wykrywania zaawansowanych Centrum zabezpieczeń Azure pomaga tooidentify zagrożenia active przeznaczonych dla zasobów platformy Microsoft Azure i zapewnia się, że z informacjami dotyczącymi hello potrzebne toorespond szybko.

- [Wykrywanie zagrożeń bazy danych Azure SQL](https://azure.microsoft.com/blog/azure-sql-database-threat-detection-your-built-in-security-expert/)

Wykrywanie zagrożeń bazy danych w usłudze Azure SQL pomogła rozwiązania ich problemów dotyczących potencjalnych zagrożeń tootheir w bazie danych.
