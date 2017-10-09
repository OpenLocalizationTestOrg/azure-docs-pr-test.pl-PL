---
title: "aaaUse PowerShell tooCreate maszyny Wirtualnej z macierzysty tryb serwera raportów | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano i przedstawiono hello wdrażania i konfiguracji serwera raportów usług SQL Server Reporting Services w trybie macierzystym w maszynie wirtualnej platformy Azure. "
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 553af55b-d02e-4e32-904c-682bfa20fa0f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: e7791199c87dff106132f1535da12de40a8dbc9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-vm-with-a-native-mode-report-server"></a><span data-ttu-id="2b6a0-103">Użyj programu PowerShell tooCreate Azure maszyny Wirtualnej z macierzysty tryb serwera raportów</span><span class="sxs-lookup"><span data-stu-id="2b6a0-103">Use PowerShell tooCreate an Azure VM With a Native Mode Report Server</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="2b6a0-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2b6a0-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="2b6a0-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="2b6a0-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="2b6a0-107">W tym temacie opisano i przedstawiono hello wdrażania i konfiguracji serwera raportów usług SQL Server Reporting Services w trybie macierzystym w maszynie wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-107">This topic describes and walks you through hello deployment and configuration of a SQL Server Reporting Services native mode report server in an Azure Virtual Machine.</span></span> <span data-ttu-id="2b6a0-108">Witaj kroków w tym dokumencie kombinacja maszyny wirtualnej hello toocreate ręczne i skrypt programu Windows PowerShell tooconfigure Reporting Services na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-108">hello steps in this document use a combination of manual steps toocreate hello virtual machine and a Windows PowerShell script tooconfigure Reporting Services on hello VM.</span></span> <span data-ttu-id="2b6a0-109">Skrypt konfiguracji Hello obejmuje otwierania portu zapory dla protokołu HTTP lub HTTPs.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-109">hello configuration script includes opening a firewall port for HTTP or HTTPs.</span></span>

> [!NOTE]
> <span data-ttu-id="2b6a0-110">Jeśli nie wymagają **HTTPS** na powitania serwera raportów, **pominąć krok 2**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-110">If you do not require **HTTPS** on hello report server, **skip step 2**.</span></span>
> 
> <span data-ttu-id="2b6a0-111">Po utworzeniu hello maszyny Wirtualnej w kroku 1, przejdź toohello sekcji Użyj skryptu tooconfigure hello raportu serwera i protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-111">After creating hello VM in step 1, go toohello section Use script tooconfigure hello report server and HTTP.</span></span> <span data-ttu-id="2b6a0-112">Po uruchomieniu skryptu hello powitania serwera raportów jest gotowy toouse.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-112">After you run hello script, hello report server is ready toouse.</span></span>

## <a name="prerequisites-and-assumptions"></a><span data-ttu-id="2b6a0-113">Wymagania wstępne i założenia</span><span class="sxs-lookup"><span data-stu-id="2b6a0-113">Prerequisites and Assumptions</span></span>
* <span data-ttu-id="2b6a0-114">**Subskrypcja platformy Azure**: Sprawdź hello liczba rdzeni dostępne w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-114">**Azure Subscription**: Verify hello number of cores available in your Azure Subscription.</span></span> <span data-ttu-id="2b6a0-115">Jeśli utworzysz zalecany rozmiar maszyny Wirtualnej hello **A3**, należy **4** dostępne rdzenie.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-115">If you create hello recommended VM size of **A3**, you need **4** available cores.</span></span> <span data-ttu-id="2b6a0-116">Jeśli używasz rozmiar maszyny Wirtualnej **A2**, należy **2** dostępne rdzenie.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-116">If you use a VM size of **A2**, you need **2** available cores.</span></span>
  
  * <span data-ttu-id="2b6a0-117">w menu u góry hello tooverify hello limit rdzeni w subskrypcji w hello klasycznego portalu Azure, kliknij w okienku po lewej stronie powitania, a następnie kliknij przycisk użycia ustawienia.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-117">tooverify hello core limit of your subscription, in hello Azure classic portal, click SETTINGS in hello left pane and then Click USAGE in hello top menu.</span></span>
  * <span data-ttu-id="2b6a0-118">tooincrease hello limit przydziału rdzeni, skontaktuj się z pomocą [pomocą techniczną platformy Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="2b6a0-118">tooincrease hello core quota, contact [Azure Support](https://azure.microsoft.com/support/options/).</span></span> <span data-ttu-id="2b6a0-119">Uzyskać rozmiaru maszyny Wirtualnej, zobacz [rozmiarów maszyn wirtualnych na platformie Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2b6a0-119">For VM size information, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="2b6a0-120">**Windows PowerShell do obsługi skryptów**: hello temacie założono, że masz podstawową wiedzę na temat pracy programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-120">**Windows PowerShell Scripting**: hello topic assumes that you have a basic working knowledge of Windows PowerShell.</span></span> <span data-ttu-id="2b6a0-121">Aby uzyskać więcej informacji o korzystaniu z programu Windows PowerShell zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-121">For more information about using Windows PowerShell, see hello following:</span></span>
  
  * [<span data-ttu-id="2b6a0-122">Uruchamianie środowiska Windows PowerShell w systemie Windows Server</span><span class="sxs-lookup"><span data-stu-id="2b6a0-122">Starting Windows PowerShell on Windows Server</span></span>](https://technet.microsoft.com/library/hh847814.aspx)
  * [<span data-ttu-id="2b6a0-123">Wprowadzenie do korzystania z programu Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="2b6a0-123">Getting Started with Windows PowerShell</span></span>](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a><span data-ttu-id="2b6a0-124">Krok 1: Udostępnić maszynie wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2b6a0-124">Step 1: Provision an Azure Virtual Machine</span></span>
1. <span data-ttu-id="2b6a0-125">Przeglądaj toohello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-125">Browse toohello Azure classic portal.</span></span>
2. <span data-ttu-id="2b6a0-126">Kliknij przycisk **maszyn wirtualnych** w okienku po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-126">Click **Virtual Machines** in hello left pane.</span></span>
   
    ![maszyny wirtualne Microsoft azure](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. <span data-ttu-id="2b6a0-128">Kliknij przycisk **Nowy**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-128">Click **New**.</span></span>
   
    ![Przycisk Nowy](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. <span data-ttu-id="2b6a0-130">Kliknij przycisk **z galerii**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-130">Click **From Gallery**.</span></span>
   
    ![Nowa maszyna wirtualna z galerii](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. <span data-ttu-id="2b6a0-132">Kliknij przycisk **SQL Server 2014 RTM Standard — Windows Server 2012 R2** a następnie kliknij przycisk hello toocontinue strzałki.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-132">Click **SQL Server 2014 RTM Standard – Windows Server 2012 R2** and then click hello arrow toocontinue.</span></span>
   
    ![Dalej](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    <span data-ttu-id="2b6a0-134">Jeśli potrzebujesz danych usług Reporting Services hello zmiennych funkcji subskrypcji, wybierz **programu SQL Server 2014 RTM Enterprise — Windows Server 2012 R2**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-134">If you need hello Reporting Services data driven subscriptions feature, choose **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span></span> <span data-ttu-id="2b6a0-135">Aby uzyskać więcej informacji o wersjach programu SQL Server i obsługę funkcji, zobacz [funkcje obsługiwane przez wersje programu SQL Server 2012 hello](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span><span class="sxs-lookup"><span data-stu-id="2b6a0-135">For more information on SQL Server editions and feature support, see [Features Supported by hello Editions of SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span></span>
6. <span data-ttu-id="2b6a0-136">Na powitania **konfiguracji maszyny wirtualnej** Edytuj hello następujące pola:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-136">On hello **Virtual machine configuration** page, edit hello following fields:</span></span>
   
   * <span data-ttu-id="2b6a0-137">Jeśli istnieje więcej niż jeden **Data wydania wersji**, wybierz hello najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-137">If there is more than one **VERSION RELEASE DATE**, select hello most recent version.</span></span>
   * <span data-ttu-id="2b6a0-138">**Nazwa maszyny wirtualnej**: Nazwa komputera hello jest również używany na następnej stronie konfiguracji hello jako hello domyślną nazwę DNS usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-138">**Virtual Machine Name**: hello machine name is also used on hello next configuration page as hello default Cloud Service DNS name.</span></span> <span data-ttu-id="2b6a0-139">Nazwa DNS Hello musi być unikatowa w hello usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-139">hello DNS name must be unique across hello Azure service.</span></span> <span data-ttu-id="2b6a0-140">Rozważ skonfigurowanie hello maszyny Wirtualnej przy użyciu nazwy komputera, który opisuje jakie hello maszyna wirtualna jest używana do.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-140">Consider configuring hello VM with a computer name that describes what hello VM is used for.</span></span> <span data-ttu-id="2b6a0-141">Na przykład ssrsnativecloud.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-141">For example ssrsnativecloud.</span></span>
   * <span data-ttu-id="2b6a0-142">**Warstwa**: standardowy</span><span class="sxs-lookup"><span data-stu-id="2b6a0-142">**Tier**: Standard</span></span>
   * <span data-ttu-id="2b6a0-143">**Rozmiar: A3** hello zaleca się rozmiar maszyny Wirtualnej dla obciążeń programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-143">**Size:A3** is hello recommended VM size for SQL Server workloads.</span></span> <span data-ttu-id="2b6a0-144">Jeśli maszyna wirtualna jest używana tylko jako serwer raportów maszyny Wirtualnej o rozmiarze A2 jest wystarczająca, chyba że serwer raportów hello napotyka duże obciążenie.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-144">If a VM is only used as a report server, a VM size of A2 is sufficient unless hello report server experiences a large workload.</span></span> <span data-ttu-id="2b6a0-145">Dla maszyny Wirtualnej, informacje o cenach, zobacz [cennik maszyn wirtualnych](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="2b6a0-145">For VM pricing information, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>
   * <span data-ttu-id="2b6a0-146">**Nową nazwę użytkownika**: należy podać nazwę hello jest tworzony jako administrator na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-146">**New User Name**: hello name you provide is created as an administrator on hello VM.</span></span>
   * <span data-ttu-id="2b6a0-147">**Nowe hasło** i **potwierdzić**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-147">**New Password** and **confirm**.</span></span> <span data-ttu-id="2b6a0-148">To hasło służy do nowego konta administratora hello i zaleca się, że używasz silne hasło.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-148">This password is used for hello new administrator account and it is recommended you use a strong password.</span></span>
   * <span data-ttu-id="2b6a0-149">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-149">Click **Next**.</span></span> <span data-ttu-id="2b6a0-150">![dalej](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span><span class="sxs-lookup"><span data-stu-id="2b6a0-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span></span>
7. <span data-ttu-id="2b6a0-151">Na następnej stronie powitania edytować hello następujące pola:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-151">On hello next page, edit hello following fields:</span></span>
   
   * <span data-ttu-id="2b6a0-152">**Usługi w chmurze**: Wybierz **Utwórz nową usługę w chmurze**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-152">**Cloud Service**: select **Create a new Cloud Service**.</span></span>
   * <span data-ttu-id="2b6a0-153">**Nazwa DNS usługi w chmurze**: jest to hello publicznej nazwy DNS hello usługę Chmurową, która jest skojarzona z hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-153">**Cloud Service DNS Name**: This is hello public DNS name of hello Cloud Service that is associated with hello VM.</span></span> <span data-ttu-id="2b6a0-154">Hello domyślna nazwa jest hello wpisane hello nazwy maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-154">hello default name is hello name you typed in for hello VM name.</span></span> <span data-ttu-id="2b6a0-155">Jeśli w kolejnych krokach tematu hello, utworzysz zaufany certyfikat SSL, a następnie nazwy DNS hello jest używany dla wartości hello hello "**wystawiony dla**" hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-155">If in later steps of hello topic, you create a trusted SSL certificate and then hello DNS name is used for hello value of hello “**Issued to**” of hello certificate.</span></span>
   * <span data-ttu-id="2b6a0-156">**Region/koligacji grupy/wirtualnej sieci**: Wybierz hello region najbliższy tooyour użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-156">**Region/Affinity Group/Virtual Network**: Choose hello region closest tooyour end users.</span></span>
   * <span data-ttu-id="2b6a0-157">**Konto magazynu**: Użyj konta magazynu wygenerowanej automatycznie.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-157">**Storage Account**: Use an automatically generated storage account.</span></span>
   * <span data-ttu-id="2b6a0-158">**Zestaw dostępności**: Brak.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-158">**Availability Set**: None.</span></span>
   * <span data-ttu-id="2b6a0-159">**Punkty końcowe** hello Zachowaj **pulpitu zdalnego** i **PowerShell** punktów końcowych, a następnie dodaj końcowy HTTP lub HTTPS, w zależności od środowiska.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-159">**ENDPOINTS** Keep hello **Remote Desktop** and **PowerShell** endpoints and then add either an HTTP or HTTPS endpoint, depending on your environment.</span></span>
     
     * <span data-ttu-id="2b6a0-160">**HTTP**: hello domyślne porty publiczne i prywatne są **80**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-160">**HTTP**: hello default public and private ports are **80**.</span></span> <span data-ttu-id="2b6a0-161">Należy pamiętać, że jeśli korzystanie z prywatnych portu innego niż 80, zmodyfikuj **$HTTPport = 80** hello http skryptu.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-161">Note that if you use a private port other than 80, modify **$HTTPport = 80** in hello http script.</span></span>
     * <span data-ttu-id="2b6a0-162">**HTTPS**: hello domyślne porty publiczne i prywatne są **443**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-162">**HTTPS**: hello default public and private ports are **443**.</span></span> <span data-ttu-id="2b6a0-163">Ze względów bezpieczeństwa jest port prywatny hello toochange i skonfigurować zapory i hello raportu server toouse hello prywatnych portów.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-163">A security best practice is toochange hello private port and configure your firewall and hello report server toouse hello private port.</span></span> <span data-ttu-id="2b6a0-164">Aby uzyskać więcej informacji dotyczących punktów końcowych, zobacz [jak tooSet komunikacji się z maszyną wirtualną](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2b6a0-164">For more information on endpoints, see [How tooSet Up Communication with a Virtual Machine](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="2b6a0-165">Należy pamiętać, że jeśli użyjesz portu innego niż 443, Zmień parametr hello **$HTTPsport = 443** w hello skryptu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-165">Note that if you use a port other than 443, change hello parameter **$HTTPsport = 443** in hello HTTPS script.</span></span>
   * <span data-ttu-id="2b6a0-166">Kliknij przycisk Dalej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-166">Click next .</span></span> ![Dalej](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. <span data-ttu-id="2b6a0-168">Na powitania ostatniej stronie kreatora hello, zachowaj domyślne hello **instalacji agenta maszyny Wirtualnej hello** wybrane.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-168">On hello last page of hello wizard, keep hello default **Install hello VM agent** selected.</span></span> <span data-ttu-id="2b6a0-169">Witaj kroki opisane w tym temacie, nie będą korzystać hello agenta maszyny Wirtualnej, ale jeśli planujesz tookeep tej maszyny Wirtualnej, agent maszyny Wirtualnej hello i rozszerzenia pozwoli tooenhance he CM.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-169">hello steps in this topic do not utilize hello VM agent but if you plan tookeep this VM, hello VM agent and extensions will allow you tooenhance he CM.</span></span>  <span data-ttu-id="2b6a0-170">Aby uzyskać więcej informacji na powitania agenta maszyny Wirtualnej, zobacz [agenta maszyny Wirtualnej i rozszerzenia — część 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span><span class="sxs-lookup"><span data-stu-id="2b6a0-170">For more information on hello VM agent, see [VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span></span> <span data-ttu-id="2b6a0-171">Jeden AD zainstalowanych rozszerzeń domyślne hello uruchomiona jest rozszerzenie "BGINFO" hello, który wyświetla na pulpicie maszyny Wirtualnej hello, informacje o systemie, takie jak wewnętrznym adresem IP i free dysków miejsca.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-171">One of hello default extensions installed ad running is hello “BGINFO” extension that displays on hello VM desktop, system information such as internal IP and free drive space.</span></span>
9. <span data-ttu-id="2b6a0-172">Kliknij polecenie ukończone.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-172">Click complete .</span></span> ![Ok](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. <span data-ttu-id="2b6a0-174">Hello **stan** z maszyny Wirtualnej będzie wyświetlany jako hello **uruchamianie (inicjowania obsługi administracyjnej)** podczas procesu udostępniania hello i następnie wyświetlana **systemem** gdy hello maszyny Wirtualnej jest zainicjowana i gotowa toouse.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-174">hello **Status** of hello VM displays as **Starting (Provisioning)** during hello provision process and then displays as **Running** when hello VM is provisioned and ready toouse.</span></span>

## <a name="step-2-create-a-server-certificate"></a><span data-ttu-id="2b6a0-175">Krok 2: Utworzenie certyfikatu serwera</span><span class="sxs-lookup"><span data-stu-id="2b6a0-175">Step 2: Create a Server Certificate</span></span>
> [!NOTE]
> <span data-ttu-id="2b6a0-176">Jeśli nie wymagają protokołu HTTPS na powitania serwera raportów, możesz **pominąć krok 2** i przejdź do sekcji toohello **używać serwera raportów hello tooconfigure skryptu i HTTP**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-176">If you do not require HTTPS on hello report server, you can **skip step 2** and go toohello section **Use script tooconfigure hello report server and HTTP**.</span></span> <span data-ttu-id="2b6a0-177">Użyj hello HTTP skryptu tooquickly skonfigurować powitania serwera raportów i raportu hello się, że serwer będzie gotowy toouse.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-177">Use hello HTTP script tooquickly configure hello report server and hello report server will be ready toouse.</span></span>

<span data-ttu-id="2b6a0-178">W kolejności toouse HTTPS na powitania maszyny Wirtualnej należy zaufany certyfikat SSL.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-178">In order toouse HTTPS on hello VM, you need a trusted SSL certificate.</span></span> <span data-ttu-id="2b6a0-179">W zależności od scenariusza należy użyć hello następujących dwóch metod:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-179">Depending on your scenario, you can use one of hello following two methods:</span></span>

* <span data-ttu-id="2b6a0-180">Prawidłowy certyfikat SSL wystawiony przez urząd certyfikacji (CA) i zaufany przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-180">A valid SSL certificate issued by a Certification Authority (CA) and trusted by Microsoft.</span></span> <span data-ttu-id="2b6a0-181">certyfikaty głównego urzędu certyfikacji Hello są wymagane toobe dystrybuowane za pośrednictwem hello programu certyfikatów głównych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-181">hello CA root certificates are required toobe distributed via hello Microsoft Root Certificate Program.</span></span> <span data-ttu-id="2b6a0-182">Aby uzyskać więcej informacji na temat tego programu, zobacz [systemu Windows i Windows Phone 8 SSL programu certyfikatów głównych (elementu członkowskiego CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) i [toohello wprowadzenie programu certyfikatów głównych firmy Microsoft](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b6a0-182">For more information about this program, see [Windows and Windows Phone 8 SSL Root Certificate Program (Member CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) and [Introduction toohello Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span></span>
* <span data-ttu-id="2b6a0-183">Certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-183">A self-signed certificate.</span></span> <span data-ttu-id="2b6a0-184">Certyfikaty z podpisem własnym nie jest zalecana dla środowisk produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-184">Self-signed certificates are not recommended for production environments.</span></span>

### <a name="toouse-a-certificate-created-by-a-trusted-certificate-authority-ca"></a><span data-ttu-id="2b6a0-185">toouse certyfikat, który został utworzony przez zaufany urząd certyfikacji</span><span class="sxs-lookup"><span data-stu-id="2b6a0-185">toouse a certificate created by a trusted Certificate Authority (CA)</span></span>
1. <span data-ttu-id="2b6a0-186">**Żądanie certyfikatu serwera dla witryny sieci Web powitania od urzędu certyfikacji**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-186">**Request a server certificate for hello website from a certification authority**.</span></span> 
   
    <span data-ttu-id="2b6a0-187">Możesz użyć hello Kreator certyfikatu serwera sieci Web albo toogenerate pliku żądania certyfikatu (Certreq.txt) wysłanie tooa urzędu certyfikacji lub toogenerate żądania dla urzędu certyfikacji w trybie online.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-187">You can use hello Web Server Certificate Wizard either toogenerate a certificate request file (Certreq.txt) that you send tooa certification authority, or toogenerate a request for an online certification authority.</span></span> <span data-ttu-id="2b6a0-188">Na przykład usług certyfikatów firmy Microsoft w systemie Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-188">For example, Microsoft Certificate Services in Windows Server 2012.</span></span> <span data-ttu-id="2b6a0-189">W zależności od poziomu hello wiarygodności identyfikacji oferowanego przez dany certyfikat serwera jest kilku miesięcy tooseveral dni tooapprove urzędu certyfikacji hello żądania i wysłać do użytkownika plik certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-189">Depending on hello level of identification assurance offered by your server certificate, it is several days tooseveral months for hello certification authority tooapprove your request and send you a certificate file.</span></span> 
   
    <span data-ttu-id="2b6a0-190">Aby uzyskać więcej informacji na temat żądania certyfikatów serwera zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-190">For more information about requesting a server certificates, see hello following:</span></span> 
   
   * <span data-ttu-id="2b6a0-191">Użyj [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b6a0-191">Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span></span>
   * <span data-ttu-id="2b6a0-192">TooAdminister narzędzi zabezpieczeń systemu Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-192">Security Tools tooAdminister Windows Server 2012.</span></span>
     
     [<span data-ttu-id="2b6a0-193">TooAdminister narzędzi zabezpieczeń systemu Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="2b6a0-193">Security Tools tooAdminister Windows Server 2012</span></span>](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > <span data-ttu-id="2b6a0-194">Witaj **wystawiony dla** pola hello zaufany certyfikat SSL powinien być hello sam jako hello **nazwa DNS usługi w chmurze** użyte do hello nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-194">hello **issued to** field of hello trusted SSL certificate should be hello same as hello **Cloud Service DNS NAME** you used for hello new VM.</span></span>

2. <span data-ttu-id="2b6a0-195">**Instalowanie certyfikatu serwera hello na powitania serwera sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-195">**Install hello server certificate on hello Web server**.</span></span> <span data-ttu-id="2b6a0-196">serwer sieci Web Hello jest w tym przypadku hello maszyny Wirtualnej, że hosty hello serwera raportów i hello witryna internetowa jest tworzona w kolejnych krokach, podczas konfigurowania usług Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-196">hello Web server in this case is hello VM that hosts hello report server and hello website is created in later steps when you configure Reporting Services.</span></span> <span data-ttu-id="2b6a0-197">Aby uzyskać więcej informacji dotyczących instalowania certyfikatu serwera hello na powitania serwera sieci Web za pomocą przystawki MMC certyfikatów hello, zobacz [zainstalować certyfikat serwera](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="2b6a0-197">For more information about installing hello server certificate on hello Web server by using hello Certificate MMC snap-in, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
    <span data-ttu-id="2b6a0-198">Jeśli chcesz, aby skrypt hello toouse uwzględnionych w tym temacie tooconfigure powitania serwera raportów, hello wartość certyfikatów hello **odcisk palca** są wymagane jako parametr hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-198">If you want toouse hello script included with this topic, tooconfigure hello report server, hello value of hello certificates **Thumbprint** is required as a parameter of hello script.</span></span> <span data-ttu-id="2b6a0-199">Zobacz hello następnej sekcji, aby uzyskać szczegółowe informacje na jak tooobtain hello odcisk palca certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-199">See hello next section for details on how tooobtain hello thumbprint of hello certificate.</span></span>
3. <span data-ttu-id="2b6a0-200">Przypisz raportów hello server certyfikatu toohello.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-200">Assign hello server certificate toohello report server.</span></span> <span data-ttu-id="2b6a0-201">Hello przydziałów zakończeniu w następnej sekcji hello podczas konfigurowania serwera raportów hello.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-201">hello assignment is completed in hello next section when you configure hello report server.</span></span>

### <a name="toouse-hello-virtual-machines-self-signed-certificate"></a><span data-ttu-id="2b6a0-202">Witaj toouse certyfikatu z podpisem własnym maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="2b6a0-202">toouse hello Virtual Machines Self-signed Certificate</span></span>
<span data-ttu-id="2b6a0-203">Certyfikatu z podpisem własnym został utworzony na powitania maszyny Wirtualnej podczas przydzielania został hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-203">A self-signed certificate was created on hello VM when hello VM was provisioned.</span></span> <span data-ttu-id="2b6a0-204">Witaj certyfikat ma hello takie same nazwy jako hello nazwę DNS maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-204">hello certificate has hello same name as hello VM DNS name.</span></span> <span data-ttu-id="2b6a0-205">W kolejności tooavoid błędów certyfikatów, jest wymagany certyfikat hello jest zaufany, na powitania samej maszyny Wirtualnej, a także przez wszystkich użytkowników hello lokacji.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-205">In order tooavoid certificate errors, it is required that hello certificate is trusted on hello VM itself, and also by all users of hello site.</span></span>

1. <span data-ttu-id="2b6a0-206">tootrust hello głównego urzędu certyfikacji certyfikatu hello na powitania lokalnej maszyny Wirtualnej, dodać hello certyfikatu toohello **zaufane główne urzędy certyfikacji**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-206">tootrust hello root CA of hello certificate on hello Local VM, add hello certificate toohello **Trusted Root Certification Authorities**.</span></span> <span data-ttu-id="2b6a0-207">Hello poniżej znajduje się podsumowanie hello czynności.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-207">hello following is a summary of hello steps required.</span></span> <span data-ttu-id="2b6a0-208">Aby uzyskać szczegółowe instrukcje na jak tootrust hello urzędu certyfikacji, zobacz [zainstalować certyfikat serwera](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="2b6a0-208">For detailed steps on how tootrust hello CA, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
   1. <span data-ttu-id="2b6a0-209">Z hello klasycznego portalu Azure, wybierz hello maszyny Wirtualnej, a następnie kliknij przycisk Połącz.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-209">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="2b6a0-210">W zależności od konfiguracji przeglądarki może być toosave zostanie wyświetlony monit o plik RDP do połączenia toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-210">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
      
       ![Połącz tooazure maszyny wirtualnej](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="2b6a0-212">Użyj nazwy maszyny Wirtualnej użytkownika hello, nazwę użytkownika i hasła skonfigurowanego podczas tworzenia hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-212">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
      
       <span data-ttu-id="2b6a0-213">Na przykład w hello po obraz, Nazwa maszyny Wirtualnej hello jest **ssrsnativecloud** i nazwa użytkownika hello jest **testuser**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-213">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
      
       ![Nazwa maszyny wirtualnej zawiera logowania](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. <span data-ttu-id="2b6a0-215">Uruchom mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-215">Run mmc.exe.</span></span> <span data-ttu-id="2b6a0-216">Aby uzyskać więcej informacji, zobacz [porady: wyświetlanie certyfikatów z hello przystawka programu MMC](https://msdn.microsoft.com/library/ms788967.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b6a0-216">For more information, see [How to: View Certificates with hello MMC Snap-in](https://msdn.microsoft.com/library/ms788967.aspx).</span></span>
   3. <span data-ttu-id="2b6a0-217">W aplikacji konsoli hello **pliku** menu Dodaj hello **certyfikaty** przystawki, wybierz pozycję **konto komputera** po wyświetleniu monitu, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-217">In hello console application **File** menu, add hello **Certificates** snap-in, select **Computer Account** when prompted, and then click **Next**.</span></span>
   4. <span data-ttu-id="2b6a0-218">Wybierz **komputera lokalnego** toomanage, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-218">Select **Local Computer** toomanage and then click **Finish**.</span></span>
   5. <span data-ttu-id="2b6a0-219">Kliknij przycisk **Ok** , a następnie rozwiń węzeł hello **certyfikaty - osobiste** węzłów, a następnie kliknij przycisk **certyfikaty**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-219">Click **Ok** and then expand hello **Certificates -Personal** nodes and then click **Certificates**.</span></span> <span data-ttu-id="2b6a0-220">Witaj certyfikatu jest nosi nazwę DNS hello hello maszyny Wirtualnej i kończy **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-220">hello certificate is named after hello DNS name of hello VM and ends with **cloudapp.net**.</span></span> <span data-ttu-id="2b6a0-221">Kliknij prawym przyciskiem myszy nazwę certyfikatu hello, a następnie kliknij przycisk **kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-221">Right-click hello certificate name and click **Copy**.</span></span>
   6. <span data-ttu-id="2b6a0-222">Rozwiń węzeł hello **zaufane główne urzędy certyfikacji** węzła, a następnie kliknij prawym przyciskiem myszy **certyfikaty** , a następnie kliknij przycisk **Wklej**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-222">Expand hello **Trusted Root Certification Authorities** node and then right-click **Certificates** and then click **Paste**.</span></span>
   7. <span data-ttu-id="2b6a0-223">toovalidate dwa razy kliknij nazwę certyfikatu hello w obszarze **zaufane główne urzędy certyfikacji** i sprawdź, czy nie ma żadnych błędów i wyświetlić certyfikat.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-223">toovalidate, double click on hello certificate name under **Trusted Root Certification Authorities** and verify that there are no errors and you see your certificate.</span></span> <span data-ttu-id="2b6a0-224">Jeśli chcesz, aby skrypt HTTPS hello toouse uwzględnionych w tym temacie tooconfigure powitania serwera raportów, hello wartość certyfikatów hello **odcisk palca** są wymagane jako parametr hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-224">If you want toouse hello HTTPS script included with this topic, tooconfigure hello report server, hello value of hello certificates **Thumbprint** is required as a parameter of hello script.</span></span> <span data-ttu-id="2b6a0-225">**wartość odcisku palca hello tooget**, wykonaj następujące czynności hello.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-225">**tooget hello thumbprint value**, complete hello following.</span></span> <span data-ttu-id="2b6a0-226">W sekcji również jest odcisk palca programu PowerShell próbki tooretrieve hello [użyć skryptu tooconfigure hello raportu serwera i protokołu HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span><span class="sxs-lookup"><span data-stu-id="2b6a0-226">There is also a PowerShell sample tooretrieve hello thumbprint in section [Use script tooconfigure hello report server and HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span></span>
      
      1. <span data-ttu-id="2b6a0-227">Kliknij dwukrotnie nazwę hello hello certyfikatu, na przykład ssrsnativecloud.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-227">Double-click hello name of hello certificate, for example ssrsnativecloud.cloudapp.net.</span></span>
      2. <span data-ttu-id="2b6a0-228">Kliknij przycisk hello **szczegóły** kartę.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-228">Click hello **Details** tab.</span></span>
      3. <span data-ttu-id="2b6a0-229">Kliknij przycisk **odcisk palca**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-229">Click **Thumbprint**.</span></span> <span data-ttu-id="2b6a0-230">wartość Hello odcisk palca hello jest wyświetlana w polu Szczegóły hello, na przykład a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-230">hello value of hello thumbprint is displayed in hello details field, for example ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span></span>
      4. <span data-ttu-id="2b6a0-231">Skopiuj odcisk palca hello i Zapisz wartość hello na później lub edycji skryptu hello teraz.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-231">Copy hello thumbprint and save hello value for later or edit hello script now.</span></span>
      5. <span data-ttu-id="2b6a0-232">(*) Przed uruchomieniem skryptu hello Usuń spacje hello Between hello par wartości.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-232">(*) Before you run hello script, remove hello spaces in between hello pairs of values.</span></span> <span data-ttu-id="2b6a0-233">Na przykład odcisk palca hello zauważyć przed będzie teraz a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-233">For example hello thumbprint noted before would now be ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span></span>
      6. <span data-ttu-id="2b6a0-234">Przypisz raportów hello server certyfikatu toohello.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-234">Assign hello server certificate toohello report server.</span></span> <span data-ttu-id="2b6a0-235">Hello przydziałów zakończeniu w następnej sekcji hello podczas konfigurowania serwera raportów hello.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-235">hello assignment is completed in hello next section when you configure hello report server.</span></span>

<span data-ttu-id="2b6a0-236">Jeśli używasz certyfikatu SSL z podpisem własnym hello nazwa certyfikatu hello już zgodna hello hosta hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-236">If you are using a self-signed SSL certificate, hello name on hello certificate already matches hello hostname of hello VM.</span></span> <span data-ttu-id="2b6a0-237">W związku z tym hello DNS maszyny hello jest już zarejestrowany globalnie i jest możliwy za pomocą dowolnego klienta.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-237">Therefore, hello DNS of hello machine is already registered globally and can be accessed from any client.</span></span>

## <a name="step-3-configure-hello-report-server"></a><span data-ttu-id="2b6a0-238">Krok 3: Konfigurowanie powitania serwera raportów</span><span class="sxs-lookup"><span data-stu-id="2b6a0-238">Step 3: Configure hello Report Server</span></span>
<span data-ttu-id="2b6a0-239">Ta sekcja przeprowadzi Cię przez konfigurację hello maszyny Wirtualnej jako serwera raportów usług Reporting Services w trybie macierzystym.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-239">This section walks you through configuring hello VM as a Reporting Services native mode report server.</span></span> <span data-ttu-id="2b6a0-240">Można użyć jednego powitania po serwera raportów hello tooconfigure metod:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-240">You can use one of hello following methods tooconfigure hello report server:</span></span>

* <span data-ttu-id="2b6a0-241">Korzystać z serwera raportów hello hello skryptu tooconfigure</span><span class="sxs-lookup"><span data-stu-id="2b6a0-241">Use hello script tooconfigure hello report server</span></span>
* <span data-ttu-id="2b6a0-242">Witaj tooConfigure Użyj Menedżera konfiguracji serwera raportów.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-242">Use Configuration Manager tooConfigure hello Report Server.</span></span>

<span data-ttu-id="2b6a0-243">Aby uzyskać bardziej szczegółowe kroki, zobacz sekcję hello [toohello Connect maszyny wirtualnej, a następnie rozpocznij hello Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="2b6a0-243">For more detailed steps, see hello section [Connect toohello Virtual Machine and Start hello Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span></span>

<span data-ttu-id="2b6a0-244">**Uwierzytelnianie Uwaga:** hello zalecana metoda uwierzytelniania jest uwierzytelnianie systemu Windows i jest hello domyślne uwierzytelnianie usług Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-244">**Authentication Note:** Windows authentication is hello recommended authentication method and it is hello default Reporting Services authentication.</span></span> <span data-ttu-id="2b6a0-245">Tylko użytkownicy, które są skonfigurowane na powitania maszyny Wirtualnej mogą uzyskiwać dostęp do usług Reporting Services i przypisane tooReporting usług ról.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-245">Only users that are configured on hello VM can access Reporting Services and assigned tooReporting Services roles.</span></span>

### <a name="use-script-tooconfigure-hello-report-server-and-http"></a><span data-ttu-id="2b6a0-246">Użyj skryptu tooconfigure hello raportu serwera i HTTP</span><span class="sxs-lookup"><span data-stu-id="2b6a0-246">Use script tooconfigure hello report server and HTTP</span></span>
<span data-ttu-id="2b6a0-247">toouse hello środowiska Windows PowerShell skryptu tooconfigure powitania serwera raportów, pełną hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-247">toouse hello Windows PowerShell script tooconfigure hello report server, complete hello following steps.</span></span> <span data-ttu-id="2b6a0-248">Konfiguracja Hello obejmuje protokołu HTTP, a nie HTTPS:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-248">hello configuration includes HTTP, not HTTPS:</span></span>

1. <span data-ttu-id="2b6a0-249">Z hello klasycznego portalu Azure, wybierz hello maszyny Wirtualnej, a następnie kliknij przycisk Połącz.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-249">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="2b6a0-250">W zależności od konfiguracji przeglądarki może być toosave zostanie wyświetlony monit o plik RDP do połączenia toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-250">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
   
    ![Połącz tooazure maszyny wirtualnej](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="2b6a0-252">Użyj nazwy maszyny Wirtualnej użytkownika hello, nazwę użytkownika i hasła skonfigurowanego podczas tworzenia hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-252">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
   
    <span data-ttu-id="2b6a0-253">Na przykład w hello po obraz, Nazwa maszyny Wirtualnej hello jest **ssrsnativecloud** i nazwa użytkownika hello jest **testuser**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-253">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
   
    ![Nazwa maszyny wirtualnej zawiera logowania](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="2b6a0-255">Na powitania maszyny Wirtualnej, otwórz **programu Windows PowerShell ISE** z uprawnieniami administracyjnymi.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-255">On hello VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="2b6a0-256">Witaj PowerShell ISE jest instalowany domyślnie w systemie Windows server 2012.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-256">hello PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="2b6a0-257">Zaleca się, że używasz hello ISE zamiast standardowego okna programu Windows PowerShell, aby można wkleić skryptu hello hello ISE, zmodyfikuj skrypt hello, a następnie uruchom skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-257">It is recommended you use hello ISE instead of a standard Windows PowerShell window so that you can paste hello script into hello ISE, modify hello script, and then run hello script.</span></span>
3. <span data-ttu-id="2b6a0-258">W środowisku Windows PowerShell ISE, kliknij przycisk hello **widoku** menu, a następnie kliknij przycisk **Pokaż okienko skryptu**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-258">In Windows PowerShell ISE, click hello **View** menu and then click **Show Script Pane**.</span></span>
4. <span data-ttu-id="2b6a0-259">Hello następującego skryptu skopiuj i Wklej hello skryptu w okienku skryptów programu Windows PowerShell ISE hello.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-259">Copy hello following script, and paste hello script into hello Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change hello value if you used a different port for hello private HTTP endpoint when hello VM was created.
   
        ## Set PowerShell execution policy toobe able toorun scripts
        Set-ExecutionPolicy RemoteSigned -Force
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port $HTTPport (for local usage)
            write-host "Calling ReserveURL port $HTTPport"
            $r = $RSObject.ReserveURL('ReportServerWebService',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportServer port $HTTPport" 
   
        ## Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port $HTTPport
            write-host "Calling ReserveURL for ReportManager, port $HTTPport"
            $r = $RSObject.ReserveURL('ReportManager',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportManager port $HTTPport"
   
        write-host -foregroundcolor green "Open Firewall port for $HTTPport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $HTTPport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $HTTPport)” -Direction Inbound –Protocol TCP –LocalPort $HTTPport
            write-host "Added rule Report Server (TCP on port $HTTPport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
5. <span data-ttu-id="2b6a0-260">Jeśli utworzono hello maszyny Wirtualnej z portem HTTP innych niż 80, zmodyfikuj parametr hello $HTTPport = 80.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-260">If you created hello VM with an HTTP port other than 80, modify hello parameter $HTTPport = 80.</span></span>
6. <span data-ttu-id="2b6a0-261">skrypt Hello jest obecnie skonfigurowany dla usług Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-261">hello script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="2b6a0-262">Toorun hello skryptów dla usług Reporting Services, zmodyfikować części wersji hello hello ścieżki toohello nazw zbyt "v11" w instrukcji hello Get-WmiObject.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-262">If you want toorun hello script for  Reporting Services, modify hello version portion of hello path toohello namespace too“v11”, on hello Get-WmiObject statement.</span></span>
7. <span data-ttu-id="2b6a0-263">Uruchom skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-263">Run hello script.</span></span>

<span data-ttu-id="2b6a0-264">**Sprawdzanie poprawności**: tooverify, który hello podstawowy raport serwera działania, zobacz hello [konfiguracji hello Sprawdź](#verify-the-configuration) później w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-264">**Validation**: tooverify that hello basic report server functionality is working, see hello [Verify hello configuration](#verify-the-configuration) section later in this topic.</span></span>

### <a name="use-script-tooconfigure-hello-report-server-and-https"></a><span data-ttu-id="2b6a0-265">Użyj skryptu tooconfigure hello raportu serwera i protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="2b6a0-265">Use script tooconfigure hello report server and HTTPS</span></span>
<span data-ttu-id="2b6a0-266">toouse programu Windows PowerShell tooconfigure powitania serwera raportów, pełną hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-266">toouse Windows PowerShell tooconfigure hello report server, complete hello following steps.</span></span> <span data-ttu-id="2b6a0-267">Konfiguracja Hello obejmuje protokołu HTTPS, a nie HTTP.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-267">hello configuration includes HTTPS, not HTTP.</span></span>

1. <span data-ttu-id="2b6a0-268">Z hello klasycznego portalu Azure, wybierz hello maszyny Wirtualnej, a następnie kliknij przycisk Połącz.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-268">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="2b6a0-269">W zależności od konfiguracji przeglądarki może być toosave zostanie wyświetlony monit o plik RDP do połączenia toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-269">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
   
    ![Połącz tooazure maszyny wirtualnej](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="2b6a0-271">Użyj nazwy maszyny Wirtualnej użytkownika hello, nazwę użytkownika i hasła skonfigurowanego podczas tworzenia hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-271">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
   
    <span data-ttu-id="2b6a0-272">Na przykład w hello po obraz, Nazwa maszyny Wirtualnej hello jest **ssrsnativecloud** i nazwa użytkownika hello jest **testuser**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-272">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
   
    ![Nazwa maszyny wirtualnej zawiera logowania](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="2b6a0-274">Na powitania maszyny Wirtualnej, otwórz **programu Windows PowerShell ISE** z uprawnieniami administracyjnymi.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-274">On hello VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="2b6a0-275">Witaj PowerShell ISE jest instalowany domyślnie w systemie Windows server 2012.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-275">hello PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="2b6a0-276">Zaleca się, że używasz hello ISE zamiast standardowego okna programu Windows PowerShell, aby można wkleić skryptu hello hello ISE, zmodyfikuj skrypt hello, a następnie uruchom skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-276">It is recommended you use hello ISE instead of a standard Windows PowerShell window so that you can paste hello script into hello ISE, modify hello script, and then run hello script.</span></span>
3. <span data-ttu-id="2b6a0-277">uruchamianie skryptów, uruchom następujące polecenia programu Windows PowerShell hello tooenable:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-277">tooenable running scripts, run hello following Windows PowerShell command:</span></span>
   
        Set-ExecutionPolicy RemoteSigned
   
    <span data-ttu-id="2b6a0-278">Następnie możesz uruchomić następujące zasady hello tooverify hello:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-278">You can then run hello following tooverify hello policy:</span></span>
   
        Get-ExecutionPolicy
4. <span data-ttu-id="2b6a0-279">W **programu Windows PowerShell ISE**, kliknij przycisk hello **widoku** menu, a następnie kliknij przycisk **Pokaż okienko skryptu**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-279">In **Windows PowerShell ISE**, click hello **View** menu and then click **Show Script Pane**.</span></span>
5. <span data-ttu-id="2b6a0-280">Skopiuj hello następujący skrypt i wklej go w okienku skryptów programu Windows PowerShell ISE hello.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-280">Copy hello following script and paste it into hello Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures hello report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when hello HTTPS endpoint was created.
   
        # You can run hello following command tooget (.cloudapp.net certificates) so you can copy hello thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # hello certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # hello certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If hello certificate is not a wildcard certificate, comment out hello following line, and enable hello full $DNSNAme reference.
        $DNSName="+"
        #$DNSName="$server.cloudapp.net"
        $DNSNameAndPort = $DNSName + ":$httpsport"
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        write-host "hello script will use $DNSNameAndPort as hello DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port 80 (for local usage)
            write-host 'Calling ReserveURL port 80'
            $r = $RSObject.ReserveURL('ReportServerWebService','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportServer port 80" 
   
        ## ReserveURL for ReportServerWebService - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportServerWebService',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportServer port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportServerWebService port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport, with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportServerWebService',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportServer port $httpsport" 
   
        ## 2. Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## 3. Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port 80
            write-host 'Calling ReserveURL for ReportManager, port 80'
            $r = $RSObject.ReserveURL('ReportManager','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportManager port 80"
   
        ## ReserveURL for ReportManager - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportManager',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportManager port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportManager port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportManager',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportManager port $httpsport" 
   
        write-host -foregroundcolor green "Open Firewall port for $httpsport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $httpsport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $httpsport)” -Direction Inbound –Protocol TCP –LocalPort $httpsport
            write-host "Added rule Report Server (TCP on port $httpsport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
6. <span data-ttu-id="2b6a0-281">Modyfikowanie hello **$certificatehash** parametru w skrypcie hello:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-281">Modify hello **$certificatehash** parameter in hello script:</span></span>
   
   * <span data-ttu-id="2b6a0-282">Jest to **wymagane** parametru.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-282">This is a **required** parameter.</span></span> <span data-ttu-id="2b6a0-283">Jeśli nie została zapisana wartość certyfikatu hello z poprzednich kroków hello, użyj jednej z poniższych wartość skrótu certyfikatu hello toocopy metody z odciskiem palca certyfikatów hello hello.:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-283">If you did not save hello certificate value from hello previous steps, use one of hello following methods toocopy hello certificate hash value from hello certificates thumbprint.:</span></span>
     
       <span data-ttu-id="2b6a0-284">Na hello maszyny Wirtualnej Otwórz program Windows PowerShell ISE i uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-284">On hello VM, open Windows PowerShell ISE and run hello following command:</span></span>
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       <span data-ttu-id="2b6a0-285">dane wyjściowe Hello będzie wyglądać podobnie następujące toohello.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-285">hello output will look similar toohello following.</span></span> <span data-ttu-id="2b6a0-286">Jeśli skrypt hello zwraca pusty wiersz, hello maszyny Wirtualnej nie ma certyfikatu skonfigurowanego na przykład, zobacz sekcję hello [toouse hello certyfikatu z podpisem własnym maszyn wirtualnych](#to-use-the-virtual-machines-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="2b6a0-286">If hello script returns a blank line, hello VM does not have a certificate configured for example, see hello section [toouse hello Virtual Machines Self-signed Certificate](#to-use-the-virtual-machines-self-signed-certificate).</span></span>
     
     <span data-ttu-id="2b6a0-287">LUB</span><span class="sxs-lookup"><span data-stu-id="2b6a0-287">OR</span></span>
   * <span data-ttu-id="2b6a0-288">Na hello mmc.exe uruchomienia maszyny Wirtualnej, a następnie dodaj hello **certyfikaty** przystawki.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-288">On hello VM Run mmc.exe and then add hello **Certificates** snap-in.</span></span>
   * <span data-ttu-id="2b6a0-289">W obszarze hello **zaufane główne urzędy certyfikacji** węzła kliknij dwukrotnie nazwę certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-289">Under hello **Trusted Root Certificate Authorities** node double-click your certificate name.</span></span> <span data-ttu-id="2b6a0-290">Jeśli używasz certyfikatu z podpisem własnym hello z hello maszyny Wirtualnej, certyfikat hello jest nosi nazwę DNS hello hello maszyny Wirtualnej i kończy się wyrazem **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-290">If you are using hello self-signed certificate of hello VM, hello certificate is named after hello DNS name of hello VM and ends with **cloudapp.net**.</span></span>
   * <span data-ttu-id="2b6a0-291">Kliknij przycisk hello **szczegóły** kartę.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-291">Click hello **Details** tab.</span></span>
   * <span data-ttu-id="2b6a0-292">Kliknij przycisk **odcisk palca**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-292">Click **Thumbprint**.</span></span> <span data-ttu-id="2b6a0-293">wartość Hello odcisk palca hello jest wyświetlana w polu Szczegóły hello, na przykład af 11 60 b6 4b 28 8 d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span><span class="sxs-lookup"><span data-stu-id="2b6a0-293">hello value of hello thumbprint is displayed in hello details field, for example af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span></span>
   * <span data-ttu-id="2b6a0-294">**Przed uruchomieniem skryptu hello**, Usuń spacje hello Between hello par wartości.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-294">**Before you run hello script**, remove hello spaces in between hello pairs of values.</span></span> <span data-ttu-id="2b6a0-295">Na przykład af1160b64b288d890a8212ff6ba9c3664f319048</span><span class="sxs-lookup"><span data-stu-id="2b6a0-295">For example af1160b64b288d890a8212ff6ba9c3664f319048</span></span>
7. <span data-ttu-id="2b6a0-296">Modyfikowanie hello **$httpsport** parametru:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-296">Modify hello **$httpsport** parameter:</span></span> 
   
   * <span data-ttu-id="2b6a0-297">Jeśli dla punktu końcowego HTTPS hello jest używany port 443, następnie nie trzeba tooupdate tego parametru w skrypcie hello.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-297">If you used port 443 for hello HTTPS endpoint, then you do not need tooupdate this parameter in hello script.</span></span> <span data-ttu-id="2b6a0-298">W przeciwnym razie użyj wartości portu hello, wybranej podczas konfigurowania prywatnej punkt końcowy HTTPS hello na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-298">Otherwise use hello port value you selected when you configured hello HTTPS private endpoint on hello VM.</span></span>
8. <span data-ttu-id="2b6a0-299">Modyfikowanie hello **$DNSName** parametru:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-299">Modify hello **$DNSName** parameter:</span></span> 
   
   * <span data-ttu-id="2b6a0-300">Witaj skrypt został skonfigurowany certyfikat wieloznaczny $DNSName = "+".</span><span class="sxs-lookup"><span data-stu-id="2b6a0-300">hello script is configured for a wild card certificate $DNSName="+".</span></span> <span data-ttu-id="2b6a0-301">Jeśli nie chcesz, aby tooconfigure jest nie w powiązanie certyfikatu symboli wieloznacznych, komentarz $DNSName = "+"i Włącz po wierszu hello $DNSNAme pełna dokumentacja ## $DNSName="$server.cloudapp.net hello".</span><span class="sxs-lookup"><span data-stu-id="2b6a0-301">If you do no want tooconfigure for a wildcard certificate binding, comment out $DNSName="+" and enable hello following line, hello full $DNSNAme reference, ##$DNSName="$server.cloudapp.net".</span></span>
     
       <span data-ttu-id="2b6a0-302">Zmień wartość hello $DNSName, jeśli nie chcesz, aby toouse hello maszyny wirtualnej na nazwy DNS dla usług Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-302">Change hello $DNSName value if you do not want toouse hello virtual machine’s DNS name for Reporting Services.</span></span> <span data-ttu-id="2b6a0-303">Jeśli parametr hello hello certyfikatu należy również użyć tej nazwy i zarejestrowaniu nazwy hello globalnie na serwerze DNS.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-303">If you use hello parameter, hello certificate must also use this name and you register hello name globally on a DNS server.</span></span>
9. <span data-ttu-id="2b6a0-304">skrypt Hello jest obecnie skonfigurowany dla usług Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-304">hello script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="2b6a0-305">Toorun hello skryptów dla usług Reporting Services, zmodyfikować części wersji hello hello ścieżki toohello nazw zbyt "v11" w instrukcji hello Get-WmiObject.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-305">If you want toorun hello script for  Reporting Services, modify hello version portion of hello path toohello namespace too“v11”, on hello Get-WmiObject statement.</span></span>
10. <span data-ttu-id="2b6a0-306">Uruchom skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-306">Run hello script.</span></span>

<span data-ttu-id="2b6a0-307">**Sprawdzanie poprawności**: tooverify, który hello podstawowy raport serwera działania, zobacz hello [konfiguracji hello Sprawdź](#verify-the-connection) później w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-307">**Validation**: tooverify that hello basic report server functionality is working, see hello [Verify hello configuration](#verify-the-connection) section later in this topic.</span></span> <span data-ttu-id="2b6a0-308">powiązanie certyfikatu hello tooverify Otwórz wiersz polecenia z uprawnieniami administracyjnymi, a następnie uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-308">tooverify hello certificate binding open a command prompt with administrative privileges, and then run hello following command:</span></span>

    netsh http show sslcert

<span data-ttu-id="2b6a0-309">Witaj wynik będzie zawierać następujące hello:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-309">hello result will include hello following:</span></span>

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-tooconfigure-hello-report-server"></a><span data-ttu-id="2b6a0-310">Witaj tooConfigure Użyj Menedżera konfiguracji serwera raportów</span><span class="sxs-lookup"><span data-stu-id="2b6a0-310">Use Configuration Manager tooConfigure hello Report Server</span></span>
<span data-ttu-id="2b6a0-311">Jeśli nie chcesz, aby serwer raportów hello tooconfigure skryptu toorun hello programu PowerShell, wykonaj kroki hello w tej sekcji toouse hello usług Reporting Services w trybie macierzystym tooconfigure hello raportu serwera programu configuration manager.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-311">If you do not want toorun hello PowerShell script tooconfigure hello report server, follow hello steps in this section toouse hello Reporting Services native mode configuration manager tooconfigure hello report server.</span></span>

1. <span data-ttu-id="2b6a0-312">Z hello klasycznego portalu Azure, wybierz hello maszyny Wirtualnej, a następnie kliknij przycisk Połącz.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-312">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="2b6a0-313">Użyj hello nazwy użytkownika i hasła skonfigurowanego podczas tworzenia hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-313">Use hello user name and password you configured when you created hello VM.</span></span>
   
    ![Połącz tooazure maszyny wirtualnej](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. <span data-ttu-id="2b6a0-315">Uruchom usługę Windows update i zainstaluj aktualizacje toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-315">Run Windows update and install updates toohello VM.</span></span> <span data-ttu-id="2b6a0-316">Jeśli wymagane jest ponowne uruchomienie hello maszyny Wirtualnej, uruchom ponownie hello maszyny Wirtualnej, a następnie ponownie toohello maszyny Wirtualnej z hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-316">If a restart of hello VM is required, restart hello VM and reconnect toohello VM from hello Azure classic portal.</span></span>
3. <span data-ttu-id="2b6a0-317">W menu Start hello na powitania maszyny Wirtualnej, wpisz **usług Reporting Services** , a następnie otwórz **Reporting Services Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-317">From hello Start menu on hello VM, type **Reporting Services** and open **Reporting Services Configuration Manager**.</span></span>
4. <span data-ttu-id="2b6a0-318">Pozostaw wartości domyślne hello **nazwy serwera** i **wystąpienie serwera raportów**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-318">Leave hello default values for **Server Name** and **Report Server Instance**.</span></span> <span data-ttu-id="2b6a0-319">Kliknij przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-319">Click **Connect**.</span></span>
5. <span data-ttu-id="2b6a0-320">W okienku po lewej stronie powitania kliknij **adres URL usługi sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-320">In hello left pane, click **Web Service URL**.</span></span>
6. <span data-ttu-id="2b6a0-321">Domyślnie RS jest skonfigurowany dla protokołu HTTP portu 80 z adresem IP "Wszystkie przypisane".</span><span class="sxs-lookup"><span data-stu-id="2b6a0-321">By default, RS is configured for HTTP port 80 with IP “All Assigned”.</span></span> <span data-ttu-id="2b6a0-322">tooadd HTTPS:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-322">tooadd HTTPS:</span></span>
   
   1. <span data-ttu-id="2b6a0-323">W **certyfikat SSL**: hello wybierz certyfikat toouse, na przykład [Nazwa maszyny Wirtualnej]. cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-323">In **SSL Certificate**: select hello certificate you want toouse, for example [VM name].cloudapp.net.</span></span> <span data-ttu-id="2b6a0-324">Jeśli żadne certyfikaty nie są wyświetlane, zobacz sekcję hello **krok 2: Utworzenie certyfikatu serwera** Aby uzyskać informacje dotyczące sposobu tooinstall i zaufania hello certyfikatu na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-324">If no certificates are listed, see hello section **Step 2: Create a Server Certificate** for information on how tooinstall and trust hello certificate on hello VM.</span></span>
   2. <span data-ttu-id="2b6a0-325">W obszarze **SSL Port**: Wybierz 443.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-325">Under **SSL Port**: choose 443.</span></span> <span data-ttu-id="2b6a0-326">Jeśli skonfigurowano prywatnej punkt końcowy HTTPS hello w hello maszyny Wirtualnej z inną port prywatny, w tym miejscu użycie tej wartości.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-326">If you configured hello HTTPS private endpoint in hello VM with a different private port, use that value here.</span></span>
   3. <span data-ttu-id="2b6a0-327">Kliknij przycisk **Zastosuj** i poczekaj, aż hello toocomplete operacji.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-327">Click **Apply** and wait for hello operation toocomplete.</span></span>
7. <span data-ttu-id="2b6a0-328">W okienku po lewej stronie powitania kliknij **bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-328">In hello left pane, click **Database**.</span></span>
   
   1. <span data-ttu-id="2b6a0-329">Kliknij przycisk **zmienić baza danych**e.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-329">Click **Change Databas**e.</span></span>
   2. <span data-ttu-id="2b6a0-330">Kliknij przycisk **Utwórz nową bazę danych serwera raportów** , a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-330">Click **Create a new report server database** and then click **Next**.</span></span>
   3. <span data-ttu-id="2b6a0-331">Pozostaw domyślną hello **nazwy serwera**: hello wirtualna Nazwij i pozostaw domyślną hello **typ uwierzytelniania** jako **bieżącego użytkownika** — **zintegrowane zabezpieczenia**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-331">Leave hello default **Server Name**: as hello VM name and leave hello default **Authentication Type** as **Current User** – **Integrated Security**.</span></span> <span data-ttu-id="2b6a0-332">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-332">Click **Next**.</span></span>
   4. <span data-ttu-id="2b6a0-333">Pozostaw domyślną hello **Nazwa bazy danych** jako **ReportServer** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-333">Leave hello default **Database Name** as **ReportServer** and click **Next**.</span></span>
   5. <span data-ttu-id="2b6a0-334">Pozostaw domyślną hello **typ uwierzytelniania** jako **poświadczenia usługi** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-334">Leave hello default **Authentication Type** as **Service Credentials** and click **Next**.</span></span>
   6. <span data-ttu-id="2b6a0-335">Kliknij przycisk **dalej** na powitania **Podsumowanie** strony.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-335">Click **Next** on hello **Summary** page.</span></span>
   7. <span data-ttu-id="2b6a0-336">Po zakończeniu konfiguracji powitania kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-336">When hello configuration is complete, click **Finish**.</span></span>
8. <span data-ttu-id="2b6a0-337">W okienku po lewej stronie powitania kliknij **adres URL Menedżera raportów**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-337">In hello left pane, click **Report Manager URL**.</span></span> <span data-ttu-id="2b6a0-338">Pozostaw domyślną hello **katalogu wirtualnego** jako **raporty** i kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-338">Leave hello default **Virtual Directory** as **Reports** and click **Apply**.</span></span>
9. <span data-ttu-id="2b6a0-339">Kliknij przycisk **zakończenia** tooclose hello Reporting Services Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-339">Click **Exit** tooclose hello Reporting Services Configuration Manager.</span></span>

## <a name="step-4-open-windows-firewall-port"></a><span data-ttu-id="2b6a0-340">Krok 4: Port zapory systemu Windows otwórz</span><span class="sxs-lookup"><span data-stu-id="2b6a0-340">Step 4: Open Windows Firewall Port</span></span>
> [!NOTE]
> <span data-ttu-id="2b6a0-341">Jeśli użyto jednego serwera raportów hello hello skrypty tooconfigure, możesz pominąć tę sekcję.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-341">If you used one of hello scripts tooconfigure hello report server, you can skip this section.</span></span> <span data-ttu-id="2b6a0-342">skrypt Hello uwzględnione port zapory hello tooopen kroku.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-342">hello script included a step tooopen hello firewall port.</span></span> <span data-ttu-id="2b6a0-343">domyślne Hello jest port 80 dla protokołu HTTP i 443 dla protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-343">hello default was port 80 for HTTP and port 443 for HTTPS.</span></span>
> 
> 

<span data-ttu-id="2b6a0-344">tooconnect zdalnie tooReport Manager lub hello raportu Server na maszynie wirtualnej hello, punkt końcowy protokołu TCP jest wymagany na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-344">tooconnect remotely tooReport Manager or hello Report Server on hello virtual machine, a TCP Endpoint is required on hello VM.</span></span> <span data-ttu-id="2b6a0-345">Jest wymagane tooopen hello sam port w zaporze hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-345">It is required tooopen hello same port in hello VM’s firewall.</span></span> <span data-ttu-id="2b6a0-346">punkt końcowy Hello został utworzony podczas zainicjowano obsługę administracyjną hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-346">hello endpoint was created when hello VM was provisioned.</span></span>

<span data-ttu-id="2b6a0-347">Ta sekcja zawiera podstawowe informacje na jak tooopen hello portu zapory.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-347">This section provides basic information on how tooopen hello firewall port.</span></span> <span data-ttu-id="2b6a0-348">Aby uzyskać więcej informacji, zobacz [konfigurowania zapory dla dostępu do serwera raportów](https://technet.microsoft.com/library/bb934283.aspx)</span><span class="sxs-lookup"><span data-stu-id="2b6a0-348">For more information, see [Configure a Firewall for Report Server Access](https://technet.microsoft.com/library/bb934283.aspx)</span></span>

> [!NOTE]
> <span data-ttu-id="2b6a0-349">Jeśli używasz serwera raportów hello hello skryptu tooconfigure, możesz pominąć tę sekcję.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-349">If you used hello script tooconfigure hello report server, you can skip this section.</span></span> <span data-ttu-id="2b6a0-350">skrypt Hello uwzględnione port zapory hello tooopen kroku.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-350">hello script included a step tooopen hello firewall port.</span></span>
> 
> 

<span data-ttu-id="2b6a0-351">Jeśli port prywatny jest skonfigurowany do obsługi protokołu HTTPS innego niż 443, zmodyfikuj hello odpowiednio następującego skryptu.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-351">If you configured a private port for HTTPS other than 443, modify hello following script appropriately.</span></span> <span data-ttu-id="2b6a0-352">tooopen port **443** na powitania zapory systemu Windows, wykonaj następujące czynności hello:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-352">tooopen port **443** on hello Windows Firewall, complete hello following:</span></span>

1. <span data-ttu-id="2b6a0-353">Otwórz okno programu Windows PowerShell z uprawnieniami administracyjnymi.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-353">Open a Windows PowerShell window with administrative privileges.</span></span>
2. <span data-ttu-id="2b6a0-354">Jeśli użyto portu innego niż 443 podczas konfigurowania punktu końcowego HTTPS hello na powitania maszyny Wirtualnej, Aktualizuj port hello w hello następujące polecenie, a następnie uruchom polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-354">If you used a port other than 443 when you configured hello HTTPS endpoint on hello VM, update hello port in hello following command and then run hello command:</span></span>
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. <span data-ttu-id="2b6a0-355">Po zakończeniu wykonywania polecenia hello **Ok** jest wyświetlany w wierszu polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-355">When hello command completes, **Ok** is displayed in hello command prompt.</span></span>

<span data-ttu-id="2b6a0-356">tooverify czy hello port jest otwarty, Otwórz okno programu Windows PowerShell i hello uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-356">tooverify that hello port is opened, open a Windows PowerShell window and run hello following command:</span></span>

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-hello-configuration"></a><span data-ttu-id="2b6a0-357">Sprawdź konfigurację hello</span><span class="sxs-lookup"><span data-stu-id="2b6a0-357">Verify hello configuration</span></span>
<span data-ttu-id="2b6a0-358">tooverify, które funkcje serwera podstawowy raport hello działa, otwórz przeglądarkę z uprawnieniami administracyjnymi i przeglądania toohello następujące raportować Menedżera raportów ad serwera adresów URL:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-358">tooverify that hello basic report server functionality is now working, open your browser with administrative privileges and then browse toohello following report server ad report manager URLS:</span></span>

* <span data-ttu-id="2b6a0-359">Na powitania maszyny Wirtualnej Przejdź toohello adres URL serwera raportów:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-359">On hello VM, browse toohello report server URL:</span></span>
  
        http://localhost/reportserver
* <span data-ttu-id="2b6a0-360">Na powitania maszyny Wirtualnej Przejdź adres URL Menedżera raportów toohello:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-360">On hello VM, browse toohello report manger URL:</span></span>
  
        http://localhost/Reports
* <span data-ttu-id="2b6a0-361">Z komputera lokalnego Przeglądaj toohello **zdalnego** raport menedżera na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-361">From your local computer, browse toohello **remote** report Manager on hello VM.</span></span> <span data-ttu-id="2b6a0-362">Aktualizacja nazwy DNS hello w hello poniższy przykład zależnie od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-362">Update hello DNS name in hello following example as appropriate.</span></span> <span data-ttu-id="2b6a0-363">Po wyświetleniu monitu o podanie hasła, Użyj poświadczeń administratora hello, utworzony zainicjowano obsługę administracyjną hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-363">When prompted for a password, use hello administrator credentials you created when hello VM was provisioned.</span></span> <span data-ttu-id="2b6a0-364">Nazwa użytkownika Hello jest hello [domena]\[nazwa użytkownika] format, w którym hello domeny jest nazwa komputera maszyny Wirtualnej hello, na przykład ssrsnativecloud\testuser.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-364">hello user name is in hello [Domain]\[user name] format, where hello domain is hello VM computer name, for example ssrsnativecloud\testuser.</span></span> <span data-ttu-id="2b6a0-365">Jeśli nie używasz HTTP**S**, Usuń hello **s** w adresie URL hello.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-365">If you are not using HTTP**S**, remove hello **s** in hello URL.</span></span> <span data-ttu-id="2b6a0-366">Zobacz hello następnej sekcji, aby uzyskać informacje na temat tworzenia dodatkowych użytkowników na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-366">See hello next section for information on creating additional users on VM.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/Reports
* <span data-ttu-id="2b6a0-367">Przeglądaj, adres URL serwera raportów zdalnego toohello z komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-367">From your local computer, browse toohello remote report server URL.</span></span> <span data-ttu-id="2b6a0-368">Aktualizacja nazwy DNS hello w hello poniższy przykład zależnie od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-368">Update hello DNS name in hello following example as appropriate.</span></span> <span data-ttu-id="2b6a0-369">Jeśli nie używasz protokołu HTTPS, należy usunąć hello s w adresie URL hello.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-369">If you are not using HTTPS, remove hello s in hello URL.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a><span data-ttu-id="2b6a0-370">Tworzenie użytkowników i przypisywania ról</span><span class="sxs-lookup"><span data-stu-id="2b6a0-370">Create Users and Assign Roles</span></span>
<span data-ttu-id="2b6a0-371">Po konfigurowania i weryfikowania hello raport serwera typowych zadań administracyjnych jest toocreate co najmniej jednego użytkownika i Przypisz użytkowników tooReporting usług ról.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-371">After configuring and verifying hello report server, a common administrative task is toocreate one or more users and assign users tooReporting Services roles.</span></span> <span data-ttu-id="2b6a0-372">Aby uzyskać więcej informacji zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-372">For more information, see hello following:</span></span>

* [<span data-ttu-id="2b6a0-373">Utwórz konto użytkownika lokalnego</span><span class="sxs-lookup"><span data-stu-id="2b6a0-373">Create a local user account</span></span>](https://technet.microsoft.com/library/cc770642.aspx)
* <span data-ttu-id="2b6a0-374">[Udziel dostępu użytkownika tooa serwer raportów (Menedżer raportów)](https://msdn.microsoft.com/library/ms156034.aspx))</span><span class="sxs-lookup"><span data-stu-id="2b6a0-374">[Grant User Access tooa Report Server (Report Manager)](https://msdn.microsoft.com/library/ms156034.aspx))</span></span>
* [<span data-ttu-id="2b6a0-375">Tworzenie i zarządzanie nimi przypisań ról</span><span class="sxs-lookup"><span data-stu-id="2b6a0-375">Create and Manage Role Assignments</span></span>](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a><span data-ttu-id="2b6a0-376">tooCreate i opublikować raporty toohello maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2b6a0-376">tooCreate and Publish Reports toohello Azure Virtual Machine</span></span>
<span data-ttu-id="2b6a0-377">Witaj poniższej tabeli przedstawiono niektóre istniejące raporty toopublish dostępne opcje hello z komputera lokalnego toohello serwera raportów hostowanych na powitania maszyny wirtualnej platformy Microsoft Azure:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-377">hello following table summarizes some of hello options available toopublish existing reports from an on-premises computer toohello report server hosted on hello Microsoft Azure Virtual Machine:</span></span>

* <span data-ttu-id="2b6a0-378">**Skrypt RS.exe**: elementy raportu toocopy RS.exe Użyj skryptu z i istniejącego raportu server tooyour maszyny wirtualnej platformy Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-378">**RS.exe script**: Use RS.exe script toocopy report items from and existing report server tooyour Microsoft Azure Virtual Machine.</span></span> <span data-ttu-id="2b6a0-379">Aby uzyskać więcej informacji, zobacz sekcję hello "w trybie macierzystym tooNative tryb — maszyny wirtualnej platformy Microsoft Azure" w [próbki Reporting Services rs.exe skryptu tooMigrate zawartości między serwerami raport](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b6a0-379">For more information, see hello section “Native mode tooNative Mode – Microsoft Azure Virtual Machine” in [Sample Reporting Services rs.exe Script tooMigrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>
* <span data-ttu-id="2b6a0-380">**Report Builder**: hello maszyny wirtualnej zawiera powitania kliknij — raz wersji programu Microsoft SQL Server Report Builder.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-380">**Report Builder**: hello virtual machine includes hello click-once version of Microsoft SQL Server Report Builder.</span></span> <span data-ttu-id="2b6a0-381">toostart raport konstruktora powitania po raz pierwszy na maszynie wirtualnej hello:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-381">toostart Report builder hello first time on hello virtual machine:</span></span>
  
  1. <span data-ttu-id="2b6a0-382">Uruchom przeglądarkę z uprawnieniami administracyjnymi.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-382">Start your browser with administrative privileges.</span></span>
  2. <span data-ttu-id="2b6a0-383">Przeglądaj Menedżera tooreport hello maszyny wirtualnej, a następnie kliknij przycisk **Report Builder** hello Wstążce.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-383">Browse tooreport manager on hello virtual machine and click **Report Builder**  in hello ribbon.</span></span>
     
     <span data-ttu-id="2b6a0-384">Aby uzyskać więcej informacji, zobacz [instalowanie, odinstalowywanie i obsługa programu Report Builder](https://technet.microsoft.com/library/dd207038.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b6a0-384">For more information, see [Installing, Uninstalling, and Supporting Report Builder](https://technet.microsoft.com/library/dd207038.aspx).</span></span>
* <span data-ttu-id="2b6a0-385">**Programu SQL Server Data Tools: Maszyna wirtualna**: Jeśli hello maszyny Wirtualnej zostały utworzone z programu SQL Server 2012, SQL Server Data Tools jest zainstalowany na maszynie wirtualnej hello i mogą być używane toocreate **projektów serwera raportów** i raporty na powitania wirtualnego maszyny.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-385">**SQL Server Data Tools: VM**:  If you created hello VM with SQL Server 2012, then SQL Server Data Tools is installed on hello virtual machine and can be used toocreate **Report Server Projects** and reports on hello virtual machine.</span></span> <span data-ttu-id="2b6a0-386">SQL Server Data Tools można opublikować serwera raportów toohello raporty hello hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-386">SQL Server Data Tools can publish hello reports toohello report server on hello virtual machine.</span></span>
  
    <span data-ttu-id="2b6a0-387">Jeśli utworzono hello maszyny Wirtualnej z programem SQL server 2014, należy zainstalować Biznesowej programu SQL Server Data Tools — dla programu visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-387">If you created hello VM with SQL server 2014, you can install SQL Server Data Tools- BI for visual Studio.</span></span> <span data-ttu-id="2b6a0-388">Aby uzyskać więcej informacji zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="2b6a0-388">For more information, see hello following:</span></span>
  
  * [<span data-ttu-id="2b6a0-389">Microsoft SQL Server Data Tools - Business Intelligence dla programu Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="2b6a0-389">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2013</span></span>](https://www.microsoft.com/download/details.aspx?id=42313)
  * [<span data-ttu-id="2b6a0-390">Microsoft SQL Server Data Tools - Business Intelligence dla programu Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="2b6a0-390">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012</span></span>](https://www.microsoft.com/download/details.aspx?id=36843)
  * [<span data-ttu-id="2b6a0-391">SQL Server Data Tools i SQL Server Business Intelligence (SSDT BI)</span><span class="sxs-lookup"><span data-stu-id="2b6a0-391">SQL Server Data Tools and SQL Server Business Intelligence (SSDT-BI)</span></span>](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* <span data-ttu-id="2b6a0-392">**Program SQL Server Data Tools: Zdalny**: na komputerze lokalnym, Utwórz projekt usług Reporting Services w programie SQL Server Data Tools, który zawiera raporty usług Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-392">**SQL Server Data Tools: Remote**:  On your local computer, create a Reporting Services project in SQL Server Data Tools that contains Reporting Services reports.</span></span> <span data-ttu-id="2b6a0-393">Skonfiguruj tooconnect projektu hello toohello URL usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-393">Configure hello project tooconnect toohello web service URL.</span></span>
  
    ![Właściwości projektu narzędzia SSDT dla projektu usług SSRS](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* <span data-ttu-id="2b6a0-395">**Użyj skryptu**: Użyj zawartości serwera raportów toocopy skryptu.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-395">**Use script**: Use script toocopy report server content.</span></span> <span data-ttu-id="2b6a0-396">Aby uzyskać więcej informacji, zobacz [próbki Reporting Services rs.exe skryptu tooMigrate zawartości między serwerami raport](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b6a0-396">For more information, see [Sample Reporting Services rs.exe Script tooMigrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>

## <a name="minimize-cost-if-you-are-not-using-hello-vm"></a><span data-ttu-id="2b6a0-397">Zminimalizować koszty, jeśli nie używasz hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2b6a0-397">Minimize cost if you are not using hello VM</span></span>
> [!NOTE]
> <span data-ttu-id="2b6a0-398">opłaty toominimize dla maszyn wirtualnych platformy Azure nieużywane, zamknij hello maszyny Wirtualnej z hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-398">toominimize charges for your Azure Virtual Machines when not in use, shut down hello VM from hello Azure classic portal.</span></span> <span data-ttu-id="2b6a0-399">Jeśli używasz Opcje zasilania systemu Windows hello wewnątrz tooshut maszyny Wirtualnej, dół hello maszyny Wirtualnej, są nadal naliczane hello sama kwota hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-399">If you use hello Windows power options inside a VM tooshut down hello VM, you are still charged hello same amount for hello VM.</span></span> <span data-ttu-id="2b6a0-400">tooreduce opłat, należy tooshut dół hello maszyny Wirtualnej w hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2b6a0-400">tooreduce charges, you need tooshut down hello VM in hello Azure classic portal.</span></span> <span data-ttu-id="2b6a0-401">Jeśli hello maszyny Wirtualnej nie są już potrzebne, pamiętaj hello toodelete maszyny Wirtualnej i hello VHD skojarzone opłaty za magazyn tooavoid dla plików. Aby uzyskać więcej informacji, zobacz sekcję hello — często zadawane pytania na [maszyny wirtualne — cennik](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="2b6a0-401">If you no longer need hello VM, remember toodelete hello VM and hello associated .vhd files tooavoid storage charges.For more information, see hello FAQ section at [Virtual Machines Pricing Details](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>

## <a name="more-information"></a><span data-ttu-id="2b6a0-402">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="2b6a0-402">More Information</span></span>
### <a name="resources"></a><span data-ttu-id="2b6a0-403">Zasoby</span><span class="sxs-lookup"><span data-stu-id="2b6a0-403">Resources</span></span>
* <span data-ttu-id="2b6a0-404">Podobne zawartości związane z wdrożenia pojedynczego serwera tooa analizy biznesowej programu SQL Server i SharePoint 2013, zobacz [tooCreate Użyj środowiska Windows PowerShell Azure maszyny Wirtualnej z Biznesowej programu SQL Server i programu SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b6a0-404">For similar content related tooa single server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Use Windows PowerShell tooCreate an Azure VM With SQL Server BI and SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span></span>
* <span data-ttu-id="2b6a0-405">Dla podobnych tooa powiązane zawartości wdrożenia wielu serwerów programu SQL Server Business Intelligence i programu SharePoint 2013, zobacz [wdrożenia programu SQL Server Business Intelligence w maszynach wirtualnych platformy Azure](https://msdn.microsoft.com/library/dn321998.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b6a0-405">For similar content related tooa multi-server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Deploy SQL Server Business Intelligence in Azure Virtual Machines](https://msdn.microsoft.com/library/dn321998.aspx).</span></span>
* <span data-ttu-id="2b6a0-406">Ogólne informacje pokrewne toodeployments analizy biznesowej programu SQL Server w maszynach wirtualnych platformy Azure, zobacz [analizy biznesowej programu SQL Server w usłudze Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).</span><span class="sxs-lookup"><span data-stu-id="2b6a0-406">For General information related toodeployments of SQL Server Business Intelligence in Azure Virtual Machines, see [SQL Server Business Intelligence in Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).</span></span>
* <span data-ttu-id="2b6a0-407">Aby uzyskać więcej informacji o hello koszt opłat obliczeń platformy Azure, zobacz karty maszyny wirtualnej hello [Azure Kalkulator cen](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="2b6a0-407">For more information about hello cost of Azure compute charges, see hello Virtual Machines tab of [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span></span>

### <a name="community-content"></a><span data-ttu-id="2b6a0-408">Zawartość społeczności</span><span class="sxs-lookup"><span data-stu-id="2b6a0-408">Community Content</span></span>
* <span data-ttu-id="2b6a0-409">Aby uzyskać instrukcje krok po kroku w sposób zgłaszania toocreate tryb macierzysty usług raportowania serwera bez użycia skryptu, zobacz [Hosting usług SQL Reporting Services na maszynie wirtualnej platformy Azure](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span><span class="sxs-lookup"><span data-stu-id="2b6a0-409">For step by step instructions on how toocreate a Reporting Services Native mode report server without using script, see [Hosting SQL Reporting Service on Azure Virtual Machine](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span></span>

### <a name="links-tooother-resources-for-sql-server-in-azure-vms"></a><span data-ttu-id="2b6a0-410">Łącza tooother zasoby dla programu SQL Server na maszynach wirtualnych Azure</span><span class="sxs-lookup"><span data-stu-id="2b6a0-410">Links tooother resources for SQL Server in Azure VMs</span></span>
[<span data-ttu-id="2b6a0-411">Program SQL Server na maszynach wirtualnych platformy Azure — omówienie</span><span class="sxs-lookup"><span data-stu-id="2b6a0-411">SQL Server on Azure Virtual Machines Overview</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

