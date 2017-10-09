Możesz połączyć tooa maszyny Wirtualnej, tworząc tooyour Podłączanie pulpitu zdalnego maszyny Wirtualnej wdrożonej tooyour sieci wirtualnej. Hello najlepsze sposób tooinitially Sprawdź, czy możesz połączyć tooyour maszyna wirtualna jest tooconnect przez adres przy użyciu jego prywatnego adresu IP, zamiast nazwy komputera. W ten sposób testowania toosee Jeśli można połączyć, nie określa, czy rozpoznawanie nazw jest skonfigurowany prawidłowo.

1. Zlokalizuj hello prywatnego adresu IP. Witaj prywatnego adresu IP maszyny wirtualnej można znaleźć na wiele sposobów. Poniżej zostanie przedstawiony kroki hello hello portalu Azure i programu PowerShell.

  - Portal Azure — zlokalizować maszyny wirtualnej w hello portalu Azure. Wyświetl właściwości hello hello maszyny Wirtualnej. znajduje się Hello prywatnego adresu IP.

  - PowerShell — Użyj hello przykład tooview listę maszyn wirtualnych i prywatnych adresów IP z grupy zasobów. W tym przykładzie nie wymagają toomodify przed jego użyciem.

    ```powershell
    $VMs = Get-AzureRmVM
    $Nics = Get-AzureRmNetworkInterface | Where VirtualMachine -ne $null

    foreach($Nic in $Nics)
    {
      $VM = $VMs | Where-Object -Property Id -eq $Nic.VirtualMachine.Id
      $Prv = $Nic.IpConfigurations | Select-Object -ExpandProperty PrivateIpAddress
      $Alloc = $Nic.IpConfigurations | Select-Object -ExpandProperty PrivateIpAllocationMethod
      Write-Output "$($VM.Name): $Prv,$Alloc"
    }
    ```

2. Sprawdź, czy są połączone tooyour sieci wirtualnej przy użyciu hello połączenia sieci VPN.
3. Otwórz **Podłączanie pulpitu zdalnego** , wpisując "RDP" lub "Podłączanie pulpitu zdalnego" w polu wyszukiwania hello na powitania zadań, a następnie wybierz Podłączanie pulpitu zdalnego. Można również otworzyć w programie PowerShell przy użyciu polecenia "mstsc" hello Podłączanie pulpitu zdalnego. 
4. Podłączanie pulpitu zdalnego wprowadź hello prywatnego adresu IP hello maszyny Wirtualnej. Możesz kliknij opcję "Pokaż opcje" tooadjust dodatkowe ustawienia, a następnie połącz.

### <a name="tootroubleshoot-an-rdp-connection-tooa-vm"></a>tootroubleshoot tooa połączenia RDP maszyny Wirtualnej

Jeśli występują problemy z połączeniem tooa maszyny wirtualnej za pośrednictwem połączenia sieci VPN, sprawdź następujące hello:

- Sprawdź, czy połączenie sieci VPN zostało pomyślnie nawiązane.
- Sprawdź, czy łączysz toohello prywatnego adresu IP dla hello maszyny Wirtualnej.
- Jeśli łączysz toohello maszyny Wirtualnej przy użyciu prywatnego adresu IP hello adresów, ale nie hello nazwę komputera, Sprawdź poprawnie skonfigurowane DNS. Aby uzyskać więcej informacji na temat tego, jak działa rozpoznawanie nazw dla maszyn wirtualnych, zobacz [Name Resolution for VMs](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) (Rozpoznawanie nazw dla maszyn wirtualnych).
- Aby uzyskać więcej informacji na temat połączeń protokołu RDP, zobacz [tooa połączeń pulpitu zdalnego Rozwiązywanie problemów z maszyny Wirtualnej](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).
