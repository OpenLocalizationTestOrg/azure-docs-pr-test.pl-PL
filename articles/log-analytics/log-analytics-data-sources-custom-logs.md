---
title: aaaCollect niestandardowych loguje OMS Log Analytics | Dokumentacja firmy Microsoft
description: "Analiza dzienników można zbierać zdarzenia z plików tekstowych na komputerach z systemami Windows i Linux.  W tym artykule opisano, jak toodefine nowy dziennik niestandardowy i szczegóły rekordów hello tworzą hello OMS repozytorium."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: aca7f6bb-6f53-4fd4-a45c-93f12ead4ae1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/15/2017
ms.author: bwren
ms.openlocfilehash: a75d058c371fecf7c43690a797d4e650c1570317
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="custom-logs-in-log-analytics"></a>Niestandardowe dzienniki w analizy dzienników
źródło danych niestandardowe dzienniki Hello w analizy dzienników umożliwia toocollect zdarzenia z plików tekstowych na komputerach z systemami Windows i Linux. Wiele aplikacji dzienniki informacji tootext zamiast standardowych usług rejestrowania, takich jak dziennika zdarzeń systemu Windows lub Syslog.  Po zebraniu danych, można przeanalizować każdego rekordu w dzienniku hello w polach tooindividual przy użyciu hello [pola niestandardowe](log-analytics-custom-fields.md) funkcji analizy dzienników.

![Zbieranie dzienników niestandardowych](media/log-analytics-data-sources-custom-logs/overview.png)

toobe pliki dziennika Hello zbierane musi odpowiadać hello następujące kryteria.

- Dziennik Hello musi mieć pojedynczy wpis wierszu albo użyj sygnatury czasowej odpowiadającego mu przez jedną z następujących hello formatuje na powitania na początku każdego wpisu.

    HH: MM: RRRR MM-DD<br>M/D/RRRR GG: MM: SS AM/PM <br>MON DD, YYYY HH: mm:

- plik dziennika Hello nie może zezwalać na aktualizacje cykliczne gdzie hello plik jest zastępowany nowe wpisy.
- plik dziennika Hello należy użyć kodowanie ASCII lub UTF-8.  Innych formatach, takich jak UTF-16 nie są obsługiwane.

>[!NOTE]
>Jeśli istnieją zduplikowane wpisy w pliku dziennika hello, analizy dzienników zapisze je.  Jednak hello wyniki wyszukiwania będą niespójne gdzie hello filtru w wynikach więcej zdarzeń niż hello liczbę wyników.  Będzie on potrzebny, sprawdzanie poprawności hello toodetermine dziennika, jeśli aplikacja hello, która tworzy jego przyczyną jest to zachowanie i rozwiązać ten Jeśli to możliwe, przed utworzeniem hello dziennik niestandardowy kolekcji definicji.  
>
  
## <a name="defining-a-custom-log"></a>Definiowanie niestandardowego dziennika
Użyj hello następujące procedury toodefine pliku dziennika niestandardowego.  Przewiń toohello na końcu artykułu przewodnik próby dodania dziennik niestandardowy.

### <a name="step-1-open-hello-custom-log-wizard"></a>Krok 1. Otwórz hello kreatora dziennika niestandardowego
Hello Kreator dziennik niestandardowy jest uruchamiana w portalu OMS hello i pozwala toodefine nowe toocollect dziennik niestandardowy.

1. W portalu OMS hello, przejdź do pozycji zbyt**ustawienia**.
2. Polecenie **danych** , a następnie **niestandardowe dzienniki**.
3. Domyślnie wszystkie zmiany konfiguracji są automatycznie wypychana agentów tooall.  Dla agentów systemów Linux plik konfiguracji jest wysyłany toohello Fluentd modułów zbierających dane.  Jeśli chcesz toomodify ten plik ręcznie na każdym agenta systemu Linux, usuń zaznaczenie pola hello *Zastosuj poniżej maszyny z systemem Linux toomy konfiguracji*.
4. Kliknij przycisk **Dodaj +** hello tooopen kreatora dziennika niestandardowego.

### <a name="step-2-upload-and-parse-a-sample-log"></a>Krok 2. Przekazywanie i przeanalizować przykładowy dziennik
Możesz uruchomić przekazywanie próbkę hello dziennik niestandardowy.  Kreator Hello przeanalizować i wyświetlić hello wpisy w tym pliku toovalidate należy.  Analiza dzienników użyje ogranicznik hello Określ tooidentify każdego rekordu.

**Nowy wiersz** hello domyślnym ogranicznikiem jest i jest używany dla plików dziennika, które mają pojedynczy wpis wierszu.  Jeśli wiersz hello rozpoczyna się od daty i godziny w jednym z formatów dostępne hello, a następnie można określić **sygnatury czasowej** ogranicznik obsługującej wpisów, obejmujące więcej niż jeden wiersz.

Jeśli używane jest ogranicznik sygnatury czasowej, a następnie hello TimeGenerated właściwości każdego rekordu przechowywane w OMS zostanie wypełniona hello daty/godziny określone dla tego wpisu w pliku dziennika hello.  Jeśli jest używany nowy ogranicznik wiersza, TimeGenerated jest wypełniane przy użyciu daty i godziny, aby analizy dzienników pobrane hello wpisu.

> [!NOTE]
> Analiza dzienników traktuje obecnie hello daty/godziny zbierane z dziennika przy użyciu ogranicznik znacznik czasu jako czas UTC.  Wkrótce będzie strefy czasowej hello toouse zmienione na powitania agenta.
>
>

1. Kliknij przycisk **Przeglądaj** i Przeglądaj tooa przykładowy plik.  Należy pamiętać, że może to przycisk może być oznaczony jako **wybierz plik** w niektórych przeglądarkach.
2. Kliknij przycisk **Dalej**.
3. przekazać hello plików i listy hello rekordów, które identyfikuje Hello kreatora dziennika niestandardowego.
4. Zmień hello ogranicznik, który jest używany tooidentify nowy rekord i znaku ogranicznika hello wybierz opcję najlepiej identyfikujący hello rekordy w pliku dziennika.
5. Kliknij przycisk **Dalej**.

### <a name="step-3-add-log-collection-paths"></a>Krok 3. Dodaj ścieżki zbierania dzienników
Należy zdefiniować co najmniej jedną ścieżkę na agencie hello, gdzie można znaleźć hello dziennik niestandardowy.  Można podać albo określoną ścieżkę i nazwę pliku dziennika hello, lub z symbolem wieloznacznym dla nazwy hello można określić ścieżkę.  Obejmuje to obsługę aplikacji, które tworzą nowy plik, każdego dnia lub gdy jeden plik osiągnie określony rozmiar.  Można też podać wiele ścieżek dla jednego pliku dziennika.

Na przykład aplikacja może utworzyć pliku dziennika każdego dnia z datą hello uwzględniony w nazwie hello jak log20100316.txt. Szablon dla takich dziennika może być *dziennika\*.txt* która powinna zostać zastosowana tooany pliku dziennika aplikacji hello po jego nazewnictwa schematu.

Witaj poniższej tabeli przedstawiono przykłady prawidłowych toospecify różnych plikach dziennika.

| Opis | Ścieżka |
|:--- |:--- |
| Wszystkie pliki w *C:\Logs* z rozszerzeniem txt agenta systemu Windows |C:\Logs\\\*txt |
| Wszystkie pliki w *C:\Logs* o nazwie rozpoczynającej się od dziennika i rozszerzeniem txt agenta systemu Windows |C:\Logs\log\*txt |
| Wszystkie pliki w */var/log/audit* z rozszerzeniem txt na agenta systemu Linux |/var/log/audit/*.txt |
| Wszystkie pliki w */var/log/audit* o nazwie rozpoczynającej się od dziennika i rozszerzeniem txt na agenta systemu Linux |/var/log/audit/log\*txt |

1. Wybierz toospecify systemu Windows lub Linux, dodanie format ścieżki.
2. Wpisz ścieżkę hello i kliknij przycisk hello  **+**  przycisku.
3. Powtórz kroki hello żadnych dodatkowych ścieżek.

### <a name="step-4-provide-a-name-and-description-for-hello-log"></a>Krok 4. Podaj nazwę i opis dla dziennika hello
Witaj przez Ciebie nazwą będzie służyć do typu dziennika hello zgodnie z powyższym opisem.  On zawsze kończy się _CL toodistinguish go jako dziennik niestandardowy.

1. Wpisz nazwę dziennika hello.  Witaj  **\_CL** sufiks jest teraz udostępniana automatycznie.
2. Dodaj opcjonalny **opis**.
3. Kliknij przycisk **dalej** toosave hello dziennik niestandardowy definicji.

### <a name="step-5-validate-that-hello-custom-logs-are-being-collected"></a>Krok 5. Zweryfikuj, że dzienników niestandardowych hello są zbierane
Może potrwać godzinę tooan hello początkowe dane z nowego tooappear dziennik niestandardowy w analizy dzienników.  Rozpocznie się zbieranie wpisów z hello dzienniki dostępne w ścieżce hello określona z punktu hello hello zdefiniowane niestandardowe zalogowanie.  Hello wpisów, które zostało przez Ciebie przekazane podczas tworzenia dziennika niestandardowego hello nie zostaną zachowane, ale będzie zbierać już istniejących wpisów w plikach dziennika hello, które klient zlokalizuje.

Po uruchomieniu analizy dzienników zbierane z dziennika niestandardowego hello swoje rekordy będą dostępne z wyszukiwania dziennika.  Użyj nazwy hello nadaną hello dziennik niestandardowy jako hello **typu** w zapytaniu.

> [!NOTE]
> Brakuje hello właściwości RawData hello wyszukiwania, może muszą tooclose i otworzyć ponownie przeglądarkę.
>
>

### <a name="step-6-parse-hello-custom-log-entries"></a>Krok 6. Przeanalizować hello wpisy dziennika niestandardowego
Wpis dziennika całego Hello będą przechowywane w jedną właściwość o nazwie **RawData**.  Prawdopodobnie należy tooseparate hello różne informacje zawarte w każdej pozycji do poszczególnych właściwości przechowywanych w rekordzie hello.  Można to zrobić przy użyciu hello [pola niestandardowe](log-analytics-custom-fields.md) funkcji analizy dzienników.

Szczegółowe informacje na temat analizowania wpis dziennika niestandardowego hello nie znajdują się w tym miejscu.  Zobacz toohello [pola niestandardowe](log-analytics-custom-fields.md) tych informacji w dokumentacji.

## <a name="disabling-a-custom-log"></a>Wyłączanie dziennika niestandardowego
Nie można usunąć definicji dziennik niestandardowy, po jest został utworzony, ale można ją wyłączyć, usuwając wszystkie jego ścieżki w kolekcji.

1. W portalu OMS hello, przejdź do pozycji zbyt**ustawienia**.
2. Polecenie **danych** , a następnie **niestandardowe dzienniki**.
3. Kliknij przycisk **szczegóły** dalej toodisable definicji dziennik niestandardowy toohello.
4. Usuwanie wszystkich ścieżek kolekcji hello hello dziennik niestandardowy definicji.

## <a name="data-collection"></a>Zbieranie danych
Analiza dzienników zbierze nowe wpisy z każdego dziennik niestandardowy co 5 minut.  Hello agent zarejestruje jego miejsce w każdym pliku dziennika, który zbiera z.  Hello agent przejdzie do trybu offline w danym okresie czasu, następnie analizy dzienników będzie gromadzić wpisów z którym ostatnio przerwał, nawet jeśli te wpisy zostały utworzone podczas hello agent jest w trybie offline.

Witaj całą zawartość hello wpis dziennika są zapisywane tooa jedną właściwość o nazwie **RawData**.  Można to przeanalizować na wiele właściwości, które mogą być przeanalizowane i przeszukiwać osobno, definiując [pól niestandardowych](log-analytics-custom-fields.md) po utworzeniu hello dziennik niestandardowy.

## <a name="custom-log-record-properties"></a>Właściwości rekordu dziennika niestandardowego
Rekordy dziennika niestandardowego mają typ o nazwie dziennika hello zapewniających i hello właściwości w hello w poniższej tabeli.

| Właściwość | Opis |
|:--- |:--- |
| TimeGenerated |Data i godzina hello rekord został zebrany przez analizy dzienników.  Jeśli dziennika hello używa ogranicznik na podstawie czasu to czas hello zebrane z hello wpisu. |
| SourceSystem |Typ rekordu hello agenta zostały zebrane. <br> Połącz OpsManager — agent systemu Windows, bądź bezpośrednio lub System Center Operations Manager <br> Linux — wszystkich agentów systemu Linux |
| RawData |Pełny tekst hello zbierane wpisu. |
| ManagementGroupName |Nazwa grupy zarządzania hello agenci zarządzania programu System Center Operations.  W przypadku innych agentów jest AOI -\<identyfikator obszaru roboczego\> |

## <a name="log-searches-with-custom-log-records"></a>Dziennik wyszukiwania z rekordów dziennika niestandardowego
Rekordy z dzienników niestandardowych są przechowywane w repozytorium OMS hello tak jak rekordy z innego źródła danych.  Dysponują typu pasującego hello nazwy podczas definiowania dziennika hello, dzięki czemu można używać właściwości typu hello w rekordach tooretrieve wyszukiwania zebrane z określonego dziennika.

Witaj poniższej tabeli przedstawiono różne przykłady dziennik wyszukiwania, które pobieranie rekordów z dzienników niestandardowych.

| Zapytanie | Opis |
|:--- |:--- |
| Typ = MyApp_CL |Wszystkie zdarzenia z niestandardowego dziennika o nazwie MyApp_CL. |
| Typ = MyApp_CL Severity_CF = błąd |Wszystkie zdarzenia z niestandardowego dziennika o nazwie MyApp_CL o wartości *błąd* w pole niestandardowe o nazwie *Severity_CF*. |

>[!NOTE]
> Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), następnie hello powyżej zapytania spowoduje zmianę następujących toohello.

> | Zapytanie | Opis |
|:--- |:--- |
| MyApp_CL |Wszystkie zdarzenia z niestandardowego dziennika o nazwie MyApp_CL. |
| MyApp_CL &#124; gdzie Severity_CF == "error" |Wszystkie zdarzenia z niestandardowego dziennika o nazwie MyApp_CL o wartości *błąd* w pole niestandardowe o nazwie *Severity_CF*. |


## <a name="sample-walkthrough-of-adding-a-custom-log"></a>Przykładowe wskazówki dodawania dziennik niestandardowy
Witaj poniższej sekcji przedstawiono przykład tworzenia dziennik niestandardowy.  Witaj przykładowy dziennik zbieranych ma pojedynczy wpis w każdym wierszu, począwszy od daty i czasu, a następnie rozdzielana przecinkami pól dla kodu, stanu i komunikatu.  Poniżej przedstawiono kilka przykładowych wpisów.

    2016-03-10 01:34:36 207,Success,Client 05a26a97-272a-4bc9-8f64-269d154b0e39 connected
    2016-03-10 01:33:33 208,Warning,Client ec53d95c-1c88-41ae-8174-92104212de5d disconnected
    2016-03-10 01:35:44 209,Success,Transaction 10d65890-b003-48f8-9cfc-9c74b51189c8 succeeded
    2016-03-10 01:38:22 302,Error,Application could not connect toodatabase
    2016-03-10 01:31:34 303,Error,Application lost connection toodatabase

### <a name="upload-and-parse-a-sample-log"></a>Przekazywanie i przeanalizować przykładowy dziennik
Firma Microsoft Podaj jeden z plików dziennika hello może uzyskać i hello zdarzenia, które będzie zbierać.  W takim przypadku nowy wiersz jest wystarczające ogranicznika.  Jeśli pojedynczy wpis w dzienniku hello można jednak obejmują wiele wierszy, ogranicznika sygnatury czasowej wymagałoby toobe używane.

![Przekazywanie i przeanalizować przykładowy dziennik](media/log-analytics-data-sources-custom-logs/delimiter.png)

### <a name="add-log-collection-paths"></a>Dodaj ścieżki zbierania dzienników
pliki dziennika Hello będą znajdować się w *C:\MyApp\Logs*.  Nowy plik będzie można utworzyć każdego dnia o nazwie zawierającej daty hello we wzorcu hello *appYYYYMMDD.log*.  Będą wystarczające wzorca dla tego dziennika *C:\MyApp\Logs\\\*log*.

![Ścieżka zbierania dzienników](media/log-analytics-data-sources-custom-logs/collection-path.png)

### <a name="provide-a-name-and-description-for-hello-log"></a>Podaj nazwę i opis dla dziennika hello
Używamy nazwę *MyApp_CL* i wpisz **opis**.

![Nazwa dziennika](media/log-analytics-data-sources-custom-logs/log-name.png)

### <a name="validate-that-hello-custom-logs-are-being-collected"></a>Zweryfikuj, że dzienników niestandardowych hello są zbierane
Używamy zapytania *typu = MyApp_CL* tooreturn wszystkie rekordy z hello zebranych dziennika.

![Dziennik zapytań bez pól niestandardowych](media/log-analytics-data-sources-custom-logs/query-01.png)

### <a name="parse-hello-custom-log-entries"></a>Przeanalizować hello wpisy dziennika niestandardowego
Używamy hello toodefine pola niestandardowe *EventTime*, *kod*, *stan*, i *komunikat* pola i firma Microsoft może widocznej różnicy hello w hello rekordy, które są zwracane przez zapytanie hello.

![Kwerenda dziennika z polami niestandardowymi](media/log-analytics-data-sources-custom-logs/query-02.png)

## <a name="next-steps"></a>Następne kroki
* Użyj [pól niestandardowych](log-analytics-custom-fields.md) tooparse hello wpisy w dzienniku niestandardowe hello, w polach tooindividual.
* Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) tooanalyze hello dane zebrane ze źródeł danych i rozwiązań.
