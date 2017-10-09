---
title: "aaaCreate równorzędna sieci wirtualnej platformy Azure — wdrożenia różnych modeli - różnych subskrypcji | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate sieci wirtualnej komunikacji równorzędnej między sieciami wirtualnymi została utworzona za pośrednictwem różne Azure modele wdrażania znajdujące się w różnych subskrypcji platformy Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: 865bdabb5b87523ba943d7b5dcbdc2475b78bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-and-subscriptions"></a>Tworzenie sieci wirtualnej równorzędna — różne modele wdrażania i subskrypcji

Z tego samouczka dowiesz się toocreate sieci wirtualnej komunikacji równorzędnej między sieciami wirtualnymi utworzone przez różne modele wdrażania. sieci wirtualne Hello istnieje w ramach różnych subskrypcji. Witaj komunikacji równorzędnej dwa zasoby umożliwia sieci wirtualnych w różnych sieciach wirtualnych toocommunicate ze sobą z tej samej przepustowości i opóźnień tak, jakby hello zasoby były hello tej samej sieci wirtualnej. Dowiedz się więcej o [równorzędna sieci wirtualnej](virtual-network-peering-overview.md). 

Witaj toocreate kroki sieci wirtualnej komunikacji równorzędnej są różne, w zależności od tego, czy hello sieci wirtualne są w hello tych samych lub różnych subskrypcji i które [modelu wdrożenia usługi Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello sieci wirtualne są tworzone za pomocą. Dowiedz się, jak toocreate a wirtualnych sieci równorzędna w innych sytuacjach, klikając hello scenariusza z hello w poniższej tabeli:

|Model wdrażania platformy Azure  | Subskrypcja platformy Azure  |
|--------- |---------|
|[Obie usługi Resource Manager](virtual-network-create-peering.md) |tym samym|
|[Obie usługi Resource Manager](create-peering-different-subscriptions.md) |Różne|
|[Jeden Resource Manager, co classic](create-peering-different-deployment-models.md) |tym samym|

Nie można utworzyć sieci wirtualnej komunikacji równorzędnej między dwiema sieciami wirtualnej wdrożone za pośrednictwem hello klasycznego modelu wdrażania. Element równorzędny sieci wirtualnej można tworzyć tylko między dwiema sieciami wirtualnych, które istnieją w hello sam region platformy Azure. Podczas tworzenia sieci wirtualnej komunikacji równorzędnej między sieciami wirtualnymi, które istnieją w ramach różnych subskrypcji, powitalne subskrypcje muszą być skojarzone toohello same usługi Azure Active Directory dzierżawy. Jeśli nie masz już dzierżawę usługi Azure Active Directory, możesz szybko [utworzyć](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch). Jeśli potrzebujesz tooconnect wirtualnych sieci zarówno utworzonych za pomocą hello klasycznego modelu wdrażania, który istnieje w różnych regionach platformy Azure lub który istnieje w subskrypcji skojarzone toodifferent dzierżaw usługi Azure Active Directory, możesz użyć Azure [Bramy sieci VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello sieci wirtualnych. 

> [!WARNING]
> Tworzenie sieci wirtualnej komunikacji równorzędnej między sieciami wirtualnymi w utworzonych za pomocą różnych wdrożenia usługi Azure modeli, które istnieją w ramach różnych subskrypcji jest obecnie w wersji zapoznawczej. Komunikacji równorzędnych sieci wirtualnych utworzonych w tym scenariuszu nie może mieć hello sam poziom dostępności i niezawodności, jak podczas tworzenia sieci wirtualnej komunikacji równorzędnej w scenariuszach ogólnie wersji dostępności. Komunikacji równorzędnych sieci wirtualnych utworzonych w tym scenariuszu nie są obsługiwane, mogą mieć ograniczone możliwości i mogą nie być dostępne we wszystkich regionach platformy Azure. Najbardziej aktualne powiadomień hello na dostępność i stan tej funkcji, sprawdź hello [aktualizuje sieci wirtualnej Azure](https://azure.microsoft.com/updates/?product=virtual-network) strony.

Można użyć hello [portalu Azure](#portal), hello Azure [interfejsu wiersza polecenia](#cli) (CLI) lub Azure [PowerShell](#powershell) toocreate sieci wirtualnej komunikacji równorzędnej. Kliknij dowolny z hello poprzedniego narzędzia łącza toogo, bezpośrednio toohello kroki tworzenia sieci wirtualnej komunikacji równorzędnej narzędzie wyboru.

## <a name="register"></a>Rejestr hello podglądu

tooregister hello podglądu, pełną hello kroki, które należy wykonać dla obu subskrypcji, które zawierają hello sieci wirtualnej mają toopeer. Witaj tylko tooregister można użyć wersji zapoznawczej hello jest narzędzie programu PowerShell.

1. Zainstaluj najnowszą wersję hello PowerShell hello [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modułu. Jeśli jesteś tooAzure nowego środowiska PowerShell, zobacz [Omówienie programu Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Uruchom sesję programu PowerShell i zaloguj się przy użyciu hello tooAzure `login-azurermaccount` polecenia.
3. Rejestracja subskrypcji dla podglądu hello wprowadzając hello następującego polecenia:

    ```powershell
    Register-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    
    Register-AzureRmResourceProvider `
      -ProviderNamespace Microsoft.Network
    ```
    Nie wykonać kroki hello w sekcjach portalu, wiersza polecenia platformy Azure lub programu PowerShell hello tego artykułu do hello **RegistrationState** output, pojawi się po wprowadzeniu hello następujące polecenia **zarejestrowanej** dla obu subskrypcji:

    ```powershell    
    Get-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    ```

## <a name="portal"></a>Utwórz równorzędna - portalu Azure

W tym samouczku korzysta z różnych kont dla każdej subskrypcji. Jeśli używasz konta mającego uprawnienia tooboth subskrypcji, można użyć hello takie same konta dla wszystkich kroków, pomiń kroki hello rejestrowania poza hello portalu i pominąć kroki hello przypisywania sieci wirtualnych toohello uprawnienia innego użytkownika. Przed wykonaniem dowolnej hello następujące kroki, należy zarejestrować hello podglądu. tooregister, pełną hello etapami hello [zarejestrować w wersji zapoznawczej hello](#register) sekcji tego artykułu. Nie wykonuj pozostałych czynności, dopóki obie subskrypcje są zarejestrowane dla podglądu hello hello.
 
1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com) jako Użytkownik_a. Zaloguj się przy użyciu konta Hello musi mieć hello toocreate niezbędne uprawnienia sieci wirtualnej komunikacji równorzędnej. Zobacz hello [uprawnienia](#permissions) sekcji tego artykułu, aby uzyskać szczegółowe informacje.
2. Kliknij przycisk **+ nowy**, kliknij przycisk **sieci**, następnie kliknij przycisk **sieci wirtualnej**.
3. W hello **Utwórz sieć wirtualną** bloku, wprowadź, lub wybierz wartości dla hello następujące ustawienia, a następnie kliknij **Utwórz**:
    - **Nazwa**: *myVnetA*
    - **Przestrzeń adresowa**: *10.0.0.0/16*
    - **Nazwa podsieci**: *domyślne*
    - **Zakres adresów podsieci**: *10.0.0.0/24*
    - **Subskrypcja**: Wybierz subskrypcję A.
    - **Grupa zasobów**: Wybierz **Utwórz nowy** , a następnie wprowadź *myResourceGroupA*
    - **Lokalizacja**: *wschodnie stany USA*
4. W hello **wyszukiwania zasobów** pole u góry hello hello portalu, typ *myVnetA*. Kliknij przycisk **myVnetA** po wyświetleniu w wynikach wyszukiwania hello. Zostanie wyświetlony blok hello **myVnetA** sieci wirtualnej.
5. W hello **myVnetA** bloku, który jest wyświetlany, kliknij przycisk **(IAM) kontroli dostępu** z hello pionowy listy opcji na powitania po lewej stronie powitania bloku.
6. W hello **myVnetA — kontrola dostępu (IAM)** bloku, który jest wyświetlany, kliknij przycisk **+ Dodaj**.
7. W hello **dodać uprawnienia** wyświetlonym bloku, wybierz **współautora sieci** w hello **roli** pole.
8. W hello **wybierz** wybierz Użytkownik_b lub wpisz toosearch adres e-mail firmy Użytkownik_b. Witaj listę użytkowników, wyświetlany jest z hello tej samej dzierżawy usługi Azure Active Directory, co sieć wirtualna hello konfigurujesz hello komunikacji równorzędnej dla. Wygląda na to, na liście powitania kliknij przycisk Użytkownik_b.
9. Kliknij pozycję **Zapisz**.
10. Wyloguj się z portalu hello jako Użytkownik_a, a następnie zaloguj się jako Użytkownik_b.
11. Kliknij przycisk **+ nowy**, typ *sieci wirtualnej* w hello **hello wyszukiwania portalu Marketplace** polu, a następnie kliknij przycisk **sieci wirtualnej** w wynikach wyszukiwania hello .
12. W hello **sieci wirtualnej** wyświetlonym bloku, wybierz **klasycznego** w hello **wybierz model wdrożenia** polu, a następnie kliknij przycisk **Utwórz**.
13.   Witaj Utwórz sieć wirtualna (klasyczna) pojawi się okno wprowadź hello następujące wartości:

    - **Nazwa**: *myVnetB*
    - **Przestrzeń adresowa**: *10.1.0.0/16*
    - **Nazwa podsieci**: *domyślne*
    - **Zakres adresów podsieci**: *10.1.0.0/24*
    - **Subskrypcja**: Wybierz subskrypcję B.
    - **Grupa zasobów**: Wybierz **Utwórz nowy** , a następnie wprowadź *myResourceGroupB*
    - **Lokalizacja**: *wschodnie stany USA*

14. W hello **wyszukiwania zasobów** pole u góry hello hello portalu, typ *myVnetB*. Kliknij przycisk **myVnetB** po wyświetleniu w wynikach wyszukiwania hello. Zostanie wyświetlony blok hello **myVnetB** sieci wirtualnej.
15. W hello **myVnetB** bloku, który jest wyświetlany, kliknij przycisk **właściwości** z hello pionowy listy opcji na powitania po lewej stronie powitania bloku. Kopiuj hello **identyfikator ZASOBU**, która jest używana w kolejnym kroku. Identyfikator zasobu Hello jest toohello podobnie poniższy przykład: /subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
16. Wykonaj kroki 5 – 9 dla myVnetB wprowadzania **Użytkownik_a** w kroku 8.
17. Wyloguj się z portalu hello jako Użytkownik_b i zaloguj się jako Użytkownik_a.
18. W hello **wyszukiwania zasobów** pole u góry hello hello portalu, typ *myVnetA*. Kliknij przycisk **myVnetA** po wyświetleniu w wynikach wyszukiwania hello. Zostanie wyświetlony blok hello **myVnet** sieci wirtualnej.
19. Kliknij przycisk **myVnetA**.
20. W hello **myVnetA** bloku, który jest wyświetlany, kliknij przycisk **komunikacji równorzędnych** z hello pionowy listy opcji na powitania po lewej stronie powitania bloku.
21. W hello **myVnetA - komunikacji równorzędnych** bloku, które wystąpiły, kliknij przycisk **+ Dodaj**
22. W hello **równorzędna Dodaj** bloku, zostanie wyświetlone, wprowadź, lub wybierz hello następujące opcje, a następnie kliknij **OK**:
     - **Nazwa**: *myVnetAToMyVnetB*
     - **Model wdrażania sieci wirtualnej**: Wybierz **klasycznego**.
     - **Sprawdzić mój identyfikator zasobu**: Zaznacz to pole wyboru.
     - **Identyfikator zasobu**: Wprowadź identyfikator zasobu hello myVnetB z kroku 15.
     - **Zezwalaj na dostęp do sieci wirtualnej:** upewnij się, że **włączone** jest zaznaczone.
    W tym samouczku są używane żadne inne ustawienia. Przeczytaj toolearn dotyczące wszystkich ustawień komunikacji równorzędnej, [Zarządzanie komunikacji równorzędnych sieci wirtualnych](virtual-network-manage-peering.md#create-a-peering).
23. Po kliknięciu przycisku **OK** w poprzednim kroku hello hello **równorzędna Dodaj** bloku zamyka i zobacz hello **myVnetA - komunikacji równorzędnych** ponownie blok. Po kilku sekundach hello równorzędna utworzonego pojawia się w bloku hello. **Połączone** ma na liście hello **RÓWNORZĘDNA stan** kolumny dla hello **myVnetAToMyVnetB** równorzędna zostanie utworzony. Witaj równorzędna zostanie ustanowione. Nie jest brak konieczności toopeer hello sieć wirtualna (klasyczna) toohello wirtualnego sieć (Resource Manager).

    Dowolnych zasobów platformy Azure, utworzone w każdej sieci wirtualnej są teraz możliwe toocommunicate ze sobą za pośrednictwem ich adresy IP. Jeśli używasz domyślnego rozwiązania Azure nazwy dla sieci wirtualnych hello, hello zasoby w sieciach wirtualnych hello nie są możliwe tooresolve nazw w sieciach wirtualnych hello. Jeśli chcesz nazwy tooresolve między sieciami wirtualnymi w komunikacji równorzędnej, należy utworzyć serwer DNS. Dowiedz się, jak tooset się [rozpoznawanie nazw przy użyciu serwera DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

24. **Opcjonalne**: Chociaż tworzenia maszyn wirtualnych nie została uwzględniona w tym samouczku, można utworzyć maszynę wirtualną w każdej sieci wirtualnej i połączyć z jednej maszyny wirtualnej toohello innych, toovalidate łączności.
25. **Opcjonalne**: toodelete hello zasobów, które możesz utworzyć w tym samouczku, pełną hello etapami hello [zasoby zostaną usunięte](#delete-portal) sekcji tego artykułu.

## <a name="cli"></a>Utwórz równorzędna - wiersza polecenia platformy Azure

W tym samouczku korzysta z różnych kont dla każdej subskrypcji. Jeśli używasz konta mającego uprawnienia tooboth subskrypcji, można użyć hello same konta dla wszystkich kroków, pomiń kroki hello logowania z platformy Azure i usunąć wiersze hello skryptu, utworzonych przypisań ról użytkownika. Zastąp UserA@azure.com i UserB@azure.com we wszystkich hello następujące skrypty z nazw użytkowników hello używasz Użytkownik_a i Użytkownik_b. 

Przed wykonaniem dowolnej hello następujące kroki, należy zarejestrować hello podglądu. tooregister, pełną hello etapami hello [zarejestrować w wersji zapoznawczej hello](#register) sekcji tego artykułu. Nie wykonuj pozostałych czynności, dopóki obie subskrypcje są zarejestrowane dla podglądu hello hello.

1. [Zainstaluj](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello Azure CLI 1.0 toocreate hello sieć wirtualna (klasyczna).
2. Otwórz sesję interfejsu wiersza polecenia, a następnie zaloguj tooAzure jako Użytkownik_b przy użyciu hello `azure login` polecenia.
3. Uruchom hello interfejsu wiersza polecenia w trybie zarządzania usługami, wprowadzając hello `azure config mode asm` polecenia.
4. Wprowadź hello następujące polecenia toocreate hello sieć wirtualna (klasyczna):
 
    ```azurecli
    azure network vnet create --vnet myVnetB --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```
5. Hello pozostałe kroki należy wykonać przy użyciu powłoki bash z hello Azure CLI 2.0.4 lub nowszym [zainstalowane](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json), lub za pomocą hello powłoki chmury Azure. Hello powłoki chmury Azure jest bezpłatna powłoki Bash, który można uruchomić bezpośrednio z poziomu hello portalu Azure. Ma ona hello Azure CLI wstępnie zainstalowane i skonfigurowane toouse z Twoim kontem. Kliknij przycisk hello **wypróbuj** przycisku na powitania skryptów poniżej, która otwiera powłokę chmury, który loguje tooyour konto platformy Azure. Opcje uruchamiania bash skrypty interfejsu wiersza polecenia na komputerze klienckim z systemem Windows, temacie [działający w systemie Windows hello Azure CLI](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 
6. Skopiuj powitania po Edytor tekstu tooa skryptu na komputerze. Zastąp `<SubscriptionB-Id>` z identyfikatorem subskrypcji Jeśli nie znasz identyfikator subskrypcji, wprowadź hello `az account show` polecenia. Witaj wartość **identyfikator** w hello jest identyfikator subskrypcji Skopiuj skrypt hello zmodyfikowane, wklej go w sesji tooyour 2.0 interfejsu wiersza polecenia i naciśnij klawisz `Enter`. 

    ```azurecli-interactive
    az role assignment create \
      --assignee UserA@azure.com \
      --role "Classic Network Contributor" \
      --scope /subscriptions/<SubscriptionB-Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

    Podczas tworzenia sieci wirtualnej hello (klasyczne) w kroku 4, Azure utworzone sieci wirtualnej hello w hello *sieci domyślne* grupy zasobów.
7. Zaloguj się Użytkownik_b poza Azure i zaloguj się jako Użytkownik_a hello 2.0 interfejsu wiersza polecenia.
8. Utwórz grupę zasobów i sieć wirtualną (Resource Manager). Następujące hello kopii skryptu, wklej go w tooyour sesji interfejsu wiersza polecenia i naciśnij klawisz `Enter`. 

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroupA"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network A (Resource Manager).
    az network vnet create \
      --name myVnetA \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Get hello id for myVnetA.
    vNetAId=$(az network vnet show \
      --resource-group $rgName \
      --name myVnetA \
      --query id --out tsv)

    # Assign UserB permissions toomyVnetA.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope $vNetAId
    ```

9. Tworzenie sieci wirtualnej komunikacji równorzędnej między Witaj dwie sieci wirtualne utworzone za pośrednictwem hello różne modele wdrażania. Skopiuj powitania po Edytor tekstu tooa skryptu na komputerze. Zastąp `<SubscriptionB-id>` z Twojego identyfikatora subskrypcji. Jeśli nie znasz identyfikator subskrypcji, wprowadź hello `az account show` polecenia. Witaj wartość **identyfikator** w hello jest identyfikator subskrypcji Azure utworzona sieć wirtualna hello (klasyczne) został utworzony w kroku 4 w grupie zasobów o nazwie *sieci domyślne*. Wklej hello zmodyfikować skrypt w sesji interfejsu wiersza polecenia, a następnie naciśnij klawisz `Enter`.

    ```azurecli-interactive
    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnetAToMyVnetB \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --remote-vnet-id  /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB \
      --allow-vnet-access
    ```

10. Po wykonaniu skryptu hello, przejrzyj hello komunikacji równorzędnej dla sieci wirtualnej hello (Resource Manager). Skopiuj hello następującego skryptu, a następnie wklej go w sesji interfejsu wiersza polecenia:

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --output table
    ```
    przedstawia dane wyjściowe Hello **połączony** w hello **PeeringState** kolumny.

    Dowolnych zasobów platformy Azure, utworzone w każdej sieci wirtualnej są teraz możliwe toocommunicate ze sobą za pośrednictwem ich adresy IP. Jeśli używasz domyślnego rozwiązania Azure nazwy dla sieci wirtualnych hello, hello zasoby w sieciach wirtualnych hello nie są możliwe tooresolve nazw w sieciach wirtualnych hello. Jeśli chcesz nazwy tooresolve między sieciami wirtualnymi w komunikacji równorzędnej, należy utworzyć serwer DNS. Dowiedz się, jak tooset się [rozpoznawanie nazw przy użyciu serwera DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

11. **Opcjonalne**: Chociaż tworzenia maszyn wirtualnych nie została uwzględniona w tym samouczku, można utworzyć maszynę wirtualną w każdej sieci wirtualnej i połączyć z jednej maszyny wirtualnej toohello innych, toovalidate łączności.
12. **Opcjonalne**: toodelete hello zasobów, które możesz utworzyć w tym samouczku, pełną hello czynnościach w ramach [zasoby zostaną usunięte](#delete-cli) w tym artykule.

## <a name="powershell"></a>Utwórz równorzędna — PowerShell

W tym samouczku korzysta z różnych kont dla każdej subskrypcji. Jeśli używasz konta mającego uprawnienia tooboth subskrypcji, można użyć hello same konta dla wszystkich kroków, pomiń kroki hello logowania z platformy Azure i usunąć wiersze hello skryptu, utworzonych przypisań ról użytkownika. Zastąp UserA@azure.com i UserB@azure.com we wszystkich hello następujące skrypty z nazw użytkowników hello używasz Użytkownik_a i Użytkownik_b. 

Przed wykonaniem dowolnej hello następujące kroki, należy zarejestrować hello podglądu. tooregister, pełną hello etapami hello [zarejestrować w wersji zapoznawczej hello](#register) sekcji tego artykułu. Nie wykonuj pozostałych czynności, dopóki obie subskrypcje są zarejestrowane dla podglądu hello hello.

1. Zainstaluj najnowszą wersję hello PowerShell hello [Azure](https://www.powershellgallery.com/packages/Azure) i [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modułów. Jeśli jesteś tooAzure nowego środowiska PowerShell, zobacz [Omówienie programu Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Uruchom sesję programu PowerShell.
3. W programie PowerShell, zaloguj się w ramach subskrypcji w tooUserB jako Użytkownik_b wprowadzając hello `Add-AzureAccount` polecenia.
4. toocreate sieci wirtualnej (wdrożenia klasyczne) przy użyciu programu PowerShell, należy utworzyć nową, lub zmodyfikować istniejący plik konfiguracji sieci. Dowiedz się, jak za[eksportu, aktualizować i importowanie plików konfiguracyjnych sieci](virtual-networks-using-network-configuration-file.md). Witaj pliku powinny zawierać następujące hello **VirtualNetworkSite** elementu dla sieci wirtualnej hello używane w tym samouczku:

    ```xml
    <VirtualNetworkSite name="myVnetB" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > Importowanie pliku konfiguracji sieci zmienione może spowodować zmiany tooexisting sieciami wirtualnymi (klasyczne) w ramach subskrypcji. Upewnij się, tylko dodać hello poprzedniej sieci wirtualnej i nie zmienić lub usunąć istniejące sieci wirtualnych z subskrypcji. 

5. Zaloguj się na tooUserB subskrypcji jako polecenia Menedżera zasobów toouse Użytkownik_b wprowadzając hello `login-azurermaccount` polecenia.
6. Przypisz Użytkownik_a uprawnienia toovirtual sieci kopii B. hello następujący skrypt tooa edytora tekstu, na komputerze i Zastąp `<SubscriptionB-id>` o identyfikatorze hello subskrypcji B. Jeśli nie znasz identyfikator subskrypcji hello, wprowadź hello `Get-AzureRmSubscription` tooview polecenia go. Witaj wartość **identyfikator** w hello zwrócone dane wyjściowe są Twojego identyfikatora subskrypcji. Azure utworzona sieć wirtualna hello (klasyczne) został utworzony w kroku 4 w grupie zasobów o nazwie *sieci domyślne*. tooexecute hello skryptu, hello kopiowania zmodyfikować skrypt, wklej go w tooPowerShell, a następnie naciśnij `Enter`.
    
    ```powershell 
    New-AzureRmRoleAssignment `
      -SignInName UserA@azure.com `
      -RoleDefinitionName "Classic Network Contributor" `
      -Scope /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

7. Wyloguj się Azure jako Użytkownik_b i logowania w ramach subskrypcji w tooUserA jako Użytkownik_a wprowadzając hello `login-azurermaccount` polecenia. Zaloguj się przy użyciu konta Hello musi mieć hello toocreate niezbędne uprawnienia sieci wirtualnej komunikacji równorzędnej. Zobacz hello [uprawnienia](#permissions) sekcji tego artykułu, aby uzyskać szczegółowe informacje.
8. Utwórz sieć wirtualną hello (Resource Manager) przez skopiowanie hello następującego skryptu, wklejając je w tooPowerShell, a następnie naciskając klawisz `Enter`:

    ```powershell
    # Variables for common values
      $rgName='MyResourceGroupA'
      $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network A.
    $vnetA = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnetA' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location
    ```

9. Przypisz toomyVnetA uprawnienia Użytkownik_b. Kopiuj hello następujący skrypt tooa edytora tekstu, na komputerze i Zastąp `<SubscriptionA-Id>` o identyfikatorze hello subskrypcji A. Jeśli nie znasz identyfikator subskrypcji hello, wprowadź hello `Get-AzureRmSubscription` tooview polecenia go. Witaj wartość **identyfikator** w hello zwrócone dane wyjściowe są Twojego identyfikatora subskrypcji. Wklej hello zmodyfikowanej wersji hello skryptu w programie PowerShell, a następnie naciśnij klawisz `Enter` tooexecute go.

    ```powershell
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

10. Kopia hello następujący skrypt tooa edytora tekstu, na komputerze i Zastąp `<SubscriptionB-id>` o identyfikatorze hello subskrypcji B. toopeer myVnetA toomyVNetB, skopiuj skrypt hello zmodyfikowane, wklej go w tooPowerShell, a następnie naciśnij `Enter`.

    ```powershell
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vnetA `
      -RemoteVirtualNetworkId /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

11. Wyświetlić stan komunikacji równorzędnej hello myVnetA przez skopiowanie hello następującego skryptu, wklejając je w programie PowerShell i naciskając klawisz `Enter`.

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName $rgName `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Stan Hello jest **połączony**. Zmienia zbyt**połączony** po instalacji hello toomyVnetA komunikacji równorzędnej z myVnetB.

    Dowolnych zasobów platformy Azure, utworzone w każdej sieci wirtualnej są teraz możliwe toocommunicate ze sobą za pośrednictwem ich adresy IP. Jeśli używasz domyślnego rozwiązania Azure nazwy dla sieci wirtualnych hello, hello zasoby w sieciach wirtualnych hello nie są możliwe tooresolve nazw w sieciach wirtualnych hello. Jeśli chcesz nazwy tooresolve między sieciami wirtualnymi w komunikacji równorzędnej, należy utworzyć serwer DNS. Dowiedz się, jak tooset się [rozpoznawanie nazw przy użyciu serwera DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

12. **Opcjonalne**: Chociaż tworzenia maszyn wirtualnych nie została uwzględniona w tym samouczku, można utworzyć maszynę wirtualną w każdej sieci wirtualnej i połączyć z jednej maszyny wirtualnej toohello innych, toovalidate łączności.
13. **Opcjonalne**: toodelete hello zasobów, które możesz utworzyć w tym samouczku, pełną hello czynnościach w ramach [zasoby zostaną usunięte](#delete-powershell) w tym artykule.

## <a name="permissions"></a>Uprawnienia

konta Hello się, że używasz toocreate sieci wirtualnej komunikacji równorzędnej musi mieć hello ról lub uprawnień. Na przykład jeśli zostały równorzędna dwie sieci wirtualne o nazwach myVnetA i myVnetB, Twoje konto musi zostać przypisane hello następujące minimalne roli lub uprawnienia dla każdej sieci wirtualnej:
    
|Sieć wirtualna|Model wdrażania|Rola|Uprawnienia|
|---|---|---|---|
|myVnetA|Resource Manager|[Współautor sieci](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Wdrożenie klasyczne|[Współautor klasycznej sieci](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Nie dotyczy|
|myVnetB|Resource Manager|[Współautor sieci](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Wdrożenie klasyczne|[Współautor klasycznej sieci](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

Dowiedz się więcej o [wbudowane role](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) i przypisywanie uprawnień określonych zbyt[role niestandardowe](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (tylko Resource Manager).

## <a name="delete"></a>Usuwanie zasobów
Po zakończeniu tego samouczka można toodelete hello zasobów, utworzony w samouczek hello w celu uniknięcia opłat użycie. Usunięcie grupy zasobów powoduje usunięcie wszystkich zasobów, które znajdują się w grupie zasobów hello.

### <a name="delete-portal"></a>Azure portal

1. W polu wyszukiwania portalu hello wpisz **myResourceGroupA**. W wynikach wyszukiwania powitania kliknij **myResourceGroupA**.
2. Na powitania **myResourceGroupA** bloku, kliknij przycisk hello **usunąć** ikony.
3. Usuwanie hello tooconfirm, w hello **hello typu nazwa grupy zasobów** wprowadź **myResourceGroupA**, a następnie kliknij przycisk **usunąć**.
4. W hello **wyszukiwania zasobów** pole u góry hello hello portalu, typ *myVnetB*. Kliknij przycisk **myVnetB** po wyświetleniu w wynikach wyszukiwania hello. Zostanie wyświetlony blok hello **myVnetB** sieci wirtualnej.
5. W hello **myVnetB** bloku, kliknij przycisk **usunąć**.
6. Usuwanie hello tooconfirm, kliknij przycisk **tak** w hello **sieci wirtualnej Usuń** pole.

### <a name="delete-cli"></a>Interfejs wiersza polecenia platformy Azure

1. Zaloguj się przy użyciu hello tooAzure CLI 2.0 toodelete hello sieci wirtualnej (Resource Manager) z hello następujące polecenie:

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```

2. Zaloguj się przy użyciu hello tooAzure Azure CLI 1.0 toodelete hello sieć wirtualna (klasyczna) z hello następującego polecenia:

    ```azurecli
    azure config mode asm 

    azure network vnet delete --vnet myVnetB --quiet
    ```

### <a name="delete-powershell"></a>Środowiska PowerShell

1. W wierszu polecenia programu PowerShell hello wprowadź hello następujące polecenia toodelete hello sieci wirtualnej (Resource Manager):

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -Force
    ```

2. toodelete hello sieci wirtualnej (wdrożenia klasyczne) przy użyciu programu PowerShell, należy zmodyfikować istniejący plik konfiguracji sieci. Dowiedz się, jak za[eksportu, aktualizować i importowanie plików konfiguracyjnych sieci](virtual-networks-using-network-configuration-file.md). Usuń hello następującego elementu VirtualNetworkSite dla sieci wirtualnej hello używane w tym samouczku:

    ```xml
    <VirtualNetworkSite name="myVnetB" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > Importowanie pliku konfiguracji sieci zmienione może spowodować zmiany tooexisting sieciami wirtualnymi (klasyczne) w ramach subskrypcji. Upewnij się, tylko Usuń hello poprzedniej sieci wirtualnej, a nie zmienić lub usunąć innych istniejących sieci wirtualnej z subskrypcji. 

## <a name="next-steps"></a>Następne kroki

- Należy dokładnie zapoznać się z ważne [ograniczenia komunikacji równorzędnej sieci wirtualnej i zachowania](virtual-network-manage-peering.md#requirements-and-constraints) przed utworzeniem sieci wirtualnej komunikacji równorzędnej w środowisku produkcyjnym należy używać.
- Więcej informacji na temat wszystkich [sieci wirtualnej komunikacji równorzędnej ustawienia](virtual-network-manage-peering.md#create-a-peering).
- Dowiedz się, jak za[tworzenie koncentratora i gwiazda topologii sieci](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) z sieci wirtualnej komunikacji równorzędnej.
