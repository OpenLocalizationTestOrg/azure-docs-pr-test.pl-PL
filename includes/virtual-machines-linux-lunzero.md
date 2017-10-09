Podczas dodawania tooa dysków danych maszyny Wirtualnej systemu Linux, mogą wystąpić błędy, jeśli dysk nie istnieje w jednostce LUN 0. Jeśli dodajesz dysk ręcznie przy użyciu hello `azure vm disk attach-new` polecenia i podaj jednostkę LUN (`--lun`) zamiast stosowanie hello toodetermine platformy Azure hello odpowiednie jednostki LUN, zwrócić uwagę, że dysk już istnieje / będzie istniał w momencie LUN 0. 

Należy wziąć pod uwagę hello poniższy przykład przedstawiający fragment danych wyjściowych hello `lsscsi`:

```bash
[5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc 
[5:0:0:1]    disk    Msft     Virtual Disk     1.0   /dev/sdd 
```

istnieje Hello dwóch dysków z danymi w jednostce LUN 0 i 1 jednostka LUN (hello pierwszej kolumny hello `lsscsi` szczegóły danych wyjściowych `[host:channel:target:lun]`). Obydwa dyski powinny być accessbile z wewnątrz hello maszyny Wirtualnej. Jeśli ręcznie ma określony hello na 1 jednostki LUN i drugiego dysku hello w jednostce LUN 2 dodaje pierwszy toobe dysku, nie widać dysków hello poprawnie z wewnątrz maszyny Wirtualnej.

> [!NOTE]
> Hello Azure `host` wartość to 5 w tym przykładzie, ale to może się różnić w zależności od typu hello magazynu należy wybrać.
> 
> 

To zachowanie dysku nie jest problem Azure, ale sposób hello, w których hello Linux jądra następuje hello specyfikacje SCSI. Gdy jądra systemu Linux hello skanuje hello magistrali SCSI urządzenia podłączone, urządzenie musi zostać znaleziony w jednostce LUN 0 Aby toocontinue systemu hello skanowanie w poszukiwaniu dodatkowych urządzeń. Sposób:

* Przejrzyj dane wyjściowe hello `lsscsi` po dodaniu tooverify dysku danych, ma dysku o numerze LUN 0.
* Jeśli dysk nie jest wyświetlany prawidłowo w ramach maszyny Wirtualnej, sprawdź, czy istnieje dysku o numerze LUN 0.

