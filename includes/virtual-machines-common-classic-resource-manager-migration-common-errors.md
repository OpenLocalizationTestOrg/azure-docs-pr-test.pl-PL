# <a name="common-errors-during-classic-tooazure-resource-manager-migration"></a>Typowe błędy podczas tooAzure Classic migracji Menedżera zasobów
Ten artykuł katalogi hello najbardziej typowe błędy i środki zaradcze podczas migracji hello zasobów IaaS z wdrożenia usługi Azure klasycznego modelu toohello usługi Azure Resource Manager stosu.

## <a name="list-of-errors"></a>Lista błędów
| Ciąg błędu | Środki zaradcze |
| --- | --- |
| Wewnętrzny błąd serwera |W niektórych przypadkach jest to błąd przejściowy, który znika przy ponownej próbie. Jeśli nadal toopersist, [skontaktuj się z pomocą techniczną platformy Azure](../articles/azure-supportability/how-to-create-azure-support-request.md) potrzeb badania dzienników platformy. <br><br> **Uwaga:** po zdarzenia hello jest śledzony przez zespół pomocy technicznej hello, należy nie należy podejmować żadnych własny środki zaradcze ponieważ może to mieć niezamierzonych konsekwencji w danym środowisku. |
| Migracja wdrożenia {nazwa_wdrożenia} w usłudze hostowanej {nazwa_usługi_hostowanej} nie jest obsługiwana, ponieważ jest to wdrożenie PaaS (sieć Web/proces roboczy). |Ma to miejsce w przypadku, gdy wdrożenie zawiera rolę sieci Web/procesu roboczego. Ponieważ migracja jest obsługiwana tylko dla maszyn wirtualnych, Usuń rolę sieci web/proces roboczy hello z hello wdrożenia, a następnie spróbuj ponownie migracji. |
| Wdrożenie szablonu {nazwa_szablonu} nie powiodło się. CorrelationId={guid} |W hello wewnętrznej bazy danych usługi migracji używany w stosie usługi Azure Resource Manager hello zasobów toocreate szablonów usługi Azure Resource Manager. Ponieważ szablony są idempotentności, zwykle można bezpiecznie ponawiania tooget operacji migracji hello poza ten błąd. Jeśli ten błąd będzie się powtarzał toopersist, skontaktuj się z [skontaktuj się z pomocą techniczną platformy Azure](../articles/azure-supportability/how-to-create-azure-support-request.md) i nadaj im hello CorrelationId. <br><br> **Uwaga:** po zdarzenia hello jest śledzony przez zespół pomocy technicznej hello, należy nie należy podejmować żadnych własny środki zaradcze ponieważ może to mieć niezamierzonych konsekwencji w danym środowisku. |
| sieć wirtualna Hello {nazwa wirtualnej sieci} nie istnieje. |Może to nastąpić, jeśli utworzono hello sieci wirtualnej w hello nowego portalu Azure. Rzeczywista nazwa sieci wirtualnej Hello zgodny hello wzorcem "grupy * <VNET name>" |
| Maszyna wirtualna {nazwa_maszyny_wirtualnej} w usłudze hostowanej {nazwa_usługi_hostowanej} zawiera rozszerzenie {nazwa_rozszerzenia}, które nie jest obsługiwane w usłudze Azure Resource Manager. Zalecane jest toouninstall z hello maszyny Wirtualnej przed kontynuowaniem migracji. |Rozszerzenia XML, takie jak BGInfo 1.*, nie są obsługiwane w usłudze Azure Resource Manager. W związku z tym nie można migrować tych rozszerzeń. Te rozszerzenia są po lewej stronie powitania zainstalowanych na maszynie wirtualnej, zostaną automatycznie odinstalowane przed ukończeniem migracji hello. |
| Maszyna wirtualna {nazwa_maszyny_wirtualnej} w usłudze hostowanej {nazwa_usługi_hostowanej} zawiera rozszerzenie VMSnapshot/VMSnapshotLinux, które nie jest obecnie obsługiwane dla migracji. Odinstaluj je z hello maszyny Wirtualnej i dodaj go ponownie przy użyciu usługi Azure Resource Manager po zakończeniu hello migracji |To hello scenariusz, gdzie hello maszyna wirtualna jest skonfigurowana dla usługi Kopia zapasowa Azure. Ponieważ aktualnie jest to nieobsługiwany scenariusz, wykonaj obejście hello na https://aka.ms/vmbackupmigration |
| {Nazwa maszyny wirtualnej} maszyny Wirtualnej w usłudze hostowanej {hostowanej usługi nazwa-} zawiera rozszerzenia {Nazwa rozszerzenia}, których stan nie jest raportowany przez hello maszyny Wirtualnej. Z tego powodu nie można migrować maszyny wirtualnej. Upewnij się, że ten stan rozszerzenia hello jest raportowany lub odinstalować rozszerzenia hello z hello maszyny Wirtualnej i ponów próbę migracji. <br><br> Maszyna wirtualna {nazwa_maszyny_wirtualnej} w usłudze hostowanej {nazwa_usługi_hostowanej} zawiera rozszerzenie {nazwa_rozszerzenia} zgłaszające stan procedury obsługi: {stan_procedury_obsługi}. W związku z tym nie można migrować hello maszyny Wirtualnej. Sprawdź, czy stan programu obsługi rozszerzenia hello zgłaszają {obsługi stanu} lub odinstaluj je z hello maszyny Wirtualnej i ponów próbę migracji. <br><br> Agent maszyny Wirtualnej dla maszyny Wirtualnej {Nazwa maszyny wirtualnej} w usłudze hostowanej {hostowanej usługi nazwa-} to jest raportowanie hello ogólny stan agenta jako nie jest gotowy. W związku z tym hello maszyny Wirtualnej mogły nie zostać zmigrowane, jeśli ma rozszerzenie migrowalna. Upewnij się, że hello agenta maszyny Wirtualnej jest raportowania ogólny stan agenta jako gotowy. Zobacz toohttps://aka.ms/classiciaasmigrationfaqs. |Agent gościa Azure & rozszerzenia maszyny Wirtualnej należy wychodzącego internet access toohello maszyny Wirtualnej magazynu konta toopopulate ich stan. Typowe przyczyny niepowodzenia stanu obejmują następujące sytuacje: <li> Grupy zabezpieczeń sieci, która blokuje toohello wychodzący dostęp internetowe <li> Jeśli hello sieci Wirtualnej ma lokalnych serwerów DNS i łączność DNS zostaną utracone <br><br> Jeśli będziesz kontynuować toosee nieobsługiwany stan, możesz odinstalować tooskip rozszerzenia hello to sprawdzenie i rozpocząć migrację. |
| Migracja wdrożenia {nazwa_wdrożenia} w usłudze hostowanej {nazwa_usługi_hostowanej} nie jest obsługiwana, ponieważ zawiera ono wiele zestawów dostępności. |Obecnie można migrować tylko usługi hostowane, które mają nie więcej niż 1 zestaw dostępności. toowork rozwiązać ten problem, Przenieś hello dodatkowe zestawy dostępności i maszyn wirtualnych w tych zestawów dostępności tooa innej usługi hostowanej. |
| Migracja nie jest obsługiwana dla wdrożenia {Nazwa wdrożenia} w usłudze hostowanej {hostowanej usługi nazwa-bajtowemu maszyn wirtualnych, które nie są częścią zestawu dostępności hello, mimo że hello usługi hostowanej zawiera jeden. |Obejście Hello w tym scenariuszu jest tooeither Przenieś wszystkie maszyny wirtualne hello w jednej dostępności ustawiania lub usuwania wszystkich maszyn wirtualnych z powitalne w usłudze hostowanej hello zestawu dostępności. |
| Magazyn konta/usługi hostowanej/wirtualnej sieci {nazwa wirtualnej sieci} trwa proces jej migrowania hello i dlatego nie można zmienić |Ten błąd wystąpi podczas operacji migracji "Prepare" hello zostało ukończone w zasobie hello i operacji spowodowałoby, że zasób toohello zmiany zostanie wywołany. Z powodu blokady hello na płaszczyźnie zarządzania powitania po wykonaniu operacji "Prepare" wszystkie zmiany toohello zasobów są zablokowane. płaszczyzny zarządzania hello toounlock, można uruchomić hello "Zatwierdź" migracji operacji toocomplete migracji lub hello "Abort" migracji operacji tooroll ponownie hello operacji "Prepare". |
| Migracja jest niedozwolona dla usługi hostowanej {nazwa_usługi_hostowanej}, ponieważ ma ona maszynę wirtualną {nazwa_maszyny_wirtualnej} w stanie: RoleStateUnknown. Migracja jest dozwolone, tylko gdy maszyna wirtualna jest w jednym z następujących hello powitalne stany — uruchomiona, zatrzymana, zatrzymana alokację. |Witaj maszyny Wirtualnej może być przeprowadzana za pośrednictwem zmiany stanu, który zazwyczaj miejsce, gdy podczas operacji update na powitania usługi hostowanej, takie jak ponowne uruchomienie komputera, instalacja rozszerzenia itp. Przed podjęciem próby migracji zaleca dla toocomplete operacji aktualizacji hello na powitania usługi hostowanej. |
| Wdrożenie {Nazwa wdrożenia} w usłudze hostowanej {hostowanej usługi nazwa-} zawiera {Nazwa maszyny wirtualnej} maszyny Wirtualnej z dyskiem danych {danych dysk name}, którego blob fizycznej w bajtach rozmiarze {size-of-the-vhd-blob-backing-the-data-disk} jest niezgodny z {rozmiar logiczny dysku danych maszyny Wirtualnej hello Size-of-the-data-Disk-specified-in-the-VM-API} bajtów. Migracja będzie kontynuowana bez określania rozmiaru dla dysku danych hello hello maszyny Wirtualnej Azure Resource Manager. | Ten błąd wystąpi, jeśli został zmieniony obiektu blob dysku VHD hello bez aktualizowania rozmiar hello hello wirtualna interfejsu API modelu. Szczegółowe kroki zaradcze przedstawiono [poniżej](#vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-the-vm-data-disk-logical-size-bytes).|
| Wystąpił wyjątek magazynu podczas weryfikowania dysku danych {nazwa_dysku_danych} z linkiem multimediów {identyfikator_URI_dysku_danych} dla maszyny wirtualnej {nazwa_maszyny_wirtualnej} w usłudze w chmurze {nazwa_usługi_w_chmurze}. Upewnij się, że tego łącza nośnika wirtualnego dysku twardego hello jest dostępny dla tej maszyny wirtualnej | Ten błąd może się zdarzyć, jeśli dyski hello hello maszyna wirtualna została usunięta lub nie są już dostępne. Upewnij się, że dyski hello hello maszyna wirtualna istnieje.|
| Maszyna wirtualna {nazwa_maszyny_wirtualnej} w usłudze hostowanej {nazwa_usługi_w_chmurze} zawiera dysk z linkiem multimediów {identyfikator_URI_pliku_vhd} mającym nazwę obiektu blob {nazwa_obiektu_blob_pliku_vhd}, który nie jest obsługiwany w usłudze Azure Resource Manager. | Ten błąd występuje, gdy nazwa hello obiektu hello blob ma "/" w nim, który nie jest obsługiwany w obliczeniowe dostawcy zasobów na aktualnie. |
| Nie jest dozwolona migracja wdrożenia {Nazwa wdrożenia} w usłudze hostowanej {— nazwa usługi w chmurze —}, ponieważ nie znajduje się w zakresie regionalnym hello. Przenoszenie ten zakres tooregional wdrożenia, zapoznaj się z toohttp://aka.ms/regionalscope. | W 2014 r. Azure anonsowania, że zasoby sieciowe zostaną przeniesione z zakresu tooregional zakresie poziomu klastra. Aby uzyskać więcej szczegółów, zobacz [http://aka.ms/regionalscope] (http://aka.ms/regionalscope). Ten błąd wystąpi podczas wdrażania hello migrowane nie miał operacji aktualizacji, które automatycznie przenosi je tooa zakresu regionalnego. Najlepsze rozwiązania jest tooeither dodać tooa punktu końcowego maszyny Wirtualnej lub danych na dysku toohello maszyny Wirtualnej, a następnie ponów próbę migracji. <br> Zobacz [jak tooset się punkty końcowe w klasycznym maszyny wirtualnej systemu Windows na platformie Azure](../articles/virtual-machines/windows/classic/setup-endpoints.md#create-an-endpoint) lub [dołączanie danych dysku tooa systemu Windows maszyny wirtualnej utworzonej z hello klasycznego modelu wdrażania](../articles/virtual-machines/windows/classic/attach-disk.md)|


## <a name="detailed-mitigations"></a>Szczegółowe środki zaradcze

### <a name="vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-hello-vm-data-disk-logical-size-bytes"></a>Maszynę Wirtualną za pomocą którego fizyczna obiektu blob w bajtach rozmiar dysku danych jest niezgodny z dysku danych maszyny Wirtualnej hello w bajtach rozmiar logiczny.

Dzieje się tak, gdy hello logicznej rozmiar dysku danych można uzyskać zsynchronizowane z hello rzeczywisty rozmiar obiektu blob dysku VHD. To można łatwo sprawdzić za pomocą następującego polecenia hello:

#### <a name="verifying-hello-issue"></a>Weryfikowanie, czy problem hello

```PowerShell
# Store hello VM details in hello VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

# Display hello data disk properties
# NOTE hello data disk LogicalDiskSizeInGB below which is 11GB. Also note hello MediaLink Uri of hello VHD blob as we'll use this in hello next step
$vm.VM.DataVirtualHardDisks


HostCaching         : None
DiskLabel           : 
DiskName            : coreosvm-coreosvm-0-201611230636240687
Lun                 : 0
LogicalDiskSizeInGB : 11
MediaLink           : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
SourceMediaLink     : 
IOType              : Standard
ExtensionData       : 

# Now get hello properties of hello blob backing hello data disk above
# NOTE hello size of hello blob is about 15 GB which is different from LogicalDiskSizeInGB above
$blob = Get-AzureStorageblob -Blob "coreosvm-dd1.vhd" -Container vhds 

$blob

ICloudBlob        : Microsoft.WindowsAzure.Storage.Blob.CloudPageBlob
BlobType          : PageBlob
Length            : 16106127872
ContentType       : application/octet-stream
LastModified      : 11/23/2016 7:16:22 AM +00:00
SnapshotTime      : 
ContinuationToken : 
Context           : Microsoft.WindowsAzure.Commands.Common.Storage.AzureStorageContext
Name              : coreosvm-dd1.vhd
```

#### <a name="mitigating-hello-issue"></a>Zmniejszenia hello problem

```PowerShell
# Convert hello blob size in bytes tooGB into a variable which we'll use later
$newSize = [int]($blob.Length / 1GB)

# See hello calculated size in GB
$newSize

15

# Store hello disk name of hello data disk as we'll use this tooidentify hello disk toobe updated
$diskName = $vm.VM.DataVirtualHardDisks[0].DiskName

# Identify hello LUN of hello data disk tooremove
$lunToRemove = $vm.VM.DataVirtualHardDisks[0].Lun

# Now remove hello data disk from hello VM so that hello disk isn't leased by hello VM and it's size can be updated
Remove-AzureDataDisk -LUN $lunToRemove -VM $vm | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       213xx1-b44b-1v6n-23gg-591f2a13cd16   Succeeded  

# Verify we have hello right disk that's going toobe updated
Get-AzureDisk -DiskName $diskName

AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : 
Location             : East US
DiskSizeInGB         : 11
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 0c56a2b7-a325-123b-7043-74c27d5a61fd
OperationStatus      : Succeeded

# Now update hello disk toohello new size
Update-AzureDisk -DiskName $diskName -ResizedSizeInGB $newSize -Label $diskName

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureDisk     cv134b65-1b6n-8908-abuo-ce9e395ac3e7 Succeeded 

# Now verify that hello "DiskSizeInGB" property of hello disk matches hello size of hello blob 
Get-AzureDisk -DiskName $diskName


AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : coreosvm-coreosvm-0-201611230636240687
Location             : East US
DiskSizeInGB         : 15
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 1v53bde5-cv56-5621-9078-16b9c8a0bad2
OperationStatus      : Succeeded

# Now we'll add hello disk back toohello VM as a data disk. First we need tooget an updated VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

Add-AzureDataDisk -Import -DiskName $diskName -LUN 0 -VM $vm -HostCaching ReadWrite | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       b0ad3d4c-4v68-45vb-xxc1-134fd010d0f8 Succeeded      
```

### <a name="moving-a-vm-tooa-different-subscription-after-completing-migration"></a>Przenoszenie maszyny Wirtualnej tooa inną subskrypcję po zakończeniu migracji

Po zakończeniu procesu migracji hello można toomove hello wirtualna tooanother subskrypcji. Jednak jeśli masz klucz tajny/certyfikatu na powitania przenieść maszynę Wirtualną, która odwołuje się do zasobu usługi Key Vault hello nie jest obecnie obsługiwane. Witaj poniżej instrukcje pozwoli tooworkaround hello problem. 

#### <a name="powershell"></a>PowerShell
```powershell
$vm = Get-AzureRmVM -ResourceGroupName "MyRG" -Name "MyVM"
Remove-AzureRmVMSecret -VM $vm
Update-AzureRmVM -ResourceGroupName "MyRG" -VM $vm
```
#### <a name="azure-cli-20"></a>Interfejs wiersza polecenia platformy Azure 2.0

```bash
az vm update -g "myrg" -n "myvm" --set osProfile.Secrets=[]
```
