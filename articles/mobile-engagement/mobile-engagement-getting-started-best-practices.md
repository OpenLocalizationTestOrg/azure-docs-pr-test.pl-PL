---
title: "aaaAzure Mobile Engagement Getting Started Guide z najlepszymi rozwiązaniami"
description: "Przewodnik wprowadzający do usługi Azure Mobile Engagement i najlepsze rozwiązania dotyczące dołączania"
services: mobile-engagement
documentationcenter: mobile
author: wesmc7777
manager: erikre
editor: 
ms.assetid: dfce1183-6398-466e-aa7e-ed702fb52818
ms.service: mobile-engagement
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/04/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: d3f81c34fe74f741a60ca511caa55c312af73b1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---getting-started-guide-with-best-practices"></a>Wprowadzenie do usługi Azure Mobile Engagement — przewodnik z najlepszymi rozwiązaniami
## <a name="overview"></a>Omówienie
**ekrany Hello jest zatłoczone:** w 2013 r., badanie znaleźć hello średni urządzenie przenośne ma 27 zainstalowane aplikacje. Na ich używanie użytkownicy zazwyczaj poświęcają 30 godzin w miesiącu. Większość tego czasu zajmuje korzystanie z sieci społecznościowych i gier (około 20 godzin). Przez 2014 r. hello Android rynku mają około 1,5 miliona aplikacji dla użytkowników toochoose z. sklepu Apple Hello zawiera mniej więcej 1,2 miliona aplikacji. Aplikacje mobilne wciąż zyskują na popularności, a ich deweloperzy konkurują ze sobą na tym rosnącym rynku. 

Hello przeciętny użytkownik urządzeń przenośnych często instaluje i odinstalowuje aplikacje z efektem zmieniających się zainteresowań i doświadczeń dotyczących używania w aplikacji. W kolejności toodetermine hello Powodzenie aplikacji staje się on niezbędne tooknow więcej niż tylko liczbę użytkowników zainstalować aplikację. Jest ważne tooknow stopień przydatności aplikacji oraz jeśli zmienia się tym trendów użycia. istotne stają się Hello następujące pytania:

* Użytkownicy zaczynają toofind aplikację jako mniej interesującą lub przestarzałą? 
* Ile osób całkowicie przestało używać aplikacji? 
* Czy liczba zakupów w aplikacji rośnie czy maleje?
* Użytkownicy nie toocomplete przepływów pracy z powodu problemów dotyczących aplikacji hello lub braku zainteresowania? 
* Czy możliwe jest utrzymanie aplikacji i przydatności przesyłając podstawowego użytkownika świeże tooyour zawartości? 
* Ta nowa zawartość będzie hello tego samego dla wszystkich użytkowników lub skupiają się na segmentów użytkowników na podstawie zachowania w aplikacji? 

Toothese podobne tooquestions odpowiedzi może pomóc rozszerzyć hello życia i przychody z aplikacji. Ułatwią również określenie i utrzymanie bazy użytkowników. 

Aplikacje zazwyczaj toohave dotyczących nośnika niektóre hello wysoki poziom przechowywania wśród użytkowników. Powodem tego jest stale dostarczają one nową toousers zawartości. Wczesne wdrożenie użytecznych powiadomień wypychanych skierowane tooa segmentu użytkowników zwykle toohave znacząco wpływa na poziom przechowywania aplikacji. 

program Azure Mobile Engagement Hello jest zaprojektowana toohelp rozszerzeniu hello życia i poziom przechowywania aplikacji, zapewniając toogather — metoda i analizować szczegółowe informacje dotyczące użycia hello aplikacji. Ułatwi to sklasyfikowanie bazy użytkowników zgodnie z toobehavior, a następnie utwórz ukierunkowanych kampanii obejmujących wysyłanie powiadomień wypychanych i komunikatów w aplikacji tooidentified segmentów użytkowników. Kluczowe wskaźniki wydajności (KPI) pozwalają mierzyć poziom aktywności użytkowników w świetle różnych aspektów korzystania z aplikacji. Usługa Azure Mobile Engagement udostępnia metody hello należy toodetermine kluczowych wskaźników wydajności. Pomaga zwiększyć hello zwrotu z inwestycji (ROI), zapewniając hello infrastruktury należy tooincrease engagement z aplikacji mobilnej. 

W kolejności tooget hello maksymalne wykorzystanie możliwości usługi Azure Mobile Engagement należy toostart z przemyślany plan zaangażowania. Pomoże zidentyfikować hello szczegółowe dane należy toosegment stanie toobe użytkownika podstawowego. Można to zrobić na podstawie zachowania użytkowników oraz ich doświadczeń dotyczących używania aplikacji. W sieci pomyślnie toobe plan jest najlepszym tooclearly praktyki zdefiniuj hello kluczowego wskaźnika wydajności, które będą mierzyć cele aplikacji hello. Z wskaźników, można łatwo osadzić hello niezbędne logiki aplikacji toocollect poprawnie szczegółowych danych, która będzie używać tooanalyze i oceny kluczowych wskaźników wydajności. Ten temat dotyczy najważniejsze wskazówki do definiowania hello kluczowych wskaźników wydajności, które będą używane w planie zaangażowania. 

## <a name="step-1-define-your-kpis-toofit-hello-bet-model"></a>Krok 1: Definiowanie modelu BET hello toofit wskaźników KPI
Poprawne określenie wskaźników KPI może być toocomplete trudne. Aplikacje przeznaczone dla różnych branż mają własne charakterystyki i cele. Ta różnorodność może tooconfuse Twojego rozwiązania. toohelp tego uniknąć, cele i wskaźniki KPI, które powinny być klasyfikowane na trzy główne kategorie: **firm**, **Engagement**, i **techniczne**. Jest to określane mianem hello **modelu BET**.

Dobry plan zwykle obejmuje cele oraz wskaźniki KPI hello, mierzące sukcesów hello w każdej z następujących kategoriach modelu BET hello hello.

#### <a name="business-kpis"></a>Wskaźniki KPI w kategorii Biznes
Biznesowe wskaźniki KPI dotyczące powinna być hello najprostszym toobuild części. Prawdopodobnie zostały już zdefiniowane w takiej czy innej formie na etapie planowania aplikacji mobilnej. Zwykle służą one do mierzenia zwrotu z inwestycji oraz przychodów generowanych przez aplikację. Witaj Poniższa lista zawiera przykładowe biznesowe wskaźniki KPI, które mogą być pomocne podczas określania wskaźników wydajności:

* Biznesowe wskaźniki KPI dotyczące multimediów
  * Liczba klikniętych reklam
  * Liczba odwiedzin strony przez użytkownika
  * Liczba bieżących subskrypcji
* Biznesowe wskaźniki KPI dotyczące gier
  * Liczba zakupów w aplikacji
  * Średni przychód na użytkownika
  * Czas trwania sesji
  * Liczba dni korzystania z gry i osiągnięty poziom
* Biznesowe wskaźniki KPI dotyczące handlu elektronicznego
  * Liczba dni używania aplikacji
  * Średni przychód na użytkownika
  * Średnia kwota w koszyku podczas finalizacji zakupu
  * Kategoria produktów najczęściej wyświetlanych i kupowanych
* Biznesowe wskaźniki KPI dotyczące bankowości i ubezpieczenia
  * Liczba kont
  * Aktywowane funkcje
  * Odwiedzone strony z ofertami
  * Kliknięte lub aktywowane alerty       

#### <a name="engagement-kpis"></a>Wskaźniki KPI w kategorii Zaangażowanie
Wskaźnik KPI zaangażowania jest wydajności wskaźnika toomeasure hello zaangażowania użytkowników. Trendy w tym obszarze określania hello poziom przechowywania aplikacji. Oto kilka przykładowych wskaźników KPI należących do tej kategorii:

* Liczba aktywnych użytkowników w hello ostatnich 7 dni
* Liczba nieaktywnych użytkowników w hello ostatnich 7 dni
* Liczba użytkowników, którzy nie używali aplikacji hello w ciągu 30 dni  

Pewne czynniki zewnętrzne mogą w oczywisty sposób wpływać na te wskaźniki. Na przykład można rozważyć toobe urządzenia przenośnego z użytkownikiem przez cały czas. może, ale nie musi być prawdziwe. Użycie aplikacji gry może być zwykle toohave świąteczne po graczy może odtworzyć więcej podczas pracy lub szkoły.   

Dobrze zdefiniowanych kluczowych wskaźników wydajności w tej kategorii powinny pomóc w miar hello relacji między aplikacji i klientów.

#### <a name="technical-kpis"></a>Wskaźniki KPI w kategorii Kwestie techniczne
Wskaźniki wydajności w tej kategorii pomagają ustalić, czy aplikacja działa prawidłowo, zawiesza się lub ulega awariom. Wskaźniki te można mierzyć kondycję aplikacji hello i znajdować problemy, które mogą uniemożliwiać użytkownikom korzystanie z aplikacji hello. Informacje zbierane na potrzeby tej kategorii mogą również zawierać informacje o wydajności, które byłyby odpowiednie toomarketing zespołów. Witaj danych mogą być również przydatne podczas rozwiązywania problemów przez IT i toohelp zespoły pomocy technicznej identyfikowanie niezgłoszonych błędów. 

Oto przykładowe wskaźniki KPI należące do kategorii Kwestie techniczne:

* Informacje dotyczące obsłużonych i nieobsłużonych wyjątków oraz liczba takich wyjątków 
* Sygnatura czasowa ostatniej awarii
* Ostatnio kliknięty przycisk lub ostatnio odwiedzona strona
* Użycie pamięci aplikacji hello
* Szybkość klatek aplikacji
* Wersja systemu operacyjnego, który aplikacja hello jest uruchomiona na
* Wersja aplikacji

Zdefiniowanie tych wskaźników KPI toohelp mierzyć wydajność aplikacji i znajdować potencjalne błędy. Wskaźników powinno pozwolić na skrócenie czasu hello należy toodeliver poprawkę dla klientów. Wskaźników z tej kategorii można również użyć w celu określenia segmentu użytkowników, którzy napotkali konkretny problem. Można użyć, że użytkownik segmentacji toocreate kampanii toodeliver powiadomień o dostępnych poprawkach i potencjalne toohelp promocji zadowolenia klientów. 

#### <a name="playbook-exercise-1-create-your-kpi-dashboard"></a>Ćwiczenie 1. Tworzenie pulpitu nawigacyjnego wskaźników KPI
Rola wskaźników KPI używanych podczas definiowania strategii marketingowej polega na przedstawieniu perspektywy poszczególnych głównych celów aplikacji. Powinny one być jasno określone punkty danych umożliwiających możesz toocollect najważniejsze informacje toomonitor Twojej aplikacji i hello zachowanie hello przez użytkownika końcowego.

Tworzenie pulpitu nawigacyjnego wskaźników KPI, zawierającą hello poniżej informacje

1. Co to są hello kluczowych wskaźników wydajności dla aplikacji hello?
2. Jakie punkty danych będą używać toorepresent poszczególnych wskaźników?
3. Gdzie znajdują się dane dla aplikacji (np. na ekranie, w ustawieniach lub w systemie)?
4. Czy można odtworzyć sekwencję angażowania dla poszczególnych wskaźników KPI?

Można użyć hello **KPI konstruktora** arkusza w naszym [Podręcznikowym szablonie dotyczącym multimediów] [ Media Playbook link] przykłady i wskazówki.

## <a name="step-2-your-engagement-program"></a>Krok 2. Program zaangażowania
Jednym z kluczowych składników aplikacji powinien być dobry marketing na urządzeniach przenośnych. Absolutnie krytycznym wymogiem jest doskonały program powitalny, uruchamiany przez użytkownika podczas hello pierwszych dni używania aplikacji. Jest to prawdopodobnie toohave bardzo pozytywny wpływ na zaangażowanie użytkownika i poziom przechowywania aplikacji. Badania wykazały, tym większość hello stop użytkowników przy użyciu aplikacji hello po kilku dniach od instalacji. Mają toostrive toomeet lub wcześniej przekracza odsetek pobudzenie oczekiwania klienta, gdy hello użytkownik nadal ma fokus w aplikacji. Upewnij się, że istnieje wartość klucza hello i korzyści wynikające z aplikacji tooyour klientów. 

![](./media/mobile-engagement-getting-started-best-practices/unsegmented-push-notifications.png)

Powiadomienia wypychane są hello najlepsze rozwiązanie tooearly korzystają z użytkownikami i urządzeniami przenośnymi. Należy jednak zachować dużą ostrożność podczas segmentowania użytkowników pod kątem powiadomień wypychanych. Jeśli użytkownik zacznie postrzegać powiadomienia jako nieinteresujące lub uzna je za spam, W kilku kliknięć, użytkownik może usunąć aplikacji nigdy nie tooreturn. Witaj użytkownicy powinni otrzymywać zamiast ogólnych komunikatów spersonalizowanych wartości w aplikacji.

Gdy użytkownicy są aktywnie zaangażowane, następnie program zaangażowania może pomóc w innych aspektach aplikacji hello.

Na przykład można skonfigurowanie kampanii żąda toorate Twojego aktywni użytkownicy aplikacji. Ponieważ ten segment użytkownika jest najbardziej aktywne hello oraz hello najwięcej doświadczenia związanego z aplikacji, można oczekiwać ich toogive hello najdokładniejszych klasyfikacji. Po utworzeniu wysoka Klasyfikacja może pomóc zwiększyć się hello organicznym pobierania aplikacji oraz ograniczyć koszty pozyskiwania klienta.

#### <a name="engagement-sequence"></a>Sekwencja angażowania
Globalny program zaangażowania obejmuje różne sekwencje, Każda z nich ma tooreach kilku celów.

###### <a name="life-push-sequence"></a>Sekwencja powiadomień wypychanych dotyczących cyklu życia
cele Hello sekwencja powiadomień wypychanych życia są różne w zależności od hello cyklem życia engagement hello użytkownika przy użyciu aplikacji hello. Użytkownicy mogą być nieaktywni lub bardzo aktywni albo mogą dopiero zaczynać poznawać aplikację. Na różnych etapach cyklu interakcji użytkownicy mogą korzystać z nową zawartość w postaci porad lub linków prowadzących toodocumentation hello. 

Na przykład nowy użytkownik może muszą pomoc, pobierania aplikacji obiektowe tooan lub korzystać z nowego użytkownika motywacji podobne toohello po pierwszym uruchomieniu aplikacji hello hello...

*"Cieszymy się, że toohave Ci przy dołączeniu! Należy pamiętać, toologin tooget Twojego 1 miesiąc za darmo! "*

###### <a name="behavioral-push-sequence"></a>Sekwencja powiadomień wypychanych dotyczących zachowania użytkowników
sekwencji Hello ma użycia tooincrease na podstawie zebranych aplikacji hello zachowania użytkownika.  

Na przykład bardzo aktywny użytkownik fantastycznej gry w piłkę nożną może korzystać z zainteresowany hello powiadomienia wypychane...

*„Jacku, jesteś wielkim fanem futbolu! Zaloguj się w sekcji Ligowej tooour i wygraj bezpłatny dostęp toohello SuperBowl"!*

###### <a name="alerting-push-sequence"></a>Sekwencja powiadomień wypychanych dotyczących alertów
Użytkownikom spodoba się otrzymywanie komunikatów związanych z ich zainteresowaniami. Sekwencja powiadomień wypychanych dotyczących alertów umożliwia zwiększenie zaangażowania przez wysyłanie komunikatów dostosowanych do ściśle określonych zainteresowań użytkowników. Mogą być określone jawnie, gdy użytkownik wybierze własnych zainteresowań w aplikacji hello. Można również określić, niejawnie na podstawie danych zebranych podczas interakcji z aplikacją hello.

Na przykład użytkownik hello aplikacji handlu elektronicznego może regularnie kupować konkretną markę kawy, które się przechwycić za pomocą biznesowego wskaźnika KPI. Witaj poniższy alert może zwiększyć zainteresowanie tego użytkownika z aplikacją hello.

*"Cześć Tomasz, jednej z Twoich ulubionych marek kawy będą realizowane w sprzedaży 25% hello pierwszym tygodniu września 2015. Dziękujemy za klientów i chce się toomake Ci cynk".*

###### <a name="rentention-push-sequence"></a>Sekwencja powiadomień wypychanych dotyczących przechowywania
Ten sekwencji cele tooretain użytkowników przy użyciu toohelp kampanii powiadomień wypychanych powtarzających się stacji regularny nawyk interakcji z aplikacją hello. Może to pomóc w zwiększeniu poziomu przechowywania aplikacji, jeśli hello użytkownicy będą zadowoleni hello interakcji. 

Na przykład hello użytkownika aplikacji sportowych może odbierać powiadomienia wypychane co tydzień na podstawie na powitania ulubionych klubów hello:

*"Dla toowin szansy 200 punktów, przejdź do głosowania czy hello Nowy Jork wydarzenia dotyczące Legii będzie win mecz ten tydzień przed Jays Blue naszej!"*

#### <a name="hello-3w-approach"></a>podejście 3 Hello
Opanowanie hello różnych sekwencji powiadomień wypychanych ułatwia angażowanie użytkowników końcowych. Jednak nadal potrzebujesz toouse hello 3W podejście do personalizacji powiadomienia. Witaj podejście 3W powinna uwzględniać kto, co i kiedy do każdego powiadomienia. Jeśli uda się uzyskać jasne odpowiedzi na te pytania, powiadomienia będą odpowiednio ukierunkowane na wzbudzenie zaangażowania klientów.

![](./media/mobile-engagement-getting-started-best-practices/who-what-when.png)

###### <a name="who-hello-user-segment-that-will-receive-messages"></a>Kto: Witaj segment użytkowników, który będą otrzymywać wiadomości
Wypychanie powiadomień tooyour użytkowników należy rozważyć użycie kanału komunikacyjnego bardzo poufne. Upewnij się, że powiadomienia hello się, że celem segmentu użytkowników tooa toosend są również zakresie toohello zainteresowań danego segmentu użytkowników. Niewłaściwie nakierowane powiadomienie jest bardzo prawdopodobne toohave negatywne wrażenie na koncie użytkownika. Mogą oni uznać je spam, co doprowadzi aplikacji tooyour odinstalowywane. 

Definiując segmenty użytkowników, którzy będą otrzymywać powiadomienia, należy zastosować kombinację specyficznych kryteriów technicznych i behawioralnych. Prosty przykład definicji segmentu użytkowników może być podobne toohello następującej instrukcji:

"Wszyscy użytkownicy, którzy uruchomili hello aplikacji mobilnej dla powitania po raz pierwszy 3 dni temu i odwiedzających stronę logowania hello dwukrotnie przerywając faktycznie nazwy logowania".

Takie wyrażenie pomoże zidentyfikować dane hello będzie potrzebny toosupport toocollect danego scenariusza.

###### <a name="what-hello-message-that-you-will-send"></a>Co: wiadomość hello, który będzie wysyłany
**Ton komunikatu**

W powiadomieniach promujących zaangażowanie należy używać tonu odpowiedniego dla danego segmentu użytkowników. Ostatecznie jest dobrze tooconnect z użytkowników końcowych i wspierania zainteresowania użytkownika w aplikacji. 

**Przekierowania**

Powiadomienie wypychane może służyć do więcej niż otwarcia aplikacji hello. Jeśli hello powiadomienie udostępnia kontekst, na przykład materiały informacyjne lub dotyczące promocji produktów, link bezpośredni maja powiadomienia bezpośrednio toohello zawartości aplikacji hello, kliknij prawym przyciskiem myszy. toosupport, musisz utworzyć adres URL aplikacji hello toolet systemu zarządzania hello przekierowania. Należy koniecznie pamiętać o tym ważnym etapie podczas pracy z sekwencjach angażowania.

Przekierowaniami można zarządzać również w przypadku korzystania z innych systemów. Na przykład adres URL akcji jest możliwe tooredirect użytkownicy końcowi toomany innych systemów w tym następujących hello:

* Witryna sieci Web
* Skrzynka pocztowa ze skonfigurowaną pocztą e-mail
* System SMS Box
* Usługa wybierania numeru
* Bezpośrednio toohello sklepu z aplikacjami dla aplikacji hello klasyfikacji. 

To zapewnia wiele możliwości użytkowników końcowych tooengage i konfigurowania automatycznych reguł tooimprove parametrów.

**Format/zawartość**

Różne typy i formaty powiadomień wypychanych:

1. **Anonse** : włącza toosend reklamy wiadomości toousers o różnych porach (poza aplikacją w aplikacji albo w dowolnym momencie).
2. **Ankiety** : włączone toogather informacji od użytkowników końcowych za pośrednictwem pytań. Uzyskane odpowiedzi będą dostępne podczas tworzenia kryteriów tootarget użytkowników końcowych.
3. **Wypychania danych** : umożliwia toosend pliku binarnego lub base64 danych pliku tooupdate hello aplikacji. Witaj informacje zawarte w wypychanych danych są wysyłane tooyour aplikacji toopersonalize hello użytkowników w aplikacji. Aplikacja wymaga danych hello toosupport toobe zaprojektowane w wypychanych danych.
4. **Kafelki (tylko Windows Phone)** : umożliwiała toouse hello usługi powiadomień wypychanych firmy Microsoft (MPNS) toosend natywnych powiadomień wypychanych zawierających dane XML (obsługiwane od wersji 0.9.0 zestawu SDK. Witaj końcowy ładunek dla kafelków nie może przekraczać 32 kilobajtów). wiadomość Hello jest wyświetlana bezpośrednio na kafelku tablicy dewelopera.
5. **Elementy Webview**: są to okna podręczne z zawartością sieci Web. Są one wyświetlane, gdy hello użytkownik końcowy kliknie powiadomienie wypychane hello. Widok sieci web umożliwia toohave poszerzyć interakcję z hello przez użytkownika końcowego.

> [!NOTE]
> Upewnij się, że hello zawartość wysyłania powiadomień wypychanych jest zgodna z hello odpowiednich platform (systemy iOS, Android i Windows) wytyczne dotyczące tworzenia aplikacji i wysyłania powiadomień wypychanych.
> 
> 

###### <a name="when-hello-timing-of-your-campaign"></a>Kiedy: Witaj czas wdrożenia kampanii
Gdy jest najlepszym tooactivate czasu hello kampanii wyzwalania powiadomień wypychanych? Czy ma to odbywać się ręczne czy automatycznie? Czy takie powiadomienia mają być cykliczne? Określanie hello odpowiednich momentach lub częstotliwości jest tooengage niezbędne użytkownikom hello uzyskać jak najlepsze rezultaty. Dla każdego scenariusza i sekwencji angażowania, należy określić, kiedy będzie najlepiej toosend czasu hello powiadomień wypychanych. Oto kilka przykładów:

![](./media/mobile-engagement-getting-started-best-practices/campaign-timing-examples.png)

W przypadku codziennego wysyłania wielu powiadomień należy koniecznie mieć na uwadze, że użytkownicy mogą postrzegać taką komunikację jako spam. 

Usługa Azure Mobile Engagement udostępnia dwa sposoby temu jako spam uniknąć toohelp. Najpierw użyj tooensure segmentacji poprawnie ziarna czy nie hello docelowych tych samych użytkowników. Ponadto usługa Azure Mobile Engagement udostępnia funkcję „przydział”. Ta funkcja może ograniczyć powiadomienia wysyłane w ramach kampanii. Na przykład ustawienie domyślnego przydziału too5 tygodniu zapewni, że użytkownik będących częścią segmentu użytkowników kampania hello odbiera nie więcej niż 5 powiadomień w tygodniu.

#### <a name="playbook-exercise-2-create-your-engagement-program"></a>Ćwiczenie 2. Tworzenie programu zaangażowania
Należy poświęcić trochę czasu na podsumowanie celów i definiowanie kampanii hello spodziewasz się tooplay przy użyciu specyficznych sekwencji. Upewnij się, że stosujesz hello 3W podejście toohello powiadomienia w ramach kampanii. 

Użyj hello **Program zaangażowania** arkuszu hello [Podręcznikowym szablonie dotyczącym multimediów] [ Media Playbook link] przykłady i wskazówki.

## <a name="step-3-app-integration"></a>Krok 3. Integracja aplikacji
#### <a name="create-a-tag-plan"></a>Tworzenie planu dodawania tagów
toointegrate usługi Azure Mobile Engagement w aplikacji należy toocreate planu dodawania tagów. plan tagu Hello jest podstawą hello hello projektu. Definiuje hello relacje między specyfikacjami marketingowymi, przepływem pracy hello aplikacji hello i hello rzeczywistymi danymi tagów zbierane w toomeasure aplikacji hello kluczowych wskaźników wydajności. Określa, jakie analizy można toosee w portalu hello. Pomaga również wyznaczeniu segmentów użytkowników, a następnie wyślij tooengage powiadomień wypychanych ukierunkowanych użytkowników końcowych. Po zdefiniowaniu planu tagu hello, dodawanie hello toointegrate kodu w aplikacji jest proste przy użyciu hello zestaw SDK usługi Azure Mobile Engagement.

W ramach planu dodawania tagów nie należy oznaczać wszystkich elementów aplikacji. Powinien on obejmować tylko dane tagów, które są częścią strategii marketingowej na urządzeniach przenośnych W przypadku różnych aplikacji te dane prawdopodobnie będą inne. Witaj [Podręcznikowym szablonie dotyczącym multimediów] [ Media Playbook link] dostarczane przez usługi Azure Mobile Engagement ułatwia utworzenie planu dodawania tagów za pomocą danej metody. Użyj hello **Plan dodawania tagów** arkusz jako toobuilding przewodnik oznakowanie planowanie.

Podczas definiowania sekcję tagów w arkuszu hello, należy dokładnie. Jest to bardzo ważne tooavoid pomyłek. Należy szczegółowo określić wszystkie oczekiwane scenariusze, w których będą wysyłane poszczególne tagi, Uwzględnij nazwę hello działania hello, gdzie każdy znacznik jest osadzony. To powinno wszystkie objęte hello **informacyjnej** część hello arkusza. Arkusz planu dodawania tagów Hello powinna być hello główny punkt odniesienia dla testów weryfikacyjnych. 

W hello **toocollect danych** sekcji, zespół deweloperów powinien Znajdź typy hello, wartości par nazw i dodatkowe informacje klucz/wartość wymagane dla poszczególnych tagów, które zostaną osadzone w aplikacji hello.

Zaleca się przegląd plan dodawania tagów hello z punktu widzenia wszystkich zespołów skojarzone z projektem hello. Po wprowadzeniu koniecznych poprawek należy upewnić się, że plan jest całkowicie zrozumiały dla zespołu marketingowego i deweloperskiego.

Witaj **instrukcji pracy** arkusza mogą być używane toohelp przewodnik wszystkich uczestników projektu hello.

#### <a name="data-types"></a>Typy danych
Są to najczęściej spotykane typy danych obsługiwane przez usługę Azure Mobile Engagement.

###### <a name="devices-and-users"></a>Urządzenia i użytkownicy
Usługa Azure Mobile Engagement identyfikuje użytkowników za pomocą unikatowych identyfikatorów generowanych dla poszczególnych urządzeń. Ten identyfikator jest określany hello identyfikator urządzenia (lub deviceid). Jest on generowany w taki sposób, że wszystkie aplikacje uruchomione na tym samego udziału urządzenia hello sam identyfikator urządzenia.

###### <a name="sessions-and-activities"></a>Sesje i działania
Sesja jest jedno wystąpienie aplikacji hello są uruchamiane przez użytkownika. Witaj sesji jest liczony od hello uruchomienia hello użytkownika aplikacji hello do jej zamknięcia.

Działanie to logiczne grupowanie zestaw czynności, które aplikacji hello może wykonywać podczas sesji. Zazwyczaj jest to określony ekran aplikacji hello, ale może być dowolnemu elementowi logiki aplikacji hello hello. Minimalnym wymaganiem jest przypisanie tagów do wszystkich ekranów i działań aplikacji. Dzięki temu będzie można toounderstand hello ścieżki użytkownika.

###### <a name="events"></a>Zdarzenia
Zdarzenia są używane tooreport interakcji użytkowników z aplikacji hello. Mogą to być natychmiastowe akcje, takie jak udostępnianie zawartości lub uruchamianie klipu wideo. Oznaczenie zdarzeń tagami umożliwi zebranie danych opisujących interakcje użytkowników z aplikacji hello. 

###### <a name="jobs"></a>Zadania
Zadania są używane tooreport akcje, które mają wartość typu duration. Przykładowe zadania obejmują:

* Wykonywanie wywołań interfejsu API
* Czas wyświetlania reklam
* Czas trwania zadań w tle 
* Czas trwania procesu zakupu
* Wyświetlanie klipu wideo

###### <a name="errors"></a>Błędy
Błędy są używane tooreport problemów wykrytych przez aplikację hello. na przykład nieprawidłowych działań użytkowników lub nieudanych wywołań interfejsu API.

###### <a name="application-information"></a>Informacje o aplikacji
Informacje o aplikacji (App-Info) są używane dane tootag powiązane środowisko użytkownika tooa z aplikacji. Jest ona generowana przez interakcji z aplikacją hello. 

Dla danego programu app-info klucza usługi Azure Mobile Engagement tylko przechowuje informacje o hello najnowszą wartość (Brak historii). Informacje o aplikacji ujawnia hello stan aplikacji lub użytkowników końcowych. Na przykład hello zalogować się w stanie lub grupy ulubionych produktów użytkownika.

###### <a name="crash-data"></a>Dane dotyczące awarii
Automatycznie gromadzone przez hello zestaw SDK usługi Mobile Engagement zgłoszenia błędów, które nie są obsługiwane przez aplikację hello dane dotyczące awarii. Mogą to być na przykład nieobsłużone wyjątki.

###### <a name="extra-data"></a>Dodatkowe dane
Do zdarzeń, błędów, działań i zadań mogą być dołączane parametry. Jest to informacji dodatkowych, deweloperzy mogą podać jako określonych danych z aplikacji hello. Jest to ważne w przypadku definiowania precyzyjnej segmentacji. 

Na przykład wartość tagu "artykuł" Witaj pozwoli toosegment użytkownicy końcowi, którzy wyświetlili stronę z konkretnym artykułem. Jednak taka informacja może nie być wystarczająca. Lepszym rozwiązaniem byłoby dołączenie w ramach działania dodatkowych informacji, takich jak „kategoria_nowości”, do tagu „artykuł”. Dzięki temu będzie można toodetermine dynamicznie hello Ulubione kategorie użytkownika hello. 

Dodatkowe informacje są zgłaszane w postaci pary klucz/wartość. W przykładzie hello aplikacji multimedialnej hello dodatkowe informacje dla "kategoria_nowości" będzie hello wartość tej kategorii. na przykład „sport”, „gospodarka” lub „polityka”.

#### <a name="tag-and-sdk-integration"></a>Integracja tagów z zestawem SDK
Instrukcje krok po kroku dotyczące integrowania hello Azure Mobile Engagement SDK w aplikacji, wykonaj hello [Engagement SDK Integration](mobile-engagement-windows-store-integrate-engagement.md) dokumentacji w witrynie systemu Azure. Wybierz docelową platformą z łącza hello hello początku tej strony.

Zaleca się utworzenie dwóch projektów aplikacji korzystających z usługi Azure Mobile Engagement. Jeden do tworzenia i testowania, a hello inne do produkcyjnego. Zespół IT może promować testu przemieszczania tooproduction podczas testów akceptacyjnych przez hello użytkowników zakończy się pomyślnie.

#### <a name="user-acceptance-testing-uat"></a>Testy akceptacyjne użytkowników
Testy akceptacyjne użytkowników służą upewnieniu się, że wszystko działa zgodnie z oczekiwaniami. Testy umożliwiają ukończenie przepływów pracy i zebranie wszystkich potrzebnych danych w oparciu o plan dodawania tagów:

* Znakowanie informacji powinny być stosowane zgodnie z pojęciami AZME toodocumented
* Zbierane są wszystkie potrzebne informacje (w tym informacje o aplikacji oraz dane dodatkowe).
* Nomenklatura jest zgodna zgodnie z tooyout Plan tagu
* Nie są wysyłane zduplikowane tagi.

Należy dokładnie przetestować wszystkie typy hello zachowanie powiadomienia, które zostały osadzone w aplikacji

* Anonse, ankiety, dane wypychane z i do aplikacji.
* Widoki tekstowe/sieci Web
* Aktualizacja wskaźnika, kategorie

#### <a name="setup"></a>Konfiguracja
Konfigurowanie usługi Azure Mobile Engagement jest bardzo proste. Cała dokumentacja hello powiązane toohello interfejs użytkownika jest dostępna w witrynie sieci Web hello Azure Mobile Engagement [jak toonavigate hello interfejsu użytkownika](mobile-engagement-user-interface-home.md).

Zaleca się uruchamiania, konfigurując hello odpowiednich ról i przynależności do ról użytkowników hello projektu. Ułatwia to zarządzanie dostępem toohello platformy dla wszystkich użytkowników. Mogą to być następujące role:

* Administratorzy
* Deweloperzy
* Osoby przeglądające 

Następnie

* Zarejestruj tootest Twojego deviceID na swoim urządzeniu.
* Przejdź do ustawień toohello Twojego konta i skonfigurować hello strefy czasowej toohave wykresów i czas dostarczenia powiadomienia dla strefy czasowej.
* Przejdź toohello ustawień aplikacji i zarejestruj hello "App-info" należy w zasięgu ręki tootarget użytkownika końcowego.

Więcej informacji dotyczących sposobu toorun pierwszego push kampanię z użyciem powiadomień, przejrzyj [jak tooget uruchomiony przy użyciu i zarządzanie wypchnięcia tooreach limit użytkowników końcowych tooyour](mobile-engagement-how-tos.md).

## <a name="conclusion"></a>Podsumowanie
Programy zaangażowania mają naturę iteracyjną, dlatego należy ciągle je usprawniać, eksperymentując z różnymi rozwiązaniami. 

Początkowym etapie zdobywania doświadczenia z engagement strategii nie próbuj toobuild globalnej strategii. Zastosowaniu podejścia krok po kroku, zidentyfikowanie kluczowych wskaźników wydajności i w jaki sposób tooleverage je. Strategia zaangażowania jest unikatowa dla każdej aplikacji.

Po zdobyciu pewnego doświadczenia można rozważyć dodanie hello następujące programy zaangażowania tooyour:

* Śledzenie: pozyskiwanie użytkowników zwykle idzie w parze z definiowaniem źródeł gromadzonych danych. Usługi Azure mobile Engagement można połączonych kolekcji toodata źródeł. Pozwala ona toomonitor ich wydajności. Te informacje będą interesujące toomaximize zmaksymalizowanie inwestycji. 
* Testy A/B: to fundamentalna część programu zaangażowania. Każda aplikacja ma własną specyfikę. Testy A/B pozwalają ulepszyć program zaangażowania.
* Geolokalizacja: to duża szansa dla marek. Dzięki funkcji toothis możesz uzyskiwać dostęp w hello w odpowiednim miejscu i czasie. Zaleca się sprawdzenie, czy zebrano wystarczającą ilość danych zachowanie użytkownika końcowego przed rozpoczęciem toouse lokalizacji geograficznej.
* Wypychanie danych: wypychane dane są niewidoczne. Wypychanie danych pozwala na dostosowywanie aplikacji na podstawie zachowania użytkowników końcowych. Na przykład jeśli segmentu użytkowników często sprawdza zaawansowanych technologicznie produktach, właściciel aplikacji hello wysłać wypychania danych w celu spersonalizowania strony głównej o zaawansowanych technologicznie zawartości.

## <a name="next-steps"></a>Następne kroki
* [Tworzenie konta usługi Azure Mobile Engagement](mobile-engagement-create.md)
* Odwiedź stronę [Definiowanie strategii Mobile Engagement](mobile-engagement-define-your-mobile-engagement-strategy.md) toolearn więcej informacji na temat definiowania strategii Mobile Engagement.

<!--Image references-->


<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
