---
title: "debugowanie zdalne z ciągłego dostarczania aaaEnable | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooenable zdalne debugowanie przy użyciu tooAzure toodeploy ciągłego dostarczania"
services: cloud-services
documentationcenter: .net
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d423639-3b2f-4ca5-ac5a-9ac19a217c29
ms.service: cloud-services
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: d9d9d1cfe5304c9526586a9164f172746a448e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-debugging-when-using-continuous-delivery-toopublish-tooazure"></a><span data-ttu-id="7ef0f-103">Włączanie debugowania zdalnego, korzystając z tooAzure toopublish ciągłego dostarczania</span><span class="sxs-lookup"><span data-stu-id="7ef0f-103">Enable remote debugging when using continuous delivery toopublish tooAzure</span></span>
<span data-ttu-id="7ef0f-104">Można włączyć debugowanie zdalne na platformie Azure dla usługi w chmurze lub maszyn wirtualnych, gdy używasz [ciągłego dostarczania](cloud-services-dotnet-continuous-delivery.md) tooAzure toopublish, wykonując następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="7ef0f-104">You can enable remote debugging in Azure, for cloud services or virtual machines, when you use [continuous delivery](cloud-services-dotnet-continuous-delivery.md) toopublish tooAzure by following these steps.</span></span>

## <a name="enabling-remote-debugging-for-cloud-services"></a><span data-ttu-id="7ef0f-105">Włączanie debugowania zdalnego dla usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="7ef0f-105">Enabling remote debugging for cloud services</span></span>
1. <span data-ttu-id="7ef0f-106">Na powitania agenta kompilacji, konfigurowanie hello początkowej środowiska platformy Azure zgodnie z opisem w [kompilacji wiersza polecenia platformy Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span><span class="sxs-lookup"><span data-stu-id="7ef0f-106">On hello build agent, set up hello initial environment for Azure as outlined in [Command-Line Build for Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span></span>
2. <span data-ttu-id="7ef0f-107">Ponieważ środowiska uruchomieniowego debugowania zdalnego hello (msvsmon.exe) jest wymagany dla pakietu hello, zainstaluj program hello **Remote Tools for Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="7ef0f-107">Because hello remote debug runtime (msvsmon.exe) is required for hello package, install hello **Remote Tools for Visual Studio**.</span></span>

    * [<span data-ttu-id="7ef0f-108">Remote Tools for Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="7ef0f-108">Remote Tools for Visual Studio 2017</span></span>](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [<span data-ttu-id="7ef0f-109">Remote Tools for Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="7ef0f-109">Remote Tools for Visual Studio 2015</span></span>](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [<span data-ttu-id="7ef0f-110">Remote Tools for Visual Studio 2013 z aktualizacją 5</span><span class="sxs-lookup"><span data-stu-id="7ef0f-110">Remote Tools for Visual Studio 2013 Update 5</span></span>](https://www.microsoft.com/download/details.aspx?id=48156)
    
    <span data-ttu-id="7ef0f-111">Alternatywnie można kopiować pliki binarne debugowania zdalnego hello z systemu, które mają zainstalowanego programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7ef0f-111">As an alternative, you can copy hello remote debug binaries from a system that has Visual Studio installed.</span></span>

3. <span data-ttu-id="7ef0f-112">Utwórz certyfikat zgodnie z opisem w [Omówienie certyfikatów dla usług w chmurze Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="7ef0f-112">Create a certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="7ef0f-113">Zachowaj hello PFX i odcisk palca certyfikatu protokołu RDP i przekaż usługi docelowej toohello hello certyfikatu w chmurze.</span><span class="sxs-lookup"><span data-stu-id="7ef0f-113">Keep hello .pfx and RDP certificate thumbprint and upload hello certificate toohello target cloud service.</span></span>
4. <span data-ttu-id="7ef0f-114">Użyj hello następujące opcje w toobuild wiersza polecenia programu MSBuild hello i pakietu z włączoną debugowania zdalnego.</span><span class="sxs-lookup"><span data-stu-id="7ef0f-114">Use hello following options in hello MSBuild command line toobuild and package with remote debug enabled.</span></span> <span data-ttu-id="7ef0f-115">(Zastąp rzeczywiste ścieżki tooyour system i pliki projektu dla elementów oddzielona kąt hello).</span><span class="sxs-lookup"><span data-stu-id="7ef0f-115">(Substitute actual paths tooyour system and project files for hello angle-bracketed items.)</span></span>
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of hello certificate added toohello cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path tooyour VS solution file>"
   
    <span data-ttu-id="7ef0f-116">`VSX64RemoteDebuggerPath`jest hello ścieżki toohello folder zawierający msvsmon.exe w hello Remote Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7ef0f-116">`VSX64RemoteDebuggerPath` is hello path toohello folder containing msvsmon.exe in hello Remote Tools for Visual Studio.</span></span>
    <span data-ttu-id="7ef0f-117">`RemoteDebuggerConnectorVersion`jest hello wersja zestawu SDK platformy Azure w usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="7ef0f-117">`RemoteDebuggerConnectorVersion` is hello Azure SDK version in your cloud service.</span></span> <span data-ttu-id="7ef0f-118">Powinna być również zgodna wersja hello zainstalowane z programem Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7ef0f-118">It should also match hello version installed with Visual Studio.</span></span>
5. <span data-ttu-id="7ef0f-119">Publikowanie usługi w chmurze docelowej toohello przy użyciu pliku pakietu i .cscfg hello wygenerowanych w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="7ef0f-119">Publish toohello target cloud service by using hello package and .cscfg file generated in hello previous step.</span></span>
6. <span data-ttu-id="7ef0f-120">Importuj hello maszyny toohello certyfikatu (pfx), która ma Visual Studio z zestawem Azure SDK dla platformy .NET zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="7ef0f-120">Import hello certificate (.pfx file) toohello machine that has Visual Studio with Azure SDK for .NET installed.</span></span> <span data-ttu-id="7ef0f-121">Upewnij się, że toohello tooimport `CurrentUser\My` magazynu certyfikatów, w przeciwnym razie dołączenia toohello debugera programu Visual Studio zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="7ef0f-121">Make sure tooimport toohello `CurrentUser\My` certificate store, otherwise attaching toohello debugger in Visual Studio will fail.</span></span>

## <a name="enabling-remote-debugging-for-virtual-machines"></a><span data-ttu-id="7ef0f-122">Włączanie zdalnego debugowania dla maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="7ef0f-122">Enabling remote debugging for virtual machines</span></span>
1. <span data-ttu-id="7ef0f-123">Utwórz maszynę wirtualną platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7ef0f-123">Create an Azure virtual machine.</span></span> <span data-ttu-id="7ef0f-124">Zobacz [Utwórz maszynę wirtualną z systemem Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) lub [tworzenie i zarządzanie nimi maszyn wirtualnych platformy Azure w programie Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7ef0f-124">See [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [Create and Manage Azure Virtual Machines in Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
2. <span data-ttu-id="7ef0f-125">Na powitania [Azure strony portalu klasycznego](http://go.microsoft.com/fwlink/p/?LinkID=269851), Wyświetl maszyny wirtualnej hello pulpitu nawigacyjnego toosee hello maszyny wirtualnej **odcisk PALCA certyfikatu protokołu RDP**.</span><span class="sxs-lookup"><span data-stu-id="7ef0f-125">On hello [Azure classic portal page](http://go.microsoft.com/fwlink/p/?LinkID=269851), view hello virtual machine's dashboard toosee hello virtual machine’s **RDP CERTIFICATE THUMBPRINT**.</span></span> <span data-ttu-id="7ef0f-126">Ta wartość jest używana dla hello `ServerThumbprint` wartości w konfiguracji rozszerzenia hello.</span><span class="sxs-lookup"><span data-stu-id="7ef0f-126">This value is used for hello `ServerThumbprint` value in hello extension configuration.</span></span>
3. <span data-ttu-id="7ef0f-127">Utwórz certyfikat klienta w sposób opisany w [Omówienie certyfikatów dla usług w chmurze Azure](cloud-services-certs-create.md) (Zachowaj hello PFX i odcisk palca certyfikatu protokołu RDP).</span><span class="sxs-lookup"><span data-stu-id="7ef0f-127">Create a client certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md) (keep hello .pfx and RDP certificate thumbprint).</span></span>
4. <span data-ttu-id="7ef0f-128">Instalowanie programu Azure Powershell (wersja 0.7.4 lub nowszym) w sposób opisany w [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7ef0f-128">Install Azure Powershell (version 0.7.4 or later) as outlined in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
5. <span data-ttu-id="7ef0f-129">Uruchom hello następujące rozszerzenie RemoteDebug hello tooenable skryptu.</span><span class="sxs-lookup"><span data-stu-id="7ef0f-129">Run hello following script tooenable hello RemoteDebug extension.</span></span> <span data-ttu-id="7ef0f-130">Zamień ścieżki hello i danych osobistych własny, takie jak nazwa subskrypcji, nazwę usługi i odcisk palca.</span><span class="sxs-lookup"><span data-stu-id="7ef0f-130">Replace hello paths and personal data with your own, such as your subscription name, service name, and thumbprint.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7ef0f-131">Ten skrypt jest skonfigurowany dla programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="7ef0f-131">This script is configured for Visual Studio 2015.</span></span> <span data-ttu-id="7ef0f-132">Jeśli używasz programu Visual Studio 2013 lub Visual Studio 2017, zmodyfikuj hello `$referenceName` i `$extensionName` poniższe przydziały zbyt`RemoteDebugVS2013` lub `RemoteDebugVS2017`.</span><span class="sxs-lookup"><span data-stu-id="7ef0f-132">If you’re using Visual Studio 2013 or Visual Studio 2017, modify hello `$referenceName` and `$extensionName` assignments below too`RemoteDebugVS2013` or `RemoteDebugVS2017`.</span></span>

    ```powershell   
    Add-AzureAccount

    Select-AzureSubscription "My Microsoft Subscription"

    $vm = Get-AzureVM -ServiceName "mytestvm1" -Name "mytestvm1"

    $endpoints = @(
                    ,@{Name="RDConnVS2013"; PublicPort=30400; PrivatePort=30398}
                    ,@{Name="RDFwdrVS2013"; PublicPort=31400; PrivatePort=31398}
                )

    foreach($endpoint in $endpoints)
    {
        Add-AzureEndpoint -VM $vm -Name $endpoint.Name -Protocol tcp -PublicPort $endpoint.PublicPort -LocalPort $endpoint.PrivatePort
    }

    $referenceName = "Microsoft.VisualStudio.WindowsAzure.RemoteDebug.RemoteDebugVS2015"
    $publisher = "Microsoft.VisualStudio.WindowsAzure.RemoteDebug"
    $extensionName = "RemoteDebugVS2015"
    $version = "1.*"
    $publicConfiguration = "<PublicConfig><Connector.Enabled>true</Connector.Enabled><ClientThumbprint>56D7D1B25B472268E332F7FC0C87286458BFB6B2</ClientThumbprint><ServerThumbprint>E7DCB00CB916C468CC3228261D6E4EE45C8ED3C6</ServerThumbprint><ConnectorPort>30398</ConnectorPort><ForwarderPort>31398</ForwarderPort></PublicConfig>"

    $vm | Set-AzureVMExtension -ReferenceName $referenceName -Publisher $publisher -ExtensionName $extensionName -Version $version -PublicConfiguration $publicConfiguration

    foreach($extension in $vm.VM.ResourceExtensionReferences)
    {
        if(($extension.ReferenceName -eq $referenceName) `
        -and ($extension.Publisher -eq $publisher) `
        -and ($extension.Name -eq $extensionName) `
        -and ($extension.Version -eq $version))
        {
            $extension.ResourceExtensionParameterValues[0].Key = 'config.txt'
            break
        }
    }

    $vm | Update-AzureVM
    ```

6. <span data-ttu-id="7ef0f-133">Importuj hello maszyny toohello certyfikatu (pfx), która ma Visual Studio z zestawem Azure SDK dla platformy .NET zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="7ef0f-133">Import hello certificate (.pfx) toohello machine that has Visual Studio with Azure SDK for .NET installed.</span></span>

