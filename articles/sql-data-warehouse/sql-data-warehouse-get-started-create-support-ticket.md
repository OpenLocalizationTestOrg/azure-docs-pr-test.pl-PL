---
title: "toocreate aaaHow biletu pomocy technicznej dla usługi SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Jak toocreate obsługi biletu w usłudze Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: a91d1f53-03cb-464b-9d5b-4a9c1a194ed3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 72f7eac82112fb7f1bfb05abca4ce40aeb3c828c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-support-ticket-for-sql-data-warehouse"></a>Jak toocreate obsługi biletu usługi SQL Data Warehouse
Jeśli masz problemy z usługą SQL Data Warehouse, utwórz bilet pomocy technicznej, aby umożliwić naszemu zespołowi inżynierów udzielenie pomocy.

> [!NOTE] 
> Począwszy od 12 20 2016-sprawdzenie kondycji zasobów hello w portalu Azure hello jest niedokładna. Obecnie pracujemy toofix ten problem. 


## <a name="create-a-support-ticket"></a>Tworzenie biletu pomocy technicznej
1. Otwórz hello [portalu Azure][Azure portal].
2. Na ekranie głównej powitania kliknij hello **Pomoc i obsługa techniczna** kafelka.
   
    ![Pomoc i obsługa techniczna](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. Na hello pomoc + Obsługa bloku, kliknij przycisk **Utwórz żądanie obsługi**.
   
    ![Nowe żądanie pomocy technicznej](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. Wybierz hello **żądania typu**.
   
    ![Typ żądania](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > Domyślnie każdy serwer SQL (np. myserver.database.windows.net) ma **limit przydziału jednostek DTU** wynoszący 45 000. Ten limit przydziału jest po prostu limitem bezpieczeństwa. Tworzenie biletu pomocy technicznej i wybierając można zwiększyć limitu przydziału *przydziału* jako typ żądania hello. toocalculate Twojego jednostek dtu w warstwie musi należy pomnożyć hello 7.5 przez hello całkowita [DWU] [ DWU] potrzebne. Na przykład chcesz toohost dwa DW6000s na jeden serwer SQL server, możesz zażądać limit przydziału jednostek DTU z 90,000.  Twoje bieżące użycie jednostek DTU z bloku serwera SQL hello można wyświetlić w portalu hello. Zarówno wstrzymana i cofanie wstrzymania bazy danych są wliczane do limitu przydziału jednostek dtu w warstwie hello. 
   > 
   > 
5. Wybierz hello **subskrypcji** czy hosty hello bazy danych z problemem hello są raportowania.
   
    ![Subskrypcja](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. Wybierz **SQL Data Warehouse** jako hello zasobów.
   
    ![Zasób](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. Wybierz odpowiedni [Plan pomocy technicznej platformy Azure][Azure support plan].
   
   * Pomoc techniczna związana z **rozliczeniami, limitami przydziałów i zarządzaniem subskrypcjami** jest dostępna na wszystkich poziomach pomocy technicznej.
   * **Naprawa w razie awarii** jest oferowana w ramach pomocy technicznej na poziomach [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] i [Premium][Premier]. Naprawa w razie awarii problemów są problemów napotykanych przez klientów podczas korzystania z usługi Azure w przypadku, gdy istnieje uzasadniona możliwość hello Microsoft spowodował problem.
   * **Wsparcie dla deweloperów** i **usługi doradcze** są dostępne pod adresem hello [Professional Direct] [ Professional Direct] i [Premier] [ Premier] poziomach pomocy technicznej. 
     
     Jeśli masz plan pomocy technicznej Premium, możesz zgłaszać także usługi SQL Data Warehouse problemy na powitania związane z [Microsoft Premier online portalu][Microsoft Premier online portal].  Zobacz [plany pomocy technicznej platformy Azure] [ Azure support plan] toolearn więcej informacji na temat hello obsługuje różne plany, ich zakresach, czasach reakcji, cenach, itp.  Często zadawane pytania na temat pomocy technicznej platformy Azure można znaleźć w temacie [Pomoc techniczna platformy Azure — często zadawane pytania][Azure support FAQs].  
     
     ![Plan pomocy technicznej](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. Wybierz hello **typ problemu** i **kategorii**. W tym przykładzie Wybraliśmy "Narzędzia" jako hello typ problemu i "klient" hello kategorii. 
   
    ![Typ problemu i kategoria](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. Opisz hello problem i wybierz poziom hello wpływ na prowadzoną działalność.
   
    ![Opis problemu](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. Twoje **informacje kontaktowe** dotyczące tego biletu pomocy technicznej zostaną wstępnie wypełnione. Zaktualizuj je w razie potrzeby.
    
    ![Informacje kontaktowe](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. Kliknij przycisk **Utwórz** toosubmit hello obsługi żądania.

## <a name="monitor-a-support-ticket"></a>Monitorowanie biletu pomocy technicznej
Gdy prześlesz żądanie pomocy technicznej hello hello zespołu pomocy technicznej platformy Azure skontaktuje się z Tobą. toocheck stan żądania i uzyskać więcej informacji, kliknij przycisk **Zarządzaj żądaniami obsługi** na powitania pulpitu nawigacyjnego.

![Sprawdzanie stanu](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a>Inne zasoby
Ponadto można połączyć z hello społeczności SQL Data Warehouse w [przepełnienie stosu] [ Stack Overflow] lub na powitania [forum MSDN magazynu danych SQL Azure] [ Azure SQL Data Warehouse MSDN forum].

<!--Image references--> 

<!--Article references--> 
[DWU]: ./sql-data-warehouse-overview-what-is.md

<!--MSDN references--> 

<!--Other web references--> 
[Azure portal]: https://portal.azure.com/
[Azure support plan]: https://azure.microsoft.com/support/plans/?WT.mc_id=Support_Plan_510979/  
[Developer]: https://azure.microsoft.com/support/plans/developer/  
[Standard]: https://azure.microsoft.com/support/plans/standard/  
[Professional Direct]: https://azure.microsoft.com/support/plans/prodirect/  
[Premier]: https://azure.microsoft.com/support/plans/premier/  
[Azure support FAQs]: https://azure.microsoft.com/support/faq/
[Microsoft Premier online portal]: https://premier.microsoft.com/
[Stack Overflow]: https://stackoverflow.com/questions/tagged/azure-sqldw/
[Azure SQL Data Warehouse MSDN forum]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse/

