## <a name="overview"></a>Omówienie
Podczas tworzenia nowej maszyny wirtualnej (VM) w grupie zasobów przez wdrożenie obrazu z [portalu Azure Marketplace](https://azure.microsoft.com/marketplace/), dysk systemu operacyjnego domyślny hello wynosi 127 GB. Mimo że jest możliwe tooadd danych dysków toohello maszyny Wirtualnej (jak wiele zależności hello SKU wybrano), a ponadto jest zalecane tooinstall aplikacji i obciążeń intensywnie korzystających z procesora CPU na tych dyskach uzupełnienie, często klienci muszą hello tooexpand systemu operacyjnego dysk toosupport niektórych scenariuszy, takich jak następujące:

1. Obsługa starszych aplikacji, które instalują składniki na dysku systemu operacyjnego.
2. Migrowanie fizycznego komputera lub maszyny wirtualnej ze środowiska lokalnego z większym dyskiem systemu operacyjnego.

> [!IMPORTANT]
> Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: model wdrażania przy użyciu usługi Resource Manager i model klasyczny. W tym artykule omówiono przy użyciu hello modelu Resource Manager. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.
> 
> 

## <a name="resize-hello-os-drive"></a>Zmień rozmiar dysku systemu operacyjnego hello
W tym artykule możemy wykonywać zadania hello zmiany rozmiaru dysku hello systemu operacyjnego za pomocą modułów Menedżera zasobów systemu [programu Azure Powershell](/powershell/azureps-cmdlets-docs). Otwórz okno programu Powershell lub programu Powershell ISE, na których w trybie administratora, a następnie wykonaj poniższe kroki hello:

1. Logowanie tooyour Microsoft Azure konta w trybie zarządzania zasobów i wybrać subskrypcję w następujący sposób:
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. Ustaw nazwę swojej grupy zasobów i nazwę maszyny wirtualnej w następujący sposób:
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. Uzyskaj odwołanie tooyour maszyny Wirtualnej w następujący sposób:
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. Zatrzymaj hello maszyny Wirtualnej przed zmianą rozmiaru dysku hello w następujący sposób:
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. I w tym miejscu możemy oczekiwania do momentu hello! Ustaw rozmiar hello wartości toohello żądanego dysku hello systemu operacyjnego i zaktualizować hello maszyny Wirtualnej w następujący sposób:
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > nowy rozmiar Hello powinna być większa niż rozmiar dysku istniejących hello. Witaj maksymalna dozwolona jest 1023 GB.
   > 
   > 
6. Trwa aktualizowanie hello maszyny Wirtualnej może potrwać kilka sekund. Po zakończeniu działania polecenia hello wykonywania, uruchom ponownie hello maszyny Wirtualnej w następujący sposób:
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

To wszystko! Teraz RDP do hello maszynę Wirtualną, otwórz Zarządzanie komputerem (lub przystawki Zarządzanie dyskami) i rozwiń przy użyciu hello nowo przydzielone miejsce na dysku hello.

## <a name="summary"></a>Podsumowanie
W tym artykule użyliśmy usługi Azure Resource Manager moduły programu Powershell tooexpand hello dysku systemu operacyjnego maszyny wirtualne IaaS. Przedstawionym poniżej jest hello wykonania skryptu użytkownikowi:

```Powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
$vm.StorageProfile.OSDisk.DiskSizeGB = 1023
Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a>Następne kroki
Chociaż w tym artykule, firma Microsoft skupia się głównie na rozszerzania dysku systemu operacyjnego hello hello maszyny Wirtualnej, hello rozwinięte skrypt może także służyć do rozszerzania hello danych dysków dołączonych toohello maszyny Wirtualnej, zmieniając pojedynczy wiersz kodu. Na przykład tooexpand hello pierwsze dane na dysku toohello dołączona maszyna wirtualna, Zastąp hello ```OSDisk``` obiektu ```StorageProfile``` z ```DataDisks``` tablicy i użyć indeksu liczbowego tooobtain dysku odwołanie toofirst dołączonych danych, jak pokazano poniżej:

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
Podobnie można odwoływać się inne toohello dołączonych dysków maszyny Wirtualnej przy użyciu indeksu, jak pokazano powyżej danych lub hello ```Name``` właściwością hello na dysku, jak przedstawiono poniżej:

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

Jeśli toofind się jak tooattach dyski tooan maszyny Wirtualnej Azure Resource Manager, należy to sprawdzić [artykułu](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

