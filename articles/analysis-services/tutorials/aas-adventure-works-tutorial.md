---
title: "AAA \"usług Azure Analysis Services Adventure Works samouczek | Dokumentacja firmy Microsoft\""
description: "Wprowadza hello samouczek Adventure Works dla usług Azure Analysis Services"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: 2df8b3ab4e8c4ffbe0086418d60fd2e2abd35e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-analysis-services---adventure-works-tutorial"></a>Azure Analysis Services – samouczek Adventure Works

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Ten samouczek zawiera wnioski dotyczące toocreate i wdrażać za pomocą modelu tabelarycznego na poziomie zgodności hello 1400 [programu SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  

W przypadku nowych usług tooAnalysis i modelowanie tabelarycznych, wykonanie kroków tego samouczka jest hello najszybszy sposób toolearn jak toocreate i wdrożenie podstawowego modelu tabelarycznego. Po określeniu wymagań wstępnych hello w miejscu powinno ono mieć między dwoma toocomplete godziny toothree.  
  
## <a name="what-you-learn"></a>Omawiane zagadnienia   
  
-   Jak toocreate nowy model tabelaryczny projektu na powitania **poziom zgodności 1400** programu SSDT.
  
-   Jak tooimport dane z relacyjnej bazy danych w projekcie modelu tabelarycznego.  
  
-   Jak toocreate relacji między tabelami w modelu hello i zarządzanie nimi.  
  
-   Jak toocreate obliczeniowe kolumn, miar i kluczowych wskaźników wydajności, które pomagają użytkownikom analizowanie metryki krytycznym znaczeniu dla firmy.  
  
-   Jak toocreate i zarządzanie nimi perspektywy oraz hierarchii, które pomagają użytkownikom łatwiej przeglądać modelu danych przez podanie biznesowych i widoki specyficzne dla aplikacji.  
  
-   Jak partycje toocreate który do dzielenia tabeli danych na mniejsze części logiczne, które można przetwarzać niezależnie od innych partycji.  
  
-   Jak toosecure model obiektów i danych, tworząc role z elementami członkowskimi użytkownika.  
  
-   Jak toodeploy tooan modelu tabelarycznego **usług Azure Analysis Services** serwera lub lokalnego serwera usług Analysis Services programu SQL Server 2017 r.  
  
## <a name="prerequisites"></a>Wymagania wstępne  
toocomplete tego samouczka należy:  
  
-   Usług Azure Analysis Services lub SQL Server 2017 Analysis Services wystąpienia toodeploy do modelu. Zarejestruj się, aby uzyskać dostęp do [wersji próbnej usług Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) i [utworzyć serwer](../analysis-services-create-server.md). Możesz też zarejestrować się i pobrać serwer [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp). 

-   Magazyn danych serwera SQL Server lub magazyn danych SQL Azure z hello [AdventureWorksDW2014 przykładowej bazy danych](http://go.microsoft.com/fwlink/?LinkID=335807). Ta przykładowa baza danych zawiera toocomplete niezbędnych danych hello w tym samouczku. Pobierz [bezpłatne wersje serwera SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads). Możesz też zarejestrować się i uzyskać bezpłatną [wersję próbną bazy danych Azure SQL Database](https://azure.microsoft.com/services/sql-database/). 

    **Ważne:** Jeśli hello przykładowej bazy danych należy zainstalować na lokalnym serwerze SQL i wdrożenia serwera usług Azure Analysis Services tooan modelu, [bramy danych lokalnych](../analysis-services-gateway.md) jest wymagana.

-   Witaj najnowszą wersję [programu SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

-   Witaj najnowszą wersję [programu SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).    

-   Aplikacja kliencka, na przykład [Power BI Desktop](https://powerbi.microsoft.com/desktop/) lub program Excel. 

## <a name="scenario"></a>Scenariusz  
Ten samouczek jest oparty na fikcyjnej firmie Adventure Works Cycles. Firma Adventure Works jest duże, międzynarodowej firma produkcyjna, które tworzy i rozpowszechnia rowerów, części i akcesoria toocommercial rynkach w Ameryce Północnej, Europie i Azji. firmy Hello zostają 500 pracowników. Ponadto firma Adventure Works zatrudnia kilka regionalnych zespołów sprzedaży obsługujących poszczególne rynki. Twój projekt jest toocreate modelu tabelarycznego dla użytkowników sprzedaży i marketingu tooanalyze sprzedaży danych w bazie danych AdventureWorksDW hello w Internecie.  
  
Samouczek hello toocomplete, należy wykonać różne — lekcje. Każda lekcja obejmuje zadania do wykonania. Niezbędne kończenia lekcji hello jest wykonanie poszczególnych zadań w kolejności. Chociaż dana lekcja może obejmować kilka zadań, których wykonanie daje podobne wyniki, to sposób wykonania poszczególnych zadań może się nieco różnić. Ten pokazuje metoda jest często więcej niż jeden sposób toocomplete zadania i toochallenge można za pomocą umiejętności znasz z poprzednich — lekcje i zadania.  
  
Celem Hello lekcje hello jest tooguide użytkownika przez proces tworzenia podstawowego modelu tabelarycznego przy użyciu hello funkcje uwzględnione w program SSDT. Ponieważ każdy lekcji bazując na powitania poprzedniej lekcji, należy wykonać lekcje hello w kolejności.
  
W tym samouczku nie dostarcza wnioski dotyczące zarządzania serwerem w portalu Azure, zarządzanie serwera lub bazy danych przy użyciu narzędzia SSMS, lub za pomocą klienta aplikacji toobrowse modelu danych. 


## <a name="lessons"></a>Lekcje  
W tym samouczku opisano następujące lekcje hello:  
  
|Lekcja|Szacowany czas toocomplete|  
|----------|------------------------------|  
|[1. Tworzenie nowego projektu modelu tabelarycznego](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)|10 minut|  
|[2. Pobieranie danych](../tutorials/aas-lesson-2-get-data.md)|10 minut|  
|[3. Oznaczanie jako tabeli dat](../tutorials/aas-lesson-3-mark-as-date-table.md)|3 minuty|  
|[4. Tworzenie relacji](../tutorials/aas-lesson-4-create-relationships.md)|10 minut|  
|[5. Tworzenie kolumn obliczeniowych](../tutorials/aas-lesson-5-create-calculated-columns.md)|15 minut|
|[6. Tworzenie miar](../tutorials/aas-lesson-6-create-measures.md)|30 minut|  
|[7. Tworzenie kluczowych wskaźników wydajności (KPI)](../tutorials/aas-lesson-7-create-key-performance-indicators.md)|15 minut|  
|[8. Tworzenie perspektyw](../tutorials/aas-lesson-8-create-perspectives.md)|5 minut|  
|[9. Tworzenie hierarchii](../tutorials/aas-lesson-9-create-hierarchies.md)|20 minut|  
|[10. Tworzenie partycji](../tutorials/aas-lesson-10-create-partitions.md)|15 minut|  
|[11. Tworzenie ról](../tutorials/aas-lesson-11-create-roles.md)|15 minut|  
|[12. Analiza w programie Excel](../tutorials/aas-lesson-12-analyze-in-excel.md)|5 minut| 
|[13. Wdrażanie](../tutorials/aas-lesson-13-deploy.md)|5 minut|  
  
## <a name="supplemental-lessons"></a>Lekcje uzupełniające  
Że wnioski nie są wymagane toocomplete hello samouczek, ale mogą być pomocne w lepsze zaawansowanego modelu tabelarycznego opis tworzenia funkcji.  
  
|Lekcja|Szacowany czas toocomplete|  
|----------|------------------------------|  
|[Wiersze szczegółów](../tutorials/aas-supplemental-lesson-detail-rows.md)|10 minut|
|[Zabezpieczenia dynamiczne](../tutorials/aas-supplemental-lesson-dynamic-security.md)|30 minut|
|[Niewyrównane hierarchie](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)|20 minut| 

  
## <a name="next-steps"></a>Następne kroki  
Zobacz tooget pracę, [Lekcja 1: Tworzenie nowego projektu modelu tabelarycznego](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).  
  
  
  

