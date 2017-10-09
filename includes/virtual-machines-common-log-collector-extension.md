
Diagnozowanie problemów z usługą w chmurze Microsoft Azure wymaga zbieranie plików dziennika usługi hello na maszynach wirtualnych, ponieważ występują problemy z hello. Można użyć hello AzureLogCollector rozszerzenia na żądanie tooperfom jednorazowe kolekcję dzienników z maszyn wirtualnych usługi w chmurze (od ról sieć web i roli proces roboczy) i transfer hello zebrane pliki tooan kontem magazynu platformy Azure — wszystko to bez zdalne logowanie tooany hello maszyn wirtualnych.

> [!NOTE]
> Opisy dla większości hello rejestrowane informacje znajdują się w http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.
> 
> 

Zależne od typów hello toobe pliki pobierane są dwa tryby kolekcji.

* Gość Azure dzienniki agentów tylko (GA). Ten tryb kolekcji zawiera wszystkich agentów gości pokrewne tooAzure hello dzienniki i inne składniki platformy Azure.
* Wszystkie dzienniki (pełną). Ten tryb kolekcji będzie zbierać wszystkie pliki w trybie GA plus:
  
  * dzienniki zdarzeń systemu i aplikacji
  * Dzienniki błędów HTTP
  * Dzienniki programu IIS
  * Dzienniki instalacji
  * inne dzienniki systemu

W obu trybach kolekcji można określić przy użyciu kolekcji hello następujące struktury folderów kolekcji dodatkowe dane:

* **Nazwa**: Nazwa hello hello kolekcji, która będzie używana jako nazwa podfolderu wewnątrz toobe pliku zip hello hello zbierane.
* **Lokalizacja**: hello toohello folder ścieżki na maszynie wirtualnej hello gdzie będą zbierane pliku.
* **SearchPattern**: hello wzorzec nazw hello toobe pliki pobierane. Domyślna to "*"
* **Cykliczne**: Jeśli hello pliki będą zbierane rekursywnie w folderze hello.

## <a name="prerequisites"></a>Wymagania wstępne
* Należy toohave konta magazynu dla plików zip toosave wygenerowany rozszerzeń.
* Należy upewnić się, że używasz V0.8.0 poleceń cmdlet programu PowerShell Azure lub nowszej. Aby uzyskać więcej informacji, zobacz [Azure pobiera](https://azure.microsoft.com/downloads/).

## <a name="add-hello-extension"></a>Dodaj rozszerzenie hello
Można użyć [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) poleceń cmdlet lub [API REST zarządzania usługami](https://msdn.microsoft.com/library/ee460799.aspx) hello tooadd AzureLogCollector rozszerzenia.

Dla usług w chmurze, hello istniejącego polecenia cmdlet Azure Powershell, **AzureServiceExtension zestaw**, mogą być używane tooenable hello rozszerzenia dla wystąpień roli usługi w chmurze. Za każdym razem, gdy to rozszerzenie jest włączona za pomocą tego polecenia cmdlet, zbieranie danych dziennika zostanie wywołany dla wystąpień roli hello wybrane wybranych ról.

W przypadku maszyn wirtualnych hello istniejącego polecenia cmdlet Azure Powershell, **AzureVMExtension zestaw**, mogą być używane tooenable hello rozszerzenia na maszynach wirtualnych. Za każdym razem, gdy to rozszerzenie jest włączona za pomocą poleceń cmdlet hello, zbierania dzienników jest wyzwalane w każdym wystąpieniu.

Wewnętrznie to rozszerzenie używa hello PublicConfiguration opartych na formacie JSON i PrivateConfiguration. następujące Hello jest układ hello próbki JSON konfiguracji publiczne i prywatne.

### <a name="publicconfiguration"></a>PublicConfiguration
    {
        "Instances":  "*",
        "Mode":  "Full",
        "SasUri":  "SasUri tooyour storage account with sp=wl",
        "AdditionalData":
        [
          {
                  "Name":  "StorageData",
                  "Location":  "%roleroot%storage",
                  "SearchPattern":  "*.*",
                  "Recursive":  "true"
          },
          {
                "Name":  "CustomDataFolder2",
                "Location":  "c:\customFolder",
                "SearchPattern":  "*.log",
                "Recursive":  "false"
          },
        ]
    }

### <a name="privateconfiguration"></a>PrivateConfiguration
    {

    }

> [!NOTE]
> To rozszerzenie nie wymaga **privateConfiguration**. Podobnie można zapewnić pustą strukturą hello **— PrivateConfiguration** argumentu.
> 
> 

Możesz wykonać jedną z dwóch hello następujące kroki tooadd hello AzureLogCollector tooone lub więcej wystąpień usługi w chmurze lub maszynę wirtualną wybranych ról, które wyzwalaczy hello kolekcje w każdej toorun maszyny Wirtualnej i wysyłać hello zebrane pliki tooAzure konta określona.

## <a name="adding-as-a-service-extension"></a>Dodawanie jako rozszerzenie usługi
1. Wykonaj hello instrukcje tooconnect programu Azure PowerShell tooyour subskrypcji.
2. Określ nazwę usługi hello, miejsca, ról i toowhich wystąpień roli mają tooadd i włączyć rozszerzenie AzureLogCollector hello.
   
        #Specify your cloud service name
        $ServiceName = 'extensiontest2'
   
        #Specify hello slot. 'Production' or 'Staging'
        $slot = 'Production'
   
        #Specified hello roles on which hello extension will be installed and enabled
        $roles = @("WorkerRole1","WebRole1")
   
        #Specify hello instances on which extension will be installed and enabled.  Use wildcard * for all instances
        $instances = @("*")
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
3. Określ folder dodatkowe dane hello, dla której będą zbierane pliki (ten krok jest opcjonalny).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > Można użyć tokenu `%roleroot%` toospecify hello roli katalog główny dysku, ponieważ nie używa dysk stały.
   > 
   > 
4. Podaj nazwę konta magazynu Azure hello i klucza toowhich zebrane pliki zostaną przekazane.
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. Wywołania hello SetAzureServiceLogCollector.ps1 (dołączony na końcu artykułu hello hello) jako sposób tooenable hello AzureLogCollector rozszerzenia dla usługi w chmurze. Po zakończeniu wykonywania hello można znaleźć pliku hello przekazany w`https://YouareStorageAccountName.blob.core.windows.net/vmlogs`
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

Witaj poniżej znajduje się definicja hello hello parametry przekazywane toohello skryptu. (To jest kopiowana poniżej również.)

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
      [Parameter(Mandatory=$true)]
    [string]   $ServiceName,

    [Parameter(Mandatory=$false)]
    [string[]] $Roles ,

    [Parameter(Mandatory=$false)]
    [string[]] $Instances,

    [Parameter(Mandatory=$false)]
    [string]   $Slot = 'Production',

    [Parameter(Mandatory=$false)]
    [string]   $Mode = 'Full',

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountName,

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountKey,

    [Parameter(Mandatory=$false)]
    [PSObject[]] $AdditionDataLocationList = $null
    )

* *ServiceName*: Nazwa usługi w chmurze.
* *Role*: lista ról, takich jak "WebRole1" lub "WorkerRole1".
* *Wystąpienia*: Lista nazw hello wystąpień roli oddzielonych przecinkami — Użyj hello ciąg symbolu wieloznacznego ("*") dla wszystkich wystąpień roli.
* *Gniazdo*: nazwa miejsca. "Production" lub "Tymczasowości".
* *Tryb*: tryb kolekcji. "Pełnej" lub "GA".
* *StorageAccountName*: Nazwa Azure konta magazynu do przechowywania zbieranych danych.
* *StorageAccountKey*: klucz konta magazynu Name Azure.
* *AdditionalDataLocationList*: Lista hello następujące struktury:
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a>Dodawanie jako rozszerzenie maszyny Wirtualnej
Wykonaj hello instrukcje tooconnect programu Azure PowerShell tooyour subskrypcji.

1. Określ nazwę usługi hello, maszyny Wirtualnej i tryb kolekcji hello.
   
        #Specify your cloud service name
        $ServiceName = 'YourCloudServiceName'
   
        #Specify hello VM name
        $VMName = "'YourVMName'"
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
   
        Specify hello additional data folder for which files will be collected (this step is optional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
2. Podaj nazwę konta magazynu Azure hello i klucza toowhich zebrane pliki zostaną przekazane.
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. Wywołania hello SetAzureVMLogCollector.ps1 (dołączony na końcu artykułu hello hello) jako sposób tooenable hello AzureLogCollector rozszerzenia dla usługi w chmurze. Po zakończeniu wykonywania hello można znaleźć pliku hello przekazany w https://YouareStorageAccountName.blob.core.windows.net/vmlogs

Witaj poniżej znajduje się definicja hello hello parametry przekazywane toohello skryptu. (To jest kopiowana poniżej również.)

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
        [Parameter(Mandatory=$true)]
      [string]   $ServiceName,

      [Parameter(Mandatory=$false)]
      [string] $VMName ,

        [Parameter(Mandatory=$false)]
      [string]   $Mode = 'Full',

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountName,

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountKey,

      [Parameter(Mandatory=$false)]
      [PSObject[]] $AdditionDataLocationList = $null
      )

* ServiceName: Twoje nazwa usługi w chmurze.
* Nazwa hello VMName hello maszyny Wirtualnej.
* Tryb: Tryb kolekcji. "Pełnej" lub "GA".
* StorageAccountName: Nazwa konta magazynu Azure do przechowywania zebranych danych.
* StorageAccountKey: Nazwa klucz konta magazynu platformy Azure.
* AdditionalDataLocationList: Lista hello następujące struktury:

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a>Rozszerzenie plików skryptów środowiska PowerShell
SetAzureServiceLogCollector.ps1

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Roles ,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Instances = '*',

                  [Parameter(Mandatory=$false)]
                  [string]   $Slot = 'Production',

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject

    if ($Instances -ne $null -and $Instances.Count -gt 0)  #Instances should be seperated by ,
    {
        $instanceText = $Instances[0]
        for ($i = 1;$i -lt $Instances.Count;$i++)
        {
              $instanceText = $instanceText+ "," + $Instances[$i]
          }
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value $instanceText
    }
    else  #For all instances if not specified.  hello value should be a space or *
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value " "
    }

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json
    "publicConfig is:  $publicConfigJSON"

    #we just provide a empty privateConfig object
    $privateconfig = "{
    }"

    if ($Roles -ne $null)
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot -Role $Roles -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }
    else
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot  -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }

    #
    #This is an optional step: generate a sasUri toohello container so it can be shared with other people if nened
    #
    $SasExpireTime = [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rl -Context $context
    $SasUri = $SasUri + "&restype=container&comp=list"
    Write-Output "hello container for uploaded file can be accessed using this link:`r`n$sasuri"


SetAzureVMLogCollector.ps1

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string] $VMName ,

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject
    $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value "*"

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(90).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json

    Write-Output "PublicConfigurtion is: \r\n$publicConfigJSON"

    #
    #we just provide a empty privateConfig object
    #
    $privateconfig = "{
    }"

    if ($VMName -ne $null )
    {
          $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
          $VM.VM.OSVirtualHardDisk.OS

          if ($VM.VM.OSVirtualHardDisk.OS -like '*Windows*')
          {
                Set-AzureVMExtension -VM $VM -ExtensionName "AzureLogCollector" -Publisher Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.* | Update-AzureVM -Verbose

                #
                #We will check hello VM status toofind if operation by extension has been completed or not. hello completion of hello operation,either succeed or fail, can be indicated by
                #hello presence of SubstatusList field.
                #
                $Completed = $false
                while ($Completed -ne $true)
                {
                        $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
                        $status = $VM.ResourceExtensionStatusList | Where-Object {$_.HandlerName -eq "Microsoft.WindowsAzure.Compute.AzureLogCollector"}

                        if ( ($status.Code -ne 0) -and ($status.Status -like '*error*'))
                        {
                            Write-Output "Error status is returned: $($Status.ExtensionSettingStatus.FormattedMessage.Message)."
                              $Completed = $true
                        }
                        elseif (($status.ExtensionSettingStatus.SubstatusList -eq $null -or $status.ExtensionSettingStatus.SubstatusList.Count -lt 1))
                        {
                              $Completed = $false
                              Write-Output "Waiting for operation toocomplete..."
                        }
                        else
                        {
                              $Completed = $true
                              Write-Output "Operation completed."

                        $UploadedFileUri = $Status.ExtensionSettingStatus.SubStatusList[0].FormattedMessage.Message
                              $blob = New-Object Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob($UploadedFileUri)

                      #
                            # This is an optional step:  For easier access toohello file, we can generate a read-only SasUri directly toohello file
                              #
                              $ExpiryTimeRead =  [DateTime]::Now.AddMinutes(120).ToString("o")
                              $ReadSasUri = New-AzureStorageBlobSASToken -ExpiryTime $ExpiryTimeRead  -FullUri  -Blob  $blob.name -Container $blob.Container.Name -Permission r -Context $context

                            Write-Output "hello uploaded file can be accessed using this link: $ReadSasUri"

                              #
                              #This is an optional step:  Remove hello extension after we are done
                              #
                              Get-AzureVM -ServiceName $ServiceName -Name $VMName | Set-AzureVMExtension -Publisher Microsoft.WindowsAzure.Compute -ExtensionName "AzureLogCollector" -Version 1.* -Uninstall | Update-AzureVM -Verbose

                        }
                        Start-Sleep -s 5
                }
          }
          else
          {
              Write-Output "VM OS Type is not Windows, hello extension cannot be enabled"
          }

    }
    else
    {
      Write-Output "VM name is not specified, hello extension cannot be enabled"
    }

## <a name="next-steps"></a>Następne kroki
Teraz możesz zbadać lub skopiuj dzienniki z jednej lokalizacji bardzo proste.

