---
title: "Zarządzanie kopiami zapasowymi przy użyciu kontroli dostępu opartej na rolach na platformie Azure | Dokumentacja firmy Microsoft"
description: "Użyj operacji zarządzania toobackup dostępu toomanage kontroli dostępu opartej na rolach w magazynie usług odzyskiwania."
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 3bd46b97-4b29-47a5-b5ac-ac174dd36760
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/22/2017
ms.author: trinadhk;markgal
ms.openlocfilehash: 26d034d152f9b77fc6d5b2ffd5ef2648b1797f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-azure-backup-recovery-points"></a>Korzystanie z punktów odzyskiwania kopia zapasowa Azure toomanage kontroli dostępu opartej na rolach
Kontrola dostępu oparta na rolach (Role-Based Access Control, RBAC) na platformie Azure umożliwia precyzyjne zarządzanie dostępem dla platformy Azure. Przy użyciu funkcji RBAC, można rozdzielenie obowiązków w obrębie organizacji i udzielić tylko hello ilość toousers dostępu do potrzebnych tooperform swoich zadań.

> [!IMPORTANT]
> Role udostępniane przez usługi Kopia zapasowa Azure są ograniczone tooactions, które mogą być wykonywane w portalu Azure lub poleceń cmdlet programu PowerShell magazyn usług odzyskiwania. Akcje wykonywane w Azure kopii zapasowej center interfejs użytkownika klienta usługi agenta lub systemu interfejs programu Data Protection Manager lub interfejsu użytkownika serwera kopii zapasowej Azure są poza kontrolą tych ról.

Kopia zapasowa Azure stanowi 3 wbudowane role toocontrol operacji zarządzania kopiami zapasowymi. Dowiedz się więcej na [wbudowane role Azure RBAC](../active-directory/role-based-access-built-in-roles.md)

* [Wykonaj kopię zapasową współautora](../active-directory/role-based-access-built-in-roles.md#backup-contributor) — ta rola ma wszystkie uprawnienia toocreate i zarządzanie kopiami zapasowymi, z wyjątkiem Tworzenie magazynu usług odzyskiwania i podając tooothers dostępu. Wyobraź sobie tej roli administratora zarządzania kopiami zapasowymi, który można wykonać każdej operacji zarządzania kopiami zapasowymi.
* [Wykonaj kopię zapasową Operator](../active-directory/role-based-access-built-in-roles.md#backup-operator) — ta rola ma tooeverything uprawnienia współautora z wyjątkiem usuwanie kopii zapasowej i zarządzanie nimi zasad tworzenia kopii zapasowych. Ta rola jest równoważne toocontributor, z wyjątkiem nie może wykonywać destrukcyjnego operacje, takie jak zatrzymanie tworzenie kopii zapasowej z usuwania danych, lub usunąć rejestrację zasobów lokalnych.
* [Wykonaj kopię zapasową czytnika](../active-directory/role-based-access-built-in-roles.md#backup-reader) — ta rola ma uprawnienia tooview wszystkie operacje zarządzania kopiami zapasowymi. Wyobraź sobie toobe tej roli monitorowania osoby.

Jeśli szukasz toodefine własne role, aby uzyskać większą kontrolę, zobacz temat jak zbyt[Tworzenie niestandardowych ról](../active-directory/role-based-access-control-custom-roles.md) w Azure RBAC.



## <a name="mapping-backup-built-in-roles-toobackup-management-actions"></a>Mapowania akcji zarządzania toobackup wbudowane role kopii zapasowej
Witaj w poniższej tabeli przechwytuje hello akcji związanych z zarządzaniem kopii zapasowej i wymagane odpowiednie minimalne uprawnienia RBAC tooperform tej operacji.

| Operacja zarządzania | Minimalna roli RBAC wymagane |
| --- | --- |
| Tworzenie magazynu usług odzyskiwania | Współautor grupy zasobów magazynu |
| Włączenia kopii zapasowej maszyn wirtualnych Azure | Operator kopii zapasowych w magazynie, współautora maszyny wirtualnej na maszynach wirtualnych |
| Na żądanie kopii zapasowej maszyny Wirtualnej | Operator kopii zapasowych |
| Przywracanie maszyny Wirtualnej | Operator kopii zapasowych maszyny Wirtualnej i sieci wirtualne są przechodzi tooget wdrożone Współautor grupy zasobów |
| Przywracanie dysków, pojedyncze pliki z kopii zapasowej maszyny Wirtualnej | Operator kopii zapasowych |
| Tworzenie zasad tworzenia kopii zapasowej dla kopii zapasowej maszyny Wirtualnej Azure | Współautor kopii zapasowej |
| Modyfikowanie zasad tworzenia kopii zapasowej kopii zapasowej maszyny Wirtualnej Azure | Współautor kopii zapasowej |
| Usuń zasady tworzenia kopii zapasowej kopii zapasowej maszyny Wirtualnej Azure | Współautor kopii zapasowej |
| Zatrzymaj kopii zapasowej (z opcją zachowania danych lub usunięcie danych) w kopii zapasowej maszyny Wirtualnej | Współautor kopii zapasowej |
| Zarejestruj lokalnego systemu Windows serwera/klienta/SCDPM lub serwer kopii zapasowej systemu Azure | Operator kopii zapasowych |
| Usuń zarejestrowane lokalnie systemu Windows serwera/klienta/SCDPM lub serwer kopii zapasowej systemu Azure | Współautor kopii zapasowej |

## <a name="next-steps"></a>Następne kroki
* [Kontroli dostępu opartej na rolach](../active-directory/role-based-access-control-configure.md): rozpoczynanie pracy z RBAC w hello portalu Azure.
* Dowiedz się, jak toomanage do uzyskiwania dostępu do:
  * [PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [Interfejs wiersza polecenia platformy Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [Interfejs API REST](../active-directory/role-based-access-control-manage-access-rest.md)
* [Rozwiązywanie kontroli dostępu opartej na rolach](../active-directory/role-based-access-control-troubleshooting.md): Pobierz sugestie dotyczące rozwiązywania typowych problemów.
