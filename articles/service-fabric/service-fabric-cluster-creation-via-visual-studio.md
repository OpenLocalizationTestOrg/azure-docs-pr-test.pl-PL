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
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a><span data-ttu-id="52417-103">Konfigurowanie klastra sieci szkieletowej usług za pomocą programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="52417-103">Set up a Service Fabric cluster by using Visual Studio</span></span>
<span data-ttu-id="52417-104">W tym artykule opisano, jak tooset się sieć szkieletowa usług Azure klastra przy użyciu programu Visual Studio i szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="52417-104">This article describes how tooset up an Azure Service Fabric cluster by using Visual Studio and an Azure Resource Manager template.</span></span> <span data-ttu-id="52417-105">Używamy szablon hello toocreate projektu programu Visual Studio Azure zasobów grupy.</span><span class="sxs-lookup"><span data-stu-id="52417-105">We will use a Visual Studio Azure resource group project toocreate hello template.</span></span> <span data-ttu-id="52417-106">Po utworzeniu szablonu hello, można ją wdrożyć bezpośrednio tooAzure z programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="52417-106">After hello template has been created, it can be deployed directly tooAzure from Visual Studio.</span></span> <span data-ttu-id="52417-107">Może również służyć ze skryptu, lub w ramach instrumentu ciągłej integracji (CI).</span><span class="sxs-lookup"><span data-stu-id="52417-107">It can also be used from a script, or as part of continuous integration (CI) facility.</span></span>

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a><span data-ttu-id="52417-108">Tworzenie szablonu klastra sieci szkieletowej usług za pomocą projektu grupy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="52417-108">Create a Service Fabric cluster template by using an Azure resource group project</span></span>
<span data-ttu-id="52417-109">Rozpoczęto tooget, Otwórz program Visual Studio i utworzyć projekt grupy zasobów platformy Azure (jest on dostępny w hello **chmury** folder):</span><span class="sxs-lookup"><span data-stu-id="52417-109">tooget started, open Visual Studio and create an Azure resource group project (it is available in hello **Cloud** folder):</span></span>

![Okno dialogowe nowego projektu z wybranego projektu grupy zasobów platformy Azure][1]

<span data-ttu-id="52417-111">Można utworzyć nowe rozwiązanie Visual Studio dla tego projektu lub dodać tooan istniejącego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="52417-111">You can create a new Visual Studio solution for this project or add it tooan existing solution.</span></span>

> [!NOTE]
> <span data-ttu-id="52417-112">Jeśli nie ma hello projektu grupy zasobów platformy Azure w węźle chmury hello, nie masz hello zainstalowany zestaw SDK platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="52417-112">If you do not see hello Azure resource group project under hello Cloud node, you do not have hello Azure SDK installed.</span></span> <span data-ttu-id="52417-113">Uruchamianie Instalatora platformy sieci Web ([go teraz zainstalować](http://www.microsoft.com/web/downloads/platform.aspx) Jeśli jeszcze tego nie zrobiono), a następnie wyszukaj "Azure SDK.NET" i zainstaluj hello wersji, która jest zgodna z wersją programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="52417-113">Launch Web Platform Installer ([install it now](http://www.microsoft.com/web/downloads/platform.aspx) if you have not already), and then search for "Azure SDK for .NET" and install hello version that is compatible with your version of Visual Studio.</span></span>
> 
> 

<span data-ttu-id="52417-114">Po naciśnięciu przycisku OK hello Visual Studio zapyta szablonu usługi Resource Manager hello tooselect ma toocreate:</span><span class="sxs-lookup"><span data-stu-id="52417-114">After you hit hello OK button, Visual Studio will ask you tooselect hello Resource Manager template you want toocreate:</span></span>

![Wybierz szablon Azure okna dialogowego z wybrany szablon klastra sieci szkieletowej usług][2]

<span data-ttu-id="52417-116">Wybierz szablon klastra sieci szkieletowej usług hello i przycisk trafień hello OK ponownie.</span><span class="sxs-lookup"><span data-stu-id="52417-116">Select hello Service Fabric Cluster template and hit hello OK button again.</span></span> <span data-ttu-id="52417-117">teraz utworzono projekt Hello i hello szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="52417-117">hello project and hello Resource Manager template have now been created.</span></span>

## <a name="prepare-hello-template-for-deployment"></a><span data-ttu-id="52417-118">Przygotowanie do wdrożenia szablonu hello</span><span class="sxs-lookup"><span data-stu-id="52417-118">Prepare hello template for deployment</span></span>
<span data-ttu-id="52417-119">Przed szablonu hello klastra hello toocreate wdrożone, należy podać wartości parametrów szablonu hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="52417-119">Before hello template is deployed toocreate hello cluster, you must provide values for hello required template parameters.</span></span> <span data-ttu-id="52417-120">Te wartości parametrów są odczytywane z hello `ServiceFabricCluster.parameters.json` pliku, który znajduje się w hello `Templates` folderu projektu grupy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="52417-120">These parameter values are read from hello `ServiceFabricCluster.parameters.json` file, which is in hello `Templates` folder of hello resource group project.</span></span> <span data-ttu-id="52417-121">Otwórz plik hello i podaj hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="52417-121">Open hello file and provide hello following values:</span></span>

| <span data-ttu-id="52417-122">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="52417-122">Parameter name</span></span> | <span data-ttu-id="52417-123">Opis</span><span class="sxs-lookup"><span data-stu-id="52417-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="52417-124">adminUserName</span><span class="sxs-lookup"><span data-stu-id="52417-124">adminUserName</span></span> |<span data-ttu-id="52417-125">Nazwa Hello hello konta administratora dla usługi Service Fabric komputerów (węzłów).</span><span class="sxs-lookup"><span data-stu-id="52417-125">hello name of hello administrator account for Service Fabric machines (nodes).</span></span> |
| <span data-ttu-id="52417-126">certificateThumbprint</span><span class="sxs-lookup"><span data-stu-id="52417-126">certificateThumbprint</span></span> |<span data-ttu-id="52417-127">Witaj odcisk palca certyfikatu hello, która zabezpiecza hello klastra.</span><span class="sxs-lookup"><span data-stu-id="52417-127">hello thumbprint of hello certificate that secures hello cluster.</span></span> |
| <span data-ttu-id="52417-128">sourceVaultResourceId</span><span class="sxs-lookup"><span data-stu-id="52417-128">sourceVaultResourceId</span></span> |<span data-ttu-id="52417-129">Witaj *identyfikator zasobu* hello magazynu kluczy przechowywania hello certyfikatu, który zabezpiecza hello klastra.</span><span class="sxs-lookup"><span data-stu-id="52417-129">hello *resource ID* of hello key vault where hello certificate that secures hello cluster is stored.</span></span> |
| <span data-ttu-id="52417-130">certificateUrlValue</span><span class="sxs-lookup"><span data-stu-id="52417-130">certificateUrlValue</span></span> |<span data-ttu-id="52417-131">adres URL Hello certyfikat zabezpieczeń hello klastra.</span><span class="sxs-lookup"><span data-stu-id="52417-131">hello URL of hello cluster security certificate.</span></span> |

<span data-ttu-id="52417-132">Szablon Menedżera zasobów sieci szkieletowej programu Visual Studio usługi Hello tworzy bezpieczne klastra, który jest chroniony za pomocą certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="52417-132">hello Visual Studio Service Fabric Resource Manager template creates a secure cluster that is protected by a certificate.</span></span> <span data-ttu-id="52417-133">Ten certyfikat jest identyfikowany przez hello ostatnie trzy parametry szablonu (`certificateThumbprint`, `sourceVaultValue`, i `certificateUrlValue`), i musi istnieć w **usługi Azure Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="52417-133">This certificate is identified by hello last three template parameters (`certificateThumbprint`, `sourceVaultValue`, and `certificateUrlValue`), and it must exist in an **Azure Key Vault**.</span></span> <span data-ttu-id="52417-134">Aby uzyskać więcej informacji dotyczących sposobu toocreate hello certyfikat zabezpieczeń klastra, zobacz [scenariusze zabezpieczeń klastra sieci szkieletowej usług](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) artykułu.</span><span class="sxs-lookup"><span data-stu-id="52417-134">For more information on how toocreate hello cluster security certificate, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) article.</span></span>

## <a name="optional-change-hello-cluster-name"></a><span data-ttu-id="52417-135">Opcjonalnie: Zmień nazwę klastra hello</span><span class="sxs-lookup"><span data-stu-id="52417-135">Optional: change hello cluster name</span></span>
<span data-ttu-id="52417-136">Każdy klaster sieci szkieletowej usług ma nazwę.</span><span class="sxs-lookup"><span data-stu-id="52417-136">Every Service Fabric cluster has a name.</span></span> <span data-ttu-id="52417-137">Po utworzeniu klastra sieci szkieletowej na platformie Azure (wraz z hello region platformy Azure) określa się nazwy klastra hello Nazwa systemu nazw domen (DNS, Domain Name System) klastra hello.</span><span class="sxs-lookup"><span data-stu-id="52417-137">When a Fabric cluster is created in Azure, cluster name determines (together with hello Azure region) hello Domain Name System (DNS) name for hello cluster.</span></span> <span data-ttu-id="52417-138">Na przykład, jeśli nazwa klastra `myBigCluster`i hello lokalizacji (regionu Azure) hello grupy zasobów, który będzie obsługiwał hello nowego klastra jest wschodnie stany USA, nazwa DNS hello hello klastra będzie `myBigCluster.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="52417-138">For example, if you name your cluster `myBigCluster`, and hello location (Azure region) of hello resource group that will host hello new cluster is East US, hello DNS name of hello cluster will be `myBigCluster.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="52417-139">Domyślnie nazwa klastra hello jest generowane automatycznie a unikatowy dołączając prefiksu "klastra" tooa losowe sufiks.</span><span class="sxs-lookup"><span data-stu-id="52417-139">By default hello cluster name is generated automatically and made unique by attaching a random suffix tooa "cluster" prefix.</span></span> <span data-ttu-id="52417-140">Dzięki temu można bardzo łatwo toouse hello szablonu jako część **ciągłej integracji** systemu (CI).</span><span class="sxs-lookup"><span data-stu-id="52417-140">This makes it very easy toouse hello template as part of a **continuous integration** (CI) system.</span></span> <span data-ttu-id="52417-141">Jeśli chcesz toouse nazwę klastra, który jest łatwy do rozpoznania tooyou, ustaw wartość hello hello `clusterName` zmiennej w pliku szablonu usługi Resource Manager hello (`ServiceFabricCluster.json`) tooyour wybrana nazwa.</span><span class="sxs-lookup"><span data-stu-id="52417-141">If you want toouse a specific name for your cluster, one that is meaningful tooyou, set hello value of hello `clusterName` variable in hello Resource Manager template file (`ServiceFabricCluster.json`) tooyour chosen name.</span></span> <span data-ttu-id="52417-142">Jest hello Pierwsza zmienna zdefiniowana w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="52417-142">It is hello first variable defined in that file.</span></span>

## <a name="optional-add-public-application-ports"></a><span data-ttu-id="52417-143">Opcjonalnie: Dodaj porty publiczny aplikacji</span><span class="sxs-lookup"><span data-stu-id="52417-143">Optional: add public application ports</span></span>
<span data-ttu-id="52417-144">Można również porty publiczny aplikacji hello toochange hello klastra przed jego wdrożeniem.</span><span class="sxs-lookup"><span data-stu-id="52417-144">You may also want toochange hello public application ports for hello cluster before you deploy it.</span></span> <span data-ttu-id="52417-145">Domyślnie szablon hello otwiera publicznego tylko dwa porty TCP (80 i 8081).</span><span class="sxs-lookup"><span data-stu-id="52417-145">By default, hello template opens up just two public TCP ports (80 and 8081).</span></span> <span data-ttu-id="52417-146">Jeśli potrzebujesz więcej aplikacji, należy zmodyfikować definicję modułu równoważenia obciążenia Azure hello hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="52417-146">If you need more for your applications, modify hello Azure Load Balancer definition in hello template.</span></span> <span data-ttu-id="52417-147">Definicja Hello są przechowywane w pliku szablonu głównego hello (`ServiceFabricCluster.json`).</span><span class="sxs-lookup"><span data-stu-id="52417-147">hello definition is stored in hello main template file (`ServiceFabricCluster.json`).</span></span> <span data-ttu-id="52417-148">Otwórz ten plik i wyszukaj `loadBalancedAppPort`.</span><span class="sxs-lookup"><span data-stu-id="52417-148">Open that file and search for `loadBalancedAppPort`.</span></span> <span data-ttu-id="52417-149">Każdy port jest skojarzona z trzech artefakty:</span><span class="sxs-lookup"><span data-stu-id="52417-149">Each port is associated with three artifacts:</span></span>

1. <span data-ttu-id="52417-150">Zmienna szablonu, która definiuje wartość portu TCP hello hello portu:</span><span class="sxs-lookup"><span data-stu-id="52417-150">A template variable that defines hello TCP port value for hello port:</span></span>
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. <span data-ttu-id="52417-151">A *sondowania* definiuje częstotliwość i czas hello modułu równoważenia obciążenia Azure prób toouse przed niepowodzeniem określonego węzła sieci szkieletowej usług za pośrednictwem tooanother jeden.</span><span class="sxs-lookup"><span data-stu-id="52417-151">A *probe* that defines how frequently and for how long hello Azure load balancer attempts toouse a specific Service Fabric node before failing over tooanother one.</span></span> <span data-ttu-id="52417-152">sondy Hello są częścią hello zasobów usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="52417-152">hello probes are part of hello Load Balancer resource.</span></span> <span data-ttu-id="52417-153">Poniżej przedstawiono definicję sondowania hello pierwszy port domyślny aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="52417-153">Here is hello probe definition for hello first default application port:</span></span>
   
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
3. <span data-ttu-id="52417-154">A *reguły równoważenia obciążenia* który wiąże ze sobą hello port i badania hello, które umożliwia funkcji równoważenia obciążenia w zestawie węzłów klastra sieci szkieletowej usług:</span><span class="sxs-lookup"><span data-stu-id="52417-154">A *load-balancing rule* that ties together hello port and hello probe, which enables load balancing across a set of Service Fabric cluster nodes:</span></span>
   
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
   <span data-ttu-id="52417-155">Jeśli aplikacji hello zaplanowanie toodeploy toohello klastra konieczne więcej portów, należy dodać je tworzenia dodatkowych badania i definicji reguł równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="52417-155">If hello applications that you plan toodeploy toohello cluster need more ports, you can add them by creating additional probe and load-balancing rule definitions.</span></span> <span data-ttu-id="52417-156">Aby uzyskać więcej informacji na temat toowork z modułem równoważenia obciążenia w Azure za pomocą szablonów usługi Resource Manager, zobacz [rozpoczęcia tworzenia wewnętrznego modułu równoważenia obciążenia przy użyciu szablonu](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="52417-156">For more information on how toowork with Azure Load Balancer through Resource Manager templates, see [Get started creating an internal load balancer using a template](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span></span>

## <a name="deploy-hello-template-by-using-visual-studio"></a><span data-ttu-id="52417-157">Wdrażanie szablonu hello przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="52417-157">Deploy hello template by using Visual Studio</span></span>
<span data-ttu-id="52417-158">Po zapisaniu wszystkich hello wartości wymaganego parametru w`ServiceFabricCluster.param.dev.json` pliku, możesz są gotowe toodeploy hello szablonu i tworzenia klastra usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="52417-158">After you have saved all hello required parameter values in the`ServiceFabricCluster.param.dev.json` file, you are ready toodeploy hello template and create your Service Fabric cluster.</span></span> <span data-ttu-id="52417-159">Kliknij prawym przyciskiem myszy projekt grupy zasobów hello w Eksploratorze rozwiązań w usłudze Visual Studio i wybierz polecenie **Wdróż | Nowe wdrożenie...** . Jeśli to konieczne, Visual Studio będzie hello **wdrażanie tooResource grupy** okno dialogowe, monitem tooauthenticate tooAzure:</span><span class="sxs-lookup"><span data-stu-id="52417-159">Right-click hello resource group project in Visual Studio Solution Explorer and choose **Deploy | New Deployment...**. If necessary, Visual Studio will show hello **Deploy tooResource Group** dialog box, asking you tooauthenticate tooAzure:</span></span>

![Wdrażanie tooResource okno dialogowe][3]

<span data-ttu-id="52417-161">okno dialogowe Hello pozwala wybrać istniejącą grupę zasobów Menedżera zasobów klastra hello i zapewnia hello toocreate opcję Nowy.</span><span class="sxs-lookup"><span data-stu-id="52417-161">hello dialog box lets you choose an existing Resource Manager resource group for hello cluster and gives you hello option toocreate a new one.</span></span> <span data-ttu-id="52417-162">Powoduje zwykle toouse znaczeniu oddzielnej grupie zasobów klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="52417-162">It normally makes sense toouse a separate resource group for a Service Fabric cluster.</span></span>

<span data-ttu-id="52417-163">Po naciśnięciu przycisku Wdróż hello Visual Studio spowoduje wyświetlenie monitu wartości parametrów szablonu hello tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="52417-163">After you hit hello Deploy button, Visual Studio will prompt you tooconfirm hello template parameter values.</span></span> <span data-ttu-id="52417-164">Witaj trafień **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="52417-164">Hit hello **Save** button.</span></span> <span data-ttu-id="52417-165">Jeden parametr ma wartość utrwalonego: hasło konta administracyjnego hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="52417-165">One parameter does not have a persisted value: hello administrative account password for hello cluster.</span></span> <span data-ttu-id="52417-166">Należy tooprovide wartość hasła, gdy program Visual Studio monituje o jeden.</span><span class="sxs-lookup"><span data-stu-id="52417-166">You need tooprovide a password value when Visual Studio prompts you for one.</span></span>

> [!NOTE]
> <span data-ttu-id="52417-167">Począwszy od zestaw Azure SDK 2.9, program Visual Studio obsługuje hasła odczytu z **usługi Azure Key Vault** podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="52417-167">Starting with Azure SDK 2.9, Visual Studio supports reading passwords from **Azure Key Vault** during deployment.</span></span> <span data-ttu-id="52417-168">W oknie dialogowym Parametry szablonu hello Zwróć uwagę, że hello `adminPassword` pole tekstowe parametr ma mało ikonę "klucz" na powitania prawo.</span><span class="sxs-lookup"><span data-stu-id="52417-168">In hello template parameters dialog notice that hello `adminPassword` parameter text box has a little "key" icon on hello right.</span></span> <span data-ttu-id="52417-169">Ta ikona umożliwia tooselect istniejącym kluczem tajnym magazynu kluczy jako hasło administracyjne hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="52417-169">This icon allows you tooselect an existing key vault secret as hello administrative password for hello cluster.</span></span> <span data-ttu-id="52417-170">Po prostu upewnij się, że toofirst włączyć dostęp usługi Azure Resource Manager do wdrażania szablonu w zasadach dostępu Advanced hello magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="52417-170">Just make sure toofirst enable Azure Resource Manager access for template deployment in hello Advanced Access Policies of your key vault.</span></span> 
> 
> 

<span data-ttu-id="52417-171">Możesz monitorować postęp hello hello procesu wdrażania w oknie danych wyjściowych programu Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="52417-171">You can monitor hello progress of hello deployment process in hello Visual Studio output window.</span></span> <span data-ttu-id="52417-172">Po zakończeniu wdrażania szablonu hello nowego klastra jest gotowe toouse!</span><span class="sxs-lookup"><span data-stu-id="52417-172">Once hello template deployment is completed, your new cluster is ready toouse!</span></span>

> [!NOTE]
> <span data-ttu-id="52417-173">Środowiska PowerShell nigdy nie było używane tooadminister Azure z hello komputera, którego obecnie używasz, należy najpierw toodo nieco celów.</span><span class="sxs-lookup"><span data-stu-id="52417-173">If PowerShell was never used tooadminister Azure from hello machine that you are using now, you need toodo a little housekeeping.</span></span>
> 
> 1. <span data-ttu-id="52417-174">Włącz PowerShell skryptów uruchamiając hello [ `Set-ExecutionPolicy` ](https://technet.microsoft.com/library/hh849812.aspx) polecenia.</span><span class="sxs-lookup"><span data-stu-id="52417-174">Enable PowerShell scripting by running hello [`Set-ExecutionPolicy`](https://technet.microsoft.com/library/hh849812.aspx) command.</span></span> <span data-ttu-id="52417-175">Programowanie maszyn "nieograniczony" zasady są zazwyczaj zaakceptować.</span><span class="sxs-lookup"><span data-stu-id="52417-175">For development machines, "unrestricted" policy is usually acceptable.</span></span>
> 2. <span data-ttu-id="52417-176">Zdecyduj, czy tooallow zbierania danych diagnostycznych z poleceń Azure PowerShell i uruchom [ `Enable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619303.aspx) lub [ `Disable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619236.aspx) odpowiednio do potrzeb.</span><span class="sxs-lookup"><span data-stu-id="52417-176">Decide whether tooallow diagnostic data collection from Azure PowerShell commands, and run [`Enable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619303.aspx) or [`Disable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619236.aspx) as necessary.</span></span> <span data-ttu-id="52417-177">Pozwoli to uniknąć niepotrzebnych monity podczas wdrażania szablonu.</span><span class="sxs-lookup"><span data-stu-id="52417-177">This will avoid unnecessary prompts during template deployment.</span></span>
> 
> 

<span data-ttu-id="52417-178">Jeśli wystąpią jakieś błędy, przejdź toohello [portalu Azure](https://portal.azure.com/) i otwórz hello grupy zasobów, która została wdrożona do.</span><span class="sxs-lookup"><span data-stu-id="52417-178">If there are any errors, go toohello [Azure portal](https://portal.azure.com/) and open hello resource group that you deployed to.</span></span> <span data-ttu-id="52417-179">Kliknij przycisk **wszystkie ustawienia**, następnie kliknij przycisk **wdrożeń** w bloku ustawień hello.</span><span class="sxs-lookup"><span data-stu-id="52417-179">Click **All settings**, then click **Deployments** on hello settings blade.</span></span> <span data-ttu-id="52417-180">Niepowodzenie wdrożenia grupy zasobów pozostawia szczegółowe informacje diagnostyczne.</span><span class="sxs-lookup"><span data-stu-id="52417-180">A failed resource-group deployment leaves detailed diagnostic information there.</span></span>

> [!NOTE]
> <span data-ttu-id="52417-181">Klastrów sieci szkieletowej usług wymaga określonej liczby węzłów toobe toomaintain dostępności i Zachowaj stan — określonego tooas "utrzymywania kworum".</span><span class="sxs-lookup"><span data-stu-id="52417-181">Service Fabric clusters require a certain number of nodes toobe up toomaintain availability and preserve state - referred tooas "maintaining quorum."</span></span> <span data-ttu-id="52417-182">W związku z tym nie jest bezpieczne tooshut dół wszystkich hello maszyn w klastrze hello, chyba że najpierw wykonali [pełnej kopii zapasowej według stanu](service-fabric-reliable-services-backup-restore.md).</span><span class="sxs-lookup"><span data-stu-id="52417-182">Therefore, it is not safe tooshut down all of hello machines in hello cluster unless you have first performed a [full backup of your state](service-fabric-reliable-services-backup-restore.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="52417-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="52417-183">Next steps</span></span>
* [<span data-ttu-id="52417-184">Więcej informacji na temat konfigurowania klastra sieci szkieletowej usług za pomocą hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="52417-184">Learn about setting up Service Fabric cluster using hello Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="52417-185">Dowiedz się, jak toomanage i wdrażania aplikacji sieci szkieletowej usług za pomocą programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="52417-185">Learn how toomanage and deploy Service Fabric applications using Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
