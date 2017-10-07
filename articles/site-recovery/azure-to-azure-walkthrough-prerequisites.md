---
title: "aaaBefore rozpoczęciem replikacji regionu tooanother maszynach wirtualnych platformy Azure | Dokumentacja firmy Microsoft"
description: "Zawiera podsumowanie kroków hello należy tootake przed replikowanie maszyn wirtualnych platformy Azure między regiony platformy Azure przy użyciu usługi Azure Site Recovery hello"
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
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 7fa633075eeb52d0c184a1dd8d53ccc15644f518
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-before-you-start"></a>Krok 2: Przed rozpoczęciem

Po przejrzeniu hello [architektura](azure-to-azure-walkthrough-architecture.md) do replikowania maszyn wirtualnych platformy Azure (maszyny wirtualne) między regiony platformy Azure z [usługi Azure Site Recovery](site-recovery-overview.md), użyj tego wymagania wstępne tooverify artykułu. 

- Po zakończeniu hello artykuł ma wyraźnego zrozumienia co jest potrzebne wdrożenia hello toomake pracy i zakończył hello wstępnie wymagane kroki.
- Opublikuj wszelkie komentarze u dołu hello w tym artykule, lub zadać pytania w hello [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

>[!NOTE]
>
> Replikacja maszyny Wirtualnej platformy Azure jest obecnie w przeglądzie.



## <a name="support-recommendations"></a>Zalecenia dotyczące pomocy technicznej

W poniższej tabeli hello przeglądu.

**Składnik** | **Wymaganie**
--- | ---
**Magazyn usług odzyskiwania** | Zaleca się tworzenie magazynu usług odzyskiwania w celu hello region platformy Azure mają toouse odzyskiwania po awarii. Na przykład jeśli chcesz tooreplicate źródłowe maszyny wirtualne w tooCentral wschodnie stany USA USA, utwórz magazyn hello w środkowe stany USA.
**Subskrypcja platformy Azure** | Subskrypcji platformy Azure powinna być włączona toocreate maszyn wirtualnych, w miejscu docelowym hello, które mają toouse jako region odzyskiwania po awarii hello. Skontaktuj się z pomocą techniczną tooenable hello wymagane limitu przydziału.
**Pojemność region docelowy** | W celu hello region platformy Azure hello subskrypcji ma za mało pojemności dla maszyn wirtualnych, kont magazynu i składników sieciowych.
**Storage** | Użyj hello [wskazówki magazynu](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) źródła maszynach wirtualnych platformy Azure, tooavoid problemy z wydajnością.<br/><br/> Konta magazynu musi być w hello tym samym regionie co magazyn hello.<br/><br/> Nie można replikować toopremium kont w środkowej i Południowa, Indie.<br/><br/> W przypadku wdrożenia replikacji z ustawieniami domyślnymi hello, Usługa Site Recovery tworzy hello wymagane konta magazynu, na podstawie hello źródło konfiguracji. Jeśli możesz dostosować ustawienia, należy wykonać hello [wartości docelowe skalowalności dysków maszyny Wirtualnej](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).
**Sieć** | Tooallow połączenia wychodzącego z maszyn wirtualnych platformy Azure, należy dla określonych zakresów adresów URL/adresu IP.<br/><br/> Kont sieci musi być w hello tym samym regionie co magazyn hello. 
**Maszyna wirtualna platformy Azure** | Upewnij się, że wszystkie certyfikaty główne najnowsze hello są na powitania maszyny Wirtualnej Azure systemu Windows i Linux. Gdy nie są one będzie hello tooregister stanie maszyny Wirtualnej w ramach odzyskiwania lokacji z powodu ograniczeń zabezpieczeń.
**Konto użytkownika systemu Azure** | Twoje konto użytkownika systemu Azure wymaga toohave niektórych [uprawnienia](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replikacji maszyny wirtualnej platformy Azure.

Pobierz pełną listę wymagań pomocy technicznej w hello [macierz obsługi](site-recovery-support-matrix-azure-to-azure.md)


## <a name="set-permissions-on-hello-account"></a>Ustawianie uprawnień dla konta hello

1. Przeczytaj informacje o hello [uprawnienia](site-recovery-role-based-linked-access-control.md) wymagane dla replikacji.
2. Postępuj zgodnie z następującymi [instrukcje](../active-directory/role-based-access-control-configure.md#add-access) tooadd uprawnienia.


## <a name="verify-target-resources"></a>Sprawdź zasoby obiektów docelowych

1. Włącz tooallow Twojej subskrypcji platformy Azure VMs toocreate w hello docelowych region ma toouse, które mają toouse jako region odzyskiwania po awarii hello odzyskiwania po awarii. Skontaktuj się z pomocą techniczną tooenable hello wymagane limitu przydziału.
2. Upewnij się, że subskrypcja ma za mało zasobów tooenable maszyn wirtualnych o rozmiarze zgodne źródłowe maszyny wirtualne. Domyślnie w przypadku skonfigurowania replikacji, Usługa Site Recovery pobrania hello sam rozmiar hello stosowane do maszyny Wirtualnej lub hello najbliższy rozmiar. Dowiedz się więcej o [Rozwiązywanie problemów z](site-recovery-azure-to-azure-troubleshoot-errors.md#azure-resource-quota-issues-error-code-150097) zasobów docelowych.

## <a name="verify-azure-vm-certificates"></a>Sprawdź certyfikaty maszyny Wirtualnej Azure

1. Sprawdź wszystkie certyfikaty główne najnowsze hello znajdują się w systemie Windows hello lub ma tooreplicate maszyn wirtualnych systemu Linux. Jeśli nie podano hello najnowsze certyfikaty główne, hello maszyny Wirtualnej nie może być zarejestrowany tooSite odzyskiwania ze względu na ograniczenia toosecurity.
2. Dla maszyn wirtualnych systemu Windows hello następujące:

    - Zainstaluj wszystkie hello najnowsze aktualizacje systemu Windows na powitania maszyny Wirtualnej, aby wszystkie certyfikaty główne hello zaufany na maszynie hello.
    - W środowisku bez połączenia procedura hello standardowe usługi Windows Update certyfikat/procesu aktualizacji w organizacji, tooget hello najnowsze certyfikaty główne i zaktualizowaną listę CRL, na maszynach wirtualnych hello.
3. Dla maszyn wirtualnych systemu Linux Wykonaj wskazówki hello Linux dystrybutora tooget hello najnowsze zaufanych certyfikatów głównych oraz hello ostatnią listę odwołania certyfikatów na powitania maszyny Wirtualnej. Dowiedz się więcej o [Rozwiązywanie problemów z](site-recovery-azure-to-azure-troubleshoot-errors.md#trusted-root-certificates-error-code-151066) zaufanych głównych problemów.


## <a name="next-steps"></a>Następne kroki

Przejdź za[krok 3: Planowanie sieci](azure-to-azure-walkthrough-network.md) tooset się łączność wychodząca.
