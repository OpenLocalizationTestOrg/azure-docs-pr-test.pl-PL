---
title: Kreator kopiowania Azure fabryki aaaData | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat sposobu toouse hello danych toocopy kreatora kopiowania Azure fabryka danych z toosinks źródeł danych obsługiwane."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 0974eb40-db98-4149-a50d-48db46817076
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: 188b3ae15f937b84a58aec1b979347ac8090abf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory-copy-wizard"></a>Kreator kopiowania fabryki danych Azure
Hello kreatora kopiowania fabryki danych Azure ułatwia proces hello wprowadzania danych, który zazwyczaj jest to pierwszy krok w scenariuszu integracji danych na całej trasie. Podczas przechodzenia za pośrednictwem hello kreatora kopiowania fabryki danych Azure, nie trzeba toounderstand żadnych definicji JSON połączonej usługi, zestawy danych i potoki. Witaj Kreator automatycznie tworzy dane toocopy potoku z docelowym wybranego źródła toohello hello wybranych danych. Ponadto hello kreatora kopiowania pomaga danych hello toovalidate trwa pozyskanych w czasie hello autorstwa. Pozwala to zaoszczędzić czas, szczególnie gdy możesz są pobierania danych dla hello po raz pierwszy z hello źródła danych. toostart hello kreatora kopiowania, kliknij przycisk hello **skopiować dane** kafelka na stronie głównej hello w fabryce danych.

![Kreator kopiowania](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="designed-for-big-data"></a>Przeznaczone dla danych big data
Ten kreator umożliwia tooeasily przenoszenia danych z różnych źródeł toodestinations w minutach. Po przejściu w Kreatorze hello potoku z działaniem kopiowania jest tworzony automatycznie, oraz jednostki zależne fabryki danych (połączonych usług i zestawy danych). Żadne dodatkowe czynności nie są wymagane toocreate hello potoku.   

![Wybierz źródło danych](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> Aby uzyskać instrukcje krok po kroku toocreate przykładowych potoku toocopy danych z tabeli bazy danych SQL Azure tooan obiektów blob platformy Azure, zobacz hello [Samouczek Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md).
>
>

Kreator Hello zaprojektowano z danymi big data na uwadze od początku hello, obsługę różnych danych i typów obiektów. Można tworzyć potoki fabryki danych, łączące setki folderów, plików i tabele. Kreator Hello obsługuje Podgląd danych, przechwytywania schematu i mapowania i filtrowanie danych.

## <a name="automatic-data-preview"></a>Podgląd danych
Można wyświetlić podgląd część danych hello z hello wybranego źródła danych w kolejności toovalidate czy hello danych ma toocopy. Ponadto w przypadku hello źródła danych w pliku tekstowym, hello kreatora kopiowania analizuje hello tekstu pliku toolearn hello wierszy i kolumn ograniczniki oraz schematu automatycznie.

![Ustawienia format pliku](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a>Przechwytywanie schematu i mapowanie
Schemat danych wejściowych Hello może nie odpowiadać hello schemat danych wyjściowych w niektórych przypadkach. W tym scenariuszu należy toomap kolumny z toocolumns schematu źródła powitania od schematu docelowej hello.

> [!TIP]
> Kopiowanie danych z serwera SQL lub bazy danych SQL Azure do usługi Azure SQL Data Warehouse, jeśli tabela hello nie istnieje w magazynie docelowym hello, fabryki danych obsługi automatycznego tworzenia tabel za pomocą schematu źródła. Dowiedz się więcej o [przenieść tooand danych z usługi Azure SQL Data Warehouse przy użyciu fabryki danych Azure](./data-factory-azure-sql-data-warehouse-connector.md).
>

Użyj listy rozwijanej tooselect kolumny z hello źródła schematu toomap tooa kolumny w hello schematu docelowego. Hello kreatora kopiowania próbuje toounderstand Twojego wzorzec mapowania kolumn. Ma to zastosowanie hello tego samego wzorca toohello rest hello kolumn, dzięki czemu nie trzeba tooselect kolumn hello indywidualnie toocomplete hello schematu mapowania. Jeśli wolisz, można zastąpić te mapowania za pomocą hello list rozwijanych toomap hello kolumn jeden po drugim. wzorzec Hello staje się bardziej dokładne mapy większą liczbę kolumn. Hello kreatora kopiowania stale aktualizuje wzorzec hello, a ostatecznie osiągnie hello prawo wzorzec zostanie w mapowaniu kolumn hello mają tooachieve.     

![Mapowanie schematu](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a>Filtrowanie danych
Dane można filtrować źródła danych tooselect tylko hello wymagające toobe skopiowane toohello ujścia danych magazynu. Filtrowanie zmniejsza ilość hello hello toobe toohello skopiowanych ujścia danych danych przechowywania i w związku z tym zwiększa przepływność hello hello operacji kopiowania. Udostępnia dane toofilter elastyczny sposób relacyjnej bazy danych przy użyciu język zapytań SQL hello lub pliki w folderze obiektów blob platformy Azure przy użyciu [funkcji fabryki danych i zmiennych](data-factory-functions-variables.md).   

### <a name="filtering-of-data-in-a-database"></a>Filtrowanie danych w bazie danych
Witaj Poniższy zrzut ekranu przedstawia zapytanie SQL, używając hello `Text.Format` funkcji i `WindowStart` zmiennej.

![Sprawdzanie poprawności wyrażenia](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a>Filtrowanie danych w folderze obiektów blob platformy Azure
W przypadku używania zmiennych w danych toocopy ścieżka folderu hello z folderu, który jest określana w czasie wykonywania na podstawie [zmienne systemowe](data-factory-functions-variables.md#data-factory-system-variables). zmienne Hello obsługiwane są: **{year}**, **{month}**, **{day}**, **{godzina}**, **{minutę}**, i **{niestandardowych}**. Na przykład: inputfolder / {year} / {month} / {day}.

Załóżmy, że podania folderów w hello następującego formatu:

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

Kliknij przycisk hello **Przeglądaj** przycisk dla **pliku lub folderu**, Przeglądaj tooone tych folderów (na przykład 2016 -> 03 -> 01 -> 02) i kliknij przycisk **wybierz**. Powinny pojawić się `2016/03/01/02` w polu tekstowym hello. Teraz, Zastąp **2016** z **{year}**, **03** z **{month}**, **01** z **{day}** , i **02** z **{godzina}**i naciśnij klawisz hello **kartę** klucza. Powinny pojawić się format hello tooselect listy rozwijane dla tych czterech zmiennych:

![Używanie zmiennych systemu](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

Jak pokazano na powitania po zrzut ekranu, można również użyć **niestandardowych** zmiennej i wszystkie [obsługiwane ciągi formatujące](https://msdn.microsoft.com/library/8kb3ddd4.aspx). tooselect folder o tej struktury, użyj hello **Przeglądaj** najpierw przycisk. Następnie zastąp wartości z **{niestandardowych}**i naciśnij klawisz hello **kartę** pole tekstowe hello toosee klucza można wpisać hello ciąg formatu.     

![Użycie niestandardowej zmiennej](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="scheduling-options"></a>Opcje harmonogramu
Można wykonać operacji kopiowania hello raz lub zgodnie z harmonogramem (co godzinę, codziennie, i tak dalej). Obie te opcje może służyć do szerokości hello hello łączników w środowiskach, w tym lokalnych, chmury i lokalnej kopii pulpitu.

Operacji kopiowania jednorazowe umożliwia przenoszenie danych z docelowym tooa źródła tylko raz. Ma to zastosowanie toodata dowolnej wielkości i dowolnego obsługiwanego formatu. Witaj zaplanowanych kopii umożliwia toocopy danych na wyznaczonych cyklu. Można użyć zaawansowanych ustawień (np. Ponów próbę, limit czasu i alertami) tooconfigure hello zaplanowanych kopii.

![Planowanie właściwości](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a>Następne kroki
Przewodnik Szybki pomocą hello kreatora kopiowania fabryki danych toocreate potoku działanie kopiowania, zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania hello](data-factory-copy-data-wizard-tutorial.md).
