---
title: "aaaAuditing w usłudze Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do inspekcji w usłudze Azure SQL Data Warehouse"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 0e6af148-b218-4b43-bb5f-907917d20330
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 08/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 948de74fa052ef206cf1aa65c0d81f084b18cb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a>Inspekcja w magazynie danych Azure SQL
> [!div class="op_single_selector"]
> * [Inspekcja](sql-data-warehouse-auditing-overview.md)
> * [Wykrywanie zagrożeń](sql-data-warehouse-security-threat-detection.md)
> 
> 

Inspekcja SQL Data Warehouse pozwala toorecord zdarzenia w dzienniku inspekcji tooan bazy danych na koncie magazynu Azure. Inspekcja pomaga zachować zgodność z przepisami, analizować aktywność bazy danych oraz uzyskać wgląd w odchylenia i anomalie, które mogą oznaczać problemy biznesowe lub podejrzane naruszenia zabezpieczeń. Inspekcja SQL Data Warehouse integruje się również z usługi Microsoft Power BI do przechodzenia raportowania i analiz.

Narzędzia inspekcji Włącz i ułatwienia standardów toocompliance zgodność, ale nie zagwarantuje zgodności. Aby uzyskać więcej informacji na temat usługi Azure programy tego zgodność ze standardami pomocy technicznej, zobacz hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Centrum zaufania Azure</a>.

* [Podstawowe informacje dotyczące bazy danych inspekcji]
* [Inspekcja bazy danych]
* [Analizowanie dzienników inspekcji i raportów]

## <a id="subheading-1"></a>Podstawy inspekcja bazy danych magazynu danych SQL Azure
Inspekcja bazy danych SQL Data Warehouse umożliwia:

* **Zachowaj** dziennik inspekcji wybranych zdarzeń. Można zdefiniować rodzaje toobe działania bazy danych inspekcji.
* **Raport** na działanie bazy danych. Można użyć wstępnie skonfigurowane raporty i tooget pulpitu nawigacyjnego, szybkie wprowadzenie aktywności i raportowanie zdarzeń.
* **Analizowanie** raportów. Można znaleźć podejrzane zdarzenia, nietypowe działania i trendów.

Można skonfigurować inspekcję hello następujących kategorii:

**Zwykły SQL** i **sparametryzowana SQL** dla których hello dzienników inspekcji zbierane są sklasyfikowane jako  

* **Toodata dostępu**
* **Zmiany schematu (DDL)**
* **Zmiany danych (DML)**
* **Konta, role i uprawnienia (DCL)**
* **Procedura składowana**, **logowania** i **zarządzania transakcji**.

Dla każdej kategorii zdarzenia inspekcji z **Powodzenie** i **błąd** operacje nie zostały skonfigurowane osobno.

Aby uzyskać więcej informacji na temat hello działań i zdarzeń inspekcji, zobacz hello <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">odwołanie do formatu dziennika inspekcji (Pobieranie pliku doc)</a>.

Dzienniki inspekcji są przechowywane na koncie magazynu Azure. Można zdefiniować okres przechowywania dziennika inspekcji.

Zasady inspekcji mogą być definiowane dla określonej bazy danych lub jako domyślne zasady serwera. Domyślne zasady inspekcji serwera stosuje tooall baz danych na serwerze, które nie mają określonej bazy danych inspekcji zasad zdefiniowane.

Przed przystąpieniem do ustawiania inspekcji inspekcji wyboru, jeśli używasz ["Klientów niższych poziomów."](sql-data-warehouse-auditing-downlevel-clients.md)

## <a id="subheading-2"></a>Inspekcja bazy danych
1. Uruchamianie hello <a href="https://portal.azure.com" target="_blank">portalu Azure</a>.
2. Przejdź toohello **ustawienia** bloku hello ma tooaudit usługi SQL Data Warehouse. W hello **ustawienia** bloku, wybierz opcję **Inspekcja i wykrywanie zagrożeń**.
   
    ![][1]
3. Należy również włączyć inspekcję, klikając hello **ON** przycisku.
   
    ![][3]
4. Hello inspekcji blok konfiguracji, wybierz **szczegóły MAGAZYNU** tooopen hello magazynu dzienniki inspekcji bloku. Wybierz hello kontem magazynu platformy Azure, w którym zostanie zapisany dzienniki i hello okresu przechowywania. 
>[!TIP]
>Witaj Użyj tego samego konta magazynu dla wszystkich baz danych inspekcji hello tooget wykorzystanie hello wstępnie skonfigurowane raporty szablonów.
   
    ![][4]
5. Kliknij przycisk hello **OK** przycisk toosave hello magazynu szczegóły konfiguracji.
6. W obszarze **rejestrowanie przez zdarzenie**, kliknij przycisk **Powodzenie** i **błąd** toolog wszystkie zdarzenia, lub wybierz kategorie poszczególnych zdarzeń.
7. W przypadku konfigurowania inspekcji bazy danych, może być konieczne parametry połączenia hello tooalter Twojego tooensure klienta, który prawidłowo przechwycone dane inspekcji. Sprawdź hello [zmodyfikować FDQN serwera w parametrach połączenia hello](sql-data-warehouse-auditing-downlevel-clients.md) tematu dla połączeń klientów niższych poziomów.
8. Kliknij przycisk **OK**.

## <a id="subheading-3"></a>Analizowanie dzienników inspekcji i raportów
Dzienniki inspekcji są agregowane w zbiorze magazynu tabel z **SQLDBAuditLogs** prefiks w hello wybrana w Instalatorze kontem magazynu platformy Azure. Można wyświetlić przy użyciu narzędzia, takie jak pliki dziennika <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Eksploratora usługi Storage Azure</a>.

Szablon raportu dotyczącego wstępnie skonfigurowane pulpit nawigacyjny jest dostępny jako <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">arkusz kalkulacyjny programu Excel do pobrania</a> toohelp szybko analizować dane dzienników. toouse hello szablonu w dziennikach inspekcji, potrzebujesz programu Excel 2013 lub nowszy i dodatku Power Query, który można pobrać <a href="http://www.microsoft.com/download/details.aspx?id=39379">tutaj</a>.

Witaj szablonu w nim fikcyjnej przykładowych danych, i służą do tworzenia dodatku Power Query tooimport dziennik inspekcji bezpośrednio z kontem magazynu platformy Azure.

## <a id="subheading-4"></a>Ponowne generowanie klucza magazynu
W środowisku produkcyjnym jest prawdopodobnie toorefresh Twojego magazynu kluczy okresowo. Podczas odświeżania kluczy, należy toosave hello zasad. Witaj proces przebiega następująco:

1. W hello inspekcji blok konfiguracji (opisane powyżej w Instalatorze hello inspekcji sekcji) Przełącz hello **klucz dostępu do magazynu** z *głównej* za*dodatkowej* i  **ZAPISZ**.

   ![][4]
2. Blok konfiguracji magazynu Przejdź toohello i **ponownie wygenerować** hello *podstawowy klucz dostępu*.
3. Przejdź wstecz toohello inspekcji bloku konfiguracji przełącznika hello **klucz dostępu do magazynu** z *dodatkowej* za*głównej* i naciśnij klawisz **ZAPISAĆ**.
4. Przejdź wstecz magazynu toohello interfejsu użytkownika i **ponownie wygenerować** hello *pomocniczy klucz dostępu* (jako przygotowanie hello klucze następnego odświeżenia cyklu.

## <a id="subheading-5"></a>Automatyzacja (programu PowerShell/REST API)
Można również skonfigurować inspekcji w usłudze Azure SQL Data Warehouse przy użyciu powitania po narzędziami automatyzacji:

* **Polecenia cmdlet programu PowerShell**:

   * [Get-AzureRMSqlDatabaseAuditingPolicy][101]
   * [Get-AzureRMSqlServerAuditingPolicy][102]
   * [Usuń AzureRMSqlDatabaseAuditing][103]
   * [Usuń AzureRMSqlServerAuditing][104]
   * [Zestaw AzureRMSqlDatabaseAuditingPolicy][105]
   * [Zestaw AzureRMSqlServerAuditingPolicy][106]
   * [Użyj AzureRMSqlServerAuditingPolicy][107]

<!--Anchors-->
[Podstawowe informacje dotyczące bazy danych inspekcji]: #subheading-1
[Inspekcja bazy danych]: #subheading-2
[Analizowanie dzienników inspekcji i raportów]: #subheading-3


<!--Image references-->
[1]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing.png
[2]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-inherit.png
[3]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-enable.png
[4]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-storage-account.png
[5]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-dashboard.png


<!--Link references-->
[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy