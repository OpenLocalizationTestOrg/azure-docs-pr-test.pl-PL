---
title: "Raportowanie aaaAccess — Azure RBAC | Dokumentacja firmy Microsoft"
description: "Generowanie raportu, że wyświetla wszystkie zmiany w tooyour dostępu do subskrypcji platformy Azure z opartej na rolach kontrola dostępu za pośrednictwem hello w ciągu ostatnich 90 dni."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 2bc68595-145e-4de3-8b71-3a21890d13d9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9ad85d3d8e66ce167032638a35e4afffb46d3892
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-access-report-for-role-based-access-control"></a>Tworzenie raportu programu access do kontroli dostępu opartej na rolach
Ilekroć ktoś lub go przydziela odwołuje dostęp w ramach subskrypcji, hello zmiany mają być rejestrowane w zdarzeń platformy Azure. Można utworzyć toosee raporty historii zmian dostępu do wszystkich zmian dla hello w ciągu ostatnich 90 dni.

## <a name="create-a-report-with-azure-powershell"></a>Tworzenie raportu przy użyciu programu Azure PowerShell
toocreate dostępu zmienić historii raportu w programie PowerShell, użyj hello [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) polecenia.

Po wywołaniu tego polecenia, można określić, które właściwości mają wymienionych w tym następujących hello przydziały hello:

| Właściwość | Opis |
| --- | --- |
| **Akcja** |Określa, czy przyznany lub odwołany dostęp |
| **Obiekt wywołujący** |Zmień właściciela Hello odpowiedzialny za hello dostępu |
| **PrincipalId** | Unikatowy identyfikator Hello hello użytkownika, grupy lub aplikacji, która została przypisana rola hello |
| **PrincipalName** |Nazwa Hello hello użytkownika, grupy lub aplikacji |
| **PrincipalType** |Określa, czy przypisania hello był przeznaczony dla użytkowników, grupy lub aplikacji |
| **Wartość RoleDefinitionId** |Witaj GUID hello roli, który został przyznany lub odwołany |
| **RoleName** |Rola Hello, który został przyznany lub odwołany |
| **Zakres** | Unikatowy identyfikator hello subskrypcji, grupy zasobów lub zasobów, które hello przypisania Hello stosuje zbyt| 
| **ScopeName** |Nazwa Hello hello subskrypcji, grupy zasobów lub zasobów |
| **ScopeType** |Określa, czy hello przydział został w hello subskrypcji, grupy zasobów lub zasobów zakresu |
| **Znacznik czasu** |Witaj Data i godzina dostęp został zmieniony |

To polecenie przykładowe są wyświetlane wszystkie zmiany dostępu w hello subskrypcji na potrzeby hello ostatnich siedmiu dni:

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog — zrzut ekranu](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a>Tworzenie raportu z wiersza polecenia platformy Azure
toocreate raportu historii zmian dostępu w hello Azure interfejsu wiersza polecenia (CLI), użyj hello `azure role assignment changelog list` polecenia.

## <a name="export-tooa-spreadsheet"></a>Arkusz kalkulacyjny tooa eksportu
toosave hello raportu lub manipulować danymi hello, Eksport hello dostępu zmiany w pliku CSV. Następnie można wyświetlić raport hello w arkuszu kalkulacyjnym do przeglądu.

![Wykaz zmian wyświetlane jako arkusz kalkulacyjny — zrzut ekranu](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a>Następne kroki
* Praca z [niestandardowych ról w Azure RBAC](role-based-access-control-custom-roles.md)
* Dowiedz się, jak toomanage [Azure RBAC przy użyciu programu powershell](role-based-access-control-manage-access-powershell.md)

