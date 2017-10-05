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
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a><span data-ttu-id="16868-103">Konfigurowanie klastra sieci szkieletowej usług za pomocą programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="16868-103">Set up a Service Fabric cluster by using Visual Studio</span></span>
<span data-ttu-id="16868-104">W tym artykule opisano, jak skonfigurować klaster sieci szkieletowej usług Azure przy użyciu programu Visual Studio i szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="16868-104">This article describes how to set up an Azure Service Fabric cluster by using Visual Studio and an Azure Resource Manager template.</span></span> <span data-ttu-id="16868-105">Projekt grupy zasobów programu Visual Studio Azure zostanie wykorzystany do utworzenia szablonu.</span><span class="sxs-lookup"><span data-stu-id="16868-105">We will use a Visual Studio Azure resource group project to create the template.</span></span> <span data-ttu-id="16868-106">Po utworzeniu szablonu można wdrożyć bezpośrednio na platformie Azure w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="16868-106">After the template has been created, it can be deployed directly to Azure from Visual Studio.</span></span> <span data-ttu-id="16868-107">Może również służyć ze skryptu, lub w ramach instrumentu ciągłej integracji (CI).</span><span class="sxs-lookup"><span data-stu-id="16868-107">It can also be used from a script, or as part of continuous integration (CI) facility.</span></span>

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a><span data-ttu-id="16868-108">Tworzenie szablonu klastra sieci szkieletowej usług za pomocą projektu grupy zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="16868-108">Create a Service Fabric cluster template by using an Azure resource group project</span></span>
<span data-ttu-id="16868-109">Aby rozpocząć, Otwórz program Visual Studio i utworzyć projekt grupy zasobów platformy Azure (jest on dostępny w **chmury** folder):</span><span class="sxs-lookup"><span data-stu-id="16868-109">To get started, open Visual Studio and create an Azure resource group project (it is available in the **Cloud** folder):</span></span>

![Okno dialogowe nowego projektu z wybranego projektu grupy zasobów platformy Azure][1]

<span data-ttu-id="16868-111">Można utworzyć nowe rozwiązanie Visual Studio dla tego projektu lub dodać do istniejącego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="16868-111">You can create a new Visual Studio solution for this project or add it to an existing solution.</span></span>

> [!NOTE]
> <span data-ttu-id="16868-112">Jeśli nie są wyświetlane w węźle chmury projektu grupy zasobów platformy Azure, nie masz zainstalowany zestaw SDK platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="16868-112">If you do not see the Azure resource group project under the Cloud node, you do not have the Azure SDK installed.</span></span> <span data-ttu-id="16868-113">Uruchamianie Instalatora platformy sieci Web ([go teraz zainstalować](http://www.microsoft.com/web/downloads/platform.aspx) Jeśli jeszcze tego nie zrobiono), a następnie wyszukaj "Azure SDK.NET" i zainstalować wersję, która jest zgodna z wersją programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="16868-113">Launch Web Platform Installer ([install it now](http://www.microsoft.com/web/downloads/platform.aspx) if you have not already), and then search for "Azure SDK for .NET" and install the version that is compatible with your version of Visual Studio.</span></span>
> 
> 

<span data-ttu-id="16868-114">Po naciśnięciu przycisku OK Visual Studio zapyta, aby wybrać szablon usługi Resource Manager, który chcesz utworzyć:</span><span class="sxs-lookup"><span data-stu-id="16868-114">After you hit the OK button, Visual Studio will ask you to select the Resource Manager template you want to create:</span></span>

![Wybierz szablon Azure okna dialogowego z wybrany szablon klastra sieci szkieletowej usług][2]

<span data-ttu-id="16868-116">Wybierz szablon klastra sieci szkieletowej usług, a następnie ponownie kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="16868-116">Select the Service Fabric Cluster template and hit the OK button again.</span></span> <span data-ttu-id="16868-117">Teraz utworzono projekt i szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="16868-117">The project and the Resource Manager template have now been created.</span></span>

## <a name="prepare-the-template-for-deployment"></a><span data-ttu-id="16868-118">Przygotowanie do wdrożenia szablonu</span><span class="sxs-lookup"><span data-stu-id="16868-118">Prepare the template for deployment</span></span>
<span data-ttu-id="16868-119">Przed wdrożeniem szablonu do utworzenia klastra, należy podać wartości parametrów szablonu wymagane.</span><span class="sxs-lookup"><span data-stu-id="16868-119">Before the template is deployed to create the cluster, you must provide values for the required template parameters.</span></span> <span data-ttu-id="16868-120">Te wartości parametrów są odczytywane z `ServiceFabricCluster.parameters.json` pliku, który znajduje się w `Templates` folderu projektu grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="16868-120">These parameter values are read from the `ServiceFabricCluster.parameters.json` file, which is in the `Templates` folder of the resource group project.</span></span> <span data-ttu-id="16868-121">Otwórz plik i podaj następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="16868-121">Open the file and provide the following values:</span></span>

| <span data-ttu-id="16868-122">Nazwa parametru</span><span class="sxs-lookup"><span data-stu-id="16868-122">Parameter name</span></span> | <span data-ttu-id="16868-123">Opis</span><span class="sxs-lookup"><span data-stu-id="16868-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="16868-124">adminUserName</span><span class="sxs-lookup"><span data-stu-id="16868-124">adminUserName</span></span> |<span data-ttu-id="16868-125">Nazwa konta administratora dla usługi Service Fabric komputerów (węzłów).</span><span class="sxs-lookup"><span data-stu-id="16868-125">The name of the administrator account for Service Fabric machines (nodes).</span></span> |
| <span data-ttu-id="16868-126">certificateThumbprint</span><span class="sxs-lookup"><span data-stu-id="16868-126">certificateThumbprint</span></span> |<span data-ttu-id="16868-127">Odcisk palca certyfikatu, która zabezpiecza klastra.</span><span class="sxs-lookup"><span data-stu-id="16868-127">The thumbprint of the certificate that secures the cluster.</span></span> |
| <span data-ttu-id="16868-128">sourceVaultResourceId</span><span class="sxs-lookup"><span data-stu-id="16868-128">sourceVaultResourceId</span></span> |<span data-ttu-id="16868-129">*Identyfikator zasobu* przechowywania certyfikatów, która zabezpiecza klastra magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="16868-129">The *resource ID* of the key vault where the certificate that secures the cluster is stored.</span></span> |
| <span data-ttu-id="16868-130">certificateUrlValue</span><span class="sxs-lookup"><span data-stu-id="16868-130">certificateUrlValue</span></span> |<span data-ttu-id="16868-131">Adres URL certyfikatu zabezpieczeń klastra.</span><span class="sxs-lookup"><span data-stu-id="16868-131">The URL of the cluster security certificate.</span></span> |

<span data-ttu-id="16868-132">Szablon Menedżera zasobów programu Visual Studio usługi sieci szkieletowej tworzy bezpieczne klastra, który jest chroniony za pomocą certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="16868-132">The Visual Studio Service Fabric Resource Manager template creates a secure cluster that is protected by a certificate.</span></span> <span data-ttu-id="16868-133">Ten certyfikat jest identyfikowany przez parametry szablonu ostatnich trzech (`certificateThumbprint`, `sourceVaultValue`, i `certificateUrlValue`), i musi istnieć w **usługi Azure Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="16868-133">This certificate is identified by the last three template parameters (`certificateThumbprint`, `sourceVaultValue`, and `certificateUrlValue`), and it must exist in an **Azure Key Vault**.</span></span> <span data-ttu-id="16868-134">Aby uzyskać więcej informacji na temat tworzenia klastra certyfikatu zabezpieczeń, zobacz [scenariusze zabezpieczeń klastra sieci szkieletowej usług](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) artykułu.</span><span class="sxs-lookup"><span data-stu-id="16868-134">For more information on how to create the cluster security certificate, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) article.</span></span>

## <a name="optional-change-the-cluster-name"></a><span data-ttu-id="16868-135">Opcjonalnie: Zmień nazwę klastra</span><span class="sxs-lookup"><span data-stu-id="16868-135">Optional: change the cluster name</span></span>
<span data-ttu-id="16868-136">Każdy klaster sieci szkieletowej usług ma nazwę.</span><span class="sxs-lookup"><span data-stu-id="16868-136">Every Service Fabric cluster has a name.</span></span> <span data-ttu-id="16868-137">Po utworzeniu klastra sieci szkieletowej na platformie Azure nazwy klastra określa (wraz z region platformy Azure) nazwy systemu nazw domen (DNS, Domain Name System) klastra.</span><span class="sxs-lookup"><span data-stu-id="16868-137">When a Fabric cluster is created in Azure, cluster name determines (together with the Azure region) the Domain Name System (DNS) name for the cluster.</span></span> <span data-ttu-id="16868-138">Na przykład, jeśli nazwa klastra `myBigCluster`i lokalizacji (regionu Azure) grupy zasobów, który będzie obsługiwał nowego klastra jest wschodnie stany USA, nazwa DNS klastra będzie `myBigCluster.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="16868-138">For example, if you name your cluster `myBigCluster`, and the location (Azure region) of the resource group that will host the new cluster is East US, the DNS name of the cluster will be `myBigCluster.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="16868-139">Domyślnie nazwa klastra jest generowane automatycznie a unikatowy dołączając sufiksem losowe do prefiksu "klastra".</span><span class="sxs-lookup"><span data-stu-id="16868-139">By default the cluster name is generated automatically and made unique by attaching a random suffix to a "cluster" prefix.</span></span> <span data-ttu-id="16868-140">Dzięki temu bardzo łatwo używać szablonu jako część **ciągłej integracji** systemu (CI).</span><span class="sxs-lookup"><span data-stu-id="16868-140">This makes it very easy to use the template as part of a **continuous integration** (CI) system.</span></span> <span data-ttu-id="16868-141">Jeśli chcesz użyć nazwy określone dla klastra, który ma znaczenie, ustaw wartość `clusterName` zmiennej w pliku szablonu usługi Resource Manager (`ServiceFabricCluster.json`) do wybranej nazwy.</span><span class="sxs-lookup"><span data-stu-id="16868-141">If you want to use a specific name for your cluster, one that is meaningful to you, set the value of the `clusterName` variable in the Resource Manager template file (`ServiceFabricCluster.json`) to your chosen name.</span></span> <span data-ttu-id="16868-142">Jest to pierwsza zmienna zdefiniowana w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="16868-142">It is the first variable defined in that file.</span></span>

## <a name="optional-add-public-application-ports"></a><span data-ttu-id="16868-143">Opcjonalnie: Dodaj porty publiczny aplikacji</span><span class="sxs-lookup"><span data-stu-id="16868-143">Optional: add public application ports</span></span>
<span data-ttu-id="16868-144">Można również zmienić porty publiczny aplikacji dla klastra, przed rozpoczęciem wdrażania.</span><span class="sxs-lookup"><span data-stu-id="16868-144">You may also want to change the public application ports for the cluster before you deploy it.</span></span> <span data-ttu-id="16868-145">Domyślnie szablon otwiera publicznego tylko dwa porty TCP (80 i 8081).</span><span class="sxs-lookup"><span data-stu-id="16868-145">By default, the template opens up just two public TCP ports (80 and 8081).</span></span> <span data-ttu-id="16868-146">Jeśli potrzebujesz więcej aplikacji, należy zmodyfikować definicję modułu równoważenia obciążenia Azure w szablonie.</span><span class="sxs-lookup"><span data-stu-id="16868-146">If you need more for your applications, modify the Azure Load Balancer definition in the template.</span></span> <span data-ttu-id="16868-147">Definicja jest przechowywana w pliku szablonu głównego (`ServiceFabricCluster.json`).</span><span class="sxs-lookup"><span data-stu-id="16868-147">The definition is stored in the main template file (`ServiceFabricCluster.json`).</span></span> <span data-ttu-id="16868-148">Otwórz ten plik i wyszukaj `loadBalancedAppPort`.</span><span class="sxs-lookup"><span data-stu-id="16868-148">Open that file and search for `loadBalancedAppPort`.</span></span> <span data-ttu-id="16868-149">Każdy port jest skojarzona z trzech artefakty:</span><span class="sxs-lookup"><span data-stu-id="16868-149">Each port is associated with three artifacts:</span></span>

1. <span data-ttu-id="16868-150">Zmienna szablonu, który definiuje wartość port TCP dla portu:</span><span class="sxs-lookup"><span data-stu-id="16868-150">A template variable that defines the TCP port value for the port:</span></span>
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. <span data-ttu-id="16868-151">A *sondowania* określający, jak często i jak długo Azure obciążenia modułu równoważenia próbuje użyć określonego węzła sieci szkieletowej usług przed awarii na inny.</span><span class="sxs-lookup"><span data-stu-id="16868-151">A *probe* that defines how frequently and for how long the Azure load balancer attempts to use a specific Service Fabric node before failing over to another one.</span></span> <span data-ttu-id="16868-152">Sondy są częścią zasobów usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="16868-152">The probes are part of the Load Balancer resource.</span></span> <span data-ttu-id="16868-153">Poniżej przedstawiono definicję sondowania pierwszy domyślny port aplikacji:</span><span class="sxs-lookup"><span data-stu-id="16868-153">Here is the probe definition for the first default application port:</span></span>
   
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
3. <span data-ttu-id="16868-154">A *reguły równoważenia obciążenia* który wiąże ze sobą, port i badania, które umożliwia funkcji równoważenia obciążenia w zestawie węzłów klastra sieci szkieletowej usług:</span><span class="sxs-lookup"><span data-stu-id="16868-154">A *load-balancing rule* that ties together the port and the probe, which enables load balancing across a set of Service Fabric cluster nodes:</span></span>
   
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
   <span data-ttu-id="16868-155">Jeśli aplikacje, które planujesz wdrożyć w klastrze muszą więcej portów, należy dodać je tworzenia dodatkowych badania i definicji reguł równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="16868-155">If the applications that you plan to deploy to the cluster need more ports, you can add them by creating additional probe and load-balancing rule definitions.</span></span> <span data-ttu-id="16868-156">Aby uzyskać więcej informacji na temat pracy z usługą równoważenia obciążenia w Azure za pośrednictwem Menedżera zasobów szablonów, zobacz [rozpoczęcia tworzenia wewnętrznego modułu równoważenia obciążenia przy użyciu szablonu](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="16868-156">For more information on how to work with Azure Load Balancer through Resource Manager templates, see [Get started creating an internal load balancer using a template](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span></span>

## <a name="deploy-the-template-by-using-visual-studio"></a><span data-ttu-id="16868-157">Wdrażanie szablonu przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="16868-157">Deploy the template by using Visual Studio</span></span>
<span data-ttu-id="16868-158">Po zapisaniu wszystkich wartości wymaganego parametru w`ServiceFabricCluster.param.dev.json` pliku, możesz przystąpić do wdrażania szablonu i tworzenia klastra usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="16868-158">After you have saved all the required parameter values in the`ServiceFabricCluster.param.dev.json` file, you are ready to deploy the template and create your Service Fabric cluster.</span></span> <span data-ttu-id="16868-159">Kliknij prawym przyciskiem myszy projekt grupy zasobów w Eksploratorze rozwiązań w usłudze Visual Studio i wybierz polecenie **Wdróż | Nowe wdrożenie...** .</span><span class="sxs-lookup"><span data-stu-id="16868-159">Right-click the resource group project in Visual Studio Solution Explorer and choose **Deploy | New Deployment...**.</span></span> <span data-ttu-id="16868-160">Jeśli to konieczne, Visual Studio będzie **wdrażanie w grupie zasobów** okno dialogowe, monitem o uwierzytelniać na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="16868-160">If necessary, Visual Studio will show the **Deploy to Resource Group** dialog box, asking you to authenticate to Azure:</span></span>

![Wdrażanie w oknie dialogowym grupy zasobów][3]

<span data-ttu-id="16868-162">Okno dialogowe pozwala wybrać istniejącą grupę zasobów Menedżera zasobów dla klastra oraz udostępnia opcję, aby utworzyć nowy.</span><span class="sxs-lookup"><span data-stu-id="16868-162">The dialog box lets you choose an existing Resource Manager resource group for the cluster and gives you the option to create a new one.</span></span> <span data-ttu-id="16868-163">Zwykle warto użyć oddzielnej grupie zasobów klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="16868-163">It normally makes sense to use a separate resource group for a Service Fabric cluster.</span></span>

<span data-ttu-id="16868-164">Po naciśnięciu przycisku Wdróż Visual Studio spowoduje wyświetlenie monitu o potwierdzenie wartości parametrów szablonu.</span><span class="sxs-lookup"><span data-stu-id="16868-164">After you hit the Deploy button, Visual Studio will prompt you to confirm the template parameter values.</span></span> <span data-ttu-id="16868-165">Trafienia **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="16868-165">Hit the **Save** button.</span></span> <span data-ttu-id="16868-166">Jeden parametr ma wartość utrwalonego: hasło konta administratora klastra.</span><span class="sxs-lookup"><span data-stu-id="16868-166">One parameter does not have a persisted value: the administrative account password for the cluster.</span></span> <span data-ttu-id="16868-167">Należy podać wartość hasła, gdy program Visual Studio monituje o jeden.</span><span class="sxs-lookup"><span data-stu-id="16868-167">You need to provide a password value when Visual Studio prompts you for one.</span></span>

> [!NOTE]
> <span data-ttu-id="16868-168">Począwszy od zestaw Azure SDK 2.9, program Visual Studio obsługuje hasła odczytu z **usługi Azure Key Vault** podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="16868-168">Starting with Azure SDK 2.9, Visual Studio supports reading passwords from **Azure Key Vault** during deployment.</span></span> <span data-ttu-id="16868-169">W oknie dialogowym Parametry szablonu należy zauważyć, że `adminPassword` pole tekstowe parametr ma mało ikonę "klucz" po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="16868-169">In the template parameters dialog notice that the `adminPassword` parameter text box has a little "key" icon on the right.</span></span> <span data-ttu-id="16868-170">Ta ikona służy do wybierania istniejącym kluczem tajnym magazynu kluczy jako hasło administratora dla klastra.</span><span class="sxs-lookup"><span data-stu-id="16868-170">This icon allows you to select an existing key vault secret as the administrative password for the cluster.</span></span> <span data-ttu-id="16868-171">Po prostu upewnij się, że pierwszy Włącz dostęp do usługi Azure Resource Manager do wdrażania szablonu w zasadach dostępu Advanced magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="16868-171">Just make sure to first enable Azure Resource Manager access for template deployment in the Advanced Access Policies of your key vault.</span></span> 
> 
> 

<span data-ttu-id="16868-172">Możesz monitorować postęp procesu wdrażania w oknie danych wyjściowych programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="16868-172">You can monitor the progress of the deployment process in the Visual Studio output window.</span></span> <span data-ttu-id="16868-173">Po zakończeniu wdrażania szablonu nowego klastra jest gotowe do użycia!</span><span class="sxs-lookup"><span data-stu-id="16868-173">Once the template deployment is completed, your new cluster is ready to use!</span></span>

> [!NOTE]
> <span data-ttu-id="16868-174">Nigdy nie użyto programu PowerShell do administrowania Azure z komputera, którego obecnie używasz, należy wykonać nieco celów.</span><span class="sxs-lookup"><span data-stu-id="16868-174">If PowerShell was never used to administer Azure from the machine that you are using now, you need to do a little housekeeping.</span></span>
> 
> 1. <span data-ttu-id="16868-175">Włączyć, uruchamiając skrypty programu PowerShell [ `Set-ExecutionPolicy` ](https://technet.microsoft.com/library/hh849812.aspx) polecenia.</span><span class="sxs-lookup"><span data-stu-id="16868-175">Enable PowerShell scripting by running the [`Set-ExecutionPolicy`](https://technet.microsoft.com/library/hh849812.aspx) command.</span></span> <span data-ttu-id="16868-176">Programowanie maszyn "nieograniczony" zasady są zazwyczaj zaakceptować.</span><span class="sxs-lookup"><span data-stu-id="16868-176">For development machines, "unrestricted" policy is usually acceptable.</span></span>
> 2. <span data-ttu-id="16868-177">Zdecyduj, czy zezwolić na zbieranie danych diagnostycznych z poleceniami środowiska Azure PowerShell i uruchom [ `Enable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619303.aspx) lub [ `Disable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619236.aspx) odpowiednio do potrzeb.</span><span class="sxs-lookup"><span data-stu-id="16868-177">Decide whether to allow diagnostic data collection from Azure PowerShell commands, and run [`Enable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619303.aspx) or [`Disable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619236.aspx) as necessary.</span></span> <span data-ttu-id="16868-178">Pozwoli to uniknąć niepotrzebnych monity podczas wdrażania szablonu.</span><span class="sxs-lookup"><span data-stu-id="16868-178">This will avoid unnecessary prompts during template deployment.</span></span>
> 
> 

<span data-ttu-id="16868-179">Jeśli wystąpią jakieś błędy, przejdź do [portalu Azure](https://portal.azure.com/) , a następnie otwórz wdrożone do grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="16868-179">If there are any errors, go to the [Azure portal](https://portal.azure.com/) and open the resource group that you deployed to.</span></span> <span data-ttu-id="16868-180">Kliknij przycisk **wszystkie ustawienia**, następnie kliknij przycisk **wdrożeń** w bloku ustawień.</span><span class="sxs-lookup"><span data-stu-id="16868-180">Click **All settings**, then click **Deployments** on the settings blade.</span></span> <span data-ttu-id="16868-181">Niepowodzenie wdrożenia grupy zasobów pozostawia szczegółowe informacje diagnostyczne.</span><span class="sxs-lookup"><span data-stu-id="16868-181">A failed resource-group deployment leaves detailed diagnostic information there.</span></span>

> [!NOTE]
> <span data-ttu-id="16868-182">Klastry usługi sieć szkieletowa usług wymagają określonej liczby węzłów pozwala uzyskać się zachować dostępność i zachować stan — nazywany "utrzymywania kworum".</span><span class="sxs-lookup"><span data-stu-id="16868-182">Service Fabric clusters require a certain number of nodes to be up to maintain availability and preserve state - referred to as "maintaining quorum."</span></span> <span data-ttu-id="16868-183">W związku z tym nie jest bezpieczne zamknięcie wszystkich komputerów w klastrze, chyba że najpierw wykonali [pełnej kopii zapasowej według stanu](service-fabric-reliable-services-backup-restore.md).</span><span class="sxs-lookup"><span data-stu-id="16868-183">Therefore, it is not safe to shut down all of the machines in the cluster unless you have first performed a [full backup of your state](service-fabric-reliable-services-backup-restore.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="16868-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="16868-184">Next steps</span></span>
* [<span data-ttu-id="16868-185">Więcej informacji na temat konfigurowania klastra sieci szkieletowej usług za pomocą portalu Azure</span><span class="sxs-lookup"><span data-stu-id="16868-185">Learn about setting up Service Fabric cluster using the Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="16868-186">Informacje o sposobie zarządzania i wdrażania aplikacji sieci szkieletowej usług za pomocą programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="16868-186">Learn how to manage and deploy Service Fabric applications using Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
