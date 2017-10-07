---
title: "dane użycia aaaInvestigate i udziału z interaktywnego skoroszytów w usłudze Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Analiza demograficznych użytkowników aplikacji sieci web."
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: bdcebe0f97fdad0a0b301df5950dc09698f5a4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="investigate-and-share-usage-data-with-interactive-workbooks-in-application-insights"></a>Badanie i udostępniać dane użycia interakcyjne skoroszytów w usłudze Application Insights

Łączenie skoroszytów [Azure Application Insights](app-insights-overview.md) wizualizacje danych [zapytania analityczne](app-insights-analytics.md)i tekstu w dokumentach interaktywnego. Skoroszyty jest edytowany przez innych członków zespołu z toohello dostępu do tego samego zasobów platformy Azure. Oznacza to, hello zapytania i formanty używane toocreate skoroszytu osób dostępne tooother odczytywania hello skoroszytu, dzięki czemu można je łatwo tooexplore, rozszerzać i sprawdź, czy błędy.

Skoroszyty są przydatne w scenariuszach, takich jak:

* Eksploracji hello użycia aplikacji, jeśli nie wiesz wcześniej metryki hello zainteresowania: liczby użytkowników, stawki przechowywania, kursy wymiany itp. W przeciwieństwie do innych narzędzi analizy użycia w usłudze Application Insights skoroszytów umożliwiają łączenie wielu rodzajów wizualizacje i analiz nadawania doskonałe rozwiązanie dla tego rodzaju dowolnych eksploracji.
* Wyjaśniający, jak działa funkcja nowo wydanego zespołu tooyour, przez użytkownika przedstawiający Liczba interakcji klucza i innych metryk.
* Udostępnianie wyników hello a / B eksperymentu w Twojej aplikacji za pomocą innych członków zespołu. Można wyjaśnić hello cele hello eksperymentować tekstu, a następnie Pokaż wszystkie metryki użycia i Analytics zapytanie użyte tooevaluate hello eksperymentu, wraz z wyczyść dokumentów wywołania do tego, czy wszystkie metryki został powyżej lub poniżej docelowe.
* Raportowanie hello wpływ awarii na powitania użycia aplikacji, połączenie danych, wyjaśnienie tekstu i omówienie dalej awarie tooprevent kroki w przyszłości hello.

> [!NOTE]
> Zasób usługi Application Insights musi zawierać wyświetleń strony lub skoroszytów toouse zdarzeń niestandardowych. [Dowiedz się, jak tooset Twojego stronę toocollect aplikacji automatycznie widoków z hello zestaw SDK usługi Application Insights JavaScript](app-insights-javascript.md).
> 
> 

## <a name="editing-rearranging-cloning-and-deleting-workbook-sections"></a>Edytowanie, zmienianie rozmieszczenia klonowania i usuwanie sekcji skoroszytu

Skoroszyt jest wprowadzonych sekcji: wizualizacje można edytować niezależnie użycia, wykresów, tabel, tekst i analiza wyników zapytania.

tooedit hello zawartości sekcji skoroszytu, kliknij przycisk hello **Edytuj** poniżej i toohello prawej części hello skoroszytu.

![Formanty edycji sekcji Application Insights skoroszytów](./media/app-insights-usage-workbooks/editing-controls.png)

1. Po zakończeniu edycji sekcji, kliknij **przeprowadzić edycję** w hello lewym dolnym rogu sekcji hello.

2. toocreate duplikat sekcji, kliknij przycisk hello **klonowania w tej sekcji** ikony. Tworzenie duplikatów sekcji jest doskonały tooway tooiterate na zapytanie bez utraty poprzedniej iteracji.

3. toomove się sekcji w skoroszycie, kliknij przycisk hello **Przenieś w górę** lub **Przenieś w dół** ikony.

4. tooremove sekcji stałe, kliknij przycisk hello **Usuń** ikony.

## <a name="adding-usage-data-visualization-sections"></a>Dodawanie sekcji wizualizacji danych użycia

Skoroszyty oferuje cztery typy wizualizacji analizy użycia wbudowanych. Każdy odpowiedzi na często zadawane pytania dotyczące użycia hello aplikacji. tooadd tabel i wykresów innych niż te cztery sekcje dodać Analytics query sekcje (patrz poniżej).

tooadd użytkowników, sesji, zdarzeń i przechowywania sekcji tooyour skoroszytu, użyj hello **Dodaj użytkowników** lub innych odpowiedni przycisk u dołu hello hello skoroszytu lub u dołu hello dowolnej sekcji.

![Sekcja użytkownicy w skoroszytach](./media/app-insights-usage-workbooks/users-section.png)

**Użytkownicy** sekcje odpowiedzi "ilu użytkowników wyświetli stronę niektórych lub używać niektórych funkcji Moja witryna"?

**Sesje** sekcje odpowiedzi "ile sesji użytkownicy poświęcają wyświetlanie niektórych strony lub funkcji z mojej lokacji?"

**Zdarzenia** sekcje odpowiedzi "ile razy użytkowników wyświetlania niektóre strony lub funkcja witryny sieci?"

Oferuje każdego z tych typów sekcji trzy hello tego samego zestawy kontrolek i wizualizacji:

* [Więcej informacji na temat edytowania sekcje użytkownikami, sesjami i zdarzenia](app-insights-usage-segmentation.md)
* Przełącz hello wykresu głównego, siatki histogram, automatyczne insights i przykładowej wizualizacji użytkowników przy użyciu hello **Pokaż wykres**, **Pokaż siatkę**, **Pokaż Insights**i **Przykładowych tych użytkowników** pola wyboru u góry hello każdej sekcji.

![Przechowywania części skoroszytów](./media/app-insights-usage-workbooks/retention-section.png)

**Przechowywania** sekcje odpowiedzi "Osób, które są wyświetlane niektóre strony lub używać niektórych funkcji w ciągu jednego dnia lub tygodnia, ile wrócił następnego dnia lub tygodnia?"

* [Dowiedz się więcej na temat edytowania sekcje przechowywania](app-insights-usage-retention.md)
* Przełącz hello opcjonalne ogólną przechowywania wykresu przy użyciu hello **Pokaż ogólną przechowywania wykresu** wyboru u góry hello hello sekcji.

## <a name="adding-application-insights-analytics-sections"></a>Dodawanie sekcji Application Insights analityka

![Analiza części skoroszytów](./media/app-insights-usage-workbooks/analytics-section.png)

tooadd Application Insights Analytics zapytania sekcja tooyour skoroszytu, użyj hello **dodać Analytics query** przycisk u dołu hello hello skoroszytu lub u dołu hello dowolnej sekcji.

Analiza zapytania sekcje umożliwiają dodawanie zapytań o dowolnego przez dane usługi Application Insights do skoroszytów. Taka elastyczność oznacza, że sekcje zapytania Analytics powinna być Twoje Przejdź toofor udzielenie odpowiedzi na pytania dotyczące witryny innej niż hello czterech wymienionych powyżej dla użytkowników, sesji zdarzeń i przechowywania, takich jak:

* Jak wiele wyjątków została throw Twojej lokacji podczas hello sam okresu jako spadek użycia?
* Jaki był hello dystrybucji czas ładowania strony dla użytkowników, którzy przeglądają niektóre strony?
* Ilu użytkowników wyświetlić niektórych zbiór stron w witrynie, ale nie innymi zestaw stron? Może to być przydatne toounderstand, jeśli masz klastrów użytkowników, którzy korzystają z różnych podzbiory funkcji witryny sieci (Użyj hello `join` operatora z hello `kind=leftanti` modyfikator w hello język zapytań usługi Analiza dzienników).

Użyj hello [materiały referencyjne dotyczące języka zapytań usługi Analiza dzienników](https://docs.loganalytics.io/) toolearn więcej informacji na temat Pisanie zapytań.

## <a name="adding-text-and-markdown-sections"></a>Dodawanie tekstu i sekcji języka znaczników Markdown

Dodawanie nagłówków, wyjaśnienia i komentarzami tooyour skoroszytów pomaga przekształcić zestaw tabel i wykresów udostępniono. Sekcje tekstu w skoroszytach obsługuje hello [składni języka Markdown](https://daringfireball.net/projects/markdown/) tekstu formatowania, takich jak nagłówki pogrubienie, kursywa i listy punktowane.

tooadd skoroszytu tooyour sekcji tekstu, użyj hello **Dodawanie tekstu** przycisk u dołu hello hello skoroszytu lub u dołu hello dowolnej sekcji.

## <a name="saving-and-sharing-workbooks-with-your-team"></a>Zapisywanie i udostępnianie skoroszytów z zespołem

Skoroszyty są zapisywane w ramach zasobu usługi Application Insights w hello **Moje raporty** sekcja, która jest prywatny tooyou lub hello **udostępnionych raportów** sekcja, która jest dostępna tooeveryone z dostępem toohello zasobu usługi Application Insights. tooview hello skoroszytów w zasobie powitania kliknij hello **Otwórz** przycisku w pasku akcji hello.

tooshare skoroszytu, który jest aktualnie **Moje raporty**:

1. Kliknij przycisk **Otwórz** na pasku akcji hello
2. Kliknij przycisk "..." hello obok skoroszytu hello ma tooshare
3. Kliknij przycisk **Przenieś raporty tooShared**.

tooshare skoroszytu z łączem lub za pośrednictwem poczty e-mail, kliknij przycisk **udziału** hello pasku akcji. Należy pamiętać, że adresaci łącza hello muszą mieć dostęp do zasobu toothis hello Azure tooview portalu hello skoroszytu. zmiany toomake adresatów muszą mieć co najmniej uprawnienia współautora hello zasobu.

toopin łącze tooan skoroszytu tooa pulpitu nawigacyjnego platformy Azure:

1. Kliknij przycisk **Otwórz** na pasku akcji hello
2. Kliknij przycisk "..." hello obok skoroszytu hello ma toopin
3. Kliknij przycisk **toodashboard numeru Pin**.

## <a name="next-steps"></a>Następne kroki

## <a name="next-steps"></a>Następne kroki
- Użycie tooenable napotyka, Rozpocznij wysyłanie [zdarzeń niestandardowych](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) lub [wyświetlenia strony](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Jeśli już wysyłania zdarzeń niestandardowych lub wyświetleń strony Eksploruj hello użycia narzędzia toolearn użytkowników wykorzystania usługi.
    - [Użytkownicy, sesje, zdarzenia](app-insights-usage-segmentation.md)
    - [Lejki](usage-funnels.md)
    - [Przechowywanie](app-insights-usage-retention.md)
    - [User Flows (Przepływy użytkowników)](app-insights-usage-flows.md)
    - [Dodaj kontekstu użytkownika](app-insights-usage-send-user-context.md)
    
