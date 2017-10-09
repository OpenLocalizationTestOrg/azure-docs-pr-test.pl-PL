---
title: "aaaSet hello źródła i celu tooAzure replikacji funkcji Hyper-V (za pomocą programu System Center VMM) z usługą Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Podsumowanie tooset kroki hello źródłowa i docelowa ustawień replikacji maszyn wirtualnych funkcji Hyper-V w magazynie tooAzure chmur programu VMM z usługą Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5edb6d87-25a5-40fe-b6f1-ddf7b55a6b31
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/25/2017
ms.author: raynew
ms.openlocfilehash: 3f8c5386cb64527c775aef636980bac098ee9905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-with-vmm-replication-tooazure"></a>Krok 8: Konfigurowanie hello źródłowa i docelowa dla tooAzure replikacji funkcji Hyper-V (w programie VMM)

Po [utworzenie magazynu](vmm-to-azure-walkthrough-create-vault.md) i określenie, które mają tooreplicate, użyj tego artykułu tooconfigure źródła i docelowych ustawień podczas replikowania maszyn wirtualnych funkcji Hyper-V lokalnymi w System Center Virtual Machine Manager (VMM) tooAzure chmury, za pomocą hello [usługi Azure Site Recovery](site-recovery-overview.md) w hello portalu Azure.

Opublikuj komentarze i pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Konfigurowanie środowiska źródłowego hello

S1. Kliknij pozycję **Przygotowanie infrastruktury** > **Źródło**.

    ![Set up source](./media/vmm-to-azure-walkthrough-source-target/set-source1.png)

2. W **Przygotuj źródło**, kliknij przycisk **+ VMM** tooadd serwera programu VMM.

    ![Konfiguracja źródła](./media/vmm-to-azure-walkthrough-source-target/set-source2.png)

3. W **Dodaj serwer**, sprawdź, czy **serwera programu System Center VMM** pojawia się w **typ serwera** , że serwer VMM hello spełnia hello [warunki wstępne i adres URL wymagania dotyczące](#prerequisites).
4. Pobierz plik instalacyjny dostawcy usługi Azure Site Recovery hello.
5. Pobierz klucz rejestracji hello. Będzie on potrzebny po uruchomieniu Instalatora. klucz Hello jest ważny przez pięć dni po jego wygenerowaniu.

    ![Konfiguracja źródła](./media/vmm-to-azure-walkthrough-source-target/set-source3.png)

## <a name="install-hello-provider-on-hello-vmm-server"></a>Zainstaluj na serwerze VMM hello hello dostawcy

1. Uruchom plik Instalatora dostawcy hello na powitania serwera VMM.
2. W usłudze **Microsoft Update** można włączyć aktualizacje, aby aktualizacje dostawcy były instalowane zgodnie z zasadami Microsoft Update.
3. W **instalacji**, Zaakceptuj lub zmodyfikuj hello domyślną lokalizację instalacji dostawcy i kliknij przycisk **zainstalować**.

    ![Lokalizacja instalacji](./media/vmm-to-azure-walkthrough-source-target/provider2.png)
4. Po zakończeniu instalacji kliknij przycisk **zarejestrować** tooregister hello menedżerem maszyny wirtualnej w magazynie hello.
5. W hello **ustawienia magazynu** kliknij przycisk **Przeglądaj** plik klucza tooselect hello magazynu. Określ subskrypcję usługi Azure Site Recovery hello i hello nazwę magazynu.

    ![Rejestracja serwera](./media/vmm-to-azure-walkthrough-source-target/provider10.png)
6. W **połączenia internetowego**, określ, jak dostawca uruchomiony na serwerze VMM hello łączą tooSite odzyskiwania przez hello hello internet.

   * Tooconnect dostawcy hello bezpośrednio, wybierz opcję **łączą się bezpośrednio tooAzure odzyskiwania lokacji bez serwera proxy**.
   * Jeśli istniejący serwer proxy wymaga uwierzytelniania lub chcesz toouse niestandardowego serwera proxy, zaznacz **połączyć tooAzure Przywracanie lokacji z użyciem serwera proxy**.
   * Jeśli używasz niestandardowego serwera proxy, określ adres hello, port oraz poświadczenia.
   * Jeśli używasz serwera proxy, możesz już zezwolono hello adresów URL opisanych w [wymagania wstępne](#on-premises-prerequisites).
   * Jeśli używasz niestandardowego serwera proxy konto Uruchom jako programu VMM (DRAProxyAccount) zostanie utworzony automatycznie za pomocą hello określone poświadczenia serwera proxy. Konfiguracja serwera proxy hello, dzięki czemu to konto mogło być pomyślnie uwierzytelnione. Ustawienia konta Uruchom jako programu VMM Hello można modyfikować w konsoli programu VMM hello. W **ustawienia**, rozwiń węzeł **zabezpieczeń** > **konta Uruchom jako**, a następnie zmodyfikuj hello hasło dla konta DRAProxyAccount. Usługa VMM hello toorestart należy tak, aby to ustawienie zostało zastosowane.

     ![Internet](./media/vmm-to-azure-walkthrough-source-target/provider13.png)
7. Zaakceptuj lub zmodyfikuj lokalizację hello certyfikat SSL, który jest automatycznie generowany do szyfrowania danych. Ten certyfikat jest używany, jeśli włączysz szyfrowanie danych dla chmury chronionej przez platformę Azure w portalu usługi Azure Site Recovery hello. Przechowuj ten certyfikat w bezpiecznym miejscu. Po uruchomieniu tooAzure trybu failover należy ją toodecrypt, jeśli jest włączone szyfrowanie danych.
8. W **nazwy serwera**, określ serwer VMM hello tooidentify przyjazną nazwę w magazynie hello. W konfiguracji klastra Określ nazwę roli klastra VMM hello.
9. Włącz **synchronizację metadanych chmury**, jeśli chcesz toosynchronize metadane dla wszystkich chmur na powitania serwera VMM w magazynie hello. Ta akcja wymaga tylko toohappen raz na każdym serwerze. Jeśli nie chcesz toosynchronize wszystkich chmur, można zaznaczać tego ustawienia i synchronizować poszczególne chmury indywidualnie WE hello właściwości chmury w konsoli programu VMM hello. Kliknij przycisk **zarejestrować** toocomplete hello procesu.

    ![Rejestracja serwera](./media/vmm-to-azure-walkthrough-source-target/provider16.png)
10. Rozpoczyna się rejestracja. Po zakończeniu rejestracji serwer hello jest wyświetlany w **infrastruktura usługi Site Recovery** > **serwery VMM**.


## <a name="install-hello-azure-recovery-services-agent-on-hyper-v-hosts"></a>Zainstaluj agenta usług odzyskiwania Azure hello na hostach funkcji Hyper-V

1. Po skonfigurowaniu hello dostawcy należy plik instalacyjny hello toodownload hello agenta usług odzyskiwania Azure. Uruchom Instalatora na każdym serwerze funkcji Hyper-V w chmurze VMM hello.

    ![Lokacje funkcji Hyper-V](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent1.png)
2. W obszarze **Sprawdzanie wymagań wstępnych** kliknij przycisk **Dalej**. Wszystkie brakujące wymagania wstępne zostaną zainstalowane automatycznie.

    ![Wymagania wstępne dotyczące agenta Usług odzyskiwania](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent2.png)
3. W **ustawienia instalacji**Zaakceptuj lub zmodyfikuj lokalizację instalacji hello i hello lokalizacji pamięci podręcznej. Witaj w pamięci podręcznej można skonfigurować na dysku, który ma co najmniej 5 GB miejsca do magazynowania, ale zalecamy dysk pamięci podręcznej z najmniej 600 GB wolnego miejsca. Następnie kliknij pozycję **Zainstaluj**.
4. Po zakończeniu instalacji kliknij przycisk **Zamknij** toofinish.

    ![Rejestracja agenta MARS](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent3.png)

### <a name="command-line-installation"></a>Instalacja przy użyciu wiersza polecenia
Hello agenta usług odzyskiwania Microsoft Azure można zainstalować z wiersza polecenia przy użyciu hello następujące polecenie:

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-toosite-recovery-from-hyper-v-hosts"></a>Konfigurowanie internetowego serwera proxy dostępu tooSite odzyskiwania z hostów funkcji Hyper-V

agenta usług odzyskiwania Hello na hostach funkcji Hyper-V musi mieć tooAzure dostęp do Internetu w przypadku replikacji maszyny Wirtualnej. Jeśli uzyskujesz dostęp do Internetu hello za pośrednictwem serwera proxy, skonfiguruj go w następujący sposób:

1. Otwórz hello Microsoft Azure Backup przystawka programu MMC na hoście funkcji Hyper-V hello. Domyślnie skrót do usługi Kopia zapasowa Microsoft Azure jest dostępny na pulpicie hello, lub C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. W przystawce hello, kliknij przycisk **Zmień właściwości**.
3. Na powitania **konfiguracji serwera Proxy** karcie, określ informacje dotyczące serwera proxy.

    ![Rejestracja agenta MARS](./media/vmm-to-azure-walkthrough-source-target/mars-proxy.png)
4. Sprawdź ten hello agent może osiągnąć adresy URL hello opisanego w hello [wymagania wstępne](#on-premises-prerequisites).

## <a name="set-up-hello-target-environment"></a>Konfigurowanie środowiska docelowego hello
Określ toobe konta magazynu Azure hello używanych w przypadku replikacji, a hello toowhich sieć platformy Azure, maszyny wirtualne Azure będą się łączyć po pracy awaryjnej.

1. Kliknij przycisk **przygotowanie infrastruktury** > **docelowego**, wybierz subskrypcję hello i hello grupy zasobów, w którym ma hello toocreate przejścia w tryb failover maszyny wirtualnej. Wybierz model wdrożenia hello, która ma toouse na platformie Azure (Zarządzanie zasobu lub classic) hello przejścia w tryb failover maszyny wirtualnej.

    ![Magazyn](./media/vmm-to-azure-walkthrough-source-target/enablerep3.png)

2. Usługa Site Recovery sprawdza, czy masz co najmniej jedno zgodne konto magazynu Azure i co najmniej jedną sieć platformy Azure.

    ![Magazyn](./media/vmm-to-azure-walkthrough-source-target/compatible-storage.png)

3. Jeśli nie utworzono konto magazynu, i chcesz toocreate jeden przy użyciu usługi Resource Manager, kliknij przycisk **+ konto magazynu** toodo tym miejscu.  Na powitania **utworzyć konto magazynu** bloku Określ nazwę konta, typ subskrypcji i lokalizacji. Witaj, konto musi należeć do hello tej samej lokalizacji co hello magazyn usług odzyskiwania.

   ![Magazyn](./media/vmm-to-azure-walkthrough-source-target/gs-createstorage.png)


   * Jeśli toocreate konto magazynu przy użyciu modelu klasycznego hello, należy to zrobić w hello portalu Azure. [Dowiedz się więcej](../storage/common/storage-create-storage-account.md)
   * Jeśli używasz konta magazynu w warstwie premium dla replikowanych danych, skonfiguruj dodatkowe konto magazynu, toostore dzienników replikacji, które przechwytują zachodzące zmiany lokalne tooon danych.
5. Jeśli nie utworzono sieci platformy Azure, i chcesz toocreate jeden przy użyciu usługi Resource Manager, kliknij przycisk **+ sieć** toodo tym miejscu. Na powitania **Utwórz sieć wirtualną** bloku określić nazwę sieciową, zakres adresów, szczegóły podsieci, subskrypcji i lokalizacji. Witaj sieć powinna znajdować się w hello tej samej lokalizacji co hello magazyn usług odzyskiwania.

   ![Sieć](./media/vmm-to-azure-walkthrough-source-target/gs-createnetwork.png)

   Jeśli toocreate sieci przy użyciu modelu klasycznego hello, należy to zrobić w hello portalu Azure. [Dowiedz się więcej](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).





## <a name="next-steps"></a>Następne kroki

Przejdź do zbyt[krok 9: Konfigurowanie mapowania sieci](vmm-to-azure-walkthrough-network-mapping.md)
