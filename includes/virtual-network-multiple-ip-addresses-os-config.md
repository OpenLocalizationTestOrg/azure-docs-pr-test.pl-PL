## <a name="os-config"></a>Adresy IP do systemu operacyjnego maszyny wirtualnej

Z utworzoną maszyną wirtualną można nawiązywać połączenie oraz logować się na niej za pomocą wielu prywatnych adresów IP. Wszystkie prywatne adresy IP (w tym podstawowy) dodane do maszyny wirtualnej muszą zostać wprowadzone ręcznie. Wykonaj poniższe kroki w odpowiednim systemie operacyjnym maszyny wirtualnej:

### <a name="windows"></a>Windows

1. W wierszu polecenia wpisz *ipconfig /all*.  Wyświetlany jest tylko *podstawowy* prywatny adres IP (przypisywany za pośrednictwem protokołu DHCP).
2. Wpisz polecenie *ncpa.cpl* w wierszu polecenia, aby otworzyć okno **Połączenia sieciowe**.
3. Otwórz właściwości odpowiedniej karty: **Połączenie lokalne**.
4. Kliknij dwukrotnie Protokół internetowy w wersji 4 (IPv4).
5. Wybierz pozycję **Użyj następującego adresu IP** i wprowadź następujące wartości:

    * **Adres IP**: wprowadź *podstawowy* prywatny adres IP.
    * **Maska podsieci**: ustaw na podstawie swojej sieci. Na przykład jeśli podsieć jest podsiecią typu /24, wprowadź maską podsieci 255.255.255.0.
    * **Brama domyślna**: pierwszy adres IP w podsieci. Jeśli podsieć jest typu 10.0.0.0/24, adresem IP bramy będzie 10.0.0.1.
    * Kliknij pozycję **Użyj następujących adresów serwerów DNS** i wprowadź następujące wartości:
        * **Preferowany serwer DNS**: jeśli nie używasz własnego serwera DNS, wprowadź adres 168.63.129.16.  Jeśli używasz własnego serwera DNS, wprowadź jego adres IP.
    * Kliknij przycisk **Zaawansowane** i dodaj dodatkowe adresy IP. Dodaj wszystkie pomocnicze prywatne adresy IP wymienione w kroku 8 do karty sieciowej z tą samą podsiecią, jaką określono dla podstawowego adresu IP.
        >[!WARNING] 
        >Jeśli nie wykonasz poprawnie powyższych czynności, możesz utracić łączność z maszyną wirtualną. Przed kontynuowaniem upewnij się, że informacje wprowadzone w kroku 5 są dokładne.

    * Kliknij przycisk **OK**, aby zamknąć ustawienia TCP/IP, a następnie kliknij ponownie przycisk **OK**, aby zamknąć ustawienia karty. Połączenie RDP zostanie ponownie nawiązane.

6. W wierszu polecenia wpisz *ipconfig /all*. Zostaną wyświetlone wszystkie dodane adresy IP, a protokół DHCP będzie wyłączony.
7. Skonfiguruj system Windows do użycia jako podstawowy adres IP prywatnego adresu IP w konfiguracji podstawowego adresu IP na platformie Azure dla systemu Windows. Zobacz [dostęp do Internetu nie z maszyny Wirtualnej systemu Windows Azure, który ma wiele adresów IP](https://support.microsoft.com/help/4040882/no-internet-access-from-azure-windows-vm-that-has-multiple-ip-addresse) szczegółowe informacje. 


### <a name="validation-windows"></a>Walidacja (Windows)

Aby upewnić się, że będziesz mieć możliwość nawiązania połączenia z Internetem przy użyciu konfiguracji pomocniczych adresów IP za pośrednictwem skojarzonego z nią publicznego adresu IP, po poprawnym dodaniu konfiguracji za pomocą powyższych kroków użyj następującego polecenia:

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
>W przypadku dodatkowej konfiguracji IP można tylko zbadać poleceniem ping z Internetem Jeśli konfiguracji ma publiczny adres IP skojarzone z nim. Dla podstawowej konfiguracji adresów IP publiczny adres IP nie jest wymagany na polecenie ping do Internetu.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)

1. Otwórz okno terminalu.
2. Upewnij się, że jesteś zalogowany jako użytkownik root. Jeśli nie, wprowadź następujące polecenie:

    ```bash
    sudo -i
    ```

3. Zaktualizuj plik konfiguracji interfejsu sieciowego (przyjęto, że jest to „eth0”).

    * Zachowaj istniejący element wiersza dla protokołu dhcp. Podstawowy adres IP pozostanie skonfigurowany tak jak poprzednio.
    * Dodaj konfigurację dla dodatkowego statycznego adresu IP za pomocą następujących poleceń:

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    Powinien zostać wyświetlony plik cfg.
4. Otwórz ten plik. Na końcu tego pliku powinny znajdować się następujące wiersze:

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. Po wierszach, które istnieją w tym pliku, dodaj następujące wiersze:

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. Zapisz plik za pomocą następującego polecenia:

    ```bash
    :wq
    ```

7. Zresetuj interfejs sieciowy przy użyciu następującego polecenia:

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > Jeśli korzystasz z połączenia zdalnego, uruchom w jednym wierszu zarówno polecenie ifdown, jak i ifup.
    >

8. Za pomocą następującego polecenia sprawdź, czy adres IP został dodany do interfejsu sieciowego:

    ```bash
    ip addr list eth0
    ```

    Dodany adres IP powinien być widoczny na liście.

### <a name="linux-redhat-centos-and-others"></a>Linux (Redhat, CentOS i inne)

1. Otwórz okno terminalu.
2. Upewnij się, że jesteś zalogowany jako użytkownik root. Jeśli nie, wprowadź następujące polecenie:

    ```bash
    sudo -i
    ```

3. Wprowadź hasło i postępuj zgodnie z wyświetlanymi instrukcjami. Jeśli jesteś zalogowany jako użytkownik root, przejdź do folderu za skryptami sieciowymi za pomocą następującego polecenia:

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. Użyj następującego polecenia, aby wyświetlić listę powiązanych plików ifcfg:

    ```bash
    ls ifcfg-*
    ```

    Jeden z plików powinien mieć nazwę *ifcfg-eth0*.

5. Aby dodać adres IP, utwórz dla niego plik konfiguracji zgodnie z poniższym wzorem. Pamiętaj, że dla każdej konfiguracji IP powinien zostać utworzony jeden plik.

    ```bash
    touch ifcfg-eth0:0
    ```

6. Otwórz plik *ifcfg-eth0:0* za pomocą następującego polecenia:

    ```bash
    vi ifcfg-eth0:0
    ```

7. Dodaj zawartość do pliku (w tym przypadku *eth0:0*) przy użyciu następującego polecenia. Pamiętaj, aby zaktualizować informacje na podstawie swojego adresu IP.

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. Zapisz plik, korzystając z następującego polecenia:

    ```bash
    :wq
    ```

9. Uruchom ponownie usługi sieciowe i upewnij się, że zmiany zostały pomyślnie wprowadzone, uruchamiając następujące polecenia:

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    Dodany adres IP (*eth0:0*) powinien być widoczny na zwróconej liście.

### <a name="validation-linux"></a>Walidacja (Linux)

Aby upewnić się, że będziesz mieć możliwość nawiązania połączenia z Internetem przy użyciu konfiguracji pomocniczego adresu IP za pośrednictwem skojarzonego z nią publicznego adresu IP, użyj następującego polecenia:

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
>W przypadku dodatkowej konfiguracji IP można tylko zbadać poleceniem ping z Internetem Jeśli konfiguracji ma publiczny adres IP skojarzone z nim. Dla podstawowej konfiguracji adresów IP publiczny adres IP nie jest wymagany na polecenie ping do Internetu.

W przypadku maszyn wirtualnych z systemem Linux podczas próby walidacji łączności wychodzącej z pomocniczej karty sieciowej może być konieczne dodanie odpowiednich tras. Istnieje wiele sposobów, aby to zrobić. Zapoznaj się z odpowiednią dokumentacją dla swojej dystrybucji systemu. Oto jedna z metod wykonania tej czynności:

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- Pamiętaj, aby zamienić:
    - wartość **10.0.0.5** na prywatny adres IP, który ma skojarzony ze sobą publiczny adres IP;
    - wartość **10.0.0.1** na bramę domyślną;
    - wartość **eth2** na nazwę pomocniczej karty sieciowej.
