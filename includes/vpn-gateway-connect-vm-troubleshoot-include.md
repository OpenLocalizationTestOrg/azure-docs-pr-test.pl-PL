Jeśli występują problemy z połączeniem tooa maszyny wirtualnej za pośrednictwem połączenia sieci VPN, sprawdź następujące hello:

- Sprawdź, czy połączenie sieci VPN zostało pomyślnie nawiązane.
- Sprawdź, czy łączysz toohello prywatnego adresu IP dla hello maszyny Wirtualnej.
- Jeśli łączysz toohello maszyny Wirtualnej przy użyciu prywatnego adresu IP hello adresów, ale nie hello nazwę komputera, Sprawdź poprawnie skonfigurowane DNS. Aby uzyskać więcej informacji na temat tego, jak działa rozpoznawanie nazw dla maszyn wirtualnych, zobacz [Name Resolution for VMs](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) (Rozpoznawanie nazw dla maszyn wirtualnych).

Podczas łączenia za pośrednictwem punkt-lokacja, sprawdź następujące dodatkowe elementy hello:

- Użyj "ipconfig" hello toocheck adres IPv4 przypisany karty Ethernet toohello na komputerze hello, z którym się łączysz. Jeśli adres IP hello jest w zakresie adresów hello hello łączysz się z sieci wirtualnej lub w zakresie adresów hello Twojej VPNClientAddressPool, to tooas określonego nakładających się przestrzeni adresowej. Przestrzeń adresowa nakłada się w ten sposób, hello ruch sieciowy będzie niższa niż Azure, pozostaje on objęty na powitania sieci lokalnej.
- Sprawdź, czy w tej konfiguracji pakietu klienta VPN hello został wygenerowany po adresów IP serwerów DNS hello zostały określone dla hello sieci wirtualnej. Zaktualizowano adresy IP serwerów DNS hello Generowanie i zainstalować nowy pakiet konfiguracji klienta sieci VPN.

Aby uzyskać więcej informacji dotyczących rozwiązywania problemów z połączenia RDP, zobacz [tooa połączeń pulpitu zdalnego Rozwiązywanie problemów z maszyny Wirtualnej](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).
