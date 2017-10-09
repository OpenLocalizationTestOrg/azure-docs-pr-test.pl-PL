
Aby uzyskać więcej informacji o dyskach, zobacz [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Informacje o dyskach i wirtualnych dyskach twardych dla maszyn wirtualnych).

<a id="attachempty"></a>

## <a name="attach-an-empty-disk"></a>Dołączanie pustego dysku
1. Otwórz 1.0 interfejsu wiersza polecenia platformy Azure i [połączyć tooyour subskrypcji platformy Azure](../articles/xplat-cli-connect.md). Upewnij się, że jesteś w trybie usługi Azure Service Management (`azure config mode asm`).
2. Wprowadź `azure vm disk attach-new` toocreate i dołączyć nowego dysku, jak pokazano w hello poniższy przykład. Zastąp *myVM* o nazwie hello z maszyny wirtualnej systemu Linux i określ rozmiar hello dysku hello w GB, który jest *100GB* w tym przykładzie:

    ```azurecli
    azure vm disk attach-new myVM 100
    ```

3. Po utworzeniu i dołączyć dysku danych hello, znajduje się w danych wyjściowych hello `azure vm disk list <virtual-machine-name>` pokazane na powitania poniższy przykład:
   
    ```azurecli
    azure vm disk list TestVM
    ```

    Witaj danych wyjściowych jest toohello podobnie poniższy przykład:

    ```bash
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        myVM-2645b8030676c8f8.vhd  Linux
     data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

<a id="attachexisting"></a>

## <a name="attach-an-existing-disk"></a>Dołączanie istniejącego dysku
Dołączanie istniejącego dysku wymaga pliku vhd dostępnego na koncie magazynu.

1. Otwórz 1.0 interfejsu wiersza polecenia platformy Azure i [połączyć tooyour subskrypcji platformy Azure](../articles/xplat-cli-connect.md). Upewnij się, że jesteś w trybie usługi Azure Service Management (`azure config mode asm`).
2. Sprawdź, czy hello wirtualnego dysku twardego mają być tooattach jest już przekazany tooyour subskrypcji platformy Azure:
   
    ```azurecli
    azure vm disk list
    ```

    Witaj danych wyjściowych jest toohello podobnie poniższy przykład:

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
     data:    Name                                          OS
     data:    --------------------------------------------  -----
     data:    myTestVhd                                     Linux
     data:    TestVM-ubuntuVMasm-0-201508060029150744  Linux
     data:    TestVM-ubuntuVMasm-0-201508060040530369
     info:    vm disk list command OK
    ```

3. Jeśli nie można znaleźć dysku hello czy chcesz toouse, może przekazać subskrypcji tooyour lokalnego wirtualnego dysku twardego za pomocą `azure vm disk create` lub `azure vm disk upload`. Przykład `disk create` byłoby jak hello poniższy przykład:
   
    ```azurecli
    azure vm disk create myVhd .\TempDisk\test.VHD -l "East US" -o Linux
    ```

    Witaj danych wyjściowych jest toohello podobnie poniższy przykład:

    ```azurecli
    info:    Executing command vm disk create
    + Retrieving storage accounts
    info:    VHD size : 10 GB
    info:    Uploading 10485760.5 KB
    Requested:100.0% Completed:100.0% Running:   0 Time:   25s Speed:    82 KB/s
    info:    Finishing computing MD5 hash, 16% is complete.
    info:    https://mystorageaccount.blob.core.windows.net/disks/myVHD.vhd was
    uploaded successfully
    info:    vm disk create command OK
    ```
   
   Można także użyć `azure vm disk upload` tooupload konta magazynu określonych tooa wirtualnego dysku twardego. Przeczytaj więcej na temat hello polecenia toomanage dysków danych maszyny wirtualnej Azure [za pośrednictwem tutaj](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

4. Teraz możesz dołączyć hello potrzeby maszyny wirtualnej tooyour wirtualnego dysku twardego:
   
    ```azurecli
    azure vm disk attach myVM myVhd
    ```
   
   Upewnij się, że tooreplace *myVM* o nazwie hello maszyny wirtualnej, i *myVHD* z żądaną dysk VHD.

5. Możesz sprawdzić dysku hello jest dołączona toohello maszynę wirtualną z `azure vm disk list <virtual-machine-name>`:
   
    ```azurecli
    azure vm disk list myVM
    ```

    Witaj danych wyjściowych jest toohello podobnie poniższy przykład:

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        TestVM-2645b8030676c8f8.vhd  Linux
     data:    1    10        test.VHD
     data:    0    100        TestVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

> [!NOTE]
> Po dodaniu dysku danych, będzie konieczne toolog na maszynie wirtualnej toohello i zainicjalizować dysk hello, więc hello może używać maszyna wirtualna hello dysku magazynu (zobacz hello następujące kroki Aby uzyskać więcej informacji na jak toodo zainicjalizować dysk hello).
> 
> 

