---
title: aaaSubmit tooan zadania HPC Pack klastra na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooset się na lokalnym komputerze toosubmit zadań klastra HPC Pack tooan na platformie Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 78f6833c-4aa6-4b3e-be71-97201abb4721
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 2918cf633917d8730487152e6a5ddb863eb8bb5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-tooan-hpc-pack-cluster-deployed-in-azure"></a><span data-ttu-id="989e3-103">Przesyłanie zadań HPC z komputera lokalnego tooan klastra HPC Pack wdrożona na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="989e3-103">Submit HPC jobs from an on-premises computer tooan HPC Pack cluster deployed in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="989e3-104">Konfigurowanie lokalnego klienta komputera toosubmit zadania tooa [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) klastra na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="989e3-104">Configure an on-premises client computer toosubmit jobs tooa [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure.</span></span> <span data-ttu-id="989e3-105">W tym artykule opisano, jak narzędzia zadania toosubmit tooset lokalnego komputera z klientem za pośrednictwem protokołu HTTPS toohello klastra na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="989e3-105">This article shows you how tooset up a local computer with client tools toosubmit job over HTTPS toohello cluster in Azure.</span></span> <span data-ttu-id="989e3-106">W ten sposób kilku użytkowników klastra można przesłać zadania tooa oparte na chmurze HPC Pack klastra, ale bez połączyć się bezpośrednio węzła głównego toohello maszyny Wirtualnej lub uzyskiwania dostępu do subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="989e3-106">In this way, several cluster users can submit jobs tooa cloud-based HPC Pack cluster, but without connecting directly toohello head node VM or accessing an Azure subscription.</span></span>

![Przedstawia klastra tooa zadania na platformie Azure][jobsubmit]

## <a name="prerequisites"></a><span data-ttu-id="989e3-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="989e3-108">Prerequisites</span></span>
* <span data-ttu-id="989e3-109">**Węzłem głównym HPC Pack wdrożony w maszynie Wirtualnej platformy Azure** -zalecane jest użycie automatycznych narzędzi takich jak [szablonie Szybki Start Azure](https://azure.microsoft.com/documentation/templates/) lub [skrypt programu PowerShell Azure](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) węzła głównego hello toodeploy i klaster.</span><span class="sxs-lookup"><span data-stu-id="989e3-109">**HPC Pack head node deployed in an Azure VM** - We recommend that you use automated tools such as an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/) or an [Azure PowerShell script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toodeploy hello head node and cluster.</span></span> <span data-ttu-id="989e3-110">Należy nazwę DNS hello hello węzła głównego i hello poświadczenia administratora klastrów, aby wykonać kroki hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="989e3-110">You need hello DNS name of hello head node and hello credentials of a cluster administrator to complete hello steps in this article.</span></span>
* <span data-ttu-id="989e3-111">**Komputer kliencki** -wymagają systemu Windows lub Windows Server komputera klienckiego, który można uruchomić narzędzia klienta HPC Pack (zobacz [wymagania systemowe](https://technet.microsoft.com/library/dn535781.aspx)).</span><span class="sxs-lookup"><span data-stu-id="989e3-111">**Client computer** - You need a Windows or Windows Server client computer that can run HPC Pack client utilities (see [system requirements](https://technet.microsoft.com/library/dn535781.aspx)).</span></span> <span data-ttu-id="989e3-112">Jeśli chcesz tylko zadania toosubmit interfejsu API REST lub portalu internetowego HPC Pack hello toouse, można użyć dowolnego komputera klienckiego wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="989e3-112">If you only want toouse hello HPC Pack web portal or REST API toosubmit jobs, you can use any client computer of your choice.</span></span>
* <span data-ttu-id="989e3-113">**Nośnik instalacyjny HPC Pack** -tooinstall hello HPC Pack narzędzi klienta, pakiet instalacyjny wolnego hello do najnowszej wersji HPC Pack (HPC Pack 2012 R2) jest niedostępna z [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span><span class="sxs-lookup"><span data-stu-id="989e3-113">**HPC Pack installation media** - tooinstall hello HPC Pack client utilities, hello free installation package for the latest version of HPC Pack (HPC Pack 2012 R2) is available from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="989e3-114">Upewnij się, że pobierać hello tej samej wersji pakietu HPC, który jest zainstalowany w węźle głównym hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="989e3-114">Make sure that you download hello same version of HPC Pack that is installed on hello head node VM.</span></span>

## <a name="step-1-install-and-configure-hello-web-components-on-hello-head-node"></a><span data-ttu-id="989e3-115">Krok 1: Instalowanie i konfigurowanie składników sieci web hello na powitania węzła głównego</span><span class="sxs-lookup"><span data-stu-id="989e3-115">Step 1: Install and configure hello web components on hello head node</span></span>
<span data-ttu-id="989e3-116">tooenable klastra toohello zadania toosubmit interfejsu REST za pośrednictwem protokołu HTTPS, upewnij się, że składniki sieci web HPC Pack hello są skonfigurowane w węźle głównym HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="989e3-116">tooenable a REST interface toosubmit jobs toohello cluster over HTTPS, ensure that hello HPC Pack web components are configured on hello HPC Pack head node.</span></span> <span data-ttu-id="989e3-117">Jeśli nie są już zainstalowane, należy najpierw zainstalować składniki sieci web hello, uruchamiając plik instalacyjny HpcWebComponents.msi hello.</span><span class="sxs-lookup"><span data-stu-id="989e3-117">If they aren't already installed, first install hello web components by running hello HpcWebComponents.msi installation file.</span></span> <span data-ttu-id="989e3-118">Następnie należy skonfigurować składniki hello przez uruchomienie skryptu środowiska PowerShell klastra HPC hello **HPCWebComponents.ps1 zestawu**.</span><span class="sxs-lookup"><span data-stu-id="989e3-118">Then, configure hello components by running hello HPC PowerShell script **Set-HPCWebComponents.ps1**.</span></span>

<span data-ttu-id="989e3-119">Aby uzyskać szczegółowe procedury, zobacz [zainstalować składniki sieci Web hello Microsoft HPC Pack](http://technet.microsoft.com/library/hh314627.aspx).</span><span class="sxs-lookup"><span data-stu-id="989e3-119">For detailed procedures, see [Install hello Microsoft HPC Pack Web Components](http://technet.microsoft.com/library/hh314627.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="989e3-120">Niektóre szablony szybkiego startu usługi Azure HPC Pack Instalowanie i konfigurowanie składników sieci web hello automatycznie.</span><span class="sxs-lookup"><span data-stu-id="989e3-120">Certain Azure quickstart templates for HPC Pack install and configure hello web components automatically.</span></span> <span data-ttu-id="989e3-121">Jeśli używasz hello [skrypt wdrożenia HPC Pack IaaS](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toocreate hello klastra, można opcjonalnie zainstalować i skonfigurować składniki sieci web hello jako część wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="989e3-121">If you use hello [HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toocreate hello cluster, you can optionally install and configure hello web components as part of hello deployment.</span></span>
> 
> 

<span data-ttu-id="989e3-122">**składniki sieci web hello tooinstall**</span><span class="sxs-lookup"><span data-stu-id="989e3-122">**tooinstall hello web components**</span></span>

1. <span data-ttu-id="989e3-123">Połącz z węzłem głównym toohello maszyny Wirtualnej, używając hello poświadczenia administratora klastra.</span><span class="sxs-lookup"><span data-stu-id="989e3-123">Connect toohello head node VM by using hello credentials of a cluster administrator.</span></span>
2. <span data-ttu-id="989e3-124">Z folderu instalacji pakietu HPC hello Uruchom HpcWebComponents.msi na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="989e3-124">From hello HPC Pack Setup folder, run HpcWebComponents.msi on hello head node.</span></span>
3. <span data-ttu-id="989e3-125">Wykonaj kroki hello w składnikach hello tooinstall hello kreatora w sieci web</span><span class="sxs-lookup"><span data-stu-id="989e3-125">Follow hello steps in hello wizard tooinstall hello web components</span></span>

<span data-ttu-id="989e3-126">**składniki sieci web hello tooconfigure**</span><span class="sxs-lookup"><span data-stu-id="989e3-126">**tooconfigure hello web components**</span></span>

1. <span data-ttu-id="989e3-127">W węźle głównym hello Uruchom program HPC PowerShell jako administrator.</span><span class="sxs-lookup"><span data-stu-id="989e3-127">On hello head node, start HPC PowerShell as an administrator.</span></span>
2. <span data-ttu-id="989e3-128">Lokalizacja toohello katalogu toochange skryptu konfiguracji hello, hello wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="989e3-128">toochange directory toohello location of hello configuration script, type hello following command:</span></span>
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. <span data-ttu-id="989e3-129">tooconfigure hello interfejsu REST i uruchomić hello HPC usługi sieci Web, hello wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="989e3-129">tooconfigure hello REST interface and start hello HPC Web Service, type hello following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. <span data-ttu-id="989e3-130">Gdy zostanie wyświetlony monit o tooselect certyfikat, wybierz certyfikat hello, który odpowiada toohello publicznej nazwy DNS hello węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="989e3-130">When prompted tooselect a certificate, choose hello certificate that corresponds toohello public DNS name of hello head node.</span></span> <span data-ttu-id="989e3-131">Na przykład w przypadku wdrożenia hello węzła głównego maszyny Wirtualnej przy użyciu hello klasycznego modelu wdrażania, nazwa certyfikatu hello wygląda następująco: CN =&lt;*HeadNodeDnsName*&gt;. cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="989e3-131">For example, if you deploy hello head node VM using hello classic deployment model, hello certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net.</span></span> <span data-ttu-id="989e3-132">Jeśli używasz modelu wdrażania usługi Resource Manager hello, nazwa certyfikatu hello wygląda CN =&lt;*HeadNodeDnsName*&gt;.&lt; *region*&gt;. cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="989e3-132">If you use hello Resource Manager deployment model, hello certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.&lt;*region*&gt;.cloudapp.azure.com.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="989e3-133">Należy wybrać ten certyfikat później podczas przesyłania zadań toohello węzła głównego z komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="989e3-133">You select this certificate later when you submit jobs toohello head node from an on-premises computer.</span></span> <span data-ttu-id="989e3-134">Brak zaznaczenia lub skonfigurować certyfikat, który odpowiada nazwa komputera toohello hello węzła głównego w domenie usługi Active Directory hello (na przykład, CN =*MyHPCHeadNode.HpcAzure.local*).</span><span class="sxs-lookup"><span data-stu-id="989e3-134">Don't select or configure a certificate that corresponds toohello computer name of hello head node in hello Active Directory domain (for example, CN=*MyHPCHeadNode.HpcAzure.local*).</span></span>
   > 
   > 
5. <span data-ttu-id="989e3-135">portal sieci web hello tooconfigure składania zadania hello wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="989e3-135">tooconfigure hello web portal for job submission, type hello following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. <span data-ttu-id="989e3-136">Po ukończeniu działania skryptu hello zatrzymać i ponownie uruchomić hello usługa harmonogramu zadań HPC, wpisując hello następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="989e3-136">After hello script completes, stop and restart hello HPC Job Scheduler Service by typing hello following commands:</span></span>
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-hello-hpc-pack-client-utilities-on-an-on-premises-computer"></a><span data-ttu-id="989e3-137">Krok 2: Zainstaluj narzędzia klienta HPC Pack hello na komputerze lokalnym</span><span class="sxs-lookup"><span data-stu-id="989e3-137">Step 2: Install hello HPC Pack client utilities on an on-premises computer</span></span>
<span data-ttu-id="989e3-138">Jeśli chcesz tooinstall hello HPC Pack klienta narzędzia na komputerze, Pobierz pliki instalacji HPC Pack (Instalacja pełna) z hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span><span class="sxs-lookup"><span data-stu-id="989e3-138">If you want tooinstall hello HPC Pack client utilities on your computer, download the HPC Pack setup files (full installation) from hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="989e3-139">Po rozpoczęciu instalacji hello, wybierz opcję instalacji hello hello **narzędzi klienta HPC Pack**.</span><span class="sxs-lookup"><span data-stu-id="989e3-139">When you begin hello installation, choose hello setup option for hello **HPC Pack client utilities**.</span></span>

<span data-ttu-id="989e3-140">klienckie HPC Pack hello toouse narzędzia toosubmit zadania toohello węzła głównego maszyny Wirtualnej, należy również tooexport certyfikat od węzła głównego hello i zainstaluj go na komputerze klienckim hello.</span><span class="sxs-lookup"><span data-stu-id="989e3-140">toouse hello HPC Pack client tools toosubmit jobs toohello head node VM, you also need tooexport a certificate from hello head node and install it on hello client computer.</span></span> <span data-ttu-id="989e3-141">Witaj, certyfikat musi mieć. CER format.</span><span class="sxs-lookup"><span data-stu-id="989e3-141">hello certificate must be in .CER format.</span></span>

<span data-ttu-id="989e3-142">**certyfikat hello tooexport z węzłem głównym hello**</span><span class="sxs-lookup"><span data-stu-id="989e3-142">**tooexport hello certificate from hello head node**</span></span>

1. <span data-ttu-id="989e3-143">W węźle głównym hello Dodaj hello certyfikatów przystawki tooa konsoli Microsoft Management Console dla hello konta na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="989e3-143">On hello head node, add hello Certificates snap-in tooa Microsoft Management Console for hello Local Computer account.</span></span> <span data-ttu-id="989e3-144">Przystawka hello tooadd znajduje się [dodać tooan hello przystawki certyfikatów konsoli MMC](https://technet.microsoft.com/library/cc754431.aspx).</span><span class="sxs-lookup"><span data-stu-id="989e3-144">For steps tooadd hello snap-in, see [Add hello Certificates Snap-in tooan MMC](https://technet.microsoft.com/library/cc754431.aspx).</span></span>
2. <span data-ttu-id="989e3-145">W drzewie konsoli hello rozwiń **certyfikaty — komputer lokalny** > **osobistych**, a następnie kliknij przycisk **certyfikaty**.</span><span class="sxs-lookup"><span data-stu-id="989e3-145">In hello console tree, expand **Certificates – Local Computer** > **Personal**, and then click **Certificates**.</span></span>
3. <span data-ttu-id="989e3-146">Zlokalizuj certyfikat hello skonfigurowane dla składników sieci web HPC Pack hello w [krok 1: Instalowanie i konfigurowanie składników sieci web hello na powitania węzła głównego](#step-1:-install-and-configure-the-web-components-on-the-head-node) (na przykład, CN =&lt;*HeadNodeDnsName* &gt;. cloudapp.net).</span><span class="sxs-lookup"><span data-stu-id="989e3-146">Locate hello certificate that you configured for hello HPC Pack web components in [Step 1: Install and configure hello web components on hello head node](#step-1:-install-and-configure-the-web-components-on-the-head-node) (for example, CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net).</span></span>
4. <span data-ttu-id="989e3-147">Kliknij prawym przyciskiem myszy hello certyfikatu, a następnie kliknij przycisk **wszystkie zadania** > **wyeksportować**.</span><span class="sxs-lookup"><span data-stu-id="989e3-147">Right-click hello certificate, and click **All Tasks** > **Export**.</span></span>
5. <span data-ttu-id="989e3-148">W Kreatorze eksportu certyfikatów hello, kliknij przycisk **dalej**i upewnij się, że **nie eksportuj klucza prywatnego hello** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="989e3-148">In hello Certificate Export Wizard, click **Next**, and ensure that **No, do not export hello private key** is selected.</span></span>
6. <span data-ttu-id="989e3-149">Certyfikat x.509 szyfrowany binarnie algorytmem hello wykonaj pozostałe kroki hello kreatora tooexport hello certyfikatu w DER (. Format CER).</span><span class="sxs-lookup"><span data-stu-id="989e3-149">Follow hello remaining steps of hello wizard tooexport hello certificate in DER encoded binary X.509 (.CER) format.</span></span>

<span data-ttu-id="989e3-150">**tooimport hello certyfikatów na komputerze klienckim hello**</span><span class="sxs-lookup"><span data-stu-id="989e3-150">**tooimport hello certificate on hello client computer**</span></span>

1. <span data-ttu-id="989e3-151">Skopiuj wyeksportowany z hello węzła głównego tooa folderu na komputerze klienckim hello hello certyfikat.</span><span class="sxs-lookup"><span data-stu-id="989e3-151">Copy hello certificate that you exported from hello head node tooa folder on hello client computer.</span></span>
2. <span data-ttu-id="989e3-152">Na komputerze klienckim hello Uruchom certmgr.msc.</span><span class="sxs-lookup"><span data-stu-id="989e3-152">On hello client computer, run certmgr.msc.</span></span>
3. <span data-ttu-id="989e3-153">Rozwiń węzeł w Menedżerze certyfikatów **Certyfikaty — bieżący użytkownik** > **zaufane główne urzędy certyfikacji**, kliknij prawym przyciskiem myszy **certyfikaty**, a następnie Kliknij przycisk **wszystkie zadania** > **importu**.</span><span class="sxs-lookup"><span data-stu-id="989e3-153">In Certificate Manager, expand **Certificates – Current user** > **Trusted Root Certification Authorities**, right-click **Certificates**, and then click **All Tasks** > **Import**.</span></span>
4. <span data-ttu-id="989e3-154">W hello Kreatora importu certyfikatów kliknij **dalej** i wykonaj hello kroki tooimport hello wyeksportowany certyfikat w magazynie zaufanych głównych urzędów certyfikacji toohello węzła głównego hello.</span><span class="sxs-lookup"><span data-stu-id="989e3-154">In hello Certificate Import Wizard, click **Next** and follow hello steps tooimport hello certificate that you exported from hello head node toohello Trusted Root Certification Authorities store.</span></span>

> [!TIP]
> <span data-ttu-id="989e3-155">Może pojawić się ostrzeżenie, ponieważ hello urzędu certyfikacji na powitania węzła głównego nie jest rozpoznawane przez komputer kliencki hello.</span><span class="sxs-lookup"><span data-stu-id="989e3-155">You might see a security warning, because hello certification authority on hello head node isn't recognized by hello client computer.</span></span> <span data-ttu-id="989e3-156">Do celów testowych, możesz zignorować to ostrzeżenie i pełne importu certyfikatów hello.</span><span class="sxs-lookup"><span data-stu-id="989e3-156">For testing purposes, you can ignore this warning and complete hello certificate import.</span></span>
> 
> 

## <a name="step-3-run-test-jobs-on-hello-cluster"></a><span data-ttu-id="989e3-157">Krok 3: Uruchamianie testu zadań w klastrze hello</span><span class="sxs-lookup"><span data-stu-id="989e3-157">Step 3: Run test jobs on hello cluster</span></span>
<span data-ttu-id="989e3-158">Spróbuj uruchomionych zadań na powitania konfiguracji klastra na platformie Azure z hello tooverify lokalnego komputera.</span><span class="sxs-lookup"><span data-stu-id="989e3-158">tooverify your configuration, try running jobs on hello cluster in Azure from hello on-premises computer.</span></span> <span data-ttu-id="989e3-159">Na przykład można użyć narzędzia HPC Pack graficznego interfejsu użytkownika lub polecenia toosubmit zadania toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="989e3-159">For example, you can use HPC Pack GUI tools or command-line commands toosubmit jobs toohello cluster.</span></span> <span data-ttu-id="989e3-160">Umożliwia także zadania toosubmit portalu sieci web.</span><span class="sxs-lookup"><span data-stu-id="989e3-160">You can also use a web-based portal toosubmit jobs.</span></span>

<span data-ttu-id="989e3-161">**toorun zadania przesyłania polecenia na komputerze klienckim hello**</span><span class="sxs-lookup"><span data-stu-id="989e3-161">**toorun job submission commands on hello client computer**</span></span>

1. <span data-ttu-id="989e3-162">Na komputerze klienckim, w którym są zainstalowane narzędzia klienta HPC Pack hello Uruchom wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="989e3-162">On a client computer where hello HPC Pack client utilities are installed, start a Command Prompt.</span></span>
2. <span data-ttu-id="989e3-163">Wpisz polecenie przykładowe.</span><span class="sxs-lookup"><span data-stu-id="989e3-163">Type a sample command.</span></span> <span data-ttu-id="989e3-164">Na przykład toolist wszystkich zadań w klastrze hello, wpisz polecenie podobne tooone z powitania po, w zależności od hello pełną nazwą DNS hello węzła głównego:</span><span class="sxs-lookup"><span data-stu-id="989e3-164">For example, toolist all jobs on hello cluster, type a command similar tooone of hello following, depending on hello full DNS name of hello head node:</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    <span data-ttu-id="989e3-165">lub</span><span class="sxs-lookup"><span data-stu-id="989e3-165">or</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > <span data-ttu-id="989e3-166">Użyj hello pełną nazwą DNS hello węzła głównego, nie adres IP hello w adresie URL harmonogramu hello.</span><span class="sxs-lookup"><span data-stu-id="989e3-166">Use hello full DNS name of hello head node, not hello IP address, in hello scheduler URL.</span></span> <span data-ttu-id="989e3-167">Jeśli określisz adresu IP hello pojawia się błąd podobny zbyt "hello, certyfikat serwera musi tooeither zawiera prawidłowy łańcuch zaufania lub toobe umieszczane w magazynie zaufanych certyfikatów głównych hello."</span><span class="sxs-lookup"><span data-stu-id="989e3-167">If you specify hello IP address, an error appears similar too"hello server certificate needs tooeither have a valid chain of trust or toobe placed in hello trusted root store."</span></span>
   > 
   > 
3. <span data-ttu-id="989e3-168">Po wyświetleniu monitu wpisz nazwę użytkownika hello (w postaci hello &lt;DomainName&gt;\\&lt;UserName&gt;) i hasło administratora klastra HPC hello lub innego użytkownika klastra skonfigurowanego.</span><span class="sxs-lookup"><span data-stu-id="989e3-168">When prompted, type hello user name (in hello form &lt;DomainName&gt;\\&lt;UserName&gt;) and password of hello HPC cluster administrator or another cluster user that you configured.</span></span> <span data-ttu-id="989e3-169">Możesz wybrać toostore poświadczenia hello lokalnie więcej operacji zadań.</span><span class="sxs-lookup"><span data-stu-id="989e3-169">You can choose toostore hello credentials locally for more job operations.</span></span>
   
    <span data-ttu-id="989e3-170">Zostanie wyświetlona lista zadań.</span><span class="sxs-lookup"><span data-stu-id="989e3-170">A list of jobs appears.</span></span>

<span data-ttu-id="989e3-171">**toouse Menedżer zadań klastra HPC na komputerze klienckim hello**</span><span class="sxs-lookup"><span data-stu-id="989e3-171">**toouse HPC Job Manager on hello client computer**</span></span>

1. <span data-ttu-id="989e3-172">Jeśli wcześniej nie przechowują poświadczeń domeny użytkownika, klastra, podczas przesyłania zadania, można dodać hello poświadczeń w Menedżerze poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="989e3-172">If you didn't previously store domain credentials for a cluster user when submitting a job, you can add hello credentials in Credential Manager.</span></span>
   
    <span data-ttu-id="989e3-173">a.</span><span class="sxs-lookup"><span data-stu-id="989e3-173">a.</span></span> <span data-ttu-id="989e3-174">W Panelu sterowania na komputerze klienckim hello Uruchom Menedżera poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="989e3-174">In Control Panel on hello client computer, start Credential Manager.</span></span>
   
    <span data-ttu-id="989e3-175">b.</span><span class="sxs-lookup"><span data-stu-id="989e3-175">b.</span></span> <span data-ttu-id="989e3-176">Kliknij przycisk **poświadczeń systemu Windows** > **Dodaj poświadczenie ogólnego**.</span><span class="sxs-lookup"><span data-stu-id="989e3-176">Click **Windows Credentials** > **Add a generic credential**.</span></span>
   
    <span data-ttu-id="989e3-177">c.</span><span class="sxs-lookup"><span data-stu-id="989e3-177">c.</span></span> <span data-ttu-id="989e3-178">Określ adres internetowy hello (na przykład https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler lub https://&lt;HeadNodeDnsName&gt;.&lt; region&gt;.cloudapp.azure.com/HpcScheduler) i nazwą użytkownika hello (&lt;DomainName&gt;\\&lt;UserName&gt;) i hasło administratora klastra hello lub innego użytkownika klastra, który został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="989e3-178">Specify hello Internet address (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com/HpcScheduler), and hello user name (&lt;DomainName&gt;\\&lt;UserName&gt;) and password of hello cluster administrator or another cluster user that you configured.</span></span>
2. <span data-ttu-id="989e3-179">Na komputerze klienckim hello Uruchom Menedżer zadań klastra HPC.</span><span class="sxs-lookup"><span data-stu-id="989e3-179">On hello client computer, start HPC Job Manager.</span></span>
3. <span data-ttu-id="989e3-180">W hello **wybierz węzeł Head** okno dialogowe, typ hello adresu URL toohello węzła głównego na platformie Azure (na przykład https://&lt;HeadNodeDnsName&gt;. cloudapp.net lub https://&lt;HeadNodeDnsName&gt;. &lt;region&gt;. cloudapp.azure.com).</span><span class="sxs-lookup"><span data-stu-id="989e3-180">In hello **Select Head Node** dialog box, type hello URL toohello head node in Azure (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com).</span></span>
   
    <span data-ttu-id="989e3-181">Menedżer zadań klastra HPC otwiera i jest wyświetlana lista zadań na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="989e3-181">HPC Job Manager opens and shows a list of jobs on hello head node.</span></span>

<span data-ttu-id="989e3-182">**portal sieci web hello toouse systemem hello węzła głównego**</span><span class="sxs-lookup"><span data-stu-id="989e3-182">**toouse hello web portal running on hello head node**</span></span>

1. <span data-ttu-id="989e3-183">Uruchom przeglądarkę sieci web na komputerze klienckim hello i wprowadź jedno z następujących adresów, w zależności od hello pełną nazwą DNS węzła głównego hello hello:</span><span class="sxs-lookup"><span data-stu-id="989e3-183">Start a web browser on hello client computer, and enter one of hello following addresses, depending on hello full DNS name of hello head node:</span></span>
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    <span data-ttu-id="989e3-184">lub</span><span class="sxs-lookup"><span data-stu-id="989e3-184">or</span></span>
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. <span data-ttu-id="989e3-185">Okno dialogowe zabezpieczeń hello, który pojawia się wpisz poświadczenia domeny hello administratora klastra HPC hello.</span><span class="sxs-lookup"><span data-stu-id="989e3-185">In hello security dialog box that appears, type hello domain credentials of hello HPC cluster administrator.</span></span> <span data-ttu-id="989e3-186">(Można również dodać innych klastra użytkowników w różnych ról.</span><span class="sxs-lookup"><span data-stu-id="989e3-186">(You can also add other cluster users in different roles.</span></span> <span data-ttu-id="989e3-187">Zobacz [Zarządzanie użytkownikami klastra](https://technet.microsoft.com/library/ff919335.aspx).)</span><span class="sxs-lookup"><span data-stu-id="989e3-187">See [Managing Cluster Users](https://technet.microsoft.com/library/ff919335.aspx).)</span></span>
   
    <span data-ttu-id="989e3-188">portal sieci web Hello otwiera widok listy toohello zadania.</span><span class="sxs-lookup"><span data-stu-id="989e3-188">hello web portal opens toohello job list view.</span></span>
3. <span data-ttu-id="989e3-189">Kliknij toosubmit przykładowe zadania, które zwraca ciąg hello "Hello World" z klastra hello **nowe zadanie** w nawigacji po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="989e3-189">toosubmit a sample job that returns hello string “Hello World” from hello cluster, click **New job** in hello left-hand navigation.</span></span>
4. <span data-ttu-id="989e3-190">Na powitania **nowe zadanie** w obszarze **ze stron przesyłania**, kliknij przycisk **HelloWorld**.</span><span class="sxs-lookup"><span data-stu-id="989e3-190">On hello **New Job** page, under **From submission pages**, click **HelloWorld**.</span></span> <span data-ttu-id="989e3-191">zostanie wyświetlona strona przesyłania zadania Hello.</span><span class="sxs-lookup"><span data-stu-id="989e3-191">hello job submission page appears.</span></span>
5. <span data-ttu-id="989e3-192">Kliknij przycisk **przesłać**.</span><span class="sxs-lookup"><span data-stu-id="989e3-192">Click **Submit**.</span></span> <span data-ttu-id="989e3-193">Po wyświetleniu monitu podaj poświadczenia domeny hello administratora klastra HPC hello.</span><span class="sxs-lookup"><span data-stu-id="989e3-193">If prompted, provide hello domain credentials of hello HPC cluster administrator.</span></span> <span data-ttu-id="989e3-194">zadanie Hello i hello identyfikator zadania jest wyświetlana na powitania **Moje zadania** strony.</span><span class="sxs-lookup"><span data-stu-id="989e3-194">hello job is submitted, and hello job ID appears on hello **My Jobs** page.</span></span>
6. <span data-ttu-id="989e3-195">wyniki hello tooview hello zadania, który zostanie przesłany, kliknij hello identyfikator zadania, a następnie kliknij **zadania widoku** danych wyjściowych polecenia hello tooview (w obszarze **dane wyjściowe**).</span><span class="sxs-lookup"><span data-stu-id="989e3-195">tooview hello results of hello job that you submitted, click hello job ID, and then click **View Tasks** tooview hello command output (under **Output**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="989e3-196">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="989e3-196">Next steps</span></span>
* <span data-ttu-id="989e3-197">Istnieje także możliwość przesyłania zadań toohello klastrze platformy Azure z hello [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="989e3-197">You can also submit jobs toohello Azure cluster with hello [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span>
* <span data-ttu-id="989e3-198">Toosubmit zadań klastra z klientów systemu Linux, zobacz hello Python przykładowa w hello [HPC Pack 2012 R2 SDK oraz przykładowy kod](https://www.microsoft.com/download/details.aspx?id=41633).</span><span class="sxs-lookup"><span data-stu-id="989e3-198">If you want toosubmit cluster jobs from a Linux client, see hello Python sample in hello [HPC Pack 2012 R2 SDK and Sample Code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span>

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png
