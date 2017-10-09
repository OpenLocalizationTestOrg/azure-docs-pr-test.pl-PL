---
title: pola aaaCustom Log Analytics | Dokumentacja firmy Microsoft
description: "Funkcja pola niestandardowe Hello analizy dzienników umożliwia toocreate pól można wyszukiwać dane OMS dodać właściwości toohello zebranych rekordu.  W tym artykule opisano hello procesu toocreate niestandardowego pola i udostępnia szczegółowy przewodnik zdarzenie próbkowania."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 31572b51-6b57-4945-8208-ecfc3b5304fc
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 1aa0e497d5b1d7898b0da6a5ef40f568e63bc589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="custom-fields-in-log-analytics"></a>Pola niestandardowe w analizy dzienników
Witaj **pola niestandardowe** funkcji analizy dzienników pozwala tooextend istniejących rekordów w repozytorium OMS hello przez dodanie pola wyszukiwania.  Pola niestandardowe zostaną automatycznie wypełnione z danych wyodrębnionych z innych właściwości w hello sam rekord.

![Przegląd pól niestandardowych](media/log-analytics-custom-fields/overview.png)

Na przykład hello przykładowy rekord poniżej zawiera przydatnych danych w opisie zdarzenia hello stosie.  Wyodrębnianie te dane w oddzielnych właściwości udostępnia takie zadania jak sortowania i filtrowania.

![Przycisk wyszukiwania dziennika](media/log-analytics-custom-fields/sample-extract.png)

> [!NOTE]
> Hello Podgląd jesteś ograniczone too100 pola niestandardowe w obszarze roboczym.  Ten limit zostaną rozwinięte, gdy ta funkcja osiągnie ogólnej dostępności.
> 
> 

## <a name="creating-a-custom-field"></a>Tworzenie niestandardowego pola
Podczas tworzenia niestandardowego pola analizy dzienników muszą zrozumieć które toopopulate toouse danych jego wartości.  Używa technologii Microsoft Research o nazwie FlashExtract tooquickly zidentyfikować te dane.  Zamiast konieczności jawnego instrukcje tooprovide, analizy dzienników uzyskuje informacje o danych hello ma tooextract w przykładach podanych.

Hello następujące sekcje zawierają informacje zawiera procedura hello do tworzenia niestandardowego pola.  Na powitania dolnej części tego artykułu jest przewodnik wyodrębniania próbki.

> [!NOTE]
> pole niestandardowe Hello jest wprowadzana jako rekordów pasujących hello określone kryteria są dodawane toohello OMS magazynu danych, więc zostanie wyświetlony tylko na rekordy zebrane po utworzeniu niestandardowego pola hello.  pole niestandardowe Hello nie zostanie dodany toorecords, które są już w magazynie danych hello podczas jego tworzenia.
> 
> 

### <a name="step-1--identify-records-that-will-have-hello-custom-field"></a>Krok 1 — Określ rekordów, które będzie mieć hello niestandardowego pola
pierwszym krokiem Hello jest tooidentify hello rekordów, które otrzymają hello niestandardowego pola.  Rozpoczyna [wyszukiwania standardowe dziennika](log-analytics-log-searches.md) a następnie wybierz tooact rekordu jako hello modelu, który będzie nauki analizy dzienników.  Po określeniu, czy ma tooextract danych do pola niestandardowego, hello **Kreator wyodrębniania pola** jest otwarty, gdzie Zweryfikuj i zoptymalizuj hello kryteriów.

1. Przejdź za**wyszukiwania dziennika** i użyj [wysyłać zapytania o rekordy hello tooretrieve](log-analytics-log-searches.md) będą mieć hello pola niestandardowego.
2. Wybierz rekord dziennika Analytics będzie używała tooact jako model, do wyodrębniania danych toopopulate hello niestandardowego pola.  Należy określić dane hello ma tooextract z tego rekordu, a analizy dzienników użyje tego informacje toodetermine hello logiki toopopulate hello pola niestandardowego dla wszystkich rekordów podobne.
3. Kliknij przycisk hello przycisk toohello po lewej żadnej właściwości tekst hello rekordów i wybierz pozycję **wyodrębniania pól z**.
4. Witaj **zostanie otwarty Kreator wyodrębniania pola**, i wybranego rekordu hello jest wyświetlany w hello **przykład Main** kolumny.  pole niestandardowe Hello są definiowane dla tych rekordów z hello takie same wartości właściwości hello, które są wybrane.  
5. Jeśli zaznaczenie hello jest dokładnie, co chcesz, dodatkowe pola toonarrow hello kryteria wyboru.  W kolejności toochange hello wartości pól kryteriów hello możesz Anuluj i wybierz inny rekord spełniających kryteria hello, który ma.

### <a name="step-2---perform-initial-extract"></a>Krok 2 — wykonywania początkowej wyodrębniania.
Po wyłaniają hello rekordów, które będą miały hello pola niestandardowego, należy zidentyfikować hello danych, które mają tooextract.  Analiza dzienników użyje wzorce podobne tooidentify informacji w rekordach podobne.  W kroku hello później będzie wyniki hello toovalidate może być i podać dodatkowe szczegóły dotyczące analizy dzienników toouse w jego analizy.

1. Wyróżnianie tekstu hello w rekordzie próbki hello, które mają toopopulate hello niestandardowego pola.  Możesz następnie zobaczy tooprovide okno dialogowe nazwę hello pola i tooperform hello początkowej wyodrębniania.  Witaj znaków  **\_CF** zostaną automatycznie dołączone.
2. Kliknij przycisk **wyodrębnić** tooperform analizę zebranych rekordów.  
3. Witaj **Podsumowanie** i **wyniki wyszukiwania** sekcjach są wyświetlane wyniki hello hello wyodrębniania, możesz sprawdzić dokładność.  **Podsumowanie** Wyświetla hello kryteria tooidentify rekordów i że liczba dla każdej hello wartości danych.  **Wyniki wyszukiwania** zawiera szczegółową listę rekordów spełniających kryteria hello.

### <a name="step-3--verify-accuracy-of-hello-extract-and-create-custom-field"></a>Krok 3 — sprawdzić dokładność wyodrębniania hello i utworzyć niestandardowego pola
Po wykonaniu początkowego wyodrębniania hello analizy dzienników wyświetli wyniki na podstawie danych, które już zostały zebrane.  Jeśli dokładne wyglądają wyniki hello można utworzyć niestandardowego pola hello z żadne dodatkowe czynności.  Jeśli nie, następnie można dostosować wyniki hello tak, aby analizy dzienników można zwiększyć swojej logiki.

1. Jeśli wszystkie wartości w początkowej wyodrębniania hello nie są poprawne, kliknij przycisk hello **Edytuj** następnego rekordu niedokładne ikona tooan i wybierz **zmodyfikować tego wyróżnienia** w kolejności toomodify hello zaznaczenia.
2. Witaj wpis jest skopiowany toohello **dodatkowe przykłady** sekcji poniżej hello **przykład Main**.  Można dostosować wyróżnienie hello tutaj toohelp analizy dzienników zrozumieć wybór hello powinien zostały wprowadzone.
3. Kliknij przycisk **wyodrębnić** toouse tego nowego tooevaluate informacji hello wszystkie istniejące rekordy.  wyniki Hello może być modyfikowany rekordów niż hello jeden po modyfikacji oparta na tego nowego analizy.
4. Nadal tooadd poprawek, dopóki wszystkie rekordy w hello wyodrębnić poprawnie zidentyfikować hello danych toopopulate hello nowego pola niestandardowego.
5. Kliknij przycisk **zapisać wyodrębnić** jeśli są zadowalające hello wyników.  pole niestandardowe Hello jest teraz zdefiniowana, ale nie zostanie dodany rekordów tooany jeszcze.
6. Oczekiwanie na nowe rekordy pasujące hello określony toobe kryteria zbieranych, a następnie ponownie uruchom hello dziennik wyszukiwania. Nowe rekordy powinny mieć hello pola niestandardowego.
7. Użyj niestandardowego pola hello, podobnie jak inne właściwości rekordu.  Można używać go tooaggregate i grupy danych i nawet go używać tooproduce nowych danych.

## <a name="viewing-custom-fields"></a>Wyświetlanie pola niestandardowe
Można wyświetlić listę wszystkich pól niestandardowych w grupie zarządzania z hello **ustawienia** kafelka pulpitu nawigacyjnego OMS hello.  Wybierz **danych** , a następnie **pola niestandardowe** listę wszystkich pól niestandardowych w obszarze roboczym.  

![Niestandardowe pola](media/log-analytics-custom-fields/list.png)

## <a name="removing-a-custom-field"></a>Usuwanie pola niestandardowego
Istnieją dwa sposoby tooremove pola niestandardowego.  Hello jest najpierw hello **Usuń** opcji dla każdego pola podczas wyświetlania hello pełną listę, zgodnie z powyższym opisem.  Witaj inną metodą jest tooretrieve rekordu i kliknij przycisk toohello przycisk hello pozostawiać hello pola.  Witaj menu będzie miał hello tooremove opcji dla pola niestandardowego.

## <a name="sample-walkthrough"></a>Przykładowe wskazówki
Witaj poniższej sekcji przedstawiono kompletnym przykładem tworzenia niestandardowego pola.  W tym przykładzie wyodrębnia hello nazwę usługi w zdarzeń systemu Windows, które wskazują zmiana stanu usługi.  Zależy to od zdarzenia utworzone przez Menedżera sterowania usługami w dzienniku systemu hello na komputerach z systemem Windows.  Jeśli chcesz toofollow w tym przykładzie, musi być [zbierania zdarzeń informacji dziennika systemu hello](log-analytics-data-sources-windows-events.md).

Firma Microsoft wprowadź hello następującego zapytania tooreturn wszystkich zdarzeń z Menedżera kontroli usług, który ma identyfikator zdarzenia 7036 czyli hello zdarzenie, które wskazuje uruchomienie lub zatrzymanie usługi.

![Zapytanie](media/log-analytics-custom-fields/query.png)

Następnie wybierz możemy żadnych rekordów z 7036 identyfikator zdarzenia.

![Rekord źródła](media/log-analytics-custom-fields/source-record.png)

Chcemy hello nazwy usługi, która jest wyświetlana w hello **RenderedDescription** właściwości i hello wybierz przycisk Dalej toothis.

![Wyodrębnianie pól](media/log-analytics-custom-fields/extract-fields.png)

Hello **Kreator wyodrębniania pola** jest otwarty i hello **EventLog** i **EventID** w hello wybrano pola **przykład Main** kolumny.  Oznacza to, że tego pola niestandardowe hello są definiowane dla zdarzenia z dziennika systemu hello o identyfikatorze zdarzenia 7036.  Może to być wystarczające, potrzebujemy nie tooselect innych pól.

![Przykład głównego](media/log-analytics-custom-fields/main-example.png)

Możemy wyróżnić hello nazwa usługi hello w hello **RenderedDescription** właściwości i użyj **usługi** nazwa usługi hello tooidentify.  pole niestandardowe Hello zostanie wywołana **Service_CF**.

![Pole tytułu](media/log-analytics-custom-fields/field-title.png)

Widzimy, że nazwa usługi hello jest rozpoznawane poprawnie niektóre rekordy, ale nie do innych użytkowników.   Witaj **wyniki wyszukiwania** Pokaż część nazwy hello hello **Karta wydajności WMI** nie został wybrany.  Witaj **Podsumowanie** pokazuje, które rejestruje cztery z **DPRMA** usługi nieprawidłowo włączone dodatkowe word i dwa rekordy określone **Instalator modułów** zamiast **Instalatora modułów systemu Windows**.  

![Wyniki wyszukiwania](media/log-analytics-custom-fields/search-results-01.png)

Możemy zaczynać hello **Karta wydajności WMI** rekordu.  Firma Microsoft, kliknij ikonę edycji, a następnie **zmodyfikować tego wyróżnienia**.  

![Modyfikowanie wyróżnienia](media/log-analytics-custom-fields/modify-highlight.png)

Firma Microsoft zwiększyć hello wyróżnienie tooinclude hello word **WMI** i uruchom ponownie hello wyodrębniania.  

![Przykład dodatkowe](media/log-analytics-custom-fields/additional-example-01.png)

Zobaczysz, że hello wpisy dla **Karta wydajności WMI** zostały skorygowane, i analizy dzienników również używać tej informacji toocorrect hello rekordy **Instalator modułu Windows**.  Zobaczysz hello **Podsumowanie** sekcji jednak, że **DPMRA** jest nadal nie są określone poprawnie.

![Wyniki wyszukiwania](media/log-analytics-custom-fields/search-results-02.png)

Firma Microsoft przewiń tooa rekord z hello usługę DPMRA i używać tego samego procesu toocorrect wykaz hello.

![Przykład dodatkowe](media/log-analytics-custom-fields/additional-example-02.png)

 Uruchomienie hello wyodrębniania, widać, że wszystkie nasze wyniki teraz są poprawne.

![Wyniki wyszukiwania](media/log-analytics-custom-fields/search-results-03.png)

Zobaczysz, że **Service_CF** zostało utworzone, ale nie została jeszcze dodana tooany rekordów.

![Liczba początkowa](media/log-analytics-custom-fields/initial-count.png)

Po upływie chwilę, więc nowe zdarzenia są zbierane, zobaczysz, że hello **Service_CF** pola teraz dodawana toorecords odpowiadających kryteriów.

![Wyniki końcowe](media/log-analytics-custom-fields/final-results.png)

Teraz można używać niestandardowego pola hello, podobnie jak inne właściwości rekordu.  tooillustrate, możemy utworzyć kwerendę, która grupy przez nowe hello **Service_CF** usługi, które są najbardziej aktywne hello tooinspect pola.

![Grupuj według zapytania](media/log-analytics-custom-fields/query-group.png)

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) toobuild zapytania przy użyciu pól niestandardowych kryteriów.
* Monitor [pliki dziennika niestandardowego](log-analytics-data-sources-custom-logs.md) który przeanalizować, przy użyciu pól niestandardowych.

