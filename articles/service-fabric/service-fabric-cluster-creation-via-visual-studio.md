---
title: "aaaSetting zapasowej klastra sieci szkieletowej usług za pomocą programu Visual Studio | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooset się usługi sieć szkieletowa klastra przy użyciu szablonu usługi Azure Resource Manager utworzone przez projekt grupy zasobów platformy Azure w programie Visual Studio"
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
ms.openlocfilehash: adb0dd2169a28b46e832c6f06c998cbed0c473f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a>Konfigurowanie klastra sieci szkieletowej usług za pomocą programu Visual Studio
W tym artykule opisano, jak tooset się sieć szkieletowa usług Azure klastra przy użyciu programu Visual Studio i szablonu usługi Azure Resource Manager. Używamy szablon hello toocreate projektu programu Visual Studio Azure zasobów grupy. Po utworzeniu szablonu hello, można ją wdrożyć bezpośrednio tooAzure z programu Visual Studio. Może również służyć ze skryptu, lub w ramach instrumentu ciągłej integracji (CI).

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a>Tworzenie szablonu klastra sieci szkieletowej usług za pomocą projektu grupy zasobów platformy Azure
Rozpoczęto tooget, Otwórz program Visual Studio i utworzyć projekt grupy zasobów platformy Azure (jest on dostępny w hello **chmury** folder):

![Okno dialogowe nowego projektu z wybranego projektu grupy zasobów platformy Azure][1]

Można utworzyć nowe rozwiązanie Visual Studio dla tego projektu lub dodać tooan istniejącego rozwiązania.

> [!NOTE]
> Jeśli nie ma hello projektu grupy zasobów platformy Azure w węźle chmury hello, nie masz hello zainstalowany zestaw SDK platformy Azure. Uruchamianie Instalatora platformy sieci Web ([go teraz zainstalować](http://www.microsoft.com/web/downloads/platform.aspx) Jeśli jeszcze tego nie zrobiono), a następnie wyszukaj "Azure SDK.NET" i zainstaluj hello wersji, która jest zgodna z wersją programu Visual Studio.
> 
> 

Po naciśnięciu przycisku OK hello Visual Studio zapyta szablonu usługi Resource Manager hello tooselect ma toocreate:

![Wybierz szablon Azure okna dialogowego z wybrany szablon klastra sieci szkieletowej usług][2]

Wybierz szablon klastra sieci szkieletowej usług hello i przycisk trafień hello OK ponownie. teraz utworzono projekt Hello i hello szablonu usługi Resource Manager.

## <a name="prepare-hello-template-for-deployment"></a>Przygotowanie do wdrożenia szablonu hello
Przed szablonu hello klastra hello toocreate wdrożone, należy podać wartości parametrów szablonu hello wymagane. Te wartości parametrów są odczytywane z hello `ServiceFabricCluster.parameters.json` pliku, który znajduje się w hello `Templates` folderu projektu grupy zasobów hello. Otwórz plik hello i podaj hello następujące wartości:

| Nazwa parametru | Opis |
| --- | --- |
| adminUserName |Nazwa Hello hello konta administratora dla usługi Service Fabric komputerów (węzłów). |
| certificateThumbprint |Witaj odcisk palca certyfikatu hello, która zabezpiecza hello klastra. |
| sourceVaultResourceId |Witaj *identyfikator zasobu* hello magazynu kluczy przechowywania hello certyfikatu, który zabezpiecza hello klastra. |
| certificateUrlValue |adres URL Hello certyfikat zabezpieczeń hello klastra. |

Szablon Menedżera zasobów sieci szkieletowej programu Visual Studio usługi Hello tworzy bezpieczne klastra, który jest chroniony za pomocą certyfikatu. Ten certyfikat jest identyfikowany przez hello ostatnie trzy parametry szablonu (`certificateThumbprint`, `sourceVaultValue`, i `certificateUrlValue`), i musi istnieć w **usługi Azure Key Vault**. Aby uzyskać więcej informacji dotyczących sposobu toocreate hello certyfikat zabezpieczeń klastra, zobacz [scenariusze zabezpieczeń klastra sieci szkieletowej usług](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) artykułu.

## <a name="optional-change-hello-cluster-name"></a>Opcjonalnie: Zmień nazwę klastra hello
Każdy klaster sieci szkieletowej usług ma nazwę. Po utworzeniu klastra sieci szkieletowej na platformie Azure (wraz z hello region platformy Azure) określa się nazwy klastra hello Nazwa systemu nazw domen (DNS, Domain Name System) klastra hello. Na przykład, jeśli nazwa klastra `myBigCluster`i hello lokalizacji (regionu Azure) hello grupy zasobów, który będzie obsługiwał hello nowego klastra jest wschodnie stany USA, nazwa DNS hello hello klastra będzie `myBigCluster.eastus.cloudapp.azure.com`.

Domyślnie nazwa klastra hello jest generowane automatycznie a unikatowy dołączając prefiksu "klastra" tooa losowe sufiks. Dzięki temu można bardzo łatwo toouse hello szablonu jako część **ciągłej integracji** systemu (CI). Jeśli chcesz toouse nazwę klastra, który jest łatwy do rozpoznania tooyou, ustaw wartość hello hello `clusterName` zmiennej w pliku szablonu usługi Resource Manager hello (`ServiceFabricCluster.json`) tooyour wybrana nazwa. Jest hello Pierwsza zmienna zdefiniowana w tym pliku.

## <a name="optional-add-public-application-ports"></a>Opcjonalnie: Dodaj porty publiczny aplikacji
Można również porty publiczny aplikacji hello toochange hello klastra przed jego wdrożeniem. Domyślnie szablon hello otwiera publicznego tylko dwa porty TCP (80 i 8081). Jeśli potrzebujesz więcej aplikacji, należy zmodyfikować definicję modułu równoważenia obciążenia Azure hello hello szablonu. Definicja Hello są przechowywane w pliku szablonu głównego hello (`ServiceFabricCluster.json`). Otwórz ten plik i wyszukaj `loadBalancedAppPort`. Każdy port jest skojarzona z trzech artefakty:

1. Zmienna szablonu, która definiuje wartość portu TCP hello hello portu:
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. A *sondowania* definiuje częstotliwość i czas hello modułu równoważenia obciążenia Azure prób toouse przed niepowodzeniem określonego węzła sieci szkieletowej usług za pośrednictwem tooanother jeden. sondy Hello są częścią hello zasobów usługi równoważenia obciążenia. Poniżej przedstawiono definicję sondowania hello pierwszy port domyślny aplikacji hello:
   
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
3. A *reguły równoważenia obciążenia* który wiąże ze sobą hello port i badania hello, które umożliwia funkcji równoważenia obciążenia w zestawie węzłów klastra sieci szkieletowej usług:
   
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
   Jeśli aplikacji hello zaplanowanie toodeploy toohello klastra konieczne więcej portów, należy dodać je tworzenia dodatkowych badania i definicji reguł równoważenia obciążenia. Aby uzyskać więcej informacji na temat toowork z modułem równoważenia obciążenia w Azure za pomocą szablonów usługi Resource Manager, zobacz [rozpoczęcia tworzenia wewnętrznego modułu równoważenia obciążenia przy użyciu szablonu](../load-balancer/load-balancer-get-started-ilb-arm-template.md).

## <a name="deploy-hello-template-by-using-visual-studio"></a>Wdrażanie szablonu hello przy użyciu programu Visual Studio
Po zapisaniu wszystkich hello wartości wymaganego parametru w`ServiceFabricCluster.param.dev.json` pliku, możesz są gotowe toodeploy hello szablonu i tworzenia klastra usługi sieć szkieletowa usług. Kliknij prawym przyciskiem myszy projekt grupy zasobów hello w Eksploratorze rozwiązań w usłudze Visual Studio i wybierz polecenie **Wdróż | Nowe wdrożenie...** . Jeśli to konieczne, Visual Studio będzie hello **wdrażanie tooResource grupy** okno dialogowe, monitem tooauthenticate tooAzure:

![Wdrażanie tooResource okno dialogowe][3]

okno dialogowe Hello pozwala wybrać istniejącą grupę zasobów Menedżera zasobów klastra hello i zapewnia hello toocreate opcję Nowy. Powoduje zwykle toouse znaczeniu oddzielnej grupie zasobów klastra sieci szkieletowej usług.

Po naciśnięciu przycisku Wdróż hello Visual Studio spowoduje wyświetlenie monitu wartości parametrów szablonu hello tooconfirm. Witaj trafień **zapisać** przycisku. Jeden parametr ma wartość utrwalonego: hasło konta administracyjnego hello hello klastra. Należy tooprovide wartość hasła, gdy program Visual Studio monituje o jeden.

> [!NOTE]
> Począwszy od zestaw Azure SDK 2.9, program Visual Studio obsługuje hasła odczytu z **usługi Azure Key Vault** podczas wdrażania. W oknie dialogowym Parametry szablonu hello Zwróć uwagę, że hello `adminPassword` pole tekstowe parametr ma mało ikonę "klucz" na powitania prawo. Ta ikona umożliwia tooselect istniejącym kluczem tajnym magazynu kluczy jako hasło administracyjne hello hello klastra. Po prostu upewnij się, że toofirst włączyć dostęp usługi Azure Resource Manager do wdrażania szablonu w zasadach dostępu Advanced hello magazynu kluczy. 
> 
> 

Możesz monitorować postęp hello hello procesu wdrażania w oknie danych wyjściowych programu Visual Studio hello. Po zakończeniu wdrażania szablonu hello nowego klastra jest gotowe toouse!

> [!NOTE]
> Środowiska PowerShell nigdy nie było używane tooadminister Azure z hello komputera, którego obecnie używasz, należy najpierw toodo nieco celów.
> 
> 1. Włącz PowerShell skryptów uruchamiając hello [ `Set-ExecutionPolicy` ](https://technet.microsoft.com/library/hh849812.aspx) polecenia. Programowanie maszyn "nieograniczony" zasady są zazwyczaj zaakceptować.
> 2. Zdecyduj, czy tooallow zbierania danych diagnostycznych z poleceń Azure PowerShell i uruchom [ `Enable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619303.aspx) lub [ `Disable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619236.aspx) odpowiednio do potrzeb. Pozwoli to uniknąć niepotrzebnych monity podczas wdrażania szablonu.
> 
> 

Jeśli wystąpią jakieś błędy, przejdź toohello [portalu Azure](https://portal.azure.com/) i otwórz hello grupy zasobów, która została wdrożona do. Kliknij przycisk **wszystkie ustawienia**, następnie kliknij przycisk **wdrożeń** w bloku ustawień hello. Niepowodzenie wdrożenia grupy zasobów pozostawia szczegółowe informacje diagnostyczne.

> [!NOTE]
> Klastrów sieci szkieletowej usług wymaga określonej liczby węzłów toobe toomaintain dostępności i Zachowaj stan — określonego tooas "utrzymywania kworum". W związku z tym nie jest bezpieczne tooshut dół wszystkich hello maszyn w klastrze hello, chyba że najpierw wykonali [pełnej kopii zapasowej według stanu](service-fabric-reliable-services-backup-restore.md).
> 
> 

## <a name="next-steps"></a>Następne kroki
* [Więcej informacji na temat konfigurowania klastra sieci szkieletowej usług za pomocą hello portalu Azure](service-fabric-cluster-creation-via-portal.md)
* [Dowiedz się, jak toomanage i wdrażania aplikacji sieci szkieletowej usług za pomocą programu Visual Studio](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
