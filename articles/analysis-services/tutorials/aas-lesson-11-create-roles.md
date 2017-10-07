---
title: aaa "lekcji samouczka usług Azure Analysis Services 11: tworzyć role | Opis elementu Microsoft Docs": w tym artykule opisano, jak toocreate ról w hello projekt samouczka usług Azure Analysis Services. usługi: documentationcenter usług analysis services: "Autor: minewiskan Menedżera: Edytor erikre:" tagów: "

MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="lesson-11-create-roles"></a>Lekcja 11. Tworzenie ról

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

W tej lekcji utworzysz role. Role zawierają modelu zabezpieczeń danych i obiektów bazy danych przez ograniczenie tooonly dostęp do tych użytkowników, którzy są członkami roli. Każda rola jest zdefiniowana z jednym uprawnieniem: Brak, Odczyt, Odczyt i przetwarzanie, Przetwarzanie lub Administrator. Role można zdefiniować podczas tworzenia modelu przy użyciu menedżera ról. Po wdrożeniu modelu rolami można zarządzać przy użyciu programu SQL Server Management Studio (SSMS). toolearn więcej, zobacz [ról](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).
  
> [!NOTE]  
> Tworzenie ról jest toocomplete nie jest konieczna w tym samouczku. Domyślnie konto hello, które są obecnie zalogowani przy użyciu ma uprawnienia administratora na powitania modelu. Jednak dla innych użytkowników w Twojej organizacji toobrowse przy użyciu klienta raportowania, należy utworzyć co najmniej jedną rolę z odczytu uprawnienia i Dodaj tych użytkowników jako elementy członkowskie.  
  
Utworzysz trzy role:  
  
-   **Kierownik** — ta rola może zawierać użytkowników w organizacji, dla której ma zostać toohave odczytu uprawnień tooall modelu obiektów i danych.  
  
-   **Analityk sprzedaży USA** — tej roli można dołączyć użytkowników w organizacji, dla którego chcesz tylko dane o stanie toobrowse toobe powiązane toosales w hello Stanów Zjednoczonych. Dla tej roli, możesz użyć toodefine formuły języka DAX *Filtr wierszy*, co ogranicza liczbę elementów członkowskich danych toobrowse tylko w przypadku hello Stanów Zjednoczonych.  
  
-   **Administrator** — ta rola może zawierać użytkowników, dla których mają uprawnienia administratora toohave, dzięki czemu nieograniczonego dostępu i uprawnienia tooperform zadań administracyjnych na powitania bazy danych modelu.  
  
Ponieważ kont użytkowników i grup systemu Windows w Twojej organizacji są unikatowe, można dodać konta z toomembers Twojej organizacji. Jednak w tym samouczku, można również puste elementy członkowskie hello. Testowanie wpływu hello każdej roli w dalszej części lekcji 12: analizować w programie Excel.  
  
Szacowany czas toocomplete tej lekcji: **15 minut**  
  
## <a name="prerequisites"></a>Wymagania wstępne  
Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności. Przed wykonaniem zadania hello w tej lekcji, powinno mieć ukończone poprzedniej lekcji hello: [10 lekcji: tworzenie partycji](../tutorials/aas-lesson-10-create-partitions.md).  
  
## <a name="create-roles"></a>Tworzenie ról  
  
#### <a name="toocreate-a-sales-manager-user-role"></a>toocreate roli użytkownika Menedżer sprzedaży  
  
1.  W Eksploratorze modelu tabelarycznego kliknij prawym przyciskiem myszy pozycje **Role** > **Role**.  
  
2.  W Menedżerze ról kliknij przycisk **Nowa**.  
  
3.  Kliknij hello nową rolę, a następnie w hello **nazwa** kolumny, Zmień nazwę roli hello zbyt**Menedżer sprzedaży**.  
  
4.  W hello **uprawnienia** kolumny, kliknij listę rozwijaną hello, a następnie wybierz hello **odczytu** uprawnienia. 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  Opcjonalnie: Kliknij hello **członków** , a następnie kliknij pozycję **Dodaj**. W hello **Wybieranie użytkowników lub grup** okna dialogowego wprowadź użytkowników systemu Windows hello lub grup z Twojej organizacji mają tooinclude hello roli.  
  
#### <a name="toocreate-a-sales-analyst-us-user-role"></a>toocreate rolę użytkownika Analityk sprzedaży stany USA  
  
1.  W Menedżerze ról kliknij przycisk **Nowa**.    
  
2.  Zmień nazwę roli hello zbyt**analityka sprzedaży USA**.  
  
3.  Nadaj tej roli uprawnienie **Odczyt**.  
  
4.  Kliknij kartę filtrów wierszy hello, a następnie hello **DimGeography** tabeli, kolumny filtru DAX hello, hello typu następującej formuły:  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    Filtr wierszy A formuła musi rozpoznać tooa wartość logiczna (PRAWDA/FAŁSZ). Tą formułą jest określenie, czy użytkownik toohello widoczne tylko wiersze z hello wartość numer kierunkowy kraju Region "PL".  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  Opcjonalnie: Kliknij hello **członków** , a następnie kliknij pozycję **Dodaj**. W hello **Wybieranie użytkowników lub grup** okna dialogowego wprowadź użytkowników systemu Windows hello lub grup z Twojej organizacji mają tooinclude hello roli.  
  
#### <a name="toocreate-an-administrator-user-role"></a>toocreate roli użytkownika Administrator  
  
1.  Kliknij przycisk **Nowy**.  
  
2.  Zmień nazwę roli hello zbyt**administratora**.  
  
3.  Nadaj tej roli uprawnienie **Administrator**.  
  
4.  Opcjonalnie: Kliknij hello **członków** , a następnie kliknij pozycję **Dodaj**. W hello **Wybieranie użytkowników lub grup** okna dialogowego wprowadź użytkowników systemu Windows hello lub grup z Twojej organizacji mają tooinclude hello roli. 
  
  
## <a name="whats-next"></a>Co dalej?
[Lekcja 12. Analiza w programie Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).

  
  
