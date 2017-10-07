---
title: "aaaCreate, zmienić lub usunąć komunikacji równorzędnej sieci wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate, zmienić lub usunąć sieci wirtualnej komunikacji równorzędnej."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: jdial
ms.openlocfilehash: 70f85364ab23e23533ad276aeec0156cebe89be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-virtual-network-peering"></a>Tworzenie, zmienianie lub usunąć sieci wirtualnej komunikacji równorzędnej

Dowiedz się, jak toocreate, zmienić lub usunąć sieci wirtualnej komunikacji równorzędnej. Umożliwia komunikacji równorzędnej sieci wirtualnej można tooconnect dwie sieci wirtualne w hello tej samej lokalizacji platformy Azure za pośrednictwem hello Azure szkieletu sieci. Po połączyć za pomocą, Witaj dwie sieci wirtualne są nadal zarządzane jako oddzielne zasoby. Zasoby w każdej sieci wirtualnej komunikowania się z hello sam opóźnienia i przepustowości tak, jakby był hello zasobów w hello są takie same sieci wirtualnej. Jeśli nie masz doświadczenia w obsłudze sieci wirtualnej komunikacji równorzędnej, zaleca się odczytywania hello [komunikacji równorzędnej omówienie sieci wirtualnej](virtual-network-peering-overview.md) i wykonując hello [tworzenie sieci wirtualnej komunikacji równorzędnej samouczek](virtual-network-create-peering.md), przed wykonaniem Witaj zadania w tym artykule.

## <a name="before-you-begin"></a>Przed rozpoczęciem

Wykonaj następujące zadania przed wykonaniem kroków w żadnej sekcji tego artykułu hello:

- Przejrzyj hello [Azure ogranicza](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn artykuł na temat limitów dla komunikacji równorzędnej.
- Zaloguj się za toohello portalu Azure, Azure interfejsu wiersza polecenia (CLI) lub Azure PowerShell przy użyciu konta platformy Azure. Jeśli nie masz jeszcze konta platformy Azure, należy zarejestrować się w celu [bezpłatnego konta wersji próbnej](https://azure.microsoft.com/free).
- Jeśli przy użyciu programu PowerShell poleceń toocomplete zadania w tym artykule [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Upewnij się, że masz najnowszą wersję hello hello Azure poleceń cmdlet programu PowerShell zainstalowane. tooget Pomoc dla poleceń programu PowerShell, wraz z przykładami, wpisz `get-help <command> -full`.
- Jeśli przy użyciu interfejsu wiersza polecenia platformy Azure (CLI) polecenia toocomplete zadania w tym artykule [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Upewnij się, że masz najnowszą wersję hello hello Azure CLI zainstalowane. tooget pomocy dla poleceń interfejsu wiersza polecenia, wpisz `az <command> --help`. Zamiast instalowania hello interfejsu wiersza polecenia i jego wymagania wstępne można użyć hello powłoki chmury Azure. Hello powłoki chmury Azure jest bezpłatna powłoki Bash, który można uruchomić bezpośrednio z poziomu hello portalu Azure. Witaj powłoki chmury ma hello Azure CLI wstępnie zainstalowane i skonfigurowane toouse z Twoim kontem. toouse hello powłoki chmury kliknij hello powłoki chmury **> _** u góry hello hello [portal](https://portal.azure.com). 

## <a name="create-a-peering"></a>Utwórz element równorzędny

>[!NOTE]
>Istnieje kilka wymagań, ograniczeń i toosuccessfully uwagi dotyczące tworzenia sieci wirtualnej komunikacji równorzędnej. Przed utworzeniem komunikacji równorzędnej, upewnij się, po zapoznaniu się ze hello [wymagań i ograniczeń](#requirements-and-constraints) i [wymagane uprawnienia](#permissions).
>

1. Zaloguj się za toohello [portal](https://portal.azure.com) przy użyciu konta przypisanego konieczne hello [roli lub uprawnienia](#permissions).
2. W polu hello, które zawiera tekst hello *wyszukiwania zasobów* u góry hello hello portalu Azure, wpisz *sieci wirtualnych*. Gdy **sieci wirtualnych** pojawia się w wynikach wyszukiwania hello, kliknij ją. Nie zaznaczaj **sieci wirtualnych (klasyczne)** Jeśli wygląda na to, na liście hello, ponieważ nie można utworzyć komunikacji równorzędnej z sieci wirtualnej wdrożone za pośrednictwem hello klasycznego modelu wdrażania.
3. W hello **sieci wirtualnych** bloku, który jest wyświetlany, kliknij przycisk hello sieci wirtualnej mają toocreate komunikacji równorzędnej dla.
4. W okienku hello wyświetlany dla sieci wirtualnej hello wybrano kliknij **komunikacji równorzędnych** w hello **ustawienia** sekcji.
5. Kliknij przycisk **+ Dodaj**. 
6. <a name="add-peering"></a>W hello **dodać równorzędna** bloku, wprowadź lub wybierz wartości hello następujące ustawienia:
    - **Nazwa:** hello nazwa dla komunikacji równorzędnej hello musi być unikatowa w ramach sieci wirtualnej hello.
    - **Model wdrażania sieci wirtualnej:** wybierz, które hello modelu wdrażania wirtualnych sieci można mają toopeer z została wdrożona za pośrednictwem.
    - **Sprawdzić mój identyfikator zasobu:** Jeśli masz dostęp do odczytu toohello sieci wirtualnej ma toopeer z, pozostaw to pole wyboru niezaznaczone. Jeśli nie masz dostęp do odczytu toohello wirtualnej sieci lub subskrypcji, który ma toopeer z, zaznacz to pole wyboru. Wprowadź hello pełny identyfikator zasobu hello sieć wirtualna ma toopeer o w hello **identyfikator zasobu** pola, które znajdowały się po zaznaczeniu pola hello. Hello zasobów możesz wprowadzić identyfikator musi być sieci wirtualnej, który istnieje w hello Azure tego samego [lokalizacji](https://azure.microsoft.com/regions) jako tej sieci wirtualnej. Witaj pełny identyfikator zasobu wygląda podobniezbyt/subskrypcji/<Id>/providers/Microsoft.Network/virtualNetworks/ <-nazwa grupy zasobów-> /resourceGroups/ < nazwa wirtualnej sieci >. Identyfikator zasobu hello sieci wirtualnej można uzyskać, wyświetlając właściwości hello sieci wirtualnej. toolearn tooview hello właściwości dla sieci wirtualnej, zobacz temat [Zarządzanie sieciami wirtualnymi](virtual-network-manage-network.md#view-vnet).
    - **Subskrypcja:** wybierz hello [subskrypcji](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) hello sieć wirtualna ma toopeer z. Co najmniej jedna subskrypcja znajdują się w zależności od tego, jak wiele subskrypcji Twoje konto ma uprawnienia do odczytu. Po zaznaczeniu hello **identyfikator zasobu** pole wyboru, to ustawienie jest niedostępne. Tak długo, jak obie sieci wirtualne utworzone za pomocą Menedżera zasobów można elementów równorzędnych sieci wirtualnych w ramach różnych subskrypcji. Witaj toopeer możliwości różnych subskrypcji została utworzona za pośrednictwem różne modele wdrażania jest w wersji zapoznawczej. Rejestr hello Preview, przed utworzeniem komunikacji równorzędnej między sieciami wirtualnymi, wdrażać przy użyciu różne modele wdrażania znajdujące się w różnych subskrypcji. Dowiedz się więcej na temat tooregister hello Preview i [elementów równorzędnych sieci wirtualnych utworzonych przez różne modele wdrażania w ramach różnych subskrypcji](create-peering-different-deployment-models-subscriptions.md).
    - **Sieć wirtualna:** wybierz hello ma toopeer z sieci wirtualnej. Można wybrać sieć wirtualną, która została utworzona za pośrednictwem albo modelu wdrożenia usługi Azure, ale hello sieć wirtualna musi być w tej samej lokalizacji co sieć wirtualna hello, który jest inicjowanie hello komunikacji równorzędnej z hello. Możesz musi mieć odczytu sieci wirtualnej toohello dostępu dla niego toobe widoczne na liście hello. Jeśli sieć wirtualna jest wyświetlana, ale wygaszone, może być, ponieważ przestrzeń adresowa hello hello sieci wirtualnej nakłada się hello przestrzeni adresowej tej sieci wirtualnej. Jeśli nakładania się przestrzenie adresowe sieci wirtualnej, ich nie można połączyć za pomocą. Po zaznaczeniu hello **identyfikator zasobu** pole wyboru, to ustawienie jest niedostępne.
    - **Zezwalaj na dostęp do sieci wirtualnej:** wybierz **włączone** (ustawienie domyślne), jeśli chcesz, aby tooenable komunikacji między sieciami wirtualnymi hello dwa. Włączenie komunikacji między sieciami wirtualnymi umożliwia zasoby podłączone tooeither toocommunicate sieci wirtualnej z innymi z hello tego samego przepustowości i opóźnień, tak jakby były połączone toohello tej samej sieci wirtualnej. Cała komunikacja między zasobami w sieciach wirtualnych dwóch hello znajduje się nad hello Azure sieci prywatnej. Witaj **VirtualNetwork** domyślne znaczniki dla grup zabezpieczeń sieci obejmuje sieci wirtualnej hello i połączyć za pomocą sieci wirtualnej. więcej informacji o toolearn sieci znaczników domyślnych grup zabezpieczeń, przeczytaj hello [Przegląd grup zabezpieczeń sieci](virtual-networks-nsg.md#default-tags) artykułu.  Wybierz **wyłączone** Jeśli nie chcesz, ruch tooflow toohello połączyć za pomocą sieci wirtualnej. Możesz wybrać pozycję **wyłączone** Jeśli już połączyć za pomocą sieci wirtualnej z inną siecią wirtualną, ale czasami być toodisable przepływem ruchu między sieciami wirtualnymi hello dwa. Może się okazać się, że włączenie/wyłączenie funkcji jest wygodniejsze niż usunięcia i ponownego utworzenia komunikacji równorzędnych. Gdy to ustawienie jest wyłączone, ruch nie przepływa między hello połączyć za pomocą sieci wirtualnych.
    - **Zezwalaj na związanego z przekazywaniem ruchu:** Sprawdź tego pola tooallow ruch przesyłany dalej toohello połączyć za pomocą sieci wirtualnej (w hello połączyć za pomocą sieci wirtualnej ruch) sieci wirtualnej toothis tooflow. Przekazywanie ruchu jest wspólne, po wdrożeniu urządzenie sieci wirtualnej w sieci wirtualnej hello jest równorzędna z i utworzony tooforward ruch trasy zdefiniowane przez użytkownika za pośrednictwem urządzenie wirtualne sieci hello. Jeżeli pole to unchecked (ustawienie domyślne), ruch przesyłany dalej z hello połączyć za pomocą sieci wirtualnej nie można wykonać przepływu toothis sieci wirtualnej. Podczas włączania tej możliwości zezwala na ruch hello przekazywane za pośrednictwem hello komunikacji równorzędnej, nie tworzyć żadnych trasy zdefiniowane przez użytkownika lub wirtualnych urządzeń sieciowych. Trasy zdefiniowane przez użytkownika i wirtualnych urządzeń sieciowych są tworzone oddzielnie. Dowiedz się więcej o [trasy zdefiniowane przez użytkownika](virtual-networks-udr-overview.md).
    - **Zezwalaj na bramy przesyłania:** zaznacz to pole wyboru, jeśli masz sieci wirtualnej dołączonych toothis bramy sieci wirtualnej i chcesz, aby ruch tooallow z hello połączyć za pomocą tooflow sieci wirtualnej za pośrednictwem bramy hello. Na przykład tej sieci wirtualnej może być dołączone tooan sieci lokalnej za pośrednictwem bramy sieci wirtualnej. Zaznaczenie tego pola zezwala na ruch z hello połączyć za pomocą tooflow sieci wirtualnej za pośrednictwem sieci wirtualnej dołączonych toothis hello bramy. Jeśli zaznaczysz to pole hello połączyć za pomocą sieci wirtualnej nie może mieć skonfigurowaną bramę. Witaj połączyć za pomocą sieć wirtualna musi mieć hello **Użyj bramy zdalnego** zaznaczone pole wyboru podczas konfigurowania hello komunikacji równorzędnej z hello innych sieci wirtualnej toothis sieci wirtualnej. Pozostawienie to niezaznaczone pole (ustawienie domyślne), ruch z sieci wirtualnej połączyć za pomocą hello nadal przepływa toothis sieci wirtualnej, ale nie można wykonać przepływu za pośrednictwem sieci wirtualnej dołączonych toothis bramy sieci wirtualnej. Dowiedz się więcej o [bram sieci wirtualnej](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#s2smulti). 
    
    Nie można włączyć tę opcję, jeśli w przypadku komunikacji równorzędnej sieć wirtualną (Resource Manager) z siecią wirtualną (klasyczny). Chociaż hello ruch przepływa między dwiema sieciami wirtualnymi hello, hello (klasyczne) ruchu w sieci wirtualnej nie można wykonać przepływu za pośrednictwem sieci bramy dołączonych toohello sieć wirtualną (Resource Manager).
    - **Użyj bramy zdalnego:** Sprawdź pole tooallow ruch z tej sieci wirtualnej tooflow za pośrednictwem sieci wirtualnej bramy dołączonych toohello sieci wirtualnej jest równorzędna z. Na przykład hello sieci wirtualnej, który jest równorzędna z ma bramy sieci VPN dołączony umożliwiającą sieć lokalną tooan komunikacji.  Zaznaczenie tego pola wyboru zezwala na ruch z tej sieci wirtualnej tooflow za pośrednictwem hello VPN bramy dołączonych toohello połączyć za pomocą sieci wirtualnej. Jeśli zaznaczysz to pole hello połączyć za pomocą sieci wirtualnej muszą mieć tooit dołączony bramy sieci wirtualnej i musi mieć hello **Zezwalaj bramy przesyłania** zaznaczono element checkbox. Pozostawienie to niezaznaczone pole (ustawienie domyślne), ruch z sieci wirtualnej połączyć za pomocą hello nadal przepływ toothis wirtualnych sieci, ale nie można wykonać przepływu za pośrednictwem sieci wirtualnej dołączonych toothis bramy sieci wirtualnej. 
    
    Nie można włączyć tę opcję, jeśli w przypadku komunikacji równorzędnej sieć wirtualną (Resource Manager) z siecią wirtualną (klasyczny). Chociaż hello ruch przepływa między dwiema sieciami wirtualnymi hello, hello ruchu sieci wirtualnej (Resource Manager) nie można wykonać przepływu za pośrednictwem sieci bramy dołączonych toohello sieci wirtualnej (wdrożenia klasyczne).
7. Kliknij przycisk hello **OK** przycisk tooadd hello podsieci toohello sieci wirtualnej wybrane.

### <a name="commands"></a>Polecenia

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia|[równorzędna az sieci wirtualne sieci równorzędne — tworzenie](/cli/azure/network/vnet/peering#create?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Dodaj AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json)|


### <a name="scenarios"></a>Scenariusze

Utworzeniu sieci wirtualnej komunikacji równorzędnej między sieciami wirtualnymi, została utworzona za pośrednictwem hello takie same lub różne modele wdrażania znajdujące się w hello tych samych lub różnych subskrypcji. Wykonaj krok samouczka jednego hello następujące scenariusze:
 
|Model wdrażania platformy Azure  | Subskrypcja  |
|---------|---------|
|Resource Manager — w obu przypadkach |[Ta sama](virtual-network-create-peering.md)|
| |[Różne](create-peering-different-subscriptions.md)|
|Jedna sieć — Resource Manager, druga — model klasyczny     |[Ta sama](create-peering-different-deployment-models.md)|
| |[Różne](create-peering-different-deployment-models-subscriptions.md)|

## <a name="view-or-change-peering-settings"></a>Wyświetl lub zmień ustawienia komunikacji równorzędnej

1. Zaloguj się za toohello [portal](https://portal.azure.com) przy użyciu konta przypisanego konieczne hello [roli lub uprawnienia](#permissions).
2. W polu hello, które zawiera tekst hello *wyszukiwania zasobów* u góry hello hello portalu Azure, wpisz *sieci wirtualnych*. Gdy **sieci wirtualnych** pojawia się w wynikach wyszukiwania hello, kliknij ją.
3. W hello **sieci wirtualnych** bloku, który jest wyświetlany, kliknij przycisk hello sieci wirtualnej mają toocreate komunikacji równorzędnej dla.
4. W okienku hello wyświetlany dla sieci wirtualnej hello wybrano kliknij **komunikacji równorzędnych** w hello **ustawienia** sekcji.
5. Kliknij przycisk równorzędna hello mają tooview lub zmienić ustawienia.
6. Zmień odpowiednie ustawienia hello. Przeczytaj informacje o hello opcje dla każdego ustawienia w [krok 6](#add-peering) z hello utworzyć komunikacji równorzędnej sekcji tego artykułu. 

    >[!NOTE]
    >Istnieje kilka wymagań, ograniczeń i toosuccessfully uwagi dotyczące tworzenia sieci wirtualnej komunikacji równorzędnej. Przed utworzeniem komunikacji równorzędnej, upewnij się, po zapoznaniu się ze hello [wymagań i ograniczeń](#requirements-and-constraints) i [wymagane uprawnienia](#permissions).
    >

7. Kliknij pozycję **Zapisz**.

**Polecenia**

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia|[Lista komunikacji równorzędnej az sieci wirtualnej](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#list) komunikacji równorzędnych toolist sieci wirtualnej [az sieci vnet show komunikacji równorzędnej](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#show) tooshow ustawienia dla określonego komunikacji równorzędnej, i [komunikacji równorzędnej aktualizacja sieci wirtualnej sieci az](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#update) ustawienia komunikacji równorzędnej toochange.|
|PowerShell|[Get-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/get-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json) tooretrieve wyświetlić ustawienia komunikacji równorzędnej i [AzureRmVirtualNetworkPeering zestaw](/powershell/module/azurerm.network/set-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json) toochange ustawienia.|

## <a name="delete-a-peering"></a>Usuń element równorzędny
Po usunięciu komunikacji równorzędnej z sieci wirtualnej nie jest już przepływa ruch toohello połączyć za pomocą sieci wirtualnej. Sieci wirtualne są wdrażane za pomocą Menedżera zasobów są połączyć za pomocą, każdej sieci wirtualnej ma komunikacji równorzędnej toohello innych sieci wirtualnej. Chociaż usuwanie hello komunikacji równorzędnej z jedną sieć wirtualną wyłącza hello komunikacji między sieciami wirtualnymi hello, nie są usuwane z hello komunikacji równorzędnej hello innych sieci wirtualnej. Witaj stan komunikacji równorzędnej dla hello komunikacji równorzędnej, który istnieje w hello innych sieci wirtualnej jest **Rozłączono**. Nie można odtworzyć hello komunikacji równorzędnej, dopóki ponownie utworzyć hello równorzędna w pierwszej sieci wirtualnej hello i hello stan komunikacji równorzędnej dla wirtualnych sieci zmiany zbyt*połączony*. 

Jeśli czasami będzie toocommunicate sieci wirtualnych, ale nie zawsze, zamiast usuwania komunikacji równorzędnej, można ustawić hello **Zezwalaj na dostęp do sieci wirtualnej** ustawienie zbyt**wyłączone** zamiast tego. jak to zrobić, przeczytaj toolearn krok 6 hello [utworzyć komunikacji równorzędnej](#create-peering) sekcji tego artykułu. Może się okazać wyłączania i włączania łatwiejsze niż usunięcie i ponowne utworzenie komunikacji równorzędnych dostępu do sieci.

1. Zaloguj się za toohello [portal](https://portal.azure.com) przy użyciu konta przypisanego konieczne hello [roli lub uprawnienia](#permissions).
2. W polu hello, które zawiera tekst hello *wyszukiwania zasobów* u góry hello hello portalu Azure, wpisz *sieci wirtualnych*. Gdy **sieci wirtualnych** pojawia się w wynikach wyszukiwania hello, kliknij ją.
3. W hello **sieci wirtualnych** bloku, który jest wyświetlany, kliknij przycisk hello sieci wirtualnej mają toodelete komunikacji równorzędnej z.
4. W hello wyświetlonym bloku dla sieci wirtualnej hello wybrano kliknij **komunikacji równorzędnych** w obszarze **ustawienia**.
5. Na liście hello komunikacji równorzędnych pojawiające się w bloku komunikacji równorzędnych hello powitania kliknij prawym przyciskiem myszy równorzędna zostanie chcesz toodelete, kliknij **usunąć**, następnie **tak** hello toodelete komunikacji równorzędnej z hello pierwszej sieci wirtualnej.
6. Zakończenie hello poprzednie kroki toodelete hello komunikacji równorzędnej z hello innych sieci wirtualnej w komunikacji równorzędnej hello.

**Polecenia**

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia|[AZ sieci wirtualnej komunikacji równorzędnej usunięcie](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Usuń AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/remove-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="requirements-and-constraints"></a>Wymagania i ograniczenia 

- Hello sieci wirtualnych, które można elementu równorzędnego musi mieć-nakładającymi się obszarami adresów IP.
- Nie można dodać obszary adresów, lub usuń przestrzeni adresów z sieci wirtualnej, po sieci wirtualnej jest połączyć za pomocą z innej sieci wirtualnej. tooadd lub usuń przestrzenie adresowe hello delete komunikacji równorzędnej, Dodaj lub usuń hello przestrzeni adresów, a następnie ponownie utwórz hello komunikacji równorzędnej. tooadd rozwiązania do magazynowania, lub usuń przestrzeni adresowych z sieciami wirtualnymi, przeczytaj hello [tworzenie, zmienianie i usuwanie sieci wirtualnych](virtual-network-manage-network.md#add-address-spaces) artykułu. 
- Można równorzędne dwie sieci wirtualne wdrożone za pośrednictwem Menedżera zasobów lub sieci wirtualnej wdrożone za pomocą Menedżera zasobów z siecią wirtualną wdrożone za pośrednictwem hello klasycznego modelu wdrażania. Nie można równorzędne dwie sieci wirtualne utworzone za pośrednictwem hello klasycznego modelu wdrażania. Jeśli nie masz doświadczenia w obsłudze modele wdrażania platformy Azure, przeczytaj hello [modele wdrażania zrozumieć Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykułu. Można użyć [bramy sieci VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect dwie sieci wirtualne utworzone za pośrednictwem hello klasycznego modelu wdrażania.
- Podczas komunikacji równorzędnej dwie sieci wirtualne utworzone za pomocą Menedżera zasobów, równorzędna muszą być skonfigurowane dla każdej sieci wirtualnej w komunikacji równorzędnej hello. Po utworzeniu hello komunikacji równorzędnej toohello drugiej sieci wirtualnej z pierwszej sieci wirtualnej hello stan komunikacji równorzędnej hello jest *zainicjowano*.  Podczas tworzenia hello komunikacji równorzędnej z pierwszej sieci wirtualnej hello sieci wirtualnej drugi toohello, jego stan komunikacji równorzędnej jest *połączony*. Jeśli możesz wyświetlić stan komunikacji równorzędnej hello hello pierwszej sieci wirtualnej, zobacz jego stan zmienił się z *zainicjowano* za*połączony*. równorzędna Hello nie zostanie pomyślnie nawiązane momentu hello stan komunikacji równorzędnej dla obu komunikacji równorzędnych sieci wirtualnych *połączony*. 
- Podczas komunikacji równorzędnej sieci wirtualnej utworzonej za pomocą Menedżera zasobów z siecią wirtualną, która została utworzona za pośrednictwem hello klasycznego modelu wdrażania, można skonfigurować tylko komunikacji równorzędnej dla sieci wirtualnej hello wdrożone za pomocą Menedżera zasobów. Nie można skonfigurować komunikację równorzędną sieci wirtualnej (wdrożenia klasyczne) lub między dwiema sieciami wirtualnej wdrożone za pośrednictwem hello klasycznego modelu wdrażania. Podczas tworzenia hello komunikacji równorzędnej z hello sieci wirtualnej (Resource Manager) toohello sieć wirtualna (klasyczna), stan komunikacji równorzędnej hello jest *aktualizacji*, wkrótce zmiany zbyt*połączony*.   
- Komunikacja równorzędna została ustanowiona między dwiema sieciami wirtualnymi. Komunikacji równorzędnych nie są przechodnie. Jeśli utworzysz komunikacji równorzędnych między:
    - VirtualNetwork1 & VirtualNetwork2
    - VirtualNetwork2 & VirtualNetwork3

  Nie ma żadnych komunikacji równorzędnej między VirtualNetwork1 i VirtualNetwork3 za pośrednictwem VirtualNetwork2. Jeśli chcesz toocreate sieci wirtualnej komunikacji równorzędnej między VirtualNetwork1 i VirtualNetwork3, masz toocreate komunikacji równorzędnej między VirtualNetwork1 i VirtualNetwork3.
- Nie można rozpoznać nazwy w połączyć za pomocą sieci wirtualnych za pomocą domyślnego rozwiązania nazwa platformy Azure. nazwy tooresolve w innych sieciach wirtualnych, należy użyć niestandardowego serwera DNS. toolearn sposób odczytać tooset własny serwer DNS hello [rozpoznawanie nazw przy użyciu serwera DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) artykułu.
- Zasoby w obie sieci wirtualne w komunikacji równorzędnej hello może komunikować się ze sobą z hello sam przepustowości i opóźnień tak, jakby były hello są takie same sieci wirtualnej. Rozmiar każdej maszyny wirtualnej ma jednak własną maksymalną przepustowość sieci. więcej informacji na temat maksymalną przepustowość sieci dla rozmiarów inną maszynę wirtualną, przeczytaj hello toolearn [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) lub [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykuły rozmiary maszyny wirtualnej.
- Można elementu równorzędnego sieci wirtualne wdrożone za pomocą Menedżera zasobów, które są w hello, lub różnych subskrypcji.
- Można elementów równorzędnych sieci wirtualnych wdrożonych przez różne modele wdrażania, które są w hello, lub różnych subskrypcji (wersja zapoznawcza). 
- Witaj subskrypcje, które są obie sieci wirtualne w musi być skojarzony toohello tej samej dzierżawy usługi Azure Active Directory. Jeśli nie masz już dzierżawę AD, możesz szybko [utworzyć](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch). Można użyć [bramy sieci VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect dwóch sieci wirtualnych, które istnieją w ramach różnych subskrypcji skojarzone toodifferent dzierżawcy usługi Active Directory.
- Sieć wirtualną można połączyć za pomocą tooanother sieci wirtualnej i również być tooanother połączonych sieci wirtualnej z bramą sieci wirtualnej platformy Azure. Jeśli sieci wirtualne są połączone za pośrednictwem komunikacji równorzędnej i bramy, ruchu między sieciami wirtualnymi hello przechodzi przez hello konfiguracji komunikacji równorzędnej, zamiast hello bramy.
- Istnieje nominalna opłata za ruch przychodzący i wychodzący w wirtualnych sieciach równorzędnych. Aby uzyskać więcej informacji, zobacz hello [cennikiem](https://azure.microsoft.com/pricing/details/virtual-network).


## <a name="permissions"></a>Uprawnienia

konta Hello się, że używasz toocreate sieci wirtualnej komunikacji równorzędnej musi mieć hello ról lub uprawnień. Na przykład jeśli zostały równorzędna dwie sieci wirtualne o nazwach myVnetA i myVnetB, Twoje konto musi zostać przypisane hello następujące minimalne roli lub uprawnienia dla każdej sieci wirtualnej:
    
|Sieć wirtualna|Model wdrażania|Rola|Uprawnienia|
|---|---|---|---|
|myVnetA|Resource Manager|[Współautor sieci](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Wdrożenie klasyczne|[Współautor klasycznej sieci](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Nie dotyczy|
|myVnetB|Resource Manager|[Współautor sieci](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Wdrożenie klasyczne|[Współautor klasycznej sieci](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

Dowiedz się więcej o [wbudowane role](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) i przypisywanie uprawnień określonych zbyt[role niestandardowe](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (tylko Resource Manager).

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak toocreate [gwiazdy topologii sieci](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 
