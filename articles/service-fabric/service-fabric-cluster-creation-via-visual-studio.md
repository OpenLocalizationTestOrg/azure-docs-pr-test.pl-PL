---
title: "Konfigurowanie klastra sieci szkieletowej usług za pomocą programu Visual Studio | Dokumentacja firmy Microsoft"
description: "Zawiera opis sposobu konfigurowania klastra sieci szkieletowej usług za pomocą szablonu usługi Azure Resource Manager utworzone przez projekt grupy zasobów platformy Azure w programie Visual Studio"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: adegeo
editor: 
ms.assetid: bd2c0511-36c9-4828-8dc3-69e4b6a70567
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/21/2017
ms.author: mikhegn
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: c43145b96cdbdfaa7e1893e50d027321fe4c0510
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a>Konfigurowanie klastra sieci szkieletowej usług za pomocą programu Visual Studio
W tym artykule opisano, jak skonfigurować klaster sieci szkieletowej usług Azure przy użyciu programu Visual Studio i szablonu usługi Azure Resource Manager. Projekt grupy zasobów programu Visual Studio Azure zostanie wykorzystany do utworzenia szablonu. Po utworzeniu szablonu można wdrożyć bezpośrednio na platformie Azure w programie Visual Studio. Może również służyć ze skryptu, lub w ramach instrumentu ciągłej integracji (CI).

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a>Tworzenie szablonu klastra sieci szkieletowej usług za pomocą projektu grupy zasobów platformy Azure
Aby rozpocząć, Otwórz program Visual Studio i utworzyć projekt grupy zasobów platformy Azure (jest on dostępny w **chmury** folder):

![Okno dialogowe nowego projektu z wybranego projektu grupy zasobów platformy Azure][1]

Można utworzyć nowe rozwiązanie Visual Studio dla tego projektu lub dodać do istniejącego rozwiązania.

> [!NOTE]
> Jeśli nie są wyświetlane w węźle chmury projektu grupy zasobów platformy Azure, nie masz zainstalowany zestaw SDK platformy Azure. Uruchamianie Instalatora platformy sieci Web ([go teraz zainstalować](http://www.microsoft.com/web/downloads/platform.aspx) Jeśli jeszcze tego nie zrobiono), a następnie wyszukaj "Azure SDK.NET" i zainstalować wersję, która jest zgodna z wersją programu Visual Studio.
> 
> 

Po naciśnięciu przycisku OK Visual Studio zapyta, aby wybrać szablon usługi Resource Manager, który chcesz utworzyć:

![Wybierz szablon Azure okna dialogowego z wybrany szablon klastra sieci szkieletowej usług][2]

Wybierz szablon klastra sieci szkieletowej usług, a następnie ponownie kliknij przycisk OK. Teraz utworzono projekt i szablonu usługi Resource Manager.

## <a name="prepare-the-template-for-deployment"></a>Przygotowanie do wdrożenia szablonu
Przed wdrożeniem szablonu do utworzenia klastra, należy podać wartości parametrów szablonu wymagane. Te wartości parametrów są odczytywane z `ServiceFabricCluster.parameters.json` pliku, który znajduje się w `Templates` folderu projektu grupy zasobów. Otwórz plik i podaj następujące wartości:

| Nazwa parametru | Opis |
| --- | --- |
| adminUserName |Nazwa konta administratora dla usługi Service Fabric komputerów (węzłów). |
| certificateThumbprint |Odcisk palca certyfikatu, która zabezpiecza klastra. |
| sourceVaultResourceId |*Identyfikator zasobu* przechowywania certyfikatów, która zabezpiecza klastra magazynu kluczy. |
| certificateUrlValue |Adres URL certyfikatu zabezpieczeń klastra. |

Szablon Menedżera zasobów programu Visual Studio usługi sieci szkieletowej tworzy bezpieczne klastra, który jest chroniony za pomocą certyfikatu. Ten certyfikat jest identyfikowany przez parametry szablonu ostatnich trzech (`certificateThumbprint`, `sourceVaultValue`, i `certificateUrlValue`), i musi istnieć w **usługi Azure Key Vault**. Aby uzyskać więcej informacji na temat tworzenia klastra certyfikatu zabezpieczeń, zobacz [scenariusze zabezpieczeń klastra sieci szkieletowej usług](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) artykułu.

## <a name="optional-change-the-cluster-name"></a>Opcjonalnie: Zmień nazwę klastra
Każdy klaster sieci szkieletowej usług ma nazwę. Po utworzeniu klastra sieci szkieletowej na platformie Azure nazwy klastra określa (wraz z region platformy Azure) nazwy systemu nazw domen (DNS, Domain Name System) klastra. Na przykład, jeśli nazwa klastra `myBigCluster`i lokalizacji (regionu Azure) grupy zasobów, który będzie obsługiwał nowego klastra jest wschodnie stany USA, nazwa DNS klastra będzie `myBigCluster.eastus.cloudapp.azure.com`.

Domyślnie nazwa klastra jest generowane automatycznie a unikatowy dołączając sufiksem losowe do prefiksu "klastra". Dzięki temu bardzo łatwo używać szablonu jako część **ciągłej integracji** systemu (CI). Jeśli chcesz użyć nazwy określone dla klastra, który ma znaczenie, ustaw wartość `clusterName` zmiennej w pliku szablonu usługi Resource Manager (`ServiceFabricCluster.json`) do wybranej nazwy. Jest to pierwsza zmienna zdefiniowana w tym pliku.

## <a name="optional-add-public-application-ports"></a>Opcjonalnie: Dodaj porty publiczny aplikacji
Można również zmienić porty publiczny aplikacji dla klastra, przed rozpoczęciem wdrażania. Domyślnie szablon otwiera publicznego tylko dwa porty TCP (80 i 8081). Jeśli potrzebujesz więcej aplikacji, należy zmodyfikować definicję modułu równoważenia obciążenia Azure w szablonie. Definicja jest przechowywana w pliku szablonu głównego (`ServiceFabricCluster.json`). Otwórz ten plik i wyszukaj `loadBalancedAppPort`. Każdy port jest skojarzona z trzech artefakty:

1. Zmienna szablonu, który definiuje wartość port TCP dla portu:
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. A *sondowania* określający, jak często i jak długo Azure obciążenia modułu równoważenia próbuje użyć określonego węzła sieci szkieletowej usług przed awarii na inny. Sondy są częścią zasobów usługi równoważenia obciążenia. Poniżej przedstawiono definicję sondowania pierwszy domyślny port aplikacji:
   
    ```json
    {
        "name": "AppPortProbe1",
        "properties": {
            "intervalInSeconds": 5,
            "numberOfProbes": 2,
            "port": "[variables('loadBalancedAppPort1')]",
            "protocol": "Tcp"
        }
    }
    ```
3. A *reguły równoważenia obciążenia* który wiąże ze sobą, port i badania, które umożliwia funkcji równoważenia obciążenia w zestawie węzłów klastra sieci szkieletowej usług:
   
    ```json
    {
        "name": "AppPortLBRule1",
        "properties": {
            "backendAddressPool": {
                "id": "[variables('lbPoolID0')]"
            },
            "backendPort": "[variables('loadBalancedAppPort1')]",
            "enableFloatingIP": false,
            "frontendIPConfiguration": {
                "id": "[variables('lbIPConfig0')]"
            },
            "frontendPort": "[variables('loadBalancedAppPort1')]",
            "idleTimeoutInMinutes": 5,
            "probe": {
                "id": "[concat(variables('lbID0'),'/probes/AppPortProbe1')]"
            },
            "protocol": "Tcp"
        }
    }
    ```
   Jeśli aplikacje, które planujesz wdrożyć w klastrze muszą więcej portów, należy dodać je tworzenia dodatkowych badania i definicji reguł równoważenia obciążenia. Aby uzyskać więcej informacji na temat pracy z usługą równoważenia obciążenia w Azure za pośrednictwem Menedżera zasobów szablonów, zobacz [rozpoczęcia tworzenia wewnętrznego modułu równoważenia obciążenia przy użyciu szablonu](../load-balancer/load-balancer-get-started-ilb-arm-template.md).

## <a name="deploy-the-template-by-using-visual-studio"></a>Wdrażanie szablonu przy użyciu programu Visual Studio
Po zapisaniu wszystkich wartości wymaganego parametru w`ServiceFabricCluster.param.dev.json` pliku, możesz przystąpić do wdrażania szablonu i tworzenia klastra usługi sieć szkieletowa usług. Kliknij prawym przyciskiem myszy projekt grupy zasobów w Eksploratorze rozwiązań w usłudze Visual Studio i wybierz polecenie **Wdróż | Nowe wdrożenie...** . Jeśli to konieczne, Visual Studio będzie **wdrażanie w grupie zasobów** okno dialogowe, monitem o uwierzytelniać na platformie Azure:

![Wdrażanie w oknie dialogowym grupy zasobów][3]

Okno dialogowe pozwala wybrać istniejącą grupę zasobów Menedżera zasobów dla klastra oraz udostępnia opcję, aby utworzyć nowy. Zwykle warto użyć oddzielnej grupie zasobów klastra sieci szkieletowej usług.

Po naciśnięciu przycisku Wdróż Visual Studio spowoduje wyświetlenie monitu o potwierdzenie wartości parametrów szablonu. Trafienia **zapisać** przycisku. Jeden parametr ma wartość utrwalonego: hasło konta administratora klastra. Należy podać wartość hasła, gdy program Visual Studio monituje o jeden.

> [!NOTE]
> Począwszy od zestaw Azure SDK 2.9, program Visual Studio obsługuje hasła odczytu z **usługi Azure Key Vault** podczas wdrażania. W oknie dialogowym Parametry szablonu należy zauważyć, że `adminPassword` pole tekstowe parametr ma mało ikonę "klucz" po prawej stronie. Ta ikona służy do wybierania istniejącym kluczem tajnym magazynu kluczy jako hasło administratora dla klastra. Po prostu upewnij się, że pierwszy Włącz dostęp do usługi Azure Resource Manager do wdrażania szablonu w zasadach dostępu Advanced magazynu kluczy. 
> 
> 

Możesz monitorować postęp procesu wdrażania w oknie danych wyjściowych programu Visual Studio. Po zakończeniu wdrażania szablonu nowego klastra jest gotowe do użycia!

> [!NOTE]
> Nigdy nie użyto programu PowerShell do administrowania Azure z komputera, którego obecnie używasz, należy wykonać nieco celów.
> 
> 1. Włączyć, uruchamiając skrypty programu PowerShell [ `Set-ExecutionPolicy` ](https://technet.microsoft.com/library/hh849812.aspx) polecenia. Programowanie maszyn "nieograniczony" zasady są zazwyczaj zaakceptować.
> 2. Zdecyduj, czy zezwolić na zbieranie danych diagnostycznych z poleceniami środowiska Azure PowerShell i uruchom [ `Enable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619303.aspx) lub [ `Disable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619236.aspx) odpowiednio do potrzeb. Pozwoli to uniknąć niepotrzebnych monity podczas wdrażania szablonu.
> 
> 

Jeśli wystąpią jakieś błędy, przejdź do [portalu Azure](https://portal.azure.com/) , a następnie otwórz wdrożone do grupy zasobów. Kliknij przycisk **wszystkie ustawienia**, następnie kliknij przycisk **wdrożeń** w bloku ustawień. Niepowodzenie wdrożenia grupy zasobów pozostawia szczegółowe informacje diagnostyczne.

> [!NOTE]
> Klastry usługi sieć szkieletowa usług wymagają określonej liczby węzłów pozwala uzyskać się zachować dostępność i zachować stan — nazywany "utrzymywania kworum". W związku z tym nie jest bezpieczne zamknięcie wszystkich komputerów w klastrze, chyba że najpierw wykonali [pełnej kopii zapasowej według stanu](service-fabric-reliable-services-backup-restore.md).
> 
> 

## <a name="next-steps"></a>Następne kroki
* [Więcej informacji na temat konfigurowania klastra sieci szkieletowej usług za pomocą portalu Azure](service-fabric-cluster-creation-via-portal.md)
* [Informacje o sposobie zarządzania i wdrażania aplikacji sieci szkieletowej usług za pomocą programu Visual Studio](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
