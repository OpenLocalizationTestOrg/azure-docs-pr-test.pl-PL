---
title: maszyny wirtualne funkcji Hyper-V aaaReplicate w tooAzure chmur programu VMM | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak tooreplicate maszyn wirtualnych funkcji Hyper-V na hostach funkcji Hyper-V znajduje się w tooAzure chmur programu System Center VMM."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 9d526a1f-0d8e-46ec-83eb-7ea762271db5
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: 136f68585534c17b615ecc4e82c0133bf813503f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure"></a>Replikowanie maszyn wirtualnych funkcji Hyper-V w tooAzure chmury VMM
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](site-recovery-vmm-to-azure.md)
> * [Program PowerShell — model usługi Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [Portal klasyczny](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell — model klasyczny](site-recovery-deploy-with-powershell.md)
>
>

Witaj usługi Azure Site Recovery przyczynia się tooyour ciągłość i strategia odzyskiwania (BCDR) poprzez organizowanie replikacji, trybu failover i odzyskiwania maszyn wirtualnych i serwerów fizycznych. Maszyny można replikowanych tooAzure lub tooa dodatkowej w lokalnym centrum danych. Aby zapoznać się z szybkim omówieniem, przeczytaj temat [Co to jest usługa Azure Site Recovery?](site-recovery-overview.md)

## <a name="overview"></a>Omówienie
W tym artykule opisano, jak maszyny wirtualne toodeploy usługi Site Recovery tooreplicate funkcji Hyper-V w ramach funkcji Hyper-V host serwerów, które znajdują się w tooAzure chmur prywatnych programu VMM.

Witaj artykuł zawiera wymagania wstępne dla scenariusza hello i wyświetlane Ci jak tooset się w magazynie usługi Site Recovery hello Azure dostawcy usługi Site Recovery zainstalowana na serwerze VMM źródła hello, Zarejestruj serwer hello w magazynie hello, Dodaj konto magazynu platformy Azure, zainstaluj hello Agent usług odzyskiwania Azure na serwerach hostów funkcji Hyper-V, skonfigurować ustawienia ochrony dla chmur programu VMM, które będzie zastosowane tooall chronionych maszyn wirtualnych, a następnie włącz ochronę tych maszyn wirtualnych. Aby zakończyć, testowania hello trybu failover toomake się, że wszystko działa zgodnie z oczekiwaniami.

Zamieść wszelkie komentarze lub pytania u dołu hello w tym artykule, albo na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="architecture"></a>Architektura
![Architektura](./media/site-recovery-vmm-to-azure-classic/topology.png)

* Witaj dostawcy usługi Azure Site Recovery jest instalowany na powitania VMM podczas wdrażania usługi Site Recovery i hello serwer VMM jest zarejestrowany w magazynie usługi Site Recovery hello. Witaj dostawca komunikuje się z aranżację toohandle usługi Site Recovery.
* agent usług odzyskiwania Azure Hello jest zainstalowany na serwerach hostów funkcji Hyper-V podczas wdrażania usługi Site Recovery. Obsługuje on magazynu tooAzure replikacji danych.

## <a name="azure-prerequisites"></a>Wymagania wstępne platformy Azure
Oto, czego będziesz potrzebować na platformie Azure.

| **Wymagania wstępne** | **Szczegóły** |
| --- | --- |
| **Konto platformy Azure** |Będziesz potrzebować konta platformy [Microsoft Azure](https://azure.microsoft.com/). Możesz rozpocząć od [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/). [Dowiedz się więcej](https://azure.microsoft.com/pricing/details/site-recovery/) o cenach usługi Site Recovery. |
| **Magazyn platformy Azure** |Będziesz potrzebować toostore replikowane dane konta magazynu platformy Azure. Replikowane dane są przechowywane w usłudze Azure Storage, a w przypadku przejścia w tryb failover uruchamiane są maszyny wirtualne platformy Azure. <br/><br/>Potrzebujesz [standardowego konta magazynu geograficznie nadmiarowego](../storage/common/storage-redundancy.md#geo-redundant-storage). Witaj, konto musi być w tym samym regionie co usługa Site Recovery hello hello i skojarzone z hello tej samej subskrypcji. Należy pamiętać, że konta magazynu toopremium replikacji nie jest obecnie obsługiwany i nie powinny być używane.<br/><br/>[Przeczytaj o](../storage/common/storage-introduction.md) usłudze Azure Storage. |
| **Sieć platformy Azure** |Będziesz potrzebować sieci wirtualnej platformy Azure, które maszyny wirtualne Azure będą się łączyć toowhen pracy awaryjnej. Witaj sieci wirtualnej platformy Azure musi być w hello tym samym regionie co magazyn usługi Site Recovery hello. |

## <a name="on-premises-prerequisites"></a>Lokalne wymagania wstępne
Oto, co należy zapewnić lokalnie.

| **Wymagania wstępne** | **Szczegóły** |
| --- | --- |
| **VMM** |Będziesz potrzebować co najmniej jednego serwera programu VMM wdrożonego jako fizyczny lub wirtualny serwer autonomiczny lub jako klaster wirtualny. <br/><br/>Serwer VMM Hello powinien być uruchamiany System Center 2012 R2 z hello najnowszymi aktualizacjami zbiorczymi.<br/><br/>Będziesz potrzebować co najmniej jednej chmury skonfigurowanej na serwerze VMM hello.<br/><br/>Chmura źródłowa Hello, które mają tooprotect musi zawierać co najmniej jedną grupę hostów programu VMM.<br/><br/>Aby dowiedzieć się więcej na temat konfigurowania chmur programu VMM, zobacz [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx) (Przewodnik: tworzenie chmur prywatnych przy użyciu programu System Center 2012 SP1 VMM) na blogu Keitha Mayera. |
| **Funkcja Hyper-V** |Będziesz potrzebować Serwery hosta funkcji Hyper-V lub klastry w hello chmury VMM. serwer hosta Hello powinien mieć i przynajmniej jednej maszyny wirtualnej. <br/><br/>Witaj funkcji Hyper-V server musi być uruchomiona w co najmniej **systemu Windows Server 2012 R2** z rolą funkcji Hyper-V hello lub **Microsoft Hyper-V Server 2012 R2** i mieć hello zainstalowane najnowsze aktualizacje.<br/><br/>Dowolnego serwera funkcji Hyper-V zawierające maszyny wirtualne mają tooprotect musi znajdować się w chmurze VMM.<br/><br/>Jeśli używasz funkcji Hyper-V w klastrze, broker klastra nie jest tworzony automatycznie, jeśli masz klaster oparty na statycznym adresie IP. Będziesz potrzebować brokera klastra hello tooconfigure ręcznie. Aby [dowiedzieć się więcej](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters), zobacz wpis na blogu Aidana Finna. |
| **Chronione maszyny** | Maszyny wirtualne mają tooprotect powinny być zgodne z [wymagania dotyczące usługi Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). |

## <a name="network-mapping-prerequisites"></a>Wymagania wstępne związane z mapowaniem sieci
Podczas ochrony maszyn wirtualnych w sieci Azure mapowania mapuje między sieciami maszyn wirtualnych na źródłowym serwerze programu VMM hello a docelowej sieci platformy Azure tooenable hello następujące:

* Wszystkie maszyny, które w tryb failover na powitania sam połączyć tooeach innych, niezależnie od tego, jakiego planu odzyskiwania, które znajdują się w sieci.
* Jeśli brama sieci jest skonfigurowana na powitania docelową sieć platformy Azure, maszyny wirtualne można łączyć z tooother lokalnych maszyn wirtualnych.
* Jeśli nie skonfigurujesz sieci mapowania tylko maszyny wirtualne, które awaryjnie w hello sam plan odzyskiwania będą mogli tooconnect tooeach innych po tooAzure pracy awaryjnej.

Jeśli chcesz, aby mapowanie sieci toodeploy potrzebne są następujące hello:

* maszyny wirtualne Hello ma tooprotect na źródłowym serwerze programu VMM hello powinna być tooa połączonych sieci maszyny Wirtualnej. Ta sieć powinna być tooa połączone sieci logicznej, która jest skojarzona z chmurą hello.
* Maszyny wirtualne replikowane toowhich sieć platformy Azure mogą łączyć po pracy awaryjnej. Należy wybrać tej sieci w czasie hello pracy awaryjnej. Witaj sieć powinna znajdować się w hello tym samym regionie co subskrypcja usługi Azure Site Recovery.


Przygotuj sieci w programie VMM:

   * [Skonfiguruj sieci logiczne](https://technet.microsoft.com/library/jj721568.aspx).
   * [Skonfiguruj sieci maszyn wirtualnych](https://technet.microsoft.com/library/jj721575.aspx).


## <a name="step-1-create-a-site-recovery-vault"></a>Krok 1. Tworzenie magazynu usługi Site Recovery
1. Zaloguj się toohello [portalu zarządzania](https://portal.azure.com) z serwera VMM hello ma tooregister.
2. Kliknij pozycje **Data Services** > **Usługi odzyskiwania** > **Magazyn usługi Site Recovery**.
3. Kliknij pozycje **Utwórz nowe** > **Szybkie tworzenie**.
4. W **nazwa**, wprowadź przyjazną nazwę tooidentify hello magazynu.
5. W **Region**, wybierz hello region geograficzny magazynu hello. toocheck obsługiwane regiony, zobacz dotyczącą dostępności geograficznej w [szczegóły cennika usługi Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Kliknij pozycję **Utwórz magazyn**.

    ![Nowy magazyn](./media/site-recovery-vmm-to-azure-classic/create-vault.png)

Sprawdź, czy hello tooconfirm paska stanu, który hello magazynu został pomyślnie utworzony. Witaj magazyn będzie wyświetlany jako **Active** na powitania głównej strony usług odzyskiwania.

## <a name="step-2-generate-a-vault-registration-key"></a>Krok 2. Generowanie klucza rejestracji magazynu
Wygeneruj klucz rejestracji w magazynie hello. Po pobraniu hello dostawcy usługi Azure Site Recovery i zainstaluj go na serwerze VMM hello, użyjesz tego serwera VMM hello tooregister kluczy w magazynie hello.

1. W hello **usług odzyskiwania** strony Szybki Start hello tooopen magazynu powitania kliknij pozycję. Szybki Start można również otworzyć w dowolnym momencie, korzystając z ikony hello.

    ![Ikona Szybki start](./media/site-recovery-vmm-to-azure-classic/qs-icon.png)
2. Z listy rozwijanej hello wybierz **między lokalną lokacją programu VMM i Microsoft Azure**.
3. W oknie **Przygotowanie serwerów programu VMM** kliknij plik **Wygeneruj klucz rejestracji**. Plik klucza Hello jest generowany automatycznie i jest ważny przez 5 dni po jego wygenerowaniu. Jeśli nie używasz hello portalu Azure z serwerem VMM hello należy toocopy tego serwera toohello plików.

    ![Klucz rejestracji](./media/site-recovery-vmm-to-azure-classic/register-key.png)

## <a name="step-3-install-hello-azure-site-recovery-provider"></a>Krok 3: Instalowanie hello dostawcy usługi Azure Site Recovery
1. W **Szybki Start** > **Przygotowanie serwerów programu VMM**, kliknij przycisk **Pobierz Microsoft dostawcy Azure Site Recovery do instalacji na serwerach VMM** tooobtain hello najnowszą wersję pliku instalacyjnego dostawcy hello.
2. Uruchom ten plik na źródłowym serwerze programu VMM hello.

   > [!NOTE]
   > Jeśli program VMM jest wdrożony w klastrze i instalujesz hello dostawcy dla powitania po raz pierwszy go zainstalować na aktywnym węźle i Zakończ hello instalacji tooregister hello serwer VMM w magazynie hello. Następnie zainstaluj hello dostawcy na powitania innych węzłów. Należy pamiętać, że Jeśli uaktualniasz hello dostawcy należy tooupgrade we wszystkich węzłach, ponieważ wszystkie powinny być uruchomione hello sama wersja dostawcy.
   >
   >
3. Witaj Instalator sprawdza wymagania wstępne i żąda uprawnienia toostop hello VMM toobegin Instalator programu service Provider. Witaj usługi programu VMM zostanie automatycznie uruchomiona po zakończeniu instalacji. Jeśli przeprowadzasz instalację na klastra VMM, który będzie wyświetlony monit o roli klastra hello toostop.
4. W usłudze **Microsoft Update** można włączyć aktualizacje. To ustawienie jest włączone aktualizacje dostawcy będą instalowane zgodnie z zasadami Microsoft Update tooyour.

    ![Usługa Microsoft Updates](./media/site-recovery-vmm-to-azure-classic/updates.png)
5. Lokalizacja instalacji dostawcy ustawiono zbyt hello Hello**<SystemDrive>\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin**. Kliknij pozycję **Zainstaluj**.

   ![InstallLocation](./media/site-recovery-vmm-to-azure-classic/install-location.png)
6. Po hello jest zainstalowany dostawca kliknij **zarejestrować** tooregister powitania serwera w magazynie hello.

    ![InstallComplete](./media/site-recovery-vmm-to-azure-classic/install-complete.png)
7. W **nazwę magazynu**, sprawdź nazwę hello hello magazynu, w którym hello serwer zostanie zarejestrowany. Kliknij przycisk *Dalej*.

    ![Rejestracja serwera](./media/site-recovery-vmm-to-azure-classic/vaultcred.PNG)
8. W **połączenia internetowego** Określ hello jak dostawca uruchomiony na powitania VMM łączy serwer toohello Internet. Wybierz **Połącz przy użyciu istniejących ustawień serwera proxy** toouse hello domyślnych ustawień połączenia internetowego skonfigurowane na powitania serwera.

    ![Ustawienia internetowe](./media/site-recovery-vmm-to-azure-classic/proxydetails.PNG)

   * Jeśli chcesz, aby toouse niestandardowego serwera proxy należy skonfigurować go przed zainstalowaniem hello dostawcy. Podczas konfigurowania niestandardowych ustawień serwera proxy wykonywany jest test w toocheck hello proxy połączenia.
   * Jeśli używasz niestandardowego serwera proxy lub domyślny serwer proxy wymaga uwierzytelniania należy tooenter hello proxy szczegółów, w tym hello adres i port proxy.
   * Następujące adresy URL powinien być dostępny hello serwer VMM i hosty funkcji Hyper-v hello
     * *.hypervrecoverymanager.windowsazure.com
     * *.accesscontrol.windows.net
     * *.backup.windowsazure.com
     * *.blob.core.windows.net
     * *.store.core.windows.net
   * Zezwalaj na adresy IP hello opisanego w [zakresów IP centrum danych Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) i protokół HTTPS (port 443). Trzeba toowhite listą zakresów IP hello region platformy Azure, możesz zaplanować toouse i zachodnie stany USA.
   * Jeśli używasz niestandardowego serwera proxy konto Uruchom jako programu VMM (DRAProxyAccount) zostanie utworzony automatycznie za pomocą hello określonych poświadczeń serwera proxy. Konfiguracja serwera proxy hello, dzięki czemu to konto mogło być pomyślnie uwierzytelnione. Ustawienia konta Uruchom jako programu VMM Hello można modyfikować w konsoli programu VMM hello. toodo, otwórz hello **ustawienia** obszaru roboczego, rozwiń węzeł **zabezpieczeń**, kliknij przycisk **konta Uruchom jako**, a następnie zmodyfikować hello hasło dla konta DRAProxyAccount. Usługa VMM hello toorestart należy tak, aby to ustawienie zostało zastosowane.
9. W **klucz rejestracji**, zaznacz klucz hello pobrany z usługi Azure Site Recovery, a następnie skopiować toohello serwera VMM.
10. ustawienie szyfrowania Hello jest używana tylko w przypadku replikacji maszyn wirtualnych funkcji Hyper-V w tooAzure chmur programu VMM. Jeśli replikujesz tooa lokacji dodatkowej nie jest używane.
11. W **nazwy serwera**, określ serwer VMM hello tooidentify przyjazną nazwę w magazynie hello. W konfiguracji klastra Określ nazwę roli klastra VMM hello.
12. W **Synchronizuj metadane chmury** wybierz, czy dla wszystkich chmur na powitania serwera VMM w magazynie hello toosynchronize metadanych. Ta akcja wymaga tylko toohappen raz na każdym serwerze. Jeśli nie chcesz toosynchronize wszystkich chmur, można zaznaczać tego ustawienia i synchronizować poszczególne chmury indywidualnie WE hello właściwości chmury w konsoli programu VMM hello.
13. Kliknij przycisk **dalej** toocomplete hello procesu. Po rejestracji metadane z serwera VMM hello są pobierane przez usługę Azure Site Recovery. Serwer Hello jest wyświetlany na powitania **serwery VMM** kartę na powitania **serwerów** strony w magazynie hello.

    ![Ostatnia strona](./media/site-recovery-vmm-to-azure-classic/provider13.PNG)

Po rejestracji metadane z serwera VMM hello są pobierane przez usługę Azure Site Recovery. Serwer Hello jest wyświetlany na powitania **serwery VMM** kartę na powitania **serwerów** strony w magazynie hello.

### <a name="command-line-installation"></a>Instalacja przy użyciu wiersza polecenia
Witaj dostawcy usługi Azure Site Recovery można również zainstalować przy użyciu hello następującego wiersza polecenia. Ta metoda może być używana tooinstall hello dostawcy w rdzeniu serwera dla systemu Windows Server 2012 R2.

1. Pobierz hello dostawcy plików i rejestracji klucza tooa folder instalacji. Na przykład C:\ASR.
2. Zatrzymaj usługę programu System Center Virtual Machine Manager hello
3. Z wiersza polecenia z podwyższonym poziomem uprawnień Wyodrębnij Instalatora dostawcy hello przy użyciu następujących poleceń:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Zainstaluj dostawcę hello w następujący sposób:

        C:\ASR> setupdr.exe /i
5. Zarejestruj hello dostawcę w następujący sposób:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>       

gdzie parametry są następujące:

* **/ Credentials** : obowiązkowy parametr, który określa lokalizację hello, w których hello znajduje się plik klucza rejestracji  
* **/ FriendlyName** : obowiązkowy parametr dla nazwy powitania serwera hosta hello funkcji Hyper-V, która jest wyświetlana w portalu usługi Azure Site Recovery hello.
* **/ EncryptionEnabled** : opcjonalny parametr toospecify, jeśli chcesz tooencryption maszynach wirtualnych platformy Azure (szyfrowanie danych w rest). Nazwa pliku Hello powinna mieć **PFX** rozszerzenia.
* **/ proxyaddress** : opcjonalny parametr określający adres hello powitania serwera proxy.
* **/ proxyport** : opcjonalny parametr określający port hello powitania serwera proxy.
* **/ proxyusername** : opcjonalny parametr określający nazwę użytkownika serwera proxy hello.
* **/ proxypassword** : opcjonalny parametr określający hasło serwera proxy hello.  

## <a name="step-4-create-an-azure-storage-account"></a>Krok 4. Tworzenie konta magazynu platformy Azure
1. Jeśli nie masz konta magazynu Azure, kliknij przycisk **Dodaj konto magazynu Azure** toocreate konta.
2. Utwórz konto z włączoną funkcją replikacji geograficznej. Musi w tym samym regionie co usługa Azure Site Recovery hello hello i być skojarzone z hello tej samej subskrypcji.

    ![Konto magazynu](./media/site-recovery-vmm-to-azure-classic/storage.png)

> [!NOTE]
> [Migracji kont magazynu](../azure-resource-manager/resource-group-move-resources.md) między zasobów grup poziomu hello tej samej subskrypcji lub różnych subskrypcji nie jest obsługiwana dla konta magazynu służące do wdrażania usługi Site Recovery.
>
>

## <a name="step-5-install-hello-azure-recovery-services-agent"></a>Krok 5: Instalowanie hello agenta usług odzyskiwania Azure
Zainstaluj agenta usług odzyskiwania Azure hello na każdym serwerze hosta funkcji Hyper-V w chmurze VMM hello.

1. Kliknij przycisk **Szybki Start** > **Pobierz agenta usług odzyskiwania lokacji Azure do instalacji na hostach** tooobtain hello najnowszą wersję pliku instalacyjnego agenta hello.

    ![Instalowanie agenta Usług odzyskiwania](./media/site-recovery-vmm-to-azure-classic/install-agent.png)
2. Uruchom plik instalacyjny hello na każdym serwerze hosta funkcji Hyper-V.
3. Na powitania **Sprawdzanie wymagań wstępnych** kliknij **dalej**. Wszystkie brakujące wymagania wstępne zostaną zainstalowane automatycznie.

    ![Wymagania wstępne dotyczące agenta Usług odzyskiwania](./media/site-recovery-vmm-to-azure-classic/agent-prereqs.png)
4. Na powitania **ustawienia instalacji** strony, określ, gdzie chcesz tooinstall hello agent i wybierz hello lokalizacji pamięci podręcznej, w którym będą instalowane metadane kopii zapasowej. Następnie kliknij pozycję **Zainstaluj**.
5. Po zakończeniu instalacji kliknij przycisk **Zamknij** toocomplete hello kreatora.

    ![Rejestracja agenta MARS](./media/site-recovery-vmm-to-azure-classic/agent-register.png)

### <a name="command-line-installation"></a>Instalacja przy użyciu wiersza polecenia
Witaj agenta usług odzyskiwania Microsoft Azure można także zainstalować z wiersza polecenia hello za pomocą tego polecenia:

    marsagentinstaller.exe /q /nu

## <a name="step-6-configure-cloud-protection-settings"></a>Krok 6. Konfigurowanie ustawień ochrony chmury
Po zarejestrowaniu serwera VMM hello, można skonfigurować ustawienia ochrony chmury. Włączona opcja hello **Synchronizuj dane chmury z magazynem hello** podczas instalowania dostawcy hello więc wszystkich chmur na serwerze VMM hello pojawią się w hello <b>chronione elementy</b> kartę w magazynie hello.

![Opublikowana chmura](./media/site-recovery-vmm-to-azure-classic/clouds-list.png)

1. Na stronie Szybki Start powitania kliknij **Konfigurowanie ochrony dla chmur programu VMM**.
2. Na powitania **chronione elementy** , kliknij pozycję w chmurze hello mają tooconfigure i przejdź toohello **konfiguracji** kartę.
3. W polu **Lokalizacja docelowa** wybierz pozycję **Azure**.
4. W **konta magazynu** wybierz konto magazynu Azure hello używanego do replikacji.
5. Ustaw **Szyfruj przechowywane dane** za**poza**. To ustawienie określa, czy dane powinny być szyfrowane podczas replikacji między lokacją lokalną hello i platformą Azure.
6. W **częstotliwość kopiowania** pozostaw ustawienie domyślne hello. Ta wartość określa, jak często dane mają być synchronizowane między lokalizacjami źródłowymi a docelowymi.
7. W **Zachowaj punkty odzyskiwania dla**, pozostaw ustawienie domyślne hello. Wartość domyślna równa zero tylko hello najnowszy punkt odzyskiwania dla podstawowej maszyny wirtualnej są przechowywane na serwerze hosta repliki.
8. W **częstotliwość migawek spójnych z aplikacją**, pozostaw ustawienie domyślne hello. Ta wartość określa, jak często toocreate migawki. Migawki używają tooensure usługi kopiowania woluminów w tle (VSS), które aplikacje są w spójnym stanie podczas hello migawki.  Jeśli ustawisz wartość, upewnij się, że jest mniejsza niż liczba hello dodatkowych punktów odzyskiwania, które można skonfigurować.
9. W **czas rozpoczęcia replikacji**, określ rozpoczęcia replikacji początkowej tooAzure danych. Strefa czasowa Hello na serwerze hosta funkcji Hyper-V hello będą używane. Firma Microsoft zaleca, aby zaplanować hello replikacji początkowej poza godzinami szczytu.

    ![Ustawienia replikacji chmury](./media/site-recovery-vmm-to-azure-classic/cloud-settings.png)

Po zapisaniu ustawień hello zadania zostanie utworzone i mogą być monitorowane na powitania **zadania** kartę. Wszystkie serwery hosta funkcji Hyper-V w hello chmura źródłowa programu VMM zostaną skonfigurowane do replikacji.

Zapisane ustawienia chmury można modyfikować na powitania **Konfiguruj** kartę toomodify hello docelowej lokalizacji lub docelowego konta magazynu będzie wymagana Konfiguracja chmury hello tooremove, a następnie ponownie skonfigurować hello chmury. Należy pamiętać, że jeśli zmienisz zmiany hello konta magazynu hello jest stosowane tylko dla maszyn wirtualnych, które są włączone dla ochrony po zmodyfikowaniu hello konta magazynu. Istniejące maszyny wirtualne nie są migrowane toohello nowe konto magazynu.

## <a name="step-7-configure-network-mapping"></a>Krok 7. Konfigurowanie mapowania sieci
Przed rozpoczęciem mapowania sieci Sprawdź, czy maszyny wirtualne na źródłowym serwerze programu VMM hello są połączone tooa sieci maszyny Wirtualnej. Ponadto należy utworzyć co najmniej jedną sieć wirtualną platformy Azure. Należy zauważyć, że wiele sieci maszyn wirtualnych mogą być mapowane tooa pojedynczej sieci platformy Azure.

1. Na stronie Szybki Start powitania kliknij **Mapuj sieci**.
2. Na powitania **sieci** karcie **lokalizacja źródłowa**, wybierz pozycję hello źródłowym serwerze programu VMM. W polu **Lokalizacja docelowa** wybierz pozycję Azure.
3. W **źródła** sieci lista sieci maszyny Wirtualnej skojarzone z serwerem VMM hello są wyświetlane. W **docelowej** sieci hello Azure sieci skojarzone z subskrypcją hello są wyświetlane.
4. Wybierz hello źródłowej sieci maszyny Wirtualnej, a następnie kliknij przycisk **mapy**.
5. Na powitania **Wybieranie sieci docelowej** stronie powitania Wybierz docelową sieć platformy Azure, które chcesz toouse.
6. Kliknij przycisk hello — proces mapowania hello toocomplete znacznik wyboru.

    ![Ustawienia replikacji chmury](./media/site-recovery-vmm-to-azure-classic/map-networks.png)

Po zapisaniu ustawień hello postęp mapowania hello tootrack uruchomienia zadania i mogą być monitorowane na karcie zadania hello. Wszystkie istniejące maszyny wirtualne repliki odpowiadające źródłowej sieci maszyny Wirtualnej toohello zostaną połączone toohello docelowymi sieciami platformy Azure. Nowych maszyn wirtualnych, które są połączone toohello źródłowej sieci maszyny Wirtualnej zostaną połączone toohello mapowanej sieci platformy Azure po replikacji. Jeśli zmodyfikujesz istniejące mapowanie, uwzględniając nową sieć maszyn wirtualnych repliki zostaną podłączone z wykorzystaniem nowych ustawień hello.

Należy pamiętać, że jeśli hello Sieć docelowa ma wiele podsieci i jedna z tych podsieci ma hello znajduje się samą nazwę jak podsieć, w których hello źródłowej maszyny wirtualnej, a następnie hello repliki maszyny wirtualnej zostaną połączone toothat docelowej podsieci po pracy awaryjnej. Jeśli nie ma żadnych docelowa podsieć o pasującej nazwie, maszyna wirtualna hello będzie toohello połączonych pierwszej podsieci w sieci hello.

> [!NOTE]
> [Migracja sieci](../azure-resource-manager/resource-group-move-resources.md) między zasobów grup poziomu hello tej samej subskrypcji lub różnych subskrypcji nie jest obsługiwana dla sieci używane do wdrażania usługi Site Recovery.
>
>

## <a name="step-8-enable-protection-for-virtual-machines"></a>Krok 8. Włączanie ochrony dla maszyn wirtualnych
Po serwerów, chmur i sieci są skonfigurowane poprawnie, można włączyć ochrony dla maszyn wirtualnych w chmurze hello. Należy uwzględnić następujące hello:

* Maszyny wirtualne muszą spełniać [wymagania związane z platformą Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
* dla maszyny wirtualnej hello musi być ustawiona systemu operacyjnego hello ochrony tooenable i właściwości dysku systemu operacyjnego. Podczas tworzenia maszyny wirtualnej w programie VMM przy użyciu szablonu maszyny wirtualnej można ustawić właściwości hello. Można również ustawić te właściwości dla istniejących maszyn wirtualnych na powitania **ogólne** i **konfiguracja sprzętu** karty hello właściwości maszyny wirtualnej. Jeśli nie ustawisz tych właściwości w programie VMM będziesz w stanie tooconfigure je w portalu usługi Azure Site Recovery hello.

    ![Tworzenie maszyny wirtualnej](./media/site-recovery-vmm-to-azure-classic/enable-new.png)

    ![Modyfikowanie właściwości maszyny wirtualnej](./media/site-recovery-vmm-to-azure-classic/enable-existing.png)

1. ochronę tooenable hello **maszyn wirtualnych** w chmurze hello, w których hello znajduje się maszyny wirtualnej, kliknij pozycję **Włącz ochronę** > **Dodawanie maszyn wirtualnych**.
2. Z listy hello maszyn wirtualnych w chmurze hello wybierz hello, co ma tooprotect.

    ![Włączanie ochrony maszyny wirtualnej](./media/site-recovery-vmm-to-azure-classic/select-vm.png)

    Śledzenie postępu hello **Włącz ochronę** akcji w hello **zadania** kartę, w tym hello replikacji początkowej. Po hello **zakończenia ochrony** zadania działa hello maszyny wirtualnej jest gotowy do trybu failover. Po włączeniu ochrony i zreplikowaniu maszyn wirtualnych, będziesz w stanie tooview je na platformie Azure.

    ![Zadanie ochrony maszyny wirtualnej](./media/site-recovery-vmm-to-azure-classic/vm-jobs.png)

1. Sprawdź właściwości maszyny wirtualnej hello i zmodyfikuj zgodnie z potrzebami.

    ![Weryfikowanie maszyn wirtualnych](./media/site-recovery-vmm-to-azure-classic/vm-properties.png)
2. Na powitania **Konfiguruj** kartę właściwości maszyny wirtualnej hello poniższe właściwości sieci może być modyfikowany.

* **Liczba kart sieciowych na docelowej maszynie wirtualnej hello** -hello liczbę kart sieciowych jest zależna hello rozmiaru określonego dla docelowej maszyny wirtualnej hello. Sprawdź [specyfikacje rozmiaru maszyny wirtualnej](../virtual-machines/linux/sizes.md) hello liczbę kart sieciowych obsługiwanych przez hello rozmiar maszyny wirtualnej. Podczas modyfikowania hello rozmiar maszyny wirtualnej i Zapisz ustawienia hello hello liczbę kart sieciowych zmieni hello następnym otwarciu hello **Konfiguruj** strony. Witaj liczbę kart sieciowych docelowych maszyn wirtualnych jest hello minimalną liczbę kart sieciowych na źródłowej maszyny wirtualnej i hello maksymalną liczbę kart sieciowych obsługiwanych przez rozmiar hello hello maszyny wirtualnej, w następujący sposób:

  * Jeśli hello liczbę kart sieciowych na maszynie źródłowej hello jest mniejsza lub równa toohello liczba kart dozwoloną dla rozmiaru maszyny docelowej hello, a następnie hello docelowa będzie mieć hello samą liczbę kart sieciowych jako źródło hello.
  * Jeśli hello liczbę kart sieciowych dla źródłowej maszyny wirtualnej hello przekracza liczbę hello dozwoloną dla hello rozmiar docelowy, a następnie maksymalny rozmiar docelowy hello będą używane.
  * Na przykład jeśli maszyna źródłowa ma dwie karty sieciowe, a rozmiar maszyny docelowej hello obsługuje cztery, maszyna docelowa hello będzie mieć dwie karty sieciowe. Jeśli hello maszyna źródłowa ma dwie karty sieciowe, ale hello rozmiar docelowy obsługiwanych obsługuje tylko jedną maszyna docelowa hello będzie mieć tylko jedną kartę.     
* **Sieć maszyny wirtualnej docelowy hello** -maszyny wirtualnej hello hello sieci toowhich łączy toois ustaleniami mapowania sieci hello sieci dla źródłowej maszyny wirtualnej. Jeśli hello źródłowa maszyna wirtualna ma więcej niż jeden sieci karty i źródła sieci są sieci zamapowanych toodifferent w lokalizacji docelowej, następnie należy zastosować toochoose jednego hello docelowych sieci.
* **Podsieć każdej karty sieciowej** — dla każdej karty sieciowej, można wybrać hello toowhich podsieci hello przejścia w tryb failover maszyny wirtualnej może zostać nawiązane połączenie.
* **Docelowy adres IP** — Jeśli karta sieciowa hello źródłowej maszyny wirtualnej jest skonfigurowana toouse statycznych adresów IP, a następnie możesz podać adres IP hello hello docelowej maszyny wirtualnej. Ta funkcja zachować hello adres IP źródłowej maszyny wirtualnej po przejściu w tryb failover. Jeśli podano żadnego adresu IP dowolny dostępny adres IP ma nadane toohello karty sieciowej w czasie hello pracy awaryjnej. Jeżeli określono hello docelowy adres IP jest już używany przez inną maszynę wirtualną uruchomioną na platformie Azure następnie trybu failover zakończy się niepowodzeniem.  

    ![Modyfikowanie właściwości sieci](./media/site-recovery-vmm-to-azure-classic/multi-nic.png)

> [!NOTE]
> Maszyny wirtualne systemu Linux ze statycznym adresem IP nie są obsługiwane.
>
>

## <a name="test-hello-deployment"></a>Testowe wdrożenie na powitania
Planowanie wdrożenia możesz uruchomić test trybu failover dla jednej maszyny wirtualnej, lub utworzyć plan odzyskiwania składające się z wielu maszyn wirtualnych, a następnie uruchom test trybu failover dla hello tootest.  

Próba przejścia w tryb failover symuluje mechanizm pracy awaryjnej i odzyskiwania w sieci izolowanej. Należy pamiętać, że:

* Maszyna wirtualna toohello tooconnect na platformie Azure przy użyciu pulpitu zdalnego po hello w tryb failover, należy włączyć Podłączanie pulpitu zdalnego na maszynie wirtualnej hello przed rozpoczęciem powitalne testowy tryb failover.
* Po pracy w trybie failover używasz publicznego adresu IP address tooconnect toohello maszyny Wirtualnej platformy Azure przy użyciu pulpitu zdalnego. Jeśli chcesz toodo to, upewnij się, że nie ma żadnych zasad domeny, które uniemożliwiają łączącego tooa maszyny wirtualnej przy użyciu adresu publicznego.

> [!NOTE]
> tooget hello najlepszą wydajność przechodzenia w tryb failover tooAzure, upewnij się, po zainstalowaniu hello Azure agenta na powitania maszyny Wirtualnej. Przyspiesza to rozruch i pomaga w rozwiązywaniu problemów. Pobierz hello [agenta systemu Linux](https://github.com/Azure/WALinuxAgent), lub hello [agenta Windows](http://go.microsoft.com/fwlink/?LinkID=394789).
>
>

### <a name="create-a-recovery-plan"></a>Tworzenie planu odzyskiwania
1. Na powitania **plany odzyskiwania** , Dodaj nowy plan. Określ nazwę, **VMM** w **typ źródła**i hello źródłowym serwerze programu VMM w **źródła**. Witaj będzie platforma Azure.

    ![Tworzenie planu odzyskiwania](./media/site-recovery-vmm-to-azure-classic/recovery-plan1.png)
2. W hello **wybierz maszyny wirtualne** strony, planu odzyskiwania toohello tooadd wybierz maszyny wirtualne. Te maszyny wirtualne są dodawane planu odzyskiwania toohello grupy domyślnej — Grupa 1. Przetestowano maksymalnie 100 maszyn wirtualnych w pojedynczym planie odzyskiwania.

* Jeśli chcesz właściwości maszyny wirtualnej hello tooverify przed dodaniem toohello planu kliknij maszynę wirtualną hello na stronie właściwości hello hello chmury, w którym się znajduje. Można również skonfigurować właściwości maszyny wirtualnej hello w konsoli programu VMM hello.
* Wszystkich hello maszyn wirtualnych, które są wyświetlane włączono ochronę. Lista Hello zawiera zarówno maszyn wirtualnych, które są włączone dla ochrony i początkowa replikacja została ukończona, a te, które są z włączoną ochroną na replikację początkową. Tylko maszyny wirtualne z ukończoną replikacją początkową mogą przechodzić w tryb failover w ramach planu odzyskiwania.

    ![Tworzenie planu odzyskiwania](./media/site-recovery-vmm-to-azure-classic/select-rp.png)

Po planu odzyskiwania utworzono go w hello pojawi się **plany odzyskiwania** kartę. Można również dodać [elementy runbook automatyzacji Azure](site-recovery-runbook-automation.md) toohello akcji tooautomate planu odzyskiwania w trybie failover.

### <a name="run-a-test-failover"></a>Wykonywanie próby przejścia w tryb failover
Istnieją dwa sposoby toorun tooAzure pracy awaryjnej testu.

* **Testowanie trybu failover bez sieci platformy Azure**— ten test trybu failover sprawdza, czy maszyna wirtualna hello funkcjonuje poprawnie na platformie Azure. Witaj maszyny wirtualnej nie będzie tooany połączonych sieci platformy Azure po pracy awaryjnej.
* **Testowanie trybu failover z siecią platformy Azure**— tego typu kontrole trybu failover, które hello całe środowisko replikacji funkcjonuje zgodnie z oczekiwaniami i tryb failover maszyny wirtualne hello będzie określony docelowy element toohello połączonych sieci platformy Azure. Do obsługi podsieci do testowania trybu failover podsieci hello hello testowej maszyny wirtualnej będzie można znalezienia oparty na powitania podsieci maszyny wirtualnej repliki hello. Jest to inny tooregular replikacji, gdy hello podsieci maszyny wirtualnej repliki jest oparta na podsieci hello hello źródłowej maszyny wirtualnej.

Jeśli chcesz toorun test trybu failover dla maszyny wirtualnej z włączonymi dla ochrony tooAzure bez określania docelowej sieci platformy Azure nie trzeba tooprepare żadnych czynności. toorun test trybu failover z docelową siecią platformy Azure, konieczne będzie toocreate nowej sieci platformy Azure, która jest odizolowana od sieci platformy Azure środowiska produkcyjnego (domyślne zachowanie podczas tworzenia nowej sieci na platformie Azure). Zobacz, jak za[testować tryb failover](site-recovery-failover.md) więcej szczegółów.

Należy również tooset się hello infrastruktury dla hello replikowane maszyny wirtualnej toowork zgodnie z oczekiwaniami. Na przykład maszynę wirtualną z kontrolerem domeny i DNS mogą być replikowane tooAzure przy użyciu usługi Azure Site Recovery i mogą zostać utworzone w sieci testowej hello przy użyciu testowego trybu Failover. Aby uzyskać więcej informacji, zobacz sekcję [Zagadnienia dotyczące testowania trybu failover dla usługi Active Directory](site-recovery-active-directory.md#test-failover-considerations).

toorun testowy tryb failover hello następujące:

1. Na powitania **plany odzyskiwania** , a następnie wybierz hello plan i kliknij przycisk **testowy tryb Failover**.
2. Na powitania **potwierdzić testowy tryb Failover** wybierz **Brak** lub określoną sieć platformy Azure.  Należy pamiętać, że jeśli wybierzesz opcję Brak będzie hello testowy tryb failover Sprawdź, czy hello maszyny wirtualnej została zreplikowana poprawnie tooAzure, ale nie Sprawdzanie konfiguracji sieci replikacji.

    ![Brak sieci](./media/site-recovery-vmm-to-azure-classic/test-no-network.png)
3. Jeśli szyfrowanie danych jest włączone dla chmury hello w **klucza szyfrowania** hello wybierz certyfikat wystawiony podczas instalacji hello dostawcy na serwerze VMM hello, włączenie szyfrowania hello opcja tooenable danych dla chmury .
4. Na powitania **zadania** można śledzić postęp trybu failover. Należy także stanie toosee hello testowa replika maszyny wirtualnej w hello portalu Azure. Jeśli ustawisz zapasowych tooaccess maszyn wirtualnych z sieci lokalnej można zainicjować maszyny wirtualnej toohello połączenia pulpitu zdalnego.
5. Gdy hello w tryb failover osiągnie hello **Ukończ testowanie** fazy, kliknij przycisk **ukończenia testowej** toofinish go. Użytkownik może przejść do szczegółów toohello **zadania** karcie tootrack postęp trybu failover, a stan i tooperform wszystkie akcje, które są potrzebne.
6. Po przejściu w tryb failover zobacz temat hello testowa replika maszyny wirtualnej w portalu Azure hello. Jeśli ustawisz zapasowych tooaccess maszyn wirtualnych z sieci lokalnej można zainicjować maszyny wirtualnej toohello połączenia pulpitu zdalnego. Witaj, po:

   1. Sprawdź pomyślnie uruchomić hello maszyn wirtualnych.
   2. Maszyna wirtualna toohello tooconnect na platformie Azure przy użyciu pulpitu zdalnego po hello w tryb failover, należy włączyć Podłączanie pulpitu zdalnego na maszynie wirtualnej hello przed rozpoczęciem powitalne testowy tryb failover. Należy również tooadd punkt końcowy protokołu RDP na maszynie wirtualnej hello. Można wykorzystać [elementów Runbook automatyzacji Azure](site-recovery-runbook-automation.md) toodo który.
   3. Po przejściu w tryb failover Jeśli używasz publicznego adresu IP address tooconnect toohello maszynę wirtualną na platformie Azure przy użyciu pulpitu zdalnego, upewnij się, że nie ma żadnych zasad domeny, które uniemożliwiają połączenie tooa maszyny wirtualnej przy użyciu adresu publicznego.
7. Po zakończeniu testowania hello hello następujące:

   * Kliknij przycisk **hello testu przejścia w tryb failover**. Czyszczenie hello test środowiska tooautomatically zasilania poza i Usuń hello testowe maszyny wirtualne.
   * Kliknij przycisk **uwagi** toorecord i zapisać wszelkie obserwacje związane z hello testowy tryb failover.


## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej na temat [konfigurowania planów odzyskiwania](site-recovery-create-recovery-plans.md) i [trybu failover](site-recovery-failover.md).
