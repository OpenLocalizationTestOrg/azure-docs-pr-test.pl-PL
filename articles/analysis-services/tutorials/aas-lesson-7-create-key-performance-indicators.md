---
title: aaa "lekcji samouczka usług Azure Analysis Services 7: tworzenie kluczowych wskaźników wydajności | Opis elementu Microsoft Docs": w tym artykule opisano, jak toocreate kluczowych wskaźników wydajności w hello projekt samouczka usług Azure Analysis Services. usługi: documentationcenter usług analysis services: "Autor: minewiskan Menedżera: Edytor erikre:" tagów: "

MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="lesson-7-create-key-performance-indicators"></a>Lekcja 7. Tworzenie kluczowych wskaźników wydajności

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

W tej lekcji utworzysz kluczowe wskaźniki wydajności (KPI). Kluczowe wskaźniki wydajności są używane toogauge wydajności z wartości zdefiniowanych przez *Base* miary, przed *docelowej* wartość również zdefiniowane przez miarę, lub wartość bezwzględna. W raportach aplikacji klienckich, wskaźników KPI może zapewnić specjaliści toounderstand szybkie i proste podsumowanie trendów powodzenie lub tooidentify biznesowych. toolearn więcej, zobacz [wskaźników KPI](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)
  
Szacowany czas toocomplete tej lekcji: **15 minut**  
  
## <a name="prerequisites"></a>Wymagania wstępne  
Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności. Przed wykonaniem zadania hello w tej lekcji, powinno mieć ukończone poprzedniej lekcji hello: [Lekcja 6: tworzenie miar](../tutorials/aas-lesson-6-create-measures.md).   
  
## <a name="create-key-performance-indicators"></a>Tworzenie kluczowych wskaźników wydajności  
  
#### <a name="toocreate-an-internetcurrentquartersalesperformance-kpi"></a>toocreate InternetCurrentQuarterSalesPerformance kluczowy wskaźnik wydajności  
  
1.  W Konstruktorze modelu powitania kliknij hello **FactInternetSales** tabeli.  
  
2.  W siatce miar hello kliknij przycisk pustej komórki.  
  
3.  Na pasku formuły hello, powyżej tabeli hello wpisz hello następującej formuły: 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    To jest miara służy jako hello miara podstawowa dla hello kluczowego wskaźnika wydajności.  
  
4.  Kliknij prawym przyciskiem myszy pozycje **InternetCurrentQuarterSalesPerformance** > **Utwórz wskaźnik KPI**.   
  
5.  W hello kluczowego wskaźnika wydajności (KPI) — okno dialogowe w **docelowej** wybierz **wartość bezwzględna**, a następnie wpisz **1.1**.  
  
7.  W polu po lewej stronie suwaka (niski) hello wpisz **1**, a następnie w hello suwak w prawo (wysoka) wpisz **1.07**.  
  
8.  W **wybierz styl ikony**wybierz hello romb (czerwony), trójkąt (żółty), koło typ ikony (zielony).
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > Powiadomienie hello rozwijania **opisy** etykiety poniżej hello ikona dostępne style. Użyj opisy dla hello różnych toomake elementów KPI ich więcej zidentyfikować w aplikacji klienta.  
  
9. Kliknij przycisk **OK** toocomplete hello kluczowego wskaźnika wydajności.  
  
    W siatce miar hello, zwróć uwagę hello ikona dalej toohello **InternetCurrentQuarterSalesPerformance** miary. Ta ikona wskazuje, że dana miara służy jako wartość podstawowa dla kluczowego wskaźnika wydajności.  
  
#### <a name="toocreate-an-internetcurrentquartermarginperformance-kpi"></a>toocreate InternetCurrentQuarterMarginPerformance kluczowy wskaźnik wydajności  
  
1.  W siatce miar hello hello **FactInternetSales** tabeli, kliknij przycisk pustej komórki.  
  
2.  Na pasku formuły hello, powyżej tabeli hello wpisz hello następującej formuły:  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  Kliknij prawym przyciskiem myszy pozycje **InternetCurrentQuarterMarginPerformance** > **Utwórz wskaźnik KPI**.  
  
4.  W hello kluczowego wskaźnika wydajności (KPI) — okno dialogowe w **docelowej** wybierz **wartość bezwzględna**, a następnie wpisz **1,25**.   
  
5.  Hello suwaka (niski) po lewej stronie pola, Przesuń do momentu wyświetlenia pola hello **0,8**, a następnie hello slajdów prawym przyciskiem myszy pole suwaka (wysoka) do momentu wyświetlenia pola hello **1,03**.  
  
6.  W **wybierz styl ikony**Wybierz romb hello (czerwony), trójkąt (żółty), typ ikony koła (zielony), a następnie kliknij przycisk **OK**.  
  
## <a name="whats-next"></a>Co dalej?
[Lekcja 8. Tworzenie perspektyw](../tutorials/aas-lesson-8-create-perspectives.md).
  
  
