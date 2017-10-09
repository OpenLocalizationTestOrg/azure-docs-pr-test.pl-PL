---
title: "aaaSet ustawienia replikacji dla usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooAzure chmur toodeploy usługi Site Recovery tooorchestrate replikacji, trybu failover i odzyskiwania maszyn wirtualnych funkcji Hyper-V w programie VMM."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: rayne-wiselman
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: 618e92e42411732a2a1bb75c5e5ea8a433cd7d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-replication-policy-for-vmware-tooazure"></a>Zarządzanie zasadami replikacji dla VMware tooAzure


## <a name="create-a-replication-policy"></a>Tworzenie zasad replikacji

1. Wybierz pozycję **Zarządzaj** > **Infrastruktura usługi Site Recovery**.
2. Wybierz pozycję **Zasady replikacji** w sekcji **Oprogramowanie VMware i maszyny fizyczne**.
3. Wybierz pozycję **+Zasady replikacji**.

    ![Tworzenie zasad replikacji](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. Wprowadź nazwę zasad hello.

5. W **próg RPO**, określ hello RPO limit. Przekroczenie tego limitu przez replikację ciągłą będzie powodować generowanie alertów.
6. W **przechowywania punktu odzyskiwania**, określ (w godzinach) hello hello przechowywania przedział czasu dla każdego punktu odzyskiwania. Chronione maszyny można odzyskać tooany punkt w obrębie okna przechowywania.

    > [!NOTE]
    > Zapasowej too24 godzin przechowywania jest obsługiwana dla maszyn toopremium replikowanego magazynu. Zapasowej too72 godzin przechowywania jest obsługiwana dla maszyn toostandard replikowanego magazynu.

    > [!NOTE]
    > Zasady replikacji na potrzeby powrotu po awarii są tworzone automatycznie.

7. W obszarze **Częstotliwość wykonywania migawek na poziomie aplikacji** określ, jak często (w minutach) będą tworzone punkty odzyskiwania zawierające migawki spójne z aplikacjami.

8. Kliknij przycisk **OK**. Witaj zasady powinny zostać utworzone w too60 30-sekundowym.

![Generowanie zasad replikacji](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a>Kojarzenie serwera konfiguracji z zasadami replikacji
1. Wybierz toowhich zasad replikacji hello ma tooassociate hello konfiguracji serwera.
2. Kliknij pozycję **Skojarz**.
![Kojarzenie serwera konfiguracji](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)

3. Wybierz serwer konfiguracji hello hello liście serwerów.
4. Kliknij przycisk **OK**. Serwer konfiguracji Hello powinna być skojarzona jeden tootwo minut.

![Kojarzenie serwera konfiguracji](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a>Edytowanie zasad replikacji
1. Wybierz zasady replikacji hello, dla której ma zostać tooedit ustawień replikacji.
![Edytowanie zasad replikacji](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)

2. Kliknij pozycję **Edytuj ustawienia**.
![Edytowanie ustawień zasad replikacji](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)

3. Zmień ustawienia hello oparte na potrzeby.
4. Kliknij pozycję **Zapisz**. zasady Hello powinny być zapisywane w dwóch minut toofive, w zależności od liczby maszyn wirtualnych korzystają z tej zasady replikacji.

![Zapisywanie zasad replikacji](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a>Usuwanie skojarzenia serwera konfiguracji z zasad replikacji
1. Wybierz toowhich zasad replikacji hello ma tooassociate hello konfiguracji serwera.
2. Kliknij pozycję **Usuń skojarzenie**.
3. Wybierz serwer konfiguracji hello hello liście serwerów.
4. Kliknij przycisk **OK**. Serwer konfiguracji Hello powinien można usunąć skojarzenia minut tootwo jeden.

    > [!NOTE]
    > Jeśli istnieje co najmniej jeden element replikowane za pomocą zasad hello nie może usunąć skojarzenie serwera konfiguracji. Upewnij się, nie ma żadnych zreplikowanych towarów przy użyciu zasad hello przed skojarzenie powitania serwera konfiguracji.

## <a name="delete-a-replication-policy"></a>Usuwanie zasad replikacji

1. Wybierz zasady replikacji hello, które mają toodelete.
2. Kliknij polecenie **Usuń**. Witaj zasady powinny zostać usunięte w ciągu 30 sekund too60.

    > [!NOTE]
    > Nie można usunąć zasad replikacji, jeśli ma ona co najmniej jeden tooit skojarzone serwerem konfiguracji. Upewnij się, że nie ma żadnych zreplikowanych elementów za pomocą zasad hello i usunąć wszystkie hello skojarzone serwery konfiguracji przed usunięciem hello zasad.
