---
title: "możliwości aaaDetection w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument ułatwia toounderstand sposób działania funkcji wykrywania Centrum zabezpieczeń Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 4c5599cc-99a1-430f-895f-601615ef12a0
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: d8001cc2acdd0026bd9b3596bbdfec56f8874513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-detection-capabilities"></a>Funkcje wykrywania usługi Azure Security Center
Ten dokument zawiera omówienie Centrum zabezpieczeń Azure wykrywania zaawansowanych funkcji, które ułatwia zidentyfikowanie active zagrożenia przeznaczonych dla zasobów platformy Microsoft Azure i zapewnia możliwość z informacjami dotyczącymi hello potrzebne toorespond szybko.

> [!NOTE]
> Wykryć zaawansowane są dostępne w hello standardowe warstwy z Centrum zabezpieczeń Azure. Dostępna jest bezpłatna 60-dniowa wersja próbna. Można uaktualnić hello wybranej warstwy cenowej w hello [zasady zabezpieczeń](security-center-policies.md). Odwiedź stronę [strony Centrum zabezpieczeń](https://azure.microsoft.com/pricing/details/security-center/) toolearn więcej o cenach. 
> 
> 

## <a name="responding-tootodays-threats"></a>Odpowiada tootoday tego zagrożenia
Miały miejsce znaczące zmiany w hello zagrożeń za pośrednictwem hello ostatnich lat 20. W przeszłości hello firmy zwykle tylko nastąpiło tooworry o atak skutkujący zmianą zawartości witryny sieci web przez poszczególne osoby atakujące, które przede wszystkim były planuje się oglądanie "co może zrobić to". Obecnie osoby atakujące są bardziej wyrafinowane i zorganizowane. Często mają określone cele finansowe i strategiczne. Ma także toothem dostępnych więcej zasobów, jak mogą być finansowane kraj lub przestępstw zorganizowanej.

Takie podejście spowodowało tooan Niespotykana poziomu profesjonalizmu w hello atakująca rangi. Nie wystarcza im już wpływ na zawartość witryn internetowych. Są one obecnie zainteresowani kradzież informacje, konta i dane prywatne — z których można użyć toogenerate pobraniem hello otwartego rynku lub tooleverage określonego rodzaju, pozycja polityczną lub godzina. Dotyczące więcej niż te osoby atakujące finansowych celu hello osoby atakujące, które naruszają tooinfrastructure obrażeniami toodo sieci i osoby.

W odpowiedzi organizacje często wdrażanie różnych rozwiązań punktu, które skupić się na obrony działania przedsiębiorstwa hello lub punktów końcowych, wyszukując podpisów znanych ataku. Te rozwiązania często toogenerate dużą liczbę alerty niskiej rozdzielczości, które wymagają tootriage analityk zabezpieczeń i Zbadaj. Większość organizacji braku hello czasu i wiedzy toorespond toothese alerty — tak wielu Przejdź nierozwiązane.  W tym samym czasie, osoby atakujące usprawnionych ich toosubvert metody wiele zabezpieczenia na podstawie podpisu i [dostosowanie środowiska toocloud](https://azure.microsoft.com/blog/detecting-threats-with-azure-security-center/). Nowe podejście są wymagane toomore szybko zidentyfikować zagrożenia pojawiające się i przyspieszenia wykrywania i odpowiedzi. 

## <a name="how-azure-security-center-detects-and-responds-toothreats"></a>Jak Centrum zabezpieczeń Azure wykrywa i odpowiada toothreats
Microsoft security pracowników naukowo-badawczych są stale na powitania poszukaj zagrożeń. Mają one zestaw obszernej tooan dostępu dane telemetryczne uzyskane na podstawie obecności globalnego firmy Microsoft w chmurze hello i lokalnych. Ta kolekcja osiągnięcia całej i różnych zestawów danych umożliwia Microsoft toodiscover nowe ataku wzorce i trendy między jego produkty konsumenckie i korporacyjne lokalnie, a także jej usług online. W związku z tym usługa Security Center może szybko zaktualizować swoje algorytmy wykrywania, w miarę jak atakujący wprowadzają nowe i coraz bardziej zaawansowane metody. Takie podejście pomaga sprostać wymaganiom szybko zmieniającego się środowiska zagrożenia. 

Wykrywanie zagrożeń Centrum zabezpieczeń polega na automatyczne zbieranie informacji o zabezpieczeniach z zasobów platformy Azure, hello sieci i rozwiązań partnerskich połączonych. Te informacje, często korelowanie informacji z wielu źródeł, zagrożenia tooidentify analizę. Alerty zabezpieczeń mają pierwszeństwo w Centrum zabezpieczeń wraz z zaleceniami w sposób tooremediate hello zagrożeń.

![Prezentacja i zbieranie danych przez usługę Security Center](./media/security-center-detection-capabilities/security-center-detection-capabilities-fig1.png)

Usługa Security Center wykorzystuje zaawansowane narzędzia analizy zabezpieczeń, które wykraczają daleko poza metody bazujące na sygnaturze. Osiągnięć w danych big data i [uczenia maszynowego](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) technologii są zdarzenia tooevaluate wykorzystywana w sieci szkieletowej chmury całego hello — wykrywanie zagrożeń, które mogą być niemożliwe tooidentify przy użyciu metod ręcznych i prognozowanie hello rozwój ataków. Do narzędzi analizy zabezpieczeń należą: 

* **Zintegrowane analizy zagrożeń**: wygląda dla znanych nieupoważnione dzięki wykorzystaniu globalnej analizy zagrożeń ze swoich produktów i usług, hello Microsoft cyfrowego ds. przestępstw jednostki (DCU), hello Microsoft Security odpowiedzi Center (MSRC) i zewnętrznego źródła danych.
* **Analizy behawioralnej**: stosuje znane wzorce toodiscover złośliwego zachowania. 
* **Wykrywanie anomalii**: używa statystyczne profilowania toobuild historycznych linii bazowej. Generuje alert w odchylenia od ustalonych linii bazowych, zgodnych ze standardami tooa potencjalnego ataku.

### <a name="threat-intelligence"></a>Analiza zagrożeń
Firma Microsoft dysponuje ogromną ilością danych do globalnej analizy zagrożeń. Dane telemetryczne przepływy w z wielu źródeł, takich jak Azure, Office 365, Microsoft CRM online, Microsoft Dynamics AX, outlook.com, MSN.com, hello Microsoft jednostki ds. przestępstw cyfrowych (DCU) i Microsoft Security odpowiedzi Center (MSRC). Pracownicy naukowo-badawczy również odbierać informacje analizy zagrożeń współużytkowany dostawcom usług w chmurze głównych i subskrybuje toothreat analizy źródeł innych firm. Centrum zabezpieczeń Azure można użyć tego tooalert informacji należy toothreats ze znanych nieupoważnione osoby. Oto niektóre przykłady:

* **Adres IP złośliwe tooa komunikacji wychodzącej**: tooa ruch wychodzący znanych botnet lub darknet prawdopodobnie wskazuje, że zasób został złamany atakujący go próby tooexecute polecenia systemu lub exfiltrate danych. Centrum zabezpieczeń Azure porównuje bazy danych globalnych zagrożeń tooMicrosoft ruchu sieciowego i ostrzega użytkownika o wykryje komunikacji tooa złośliwe adresu IP.

## <a name="behavioral-analytics"></a>Analiza behawioralna
Analizy behawioralnej to technika, która analizuje i porównuje zbierania danych tooa wzorców znane. Wzorce te nie są jednak prostymi sygnaturami. Są one określone za pomocą algorytmów uczenia maszynowego złożonych, które są stosowane toomassive zestawów danych. Są one również określane przez specjalistów od analizy, którzy dokonują dokładnej analizy złośliwych zachowań. Centrum zabezpieczeń Azure można użyć analizy behawioralnej tooidentify naruszony zasoby oparte na analizie dzienników maszyny wirtualnej, dzienniki urządzeń sieci wirtualnej, dzienniki sieci szkieletowej, zrzuty awaryjne i innych źródeł. 

Ponadto jest korelacji z innych toocheck sygnałów do obsługi dowód powszechnie kampanii. Ta korelacja pomaga tooidentify zdarzenia, które są zgodne z ustalonych wskaźniki naruszenia. Oto niektóre przykłady:

* **Wykonanie procesu podejrzane**: osoby atakujące stosować kilka technik tooexecute złośliwego oprogramowania bez wykrywania. Na przykład osoba atakująca może nadać hello złośliwego oprogramowania tych samych nazw co wiarygodnego systemu plików, ale umieścić te pliki w innej lokalizacji, użyj nazwy, która jest bardzo podobne tooa niegroźne, lub plik hello maska true rozszerzenie pliku. Centrum zabezpieczeń modeli procesów zachowania i monitory procesu wartości odstających toodetect wykonaniami takie.  
* **Ukryte przed złośliwym oprogramowaniem i wykorzystywania prób**: Zaawansowane złośliwego oprogramowania jest produktów tradycyjnych ochrony przed złośliwym kodem tooevade może nigdy nie zapisywania toodisk lub szyfrowania składników oprogramowania przechowywane na dysku.  Jednak takie złośliwego oprogramowania mogą być wykrywane przy użyciu analizy pamięci, jak złośliwe oprogramowanie hello musi pozostać dane śledzenia w pamięci w kolejności toofunction. W przypadku awarii oprogramowania zrzutu awaryjnego przechwytuje część pamięci w czasie hello hello awarii (Crash).  Analizując hello pamięci hello zrzutu awaryjnego, Centrum zabezpieczeń Azure mogą wykrywać techniki stosowane tooexploit luk w zabezpieczeniach oprogramowania, dostęp do poufnych danych i ukryty sposób utrwalić w ramach którego bezpieczeństwo zostało naruszone komputera bez wpływu na wydajność hello tego komputera.
* **Penetracji przepływu i Rekonesans wewnętrzny**: toopersist w złamany sieci i zlokalizuj zbiorów cennych danych, osoby atakujące często usiłują toomove bok z hello złamane tooothers maszyny w hello tej samej sieci. Centrum zabezpieczeń monitoruje proces i działań logowania w kolejności toodiscover prób tooexpand stopień osoba atakująca w ramach sieci hello, takich jak polecenia zdalnego wykonywania sieci sondowanie i wyliczania kont.
* **Złośliwych skryptów PowerShell**: programu PowerShell jest używany przez osoby atakujące tooexecute złośliwego kodu na docelowych maszyn wirtualnych do różnych celów. Usługa Security Center sprawdza działanie programu PowerShell w poszukiwaniu dowodów na podejrzaną aktywność. 
* **Wychodzące ataków**: osoby atakujące często docelowych zasobów w chmurze z celem hello przy użyciu tych zasobów toomount dodatkowe ataków. Zagrożonych maszyn wirtualnych, na przykład może być używane toolaunch ataków siłowych wobec innych maszyn wirtualnych, wysyłania SPAMU lub skanowania otwartych portów i inne urządzenia na hello internet. Stosując machine learning toonetwork ruchu, Centrum zabezpieczeń może wykryć komunikacji sieciowej wychodzącego przekracza normy hello. W przypadku hello wiadomości-ŚMIECI, Centrum zabezpieczeń również są powiązane z ruchu nietypowe wiadomości e-mail z informacjami z usługi Office 365 toodetermine czy prawdopodobnie wiadomości powitania nefarious lub wynik hello kampanii uzasadnionych poczty e-mail.  

### <a name="anomaly-detection"></a>Wykrywanie anomalii
Centrum zabezpieczeń Azure używa również zagrożenia tooidentify wykrywania anomalii. W module toobehavioral analiz kontrast, (która zależy od znane wzorce pochodzące z dużych zestawów danych) wykrywania anomalii jest bardziej "spersonalizowane" i koncentruje się na linie bazowe, które są określone tooyour wdrożeń. Machine learning to normalne działanie toodetermine zastosowanych wdrożeń, a następnie reguły zostaną wygenerowane toodefine odstające warunki, które może reprezentować zdarzeń zabezpieczeń. Oto przykład:

* **Przychodzące ataki siłowe RDP/SSH**: wdrożenia mogą mieć do czynienia z maszynami wirtualnymi o dużej ilości logowań każdego dnia lub maszynami wirtualnymi o bardzo nielicznych logowaniach lub żadnych. Centrum zabezpieczeń Azure można ustalić aktywność logowania linii bazowej dla tych maszyn wirtualnych i używać machine learning toodefine, co to jest poza logowania normalnego działania. Jeśli hello liczba logowań lub godzina hello hello logowania lub hello lokalizacji, z których hello wymagane są logowania lub inne właściwości skojarzone z logowaniem są znacznie różni się od linii bazowej hello, można wygenerować alert. To uczenie maszynowe określa co jest istotne.

## <a name="continuous-threat-intelligence-monitoring"></a>Ciągłe monitorowanie analizy zagrożeń
Centrum zabezpieczeń Azure działa zabezpieczeń zespoły badawczo -danych nauki które na stałe monitorowanie zmian w hello zagrożeń. Obejmuje to następujące inicjatyw hello:

* **Monitorowanie analizy zagrożeń**: analiza zagrożeń obejmuje mechanizmy, wskaźniki, konsekwencje i wiarygodne porady dotyczące istniejących lub pojawiających się zagrożeń. Te informacje są udostępniane w branży zabezpieczeń hello i Microsoft stale monitoruje źródła analizy zagrożeń wewnętrznych i zewnętrznych źródeł.
* **Udostępnianie sygnału**: uwagi zespołów ds. zabezpieczeń formułowane na podstawie informacji zebranych z szerokiej gamy produktów firmy Microsoft, takich jak usługi w chmurze i usługi lokalne, serwery i urządzenia klienckie w punkcie końcowym, są udostępniane i analizowane. 
* **Specjaliści ds. zabezpieczeń firmy Microsoft**: ciągła współpraca zespołów firmy Microsoft w zakresie wyspecjalizowanych zabezpieczeń, takich jak analiza śledcza i wykrywanie ataków w sieci Web.
* **Dostrajanie wykrywania**: algorytmy są uruchamiane w odniesieniu do zestawów danych rzeczywistych klienta i bezpieczeństwa pracowników naukowo-badawczych pracy z wynikami hello toovalidate klientów. Wartość TRUE i false alarmów są algorytmów uczenia maszynowego toorefine używane.

Te połączonych działań kulminacyjny w wykryć nowe i ulepszone, które mogą korzystać z natychmiast — nie akcji dla tootake użytkownik.

## <a name="see-also"></a>Zobacz też
W tym dokumencie przedstawiono sposób działania funkcji wykrywania Centrum zabezpieczeń tooAzure. toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

* [Przewodnik planowania i obsługi usługi Azure Security Center](security-center-planning-and-operations-guide.md)
* [Reagowanie na alerty toosecurity w Centrum zabezpieczeń Azure i zarządzanie nimi](security-center-managing-and-responding-alerts.md)
* [Alerty zabezpieczeń według typu w usłudze Azure Security Center](security-center-alerts-type.md)
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.
* [Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Blog Azure Security](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń i zgodności platformy Azure.

