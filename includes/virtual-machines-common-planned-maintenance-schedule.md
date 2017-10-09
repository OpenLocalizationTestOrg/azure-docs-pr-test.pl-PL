

## <a name="multi-and-single-instance-vms"></a>Obsługa wielu i jednego wystąpienia maszyny wirtualne
Wielu klientów systemem Azure liczba go krytycznych, czy można zaplanować podczas ich maszyny wirtualne przechodzą zaplanowanej konserwacji powodu przestoju toohello — około 15 minut — występuje podczas konserwacji. Podczas zaplanowanej konserwacji odbierania elastycznie maszyn wirtualnych, można użyć formantu toohelp zestawów dostępności.

Istnieją dwie możliwe konfiguracje dla maszyn wirtualnych działających na platformie Azure. Maszyny wirtualne albo są skonfigurowane jako jednym czy wielu wystąpieniach. W przypadku maszyn wirtualnych w zestawie dostępności, następnie są skonfigurowane z opcją wielu wystąpień. Należy pamiętać, nawet pojedynczy maszyn wirtualnych można wdrożyć w zestawie dostępności, dzięki czemu są one traktowane jako mająca wiele wystąpień. Jeśli maszyny wirtualne nie są dostępne w zestawie dostępności, następnie są skonfigurowane z opcją jednego wystąpienia.  Szczegółowe informacje dotyczące zestawów dostępności, zobacz [hello Zarządzaj dostępność maszyn wirtualnych z systemem Windows](../articles/virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) lub [hello Zarządzaj dostępności dla maszyn wirtualnych systemu Linux](../articles/virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Zaplanowanej konserwacji aktualizuje wystąpienia toosingle i wielu wystąpień maszyn wirtualnych stanie oddzielnie. Przy ponownej konfiguracji sieci maszyn wirtualnych toobe jednego wystąpienia (jeśli są one wielu wystąpień) lub wielu wystąpieniach toobe (jeśli są one jednego wystąpienia) można kontrolować, po ich maszyn wirtualnych komunikatu hello planowanych konserwacji. Zobacz [zaplanowanej konserwacji dla maszyn wirtualnych systemu Linux Azure](../articles/virtual-machines/linux/planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub [zaplanowanej konserwacji dla maszyn wirtualnych Azure Windows](../articles/virtual-machines/windows/planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) szczegółowe informacje o zaplanowanej konserwacji dla maszyn wirtualnych platformy Azure.

## <a name="for-multi-instance-configuration"></a>Mająca wiele wystąpień konfiguracji
Możesz wybrać czas hello zaplanowanej konserwacji ma wpływ na maszyn wirtualnych wdrożonych w konfiguracji zestawu dostępności przez usunięcie tych maszyn wirtualnych z zestawów dostępności.

1. Zostanie wysłana wiadomość e-mail tooyou siedmiu dni przed hello planowanych konserwacji tooyour maszyn wirtualnych w konfiguracji wielu wystąpień. Hello subskrypcji identyfikatorów i nazw hello wpływ na wiele wystąpień w maszynach wirtualnych są uwzględniane w hello treść wiadomości e-mail hello.
2. Te siedem dni, można wybrać hello swoich wystąpień są aktualizowane przez usunięcie wielu wystąpień maszyn wirtualnych w tym regionie z ich zestawu dostępności. Ta zmiana w konfiguracji powoduje ponowne uruchomienie komputera, jako hello maszyny wirtualnej jest przenoszona z jednego hosta fizycznego, przeznaczony dla konserwacji, tooanother hosta fizycznego, który nie jest przeznaczone do obsługi.
3. Możesz usunąć hello maszyny Wirtualnej z jego zestawem dostępności w hello portalu Azure.

   1. W portalu hello wybierz hello tooremove maszyny Wirtualnej z hello zestawu dostępności.  

   2. W obszarze **ustawienia**, kliknij przycisk **zestawu dostępności**.

      ![Wybór zestawu dostępności](./media/virtual-machines-planned-maintenance-schedule/availabilitysetselection.png)

   3. W funkcji dostępność hello ustawić menu rozwijane, wybierz opcję "Nie jest częścią zestawu dostępności."

      ![Usuń ze zbioru](./media/virtual-machines-planned-maintenance-schedule/availabilitysetwarning.png)

   4. U góry hello kliknij **zapisać**. Kliknij przycisk **tak** tooacknowledge, który ta akcja powoduje ponowne uruchomienie hello maszyny Wirtualnej.

   >[!TIP]
   >Wystąpienie toomulti hello maszyny Wirtualnej można zmienić później, wybierając jedną z wymienionych hello zestawów dostępności.

4. Maszyny wirtualne, usuwane z zestawów dostępności hostów przeniesionego wystąpienia tooSingle i nie są aktualizowane podczas hello planowanych konserwacji tooAvailability Ustaw konfiguracje.
5. Po zakończeniu hello aktualizacji tooAvailability ustawić maszyn wirtualnych (zgodnie z tooschedule opisane w hello oryginalnej wiadomości e-mail), należy dodać hello maszyn wirtualnych do ich zestawów dostępności. Staje się częścią zestawu dostępności jako występująca ponownie konfiguruje hello maszyn wirtualnych i powoduje ponowne uruchomienie komputera. Zwykle po wykonaniu wszystkich aktualizacji wielu wystąpień w środowisku Azure całego hello następuje konserwacji jednego wystąpienia.

Usuwanie maszyny Wirtualnej z zestawu dostępności może być również uzyskany przy użyciu programu Azure PowerShell:

```
Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Remove-AzureAvailabilitySet | Update-AzureVM
```

## <a name="for-single-instance-configuration"></a>Dla jednego wystąpienia konfiguracji
Możesz wybrać czas hello zaplanowanej konserwacji ma wpływ na możesz maszyn wirtualnych w konfiguracji jednego wystąpienia przez dodanie tych maszyn wirtualnych do zestawów dostępności.

Krok po kroku

1. Zostanie wysłana wiadomość e-mail tooyou siedmiu dni przed hello planowanych konserwacji tooVMs w konfiguracji jednego wystąpienia. Hello identyfikatorów subskrypcji, a nazwy maszyn wirtualnych z jednego wystąpienia hello, których to dotyczy znajdują się w treści hello hello poczty e-mail.
2. Te siedem dni, można wybrać hello wystąpienia przez dodanie sieci maszyn wirtualnych z jednego wystąpienia tooan dostępności jest uruchamiany ponownie ustawiony w tym samym regionie. Ta zmiana w konfiguracji powoduje ponowne uruchomienie komputera, jako hello maszyny wirtualnej jest przenoszona z jednego hosta fizycznego, przeznaczony dla konserwacji, tooanother hosta fizycznego, który nie jest przeznaczone do obsługi.
3. Postępuj zgodnie z instrukcjami tutaj tooadd istniejących maszyn wirtualnych do zestawów dostępności za pomocą hello portalu Azure i programu Azure PowerShell. (Zobacz przykład programu Azure PowerShell hello, który obejmuje następujące kroki.)
4. Gdy te maszyny wirtualne są konfigurowane jako występująca, są wykluczone z hello planowanych konserwacji wystąpienia tooSingle maszyn wirtualnych.
5. Po zakończeniu hello jednym wystąpieniu maszyny Wirtualnej aktualizacji (zgodnie z tooschedule w hello oryginalnej wiadomości e-mail), można zwrócić wystąpienia toosingle hello maszyn wirtualnych przez usunięcie hello maszyn wirtualnych z ich zestawów dostępności.

Dodawanie tooan maszyna wirtualna również zestaw dostępności można osiągnąć za pomocą programu Azure PowerShell:

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

<!--Anchors-->



<!--Link references-->
[Virtual Machines Manage Availability]: virtual-machines-windows-tutorial.md
[Understand planned versus unplanned maintenance]: virtual-machines-manage-availability.md#Understand-planned-versus-unplanned-maintenance/
