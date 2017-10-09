---
title: "aaaCreate widoków danych tooanalyze w OMS Log Analytics | Dokumentacja firmy Microsoft"
description: "Widok projektanta w analizy dzienników umożliwia toocreate niestandardowe widoki, które są wyświetlane w portalu OMS i Azure hello i zawierają różne wizualizacje danych w repozytorium OMS hello. Ten artykuł zawiera omówienie projektanta widoków i procedur tworzenia i edytowania widoków niestandardowych."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: ce41dc30-e568-43c1-97fa-81e5997c946a
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 40b4bfef50d70e4479b6cae16abfa8ec33d1a2f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-view-designer-toocreate-custom-views-in-log-analytics"></a>Korzystanie z projektanta widoków toocreate niestandardowych widoków w analizy dzienników
Witaj Projektant widoków w [analizy dzienników](log-analytics-overview.md) pozwala toocreate niestandardowe widoki w konsoli OMS hello zawierających różne wizualizacje danych w repozytorium OMS hello. Ten artykuł zawiera omówienie projektanta widoków i procedur tworzenia i edytowania widoków niestandardowych.

Inne artykuły, które są dostępne dla projektanta widoku są następujące:

* [Kafelek odwołanie](log-analytics-view-designer-tiles.md) — odwołanie hello ustawienia dla każdego z hello Kafelki toouse dostępne w niestandardowych widoków.
* [Odwołanie do części wizualizacji](log-analytics-view-designer-parts.md) — odwołanie hello ustawienia dla każdego z hello Kafelki toouse dostępne w niestandardowych widoków.

>[!NOTE]
> Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), następnie zapytania we wszystkich widokach musi być napisana w hello [nowy język kwerendy](https://go.microsoft.com/fwlink/?linkid=856078).  Wszystkie widoki, które zostały utworzone przed uaktualniono hello obszaru roboczego będzie automtically przekonwertować.

## <a name="concepts"></a>Pojęcia
Widoki utworzone z projektanta widoków hello zawierać elementów hello w hello w poniższej tabeli.

| Część | Opis |
|:--- |:--- |
| Kafelek |Wyświetlane na pulpicie nawigacyjnym hello głównego omówienie analizy dziennika.  Zawiera podsumowania visual hello informacji zawartych w hello widok niestandardowy.  Różne typy kafelka zapewniają różne wizualizacje rekordów w repozytorium OMS hello.  Polecenie hello kafelka tooopen hello widok niestandardowy. |
| Widok niestandardowy |Wyświetlane po kliknięciu przez użytkownika hello na powitania kafelka.  Zawiera co najmniej jeden części wizualizacji. |
| Części wizualizacji |Wizualizacja danych w repozytorium OMS hello oparte na co najmniej jeden [dziennika wyszukiwania](log-analytics-log-searches.md).  Większość elementów zawiera nagłówek, który zapewnia wysokiego poziomu wizualizacji i lista wyników najwyższego hello.  Typy różnych części zapewniają różne wizualizacje rekordów w repozytorium OMS hello.  Polecenie elementów w tooperform części hello wyszukiwania dziennika, zapewniając szczegółowe dane. |

![Omówienie projektanta widoku](media/log-analytics-view-designer/overview.png)

## <a name="add-view-designer-tooyour-workspace"></a>Dodaj obszar roboczy tooyour Projektant widoków
Gdy widok projektanta jest w wersji zapoznawczej, należy go dodać tooyour obszaru roboczego, wybierając **funkcje w wersji zapoznawczej** w hello **ustawienia** sekcji hello portalu OMS.

![Włącz podgląd](media/log-analytics-view-designer/preview.png)

## <a name="creating-and-editing-views"></a>Tworzenie i edytowanie widoków
### <a name="create-a-new-view"></a>Utwórz nowy widok
Otwórz nowy widok w hello **Widok projektanta** , klikając hello Widok projektanta kafelka na pulpicie nawigacyjnym hello głównego OMS.

![Widok projektanta kafelka](media/log-analytics-view-designer/view-designer-tile.png)

### <a name="edit-an-existing-view"></a>Edytuj istniejący widok
tooedit istniejącego widoku w hello Projektant widoków, otwórz hello widoku, klikając jej kafelka na pulpicie nawigacyjnym hello głównego OMS.  Następnie kliknij przycisk hello **Edytuj** przycisk Widok hello tooopen hello Widok projektanta.

![Edytowanie widoku](media/log-analytics-view-designer/menu-edit.png)

### <a name="clone-an-existing-view"></a>Klonowanie istniejącego widoku
Podczas klonowania widoku, tworzy nowy widok i otwarcie go w hello Widok projektanta.  Nowy widok Hello będzie miał hello takie same nazwy co oryginalna z zakończoną dołączany toohello "Kopiuj" hello.  tooclone widok, otwórz hello istniejącego widoku, klikając jej kafelka na pulpicie nawigacyjnym hello głównego OMS.  Następnie kliknij przycisk hello **klonowania** przycisk Widok hello tooopen hello Widok projektanta.

![Klonowanie widoku](media/log-analytics-view-designer/edit-menu-clone.png)

### <a name="delete-an-existing-view"></a>Usuwanie istniejącego widoku
toodelete istniejący widok, otwórz hello widoku, klikając jej kafelka na pulpicie nawigacyjnym hello głównego OMS.  Następnie kliknij przycisk hello **Edytuj** przycisk Widok hello tooopen hello Projektant widoków, a następnie kliknij przycisk **Usuń widok**.

![Usuwanie widoku](media/log-analytics-view-designer/edit-menu-delete.png)

### <a name="export-an-existing-view"></a>Eksportuj istniejącego widoku
Możesz wyeksportować plik JSON tooa widoku, który można zaimportować do innego obszaru roboczego lub użyć w [szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).  tooexport istniejący widok, otwórz hello widoku, klikając jej kafelka na pulpicie nawigacyjnym hello głównego OMS.  Następnie kliknij przycisk hello **wyeksportować** toocreate przycisk plików w folderze pobierania hello przeglądarki.  Nazwa Hello hello pliku będzie hello Nazwa widoku hello z rozszerzeniem hello *omsview*.

![Eksportowanie widoku](media/log-analytics-view-designer/edit-menu-export.png)

### <a name="import-an-existing-view"></a>Importuj istniejący widok
Możesz zaimportować *omsview* pliku, który został wyeksportowany z innej grupy zarządzania.  tooimport istniejącego widoku, najpierw utwórz nowy widok.  Następnie kliknij przycisk hello **importu** przycisk i wybierz hello *omsview* pliku.  Konfiguracja Hello w pliku hello zostaną skopiowane do hello istniejącego widoku.

![Eksportowanie widoku](media/log-analytics-view-designer/edit-menu-import.png)

## <a name="working-with-view-designer"></a>Praca z projektanta widoków
Witaj Widok projektanta ma trzy okienka.  Witaj **projekt** okienko reprezentuje hello widok niestandardowy.  Po dodaniu Kafelki i części z hello **kontroli** toohello okienko **projekt** okienku są dodawane toohello widoku.  Witaj **właściwości** okienku zostaną wyświetlone właściwości hello kafelka hello lub wybranej części.

![Projektant widoków](media/log-analytics-view-designer/view-designer-screenshot.png)

### <a name="configure-view-tile"></a>Konfigurowanie widoku kafelków
Widok niestandardowy może mieć tylko jednego kafelka.  Wybierz hello **Kafelek** kartę w hello **kontroli** okienko tooview hello bieżący Kafelek lub wybierz alternatywny.  Witaj **właściwości** okienku zostaną wyświetlone właściwości hello hello bieżący Kafelek.  Skonfiguruj właściwości kafelka hello zgodnie z toohello szczegółowe informacje w hello [Kafelek odwołania](log-analytics-view-designer-tiles.md) i kliknij przycisk **Zastosuj** toosave zmiany.

### <a name="configure-visualization-parts"></a>Skonfiguruj części wizualizacji
Widok może zawierać dowolną liczbę części wizualizacji.  Wybierz hello **widoku** kartę, a następnie wizualizacji część tooadd toohello widoku.  Witaj **właściwości** okienku zostaną wyświetlone właściwości hello hello wybrane części.  Konfigurowanie widoku hello właściwości zgodnie z toohello szczegółowe informacje w hello [odwołanie do części wizualizacji](log-analytics-view-designer-parts.md) i kliknij przycisk **Zastosuj** toosave zmiany.

### <a name="delete-a-visualization-part"></a>Usunąć części wizualizacji
Możesz usunąć część wizualizacji z widoku hello klikając hello **X** przycisku na powitania prawym górnym rogu hello części.

### <a name="rearrange-visualization-parts"></a>Rozmieszczanie części wizualizacji
Widoki mieć tylko jeden wiersz części wizualizacji.  Rozmieszczanie istniejące składniki w widoku, klikając i przeciągając je tooa nowej lokalizacji.

## <a name="next-steps"></a>Następne kroki
* Dodaj [Kafelki](log-analytics-view-designer-tiles.md) tooyour widok niestandardowy.
* Dodaj [części wizualizacji](log-analytics-view-designer-parts.md) tooyour widok niestandardowy.
