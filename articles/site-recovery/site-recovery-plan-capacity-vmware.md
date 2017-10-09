---
title: "aaaPlan wydajności i skalowania dla tooAzure replikacji VMware z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Użyj tego artykułu tooplan pojemności i skali, podczas replikowania maszyn wirtualnych VMware tooAzure z usługą Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 0a1cd8eb-a8f7-4228-ab84-9449e0b2887b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/24/2017
ms.author: rayne
ms.openlocfilehash: 7ca9147d1b4611f6b4a67c3de3f27fb9878f4c4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="plan-capacity-and-scaling-for-vmware-replication-with-azure-site-recovery"></a>Planowanie wydajności i skalowania w przypadku replikacji maszyn wirtualnych VMware z usługą Azure Site Recovery

Użyj tego artykułu toofigure Planowanie pojemności i skalowanie podczas replikowania lokalnych maszyn wirtualnych VMware i serwery fizyczne tooAzure z [usługi Azure Site Recovery](site-recovery-overview.md).

## <a name="how-do-i-start-capacity-planning"></a>Jak rozpocząć planowanie pojemności

Zbierz informacje o środowisku replikacji, uruchamiając hello [Azure lokacji odzyskiwania wdrożenia Planistę](https://aka.ms/asr-deployment-planner-doc) dla replikacji maszyn wirtualnych VMware. [Dowiedz się więcej](site-recovery-deployment-planner.md) o tym narzędziu. Będzie zbierać informacje o zgodnych i niezgodnych maszyn wirtualnych, dysków dla maszyny Wirtualnej, a danych churn — na dysku. Narzędzie Hello obejmuje również wymagania dotyczące przepustowości sieci i hello Azure infrastrukturę potrzebną dla pracę w trybie failover replikacji i testowania.

## <a name="capacity-considerations"></a>Zagadnienia dotyczące wydajności

**Składnik** | **Szczegóły** |
--- | --- | ---
**Replikacja** | **Maksymalna szybkość codziennych zmian:** chronionej maszyny można używać tylko jednego serwera przetwarzania i serwer pojedynczego procesu może obsługiwać codzienne szybkość zmian w górę too2 TB. W związku z tym 2 TB jest hello, codzienne dane zmienić szybkość, z której jest obsługiwana dla komputera chronionego.<br/><br/> **Maksymalna przepustowość:** zreplikowanej maszyny mogą należeć tooone konta magazynu na platformie Azure. Konto magazynu w warstwie standardowa może obsługiwać maksymalnie 20 000 żądań na sekundę, i zaleca się utrzymać hello liczba operacji wejścia/wyjścia na sekundę (IOPS) dla too20 maszyny źródłowej, 000. Na przykład jeśli masz maszyny źródłowej z dyskami 5, a każdy dysk generuje 120 IOPS (rozmiarze 8 KB) na maszynie źródłowej hello, następnie będzie w hello Azure limitu IOPS dysku 500. (hello liczba kont magazynu wymagana jest równy toohello maszyny źródłowej całkowita IOPS, podzielona przez 20 000).
**Serwer konfiguracji** | Serwer konfiguracji Hello powinien być stanie toohandle hello codziennych zmian szybkość pojemności we wszystkich obciążeń uruchomionych na chronionych komputerach i musi wystarczającą przepustowość toocontinuously replikowany tooAzure danych magazynu.<br/><br/> Najlepszym rozwiązaniem, zlokalizować hello konfiguracji serwera na powitania tej samej sieci, a segment sieci LAN jako hello maszyn, które mają tooprotect. Może znajdować się na inną sieć, ale ma tooprotect powinny mieć warstwy 3 sieci widoczność tooit maszyny.<br/><br/> Zalecenia dotyczące rozmiaru na powitania serwera konfiguracji są podsumowane w tabeli hello w hello następujących sekcji.
**Serwer przetwarzania** | pierwszy serwer przetwarzania Hello jest instalowany domyślnie na powitania serwera konfiguracji. Tooscale serwery dodatkowych procesów można wdrożyć w środowisku. <br/><br/> serwer przetwarzania Hello odbiera dane replikacji z chronionych maszyn i optymalizuje je przy użyciu pamięci podręcznej, kompresji i szyfrowania. Wysyła następnie hello tooAzure danych. Hello procesu serwera maszyny ma wystarczające zasoby tooperform tych zadań.<br/><br/> serwer przetwarzania Hello korzysta z pamięci podręcznej opartej na dysku. Użyj oddzielnych pamięci podręcznej dysku 600 GB lub więcej toohandle zmian danych przechowywanych w zdarzeniu hello wąskich gardeł lub awarii.

## <a name="size-recommendations-for-hello-configuration-server"></a>Zalecenia dotyczące rozmiaru hello konfiguracji serwera

**PROCESOR CPU** | **Pamięci** | **Rozmiar pamięci podręcznej dysku** | **Częstotliwość zmian danych** | **Chronione maszyny**
--- | --- | --- | --- | ---
8 Vcpu (2 sockets * 4 rdzenie @ 2,5 GHz [GHz]) | 16 GB | 300 GB | 500 GB lub mniej | Replikowanie maszyn mniej niż 100.
12 Vcpu (2 sockets * 6 rdzeni @ 2,5 GHz) | 18 GB | 600 GB | TB too1 500 GB | Replikują między 100 150 maszyn.
16 Vcpu (2 sockets * 8 rdzeni @ 2,5 GHz) | 32 GB | 1 TB | 1 TB too2 TB | Replikują między 150 – 200 maszyn.
Wdrażanie inny serwer przetwarzania | | | > 2 TB | Wdrażanie serwerów dodatkowych procesów, Jeśli replikujesz ponad 200 maszyn lub zmiana hello codzienne dane szybkość przekracza 2 TB.

Gdzie:

* Każda maszyna źródłowa jest skonfigurowany z 3 dyski 100 GB.
* My używamy najlepszymi magazynu 8 dysków SAS 10 k obr. / min, z RAID 10 dla pamięci podręcznej dysku pomiarów.

## <a name="size-recommendations-for-hello-process-server"></a>Zalecenia dotyczące rozmiaru na powitania serwera przetwarzania

Jeśli potrzebujesz tooprotect ponad 200 maszyn lub stawki dziennej zmiany hello jest większa niż 2 TB, można dodać procesu serwerów toohandle hello replikacji obciążenia. tooscale wychodzących, można:

* Zwiększ liczbę hello serwery konfiguracji. Na przykład można chronić zapasowych too400 maszyn przy użyciu dwóch serwerów konfiguracji.
* Dodawanie kolejnych serwerów procesu i użyć tych toohandle ruchu zamiast (lub oprócz) hello konfiguracji serwera.

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


## <a name="control-network-bandwidth"></a>Sterowania przepustowością sieci

Po używano hello [narzędzie wdrożenia Planistę hello](site-recovery-deployment-planner.md) toocalculate hello przepustowości wymagane dla replikacji (Replikacja początkowa hello i następnie delta), można kontrolować hello ilość przepustowości używanej w ramach replikacji przy użyciu kilku opcje:

* **Ograniczanie przepustowości**: VMware ruchu, który replikuje tooAzure przechodzi przez serwer określonego procesu. Możesz ograniczyć przepustowość na maszynach hello działających jako serwery procesu.
* **Wpływ przepustowości**: możesz wywrzeć wpływ hello przepustowość dla replikacji przy użyciu kilku kluczy rejestru:
  * Witaj **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\UploadThreadsPerVM** wartość rejestru określa hello liczbę wątków, które są używane do transferu danych (Replikacja początkowa lub przyrostowa) dysku. Wyższa wartość zwiększa przepustowość sieci hello używanych w przypadku replikacji.
  * Witaj **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\DownloadThreadsPerVM** określa hello liczbę wątków używanych do transferu danych podczas powrotu po awarii.

### <a name="throttle-bandwidth"></a>Ograniczanie przepustowości

1. Otwórz hello przystawki MMC kopia zapasowa Azure na powitania maszyny działania jako serwer przetwarzania hello. Domyślnie skrót do utworzenia kopii zapasowej jest pulpitu hello, lub w hello następującego folderu: C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. W przystawce hello, kliknij przycisk **Zmień właściwości**.

    ![Zrzut ekranu Azure Backup MMC przystawki opcja toochange właściwości](./media/site-recovery-vmware-to-azure/throttle1.png)
3. Na powitania **ograniczania** wybierz opcję **włączyć użycia przepustowości połączenia internetowego do operacji tworzenia kopii zapasowej**. Ustaw limity hello do pracy oraz innych niż godziny pracy. Prawidłowe zakresy są od 512 KB/s too102 MB/s na sekundę.

    ![Okno dialogowe zrzut ekranu Azure Backup właściwości](./media/site-recovery-vmware-to-azure/throttle2.png)

Można również użyć hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) ograniczania tooset polecenia cmdlet. Oto przykład:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** wskazuje, że ograniczanie przepływności nie jest wymagane.

### <a name="influence-network-bandwidth-for-a-vm"></a>Wpływ na przepustowość sieci dla maszyny Wirtualnej

1. W rejestrze hello maszyny Wirtualnej, przejdź zbyt**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.
   * tooinfluence hello przepustowości ruchu replikacji dysku, zmodyfikuj wartość hello **UploadThreadsPerVM**, lub Utwórz klucz hello, jeśli nie istnieje.
   * tooinfluence hello przepustowości dla ruchu powrotu po awarii z platformy Azure, zmodyfikuj wartość hello **DownloadThreadsPerVM**.
2. Witaj, wartość domyślna to 4. W sieci "o nadmiarowych zasobach" należy zmienić te klucze rejestru hello wartości domyślnych. Witaj maksymalna to 32. Monitorowanie ruchu toooptimize hello wartość.


## <a name="deploy-additional-process-servers"></a>Wdrażanie serwerów dodatkowych procesów

Jeśli masz tooscale limit wdrożenia ponad 200 maszyn źródłowych lub łączna codziennie churn — liczba więcej niż 2 TB, należy procesu dodatkowe serwery toohandle hello ruchu woluminu. Wykonaj te instrukcje tooset hello procesu serwera. Po skonfigurowaniu serwera hello, migracja toouse maszyny źródłowej go.

1. W **serwerów usługi Site Recovery**, kliknij hello konfiguracji serwera, a następnie kliknij przycisk **serwera przetwarzania**.

    ![Zrzut ekranu usługi Site Recovery serwerów opcja tooadd serwera przetwarzania](./media/site-recovery-vmware-to-azure/migrate-ps1.png)
2. W **typ serwera**, kliknij przycisk **serwera przetwarzania (lokalnego)**.

    ![Zrzut ekranu serwera przetwarzania, okno dialogowe](./media/site-recovery-vmware-to-azure/migrate-ps2.png)
3. Pobierz plik Instalatora Unified usługi Site Recovery hello i uruchom go tooinstall hello procesu serwera. To również rejestruje go w magazynie hello.
4. W **przed rozpoczęciem**, wybierz pozycję **dodać dodatkowych procesów serwerów tooscale limit wdrożenia**.
5. Kreator pełną hello w hello taki sam sposób jak podczas możesz [Konfigurowanie](#step-2-set-up-the-source-environment) powitania serwera konfiguracji.

    ![Zrzut ekranu z Instalatora Azure Site Recovery Unified Kreatora](./media/site-recovery-vmware-to-azure/add-ps1.png)
6. W **szczegóły konfiguracji serwera**Określ adres IP hello hello konfiguracji serwera, a hello hasło. hasło hello tooobtain, uruchom **[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe – n** na powitania serwera konfiguracji.

    ![Zrzut ekranu konfiguracji szczegóły serwera strony](./media/site-recovery-vmware-to-azure/add-ps2.png)

### <a name="migrate-machines-toouse-hello-new-process-server"></a>Migrowanie maszyn toouse hello nowego serwera przetwarzania
1. W **ustawienia** > **serwerów usługi Site Recovery**kliknij hello konfiguracji serwera, a następnie rozwiń węzeł **przetworzyć serwerów**.

    ![Zrzut ekranu serwera przetwarzania, okno dialogowe](./media/site-recovery-vmware-to-azure/migrate-ps2.png)
2. Kliknij prawym przyciskiem myszy serwer przetwarzania hello obecnie w użyciu, a następnie kliknij przycisk **przełącznika**.

    ![Zrzut ekranu konfiguracji serwera, okno dialogowe](./media/site-recovery-vmware-to-azure/migrate-ps3.png)
3. W **wybierz docelowy serwer przetwarzania**, wybierz pozycję hello nowego serwera przetwarzania mają toouse, a następnie wybierz maszyny wirtualne powitania serwera hello będzie obsługiwać. Kliknij przycisk hello informacji ikona tooget informacji o serwerze hello. toohelp należy załadować decyzji, hello średni miejsca na potrzeby tooreplicate każdego nowego serwera przetwarzania wybraną maszynę wirtualną toohello jest wyświetlany. Kliknij przycisk toostart znacznik wyboru hello replikowanie toohello nowego serwera przetwarzania.


## <a name="next-steps"></a>Następne kroki

Pobierz i uruchom hello [Azure lokacji odzyskiwania wdrożenia Planistę](https://aka.ms/asr-deployment-planner)
