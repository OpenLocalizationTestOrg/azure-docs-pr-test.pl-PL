


W tym artykule opisano często zadawane pytania, które Poproś użytkowników o utworzone za pomocą hello klasycznego modelu wdrażania maszyn wirtualnych platformy Azure.

## <a name="can-i-migrate-my-vm-created-in-hello-classic-deployment-model-toohello-new-resource-manager-model"></a>Czy mogę przenieść mój maszyny Wirtualnej utworzonej w hello wdrażania klasycznego modelu toohello nowego modelu Resource Manager
Tak. Aby uzyskać instrukcje dotyczące toomigrate, zobacz:

* [Migracja z klasycznego tooAzure Resource Manager przy użyciu programu Azure PowerShell](../articles/virtual-machines/windows/migration-classic-resource-manager-ps.md).
* [Migracja z klasycznego tooAzure Resource Manager przy użyciu interfejsu wiersza polecenia Azure](../articles/virtual-machines/virtual-machines-linux-cli-migration-classic-resource-manager.md).

## <a name="what-can-i-run-on-an-azure-vm"></a>Co mogę uruchomić na maszynie wirtualnej platformy Azure?
Wszyscy subskrybenci mogą uruchomić oprogramowanie serwerowe na maszynie wirtualnej platformy Azure. Możesz uruchomić nowe wersje systemu Windows Server oraz różne dystrybucje systemu Linux. Aby uzyskać szczegółowe informacje na temat pomocy technicznej, zobacz:

• Dla maszyn wirtualnych z systemem Windows — [pomoc techniczna dla oprogramowania serwerowego firmy Microsoft dla usługi Azure Virtual Machines](http://go.microsoft.com/fwlink/p/?LinkId=393550)

• Dla maszyn wirtualnych z systemem Linux — [dystrybucje systemu Linux zalecane dla platformy Azure](http://go.microsoft.com/fwlink/p/?LinkId=393551)

Dla obrazów klienta systemu Windows określonych wersji systemu Windows 7 i Windows 8.1 są dostępne tooMSDN Azure korzyści subskrybentów i subskrybentów MSDN: Programowanie i testowanie płatność za rzeczywiste użycie, dla zadań tworzenia i testowania. Aby uzyskać szczegółowe informacje, łącznie z instrukcjami i ograniczeniami, zobacz [Windows Client images for MSDN subscribers](https://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/) (Obrazy klienta systemu Windows dla subskrybentów MSDN).

## <a name="why-are-affinity-groups-being-deprecated"></a>Dlaczego grupy koligacji stały się przestarzałe?
Grupy koligacji to starsza koncepcja geograficznego grupowania wdrożeń usługi w chmurze klienta i kont magazynu w ramach platformy Azure. Zostały one pierwotnie udostępniane tooimprove wydajność sieci maszyn wirtualnych do maszyny Wirtualnej w hello wczesne projektów sieci platformy Azure. Początkowa wersja hello sieci wirtualnych (sieci wirtualne), które były ograniczone tooa niewielki zbiór sprzętu w regionie one również obsługiwane.

Bieżąca sieć Hello w obrębie regionu Azure zaprojektowano tak, aby grup koligacji nie są już wymagane. Sieci wirtualne znajdują się również w zakresie regionalnym, więc grupy koligacji nie są już wymagane, gdy korzystasz z sieci wirtualnej. Ze względu na ulepszenia toothese nie zaleca się klienci powinni używać grupy koligacji, ponieważ może być ograniczenie w niektórych scenariuszach. Korzystanie z grup koligacji niepotrzebnie skojarzyć ograniczające wybór hello rozmiarów maszyn wirtualnych, które są dostępne tooyou sprzętu toospecific maszyn wirtualnych. Może również spowodować błędy związane z toocapacity podczas próby tooadd nowych maszyn wirtualnych, jeśli sprzętu hello skojarzone z grupą koligacji hello jest bliski pojemności.

Funkcje grupy koligacji są już przestarzałe w modelu wdrażania usługi Azure Resource Manager hello i hello portalu Azure. Hello klasycznego portalu Azure możemy Cię wycofano obsługę tworzenia grupy koligacji i tworzenia zasobów magazynu, które są tooan przypiętych grupy koligacji. Nie trzeba toomodify istniejącej usługi w chmurze korzystających z grupy koligacji. Jednak nie należy używać grup koligacji dla nowych usług w chmurze, chyba że specjalista pomocy technicznej platformy Azure je zaleci.

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>Ile pamięci masowej mogę użyć w maszynie wirtualnej?
Każdy dysk danych można się too1 TB. Witaj liczba dysków z danymi, których można używać zależy od rozmiaru hello hello maszyny wirtualnej. Aby uzyskać szczegółowe informacje, zobacz [Sizes for virtual machines](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Rozmiary maszyn wirtualnych).

Konto usługi Azure storage udostępnia magazyn hello dysku systemu operacyjnego i dysków z danymi. Każdy dysk jest plikiem VHD przechowywanym jako stronicowy obiekt blob. Aby uzyskać szczegółowe informacje o cenach, zobacz [Szczegóły cennika magazynu](http://go.microsoft.com/fwlink/p/?LinkId=396819).

## <a name="which-virtual-hard-disk-types-can-i-use"></a>Jakich typów wirtualnego dysku twardego mogę używać?
Platforma Azure obsługuje tylko stałe wirtualne dyski twarde w formacie VHD. Jeśli plik VHDX, które mają toouse na platformie Azure, trzeba toofirst przekonwertować go za pomocą Menedżera funkcji Hyper-V lub hello [convert-VHD](http://go.microsoft.com/fwlink/p/?LinkId=393656) polecenia cmdlet. Po wykonaniu tej czynności, za pomocą [Add-AzureVHD](https://msdn.microsoft.com/library/azure/dn495173.aspx) hello tooupload polecenia cmdlet (w trybie zarządzania usługami) konta magazynu tooa wirtualnego dysku twardego na platformie Azure, dzięki czemu można używać z maszynami wirtualnymi.

* Instrukcje Linux, zobacz [tworząc i przekazując wirtualny dysk twardy zawierający System operacyjny Linux hello](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).
* Instrukcje systemu Windows, temacie [tworzenie i przekazywanie wirtualnego dysku twardego z systemem Windows Server tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="are-these-virtual-machines-hello-same-as-hyper-v-virtual-machines"></a>Czy na pewno hello tych maszyn wirtualnych jak w przypadku maszyn wirtualnych funkcji Hyper-V?
Na wiele sposobów, które są podobne zbyt maszyn wirtualnych funkcji Hyper-V "Generacja 1", ale jest dokładnie hello tego samego. Oba typy Podaj sprzętu zwirtualizowanego, a wirtualne dyski twarde hello formatu wirtualnego dysku twardego są zgodne. Oznacza to, że możesz je przenosić między funkcją Hyper-V a platformą Azure. Trzema podstawowymi różnicami, które czasami zaskakują użytkowników funkcji Hyper-V, są:

* Azure nie zapewnia maszyny wirtualnej tooa dostępu do konsoli. Nie jest brak tooaccess sposób maszyny Wirtualnej, dopóki nie została ona wysłana rozruch.
* Maszyny wirtualne platformy Azure w większości [rozmiarów](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) mają tylko 1 wirtualną kartę sieciową, co oznacza, że mogą mieć również tylko 1 zewnętrzny adres IP. (hello A8 i A9 rozmiary użyć drugiej karty sieciowej dla aplikacji komunikacji między wystąpieniami w scenariuszach ograniczona).
* Maszyny wirtualne platformy Azure nie obsługują funkcji maszyn wirtualnych 2. generacji funkcji Hyper-V. Aby uzyskać więcej informacji o tych funkcjach, zobacz [Virtual Machine Specifications for Hyper-V](http://technet.microsoft.com/library/dn592184.aspx) (Specyfikacje maszyny wirtualnej dla funkcji Hyper-V) i [Generation 2 Virtual Machine Overview](https://technet.microsoft.com/library/dn282285.aspx) (Maszyna wirtualna 2. generacji — omówienie).

## <a name="can-these-virtual-machines-use-my-existing-on-premises-networking-infrastructure"></a>Czy te maszyny wirtualne mogą korzystać z mojej istniejącej lokalnej infrastruktury sieci?
Dla maszyn wirtualnych utworzonych w hello klasycznego modelu wdrażania można użyć sieci wirtualnej Azure tooextend istniejącej infrastruktury. podejście Hello jest podobne do konfigurowania biura oddziału. Można udostępnić i zarządzanie wirtualnych sieci prywatnych (VPN) na platformie Azure oraz jak bezpiecznie łączyć je z lokalnym tooon infrastruktury IT. Aby uzyskać szczegółowe informacje, zobacz [Omówienie usługi Virtual Network](../articles/virtual-network/virtual-networks-overview.md).

Będziesz potrzebować toospecify hello sieci, która ma hello tworzenia maszyny wirtualnej hello toowhen toobelong maszyny wirtualnej. Nie można połączyć się z istniejącą siecią wirtualną tooa maszyny wirtualnej. Jednak można obejść ten problem przez odłączenie hello wirtualnego dysku twardego (VHD) z istniejącej maszyny wirtualnej hello, a następnie używać toocreate nowej maszyny wirtualnej z hello konfiguracji sieci, który ma.

## <a name="how-can-i-access--my-virtual-machine"></a>Jak mogę uzyskać dostęp do mojej maszyny wirtualnej?
Należy tooestablish toolog połączenia zdalnego, na maszynie wirtualnej toohello przy użyciu usługi Podłączanie pulpitu zdalnego dla maszyny Wirtualnej systemu Windows lub protokołu Secure Shell (SSH) dla maszyny Wirtualnej systemu Linux. Aby uzyskać instrukcje, zobacz:

* [Jak tooLog na tooa maszyny wirtualnej z systemu Windows Server](../articles/virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Obsługuje maksymalnie 2 równoczesnych połączeń, chyba że hello serwer jest skonfigurowany jako host sesji usług pulpitu zdalnego.  
* [Jak tooLog na tooa maszyny wirtualnej systemem Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Domyślnie protokół SSH umożliwia maksymalnie 10 równoczesnych połączeń. Można zwiększyć tę liczbę, edytując hello pliku konfiguracji.

Jeśli masz problemy z pulpitu zdalnego lub SSH, zainstalować i używać hello [VMAccess](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) rozszerzenia toohelp poprawka hello problem.

Dla maszyn wirtualnych z systemem Windows dostępne są następujące opcje dodatkowe:

* W hello klasycznego portalu Azure, Znajdź hello maszyny Wirtualnej, a następnie kliknij przycisk **Resetuj dostęp zdalny** z hello paska poleceń.
* Przegląd [tooa połączeń pulpitu zdalnego Rozwiązywanie problemów z maszyny wirtualnej z systemem Windows Azure](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Użyj funkcji komunikacji zdalnej programu Windows PowerShell tooconnect toohello maszyny Wirtualnej lub Utwórz dodatkowe punkty końcowe dla innych toohello tooconnect zasobów maszyny Wirtualnej. Aby uzyskać więcej informacji, zobacz [jak tooSet się punkty końcowe tooa maszyny wirtualnej](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Jeśli znasz funkcji Hyper-V, zapoznają się dla narzędzia tooVMConnect podobne. Azure nie oferuje podobne narzędzie, ponieważ maszyna wirtualna tooa dostępu do konsoli nie jest obsługiwana.

## <a name="can-i-use-hello-temporary-disk-hello-d-drive-for-windows-or-devsdb1-for-linux-toostore-data"></a>Można użyć hello dysku tymczasowym (hello D: dysku dla systemu Windows lub /dev/sdb1 dla systemu Linux) toostore danych?
Nie można używać hello dysku tymczasowym (hello dysku D: domyślnie dla systemu Windows oraz /dev/sdb1 dla systemu Linux) toostore danych. Są to wyłącznie magazyny tymczasowe, czyli istnieje ryzyko utraty danych, których nie będzie można odzyskać. Taka sytuacja może wystąpić podczas przenoszenia maszyny wirtualnej hello tooa innego hosta. Zmiana rozmiaru maszyny wirtualnej, aktualizowania hosta hello lub awaria sprzętu na hoście hello są niektóre przyczyny hello może przenieść maszynę wirtualną.

## <a name="how-can-i-change-hello-drive-letter-of-hello-temporary-disk"></a>Jak zmienić hello litera dysku tymczasowego hello?
Na maszynie wirtualnej systemu Windows można zmienić literę dysku hello przez przenoszenie pliku strony hello i ponowne przypisywanie litery dysku, ale należy toomake się, że hello kroki w określonej kolejności. Aby uzyskać instrukcje, zobacz [zmiany hello literę dysku tymczasowym systemu Windows hello](../articles/virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="how-can-i-upgrade-hello-guest-operating-system"></a>Jak uaktualnić system operacyjny gościa hello?
Witaj uaktualnienia termin zazwyczaj oznacza tooa przenoszenie więcej aktualną wersją systemu operacyjnego, pozostając w hello tego samego sprzętu. Dla maszyn wirtualnych platformy Azure, hello procesu przenoszenia tooa nowszej wersji jest różny dla systemów Linux i Windows:

* Dla maszyn wirtualnych systemu Linux Użyj narzędzia do zarządzania pakietów hello i procedury odpowiednie dla dystrybucji hello.
* Dla maszyny wirtualnej systemu Windows należy toomigrate powitania serwera przy użyciu przypominać hello narzędzi migracji systemu Windows Server. Nie próbuj system operacyjny gościa hello tooupgrade, gdy znajduje się on na platformie Azure. Nie są obsługiwane z powodu hello ryzyko utraty maszyny wirtualnej toohello dostępu. Podczas uaktualniania hello wystąpią problemy, może spowodować utratę hello możliwości toostart pulpitu zdalnego sesji i nie będą mogli tootroubleshoot hello problemów.

Aby uzyskać ogólne informacje o narzędziach hello i procesów dotyczących migracji systemu Windows Server, zobacz [tooWindows Migrowanie ról i funkcji serwera](http://go.microsoft.com/fwlink/p/?LinkId=396940).

## <a name="whats-hello-default-user-name-and-password-on-hello-virtual-machine"></a>Co to jest hello domyślna nazwa użytkownika i hasło na maszynie wirtualnej hello?
obrazy Hello dostarczany przez platformę Azure nie ma nazwy wstępnie skonfigurowane użytkownika i hasła. Podczas tworzenia maszyny wirtualnej przy użyciu jednej z tych obrazów, będziesz potrzebować tooprovide nazwę użytkownika i hasło, którego użyjesz toolog toohello maszyny wirtualnej.

Jeśli pamiętasz hello nazwa użytkownika lub hasło, a po zainstalowaniu hello agenta maszyny Wirtualnej, można zainstalować i używać hello [VMAccess](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) rozszerzenia toofix hello problem.

Dodatkowe szczegóły:

* Hello Linux obrazów Jeśli używasz hello klasycznego portalu Azure, "azureuser" jest podawana jako domyślna nazwa użytkownika, ale można to zmienić za pomocą "Z galerii" zamiast "Szybkie tworzenie" jako maszyna wirtualna hello toocreate sposób hello. Za pomocą "Z galerii" umożliwia także zdecydować, czy toouse hasła, kluczem SSH lub obu toolog w. Witaj konto użytkownika jest poziomem uprawnień użytkownika, który ma dostępu "sudo" toorun uprzywilejowany poleceń. konta "root" Hello jest wyłączona.
* Dla obrazów systemu Windows musisz tooprovide nazwy użytkownika i hasła podczas tworzenia hello maszyny Wirtualnej. Witaj, konto zostanie dodane toohello grupy Administratorzy.

## <a name="can-azure-run-anti-virus-on-my-virtual-machines"></a>Czy platforma Azure może uruchamiać oprogramowanie antywirusowe na moich maszynach wirtualnych?
Platforma Azure oferuje kilka możliwości rozwiązania oprogramowania antywirusowego, ale jest tooyou toomanage go. Na przykład oddzielnej subskrypcji mogą być wymagane do ochrony przed złośliwym oprogramowaniem i potrzebne są toodecide toorun skanowania i zainstalować aktualizacje. Obsługę antywirusową możesz dodać za pomocą rozszerzenia maszyny wirtualnej dla usługi firmy Microsoft chroniącej przed złośliwym kodem, programu Symantec Endpoint Protection lub agenta TrendMicro Deep Security Agent podczas tworzenia maszyny wirtualnej systemu Windows lub w późniejszym czasie. Witaj firmy Symantec i rozszerzenia TrendMicro pozwala korzystać z bezpłatnej subskrypcji próbnej ograniczonej czasowo lub istniejącej subskrypcji enterprise. Usługa firmy Microsoft chroniąca przed złośliwym kodem jest bezpłatna. Aby uzyskać szczegółowe informacje, zobacz:

* [Jak tooinstall i skonfigurować Symantec Endpoint Protection na maszynie Wirtualnej platformy Azure](http://go.microsoft.com/fwlink/p/?LinkId=404207)
* [Jak tooinstall i skonfigurować Trend Micro głębokie zabezpieczeń jako usługa na maszynie Wirtualnej platformy Azure](http://go.microsoft.com/fwlink/p/?LinkId=404206)
* [Wdrażanie rozwiązań do ochrony przed złośliwym kodem na maszynach wirtualnych platformy Azure](https://azure.microsoft.com/blog/2014/05/13/deploying-antimalware-solutions-on-azure-virtual-machines/)

## <a name="what-are-my-options-for-backup-and-recovery"></a>Jakie są możliwości tworzenia kopii zapasowych i odzyskiwania?
Kopia zapasowa Azure jest dostępna w pewnych regionach jako wersja zapoznawcza. Aby uzyskać szczegółowe informacje, zobacz [Tworzenie kopii zapasowych maszyn wirtualnych platformy Azure](../articles/backup/backup-azure-vms.md). Inne rozwiązania są dostępne u certyfikowanych partnerów. toofind, co jest obecnie dostępna, wyszukaj hello Azure Marketplace.

Dodatkowa opcja jest tworzenie migawek hello toouse magazynu obiektów blob. toodo, będziesz potrzebować tooshut dół hello maszyny Wirtualnej przed żadnej operacji, która zależy od migawki obiektu blob. Zapisuje zapisów oczekujących danych i umieszcza hello systemu plików w spójnym stanie.

## <a name="how-does-azure-charge-for-my-vm"></a>Jak platforma Azure nalicza opłaty za moją maszynę wirtualną?
Azure opłat cenę godzinową określoną na podstawie rozmiaru i systemu operacyjnego hello maszyny Wirtualnej. Za kolejne rozpoczęte godziny Azure opłaty wyłącznie za wykorzystane minuty hello. Jeśli tworzysz hello maszyny Wirtualnej z obrazu maszyny Wirtualnej zawierający niektórych wstępnie zainstalowanego oprogramowania, dodatkowe co godzinę oprogramowania może opłaty. Azure opłaty oddzielnie dla magazynu dla systemu operacyjnego i dysków z danymi hello maszyny Wirtualnej. Tymczasowy magazyn dysków jest bezpłatny.

Naliczane są opłaty hello stanu maszyny Wirtualnej jest uruchomiona lub zatrzymana, ale nie są naliczane po zatrzymaniu hello stanu maszyny Wirtualnej (cofnąć alokacji). tooput maszyny Wirtualnej w ramach hello zatrzymana stanu (cofnąć przydziału), wykonaj jedną z następujących hello:

* Wyłączanie lub usuwanie hello maszyny Wirtualnej z hello klasycznego portalu Azure.
* Należy użyć polecenia Stop-AzureVM hello, dostępne w hello modułu Azure PowerShell.
* Za pomocą operacji zamknięcia roli hello w hello interfejs API REST zarządzania usługami i określ StoppedDeallocated hello PostShutdownAction elementu.

Aby uzyskać więcej informacji, zobacz [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/) (Cennik usługi Virtual Machines).

## <a name="will-azure-reboot-my-vm-for-maintenance"></a>Czy platforma Azure ponownie uruchomi moją maszynę wirtualną w celu konserwacji?
Azure czasami powoduje ponowne uruchomienie maszyny Wirtualnej jako część aktualizacji w zwykłym, planowanej konserwacji w hello centrach danych platformy Azure.

Nieplanowane zdarzenia konserwacji mogą wystąpić, gdy platforma Azure wykryje poważny problem sprzętowy, który ma wpływ na Twoją maszynę wirtualną. Nieplanowane zdarzeń Azure automatycznie migruje hello hosta dobrej kondycji tooa maszyny Wirtualnej i ponownie uruchamia hello maszyny Wirtualnej.

Dla dowolnego autonomicznej maszyny Wirtualnej (to znaczy hello maszyny Wirtualnej nie jest częścią zestawu dostępności), Azure powiadamia administratora usługi hello subskrypcji za pośrednictwem poczty e-mail co najmniej jeden tydzień przed zaplanowanej konserwacji ponieważ hello maszyn wirtualnych mogła zostać ponownie uruchomiona podczas aktualizacji hello. Aplikacje działające na maszynach wirtualnych hello można Przestój.

Można też użyć hello klasycznego portalu Azure lub programu Azure PowerShell tooview hello ponowny rozruch dzienniki podczas ponownego uruchomienia hello wystąpienia powodu tooplanned konserwacji. Aby uzyskać szczegółowe informacje, zobacz [Wyświetlanie dzienników ponownego uruchamiania maszyny wirtualnej](https://azure.microsoft.com/blog/2015/04/01/viewing-vm-reboot-logs/).

nadmiarowość tooprovide, umieść dwa lub więcej podobnie skonfigurowana maszyn wirtualnych w hello tego samego zestawu dostępności. Pomaga to w zapewnieniu, że co najmniej jedna maszyna wirtualna jest dostępna podczas planowanej lub nieplanowanej konserwacji. Platforma Azure gwarantuje pewne poziomy dostępności maszyny wirtualnej dla tej konfiguracji. Aby uzyskać więcej informacji, zobacz [Zarządzanie hello dostępność maszyn wirtualnych](../articles/virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="additional-resources"></a>Dodatkowe zasoby
[Informacje o maszynach wirtualnych platformy Azure](../articles/virtual-machines/virtual-machines-linux-about.md)

[Tworzenie i zarządzanie maszyn wirtualnych systemu Linux z hello wiersza polecenia platformy Azure](../articles/virtual-machines/linux/tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Tworzenie maszyn wirtualnych z systemem Windows i zarządzanie nimi za pomocą programu Azure PowerShell](../articles/virtual-machines/windows/tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

