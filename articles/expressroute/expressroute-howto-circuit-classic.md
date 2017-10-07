---
title: "Tworzenie i modyfikowanie obwodu usługi ExpressRoute: środowiska PowerShell: klasyczny Portal Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule przedstawiono kroki hello do tworzenia i inicjowania obsługi administracyjnej obwodu usługi ExpressRoute. Ten artykuł zawiera także sposób toocheck hello stanu, zaktualizować, lub usuń i anulowanie zastrzeżenia obwodu."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0134d242-6459-4dec-a2f1-4657c3bc8b23
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 9897c88776a2153ba22aa9ff328becb9f12b660b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a>Tworzenie i modyfikowanie obwodu usługi ExpressRoute, przy użyciu programu PowerShell (klasyczne)
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Interfejs wiersza polecenia platformy Azure](howto-circuit-cli.md)
> * [Video - portalu Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (klasyczny)](expressroute-howto-circuit-classic.md)
>

W tym artykule przedstawiono toocreate kroki hello obwodu usługi Azure ExpressRoute przy użyciu programu PowerShell polecenia cmdlet i hello klasycznego modelu wdrażania. Ten artykuł zawiera także sposób toocheck hello stanu, zaktualizować, lub usuń i anulowanie zastrzeżenia obwodu usługi ExpressRoute.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


**Modele wdrażania Azure — informacje**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a>Przed rozpoczęciem
### <a name="step-1-review-hello-prerequisites-and-workflow-articles"></a>Krok 1. Przejrzyj wymagania wstępne hello i artykuły przepływu pracy
Upewnij się, że użytkownik przejrzał hello [wymagania wstępne](expressroute-prerequisites.md) i [przepływy pracy](expressroute-workflows.md) przed rozpoczęciem konfigurowania.  

### <a name="step-2-install-hello-latest-versions-of-hello-azure-service-management-sm-powershell-modules"></a>Krok 2. Zainstaluj najnowsze wersje hello hello moduły programu PowerShell Azure usługi zarządzania (ko)
Postępuj zgodnie z instrukcjami hello [wprowadzenie do poleceń cmdlet programu Azure PowerShell](/powershell/azure/overview) wskazówki krok po kroku na temat tooconfigure moduły programu Azure PowerShell hello toouse komputera.

### <a name="step-3-log-in-tooyour-azure-account-and-select-a-subscription"></a>Krok 3. Zaloguj się za tooyour konto platformy Azure i wybierz subskrypcję
1. Otwórz konsolę programu PowerShell z podwyższonym poziomem uprawnień i Połącz konto tooyour. Użyj powitania po toohelp przykład, gdy nawiązujesz połączenie:

        Login-AzureRmAccount

2. Sprawdź subskrypcje hello hello konta.

        Get-AzureRmSubscription

3. Jeśli masz więcej niż jedną subskrypcję, wybierz subskrypcję hello, które mają toouse.

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. Następnie należy użyć następującego polecenia cmdlet tooadd hello tooPowerShell Twojej subskrypcji platformy Azure dla hello klasycznego modelu wdrażania.

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a>Tworzenie i przydzielanie obwodu usługi ExpressRoute
### <a name="step-1-import-hello-powershell-modules-for-expressroute"></a>Krok 1. Zaimportuj hello moduły programu PowerShell dla usługi ExpressRoute
 Jeśli jeszcze nie należy zaimportować do sesji programu PowerShell hello w kolejności toostart za pomocą poleceń cmdlet usługi ExpressRoute hello modułów hello Azure i usługi ExpressRoute. Zaimportuj moduły hello z hello lokalizacji, które były zainstalowane tooon komputera lokalnego. W zależności od metody hello są używane moduły hello tooinstall, hello lokalizacji może być inna niż powitania po przykładzie. W razie potrzeby zmodyfikować przykład Witaj.  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>Krok 2. Pobierz listę hello obsługiwanych dostawców, lokalizacji i przepustowości
Przed utworzeniem obwodu usługi ExpressRoute, należy hello listę dostawców obsługiwanych łączności, lokalizacji i opcji przepustowości.

polecenia cmdlet programu PowerShell Hello `Get-AzureDedicatedCircuitServiceProvider` zwraca informację, która będzie używana w dalszych krokach:

    Get-AzureDedicatedCircuitServiceProvider

Określ, czy toosee podane jest dostawcą połączenia. Zanotuj następujące informacje, ponieważ będzie on potrzebny później podczas tworzenia obwód hello:

* Nazwa
* PeeringLocations
* BandwidthsOffered

Możesz teraz gotowy toocreate obwodu usługi ExpressRoute.         

### <a name="step-3-create-an-expressroute-circuit"></a>Krok 3. Create an ExpressRoute circuit (Tworzenie obwodu usługi ExpressRoute)
Witaj poniższy przykład przedstawia sposób toocreate ExpressRoute 200 MB/s obwodu za pośrednictwem Equinix w Dolinie Krzemowej. Jeśli używasz innego dostawcy i inne ustawienia, należy zastąpić te informacje po wprowadzeniu żądania.

> [!IMPORTANT]
> Od momentu hello wygenerowaniu klucza usługi będą naliczane obwodu usługi ExpressRoute. Upewnij się, wykonać tę operację, gdy dostawca połączenia hello jest gotowy tooprovision hello obwodu.
> 
> 

Hello poniżej przedstawiono przykładowe żądanie dla nowego klucza usługi.

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

Lub, jeśli chcesz toocreate obwodu usługi ExpressRoute z dodatkiem premium hello hello Użyj poniższy przykład. Zobacz toohello [ExpressRoute — często zadawane pytania](expressroute-faqs.md) więcej szczegółów dotyczących dodatek hello w warstwie premium.

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


odpowiedź Hello będzie zawierać hello klucza usługi. Szczegółowy opis wszystkich parametrów hello można uzyskać, uruchamiając następujące hello:

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-hello-expressroute-circuits"></a>Krok 4. Wyświetl listę wszystkich obwody usługi ExpressRoute hello
Możesz uruchomić hello `Get-AzureDedicatedCircuit` polecenia tooget listę wszystkich hello obwody usługi ExpressRoute, które zostały utworzone:

    Get-AzureDedicatedCircuit

odpowiedź Hello będzie coś podobnego toohello poniższy przykład:

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

Te informacje w dowolnym momencie można pobrać za pomocą hello `Get-AzureDedicatedCircuit` polecenia cmdlet. Co hello wywołania bez parametrów wyświetla listę wszystkich obwodów hello. Klucz usługi będzie wyświetlane w hello *bindingTemplate* pola.

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

Szczegółowy opis wszystkich parametrów hello można uzyskać, uruchamiając następujące hello:

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>Krok 5. Wyślij łączności hello usługodawcy tooyour klucza do inicjowania obsługi
*ServiceProviderProvisioningState* zawiera informacje na temat hello bieżący stan inicjowania obsługi administracyjnej po stronie dostawcy usług hello. *Stan* zawiera stan hello na powitania po stronie firmy Microsoft. Aby uzyskać więcej informacji na temat obwodu inicjowania obsługi administracyjnej stanów Zobacz hello [przepływy pracy](expressroute-workflows.md#expressroute-circuit-provisioning-states) artykułu.

Podczas tworzenia nowego obwodu ExpressRoute obwodu hello będą powitania po stanu:

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


obwód Hello przejdzie toohello po stanu, gdy dostawca łączności hello jest w toku hello włączenie go dla Ciebie:

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

Obwodu usługi ExpressRoute musi mieć następujące stan możesz toobe stanie toouse hello go:

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>Krok 6. Okresowo sprawdzać stan hello i stan hello hello obwodu klucza
Dzięki temu można dowiedzieć się, gdy dostawca jest włączony obwodu. Po skonfigurowaniu obwodu hello *ServiceProviderProvisioningState* będą wyświetlane jako *obsługiwane administracyjnie* pokazane na powitania poniższy przykład:

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a>Krok 7. Tworzenie konfiguracji routingu
Zobacz toohello [obwodu ExpressRoute konfiguracji routingu (tworzenia i modyfikowania obwodu komunikacji równorzędnych)](expressroute-howto-routing-classic.md) artykułu, aby uzyskać instrukcje krok po kroku.

> [!IMPORTANT]
> Te instrukcje mają zastosowanie tylko toocircuits, które są tworzone za pomocą dostawcy usług, które oferują warstwy 2 łączność usługi. Jeśli używasz usługodawcy, który oferuje zarządzanych warstwy 3 usługi (zazwyczaj IP sieci VPN, takie jak MPLS), dostawca połączenia będzie Konfigurowanie i zarządzanie nimi routingu dla Ciebie.
> 
> 

### <a name="step-8-link-a-virtual-network-tooan-expressroute-circuit"></a>Krok 8. Link sieci wirtualnej tooan obwodu usługi expressroute
Następnie połącz tooyour sieci wirtualnej obwodu usługi expressroute. Odwołuje się zbyt[połączeń ExpressRoute obwody sieci toovirtual](expressroute-howto-linkvnet-classic.md) instrukcje krok po kroku. Jeśli potrzebujesz toocreate sieć wirtualną przy użyciu hello klasycznego modelu wdrażania w przypadku połączeń ExpressRoute, zobacz [utworzyć sieć wirtualną w przypadku połączeń ExpressRoute](expressroute-howto-vnet-portal-classic.md).

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>Pobieranie stanu hello obwodu usługi ExpressRoute
Te informacje w dowolnym momencie można pobrać za pomocą hello `Get-AzureCircuit` polecenia cmdlet. Co hello wywołania bez parametrów wyświetla listę wszystkich obwodów hello.

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

    Bandwidth                        : 1000
    CircuitName                      : MyAsiaCircuit
    Location                         : Singapore
    ServiceKey                       : #################################
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

Przez przekazanie klucza usługi hello jako parametr wywołanie toohello można uzyskać informacji na temat określonych obwodu usługi expressroute.

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


Szczegółowy opis wszystkich parametrów hello można uzyskać, uruchamiając hello poniższy przykład:

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a>Modyfikowanie obwodu usługi ExpressRoute
Można zmodyfikować niektórych właściwości obwodu usługi ExpressRoute, bez wywierania wpływu na łączność.

Możesz zrobić hello po bez przestojów:

* Włącz lub Wyłącz dodatek premium usługi ExpressRoute dla obwodu usługi ExpressRoute.
* Hello zwiększyć przepustowość obwodu ExpressRoute pod warunkiem, że na porcie hello jest dostępna pojemność. Należy pamiętać, że zmiany na starszą wersję hello przepustowości obwodu nie jest obsługiwany. 
* Zmień hello planu z danych naliczane tooUnlimited danych pomiaru. Należy pamiętać, zmiana planu zliczania hello z tooMetered nieograniczone danych, danych nie jest obsługiwane.
* Można włączyć lub wyłączyć *operacje klasycznego*.

Zobacz toohello [ExpressRoute — często zadawane pytania](expressroute-faqs.md) Aby uzyskać więcej informacji na temat limity i ograniczenia.

### <a name="tooenable-hello-expressroute-premium-add-on"></a>Dodatek tooenable ExpressRoute hello w warstwie premium
Dodatek premium ExpressRoute hello można włączyć dla istniejącego obwodu za pomocą następującego polecenia cmdlet programu PowerShell hello:

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

Obwodu będzie teraz hello ExpressRoute premium dodatkowe funkcje są włączone. Należy pamiętać, że firma Microsoft będzie uruchamiane rozliczeń dla hello premium dodatkowe możliwości, jak polecenie hello został uruchomiony pomyślnie.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>Dodatek toodisable ExpressRoute hello w warstwie premium
> [!IMPORTANT]
> Ta operacja może zakończyć się niepowodzeniem, jeśli używasz zasobów, które są większe niż co to jest dozwolone dla obwodu standardowe hello.
> 
> 

#### <a name="considerations"></a>Zagadnienia do rozważenia

* Należy się upewnić, numer hello obwodu toohello połączone sieci wirtualnych jest mniejsza niż 10, aby obniżyć z premium toostandard. Jeśli tego nie zrobisz, żądanie aktualizacji zakończy się niepowodzeniem, a będziesz rachunku hello premium stawki.
* Należy odłączyć wszystkie sieci wirtualne w różnych regionach geograficznymi. Jeśli tego nie zrobisz, żądanie aktualizacji zakończy się niepowodzeniem, a będziesz rachunku hello premium stawki.
* Tabela tras musi być mniejsza niż 4000 tras dla prywatnej komunikacji równorzędnej. Jeśli rozmiar tabeli tras jest większa niż 4000 tras, sesji BGP hello spowoduje porzucenie i nie będzie reenabled, aż przejdzie hello liczby prefiksów anonsowanych poniżej 4000.

#### <a name="disable-hello-premium-add-on"></a>Wyłącz dodatek hello w warstwie premium
Dodatek premium ExpressRoute hello dla istniejącego obwodu można wyłączyć za pomocą następującego polecenia cmdlet programu PowerShell hello:

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>przepustowości obwodu ExpressRoute hello tooupdate
Sprawdź hello [ExpressRoute — często zadawane pytania](expressroute-faqs.md) obsługiwane opcje przepustowości dla dostawcy. Można wybrać żadnych ma rozmiar większy niż rozmiar hello obwodu istniejących tak długo, jak umożliwia hello fizyczny port (na którym jest tworzony obwodu).

> [!IMPORTANT]
> Konieczne może być obwodu ExpressRoute hello toorecreate na powitania istniejącego portu jest nieodpowiedni pojemności. Nie można uaktualnić obwodu hello, jeśli nie bez dodatkowej pojemności dostępnej w tej lokalizacji.
>
> Nie można zmniejszyć hello przepustowości obwodu ExpressRoute bez zakłóceń. Obniżenie przepustowości wymaga obwodu ExpressRoute hello toodeprovision, a następnie Udostępnij ponownie nowy obwód usługi ExpressRoute.
> 
> 

#### <a name="resize-a-circuit"></a>Zmień rozmiar obwodu

Po wybraniu rozmiar, jaki należy można użyć następującego polecenia tooresize hello obwodu:

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

Obwodu będzie zostały wielkości po stronie firmy Microsoft hello. Należy skontaktować się konfiguracje łączności dostawcy tooupdate na ich toomatch po stronie tej zmiany. Należy pamiętać, że firma Microsoft będzie uruchamiane rozliczeń można uzyskać hello zaktualizować opcji przepustowości z tego punktu w.

Jeśli zostanie wyświetlony następujący błąd podczas zwiększyć przepustowość obwodu hello hello, to pozostaje nie wystarczającą przepustowość na fizyczny port hello, gdy jest tworzony z istniejącym obwodem. Masz toodelete ten obwód i utworzyć nowy obwód rozmiar hello, które są potrzebne. 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available tooperform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Anulowania obsługi i usuwania obwodu usługi ExpressRoute

### <a name="considerations"></a>Zagadnienia do rozważenia

* Należy odłączyć wszystkie sieci wirtualne od hello obwodu usługi expressroute dla toosucceed tej operacji. Sprawdź toosee, jeśli masz żadnych sieci wirtualnych, które są połączone obwodu toohello, jeśli ta operacja nie powiedzie się.
* Jeśli stan inicjowania obsługi hello ExpressRoute obwodu usługi Dostawca jest **inicjowania obsługi administracyjnej** lub **obsługiwane administracyjnie** należy skontaktować się z obwodu hello toodeprovision dostawcy usług w bok. Firma Microsoft będzie kontynuować tooreserve zasobów i obciążać Cię do momentu dostawcy usług hello kończy obwodu hello anulowania obsługi i powiadamia nam.
* Jeśli dostawcy usług hello została anulowana obwodu hello (stan inicjowania dostawcy usług hello ustawiono zbyt**nieudostępniane**) następnie można usunąć obwodu hello. Spowoduje to zatrzymanie rozliczeń dla hello obwodu.

#### <a name="delete-a-circuit"></a>Usunąć obwód

Można usunąć obwodu usługi ExpressRoute, uruchamiając następujące polecenie hello:

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a>Następne kroki
Po utworzeniu obwodu, upewnij się, że hello następujące:

* [Tworzenie i modyfikowanie routingu dla obwodu usługi ExpressRoute](expressroute-howto-routing-classic.md)
* [Łączenie z sieci wirtualnej tooyour obwodu usługi expressroute](expressroute-howto-linkvnet-classic.md)

