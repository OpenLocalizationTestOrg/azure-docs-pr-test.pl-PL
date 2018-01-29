---
title: "Jak przypisać MSI dostępu do zasobów platformy Azure przy użyciu programu PowerShell"
description: "Krok po kroku instrukcje dotyczące przypisywania MSI dla jednego zasobu, dostęp do innego zasobu, przy użyciu programu PowerShell."
services: active-directory
documentationcenter: 
author: bryanla
manager: mtillman
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 09/14/2017
ms.author: bryanla
ms.openlocfilehash: 2211146dec8ea1f460785af9efd801780c46df60
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="assign-a-managed-service-identity-msi-access-to-a-resource-using-powershell"></a>Przypisywanie dostępu zarządzane tożsamości usługi (MSI) do zasobów przy użyciu programu PowerShell

[!INCLUDE[preview-notice](../../includes/active-directory-msi-preview-notice.md)]

Po skonfigurowaniu zasobów platformy Azure z Instalatora MSI, możesz zapewnić dostęp MSI do innego zasobu, podobnie jak wszelkie podmiotu zabezpieczeń. Ten przykład przedstawia sposób udzielić dostępu MSI Azure maszyny wirtualnej do konta magazynu platformy Azure, przy użyciu programu PowerShell.

## <a name="prerequisites"></a>Wymagania wstępne

[!INCLUDE [msi-qs-configure-prereqs](../../includes/active-directory-msi-qs-configure-prereqs.md)]

Ponadto zainstalować [Azure PowerShell w wersji 4.3.1](https://www.powershellgallery.com/packages/AzureRM/4.3.1) Jeśli jeszcze.

## <a name="use-rbac-to-assign-the-msi-access-to-another-resource"></a>Użycie funkcji RBAC można przypisać MSI dostęp do innego zasobu

Po włączeniu MSI na zasobów platformy Azure, [takich jak maszyny Wirtualnej platformy Azure](msi-qs-configure-powershell-windows-vm.md):

1. Zaloguj się do platformy Azure przy użyciu `Login-AzureRmAccount` polecenia cmdlet. Użyj konta, które jest skojarzone z subskrypcją platformy Azure, w którym skonfigurowano MSI:

   ```powershell
   Login-AzureRmAccount
   ```
2. W tym przykładzie udostępniamy możliwość sprawowania maszyny Wirtualnej Azure dostęp do konta magazynu. Najpierw używamy [Get AzureRMVM](/powershell/module/azurerm.compute/get-azurermvm) można pobrać nazwy głównej usługi dla maszyny Wirtualnej o nazwie "myVM", który został utworzony po włączeniu możemy MSI. Następnie używamy [AzureRmRoleAssignment nowy](/powershell/module/AzureRM.Resources/New-AzureRmRoleAssignment) umożliwiają Maszynie wirtualnej "Czytnika" dostęp do konta magazynu o nazwie "myStorageAcct":

    ```powershell
    $spID = (Get-AzureRMVM -ResourceGroupName myRG -Name myVM).identity.principalid
    New-AzureRmRoleAssignment -ObjectId $spID -RoleDefinitionName "Reader" -Scope "/subscriptions/<mySubscriptionID>/resourceGroups/<myResourceGroup>/providers/Microsoft.Storage/storageAccounts/<myStorageAcct>"
    ```

## <a name="troubleshooting"></a>Rozwiązywanie problemów

Jeśli plik MSI dla zasobu nie występuje na liście dostępnych tożsamości, sprawdź, czy MSI została prawidłowo włączona. W tym przypadku firma Microsoft wrócić do maszyny Wirtualnej platformy Azure w ramach [portalu Azure](https://portal.azure.com) oraz:

- Szukaj na stronie "Konfiguracja" i upewnij się, MSI włączone = "Yes".
- Przyjrzyj się Strona "Rozszerzenia" i upewnij się, z rozszerzeniem MSI pomyślnie wdrożone.

Jeśli jest albo nieprawidłowa, może być konieczne ponownie Wdróż ponownie MSI na zasobie oraz rozwiązywania problemów dotyczących niepowodzenia wdrożenia.

## <a name="related-content"></a>Zawartość pokrewna

- Omówienie MSI, zobacz [omówienie zarządzane tożsamość usługi](msi-overview.md).
- Aby włączyć MSI w maszynie Wirtualnej platformy Azure, zobacz [skonfigurować Azure VM zarządzane usługi tożsamości (MSI) przy użyciu programu PowerShell](msi-qs-configure-powershell-windows-vm.md).

W poniższej sekcji komentarzy umożliwia wyrazić swoją opinię i pomóc nam dostosować i kształtu zawartość.

