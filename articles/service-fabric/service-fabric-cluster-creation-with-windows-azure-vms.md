---
title: Tworzenie klastra autonomiczny z systemem Windows maszynach wirtualnych platformy Azure | Dokumentacja firmy Microsoft
description: "Informacje o sposobie tworzenia i zarządzania nimi klastra usługi sieć szkieletowa usług Azure na maszynach wirtualnych Azure systemem Windows Server."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 7eeb40d2-fb22-4a77-80ca-f1b46b22edbc
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: ryanwi;chackdan
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: f8a0305a22c00f9bdbdb1bdb06dc299cccee23dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a><span data-ttu-id="3cd46-103">Tworzenie klastra sieci szkieletowej usług autonomiczny trzech węzłów z systemem Windows Server maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3cd46-103">Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server</span></span>
<span data-ttu-id="3cd46-104">W tym artykule opisano sposób tworzenia klastra w przypadku komputerów z systemem Windows Azure maszyn wirtualnych (VM), za pomocą autonomicznego Instalatora usługi sieć szkieletowa usług dla systemu Windows Server.</span><span class="sxs-lookup"><span data-stu-id="3cd46-104">This article describes how to create a cluster on Windows-based Azure virtual machines (VMs), using the standalone Service Fabric installer for Windows Server.</span></span> <span data-ttu-id="3cd46-105">Scenariusz jest specjalny przypadek [tworzenie i Zarządzanie klastrem w systemie Windows Server](service-fabric-cluster-creation-for-windows-server.md) skutkującej maszyn wirtualnych [maszynach wirtualnych platformy Azure, systemem operacyjnym Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), ale nie są tworzone [platformy Azure oparte na chmurze klaster sieci szkieletowej usług](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3cd46-105">The scenario is a special case of [Create and manage a cluster running on Windows Server](service-fabric-cluster-creation-for-windows-server.md) where the VMs are [Azure VMs running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), however you are not creating [an Azure cloud-based Service Fabric cluster](service-fabric-cluster-creation-via-portal.md).</span></span> <span data-ttu-id="3cd46-106">Różnica w poniższych ten wzorzec jest czy klastra sieci szkieletowej usług autonomiczny utworzony przez następujące kroki całkowicie jest zarządzana przez użytkownika, Azure opartej na chmurze klastrów sieci szkieletowej usług są zarządzane i uaktualniane przez zasobów sieci szkieletowej usług Dostawca.</span><span class="sxs-lookup"><span data-stu-id="3cd46-106">The distinction in following this pattern is that the standalone Service Fabric cluster created by the following steps is entirely managed by you, whereas the Azure cloud-based Service Fabric clusters are managed and upgraded by the Service Fabric resource provider.</span></span>

## <a name="steps-to-create-the-standalone-cluster"></a><span data-ttu-id="3cd46-107">Kroki umożliwiające utworzenie klastra autonomiczny</span><span class="sxs-lookup"><span data-stu-id="3cd46-107">Steps to create the standalone cluster</span></span>
1. <span data-ttu-id="3cd46-108">Zaloguj się do portalu Azure i utworzyć nowe systemu Windows Server 2012 R2 Datacenter lub maszyny Wirtualnej systemu Windows Server 2016 centrum danych w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="3cd46-108">Sign in to the Azure portal and create a new Windows Server 2012 R2 Datacenter or Windows Server 2016 Datacenter VM in a resource group.</span></span> <span data-ttu-id="3cd46-109">Przeczytaj artykuł na temat [utworzyć Maszynę wirtualną systemu Windows w portalu Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="3cd46-109">Read the article [Create a Windows VM in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more details.</span></span>
2. <span data-ttu-id="3cd46-110">Dodaj kilka więcej maszyn wirtualnych do tej samej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="3cd46-110">Add a couple more VMs to the same resource group.</span></span> <span data-ttu-id="3cd46-111">Sprawdź, czy poszczególnych maszyn wirtualnych ma taką samą nazwę użytkownika administratora i hasła podczas tworzenia.</span><span class="sxs-lookup"><span data-stu-id="3cd46-111">Ensure that each of the VMs has the same administrator user name and password when created.</span></span> <span data-ttu-id="3cd46-112">Po utworzeniu powinny być widoczne wszystkie trzy maszyny wirtualne w tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3cd46-112">Once created you should see all three VMs in the same virtual network.</span></span>
3. <span data-ttu-id="3cd46-113">Nawiązywanie połączenia wszystkich maszynach wirtualnych i wyłączyć za pomocą zapory systemu Windows [Menedżera serwera, pulpitu nawigacyjnego serwera lokalnego](https://technet.microsoft.com/library/jj134147.aspx).</span><span class="sxs-lookup"><span data-stu-id="3cd46-113">Connect to each of the VMs and turn off the Windows Firewall using the [Server Manager, Local Server dashboard](https://technet.microsoft.com/library/jj134147.aspx).</span></span> <span data-ttu-id="3cd46-114">Dzięki temu, że ruch sieciowy może komunikować się między komputerami.</span><span class="sxs-lookup"><span data-stu-id="3cd46-114">This ensures that the network traffic can communicate between the machines.</span></span> <span data-ttu-id="3cd46-115">Podczas połączenia z każdego komputera, należy uzyskać adres IP, należy otworzyć wiersz polecenia i wpisując `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="3cd46-115">While connected to each machine, get the IP address by opening a command prompt and typing `ipconfig`.</span></span> <span data-ttu-id="3cd46-116">Alternatywnie można wyświetlić adres IP każdego komputera na portalu, wybierając zasobów sieci wirtualnej dla grupy zasobów i sprawdzanie interfejsów sieciowych, tworzony dla każdego z tych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="3cd46-116">Alternatively you can see the IP address of each machine on the portal, by selecting the virtual network resource for the resource group and checking the network interfaces created for each of these machines.</span></span>
4. <span data-ttu-id="3cd46-117">Połącz do jednej z maszyn wirtualnych i przetestować, czy można pomyślnie ping innych dwóch maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="3cd46-117">Connect to one of the VMs and test that you can ping the other two VMs successfully.</span></span>
5. <span data-ttu-id="3cd46-118">Podłącz do jednego z maszyn wirtualnych i [Pobierz autonomicznych pakietu sieci szkieletowej usług dla systemu Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) do nowego folderu na komputerze i wyodrębniania pakietu.</span><span class="sxs-lookup"><span data-stu-id="3cd46-118">Connect to one of the VMs and [download the standalone Service Fabric package for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) into a new folder on the machine and extract the package.</span></span>
6. <span data-ttu-id="3cd46-119">Otwórz *ClusterConfig.Unsecure.MultiMachine.json* pliku w Notatniku i edytować każdy węzeł z trzech adresów IP maszyn.</span><span class="sxs-lookup"><span data-stu-id="3cd46-119">Open the *ClusterConfig.Unsecure.MultiMachine.json* file in Notepad and edit each node with the three IP addresses of the machines.</span></span> <span data-ttu-id="3cd46-120">Zmień nazwę klastra u góry i Zapisz plik.</span><span class="sxs-lookup"><span data-stu-id="3cd46-120">Change the cluster name at the top and save the file.</span></span>  <span data-ttu-id="3cd46-121">Poniżej przedstawiono częściowe przykład manifestu klastra.</span><span class="sxs-lookup"><span data-stu-id="3cd46-121">A partial example of the cluster manifest is shown below.</span></span>
   
    ```
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "01-2017",
        "nodes": [
        {
            "nodeName": "standalonenode0",
            "iPAddress": "10.1.0.4",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD0"
        },
        {
            "nodeName": "standalonenode1",
            "iPAddress": "10.1.0.5",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc2/r0",
            "upgradeDomain": "UD1"
        },
        {
            "nodeName": "standalonenode2",
            "iPAddress": "10.1.0.6",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc3/r0",
            "upgradeDomain": "UD2"
        }
        ],
    ```
7. <span data-ttu-id="3cd46-122">Zdecyduj, czy ma być bezpieczne klastra, zabezpieczenie chcesz i wykonaj kroki opisane w temacie skojarzone łącze: [certyfikatu X509](service-fabric-windows-cluster-x509-security.md) lub [zabezpieczenia systemu Windows](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="3cd46-122">If you intend this to be a secure cluster, decide the security measure you would like to use and follow the steps at the associated link: [X509 Certificate](service-fabric-windows-cluster-x509-security.md) or [Windows Security](service-fabric-windows-cluster-windows-security.md).</span></span> <span data-ttu-id="3cd46-123">Konfigurowanie klastra przy użyciu zabezpieczeń systemu Windows, należy skonfigurować kontroler domeny do zarządzania usługą Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3cd46-123">If setting up the cluster using Windows Security, you will need to set up a domain controller to manage Active Directory.</span></span> <span data-ttu-id="3cd46-124">Należy pamiętać, że używanie maszyny kontrolera domeny jako usługi sieć szkieletowa węzeł nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="3cd46-124">Note that using a domain controller machine as a Service Fabric node is not supported.</span></span>
8. <span data-ttu-id="3cd46-125">Otwórz [okno programu PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span><span class="sxs-lookup"><span data-stu-id="3cd46-125">Open a [PowerShell ISE window](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span></span> <span data-ttu-id="3cd46-126">Przejdź do folderu, w którym wyodrębniono pakiet pobrany Autonomiczny Instalator i zapisania pliku konfiguracji klastra.</span><span class="sxs-lookup"><span data-stu-id="3cd46-126">Navigate to the folder where you extracted the downloaded standalone installer package and saved the cluster configuration file.</span></span> <span data-ttu-id="3cd46-127">Uruchom następujące polecenie programu PowerShell, aby wdrożyć klaster:</span><span class="sxs-lookup"><span data-stu-id="3cd46-127">Run the following PowerShell command to deploy the cluster:</span></span>
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

<span data-ttu-id="3cd46-128">Skrypt zdalnie konfiguruje klaster sieci szkieletowej usług i zgłoś postęp wdrażania przedstawia za pośrednictwem.</span><span class="sxs-lookup"><span data-stu-id="3cd46-128">The script will remotely configure the Service Fabric cluster and should report progress as deployment rolls through.</span></span>

9. <span data-ttu-id="3cd46-129">Po około minutę, możesz sprawdzić, czy klaster działa przez nawiązanie połączenia za pomocą jednego z adresów IP na komputerze, na przykład za pomocą Eksploratora usługi sieć szkieletowa `http://10.1.0.5:19080/Explorer/index.html`.</span><span class="sxs-lookup"><span data-stu-id="3cd46-129">After about a minute, you can check if the cluster is operational by connecting to the Service Fabric Explorer using one of the machine's IP addresses, for example by using `http://10.1.0.5:19080/Explorer/index.html`.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3cd46-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3cd46-130">Next steps</span></span>
* [<span data-ttu-id="3cd46-131">Tworzenie autonomicznych klastrów usługi Service Fabric w systemie Windows Server lub Linux</span><span class="sxs-lookup"><span data-stu-id="3cd46-131">Create standalone Service Fabric clusters on Windows Server or Linux</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="3cd46-132">Dodaj lub usuń węzły do klastra usługi sieć szkieletowa autonomiczny</span><span class="sxs-lookup"><span data-stu-id="3cd46-132">Add or remove nodes to a standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="3cd46-133">Ustawienia konfiguracji dla autonomicznych klastra systemu Windows</span><span class="sxs-lookup"><span data-stu-id="3cd46-133">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="3cd46-134">Zabezpieczanie klastra autonomicznego w systemie Windows przy użyciu zabezpieczeń systemu Windows</span><span class="sxs-lookup"><span data-stu-id="3cd46-134">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="3cd46-135">Secure autonomiczny klastra w systemie Windows przy użyciu X509 certyfikatów</span><span class="sxs-lookup"><span data-stu-id="3cd46-135">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

