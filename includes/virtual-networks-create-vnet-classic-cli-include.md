## <a name="how-toocreate-a-classic-vnet-using-azure-cli"></a>Jak toocreate klasycznej sieci wirtualnej przy użyciu wiersza polecenia platformy Azure
Można użyć hello Azure CLI toomanage zasobów platformy Azure z wiersza polecenia hello z dowolnego komputera z systemem Windows, Linux lub OS x. toocreate sieć wirtualną przy użyciu hello Azure CLI, wykonaj poniższe kroki hello.

1. Jeśli po raz pierwszy używasz interfejsu wiersza polecenia Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../articles/cli-install-nodejs.md) i wykonaj instrukcje hello zapasowej punktu toohello, gdzie należy wybrać konto platformy Azure i subskrypcji.
2. Uruchom hello **Utwórz sieć wirtualną sieć platformy azure** polecenia toocreate sieć wirtualną i podsieć, jak pokazano poniżej. Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane.
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    Oczekiwane dane wyjściowe:
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * **--vnet**. Nazwa toobe sieci wirtualnej hello utworzony. W naszym scenariuszu jest to *TestVNet*
   * **-e (lub--przestrzeni adresowej)**. Przestrzeń adresowa sieci wirtualnej. W naszym scenariuszu *192.168.0.0*
   * **-i (lub - cidr)**. Maska sieci w formacie CIDR. W naszym scenariuszu *16*.
   * **-n (lub--nazwy podsieci**). Nazwa hello pierwszej podsieci. W naszym scenariuszu jest to *FrontEnd*.
   * **-p (lub--podsieci start-ip)**. Początkowy adres IP dla podsieci lub przestrzeni adresowej podsieci. W naszym scenariuszu *192.168.1.0*.
   * **-r (lub--podsieci cidr)**. Maska sieci w formacie CIDR podsieci. W naszym scenariuszu *24*.
   * **-l (lub --location)**. Region platformy Azure, w której zostanie utworzona hello sieci wirtualnej. W naszym scenariuszu *środkowe stany USA*.
3. Uruchom hello **Utwórz podsieć sieci wirtualnej platformy azure sieci** toocreate polecenia podsieci, jak pokazano poniżej. Lista Hello wyświetlana po danych wyjściowych hello wyjaśniono hello parametry używane.
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    Oto hello oczekiwane dane wyjściowe polecenia hello powyżej:
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * **-t (lub--vnet-name**. Nazwa sieci wirtualnej, w którym zostanie utworzona podsieć hello hello. W naszym scenariuszu jest to *TestVNet*.
   * **-n (lub --name)**. Nazwa nowej podsieci hello. W naszym scenariuszu *zaplecza*.
   * **-a (lub --address-prefix)**. Blok CIDR podsieci. Cztery naszym scenariuszu *192.168.2.0/24*.
4. Uruchom hello **Pokaż sieci wirtualnej sieci platformy azure** polecenia tooview właściwości hello hello nowej sieci wirtualnej, jak pokazano poniżej.
   
            azure network vnet show
   
    Oto hello oczekiwane dane wyjściowe polecenia hello powyżej:
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

