---
title: "tooAzure aaaMigrating magazyn w warstwie Premium za pomocą usługi Azure Site Recovery (niezarządzany dysków) | Dokumentacja firmy Microsoft"
description: "Migrowanie istniejących tooAzure maszyn wirtualnych przy użyciu usługi Site Recovery (niezarządzany dysków) Magazyn w warstwie Premium."
services: storage
documentationcenter: 
author: luywang
manager: kavithag
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: luywang
ms.openlocfilehash: 2c82fffaa38baeeb4a676748125bd85d6e0500f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-toopremium-storage-using-azure-site-recovery-unmanaged-disks"></a>Migrowanie tooPremium magazynu przy użyciu usługi Azure Site Recovery (niezarządzany dysków)

[Usługa Azure Premium Storage](storage-premium-storage.md) zapewnia obsługę wysokiej wydajności i małych opóźnień dysków dla maszyny wirtualnej (VM), które są uruchomione/O wykonujących obciążeń. przeznaczenie tego przewodnika Hello jest użytkowników toohelp migracji ich dyski maszyny Wirtualnej z tooa konta magazynu standardowego konta magazynu Premium za pomocą [usługi Azure Site Recovery](../../site-recovery/site-recovery-overview.md).

Usługa Site Recovery jest usługą platformy Azure, która wspiera tooyour ciągłość i strategii odzyskiwania po awarii poprzez organizowanie hello replikacji lokalnych serwerów fizycznych i maszyn wirtualnych toohello chmury (Azure) lub tooa dodatkowego centrum danych. W przypadku wystąpienia awarii w lokalizacji głównej, należy przełączyć toohello dodatkowej lokalizacji tookeep aplikacje i obciążenia, które są dostępne. Lokalizacją główną tooyour Wstecz nie zostanie zwrócona toonormal operacji. Usługa Site Recovery zapewnia testowy tryb failover testowanie odzyskiwania po awarii toosupport bez wpływu na środowiska produkcyjne. Można uruchomić tryb failover minimalna utrata danych (w zależności od częstotliwości replikacji) dla nieoczekiwanych awarii. W scenariuszu hello z migracji tooPremium magazynu, można użyć hello [pracy awaryjnej w usłudze Site Recovery](../../site-recovery/site-recovery-failover.md) w usłudze Azure Site Recovery toomigrate docelowych dysków tooa konta magazynu w warstwie Premium.

Zaleca się migrowanie tooPremium magazynu przy użyciu usługi Site Recovery, ponieważ ta opcja zapewnia minimalnym czasem przestojów i pozwala uniknąć hello wykonywania ręczne kopiowanie dysków i tworzenie nowych maszyn wirtualnych. Usługa Site Recovery systematycznie skopiuje dysków i tworzenie nowych maszyn wirtualnych w trybie failover. Usługa Site Recovery obsługuje kilka typów trybu failover z minimalnym lub bez przestojów. tooplan z czasem przestoju oraz szacowania utraty danych, zobacz hello [typach trybu failover](../../site-recovery/site-recovery-failover.md) tabeli w usłudze Site Recovery. Jeśli użytkownik [przygotowanie tooconnect tooAzure maszyn wirtualnych po pracy awaryjnej](../../site-recovery/vmware-walkthrough-overview.md), powinno być możliwe tooconnect toohello maszyny Wirtualnej platformy Azure za pomocą protokołu RDP po pracy awaryjnej.

![][1]

## <a name="azure-site-recovery-components"></a>Składniki usługi Azure Site Recovery

Są to składniki usługi Site Recovery hello, które są odpowiednie toothis scenariusza migracji.

* **Serwer konfiguracji** jest maszyny Wirtualnej platformy Azure, koordynowania komunikacji, który zarządza procesami replikacji i odzyskiwania danych. Na tej maszynie Wirtualnej należy uruchomić serwer konfiguracji pojedynczego pliku tooinstall hello konfiguracji oraz dodatkowych składników, nazywany serwerem procesu, jako brama replikacji. Przeczytaj informacje o [wymagania wstępne dotyczące konfiguracji serwera](../../site-recovery/vmware-walkthrough-overview.md). Serwer konfiguracji tylko musi toobe skonfigurowany raz i może służyć do wszystkich toohello migracji tego samego regionu.

* **Serwer przetwarzania** jest brama replikacji, który odbiera dane replikacji z źródłowe maszyny wirtualne optymalizuje hello danych z pamięci podręcznej, kompresji i szyfrowania i wysyła je tooa konta magazynu. Również obsługę instalacji wypychanej programu toosource usługi mobilności hello maszyn wirtualnych i przeprowadza automatyczne odnajdywanie źródłowe maszyny wirtualne. serwer przetwarzania domyślne Hello jest zainstalowany na powitania serwera konfiguracji. Można wdrożyć dodatkowe autonomiczne procesu serwerów tooscale wdrożenia. Przeczytaj informacje o [najlepszych rozwiązań dotyczących wdrażania serwera procesu](https://azure.microsoft.com/blog/best-practices-for-process-server-deployment-when-protecting-vmware-and-physical-workloads-with-azure-site-recovery/) i [wdrażanie serwerów dodatkowych procesów](../../site-recovery/site-recovery-plan-capacity-vmware.md#deploy-additional-process-servers). Serwer przetwarzania tylko musi toobe skonfigurowany raz i może służyć do wszystkich toohello migracji tego samego regionu.

* **Usługa mobilności** jest składnikiem, który jest wdrożony na każdy standardowa maszyna wirtualna ma tooreplicate. Zarejestrowaniu zapisów danych na hello standardowe maszyny Wirtualnej i przekazuje je toohello serwera przetwarzania. Przeczytaj informacje o [replikowane wymagania wstępne dotyczące maszyny](../../site-recovery/vmware-walkthrough-overview.md).

Ten rysunek przedstawia interakcje między tymi składnikami.

![][15]

> [!NOTE]
> Usługa Site Recovery nie obsługuje migracji hello dysków miejsca do magazynowania.

Dodatkowe składniki w innych sytuacjach można znaleźć w artykule zbyt[architektura scenariusza](../../site-recovery/vmware-walkthrough-overview.md).

## <a name="azure-essentials"></a>Azure essentials

Są one hello Azure wymagań dotyczących tego scenariusza migracji.

* Subskrypcja platformy Azure
* Toostore konto magazynu Azure Premium zreplikowanych danych
* Sieć wirtualna platformy Azure (VNet) toowhich maszyn wirtualnych będzie Połącz, gdy są tworzone w trybie failover. Hello sieci wirtualnej platformy Azure musi znajdować się w tym samym regionie Witaj, zgodnie z jedną, w których hello działa usługa Site Recovery hello
* Azure standardowe konto magazynu, w których toostore dzienników replikacji. Może to być hello tego samego konta magazynu, zgodnie z hello maszyny Wirtualnej dyski migrowane

## <a name="prerequisites"></a>Wymagania wstępne

* Zrozumienie składniki scenariusza migracji odpowiednich hello w powyższej sekcji hello
* Zaplanowaniu czasu na przestoje przez learning o hello [pracy awaryjnej w usłudze Site Recovery](../../site-recovery/site-recovery-failover.md)

## <a name="setup-and-migration-steps"></a>Kroki instalacji i migracji

Możesz użyć usługi Site Recovery toomigrate maszyn wirtualnych IaaS platformy Azure między regionami lub w tym samym regionie. Witaj następujące instrukcje są ściśle dostosowane w tym scenariuszu migracji z artykułu hello [replikowanie maszyn wirtualnych VMware lub serwerów fizycznych tooAzure](../../site-recovery/vmware-walkthrough-overview.md). Wykonaj hello łącza, aby uzyskać szczegółowe instrukcje w toohello dodatkowe instrukcje w tym artykule.

1. **Tworzenie magazynu usług odzyskiwania**. Tworzenie i zarządzanie nimi hello magazynu usługi Site Recovery za pośrednictwem hello [portalu Azure](https://portal.azure.com). Kliknij przycisk **nowe** > **zarządzania** > **kopii zapasowej** i **lokacji odzyskiwania (OMS)**. Alternatywnie możesz kliknąć **Przeglądaj** > **magazyn usług odzyskiwania** > **Dodaj**. Maszyny wirtualne będą replikowane toohello regionu, podane w tym kroku. Witaj w celu migracji w hello tego samego regionu, regionu wybierz hello skutkującej źródła maszyn wirtualnych i kont magazynu źródłowego. 

2. Witaj Poniższe etapy ułatwiają **wybranie celów ochrony**.

    2a. Na powitania maszyny Wirtualnej, w którym ma tooinstall hello konfiguracji serwera, otwórz hello [portalu Azure](https://portal.azure.com). Przejdź za**Magazyny usług odzyskiwania** > **ustawienia**. W obszarze **ustawienia**, wybierz pozycję **usługi Site Recovery**. W obszarze **usługi Site Recovery**, wybierz pozycję **krok 1: Przygotowanie infrastruktury**. W obszarze **przygotowanie infrastruktury**, wybierz pozycję **cel ochrony**.

    ![][2]

    2b. W obszarze **cel ochrony**, w pierwszej listy rozwijanej Witaj, wybierz **tooAzure**. Hello drugiej listy rozwijanej, wybierz **nie zwirtualizowanych / inne**, a następnie kliknij przycisk **OK**.

    ![][3]

3. Witaj Poniższe etapy ułatwiają **Konfigurowanie środowiska źródłowego hello (serwer konfiguracji)**.

    3a. Pobierz hello **Unified instalacja usługi Azure Site Recovery** i hello **klucza rejestracji magazynu** przez przejście toohello **przygotowanie infrastruktury**  >  **Przygotuj źródło** > **Dodaj serwer** bloku. Konieczne będzie hello Konfiguracja hello unified toorun klucza rejestracji magazynu. klucz Hello jest ważny przez 5 dni po jego wygenerowaniu.

    ![][4]

    3b. Dodaj serwer konfiguracji w hello **Dodaj serwer** bloku.

    ![][5]

    3c. Na powitania używasz jako powitania serwera konfiguracji maszyny Wirtualnej uruchom Instalatora Unified tooinstall hello konfiguracji serwera i serwera przetwarzania hello. Można przeprowadzić za pomocą zrzuty ekranu hello [tutaj](../../site-recovery/vmware-walkthrough-overview.md) toocomplete hello instalacji. Może się odwoływać toohello po zrzuty ekranu dla kroki określone w tym scenariuszu migracji.

    W **przed rozpoczęciem**, wybierz pozycję **zainstalować hello konfiguracji serwera i serwera przetwarzania**.

    ![][6]

    3W. W **rejestracji**, wyszukaj i wybierz hello klucza rejestracji pobranego z hello magazynu.

    ![][7]

    3E. W **szczegóły środowiska**wybierz, czy chcesz zacząć tooreplicate maszyn wirtualnych VMware. W tym scenariuszu migracji, wybierz **nr**.

    ![][8]

    3F. Po zakończeniu instalacji hello zobaczysz hello **serwera konfiguracji odzyskiwania Microsoft Azure lokacji** okna. Użyj hello **Zarządzanie kontami** karcie toocreate hello konta usługi Site Recovery można użyć automatycznego wykrywania. (W scenariuszu hello o ochronie komputerów fizycznych, skonfigurowanie konta hello nie jest istotne, ale należy co najmniej jednego konta tooenable jedną z hello następujące kroki. W takim przypadku można określić nazwę hello konta i hasła wszystkich.) Użyj hello **rejestracji magazynu** plik poświadczeń magazynu hello tooupload kartę.

    ![][9]

4. **Konfigurowanie środowiska docelowego hello**. Kliknij przycisk **przygotowanie infrastruktury** > **docelowego**i określ model wdrożenia hello ma toouse dla maszyn wirtualnych po pracy awaryjnej. Możesz wybrać **klasycznego** lub **Resource Manager**, w zależności od danego scenariusza.

    ![][10]

    Usługa Site Recovery sprawdza, czy masz co najmniej jedno zgodne konto magazynu Azure i co najmniej jedną sieć platformy Azure. Należy pamiętać, że jeśli używasz konta magazynu w warstwie Premium dla replikowanych danych, należy tooset replikacji toostore konta magazynu w warstwie standardowa dodatkowe dzienniki.

5. **Konfigurowanie ustawień replikacji**. Wykonaj [Konfigurowanie ustawień replikacji](../../site-recovery/vmware-walkthrough-overview.md) tooverify, który serwer konfiguracji jest pomyślnie skojarzone z zasadami replikacji hello tworzenia.

6. **Planowanie pojemności**. Użyj hello [planowania pojemności](../../site-recovery/site-recovery-capacity-planner.md) tooaccurately szacowania przepustowości, magazynu i inne wymagania toomeet musi z replikacji. Gdy wszystko będzie gotowe, wybierz **tak** w **czy ukończono Planowanie wydajności?**.

    ![][11]

7. Witaj Poniższe etapy ułatwiają **zainstalować usługi mobilności i włączyć replikację**.

    7a. Możesz wybrać zbyt[instalacji wypychanej](../../site-recovery/vmware-walkthrough-overview.md) tooyour źródłowe maszyny wirtualne lub zbyt[ręcznie zainstalować usługi mobilności](../../site-recovery/site-recovery-vmware-to-azure-install-mob-svc.md) na źródłowe maszyny wirtualne. Wymaganie hello położenia instalacji i ścieżkę hello hello ręczne Instalatora można znaleźć w hello łączem. Jeśli przeprowadzasz instalację ręcznie, może być konieczne toouse wewnętrznego serwera adresami IP toofind hello konfiguracji.

    ![][12]

    Witaj przełączona w tryb failover maszyny Wirtualnej będzie mieć dwa dyski tymczasowego: hello z podstawowej maszyny Wirtualnej i hello inne utworzone podczas inicjowania obsługi administracyjnej maszyny Wirtualnej w regionie odzyskiwania hello hello. tooexclude dysku tymczasowym hello przed replikacji, zainstalować usługi mobilności hello przed włączeniem replikacji. toolearn więcej informacji na temat sposobu tooexclude hello tymczasowego dysku, można znaleźć zbyt[wykluczyć z replikacji dyski](../../site-recovery/vmware-walkthrough-overview.md).

    7b. Teraz włącz replikację w następujący sposób:
      * Kliknij przycisk **Replikowanie aplikacji** > **źródła**. Po włączeniu replikacji dla powitania po raz pierwszy, kliknij pozycję + replikacji w hello magazynu tooenable replikację dla dodatkowych maszyn.
      * W kroku 1 — Konfiguracja źródła jako serwera przetwarzania.
      * W kroku 2 Określ model wdrożenia trybu failover post hello, toomigrate konta magazynu Premium, aby, dzienniki toosave konta Standard storage i toofail sieci wirtualnej, aby.
      * W kroku 3, Dodaj chronionych maszyn wirtualnych za pomocą adresu IP (wewnętrzny toofind adresu IP może być konieczne ich).
      * W kroku 4 należy skonfigurować właściwości hello wybierając hello kont, których należy wcześniej skonfigurować na powitania serwera przetwarzania.
      * W kroku 5 wybierz zasady replikacji hello utworzonego wcześniej, konfigurowanie ustawień replikacji.
      Kliknij przycisk **OK** i włączyć replikację.

    > [!NOTE]
    > Po cofnięciu przydziału maszyny Wirtualnej platformy Azure i ponownego uruchomienia, nie ma żadnej gwarancji, która pobierze hello tego samego adresu IP. Adres IP hello hello konfiguracji serwera/procesu serwera lub hello chroniony zmiany maszyn wirtualnych platformy Azure, replikacji hello w tym scenariuszu może nie działać poprawnie.

    ![][13]

    Podczas projektowania środowiska usługi Azure Storage, zalecane jest użycie kont magazynu osobne dla każdej maszyny Wirtualnej w zestawie dostępności. Firma Microsoft zaleca, wykonaj hello najlepszym rozwiązaniem w warstwie magazynu hello zbyt[użycia wielu kont magazynu dla każdego zestawu dostępności](../../virtual-machines/windows/manage-availability.md). Dystrybucja kont magazynu toomultiple dysków maszyny Wirtualnej pomaga dostępność magazynu tooimprove i dystrybuuje hello we/wy na powitania infrastruktury magazynu Azure. W przypadku maszyn wirtualnych w zestawie dostępności, zamiast replikować dysków wszystkich maszyn wirtualnych na jedno konto magazynu, zaleca się migracja wielu maszyn wirtualnych wielokrotnie, dzięki czemu maszyny wirtualne hello w hello sam zestaw dostępności nie mają konta jednego magazynu. Użyj hello **włączania replikacji** tooset bloku konto magazynu docelowego dla każdej maszyny Wirtualnej, jeden z nich. Można wybrać według potrzeby tooyour model wdrożenia trybu failover post. Jeśli wybierzesz Menedżera zasobów (RM) jako model wdrożenia trybu failover post, możesz w trybie Failover tooan RM maszyny Wirtualnej RM VM lub może zakończyć się niepowodzeniem w klasycznym tooan maszyny Wirtualnej VM Menedżera zasobów.

8. **Uruchom test trybu failover**. toocheck czy z replikacji zostanie zakończone, kliknij przycisk odzyskiwania lokacji, a następnie kliknij przycisk **ustawienia** > **elementy replikowane**. Pojawi się stan hello i procent procesu replikacji. Po początkowej replikacji jest toovalidate testowy tryb Failover zakończy pracę, uruchom strategii replikacji. Szczegółowy opis kroków testu pracy w trybie Failover, można znaleźć w artykule zbyt[uruchomić test trybu failover w usłudze Site Recovery](../../site-recovery/vmware-walkthrough-overview.md). Można wyświetlić stan hello testowy tryb failover w **ustawienia** > **zadania** > **YOUR_FAILOVER_PLAN_NAME**. W bloku hello zobaczysz podział hello kroków i wyniki powodzeń/niepowodzeń. W przypadku niepowodzenia hello testowy tryb failover na dowolnym etapie kliknij komunikat o błędzie hello krok toocheck hello. Upewnij się, że maszyn wirtualnych i strategii replikacji wymagań hello przed uruchomieniem trybu failover. Odczyt [tooAzure testowego trybu Failover w usłudze Site Recovery](../../site-recovery/site-recovery-test-failover-to-azure.md) uzyskać więcej informacji oraz instrukcje testowy tryb failover.

9. **Tryb failover**. Po zakończeniu hello testowy tryb failover Uruchom toomigrate trybu failover z tooPremium dyski magazynu i replikować hello wystąpień maszyn wirtualnych. Wykonaj hello szczegółowe kroki [tryb failover](../../site-recovery/site-recovery-failover.md#run-a-failover). Upewnij się, że wybrano **Zamknij maszyny wirtualne i zsynchronizuj najnowsze dane hello** toospecify czy Site Recovery należy spróbuj tooshut dół hello chronione maszyny wirtualne i zsynchronizować dane hello, dzięki czemu hello najnowszej wersji hello danych będzie można przełączyć. Jeśli nie zaznaczysz tej opcji lub nie powiodła się próba hello jest hello pracy awaryjnej od hello najnowszym dostępnym punktem odzyskiwania dla hello maszyny Wirtualnej. Usługa Site Recovery tworzy wystąpienia maszyny Wirtualnej, którego typ jest hello identyczny lub podobne tooa mogących magazynu maszyny Wirtualnej — wersja Premium. Możesz sprawdzić wydajność hello i cen różnych wystąpień maszyny Wirtualnej, przechodząc zbyt[cennik maszyn wirtualnych systemu Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) lub [cennik maszyn wirtualnych systemu Linux](https://azure.microsoft.com/pricing/details/virtual-machines/linux/).

## <a name="post-migration-steps"></a>Czynności wykonywane po migracji

1. **Skonfigurować zestaw stosownych dostępności toohello maszyn wirtualnych replikowanych**. Usługa Site Recovery nie obsługuje migracji maszyn wirtualnych wraz z zestawem dostępności hello. W zależności od wdrożenia hello zreplikowanej maszyny Wirtualnej wykonaj jedną z następujących hello:
  * Dla maszyny Wirtualnej utworzonej przy użyciu modelu klasycznego wdrażania hello: Dodaj hello wirtualna toohello zestawem dostępności w hello portalu Azure. Aby uzyskać szczegółowy opis kroków, przejdź zbyt[Dodawanie istniejącego zestawu dostępności maszyny wirtualnej tooan](../../virtual-machines/windows/classic/configure-availability.md#addmachine).
  * Dla modelu wdrażania usługi Resource Manager hello: Zapisz konfigurację hello maszyny Wirtualnej, a następnie usunięcie i ponowne utworzenie maszyn wirtualnych hello w zestawie dostępności hello. toodo tak, użyj skryptu hello na [ustawić Azure Resource Manager maszyny Wirtualnej zestawu dostępności](https://gallery.technet.microsoft.com/Set-Azure-Resource-Manager-f7509ec4). Sprawdź ograniczenia hello tego skryptu i zaplanować przestój przed uruchomieniem skryptu hello.

2. **Usuń stare maszyn wirtualnych i dysków**. Przed usunięciem te, upewnij się, czy dyski Premium hello są zgodne z dysków źródłowych i hello nowych maszyn wirtualnych wykonać hello same pełnią funkcję hello źródłowe maszyny wirtualne. W modelu wdrażania Menedżera zasobów (RM) hello Usuń hello maszyny Wirtualnej, a następnie usuń dyski hello z kont magazynu źródła w hello portalu Azure. W hello klasycznego modelu wdrażania można usunąć hello maszyny Wirtualnej i dysków w portalu klasycznym hello lub portalu Azure. Jeśli wystąpi problem, w których hello dysku nie zostanie usunięta, nawet jeśli usunięto hello maszyny Wirtualnej, zapoznaj się z artykułem [Rozwiązywanie problemów podczas usuwania wirtualne dyski twarde](storage-resource-manager-cannot-delete-storage-account-container-vhd.md).

3. **Wyczyść hello infrastruktury usługi Azure Site Recovery**. Jeśli usługa Site Recovery nie jest już potrzebne, można czyścić swoją infrastrukturę usuwania zreplikowanych elementów, powitania serwera konfiguracji i hello zasady odzyskiwania, a następnie usuwając hello magazyn Azure Site Recovery.

## <a name="troubleshooting"></a>Rozwiązywanie problemów

* [Monitorowanie i rozwiązywanie problemów z ochroną maszyn wirtualnych i serwerów fizycznych](../../site-recovery/site-recovery-monitoring-and-troubleshooting.md)
* [Forum usługi Microsoft Azure Site Recovery](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr)

## <a name="next-steps"></a>Następne kroki

Zobacz następujące zasoby w określonych scenariuszach migracji maszyn wirtualnych hello:

* [Migrowanie maszyn wirtualnych platformy Azure między kontami magazynu](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [Tworzenie i przekazywanie tooAzure wirtualnego dysku twardego z systemem Windows Server.](../../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Tworzenie i przekazywanie wirtualnego dysku twardego zawierający hello System operacyjny Linux](../../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Migrowanie maszyn wirtualnych z usług AWS Amazon tooMicrosoft Azure](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

Zobacz też hello następujące zasoby toolearn więcej informacji na temat usługi Azure Storage i maszyn wirtualnych platformy Azure:

* [Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Maszyny wirtualne platformy Azure](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Premium Storage: magazyn o wysokiej wydajności dla obciążeń maszyn wirtualnych platformy Azure](storage-premium-storage.md)

[1]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-1.png
[2]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-2.png
[3]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-3.png
[4]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-4.png
[5]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-5.png
[6]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-6.PNG
[7]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-7.PNG
[8]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-8.PNG
[9]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-9.PNG
[10]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-10.png
[11]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-11.PNG
[12]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-12.PNG
[13]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-13.png
[14]:../site-recovery/media/site-recovery-vmware-to-azure/v2a-architecture-henry.png
[15]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-14.png
