---
title: "aaaManage usług Azure Analysis Services przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Zarządzanie Azure Analysis Services przy użyciu programu PowerShell."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: owend
ms.openlocfilehash: bc4250bf77b5a0d86c1049ee57493bcf2a1f0c1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-analysis-services-with-powershell"></a>Zarządzanie usług Azure Analysis Services przy użyciu programu PowerShell

W tym artykule opisano zadania programu PowerShell polecenia cmdlet używane tooperform usług Azure Analysis Services serwera i bazy danych zarządzania. 

Zadania zarządzania serwerem, takie jak tworzenie lub usuwanie serwera, wstrzymywania lub wznawiania operacji serwera lub zmiana hello poziomu usług (warstwy), użyj polecenia cmdlet usługi Azure Resource Manager (AzureRM). Innych zadań związanych z zarządzaniem baz danych, takich jak dodawanie lub usuwanie członków roli, przetwarzania i podziału na partycje za pomocą poleceń cmdlet zawarte w hello tego samego modułu SqlServer jako SQL Server Analysis Services.

## <a name="permissions"></a>Uprawnienia
Większość zadań programu PowerShell wymaga uprawnień administratora na serwerze usług Analysis Services hello, którym zarządzasz. Zaplanowane zadania programu PowerShell są operacje instalacji nienadzorowanej. Konto Hello hello harmonogramu musi mieć uprawnienia administratora na powitania serwera usług Analysis Services. 

Dla operacji serwera za pomocą poleceń cmdlet AzureRm, Twoje konto lub konto hello harmonogramu musi również należeć toohello właściciela roli dla zasobu hello w [based kontroli dostępu (RBAC)](../active-directory/role-based-access-control-what-is.md). 

## <a name="server-operations"></a>Operacji serwera 
Polecenia cmdlet systemu Azure Analysis Services są objęte hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) składnika modułu. tooinstall AzureRM moduły poleceń cmdlet, zobacz [poleceń cmdlet usługi Azure Resource Manager](/powershell/azure/overview) w hello galerii programu PowerShell.

|Polecenie cmdlet|Opis| 
|------------|-----------------| 
|[AzureAnalysisServicesInstance eksportu](/powershell/module/azurerm.analysisservices/export-azureanalysisservicesinstancelog)|Eksporty dziennika toofile.| 
|[Get-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/get-azurermanalysisservicesserver)|Pobiera Szczegóły wystąpienia serwera.|  
|[Nowe AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver)|Tworzy wystąpienie serwera.|
|[Usuń AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/remove-azurermanalysisservicesserver)|Usuwa wystąpienie serwera.|  
|[Wstrzymaj AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/suspend-azurermanalysisservicesserver)|Wstrzymuje wystąpienia serwera.| 
|[Resume-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/resume-azurermanalysisservicesserver)|Wznawia wystąpienia serwera.|  
|[Zestaw AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/set-azurermanalysisservicesserver)|Modyfikuje wystąpienia serwera.|   
|[AzureRmAnalysisServicesServer testu](/powershell/module/azurerm.analysisservices/test-azurermanalysisservicesserver)|Testy istnienia hello wystąpienia serwera.| 

## <a name="database-operations"></a>Operacje bazy danych

Tekst hello Azure Analysis Services, użyj operacji w bazie danych sam [SqlServer](https://www.powershellgallery.com/packages/SqlServer) modułu jako SQL Server Analysis Services. Jednak nie wszystkie polecenia cmdlet są obsługiwane dla usług Azure Analysis Services. 

Moduł SqlServer Hello zapewnia poszczególnych zadań bazy danych poleceń cmdlet do zarządzania, jak również jako polecenia cmdlet ogólnego przeznaczenia Invoke ASCmd hello akceptującego tabelaryczny Model skryptów języka (TMSL) zapytania lub skryptu. Witaj następujących poleceń cmdlet w hello SqlServer module są obsługiwane dla usług Azure Analysis Services.

  
|Polecenie cmdlet|Opis|
|------------|-----------------| 
|[Dodaj RoleMember](https://msdn.microsoft.com/library/hh510167.aspx)|Dodaj element członkowski tooa roli bazy danych.| 
|[ASDatabase kopii zapasowej](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet)|Wykonywanie kopii zapasowej bazy danych usług Analysis Services.|  
|[Usuń RoleMember](https://msdn.microsoft.com/library/hh510173.aspx)|Usuwanie członka z roli bazy danych.|   
|[Wywołanie ASCmd](https://msdn.microsoft.com/library/hh479579.aspx)|Wykonanie skryptu TMSL.|
|[Wywołanie ProcessASDatabase](https://msdn.microsoft.com/library/mt651773.aspx)|Przetwarzanie bazy danych.|  
|[Wywołanie ProcessPartition](https://msdn.microsoft.com/library/hh510164.aspx)|Przetwarzanie partycji.| 
|[Wywołanie ProcessTable](https://msdn.microsoft.com/library/mt651774.aspx)|Przetwarza tabelę.|  
|[Scalania partycji](https://msdn.microsoft.com/library/hh479576.aspx)|Scalania partycji.|  
|[Przywracanie ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet)|Przywróć bazę danych usług Analysis Services.| 
  

## <a name="related-information"></a>Informacje pokrewne

* [Pobierz moduł PowerShell programu SQL Server](https://docs.microsoft.com/sql/ssms/download-sql-server-ps-module)   
* [Pobierz narzędzia SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)   
* [Moduł SqlServer w galerii programu PowerShell](https://www.powershellgallery.com/packages/SqlServer)    
* [Tabelaryczne modelu programowania dla 1200 poziom zgodności lub nowszym](https://msdn.microsoft.com/library/mt712541.aspx)
