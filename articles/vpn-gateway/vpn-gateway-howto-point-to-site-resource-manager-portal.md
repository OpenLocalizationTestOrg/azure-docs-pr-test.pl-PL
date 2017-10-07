---
title: "Połącz komputer tooa sieć wirtualną przy użyciu punkt-lokacja i uwierzytelnianie certyfikatu: Azure Portal | Dokumentacja firmy Microsoft"
description: "Bezpieczne łączenie z tooyour komputera sieci wirtualnej platformy Azure, tworząc połączenie bramy sieci VPN typu punkt-lokacja używa wstępnego uwierzytelniania certyfikatu. Ten artykuł dotyczy modelu wdrażania usługi Resource Manager toohello i używa hello portalu Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a15ad327-e236-461f-a18e-6dbedbf74943
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: 1419d6b4c160140b62d656b25bd02f6af7fd6655
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-azure-portal"></a>Skonfiguruj tooa połączenie punkt-lokacja sieci wirtualnej przy użyciu uwierzytelniania certyfikatów: Azure portal

W tym artykule opisano, jak toocreate sieci wirtualnej za pomocą połączenia punkt-lokacja za pomocą modelu wdrażania usługi Resource Manager hello hello portalu Azure. Ta konfiguracja korzysta z certyfikatów tooauthenticate hello połączenie klienta. Można również utworzyć tę konfigurację za pomocą narzędzia wdrażania różnych lub model wdrożenia, wybierając inną opcję z hello następującej listy:

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Portal Azure (klasyczny)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

Brama sieci VPN typu punkt-lokacja (P2S) umożliwia tworzenie sieci wirtualnej tooyour bezpiecznego połączenia z pojedynczym komputerem klienckim. Połączenia sieci VPN punkt-lokacja są przydatne, gdy chcesz tooyour tooconnect sieci wirtualnej z lokalizacji zdalnej, takie, gdy są Niezale¿nie z domu lub konferencji. P2S sieci VPN jest również toouse przydatne rozwiązanie, zamiast VPN lokacja-lokacja, jeśli istnieje tylko kilka klientów, którzy potrzebują tooa tooconnect sieci wirtualnej. 

Używa P2S hello gniazda Tunelowanie protokołu SSTP (Secure), która jest oparta na protokole SSL protokołu sieci VPN. Uruchamiając go z komputera klienckiego hello jest nawiązywane połączenie sieci VPN P2S.

![Diagram: połączenie typu punkt-lokacja](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/point-to-site-connection-diagram.png)

Połączenia uwierzytelniania certyfikatów punkt-lokacja wymagają następujących hello:

* Brama sieci VPN oparta na trasie.
* Witaj klucz publiczny (plik cer) dla certyfikatu głównego, czyli tooAzure przekazane. Po przekazaniu plików certyfikatów hello jest uznawany za zaufany certyfikat i jest używany do uwierzytelniania.
* Certyfikat klienta, który jest generowany na podstawie certyfikatu głównego hello i zainstalowane na każdym komputerze klienckim, w którym będą łączyć toohello sieci wirtualnej. Ten certyfikat jest używany do uwierzytelniania klientów.
* Pakiet konfiguracji klienta sieci VPN. Pakiet konfiguracji klienta VPN Hello zawiera hello informacji niezbędnych do powitania klienta tooconnect toohello sieci wirtualnej. Pakiet HELLO konfiguruje hello istniejącej sieci VPN klienta, który jest natywny toohello systemu operacyjnego Windows. Każdy klient, który łączy muszą być skonfigurowane przy użyciu hello konfiguracji pakietu.

Połączenia typu punkt-lokacja nie wymagają urządzenia sieci VPN ani lokalnego publicznego adresu IP. Witaj połączenia sieci VPN jest tworzony za pośrednictwem protokołu SSTP (Secure Socket Tunneling Protocol). Na powitania po stronie serwera firma Microsoft obsługuje protokół SSTP w wersji 1.0, 1.1 i 1.2. powitania klienta decyduje o tym, które toouse wersji. W przypadku systemu Windows 8.1 i nowszych protokół SSTP domyślnie używa wersji 1.2.

Aby uzyskać więcej informacji na temat połączenia punkt-lokacja, zobacz hello [punkt-lokacja często zadawane pytania dotyczące](#faq) na końcu hello w tym artykule.

#### <a name="example"></a>Przykładowe wartości

Można użyć hello następujące wartości toocreate środowiska testowego lub można znaleźć wartości toothese toobetter zrozumieć hello przykłady w tym artykule:

* **Nazwa sieci wirtualnej:** VNet1
* **Przestrzeń adresowa:** 192.168.0.0/16<br>W tym przykładzie zostanie wykorzystana tylko jedna przestrzeń adresowa. Istnieje możliwość użycia więcej niż jednej przestrzeni adresowej dla sieci wirtualnej.
* **Nazwa podsieci:** FrontEnd
* **Zakres adresów podsieci:** 192.168.1.0/24
* **Subskrypcja:** Jeśli masz więcej niż jedną subskrypcję, sprawdź, czy używasz hello właściwy.
* **Grupa zasobów:** TestRG
* **Lokalizacja:** Wschodnie stany USA
* **GatewaySubnet:** 192.168.200.0/24<br>
* **Serwer DNS:** (opcjonalnie) adres IP serwera DNS hello mają toouse do rozpoznawania nazw.
* **Nazwa bramy sieci wirtualnej:** VNet1GW
* **Typ bramy:** VPN
* **Typ sieci VPN:** oparta na trasach
* **Publiczny adres IP:** VNet1GWpip
* **Typ połączenia:** Punkt-lokacja
* **Pula adresów klienta:** 172.16.201.0/24<br>Klienci sieci VPN, łączący toohello sieci wirtualnej za pomocą to połączenie punkt-lokacja otrzymywać adresy IP z puli adresów powitania klienta.

## <a name="createvnet"></a>1. Tworzenie sieci wirtualnej

Przed rozpoczęciem sprawdź, czy masz subskrypcję platformy Azure. Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial).

[!INCLUDE [Basic Point-to-Site VNet](../../includes/vpn-gateway-basic-p2s-vnet-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>2. Dodawanie podsieci bramy

Przed połączeniem tooa bramy sieci wirtualnej, należy najpierw podsieci bramy hello toocreate hello toowhich sieć wirtualna ma zostać tooconnect. usługi bramy Hello używać hello adresami IP określonymi w hello podsieci bramy. Jeśli to możliwe, Utwórz podsieć bramy przy użyciu blok CIDR /28 lub /27 tooprovide adresów IP za mało, tooaccommodate dodatkowych przyszłych wymagań konfiguracyjnych.

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-p2s-rm-portal-include.md)]

## <a name="dns"></a>3. Określanie serwera DNS (opcjonalne)

Po utworzeniu sieci wirtualnej, można dodać hello adres IP serwera toohandle nazwę DNS. Serwer DNS Hello jest opcjonalne dla tej konfiguracji, ale wymagane, jeśli rozpoznawania nazw. Określenie wartości nie powoduje utworzenia nowego serwera DNS. Witaj adres IP serwera DNS, który określisz powinna być serwera DNS, który może rozpoznawać nazwy hello hello zasoby, które są nawiązywane. W tym przykładzie użyliśmy prywatnego adresu IP, ale istnieje duże prawdopodobieństwo, że nie jest hello adres IP serwera DNS. Należy się toouse własne wartości.

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="creategw"></a>4. Tworzenie bramy sieci wirtualnej

[!INCLUDE [create-gateway](../../includes/vpn-gateway-add-gw-p2s-rm-portal-include.md)]

## <a name="generatecert"></a>5. Generowanie certyfikatów klienta

Certyfikaty są używane przez klientów Azure tooauthenticate łączenie tooa sieci wirtualnej za pośrednictwem połączenia sieci VPN typu punkt-lokacja. Po uzyskaniu certyfikatu głównego, możesz [przekazać](#uploadfile) hello tooAzure informacje o kluczu publicznym. certyfikat główny Hello jest następnie uznawany za "zaufanych" przez platformę Azure, dla połączenia za pośrednictwem sieci wirtualnej toohello P2S. Także wygenerować certyfikaty klienta z hello zaufanego certyfikatu głównego, a następnie zainstaluj je na każdym komputerze klienckim. certyfikat klienta na powitania jest używane tooauthenticate powitania klienta, gdy inicjują połączenia toohello sieci wirtualnej. 

### <a name="getcer"></a>1. Uzyskaj plik cer hello hello certyfikatu głównego

[!INCLUDE [root-certificate](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <a name="generateclientcert"></a>2. Generowanie certyfikatu klienta

[!INCLUDE [generate-client-cert](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="addresspool"></a>6. Dodaj pulę adresów powitania klienta

Pula adresów klienta Hello jest zakresu prywatnych adresów IP, które określisz. klientom Witaj, łączących się za pośrednictwem sieci VPN punkt-lokacja otrzymywać adresy IP z tego zakresu. Za pomocą zakresu prywatnych adresów IP, który nie nakłada się na hello lokalizacji lokalnej, która nawiązywanie połączenia z lub hello sieci wirtualnej, który ma tooconnect do.

1. Po utworzeniu bramy sieci wirtualnej hello Przejdź toohello **ustawienia** sekcji strony hello bramy sieci wirtualnej. W hello **ustawienia** kliknij **konfiguracjipunkt lokacja** tooopen hello **punkt do-— konfiguracja lokacji** strony.

  ![Strona połączenia typu punkt-lokacja](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/gatewayblade.png)
2. Na powitania **punkt do-— konfiguracja lokacji** strony, możesz usunąć hello automatycznie wypełnianej zakresu, a następnie dodaj hello zakresu prywatnych adresów IP, które mają toouse. Kliknij przycisk **zapisać** toovalidate i zapisać ustawienia hello.

  ![Pula adresów klienta](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/ipaddresspool.png)

## <a name="uploadfile"></a>7. Przekazywanie danych certyfikatu publicznego certyfikatu głównego hello

Po utworzeniu bramy hello, możesz przekazać hello informacje o kluczu publicznym dla tooAzure certyfikatu głównego hello. Po przekazaniu plików danych certyfikatu publicznego hello Azure może być używany tooauthenticate klientów, którzy zainstalowali generowane na podstawie hello zaufanego certyfikatu głównego certyfikatu klienta. Możesz przekazać łącznie tooa up certyfikatów zaufanych głównych 20.

1. Certyfikaty są dodawane na powitania **konfiguracjępunktuwitryny** strony w hello **certyfikat główny** sekcji.  
2. Upewnij się, wyeksportowany certyfikat główny hello, zgodnie z algorytmem Base-64 pliku X.509 (.cer). Wymagany jest certyfikat hello tooexport w następującym formacie, możesz otworzyć hello certyfikatu za pomocą edytora tekstu.
3. Otwórz hello certyfikatu za pomocą edytora tekstu, takiego jak Notatnik. Kopiowanie danych certyfikatu hello, upewnij się, że możesz skopiować tekst hello jako pojedynczy wiersz ciągłego bez powrotu karetki i nowego wiersza. Toomodify może być konieczne widoku w too'Show Edytor tekstu hello Symbol/Pokaż wszystkie znaki toosee hello karetki zwraca i wiersz źródła danych. Skopiuj hello tylko po sekcji jako pojedynczy wiersz ciągłego:

  ![Dane dotyczące certyfikatu](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/copycert.png)
4. Wklej dane certyfikatu hello do hello **danych certyfikatu publicznego** pola. **Nazwa** hello certyfikatu, a następnie kliknij przycisk **zapisać**. Możesz dodać zapasowej too20 zaufanych certyfikatów głównych.

  ![Przekazywanie certyfikatu](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/rootcertupload.png)

## <a name="clientconfig"></a>8. Generowanie i zainstalować pakiet konfiguracji klienta VPN hello

tooa tooconnect sieci wirtualnej za pomocą sieci VPN punkt-lokacja, każdego klienta należy zainstalować pakiet konfiguracji klienta, który konfiguruje hello natywny klient VPN przy hello ustawień i plików, które są niezbędne tooconnect toohello wirtualnej sieci. natywny klient VPN systemu Windows hello konfiguruje pakietu konfiguracji klienta VPN Hello, nie instaluje nowe lub inne klienta sieci VPN.

Tak długo, jak wersja hello zgodna architektura hello powitania klienta, można użyć hello pakietu tej samej konfiguracji klienta sieci VPN na każdym komputerze klienckim. Aby hello listę systemów operacyjnych klienta, które są obsługiwane, zobacz hello [połączeńpunkt-lokacja często zadawane pytania dotyczące](#faq) na końcu hello w tym artykule.

### <a name="step-1---generate-and-download-hello-client-configuration-package"></a>Krok 1 — Generowanie i Pobierz pakiet konfiguracji powitania klienta

1. Na powitania **konfiguracjępunktuwitryny** kliknij przycisk **klienta VPN Pobierz** tooopen hello **klienta VPN Pobierz** strony. Trwa minutę lub dwie na powitania toogenerate pakietu.

  ![Pobieranie klienta VPN — sposób 1](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/downloadvpnclient1.png)
2. Wybierz pakiet poprawne powitania klienta, a następnie kliknij przycisk **Pobierz**. Zapisz plik pakietu konfiguracji hello. Pakiet konfiguracji klienta VPN hello należy zainstalować na każdym komputerze klienckim, łączącego toohello sieci wirtualnej.

  ![Pobieranie klienta VPN — sposób 2](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/vpnclient.png)

### <a name="step-2---install-hello-client-configuration-package"></a>Krok 2 — pakiet konfiguracji klienta hello instalacji

1. Plik konfiguracji hello kopiowania lokalnie toohello komputera, które mają sieci wirtualnej tooyour tooconnect. 
2. Kliknij dwukrotnie pakiet pliku .exe hello hello tooinstall na komputerze klienckim hello. Ponieważ utworzono pakiet konfiguracji hello, nie jest podpisany i mogą pojawić się ostrzeżenie. Jeśli otrzymasz wyskakujące okienko filtru Windows SmartScreen, kliknij przycisk **więcej informacji o** (po lewej stronie powitania), następnie **Uruchom mimo to** tooinstall hello pakietu.
3. Zainstaluj pakiet hello na komputerze klienckim hello. Jeśli otrzymasz wyskakujące okienko filtru Windows SmartScreen, kliknij przycisk **więcej informacji o** (po lewej stronie powitania), następnie **Uruchom mimo to** tooinstall hello pakietu.
4. Na komputerze klienckim hello Przejdź zbyt**ustawienia sieciowe** i kliknij przycisk **VPN**. Witaj połączenia sieci VPN jest wyświetlana nazwa hello hello sieci wirtualnej, która łączy się z.

## <a name="installclientcert"></a>9. Instalowanie wyeksportowanego certyfikatu klienta

Jeśli chcesz toocreate P2S połączenie z komputera klienckiego niż hello jeden używane certyfikaty klienta na powitania toogenerate należy tooinstall certyfikat klienta. Podczas instalowania certyfikatu klienta, należy hello hasło, które utworzono podczas eksportowania hello certyfikatu klienta. Zazwyczaj jest wystarczy dwukrotnie hello certyfikatu i instalując je.

Upewnij się, że certyfikat klienta na powitania została wyeksportowana do pliku PFX oraz hello całego łańcucha certyfikatów (który jest domyślnym hello). W przeciwnym razie informacje o certyfikacie głównym hello nie jest obecny na komputerze klienckim hello i powitania klienta nie będzie możliwe tooauthenticate poprawnie. Aby uzyskać więcej informacji, zobacz [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install) (Instalowanie wyeksportowanego certyfikatu klienta).

## <a name="connect"></a>10. Połącz tooAzure

1. tooconnect tooyour sieci wirtualnej, na komputerze klienckim hello Przejdź tooVPN połączeń i Znajdź hello połączenia sieci VPN, który został utworzony. Nazwie hello sama nazwa jak sieci wirtualnej. Kliknij przycisk **Połącz**. Komunikat podręczny może pojawić się odwołuje się toousing hello certyfikatu. Kliknij przycisk **Kontynuuj** toouse podwyższonego poziomu uprawnień.

2. Na powitania **połączenia** stan strony, kliknij przycisk **Connect** toostart hello połączenia. Jeśli widzisz **wybierz certyfikat** ekranu, sprawdź, czy powitania klienta certyfikatu przedstawiający hello jedną, które mają toouse tooconnect. Jeśli nie, hello strzałkę listy rozwijanej tooselect hello poprawny certyfikat, a następnie kliknij przycisk **OK**.

  ![Klient sieci VPN łączy tooAzure](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/clientconnect.png)
3. Połączenie zostało ustanowione.

  ![Ustanowiono połączenie](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>Rozwiązywanie problemów dotyczących połączeń typu punkt-lokacja

[!INCLUDE [verifies client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <a name="verify"></a>11. Weryfikowanie połączenia

1. tooverify, że połączenie sieci VPN jest aktywne, otwórz wiersz polecenia z podwyższonym poziomem uprawnień i uruchom *ipconfig/all*.
2. Wyświetl wyniki hello. Zauważ, że adres IP hello otrzymany jest jeden hello adresów w puli adresów klienta sieci VPN hello punkt-lokacja, określona w konfiguracji. wyniki Hello są podobny przykład toothis:

  ```
  PPP adapter VNet1:
      Connection-specific DNS Suffix .:
      Description.....................: VNet1
      Physical Address................:
      DHCP Enabled....................: No
      Autoconfiguration Enabled.......: Yes
      IPv4 Address....................: 172.16.201.3(Preferred)
      Subnet Mask.....................: 255.255.255.255
      Default Gateway.................:
      NetBIOS over Tcpip..............: Enabled
  ```

## <a name="connectVM"></a>Połącz tooa maszyny wirtualnej

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <a name="add"></a>Dodawanie lub usuwanie zaufanych certyfikatów głównych

Zaufane certyfikaty główne można dodawać do platformy Azure lub z niej usuwać. Po usunięciu certyfikatu głównego, nie będzie możliwe tooauthenticate klientów, którzy mają certyfikat, który został wygenerowany z elementem głównym, a w związku z tym nie będą mogli tooconnect. Jeśli mają tooauthenticate klienta i połączyć, należy tooinstall nowego certyfikatu klienta generowane na podstawie certyfikatu głównego, który jest zaufany tooAzure (przekazanego).

### <a name="tooadd-a-trusted-root-certificate"></a>tooadd zaufanego certyfikatu głównego

Możesz dodać zapasowej too20 zaufanego głównego certyfikatu .cer pliki tooAzure. Aby uzyskać instrukcje, zobacz sekcję hello [przekazać z zaufanym certyfikatem głównym](#uploadfile) w tym artykule.

### <a name="tooremove-a-trusted-root-certificate"></a>tooremove zaufanego certyfikatu głównego

1. tooremove z zaufanym certyfikatem głównym, przejdź toohello **punkt lokacja konfiguracji** strony dla bramy sieci wirtualnej.
2. W hello **certyfikat główny** sekcji strony hello, zlokalizuj certyfikat hello, które mają tooremove.
3. Kliknij przycisk wielokropka hello dalej certyfikat toohello, a następnie kliknij przycisk "Usuń".

## <a name="revokeclient"></a>Odwoływanie certyfikatu klienta

Certyfikaty klienta można odwołać. certyfikat Hello listy odwołania umożliwia tooselectively odmowy połączenia punkt-lokacja, w oparciu o certyfikaty klienta. Różni się to od usuwania zaufanego certyfikatu głównego. Jeśli usuniesz .cer certyfikatu zaufanego głównego z platformy Azure, odwołuje hello dostępu dla wszystkich certyfikatów klienta wygenerowany podpisane przez hello certyfikat główny odwołane. Odwoływanie certyfikatu klienta, zamiast hello certyfikatu głównego, umożliwia hello innych certyfikatów, które zostały wygenerowane z hello głównego certyfikatu toocontinue toobe używany do uwierzytelniania.

Hello popularną praktyką jest toouse hello certyfikatu toomanage dostęp do konta root na poziomach zespół lub organizacja, używając cofnięte certyfikaty klienta dla szczegółowej kontroli dostępu na poszczególnych użytkowników.

### <a name="toorevoke-a-client-certificate"></a>toorevoke certyfikatu klienta

Dodając listy odwołania toohello odcisk palca hello można odwołać certyfikat klienta.

1. Pobrać hello odcisk palca certyfikatu klienta. Aby uzyskać więcej informacji, zobacz [jak tooretrieve hello odcisk palca certyfikatu](https://msdn.microsoft.com/library/ms734695.aspx).
2. Skopiuj Edytor tekstu tooa informacji hello i Usuń wszystkie spacje tak, aby ciąg.
3. Przejdź do bramy sieci wirtualnej toohello **punkt do-— konfiguracja lokacji** strony. Jest to hello tej samej stronie, który został użyty zbyt[przekazać z zaufanym certyfikatem głównym](#uploadfile).
4. W hello **odwołane certyfikaty** sekcji, wprowadź przyjazną nazwę certyfikatu hello (nazwa Pospolita certyfikatu hello toobe nie ma).
5. Skopiuj i Wklej hello odcisk palca ciąg toohello **odcisk palca** pola.
6. Odcisk palca Hello weryfikuje i jest automatycznie dodawany toohello listy odwołania. Zostanie wyświetlony na ekranie powitania tego hello aktualizuje listy. 
7. Po zakończeniu aktualizowania hello certyfikatu nie można już tooconnect używane. Klienci, którzy spróbuj tooconnect przy użyciu tego certyfikatu wyświetlony komunikat z informacją, że ten certyfikat hello nie jest już prawidłowy.

## <a name="faq"></a>Często zadawane pytania dotyczące połączeń typu punkt-lokacja

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Następne kroki
Po zakończeniu połączenia można dodać sieci wirtualnych tooyour maszyn wirtualnych. Aby uzyskać więcej informacji, zobacz [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) (Maszyny wirtualne). toounderstand więcej informacji na temat sieci i maszyn wirtualnych, zobacz [omówienie sieci platformy Azure i maszyny Wirtualnej systemu Linux](../virtual-machines/linux/azure-vm-network-overview.md).
