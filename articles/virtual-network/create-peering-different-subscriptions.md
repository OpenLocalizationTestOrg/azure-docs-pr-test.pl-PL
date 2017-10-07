---
title: "równorzędna - Resource Manager - różnych subskrypcji sieci aaaCreate wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate sieci wirtualnej komunikacji równorzędnej między sieciami wirtualnymi utworzone za pomocą Menedżera zasobów istnieje ona w innej subskrypcji platformy Azure."
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
ms.openlocfilehash: c7983a86031e061c1155144e5c493ee9578fa583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-different-subscriptions"></a>Tworzenie sieci wirtualnej równorzędna - Resource Manager różnych subskrypcji 

Z tego samouczka dowiesz się toocreate sieci wirtualnej komunikacji równorzędnej między sieciami wirtualnymi utworzone za pomocą Menedżera zasobów. sieci wirtualne Hello istnieje w ramach różnych subskrypcji. Witaj komunikacji równorzędnej dwa zasoby umożliwia sieci wirtualnych w różnych sieciach wirtualnych toocommunicate ze sobą z tej samej przepustowości i opóźnień tak, jakby hello zasoby były hello tej samej sieci wirtualnej. Dowiedz się więcej o [równorzędna sieci wirtualnej](virtual-network-peering-overview.md). 

Witaj toocreate kroki sieci wirtualnej komunikacji równorzędnej są różne, w zależności od tego, czy hello sieci wirtualne są w hello tych samych lub różnych subskrypcji i które [modelu wdrożenia usługi Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello sieci wirtualne są tworzone za pomocą. Dowiedz się, jak toocreate a wirtualnych sieci równorzędna w innych sytuacjach, klikając hello scenariusza z hello w poniższej tabeli:

|Model wdrażania platformy Azure  | Subskrypcja platformy Azure  |
|--------- |---------|
|[Obie usługi Resource Manager](virtual-network-create-peering.md) |tym samym|
|[Jeden Resource Manager, co classic](create-peering-different-deployment-models.md) |tym samym|
|[Jeden Resource Manager, co classic](create-peering-different-deployment-models-subscriptions.md) |Różne|

Nie można utworzyć sieci wirtualnej komunikacji równorzędnej między dwiema sieciami wirtualnej wdrożone za pośrednictwem hello klasycznego modelu wdrażania. Element równorzędny sieci wirtualnej można tworzyć tylko między dwiema sieciami wirtualnych, które istnieją w hello sam region platformy Azure. Podczas tworzenia sieci wirtualnej komunikacji równorzędnej między sieciami wirtualnymi, które istnieją w ramach różnych subskrypcji, powitalne subskrypcje muszą być skojarzone toohello same usługi Azure Active Directory dzierżawy. Jeśli nie masz już dzierżawę usługi Azure Active Directory, możesz szybko [utworzyć](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch). Jeśli potrzebujesz tooconnect wirtualnych sieci zarówno utworzonych za pomocą hello klasycznego modelu wdrażania, który istnieje w różnych regionach platformy Azure lub który istnieje w subskrypcji skojarzone toodifferent dzierżaw usługi Azure Active Directory, możesz użyć Azure [Bramy sieci VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello sieci wirtualnych. 

Można użyć hello [portalu Azure](#portal), hello Azure [interfejsu wiersza polecenia](#cli) (CLI) lub Azure [PowerShell](#powershell) toocreate sieci wirtualnej komunikacji równorzędnej. Kliknij dowolny z hello poprzedniego narzędzia łącza toogo, bezpośrednio toohello kroki tworzenia sieci wirtualnej komunikacji równorzędnej narzędzie wyboru.

## <a name="portal"></a>Utwórz równorzędna - portalu Azure

W tym samouczku korzysta z różnych kont dla każdej subskrypcji. Jeśli używasz konta mającego uprawnienia tooboth subskrypcji, można użyć hello takie same konta dla wszystkich kroków, pomiń kroki hello rejestrowania poza hello portalu i pominąć kroki hello przypisywania sieci wirtualnych toohello uprawnienia innego użytkownika.

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
8. W hello **wybierz** wybierz Użytkownik_b lub wpisz toosearch adres e-mail firmy Użytkownik_b. Witaj listę użytkowników, wyświetlany jest z hello tej samej dzierżawy usługi Azure Active Directory, co sieć wirtualna hello konfigurujesz hello komunikacji równorzędnej dla.
9. Kliknij pozycję **Zapisz**.
10. W hello **myVnetA — kontrola dostępu (IAM)** bloku, kliknij przycisk **właściwości** z hello pionowy listy opcji na powitania po lewej stronie powitania bloku. Kopiuj hello **identyfikator ZASOBU**, która jest używana w kolejnym kroku. Identyfikator zasobu Hello jest toohello podobnie poniższy przykład: /subscriptions/<Subscription Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/virtualNetworks/myVnetA.
11. Wyloguj się z portalu hello jako Użytkownik_a, a następnie zaloguj się jako Użytkownik_b.
12. Wykonaj kroki 2 – 3, wprowadzania lub wybierając hello następujące wartości w kroku 3:

    - **Nazwa**: *myVnetB*
    - **Przestrzeń adresowa**: *10.1.0.0/16*
    - **Nazwa podsieci**: *domyślne*
    - **Zakres adresów podsieci**: *10.1.0.0/24*
    - **Subskrypcja**: Wybierz subskrypcję B.
    - **Grupa zasobów**: Wybierz **Utwórz nowy** , a następnie wprowadź *myResourceGroupB*
    - **Lokalizacja**: *wschodnie stany USA*

13. W hello **wyszukiwania zasobów** pole u góry hello hello portalu, typ *myVnetB*. Kliknij przycisk **myVnetB** po wyświetleniu w wynikach wyszukiwania hello. Zostanie wyświetlony blok hello **myVnetB** sieci wirtualnej.
14. W hello **myVnetB** bloku, który jest wyświetlany, kliknij przycisk **właściwości** z hello pionowy listy opcji na powitania po lewej stronie powitania bloku. Kopiuj hello **identyfikator ZASOBU**, która jest używana w kolejnym kroku. Identyfikator zasobu Hello jest toohello podobnie poniższy przykład: /subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB.
15. Kliknij przycisk **(IAM) kontroli dostępu** w hello **myVnetB** bloku, a następnie wykonaj kroki 5 – 10 dla myVnetB wprowadzania **Użytkownik_a** w kroku 8.
16. Wyloguj się z portalu hello jako Użytkownik_b i zaloguj się jako Użytkownik_a.
17. W hello **wyszukiwania zasobów** pole u góry hello hello portalu, typ *myVnetA*. Kliknij przycisk **myVnetA** po wyświetleniu w wynikach wyszukiwania hello. Zostanie wyświetlony blok hello **myVnet** sieci wirtualnej.
18. Kliknij przycisk **myVnetA**.
19. W hello **myVnetA** bloku, który jest wyświetlany, kliknij przycisk **komunikacji równorzędnych** z hello pionowy listy opcji na powitania po lewej stronie powitania bloku.
20. W hello **myVnetA - komunikacji równorzędnych** bloku, które wystąpiły, kliknij przycisk **+ Dodaj**
21. W hello **równorzędna Dodaj** bloku, zostanie wyświetlone, wprowadź, lub wybierz hello następujące opcje, a następnie kliknij **OK**:
     - **Nazwa**: *myVnetAToMyVnetB*
     - **Model wdrażania sieci wirtualnej**: Wybierz **Resource Manager**.
     - **Sprawdzić mój identyfikator zasobu**: Zaznacz to pole wyboru.
     - **Identyfikator zasobu**: Wprowadź identyfikator zasobu hello z kroku 14.
     - **Zezwalaj na dostęp do sieci wirtualnej:** upewnij się, że **włączone** jest zaznaczone.
    W tym samouczku są używane żadne inne ustawienia. Przeczytaj toolearn dotyczące wszystkich ustawień komunikacji równorzędnej, [Zarządzanie komunikacji równorzędnych sieci wirtualnych](virtual-network-manage-peering.md#create-a-peering).
22. Po kliknięciu przycisku **OK** w poprzednim kroku hello hello **równorzędna Dodaj** bloku zamyka i zobacz hello **myVnetA - komunikacji równorzędnych** ponownie blok. Po kilku sekundach hello równorzędna utworzonego pojawia się w bloku hello. **Zainicjowane** ma na liście hello **RÓWNORZĘDNA stan** kolumny dla hello **myVnetAToMyVnetB** równorzędna zostanie utworzony. Już połączyć za pomocą myVnetA toomyVnetB, ale teraz musi równorzędnego myVnetB toomyVnetA. równorzędna Hello należy utworzyć w obu kierunkach tooenable zasobów w toocommunicate sieci wirtualnych hello ze sobą.
23. Wyloguj się z portalu hello jako Użytkownik_a i zaloguj się jako Użytkownik_b.
24. Wykonaj kroki 17 21 ponownie dla myVnetB. W kroku 21 nazwa komunikacji równorzędnej hello *myVnetBToMyVnetA*, wybierz pozycję *myVnetA* dla **sieci wirtualnej**i podaj identyfikator hello z kroku 10 hello **identyfikator zasobu** pole.
25. Kilka sekund po kliknięciu przycisku **OK** toocreate hello komunikacji równorzędnej dla myVnetB, hello **myVnetBToMyVnetA** równorzędna właśnie utworzony znajduje się **połączony** w hello  **Komunikacja RÓWNORZĘDNA stan** kolumny.
26. Wyloguj się z portalu hello jako Użytkownik_b i zaloguj się jako Użytkownik_a.
27. Wykonaj ponownie czynności 17-19. Witaj **RÓWNORZĘDNA stan** dla hello **myVnetAToVNetB** komunikacji równorzędnej jest teraz również **połączony**. równorzędna Hello zostanie pomyślnie nawiązane po **połączony** w hello **RÓWNORZĘDNA stan** kolumny dla obu sieci wirtualnych w komunikacji równorzędnej hello. Dowolnych zasobów platformy Azure, utworzone w każdej sieci wirtualnej są teraz możliwe toocommunicate ze sobą za pośrednictwem ich adresy IP. Jeśli używasz domyślnego rozwiązania Azure nazwy dla sieci wirtualnych hello, hello zasoby w sieciach wirtualnych hello nie są możliwe tooresolve nazw w sieciach wirtualnych hello. Jeśli chcesz nazwy tooresolve między sieciami wirtualnymi w komunikacji równorzędnej, należy utworzyć serwer DNS. Dowiedz się, jak tooset się [rozpoznawanie nazw przy użyciu serwera DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
28. **Opcjonalne**: Chociaż tworzenia maszyn wirtualnych nie została uwzględniona w tym samouczku, można utworzyć maszynę wirtualną w każdej sieci wirtualnej i połączyć z jednej maszyny wirtualnej toohello innych, toovalidate łączności.
29. **Opcjonalne**: toodelete hello zasobów, które możesz utworzyć w tym samouczku, pełną hello etapami hello [zasoby zostaną usunięte](#delete-portal) sekcji tego artykułu.

## <a name="cli"></a>Utwórz równorzędna - wiersza polecenia platformy Azure

W tym samouczku korzysta z różnych kont dla każdej subskrypcji. Jeśli używasz konta mającego uprawnienia tooboth subskrypcji, można użyć hello same konta dla wszystkich kroków, pomiń kroki hello logowania z platformy Azure i usunąć wiersze hello skryptu, utworzonych przypisań ról użytkownika. Zastąp UserA@azure.com i UserB@azure.com we wszystkich hello następujące skrypty z nazw użytkowników hello używasz Użytkownik_a i Użytkownik_b.

Witaj następującego skryptu:

- Wymaga hello Azure CLI w wersji 2.0.4 lub nowszej. Wersja hello toofind, uruchom `az --version`. Jeśli potrzebujesz tooupgrade, zobacz [zainstalować Azure CLI 2.0](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).
- Działanie powłoki Bash. Aby wyświetlić opcje uruchamiania skryptów wiersza polecenia platformy Azure na kliencie systemu Windows, zobacz [działający w systemie Windows hello Azure CLI](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

Zamiast instalowania hello interfejsu wiersza polecenia i jego zależności, możesz użyć hello powłoki chmury Azure. Hello powłoki chmury Azure jest bezpłatna powłoki Bash, który można uruchomić bezpośrednio z poziomu hello portalu Azure. Ma ona hello Azure CLI wstępnie zainstalowane i skonfigurowane toouse z Twoim kontem. Kliknij przycisk hello **wypróbuj** przycisk w skrypcie hello poniżej, który wywołuje powłoki chmury, które możesz zalogować się tooyour konto platformy Azure z. 

1. Otwórz sesję programu interfejsu wiersza polecenia, a następnie zaloguj się jako Użytkownika_a przy użyciu hello tooAzure `azure login` polecenia. Zaloguj się przy użyciu konta Hello musi mieć hello toocreate niezbędne uprawnienia sieci wirtualnej komunikacji równorzędnej. Zobacz hello [uprawnienia](#permissions) sekcji tego artykułu, aby uzyskać szczegółowe informacje.
2. Skopiuj powitania po Edytor tekstu tooa skryptu na komputerze, zastąpić `<SubscriptionA-Id>` następnie z hello identyfikator SubscriptionA hello kopiowania zmodyfikować skrypt, wklej go w sesji interfejsu wiersza polecenia i naciśnij klawisz `Enter`. Jeśli nie znasz identyfikator subskrypcji, wprowadź polecenie "Pokaż konto az" hello. Witaj wartość **identyfikator** w hello jest identyfikator subskrypcji

    ```azurecli-interactive
    # Create a resource group.
    az group create \
      --name myResourceGroupA \
      --location eastus

    # Create virtual network A.
    az network vnet create \
      --name myVnetA \
      --resource-group myResourceGroupA \
      --location eastus \
      --address-prefix 10.0.0.0/16

    # Assign UserB permissions toovirtual network A.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```
    
     Przypisanie uprawnień powitania dla Użytkownik_b nie jest wymagane. Równorzędna można ustanowić nawet wtedy, gdy użytkownicy podnieść pojedynczo żądania komunikacji równorzędnej dla odpowiednich sieci wirtualnych, tak długo, jak hello żądań dopasowania. Dodawanie użytkownika uprzywilejowanego myVNetB jako współautor sieci w sieci wirtualnej lokalne powitania umożliwia łatwiejsze toodo hello Instalatora.
3. Wyloguj się z platformy Azure jako Użytkownika_a przy użyciu hello `az logout` polecenia, a następnie zaloguj się za tooAzure jako Użytkownik_b. Zaloguj się przy użyciu konta Hello musi mieć hello toocreate niezbędne uprawnienia sieci wirtualnej komunikacji równorzędnej. Zobacz hello [uprawnienia](#permissions) sekcji tego artykułu, aby uzyskać szczegółowe informacje.
4. Utwórz myVnetB. Kopiuj zawartość skryptu hello w edytorze tekstu 2 tooa krok na komputerze. Zastąp `<SubscriptionA-Id>` z hello identyfikator SubscriptionB. Zmień 10.0.0.0/16 too10.1.0.0/16, Zmień wszystkie jako tooB i wszystkie tooA Bs. Skopiuj skrypt hello zmodyfikowane, wklej go w tooyour sesji interfejsu wiersza polecenia i naciśnij klawisz `Enter`. 
5. Wyloguj się z platformy Azure jako Użytkownik_b i logowania tooAzure jako Użytkownik_a.
6. Tworzenie sieci wirtualnej komunikacji równorzędnej z myVnetA toomyVnetB. Skopiuj powitania po Edytor tekstu tooa zawartość skryptu na komputerze. Zastąp `<SubscriptionB-Id>` z hello identyfikator SubscriptionB. tooexecute hello skryptu, skopiuj skrypt hello zmodyfikowane, wklej go do sesji interfejsu wiersza polecenia i naciśnij klawisz Enter.
 
    ```azurecli-interactive
        # Get hello id for myVnetA.
        vnetAId=$(az network vnet show \
          --resource-group myResourceGroupA \
          --name myVnetA \
          --query id --out tsv)
    
        # Peer myVNetA toomyVNetB.
        az network vnet peering create \
          --name myVnetAToMyVnetB \
          --resource-group myResourceGroupA \
          --vnet-name myVnetA \
          --remote-vnet-id /subscriptions/<SubscriptionB-Id>/resourceGroups/myResourceGroupB/providers/Microsoft.Network/VirtualNetworks/myVnetB \
          --allow-vnet-access
    ```

7. Wyświetl stan komunikacji równorzędnej hello myVnetA.

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroupA \
      --vnet-name myVnetA \
      --output table
    ```

    Stan Hello jest **zainicjowano**. Zmienia zbyt**połączony** po utworzeniu hello toomyVnetA komunikacji równorzędnej z myVnetB.

8. Wyloguj się Użytkownik_a z platformy Azure i zaloguj się za tooAzure jako Użytkownik_b.
9. Utwórz hello komunikacji równorzędnej z myVnetB toomyVnetA. Kopiuj zawartość skryptu hello w edytorze tekstu 6 tooa krok na komputerze. Zastąp `<SubscriptionB-Id>` o identyfikatorze hello SubscriptionA i Zmień wszystkie jako tooB i wszystkie tooA Bs. Po dokonaniu zmiany hello hello kopiowania zmodyfikować skrypt, wklej go do sesji interfejsu wiersza polecenia i naciśnij klawisz `Enter`.
10. Wyświetl stan komunikacji równorzędnej hello myVnetB. Kopiuj zawartość skryptu hello w edytorze tekstu 7 tooa krok na komputerze. Zmień tooB dla grupy zasobów hello i nazwy sieci wirtualnej, skopiuj skrypt hello, Wklej hello zmodyfikować skrypt w sesji CLI tooyour i naciśnij klawisz `Enter`. Witaj stanu komunikacji równorzędnej jest **połączony**. Witaj komunikacji równorzędnej stan zmiany myVnetA zbyt**połączony** po utworzeniu hello komunikacji równorzędnej z myVnetB toomyVnetA. Możesz zalogować się Użytkownik_a ponownie tooAzure i wykonaj krok 7 ponownie tooverify hello komunikacji równorzędnej stan myVnetA. 

    > [!NOTE]
    > równorzędna Hello nie zostanie nawiązane, dopóki stan komunikacji równorzędnej hello jest **połączony** dla obu sieci wirtualnej.

11. **Opcjonalne**: Chociaż tworzenia maszyn wirtualnych nie została uwzględniona w tym samouczku, można utworzyć maszynę wirtualną w każdej sieci wirtualnej i połączyć z jednej maszyny wirtualnej toohello innych, toovalidate łączności.
12. **Opcjonalne**: toodelete hello zasobów, które możesz utworzyć w tym samouczku, pełną hello czynnościach w ramach [zasoby zostaną usunięte](#delete-cli) w tym artykule.

Dowolnych zasobów platformy Azure, utworzone w każdej sieci wirtualnej są teraz możliwe toocommunicate ze sobą za pośrednictwem ich adresy IP. Jeśli używasz domyślnego rozwiązania Azure nazwy dla sieci wirtualnych hello, hello zasoby w sieciach wirtualnych hello nie są możliwe tooresolve nazw w sieciach wirtualnych hello. Jeśli chcesz nazwy tooresolve między sieciami wirtualnymi w komunikacji równorzędnej, należy utworzyć serwer DNS. Dowiedz się, jak tooset się [rozpoznawanie nazw przy użyciu serwera DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
 
## <a name="powershell"></a>Utwórz równorzędna — PowerShell

W tym samouczku korzysta z różnych kont dla każdej subskrypcji. Jeśli używasz konta mającego uprawnienia tooboth subskrypcji, można użyć hello same konta dla wszystkich kroków, pomiń kroki hello logowania z platformy Azure i usunąć wiersze hello skryptu, utworzonych przypisań ról użytkownika. Zastąp UserA@azure.com i UserB@azure.com we wszystkich hello następujące skrypty z nazw użytkowników hello używasz Użytkownik_a i Użytkownik_b.

1. Zainstaluj najnowszą wersję hello PowerShell hello [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modułu. Jeśli jesteś tooAzure nowego środowiska PowerShell, zobacz [Omówienie programu Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Uruchom sesję programu PowerShell.
3. W programie PowerShell Zaloguj tooAzure jako Użytkownik_a wprowadzając hello `login-azurermaccount` polecenia. Zaloguj się przy użyciu konta Hello musi mieć hello toocreate niezbędne uprawnienia sieci wirtualnej komunikacji równorzędnej. Zobacz hello [uprawnienia](#permissions) sekcji tego artykułu, aby uzyskać szczegółowe informacje.
4. Utwórz grupę zasobów i sieci wirtualnej kopiowania A. hello następującego skryptu tooa tekstu edytor na komputerze. Zastąp `<SubscriptionA-Id>` z hello identyfikator SubscriptionA. Jeśli nie znasz identyfikator subskrypcji, wprowadź hello `Get-AzureRmSubscription` tooview polecenia go. Witaj wartość **identyfikator** w hello zwrócone dane wyjściowe są Twojego identyfikatora subskrypcji. tooexecute hello skryptu, hello kopiowania zmodyfikować skrypt, wklej go w tooPowerShell, a następnie naciśnij `Enter`.

    ```powershell
    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name MyResourceGroupA `
      -Location eastus

    # Create virtual network A.
    $vNetA = New-AzureRmVirtualNetwork `
      -ResourceGroupName MyResourceGroupA `
      -Name 'myVnetA' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus

    # Assign UserB permissions toomyVnetA.
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

    Przypisanie uprawnień powitania dla Użytkownik_b nie jest wymagane. Równorzędna można ustanowić nawet wtedy, gdy użytkownicy podnieść pojedynczo żądania komunikacji równorzędnej dla odpowiednich sieci wirtualnych, tak długo, jak hello żądań dopasowania. Dodawanie użytkownika uprzywilejowanego hello innych sieci wirtualnej jako użytkownik w sieci wirtualnej lokalne powitania umożliwia łatwiejsze toodo hello Instalatora.
5. Wyloguj się Użytkownik_a z platformy Azure i zaloguj się za Użytkownik_b. Zaloguj się przy użyciu konta Hello musi mieć hello toocreate niezbędne uprawnienia sieci wirtualnej komunikacji równorzędnej. Zobacz hello [uprawnienia](#permissions) sekcji tego artykułu, aby uzyskać szczegółowe informacje.
6. Kopiuj zawartość skryptu hello w edytorze tekstu 4 tooa krok na komputerze. Zastąp `<SubscriptionA-Id>` o identyfikatorze hello subskrypcji too10.1.0.0/16 10.0.0.0/16 B. zmiana. Zmień wszystkie jako tooB i wszystkie tooA Bs. tooexecute hello skryptu, hello kopiowania zmodyfikować skrypt, Wklej do środowiska PowerShell i naciśnij klawisz `Enter`.
7. Wyloguj się Użytkownik_b z platformy Azure i zaloguj się za Użytkownik_a.
8. Utwórz hello komunikacji równorzędnej z myVnetA toomyVnetB. Skopiuj powitania po Edytor tekstu tooa skryptu na komputerze. Zastąp `<SubscriptionB-Id>` o identyfikatorze hello subskrypcji B. tooexecute hello skryptu, skopiuj skrypt hello zmodyfikowane, Wklej tooPowerShell, a następnie naciśnij `Enter`.
 
    ```powershell
    # Peer myVnetA toomyVnetB.
    $vNetA=Get-AzureRmVirtualNetwork -Name myVnetA -ResourceGroupName myResourceGroupA
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vNetA `
      -RemoteVirtualNetworkId "/subscriptions/<SubscriptionB-Id>/resourceGroups/myResourceGroupB/providers/Microsoft.Network/virtualNetworks/myVnetB"
    ```

9. Wyświetl stan komunikacji równorzędnej hello myVnetA.

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroupA `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Stan Hello jest **zainicjowano**. Zmienia zbyt**połączony** po instalacji hello toomyVnetA komunikacji równorzędnej z myVnetB.

10. Wyloguj się Użytkownik_a z platformy Azure i zaloguj się za Użytkownik_b.
11. Utwórz hello komunikacji równorzędnej z myVnetB toomyVnetA. Kopiuj zawartość skryptu hello w edytorze tekstu 8 tooa krok na komputerze. Zastąp `<SubscriptionB-Id>` o identyfikatorze hello subskrypcji A, a wszystkie A tooB i B wszystkich tooA. tooexecute hello skryptu, hello kopiowania zmodyfikować skrypt, wklej go w tooPowerShell, a następnie naciśnij `Enter`.
12. Wyświetl stan komunikacji równorzędnej hello myVnetB. Kopiuj zawartość skryptu hello w edytorze tekstu 9 tooa krok na komputerze. Zmień tooB dla grupy zasobów hello i nazwy sieci wirtualnej. skrypt hello tooexecute wkleić hello zmodyfikować skrypt programu PowerShell, a następnie naciśnij `Enter`. Stan Hello jest **połączony**. Witaj komunikacji równorzędnej stan **myVnetA** zmiany zbyt**połączony** po utworzeniu hello komunikacji równorzędnej z **myVnetB** za**myVnetA**. Możesz zalogować się Użytkownik_a ponownie tooAzure i wykonaj krok 9 ponownie tooverify hello komunikacji równorzędnej stan myVnetA. 

    > [!NOTE]
    > równorzędna Hello nie zostanie nawiązane, dopóki stan komunikacji równorzędnej hello jest **połączony** dla obu sieci wirtualnej.

    Dowolnych zasobów platformy Azure, utworzone w każdej sieci wirtualnej są teraz możliwe toocommunicate ze sobą za pośrednictwem ich adresy IP. Jeśli używasz domyślnego rozwiązania Azure nazwy dla sieci wirtualnych hello, hello zasoby w sieciach wirtualnych hello nie są możliwe tooresolve nazw w sieciach wirtualnych hello. Jeśli chcesz nazwy tooresolve między sieciami wirtualnymi w komunikacji równorzędnej, należy utworzyć serwer DNS. Dowiedz się, jak tooset się [rozpoznawanie nazw przy użyciu serwera DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

13. **Opcjonalne**: Chociaż tworzenia maszyn wirtualnych nie została uwzględniona w tym samouczku, można utworzyć maszynę wirtualną w każdej sieci wirtualnej i połączyć z jednej maszyny wirtualnej toohello innych, toovalidate łączności.
14. **Opcjonalne**: toodelete hello zasobów, które możesz utworzyć w tym samouczku, pełną hello czynnościach w ramach [zasoby zostaną usunięte](#delete-powershell) w tym artykule.

## <a name="permissions"></a>Uprawnienia

konta Hello się, że używasz toocreate sieci wirtualnej komunikacji równorzędnej musi mieć hello ról lub uprawnień. Na przykład, jeśli zostały równorzędna dwie sieci wirtualnej o nazwie **myVnetA** i **myVnetB**, Twoje konto musi mieć przypisaną hello następujące minimalne roli lub uprawnienia dla każdej sieci wirtualnej:
    
|Sieć wirtualna|Rola|Uprawnienia|
|---|---|---|
|myVnetA|[Współautor sieci](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
|myVnetB|[Współautor sieci](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|

Dowiedz się więcej o [wbudowane role](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) i przypisywanie uprawnień określonych zbyt[role niestandardowe](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (tylko Resource Manager).

## <a name="delete"></a>Usuwanie zasobów
Po zakończeniu tego samouczka można toodelete hello zasobów, utworzony w samouczek hello w celu uniknięcia opłat użycie. Usunięcie grupy zasobów powoduje usunięcie wszystkich zasobów, które znajdują się w grupie zasobów hello.

### <a name="delete-portal"></a>Azure portal

1. Zaloguj się w toohello portalu Azure jako Użytkownik_a.
2. W polu wyszukiwania portalu hello wpisz **myResourceGroupA**. W wynikach wyszukiwania powitania kliknij **myResourceGroupA**.
3. Na powitania **myResourceGroupA** bloku, kliknij przycisk hello **usunąć** ikony.
4. Usuwanie hello tooconfirm, w hello **hello typu nazwa grupy zasobów** wprowadź **myResourceGroupA**, a następnie kliknij przycisk **usunąć**.
5. Wyloguj się z portalu hello jako Użytkownik_a i zaloguj się jako Użytkownik_b.
6. Wykonaj kroki od 2 do 4 dla myResourceGroupB.

### <a name="delete-cli"></a>Interfejs wiersza polecenia platformy Azure

1. Zaloguj się za tooAzure jako Użytkownik_a i wykonaj hello następujące polecenie:

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```
2. Wyloguj Azure jako Użytkownik_a i zaloguj się jako Użytkownik_b.
3. Wykonaj hello następujące polecenie:

    ```azurecli-interactive
    az group delete --name myResourceGroupB --yes
    ```

### <a name="delete-powershell"></a>Środowiska PowerShell

1. Zaloguj się za tooAzure jako Użytkownik_a i wykonaj hello następujące polecenie:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -force
    ```

2. Wyloguj Azure jako Użytkownik_a i zaloguj się jako Użytkownik_b.
3. Wykonaj hello następujące polecenie:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupB -force
    ```

## <a name="next-steps"></a>Następne kroki

- Należy dokładnie zapoznać się z ważne [ograniczenia komunikacji równorzędnej sieci wirtualnej i zachowania](virtual-network-manage-peering.md#requirements-and-constraints) przed utworzeniem sieci wirtualnej komunikacji równorzędnej w środowisku produkcyjnym należy używać.
- Więcej informacji na temat wszystkich [sieci wirtualnej komunikacji równorzędnej ustawienia](virtual-network-manage-peering.md#create-a-peering).
- Dowiedz się, jak za[tworzenie koncentratora i gwiazda topologii sieci](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) z sieci wirtualnej komunikacji równorzędnej.
