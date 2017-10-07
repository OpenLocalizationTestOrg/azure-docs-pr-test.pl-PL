---
title: aaaCreate autonomiczny klastra z systemem Windows maszynach wirtualnych platformy Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate i zarządzanie nimi klastra usługi sieć szkieletowa usług Azure na maszynach wirtualnych Azure systemem Windows Server."
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
ms.openlocfilehash: 8900204fe69887a7a0ca54b06e0d32534421bcfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a><span data-ttu-id="3f23c-103">Tworzenie klastra sieci szkieletowej usług autonomiczny trzech węzłów z systemem Windows Server maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3f23c-103">Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server</span></span>
<span data-ttu-id="3f23c-104">W tym artykule opisano, jak toocreate a klastra na opartych na systemie Windows Azure maszynach wirtualnych (VM), za pomocą hello autonomicznego Instalatora usługi sieć szkieletowa usług dla systemu Windows Server.</span><span class="sxs-lookup"><span data-stu-id="3f23c-104">This article describes how toocreate a cluster on Windows-based Azure virtual machines (VMs), using hello standalone Service Fabric installer for Windows Server.</span></span> <span data-ttu-id="3f23c-105">Scenariusz Hello jest specjalny przypadek [tworzenie i Zarządzanie klastrem w systemie Windows Server](service-fabric-cluster-creation-for-windows-server.md) gdzie hello maszyny wirtualne są [maszynach wirtualnych platformy Azure, systemem operacyjnym Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), ale nie są tworzone [platformy Azure oparte na chmurze klaster sieci szkieletowej usług](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3f23c-105">hello scenario is a special case of [Create and manage a cluster running on Windows Server](service-fabric-cluster-creation-for-windows-server.md) where hello VMs are [Azure VMs running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), however you are not creating [an Azure cloud-based Service Fabric cluster](service-fabric-cluster-creation-via-portal.md).</span></span> <span data-ttu-id="3f23c-106">rozróżnienie Hello w poniższych ten wzorzec jest hello klastra sieci szkieletowej usług autonomiczny utworzony przez hello następujące kroki całkowicie jest zarządzane przez użytkownika, powitalne Azure opartej na chmurze usługi sieć szkieletowa klastry są zarządzane i uaktualniane przez hello sieci szkieletowej usług dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="3f23c-106">hello distinction in following this pattern is that hello standalone Service Fabric cluster created by hello following steps is entirely managed by you, whereas hello Azure cloud-based Service Fabric clusters are managed and upgraded by hello Service Fabric resource provider.</span></span>

## <a name="steps-toocreate-hello-standalone-cluster"></a><span data-ttu-id="3f23c-107">Kroki toocreate hello autonomiczny klastra</span><span class="sxs-lookup"><span data-stu-id="3f23c-107">Steps toocreate hello standalone cluster</span></span>
1. <span data-ttu-id="3f23c-108">Zaloguj się toohello portalu Azure i utworzyć nowe systemu Windows Server 2012 R2 Datacenter lub maszyny Wirtualnej systemu Windows Server 2016 centrum danych w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="3f23c-108">Sign in toohello Azure portal and create a new Windows Server 2012 R2 Datacenter or Windows Server 2016 Datacenter VM in a resource group.</span></span> <span data-ttu-id="3f23c-109">Przeczytaj artykuł hello [utworzyć Maszynę wirtualną systemu Windows w portalu Azure hello](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="3f23c-109">Read hello article [Create a Windows VM in hello Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more details.</span></span>
2. <span data-ttu-id="3f23c-110">Dodaj kilka więcej toohello maszyn wirtualnych tej samej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="3f23c-110">Add a couple more VMs toohello same resource group.</span></span> <span data-ttu-id="3f23c-111">Upewnij się, że każdy hello maszyn wirtualnych ma hello tej samej nazwy użytkownika administratora i hasła podczas tworzenia.</span><span class="sxs-lookup"><span data-stu-id="3f23c-111">Ensure that each of hello VMs has hello same administrator user name and password when created.</span></span> <span data-ttu-id="3f23c-112">Po utworzeniu powinny być widoczne wszystkie trzy maszyny wirtualne w hello tej samej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3f23c-112">Once created you should see all three VMs in hello same virtual network.</span></span>
3. <span data-ttu-id="3f23c-113">Połącz tooeach hello maszyn wirtualnych i wyłączyć hello zapory systemu Windows przy użyciu hello [Menedżera serwera, pulpitu nawigacyjnego serwera lokalnego](https://technet.microsoft.com/library/jj134147.aspx).</span><span class="sxs-lookup"><span data-stu-id="3f23c-113">Connect tooeach of hello VMs and turn off hello Windows Firewall using hello [Server Manager, Local Server dashboard](https://technet.microsoft.com/library/jj134147.aspx).</span></span> <span data-ttu-id="3f23c-114">Dzięki temu, że ruch sieciowy hello może komunikować się między maszynami hello.</span><span class="sxs-lookup"><span data-stu-id="3f23c-114">This ensures that hello network traffic can communicate between hello machines.</span></span> <span data-ttu-id="3f23c-115">Podczas tooeach podłączonego komputera, należy uzyskać adres IP hello, otwórz wiersz polecenia i wpisując `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="3f23c-115">While connected tooeach machine, get hello IP address by opening a command prompt and typing `ipconfig`.</span></span> <span data-ttu-id="3f23c-116">Można również widać hello IP adres każdej maszyny w portalu hello, wybierając hello zasobów sieci wirtualnej dla grupy zasobów hello i sprawdzanie interfejsów sieciowych hello tworzony dla każdego z tych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="3f23c-116">Alternatively you can see hello IP address of each machine on hello portal, by selecting hello virtual network resource for hello resource group and checking hello network interfaces created for each of these machines.</span></span>
4. <span data-ttu-id="3f23c-117">Połącz tooone hello maszyn wirtualnych i test, który może wysyłać polecenia ping hello pomyślnie innych dwóch maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="3f23c-117">Connect tooone of hello VMs and test that you can ping hello other two VMs successfully.</span></span>
5. <span data-ttu-id="3f23c-118">Połącz tooone hello maszyn wirtualnych i [Pobierz hello autonomicznej usługi sieć szkieletowa usług dla systemu Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) do nowego folderu na powitania komputera i wyodrębniać hello pakietu.</span><span class="sxs-lookup"><span data-stu-id="3f23c-118">Connect tooone of hello VMs and [download hello standalone Service Fabric package for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) into a new folder on hello machine and extract hello package.</span></span>
6. <span data-ttu-id="3f23c-119">Otwórz hello *ClusterConfig.Unsecure.MultiMachine.json* pliku w Notatniku i edytować każdy węzeł z adresami IP hello trzech hello maszyn.</span><span class="sxs-lookup"><span data-stu-id="3f23c-119">Open hello *ClusterConfig.Unsecure.MultiMachine.json* file in Notepad and edit each node with hello three IP addresses of hello machines.</span></span> <span data-ttu-id="3f23c-120">Zmień nazwę klastra hello u góry hello i Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="3f23c-120">Change hello cluster name at hello top and save hello file.</span></span>  <span data-ttu-id="3f23c-121">Poniżej przedstawiono częściowe przykład hello manifestu klastra.</span><span class="sxs-lookup"><span data-stu-id="3f23c-121">A partial example of hello cluster manifest is shown below.</span></span>
   
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
7. <span data-ttu-id="3f23c-122">Jeśli planujesz tego toobe bezpiecznego klastra, zdecyduj, zabezpieczenie hello chcesz toouse i wykonaj czynności hello hello skojarzone łącze: [certyfikatu X509](service-fabric-windows-cluster-x509-security.md) lub [zabezpieczenia systemu Windows](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="3f23c-122">If you intend this toobe a secure cluster, decide hello security measure you would like toouse and follow hello steps at hello associated link: [X509 Certificate](service-fabric-windows-cluster-x509-security.md) or [Windows Security](service-fabric-windows-cluster-windows-security.md).</span></span> <span data-ttu-id="3f23c-123">Konfigurowanie klastra hello przy użyciu zabezpieczeń systemu Windows, należy tooset się toomanage kontrolera domeny usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3f23c-123">If setting up hello cluster using Windows Security, you will need tooset up a domain controller toomanage Active Directory.</span></span> <span data-ttu-id="3f23c-124">Należy pamiętać, że używanie maszyny kontrolera domeny jako usługi sieć szkieletowa węzeł nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="3f23c-124">Note that using a domain controller machine as a Service Fabric node is not supported.</span></span>
8. <span data-ttu-id="3f23c-125">Otwórz [okno programu PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span><span class="sxs-lookup"><span data-stu-id="3f23c-125">Open a [PowerShell ISE window](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span></span> <span data-ttu-id="3f23c-126">Przejdź toohello folder, w którym wyodrębnić pakiet instalatora autonomicznego pobrany hello i zapisania pliku konfiguracji klastra hello.</span><span class="sxs-lookup"><span data-stu-id="3f23c-126">Navigate toohello folder where you extracted hello downloaded standalone installer package and saved hello cluster configuration file.</span></span> <span data-ttu-id="3f23c-127">Uruchom powitania po klastra hello toodeploy polecenia programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3f23c-127">Run hello following PowerShell command toodeploy hello cluster:</span></span>
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

<span data-ttu-id="3f23c-128">skrypt Hello zdalnie konfiguruje klaster sieci szkieletowej usług hello i zgłoś postęp wdrażania przedstawia za pośrednictwem.</span><span class="sxs-lookup"><span data-stu-id="3f23c-128">hello script will remotely configure hello Service Fabric cluster and should report progress as deployment rolls through.</span></span>

9. <span data-ttu-id="3f23c-129">Po około minutę, możesz sprawdzić, jeśli klaster hello działa łącząc toohello Service Fabric Explorer przy użyciu jednego adresu IP komputera hello dotyczy, na przykład za pomocą `http://10.1.0.5:19080/Explorer/index.html`.</span><span class="sxs-lookup"><span data-stu-id="3f23c-129">After about a minute, you can check if hello cluster is operational by connecting toohello Service Fabric Explorer using one of hello machine's IP addresses, for example by using `http://10.1.0.5:19080/Explorer/index.html`.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3f23c-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3f23c-130">Next steps</span></span>
* [<span data-ttu-id="3f23c-131">Tworzenie autonomicznych klastrów usługi Service Fabric w systemie Windows Server lub Linux</span><span class="sxs-lookup"><span data-stu-id="3f23c-131">Create standalone Service Fabric clusters on Windows Server or Linux</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="3f23c-132">Dodawanie lub usuwanie klastra sieci szkieletowej usług autonomiczny tooa węzłów</span><span class="sxs-lookup"><span data-stu-id="3f23c-132">Add or remove nodes tooa standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="3f23c-133">Ustawienia konfiguracji dla autonomicznych klastra systemu Windows</span><span class="sxs-lookup"><span data-stu-id="3f23c-133">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="3f23c-134">Zabezpieczanie klastra autonomicznego w systemie Windows przy użyciu zabezpieczeń systemu Windows</span><span class="sxs-lookup"><span data-stu-id="3f23c-134">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="3f23c-135">Secure autonomiczny klastra w systemie Windows przy użyciu X509 certyfikatów</span><span class="sxs-lookup"><span data-stu-id="3f23c-135">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

