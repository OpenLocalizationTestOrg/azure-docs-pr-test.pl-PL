---
title: scenariusze aaaIdentify i Planowanie procesu analytics - Azure | Dokumentacja firmy Microsoft
description: "Planowanie zaawansowana analityka przy uwzględnieniu szereg pytań klucza."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 421520dd-7728-4d29-889c-ebe6a0a6fb07
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: e445973be0d020a4f9949e5c9d8554fbbd4b515f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooidentify-scenarios-and-plan-for-advanced-analytics-data-processing"></a>Jak tooidentify scenariuszy i planowanie zaawansowane analizy przetwarzania danych
Jakie zasoby powinny planujesz tooinclude podczas konfigurowania środowiska toodo zaawansowane analizy przetwarzania na zestaw danych? W tym artykule sugeruje szereg pytań tooask, która pomoże zidentyfikować zadania hello i odpowiednie zasoby danego scenariusza. kolejność Hello wysokiego poziomu kroków analizy predykcyjnej jest opisane w temacie [co to jest hello zespołu danych nauki procesu (TDSP)?](data-science-process-overview.md). Każda z tych czynności będzie wymagać określonych zasobów dla danego scenariusza tooyour odpowiednich zadań hello. Witaj ważne pytania tooidentify Twojego scenariusza dotyczą danych logistyki, właściwości, jakości hello hello zestawów danych i hello narzędzi i języków wolisz toodo hello analizy.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="logistic-questions-data-locations-and-movement"></a>Pytania logistyczna: lokalizacje danych i przepływu
Hello logistyczna pytania dotyczą hello lokalizację hello **źródła danych**, hello **docelowej** platformy Azure i wymagania dotyczące przenoszenia danych hello, w tym hello harmonogramu, wielkość i zasobów zaangażowany. Witaj danych może być konieczne toobe przenieść kilka razy podczas procesu analytics hello. Typowy scenariusz obejmuje toomove danych lokalnych do jakiegoś miejsca w magazynie Azure, a następnie do usługi Machine Learning Studio.

1. **Co to jest źródło danych?** Jest lokalnym lub w chmurze hello? Na przykład:
   
   * dane Hello jest publicznie dostępna pod adresem HTTP.
   * Witaj dane znajdują się w lokalizacji pliku sieć lokalna.
   * dane Hello znajdują się w bazie danych programu SQL Server.
   * Witaj dane są przechowywane w kontenerze magazynu Azure
2. **Co to jest hello Azure docelowego?** Gdy wymagana toobe przetwarzania lub modelowania? Na przykład:
   
   * Azure Blob Storage
   * Baz danych SQL Azure
   * Program SQL Server na maszynie wirtualnej platformy Azure
   * HDInsight (Hadoop na platformie Azure) lub tabele programu Hive
   * Azure Machine Learning
   * Instalację Azure wirtualnych dysków twardych.
3. **Jak będą toomove hello danych?**  hello procedury i zasoby dostępne tooingest lub załadować danych do różnych innego magazynu i środowisk przetwarzania są opisane w hello następujące tematy.
   
   * [Ładowanie danych do środowiska magazynu dla analityka](machine-learning-data-science-ingest-data.md)
   * [Importowanie danych szkoleniowych w usłudze Azure Machine Learning Studio z różnych źródeł danych](machine-learning-data-science-import-data.md).
4. **Czy dane hello muszą toobe przeniesiony zgodnie z ustalonym harmonogramem lub zmodyfikować w trakcie migracji?** Należy wziąć pod uwagę przy użyciu fabryki danych Azure (ADF) podczas toobe potrzeb danych stale migracji, zwłaszcza w wypadku scenariusza hybrydowego, który uzyskuje dostęp do swoich lokalnych uczestniczy zasobów w chmurze i po danych hello jest nietransakcyjnego lub musi toobe zmodyfikowany lub mieć logiki biznesowej dodaje tooit w toku hello migrowane. Aby uzyskać więcej informacji, zobacz [przenoszenia danych z lokalnego tooSQL serwera SQL Azure z fabryką danych Azure](machine-learning-data-science-move-sql-azure-adf.md)
5. **Ile danych hello jest tooAzure toobe przenieść?** Są bardzo dużych zestawów danych może przekroczyć hello pojemności niektórych środowiskach. Na przykład Zobacz Omówienie hello limity rozmiaru dla usługi Machine Learning Studio w następnej sekcji hello. W takich przypadkach próbkę danych hello może być używany podczas analizy hello. Szczegółowe jak toodown próbki zestawu danych w różnych środowiskach Azure można znaleźć [przykładowe dane w hello proces nauki danych zespołu](machine-learning-data-science-sample-data.md).

## <a name="data-characteristics-questions-type-format-and-size"></a>Pytania dotyczące danych właściwości: typ, format i rozmiar
Pytania te są tooplanning klucza magazynu i przetwarzania środowiskach, które są odpowiednie toovarious typów danych, a każdy z nich ma pewne ograniczenia.

1. **Co to są typy danych hello?** Na przykład:
   
   * Wartości liczbowych
   * Podzielone na kategorie
   * Ciągi
   * Binarne
2. **Sposób formatowania danych?** Na przykład:
   
   * Rozdzielana przecinkami (CSV) lub tabulatorami (TSV) plików prostych
   * Skompresowane lub nieskompresowane
   * Obiekty BLOB platformy Azure
   * Tabele programu Hive usługi Hadoop
   * Tabel programu SQL Server
3. **Jak duże jest danych?**
   
   * Mała liczba godzin: mniej niż 2GB
   * Średnia liczba godzin: Większa niż 2GB i mniejsza niż 10GB
   * Duże: Ponad 10GB

Na przykład wykonać hello Azure Machine Learning Studio środowiska:

* Listę formatów danych hello i typów obsługiwanych w usłudze Azure Machine Learning Studio, zobacz [danych formaty i typy danych obsługiwane](machine-learning-data-science-import-data.md#data-formats-and-data-types-supported) sekcji.
* Informacje w danych ograniczenia dotyczące usługi Azure Machine Learning Studio, zobacz hello **jak duży może hello być zestaw danych dla moich modułów?** sekcji [importowanie i eksportowanie danych na potrzeby uczenia maszynowego](machine-learning-faq.md#machine-learning-studio-questions)

Uzyskać informacji na temat ograniczeń hello z innymi usługami Azure, używane w procesie analytics hello, zobacz [subskrypcji platformy Azure i ograniczenia usługi, przydziały i ograniczenia](../azure-subscription-service-limits.md).

## <a name="data-quality-questions-exploration-and-pre-processing"></a>Pytania dotyczące jakości danych: eksploracji i przetwarzania wstępnego
1. **Co należy wiedzieć o danych?** Eksplorowanie danych gdy będziesz potrzebować toogain omówienie ich podstawowymi charakterystykami. Co wzorce lub trendów go dowody, co to jest wartości odstających lub brak wartości liczby. Ten krok jest ważne w przypadku określania zakresu hello przetwarzanie wstępne potrzebnych formułowania hipotez, które może sugerować hello najbardziej odpowiednie funkcje lub wpisz analizy i opracowywania planów zbierania dodatkowych danych. Obliczanie statystyki opisowe i kreślenia wizualizacje są przydatne techniki danych inspekcji. Aby uzyskać więcej informacji o tooexplore zestawu danych w różnych środowiskach Azure, zobacz temat [Eksplorowanie danych hello proces nauki danych zespołu](machine-learning-data-science-explore-data.md).
2. **Witaj danych wymaga wstępne przetworzenie lub czyszczenie?**
   Przetwarzanie wstępne i czyszczenia danych są ważne zadania, które zwykle należy przeprowadzić przed zestawu danych można skutecznie uczenia maszynowego. Dane pierwotne jest często zakłócenia i zawodnych i może brakować wartości. Przy użyciu tych danych do modelowania może wygenerować błędne wyniki. Aby uzyskać opis, zobacz [tooprepare danych do uczenia maszynowego rozszerzone zadań](machine-learning-data-science-prepare-data.md).

## <a name="tools-and-languages-questions"></a>Narzędzia i języki pytania
Istnieje wiele opcji w zależności od jakich języków i środowisk deweloperskich lub narzędzia konieczne lub są najbardziej conformable przy użyciu.

1. **Co języków czy preferować toouse analizy?**  
   
   * R
   * Python
   * SQL
2. **Jakie narzędzia należy używać do analizy danych?**
   
   * [Microsoft Azure Powershell](/powershell/azure/overview) -język skryptów używane tooadminister zasobów platformy Azure w język skryptów.
   * [Usługa Azure Machine Learning Studio](machine-learning-what-is-ml-studio.md)
   * [Obrót analityka](http://www.revolutionanalytics.com/revolution-r-open)
   * [Programu RStudio](http://www.rstudio.com)
   * [Python Tools for Visual Studio](http://microsoft.github.io/PTVS/)
   * [Anaconda](https://www.continuum.io/why-anaconda)
   * [Notesy Jupyter](http://jupyter.org/)
   * [Microsoft Power BI](http://powerbi.microsoft.com)

## <a name="identify-your-advanced-analytics-scenario"></a>Zidentyfikuj scenariusz zaawansowana analityka
Po ma odpowiedzi na pytania hello w poprzedniej sekcji hello jest gotowy toodetermine scenariusza najlepiej pasuje do sprawę. Witaj przykładowe scenariusze są opisane w temacie [scenariusze zaawansowana analityka w usłudze Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md).

