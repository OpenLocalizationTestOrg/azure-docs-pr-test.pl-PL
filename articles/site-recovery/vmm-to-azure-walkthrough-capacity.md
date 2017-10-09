---
title: "aaaPlan wydajności i skalowania dla maszyny Wirtualnej funkcji Hyper-V tooAzure replikacji (w programie VMM) z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Użyj tego artykułu tooplan pojemności i skali, podczas replikacji maszyn wirtualnych funkcji Hyper-V w programie VMM chmur tooAzure z usługą Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 41c3c83e-6b1a-496a-8179-498c552ef0c7
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 9818ada9bb21f60ac00b3894696201b06630cb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-with-vmm-tooazure-replication"></a>Krok 3: Planowanie wydajności i skalowania dla replikacji tooAzure funkcji Hyper-V (w programie VMM)

Po przejrzeniu hello [wymagania wstępne dotyczące wdrażania](vmm-to-azure-walkthrough-prerequisites.md), użyj tego artykułu toofigure limit planowania pojemności, jak i skalowanie podczas replikowania lokalnych maszyn wirtualnych funkcji Hyper-V w tooAzure chmur programu System Center Virtual Machine Manager (VMM), z [usługi Azure Site Recovery](site-recovery-overview.md).

Po przeczytaniu tego artykułu, post wszelkie komentarze u dołu hello, lub zadać pytania techniczne na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="how-do-i-start-capacity-planning"></a>Jak rozpocząć planowanie pojemności


Możesz zbierać informacje o środowisku replikacji i następnie pojemności planu przy użyciu hello dane, wraz z uwagi hello wyróżniane w tym artykule.


## <a name="gather-information"></a>Zbieranie informacji

1. Zebrać informacje o środowisku replikacji, w tym o maszynach wirtualnych, liczbie dysków na maszynę wirtualną oraz pojemności dysków.
2. Określ częstotliwość codziennych zmian (przenoszenia) dla replikowanych danych. Pobierz hello [narzędzia do planowania pojemności funkcji Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) szybkość zmian hello tooget. Firma Microsoft zaleca się, że możesz uruchomić to narzędzie za pośrednictwem toocapture tygodnia średnie.
 

## <a name="figure-out-capacity"></a>Ustalenia pojemności

Na podstawie informacji hello znasz zbieranie, uruchom hello [Planisty wydajności odzyskiwania lokacji](http://aka.ms/asr-capacity-planner-excel) tooanalyze Twojego środowiska źródłowego i obciążeń, oszacować wymagania dotyczące przepustowości i zasobów serwera dla lokalizacji źródła hello i hello zasoby (maszyn wirtualnych i magazynu itp.), które należy w miejscu docelowym hello. Można uruchomić narzędzie hello w kilka metod:

- Planowanie szybkie: Uruchom narzędzie hello w tym trybie tooget sieci i serwera prognozy oparte na średnich liczbach maszyn wirtualnych, dysków, magazynu i szybkość zmian.
- Szczegółowe planowanie: Uruchom narzędzie hello w tym trybie i podaj szczegóły poszczególnych obciążeń na poziomie maszyny Wirtualnej. Analizowanie zgodności maszyny Wirtualnej i uzyskać projekcje sieci i serwera.

Teraz uruchom narzędzie hello:

1. Pobierz hello [narzędzia](http://aka.ms/asr-capacity-planner-excel)
2. Szybkie planner hello toorun wykonaj [tych instrukcji](site-recovery-capacity-planner.md#run-the-quick-planner)oraz scenariusz hello wybierz **tooAzure funkcji Hyper-V**.
3. toorun hello planner szczegółowe, należy wykonać [tych instrukcji](site-recovery-capacity-planner.md#run-the-detailed-planner)oraz scenariusz wybierz hello **tooAzure funkcji Hyper-V**.

## <a name="control-network-bandwidth"></a>Sterowania przepustowością sieci

Po znasz obliczeniowej hello wymaganą przepustowość, masz kilka opcji kontrolowanie hello ilość przepustowości używanej w ramach replikacji:

* **Ograniczanie przepustowości**: ruch funkcji Hyper-V, który replikuje tooAzure przechodzi przez konkretnego hosta funkcji Hyper-V. Można ograniczyć przepustowość na powitania serwera hosta.
* **Wpływ przepustowości**: możesz wywrzeć wpływ hello przepustowość dla replikacji przy użyciu kilku kluczy rejestru.

### <a name="throttle-bandwidth"></a>Ograniczanie przepustowości
1. Otwórz hello Microsoft Azure Backup przystawka programu MMC na serwerze hosta funkcji Hyper-V hello. Domyślnie skrót do usługi Kopia zapasowa Microsoft Azure jest dostępny na pulpicie hello, lub C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. W przystawce powitania kliknij **Zmień właściwości**.
3. Na powitania **ograniczania** wybierz pozycję **włączyć użycia przepustowości połączenia internetowego do operacji tworzenia kopii zapasowej**i Ustaw limity hello do pracy oraz innych niż godziny pracy. Prawidłowe zakresy są od 512 KB/s too102 MB/s na sekundę.

    ![Ograniczanie przepustowości](./media/vmm-to-azure-walkthrough-capacity/throttle2.png)

Można również użyć hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) ograniczania tooset polecenia cmdlet. Oto przykład:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** wskazuje, że ograniczanie przepływności nie jest wymagane.

### <a name="influence-network-bandwidth"></a>Wywieranie wpływu na przepustowość sieci
1. W rejestrze hello Przejdź zbyt**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.
   * tooinfluence hello przepustowości ruchu replikacji dysku, zmodyfikuj hello wartość hello **UploadThreadsPerVM**, lub Utwórz klucz hello, jeśli nie istnieje.
   * tooinfluence hello przepustowości dla ruchu powrotu po awarii z platformy Azure, zmodyfikuj wartość hello **DownloadThreadsPerVM**.
2. Witaj, wartość domyślna to 4. W sieci "o nadmiarowych zasobach" należy zmienić te klucze rejestru hello wartości domyślnych. Witaj maksymalna to 32. Monitorowanie ruchu toooptimize hello wartość.

## <a name="next-steps"></a>Następne kroki

Przejdź za[krok 4: Planowanie sieci](vmm-to-azure-walkthrough-network.md).
