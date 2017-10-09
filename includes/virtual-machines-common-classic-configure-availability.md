


Zbiór dostępności pomaga zachować maszyn wirtualnych dostępnych w trakcie przestoju, takich jak podczas konserwacji. Wprowadzenie do dwóch lub więcej podobnie skonfigurowane maszyny wirtualne w zestawie dostępności tworzy hello nadmiarowość potrzebne toomaintain dostępności hello aplikacji lub usług, które są wykonywane na komputerze wirtualnym. Aby uzyskać szczegółowe informacje dotyczące sposobu działania, zobacz [Zarządzanie hello dostępność maszyn wirtualnych][Manage hello availability of virtual machines].

Jest najlepszym toouse praktyki zarówno zestawów dostępności i równoważenia obciążenia toohelp punkty końcowe upewnij się, że aplikacja jest zawsze dostępny i działa wydajnie. Aby uzyskać więcej informacji o punktach końcowych z równoważeniem obciążenia, zobacz [równoważenia obciążenia dla usług infrastruktury platformy Azure][Load balancing for Azure infrastructure services].

Klasyczne maszyny wirtualne można dodać do zestawu przy użyciu jednej z dwóch opcji dostępności:

* [Opcja 1: Utwórz maszynę wirtualną i zestawu dostępności na powitania sam czas][Option 1: Create a virtual machine and an availability set at hello same time]. Następnie należy dodać nowy toohello maszyn wirtualnych po utworzeniu tych maszyn wirtualnych.
* [Opcja 2: Dodawanie istniejącego zestawu dostępności maszyny wirtualnej tooan][Option 2: Add an existing virtual machine tooan availability set].

> [!NOTE]
> W klasycznym modelu hello maszyn wirtualnych, które mają być tooput w hello sam zestaw dostępności muszą należeć toohello sama usługa w chmurze.
> 
> 

## <a id="createset"></a>— Opcja 1: Utwórz maszynę wirtualną i zestawu dostępności na powitania sam czas
Możesz użyć albo hello portalu Azure lub poleceń programu Azure PowerShell toodo to.

Witaj toouse portalu Azure:

1. Jeśli jeszcze tego nie zrobiono, zaloguj się w toohello [portalu Azure](https://portal.azure.com).
2. W menu Centrum powitania kliknij **+ nowy**, a następnie kliknij przycisk **maszyny wirtualnej**.
   
    ![Tekst alternatywny obrazu](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. Wybierz obraz maszyny wirtualnej z witryny Marketplace hello mają toouse. Możesz wybrać toocreate maszyny wirtualnej systemu Linux lub Windows.
4. Dla hello wybranych maszyny wirtualnej, sprawdź modelu wdrażania hello ustawiono zbyt**klasycznego** , a następnie kliknij przycisk **Utwórz**
   
    ![Tekst alternatywny obrazu](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. Wprowadź nazwę maszyny wirtualnej, nazwę użytkownika i hasło (dla komputerów z systemem Windows) lub klucz publiczny SSH (w przypadku maszyn z systemem Linux). 
6. Wybierz rozmiar maszyny Wirtualnej hello, a następnie kliknij przycisk **wybierz** toocontinue.
7. Wybierz **konfiguracji opcjonalnej > zestawu dostępności**i wybierz zestaw dostępności hello ma maszynę wirtualną hello tooadd.
   
    ![Tekst alternatywny obrazu](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. Przejrzyj ustawienia konfiguracji. Gdy wszystko będzie gotowe, kliknij przycisk **Utwórz**.
9. Podczas gdy platforma Azure tworzy maszynę wirtualną, możesz śledzić postępy hello w obszarze **maszyn wirtualnych** w menu centralnym hello.

toouse programu Azure PowerShell poleceń toocreate maszyny wirtualnej platformy Azure i dodać zestaw dostępności nowych lub istniejących tooa, zobacz [toocreate Użyj programu PowerShell Azure i wstępnie skonfigurować maszyn wirtualnych z systemem Windows](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a id="addmachine"></a>Opcja 2: Dodawanie istniejącego zestawu dostępności tooan maszyny wirtualnej
Hello portalu Azure należy dodać istniejący tooan klasycznych maszyn wirtualnych istniejącego zestawu dostępności lub Utwórz nową dla nich. (Należy pamiętać, że hello maszyn wirtualnych w hello na tym samym zestawie dostępności muszą należeć toohello sama usługa w chmurze.) Witaj kroki są prawie hello tego samego. Przy użyciu programu Azure PowerShell można dodać hello maszyny wirtualnej tooan istniejącego zestawu dostępności.

1. Jeśli nie zostało to jeszcze zrobione, zaloguj się w toohello [portalu Azure](https://portal.azure.com).
2. W menu Centrum powitania kliknij **maszyn wirtualnych (klasyczne)**.
   
    ![Tekst alternatywny obrazu](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. Z listy hello maszyny wirtualne wybierz nazwę hello hello maszyny wirtualnej, które mają tooadd toohello zestawu.
4. Wybierz **zestawu dostępności** z maszyny wirtualnej hello **ustawienia**.
   
    ![Tekst alternatywny obrazu](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. Wybierz zestaw dostępności hello, które mają tooadd hello maszyny wirtualnej w celu. Maszyna wirtualna Hello musi należeć toohello sama usługa w chmurze jako hello zestawu dostępności.
   
    ![Tekst alternatywny obrazu](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. Kliknij pozycję **Zapisz**.

toouse polecenia programu Azure PowerShell, otwórz sesję programu PowerShell Azure poziomie administratora i uruchom następujące polecenie hello. Witaj symboli zastępczych (takich jak &lt;VmCloudServiceName&gt;), Zastąp wszystkie elementy w cudzysłowy hello, w tym hello < i > znaków, z hello rozwiązać nazwy.

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> Witaj, maszyna wirtualna może dysponować toofinish toobe ponownego uruchomienia, dodając toohello zestawu dostępności.
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at hello same time]: #createset
[Option 2: Add an existing virtual machine tooan availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage hello availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

