---
title: "Replikowanie maszyn wirtualnych platformy Azure między regiony platformy Azure na potrzeby odzyskiwania po awarii: Azure tooAzure | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków hello należy maszynach wirtualnych platformy Azure tooreplicate między regiony platformy Azure (Azure-Azure) z usługą Azure Site Recovery hello na potrzeby odzyskiwania po awarii."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: raynew
ms.openlocfilehash: c4c425af260a9bcc3dd4dcc13da26109e20f03bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a>Replikowanie maszyn wirtualnych Azure między regionami z usługą Azure Site Recovery

>[!NOTE]
>
> Azure Site Recovery replikacji maszyn wirtualnych platformy Azure (VM) jest obecnie w przeglądzie.

W tym artykule opisano, jak hello tooreplicate maszynach wirtualnych platformy Azure między regiony platformy Azure przy użyciu [usługi Site Recovery](site-recovery-overview.md) w hello portalu Azure.

Opublikuj komentarze i pytania u dołu hello tym artykułem lub na powitania [forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="disaster-recovery-in-azure"></a>Odzyskiwanie po awarii na platformie Azure

Funkcje i możliwości wbudowanego infrastruktury platformy Azure wpływ tooa strategii dostępności niezawodny i odporność dla zadań uruchamianych na maszynach wirtualnych platformy Azure. Istnieje jednak wiele przyczyn, czego potrzebujesz tooplan odzyskiwania po awarii między regiony platformy Azure samodzielnie:

- Należy toomeet wytycznych dotyczących zgodności określonych aplikacji i obciążeń, które wymagają ciągłość prowadzenia działalności biznesowej i strategia odzyskiwania (BCDR).
- Mają hello możliwości tooprotect i odzyskiwania maszyn wirtualnych platformy Azure w zależności od decyzji biznesowych, a nie tylko oparte na wbudowanych funkcji platformy Azure.
- Należy tootest trybu failover i odzyskiwania zgodnie z potrzebami działalności biznesowej i zgodności bez wpływu na produkcję.
- Wymagana jest toofail toohello region odzyskiwania w razie awarii hello i bezproblemowo niepowodzenie wstecz toohello oryginalnego źródła regionu.

Użyj usługi Site Recovery dla maszyny Wirtualnej Azure-Azure replikacji toohelp wykonać te zadania.


## <a name="why-use-site-recovery"></a>Dlaczego warto używać usługi Site Recovery?      

Usługa Site Recovery zapewnia tooreplicate prosty sposób maszynach wirtualnych platformy Azure między regionami:

- **Automatyczne wdrażanie**. W przeciwieństwie do modelu typu aktywny aktywny replikacji nie istnieje potrzeba infrastruktury kosztowne i złożone w regionie pomocniczym hello. Po włączeniu replikacji usługi Site Recovery automatycznie tworzy hello wymagane zasoby w hello region docelowy, na podstawie ustawień regionu źródła.
- **Kontrolowanie regionów**. Z usługą Site Recovery może replikować wszelkie tooany regionu w kontynencie. To porównać z magazynu geograficznie nadmiarowego dostęp do odczytu, która asynchronicznie replikuje dane między standard [łączyć regionów](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) tylko. Dostęp do odczytu magazynu geograficznie nadmiarowego udostępnia dane toohello dostęp tylko do odczytu w hello region docelowy.
- **Automatyczne replikacji**. Usługa Site Recovery zapewnia zautomatyzowane replikacji ciągłej. Tryb failover i powrotu po awarii może być uruchomiona za pomocą jednego kliknięcia.
- **RTO i RPO**. Odzyskiwanie lokacji korzysta z infrastruktury sieci Azure hello łączy tookeep regionów RTO i RPO bardzo niskie.
- **Testowanie**. Testowanie odzyskiwania po awarii można uruchomić z na żądanie testu pracy w trybie Failover, gdy potrzebne bez wpływu na Twoje obciążeń produkcyjnych lub trwającej replikacji.
- **Plany odzyskiwania**. Można użyć trybu failover tooorchestrate planów odzyskiwania i powrotu po awarii całej aplikacji hello działające na wielu maszynach wirtualnych. Funkcja planu odzyskiwania Hello ma sformatowanego najwyższej jakości integracji z elementu runbook usługi Automatyzacja Azure.


## <a name="deployment-summary"></a>Podsumowanie wdrożenia

Oto co należy podsumowanie tooset toodo replikacji maszyn wirtualnych między regiony platformy Azure:

1. Utwórz magazyn usługi Recovery Services. Magazyn Hello zawiera ustawienia konfiguracji i organizuje replikację.
2. Włącz replikację hello maszynach wirtualnych platformy Azure.
3. Uruchom test toomake trybu failover, się, że wszystko działa zgodnie z oczekiwaniami.

>[!IMPORTANT]
>
> Możesz sprawdzić hello [macierzy obsługi replikacji maszyny Wirtualnej Azure](./site-recovery-support-matrix-azure-to-azure.md).

>[!IMPORTANT]
>
> Aby informacji na temat sposobu tooconfigure hello wymagane wychodzące połączenie sieciowe dla maszyn wirtualnych platformy Azure dla replikacji usługi Site Recovery, zobacz hello [sieci wytycznych](./site-recovery-azure-to-azure-networking-guidance.md).

### <a name="before-you-start"></a>Przed rozpoczęciem

* Twoje konto użytkownika systemu Azure wymaga toohave niektórych [uprawnienia](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replikacji maszyny wirtualnej platformy Azure.
* Subskrypcja platformy Azure powinna być maszyn wirtualnych toocreate włączone w miejscu docelowym hello, które mają toouse jako region odzyskiwania po awarii hello. Skontaktuj się z pomocą techniczną tooenable hello wymagane limitu przydziału.

## <a name="create-a-recovery-services-vault"></a>Tworzenie magazynu Usług odzyskiwania

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> Zaleca się tworzenie magazynu usług odzyskiwania hello w hello lokalizację tooreplicate sieci maszyn wirtualnych. Na przykład, jeśli w lokalizacji docelowej jest hello centralnego nam, utwórz magazyn hello w **środkowe stany USA**.

## <a name="enable-replication"></a>Włączanie replikacji

W **Magazyny usług odzyskiwania**, kliknij nazwę magazynu hello. W magazynie powitania kliknij hello **+ Replikuj** przycisku.

### <a name="step-1-configure-hello-source"></a>Krok 1. Konfigurowanie źródła hello
1. W **źródła**, wybierz pozycję **Azure — wersja ZAPOZNAWCZA**.
2. W **lokalizacja źródłowa**, wybierz źródło hello region platformy Azure, w którym są uruchomione maszyny wirtualne.
3. Hello wybierz model wdrażania maszyn wirtualnych: **Resource Manager** lub **klasycznego**.
4. Wybierz hello **źródłowa grupa zasobów** dla maszyn wirtualnych Menedżera zasobów lub **usługi w chmurze** klasycznych maszyn wirtualnych.

    ![Konfigurowanie źródła hello](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a>Krok 2. Wybierz maszyny wirtualne

* Wybierz VMs hello tooreplicate, a następnie kliknij przycisk **OK**.

    ![Wybierz maszyny wirtualne](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a>Krok 3. Konfigurowanie ustawień

1. domyślne hello toooverride target ustawienia i określ ustawienia hello wybór, kliknij przycisk **Dostosuj**. Aby uzyskać więcej informacji, zobacz [dostosować zasoby docelowe](site-recovery-replicate-azure-to-azure.md##customize-target-resources).

    ![Konfigurowanie ustawień](./media/site-recovery-azure-to-azure/settings.png)


2. Domyślnie usługa Site Recovery tworzy zasady replikacji, która przyjmuje migawki spójne z aplikacjami co 4 godziny i przechowuje punkty odzyskiwania przez 24 godziny. Kliknij toocreate zasady z różnymi ustawieniami **Dostosuj** dalej zbyt**zasad replikacji**.

    ![Dostosuj zasady](./media/site-recovery-azure-to-azure/customize-policy.png)

3. toostart inicjowania obsługi administracyjnej hello zasobów docelowych, kliknij przycisk **Utwórz zasoby docelowe**. Inicjowanie obsługi administracyjnej ma minuty. Nie zamykaj bloku hello podczas inicjowania obsługi lub wymagana jest toostart.

4. Replikacja tootrigger hello zaznaczone maszyny Wirtualnej, kliknij przycisk **włączyć replikację**.

5. Możesz śledzić postępy hello **Włącz ochronę** zadania w **ustawienia** > **zadania** > **zadania usługi Site Recovery**.

6. W **ustawienia** > **elementy replikowane**, można wyświetlić stan hello maszyn wirtualnych i hello postęp replikacji początkowej. Kliknij przycisk hello toodrill maszyny Wirtualnej w dół do jego ustawień.

## <a name="run-a-test-failover"></a>Wykonywanie próby przejścia w tryb failover

Po skonfigurowaniu wszystko, uruchom test toomake trybu failover, czy wszystko działa zgodnie z oczekiwaniami:

1. toofail na jednym komputerze, w **ustawienia** > **elementy replikowane**, kliknij przycisk hello wirtualna **+ testowy tryb Failover** ikony.

2. zaplanować toofail za pośrednictwem odzyskiwania, **ustawienia** > **plany odzyskiwania**, kliknij prawym przyciskiem myszy hello planu **testowy tryb Failover**. toocreate planu odzyskiwania [wykonaj te instrukcje](site-recovery-create-recovery-plans.md). 

3. W **testowy tryb Failover**, wybierz pozycję hello docelowej sieci wirtualnej platformy Azure toowhich maszynach wirtualnych platformy Azure są połączone po hello pracy awaryjnej.

4. toostart hello trybu failover, kliknij przycisk **OK**. tootrack postępu, kliknij przycisk tooopen wirtualna hello jego właściwości. Można też kliknąć przycisk hello **testowy tryb Failover** zadania w nazwie magazynu hello > **ustawienia** > **zadania** > **zadania usługi Site Recovery**.

5. Po hello trybu failover zakończy, replika hello Azure maszyny pojawia się w hello portalu Azure > **maszyn wirtualnych**. Upewnij się, że tej maszyny Wirtualnej hello jest hello odpowiedni rozmiar, który połączył toohello odpowiedniej sieci i czy działa.

6. toodelete hello maszyn wirtualnych, które zostały utworzone podczas hello testowania trybu failover kliknij **oczyszczania testowy tryb failover** na powitania replikowane element lub hello planu odzyskiwania. W **uwagi**, zarejestrować i zapisać wszelkie obserwacje związane z hello testowy tryb failover. 

[Dowiedz się więcej](site-recovery-test-failover-to-azure.md) o testowy tryb failover.


## <a name="next-steps"></a>Następne kroki

Po przetestowaniu hello wdrażania:

- [Dowiedz się więcej](site-recovery-failover.md) o różnych typach trybu failover i w jaki sposób toorun je.
- Dowiedz się więcej o [przy użyciu planów odzyskiwania](site-recovery-create-recovery-plans.md) tooreduce RTO.
