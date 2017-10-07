---
title: "Połącz tooAzure klasycznych sieci wirtualnych Menedżera zasobów sieci wirtualnych: Portal | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate połączenia sieci VPN między klasycznych sieci wirtualnych i sieci wirtualnych Menedżera zasobów przy użyciu bramy sieci VPN i hello portalu"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 5a90498c-4520-4bd3-a833-ad85924ecaf9
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: bef63b4e829335b2e1a9434a35ebfe33b4fd7373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-hello-portal"></a>Nawiązywanie połączenia sieci wirtualnych z różne modele wdrażania przy użyciu portalu hello

W tym artykule opisano, jak tooconnect klasycznych sieci wirtualnych tooResource tooallow Menedżera sieci wirtualnych hello zasobów znajdujących się w hello oddzielne wdrażania modeli toocommunicate ze sobą. Hello opisanych w tym artykule głównie używać hello portalu Azure, ale można również utworzyć w tej konfiguracji przy użyciu programu PowerShell hello, wybierając hello artykułu z tej listy.

> [!div class="op_single_selector"]
> * [Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

Łączenie klasycznego tooa sieci wirtualnej Menedżera zasobów w sieci wirtualnej jest podobne tooconnecting lokalizacji sieci wirtualnej tooan lokalnej lokacji. Oba typy łączności Użyj tooprovide bramy sieci VPN przy użyciu protokołu IPsec/IKE bezpiecznego tunelu. Można utworzyć połączenia między sieciami wirtualnymi, które są w różnych subskrypcji i w różnych regionach. Można też połączyć sieci wirtualnych, która jeszcze połączenia lokalnego tooon sieci, tak długo, jak jest hello bramy, które zostały skonfigurowane z dynamicznego lub oparte na trasach. Aby uzyskać więcej informacji o połączeniach sieci wirtualnej do sieci wirtualnej, zobacz hello [wirtualnymi — często zadawane pytania dotyczące](#faq) na końcu hello w tym artykule. 

Jeśli hello Twojej sieci wirtualnych tego samego regionu, można wziąć pod uwagę tooinstead, łącząc je przy użyciu sieci wirtualnej komunikacji równorzędnej. W przypadku komunikacji równorzędnej sieci wirtualnych nie jest używana brama sieci VPN. Aby uzyskać więcej informacji, zobacz temat [Komunikacja równorzędna sieci wirtualnych](../virtual-network/virtual-network-peering-overview.md). 

### <a name="prerequisites"></a>Wymagania wstępne

* Tych krokach przyjęto założenie, że obie sieci wirtualne zostały już utworzone. Jeśli jest używany w tym artykule jako wykonywania i nie ma sieci wirtualnych, są łącza w hello toohelp kroki tworzenia.
* Sprawdź, czy zakresy adresów hello powitalne sieci wirtualne nie pokrywają się ze sobą lub nakładanie się ze wszystkimi hello zakresów dla innych połączeń bramy mogą być połączone z tym powitalne.
* Zainstaluj hello najnowszych poleceń cmdlet programu PowerShell dla usługi Resource Manager i usługi zarządzania (klasyczny). W tym artykule używamy zarówno hello portalu Azure i programu PowerShell. PowerShell jest wymagane toocreate hello połączenie z hello klasycznej sieci wirtualnej toohello Menedżera zasobów w sieci wirtualnej. Aby uzyskać więcej informacji, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview). 

### <a name="values"></a>Przykładowe ustawienia

Można użyć tych wartości toocreate środowiska testowego, lub zobacz toothem toobetter zrozumieć hello przykłady w tym artykule.

**Klasyczne sieci wirtualnej**

Nazwa sieci wirtualnej = ClassicVNet <br>
Przestrzeń adresowa = 10.0.0.0/24 <br>
Podsieć 1 = 10.0.0.0/27 <br>
Grupa zasobów = ClassicRG <br>
Lokalizacja = zachodnie stany USA <br>
GatewaySubnet = 10.0.0.32/28 <br>
Lokalna witryna = RMVNetLocal <br>

**Menedżer zasobów w sieci wirtualnej**

Nazwa sieci wirtualnej = RMVNet <br>
Przestrzeń adresowa = 192.168.0.0/16 <br>
Podsieć 1 = 192.168.1.0/24 <br>
GatewaySubnet = 192.168.0.0/26 <br>
Grupa zasobów = RG1 <br>
Lokalizacja = wschodnie stany USA <br>
Nazwa bramy sieci wirtualnej = RMGateway <br>
Typ bramy sieci VPN = <br>
Typ sieci VPN = opartej na trasach <br>
Nazwa adres publiczny adres IP bramy = rmgwpip <br>
Brama sieci lokalnej = ClassicVNetLocal <br>
Nazwa połączenia = RMtoClassic

### <a name="connection-overview"></a>Omówienie połączenia

W przypadku tej konfiguracji za pośrednictwem tunelu IPsec i IKE sieci VPN między sieciami wirtualnymi hello tworzenia połączenia bramy sieci VPN. Upewnij się, że żaden z zakresów w Twojej sieci wirtualnej nakłada się ze sobą lub za pomocą dowolnego z sieci lokalne powitania, które łączą się z.

Witaj poniższej tabeli przedstawiono przykładowy sposób definiowania przykład Witaj sieci wirtualnych i witryn lokalnych:

| Virtual Network | Przestrzeń adresów | Region | Łączy lokację sieciową toolocal |
|:--- |:--- |:--- |:--- |
| ClassicVNet |(10.0.0.0/24) |Zachodnie stany USA | RMVNetLocal (192.168.0.0/16) |
| RMVNet | (192.168.0.0/16) |Wschodnie stany USA |ClassicVNetLocal (10.0.0.0/24) |

## <a name="classicvnet"></a>1. Skonfiguruj hello klasycznych ustawień sieci wirtualnej

W tej sekcji utworzysz hello lokalnej sieci (lokalnej lokacji) i bramy sieci wirtualnej hello klasycznej sieci wirtualnej. Jeśli nie masz klasycznej sieci wirtualnej i są uruchomione te kroki jako wykonywania, można utworzyć sieci wirtualnej przy użyciu [w tym artykule](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) i hello [przykład](#values) wartości ustawienia z powyżej.

Korzystając z portalu toocreate hello klasycznej sieci wirtualnej, musisz przejść toohello bloku sieci wirtualnej przy użyciu hello, wykonaj następujące kroki, w przeciwnym razie nie ma toocreate opcji hello klasycznej sieci wirtualnej:

1. Kliknij przycisk hello bloku "New" hello tooopen "+".
2. W polu "Marketplace wyszukiwania powitania" hello wpisz "Sieci wirtualnej". Jeśli zamiast tego należy wybrać sieć -> Sieć wirtualna, nie otrzymasz toocreate opcji hello klasycznej sieci wirtualnej.
3. Zlokalizuj "Sieci wirtualnej" z hello zwrócił listy i kliknij ją bloku sieci wirtualnej hello tooopen. 
4. W bloku sieci wirtualnej hello wybierz "Klasycznym" toocreate klasycznej sieci wirtualnej. 

Jeśli masz już sieć wirtualną z bramą sieci VPN, sprawdź, czy brama tego hello jest dynamiczny. Jeśli jest statyczna, należy najpierw usunąć hello bramy sieci VPN, a następnie kontynuować.

Zamieszczone zrzuty ekranu są przykładowe. Należy się tooreplace hello wartości własnymi, lub użyj hello [przykład](#values) wartości.

### <a name="part-1---configure-hello-local-site"></a>Część 1 — Konfigurowanie hello lokacji lokalnej

Otwórz hello [portalu Azure](https://ms.portal.azure.com) i zaloguj się przy użyciu konta platformy Azure.

1. Przejdź za**wszystkie zasoby** i Znajdź hello **ClassicVNet** hello na liście.
2. Na powitania **omówienie** bloku w hello **połączeń sieci VPN** kliknij hello **bramy** graficzne toocreate bramy.

    ![Konfigurowanie bramy sieci VPN](./media/vpn-gateway-connect-different-deployment-models-portal/gatewaygraphic.png "Brama sieci VPN")
3. Na powitania **nowego połączenia sieci VPN** bloku dla **typ połączenia**, wybierz pozycję **lokacja lokacja**.
4. Aby uzyskać **lokacji lokalnej**, kliknij przycisk **Skonfiguruj wymagane ustawienia**. Spowoduje to otwarcie hello **lokacji lokalnej** bloku.
5. Na powitania **lokacji lokalnej** bloku Utwórz nazwę toorefer toohello Menedżera zasobów w sieci wirtualnej. Na przykład "RMVNetLocal".
6. Jeśli bramy sieci VPN hello hello Menedżera zasobów w sieci wirtualnej ma już do publicznego adresu IP, użyj wartości hello na powitania **adres IP bramy sieci VPN** pola. Jeśli wykonanie tych czynności jako wykonywania, lub nie masz jeszcze bramy sieci wirtualnej sieci wirtualnej Menedżera zasobów, można uzupełnić adres IP — symbol zastępczy. Upewnij się, że adres IP — symbol zastępczy hello jest używany prawidłowy format. Później należy zastąpić adres IP — symbol zastępczy hello hello publiczny adres IP bramy sieci wirtualnej hello Menedżera zasobów.
7. Dla **przestrzeni adresowej klienta**, użyj wartości powitania dla hello przestrzeni adresów IP sieci wirtualnej dla hello Menedżera zasobów w sieci wirtualnej. To ustawienie jest używane toospecify hello adres spacje tooroute toohello Menedżera zasobów sieci wirtualnej.
8. Kliknij przycisk **OK** toosave hello wartości i zwraca toohello **nowego połączenia sieci VPN** bloku.

### <a name="part-2---create-hello-virtual-network-gateway"></a>Część 2 — Tworzenie hello bramy sieci wirtualnej

1. Na powitania **nowego połączenia sieci VPN** bloku, wybierz hello **Utwórz bramę natychmiast** wyboru i kliknij przycisk **konfiguracji bramy opcjonalne** tooopen hello  **Konfiguracja bramy** bloku. 

    ![Blok konfiguracji bramy Otwórz](./media/vpn-gateway-connect-different-deployment-models-portal/optionalgatewayconfiguration.png "bramy Otwórz blok konfiguracji")
2. Kliknij przycisk **podsieci — Skonfiguruj wymagane ustawienia** tooopen hello **Dodaj podsieć** bloku. Witaj **nazwa** jest już skonfigurowana z wartością hello wymagane **GatewaySubnet**.
3. Witaj **zakres adresów** odwołuje się zakres toohello hello podsieci bramy. Mimo że można utworzyć podsieci bramy z /29 (adresy 3), zakres adresów zaleca się utworzenie podsieć bramy, który zawiera więcej adresów IP. Pomieszczenie tylu przyszłych konfiguracje, które mogą wymagać więcej dostępnych adresów IP. Jeśli to możliwe Użyj /27 lub /28. Jeśli używasz tych kroków jako wykonywania, może się odwoływać toohello [przykład](#values) wartości. Kliknij przycisk **OK** podsieci bramy hello toocreate.
4. Na powitania **konfiguracji bramy** bloku **rozmiar** odwołuje się jednostka SKU bramy toohello. Wybierz hello jednostka SKU bramy dla bramy sieci VPN.
5. Sprawdź hello **typ routingu** jest **dynamiczne**, następnie kliknij przycisk **OK** tooreturn toohello **nowego połączenia sieci VPN** bloku.
6. Na powitania **nowego połączenia sieci VPN** bloku, kliknij przycisk **OK** toobegin Tworzenie bramy sieci VPN. Tworzenie bramy sieci VPN może potrwać too45 toocomplete minut.

### <a name="ip"></a>Część 3 - bramy sieci wirtualnej hello kopiowania publicznego adresu IP

Po utworzeniu bramy sieci wirtualnej hello można wyświetlić adres IP bramy hello. 

1. Przejdź tooyour klasycznej sieci wirtualnej, a następnie kliknij przycisk **omówienie**.
2. Kliknij przycisk **połączeń sieci VPN** bloku połączeń sieci VPN hello tooopen. W bloku połączeń sieci VPN hello można wyświetlić hello publicznego adresu IP. Jest to hello publiczny adres IP przypisany tooyour bramy sieci wirtualnej. 
3. Zapisz lub skopiuj hello adresu IP. Można użyć go w kolejnych krokach podczas pracy z ustawieniami konfiguracji bramy sieci lokalnej usługi Resource Manager. Można również wyświetlić stan hello połączenia bramy. Lokacja sieci lokalnej hello powiadomień utworzone jest wyświetlany jako "Łączenie". Witaj stan zmieni się po utworzeniu połączenia.
4. Zamknij hello blok po skopiowaniu adres IP bramy hello.

## <a name="rmvnet"></a>2. Konfigurowanie ustawień sieci wirtualnej z Menedżera zasobów hello

W tej sekcji utworzysz hello bramy sieci wirtualnej i Brama sieci lokalnej hello Menedżera zasobów sieci wirtualnej. Jeśli nie masz Menedżera zasobów sieci wirtualnej i są uruchomione te kroki jako wykonywania, można utworzyć sieci wirtualnej przy użyciu [w tym artykule](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) i hello [przykład](#values) wartości ustawienia z powyżej.

Zamieszczone zrzuty ekranu są przykładowe. Należy się tooreplace hello wartości własnymi, lub użyj hello [przykład](#values) wartości.

### <a name="part-1---create-a-gateway-subnet"></a>Część 1 — Tworzenie podsieci bramy

Przed utworzeniem bramy sieci wirtualnej, najpierw podsieci bramy hello toocreate. Utwórz podsieć bramy z licznikiem CIDR /28 lub większy. (/ 27, / 26, itp.)

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

### <a name="part-2---create-a-virtual-network-gateway"></a>Część 2 — Tworzenie bramy sieci wirtualnej

[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

### <a name="createlng"></a>Część 3 — Tworzenie bramy sieci lokalnej

bramy sieci lokalnej Hello określa zakres adresów hello i hello publiczny adres IP skojarzone z klasycznej sieci wirtualnej i jej bramy sieci wirtualnej.

Jeśli przeprowadzasz te kroki jako wykonywania, można znaleźć ustawienia toothese:

| Virtual Network | Przestrzeń adresów | Region | Łączy lokację sieciową toolocal |Adres publiczny adres IP bramy|
|:--- |:--- |:--- |:--- |:--- |
| ClassicVNet |(10.0.0.0/24) |Zachodnie stany USA | RMVNetLocal (192.168.0.0/16) |Witaj adres publiczny adres IP, który jest przypisywany toohello ClassicVNet bramy|
| RMVNet | (192.168.0.0/16) |Wschodnie stany USA |ClassicVNetLocal (10.0.0.0/24) |Witaj adres publiczny adres IP, który jest przypisywany toohello RMVNet bramy.|

[!INCLUDE [vpn-gateway-add-lng-rm-portal](../../includes/vpn-gateway-add-lng-rm-portal-include.md)]

## <a name="modifylng"></a>3. Modyfikowanie hello klasycznych ustawień lokalnej lokacji sieci wirtualnej

W tej sekcji musisz zastąpić adres IP — symbol zastępczy hello używane podczas określania ustawień lokacji lokalnej hello, z hello adres IP bramy sieci VPN usługi Resource Manager. Ta sekcja używa hello klasyczny (SM) poleceń cmdlet programu PowerShell.

1. W hello portalu Azure Przejdź toohello klasycznej sieci wirtualnej.
2. W bloku hello sieci wirtualnej, kliknij **omówienie**.
3. W hello **połączeń sieci VPN** sekcji, kliknij nazwę hello witryny lokalne powitania rysunku.

    ![Połączenia sieci VPN](./media/vpn-gateway-connect-different-deployment-models-portal/vpnconnections.png "połączeń sieci VPN")
4. Na powitania **połączenia sieci VPN typu lokacja lokacja** bloku, kliknij nazwę hello hello witryny.

    ![Nazwa witryny](./media/vpn-gateway-connect-different-deployment-models-portal/sitetosite3.png "nazwy lokacji lokalnych")
5. W bloku połączenia hello witryny lokalnej, kliknij nazwę hello hello lokacji lokalnej tooopen hello **lokacji lokalnej** bloku.

    ![Otwórz lokalnej lokacji](./media/vpn-gateway-connect-different-deployment-models-portal/openlocal.png "Otwórz lokacji lokalnej")
6. Na powitania **lokacji lokalnej** bloku, Zastąp hello **adres IP bramy sieci VPN** adresu IP hello hello Menedżera zasobów bramy.

    ![Adres ip bramy](./media/vpn-gateway-connect-different-deployment-models-portal/gwipaddress.png "adresu IP bramy")
7. Kliknij przycisk **OK** adresu IP hello tooupdate.

## <a name="RMtoclassic"></a>4. Utwórz połączenie tooclassic Resource Manager

W tych kroków, skonfiguruj połączenie hello hello Menedżera zasobów w sieci wirtualnej toohello klasycznego przy użyciu sieci wirtualnej hello portalu Azure.

1. W **wszystkie zasoby**, zlokalizuj hello bramy sieci lokalnej. W naszym przykładzie Brama sieci lokalnej hello jest **ClassicVNetLocal**.
2. Kliknij przycisk **konfiguracji** i sprawdź, czy wartość adresu IP hello hello bramy sieci VPN dla hello klasycznej sieci wirtualnej. Aktualizacja, w razie potrzeby, a następnie kliknij przycisk **zapisać**. Zamknij hello bloku.
3. W **wszystkie zasoby**, kliknij przycisk hello bramy sieci lokalnej.
4. Kliknij przycisk **połączeń** tooopen hello połączeń bloku.
5. Na powitania **połączeń** bloku, kliknij przycisk  **+**  tooadd połączenia.
6. Na powitania **Dodaj połączenie** bloku, nazwa hello połączenia. Na przykład "RMtoClassic".
7. **Lokacja-lokacja** jest już wybrana w tym bloku.
8. Wybierz bramę sieci wirtualnej hello, które mają tooassociate z tą lokacją.
9. Utwórz **klucza wspólnego**. Ten klucz jest również używany w połączeniu hello, utworzona na podstawie hello klasycznej sieci wirtualnej toohello Menedżera zasobów w sieci wirtualnej. Można wygenerować klucz hello lub go utworzyć. W tym przykładzie używamy "abc123", ale można i powinien używasz bardziej złożonych.
10. Kliknij przycisk **OK** toocreate hello połączenia.

##<a name="classictoRM"></a>5. Tworzenie klasycznego tooResource Menedżera połączeń

W tych krokach skonfigurujesz hello połączenia z hello klasycznej sieci wirtualnej toohello Menedżera zasobów w sieci wirtualnej. Kroki te wymagają programu PowerShell. Nie można utworzyć tego połączenia w portalu hello. Upewnij się, że zostały pobrane i zainstalowane zarówno hello klasyczny (ko), jak i poleceń cmdlet programu PowerShell Menedżera zasobów (RM).

### <a name="1-connect-tooyour-azure-account"></a>1. Połącz tooyour konto platformy Azure

Otwórz konsolę programu PowerShell hello z podwyższonym poziomem uprawnień i logowania tooyour konto platformy Azure. Witaj następujące polecenie cmdlet monituje o hello poświadczenia logowania dla konta platformy Azure. Po zalogowaniu ustawienia konta są pobierane, tak aby były dostępne tooAzure środowiska PowerShell.

```powershell
Login-AzureRmAccount
```
   
Pobierz listę subskrypcji Azure, jeśli masz więcej niż jedną subskrypcję.

```powershell
Get-AzureRmSubscription
```

Określ, które mają toouse subskrypcji hello. 

```powershell
Select-AzureRmSubscription -SubscriptionName "Name of subscription"
```

Dodawanie Twojego konta Azure toouse hello klasycznego poleceń cmdlet programu PowerShell (ko). toodo tak, można użyć następującego polecenia hello:

```powershell
Add-AzureAccount
```

### <a name="2-view-hello-network-configuration-file-values"></a>2. Wyświetl wartości w pliku konfiguracji sieci hello

Po utworzeniu sieci wirtualnej w portalu Azure hello hello pełną nazwę, która używa usługi Azure nie jest widoczne w portalu Azure hello. Na przykład sieć wirtualną, która jest wyświetlana w portalu Azure hello o nazwie "ClassicVNet" toobe może mieć wiele nazwę dłużej w pliku konfiguracji sieci hello. Witaj nazwę może wyglądać mniej więcej tak: "ClassicRG ClassicVNet grupy". Poniższe kroki możesz pobrać hello sieci plik i widok hello wartości konfiguracji.

Utwórz katalog na komputerze, a następnie wyeksportować katalogu toohello pliku konfiguracji sieci hello. W tym przykładzie pliku konfiguracji sieci hello jest tooC:\AzureNet wyeksportowane.

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

Otwórz plik hello nazwą tekstu Edytor i widoku hello klasycznej sieci wirtualnej. Użyj nazwy hello w pliku konfiguracji sieci hello podczas uruchamiania polecenia cmdlet programu PowerShell.

- Nazwy sieci wirtualnej są wyświetlane jako **VirtualNetworkSite name =**
- Nazwy lokacji są wyświetlane jako **LocalNetworkSite name =**

### <a name="3-create-hello-connection"></a>3. Utwórz połączenie hello

Ustaw klucz udostępniony hello oraz tworzenie połączenia hello z hello klasycznej sieci wirtualnej toohello Menedżera zasobów w sieci wirtualnej. Nie można ustawić klucza wspólnego hello przy użyciu portalu hello. Upewnij się, że uruchomienie tych kroków, logując się przy użyciu wersji klasycznej hello hello poleceń cmdlet programu PowerShell. tak, użyj toodo **Add-AzureAccount**. W przeciwnym razie nie będzie możliwe tooset hello "-AzureVNetGatewayKey".

- W tym przykładzie **- VNetName** jest nazwą hello hello klasycznej sieci wirtualnej jako odnaleźć w pliku konfiguracji sieci. 
- Witaj **- LocalNetworkSiteName** określony dla witryny lokalne powitania, jako nazwę hello znajduje się w pliku konfiguracji sieci.
- Witaj **- SharedKey** to Generowanie i określ wartość. W tym przykładzie użyliśmy *abc123*, ale można generować bardziej złożonych. Witaj ważne, czy element jest daną hello określone w tym miejscu musi być powitalne samą wartość, należy określić podczas tworzenia połączenia tooclassic Menedżera zasobów.

```powershell
Set-AzureVNetGatewayKey -VNetName "Group ClassicRG ClassicVNet" `
-LocalNetworkSiteName "172B9E16_RMVNetLocal" -SharedKey abc123
```

##<a name="verify"></a>6. Sprawdź połączenia

Możesz sprawdzić, czy hello połączeń przy użyciu portalu Azure lub programu PowerShell. Podczas sprawdzania poprawności, może być konieczne toowait minucie lub dwóch tworzenia hello połączenia. Gdy połączenie zostanie nawiązane, stan łączności hello zmienia się z too'Connected "Łączenie" ".

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a>tooverify hello połączenia z klasycznym tooyour sieci wirtualnej Menedżera zasobów w sieci wirtualnej

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

###<a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a>tooverify hello połączenia z Twojej sieci wirtualnej Resource Manager tooyour klasycznej sieci wirtualnej

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="faq"></a>Często zadawane pytania dotyczące połączeń między sieciami wirtualnymi

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]
