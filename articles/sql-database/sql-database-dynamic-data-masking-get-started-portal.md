---
title: 'Portalu Azure: maskowania danych dynamicznych bazy danych SQL | Dokumentacja firmy Microsoft'
description: "Sposób uruchamiania tooget z danymi dynamicznymi bazy danych SQL maskowania w hello portalu Azure"
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: "2"
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: ronitr; ronmat
ms.openlocfilehash: 5c5f74682a15d42eceb78c3ca0705401e1ac0ae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-hello-azure-portal"></a>Rozpoczynanie pracy z danymi dynamicznymi bazy danych SQL maskowania z hello portalu Azure

W tym temacie opisano sposób tooimplement [maskowania danych dynamicznych](sql-database-dynamic-data-masking-get-started.md) z hello portalu Azure. Można też wdrożyć przy użyciu maskowania danych dynamicznych [poleceń cmdlet usługi Azure SQL Database](https://msdn.microsoft.com/library/azure/mt574084.aspx) lub hello [interfejsu API REST](https://msdn.microsoft.com/library/dn505719.aspx).


## <a name="set-up-dynamic-data-masking-for-your-database-using-hello-azure-portal"></a>Konfigurowanie maskowania danych dynamicznych dla bazy danych przy użyciu hello portalu Azure
1. Uruchom hello portalu Azure pod adresem [https://portal.azure.com](https://portal.azure.com).
2. Przejdź bloku ustawienia toohello hello bazy danych, która zawiera hello poufne dane, które mają toomask.
3. Kliknij przycisk hello **dynamicznego maskowania danych** kafelka, który uruchamia hello **dynamicznego maskowania danych** blok konfiguracji.
   
   * Alternatywnie przewiń toohello **operacji** sekcji, a następnie kliknij przycisk **dynamicznego maskowania danych**.
     
     ![Okienko nawigacji](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. W hello **dynamicznego maskowania danych** który aparat zalecenia hello blok konfiguracji może zostać wyświetlony niektóre kolumny bazy danych ma flagę maskowania. W celu tooaccept hello zalecenia, kliknij **Dodaj maskę** do co najmniej jedną kolumnę i maski zostanie utworzony na podstawie na powitania domyślny typ dla tej kolumny. Możesz zmienić hello funkcji maskowania klikając hello reguła i edytowanie hello maskowania innym formacie tooa format pole wybranych przez użytkownika. Należy się tooclick **zapisać** toosave ustawień.
   
    ![Okienko nawigacji](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. tooadd maska dla każdej kolumny w bazie danych, u góry hello hello **dynamicznego maskowania danych** konfiguracji bloku, kliknij przycisk **Dodaj maskę** tooopen hello **Dodaj regułę maskowania** Blok konfiguracji
   
    ![Okienko nawigacji](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. Wybierz hello **schematu**, **tabeli** i **kolumny** toodefine Witaj wyznaczone pola, które maskowania.
7. Wybierz **Format maskowania pola** z listy hello kategorii maskowanie danych poufnych.
   
    ![Okienko nawigacji](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. Kliknij przycisk **zapisać** danych hello maskowania bloku tooupdate hello zestawu reguł maskowania reguły w hello dynamiczne maskowanie zasad danych.
9. Użytkownicy SQL hello typu lub tożsamości usługi AAD, które powinny być wykluczeni z maskowania i mają dostęp toohello pozbawione maskowania poufnych danych. Powinno to być rozdzielana średnikami lista użytkowników. Należy pamiętać, że użytkownicy z uprawnieniami administratora zawsze mają oryginalnych danych zamaskowana toohello dostępu.
   
    ![Okienko nawigacji](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > toomake tak hello warstwy aplikacji można wyświetlić danymi poufnymi w przypadku użytkowników aplikacji uprzywilejowane, Dodaj hello użytkownika SQL lub aplikacji hello tożsamości usługi AAD używa tooquery hello w bazie danych. Zdecydowanie zaleca się, że ta lista zawiera minimalnej liczbie użytkownicy o odpowiednich uprawnieniach toominimize ujawnianie danych wrażliwych hello.
   > 
   > 
10. Kliknij przycisk **zapisać** danych hello maskowania konfiguracji bloku toosave hello maskowania nowych lub zaktualizowanych zasad.


## <a name="next-steps"></a>Następne kroki

* Omówienie maskowania danych dynamicznych, zobacz [maskowania danych dynamicznych](sql-database-dynamic-data-masking-get-started.md).
* Można też wdrożyć przy użyciu maskowania danych dynamicznych [poleceń cmdlet usługi Azure SQL Database](https://msdn.microsoft.com/library/azure/mt574084.aspx) lub hello [interfejsu API REST](https://msdn.microsoft.com/library/dn505719.aspx).
