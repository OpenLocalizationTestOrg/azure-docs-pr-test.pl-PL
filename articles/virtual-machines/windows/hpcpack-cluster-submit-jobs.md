---
title: "Przesyłanie zadań HPC Pack klastra na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować na komputerze lokalnym do przesyłania zadań do klastra HPC Pack na platformie Azure"
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
ms.openlocfilehash: d5953f1e1dd2deb4d871bd67352a6a5b2ae13dbf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-to-an-hpc-pack-cluster-deployed-in-azure"></a><span data-ttu-id="b01e8-103">Przesyłanie zadań HPC z lokalnego komputera do klastra pakietu HPC Pack wdrożonego na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="b01e8-103">Submit HPC jobs from an on-premises computer to an HPC Pack cluster deployed in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="b01e8-104">Konfigurowanie komputera klienckiego lokalnymi umożliwiają przesyłanie zadań do [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) klastra na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b01e8-104">Configure an on-premises client computer to submit jobs to a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure.</span></span> <span data-ttu-id="b01e8-105">W tym artykule przedstawiono sposób konfigurowania lokalnego komputera z narzędziami klienckimi można przesłać zadania przy użyciu protokołu HTTPS do klastra w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="b01e8-105">This article shows you how to set up a local computer with client tools to submit job over HTTPS to the cluster in Azure.</span></span> <span data-ttu-id="b01e8-106">W ten sposób wielu użytkowników klastra można przesłać zadania do klastra HPC Pack oparte na chmurze, ale bez połączenie bezpośrednio z węzłem głównym maszyny Wirtualnej lub uzyskiwanie dostępu do subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b01e8-106">In this way, several cluster users can submit jobs to a cloud-based HPC Pack cluster, but without connecting directly to the head node VM or accessing an Azure subscription.</span></span>

![Przesyłanie zadań do klastra w systemie Azure][jobsubmit]

## <a name="prerequisites"></a><span data-ttu-id="b01e8-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b01e8-108">Prerequisites</span></span>
* <span data-ttu-id="b01e8-109">**Węzłem głównym HPC Pack wdrożony w maszynie Wirtualnej platformy Azure** -zalecane jest użycie automatycznych narzędzi takich jak [szablonie Szybki Start Azure](https://azure.microsoft.com/documentation/templates/) lub [skrypt programu PowerShell Azure](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) wdrażania węzła głównego i klaster.</span><span class="sxs-lookup"><span data-stu-id="b01e8-109">**HPC Pack head node deployed in an Azure VM** - We recommend that you use automated tools such as an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/) or an [Azure PowerShell script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) to deploy the head node and cluster.</span></span> <span data-ttu-id="b01e8-110">Należy nazwy DNS węzła głównego i poświadczenia administratora klastra, aby wykonać kroki opisane w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="b01e8-110">You need the DNS name of the head node and the credentials of a cluster administrator to complete the steps in this article.</span></span>
* <span data-ttu-id="b01e8-111">**Komputer kliencki** -wymagają systemu Windows lub Windows Server komputera klienckiego, który można uruchomić narzędzia klienta HPC Pack (zobacz [wymagania systemowe](https://technet.microsoft.com/library/dn535781.aspx)).</span><span class="sxs-lookup"><span data-stu-id="b01e8-111">**Client computer** - You need a Windows or Windows Server client computer that can run HPC Pack client utilities (see [system requirements](https://technet.microsoft.com/library/dn535781.aspx)).</span></span> <span data-ttu-id="b01e8-112">Jeśli chcesz użyć portalu internetowego HPC Pack lub interfejsu API REST do przesyłania zadań, można użyć dowolnego komputera klienckiego wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b01e8-112">If you only want to use the HPC Pack web portal or REST API to submit jobs, you can use any client computer of your choice.</span></span>
* <span data-ttu-id="b01e8-113">**Nośnik instalacyjny HPC Pack** — Aby zainstalować narzędzia HPC Pack klienta pakietu instalacyjnego wolnego do najnowszej wersji HPC Pack (HPC Pack 2012 R2) jest niedostępna z [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span><span class="sxs-lookup"><span data-stu-id="b01e8-113">**HPC Pack installation media** - To install the HPC Pack client utilities, the free installation package for the latest version of HPC Pack (HPC Pack 2012 R2) is available from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="b01e8-114">Upewnij się, pobrania tej samej wersji pakietu HPC, który jest zainstalowany w węźle głównym maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b01e8-114">Make sure that you download the same version of HPC Pack that is installed on the head node VM.</span></span>

## <a name="step-1-install-and-configure-the-web-components-on-the-head-node"></a><span data-ttu-id="b01e8-115">Krok 1: Instalowanie i konfigurowanie składników sieci web na węzła głównego</span><span class="sxs-lookup"><span data-stu-id="b01e8-115">Step 1: Install and configure the web components on the head node</span></span>
<span data-ttu-id="b01e8-116">Aby włączyć interfejs REST umożliwiają przesyłanie zadań do klastra przy użyciu protokołu HTTPS, upewnij się, że składniki sieci web HPC Pack są skonfigurowane w węźle głównym HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="b01e8-116">To enable a REST interface to submit jobs to the cluster over HTTPS, ensure that the HPC Pack web components are configured on the HPC Pack head node.</span></span> <span data-ttu-id="b01e8-117">Jeśli nie są już zainstalowane, należy najpierw zainstalować składniki sieci web, uruchamiając plik instalacyjny HpcWebComponents.msi.</span><span class="sxs-lookup"><span data-stu-id="b01e8-117">If they aren't already installed, first install the web components by running the HpcWebComponents.msi installation file.</span></span> <span data-ttu-id="b01e8-118">Następnie należy skonfigurować składniki przez uruchomienie skryptu środowiska PowerShell klastra HPC **HPCWebComponents.ps1 zestawu**.</span><span class="sxs-lookup"><span data-stu-id="b01e8-118">Then, configure the components by running the HPC PowerShell script **Set-HPCWebComponents.ps1**.</span></span>

<span data-ttu-id="b01e8-119">Aby uzyskać szczegółowe procedury, zobacz [zainstalować składniki sieci Web programu Microsoft HPC Pack](http://technet.microsoft.com/library/hh314627.aspx).</span><span class="sxs-lookup"><span data-stu-id="b01e8-119">For detailed procedures, see [Install the Microsoft HPC Pack Web Components](http://technet.microsoft.com/library/hh314627.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="b01e8-120">Niektóre szablony szybkiego startu usługi Azure HPC Pack zainstalować i skonfigurować składniki sieci web automatycznie.</span><span class="sxs-lookup"><span data-stu-id="b01e8-120">Certain Azure quickstart templates for HPC Pack install and configure the web components automatically.</span></span> <span data-ttu-id="b01e8-121">Jeśli używasz [skrypt wdrożenia HPC Pack IaaS](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) do utworzenia klastra, można opcjonalnie zainstalować i skonfigurować składniki sieci web jako część wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="b01e8-121">If you use the [HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) to create the cluster, you can optionally install and configure the web components as part of the deployment.</span></span>
> 
> 

<span data-ttu-id="b01e8-122">**Aby zainstalować składniki sieci web**</span><span class="sxs-lookup"><span data-stu-id="b01e8-122">**To install the web components**</span></span>

1. <span data-ttu-id="b01e8-123">Połączenie z węzłem głównym maszyny Wirtualnej przy użyciu poświadczeń administratora klastra.</span><span class="sxs-lookup"><span data-stu-id="b01e8-123">Connect to the head node VM by using the credentials of a cluster administrator.</span></span>
2. <span data-ttu-id="b01e8-124">Uruchom z folderu instalacji pakietu HPC, HpcWebComponents.msi w węźle głównym.</span><span class="sxs-lookup"><span data-stu-id="b01e8-124">From the HPC Pack Setup folder, run HpcWebComponents.msi on the head node.</span></span>
3. <span data-ttu-id="b01e8-125">Postępuj zgodnie z instrukcjami kreatora, aby zainstalować składniki sieci web</span><span class="sxs-lookup"><span data-stu-id="b01e8-125">Follow the steps in the wizard to install the web components</span></span>

<span data-ttu-id="b01e8-126">**Aby skonfigurować składniki sieci web**</span><span class="sxs-lookup"><span data-stu-id="b01e8-126">**To configure the web components**</span></span>

1. <span data-ttu-id="b01e8-127">W węźle głównym Uruchom program HPC PowerShell jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b01e8-127">On the head node, start HPC PowerShell as an administrator.</span></span>
2. <span data-ttu-id="b01e8-128">Aby zmienić katalog do lokalizacji pliku skryptu konfiguracji, wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b01e8-128">To change directory to the location of the configuration script, type the following command:</span></span>
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. <span data-ttu-id="b01e8-129">Aby skonfigurować interfejs REST i uruchomić usługę sieci Web HPC, wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b01e8-129">To configure the REST interface and start the HPC Web Service, type the following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. <span data-ttu-id="b01e8-130">Gdy zostanie wyświetlony monit o wybranie certyfikatu, należy wybrać certyfikat, który odpowiada publicznej nazwy DNS węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="b01e8-130">When prompted to select a certificate, choose the certificate that corresponds to the public DNS name of the head node.</span></span> <span data-ttu-id="b01e8-131">Na przykład w przypadku wdrożenia maszyny Wirtualnej przy użyciu klasycznego modelu wdrażania węzłem głównym, nazwa certyfikatu wygląda CN =&lt;*HeadNodeDnsName*&gt;. cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="b01e8-131">For example, if you deploy the head node VM using the classic deployment model, the certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net.</span></span> <span data-ttu-id="b01e8-132">Jeśli używasz modelu wdrażania usługi Resource Manager, nazwa certyfikatu wygląda CN =&lt;*HeadNodeDnsName*&gt;.&lt; *region*&gt;. cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="b01e8-132">If you use the Resource Manager deployment model, the certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.&lt;*region*&gt;.cloudapp.azure.com.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b01e8-133">Należy wybrać ten certyfikat później podczas przesyłania zadań do węzła głównego z komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="b01e8-133">You select this certificate later when you submit jobs to the head node from an on-premises computer.</span></span> <span data-ttu-id="b01e8-134">Brak zaznaczenia lub skonfigurować certyfikat, który odpowiada nazwie komputera węzła głównego w domenie usługi Active Directory (na przykład, CN =*MyHPCHeadNode.HpcAzure.local*).</span><span class="sxs-lookup"><span data-stu-id="b01e8-134">Don't select or configure a certificate that corresponds to the computer name of the head node in the Active Directory domain (for example, CN=*MyHPCHeadNode.HpcAzure.local*).</span></span>
   > 
   > 
5. <span data-ttu-id="b01e8-135">Aby skonfigurować dla przesyłanie zadań do portalu sieci web, wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b01e8-135">To configure the web portal for job submission, type the following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. <span data-ttu-id="b01e8-136">Po ukończeniu działania skryptu, zatrzymać i ponownie uruchomić usługa harmonogramu zadań HPC, wpisując następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="b01e8-136">After the script completes, stop and restart the HPC Job Scheduler Service by typing the following commands:</span></span>
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-the-hpc-pack-client-utilities-on-an-on-premises-computer"></a><span data-ttu-id="b01e8-137">Krok 2: Zainstaluj narzędzia klienta HPC Pack na komputerze lokalnym</span><span class="sxs-lookup"><span data-stu-id="b01e8-137">Step 2: Install the HPC Pack client utilities on an on-premises computer</span></span>
<span data-ttu-id="b01e8-138">Jeśli chcesz zainstalować narzędzia klienta HPC Pack na komputerze, należy pobrać pliki instalacji HPC Pack (Instalacja pełna) z [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span><span class="sxs-lookup"><span data-stu-id="b01e8-138">If you want to install the HPC Pack client utilities on your computer, download the HPC Pack setup files (full installation) from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="b01e8-139">Po rozpoczęciu instalacji wybierz opcję instalacji dla **narzędzi klienta HPC Pack**.</span><span class="sxs-lookup"><span data-stu-id="b01e8-139">When you begin the installation, choose the setup option for the **HPC Pack client utilities**.</span></span>

<span data-ttu-id="b01e8-140">Aby użyć narzędzia klienta HPC Pack umożliwiają przesyłanie zadań do węzła głównego maszyny Wirtualnej, należy również eksportowania certyfikatu z węzła głównego i zainstaluj go na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="b01e8-140">To use the HPC Pack client tools to submit jobs to the head node VM, you also need to export a certificate from the head node and install it on the client computer.</span></span> <span data-ttu-id="b01e8-141">Certyfikat musi być w. CER format.</span><span class="sxs-lookup"><span data-stu-id="b01e8-141">The certificate must be in .CER format.</span></span>

<span data-ttu-id="b01e8-142">**Aby wyeksportować certyfikat z węzła głównego**</span><span class="sxs-lookup"><span data-stu-id="b01e8-142">**To export the certificate from the head node**</span></span>

1. <span data-ttu-id="b01e8-143">W węźle głównym Dodaj przystawkę Certyfikaty do programu Microsoft Management Console dla konta komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="b01e8-143">On the head node, add the Certificates snap-in to a Microsoft Management Console for the Local Computer account.</span></span> <span data-ttu-id="b01e8-144">Aby uzyskać instrukcje dotyczące dodawania przystawki, zobacz [Dodawanie przystawki Certyfikaty do programu MMC](https://technet.microsoft.com/library/cc754431.aspx).</span><span class="sxs-lookup"><span data-stu-id="b01e8-144">For steps to add the snap-in, see [Add the Certificates Snap-in to an MMC](https://technet.microsoft.com/library/cc754431.aspx).</span></span>
2. <span data-ttu-id="b01e8-145">W drzewie konsoli rozwiń węzeł **certyfikaty — komputer lokalny** > **osobistych**, a następnie kliknij przycisk **certyfikaty**.</span><span class="sxs-lookup"><span data-stu-id="b01e8-145">In the console tree, expand **Certificates – Local Computer** > **Personal**, and then click **Certificates**.</span></span>
3. <span data-ttu-id="b01e8-146">Zlokalizować certyfikatu, który skonfigurowany dla składników sieci web HPC Pack w [krok 1: Instalowanie i konfigurowanie składników sieci web w węźle głównym](#step-1:-install-and-configure-the-web-components-on-the-head-node) (na przykład, CN =&lt;*HeadNodeDnsName* &gt;. cloudapp.net).</span><span class="sxs-lookup"><span data-stu-id="b01e8-146">Locate the certificate that you configured for the HPC Pack web components in [Step 1: Install and configure the web components on the head node](#step-1:-install-and-configure-the-web-components-on-the-head-node) (for example, CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net).</span></span>
4. <span data-ttu-id="b01e8-147">Kliknij prawym przyciskiem myszy certyfikat, a następnie kliknij przycisk **wszystkie zadania** > **wyeksportować**.</span><span class="sxs-lookup"><span data-stu-id="b01e8-147">Right-click the certificate, and click **All Tasks** > **Export**.</span></span>
5. <span data-ttu-id="b01e8-148">W Kreatorze eksportu certyfikatów kliknij **dalej**i upewnij się, że **nie eksportuj klucza prywatnego** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="b01e8-148">In the Certificate Export Wizard, click **Next**, and ensure that **No, do not export the private key** is selected.</span></span>
6. <span data-ttu-id="b01e8-149">Wykonaj pozostałe kroki kreatora, aby wyeksportować certyfikat w certyfikat x.509 szyfrowany binarnie algorytmem DER (. Format CER).</span><span class="sxs-lookup"><span data-stu-id="b01e8-149">Follow the remaining steps of the wizard to export the certificate in DER encoded binary X.509 (.CER) format.</span></span>

<span data-ttu-id="b01e8-150">**Aby zaimportować certyfikat na komputerze klienckim**</span><span class="sxs-lookup"><span data-stu-id="b01e8-150">**To import the certificate on the client computer**</span></span>

1. <span data-ttu-id="b01e8-151">Skopiuj certyfikat, który został wyeksportowany z węzła głównego do folderu na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="b01e8-151">Copy the certificate that you exported from the head node to a folder on the client computer.</span></span>
2. <span data-ttu-id="b01e8-152">Uruchom certmgr.msc na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="b01e8-152">On the client computer, run certmgr.msc.</span></span>
3. <span data-ttu-id="b01e8-153">Rozwiń węzeł w Menedżerze certyfikatów **Certyfikaty — bieżący użytkownik** > **zaufane główne urzędy certyfikacji**, kliknij prawym przyciskiem myszy **certyfikaty**, a następnie Kliknij przycisk **wszystkie zadania** > **importu**.</span><span class="sxs-lookup"><span data-stu-id="b01e8-153">In Certificate Manager, expand **Certificates – Current user** > **Trusted Root Certification Authorities**, right-click **Certificates**, and then click **All Tasks** > **Import**.</span></span>
4. <span data-ttu-id="b01e8-154">Kreatora importu certyfikatów kliknij **dalej** i wykonaj kroki, aby zaimportować certyfikat, który został wyeksportowany z węzłem głównym w magazynie zaufanych głównych urzędów certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="b01e8-154">In the Certificate Import Wizard, click **Next** and follow the steps to import the certificate that you exported from the head node to the Trusted Root Certification Authorities store.</span></span>

> [!TIP]
> <span data-ttu-id="b01e8-155">Może pojawić się ostrzeżenie, ponieważ urzędu certyfikacji w węźle głównym nie jest rozpoznawane przez komputer kliencki.</span><span class="sxs-lookup"><span data-stu-id="b01e8-155">You might see a security warning, because the certification authority on the head node isn't recognized by the client computer.</span></span> <span data-ttu-id="b01e8-156">Do celów testowych, możesz zignorować to ostrzeżenie i ukończenie importu certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="b01e8-156">For testing purposes, you can ignore this warning and complete the certificate import.</span></span>
> 
> 

## <a name="step-3-run-test-jobs-on-the-cluster"></a><span data-ttu-id="b01e8-157">Krok 3: Uruchamianie testu zadań w klastrze</span><span class="sxs-lookup"><span data-stu-id="b01e8-157">Step 3: Run test jobs on the cluster</span></span>
<span data-ttu-id="b01e8-158">Aby sprawdzić konfigurację, spróbuj uruchomionych zadań w klastrze na platformie Azure z komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="b01e8-158">To verify your configuration, try running jobs on the cluster in Azure from the on-premises computer.</span></span> <span data-ttu-id="b01e8-159">Na przykład można użyć narzędzia HPC Pack GUI lub poleceń wiersza polecenia do przesyłania zadań do klastra.</span><span class="sxs-lookup"><span data-stu-id="b01e8-159">For example, you can use HPC Pack GUI tools or command-line commands to submit jobs to the cluster.</span></span> <span data-ttu-id="b01e8-160">Portal sieci web służy także do przesyłania zadań.</span><span class="sxs-lookup"><span data-stu-id="b01e8-160">You can also use a web-based portal to submit jobs.</span></span>

<span data-ttu-id="b01e8-161">**Aby uruchomić polecenia przesyłania zadań na komputerze klienckim**</span><span class="sxs-lookup"><span data-stu-id="b01e8-161">**To run job submission commands on the client computer**</span></span>

1. <span data-ttu-id="b01e8-162">Na komputerze klienckim, w którym są zainstalowane narzędzia klienta HPC Pack należy uruchomić wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="b01e8-162">On a client computer where the HPC Pack client utilities are installed, start a Command Prompt.</span></span>
2. <span data-ttu-id="b01e8-163">Wpisz polecenie przykładowe.</span><span class="sxs-lookup"><span data-stu-id="b01e8-163">Type a sample command.</span></span> <span data-ttu-id="b01e8-164">Na przykład aby wyświetlić listę wszystkich zadań w klastrze, wpisz polecenie podobne do jednej z następujących czynności, w zależności od węzła głównego pełną nazwę DNS:</span><span class="sxs-lookup"><span data-stu-id="b01e8-164">For example, to list all jobs on the cluster, type a command similar to one of the following, depending on the full DNS name of the head node:</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    <span data-ttu-id="b01e8-165">lub</span><span class="sxs-lookup"><span data-stu-id="b01e8-165">or</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > <span data-ttu-id="b01e8-166">Pełna nazwa DNS węzła głównego, a nie adres IP, należy użyć w adresie URL harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="b01e8-166">Use the full DNS name of the head node, not the IP address, in the scheduler URL.</span></span> <span data-ttu-id="b01e8-167">Jeśli określony adres IP, pojawia się błąd podobny do "certyfikat serwera musi mieć prawidłowy łańcuch zaufania lub umieszczone w magazynie zaufanych certyfikatów głównych."</span><span class="sxs-lookup"><span data-stu-id="b01e8-167">If you specify the IP address, an error appears similar to "The server certificate needs to either have a valid chain of trust or to be placed in the trusted root store."</span></span>
   > 
   > 
3. <span data-ttu-id="b01e8-168">Po wyświetleniu monitu wpisz nazwę użytkownika (w postaci &lt;DomainName&gt;\\&lt;UserName&gt;) i hasło administratora klastrów HPC lub innego użytkownika klastra skonfigurowanego.</span><span class="sxs-lookup"><span data-stu-id="b01e8-168">When prompted, type the user name (in the form &lt;DomainName&gt;\\&lt;UserName&gt;) and password of the HPC cluster administrator or another cluster user that you configured.</span></span> <span data-ttu-id="b01e8-169">Można zapisać poświadczenia lokalnie dla kolejnych operacjach zadania.</span><span class="sxs-lookup"><span data-stu-id="b01e8-169">You can choose to store the credentials locally for more job operations.</span></span>
   
    <span data-ttu-id="b01e8-170">Zostanie wyświetlona lista zadań.</span><span class="sxs-lookup"><span data-stu-id="b01e8-170">A list of jobs appears.</span></span>

<span data-ttu-id="b01e8-171">**Na komputerze klienckim za pomocą Menedżera zadań HPC**</span><span class="sxs-lookup"><span data-stu-id="b01e8-171">**To use HPC Job Manager on the client computer**</span></span>

1. <span data-ttu-id="b01e8-172">Jeśli wcześniej nie przechowują poświadczeń domeny użytkownika, klastra, podczas przesyłania zadania, można dodać poświadczeń w Menedżerze poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="b01e8-172">If you didn't previously store domain credentials for a cluster user when submitting a job, you can add the credentials in Credential Manager.</span></span>
   
    <span data-ttu-id="b01e8-173">a.</span><span class="sxs-lookup"><span data-stu-id="b01e8-173">a.</span></span> <span data-ttu-id="b01e8-174">W Panelu sterowania na komputerze klienckim otwórz Menedżera poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="b01e8-174">In Control Panel on the client computer, start Credential Manager.</span></span>
   
    <span data-ttu-id="b01e8-175">b.</span><span class="sxs-lookup"><span data-stu-id="b01e8-175">b.</span></span> <span data-ttu-id="b01e8-176">Kliknij przycisk **poświadczeń systemu Windows** > **Dodaj poświadczenie ogólnego**.</span><span class="sxs-lookup"><span data-stu-id="b01e8-176">Click **Windows Credentials** > **Add a generic credential**.</span></span>
   
    <span data-ttu-id="b01e8-177">c.</span><span class="sxs-lookup"><span data-stu-id="b01e8-177">c.</span></span> <span data-ttu-id="b01e8-178">Określ adres internetowy (na przykład https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler lub https://&lt;HeadNodeDnsName&gt;.&lt; region&gt;.cloudapp.azure.com/HpcScheduler) oraz nazwy użytkownika (&lt;DomainName&gt;\\&lt;UserName&gt;) i hasło administratora klastra lub innego użytkownika klastra, który został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="b01e8-178">Specify the Internet address (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com/HpcScheduler), and the user name (&lt;DomainName&gt;\\&lt;UserName&gt;) and password of the cluster administrator or another cluster user that you configured.</span></span>
2. <span data-ttu-id="b01e8-179">Na komputerze klienckim, aby uruchomić Menedżer zadań klastra HPC.</span><span class="sxs-lookup"><span data-stu-id="b01e8-179">On the client computer, start HPC Job Manager.</span></span>
3. <span data-ttu-id="b01e8-180">W **wybierz węzeł Head** okna dialogowego, wpisz adres URL węzła głównego na platformie Azure (na przykład https://&lt;HeadNodeDnsName&gt;. cloudapp.net lub https://&lt;HeadNodeDnsName&gt;.&lt; region&gt;. cloudapp.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b01e8-180">In the **Select Head Node** dialog box, type the URL to the head node in Azure (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com).</span></span>
   
    <span data-ttu-id="b01e8-181">Menedżer zadań klastra HPC otwiera i zawiera listę zadań z węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="b01e8-181">HPC Job Manager opens and shows a list of jobs on the head node.</span></span>

<span data-ttu-id="b01e8-182">**Aby korzystać z portalu sieci web uruchomiona w węźle głównym**</span><span class="sxs-lookup"><span data-stu-id="b01e8-182">**To use the web portal running on the head node**</span></span>

1. <span data-ttu-id="b01e8-183">Uruchom przeglądarkę sieci web na komputerze klienckim i wprowadź jedno z następujących adresów, w zależności od węzła głównego pełną nazwę DNS:</span><span class="sxs-lookup"><span data-stu-id="b01e8-183">Start a web browser on the client computer, and enter one of the following addresses, depending on the full DNS name of the head node:</span></span>
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    <span data-ttu-id="b01e8-184">lub</span><span class="sxs-lookup"><span data-stu-id="b01e8-184">or</span></span>
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. <span data-ttu-id="b01e8-185">W oknie dialogowym Zabezpieczenia wpisz poświadczenia domeny administratora klastra HPC.</span><span class="sxs-lookup"><span data-stu-id="b01e8-185">In the security dialog box that appears, type the domain credentials of the HPC cluster administrator.</span></span> <span data-ttu-id="b01e8-186">(Można również dodać innych klastra użytkowników w różnych ról.</span><span class="sxs-lookup"><span data-stu-id="b01e8-186">(You can also add other cluster users in different roles.</span></span> <span data-ttu-id="b01e8-187">Zobacz [Zarządzanie użytkownikami klastra](https://technet.microsoft.com/library/ff919335.aspx).)</span><span class="sxs-lookup"><span data-stu-id="b01e8-187">See [Managing Cluster Users](https://technet.microsoft.com/library/ff919335.aspx).)</span></span>
   
    <span data-ttu-id="b01e8-188">Portal sieci web zostanie otwarty widok listy zadań.</span><span class="sxs-lookup"><span data-stu-id="b01e8-188">The web portal opens to the job list view.</span></span>
3. <span data-ttu-id="b01e8-189">Aby przesłać zadanie próbki, która zwraca ciąg "Hello World" z klastra, kliknij przycisk **nowe zadanie** w obszarze nawigacji po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="b01e8-189">To submit a sample job that returns the string “Hello World” from the cluster, click **New job** in the left-hand navigation.</span></span>
4. <span data-ttu-id="b01e8-190">Na **nowe zadanie** w obszarze **ze stron przesyłania**, kliknij przycisk **HelloWorld**.</span><span class="sxs-lookup"><span data-stu-id="b01e8-190">On the **New Job** page, under **From submission pages**, click **HelloWorld**.</span></span> <span data-ttu-id="b01e8-191">Zostanie wyświetlona strona przesyłania zadania.</span><span class="sxs-lookup"><span data-stu-id="b01e8-191">The job submission page appears.</span></span>
5. <span data-ttu-id="b01e8-192">Kliknij przycisk **przesłać**.</span><span class="sxs-lookup"><span data-stu-id="b01e8-192">Click **Submit**.</span></span> <span data-ttu-id="b01e8-193">Po wyświetleniu monitu podaj poświadczenia domeny administratora klastra HPC.</span><span class="sxs-lookup"><span data-stu-id="b01e8-193">If prompted, provide the domain credentials of the HPC cluster administrator.</span></span> <span data-ttu-id="b01e8-194">Zadanie, a identyfikator zadania są wyświetlane na **Moje zadania** strony.</span><span class="sxs-lookup"><span data-stu-id="b01e8-194">The job is submitted, and the job ID appears on the **My Jobs** page.</span></span>
6. <span data-ttu-id="b01e8-195">Aby wyświetlić wyniki zadania, który zostanie przesłany, kliknij Identyfikatora zadania, a następnie kliknij **zadania widoku** do wyświetlania danych wyjściowych polecenia (w obszarze **dane wyjściowe**).</span><span class="sxs-lookup"><span data-stu-id="b01e8-195">To view the results of the job that you submitted, click the job ID, and then click **View Tasks** to view the command output (under **Output**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b01e8-196">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b01e8-196">Next steps</span></span>
* <span data-ttu-id="b01e8-197">Istnieje także możliwość przesyłania zadań do klastra platformy Azure z [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="b01e8-197">You can also submit jobs to the Azure cluster with the [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span>
* <span data-ttu-id="b01e8-198">Jeśli chcesz przesłać zadań klastra z klientów systemu Linux, zobacz próbki Python w [HPC Pack 2012 R2 SDK oraz przykładowy kod](https://www.microsoft.com/download/details.aspx?id=41633).</span><span class="sxs-lookup"><span data-stu-id="b01e8-198">If you want to submit cluster jobs from a Linux client, see the Python sample in the [HPC Pack 2012 R2 SDK and Sample Code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span>

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png
