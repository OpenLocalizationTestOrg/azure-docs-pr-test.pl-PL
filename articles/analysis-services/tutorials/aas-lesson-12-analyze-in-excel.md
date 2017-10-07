---
title: aaa "lekcji samouczka usług Azure Analysis Services 12: analizować w programie Excel | Opis elementu Microsoft Docs": w tym artykule opisano, jak toouse analizy w programie Excel w hello Azure Analysis Services projekt samouczka. usługi: documentationcenter usług analysis services: "Autor: minewiskan Menedżera: Edytor erikre:" tagów: "

MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="lesson-12-analyze-in-excel"></a>Lekcja 12. Analiza w programie Excel

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

W tej lekcji Użyj hello analizowanie w Excel tooopen funkcji programu Microsoft Excel, automatycznie Utwórz obszar roboczy modelu toohello połączenia i automatycznie dodać arkusz toohello tabeli przestawnej. Witaj analizy w programie Excel funkcji oznacza tooprovide skuteczności hello tootest szybka i łatwa metoda model projektowania wcześniejsze toodeploying modelu. Podczas tej lekcji nie wykonasz żadnej analizy danych. Celem tej lekcji Hello jest toofamiliarize, hello model tworzenia, narzędziami hello można użyć tootest projektowania modelu.   
  
toocomplete tej lekcji programu Excel należy zainstalować na powitania tym samym komputerze co program SSDT.
  
Szacowany czas toocomplete tej lekcji: **pięć minut**  
  
## <a name="prerequisites"></a>Wymagania wstępne  
Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności. Przed wykonaniem zadania hello w tej lekcji, powinno mieć ukończone poprzedniej lekcji hello: [lekcji 11: tworzenie ról](../tutorials/aas-lesson-11-create-roles.md).  
  
## <a name="browse-using-hello-default-and-internet-sales-perspectives"></a>Przeglądaj za pomocą perspektywy domyślnej i sprzedaży Internet hello  
W tych zadań pierwszego przeglądania modelu przy użyciu obu hello perspektywy domyślnej, która obejmuje wszystkie obiekty modelu, a także za pomocą perspektywy sprzedaży internetowej hello należy wcześniej. Witaj perspektywy sprzedaży internetowej wyklucza powitania klienta tabeli obiektów.  
  
#### <a name="toobrowse-by-using-hello-default-perspective"></a>toobrowse za pomocą perspektywy domyślnej hello  
  
1.  Kliknij przycisk hello **modelu** menu > **analizy w programie Excel**.  
  
2.  W hello **analizy w programie Excel** okno dialogowe, kliknij przycisk **OK**.  
  
    Zostanie otwarty nowy skoroszyt w programie Excel. Połączenie ze źródłem danych jest tworzony przy użyciu bieżącego konta użytkownika hello i hello perspektywy domyślnej jest używana toodefine pól możliwych do wyświetlenia. Tabela przestawna jest automatycznie dodawany arkusz toohello.  
  
3.  W programie Excel w hello **listy pól tabeli przestawnej**, powiadomienia hello **DimDate** i **FactInternetSales** grupy miar są wyświetlane. Witaj **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, i **FactInternetSales** tabel z odpowiednich kolumnach są również wyświetlane.  
  
4.  Zamknij program Excel bez zapisywania hello skoroszytu.  
  
#### <a name="toobrowse-by-using-hello-internet-sales-perspective"></a>toobrowse za pomocą perspektywy sprzedaży internetowej hello  
  
1.  Kliknij przycisk hello **modelu** menu, a następnie kliknij przycisk **analizy w programie Excel**.  
  
2.  W hello **analizy w programie Excel** okno dialogowe, pozostaw **bieżącego użytkownika systemu Windows** zaznaczone, następnie w hello **perspektywy** pole listy rozwijanej, wybierz opcję **sprzedaży Internet** , a następnie kliknij przycisk **OK**. 
    
    ![aas-lesson12-perspective](../tutorials/media/aas-lesson12-perspective.png)
    
3.  W programie Excel w **pól tabeli przestawnej**, zwróć uwagę, tabeli DimCustomer hello jest wykluczony z listy pól hello.  
    
    ![aas-lesson12-fields](../tutorials/media/aas-lesson12-fields.png)
    
4.  Zamknij program Excel bez zapisywania hello skoroszytu.  
  
## <a name="browse-by-using-roles"></a>Przeglądanie przy użyciu ról  
Role są ważnym elementem każdego modelu tabelarycznego. Bez co najmniej jedną rolę toowhich użytkownicy zostaną dodane jako członkowie, użytkownicy nie może uzyskać dostęp i analizować dane przy użyciu modelu. Witaj analizy w programie Excel funkcji umożliwia dla Ciebie tootest hello ról, które zostały zdefiniowane.  
  
#### <a name="toobrowse-by-using-hello-sales-manager-user-role"></a>toobrowse przy użyciu roli użytkownika Menedżer sprzedaży hello  
  
1.  Programu SSDT, kliknij przycisk hello **modelu** menu, a następnie kliknij przycisk **analizy w programie Excel**.  
  
2.  W **Określ hello użytkownika nazwę lub rolę toouse tooconnect toohello modelu**, wybierz pozycję **roli**, a następnie w polu listy rozwijanej hello, wybierz **Menedżer sprzedaży**, a następnie kliknij przycisk  **OK**.  
  
    Zostanie otwarty nowy skoroszyt w programie Excel. Automatycznie utworzona zostanie tabela przestawna. Witaj listy pól tabeli przestawnej obejmuje wszystkie pola danych hello dostępne w nowym modelu.  
      
3.  Zamknij program Excel bez zapisywania hello skoroszytu.  
  
## <a name="whats-next"></a>Co dalej?
Toohello Przejdź dalej lekcji: [lekcji 13: Wdrażanie](../tutorials/aas-lesson-13-deploy.md).

  
  
  
