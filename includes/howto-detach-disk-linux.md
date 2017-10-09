Jeśli nie ma potrzeby dysku danych, który jest dołączony tooa maszyny wirtualnej (VM), możesz ją łatwo odłączyć. Jeśli można odłączyć dysku od maszyny Wirtualnej hello, hello dysku nie jest on usunięty z magazynu. Jeśli chcesz ponownie toouse hello istniejące dane na dysku hello, użytkownik może dołączyć go toohello tej samej maszyny Wirtualnej lub innej.  

> [!NOTE]
> Maszyna wirtualna na platformie Azure używa różnych typów dysku — dysku systemu operacyjnego, lokalnego dysku tymczasowego i opcjonalnych dysków danych. Szczegółowe informacje zawiera artykuł [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Informacje o dyskach i dyskach VHD maszyn wirtualnych). Nie można odłączyć dysku systemu operacyjnego, chyba że zostaną również usunięte hello maszyny Wirtualnej.

## <a name="find-hello-disk"></a>Znajdź hello dysku
Zanim można odłączyć dysku od maszyny Wirtualnej należy toofind limit hello numer jednostki LUN, który jest identyfikatorem toobe dysku hello odłączona. toodo, który, wykonaj następujące kroki:

1. Otwieranie wiersza polecenia platformy Azure i [połączyć tooyour subskrypcji platformy Azure](../articles/xplat-cli-connect.md). Upewnij się, że jesteś w trybie usługi Azure Service Management (`azure config mode asm`).
2. Dowiedz się, które dyski są dołączone tooyour maszyny Wirtualnej. Witaj poniższy przykład zawiera listę dysków dla maszyny Wirtualnej o nazwie hello `myVM`:

    ```azurecli
    azure vm disk list myVM
    ```

    Witaj danych wyjściowych jest toohello podobnie poniższy przykład:

    ```azurecli
    * Fetching disk images
    * Getting virtual machines
    * Getting VM disks
      data:    Lun  Size(GB)  Blob-Name                         OS
      data:    ---  --------  --------------------------------  -----
      data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
      data:    0    30        myDataDisk.vhd
      info:    vm disk list command OK
    ```

3. Należy zwrócić uwagę hello jednostki LUN lub hello **numeru jednostki logicznej** hello dysku, które mają toodetach.

## <a name="remove-operating-system-references-toohello-disk"></a>Usuń dysk toohello odwołuje się do systemu operacyjnego
Przed odłączeniem dysku powitania od hello Linux gościa, należy się upewnić, że wszystkie partycje dysku hello nie są używane. Upewnij się, hello systemu operacyjnego nie będzie podejmował tooremount je po ponownym rozruchu. Te kroki cofnąć prawdopodobnie zostały utworzone podczas konfiguracji hello [dołączanie](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) hello dysku.

1. Użyj hello `lsscsi` identyfikator dysku hello toodiscover polecenia. Program `lsscsi` można zainstalować za pomocą polecenia `yum install lsscsi` (dystrybucje oparte na systemie Red Hat) lub `apt-get install lsscsi` (dystrybucje oparte na systemie Debian). Można znaleźć identyfikatora dysku hello, którego szukasz przy użyciu numeru LUN hello. numer ostatniej Hello w spójnej kolekcji hello w każdym wierszu jest hello jednostki LUN. W hello poniższy przykład z `lsscsi`, jednostka LUN 0 mapuje zbyt  */dev/sdc*

    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```

2. Użyj `fdisk -l <disk>` partycje hello toodiscover skojarzone z toobe dysku hello odłączona. Witaj poniższy przykład przedstawia dane wyjściowe hello `/dev/sdc`:

    ```bash
    Disk /dev/sdc: 1098.4 GB, 1098437885952 bytes, 2145386496 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x5a1d2a1a
    
        Device Boot      Start         End      Blocks   Id  System
    /dev/sdc1            2048  2145386495  1072692224   83  Linux
    ```

3. Odinstaluj każdej partycji dysku hello na liście. Witaj poniższy przykład odinstalowuje `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

4. Użyj hello `blkid` polecenia toodiscovery hello UUID dla wszystkich partycji. Witaj danych wyjściowych jest toohello podobnie poniższy przykład:

    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

5. Usunięcie pozycji hello **/etc/fstab** plik skojarzony z ścieżek urządzeń hello lub UUID dla wszystkich partycji dla toobe dysku hello odłączona.  Wpisy dla tego przykładu mogą być następujące:

    ```sh  
   UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2
   ```

    lub
   
   ```sh   
   /dev/sdc1   /datadrive   ext4   defaults   1   2
   ```

## <a name="detach-hello-disk"></a>Odłączanie dysku hello
Po znalezieniu numer jednostki LUN hello hello dysku i usuniętych hello odwołań systemu operacyjnego, wszystko jest gotowe toodetach go:

1. Odłącz hello wybrany dysk z maszyny wirtualnej hello, uruchamiając polecenie hello `azure vm disk detach
   <virtual-machine-name> <LUN>`. Witaj poniższy przykład odłącza LUN `0` z hello maszyny Wirtualnej o nazwie `myVM`:
   
    ```azurecli
    azure vm disk detach myVM 0
    ```

2. Możesz sprawdzić, jeśli hello dysku został odłączony, uruchamiając `azure vm disk list` ponownie. powitania po kontroli przykład Witaj maszyny Wirtualnej o nazwie `myVM`:
   
    ```azurecli
    azure vm disk list myVM
    ```

    Witaj danych wyjściowych jest podobne toohello poniższy przykład, który zawiera informacje o dysku danych hello jest już dołączony:

    ```azurecli
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
     info:    vm disk list command OK
    ```

Hello odłączyć dysk przechowywania, ale nie jest już dołączony tooa maszyny wirtualnej.

