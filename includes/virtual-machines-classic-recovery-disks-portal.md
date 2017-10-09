Jeśli maszyny wirtualnej (VM) na platformie Azure napotkał błąd podczas rozruchu lub dysk, może być konieczne tooperform kroki na powitania wirtualnego dysku twardego sam rozwiązywania problemów. Typowym przykładem jest aktualizację aplikacji, która uniemożliwia rozruch pomyślnie hello maszyny Wirtualnej. W tym artykule opisano sposób toouse tooconnect portalu Azure toofix wirtualna tooanother Twojego wirtualnego dysku twardego wszelkie błędy i ponownie utwórz oryginalnego maszyny Wirtualnej.

## <a name="recovery-process-overview"></a>Omówienie procesu odzyskiwania
proces rozwiązywania problemów Hello jest następujący:

1. Usunąć hello maszynę Wirtualną, która napotyka problemy, ale zachować hello wirtualnych dysków twardych.
2. Dołączanie i instalacji hello tooanother wirtualnego dysku twardego maszyny Wirtualnej do rozwiązywania problemów.
3. Połącz toohello Rozwiązywanie problemów z maszyny Wirtualnej. Edytowanie plików lub uruchamianie narzędzi toofix błędy na oryginalny wirtualny dysk twardy hello.
4. Odinstaluj obraz i odłączyć hello wirtualnego dysku twardego z hello Rozwiązywanie problemów z maszyny Wirtualnej.
5. Utwórz maszynę Wirtualną za pomocą oryginalny wirtualny dysk twardy hello.

## <a name="delete-hello-original-vm"></a>Usuń hello oryginalna maszyna wirtualna
Wirtualne dyski twarde i maszyny wirtualne to dwa odrębne zasoby na platformie Azure. Wirtualny dysk twardy jest przechowywania hello systemu operacyjnego, aplikacje i konfiguracje. Witaj maszyny Wirtualnej są tylko metadane definiujący rozmiar hello lub lokalizacji i który odwołuje się do zasobów, takich jak wirtualny dysk twardy lub sieć wirtualna karta sieciowa (NIC). Każdy wirtualny dysk twardy pobiera dzierżawy, przypisać właściwości, gdy jest podłączone tooa maszyny Wirtualnej. Mimo że dysków z danymi można dołączone i odłączone nawet wtedy, gdy hello maszyna wirtualna jest uruchomiona, dysk systemu operacyjnego hello nie można odłączyć, chyba że hello zasobu maszyny Wirtualnej zostanie usunięta. dzierżawy Hello nadal tooa dysku systemu operacyjnego hello tooassociate maszyny Wirtualnej, nawet w przypadku tej maszyny Wirtualnej w stanie zatrzymania i deallocated.

pierwszy krok toorecovering Hello maszyny Wirtualnej jest zasobu maszyny Wirtualnej na powitania toodelete samej siebie. Usuwanie hello maszyny Wirtualnej pozostawia hello wirtualnych dysków twardych na koncie magazynu. Po hello usuwać maszyny Wirtualnej można dołączyć hello wirtualnego dysku twardego tooanother wirtualna tootroubleshoot i usuń błędy hello. 

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com). 
2. Polecenie hello menu po lewej stronie powitania **maszyn wirtualnych (klasyczne)**.
3. Kliknij maszynę Wirtualną, która ma hello problem wybierz hello **dysków**, a następnie określ nazwę hello hello wirtualnego dysku twardego. 
4. Wybierz wirtualny dysk twardy hello systemu operacyjnego i sprawdzić hello **lokalizacji** konta magazynu hello tooidentify, który zawiera ten wirtualny dysk twardy. W hello poniższy przykład, hello ciąg bezpośrednio przed wywołaniem ". blob.core.windows.net" jest nazwą konta magazynu hello.

    ```
    https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd
    ```

    ![Obraz powitania o lokalizację maszyny Wirtualnej](./media/virtual-machines-classic-recovery-disks-portal/vm-location.png)

5. Kliknij prawym przyciskiem myszy hello maszyny Wirtualnej, a następnie wybierz **usunąć**. Upewnij się, hello dyski nie są wybrane po usunięciu hello maszyny Wirtualnej.
6. Utwórz nową maszynę wirtualną odzyskiwania. Ta maszyna wirtualna musi być w hello tego samego regionu i grupie zasobów (usługi w chmurze) jako problem hello maszyny Wirtualnej.
7. Wybierz hello odzyskiwania maszyny Wirtualnej, a następnie wybierz **dysków** > **dołączanie istniejącego**.
8. tooselect istniejącego wirtualnego dysku twardego, kliknij przycisk **pliku VHD**:

    ![Przeglądnie w poszukiwaniu istniejącego dysku VHD](./media/virtual-machines-classic-recovery-disks-portal/select-vhd-location.png)

9. Wybierz konto magazynu hello > kontener wirtualnego dysku twardego > hello wirtualnego dysku twardego, kliknij przycisk hello **wybierz** przycisk tooconfirm wybór.

    ![Wybieranie istniejącego wirtualnego dysku twardego](./media/virtual-machines-classic-recovery-disks-portal/select-vhd.png)

10. Teraz wybrać dysk VHD, wybierz polecenie **OK** tooattach hello istniejącego wirtualnego dysku twardego.
11. Po kilku sekundach hello **dysków** okienku dla maszyny Wirtualnej zostaną wyświetlone istniejącego wirtualnego dysku twardego połączenia jako dysk z danymi:

    ![Istniejący wirtualny dysk twardy dołączony jako dysk danych](./media/virtual-machines-classic-recovery-disks-portal/attached-disk.png)

## <a name="fix-issues-on-hello-original-virtual-hard-disk"></a>Rozwiązywanie problemów na oryginalny wirtualny dysk twardy hello
W przypadku istniejącego wirtualnego dysku twardego hello jest zainstalowany, można teraz wykonywać żadnych konserwacji i kroki rozwiązywania problemów, zgodnie z potrzebami. Po ma problemu hello problemów, należy kontynuować hello następujące kroki.

## <a name="unmount-and-detach-hello-original-virtual-hard-disk"></a>Odinstaluj obraz i odłączyć oryginalny wirtualny dysk twardy hello
Po rozwiązaniu wszelkie błędy, odinstaluj i odłączyć hello istniejącego wirtualnego dysku twardego z rozwiązywania problemów z maszyny Wirtualnej. Nie można użyć wirtualnego dysku twardego wraz z innych maszyn wirtualnych, do czasu zwolnienia dzierżawy hello, łączący toohello wirtualnego dysku twardego hello Rozwiązywanie problemów z maszyny Wirtualnej.  

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com). 
2. Witaj menu po lewej stronie powitania, wybierz **maszyn wirtualnych (klasyczne)**.
3. Zlokalizuj hello odzyskiwania maszyny Wirtualnej. Wybierz dyski, dysku powitania kliknij prawym przyciskiem myszy, a następnie wybierz **Detach**.

## <a name="create-a-vm-from-hello-original-hard-disk"></a>Utwórz maszynę Wirtualną z hello oryginalny dysk twardy

Użyj Maszynę wirtualną z oryginalnego wirtualnego dysku twardego, toocreate [klasycznego portalu Azure](https://manage.windowsazure.com).

1. Zaloguj się do [klasycznej witryny Azure Portal](https://manage.windowsazure.com).
2. U dołu hello hello portalu, wybierz **nowy** > **obliczeniowe** > **maszyny wirtualnej** > **z galerii** .
3. W hello **wybierz obraz** zaznacz **dysków**, a następnie wybierz hello oryginalny wirtualny dysk twardy. Sprawdź informacje o lokalizacji hello. Jest to region hello musi wdrożonym hello maszyny Wirtualnej. Wybierz przycisk Dalej hello.
4. W hello **konfiguracji maszyny wirtualnej** sekcji, wpisz nazwę maszyny Wirtualnej hello i wybierz rozmiar hello maszyny Wirtualnej.
