---
title: "Witaj aaaUse widoku wykonania wierzchołka w narzędzi Data Lake Tools dla programu Visual Studio | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello zadania usługi Data Lake Analytics tooexam widoku wykonania wierzchołka."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5366d852-e7d6-44cf-a88c-e9f52f15f7df
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/13/2016
ms.author: jgao
ms.openlocfilehash: fb54d2af8a32aa27a54ff50a73c1b4903677a21e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a>Użyj widoku wykonania wierzchołka hello w narzędzi Data Lake Tools dla programu Visual Studio
Dowiedz się, jak toouse hello zadania usługi Data Lake Analytics tooexam widoku wykonania wierzchołka.

## <a name="prerequisites"></a>Wymagania wstępne

Należy podstawową wiedzę na temat przy użyciu narzędzi Data Lake Tools dla Visual Studio skryptu toodevelop U-SQL.  Zobacz [samouczek: tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).

## <a name="open-hello-vertex-execution-view"></a>Otwórz hello widoku wykonania wierzchołka
Otwórz zadania skryptu U-SQL w narzędzi Data Lake Tools dla programu Visual Studio. Kliknij przycisk **widoku wykonania wierzchołka** hello dole po lewej stronie ekranu. Zostanie wyświetlony monit o tooload profile może być najpierw i może potrwać pewien czas w zależności od połączenia sieciowego.

![Widoku wykonania wierzchołka narzędzi Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a>Zrozumienie widoku wykonania wierzchołka
Witaj, widoku wykonania wierzchołka ma trzy części:

![Widoku wykonania wierzchołka narzędzi Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

Witaj **selektora wierzchołków** na powitania po lewej stronie umożliwia wybrania wierzchołków przez funkcje (takie jak pierwszych 10 danych do odczytu, lub wybierz etapem). Jeden z filtrów najbardziej często używanych hello jest toosee hello **wierzchołków ścieżkę krytyczną**. Witaj **ścieżkę krytyczną** hello łańcuch najdłuższym wierzchołków zadania skryptu U-SQL. Ścieżkę krytyczną hello opis przydaje się do optymalizacji zadaniach sprawdzając, które wierzchołek ma najdłużej hello.
  
![Widoku wykonania wierzchołka narzędzi Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

Witaj górnej w okienku zostaną wyświetlone hello **bieżący stan wszystkich wierzchołków hello**.
  
![Widoku wykonania wierzchołka narzędzi Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

Witaj dołu w środkowym okienku przedstawia informacje o każdy wierzchołek:
* Nazwa procesu: Nazwa hello hello wierzchołków wystąpienia. Składa się z różnych części w Nazwa etapu | VertexName | VertexRunInstance. Na przykład wierzchołków [62] .v1 hello SV7_Split oznacza hello drugi działającego wystąpienia (.v1, indeksem rozpoczynającym się od 0) liczby wierzchołków 62 w SV7_Split etapu.
* Całkowita odczytu danych/Written: hello danych została odczytana/zapisana przez ten wierzchołka.
* Stan Stan/wyjścia: hello stan końcowy po zakończeniu hello wierzchołka.
* Typu wystąpił błąd i kodu zakończenia: błąd hello hello wierzchołków nie powiodło się.
* Tworzenie Przyczyna: Dlaczego wierzchołków hello został utworzony.
* Zasobów opóźnienia/procesu opóźnienia/NC kolejki opóźnienia: hello czas poświęcony na powitania wierzchołków toowait zasobów, tooprocess danych i toostay w kolejce hello.
* Identyfikator GUID procesu/Twórcy: Identyfikator GUID bieżącej wierzchołków uruchomionych hello lub twórcy.
* Wersja: hello N-ty percentyl wystąpienie hello systemem wierzchołków (hello systemu zaplanować nowych wystąpień wierzchołek dla wiele przyczyn, na przykład przejścia w tryb failover obliczeniowe nadmiarowość itp.)
* Utworzona wersja czasu.
* Utwórz początkowy czas i proces w kolejce czas i proces początkowy czas i proces Complete przetworzyć czasu: po uruchomieniu hello wierzchołków procesu tworzenia; podczas procesu wierzchołków hello uruchamiania tooqueue; gdy hello niektórych uruchamia proces wierzchołka; gdy hello niektórych wierzchołków zostanie ukończona.

## <a name="next-steps"></a>Następne kroki
* informacje diagnostyczne toolog, zobacz [uzyskiwanie dostępu do dzienników diagnostycznych dla usługi Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)
* toosee bardziej złożonego zapytania, zobacz [witryny sieci Web analizowanie dzienników przy użyciu usługi Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).
* Zobacz szczegóły zadania tooview, [użyj przeglądarki zadania i widok zadań dla zadania usługi Azure Data lake Analytics](data-lake-analytics-data-lake-tools-view-jobs.md)
