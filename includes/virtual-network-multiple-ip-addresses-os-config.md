## <span data-ttu-id="29826-101"><a name="os-config"></a>Dodaj system operacyjny maszyny Wirtualnej tooa adresów IP</span><span class="sxs-lookup"><span data-stu-id="29826-101"><a name="os-config"></a>Add IP addresses tooa VM operating system</span></span>

<span data-ttu-id="29826-102">Połącz i logowania tooa maszyna wirtualna utworzona z wielu prywatnych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="29826-102">Connect and login tooa VM you created with multiple private IP addresses.</span></span> <span data-ttu-id="29826-103">Należy ręcznie dodać wszystkie hello prywatnych adresów IP (takie jak podstawowy hello) dodania toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="29826-103">You must manually add all hello private IP addresses (including hello primary) that you added toohello VM.</span></span> <span data-ttu-id="29826-104">Wykonaj następujące kroki dla systemu operacyjnego maszyny Wirtualnej hello:</span><span class="sxs-lookup"><span data-stu-id="29826-104">Complete hello following steps for your VM operating system:</span></span>

### <a name="windows"></a><span data-ttu-id="29826-105">Windows</span><span class="sxs-lookup"><span data-stu-id="29826-105">Windows</span></span>

1. <span data-ttu-id="29826-106">W wierszu polecenia wpisz *ipconfig /all*.</span><span class="sxs-lookup"><span data-stu-id="29826-106">From a command prompt, type *ipconfig /all*.</span></span>  <span data-ttu-id="29826-107">Wyświetlane są tylko hello *głównej* prywatnego adresu IP (za pośrednictwem protokołu DHCP).</span><span class="sxs-lookup"><span data-stu-id="29826-107">You only see hello *Primary* private IP address (through DHCP).</span></span>
2. <span data-ttu-id="29826-108">Typ *ncpa.cpl* w hello wiersza polecenia tooopen hello **połączenia sieciowe** okna.</span><span class="sxs-lookup"><span data-stu-id="29826-108">Type *ncpa.cpl* in hello command prompt tooopen hello **Network connections** window.</span></span>
3. <span data-ttu-id="29826-109">Otwórz właściwości hello odpowiednie karty hello: **połączenie lokalne**.</span><span class="sxs-lookup"><span data-stu-id="29826-109">Open hello properties for hello appropriate adapter: **Local Area Connection**.</span></span>
4. <span data-ttu-id="29826-110">Kliknij dwukrotnie Protokół internetowy w wersji 4 (IPv4).</span><span class="sxs-lookup"><span data-stu-id="29826-110">Double-click Internet Protocol version 4 (IPv4).</span></span>
5. <span data-ttu-id="29826-111">Wybierz **hello Użyj następującego adresu IP** , a następnie wprowadź hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="29826-111">Select **Use hello following IP address** and enter hello following values:</span></span>

    * <span data-ttu-id="29826-112">**Adres IP**: Wprowadź hello *głównej* prywatnego adresu IP</span><span class="sxs-lookup"><span data-stu-id="29826-112">**IP address**: Enter hello *Primary* private IP address</span></span>
    * <span data-ttu-id="29826-113">**Maska podsieci**: ustaw na podstawie swojej sieci.</span><span class="sxs-lookup"><span data-stu-id="29826-113">**Subnet mask**: Set based on your subnet.</span></span> <span data-ttu-id="29826-114">Na przykład jeśli hello podsieci jest prefiksie/24 podsieci, a następnie hello podsieci 255.255.255.0 jest maski.</span><span class="sxs-lookup"><span data-stu-id="29826-114">For example, if hello subnet is a /24 subnet then hello subnet mask is 255.255.255.0.</span></span>
    * <span data-ttu-id="29826-115">**Brama domyślna**: hello pierwszy adres IP w podsieci hello.</span><span class="sxs-lookup"><span data-stu-id="29826-115">**Default gateway**: hello first IP address in hello subnet.</span></span> <span data-ttu-id="29826-116">Jeśli podsieć 10.0.0.0/24, adres IP bramy hello jest 10.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="29826-116">If your subnet is 10.0.0.0/24, then hello gateway IP address is 10.0.0.1.</span></span>
    * <span data-ttu-id="29826-117">Kliknij przycisk **hello Użyj następujących adresów serwerów DNS** , a następnie wprowadź hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="29826-117">Click **Use hello following DNS server addresses** and enter hello following values:</span></span>
        * <span data-ttu-id="29826-118">**Preferowany serwer DNS**: jeśli nie używasz własnego serwera DNS, wprowadź adres 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="29826-118">**Preferred DNS server**: If you are not using your own DNS server, enter 168.63.129.16.</span></span>  <span data-ttu-id="29826-119">Jeśli używasz serwera DNS wprowadź adres IP hello serwera.</span><span class="sxs-lookup"><span data-stu-id="29826-119">If you are using your own DNS server, enter hello IP address for your server.</span></span>
    * <span data-ttu-id="29826-120">Kliknij przycisk hello **zaawansowane** przycisk i dodawania dodatkowych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="29826-120">Click hello **Advanced** button and add additional IP addresses.</span></span> <span data-ttu-id="29826-121">Dodaj wszystkie hello dodatkowej prywatnych adresów IP w kroku 8 toohello kart interfejsu Sieciowego z tej samej podsieci, określony dla podstawowego adresu IP hello hello na liście.</span><span class="sxs-lookup"><span data-stu-id="29826-121">Add each of hello secondary private IP addresses listed in step 8 toohello NIC with hello same subnet specified for hello primary IP address.</span></span>
        >[!WARNING] 
        ><span data-ttu-id="29826-122">Nie wykonuj poprawnie hello kroków opisanych powyżej, może spowodować utratę łączności tooyour maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="29826-122">If you do not follow hello steps above correctly, you may lose connectivity tooyour VM.</span></span> <span data-ttu-id="29826-123">Upewnij się, że informacje hello wprowadzona w kroku 5 są prawidłowe przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="29826-123">Ensure hello information entered for step 5 is accurate before proceeding.</span></span>

    * <span data-ttu-id="29826-124">Kliknij przycisk **OK** tooclose się ustawienia hello TCP/IP, a następnie **OK** ponownie tooclose hello karty Ustawienia.</span><span class="sxs-lookup"><span data-stu-id="29826-124">Click **OK** tooclose out hello TCP/IP settings and then **OK** again tooclose hello adapter settings.</span></span> <span data-ttu-id="29826-125">Połączenie RDP zostanie ponownie nawiązane.</span><span class="sxs-lookup"><span data-stu-id="29826-125">Your RDP connection is re-established.</span></span>

6. <span data-ttu-id="29826-126">W wierszu polecenia wpisz *ipconfig /all*.</span><span class="sxs-lookup"><span data-stu-id="29826-126">From a command prompt, type *ipconfig /all*.</span></span> <span data-ttu-id="29826-127">Zostaną wyświetlone wszystkie dodane adresy IP, a protokół DHCP będzie wyłączony.</span><span class="sxs-lookup"><span data-stu-id="29826-127">All IP addresses you added are shown and DHCP is turned off.</span></span>


### <a name="validation-windows"></a><span data-ttu-id="29826-128">Walidacja (Windows)</span><span class="sxs-lookup"><span data-stu-id="29826-128">Validation (Windows)</span></span>

<span data-ttu-id="29826-129">tooensure toohello tooconnect stanie, przez internet z konfiguracji IP dodatkowej za pośrednictwem publicznego adresu IP skojarzonego, po dodaniu poprawnie za pomocą hello kroki opisane powyżej, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="29826-129">tooensure you are able tooconnect toohello internet from your secondary IP configuration via hello public IP associated it, once you have added it correctly using steps above, use hello following command:</span></span>

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="29826-130">Dodatkowej konfiguracji adresu IP można tylko ping toohello Internet, jeśli konfiguracja hello ma publiczny adres IP skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="29826-130">For secondary IP configurations, you can only ping toohello Internet if hello configuration has a public IP address associated with it.</span></span> <span data-ttu-id="29826-131">W przypadku podstawowej konfiguracji IP publiczny adres IP nie jest wymagane tooping toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="29826-131">For primary IP configurations, a public IP address is not required tooping toohello Internet.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="29826-132">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="29826-132">Linux (Ubuntu)</span></span>

1. <span data-ttu-id="29826-133">Otwórz okno terminalu.</span><span class="sxs-lookup"><span data-stu-id="29826-133">Open a terminal window.</span></span>
2. <span data-ttu-id="29826-134">Upewnij się, że jesteś hello użytkownika głównego.</span><span class="sxs-lookup"><span data-stu-id="29826-134">Make sure you are hello root user.</span></span> <span data-ttu-id="29826-135">Jeśli nie masz, wprowadź hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="29826-135">If you are not, enter hello following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="29826-136">Aktualizuj plik konfiguracji hello hello interfejsu sieciowego (przy założeniu "eth0").</span><span class="sxs-lookup"><span data-stu-id="29826-136">Update hello configuration file of hello network interface (assuming ‘eth0’).</span></span>

    * <span data-ttu-id="29826-137">Zachowaj hello istniejący element wiersza dla protokołu dhcp.</span><span class="sxs-lookup"><span data-stu-id="29826-137">Keep hello existing line item for dhcp.</span></span> <span data-ttu-id="29826-138">podstawowy adres IP Hello pozostaje skonfigurowany zgodnie z wcześniej był.</span><span class="sxs-lookup"><span data-stu-id="29826-138">hello primary IP address remains configured as it was previously.</span></span>
    * <span data-ttu-id="29826-139">Dodaj konfigurację dodatkowe statyczny adres IP z hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="29826-139">Add a configuration for an additional static IP address with hello following commands:</span></span>

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    <span data-ttu-id="29826-140">Powinien zostać wyświetlony plik cfg.</span><span class="sxs-lookup"><span data-stu-id="29826-140">You should see a .cfg file.</span></span>
4. <span data-ttu-id="29826-141">Witaj Otwórz plik.</span><span class="sxs-lookup"><span data-stu-id="29826-141">Open hello file.</span></span> <span data-ttu-id="29826-142">Powinny pojawić się następujące wiersze na końcu pliku hello hello hello:</span><span class="sxs-lookup"><span data-stu-id="29826-142">You should see hello following lines at hello end of hello file:</span></span>

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. <span data-ttu-id="29826-143">Dodaj następujące wiersze po hello wierszy, które istnieją w tym pliku hello:</span><span class="sxs-lookup"><span data-stu-id="29826-143">Add hello following lines after hello lines that exist in this file:</span></span>

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. <span data-ttu-id="29826-144">Zapisz plik hello przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="29826-144">Save hello file by using hello following command:</span></span>

    ```bash
    :wq
    ```

7. <span data-ttu-id="29826-145">Resetuj hello interfejsu sieciowego z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="29826-145">Reset hello network interface with hello following command:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="29826-146">Uruchom zarówno ifdown i ifup w hello sam wiersz, jeśli przy użyciu połączenia zdalnego.</span><span class="sxs-lookup"><span data-stu-id="29826-146">Run both ifdown and ifup in hello same line if using a remote connection.</span></span>
    >

8. <span data-ttu-id="29826-147">Sprawdź, czy hello jest dodawany adres IP interfejsu sieciowego toohello z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="29826-147">Verify hello IP address is added toohello network interface with hello following command:</span></span>

    ```bash
    ip addr list eth0
    ```

    <span data-ttu-id="29826-148">Powinna zostać wyświetlona zostanie dodany jako część hello listy adresów IP hello.</span><span class="sxs-lookup"><span data-stu-id="29826-148">You should see hello IP address you added as part of hello list.</span></span>

### <a name="linux-redhat-centos-and-others"></a><span data-ttu-id="29826-149">Linux (Redhat, CentOS i inne)</span><span class="sxs-lookup"><span data-stu-id="29826-149">Linux (Redhat, CentOS, and others)</span></span>

1. <span data-ttu-id="29826-150">Otwórz okno terminalu.</span><span class="sxs-lookup"><span data-stu-id="29826-150">Open a terminal window.</span></span>
2. <span data-ttu-id="29826-151">Upewnij się, że jesteś hello użytkownika głównego.</span><span class="sxs-lookup"><span data-stu-id="29826-151">Make sure you are hello root user.</span></span> <span data-ttu-id="29826-152">Jeśli nie masz, wprowadź hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="29826-152">If you are not, enter hello following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="29826-153">Wprowadź hasło i postępuj zgodnie z wyświetlanymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="29826-153">Enter your password and follow instructions as prompted.</span></span> <span data-ttu-id="29826-154">Po przejściu hello głównego użytkownika, przejdź folder skryptów sieci toohello z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="29826-154">Once you are hello root user, navigate toohello network scripts folder with hello following command:</span></span>

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. <span data-ttu-id="29826-155">Lista hello powiązane pliki ifcfg za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="29826-155">List hello related ifcfg files using hello following command:</span></span>

    ```bash
    ls ifcfg-*
    ```

    <span data-ttu-id="29826-156">Powinny pojawić się *ifcfg eth0* jako jednego z plików hello.</span><span class="sxs-lookup"><span data-stu-id="29826-156">You should see *ifcfg-eth0* as one of hello files.</span></span>

5. <span data-ttu-id="29826-157">tooadd adresu IP dla niego utworzyć plik konfiguracji, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="29826-157">tooadd an IP address, create a configuration file for it as shown below.</span></span> <span data-ttu-id="29826-158">Pamiętaj, że dla każdej konfiguracji IP powinien zostać utworzony jeden plik.</span><span class="sxs-lookup"><span data-stu-id="29826-158">Note that one file must be created for each IP configuration.</span></span>

    ```bash
    touch ifcfg-eth0:0
    ```

6. <span data-ttu-id="29826-159">Otwórz hello *ifcfg-eth0:0* pliku z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="29826-159">Open hello *ifcfg-eth0:0* file with hello following command:</span></span>

    ```bash
    vi ifcfg-eth0:0
    ```

7. <span data-ttu-id="29826-160">Dodaj plik zawartości toohello *eth0:0* w tym przypadku z hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="29826-160">Add content toohello file, *eth0:0* in this case, with hello following command.</span></span> <span data-ttu-id="29826-161">Informacje tooupdate się opierać się na adres IP.</span><span class="sxs-lookup"><span data-stu-id="29826-161">Be sure tooupdate information based on your IP address.</span></span>

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. <span data-ttu-id="29826-162">Zapisz plik hello z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="29826-162">Save hello file with hello following command:</span></span>

    ```bash
    :wq
    ```

9. <span data-ttu-id="29826-163">Uruchom ponownie usługi sieciowe hello i upewnij się, że zmiany hello zostały wykonane pomyślnie, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="29826-163">Restart hello network services and make sure hello changes are successful by running hello following commands:</span></span>

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    <span data-ttu-id="29826-164">Powinna zostać wyświetlona zostanie dodany, adresów IP hello *eth0:0*, na liście hello zwracane.</span><span class="sxs-lookup"><span data-stu-id="29826-164">You should see hello IP address you added, *eth0:0*, in hello list returned.</span></span>

### <a name="validation-linux"></a><span data-ttu-id="29826-165">Walidacja (Linux)</span><span class="sxs-lookup"><span data-stu-id="29826-165">Validation (Linux)</span></span>

<span data-ttu-id="29826-166">tooensure są toohello tooconnect stanie Internetem dodatkowej konfiguracji IP za pośrednictwem publicznego adresu IP hello skojarzone go, skorzystaj z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="29826-166">tooensure you are able tooconnect toohello internet from your secondary IP configuration via hello public IP associated it, use hello following command:</span></span>

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="29826-167">Dodatkowej konfiguracji adresu IP można tylko ping toohello Internet, jeśli konfiguracja hello ma publiczny adres IP skojarzone z nim.</span><span class="sxs-lookup"><span data-stu-id="29826-167">For secondary IP configurations, you can only ping toohello Internet if hello configuration has a public IP address associated with it.</span></span> <span data-ttu-id="29826-168">W przypadku podstawowej konfiguracji IP publiczny adres IP nie jest wymagane tooping toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="29826-168">For primary IP configurations, a public IP address is not required tooping toohello Internet.</span></span>

<span data-ttu-id="29826-169">Dla maszyn wirtualnych systemu Linux, podczas próby toovalidate łączność wychodząca z pomocniczego karty Sieciowej może być konieczne tooadd odpowiednie trasy.</span><span class="sxs-lookup"><span data-stu-id="29826-169">For Linux VMs, when trying toovalidate outbound connectivity from a secondary NIC, you may need tooadd appropriate routes.</span></span> <span data-ttu-id="29826-170">Istnieje wiele sposobów toodo to.</span><span class="sxs-lookup"><span data-stu-id="29826-170">There are many ways toodo this.</span></span> <span data-ttu-id="29826-171">Zapoznaj się z odpowiednią dokumentacją dla swojej dystrybucji systemu.</span><span class="sxs-lookup"><span data-stu-id="29826-171">Please see appropriate documentation for your Linux distribution.</span></span> <span data-ttu-id="29826-172">następujące Hello jest jeden tooaccomplish metody to:</span><span class="sxs-lookup"><span data-stu-id="29826-172">hello following is one method tooaccomplish this:</span></span>

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- <span data-ttu-id="29826-173">Należy się tooreplace:</span><span class="sxs-lookup"><span data-stu-id="29826-173">Be sure tooreplace:</span></span>
    - <span data-ttu-id="29826-174">**10.0.0.5** z prywatnego adresu IP hello adres, który ma publicznego adresu IP adres skojarzony tooit</span><span class="sxs-lookup"><span data-stu-id="29826-174">**10.0.0.5** with hello private IP address that has a public IP address associated tooit</span></span>
    - <span data-ttu-id="29826-175">**10.0.0.1** tooyour brama domyślna</span><span class="sxs-lookup"><span data-stu-id="29826-175">**10.0.0.1** tooyour default gateway</span></span>
    - <span data-ttu-id="29826-176">**eth2** nazwa toohello Twojego dodatkowej karty sieciowej</span><span class="sxs-lookup"><span data-stu-id="29826-176">**eth2** toohello name of your secondary NIC</span></span>
