---
title: aaaConnect Excel tooSQL bazy danych | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooconnect programu Microsoft Excel tooAzure SQL bazy danych w chmurze hello. Importowanie danych do programu Excel, raportowanie i eksploracja danych."
services: sql-database
keywords: "Łączenie programu excel toosql, zaimportuj tooexcel danych"
documentationcenter: 
author: joseidz
manager: jhubbard
editor: 
ms.assetid: 906924bc-2707-48d3-bac6-397976a0409d
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: jhubbard
ms.openlocfilehash: 0048849432023145bd1009d45b6d9b64a9c7ac3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-tooan-azure-sql-database-and-create-a-report"></a>Połączenia bazy danych Azure SQL tooan programu Excel i tworzenie raportu

Połącz Excel tooa SQL database w chmurze hello i importowanie danych i tworzenie tabel i wykresów na podstawie wartości w bazie danych hello. W tym samouczku skonfigurujesz połączenie hello pomiędzy programami Excel i tabelą bazy danych Zapisz plik hello, która przechowuje dane i hello informacje o połączeniu dla programu Excel, a następnie utworzysz wykres przestawny z hello wartościami bazy danych.

Przed rozpoczęciem pracy będziesz potrzebować bazy danych SQL na platformie Azure. Jeśli nie masz, zobacz [utworzyć pierwszą bazę danych SQL](sql-database-get-started-portal.md) tooget bazy danych z przykładowymi danymi do pracy w ciągu kilku minut. W tym artykule będzie importować przykładowe dane do programu Excel z tego artykułu, ale można wykonać podobne kroki z użyciem własnych danych.

Potrzebna będzie również kopia programu Excel. W tym artykule wykorzystano program [Microsoft Excel 2016](https://products.office.com/).

## <a name="connect-excel-tooa-sql-database-and-create-an-odc-file"></a>Łączenie bazy danych SQL tooa programu Excel i tworzenie pliku odc
1. bazy danych tooSQL programu Excel tooconnect, Otwórz program Excel, a następnie utwórz nowy skoroszyt lub Otwórz istniejący skoroszyt programu Excel.
2. Na pasku menu hello u góry strony hello powitania kliknij **danych**, kliknij przycisk **z innych źródeł**, a następnie kliknij przycisk **z programu SQL Server**.
   
   ![Wybierz źródło danych: Połącz program Excel tooSQL w bazie danych.](./media/sql-database-connect-excel/excel_data_source.png)
   
   zostanie otwarty Kreator połączenia danych Hello.
3. W hello **połączyć tooDatabase serwera** okno dialogowe, hello typu bazy danych SQL **nazwy serwera** tooconnect tooin hello formularz <*servername* > **. database.windows.net**. Na przykład **adworkserver.database.windows.net**.
4. W obszarze **poświadczenia logowania**, kliknij przycisk **hello użyj następującej nazwy użytkownika i hasła**, typ hello **nazwy użytkownika** i **hasło** ustawione dla Witaj bazy danych programu SQL server podczas jego tworzenia, a następnie kliknij przycisk **dalej**.
   
   ![Wpisz powitania serwera nazwę i poświadczenia logowania](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > W zależności od środowiska sieciowego może być możliwe tooconnect lub jeśli hello bazy danych programu SQL server nie zezwala na ruch z adresu IP klienta może spowodować utratę połączenia hello. Przejdź toohello [portalu Azure](https://portal.azure.com/), kliknij serwery SQL, kliknij serwer, kliknij ikonę Zapora w ustawieniach i Dodaj swój adres IP klienta. Zobacz [jak ustawienia zapory tooconfigure](sql-database-configure-firewall-settings.md) szczegółowe informacje.
   > 
   > 
5. W hello **wybierz bazę danych i tabeli** okno dialogowe, wybierz hello bazy danych, mają toowork z z listy hello, a następnie kliknij hello tabele lub widoki mają toowork z (Wybraliśmy **vGetAllCategories**), a następnie Kliknij przycisk **dalej**.
   
    ![Wybierz bazę danych i tabelę.](./media/sql-database-connect-excel/select-database-and-table.png)
   
    Witaj **zapisywanie pliku połączenia danych i kończenie** zostanie wyświetlone okno dialogowe, w którym należy podać informacje o pliku połączenia (*.odc) bazy danych pakietu Office hello, który korzysta z programu Excel. Można pozostawić wartości domyślne hello lub dostosować ustawienia.
6. Możesz pozostawić domyślne hello, ale hello Uwaga **nazwę pliku** w szczególności. A **opis**, **przyjazną nazwę**, i **słowa kluczowe do wyszukania** ułatwiają i innym użytkownikom, co w przypadku podłączania tooand odnaleźć hello połączenia. Kliknij przycisk **zawsze podejmować toouse te dane toorefresh pliku** Jeśli chcesz, aby przechowywane w pliku odc hello, więc można zaktualizować, gdy połączenie tooit, a następnie kliknij przycisk informacje o połączeniu **Zakończ**.
   
    ![Zapisywanie pliku odc](./media/sql-database-connect-excel/save-odc-file.png)
   
    Witaj **importowania danych** zostanie wyświetlone okno dialogowe.

## <a name="import-hello-data-into-excel-and-create-a-pivot-chart"></a>Importowanie danych hello do programu Excel i tworzenie wykresu przestawnego
Teraz, gdy zostaną utworzone połączenie hello i hello utworzony plik z danych oraz informacje o połączeniu, czytasz tooimport hello danych.

1. W hello **i zaimportuj dane** okna dialogowego, kliknij hello opcję prezentacji danych w arkuszu hello, a następnie kliknij przycisk **OK**. Wybrano **Wykres przestawny**. Możesz również toocreate **nowy arkusz** lub zbyt**Dodaj ten tooa danych modelu danych**. Więcej informacji o modelach danych można znaleźć w temacie [Tworzenie modelu danych w programie Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B). Kliknij przycisk **właściwości** tooexplore informacji na temat hello pliku odc utworzone w hello poprzedniego kroku i toochoose opcje odświeżania danych hello.
   
    ![Wybieranie formatu hello danych w programie Excel](./media/sql-database-connect-excel/import-data.png)
   
    Witaj arkusz zawiera teraz pustą tabelę przestawną i wykres.
2. W obszarze **pól tabeli przestawnej**, wybierz hello wszystkich pól wyboru dla hello pola mają tooview.
   
    ![Skonfiguruj raport bazy danych.](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> Tooconnect innych Excel skoroszyty i arkusze toohello bazy danych, kliknij przycisk **danych**, kliknij przycisk **połączeń**, kliknij przycisk **Dodaj**, wybierz utworzone połączenie hello z listy hello, a następnie kliknij przycisk **Otwórz**.
> ![Otwieranie połączenia z innego skoroszytu](./media/sql-database-connect-excel/open-from-another-workbook.png)
> 
> 

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[uzyskuj tooSQL bazy danych programu SQL Server Management Studio](sql-database-connect-query-ssms.md) zaawansowane zapytania i analizy.
* Więcej informacji na temat zalet hello [pule elastyczne](sql-database-elastic-pool.md).
* Dowiedz się, jak za[tworzenia aplikacji sieci web, łączącego tooSQL bazy danych na powitania zaplecza](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).

