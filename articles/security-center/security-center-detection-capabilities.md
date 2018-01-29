---
title: "Funkcje wykrywania w usłudze Azure Security Center | Microsoft Docs"
description: "Ten dokument pomaga zrozumieć, jak działają funkcje wykrywania usługi Azure Security Center."
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
ms.date: 09/20/2017
ms.author: yurid
ms.openlocfilehash: edef9bc1ba2420a4b7d95f891fd8b0b7e144c2ae
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="azure-security-center-detection-capabilities"></a>Funkcje wykrywania usługi Azure Security Center
W tym dokumencie omówiono zaawansowane funkcje wykrywania usługi Azure Security Center, która ułatwia identyfikację aktywnych zagrożeń atakujących zasoby platformy Microsoft Azure i udostępnia potrzebne informacje w celu szybkiego reagowania.

Funkcje zaawansowanego wykrywania są dostępne w warstwie Standardowa usługi Azure Security Center. Dostępna jest bezpłatna 60-dniowa wersja próbna. Uaktualnienie usługi jest możliwe po przejściu do wyboru warstwy cenowej na stronie [Zasady zabezpieczeń](security-center-policies.md). Odwiedź [stronę usługi Security Center](https://azure.microsoft.com/pricing/details/security-center/), aby dowiedzieć się więcej na temat cen. 

> [!NOTE]
> Usługa Security Center została wydana w ograniczonej wersji zapoznawczej z nowym zestawem funkcji wykrywania, które wykorzystują rekordy inspekcji, czyli wspólną platformę inspekcji, do wykrywania złośliwych zachowań na maszynach z systemem Linux. Wyślij [nam](mailto:ASC_linuxdetections@microsoft.com) wiadomość e-mail ze swoim identyfikatorem subskrypcji, aby dołączyć do tej wersji zapoznawczej.

## <a name="responding-to-todays-threats"></a>Odpowiadanie na nowe rodzaje zagrożeń
W ciągu ostatnich 20 lat miały miejsce istotne zmiany dotyczące charakteru występujących zagrożeń. W przeszłości firmy martwiły się tylko atakami skutkującymi zmianą zawartości witryny internetowej, a sami atakujący chcieli przede wszystkim przekonać się, co potrafią zrobić. Obecnie osoby atakujące są bardziej wyrafinowane i zorganizowane. Często mają określone cele finansowe i strategiczne. Ponadto dysponują większą ilością zasobów, ponieważ mogą być finansowane przez państwa lub zorganizowane grupy przestępcze.

Takie podejście doprowadziło do osiągnięcia niespotykanego poziomu profesjonalizmu przez osoby atakujące. Nie wystarcza im już wpływ na zawartość witryn internetowych. Teraz atakujący są zainteresowani wykradaniem informacji, kont finansowych i prywatnych danych, które mogą wykorzystać do generowania środków pieniężnych na wolnym rynku lub do wywierania wpływu na politykę, gospodarkę czy wojsko. Bardziej niepokojący od osób o motywach finansowych są atakujący, którzy naruszają bezpieczeństwo sieci, aby uszkodzić infrastrukturę lub zaszkodzić ludziom.

W odpowiedzi na takie działania organizacje często wdrażają różne rozwiązania punktowe, które poprzez wyszukiwanie znanych sygnatur ataku koncentrują się na obronie obwodów lub punktów końcowych przedsiębiorstwa. Tego typu rozwiązania zazwyczaj generują duże ilości alertów niskiej jakości, które wymagają dokonania klasyfikacji i przeprowadzenia badań przez analityka zabezpieczeń. Większość organizacji nie dysponuje czasem i niezbędną wiedzą, które umożliwiłyby odpowiednie zareagowanie na te ostrzeżenia — wiele z nich nie jest rozwiązywanych.  Tymczasem osoby atakujące usprawniły swoje metody tak, aby móc złamać wiele zabezpieczeń opartych na sygnaturze, a prowadzone działania [dostosować do środowisk w chmurze](https://azure.microsoft.com/blog/detecting-threats-with-azure-security-center/). Wymagane jest nowe podejście do problemu zabezpieczeń, które pozwoliłoby na szybszą identyfikację potencjalnych zagrożeń, a także przyspieszone wykrywanie ich i reagowanie na nie. 

## <a name="how-azure-security-center-detects-and-responds-to-threats"></a>Jak usługa Azure Security Center wykrywa zagrożenia i reaguje na nie
Pracownicy naukowo-badawczy firmy Microsoft stale poszukują nowych zagrożeń. Mają oni dostęp do szerokiej gamy rozwiązań telemetrycznych uzyskanych dzięki obecności firmy Microsoft na całym świecie zarówno w chmurze, jak i lokalnie. Bogata i różnorodna kolekcja zestawów danych pozwala firmie Microsoft odnajdywać nowe trendy i wzorce ataków, które pojawiają się w jej lokalnych produktach dla firm i osób prywatnych, a także usługach online. W związku z tym usługa Security Center może szybko zaktualizować swoje algorytmy wykrywania, w miarę jak atakujący wprowadzają nowe i coraz bardziej zaawansowane metody. Takie podejście pomaga sprostać wymaganiom szybko zmieniającego się środowiska zagrożenia. 

Wykrywanie zagrożeń za pomocą usługi Security Center polega na automatycznym zbieraniu informacji o zabezpieczeniach uzyskanych z zasobów platformy Azure, sieci i powiązanych rozwiązań partnerskich. Analizuje ona te informacje, często zestawiając informacje z wielu źródeł, aby zidentyfikować zagrożenia. Alerty zabezpieczeń wraz z zaleceniami dotyczącymi usuwania zagrożeń są traktowane przez usługę Security Center priorytetowo.

![Prezentacja i zbieranie danych przez usługę Security Center](./media/security-center-detection-capabilities/security-center-detection-capabilities-fig1.png)

Usługa Security Center wykorzystuje zaawansowane narzędzia analizy zabezpieczeń, które wykraczają daleko poza metody bazujące na sygnaturze. Przełomowe rozwiązania dotyczące danych big data i technologii [uczenia maszynowego](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) są używane do oceny zdarzeń zachodzących w całej sieci szkieletowej chmury. Wykrywane są zagrożenia, które byłyby niemożliwe do wykrycia przy użyciu ręcznych metod, i przewidywany jest kierunek ewolucji ataków. Do narzędzi analizy zabezpieczeń należą: 

* **Zintegrowana analiza zagrożeń**: wyszukuje znane złośliwe podmioty, wykorzystując do tego analizę globalnych zagrożeń z produktów i usług firmy Microsoft, jednostki Microsoft Digital Crimes Unit (DCU), centrum Microsoft Security Response Center (MSRC) i zewnętrznych kanałów.
* **Analiza behawioralna**: stosuje znane wzorce w celu wykrycia złośliwego zachowania. 
* **Wykrywanie anomalii**: korzysta z profilowania statystycznego w celu skompilowania historycznych linii bazowych. Narzędzie to alarmuje o odchyleniach od ustalonych linii bazowych zgodnych z wektorem potencjalnego ataku.

### <a name="threat-intelligence"></a>Analiza zagrożeń
Firma Microsoft dysponuje ogromną ilością danych do globalnej analizy zagrożeń. Telemetria pochodzi z wielu źródeł, takich jak usługi Azure, Office 365, Microsoft CRM online, Microsoft Dynamics AX, outlook.com i MSN.com, jednostka Microsoft Digital Crimes Unit (DCU) oraz centrum Microsoft Security Response Center (MSRC). Pracownicy naukowi otrzymują również informacje dotyczące analizy zagrożeń, które są wymieniane między największymi dostawcami usług w chmurze oraz subskrypcje źródeł analizy zagrożeń od innych firm. Usługa Azure Security Center może użyć tych informacji, aby ostrzec użytkownika przed zagrożeniami ze strony znanych złośliwych podmiotów. Oto niektóre przykłady:

* **Komunikacja wychodząca pod złośliwy adres IP**: ruch wychodzący do znanego botnetu lub darknetu prawdopodobnie wskazuje, że bezpieczeństwo zasobu użytkownika zostało naruszone, a osoba atakująca próbuje wykonać polecenia na systemie lub wyprowadzić dane. Usługa Azure Security Center porównuje ruch sieciowy z bazą danych globalnych zagrożeń firmy Microsoft i ostrzega w razie wykrycia komunikacji ze złośliwym adresem IP.

## <a name="behavioral-analytics"></a>Analiza behawioralna
Analiza behawioralna to metoda, która polega na analizie danych i porównywaniu ich z kolekcją znanych wzorców. Wzorce te nie są jednak prostymi sygnaturami. Określa się je za pośrednictwem złożonych algorytmów uczenia maszynowego, które są stosowane w przypadku wielkich zestawów danych. Są one również określane przez specjalistów od analizy, którzy dokonują dokładnej analizy złośliwych zachowań. Usługa Azure Security Center może użyć analizy behawioralnej w celu identyfikacji zasobów, których bezpieczeństwo zostało naruszone, na podstawie analizy dzienników maszyny wirtualnej, dzienników urządzenia sieci wirtualnej, dzienników sieci szkieletowej, zrzutów awaryjnych i innych źródeł. 

Ponadto istnieje korelacja z innymi sygnałami, które wykrywają dowody potwierdzające istnienie szeroko zakrojonej kampanii ataku. Ta korelacja pomaga w identyfikacji zdarzeń, które są zgodne ze sprawdzonymi wskaźnikami naruszenia bezpieczeństwa. Oto niektóre przykłady:

* **Wykonanie podejrzanego procesu**: osoby atakujące stosują kilka metod, które pozwalają na niezauważalne uruchomienie złośliwego oprogramowania. Na przykład osoba atakująca może nadać złośliwemu oprogramowaniu takie same nazwy, jakie mają pliki w legalnym systemie, ale umieścić je w innej lokalizacji, użyć nazwy bardzo podobnej do nazwy niezłośliwego pliku lub zamaskować prawdziwe rozszerzenie tego pliku. Usługa Security Center modeluje zachowania procesów oraz monitoruje wykonanie procesu, aby wykryć elementy odstające, takie jak w przykładzie.  
* **Ukryte złośliwe oprogramowanie i próby eksploatacji**: zaawansowane złośliwe oprogramowanie jest w stanie umknąć przed działaniem tradycyjnych produktów, które mają przed nim chronić, dzięki temu, że szyfruje składniki oprogramowania przechowywane na dysku lub nigdy nie zapisuje się na dysku.  Złośliwe oprogramowanie może zostać jednak wykryte za pomocą analizy pamięci, ponieważ aby mogło działać, musi zostawić ślady w pamięci maszyny. Jeśli wystąpi awaria oprogramowania, zrzut awaryjny przechwytuje część pamięci w chwili pojawienia się awarii.  Analizując pamięć w zrzucie awaryjnym, usługa Azure Security Center może wykryć metody, jakie zostały użyte w celu wykorzystania luk obecnych w oprogramowaniu, uzyskać dostęp do poufnych danych oraz dyskretnie pozostać na zagrożonym komputerze bez wywierania wpływu na jego wydajność.
* **Penetracja sieci i wewnętrzny rekonesans**: aby pozostać w zagrożonej sieci oraz zlokalizować i zebrać cenne dane, atakujący często przemieszczają się z zagrożonego komputera do innych maszyn w tej samej sieci. Usługa Security Center monitoruje aktywność procesów i logowania w celu odnalezienia ewentualnych prób zdobycia przez osobę atakującą nowych przyczółków w sieci. Działania te mogą dotyczyć wykonania polecenia zdalnego w celu sondowania sieci i wyliczania kont.
* **Złośliwe skrypty programu PowerShell**: program PowerShell jest używany przez osoby atakujące, aby wykonać złośliwy kod na docelowych maszynach wirtualnych — co może być przez nie wykorzystane do różnych celów. Usługa Security Center sprawdza działanie programu PowerShell w poszukiwaniu dowodów na podejrzaną aktywność. 
* **Ataki wychodzące**: dla osób atakujących częstym celem są zasoby w chmurze, ponieważ mogą one być użyte do przeprowadzenia dodatkowych ataków. Maszyny wirtualne, których bezpieczeństwo zostało naruszone, mogą służyć do przeprowadzania ataków siłowych na inne maszyny wirtualne, wysyłania spamu lub skanowania otwartych portów i innych urządzeń w Internecie. Dzięki zastosowaniu uczenia maszynowego do ruchu sieciowego usługa Security Center może wykryć, kiedy wychodząca komunikacja sieciowa przekracza normy. W przypadku spamu usługa Security Center zestawia nietypowy ruch wiadomości e-mail z danymi analizy usługi Office 365 w celu określenia, czy poczta jest szkodliwa, czy może jest wynikiem uzasadnionej kampanii e-mail.  

### <a name="anomaly-detection"></a>Wykrywanie anomalii
Usługa Azure Security Center używa również wykrywania anomalii do identyfikowania zagrożeń. W przeciwieństwie do analizy behawioralnej (która zależy od znanych wzorców wyprowadzonych z dużych zestawów danych), wykrywanie anomalii jest bardziej „spersonalizowane” i koncentruje się na liniach bazowych, które są specyficzne dla przeprowadzonych wdrożeń. Uczenie maszynowe jest stosowane do określania normalnego działania wdrożeń, a następnie generowania reguł definiujących odstające warunki, które mogą reprezentować zdarzenie związane z zabezpieczeniami. Oto przykład:

* **Przychodzące ataki siłowe RDP/SSH**: wdrożenia mogą mieć do czynienia z maszynami wirtualnymi o dużej ilości logowań każdego dnia lub maszynami wirtualnymi o bardzo nielicznych logowaniach lub żadnych. Usługa Azure Security Center może ustalić linię bazową aktywności logowania dla tych maszyn wirtualnych i używać uczenia maszynowego w celu zdefiniowania, co dzieje się poza normalną aktywnością logowania. Jeśli liczba logowań, godzina logowania, lokalizacja, z której wysłano żądanie logowania, lub inna związana z logowaniem właściwość w znaczący sposób odbiega od linii bazowej, może zostać wygenerowany alert. To uczenie maszynowe określa co jest istotne.

## <a name="continuous-threat-intelligence-monitoring"></a>Ciągłe monitorowanie analizy zagrożeń
Usługa Azure Security Center obsługuje zespoły zajmujące się zabezpieczeniami i analizą danych, które stale monitorują zmiany w pojawiających się zagrożeniach. Obejmuje to następujące inicjatywy:

* **Monitorowanie analizy zagrożeń**: analiza zagrożeń obejmuje mechanizmy, wskaźniki, konsekwencje i wiarygodne porady dotyczące istniejących lub pojawiających się zagrożeń. Te informacje są udostępniane w branży zabezpieczeń, a firma Microsoft stale monitoruje zagrożenia płynące z wewnętrznych i zewnętrznych źródeł.
* **Udostępnianie sygnału**: uwagi zespołów ds. zabezpieczeń formułowane na podstawie informacji zebranych z szerokiej gamy produktów firmy Microsoft, takich jak usługi w chmurze i usługi lokalne, serwery i urządzenia klienckie w punkcie końcowym, są udostępniane i analizowane. 
* **Specjaliści ds. zabezpieczeń firmy Microsoft**: ciągła współpraca zespołów firmy Microsoft w zakresie wyspecjalizowanych zabezpieczeń, takich jak analiza śledcza i wykrywanie ataków w sieci Web.
* **Dostrajanie wykrywania zagrożeń**: algorytmy są uruchamiane na rzeczywistych zestawach danych klienta, a pracownicy naukowo-badawczy z zakresu zabezpieczeń pracują z klientami w celu weryfikacji otrzymanych wyników. Wyniki prawdziwie i fałszywie dodatnie są używane w celu udoskonalania algorytmów uczenia maszynowego.

Wszystkie te połączone wysiłki skutkują nowymi i ulepszonymi sposobami wykrywania zagrożeń, z których można korzystać od razu — użytkownik nie musi w tym kierunku nic robić.

## <a name="see-also"></a>Zobacz też
W tym dokumencie omówiono, na czym polegają funkcje wykrywania w usłudze Azure Security Center. Aby dowiedzieć się więcej na temat Centrum zabezpieczeń, zobacz następujące artykuły:

* [Przewodnik planowania i obsługi usługi Azure Security Center](security-center-planning-and-operations-guide.md)
* [Reagowanie na alerty zabezpieczeń i zarządzanie nimi w usłudze Azure Security Center](security-center-managing-and-responding-alerts.md)
* [Alerty zabezpieczeń według typu w usłudze Azure Security Center](security-center-alerts-type.md)
* [Monitorowanie kondycji zabezpieczeń w usłudze Azure Security Center](security-center-monitoring.md) — informacje na temat monitorowania kondycji zasobów platformy Azure.
* [Monitorowanie rozwiązań partnerskich w usłudze Azure Security Center](security-center-partner-solutions.md) — informacje na temat monitorowania stanu kondycji rozwiązań partnerskich.
* [Azure Security Center — często zadawane pytania](security-center-faq.md) — odpowiedzi na często zadawane pytania dotyczące korzystania z usługi.
* [Blog Azure Security](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń i zgodności platformy Azure.

