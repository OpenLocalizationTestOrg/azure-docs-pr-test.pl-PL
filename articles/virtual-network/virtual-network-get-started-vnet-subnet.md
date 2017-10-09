---
title: aaaCreate Twojego pierwszego wirtualnej Azure sieci | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak połączyć dwóch maszyn wirtualnych (VM) toohello sieci wirtualnej toocreate sieci wirtualnej platformy Azure (VNet) i połączyć toohello maszyn wirtualnych."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2016
ms.author: jdial
ms.openlocfilehash: 1981524cf706d5ebc83b1ff77735617550ff058a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-virtual-network"></a>Tworzenie pierwszej sieci wirtualnej

Dowiedz się, jak tworzyć dwóch maszyn wirtualnych (VM) toocreate sieć wirtualną (VNet) z dwoma podsieciami i połączyć tooone każdej maszyny Wirtualnej podsieci hello, pokazane na poniższej ilustracji hello:

![Diagram sieci wirtualnej](./media/virtual-network-get-started-vnet-subnet/vnet-diagram.png)

Sieć wirtualna platformy Azure (VNet) to reprezentacja sieci w chmurze hello. Możesz kontrolować ustawienia sieciowe Azure i definiować bloki adresów DHCP, ustawienia DNS, zasady zabezpieczeń oraz routing. więcej informacji na temat pojęć dotyczących sieci wirtualnej, przeczytaj hello toolearn [omówienie sieci wirtualnej](virtual-networks-overview.md) artykułu. Wykonaj następujące zasoby hello toocreate kroki przedstawiono na rysunku hello hello:

1. [Utwórz sieć wirtualną z dwiema podsieciami](#create-vnet).
2. [Utwórz dwie maszyny wirtualne, każde z nich jeden interfejs sieciowy (NIC)](#create-vms)i skojarz tooeach grupa zabezpieczeń sieci karty Sieciowej
3. [Łączenie z tooand z hello maszyny wirtualne](#connect-to-from-vms)
4. [Usuń wszystkie zasoby](#delete-resources). Opłaty są naliczane dla niektórych zasobów hello tworzyć w tym ćwiczeniu, gdy są one udostępniane. toominimize hello opłat, po zakończeniu wykonywania hello, upewnij się, że toocomplete hello kroki opisane w tej sekcji zasobów hello toodelete utworzone.

Będą mieć podstawową wiedzę na temat sposobu użycia sieci wirtualnej po Kończenie hello kroków w tym artykule. Następne kroki są dostarczane, aby dowiedzieć się więcej na temat toouse sieci wirtualnych jest dokładniejsze.

## <a name="create-vnet"></a>Tworzenie sieci wirtualnej z dwiema podsieciami

toocreate sieć wirtualną z dwiema podsieciami, pełną hello kroki, które należy wykonać. Zazwyczaj są to różne podsieci używane toocontrol hello przepływu ruchu między podsieciami.

1. Zaloguj się za toohello [portalu Azure](<https://portal.azure.com>). Jeśli jeszcze nie masz konta, możesz skorzystać z [bezpłatnej miesięcznej wersji próbnej](https://azure.microsoft.com/free). 
2. W hello **ulubione** kliknij okienko portalu hello **nowy**.
3. W hello **nowy** bloku, kliknij przycisk **sieci**. W hello **sieci** bloku, kliknij przycisk **sieci wirtualnej**, jak pokazano na poniższej ilustracji hello:

    ![Diagram sieci wirtualnej](./media/virtual-network-get-started-vnet-subnet/virtual-network.png)

4.  W hello **sieci wirtualnej** bloku, pozostaw *Resource Manager* wybrany jako model wdrażania hello, a następnie kliknij przycisk **Utwórz**.
5.  W hello **bloku sieci wirtualnej Utwórz** wyświetlonym, wprowadź następujące wartości hello, a następnie kliknij przycisk **Utwórz**:

    |**Ustawienie**|**Wartość**|**Szczegóły**|
    |---|---|---|
    |**Nazwa**|*MojaSiećWirtualna*|Nazwa Hello musi być unikatowa w obrębie grupy zasobów hello.|
    |**Przestrzeń adresowa**|*10.0.0.0/16*|Można podać dowolną przestrzeń adresową w notacji CIDR.|
    |**Nazwa podsieci**|*Fronton*|Witaj nazwy podsieci muszą być unikatowe w sieci wirtualnej hello.|
    |**Zakres adresów podsieci**|*10.0.0.0/24*| zakresu Hello musi istnieć w przestrzeni adresowej hello zdefiniowanych dla sieci wirtualnej hello.|
    |**Subskrypcja**|*[Twoja subskrypcja]*|Wybierz subskrypcję toocreate hello sieci wirtualnej w. Sieć wirtualna istnieje w jednej subskrypcji.|
    |**Grupa zasobów**|**Utwórz nową:** *MojaGZ*|Utwórz grupę zasobów. Nazwa grupy zasobów Hello musi być unikatowa w ramach subskrypcji hello, wybranych. więcej informacji na temat grup zasobów, przeczytaj hello toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-groups) artykuł z omówieniem.|
    |**Lokalizacja**|*Zachodnie stany USA*| Zazwyczaj wybierana jest hello lokalizacji, która jest najbliższym tooyour fizycznej lokalizacji.|

    Witaj sieć wirtualna ma kilka toocreate sekund. Po utworzeniu, zobacz hello Azure pulpitu nawigacyjnego portalu.

6. Z siecią wirtualną hello utworzone w portalu Azure hello **ulubione** okienku, kliknij przycisk **wszystkie zasoby**. Kliknij przycisk hello **MyVNet** sieci wirtualnej w hello **wszystkie zasoby** bloku. Jeśli subskrypcja hello już ma kilka zasobów, możesz wprowadzić *MyVNet* w hello **filtrować według nazwy...** pole tooeasily dostępu hello sieci wirtualnej.
7. Witaj **MyVNet** bloku otwiera i wyświetla informacje o hello sieci wirtualnej, jak pokazano na poniższej ilustracji hello:

    ![Diagram sieci wirtualnej](./media/virtual-network-get-started-vnet-subnet/myvnet.png)

8. Jak pokazano na poprzednich obraz powitania, kliknij przycisk **podsieci** toodisplay listę podsieci hello w hello sieci wirtualnej. Witaj tylko podsieci, która istnieje jest **frontonu**, hello podsieć utworzona w kroku 5.
9. W hello MyVNet - bloku podsieci kliknij **+ podsieci** toocreate podsieci z hello następujące informacje i kliknij przycisk **OK** toocreate hello podsieci:

    |**Ustawienie**|**Wartość**|**Szczegóły**|
    |---|---|---|
    |**Nazwa**|*Zaplecze*|Nazwa Hello musi być unikatowa w ramach sieci wirtualnej hello.|
    |**Zakres adresów**|*10.0.1.0/24*|zakresu Hello musi istnieć w przestrzeni adresowej hello zdefiniowanych dla sieci wirtualnej hello.|
    |**Sieciowa grupa zabezpieczeń** i **Tabela tras**|*Brak* (domyślnie)|Sieciowe grupy zabezpieczeń zostały omówione w dalszej części tego artykułu. więcej informacji na temat trasy zdefiniowane przez użytkownika, odczytać hello toolearn [trasy zdefiniowane przez użytkownika](virtual-networks-udr-overview.md) artykułu.|

10. Po dodaniu nowej podsieci hello toohello sieć wirtualną można zamknąć hello **MyVNet — podsieci** bloku, a następnie zamknij hello **wszystkie zasoby** bloku.

## <a name="create-vms"></a>Tworzenie maszyn wirtualnych

Hello sieci wirtualnej i podsieci utworzony można utworzyć hello maszyn wirtualnych. Jednak w tym ćwiczeniu obie maszyny wirtualne, uruchom hello systemu operacyjnego Windows Server, mogą uruchamiać dowolnego systemu operacyjnego, obsługiwany przez platformę Azure, łącznie z kilku różnych dystrybucje systemu Linux.

### <a name="create-web-server-vm"></a>Tworzenie serwera sieci web hello maszyny Wirtualnej

toocreate powitania serwera sieci web maszyny Wirtualnej, pełną hello następujące kroki:

1. W okienku hello Ulubione portalu Azure kliknij **nowy**, **obliczeniowe**, następnie **systemu Windows Server Datacenter 2016**.
2. W hello **systemu Windows Server Datacenter 2016** bloku, kliknij przycisk **Utwórz**.
3. W hello **podstawy** bloku, który pojawia się, wprowadź lub wybierz następujące wartości hello i kliknij przycisk **OK**:

    |**Ustawienie**| **Wartość**|**Szczegóły**|
    |---|---|---|
    |**Nazwa**|*MójSerwerSieciWeb*|Ta maszyna wirtualna służy jako serwer sieci Web, z którym łączą się zasoby internetowe.|
    |**Typ dysku maszyny wirtualnej**|*SSD*|
    |**Nazwa użytkownika**|*Wartość wybrana przez użytkownika*|
    |**Hasło i Potwierdź hasło**|*Wartość wybrana przez użytkownika*|
    | **Subskrypcja**|*<Your subscription>*|Subskrypcja Hello musi być hello tej samej subskrypcji, które wybrano w kroku 5 hello [utworzyć sieć wirtualną z dwiema podsieciami](#create-vnet) sekcji tego artykułu. Hello sieci wirtualnej, Połącz toomust maszyna wirtualna istnieje w hello sam subskrypcji, jak hello maszyny Wirtualnej.|
    |**Grupa zasobów**|**Użyj istniejącej:** wybierz wartość *MojaGZ*|Chociaż firma Microsoft korzysta z tej samej grupie zasobów, jak robiliśmy dla sieci wirtualnej, hello hello hello zasoby nie zawierają tooexist hello tej samej grupie zasobów.|
    |**Lokalizacja**|*Zachodnie stany USA*|Lokalizacja Hello musi być hello tej samej lokalizacji określonej w kroku 5 hello [utworzyć sieć wirtualną z dwiema podsieciami](#create-vnet) sekcji tego artykułu. Maszyny wirtualne i hello sieci wirtualnych łączą toomust istnieje w hello sam lokalizacji.|

4. W hello **wybierz rozmiar** bloku, kliknij przycisk *DS1_V2 standardowe*, następnie kliknij przycisk **wybierz**. Witaj odczytu [rozmiarów maszyn wirtualnych systemu Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykuł zawiera listę wszystkich rozmiarów maszyn wirtualnych systemu Windows, obsługiwane przez platformę Azure.
5. W hello **ustawienia** bloku, wprowadź lub wybierz następujące wartości hello i kliknij przycisk **OK**:

    |**Ustawienie**|**Wartość**|**Szczegóły**|
    |---|---|---|
    |**Przestrzeń dyskowa: użyj zarządzanych dysków**|*Tak*||
    |**Sieć wirtualna**| Wybierz wartość *MojaSiećWirtualna*|Można wybrać żadnych sieci wirtualnej, który istnieje w hello takie same lokalizacji jako hello tworzenia maszyny Wirtualnej. więcej informacji na temat sieci wirtualnych i podsieci, przeczytaj hello toolearn [sieci wirtualnej](virtual-networks-overview.md) artykułu.|
    |**Podsieć**|Wybierz wartość *Fronton*|Możesz wybrać żadnej podsieci, który istnieje w ramach hello sieci wirtualnej.|
    |**Publiczny adres IP**|Zaakceptuj domyślną hello|Publiczny adres IP umożliwia możesz tooconnect toohello maszyny Wirtualnej z hello Internet. więcej informacji na temat publiczne adresy IP, przeczytaj hello toolearn [adresów IP](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses) artykułu.|
    |**Sieciowa grupa zabezpieczeń (zapora)**|Zaakceptuj domyślną hello|Kliknij przycisk hello **(nowy) nsg MyWebServer** portal hello NSG domyślny utworzony tooview jego ustawienia. W hello **Utwórz grupę zabezpieczeń sieci** bloku, który zostanie otwarty, powiadomienia, że ma jedną przychodzącej reguły, która zezwala na ruch TCP/3389 protokołu RDP z dowolny źródłowy adres IP.|
    |**Wszystkie inne wartości**|Zaakceptuj ustawienia domyślne hello|więcej informacji na temat hello pozostałe ustawienia odczytu hello toolearn [maszyn wirtualnych o](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykułu.|

    Grupy zabezpieczeń sieci (NSG) pozwalają toocreate reguły ruchu przychodzącego/wychodzącego hello typu ruchu sieciowego, który może przepływać tooand z hello maszyny Wirtualnej. Domyślnie wszystkie toohello przychodzący ruch maszyny Wirtualnej zostanie odrzucone. W przypadku serwera sieci Web w środowisku produkcyjnym można dodać reguły ruchu przychodzącego dla portów TCP/80 (HTTP) i TCP/443 (HTTPS). Dla ruchu wychodzącego nie ma reguł, ponieważ domyślnie cały ruch wychodzący jest dozwolony. Możesz dodać lub usunąć zasady toocontrol ruchu na zasad. Witaj odczytu [sieciowej grupy zabezpieczeń](virtual-networks-nsg.md) toolearn artykułu więcej informacji na temat grup NSG.

6.  W hello **Podsumowanie** bloku, przejrzyj hello ustawienia i kliknij przycisk **OK** hello toocreate maszyny Wirtualnej. Kafelek stanu jest wyświetlana na pulpicie nawigacyjnym portalu hello jako powitalne tworzy maszyny Wirtualnej. Może upłynąć kilka minut toocreate. Nie trzeba toowait dla niego toocomplete. Można kontynuować toohello następnym krokiem podczas hello utworzenia maszyny Wirtualnej.

### <a name="create-database-server-vm"></a>Tworzenie serwera bazy danych hello maszyny Wirtualnej

toocreate powitania serwera bazy danych maszyny Wirtualnej, pełną hello następujące kroki:

1.  W okienku Ulubione powitania kliknij **nowy**, **obliczeniowe**, następnie **systemu Windows Server Datacenter 2016**.
2.  W hello **systemu Windows Server Datacenter 2016** bloku, kliknij przycisk **Utwórz**.
3.  W hello **blok podstawowych ustawień**, wprowadź lub wybierz hello następujące wartości, a następnie kliknij przycisk **OK**:

    |**Ustawienie**|**Wartość**|**Szczegóły**|
    |---|---|---|
    |**Nazwa**|*MójSerwerBD*|Ta maszyna wirtualna służy jako serwer bazy danych, serwer sieci web hello łączy się, że tego hello Internet nie można nawiązać połączenia.|
    |**Typ dysku maszyny wirtualnej**|*SSD*||
    |**Nazwa użytkownika**|Wartość wybrana przez użytkownika||
    |**Hasło i Potwierdź hasło**|Wartość wybrana przez użytkownika||
    |**Subskrypcja**|<Your subscription>|Subskrypcja Hello musi być hello tej samej subskrypcji, które wybrano w kroku 5 hello [utworzyć sieć wirtualną z dwiema podsieciami](#create-vnet) sekcji tego artykułu.|
    |**Grupa zasobów**|**Użyj istniejącej:** wybierz wartość *MojaGZ*|Chociaż firma Microsoft korzysta z tej samej grupie zasobów, jak robiliśmy dla sieci wirtualnej, hello hello hello zasoby nie zawierają tooexist hello tej samej grupie zasobów.|
    |**Lokalizacja**|*Zachodnie stany USA*|Lokalizacja Hello musi być hello tej samej lokalizacji określonej w kroku 5 hello [utworzyć sieć wirtualną z dwiema podsieciami](#create-vnet) sekcji tego artykułu.|

4.  W hello **wybierz rozmiar** bloku, kliknij przycisk *DS1_V2 standardowe*, następnie kliknij przycisk **wybierz**.
5.  W hello **ustawienia** bloku, wprowadź lub wybierz następujące wartości hello i kliknij przycisk **OK**:

    |**Ustawienie**|**Wartość**|**Szczegóły**|
    |----|----|---|
    |**Przestrzeń dyskowa: użyj zarządzanych dysków**|*Tak*||
    |**Sieć wirtualna**|Wybierz wartość *MojaSiećWirtualna*|Można wybrać żadnych sieci wirtualnej, który istnieje w hello takie same lokalizacji jako hello tworzenia maszyny Wirtualnej.|
    |**Podsieć**|Wybierz *zaplecza* klikając hello **podsieci** pola, wybierając **zaplecza** z hello **Wybierz podsieć** bloku|Możesz wybrać żadnej podsieci, który istnieje w ramach hello sieci wirtualnej.|
    |**Publiczny adres IP**|Brak — kliknij hello domyślny adres, a następnie kliknij przycisk **Brak** z hello **wybierz publiczny adres IP** bloku|Bez publicznego adresu IP, można połączyć tylko toohello maszyny Wirtualnej z innej maszyny Wirtualnej podłączone toohello tej samej sieci wirtualnej. Nie można połączyć tooit bezpośrednio z hello Internet.|
    |**Sieciowa grupa zabezpieczeń (zapora)**|Zaakceptuj domyślną hello| Jak domyślne hello, utworzone grupy NSG hello MyWebServer maszyny Wirtualnej, tym NSG również ma hello same domyślne reguły dla ruchu przychodzącego. W przypadku serwera bazy danych można dodać regułę ruchu przychodzącego dla protokołu TCP/1433 (MS SQL). Dla ruchu wychodzącego nie ma reguł, ponieważ domyślnie cały ruch wychodzący jest dozwolony. Możesz dodać lub usunąć zasady toocontrol ruchu na zasad.|
    |**Wszystkie inne wartości**|Zaakceptuj ustawienia domyślne hello||

6.  W hello **Podsumowanie** bloku, przejrzyj hello ustawienia i kliknij przycisk **OK** hello toocreate maszyny Wirtualnej. Kafelek stanu jest wyświetlana na pulpicie nawigacyjnym portalu hello jako powitalne tworzy maszyny Wirtualnej. Może upłynąć kilka minut toocreate. Nie trzeba toowait dla niego toocomplete. Można kontynuować toohello następnym krokiem podczas hello utworzenia maszyny Wirtualnej.

## <a name="review"></a>Przeglądanie zasobów

Jeśli utworzono jedną sieć wirtualną i dwie maszyny wirtualne, hello portalu Azure utworzony kilka dodatkowych zasobów w grupie zasobów MyRG hello. Przejrzyj zawartość hello grupy zasobów MyRG hello, wykonując następujące kroki hello:

1. W hello **ulubione** okienku, kliknij przycisk **więcej usług**.
2. W hello **więcej usług** okienka, typ *grup zasobów* w polu hello hello word *filtru* w nim. Kliknij przycisk **grup zasobów** po wyświetleniu go w hello filtrowane listy.
3. W hello **grup zasobów** okienku, kliknij przycisk hello *MyRG* grupy zasobów. Jeśli masz wiele grup zasobów w ramach subskrypcji, możesz wpisać *MyRG* hello pole, które zawiera tekst hello *filtrować według nazwy...* Grupa zasobów tooquickly dostępu hello MyRG.
4.  W hello **MyRG** bloku, zostanie wyświetlony których hello grupa zasobów zawiera zasoby 12, jak pokazano na poniższej ilustracji hello:

    ![Zawartość grupy zasobów](./media/virtual-network-get-started-vnet-subnet/resource-group-contents.png)

więcej informacji na temat maszyn wirtualnych, dysków i kont magazynu, przeczytaj hello toolearn [maszyny wirtualnej](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [dysku](../virtual-machines/windows/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-network%2ftoc.json), i [konta magazynu](../storage/common/storage-introduction.md?toc=%2fazure%2fvirtual-network%2ftoc.json) omówienie artykułów. Hello dwie domyślne grupy NSG hello portalu utworzony widoczny. Można również sprawdzić tego portalu hello utworzone dwie sieci interfejsu (NIC) zasoby. Karta sieciowa umożliwia zasobów tooother tooconnect maszyny Wirtualnej przez hello sieci wirtualnej. Witaj odczytu [kart](virtual-network-network-interface.md) toolearn artykułu więcej informacji na temat kart sieciowych. Hello portal również utworzyć jeden zasób adres publiczny adres IP. Publiczne adresy IP to jedno z ustawień zasobu publicznych adresów IP. więcej informacji na temat publiczne adresy IP, przeczytaj hello toolearn [adresów IP](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses) artykułu.

## <a name="connect-to-from-vms"></a>Połącz toohello maszyny wirtualne

Za pomocą sieci wirtualnej i dwie maszyny wirtualne utworzone można teraz połączyć toohello maszyn wirtualnych, wykonując kroki hello hello następujące sekcje:

### <a name="connect-from-internet"></a>Połącz serwer sieci web toohello maszyny Wirtualnej z hello Internet

tooconnect toohello serwer sieci web maszyny Wirtualnej z hello Internet, pełną hello następujące kroki:

1. W portalu hello hello Otwórz grupę zasobów MyRG, wykonując hello etapami hello [Przejrzyj zasoby](#review) sekcji tego artykułu.
2. W hello **MyRG** bloku, kliknij przycisk hello **MyWebServer** maszyny Wirtualnej.
3. W hello **MyWebServer** bloku, kliknij przycisk **Connect**, jak pokazano na poniższej ilustracji hello:

    ![Połącz serwer tooweb maszyny Wirtualnej](./media/virtual-network-get-started-vnet-subnet/webserver.png)

4. Zezwalaj na powitania toodownload Twojego przeglądarki *MyWebServer.rdp* pliku, a następnie otwórz go.
5. Jeśli pojawi się okno z okna dialogowego informowania, możesz tego wydawcy hello hello połączenia zdalnego nie można zweryfikować, kliknij przycisk **Connect**.
6. Podczas wprowadzania poświadczeń, upewnij się, należy zalogować się za pomocą hello nazwę użytkownika i hasło określone w kroku 3 hello [serwera sieci web hello tworzenie maszyny Wirtualnej](#create-web-server-vm) sekcji tego artykułu. Jeśli hello **zabezpieczenia systemu Windows** pojawi się okno nie listy hello poprawne poświadczenia, może być konieczne tooclick **więcej opcji**, następnie **korzystała z innego konta**, więc możesz Określ hello poprawną nazwę użytkownika i hasło). Kliknij przycisk **OK** toohello tooconnect maszyny Wirtualnej.
7. Jeśli zostanie wyświetlony **Podłączanie pulpitu zdalnego** pole dowie się, że tożsamość komputera zdalnego hello hello nie można zweryfikować, kliknij przycisk **tak**.
8. Jesteś teraz połączonych toohello MyWebServer maszyny Wirtualnej z hello Internet. Pozostaw hello połączeń usług pulpitu zdalnego otwórz toocomplete hello kroki w następnej sekcji hello.

połączenie zdalnego Hello jest toohello publicznego adresu IP przypisanego toohello publicznego adresu IP Adres zasobu hello portalu utworzony w kroku 5 hello [utworzyć sieć wirtualną z dwiema podsieciami](#create-vnet) sekcji tego artykułu. połączenie Hello jest dozwolona, ponieważ reguła domyślna hello utworzone w hello **MyWebServer nsg** toohello maszyny Wirtualnej z dowolnego adresu IP źródłowego ruchu przychodzącego grupy NSG dozwolone TCP/3389 (RDP). Jeśli spróbujesz tooconnect toohello maszyny Wirtualnej za pośrednictwem innego portu, hello połączenia nie powiedzie się, jeśli nie możesz dodać dodatkowe reguły ruchu przychodzącego toohello NSG zezwalanie hello dodatkowych portów.

>[!NOTE]
>Jeśli dodasz toohello dodatkowe reguły ruchu przychodzącego grupy NSG, upewnij się, że hello tych samych portów w Zaporze systemu Windows hello są otwarte lub hello połączenia kończy się niepowodzeniem.
>

### <a name="connect-to-internet"></a>Połącz toohello Internetu z serwera sieci web hello maszyny Wirtualnej

tooconnect wychodzących toohello Internetu z serwera sieci web hello maszyny Wirtualnej, pełną hello następujące kroki:

1. Jeśli nie masz jeszcze toohello połączenia zdalnego, otwórz MyWebServerVM, należy toohello połączenia zdalnego maszyny Wirtualnej, wykonując kroki hello hello [serwera sieci web toohello Connect maszyny Wirtualnej z hello Internet](#connect-from-internet) sekcji tego artykułu.
2. Na pulpicie systemu Windows hello Otwórz program Internet Explorer. W hello **ustawienia programu Internet Explorer 11** okno dialogowe, kliknij przycisk **nie skorzystać z zalecanych ustawień**, następnie kliknij przycisk **OK**. Jest zalecana tooaccept hello zalecane ustawienia dla serwera produkcyjnego.
3. Na pasku adresu programu Internet Explorer hello, wprowadź [bing.com](http:www.bing.com). Jeśli zostanie wyświetlone okno dialogowe programu Internet Explorer, kliknij przycisk **Dodaj**, następnie **Dodaj** w hello **Zaufane witryny** okno dialogowe i kliknij przycisk **Zamknij**. Powtórz te czynności we wszystkich innych oknach dialogowych programu Internet Explorer.
4. Strona wyszukiwania na powitania Bing, wprowadź *whatsmyipaddress*, następnie kliknij przycisk Lupa hello. Bing zwraca hello publiczny adres przypisany toohello publicznego adresu IP zasobu adresu IP utworzonych przez portal powitania po utworzeniu hello maszyny Wirtualnej. Jeśli należy zbadać ustawienia hello hello **MyWebServer ip** zasobów, zobacz hello tego samego adresu IP przypisanego toohello publicznego zasobu adresu IP, jak przedstawiono na rysunku hello, który jest zgodny. tooyour przypisany adres IP Hello maszyny Wirtualnej różni się jednak.

    ![Połącz serwer tooweb maszyny Wirtualnej](./media/virtual-network-get-started-vnet-subnet/webserver-pip.png)

5.  Pozostaw hello połączeń usług pulpitu zdalnego otwórz toocomplete hello kroki w następnej sekcji hello.

Możesz są stanie tooconnect toohello Internet z hello maszyny Wirtualnej, ponieważ wszystkie połączenia wychodzące z hello maszyna wirtualna jest domyślnie dozwolona. Łączność wychodząca można ograniczyć, dodając dodanie reguły toohello grupa NSG stosowana toohello karty Sieciowej, toohello podsieci hello jest połączona karta sieciowa, lub obie.

Jeśli hello maszyny Wirtualnej jest umieszczany hello zatrzymana stan (cofnięciu przydziału) za pomocą portalu hello, zmienić hello publicznego adresu IP. Jeśli potrzebujesz publicznego adresu IP hello adresów nigdy nie zmiany, można użyć hello statyczną metodą przydziału hello adresu IP, a nie hello — metoda alokacji dynamicznego (który jest domyślnym hello). więcej informacji o toolearn hello różnice między metodami alokacji odczytu hello [adresów IP, typy i metody alokacji](virtual-network-ip-addresses-overview-arm.md) artykułu.

### <a name="webserver-to-dbserver"></a>Połącz serwer bazy danych toohello maszyny Wirtualnej z serwera sieci web hello maszyny Wirtualnej

tooconnect toohello serwer bazy danych maszyny Wirtualnej z serwera sieci web hello maszyny Wirtualnej, pełną hello następujące kroki:

1. Jeśli nie masz jeszcze toohello połączenia zdalnego, otwórz MyWebServer maszyny Wirtualnej, należy toohello połączenia zdalnego maszyny Wirtualnej, wykonując kroki hello hello [serwera sieci web toohello Connect maszyny Wirtualnej z hello Internet](#connect-from-internet) sekcji tego artykułu.
2. Kliknij przycisk Uruchom hello na powitania lewym dolnym rogu pulpitu systemu Windows hello, a następnie zacznij wpisywać ciąg *pulpitu zdalnego*. Gdy Wyświetla listę menu Start hello **Podłączanie pulpitu zdalnego**, kliknij ją.
3. W hello **Podłączanie pulpitu zdalnego** okna dialogowego wprowadź *MójSerwerBD* hello nazwy komputera i kliknij przycisk **Connect**.
4. Wprowadź hello nazwy użytkownika i hasła, wprowadzona w kroku 3 hello [serwera bazy danych utwórz hello wirtualna](#create-database-server-vm) sekcji tego artykułu, następnie kliknij przycisk **OK**.
5. Jeśli pojawi się okno z okna dialogowego informowania, możesz tego hello tożsamość komputera zdalnego hello nie można zweryfikować, kliknij przycisk **tak**.
6. Pozostaw serwery tooboth hello Otwórz toocomplete kroki opisane w następnej sekcji hello hello połączeń usług pulpitu zdalnego.

Jesteś serwera bazy danych toohello połączenia hello toomake stanie maszyny Wirtualnej z serwera sieci web hello maszyny Wirtualnej dla hello z następujących powodów:

- TCP/3389 połączenia przychodzące są włączone dla dowolnego źródłowy adres IP w domyślnej hello NSG utworzony w kroku 5 hello [serwera bazy danych utwórz hello wirtualna](#create-database-server-vm) sekcji tego artykułu.
- Zainicjowano hello połączenie z serwerem sieci web hello maszyny Wirtualnej, który jest połączony toohello tej samej sieci wirtualnej jako serwera bazy danych hello maszyny Wirtualnej. tooa tooconnect maszynę Wirtualną, która nie ma publicznego tooit przypisany adres IP, należy połączyć z innym toohello maszyny Wirtualnej podłączone sam sieci wirtualnej, nawet jeśli hello maszyny Wirtualnej jest połączonych tooa innej podsieci.
- Mimo że hello maszyny wirtualne są połączone toodifferent podsieci, platforma Azure tworzy trasy domyślne, które umożliwiają łączność między podsieciami. Tworzenie własnych jednak można zastąpić hello trasy domyślne. Witaj odczytu [trasy zdefiniowane przez użytkownika](virtual-networks-udr-overview.md) toolearn artykułu dodatkowe informacje o routing na platformie Azure.

Jeśli spróbujesz tooinitiate połączenia zdalnego serwera bazy danych toohello maszyny Wirtualnej z hello Internet, tak jak w hello [serwera sieci web toohello Connect maszyny Wirtualnej z hello Internet](#connect-from-internet) sekcji tego artykułu, zobacz ten hello **Connect** opcją jest niedostępny. Połączenie jest niedostępne, ponieważ nie istnieje żadne publicznego toohello przypisany adres IP maszyny Wirtualnej, więc tooit połączenia przychodzące z Internetu hello nie są możliwe.

### <a name="connect-toohello-internet-from-hello-database-server-vm"></a>Połączyć toohello Internetu z poziomu serwera bazy danych hello maszyny Wirtualnej

Połączenia wychodzące toohello Internet z serwera bazy danych hello maszyny Wirtualnej, wykonując następujące kroki hello:

1. Jeśli nie masz jeszcze toohello połączenia zdalnego, otwórz MójSerwerBD maszyny Wirtualnej z hello MyWebServer maszyny Wirtualnej, pełną hello etapami hello [Connect toohello serwera bazy danych maszyny Wirtualnej z serwera sieci web hello wirtualna](#webserver-to-dbserver) sekcji tego artykułu.
2. Na pulpicie systemu Windows hello na powitania MójSerwerBD maszyny Wirtualnej, Otwórz program Internet Explorer i odpowiadać toohello okien dialogowych, tak jak w kroku 2 i 3 hello [połączyć toohello Internetu z poziomu serwera sieci web hello wirtualna](#connect-to-internet) sekcji tego artykułu.
3. Na pasku adresu hello, wprowadź [bing.com](http:www.bing.com).
4. Kliknij przycisk **Dodaj** w hello programu Internet Explorer pojawi się okno dialogowe, następnie **Dodaj**, następnie **Zamknij** w hello **zaufane** okno dialogowe witryny. Wykonaj te czynności we wszystkich innych oknach dialogowych, które się pojawią.
5. Strona wyszukiwania na powitania Bing, wprowadź *whatsmyipaddress*, następnie kliknij przycisk Lupa hello. Bing zwraca hello publicznego adresu IP adres przypisany aktualnie toohello maszyny Wirtualnej na podstawie hello infrastruktury platformy Azure. 6. Zamknij hello zdalnego pulpitu toohello MójSerwerBD maszyny Wirtualnej z hello MyWebServer maszyny Wirtualnej, a następnie zamknij hello połączenia zdalnego toohello MyWebServer maszyny Wirtualnej.

Witaj toohello wychodzące połączenie internetowe jest dozwolona, ponieważ domyślnie dozwolony jest cały ruch wychodzący nawet, jeśli zasób publiczny adres IP nie jest przypisany toohello MójSerwerBD maszyny Wirtualnej. Wszystkie maszyny wirtualne, domyślnie są możliwe tooconnect wychodzących toohello Internetu, z lub bez publicznego adresu IP adres zasób przydzielony toohello maszyny Wirtualnej. Nie jesteś toohello tooconnect stanie publicznego adresu IP adresu z hello Internet, tak jak zostały hello stanie toofor zasób przydzielony adres MyWebServer maszyny Wirtualnej, który ma publicznego adresu IP.

## <a name="delete-resources"></a>Usuwanie wszystkich zasobów

toodelete wszystkie zasoby są tworzone w tym artykule pełną hello następujące kroki:

1. tooview hello MyRG grupy zasobów utworzonej w tym artykule, pełną kroki 1 – 3 w hello [Przejrzyj zasoby](#review) sekcji tego artykułu. Ponownie Przejrzyj hello zasoby w grupie zasobów hello. Jeśli utworzono hello MyRG grupy zasobów na poprzednie kroki, znajdują się hello zasobach 12 przedstawiono na rysunku hello w kroku 4.
2. W bloku MyRG powitania kliknij hello **usunąć** przycisku.
3. Witaj portal wymaga nazwy hello tootype tooconfirm grupy zasobów hello, które mają toodelete go. Jeśli widzisz zasobów innych niż zasoby hello przedstawionym w kroku 4 hello [Przejrzyj zasobów](#review) sekcji tego artykułu, kliknij przycisk **anulować**. Jeśli zostanie wyświetlony tylko zasoby hello 12 utworzone jako część tego artykułu, wpisz *MyRG* hello Nazwa grupy zasobów, klikając **usunąć**. Usunięcie grupy zasobów powoduje usunięcie wszystkich zasobów w grupie zasobów hello, więc zawsze tooconfirm się, że zawartość hello grupy zasobów przed jego usunięciem. Hello portal usuwa wszystkie zasoby zawarte w grupie zasobów hello, a następnie usuwa samej grupy zasobów hello. Ten proces trwa kilka minut.

## <a name="next-steps"></a>Następne kroki

W tym ćwiczeniu utworzono sieć wirtualną i dwie maszyny wirtualne. Maszyny wirtualne zostały utworzone przy użyciu zarówno niestandardowych, jak i domyślnych ustawień. Zalecamy przeczytanie hello następujące artykuły, przed wdrożeniem w produkcyjnej sieci wirtualnych i maszyn wirtualnych, tooensure zrozumieć wszystkich dostępnych ustawień:

- [Sieci wirtualne](virtual-networks-overview.md)
- [Publiczne adresy IP](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses)
- [Interfejsy sieciowe](virtual-network-network-interface.md)
- [Sieciowe grupy zabezpieczeń](virtual-networks-nsg.md)
- [Maszyny wirtualne](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
