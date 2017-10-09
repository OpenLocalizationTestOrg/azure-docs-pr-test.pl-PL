---
title: "Tworzenie połączenia między sieciami wirtualnymi: klasycznym: portalu Azure | Dokumentacja firmy Microsoft"
description: "Jak tooconnect Azure wirtualnych sieci ze sobą przy użyciu programu PowerShell i hello klasycznego portalu Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: f29c3c091d049ff96cf59f4c28ab86a100bcb5fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-connection-classic"></a>Konfigurowanie połączenia do wirtualnymi (klasyczne)

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

W tym artykule opisano sposób toocreate połączenie bramy sieci VPN między sieciami wirtualnymi. Witaj sieci wirtualne mogą być w hello tych samych lub różnych regionów, a z hello takie same lub różnych subskrypcji. czynności Hello w tym artykule dotyczą toohello klasycznego modelu wdrażania i hello portalu Azure. Można również utworzyć tę konfigurację za pomocą narzędzia wdrażania różnych lub model wdrożenia, wybierając inną opcję z hello następującej listy:

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Interfejs wiersza polecenia platformy Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Portal Azure (klasyczny)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Łączenie różnych modeli wdrażania — witryna Azure Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Łączenie różnych modeli wdrażania — program PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![Sieć wirtualna tooVNet Diagram łączności](./media/vpn-gateway-howto-vnet-vnet-portal-classic/v2vclassic.png)

## <a name="about-vnet-to-vnet-connections"></a>Informacje o połączeniach między sieciami wirtualnymi

Połączenie wirtualnej sieci tooanother sieci wirtualnej (aby wirtualnymi) w hello klasycznego modelu wdrażania przy użyciu bramy sieci VPN jest podobne tooconnecting lokalizacji sieci wirtualnej tooan lokalnej lokacji. Oba typy łączności Użyj tooprovide bramy sieci VPN przy użyciu protokołu IPsec/IKE bezpiecznego tunelu.

Hello łączenia sieci wirtualnych może być w różnych regionach i różnych subskrypcji. Można połączyć sieci wirtualnej tooVNet komunikacji z konfiguracjami obejmujący wiele lokacji. Pozwala to tworzyć topologie sieci, które łączą wdrożenia obejmujące wiele lokalizacji z połączeniami między sieciami wirtualnymi.

![Sieć wirtualna tooVNet połączeń](./media/vpn-gateway-howto-vnet-vnet-portal-classic/aboutconnections.png)

### <a name="why"></a>Dlaczego łączy się sieci wirtualne?

Warto sieci wirtualnych tooconnect hello z następujących powodów:

* **Niezależna od regionu nadmiarowość i obecność geograficzna**

  * Można tworzyć własne replikacje geograficzne lub przeprowadzać synchronizację z bezpiecznym połączeniem bez przechodzenia przez punkty końcowe dostępne z Internetu.
  * Z usługi równoważenia obciążenia Azure i firmy Microsoft lub innych technologii klastrowania można skonfigurować obciążenia wysokiej dostępności z nadmiarowość geograficzna w różnych regionach platformy Azure. Przykładem ważne jest tooset się SQL zawsze włączone grupy dostępności rozsyłanie się w różnych regionach platformy Azure.
* **Regionalne aplikacje wielowarstwowe z granicą silne izolacji**

  * Poziomu hello sam region, możesz skonfigurować aplikacje wielowarstwowe z wielu sieci wirtualnych połączone razem z silną izolacji i zapewnienia bezpiecznej komunikacji między warstwy.
* **Krzyżowe subskrypcji i komunikacji między organizacji na platformie Azure**

  * Jeśli masz wiele subskrypcji Azure, możesz połączyć obciążeń z różnych subskrypcji razem bezpiecznie między sieciami wirtualnymi.
  * Dla przedsiębiorstw i dostawców usług można włączyć komunikację między organizacji bezpiecznego technologii sieci VPN w systemie Azure.

Aby uzyskać więcej informacji o połączeniach sieci wirtualnej do sieci wirtualnej, zobacz [uwagi do wirtualnymi](#faq) na końcu hello w tym artykule.

### <a name="before-you-begin"></a>Przed rozpoczęciem

Przed rozpoczęciem tego ćwiczenia, Pobierz i zainstaluj najnowszą wersję hello hello poleceń cmdlet programu PowerShell Azure usługi zarządzania (ko). Aby uzyskać więcej informacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview). Używamy hello portal dla większości hello czynności, ale należy użyć programu PowerShell toocreate hello połączeń między sieciami wirtualnymi hello. Nie można utworzyć hello połączeń za pomocą hello portalu Azure.

## <a name="plan"></a>Krok 1 — Planowanie zakresów adresów IP

Jest ważne toodecide hello zakresy czy użyjesz tooconfigure sieci wirtualne. W przypadku tej konfiguracji, należy się upewnić, że żaden z zakresów w Twojej sieci wirtualnej nakłada się ze sobą lub za pomocą dowolnego z sieci lokalne powitania, które łączą się z.

Witaj poniższej tabeli przedstawiono przykładowy sposób toodefine Twojego sieci wirtualnych. Użyj zakresów hello tylko przyjąć. Zapisz hello zakresy dla sieci wirtualnej. Te informacje są niezbędne do wykonania kolejnych kroków.

**Przykład**

| Virtual Network | Przestrzeń adresów | Region | Łączy lokację sieciową toolocal |
|:--- |:--- |:--- |:--- |
| TestVNet1 |TestVNet1<br>(10.11.0.0/16)<br>(10.12.0.0/16) |Wschodnie stany USA |VNet4Local<br>(10.41.0.0/16)<br>(10.42.0.0/16) |
| TestVNet4 |TestVNet4<br>(10.41.0.0/16)<br>(10.42.0.0/16) |Zachodnie stany USA |VNet1Local<br>(10.11.0.0/16)<br>(10.12.0.0/16) |

## <a name="vnetvalues"></a>Krok 2 — Tworzenie hello sieci wirtualnych

Utwórz dwie sieci wirtualne w hello [portalu Azure](https://portal.azure.com). Aby hello kroki toocreate klasycznych sieci wirtualnych, zobacz [utworzyć sieć wirtualną klasycznego](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). 

Korzystając z portalu toocreate hello klasycznej sieci wirtualnej, musisz przejść toohello bloku sieci wirtualnej przy użyciu hello, wykonaj następujące kroki, w przeciwnym razie nie ma toocreate opcji hello klasycznej sieci wirtualnej:

1. Kliknij przycisk hello bloku "New" hello tooopen "+".
2. W polu "Marketplace wyszukiwania powitania" hello wpisz "Sieci wirtualnej". Jeśli zamiast tego należy wybrać sieć -> Sieć wirtualna, nie otrzymasz toocreate opcji hello klasycznej sieci wirtualnej.
3. Zlokalizuj "Sieci wirtualnej" z hello zwrócił listy i kliknij ją bloku sieci wirtualnej hello tooopen. 
4. W bloku sieci wirtualnej hello wybierz "Klasycznym" toocreate klasycznej sieci wirtualnej. 

Jeśli korzystasz z tego artykułu jako wykonywania, można użyć hello następujące przykładowe wartości:

**Wartości TestVNet1**

Nazwa: TestVNet1<br>
Przestrzeń adresowa: 10.11.0.0/16, 10.12.0.0/16 (opcjonalnie)<br>
Nazwa podsieci: domyślna<br>
Zakres adresów podsieci: 10.11.0.1/24<br>
Grupa zasobów: ClassicRG<br>
Lokalizacja: Wschodnie stany USA<br>
GatewaySubnet: 10.11.1.0/27

**Wartości TestVNet4**

Nazwa: TestVNet4<br>
Przestrzeń adresowa: 10.41.0.0/16, 10.42.0.0/16 (opcjonalnie)<br>
Nazwa podsieci: domyślna<br>
Zakres adresów podsieci: 10.41.0.1/24<br>
Grupa zasobów: ClassicRG<br>
Lokalizacja: West US<br>
GatewaySubnet: 10.41.1.0/27

**Podczas tworzenia sieci wirtualnych, należy pamiętać hello następujące ustawienia:**

* **Przestrzeniami adresów sieci wirtualnej** — na stronie powitania, przestrzeniami adresów sieci wirtualnej, określ zakres adresów hello mają toouse dla sieci wirtualnej. Są to hello dynamiczne adresy IP przypisane toohello maszyn wirtualnych i innych wystąpień roli wdrożenie toothis sieci wirtualnej.<br>adres Hello spacje, którą wybierzesz nie może nakładać się przestrzeni adresowych hello jakichkolwiek hello innych lokalizacji sieci wirtualnych lub lokalnymi łączących się tej sieci wirtualnej.

* **Lokalizacja** — po utworzeniu sieci wirtualnej, należy ją skojarzyć z lokalizacji platformy Azure (regionu). Na przykład jeśli chcesz sieci maszyn wirtualnych, które są wdrożone toobe sieci wirtualnej tooyour fizycznie znajduje się w zachodnie stany USA, wybierz tej lokalizacji. Nie można zmienić lokalizacji hello skojarzonej z sieci wirtualnej, po jego utworzeniu.

**Po utworzeniu Twojej sieci wirtualnych, można dodać hello następujące ustawienia:**

* **Przestrzeń adresowa** — dodatkową przestrzeń adresów nie jest wymagana dla tej konfiguracji, ale można dodać dodatkową przestrzeń adresów po utworzeniu hello sieci wirtualnej.

* **Podsieci** — dodatkowe podsieci nie są wymagane dla tej konfiguracji, ale może być toohave maszyn wirtualnych w podsieci, która jest oddzielona od innych wystąpień roli.

* **Serwery DNS** — wprowadź nazwę serwera DNS hello i adres IP. To ustawienie nie powoduje jednak utworzenia serwera DNS. Pozwala ona serwery DNS hello toospecify mają toouse do rozpoznawania nazw dla tej sieci wirtualnej.

W tej sekcji Skonfiguruj typ połączenia hello hello lokalnej witryny i utworzyć hello bramy.

## <a name="localsite"></a>Krok 3 — Konfigurowanie hello lokacji lokalnej

Hello Azure używane są ustawienia określone w każdej toodetermine lokacji sieci lokalnej, jak tooroute ruchu między sieciami wirtualnymi hello. Każdej sieci wirtualnej musi wskazywać toohello odpowiednich sieci lokalnej, które chcesz tooroute ruchu. Należy określić nazwę hello ma toouse toorefer tooeach sieci lokalnej lokacji. Jest najlepszym toouse coś opisowy.

Na przykład TestVNet1 łączy tooa sieci lokalnej witryny o nazwie "VNet4Local". Ustawienia Hello VNet4Local zawiera prefiksy adresów hello TestVNet4.

lokalne powitania lokacji dla każdej sieci wirtualnej jest hello innych sieci wirtualnej. następujące przykładowe wartości Hello są używane do naszej konfiguracji:

| Virtual Network | Przestrzeń adresów | Region | Łączy lokację sieciową toolocal |
|:--- |:--- |:--- |:--- |
| TestVNet1 |TestVNet1<br>(10.11.0.0/16)<br>(10.12.0.0/16) |Wschodnie stany USA |VNet4Local<br>(10.41.0.0/16)<br>(10.42.0.0/16) |
| TestVNet4 |TestVNet4<br>(10.41.0.0/16)<br>(10.42.0.0/16) |Zachodnie stany USA |VNet1Local<br>(10.11.0.0/16)<br>(10.12.0.0/16) |

1. Znajdź TestVNet1 w hello portalu Azure. W hello **połączeń sieci VPN** sekcji hello bloku, kliknij przycisk **bramy**.

    ![Brak bramy](./media/vpn-gateway-howto-vnet-vnet-portal-classic/nogateway.png)
2. Na powitania **nowego połączenia sieci VPN** wybierz pozycję **lokacja-lokacja**.
3. Kliknij przycisk **lokacji lokalnej** tooopen hello strony lokacji lokalnej i skonfiguruj ustawienia hello.
4. Na powitania **lokacji lokalnej** pozycję nazwy lokalnej witrynie. W naszym przykładzie nazywamy hello lokacji lokalnej "VNet4Local".
5. Aby uzyskać **adres IP bramy sieci VPN**, można użyć dowolnego adresu IP, który ma, tak długo, jak jest w nieprawidłowym formacie. Zazwyczaj użyje rzeczywiste zewnętrzny adres IP hello urządzenia sieci VPN. Jednak klasycznego konfiguracji sieci wirtualnej do sieci wirtualnej, użyj hello publicznego adresu IP przypisanego toohello bramy sieci wirtualnej. Biorąc pod uwagę, że nie została jeszcze utworzona hello bramy sieci wirtualnej, należy określić dowolnego prawidłowego publicznego adresu IP jako symbol zastępczy.<br>Nie wypełniaj tego pola to — nie jest opcjonalny w przypadku tej konfiguracji. W kolejnym kroku Przejdź wstecz do tych ustawień i skonfiguruj je z adresami IP bramy sieci wirtualnej hello odpowiednie, gdy platforma Azure generuje go.
6. Dla **przestrzeni adresowej klienta**, użyj przestrzeni adresowej hello hello innych sieci wirtualnej. Zobacz planowanie przykład tooyour. Kliknij przycisk **OK** toosave ustawień i zwracany wstecz toohello **nowego połączenia sieci VPN** bloku.

    ![lokacji lokalnej](./media/vpn-gateway-howto-vnet-vnet-portal-classic/localsite.png)

## <a name="gw"></a>Krok 4 — Utwórz bramę sieci wirtualnej hello

Każda sieć wirtualna musi mieć bramy sieci wirtualnej. Brama sieci wirtualnej Hello trasy i szyfruje ruch.

1. Na powitania **nowego połączenia sieci VPN** bloku, hello zaznacz pole wyboru **Utwórz bramę natychmiast**.
2. Kliknij przycisk **podsieć, rozmiar i typ routingu**. Na powitania **konfiguracji bramy** bloku, kliknij przycisk **podsieci**.
3. Nazwa podsieci bramy Hello jest wypełniane automatycznie hello wymaganej nazwy "GatewaySubnet". Witaj **zakres adresów** zawiera adresy IP hello przydzielonych usługi bramy sieci VPN toohello. Niektóre konfiguracje Zezwalaj podsieć bramy /29, ale jego najlepszych toouse /28 lub /27 tooaccommodate przyszłych konfiguracje, które mogą wymagać więcej adresów IP dla usługi bramy hello. W naszym przykładzie ustawienia używamy 10.11.1.0/27. Dostosuj hello przestrzeni adresowej, a następnie kliknij przycisk **OK**.
4. Skonfiguruj hello **rozmiaru bramy**. To ustawienie oznacza toohello [jednostka SKU bramy](vpn-gateway-about-vpn-gateway-settings.md#gwsku).
5. Skonfiguruj hello **routingu typu**. Witaj typ routingu dla tej konfiguracji musi być **dynamiczne**. Nie można zmienić typu routingu hello później, chyba że zerwanie hello bramy i Utwórz nową.
6. Kliknij przycisk **OK**.
7. Na powitania **nowego połączenia sieci VPN** bloku, kliknij przycisk **OK** toobegin tworzenie hello bramy sieci wirtualnej. Tworzenie bramy może potrwać często 45 minut lub dłużej, w zależności od hello bramy wybranej jednostki SKU.

## <a name="vnet4settings"></a>Krok 5 — Konfigurowanie ustawień TestVNet4

Powtórz kroki od hello zbyt[utworzyć lokalnej witryny](#localsite) i [Utwórz bramę sieci wirtualnej hello](#gw) tooconfigure TestVNet4, zastępując wartości hello, gdy jest to konieczne. Jeśli przeprowadzasz to jako wykonywania, użyj hello [przykładowe wartości](#vnetvalues).

## <a name="updatelocal"></a>Krok 6 - witryny lokalne powitania aktualizacji

Po z bram sieci wirtualnej zostały utworzone dla obu sieci wirtualnych, należy dostosować witryny lokalne powitania **adres IP bramy sieci VPN** wartości.

|Nazwa sieci wirtualnej|Podłączonej lokacji|Adres IP bramy|
|:--- |:--- |:--- |
|TestVNet1|VNet4Local|Adres IP bramy sieci VPN dla TestVNet4|
|TestVNet4|VNet1Local|Adres IP bramy sieci VPN dla TestVNet1|

### <a name="part-1---get-hello-virtual-network-gateway-public-ip-address"></a>Część 1 - Get hello sieci wirtualnej publiczny adres IP bramy

1. Znajdź sieci wirtualnej w hello portalu Azure.
2. Kliknij przycisk hello tooopen sieci wirtualnej **omówienie** bloku. W bloku hello w **połączeń sieci VPN**, można wyświetlić hello adresu IP dla bramy sieci wirtualnej.

  ![Publiczny adres IP](./media/vpn-gateway-howto-vnet-vnet-portal-classic/publicIP.png)
3. Skopiuj hello adresu IP. Będą używać go w następnej sekcji hello.
4. Powtórz te kroki dla TestVNet4

### <a name="part-2---modify-hello-local-sites"></a>Część 2 - modyfikowanie witryny lokalne powitania

1. Znajdź sieci wirtualnej w hello portalu Azure.
2. Na powitania sieci wirtualnej **omówienie** bloku, kliknij lokację lokalne powitania.

  ![Utworzony lokacji lokalnej](./media/vpn-gateway-howto-vnet-vnet-portal-classic/local.png)
3. Na powitania **połączeń VPN lokacja-lokacja** bloku, kliknij nazwę hello hello witryny lokalnej, które mają toomodify.

  ![Otwórz witrynę lokalnego](./media/vpn-gateway-howto-vnet-vnet-portal-classic/openlocal.png)
4. Kliknij przycisk hello **lokacji lokalnej** , które mają toomodify.

  ![modyfikowanie lokacji](./media/vpn-gateway-howto-vnet-vnet-portal-classic/connections.png)
5. Aktualizacja hello **adres IP bramy sieci VPN** i kliknij przycisk **OK** toosave hello ustawienia.

  ![brama IP](./media/vpn-gateway-howto-vnet-vnet-portal-classic/gwupdate.png)
6. Zamknij hello innych bloków.
7. Powtórz te kroki dla TestVNet4.

## <a name="getvalues"></a>Krok 7: pobieranie wartości z pliku konfiguracji sieci hello

Po utworzeniu klasyczne sieci wirtualne w portalu Azure hello nazwa hello, które możesz wyświetlać nie jest hello pełną nazwę, używanego programu PowerShell. Na przykład sieć wirtualną o nazwie toobe wyświetlany **TestVNet1** w portalu hello może być znacznie dłuższe nazwę w pliku konfiguracji sieci hello. Witaj nazwę może wyglądać mniej więcej tak: **ClassicRG TestVNet1 grupy**. Podczas tworzenia połączenia jest ważne toouse hello wartości, które widać w pliku konfiguracji sieci hello.

W hello następujące kroki połączy tooyour konto platformy Azure i pobierania oraz przeglądanie hello sieci konfiguracji pliku tooobtain hello wartości, które są wymagane dla połączenia.

1. Pobierz i zainstaluj najnowszą wersję hello hello poleceń cmdlet programu PowerShell Azure usługi zarządzania (ko). Aby uzyskać więcej informacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

2. Otwórz konsolę programu PowerShell z podwyższonym poziomem uprawnień i Połącz konto tooyour. Użyj powitania po toohelp przykład, gdy nawiązujesz połączenie:

  ```powershell
  Login-AzureRmAccount
  ```

  Sprawdź subskrypcje hello hello konta.

  ```powershell
  Get-AzureRmSubscription
  ```

  Jeśli masz więcej niż jedną subskrypcję, wybierz subskrypcję hello, które mają toouse.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
  ```

  Następnie należy użyć następującego polecenia cmdlet tooadd hello tooPowerShell Twojej subskrypcji platformy Azure dla hello klasycznego modelu wdrażania.

  ```powershell
  Add-AzureAccount
  ```
3. Eksportowanie i widoku hello sieci pliku konfiguracji. Utwórz katalog na komputerze, a następnie wyeksportować katalogu toohello pliku konfiguracji sieci hello. W tym przykładzie pliku konfiguracji sieci hello są eksportowane zbyt**C:\AzureNet**.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
4. Otwórz plik hello tekstu Edytor widoku hello nazwami i dla sieci wirtualnych i witryny. Będą one hello nazwa używana podczas tworzenia połączenia.<br>Nazwy sieci wirtualnej są wyświetlane jako **VirtualNetworkSite name =**<br>Nazwy lokacji są wyświetlane jako **nazwy elementu LocalNetworkSiteRef =**

## <a name="createconnections"></a>Krok 8 - tworzenie hello połączenia bramy sieci VPN

Po ukończeniu wszystkich poprzednich krokach hello można ustawić kluczy wstępnych hello IPsec i IKE i utworzyć hello połączenia. Ten zestaw kroków korzysta z programu PowerShell. Nie można skonfigurować połączenia do wirtualnymi hello klasycznego modelu wdrażania w hello portalu Azure.

W przykładach hello Zwróć uwagę, że klucz udostępniony hello jest dokładnie hello takie same. klucz współużytkowany Hello musi zawsze odpowiadać. Należy się tooreplace wartości hello w tych przykładach hello dokładnej nazwy dla sieci wirtualnych i lokalnych witryn sieci.

1. Utwórz połączenie tooTestVNet4 TestVNet1 hello.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet1' `
  -LocalNetworkSiteName '17BE5E2C_VNet4Local' -SharedKey A1b2C3D4
  ```
2. Utwórz połączenie tooTestVNet1 TestVNet4 hello.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet4' `
  -LocalNetworkSiteName 'F7F7BFC7_VNet1Local' -SharedKey A1b2C3D4
  ```
3. Poczekaj na powitania tooinitialize połączenia. Po hello bramy został zainicjowany, hello stanu jest "Powodzenie".

  ```
  Error          :
  HttpStatusCode : OK
  Id             :
  Status         : Successful
  RequestId      :
  StatusCode     : OK
  ```

## <a name="faq"></a>Aby wirtualnymi zagadnienia dotyczące klasyczne sieci wirtualne
* sieci wirtualne Hello może znajdować się w hello tych samych lub różnych subskrypcji.
* sieci wirtualne Hello może znajdować się w hello tych samych lub różnych regionach platformy Azure (lokalizacja).
* Usługa w chmurze ani punkt końcowy z równoważeniem obciążenia nie mogą rozciągać się na sieci wirtualne, nawet jeśli są one ze sobą połączone.
* Łączenie wielu sieci wirtualnych nie wymaga żadnych urządzeń sieci VPN.
* Aby wirtualnymi obsługuje łączenia sieci wirtualnej platformy Azure. Nie obsługuje łączenia maszyny wirtualnej lub usługi w chmurze, które nie są wdrażane tooa sieci wirtualnej.
* Aby wirtualnymi wymaga dynamicznymi bramami routingu. Azure statycznymi bramami routingu nie są obsługiwane.
* Połączenie sieci wirtualnej może być używane równocześnie z sieciami VPN obejmującymi wiele lokacji. Brak maksymalnie 10 tuneli VPN dla bramy sieci VPN sieci wirtualnej łączenie tooeither innych sieci wirtualnych lub w lokacjach lokalnych.
* Witaj hello wirtualnych sieci lokalnych i w których lokacji sieci lokalnej nie może nakładać się na przestrzeni adresowych. Spowoduje hello tworzenie sieci wirtualnych lub przekazywania toofail pliki konfiguracji netcfg nakładających się przestrzeni adresowych.
* Nadmiarowe tunele między dwiema sieciami wirtualnymi nie są obsługiwane.
* Wszystkie tuneli VPN do sieci wirtualnej, w tym sieci VPN P2S hello, udostępniania hello dostępnej przepustowości dla bramy sieci VPN hello oraz hello tego samego SLA czas działania bramy sieci VPN w systemie Azure.
* Do wirtualnymi ruchu przechodzącego przez hello Azure sieci szkieletowej.

## <a name="next-steps"></a>Następne kroki
Sprawdź połączenia. Zobacz [sprawdzić połączenie bramy sieci VPN](vpn-gateway-verify-connection-resource-manager.md).
