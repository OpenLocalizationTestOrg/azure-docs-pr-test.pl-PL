---
title: "dane aaaCopy łatwo za pomocą Kreatora kopiowania - Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu toouse hello danych toocopy kreatora kopiowania fabryka danych z toosinks źródeł danych obsługiwane."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f904972f-cd33-48db-9755-2b3196ae4168
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 99437ec16facf3b94c8be18487ec89e9f13acc9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-or-move-data-easily-with-azure-data-factory-copy-wizard"></a>Skopiować lub przenieść dane z Kreatora kopiowania fabryki danych Azure
Witaj kreatora kopiowania fabryki danych Azure to proces hello tooease wprowadzania danych, który zazwyczaj jest to pierwszy krok w scenariuszu integracji danych na całej trasie. Podczas przechodzenia za pośrednictwem hello kreatora kopiowania fabryki danych Azure, nie trzeba toounderstand żadnych definicji JSON połączonej usługi, zestawy danych i potoki. Po zakończeniu wszystkich kroków powitania w Kreatorze hello hello Kreator automatycznie tworzy jednak danych toocopy potoku z docelowym wybranego źródła toohello hello wybranych danych. Ponadto hello Kreator kopiowania ułatwia toovalidate danych hello jest pozyskanych w czasie tworzenia hello, który zapisuje większość czasu, szczególnie gdy możesz są pobierania danych dla hello po raz pierwszy ze źródła danych hello. toostart hello kreatora kopiowania, kliknij przycisk hello **skopiować dane** kafelka na stronie głównej hello w fabryce danych.

![Kreator kopiowania](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="an-intuitive-wizard-for-copying-data"></a>Intuicyjne Kreator kopiowania danych
Ten kreator umożliwia tooeasily przenoszenia danych z różnych źródeł toodestinations w minutach. Po przejściu w Kreatorze hello, potoku z działaniem kopiowania jest utworzony automatycznie wraz z zależnych jednostek fabryki danych (połączonych usług i zbiory danych). Żadne dodatkowe czynności nie są wymagane toocreate hello potoku.   

![Wybierz źródło danych](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> Zobacz [Samouczek Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) artykułu dla toocreate instrukcje krok po kroku przykładowych potoku toocopy danych z tabeli bazy danych SQL Azure tooan obiektów blob platformy Azure. 
> 
> 

Kreator Hello zaprojektowano z danymi big data na uwadze od początku hello. To proste i skuteczne tooauthor fabryki danych potoki, łączące setki folderów, plików lub za pomocą Kreatora kopiowania danych hello tabel. Witaj Kreator obsługuje hello następujących trzech funkcji: Podgląd danych, przechwytywania schematu i mapowania i filtrowanie danych. 

## <a name="automatic-data-preview"></a>Podgląd danych
Kreator kopiowania Hello umożliwia możesz tooreview część hello danych z hello wybrane źródło danych dla Ciebie toovalidate czy hello danych jest powitania kliknij prawym przyciskiem myszy dane, które mają toocopy. Ponadto w przypadku hello źródła danych w pliku tekstowym, Kreator kopiowania hello analizuje hello tekstu pliku toolearn wiersza i kolumny, ograniczniki i schematu automatycznie. 

![Ustawienia format pliku](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a>Przechwytywanie schematu i mapowanie
Schemat danych wejściowych Hello może nie odpowiadać hello schemat danych wyjściowych w niektórych przypadkach. W tym scenariuszu należy toomap kolumny z toocolumns schematu źródła powitania od schematu docelowej hello. 

Kreator kopiowania Hello mapuje automatycznie kolumn w toocolumns schematu źródła hello w schemacie docelowego hello. Można zastąpić hello mapowania za pomocą list rozwijanych hello (lub) określ, czy kolumna musi toobe pominięte podczas kopiowania danych hello.   

![Mapowanie schematu](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a>Filtrowanie danych
Kreator Hello pozwala toofilter źródła danych tooselect tylko hello dane wymagające toobe skopiowane toohello docelowego/ujście danych magazynu. Filtrowanie zmniejsza ilość hello hello toobe toohello skopiowanych ujścia danych danych przechowywania i w związku z tym zwiększa przepływność hello hello operacji kopiowania. Zapewnia elastyczne danych toofilter relacyjnej bazy danych przy użyciu SQL zapytań języka (lub) plików w folderze obiektów blob platformy Azure przy użyciu [funkcji fabryki danych i zmiennych](data-factory-functions-variables.md).   

### <a name="filtering-of-data-in-a-database"></a>Filtrowanie danych w bazie danych
Przykład Witaj zapytanie SQL hello używa hello `Text.Format` funkcji i `WindowStart` zmiennej. 

![Sprawdzanie poprawności wyrażenia](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a>Filtrowanie danych w folderze obiektów blob platformy Azure
W przypadku używania zmiennych w danych toocopy ścieżka folderu hello z folderu, który jest określana w czasie wykonywania na podstawie [zmienne systemowe](data-factory-functions-variables.md#data-factory-system-variables). zmienne Hello obsługiwane są: **{year}**, **{month}**, **{day}**, **{godzina}**, **{minutę}**, i **{niestandardowych}**. Przykład: inputfolder / {year} / {month} / {day}.

Załóżmy, że podania folderów w hello następującego formatu:

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

Kliknij przycisk hello **Przeglądaj** przycisk dla **pliku lub folderu**, Przeglądaj tooone tych folderów (na przykład 2016 -> 03 -> 01 -> 02) i kliknij przycisk **wybierz**. Powinny pojawić się `2016/03/01/02` w polu tekstowym hello. Teraz, Zastąp **2016** z **{year}**, **03** z **{month}**, **01** z **{day}**, i **02** z **{godzina}**, i naciśnij klawisz Tab. Powinny pojawić się format hello tooselect listy rozwijane dla tych czterech zmiennych:

![Używanie zmiennych systemu](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

Jak pokazano na powitania po zrzut ekranu, można również użyć **niestandardowych** zmiennej i wszystkie [obsługiwane ciągi formatujące](https://msdn.microsoft.com/library/8kb3ddd4.aspx). tooselect folder o tej struktury, użyj hello **Przeglądaj** najpierw przycisk. Następnie zastąp wartości z **{niestandardowych}**i naciśnij klawisz Tab toosee hello pole tekstowe można wpisać ciąg formatu hello.     

![Użycie niestandardowej zmiennej](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="support-for-diverse-data-and-object-types"></a>Obsługa różnych danych i typów obiektów
Za pomocą Kreatora kopiowania hello, można wydajnie przenosić setki folderów, plików i tabele.

![Wybierz tabele, z których dane toocopy](./media/data-factory-copy-wizard/select-tables-to-copy-data.png)

## <a name="scheduling-options"></a>Opcje harmonogramu
Można wykonać operacji kopiowania hello raz lub zgodnie z harmonogramem (co godzinę, codziennie, i tak dalej). Obie te opcje można dla szerokości hello łączników hello między lokalnymi, chmurze i lokalnej kopii pulpitu.

Operacji kopiowania jednorazowe umożliwia przenoszenie danych z docelowym tooa źródła tylko raz. Ma to zastosowanie toodata dowolnej wielkości i dowolnego obsługiwanego formatu. Witaj zaplanowanych kopii umożliwia toocopy danych na wyznaczonych cyklu. Można użyć zaawansowanych ustawień (np. Ponów próbę, limit czasu i alertami) tooconfigure hello zaplanowanych kopii.

![Planowanie właściwości](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a>Następne kroki
Przewodnik Szybki pomocą hello kreatora kopiowania fabryki danych toocreate potoku działanie kopiowania, zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania hello](data-factory-copy-data-wizard-tutorial.md).

