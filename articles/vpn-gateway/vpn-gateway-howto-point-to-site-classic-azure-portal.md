---
title: "Połącz komputer tooa sieć wirtualną przy użyciu punkt-lokacja i uwierzytelnianie certyfikatu: klasycznego portalu Azure | Dokumentacja firmy Microsoft"
description: "Bezpieczne łączenie tooyour klasycznego Azure Virtual Network, tworząc połączenie bramy sieci VPN typu punkt-lokacja za pomocą hello portalu Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 65e14579-86cf-4d29-a6ac-547ccbd743bd
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 9b53ba43ee4dfb61defeec458905fb1f1b18c3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-classic-azure-portal"></a>Skonfiguruj tooa połączenie punkt-lokacja sieci wirtualnej przy użyciu uwierzytelniania certyfikatów (klasyczne): Azure portal

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

W tym artykule opisano, jak toocreate sieci wirtualnej za pomocą połączenia punkt-lokacja za pomocą modelu wdrażania klasycznego hello hello portalu Azure. Ta konfiguracja korzysta z certyfikatów tooauthenticate hello połączenie klienta. Można również utworzyć tę konfigurację za pomocą narzędzia wdrażania różnych lub model wdrożenia, wybierając inną opcję z hello następującej listy:

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Portal Azure (klasyczny)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>

Brama sieci VPN typu punkt-lokacja (P2S) umożliwia tworzenie sieci wirtualnej tooyour bezpiecznego połączenia z pojedynczym komputerem klienckim. Połączenia sieci VPN punkt-lokacja są przydatne, gdy chcesz tooyour tooconnect sieci wirtualnej z lokalizacji zdalnej, takie, gdy są Niezale¿nie z domu lub konferencji. P2S sieci VPN jest również toouse przydatne rozwiązanie, zamiast VPN lokacja-lokacja, jeśli istnieje tylko kilka klientów, którzy potrzebują tooa tooconnect sieci wirtualnej. 

Używa P2S hello gniazda Tunelowanie protokołu SSTP (Secure), która jest oparta na protokole SSL protokołu sieci VPN. Uruchamiając go z komputera klienckiego hello jest nawiązywane połączenie sieci VPN P2S.


![Diagram: połączenie typu punkt-lokacja](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/point-to-site-connection-diagram.png)


Połączenia uwierzytelniania certyfikatów punkt-lokacja wymagają następujących hello:

* Brama dynamicznej sieci VPN.
* Witaj klucz publiczny (plik cer) dla certyfikatu głównego, czyli tooAzure przekazane. Jest uznawany za certyfikat zaufany i używany do uwierzytelniania.
* Certyfikat klienta generowane na podstawie certyfikatu głównego hello i zainstalowane na każdym komputerze klienckim, na którym będzie się łączyć. Ten certyfikat jest używany do uwierzytelniania klientów.
* Pakiet konfiguracji klienta sieci VPN musi zostać wygenerowany i zainstalowany na każdym komputerze klienckim, który nawiązuje połączenie. Pakiet konfiguracji klienta Hello konfiguruje hello natywny klient VPN, który jest już w systemie operacyjnym hello z hello koniecznych tooconnect toohello sieci wirtualnej.

Połączenia typu punkt-lokacja nie wymagają urządzenia sieci VPN ani lokalnego publicznego adresu IP. Witaj połączenia sieci VPN jest tworzony za pośrednictwem protokołu SSTP (Secure Socket Tunneling Protocol). Na powitania po stronie serwera firma Microsoft obsługuje protokół SSTP w wersji 1.0, 1.1 i 1.2. powitania klienta decyduje o tym, które toouse wersji. W przypadku systemu Windows 8.1 i nowszych protokół SSTP domyślnie używa wersji 1.2. 

Aby uzyskać więcej informacji na temat połączenia punkt-lokacja, zobacz hello [punkt-lokacja często zadawane pytania dotyczące](#faq) na końcu hello w tym artykule.

### <a name="example-settings"></a>Przykładowe ustawienia

Można użyć hello następujące wartości toocreate środowiska testowego lub można znaleźć wartości toothese toobetter zrozumieć hello przykłady w tym artykule:

* **Nazwa: VNet1**
* **Przestrzeń adresowa: 192.168.0.0/16**<br>W tym przykładzie zostanie wykorzystana tylko jedna przestrzeń adresowa. Istnieje możliwość użycia więcej niż jednej przestrzeni adresowej dla sieci wirtualnej.
* **Nazwa podsieci: FrontEnd**
* **Zakres adresów podsieci: 192.168.1.0/24**
* **Subskrypcja:** Jeśli masz więcej niż jedną subskrypcję, sprawdź, czy używasz hello właściwy.
* **Grupa zasobów: TestRG**
* **Lokalizacja: Wschodnie stany USA**
* **Typ połączenia: Punkt-lokacja**
* **Przestrzeń adresowa klienta: 172.16.201.0/24**. Klienci sieci VPN, łączący toohello sieci wirtualnej za pomocą to połączenie punkt-lokacja otrzymywać adresy IP z hello określonej puli.
* **GatewaySubnet: 192.168.200.0/24**. podsieć bramy Hello musi używać hello o nazwie "GatewaySubnet".
* **Rozmiar:** wybierz hello bramy, które mają toouse jednostki SKU.
* **Typ routingu: Dynamiczny**

## <a name="vnetvpn"></a>1. Tworzenie sieci wirtualnej i bramy VPN Gateway

Przed rozpoczęciem sprawdź, czy masz subskrypcję platformy Azure. Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial).

### <a name="createvnet"></a>Część 1. Tworzenie sieci wirtualnej

Jeśli nie masz jeszcze sieci wirtualnej, utwórz ją. Zamieszczone zrzuty ekranu są przykładowe. Należy się, że wartości hello tooreplace własnymi. toocreate sieć wirtualną przy użyciu hello portalu Azure, użyj hello następujące kroki:

1. W przeglądarce Przejdź toohello [portalu Azure](http://portal.azure.com) i, jeśli to konieczne, zaloguj się przy użyciu konta platformy Azure.
2. Kliknij przycisk **Nowy**. W hello **marketplace hello wyszukiwania** wpisz "Sieci wirtualnej". Zlokalizuj **sieci wirtualnej** hello zwrócił listy i kliknij przycisk tooopen hello **sieci wirtualnej** strony.

  ![Strona wyszukiwania sieci wirtualnej](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvnetportal700.png)
3. Dolnej hello hello strony sieci wirtualnej, z hello **wybierz model wdrożenia** wybierz **klasycznego**, a następnie kliknij przycisk **Utwórz**.

  ![Wybieranie modelu wdrożenia](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/selectmodel.png)
4. Na powitania **Utwórz sieć wirtualną** skonfiguruj hello ustawienia sieci wirtualnej. Na tej stronie dodaj pierwszą przestrzeń adresową i zakres adresów pojedynczej podsieci. Po utworzeniu hello sieci wirtualnej można wrócić do poprzedniej strony i dodać dodatkowe podsieci oraz przestrzenie adresowe.

  ![Strona Tworzenie sieci wirtualnej](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/vnet125.png)
5. Sprawdź, że hello **subskrypcji** jest hello właściwy. Subskrypcje można zmienić za pomocą listy rozwijanej hello.
6. Kliknij przycisk **Grupy zasobów** i wybierz istniejącą grupę zasobów lub utwórz nową, wpisując nazwę nowej grupy zasobów. Jeśli tworzysz nową grupę zasobów, grupy zasobów hello nazwy zgodnie z tooyour planowane wartości konfiguracji. Aby uzyskać więcej informacji na temat grup zasobów, zobacz temat [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).
7. Następnie wybierz pozycję hello **lokalizacji** ustawienia sieci wirtualnej. Lokalizacja Hello Określa, gdzie znajdują się zasoby hello wdrożenie toothis sieci wirtualnej.
8. Wybierz **toodashboard numeru Pin** jeśli mają toobe toofind może łatwo na pulpicie nawigacyjnym hello sieci wirtualnej, a następnie kliknij przycisk **Utwórz**.

  ![Toodashboard numeru PIN](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/pintodashboard150.png)
9. Po kliknięciu przycisku Utwórz na pulpicie nawigacyjnym, który będzie odzwierciedlać postęp Twojej sieci wirtualnej hello pojawi się Kafelek. Trwa tworzenie Hello kafelka zmienia hello sieci wirtualnej.

  ![Kafelek tworzenia sieci wirtualnej](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png)
10. Po utworzeniu sieci wirtualnej, zobacz **utworzony** kategorii **stan** na stronie sieci hello hello klasycznego portalu Azure.
11. Dodaj serwer DNS (opcjonalnie). Po utworzeniu sieci wirtualnej, można dodać hello adres IP serwera DNS do rozpoznawania nazw. adres IP serwera DNS, który określisz Hello powinna być hello adres serwera DNS, który można rozwiązać nazw hello hello zasobów w sieci wirtualnej.<br>tooadd serwera DNS, otwórz hello ustawienia dla sieci wirtualnej, kliknij serwery DNS i Dodaj adres IP hello powitania serwera DNS, które mają toouse.

### <a name="gateway"></a>Część 2. Tworzenie podsieci bramy i bramy o dynamicznym routingu

W tym kroku tworzona jest podsieć bramy i brama o dynamicznym routingu. W hello portal Azure hello klasycznego modelu wdrażania, tworzenie hello podsieci bramy i hello bramy może odbywać się za pośrednictwem hello takie same strony konfiguracji.

1. W portalu hello Przejdź toohello sieci wirtualnej, dla której ma zostać toocreate bramy.
2. Na stronie powitania dla sieci wirtualnej, na powitania **omówienie** w sekcji połączenia sieci VPN hello, kliknij **bramy**.

  ![Kliknij przycisk toocreate bramy](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/beforegw125.png)
3. Na powitania **nowego połączenia sieci VPN** wybierz pozycję **punkt lokacja**.

  ![Połączenie typu punkt-lokacja](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvpnconnect.png)
4. Aby uzyskać **przestrzeni adresowej klienta**, zakres adresów IP hello. To jest zakres hello, z których klienci VPN hello otrzymywać adresu IP podczas nawiązywania połączenia. Użyj zakresu prywatnych adresów IP, który nie nakłada się na powitania lokalnej lokalizacji, która ma zostać nawiązane połączenie z lub hello sieci wirtualnej, który ma tooconnect do. Można usunąć hello automatycznie wypełnianej zakresu, a następnie dodaj hello zakresu prywatnych adresów IP, które mają toouse.

  ![Przestrzeń adresowa klienta](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientaddress.png)
5. Wybierz hello **Utwórz bramę natychmiast** wyboru.

  ![Utwórz bramę natychmiast](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/creategwimm.png)
6. Kliknij przycisk **konfiguracji bramy opcjonalne** tooopen hello **konfiguracji bramy** strony.

  ![Kliknij pozycję Opcjonalna konfiguracja bramy](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/optsubnet125.png)
7. Kliknij przycisk **podsieci, skonfiguruj wymagane ustawienia** tooadd hello **podsieci bramy**. Mimo że jest możliwe toocreate jak /29 podsieć bramy, zaleca się utworzenie większej podsieć, która zawiera więcej adresów, wybierając co najmniej /28 lub /27. Umożliwi to za mało adresów tooaccommodate możliwe dodatkowe konfiguracje, które można w hello przyszłych. Podczas pracy z podsieciami bramy, należy unikać kojarzenia podsieci bramy toohello grupa zabezpieczeń sieci. Kojarzenie podsieci toothis grupy zabezpieczeń sieci może spowodować toostop bramy sieci VPN, działa zgodnie z oczekiwaniami.

  ![Dodawanie podsieci GatewaySubnet](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsubnet125.png)
8. Wybierz hello bramy **rozmiar**. rozmiar Hello jest hello jednostka SKU bramy dla bramy sieci wirtualnej. W portalu hello hello domyślne jednostka SKU jest **podstawowe**. Więcej informacji o jednostkach SKU bramy zawiera artykuł [Informacje o ustawieniach bramy VPN Gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

  ![Rozmiar bramy](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsize125.png)
9. Wybierz hello **typ routingu** dla bramy. Konfiguracje P2S wymagają typu routingu **Dynamiczny**. Kliknij przycisk **OK** po zakończeniu konfigurowania tej strony.

  ![Konfigurowanie typu routingu](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/routingtype125.png)
10. Na powitania **nowego połączenia sieci VPN** kliknij przycisk **OK** u dołu hello toobegin strony hello Tworzenie bramy sieci wirtualnej. Brama sieci VPN może potrwać too45 toocomplete minut, w zależności od hello jednostka sku bramy, który można wybrać.

## <a name="generatecerts"></a>2. Tworzenie certyfikatów

Certyfikaty są używane przez klientów sieci VPN platformy Azure tooauthenticate sieci VPN punkt-lokacja. Możesz przekazać hello informacje o kluczu publicznym z tooAzure certyfikatu głównego hello. klucz publiczny Hello następnie jest uznawany za "zaufanych". Certyfikaty klienta musi generowane na podstawie hello zaufanego certyfikatu głównego, a następnie zainstalowany na każdym komputerze klienckim w hello certyfikatów bieżącego użytkownika/osobistego magazynu certyfikatów. certyfikatu Hello jest używane tooauthenticate powitania klienta, gdy inicjują połączenia toohello sieci wirtualnej. 

Jeśli używasz certyfikatów z podpisem własnym, należy je utworzyć przy użyciu określonych parametrów. Można utworzyć certyfikatu z podpisem własnym za pomocą instrukcji hello [środowiska PowerShell i Windows 10](vpn-gateway-certificates-point-to-site.md), lub [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md). Jest ważne, należy wykonać kroki hello w tych instrukcjach podczas pracy z certyfikatami z podpisem głównego i generowania certyfikatów klienta z hello certyfikatu głównego z podpisem własnym. W przeciwnym razie hello certyfikaty, które tworzysz, nie będzie zgodna z połączeń P2S i zostanie wyświetlony błąd połączenia.

### <a name="cer"></a>Część 1: Uzyskać klucz publiczny hello (.cer) dla certyfikatu głównego hello

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <a name="genclientcert"></a>Część 2. Generowanie certyfikatu klienta

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="upload"></a>3. Przekaż plik .cer certyfikatu głównego hello

Po utworzeniu bramy hello, możesz przekazać plik .cer hello, (zawierający informacje o kluczu publicznym hello) dla tooAzure certyfikatów zaufanych certyfikatów głównych. Nie możesz przekazać hello klucz prywatny dla tooAzure certyfikatu głównego hello. Po przekazaniu pliku a.cer Azure może być używany tooauthenticate klientów, którzy zainstalowali generowane na podstawie hello zaufanego certyfikatu głównego certyfikatu klienta. Możesz przekazać pliki certyfikatów zaufanych głównych - zapasowej tooa łącznie 20 - później, w razie potrzeby.  

1. Na powitania **połączeń sieci VPN** sekcji hello strony dla sieci wirtualnej, kliknij przycisk hello **klientów** hello graficzne tooopen **punkt lokacja sieci VPN połączenia** strony.

  ![Klienci](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. Na powitania **połączeniapunkt lokacja** kliknij przycisk **zarządzanie certyfikatami** tooopen hello **certyfikaty** strony.<br>

  ![Strona Certyfikaty](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. Na powitania **certyfikaty** kliknij przycisk **przekazać** tooopen hello **przekazywania certyfikatu** strony.<br>

    ![Strona przekazywania certyfikatów](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/uploadcerts.png)<br>
4. Kliknij przycisk hello toobrowse graficzne folderu pliku .cer hello. Wybierz plik hello, a następnie kliknij przycisk **OK**. Odświeżanie hello strony toosee hello przekazać certyfikat na powitania **certyfikaty** strony.

  ![Przekazywanie certyfikatu](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/upload.png)<br>

## <a name="vpnclientconfig"></a>4. Konfigurowanie powitania klienta

tooa tooconnect sieci wirtualnej za pomocą sieci VPN punkt-lokacja, każdego klienta należy zainstalować natywny klient VPN systemu Windows pakietu tooconfigure hello. Pakiet konfiguracji Hello konfiguruje hello natywny klient VPN systemu Windows przy użyciu sieci wirtualnej toohello tooconnect niezbędne ustawienia hello.

Tak długo, jak wersja hello zgodna architektura hello powitania klienta, można użyć hello pakietu tej samej konfiguracji klienta sieci VPN na każdym komputerze klienckim. Aby hello listę systemów operacyjnych klienta, które są obsługiwane, zobacz hello [połączeńpunkt-lokacja często zadawane pytania dotyczące](#faq) na końcu hello w tym artykule.

### <a name="generateconfigpackage"></a>Część 1: Generowanie i zainstalować pakiet konfiguracji klienta VPN hello

1. W portalu Azure w hello hello **omówienie** sieci wirtualnej, w obszarze **połączeń sieci VPN**, kliknij powitania klienta graficzne tooopen hello **punkt lokacja sieci VPN połączenia** strony.
2. U góry hello hello **punkt lokacja sieci VPN połączenia** kliknij przycisk hello pobierania pakietu, który odpowiada toohello kliencki system operacyjny na którym ma zostać zainstalowany:

  * Dla klientów 64-bitowych wybierz pakiet **Klient sieci VPN (64-bitowy)**.
  * Dla klientów 32-bitowych wybierz pakiet **Klient sieci VPN (32-bitowy)**.

  ![Pobieranie pakietu konfiguracji klienta VPN](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/dlclient.png)<br>
3. Po hello spakowane generuje, Pobierz i zainstaluj go na komputerze klienckim. Jeśli zostanie wyświetlone okno podręczne SmartScreen, kliknij pozycję **Więcej informacji**, a następnie pozycję **Uruchom mimo to**. Można także zapisać tooinstall pakietu hello na innych komputerach klienckich.

### <a name="installclientcert"></a>Część 2: Certyfikat klienta na powitania instalacji

Jeśli chcesz toocreate P2S połączenie z komputera klienckiego niż hello jeden używane certyfikaty klienta na powitania toogenerate należy tooinstall certyfikat klienta. Podczas instalowania certyfikatu klienta, należy hello hasło, które utworzono podczas eksportowania hello certyfikatu klienta. Zazwyczaj jest to wystarczy dwukrotnie hello certyfikatu i instalując je. Aby uzyskać więcej informacji, zobacz [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install) (Instalowanie wyeksportowanego certyfikatu klienta).

## <a name="connect"></a>5. Połącz tooAzure

### <a name="connect-tooyour-vnet"></a>Połącz tooyour sieci wirtualnej

1. tooconnect tooyour sieci wirtualnej, na komputerze klienckim hello Przejdź tooVPN połączeń i Znajdź hello połączenia sieci VPN, który został utworzony. Nazwie hello sama nazwa jak sieci wirtualnej. Kliknij przycisk **Połącz**. Komunikat podręczny może pojawić się odwołuje się toousing hello certyfikatu. Jeśli tak się stanie, kliknij przycisk **Kontynuuj** toouse podwyższonego poziomu uprawnień.
2. Na powitania **połączenia** stan strony, kliknij przycisk **Connect** toostart hello połączenia. Jeśli widzisz **wybierz certyfikat** ekranu, sprawdź, czy powitania klienta certyfikatu przedstawiający hello jedną, które mają toouse tooconnect. Jeśli nie, hello strzałkę listy rozwijanej tooselect hello poprawny certyfikat, a następnie kliknij przycisk **OK**.

  ![Połączenie klienta sieci VPN](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientconnect.png)
3. Połączenie zostało ustanowione.

  ![Ustanowiono połączenie](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>Rozwiązywanie problemów dotyczących połączeń typu punkt-lokacja

[!INCLUDE [verify-client-certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

### <a name="verifyvpnconnect"></a>Sprawdź hello połączenia sieci VPN

1. tooverify, że połączenie sieci VPN jest aktywne, otwórz wiersz polecenia z podwyższonym poziomem uprawnień i uruchom *ipconfig/all*.
2. Wyświetl wyniki hello. Zauważ, że adres IP hello otrzymany jest jednym z adresów hello w zakresie adresów łączności hello punkt-lokacja określone podczas tworzenia sieci wirtualnej. Witaj wyniki powinny mieć podobny przykład toothis:

  ```
    PPP adapter VNet1:
        Connection-specific DNS Suffix .:
        Description.....................: VNet1
        Physical Address................:
        DHCP Enabled....................: No
        Autoconfiguration Enabled.......: Yes
        IPv4 Address....................: 192.168.130.2(Preferred)
        Subnet Mask.....................: 255.255.255.255
        Default Gateway.................:
        NetBIOS over Tcpip..............: Enabled
  ```

## <a name="connectVM"></a>Połącz tooa maszyny wirtualnej

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-classic-include.md)]

## <a name="add"></a>Dodawanie lub usuwanie zaufanych certyfikatów głównych

Zaufane certyfikaty główne można dodawać do platformy Azure lub z niej usuwać. Po usunięciu certyfikatu głównego, nie będzie możliwe tooauthenticate klientów, którzy mają certyfikat, który został wygenerowany z elementem głównym, a w związku z tym nie będą mogli tooconnect. Jeśli mają tooauthenticate klienta i połączyć, należy tooinstall nowego certyfikatu klienta generowane na podstawie certyfikatu głównego, który jest zaufany tooAzure (przekazanego).

### <a name="addtrustedroot"></a>tooadd zaufanego certyfikatu głównego

Możesz dodać zapasowej too20 zaufanego głównego certyfikatu .cer pliki tooAzure. Aby uzyskać instrukcje, zobacz [sekcja 3 - plik .cer certyfikatu głównego hello przekazywania](#upload).

### <a name="removetrustedroot"></a>tooremove zaufanego certyfikatu głównego

1. Na powitania **połączeń sieci VPN** sekcji hello strony dla sieci wirtualnej, kliknij przycisk hello **klientów** hello graficzne tooopen **punkt lokacja sieci VPN połączenia** strony.

  ![Klienci](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. Na powitania **połączeniapunkt lokacja** kliknij przycisk **zarządzanie certyfikatami** tooopen hello **certyfikaty** strony.<br>

  ![Strona Certyfikaty](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. Na powitania **certyfikaty** kliknij hello wielokropka dalej toohello certyfikatu czy tooremove, a następnie kliknij pozycję **usunąć**.

  ![Usuwanie certyfikatu głównego](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deleteroot.png)<br>

## <a name="revokeclient"></a>Odwoływanie certyfikatu klienta

Certyfikaty klienta można odwołać. certyfikat Hello listy odwołania umożliwia tooselectively odmowy połączenia punkt-lokacja, w oparciu o certyfikaty klienta. Różni się to od usuwania zaufanego certyfikatu głównego. Jeśli usuniesz .cer certyfikatu zaufanego głównego z platformy Azure, odwołuje hello dostępu dla wszystkich certyfikatów klienta wygenerowany podpisane przez hello certyfikat główny odwołane. Odwoływanie certyfikatu klienta, zamiast hello certyfikatu głównego, umożliwia hello innych certyfikatów, które zostały wygenerowane z hello głównego certyfikatu toocontinue toobe używany do uwierzytelniania dla połączenia hello punkt-lokacja.

Hello popularną praktyką jest toouse hello certyfikatu toomanage dostęp do konta root na poziomach zespół lub organizacja, używając cofnięte certyfikaty klienta dla szczegółowej kontroli dostępu na poszczególnych użytkowników.

### <a name="revokeclientcert"></a>toorevoke certyfikatu klienta

Dodając listy odwołania toohello odcisk palca hello można odwołać certyfikat klienta.

1. Pobrać hello odcisk palca certyfikatu klienta. Aby uzyskać więcej informacji, zobacz [porady: pobieranie hello odcisk palca certyfikatu](https://msdn.microsoft.com/library/ms734695.aspx).
2. Skopiuj Edytor tekstu tooa informacji hello i Usuń wszystkie spacje tak, aby ciąg.
3. Przejdź toohello **"klasycznego wirtualną nazwą sieciową" > połączenia sieci VPN typu punkt lokacja > Certyfikaty** a następnie kliknij przycisk **listy odwołania** strony listy odwołania hello tooopen. 
4. Na powitania **listy odwołania** kliknij przycisk **+ Dodaj certyfikat** tooopen hello **listy toorevocation certyfikatów Dodaj** strony.
5. Na powitania **listy toorevocation certyfikatów Dodaj** strony, Wklej odcisk palca certyfikatu hello jako pojedynczy wiersz ciągłego tekstu, nie może zawierać spacji. Kliknij przycisk **OK** u dołu hello hello strony.
6. Po zakończeniu aktualizowania hello certyfikatu nie można już tooconnect używane. Klienci, którzy spróbuj tooconnect przy użyciu tego certyfikatu wyświetlony komunikat z informacją, że ten certyfikat hello nie jest już prawidłowy.

## <a name="faq"></a>Często zadawane pytania dotyczące połączeń typu punkt-lokacja

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Następne kroki
Po zakończeniu połączenia można dodać sieci wirtualnych tooyour maszyn wirtualnych. Aby uzyskać więcej informacji, zobacz [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) (Maszyny wirtualne). toounderstand więcej informacji na temat sieci i maszyn wirtualnych, zobacz [omówienie sieci platformy Azure i maszyny Wirtualnej systemu Linux](../virtual-machines/linux/azure-vm-network-overview.md).
