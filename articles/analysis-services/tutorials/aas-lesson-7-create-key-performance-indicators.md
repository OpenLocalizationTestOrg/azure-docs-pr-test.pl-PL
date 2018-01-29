---
title: "Samouczek Azure Analysis Services: lekcja 7 — tworzenie kluczowych wskaźników wydajności | Microsoft Docs"
description: "Opisuje sposób tworzenia kluczowych wskaźników wydajności w projekcie samouczka usług Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 01/08/2018
ms.author: owend
ms.openlocfilehash: 8f25773541deba2a94d3adc0c9b61c1b90a90aa6
ms.sourcegitcommit: 176c575aea7602682afd6214880aad0be6167c52
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/09/2018
---
# <a name="create-key-performance-indicators"></a>Tworzenie kluczowych wskaźników wydajności

W tej lekcji utworzysz kluczowe wskaźniki wydajności (KPI). Kluczowe wskaźniki wydajności służą do oceny wydajności wartości zdefiniowanej przy użyciu miary *Podstawowa* względem wartości *Docelowa*, również zdefiniowanej przez miarę lub wartość bezwzględną. Kluczowe wskaźniki wydajności zawarte w aplikacjach klienckich do raportowania umożliwiają specjalistom szybkie i łatwe wyświetlenie podsumowania działalności biznesowej firmy oraz identyfikację trendów. Aby dowiedzieć się więcej, zobacz temat [Kluczowe wskaźniki wydajności](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular).
  
Szacowany czas trwania lekcji: **15 minut**  
  
## <a name="prerequisites"></a>Wymagania wstępne  
Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności. Przed przystąpieniem do wykonywania zadań w tej lekcji należy ukończyć lekcję poprzednią: [Lekcja 6. Tworzenie miar](../tutorials/aas-lesson-6-create-measures.md).   
  
## <a name="create-key-performance-indicators"></a>Tworzenie kluczowych wskaźników wydajności  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a>Tworzenie wskaźnika KPI InternetCurrentQuarterSalesPerformance  
  
1.  W projektancie modeli kliknij tabelę **FactInternetSales**.  
  
2.  W siatce miar kliknij pustą komórkę.  
  
3.  Na pasku formuły powyżej tabeli wpisz następującą formułę: 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    Ta miara służy jako miara podstawowa kluczowego wskaźnika wydajności.  
  
4.  W siatce miar kliknij prawym przyciskiem myszy pozycje **InternetCurrentQuarterSalesPerformance** > **Utwórz wskaźnik KPI**.   
  
5.  W oknie dialogowym Kluczowy wskaźnik wydajności (KPI) w obszarze **Docelowa** wybierz opcję **Wartość bezwzględna**, a następnie wpisz wartość **1,1**.  
  
7.  W polu lewego suwaka (niższe wartości) wpisz **1**, a w polu prawego suwaka (wyższe wartości) wpisz wartość **1,07**.  
  
8.  W obszarze **Wybierz styl ikon** wybierz romb (czerwony), trójkąt (żółty), okrąg (zielony).
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > Zwróć uwagę na rozwijaną etykietę **Opisy** poniżej dostępnych stylów ikon. Dodaj opisy różnych elementów wskaźników KPI, aby ułatwić ich identyfikację w aplikacjach klienckich.  
  
9. Kliknij przycisk **OK**, aby zakończyć definiowanie kluczowego wskaźnika wydajności.  
  
    W siatce miar zwróć uwagę na ikonę znajdującą się obok miary **InternetCurrentQuarterSalesPerformance**. Ta ikona wskazuje, że dana miara służy jako wartość podstawowa dla kluczowego wskaźnika wydajności.  
  
#### <a name="to-create-an-internetcurrentquartermarginperformance-kpi"></a>Tworzenie wskaźnika KPI InternetCurrentQuarterMarginPerformance  
  
1.  W siatce miar tabeli **FactInternetSales** kliknij pustą komórkę.  
  
2.  Na pasku formuły powyżej tabeli wpisz następującą formułę:  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  Kliknij prawym przyciskiem myszy pozycje **InternetCurrentQuarterMarginPerformance** > **Utwórz wskaźnik KPI**.  
  
4.  W oknie dialogowym Kluczowy wskaźnik wydajności (KPI) w obszarze **Docelowa** wybierz opcję **Wartość bezwzględna**, a następnie wpisz wartość **1,25**.   
  
5.  Przesuwaj lewy suwak (niższe wartości) do momentu wyświetlenia wartości **0,8**, a następnie przesuwaj prawy suwak (wyższe wartości), aż zostanie wyświetlona wartość **1,03**.  
  
6.  W obszarze **Wybierz styl ikon** wybierz romb (czerwony), trójkąt (żółty), okrąg (zielony), a następnie kliknij przycisk **OK**.  
  
## <a name="whats-next"></a>Co dalej?
[Lekcja 8. Tworzenie perspektyw](../tutorials/aas-lesson-8-create-perspectives.md).
  
  
