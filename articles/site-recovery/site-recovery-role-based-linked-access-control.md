---
title: "aaaUsing toomanage kontroli dostępu opartej na roli Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tooapply i używanie kontroli dostępu opartej na rolach (RBAC) toomanage wdrażanie usługi Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: manayar
ms.openlocfilehash: 7b721090351e561b28317ccdcf0ff283e0b146ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-azure-site-recovery-deployments"></a>Wdrożenia usługi Azure Site Recovery toomanage kontroli dostępu opartej na rolach

Kontrola dostępu oparta na rolach (Role-Based Access Control, RBAC) na platformie Azure umożliwia precyzyjne zarządzanie dostępem dla platformy Azure. Przy użyciu funkcji RBAC, można rozdzielenie obowiązków w obrębie organizacji i udzielić tylko toousers uprawnienia dostępu do określonych jako wymagane tooperform określonego zadania.

Usługa Azure Site Recovery zapewnia 3 wbudowane role operacji zarządzania toocontrol usługi Site Recovery. Dowiedz się więcej na [wbudowane role Azure RBAC](../active-directory/role-based-access-built-in-roles.md)

* [Lokacja odzyskiwania współautora](../active-directory/role-based-access-built-in-roles.md#site-recovery-contributor) — ta rola ma wszystkie operacje usługi Azure Site Recovery toomanage wymaganych uprawnień w magazynie usług odzyskiwania. Użytkownika z tą rolą, jednak nie można utworzyć lub usuwanie magazynu usług odzyskiwania lub przypisać dostęp użytkownicy z uprawnieniami tooother. Ta rola jest najbardziej odpowiednie dla administratorów odzyskiwania po awarii można włączyć i zarządzać odzyskiwania po awarii dla aplikacji lub w całej organizacji, jak w przypadku hello.
* [Operator odzyskiwania lokacji](../active-directory/role-based-access-built-in-roles.md#site-recovery-operator) — ta rola ma uprawnienia tooexecute i menedżera trybu Failover i powrotu po awarii operacji. Użytkownika z tą rolą nie Włącz lub Wyłącz replikację, utworzyć lub usunąć magazynów, zarejestrować nową infrastrukturę lub przypisać dostęp użytkownicy z uprawnieniami tooother. Ta rola jest najbardziej odpowiednie dla operatora odzyskiwania po awarii, który można trybu failover maszyny wirtualnej lub przejść do szczegółów aplikacji zaleceniami właściciele aplikacji i Administratorzy systemów informatycznych w sytuacji rzeczywista lub symulowane po awarii, takich jak odzyskiwania po awarii. Post rozpoznawanie powitania po awarii, operator hello odzyskiwania po awarii można ponownie włączyć ochronę i powrotu po awarii hello maszyn wirtualnych.
* [Czytnik odzyskiwania lokacji](../active-directory/role-based-access-built-in-roles.md#site-recovery-reader) — ta rola ma uprawnienia tooview wszystkie operacje zarządzania usługi Site Recovery. Ta rola jest najbardziej odpowiednie dla zarządu monitorowania IT, który można monitorować bieżący stan ochrony hello i podnieść biletami pomocy technicznej, jeśli jest to wymagane.

Jeśli szukasz toodefine własne role, aby uzyskać większą kontrolę, zobacz temat jak zbyt[Tworzenie niestandardowych ról](../active-directory/role-based-access-control-custom-roles.md) na platformie Azure.

## <a name="permissions-required-tooenable-replication-for-new-virtual-machines"></a>Wymagane uprawnienia tooEnable replikacji dla nowych maszyn wirtualnych
Gdy nowej maszyny wirtualnej jest replikowany tooAzure przy użyciu usługi Azure Site Recovery, poziomy dostępu użytkownika hello skojarzone są tooensure zweryfikowane, który hello użytkownika hello wymaga uprawnień toouse hello Azure zasobów udostępnianych tooSite odzyskiwania.

tooenable replikacji dla nowej maszyny wirtualnej, użytkownik musi mieć:
* Uprawnienie toocreate maszynę wirtualną w hello wybranej grupy zasobów
* Uprawnienie toocreate maszynę wirtualną w wybranej sieci wirtualnej hello
* Uprawnienie toowrite toohello wybranego konta magazynu

Użytkownik musi hello następujące uprawnienia replikacji toocomplete nowej maszyny wirtualnej.

> [!IMPORTANT]
>Upewnij się, że odpowiednie uprawnienia są dodawane na powitania modelu wdrażania (Resource Manager / klasycznego) używany do wdrażania zasobów.

| **Typ zasobu** | **Model wdrażania** | **Uprawnienia** |
| --- | --- | --- |
| Wystąpienia obliczeniowe | Resource Manager | Microsoft.Compute/availabilitySets/read |
|  |  | Microsoft.Compute/virtualMachines/read |
|  |  | Microsoft.Compute/virtualMachines/write |
|  |  | Microsoft.Compute/virtualMachines/delete |
|  | Wdrożenie klasyczne | Microsoft.ClassicCompute/domainNames/read |
|  |  | Microsoft.ClassicCompute/domainNames/write |
|  |  | Microsoft.ClassicCompute/domainNames/delete |
|  |  | Microsoft.ClassicCompute/virtualMachines/read |
|  |  | Microsoft.ClassicCompute/virtualMachines/write |
|  |  | Microsoft.ClassicCompute/virtualMachines/delete |
| Sieć | Resource Manager | Microsoft.Network/networkInterfaces/read |
|  |  | Microsoft.Network/networkInterfaces/write |
|  |  | Microsoft.Network/networkInterfaces/delete |
|  |  | Microsoft.Network/networkInterfaces/join/action |
|  |  | Microsoft.Network/virtualNetworks/read |
|  |  | Microsoft.Network/virtualNetworks/subnets/read |
|  |  | Microsoft.Network/virtualNetworks/subnets/join/action |
|  | Wdrożenie klasyczne | Microsoft.ClassicNetwork/virtualNetworks/read |
|  |  | Microsoft.ClassicNetwork/virtualNetworks/join/action |
| Magazyn | Resource Manager | Microsoft.Storage/storageAccounts/read |
|  |  | Microsoft.Storage/storageAccounts/listkeys/action |
|  | Wdrożenie klasyczne | Microsoft.ClassicStorage/storageAccounts/read |
|  |  | Microsoft.ClassicStorage/storageAccounts/listKeys/action |
| Grupa zasobów | Resource Manager | Microsoft.Resources/deployments/* |
|  |  | Microsoft.Resources/subscriptions/resourceGroups/read |

Należy rozważyć użycie hello "Współautora maszyny wirtualnej" i "Klasycznego współautora maszyny wirtualnej" [wbudowane role](../active-directory/role-based-access-built-in-roles.md) wdrożenia usługi Resource Manager i Model Klasyczny odpowiednio modeli.

## <a name="next-steps"></a>Następne kroki
* [Kontrola dostępu oparta na rolach](../active-directory/role-based-access-control-configure.md): rozpoczynanie pracy z RBAC w hello portalu Azure.
* Dowiedz się, jak toomanage do uzyskiwania dostępu do:
  * [PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [Interfejs wiersza polecenia platformy Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [Interfejs API REST](../active-directory/role-based-access-control-manage-access-rest.md)
* [Rozwiązywanie kontroli dostępu opartej na rolach](../active-directory/role-based-access-control-troubleshooting.md): Pobierz sugestie dotyczące rozwiązywania typowych problemów.
