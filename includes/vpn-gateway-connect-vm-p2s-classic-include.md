Możesz połączyć tooa maszyny Wirtualnej, tworząc tooyour Podłączanie pulpitu zdalnego maszyny Wirtualnej wdrożonej tooyour sieci wirtualnej. Hello najlepsze sposób tooinitially Sprawdź, czy możesz połączyć tooyour maszyna wirtualna jest tooconnect przez adres przy użyciu jego prywatnego adresu IP, zamiast nazwy komputera. W ten sposób testowania toosee Jeśli można połączyć, nie określa, czy rozpoznawanie nazw jest skonfigurowany prawidłowo. 

1. Zlokalizuj hello prywatnego adresu IP dla maszyny Wirtualnej. Hello prywatnego adresu IP maszyny wirtualnej można znaleźć, analizując albo właściwości hello hello maszyny Wirtualnej w portalu Azure hello lub przy użyciu programu PowerShell.
2. Sprawdź, czy są połączone tooyour sieci wirtualnej za pomocą hello punkt-lokacja sieci VPN połączenia. 
3. Otwórz Podłączanie pulpitu zdalnego, wpisując "RDP" lub "Podłączanie pulpitu zdalnego" w polu wyszukiwania hello na powitania zadań, a następnie wybierz Podłączanie pulpitu zdalnego. Można również otworzyć w programie PowerShell przy użyciu polecenia "mstsc" hello Podłączanie pulpitu zdalnego. 
3. Podłączanie pulpitu zdalnego wprowadź hello prywatnego adresu IP hello maszyny Wirtualnej. Możesz kliknij opcję "Pokaż opcje" tooadjust dodatkowe ustawienia, a następnie połącz.

### <a name="tootroubleshoot-an-rdp-connection-tooa-vm"></a>tootroubleshoot tooa połączenia RDP maszyny Wirtualnej

Jeśli występują problemy z połączeniem tooa maszyny wirtualnej za pośrednictwem połączenia sieci VPN, istnieje kilka rzeczy, które można sprawdzić. Aby uzyskać więcej informacji o rozwiązywaniu problemów, zobacz [tooa połączeń pulpitu zdalnego Rozwiązywanie problemów z maszyny Wirtualnej](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).

- Sprawdź, czy połączenie sieci VPN zostało pomyślnie nawiązane.
- Sprawdź, czy łączysz toohello prywatnego adresu IP dla hello maszyny Wirtualnej.
- Użyj "ipconfig" hello toocheck adres IPv4 przypisany karty Ethernet toohello na komputerze hello, z którym się łączysz. Jeśli adres IP hello jest w zakresie adresów hello hello łączysz się z sieci wirtualnej lub w zakresie adresów hello Twojej VPNClientAddressPool, to tooas określonego nakładających się przestrzeni adresowej. Przestrzeń adresowa nakłada się w ten sposób, hello ruch sieciowy będzie niższa niż Azure, pozostaje on objęty na powitania sieci lokalnej.
- Jeśli łączysz toohello maszyny Wirtualnej przy użyciu prywatnego adresu IP hello adresów, ale nie hello nazwę komputera, Sprawdź poprawnie skonfigurowane DNS. Aby uzyskać więcej informacji na temat tego, jak działa rozpoznawanie nazw dla maszyn wirtualnych, zobacz [Name Resolution for VMs](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) (Rozpoznawanie nazw dla maszyn wirtualnych).
- Sprawdź, czy w tej konfiguracji pakietu klienta VPN hello został wygenerowany po adresów IP serwerów DNS hello zostały określone dla hello sieci wirtualnej. Zaktualizowano adresy IP serwerów DNS hello Generowanie i zainstalować nowy pakiet konfiguracji klienta sieci VPN.
