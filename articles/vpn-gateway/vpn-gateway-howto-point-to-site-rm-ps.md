---
title: "Połącz tooan komputera przy użyciu punkt-lokacja sieci wirtualnej platformy Azure i certyfikat uwierzytelniania: programu PowerShell | Dokumentacja firmy Microsoft"
description: "Bezpiecznego łączenia z sieci wirtualnej tooyour komputera, tworząc połączenie bramy sieci VPN typu punkt-lokacja używa wstępnego uwierzytelniania certyfikatu. Ten artykuł dotyczy modelu wdrażania usługi Resource Manager toohello i korzysta z programu PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3eddadf6-2e96-48c4-87c6-52a146faeec6
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: b962e4b1946a4ae17d4eb2b920ed54437bc26b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-powershell"></a>Skonfiguruj tooa połączenie punkt-lokacja sieci wirtualnej przy użyciu uwierzytelniania certyfikatów: środowiska PowerShell

W tym artykule opisano, jak toocreate sieci wirtualnej za pomocą połączenia punkt-lokacja we wdrożeniu usługi Resource Manager hello modelu przy użyciu programu PowerShell. Ta konfiguracja korzysta z certyfikatów tooauthenticate hello połączenie klienta. Można również utworzyć tę konfigurację za pomocą narzędzia wdrażania różnych lub model wdrożenia, wybierając inną opcję z hello następującej listy:

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Portal Azure (klasyczny)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

Brama sieci VPN typu punkt-lokacja (P2S) umożliwia tworzenie sieci wirtualnej tooyour bezpiecznego połączenia z pojedynczym komputerem klienckim. Połączenia sieci VPN punkt-lokacja są przydatne, gdy chcesz tooyour tooconnect sieci wirtualnej z lokalizacji zdalnej, takie, gdy są Niezale¿nie z domu lub konferencji. P2S sieci VPN jest również toouse przydatne rozwiązanie, zamiast VPN lokacja-lokacja, jeśli istnieje tylko kilka klientów, którzy potrzebują tooa tooconnect sieci wirtualnej.

Używa P2S hello gniazda Tunelowanie protokołu SSTP (Secure), która jest oparta na protokole SSL protokołu sieci VPN. Uruchamiając go z komputera klienckiego hello jest nawiązywane połączenie sieci VPN P2S.

![Połącz komputer tooan sieci wirtualnej Azure - diagram połączenie punkt-lokacja](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

Połączenia uwierzytelniania certyfikatów punkt-lokacja wymagają następujących hello:

* Brama sieci VPN oparta na trasie.
* Witaj klucz publiczny (plik cer) dla certyfikatu głównego, czyli tooAzure przekazane. Po przekazaniu plików certyfikatów hello jest uznawany za zaufany certyfikat i jest używany do uwierzytelniania.
* Certyfikat klienta, który jest generowany na podstawie certyfikatu głównego hello i zainstalowane na każdym komputerze klienckim, w którym będą łączyć toohello sieci wirtualnej. Ten certyfikat jest używany do uwierzytelniania klientów.
* Pakiet konfiguracji klienta sieci VPN. Pakiet konfiguracji klienta VPN Hello zawiera hello informacji niezbędnych do powitania klienta tooconnect toohello sieci wirtualnej. Pakiet HELLO konfiguruje hello istniejącej sieci VPN klienta, który jest natywny toohello systemu operacyjnego Windows. Każdy klient, który łączy muszą być skonfigurowane przy użyciu hello konfiguracji pakietu.

Połączenia typu punkt-lokacja nie wymagają urządzenia sieci VPN ani lokalnego publicznego adresu IP. Witaj połączenia sieci VPN jest tworzony za pośrednictwem protokołu SSTP (Secure Socket Tunneling Protocol). Na powitania po stronie serwera firma Microsoft obsługuje protokół SSTP w wersji 1.0, 1.1 i 1.2. powitania klienta decyduje o tym, które toouse wersji. W przypadku systemu Windows 8.1 i nowszych protokół SSTP domyślnie używa wersji 1.2. 

Aby uzyskać więcej informacji na temat połączenia punkt-lokacja, zobacz hello [punkt-lokacja często zadawane pytania dotyczące](#faq) na końcu hello w tym artykule.

## <a name="before-beginning"></a>Przed rozpoczęciem

* Sprawdź, czy masz subskrypcję platformy Azure. Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial).
* Zainstaluj najnowszą wersję hello hello poleceń cmdlet programu PowerShell usługi Azure Resource Manager. Aby uzyskać więcej informacji na temat instalacji poleceń cmdlet programu PowerShell, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

### <a name="example"></a>Przykładowe wartości

Można użyć hello przykładowe wartości toocreate środowiska testowego lub można znaleźć wartości toothese toobetter zrozumieć hello przykłady w tym artykule. Firma Microsoft Ustaw zmienne hello w sekcji [1](#declare) hello artykułu. Można użyć kroki hello jako przewodnika i użyj wartości hello bez konieczności ich zmieniania lub je zmienić tooreflect środowiska. 

* **Nazwa: VNet1**
* **Przestrzeń adresowa: 192.168.0.0/16** i **10.254.0.0/16**<br>W tym przykładzie używamy więcej niż jeden tooillustrate przestrzeni adresów ta konfiguracja działa wiele przestrzeni adresowych. Jednak ta konfiguracja nie wymaga wielu przestrzeni adresowych.
* **Nazwa podsieci: FrontEnd**
  * **Zakres adresów podsieci: 192.168.1.0/24**
* **Nazwa podsieci: BackEnd**
  * **Zakres adresów podsieci: 10.254.1.0/24**
* **Nazwa podsieci: GatewaySubnet**<br>Nazwa podsieci Hello *GatewaySubnet* jest obowiązkowa w przypadku toowork bramy sieci VPN hello.
  * **Zakres adresów podsieci bramy: 192.168.200.0/24** 
* **Pula adresów klienta sieci VPN: 172.16.201.0/24**<br>Klienci sieci VPN, łączący toohello sieci wirtualnej za pomocą to połączenie punkt-lokacja otrzymywać adresy IP z hello pula adresów klienta sieci VPN.
* **Subskrypcja:** Jeśli masz więcej niż jedną subskrypcję, sprawdź, czy używasz hello właściwy.
* **Grupa zasobów: TestRG**
* **Lokalizacja: Wschodnie stany USA**
* **Serwera DNS: Adres IP** powitania serwera DNS ma toouse do rozpoznawania nazw.
* **Nazwa bramy: Vnet1GW**
* **Nazwa publicznego adresu IP: VNet1GWPIP**
* **VpnType: RouteBased** 

## <a name="declare"></a>1. Logowanie się i ustawianie zmiennych

W tej sekcji Zaloguj się i zadeklarować hello wartości używanych dla tej konfiguracji. Witaj zadeklarowane jako wartości są używane w hello przykładowe skrypty. Zmień tooreflect wartości hello własnego środowiska. Lub użyj hello zadeklarowany wartości i wykonanie kroków hello jako wykonywania.

1. Otwórz konsolę programu PowerShell z podwyższonym poziomem uprawnień i logowania tooyour konto platformy Azure. To polecenie cmdlet monituje o poświadczenia logowania hello. Po zalogowaniu pobraniu ustawienia konta, aby były dostępne tooAzure środowiska PowerShell.

  ```powershell
  Login-AzureRmAccount
  ```
2. Pobierz listę subskrypcji platformy Azure.

  ```powershell
  Get-AzureRmSubscription
  ```
3. Określ, które mają toouse subskrypcji hello.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. Zadeklaruj zmienne hello, które mają toouse. Użyj hello następujące przykładowe, zastępując hello własne wartości gdy jest to konieczne.

  ```powershell
  $VNetName  = "VNet1"
  $FESubName = "FrontEnd"
  $BESubName = "Backend"
  $GWSubName = "GatewaySubnet"
  $VNetPrefix1 = "192.168.0.0/16"
  $VNetPrefix2 = "10.254.0.0/16"
  $FESubPrefix = "192.168.1.0/24"
  $BESubPrefix = "10.254.1.0/24"
  $GWSubPrefix = "192.168.200.0/26"
  $VPNClientAddressPool = "172.16.201.0/24"
  $RG = "TestRG"
  $Location = "East US"
  $DNS = "10.1.1.3"
  $GWName = "VNet1GW"
  $GWIPName = "VNet1GWPIP"
  $GWIPconfName = "gwipconf"
  ```

## <a name="ConfigureVNet"></a>2. Konfigurowanie sieci wirtualnej

1. Utwórz grupę zasobów.

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. Utwórz hello konfiguracje podsieci sieci wirtualnej hello, ich nazewnictwa *frontonu*, *zaplecza*, i *GatewaySubnet*. Te prefiksy muszą być częścią hello przestrzeni adresowej sieci wirtualnej, która została zadeklarowana.

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. Utwórz sieć wirtualną hello.

  W tym przykładzie powitania serwera DNS jest opcjonalny. Określenie wartości nie powoduje utworzenia nowego serwera DNS. Witaj adres IP serwera DNS, który określisz powinna być serwera DNS, który może rozpoznawać nazwy hello hello zasoby, które są nawiązywane. W tym przykładzie użyliśmy prywatnego adresu IP, ale istnieje duże prawdopodobieństwo, że nie jest hello adres IP serwera DNS. Należy się toouse własne wartości.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. Określ zmienne hello hello sieci wirtualnej, który został utworzony.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. Brama sieci VPN musi mieć publiczny adres IP. Najpierw zażądać zasobu adresu IP hello i odwoływać się tooit podczas tworzenia bramy sieci wirtualnej. adres IP Hello jest przypisywane dynamicznie toohello zasobów, po utworzeniu bramy sieci VPN hello. Brama sieci VPN aktualnie obsługuje tylko *dynamiczne* przypisywanie publicznych adresów IP. Nie można zażądać przypisania statycznego publicznego adresu IP. Jednak nie oznacza, że adres IP hello ulegnie zmianie po przypisaniu tooyour bramy sieci VPN. Hello czasu tylko zmiany adresu publicznego adresu IP hello jest po hello bramy zostanie usunięta i utworzona ponownie. Nie zmienia się on w przypadku zmiany rozmiaru, zresetowania ani przeprowadzania innych wewnętrznych czynności konserwacyjnych bądź uaktualnień bramy sieci VPN.

  Zażądaj dynamicznie przydzielanego publicznego adresu IP.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <a name="creategateway"></a>3. Tworzenie bramy sieci VPN hello

Skonfiguruj i Utwórz bramę sieci wirtualnej hello sieci wirtualnej.

* Witaj *elementu GatewayType -* musi być **Vpn** i hello *- VpnType* musi być **RouteBased**.
* Brama sieci VPN może potrwać too45 toocomplete minut, w zależności od hello [jednostka sku bramy](vpn-gateway-about-vpn-gateway-settings.md) wybrania.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <a name="addresspool"></a>4. Dodaj pulę adresów klienta sieci VPN hello

Po zakończeniu tworzenia bramy sieci VPN hello można dodać puli adresów klienta sieci VPN hello. Hello pula adresów klienta sieci VPN jest zakres hello, z których klienci VPN hello otrzymywać adresu IP podczas nawiązywania połączenia. Użyj zakresu prywatnych adresów IP, który nie nakłada się na hello lokalizacji lokalnej, która nawiązywanie połączenia z lub hello sieci wirtualnej, który ma tooconnect do. W tym przykładzie hello pula adresów klienta sieci VPN jest zadeklarowany jako [zmiennej](#declare) w kroku 1.

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <a name="Certificates"></a>5. Generowanie certyfikatów klienta

Certyfikaty są używane przez klientów sieci VPN platformy Azure tooauthenticate sieci VPN punkt-lokacja. Możesz przekazać hello informacje o kluczu publicznym z tooAzure certyfikatu głównego hello. klucz publiczny Hello następnie jest uznawany za "zaufanych". Certyfikaty klienta musi generowane na podstawie hello zaufanego certyfikatu głównego, a następnie zainstalowany na każdym komputerze klienckim w hello certyfikatów bieżącego użytkownika/osobistego magazynu certyfikatów. certyfikatu Hello jest używane tooauthenticate powitania klienta, gdy inicjują połączenia toohello sieci wirtualnej. 

Jeśli używasz certyfikatów z podpisem własnym, należy je utworzyć przy użyciu określonych parametrów. Można utworzyć certyfikatu z podpisem własnym za pomocą instrukcji hello [środowiska PowerShell i Windows 10](vpn-gateway-certificates-point-to-site.md), lub jeśli nie masz systemu Windows 10, możesz użyć [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md). Jest ważne, należy wykonać kroki hello w instrukcjach hello podczas generowania certyfikatów głównych z podpisem własnym i certyfikatów klientów. W przeciwnym razie nie będzie zgodny z połączeń P2S hello certyfikaty, które można wygenerować i zostanie wyświetlony błąd połączenia.

### <a name="cer"></a>1. Uzyskaj plik cer hello hello certyfikatu głównego

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <a name="generate"></a>2. Generowanie certyfikatu klienta

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="upload"></a>6. Przekaż hello głównego certyfikatu informacje o kluczu publicznym

Upewnij się, że zakończono tworzenie bramy VPN Gateway. Po zakończeniu, możesz przekazać plik .cer hello, (zawierający informacje o kluczu publicznym hello) dla tooAzure certyfikatów zaufanych certyfikatów głównych. Po przekazaniu pliku a.cer Azure może być używany tooauthenticate klientów, którzy zainstalowali generowane na podstawie hello zaufanego certyfikatu głównego certyfikatu klienta. Możesz przekazać pliki certyfikatów zaufanych głównych - zapasowej tooa łącznie 20 - później, w razie potrzeby.

1. Zadeklarować zmienną hello nazwy certyfikatu, zastępując wartość hello własne.

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. Zamień na ścieżkę pliku hello własnych, a następnie uruchom polecenia cmdlet hello.

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. Przekaż hello tooAzure informacje o kluczu publicznym. Po przekazaniu informacji o certyfikacie hello Azure uwzględnia ten toobe z zaufanym certyfikatem głównym.

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <a name="clientconfig"></a>7. Pobierz pakiet konfiguracji klienta sieci VPN hello

tooa tooconnect sieci wirtualnej za pomocą sieci VPN punkt-lokacja, każdego klienta należy zainstalować pakiet konfiguracji klienta, który konfiguruje hello natywny klient VPN przy hello ustawień i plików, które są niezbędne tooconnect toohello wirtualnej sieci. natywny klient VPN systemu Windows hello konfiguruje pakietu konfiguracji klienta VPN Hello, nie instaluje nowe lub inne klienta sieci VPN. 

Tak długo, jak wersja hello zgodna architektura hello powitania klienta, można użyć hello pakietu tej samej konfiguracji klienta sieci VPN na każdym komputerze klienckim. Aby hello listę systemów operacyjnych klienta, które są obsługiwane, zobacz hello [połączeńpunkt-lokacja często zadawane pytania dotyczące](#faq) na końcu hello w tym artykule.

1. Po utworzeniu bramy hello, można wygenerować i pobrać pakiet konfiguracji powitania klienta. W tym przykładzie pliki do pobrania pakietu hello na klientach 64-bitowych. Jeśli chcesz toodownload hello 32-bitowego klienta, zastąp "Amd64" "x86". Możesz również pobrać powitania klienta VPN za pomocą hello portalu Azure.

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. Skopiuj i Wklej łącze hello jest zwracany tooa pakiet przeglądarki sieci web toodownload hello, zwracając szczególną uwagę cudzysłowy hello tooremove otaczającego hello łącza. 
3. Pobierz i zainstaluj pakiet hello na komputerze klienckim hello. Jeśli zostanie wyświetlone okno podręczne SmartScreen, kliknij pozycję **Więcej informacji**, a następnie pozycję **Uruchom mimo to**. Można także zapisać tooinstall pakietu hello na innych komputerach klienckich.
4. Na komputerze klienckim hello Przejdź zbyt**ustawienia sieciowe** i kliknij przycisk **VPN**. Witaj połączenia sieci VPN jest wyświetlana nazwa hello hello sieci wirtualnej, która łączy się z.

## <a name="clientcertificate"></a>8. Instalowanie wyeksportowanego certyfikatu klienta

Jeśli chcesz toocreate P2S połączenie z komputera klienckiego niż hello jeden używane certyfikaty klienta na powitania toogenerate należy tooinstall certyfikat klienta. Podczas instalowania certyfikatu klienta, należy hello hasło, które utworzono podczas eksportowania hello certyfikatu klienta. Zazwyczaj jest wystarczy dwukrotnie hello certyfikatu i instalując je.

Upewnij się, że certyfikat klienta na powitania została wyeksportowana do pliku PFX oraz hello całego łańcucha certyfikatów (który jest domyślnym hello). W przeciwnym razie informacje o certyfikacie głównym hello nie jest obecny na komputerze klienckim hello i powitania klienta nie będzie możliwe tooauthenticate poprawnie. Aby uzyskać więcej informacji, zobacz [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install) (Instalowanie wyeksportowanego certyfikatu klienta). 

## <a name="connect"></a>9. Połącz tooAzure

1. tooconnect tooyour sieci wirtualnej, na komputerze klienckim hello Przejdź tooVPN połączeń i Znajdź hello połączenia sieci VPN, który został utworzony. Nazwie hello sama nazwa jak sieci wirtualnej. Kliknij przycisk **Połącz**. Komunikat podręczny może pojawić się odwołuje się toousing hello certyfikatu. Kliknij przycisk **Kontynuuj** toouse podwyższonego poziomu uprawnień. 
2. Na powitania **połączenia** stan strony, kliknij przycisk **Connect** toostart hello połączenia. Jeśli widzisz **wybierz certyfikat** ekranu, sprawdź, czy powitania klienta certyfikatu przedstawiający hello jedną, które mają toouse tooconnect. Jeśli nie, hello strzałkę listy rozwijanej tooselect hello poprawny certyfikat, a następnie kliknij przycisk **OK**.

  ![Klient sieci VPN łączy tooAzure](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. Połączenie zostało ustanowione.

  ![Ustanowiono połączenie](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>Rozwiązywanie problemów dotyczących połączeń typu punkt-lokacja

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <a name="verify"></a>10. Weryfikowanie połączenia

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

## <a name="addremovecert"></a>Dodawanie lub usuwanie certyfikatu głównego

Zaufane certyfikaty główne można dodawać do platformy Azure lub z niej usuwać. Po usunięciu certyfikatu głównego, klientów, którzy mają certyfikat generowane na podstawie certyfikatu głównego hello nie mogą uwierzytelnić się i nie będzie możliwe tooconnect. Jeśli mają tooauthenticate klienta i połączyć, należy tooinstall nowego certyfikatu klienta generowane na podstawie certyfikatu głównego, który jest zaufany tooAzure (przekazanego).

### <a name="addtrustedroot"></a>tooadd zaufanego certyfikatu głównego

Możesz dodać zapasowej too20 głównego certyfikatu .cer pliki tooAzure. następujące Hello czynności pomocy dodać certyfikat główny:

#### <a name="certmethod1"></a>Metoda 1

Jest to hello najbardziej efektywny metody tooupload certyfikatu głównego.

1. Przygotuj tooupload pliku .cer hello:

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. Przekaż plik hello. Jednocześnie możesz przekazać tylko jeden plik.

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. tooverify przekazać ten plik certyfikatu hello:

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <a name="certmethod2"></a>Metoda 2

Ta metoda jest więcej czynności niż metoda 1, ale skonfigurowano hello takiego samego wyniku. Został uwzględniony w razie potrzeby tooview hello certyfikatu danych.

1. Tworzenie i przygotowanie hello tooAzure tooadd w nowego certyfikatu głównego. Wyeksportować klucz publiczny hello, ponieważ certyfikat x.509 szyfrowany algorytmem Base-64 (. CER), a następnie otwórz go w edytorze tekstów. Skopiuj wartości hello, jak pokazano w hello poniższy przykład:

  ![certyfikat](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > Kopiowanie danych certyfikatu hello, upewnij się, że możesz skopiować tekst hello jako pojedynczy wiersz ciągłego bez powrotu karetki i nowego wiersza. Toomodify może być konieczne widoku w too'Show Edytor tekstu hello Symbol/Pokaż wszystkie znaki toosee hello karetki zwraca i wiersz źródła danych.
  >
  >

2. Określ nazwę certyfikatu hello i informacje o kluczu jako zmienną. Zastąp informacje hello własny, jak pokazano na powitania w poniższym przykładzie:

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. Dodaj nowy certyfikat główny hello. Można dodawać tylko jeden certyfikat naraz.

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. Możesz sprawdzić, czy nowy certyfikat hello została poprawnie dodana przy użyciu hello poniższy przykład:

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <a name="removerootcert"></a>tooremove certyfikatu głównego

1. Zadeklaruj zmienne hello.

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. Usuń certyfikat hello.

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. Użyj powitania po tooverify przykład, który hello certyfikat został pomyślnie usunięty.

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <a name="revoke"></a>Odwoływanie certyfikatu klienta

Certyfikaty klienta można odwołać. certyfikat Hello listy odwołania umożliwia tooselectively odmowy połączenia punkt-lokacja, w oparciu o certyfikaty klienta. Różni się to od usuwania zaufanego certyfikatu głównego. Jeśli usuniesz .cer certyfikatu zaufanego głównego z platformy Azure, odwołuje hello dostępu dla wszystkich certyfikatów klienta wygenerowany podpisane przez hello certyfikat główny odwołane. Odwoływanie certyfikatu klienta, zamiast hello certyfikatu głównego, umożliwia hello innych certyfikatów, które zostały wygenerowane z hello głównego certyfikatu toocontinue toobe używany do uwierzytelniania.

Hello popularną praktyką jest toouse hello certyfikatu toomanage dostęp do konta root na poziomach zespół lub organizacja, używając cofnięte certyfikaty klienta dla szczegółowej kontroli dostępu na poszczególnych użytkowników.

### <a name="revokeclientcert"></a>toorevoke certyfikatu klienta

1. Pobrać hello odcisk palca certyfikatu klienta. Aby uzyskać więcej informacji, zobacz [jak tooretrieve hello odcisk palca certyfikatu](https://msdn.microsoft.com/library/ms734695.aspx).
2. Skopiuj Edytor tekstu tooa informacji hello i Usuń wszystkie spacje tak, aby ciąg. Ten ciąg jest zadeklarowana jako zmienna w hello następnego kroku.
3. Zadeklaruj zmienne hello. Upewnij się, że palca hello toodeclare, który można pobrać hello poprzedniego kroku.

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. Dodaj hello odcisk palca toohello listy odwołania certyfikatów. Po dodaniu hello odcisk palca zostanie wyświetlony "Powodzenie".

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. Sprawdź, czy że odcisk palca hello dodano listy odwołania certyfikatów toohello.

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. Po dodaniu hello odcisk palca certyfikatu hello nie można już tooconnect używane. Klienci, którzy spróbuj tooconnect przy użyciu tego certyfikatu wyświetlony komunikat z informacją, że ten certyfikat hello nie jest już prawidłowy.

### <a name="reinstateclientcert"></a>tooreinstate certyfikatu klienta

Certyfikat klienta można przywrócić przez usunięcie hello odcisk palca z listy hello odwołanych certyfikatów klientów.

1. Zadeklaruj zmienne hello. Upewnij się, że zadeklarować hello poprawne odcisk palca certyfikatu hello, które mają tooreinstate.

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. Usuń hello odcisk palca certyfikatu z listy odwołania certyfikatów hello.

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. Sprawdź, czy odcisku palca hello jest usuwany z hello odwołany listy.

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <a name="faq"></a>Często zadawane pytania dotyczące połączeń typu punkt-lokacja

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Następne kroki
Po zakończeniu połączenia można dodać sieci wirtualnych tooyour maszyn wirtualnych. Aby uzyskać więcej informacji, zobacz [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) (Maszyny wirtualne). toounderstand więcej informacji na temat sieci i maszyn wirtualnych, zobacz [omówienie sieci platformy Azure i maszyny Wirtualnej systemu Linux](../virtual-machines/linux/azure-vm-network-overview.md).
