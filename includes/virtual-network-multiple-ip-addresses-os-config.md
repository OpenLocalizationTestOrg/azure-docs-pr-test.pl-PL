## <a name="os-config"></a>Dodaj system operacyjny maszyny Wirtualnej tooa adresów IP

Połącz i logowania tooa maszyna wirtualna utworzona z wielu prywatnych adresów IP. Należy ręcznie dodać wszystkie hello prywatnych adresów IP (takie jak podstawowy hello) dodania toohello maszyny Wirtualnej. Wykonaj następujące kroki dla systemu operacyjnego maszyny Wirtualnej hello:

### <a name="windows"></a>Windows

1. W wierszu polecenia wpisz *ipconfig /all*.  Wyświetlane są tylko hello *głównej* prywatnego adresu IP (za pośrednictwem protokołu DHCP).
2. Typ *ncpa.cpl* w hello wiersza polecenia tooopen hello **połączenia sieciowe** okna.
3. Otwórz właściwości hello odpowiednie karty hello: **połączenie lokalne**.
4. Kliknij dwukrotnie Protokół internetowy w wersji 4 (IPv4).
5. Wybierz **hello Użyj następującego adresu IP** , a następnie wprowadź hello następujące wartości:

    * **Adres IP**: Wprowadź hello *głównej* prywatnego adresu IP
    * **Maska podsieci**: ustaw na podstawie swojej sieci. Na przykład jeśli hello podsieci jest prefiksie/24 podsieci, a następnie hello podsieci 255.255.255.0 jest maski.
    * **Brama domyślna**: hello pierwszy adres IP w podsieci hello. Jeśli podsieć 10.0.0.0/24, adres IP bramy hello jest 10.0.0.1.
    * Kliknij przycisk **hello Użyj następujących adresów serwerów DNS** , a następnie wprowadź hello następujące wartości:
        * **Preferowany serwer DNS**: jeśli nie używasz własnego serwera DNS, wprowadź adres 168.63.129.16.  Jeśli używasz serwera DNS wprowadź adres IP hello serwera.
    * Kliknij przycisk hello **zaawansowane** przycisk i dodawania dodatkowych adresów IP. Dodaj wszystkie hello dodatkowej prywatnych adresów IP w kroku 8 toohello kart interfejsu Sieciowego z tej samej podsieci, określony dla podstawowego adresu IP hello hello na liście.
        >[!WARNING] 
        >Nie wykonuj poprawnie hello kroków opisanych powyżej, może spowodować utratę łączności tooyour maszyny Wirtualnej. Upewnij się, że informacje hello wprowadzona w kroku 5 są prawidłowe przed kontynuowaniem.

    * Kliknij przycisk **OK** tooclose się ustawienia hello TCP/IP, a następnie **OK** ponownie tooclose hello karty Ustawienia. Połączenie RDP zostanie ponownie nawiązane.

6. W wierszu polecenia wpisz *ipconfig /all*. Zostaną wyświetlone wszystkie dodane adresy IP, a protokół DHCP będzie wyłączony.


### <a name="validation-windows"></a>Walidacja (Windows)

tooensure toohello tooconnect stanie, przez internet z konfiguracji IP dodatkowej za pośrednictwem publicznego adresu IP skojarzonego, po dodaniu poprawnie za pomocą hello kroki opisane powyżej, użyj następującego polecenia hello:

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
>Dodatkowej konfiguracji adresu IP można tylko ping toohello Internet, jeśli konfiguracja hello ma publiczny adres IP skojarzone z nim. W przypadku podstawowej konfiguracji IP publiczny adres IP nie jest wymagane tooping toohello Internet.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)

1. Otwórz okno terminalu.
2. Upewnij się, że jesteś hello użytkownika głównego. Jeśli nie masz, wprowadź hello następujące polecenie:

    ```bash
    sudo -i
    ```

3. Aktualizuj plik konfiguracji hello hello interfejsu sieciowego (przy założeniu "eth0").

    * Zachowaj hello istniejący element wiersza dla protokołu dhcp. podstawowy adres IP Hello pozostaje skonfigurowany zgodnie z wcześniej był.
    * Dodaj konfigurację dodatkowe statyczny adres IP z hello następującego polecenia:

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    Powinien zostać wyświetlony plik cfg.
4. Witaj Otwórz plik. Powinny pojawić się następujące wiersze na końcu pliku hello hello hello:

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. Dodaj następujące wiersze po hello wierszy, które istnieją w tym pliku hello:

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. Zapisz plik hello przy użyciu hello następujące polecenie:

    ```bash
    :wq
    ```

7. Resetuj hello interfejsu sieciowego z hello następujące polecenie:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > Uruchom zarówno ifdown i ifup w hello sam wiersz, jeśli przy użyciu połączenia zdalnego.
    >

8. Sprawdź, czy hello jest dodawany adres IP interfejsu sieciowego toohello z hello następujące polecenie:

    ```bash
    ip addr list eth0
    ```

    Powinna zostać wyświetlona zostanie dodany jako część hello listy adresów IP hello.

### <a name="linux-redhat-centos-and-others"></a>Linux (Redhat, CentOS i inne)

1. Otwórz okno terminalu.
2. Upewnij się, że jesteś hello użytkownika głównego. Jeśli nie masz, wprowadź hello następujące polecenie:

    ```bash
    sudo -i
    ```

3. Wprowadź hasło i postępuj zgodnie z wyświetlanymi instrukcjami. Po przejściu hello głównego użytkownika, przejdź folder skryptów sieci toohello z hello następujące polecenie:

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. Lista hello powiązane pliki ifcfg za pomocą następującego polecenia hello:

    ```bash
    ls ifcfg-*
    ```

    Powinny pojawić się *ifcfg eth0* jako jednego z plików hello.

5. tooadd adresu IP dla niego utworzyć plik konfiguracji, jak pokazano poniżej. Pamiętaj, że dla każdej konfiguracji IP powinien zostać utworzony jeden plik.

    ```bash
    touch ifcfg-eth0:0
    ```

6. Otwórz hello *ifcfg-eth0:0* pliku z hello następujące polecenie:

    ```bash
    vi ifcfg-eth0:0
    ```

7. Dodaj plik zawartości toohello *eth0:0* w tym przypadku z hello następujące polecenia. Informacje tooupdate się opierać się na adres IP.

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. Zapisz plik hello z hello następujące polecenie:

    ```bash
    :wq
    ```

9. Uruchom ponownie usługi sieciowe hello i upewnij się, że zmiany hello zostały wykonane pomyślnie, uruchamiając następujące polecenia hello:

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    Powinna zostać wyświetlona zostanie dodany, adresów IP hello *eth0:0*, na liście hello zwracane.

### <a name="validation-linux"></a>Walidacja (Linux)

tooensure są toohello tooconnect stanie Internetem dodatkowej konfiguracji IP za pośrednictwem publicznego adresu IP hello skojarzone go, skorzystaj z hello następujące polecenie:

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
>Dodatkowej konfiguracji adresu IP można tylko ping toohello Internet, jeśli konfiguracja hello ma publiczny adres IP skojarzone z nim. W przypadku podstawowej konfiguracji IP publiczny adres IP nie jest wymagane tooping toohello Internet.

Dla maszyn wirtualnych systemu Linux, podczas próby toovalidate łączność wychodząca z pomocniczego karty Sieciowej może być konieczne tooadd odpowiednie trasy. Istnieje wiele sposobów toodo to. Zapoznaj się z odpowiednią dokumentacją dla swojej dystrybucji systemu. następujące Hello jest jeden tooaccomplish metody to:

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- Należy się tooreplace:
    - **10.0.0.5** z prywatnego adresu IP hello adres, który ma publicznego adresu IP adres skojarzony tooit
    - **10.0.0.1** tooyour brama domyślna
    - **eth2** nazwa toohello Twojego dodatkowej karty sieciowej
