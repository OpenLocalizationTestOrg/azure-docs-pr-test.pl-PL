

Rozszerzenia maszyn wirtualnych umożliwiają:

* Modyfikowanie funkcji zabezpieczeń i tożsamości, takich jak resetowanie wartości konta i korzystanie z oprogramowania chroniącego przed złośliwym kodem
* Uruchamianie, zatrzymywanie lub konfigurowanie monitorowania i diagnostyki
* Resetowanie lub instalowanie funkcji łączności, takich jak protokoły RDP i SSH
* Diagnozowanie i monitorowanie maszyn wirtualnych oraz zarządzanie nimi

Istnieje również wiele innych funkcji. Nowe funkcje rozszerzenia maszyny wirtualnej są regularnie wydawane. W tym artykule opisano hello Azure VM agentów dla systemu Windows i Linux oraz sposobu ich obsługi funkcji rozszerzenia maszyny Wirtualnej. Aby uzyskać listę rozszerzeń maszyn wirtualnych według kategorii funkcji, zobacz [Azure VM Extensions and Features](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Rozszerzenia i funkcje maszyn wirtualnych platformy Azure).

## <a name="azure-vm-agents-for-windows-and-linux"></a>Agenci maszyn wirtualnych platformy Azure dla systemu Windows i Linux
Hello Azure maszyny wirtualne Agent (Agent maszyny Wirtualnej) jest procesem zabezpieczonych, lekki, który instaluje, konfiguruje i usuwa rozszerzeń maszyny Wirtualnej na wystąpień maszyn wirtualnych Azure. Hello agenta maszyny Wirtualnej działa jako usługa bezpiecznego kontroli lokalne powitania dla maszyny Wirtualnej Azure. rozszerzenia Hello, które hello obciążenia agenta zapewniają tooincrease określonych funkcji wydajność pracy przy użyciu wystąpienia hello.

Istnieją dwaj agenci maszyn wirtualnych platformy Azure — jeden dla maszyn wirtualnych z systemem Windows i jeden dla maszyn wirtualnych z systemem Linux.

Jeśli chcesz toouse wystąpienie maszyny wirtualnej, jeden lub więcej rozszerzeń maszyny Wirtualnej, hello wystąpienia muszą mieć zainstalowanego agenta maszyny Wirtualnej. Obraz maszyny wirtualnej, utworzony przy użyciu hello portalu Azure i obrazu z hello **Marketplace** automatycznie instaluje agenta maszyny Wirtualnej w procesie tworzenia hello. Jeśli wystąpienie maszyny wirtualnej nie ma agenta maszyny Wirtualnej, należy zainstalować hello agenta maszyny Wirtualnej po utworzeniu hello wystąpienie maszyny wirtualnej. Można także zainstalować agenta hello w niestandardowego obrazu maszyny Wirtualnej, który można następnie przekazać.

> [!IMPORTANT]
> Agenci maszyn wirtualnych to bardzo lekkie usługi umożliwiające bezpieczne administrowanie wystąpieniami maszyn wirtualnych. Może to być przypadki, w których nie chcesz hello agenta maszyny Wirtualnej. Jeśli tak, można się, że maszyny wirtualne toocreate, które nie mają hello agenta maszyny Wirtualnej, zainstalować za pomocą hello wiersza polecenia platformy Azure lub programu PowerShell. Mimo że hello agenta maszyny Wirtualnej można usunąć fizycznie, zachowanie hello rozszerzeń maszyny Wirtualnej w wystąpieniu hello jest niezdefiniowana. W związku z tym usunięcie zainstalowanego agenta maszyny wirtualnej nie jest obsługiwane.
>

Witaj agenta maszyny Wirtualnej jest włączona w hello następujące sytuacje:

* Podczas tworzenia wystąpienia maszyny wirtualnej za pomocą hello portalu Azure i wybierając obrazu z hello **Marketplace**,
* Podczas tworzenia wystąpienia maszyny wirtualnej za pomocą hello [AzureVM nowy](https://msdn.microsoft.com/library/azure/dn495254.aspx) lub hello [AzureQuickVM nowy](https://msdn.microsoft.com/library/azure/dn495183.aspx) polecenia cmdlet. Można utworzyć Maszynę wirtualną bez agenta maszyny Wirtualnej przez dodanie hello **— DisableGuestAgent** toohello parametru [AzureProvisioningConfig Dodaj](https://msdn.microsoft.com/library/azure/dn495299.aspx) polecenia cmdlet

* Kiedy należy ręcznie pobranie i zainstalowanie hello agenta maszyny Wirtualnej na istniejące wystąpienie maszyny Wirtualnej i ustaw hello **ProvisionGuestAgent** wartość zbyt**true**. Tej metody można użyć w przypadku agentów systemu Windows i Linux za pomocą polecenia programu PowerShell lub wywołania REST. (Jeśli nie ustawisz hello **ProvisionGuestAgent** wartość po ręcznej instalacji agenta maszyny Wirtualnej, dodanie hello hello agenta maszyny Wirtualnej nie jest poprawnie wykrywane hello.) hello po kodu przykładzie pokazano sposób toodo to przy użyciu programu PowerShell, gdzie hello `$svc` i `$name` argumenty zostały już ustalone:

      $vm = Get-AzureVM –ServiceName $svc –Name $name
      $vm.VM.ProvisionGuestAgent = $TRUE
      Update-AzureVM –Name $name –VM $vm.VM –ServiceName $svc

* Po utworzeniu obrazu maszyny wirtualnej zawierającego zainstalowanego agenta maszyny wirtualnej. Gdy obraz powitania z hello agenta maszyny Wirtualnej istnieje, możesz przekazać tooAzure tego obrazu. Dla maszyny Wirtualnej systemu Windows, Pobierz hello [pliku msi agenta maszyny Wirtualnej systemu Windows](http://go.microsoft.com/fwlink/?LinkID=394789) i zainstaluj hello agenta maszyny Wirtualnej. Dla maszyny Wirtualnej systemu Linux, zainstaluj hello agenta maszyny Wirtualnej z repozytorium GitHub hello znajdujący się w <https://github.com/Azure/WALinuxAgent>. Aby uzyskać więcej informacji dotyczących sposobu tooinstall hello agenta maszyny Wirtualnej w systemie Linux, zobacz hello [Podręcznik użytkownika agenta maszyny Wirtualnej systemu Linux Azure](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

> [!NOTE]
> W PaaS, hello agenta maszyny Wirtualnej jest nazywany **WindowsAzureGuestAgent**i jest zawsze dostępna w sieci Web i maszyn wirtualnych roli procesu roboczego. (Aby uzyskać więcej informacji, zobacz [Azure roli architektura](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx).) hello agenta maszyny Wirtualnej dla maszyn wirtualnych roli można teraz dodawać usługi w chmurze toohello rozszerzenia maszyn wirtualnych hello tak samo, jak w przypadku trwałe maszyny wirtualne. Różnica największych Hello rozszerzeń maszyny Wirtualnej w roli maszyn wirtualnych i trwałe maszyny wirtualne jest po dodaniu hello rozszerzeń maszyny Wirtualnej. Za pomocą roli maszyn wirtualnych rozszerzenia są dodawane pierwszego toohello usługi w chmurze, następnie toohello wdrożenia w ramach danej usługi w chmurze.
>
> Użyj [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) toolist polecenia cmdlet wszystkie rozszerzenia maszyny Wirtualnej dostępną rolę.
>
>

## <a name="find-add-update-and-remove-vm-extensions"></a>Znajdowanie, dodawanie, aktualizowanie i usuwanie rozszerzeń maszyn wirtualnych
Aby uzyskać szczegółowe informacje na temat tych zadań, zobacz [Add, Find, Update, and Remove Azure VM Extensions](../articles/virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (Dodawanie, znajdowanie, aktualizowanie i usuwanie rozszerzeń maszyn wirtualnych platformy Azure).
