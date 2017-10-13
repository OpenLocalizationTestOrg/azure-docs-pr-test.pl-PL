---
title: "Tworzenie biletu pomocy technicznej dotyczącej usługi SQL Data Warehouse | Microsoft Docs"
description: "Tworzenie biletu pomocy technicznej w usłudze Azure SQL Data Warehouse."
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
ms.openlocfilehash: 058ff1229acee5d03db7c0305c5565ae95a85758
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-create-a-support-ticket-for-sql-data-warehouse"></a>Tworzenie biletu pomocy technicznej dotyczącej usługi SQL Data Warehouse
Jeśli masz problemy z usługą SQL Data Warehouse, utwórz bilet pomocy technicznej, aby umożliwić naszemu zespołowi inżynierów udzielenie pomocy.

> [!NOTE] 
> Począwszy od 20.12.2016 r., sprawdzenie kondycji zasobów w witrynie Azure Portal nie jest dokładne. Pracujemy nad rozwiązaniem tego problemu. 


## <a name="create-a-support-ticket"></a>Tworzenie biletu pomocy technicznej
1. Otwórz witrynę [Azure Portal][Azure portal].
2. Na ekranie głównym kliknij kafelek **Pomoc i obsługa techniczna**.
   
    ![Pomoc i obsługa techniczna](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. W bloku Pomoc i obsługa techniczna kliknij opcję **Utwórz żądanie obsługi**.
   
    ![Nowe żądanie pomocy technicznej](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. Wybierz typ żądania w polu **Typ żądania**.
   
    ![Typ żądania](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > Domyślnie każdy serwer SQL (np. myserver.database.windows.net) ma **limit przydziału jednostek DTU** wynoszący 45 000. Ten limit przydziału jest po prostu limitem bezpieczeństwa. Możesz zwiększyć limit przydziału, tworząc bilet pomocy technicznej i wybierając pozycję *Limit przydziału* jako typ żądania. Aby obliczyć zapotrzebowanie na jednostki DTU, należy pomnożyć 7,5 przez łączną wymaganą liczbę jednostek [DWU][DWU]. Jeśli na przykład chcesz hostować dwie bazy danych z poziomem celu usługi DW6000 na jednym serwerze SQL, zażądaj limitu przydziału wynoszącego 90 000.  Aktualne użycie jednostek DTU możesz zobaczyć z poziomu bloku serwera SQL w portalu. Limit przydziału jednostek DTU obejmuje zarówno wstrzymane, jak i niewstrzymane bazy danych. 
   > 
   > 
5. W polu **Subskrypcja** wybierz subskrypcję obejmującą problematyczną bazę danych.
   
    ![Subskrypcja](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. Wybierz opcję **SQL Data Warehouse** jako zasób.
   
    ![Zasób](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. Wybierz odpowiedni [Plan pomocy technicznej platformy Azure][Azure support plan].
   
   * Pomoc techniczna związana z **rozliczeniami, limitami przydziałów i zarządzaniem subskrypcjami** jest dostępna na wszystkich poziomach pomocy technicznej.
   * **Naprawa w razie awarii** jest oferowana w ramach pomocy technicznej na poziomach [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] i [Premium][Premier]. Naprawa w razie awarii dotyczy problemów napotykanych przez klientów podczas korzystania z platformy Azure, jeśli istnieje uzasadnione podejrzenie, że problem leży po stronie firmy Microsoft.
   * **Wsparcie dla deweloperów** i **usługi doradcze** są dostępne na poziomach pomocy technicznej [Professional Direct][Professional Direct] i [Premium][Premier]. 
     
     Jeśli masz plan pomocy technicznej Premium, możesz zgłaszać problemy związane z usługą SQL Data Warehouse także w portalu [Microsoft Premier Online][Microsoft Premier online portal].  Zobacz temat [Plany pomocy technicznej platformy Azure][Azure support plan], aby dowiedzieć się więcej o różnych planach pomocy technicznej, ich zakresach, czasach reakcji, cenach itp.  Często zadawane pytania na temat pomocy technicznej platformy Azure można znaleźć w temacie [Pomoc techniczna platformy Azure — często zadawane pytania][Azure support FAQs].  
     
     ![Plan pomocy technicznej](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. Wybierz odpowiednie wartości w polach **Typ problemu** i **Kategoria**. W tym przykładzie wybraliśmy typ problemu „Narzędzia” oraz kategorię „Narzędzia klienta”. 
   
    ![Typ problemu i kategoria](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. Opisz problem i wybierz poziom jego wpływu na prowadzoną działalność.
   
    ![Opis problemu](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. Twoje **informacje kontaktowe** dotyczące tego biletu pomocy technicznej zostaną wstępnie wypełnione. Zaktualizuj je w razie potrzeby.
    
    ![Informacje kontaktowe](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. Kliknij przycisk **Utwórz**, aby przesłać żądanie pomocy technicznej.

## <a name="monitor-a-support-ticket"></a>Monitorowanie biletu pomocy technicznej
Po przesłaniu żądania pomocy technicznej zespół pomocy technicznej platformy Azure skontaktuje się z Tobą. Aby sprawdzić stan żądania i szczegółowe informacje, kliknij opcję **Zarządzaj żądaniami obsługi** na pulpicie nawigacyjnym.

![Sprawdzanie stanu](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a>Inne zasoby
Ponadto można nawiązać kontakt ze społecznością usługi SQL Data Warehouse w witrynie [Stack Overflow][Stack Overflow] lub na [forum MSDN dotyczącym usługi Azure SQL Data Warehouse][Azure SQL Data Warehouse MSDN forum].

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

