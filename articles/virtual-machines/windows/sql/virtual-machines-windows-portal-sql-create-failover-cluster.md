---
title: aaaSQL Server FCI - maszynach wirtualnych platformy Azure | Dokumentacja firmy Microsoft
description: "W tym artykule opisano sposób toocreate wystąpienie klastra pracy awaryjnej programu SQL Server na maszynach wirtualnych platformy Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 9fc761b1-21ad-4d79-bebc-a2f094ec214d
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: bee3b27805c5f6cc02a43b25d480c129c254cb90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a>Skonfiguruj wystąpienie klastra pracy awaryjnej programu SQL Server na maszynach wirtualnych Azure

W tym artykule opisano, jak toocreate programu SQL Server klastra trybu Failover wystąpienia (FCI), maszynach wirtualnych Azure w modelu usługi Resource Manager. To rozwiązanie wymaga [systemu Windows Server 2016 Datacenter edition bezpośrednie miejsca do magazynowania \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) jako opartych na oprogramowaniu wirtualnej sieci SAN synchronizujący hello magazynu (dysków danych) między hello węzłach (maszynach wirtualnych platformy Azure) Klaster systemu Windows. S2D stanowi nowość w systemie Windows Server 2016.

Witaj Poniższy diagram przedstawia kompletnego rozwiązania hello na maszynach wirtualnych Azure:

![Grupy dostępności](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

Witaj poprzedzających diagramie przedstawiono:

- Dwóch maszyn wirtualnych platformy Azure w klastrze pracy awaryjnej systemu Windows. Maszyna wirtualna jest w klastrze pracy awaryjnej jest również nazywany *węzła klastra*, lub *węzłów*.
- Każda maszyna wirtualna ma co najmniej dwa dyski danych.
- S2D synchronizuje dane hello na dysku danych hello i przedstawia magazynu hello synchronizowane jako puli magazynów.
- puli magazynu Hello przedstawia klastra pracy awaryjnej toohello (CSV) woluminu udostępnionego klastra.
- rolę klastra programu SQL Server FCI Hello używa hello CSV hello dysków z danymi.
- Azure adres usługi równoważenia obciążenia toohold hello IP dla hello SQL Server FCI.
- Zestaw dostępności Azure zawiera wszystkie zasoby hello.

   >[!NOTE]
   >Wszystkie zasoby platformy Azure są na diagramie hello w hello tej samej grupie zasobów.

Aby uzyskać szczegółowe informacje o S2D, zobacz [systemu Windows Server 2016 Datacenter edition bezpośrednie miejsca do magazynowania \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).

S2D obsługuje dwa typy architektury - konwergentnej i hiperkonwergentnych. Architektura Hello w tym dokumencie jest hiperkonwergentnych. Hiperkonwergentnych infrastruktury magazynu hello miejsca na hello samych serwerów w tej aplikacji hello w klastrze hosta. W ramach tej architektury magazynu hello jest w każdym węźle SQL Server FCI.

### <a name="example-azure-template"></a>Przykład szablonu Azure

Można utworzyć hello całego rozwiązania na platformie Azure w ramach szablonu. Przykład szablonu jest dostępny w hello GitHub [szablonów Szybki Start Azure](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad). W tym przykładzie nie jest przeznaczona lub sprawdzane pod kątem żadnych określonego obciążenia. Możesz uruchomić toocreate szablonu hello FCI serwera SQL z S2D magazynu podłączonego tooyour domeny. Ocena hello szablonu i zmodyfikuj go do własnych celów.

## <a name="before-you-begin"></a>Przed rozpoczęciem

Jest kilka rzeczy, przed kontynuowaniem należy tooknow i kilka rzeczy, które są potrzebne w miejscu.

### <a name="what-tooknow"></a>Jakie tooknow
Musisz mieć operacyjne zrozumienia hello następujące technologie:

- [Technologie klastra systemu Windows](http://technet.microsoft.com/library/hh831579.aspx)
-  [Wystąpienia klastra trybu Failover programu SQL Server](http://msdn.microsoft.com/library/ms189134.aspx).

Ponadto musisz mieć ogólną wiedzą hello następujące technologie:

- [Zbieżność Hyper rozwiązania przy użyciu bezpośrednie miejsca do magazynowania w systemie Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [Grup zasobów platformy Azure](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-toohave"></a>Jakie toohave

Przed rozpoczęciem powitalne instrukcje w tym artykule, należy:

- Subskrypcja Microsoft Azure.
- Domena systemu Windows na maszynach wirtualnych Azure.
- Konto z obiektami toocreate uprawnień w hello maszyny wirtualnej platformy Azure.
- Sieć wirtualna platformy Azure i podsieci z wystarczającą przestrzenią adresów IP dla hello następujące składniki:
   - Obydwie maszyny wirtualne.
   - Witaj adres IP klastra pracy awaryjnej.
   - Adres IP dla każdego infrastruktury klasyfikacji plików.
- DNS skonfigurowane na powitania sieci Azure, wskazując toohello kontrolerów domeny.

Z tych wymagań wstępnych w miejscu można kontynuować tworzenie klastra trybu failover. pierwszym krokiem Hello jest maszyn wirtualnych hello toocreate.

## <a name="step-1-create-virtual-machines"></a>Krok 1: Tworzenie maszyn wirtualnych

1. Zaloguj się za toohello [portalu Azure](http://portal.azure.com) w ramach subskrypcji.

1. [Tworzenie zestawu dostępności Azure](../tutorial-availability-sets.md).

   dostępność Hello ustawienia grupy maszyn wirtualnych w domenach awarii lub uaktualnienia domen. zestaw dostępności Hello upewnia się, że aplikacja nie ma wpływu na pojedyncze punkty awarii, takie jak przełącznik sieci hello lub jednostki zasilania hello stojak serwerów.

   Jeśli nie utworzono hello grupy zasobów dla maszyn wirtualnych, należy to zrobić, podczas tworzenia zestawu dostępności Azure. Jeśli używasz zestaw dostępności hello Azure toocreate portalu hello hello następujące kroki:

   - W portalu Azure hello, kliknij przycisk  **+**  tooopen hello Azure Marketplace. Wyszukaj **zestawu dostępności**.
   - Kliknij przycisk **zestawu dostępności**.
   - Kliknij przycisk **Utwórz**.
   - Na powitania **tworzenia zestawu dostępności** bloku hello ustaw następujące wartości:
      - **Nazwa**: Nazwa zestawu dostępności hello.
      - **Subskrypcja**: Azure Twojej subskrypcji.
      - **Grupa zasobów**: toouse istniejącą grupę, kliknij przycisk **Użyj istniejącego** i hello wybierz grupę z listy rozwijanej hello. W przeciwnym razie wybierz **Utwórz nowy** i wpisz nazwę grupy hello.
      - **Lokalizacja**: Ustaw lokalizację hello, w którym planujesz toocreate maszyn wirtualnych.
      - **Odporność domen**: używanie domyślnych hello (3).
      - **Aktualizowanie domeny**: Użyj domyślnej hello [5].
   - Kliknij przycisk **Utwórz** zestawu dostępności hello toocreate.

1. Tworzenie maszyn wirtualnych hello hello zestawu dostępności.

   Umieszczanie dwóch maszyn wirtualnych programu SQL Server w zestawie dostępności Azure hello. Aby uzyskać instrukcje, zobacz [Aprowizowanie maszyny wirtualnej programu SQL Server w portalu Azure hello](virtual-machines-windows-portal-sql-server-provision.md).

   Umieść obydwie maszyny wirtualne:

   - W hello zestawu dostępności z tej samej grupy zasobów platformy Azure jest w.
   - Na powitania sam sieci jako kontroler domeny.
   - W podsieci z wystarczającą przestrzenią adresów IP dla maszyn wirtualnych i wszystkie wystąpienia, które użytkownik może użyć w tym klastrze.
   - W zestawie dostępności Azure hello.   

      >[!IMPORTANT]
      >Nie można ustawić lub zmienić dostępności ustawić po utworzeniu maszyny wirtualnej.

   Wybierz obraz z hello Azure Marketplace. Korzystając z witryny Marketplace zawiera obraz z tym systemu Windows Server i SQL Server lub po prostu hello systemu Windows Server. Aby uzyskać więcej informacji, zobacz [Omówienie programu SQL Server na maszynach wirtualnych platformy Azure](../../virtual-machines-windows-sql-server-iaas-overview.md)

   Hello oficjalnego obrazów programu SQL Server w galerii Azure hello obejmują zainstalowane wystąpienie programu SQL Server, oraz oprogramowanie instalacyjne programu SQL Server hello i hello wymaganego klucza.

   Wybierz obraz prawym hello zgodnie z toohow, który ma toopay hello licencję programu SQL Server:

   - **Należy zwrócić na użycie licencjonowania**: hello na minutę koszt tych obrazów obejmuje hello licencjonowania programu SQL Server:
      - **SQL Server 2016 przedsiębiorstwa w systemie Windows Server Datacenter 2016**
      - **SQL Server 2016 Standard w systemie Windows Server Datacenter 2016**
      - **SQL Server 2016 Developer w systemie Windows Server Datacenter 2016**

   - **Przełącz your właścicielem licencji (BYOL)**

      - **{BYOL} SQL Server 2016 przedsiębiorstwa w systemie Windows Server Datacenter 2016**
      - **{BYOL} SQL Server 2016 Standard w systemie Windows Server Datacenter 2016**

   >[!IMPORTANT]
   >Po utworzeniu maszyny wirtualnej hello, należy usunąć wystąpienia programu SQL Server zainstalowane wcześniej autonomiczne hello. Po skonfigurowaniu klastra trybu failover hello i S2D użyjesz hello wstępnie zainstalowane programu SQL Server nośnika toocreate hello SQL Server FCI.

   Alternatywnie można użyć obrazów Azure Marketplace właśnie hello systemu operacyjnego. Wybierz **systemu Windows Server 2016 Datacenter** obrazu i zainstaluj hello SQL Server FCI, po skonfigurowaniu klastra trybu failover hello i S2D. Ten obraz zawiera nośnik instalacyjny programu SQL Server. Umieść nośnik instalacyjny hello w lokalizacji, w której można uruchamiać hello instalacji programu SQL Server dla każdego serwera.

1. Po Azure utworzy maszyn wirtualnych, należy połączyć tooeach maszyny wirtualnej z protokołem RDP.

   Podczas pierwszego łączenia tooa maszyny wirtualnej z protokołem RDP, komputer hello pyta użytkownika tooallow toobe tego komputera wykrywalny hello sieci. Kliknij przycisk **Yes** (Tak).

1. Jeśli jeden z obrazów maszyny wirtualnej na serwerze SQL hello są używane, należy usunąć hello wystąpienia programu SQL Server.

   - W **programy i funkcje**, kliknij prawym przyciskiem myszy **Microsoft SQL Server 2016 (64-bitowy)** i kliknij przycisk **Odinstaluj/Zmień**.
   - Kliknij przycisk **Usuń**.
   - Wybierz wystąpienie domyślne hello.
   - Usuwanie wszystkich funkcji w obszarze **usługi aparatu bazy danych**. Nie usuwaj **wspólne funkcje**. Zobacz hello poniższej ilustracji:

      ![Usuwanie funkcji](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - Kliknij przycisk **dalej**, a następnie kliknij przycisk **Usuń**.

1. <a name="ports"></a>Otwórz porty zapory hello.

   Na każdej maszynie wirtualnej Otwórz hello następujących portów w Zaporze systemu Windows hello.

   | Przeznaczenie | TCP Port | Uwagi
   | ------ | ------ | ------
   | Oprogramowanie SQL Server | 1433 | Normalne port dla domyślnego wystąpienia programu SQL Server. Jeśli używasz obrazu z galerii hello ten port jest automatycznie otwierane.
   | Badania kondycji | 59999 | Wszelkie Otwórz TCP port. W kolejnym kroku, należy skonfigurować usługi równoważenia obciążenia hello [sondy kondycji](#probe) i hello toouse klastra tego portu.  

1. Dodaj maszynę wirtualną toohello magazynu. Aby uzyskać szczegółowe informacje, zobacz [dodać magazyn](../../../storage/common/storage-premium-storage.md).

   Dane co najmniej dwa dyski należy obie maszyny wirtualne.

   Dołącz raw dyski - dysków sformatowanych nie systemu plików NTFS.
      >[!NOTE]
      >Po dołączeniu dyski sformatowane przy użyciu systemu plików NTFS, można włączyć tylko S2D z bez sprawdzania kwalifikujące dysku.  

   Dołącz co najmniej dwóch tooeach magazyn w warstwie Premium (SSD dyski) maszyny Wirtualnej. Zaleca się co najmniej P30 dysków (1 TB).

   Zbyt buforowania hosta zestawu**tylko do odczytu**.

   pojemność magazynu Hello używanego w środowiskach produkcyjnych zależy od obciążenia. wartości Hello opisanych w tym artykule dotyczą pokazu i testowania.

1. [Dodawanie domeny istniejące hello maszyn wirtualnych tooyour](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).

Po hello maszyny wirtualne są tworzone i skonfigurowany, można skonfigurować hello klastra pracy awaryjnej.

## <a name="step-2-configure-hello-windows-failover-cluster-with-s2d"></a>Krok 2: Konfigurowanie klastra trybu Failover systemu Windows hello z S2D

Witaj następnym krokiem jest klaster trybu failover hello tooconfigure S2D. W tym kroku będziesz wykonywać hello następujących podetapów:

1. Dodaj funkcję Klaster pracy awaryjnej systemu Windows
1. Sprawdzanie poprawności klastra hello
1. Tworzenie klastra pracy awaryjnej hello
1. Tworzenie monitora chmury hello
1. Dodawanie magazynu

### <a name="add-windows-failover-clustering-feature"></a>Dodaj funkcję Klaster pracy awaryjnej systemu Windows

1. toobegin, Połącz toohello pierwszej maszyny wirtualnej z protokołem RDP przy użyciu konta domeny, które jest członkiem grupy administratorów lokalnych i ma uprawnienia toocreate obiektów w usłudze Active Directory. Konto służy do reszty hello hello konfiguracji.

1. [Dodaj klaster trybu Failover maszyny wirtualnej funkcji tooeach](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).

   Funkcja Klaster pracy awaryjnej tooinstall z interfejsu użytkownika, powitalne hello następujące kroki na obu maszynach wirtualnych.
   - W **Menedżera serwera**, kliknij przycisk **Zarządzaj**, a następnie kliknij przycisk **Dodaj role i funkcje**.
   - W **Kreatora dodawania ról i funkcji**, kliknij przycisk **dalej** do momentu uzyskania zbyt**Wybieranie funkcji**.
   - W **Wybieranie funkcji**, kliknij przycisk **klaster pracy awaryjnej**. Obejmują wszystkie wymagane funkcje i narzędzia do zarządzania hello. Kliknij przycisk **dodawania funkcji**.
   - Kliknij przycisk **dalej** , a następnie kliknij przycisk **Zakończ** tooinstall hello funkcji.

   tooinstall hello funkcji Klaster trybu Failover przy użyciu programu PowerShell, uruchom hello następującego skryptu z sesji programu PowerShell administratora na jednym hello maszyn wirtualnych.

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

Odwołania, kolejne kroki hello wykonaj instrukcje hello w kroku 3 [zbieżność Hyper rozwiązania przy użyciu bezpośrednie miejsca do magazynowania w systemie Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).

### <a name="validate-hello-cluster"></a>Sprawdzanie poprawności klastra hello

Ten przewodnik odwołuje się tooinstructions w obszarze [weryfikacji klastra](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).

Sprawdzanie poprawności klastra hello hello interfejsu użytkownika lub przy użyciu programu PowerShell.

klaster hello toovalidate z interfejsu użytkownika, powitalne hello następujące kroki z jednej z maszyn wirtualnych hello.

1. W **Menedżera serwera**, kliknij przycisk **narzędzia**, następnie kliknij przycisk **Menedżera klastra trybu Failover**.
1. W **Menedżera klastra trybu Failover**, kliknij przycisk **akcji**, następnie kliknij przycisk **Sprawdź poprawność konfiguracji...** .
1. Kliknij przycisk **Dalej**.
1. Na **Wybieranie serwerów lub klastrów**, nazwa typu hello zarówno maszyn wirtualnych.
1. Na **opcji testowania**, wybierz **uruchamianie tylko testów I wybrać**. Kliknij przycisk **Dalej**.
1. Na **Test wybór**, obejmują wszystkich testów oprócz **magazynu**. Zobacz hello poniższej ilustracji:

   ![Zweryfikuj testy](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. Kliknij przycisk **Dalej**.
1. Na **potwierdzenie**, kliknij przycisk **dalej**.

Witaj **Kreator weryfikacji konfiguracji** uruchamia hello testów sprawdzania poprawności.

toovalidate hello klastra przy użyciu programu PowerShell, uruchom hello następującego skryptu z sesji programu PowerShell administratora na jednym hello maszyn wirtualnych.

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

Po sprawdzania poprawności klastra hello utworzyć hello klastra pracy awaryjnej.

### <a name="create-hello-failover-cluster"></a>Tworzenie klastra pracy awaryjnej hello

Ten przewodnik odwołuje się zbyt[Utwórz klaster pracy awaryjnej hello](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).

toocreate hello klastra pracy awaryjnej, potrzebne są:
- nazwy Hello hello maszyn wirtualnych, które stają się hello węzłów klastra.
- Nazwa klastra trybu failover hello
- Adres IP dla klastra trybu failover hello. Adres IP, który nie jest używany na powitania można użyć tej samej sieci wirtualnej platformy Azure i podsieć, jak hello węzłów klastra.

Witaj następującego środowiska PowerShell tworzy klastra pracy awaryjnej. Aktualizacja hello skryptu z nazwami hello hello węzłów (hello nazwy maszyny wirtualnej) i dostępny adres IP z hello sieci Wirtualnej platformy Azure:

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a>Tworzenie monitora chmury

Monitor chmury jest nowy typ monitora kworum klastra przechowywane w obiekcie Blob magazynu Azure. To eliminuje potrzebę hello oddzielne hosting udziału monitora maszyny wirtualnej.

1. [Tworzenie chmury monitora dla klastra trybu failover hello](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).

1. Tworzenie kontenera obiektów blob.

1. Zapisz hello klucze dostępu i hello adresu URL kontenera.

1. Skonfiguruj Monitor kworum klastra klastra pracy awaryjnej hello. Zobacz [Konfiguruj hello monitora kworum w interfejsie użytkownika hello]. (http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) w hello interfejsu użytkownika.

### <a name="add-storage"></a>Dodawanie magazynu

dyski Hello S2D muszą toobe pusty i bez partycji lub innych danych. Wykonaj dysków tooclean [hello kroków w tym przewodniku](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).

1. [Włącz sklepu odstępów bezpośrednio \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).

   Witaj następującego środowiska PowerShell umożliwia bezpośrednie miejsca do magazynowania.  

   ```PowerShell
   Enable-ClusterS2D
   ```

   W **Menedżera klastra trybu Failover**, możesz teraz przeglądać hello puli magazynu.

1. [Tworzenie woluminu](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).

   Jedną z funkcji hello S2D jest on automatycznie tworzona jest pula magazynu po jej włączeniu. Wszystko jest teraz gotowy toocreate woluminu. Witaj polecenia programu PowerShell `New-Volume` automatyzuje proces tworzenia woluminu hello oraz formatowanie, dodawanie toohello klastra i utworzenie udostępnionego woluminu klastra (CSV). Witaj poniższy przykład tworzy 800 gigabajt (GB) CSV.

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   Po wykonaniu tego polecenia, jako zasób klastra został zainstalowany wolumin 800 GB. wolumin Hello jest na `C:\ClusterStorage\Volume1\`.

   powitania po diagram przedstawia udostępniony wolumin klastra z S2D:

   ![ClusterSharedVolume](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a>Krok 3: Testowanie trybu failover klastra trybu failover

W Menedżerze klastra trybu Failover Sprawdź, czy można przenieść toohello zasobów magazynu hello innym węźle klastra. Jeśli można połączyć toohello trybu failover klaster z **Menedżera klastra trybu Failover** i przeniesienie magazynu hello z jednego węzła toohello innych, są gotowe tooconfigure hello infrastruktury klasyfikacji plików.

## <a name="step-4-create-sql-server-fci"></a>Krok 4: Tworzenie programu SQL Server infrastruktury klasyfikacji plików

Po skonfigurowaniu klastra trybu failover hello i wszystkie składniki klastra, łącznie z magazynem, można utworzyć hello SQL Server FCI.

1. Połącz toohello pierwszej maszyny wirtualnej z protokołem RDP.

1. W **Menedżera klastra trybu Failover**, upewnij się, że wszystkie zasoby podstawowe klastra znajdują się na pierwszej maszynie wirtualnej hello. Jeśli to konieczne, Przenieś wszystkie maszyny wirtualnej toothis zasobów.

1. Zlokalizuj hello nośnika instalacyjnego. Jeśli maszyna wirtualna hello używa jednego z obrazów Azure Marketplace hello, hello nośnika znajduje się pod adresem `C:\SQLServer_<version number>_Full`. Kliknij przycisk **Instalatora**.

1. W hello **Centrum instalacji programu SQL Server**, kliknij przycisk **instalacji**.

1. Kliknij przycisk **instalacji klastra pracy awaryjnej nowy serwer SQL**. Wykonaj instrukcje hello hello kreatora tooinstall hello SQL Server FCI.

   katalogi danych FCI Hello muszą toobe w magazynie klastra. Z S2D nie jest udostępniony dysk, ale tooa punktu instalacji woluminu na każdym serwerze. S2D synchronizuje woluminu hello między obu węzłów. wolumin Hello są prezentowane toohello klastra jako udostępniony wolumin klastra. Użyj punktu instalacji woluminu CSV hello hello danych katalogów.

   ![DataDirectories](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. Po zakończeniu pracy Kreatora hello Instalator zainstaluje na pierwszym węźle hello FCI serwera SQL.

1. Po zainstalowaniu Instalator pomyślnie hello infrastruktury klasyfikacji plików na pierwszym węźle hello Uzyskuj dostęp do drugiego węzła toohello RDP.

1. Otwórz hello **Centrum instalacji programu SQL Server**. Kliknij przycisk **instalacji**.

1. Kliknij przycisk **klastra pracy awaryjnej programu SQL Server Dodaj węzeł tooa**. Wykonaj te instrukcje hello hello kreatora tooinstall programu SQL server, a następnie dodaj ten toohello serwera infrastruktury klasyfikacji plików.

   >[!NOTE]
   >Jeśli używasz obrazu galerii Azure Marketplace z programem SQL Server, narzędzia programu SQL Server zostały zawarte w hello obrazu. Jeśli nie używasz tego obrazu, hello narzędzia SQL Server należy zainstalować oddzielnie. Zobacz [pobierania programu SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).

## <a name="step-5-create-azure-load-balancer"></a>Krok 5: Tworzenie usługi równoważenia obciążenia Azure

Na maszynach wirtualnych Azure klastrom toohold usługi równoważenia obciążenia adres IP, który wymaga toobe na jednym węźle klastra w czasie. W tym rozwiązaniu usługi równoważenia obciążenia hello zawiera adres IP hello hello SQL Server FCI.

[Tworzenie i konfigurowanie usługi równoważenia obciążenia Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).

### <a name="create-hello-load-balancer-in-hello-azure-portal"></a>Tworzenie usługi równoważenia obciążenia hello w hello portalu Azure

Moduł równoważenia obciążenia hello toocreate:

1. W hello portalu Azure Przejdź toohello grupy zasobów z maszynami wirtualnymi hello.

1. Kliknij przycisk **+ Dodaj**. Wyszukiwanie hello Marketplace dla **modułu równoważenia obciążenia**. Kliknij przycisk **modułu równoważenia obciążenia**.

1. Kliknij przycisk **Utwórz**.

1. Skonfiguruj hello modułu równoważenia obciążenia z:

   - **Nazwa**: nazwę identyfikującą hello modułu równoważenia obciążenia.
   - **Typ**: hello modułu równoważenia obciążenia mogą być publicznych lub prywatnych. Moduł równoważenia obciążenia prywatnej jest możliwy za pomocą hello tej samej sieci Wirtualnej. Najbardziej Azure aplikacje mogą używać modułu równoważenia obciążenia prywatnych. Jeśli aplikacja wymaga dostępu tooSQL serwera bezpośrednio przez hello Internet, użyj publiczny moduł równoważenia obciążenia.
   - **Sieć wirtualna**: hello sam sieci jako hello maszyn wirtualnych.
   - **Podsieci**: hello tej samej podsieci co hello maszyn wirtualnych.
   - **Prywatny adres IP**: hello przypisania zasobu sieciowego klastra programu SQL Server FCI toohello tego samego adresu IP.
   - **Subskrypcja**: Azure Twojej subskrypcji.
   - **Grupa zasobów**: Użyj hello sam grupie zasobów co maszyn wirtualnych.
   - **Lokalizacja**: Użyj hello sam lokalizacji platformy Azure jako maszyn wirtualnych.
   Zobacz hello poniższej ilustracji:

   ![CreateLoadBalancer](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-hello-load-balancer-backend-pool"></a>Konfigurowanie puli zaplecza modułu równoważenia obciążenia hello

1. Zwraca toohello grupy zasobów platformy Azure z maszynami wirtualnymi hello i Znajdź hello nowego modułu równoważenia obciążenia. Mogą mieć widok hello toorefresh na powitania grupy zasobów. Kliknij przycisk hello modułu równoważenia obciążenia.

1. W bloku modułu równoważenia obciążenia hello, kliknij **pul zaplecza**.

1. Kliknij przycisk **+ Dodaj** tooadd puli wewnętrznej bazy danych.

1. Wpisz nazwę hello puli wewnętrznej bazy danych.

1. Kliknij przycisk **Dodaj maszynę wirtualną**.

1. Na powitania **wybierz maszyny wirtualne** bloku, kliknij przycisk **wybierz zestaw dostępności**.

1. Wybieranie zestawu dostępności hello umieszczanie maszyn wirtualnych programu SQL Server hello w.

1. Na powitania **wybierz maszyny wirtualne** bloku, kliknij przycisk **wybierz maszyny wirtualne hello**.

   Portalem Azure powinna wyglądać hello poniższej ilustracji:

   ![CreateLoadBalancerBackEnd](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. Kliknij przycisk **wybierz** na powitania **wybierz maszyny wirtualne** bloku.

1. Kliknij przycisk **OK** dwa razy.

### <a name="configure-a-load-balancer-health-probe"></a>Skonfiguruj kondycji sondę modułu równoważenia obciążenia

1. W bloku modułu równoważenia obciążenia hello, kliknij **sondy kondycji**.

1. Kliknij przycisk **+ Dodaj**.

1. Na powitania **sondy kondycji Dodaj** bloku <a name="probe"> </a>Ustaw parametry sondy kondycji hello:

   - **Nazwa**: Nazwa sondy kondycji hello.
   - **Protokół**: TCP.
   - **Port**: Ustaw tooan dostępny port TCP. Ten port wymaga port zapory otwarte. Użyj hello [tego samego portu](#ports) ustawiony dla sondy kondycji hello na zaporze hello.
   - **Interwał**: 5 sekund.
   - **Próg złej kondycji**: 2 kolejnych błędów.

1. Kliknij przycisk OK.

### <a name="set-load-balancing-rules"></a>Ustaw reguły równoważenia obciążenia

1. W bloku modułu równoważenia obciążenia hello, kliknij **reguły równoważenia obciążenia**.

1. Kliknij przycisk **+ Dodaj**.

1. Ustaw parametry reguły równoważenia obciążenia hello:

   - **Nazwa**: nazwę reguły równoważenia obciążenia hello.
   - **Adres IP frontonu**: Użyj hello adresu IP dla hello zasobu sieciowego klastra programu SQL Server infrastruktury klasyfikacji plików.
   - **Port**: Ustaw dla hello port TCP programu SQL Server infrastruktury klasyfikacji plików. Witaj domyślnego wystąpienia portu to 1433.
   - **Port zaplecza**: Ta wartość używa hello sam portu jako hello **portu** wartość po włączeniu **pływającego adresu IP (bezpośredni zwrot serwera)**.
   - **Puli zaplecza**: Nazwa puli zaplecza hello Użyj, wcześniej skonfigurowany.
   - **Sondy kondycji**: badanie kondycji hello użycia, które skonfigurowane wcześniej.
   - **Trwałość sesji**: Brak.
   - **Czas bezczynności (w minutach)**: 4.
   - **Zmienny adres IP (bezpośredni zwrot serwera)**: włączone

1. Kliknij przycisk **OK**.

## <a name="step-6-configure-cluster-for-probe"></a>Krok 6: Konfigurowanie klastra dla sondy

Wartość parametru port sondy klastra hello w programie PowerShell.

tooset hello parametru port sondy klastra, zaktualizuj zmienne w hello następującego skryptu ze środowiska.

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "IP Address Resource Name" # hello IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a>Krok 7: Testowanie trybu failover z infrastruktury klasyfikacji plików

Testowanie pracy awaryjnej hello funkcje klastra toovalidate infrastruktury klasyfikacji plików. Witaj następujące kroki:

1. Połącz tooone węzłów klastra programu SQL Server FCI hello z protokołem RDP.

1. Otwórz **Menedżera klastra trybu Failover**. Kliknij przycisk **ról**. Powiadomienia, który węzeł jest właścicielem roli SQL Server FCI hello.

1. Kliknij prawym przyciskiem myszy hello roli SQL Server FCI.

1. Kliknij przycisk **Przenieś** i kliknij przycisk **najlepszego możliwego węzła**.

**Menedżer klastra trybu failover** pokazuje hello roli i jej zasobach przejścia do trybu offline. Witaj zasobów następnie przenieś i przejdzie w tryb online hello na inny węzeł.

### <a name="test-connectivity"></a>Testowanie łączności

połączenie tootest, logowanie tooanother maszyny wirtualnej w hello tej samej sieci wirtualnej. Otwórz **programu SQL Server Management Studio** i połącz toohello Nazwa SQL Server FCI.

>[!NOTE]
>Jeśli to konieczne, możesz [pobierania programu SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).

## <a name="limitations"></a>Ograniczenia
Na maszynach wirtualnych Azure Microsoft Distributed Transaction Coordinator (DTC) nie jest obsługiwana na wystąpienia ponieważ hello portu RPC nie jest obsługiwana przez hello równoważenia obciążenia.

## <a name="see-also"></a>Zobacz też

[Instalacja S2D przy użyciu pulpitu zdalnego (Azure)](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

[Zbieżność Hyper rozwiązania z bezpośrednie miejsca do magazynowania](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).

[Omówienie bezpośrednie miejsca magazynu](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[Obsługa programu SQL Server dla S2D](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)
