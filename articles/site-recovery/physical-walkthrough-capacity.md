---
title: "aaaPlan wydajności i skalowania dla tooAzure replikacji serwerze fizycznym z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Użyj tego artykułu tooplan wydajności i skali, podczas replikowania tooAzure serwerach fizycznych systemu Windows i Linux z usługą Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 554f59ee-0b49-4779-9737-90cb601ef6fe
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: rayne
ms.openlocfilehash: 209980963c07d13e15802a5da44769ac559217d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-physical-server-tooazure-replication"></a>Krok 3: Planowanie wydajności i skalowania replikacji tooAzure serwera fizycznego

Użyj tego artykułu toofigure limitu pojemności i skalowania, Jeśli replikujesz lokalnymi tooAzure serwerach fizycznych systemu Windows i Linux z [usługi Azure Site Recovery](site-recovery-overview.md).

Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="plan-deployment-capacity"></a>Planowanie pojemności wdrożenia

1. Przeczytaj [artykułu](site-recovery-plan-capacity-vmware.md) toolearn o określenie wymagań dotyczących replikacji oraz wskazówki dotyczące ustalania rozmiaru składnikami usługi Site Recovery.
2. Przeczytaj uwagi hello poniżej toolearn o skalowania składników serwerów i sterowania przepustowością zreplikowanej maszyny.

## <a name="replication-considerations"></a>Uwagi dotyczące replikacji

Użyj toofigure te zagadnienia wymagania replikowanych serwera.

**Składnik** | **Szczegóły** 
--- | --- 
**Replikacja** | **Maksymalna szybkość codziennych zmian:** chronionej maszyny można używać tylko jednego serwera przetwarzania i serwer pojedynczego procesu może obsługiwać codzienne szybkość zmian w górę too2 TB. W związku z tym 2 TB jest hello, codzienne dane zmienić szybkość, z której jest obsługiwana dla komputera chronionego.<br/><br/> **Maksymalna przepustowość:** zreplikowanej maszyny mogą należeć tooone konta magazynu na platformie Azure. Konto magazynu w warstwie standardowa może obsługiwać maksymalnie 20 000 żądań na sekundę, i zaleca się utrzymać hello liczba operacji wejścia/wyjścia na sekundę (IOPS) dla too20 maszyny źródłowej, 000. Na przykład jeśli masz maszyny źródłowej z dyskami 5, a każdy dysk generuje 120 IOPS (rozmiarze 8 KB) na maszynie źródłowej hello, następnie będzie w hello Azure limitu IOPS dysku 500. (hello liczba kont magazynu wymagana jest równy toohello maszyny źródłowej całkowita IOPS, podzielona przez 20 000).

## <a name="configuration-server-capacity"></a>Pojemność serwera konfiguracji

Serwer konfiguracji Hello powinien być stanie toohandle hello codziennych zmian szybkość pojemności we wszystkich obciążeń uruchomionych na chronionych komputerach i musi wystarczającą przepustowość toocontinuously replikowany tooAzure danych magazynu.

Najlepszym rozwiązaniem, zlokalizować hello konfiguracji serwera na powitania tej samej sieci, a segment sieci LAN jako hello maszyn, które mają tooprotect. Może znajdować się na inną sieć, ale ma tooprotect powinny mieć warstwy 3 sieci widoczność tooit maszyny.

## <a name="sizing-recommendations"></a>Zalecenia dotyczące zmiany rozmiaru

Witaj tabela zawiera podsumowanie zaleceń zmiany rozmiaru oparte na Procesorze.

**PROCESOR CPU** | **Pamięci** | **Rozmiar pamięci podręcznej dysku** | **Częstotliwość zmian danych** | **Chronione maszyny**
--- | --- | --- | --- | ---
8 Vcpu (2 sockets * 4 rdzenie @ 2,5 GHz [GHz]) | 16 GB | 300 GB | 500 GB lub mniej | Replikowanie maszyn mniej niż 100.
12 Vcpu (2 sockets * 6 rdzeni @ 2,5 GHz) | 18 GB | 600 GB | TB too1 500 GB | Replikują między 100 150 maszyn.
16 Vcpu (2 sockets * 8 rdzeni @ 2,5 GHz) | 32 GB | 1 TB | 1 TB too2 TB | Replikują między 150 – 200 maszyn.
Wdrażanie inny serwer przetwarzania | | | > 2 TB | Wdrażanie serwerów dodatkowych procesów, Jeśli replikujesz ponad 200 maszyn lub zmiana hello codzienne dane szybkość przekracza 2 TB.

Gdzie:

* Każda maszyna źródłowa jest skonfigurowany z 3 dyski 100 GB.
* My używamy najlepszymi magazynu 8 dysków SAS 10 k obr. / min, z RAID 10 dla pamięci podręcznej dysku pomiarów.

## <a name="process-server-capacity"></a>Pojemność serwera przetwarzania


serwer przetwarzania Hello odbiera dane replikacji z chronionych maszyn i optymalizuje je przy użyciu pamięci podręcznej, kompresji i szyfrowania. Wysyła następnie hello tooAzure danych.

- Hello procesu serwera maszyny ma wystarczające zasoby tooperform tych zadań.
- pierwszy serwer przetwarzania Hello jest instalowany domyślnie na powitania serwera konfiguracji. Tooscale serwery dodatkowych procesów można wdrożyć w środowisku.
- serwer przetwarzania Hello korzysta z pamięci podręcznej opartej na dysku. Użyj oddzielnych pamięci podręcznej dysku 600 GB lub więcej toohandle zmian danych przechowywanych w zdarzeniu hello wąskich gardeł lub awarii.
- Jeśli potrzebujesz tooprotect ponad 200 maszyn lub stawki dziennej zmiany hello jest większa niż 2 TB, można dodać procesu serwerów toohandle hello replikacji obciążenia. tooscale wychodzących, można:
    - Zwiększ liczbę hello serwery konfiguracji. Na przykład można chronić zapasowych too400 maszyn przy użyciu dwóch serwerów konfiguracji.
    - Dodawanie kolejnych serwerów procesu i użyć tych toohandle ruchu zamiast (lub oprócz) hello konfiguracji serwera.


### <a name="example-process-server-scaling"></a>Przykład procesu serwera skalowania

Witaj w poniższej tabeli opisano scenariusz, w którym:

* Nie planujesz toouse hello konfiguracji serwera jako serwera przetwarzania.
* Po skonfigurowaniu serwera dodatkowego przetwarzania.
* Skonfigurowano serwer przetwarzania dodatkowe hello toouse chronionych maszyn wirtualnych.
* Każda maszyna chronionego źródła jest skonfigurowany z trzech dysków 100 GB.

**Serwer konfiguracji** | **Serwer przetwarzania dodatkowe** | **Rozmiar pamięci podręcznej dysku** | **Częstotliwość zmian danych** | **Chronione maszyny**
--- | --- | --- | --- | ---
8 Vcpu (2 sockets * 4 rdzenie @ 2,5 GHz), 16 GB pamięci | 4 Vcpu (2 sockets * 2 rdzenie @ 2,5 GHz), 8 GB pamięci | 300 GB | 250 GB lub mniej | Replikowanie maszyn 85 lub mniej.
8 Vcpu (2 sockets * 4 rdzenie @ 2,5 GHz), 16 GB pamięci | 8 Vcpu (2 sockets * 4 rdzenie @ 2,5 GHz), 12 GB pamięci RAM | 600 GB | TB too1 250 GB | Replikują między 85 150 maszyny.
12 Vcpu (2 sockets * 6 rdzeni @ 2,5 GHz), 18 GB pamięci | 12 Vcpu (2 sockets * 6 rdzeni @ 2,5 GHz) 24 GB pamięci | 1 TB | 1 TB too2 TB | Replikują między 150 225 komputerów.

sposób Hello, w którym można skalować serwery zależy od swoich preferencji modelu skalowania w górę i skalowania w poziomie.  Skalowanie w górę przez wdrożenie kilku konfiguracje i serwerów procesu lub skalowanie w poziomie przez wdrożenie więcej serwerów z mniejszą liczbą zasobów. Na przykład tooprotect 220 maszyny, należy, wykonaj jedną z następujących hello:

* Konfigurowanie serwera konfiguracji hello 12 vCPU, 18 GB pamięci i serwera przetwarzania dodatkowych z 12 vCPU, 24 GB pamięci. Konfigurowanie chronione maszyny toouse hello dodatkowego procesu serwera tylko.
* Skonfiguruj dwa serwery konfiguracji (vCPU, 16 GB pamięci RAM 2 x 8) i dwa serwery dodatkowych procesów (vCPU 1 x 8 i 4 vCPU x 1 toohandle 135 + 85 [220] maszyny). Skonfiguruj chronione maszyny toouse hello procesu dodatkowe serwery tylko.

## <a name="deploy-additional-process-servers"></a>Wdrażanie serwerów dodatkowych procesów

1. Postępuj zgodnie z [tych instrukcji](site-recovery-vmware-setup-azure-ps-resource-manager.md) tooset serwera dodatkowych procesów.
2. Jeśli nie masz hasła hello Uruchom **[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe – n** na powitania konfiguracji serwera tooget go.
3. Po skonfigurowaniu serwera przetwarzania hello, migracja toouse maszyny źródłowej go.

    1. W **ustawienia** > **serwerów usługi Site Recovery**, kliknij serwer konfiguracji hello > **przetworzyć serwerów**.
    2. Kliknij prawym przyciskiem myszy serwer przetwarzania hello obecnie w użyciu > **przełącznika**.
    3. W **wybierz docelowy serwer przetwarzania**, wybierz serwer przetwarzania hello toouse, a następnie wybierz hello maszyn wirtualnych serwera hello będzie obsługiwać.
    4. Kliknij ikonę informacji o hello. toohelp należy załadować decyzji, hello średni miejsca na potrzeby tooreplicate każdej wybranej maszyny Wirtualnej toohello nowego serwera przetwarzania zostanie wyświetlony.
    5. Kliknij przycisk hello znacznik wyboru toostart replikacji toohello nowego serwera przetwarzania.

## <a name="control-network-bandwidth"></a>Sterowania przepustowością sieci

Po uruchomieniu [narzędzie wdrożenia Planistę hello](site-recovery-deployment-planner.md) toocalculate hello przepustowości wymagane dla replikacji (Replikacja początkowa hello i następnie delta), można kontrolować hello ilość przepustowości używanej w ramach replikacji przy użyciu kilku opcji:

* **Ograniczanie przepustowości**: VMware ruchu, który replikuje tooAzure przechodzi przez serwer określonego procesu. Możesz ograniczyć przepustowość na maszynach hello działających jako serwery procesu.
* **Wpływ przepustowości**: możesz wywrzeć wpływ hello przepustowość dla replikacji przy użyciu kilku kluczy rejestru:
  * Witaj **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\UploadThreadsPerVM** wartość rejestru określa hello liczbę wątków, które są używane do transferu danych (Replikacja początkowa lub przyrostowa) dysku. Wyższa wartość zwiększa przepustowość sieci hello używanych w przypadku replikacji.
  * Witaj **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\DownloadThreadsPerVM** określa hello liczbę wątków używanych do transferu danych podczas powrotu po awarii.

### <a name="throttle-bandwidth"></a>Ograniczanie przepustowości

1. Otwórz hello przystawki MMC kopia zapasowa Azure na powitania maszyny działania jako serwer przetwarzania hello. Domyślnie skrót do utworzenia kopii zapasowej jest pulpitu hello, lub w hello następującego folderu: C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. W przystawce hello, kliknij przycisk **Zmień właściwości**.
3. Na powitania **ograniczania** wybierz opcję **włączyć użycia przepustowości połączenia internetowego do operacji tworzenia kopii zapasowej**.
4. Ustaw limity hello do pracy oraz innych niż godziny pracy. Prawidłowe zakresy są od 512 KB/s too102 MB/s na sekundę.

    ![Ograniczenie](./media/physical-walkthrough-capacity/throttle2.png)

Można również użyć hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) ograniczania tooset polecenia cmdlet. Oto przykład:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** wskazuje, że ograniczanie przepływności nie jest wymagane.

### <a name="influence-network-bandwidth-for-a-vm"></a>Wpływ na przepustowość sieci dla maszyny Wirtualnej

1. W rejestrze hello maszyny Wirtualnej, przejdź zbyt**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.
   * tooinfluence hello przepustowości ruchu replikacji dysku, zmodyfikuj wartość hello **UploadThreadsPerVM**, lub Utwórz klucz hello, jeśli nie istnieje.
   * tooinfluence hello przepustowości dla ruchu powrotu po awarii z platformy Azure, zmodyfikuj wartość hello **DownloadThreadsPerVM**.
2. Witaj, wartość domyślna to 4. W sieci o nadmiarowych zasobach można zmodyfikować te klucze rejestru. Witaj maksymalna to 32. Monitorowanie ruchu toooptimize hello wartość.




## <a name="next-steps"></a>Następne kroki

Przejdź za[krok 4: Planowanie sieci](physical-walkthrough-network.md).
