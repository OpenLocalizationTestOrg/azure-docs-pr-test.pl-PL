---
title: 'Kopia zapasowa Azure: Przygotowanie tooback zapasowe | Dokumentacja firmy Microsoft'
description: "Upewnij się, że środowisko jest przygotowane do tworzenia kopii zapasowych maszyn wirtualnych na platformie Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: Tworzenie kopii zapasowych; Tworzenie kopii zapasowej;
ms.assetid: e87e8db2-b4d9-40e1-a481-1aa560c03395
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 5c3a41b5d3bd56e62ca5f207442867913aa99816
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-environment-tooback-up-resource-manager-deployed-virtual-machines"></a>Przygotowanie Twojego środowiska tooback zapasowych maszyn wirtualnych wdrożonych przez Menedżera zasobów
> [!div class="op_single_selector"]
> * [Model usługi Resource Manager](backup-azure-arm-vms-prepare.md)
> * [Modelu klasycznego](backup-azure-vms-prepare.md)
>
>

Ten artykuł zawiera kroki hello przygotowania tooback Twojego środowiska wdrożonych przez Menedżera zasobów maszyny wirtualnej (VM). Witaj kroki opisane w procedurach hello Użyj hello portalu Azure.  

Witaj usługi Kopia zapasowa Azure ma dwa typy magazynów (Utwórz kopię zapasową magazynów i magazyny usług odzyskiwania) w celu ochrony maszyn wirtualnych. Magazyn kopii zapasowych chroni maszyny wirtualne wdrażane za pomocą hello klasycznego modelu wdrożenia. Chroni magazyn usług odzyskiwania **maszyn wirtualnych zarówno wdrożone w klasycznej lub wdrożeniu usługi Resource Manager**. Należy użyć tooprotect magazyn usług odzyskiwania maszyn wirtualnych wdrożonych przez Menedżera zasobów.

> [!NOTE]
> Platforma Azure ma dwa modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md). Zobacz [przygotowanie Twojego środowiska tooback zapasowych maszyn wirtualnych Azure](backup-azure-vms-prepare.md) szczegółowe informacje na temat pracy z Classic deployment model maszyn wirtualnych.
>
>

Zanim można chronić lub utworzyć kopię zapasową wdrożonych przez Menedżera zasobów maszyny wirtualnej (VM), upewnij się, że istnieją następujące wymagania wstępne:

* Tworzenie magazynu usług odzyskiwania (lub Zidentyfikuj istniejącego magazynu usług odzyskiwania) *w hello tej samej lokalizacji co maszyna wirtualna*.
* Wybierz scenariusz, definiowanie zasad tworzenia kopii zapasowej hello i zdefiniuj tooprotect elementów.
* Sprawdź hello instalacji agenta maszyny Wirtualnej na maszynie wirtualnej.
* Sprawdź łączność z siecią
* Dla maszyn wirtualnych systemu Linux, w przypadku, gdy chcesz toocustomize środowisko tworzenia kopii zapasowej dla aplikacji spójne tworzenie kopii zapasowych wykonaj hello [tooconfigure kroki wstępnie migawki i używany po utworzeniu migawki skryptów](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)

Jeśli znasz te warunki już istnieje w danym środowisku, a następnie kontynuować toohello [kopii zapasowych maszyn wirtualnych artykuł](backup-azure-vms.md). Jeśli muszą tooset się, czy sprawdzanie wszystkich wymagań wstępnych w tym artykule poprowadzi Cię przez tooprepare kroki hello tej wstępnie wymaganego.

##<a name="supported-operating-system-for-backup"></a>Obsługiwany system operacyjny do utworzenia kopii zapasowej
 * **Linux**: usługa Azure Backup obsługuje [dystrybucje zalecane dla platformy Azure](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) z wyjątkiem systemu operacyjnego Linux Core. _Innych Bring-Your-właścicielem — dystrybucje systemu Linux mogą również działać, dopóki agent maszyny Wirtualnej hello jest dostępne na maszynie wirtualnej hello i obsługę języka Python istnieje. Jednak firma Microsoft nie zatwierdza tych dystrybucji dla kopii zapasowej._
 * **Windows Server**: wersje starsze niż Windows Server 2008 R2 nie są obsługiwane.

## <a name="limitations-when-backing-up-and-restoring-a-vm"></a>Ograniczenia w przypadku tworzenia kopii zapasowej i przywracanie maszyny Wirtualnej
Aby przygotować środowisko, nieprzesyłanie hello ograniczenia.

* Tworzenie kopii zapasowych maszyn wirtualnych z więcej niż 16 dysków danych nie jest obsługiwane.
* Tworzenie kopii zapasowych maszyn wirtualnych z danymi dysku o rozmiarze przekraczającym 1023GB nie jest obsługiwane.
* Tworzenie kopii zapasowych maszyn wirtualnych z zastrzeżonego adresu IP i nie zdefiniowanych punktów końcowych nie jest obsługiwane.
* Kopia zapasowa maszyn wirtualnych jest szyfrowana przy użyciu tylko BEK nie jest obsługiwane. Kopia zapasowa szyfrowane przy użyciu szyfrowania LUKS maszyn wirtualnych systemu Linux nie jest obsługiwane.
* Kopia zapasowa maszyn wirtualnych na skali limit konfiguracji serwera plików nie jest zalecane.
* Dane kopii zapasowej nie zawiera tooVM dołączone dyski sieciowe zainstalowane.
* Zamiana istniejącej maszyny wirtualnej podczas przywracania nie jest obsługiwana. Przy próbie hello toorestore maszyny Wirtualnej, gdy istnieje hello maszyny Wirtualnej, hello przywracania kończy się niepowodzeniem.
* Region między kopii zapasowej i przywracania nie są obsługiwane.
* Można tworzyć kopie zapasowe maszyn wirtualnych we wszystkich regionach publicznej platformy Azure (zobacz hello [Lista kontrolna](https://azure.microsoft.com/regions/#services) obsługiwanych regionów). Jeśli obecnie jest obsługiwany region hello, którego szukasz, nie zostanie wyświetlony na liście rozwijanej hello podczas tworzenia magazynu.
* Przywracanie kontrolera domeny (DC) maszyny Wirtualnej, która jest częścią konfiguracji kontrolera domeny na wielu jest obsługiwane tylko za pomocą programu PowerShell. Przeczytaj więcej na temat [Przywracanie kontrolera domeny, kontrolera domeny na wielu](backup-azure-restore-vms.md#restoring-domain-controller-vms).
* Przywracanie maszyn wirtualnych, które mają następujące konfiguracje sieciowe specjalne hello jest obsługiwane tylko za pomocą programu PowerShell. Maszyny wirtualne utworzone za pomocą przepływu pracy przywracania hello w hello interfejsu użytkownika nie będą miały te konfiguracje sieci, po zakończeniu operacji przywracania hello. toolearn więcej, zobacz [przywracanie maszyn wirtualnych z konfiguracjami sieci specjalne](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations).
  * Maszyny wirtualne znajdujące się w konfiguracji usługi równoważenia obciążenia (wewnętrznych i zewnętrznych)
  * Maszyny wirtualne z wielu zastrzeżonych adresów IP
  * Maszyny wirtualne z wieloma kartami sieciowymi

## <a name="create-a-recovery-services-vault-for-a-vm"></a>Tworzenie magazynu usługi Recovery Services dla maszyny wirtualnej
Magazyn usług odzyskiwania jest jednostka, która przechowuje hello kopie zapasowe i punkty odzyskiwania, które zostały utworzone w czasie. Magazyn usług odzyskiwania Hello zawiera również zasady tworzenia kopii zapasowej hello skojarzone z hello chronionych maszyn wirtualnych.

toocreate odzyskiwania usług magazynu:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/).
2. W menu Centrum powitania kliknij **Przeglądaj** i hello listy zasobów, wpisz **usług odzyskiwania**. Po rozpoczęciu wpisywania, spowoduje odfiltrowanie listy hello oparte na dane wejściowe. Kliknij opcję **Magazyn Usług odzyskiwania**.

    ![Kliknij przycisk Przeglądaj hello i wpisz usług odzyskiwania. Po wyświetleniu usług odzyskiwania hello opcji magazynu, kliknij go tooopen hello blok magazyn usług odzyskiwania.](./media/backup-azure-arm-vms-prepare/browse-to-rs-vaults-updated.png) <br/>

    zostanie wyświetlona lista Hello Magazyny usług odzyskiwania.
3. Na powitania **Magazyny usług odzyskiwania** menu, kliknij przycisk **Dodaj**.

    ![Tworzenie magazynu Usług odzyskiwania — krok 2](./media/backup-azure-arm-vms-prepare/rs-vault-menu.png)

    Usługi odzyskiwania Hello zostanie otwarty blok magazyn monitem tooprovide **nazwa**, **subskrypcji**, **grupy zasobów**, i **lokalizacji**.

    ![Tworzenie magazynu Usług odzyskiwania — krok 5](./media/backup-azure-arm-vms-prepare/rs-vault-attributes.png)
4. Aby uzyskać **nazwa**, wprowadź przyjazną nazwę tooidentify hello magazynu. Nazwa Hello musi toobe unikatowy dla hello subskrypcji platformy Azure. Wpisz nazwę o długości od 2 do 50 znaków. Musi ona rozpoczynać się od litery i może zawierać tylko litery, cyfry i łączniki.
5. Kliknij przycisk **subskrypcji** toosee hello listę dostępnych subskrypcji. Jeśli nie masz pewności, który toouse subskrypcji, użyj domyślnej hello (lub sugerowane) subskrypcji. Większa liczba opcji do wyboru będzie dostępna tylko w przypadku, gdy konto organizacji jest skojarzone z wieloma subskrypcjami platformy Azure.
6. Kliknij przycisk **grupy zasobów** toosee hello listę dostępnych grup zasobów, lub kliknij przycisk **nowy** toocreate nową grupę zasobów. Pełne informacje na temat grup zasobów można znaleźć w temacie [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
7. Kliknij przycisk **lokalizacji** tooselect hello region geograficzny magazynu hello. Magazyn Hello **musi** w hello hello maszyn wirtualnych, które mają tooprotect tego samego regionu.

   > [!IMPORTANT]
   > Jeśli nie wiesz hello lokalizacji, w której istnieje maszyna wirtualna, Zamknij z okna dialogowego Tworzenie magazynu hello i przejdź toohello listę maszyn wirtualnych w portalu hello. Jeśli masz maszyny wirtualne w wielu regionach, konieczne będzie toocreate magazynu usług odzyskiwania w każdym regionie. Utwórz magazyn hello w miejscu pierwszego hello przed przejściem do następnej lokalizacji toohello. Nie ma żadnych kont magazynu toospecify potrzeby toostore hello kopii zapasowej danych--hello magazyn usług odzyskiwania i obsługiwać to automatycznie hello usługi Kopia zapasowa Azure.
   >
   >

8. Kliknij przycisk **Utwórz**. Może upłynąć trochę czasu zanim hello toobe utworzony magazyn usług odzyskiwania. Monitoruje powiadomienia o stanie hello hello górnym obszarze po prawej stronie w portalu hello. Po utworzeniu magazynu zostanie wyświetlony hello listę magazynów usług odzyskiwania. Jeśli nie widzisz magazynu, kliknij przycisk **Odśwież** do

    ![Lista magazynów kopii zapasowych](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

    Po utworzeniu magazynu, Dowiedz się, jak tooset hello replikacji magazynu.

## <a name="set-storage-replication"></a>Konfigurowanie replikacji magazynu
opcji replikacji magazynu Hello umożliwia toochoose między magazynu geograficznie nadmiarowego i lokalnie nadmiarowego magazynu. Domyślnie magazyn jest nadmiarowy geograficznie. Pozostaw hello opcji set toogeo nadmiarowego magazynu, jeśli jest to Twoja podstawowa kopia zapasowa. Wybierz magazyn lokalnie nadmiarowy, jeśli chcesz skorzystać z tańszej, ale mniej trwałej opcji.

ustawienia replikacji magazynu hello tooedit:

1. Na powitania **Magazyny usług odzyskiwania** bloku, wybierz magazyn.
    Po kliknięciu magazynu hello blok ustawień (*mającego nazwę hello magazynu hello u góry hello*) i otwiera blok zawiera szczegóły hello magazynu.

    ![Wybierz magazyn z hello lista magazynów kopii zapasowych](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)

2. Na powitania **ustawienia** bloku, użyj hello pionowej kontrolce slider tooscroll dół toohello **Zarządzaj** sekcji. Kliknij przycisk **infrastruktura kopii zapasowej** tooopen jego bloku. W hello **ogólne** kliknij sekcję **konfiguracji kopii zapasowej** tooopen jego bloku. Na powitania **konfiguracji kopii zapasowej** bloku, wybierz hello opcji replikacji magazynu dla magazynu. Domyślnie magazyn jest nadmiarowy geograficznie. Jeśli zmienisz typ replikacji magazynu powitania kliknij **zapisać**.

    ![Lista magazynów kopii zapasowych](./media/backup-azure-arm-vms-prepare/full-blade.png)

     Jeśli używasz platformy Azure jako punktu końcowego podstawowego magazynu kopii zapasowych, kontynuuj korzystanie z magazynu geograficznie nadmiarowego. Jeśli używasz platformy Azure jako punktu końcowego magazynu kopii zapasowych innego niż podstawowy, następnie wybierz magazyn lokalnie nadmiarowy. Przeczytaj więcej na temat [geograficznie nadmiarowego](../storage/common/storage-redundancy.md#geo-redundant-storage) i [magazyn lokalnie nadmiarowy](../storage/common/storage-redundancy.md#locally-redundant-storage) opcje magazynu w hello [Omówienie replikacji usługi Azure Storage](../storage/common/storage-redundancy.md).
    Po wybraniu opcji magazynu powitania dla magazynu, wszystko jest gotowe tooassociate hello maszyn wirtualnych z magazynem hello. toobegin hello skojarzenia, należy odnaleźć i zarejestrować hello maszyn wirtualnych platformy Azure.

## <a name="select-a-backup-goal-set-policy-and-define-items-tooprotect"></a>Wybierz cel kopii zapasowej, ustawienie zasad i zdefiniowanie tooprotect elementów
Przed zarejestrowaniem maszyny Wirtualnej w magazynie, uruchom tooensure procesu odnajdywania hello rozpoznaniem żadnych nowych maszyn wirtualnych, które zostały dodane toohello subskrypcji. kwerendy procesu Hello Azure hello listę maszyn wirtualnych w subskrypcji hello, wraz z dodatkowymi informacjami, takie jak nazwa usługi w chmurze hello i hello regionu. W hello portalu Azure scenariusz odnosi się do magazynu usług odzyskiwania hello ma tooput toowhat. Zasady są harmonogram hello kiedy i jak często są pobierane punktów odzyskiwania. Zasady obejmują również zakres przechowywania hello hello punktów odzyskiwania.

1. Jeśli masz już magazyn usług odzyskiwania, Otwórz, przejdź toostep 2. Jeśli nie masz magazyn usług odzyskiwania, Otwórz, a następnie otwórz hello [portalu Azure](https://portal.azure.com/) i w menu Centrum powitania kliknij **więcej usług**.

   * Na liście hello zasobów, wpisz **usług odzyskiwania**.
   * Po rozpoczęciu wpisywania, spowoduje odfiltrowanie listy hello oparte na dane wejściowe. Po wyświetleniu pozycji **Magazyny Usług odzyskiwania** kliknij ją.

     ![Tworzenie magazynu usługi Recovery Services — krok 1](./media/backup-azure-arm-vms-prepare/browse-to-rs-vaults-updated.png) <br/>

     zostanie wyświetlona lista Hello Magazyny usług odzyskiwania. Jeśli w Twojej subskrypcji nie żadnego magazynu, ta lista będzie pusta.

    ![Lista magazynów widoku hello usług odzyskiwania](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

   * Z listy hello Magazyny usług odzyskiwania wybierz tooopen magazynu jego pulpitu nawigacyjnego.

     Blok ustawień Hello i hello magazynu, odwiedź pulpit nawigacyjny hello wybrany magazyn, zostanie otwarty.

     ![Otwarcie bloku magazynu](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)
2. W menu nawigacyjnym magazynu hello kliknij **kopii zapasowej** tooopen hello kopii zapasowej bloku.

    ![Otwarcie bloku Kopia zapasowa](./media/backup-azure-arm-vms-prepare/backup-button.png)

    Otwórz Hello tworzenia kopii zapasowej i cel kopii zapasowej blokach.

    ![Otwarcie bloku scenariusza](./media/backup-azure-arm-vms-prepare/select-backup-goal-1.png)

3. Na powitania bloku celu kopii zapasowej, należy ustawić **gdzie działa Twoje obciążenie** tooAzure i **co chcesz toobackup** tooVirtual komputera, a następnie kliknij przycisk **OK**.

    W magazynie hello to rejestruje hello rozszerzenia maszyny Wirtualnej. Hello zamyka bloku celu kopii zapasowej i hello **kopii zapasowej zasad** zostanie otwarty blok.

    ![Otwarcie bloku scenariusza](./media/backup-azure-arm-vms-prepare/select-backup-goal-2.png)
4. W bloku zasad tworzenia kopii zapasowej hello wybierz zasady tworzenia kopii zapasowej hello ma tooapply toohello magazynu.

    ![Wybór zasad tworzenia kopii zapasowej](./media/backup-azure-arm-vms-prepare/setting-rs-backup-policy-new.png)

    Szczegóły Hello hello domyślne zasady są wyświetlane w menu rozwijanym hello. Jeśli chcesz toocreate nowe zasady, wybierz opcję **Utwórz nowy** z menu rozwijanego hello. Instrukcje dotyczące definiowania zasad tworzenia kopii zapasowych można znaleźć w sekcji [Definiowanie zasad tworzenia kopii zapasowej](backup-azure-vms-first-look-arm.md#defining-a-backup-policy).
    Kliknij przycisk **OK** tooassociate hello zasad tworzenia kopii zapasowej w magazynie hello.

    Witaj zamknięciu bloku zasady tworzenia kopii zapasowej i hello **wybierz maszyny wirtualne** zostanie otwarty blok.
5. W hello **wybierz maszyny wirtualne** bloku, wybierz hello tooassociate maszyn wirtualnych z hello określone zasady i kliknij przycisk **OK**.

    ![Wybieranie obciążenia](./media/backup-azure-arm-vms-prepare/select-vms-to-backup.png)

    maszyny wirtualnej wybrany Hello jest weryfikowana. Jeżeli nie hello maszyn wirtualnych, że oczekiwany toosee, sprawdź, czy istnieją one w tej samej lokalizacji platformy Azure jako hello magazyn usług odzyskiwania i nie są już chronione w innym magazynie hello. na pulpicie nawigacyjnym magazynu hello wyświetlana jest lokalizacja Hello powitalne magazyn usług odzyskiwania.

6. Teraz, gdy zdefiniowano wszystkich ustawień dla magazynu hello w hello bloku kopii zapasowej kliknij **włączenia kopii zapasowej**. Powoduje to wdrożenie hello zasad toohello magazyn i hello maszyn wirtualnych. Nie tworzy hello początkowego punktu odzyskiwania dla maszyny wirtualnej hello.

    ![Włączenie kopii zapasowej](./media/backup-azure-arm-vms-prepare/vm-validated-click-enable.png)

Po pomyślnym włączeniu kopii zapasowej hello zasad tworzenia kopii zapasowej będą wykonywane zgodnie z harmonogramem. Jeśli chcesz toogenerate tooback zadanie tworzenia kopii zapasowej na żądanie zapasowych hello maszyn wirtualnych teraz, zobacz [zadanie tworzenia kopii zapasowej hello Triggering](./backup-azure-arm-vms.md#triggering-the-backup-job).

Jeśli masz problemy z zarejestrowaniem hello maszyny wirtualnej, zobacz hello następujących informacji na temat instalowania hello agenta maszyny Wirtualnej i łączność sieciową. Prawdopodobnie nie potrzebujesz hello następujących informacji w przypadku ochrony maszyn wirtualnych utworzonych na platformie Azure. Jednak po migracji maszyn wirtualnych na platformie Azure, następnie upewnij się, że poprawnie zainstalowano agenta maszyny Wirtualnej hello i maszyny wirtualnej można komunikować się z siecią wirtualną hello.

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Zainstaluj hello agenta maszyny Wirtualnej na maszynie wirtualnej hello
Witaj Agent maszyny Wirtualnej musi być zainstalowany na powitania maszyny wirtualnej platformy Azure dla hello kopii zapasowej rozszerzenia toowork. Jeśli maszyna wirtualna została utworzona z hello galerii Azure, następnie hello agenta maszyny Wirtualnej jest już obecny w maszynie wirtualnej hello. Informacje dotyczące sytuacji hello, gdzie są *nie* przy użyciu maszyny Wirtualnej utworzone na podstawie hello galerii Azure — na przykład w przypadku migracji maszyny Wirtualnej z lokalnego centrum danych. W takim przypadku hello agenta maszyny Wirtualnej musi toobe zainstalowany na maszynie wirtualnej hello tooprotect kolejności. Dowiedz się więcej o hello [agenta maszyny Wirtualnej](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux).

Jeśli masz problemy z tworzenia kopii zapasowej hello maszyny Wirtualnej platformy Azure, sprawdź, czy Agent maszyny Wirtualnej hello jest poprawnie zainstalowany na maszynie wirtualnej hello (patrz poniższa tabela hello). w poniższej tabeli Hello udostępnia dodatkowe informacje o hello VM Agent dla systemu Windows i maszyn wirtualnych systemu Linux.

| **Operacja** | **Windows** | **Linux** |
| --- | --- | --- |
| Instalowanie hello agenta maszyny Wirtualnej |Pobierz i zainstaluj hello [pliku MSI agenta](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Konieczne będzie instalacji hello toocomplete uprawnienia administratora. |<li> Zainstaluj najnowsze hello [agenta systemu Linux](../virtual-machines/linux/agent-user-guide.md). Konieczne będzie instalacji hello toocomplete uprawnienia administratora. Zaleca się zainstalowanie agenta z repozytorium dystrybucji. Firma Microsoft **nie jest zalecane** Instalowanie agenta maszyny Wirtualnej systemu Linux bezpośrednio z usługi github.  |
| Aktualizowanie hello agenta maszyny Wirtualnej |Aktualizowanie hello agenta maszyny Wirtualnej jest tak proste, jak ponowne zainstalowanie hello [plików binarnych agenta maszyny Wirtualnej](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br>Upewnij się, że żadna operacja tworzenia kopii zapasowej działa podczas aktualizowania hello agenta maszyny Wirtualnej. |Wykonaj instrukcje hello [aktualizowanie hello agenta maszyny Wirtualnej systemu Linux](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Firma Microsoft zaleca aktualizacji agenta z repozytorium dystrybucji. Firma Microsoft **nie jest zalecane** aktualizacji agenta maszyny Wirtualnej systemu Linux bezpośrednio z usługi github.<br>Upewnij się, że podczas powitalne agenta maszyny Wirtualnej jest aktualizowana działa żadna operacja tworzenia kopii zapasowej. |
| Sprawdzanie poprawności instalacji agenta maszyny Wirtualnej hello |<li>Przejdź toohello *C:\WindowsAzure\Packages* folderu w hello maszyny Wirtualnej platformy Azure. <li>Powinien znajdować się plik WaAppAgent.exe hello jest obecny.<li> Kliknij prawym przyciskiem myszy plik hello znajduje się zbyt**właściwości**, a następnie wybierz hello **szczegóły** kartę hello wersji produktu pole powinno być 2.6.1198.718 lub nowszej. |Nie dotyczy |

### <a name="backup-extension"></a>Rozszerzenie kopii zapasowej
Raz powitalne Agent maszyny Wirtualnej jest zainstalowany na maszynie wirtualnej hello hello usługi Kopia zapasowa Azure instaluje hello zapasowy numer wewnętrzny toohello agenta maszyny Wirtualnej. Witaj usługi Kopia zapasowa Azure bezproblemowo uaktualniania i poprawek hello zapasowy numer wewnętrzny.

zapasowy numer wewnętrzny Hello jest zainstalowana przez usługę tworzenia kopii zapasowej hello hello maszyna wirtualna jest uruchomiona lub nie. Uruchomionych maszynach wirtualnych zapewnia największe prawdopodobieństwo hello pobieranie punktów odzyskiwania zapewniających spójność aplikacji. Jednak hello usługi Kopia zapasowa Azure nadal tooback się hello maszyny Wirtualnej, nawet jeśli jest wyłączony i nie można zainstalować rozszerzenia hello. To tzw. „maszyna wirtualna offline”. W takim przypadku hello punkt odzyskiwania będzie *awaria spójne*.

## <a name="network-connectivity"></a>Połączenie sieciowe
W kolejności toomanage hello migawki maszyny Wirtualnej, zapasowy numer wewnętrzny hello musi mieć łączność toohello Azure publicznych adresów IP. Bez hello prawo łączność z Internetem, maszyny wirtualnej hello HTTP żądania limitu czasu i hello kopii zapasowej kończy się niepowodzeniem. Jeśli wdrożenie obowiązują ograniczenia dostępu w (za pośrednictwem sieciową grupę zabezpieczeń (NSG), na przykład), wybierz jedną z następujących opcji do prezentowania wyczyść ścieżki dla kopii zapasowej ruchu:

* [Zakresy IP centrum danych Azure hello dozwolonych](http://www.microsoft.com/en-us/download/details.aspx?id=41653) — zobacz artykuł hello instrukcje w sposób toowhitelist hello adresów IP.
* Wdrażanie serwera proxy HTTP dla routingu ruchu.

Podczas wybierania który toouse opcji, kompromisy hello należą do zakresu od możliwości zarządzania, kontrolę i kosztów.

| Opcja | Zalety | Wady |
| --- | --- | --- |
| Lista dozwolonych adresów IP, zakresów |Brak dodatkowych kosztów.<br><br>Do otwierania dostępu w grupy NSG, użyj hello <i>AzureNetworkSecurityRule zestaw</i> polecenia cmdlet. |Złożone toomanage jako hello wpływ zmiany zakresów adresów IP w czasie.<br><br>Zapewnia dostęp do całej toohello Azure, a nie tylko magazynu. |
| Serwer proxy HTTP |Dozwolone adresy URL kontrolę powitania serwera proxy za pośrednictwem hello magazynu.<br>Pojedynczy punkt Internet tooVMs dostępu.<br>Nie podmiotu tooAzure zmiany adresu IP. |Dodatkowe koszty uruchomioną maszynę Wirtualną z hello oprogramowanie serwera proxy. |

### <a name="whitelist-hello-azure-datacenter-ip-ranges"></a>Zakresy IP centrum danych Azure hello listy dozwolonych adresów IP
toowhitelist hello zakresy IP centrum danych Azure, zobacz hello [witryny sieci Web Azure](http://www.microsoft.com/en-us/download/details.aspx?id=41653) szczegółowe informacje na temat zakresów IP hello i instrukcje.

### <a name="using-an-http-proxy-for-vm-backups"></a>Za pomocą serwera proxy HTTP dla kopii zapasowych maszyn wirtualnych
Podczas tworzenia kopii zapasowej maszyny Wirtualnej, zapasowy numer wewnętrzny hello na powitania maszyna wirtualna wysyła hello migawki zarządzania polecenia tooAzure magazynu przy użyciu interfejsu API protokołu HTTPS. Kierować ruchem zapasowy numer wewnętrzny hello za pośrednictwem serwera proxy hello HTTP, ponieważ jest jedynym składnikiem hello skonfigurowane dla toohello dostępu do publicznej sieci Internet.

> [!NOTE]
> Nie ma żadnych zalecenie hello proxy oprogramowania, które mają być używane. Upewnij się, że możesz wybrać serwer proxy, który jest zgodny z poniższych czynności konfiguracyjne hello.
>
>

Hello przykład obraz poniżej przedstawia kroki konfiguracji trzy hello niezbędne toouse HTTP serwera proxy:

* Trasy wirtualna aplikacji, które powiązane cały ruch HTTP dla hello publicznej sieci Internet za pośrednictwem serwera Proxy maszyny Wirtualnej.
* Maszyna wirtualna serwera proxy zezwala na ruch przychodzący z maszyn wirtualnych w sieci wirtualnej hello.
* Witaj sieciowej grupy zabezpieczeń (NSG) o nazwie NF blokady musi zabezpieczeń reguły zezwalanie Internet ruch wychodzący z maszyny Wirtualnej serwera Proxy.

![Grupy NSG z diagram wdrożenia serwera proxy HTTP](./media/backup-azure-vms-prepare/nsg-with-http-proxy.png)

toouse HTTP serwera proxy toocommunicating toohello publicznej sieci Internet, wykonaj następujące kroki:

#### <a name="step-1-configure-outgoing-network-connections"></a>Krok 1. Konfigurowanie połączeń wychodzących sieci
###### <a name="for-windows-machines"></a>W przypadku komputerów z systemem Windows
Będzie to ustawienia konfiguracji serwera proxy dla lokalnego konta systemowego.

1. Pobierz [PsExec](https://technet.microsoft.com/sysinternals/bb897553)
2. Uruchom następujące polecenia z podwyższonym poziomem uprawnień wiersza

     ```
     psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"
     ```
     Otworzy się okno programu internet explorer.
3. Przejdź tooTools -> Opcje internetowe -> połączenia -> Ustawienia sieci LAN.
4. Sprawdź ustawienia serwera proxy dla konta System. Ustaw Proxy adresu IP i portu.
5. Zamknij program Internet Explorer.

Zostanie utworzenie konfiguracji serwera proxy dla komputera i będą używane dla każdego wychodzącego ruchu HTTP/HTTPS.

Jeśli skonfigurowano serwer proxy dla bieżącego konta użytkownika (nie lokalnego konta systemowego), użyj hello następujący skrypt tooapply ich tooSYSTEMACCOUNT:

```
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name DefaultConnectionSettings -Value $obj.DefaultConnectionSettings
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name SavedLegacySettings -Value $obj.SavedLegacySettings
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name ProxyEnable -Value $obj.ProxyEnable
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name Proxyserver -Value $obj.Proxyserver
```

> [!NOTE]
> Jeśli zauważysz "(407) uwierzytelniania serwera Proxy wymagane" w dzienniku serwera proxy, sprawdź, czy uwierzytelnianie jest poprawnie skonfigurowana.
>
>

###### <a name="for-linux-machines"></a>Dla maszyn z systemem Linux
Dodaj powitania po wierszu toohello ```/etc/environment``` pliku:

```
http_proxy=http://<proxy IP>:<proxy port>
```

Dodaj następujące wiersze toohello hello ```/etc/waagent.conf``` pliku:

```
HttpProxy.Host=<proxy IP>
HttpProxy.Port=<proxy port>
```

#### <a name="step-2-allow-incoming-connections-on-hello-proxy-server"></a>Krok 2. Zezwalaj na połączenia przychodzące na powitania serwera proxy:
1. Na powitania serwera proxy otwórz Zaporę systemu Windows. Witaj Najprostszym sposobem tooaccess hello zapory jest toosearch zapory systemu Windows z zabezpieczeniami zaawansowanymi.

    ![Otwórz hello zapory](./media/backup-azure-vms-prepare/firewall-01.png)
2. W oknie dialogowym zapory systemu Windows hello, kliknij prawym przyciskiem myszy **reguły ruchu przychodzącego** i kliknij przycisk **nową regułę...** .

    ![Utwórz nową regułę](./media/backup-azure-vms-prepare/firewall-02.png)
3. W hello **Kreatora nowej reguły przychodzącej**, wybierz hello **niestandardowy** opcję hello **typ reguły** i kliknij przycisk **dalej**.
4. Na powitania strony tooselect hello **Program**, wybierz **wszystkie programy** i kliknij przycisk **dalej**.
5. Na powitania **protokoły i porty** , wprowadź hello następujące informacje i kliknij przycisk **dalej**:

    ![Utwórz nową regułę](./media/backup-azure-vms-prepare/firewall-03.png)

   * Aby uzyskać *protokół typu* wybierz *TCP*
   * dla *portów lokalnych* wybierz *określonych portów*, w polu hello poniżej Określ hello ```<Proxy Port>``` który został skonfigurowany.
   * Aby uzyskać *port zdalny* wybierz *wszystkie porty*

     Hello pozostałej części hello kreatora kliknij wszystkie hello sposób toohello zakończenia i nadaj nazwę tej reguły.

#### <a name="step-3-add-an-exception-rule-toohello-nsg"></a>Krok 3. Dodaj wyjątek toohello reguły NSG:
W wierszu polecenia programu PowerShell systemu Azure wprowadź hello następujące polecenie:

Witaj następujące polecenie dodaje wyjątek toohello NSG. Ten wyjątek zezwala na ruch TCP z dowolnego portu na 10.0.0.5 tooany adresu internetowego na porcie 80 (HTTP) lub 443 (HTTPS). Jeśli potrzebujesz określonego portu w hello publicznej sieci Internet, można tooadd się upewnić, że port toohello ```-DestinationPortRange``` również.

```
Get-AzureNetworkSecurityGroup -Name "NSG-lockdown" |
Set-AzureNetworkSecurityRule -Name "allow-proxy " -Action Allow -Protocol TCP -Type Outbound -Priority 200 -SourceAddressPrefix "10.0.0.5/32" -SourcePortRange "*" -DestinationAddressPrefix Internet -DestinationPortRange "80-443"
```


*Kroki przy użyciu określonej nazwy i wartości w tym przykładzie. Użyj hello nazwy i wartości dla wdrożenia, wprowadzając, lub wycinanie i wklejanie informacji w kodzie.*

Teraz wiesz, że masz połączenie z siecią, wszystko jest gotowe tooback się z maszyną Wirtualną. Zobacz [kopię zapasową wdrożonych przez Menedżera zasobów maszyn wirtualnych](backup-azure-arm-vms.md).

## <a name="questions"></a>Pytania?
Jeśli masz pytania lub w przypadku dowolnej funkcji, które chcesz toosee uwzględnione, [Prześlij nam opinię](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Następne kroki
Teraz, kiedy przygotowania środowiska do tworzenia kopii zapasowej maszyny Wirtualnej, następnym krokiem logicznej jest toocreate kopii zapasowej. Witaj planowania artykuł zawiera bardziej szczegółowe informacje o tworzeniu kopii zapasowych maszyn wirtualnych.

* [Tworzenie kopii zapasowych maszyn wirtualnych](backup-azure-vms.md)
* [Zaplanuj infrastrukturę kopii zapasowej maszyny Wirtualnej](backup-azure-vms-introduction.md)
* [Zarządzanie kopii zapasowych maszyn wirtualnych](backup-azure-manage-vms.md)
