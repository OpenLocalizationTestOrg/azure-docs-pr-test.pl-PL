---
title: "Tworzenie maszyny Wirtualnej z serwerem raportów w trybie macierzystym przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano i przedstawiono wdrożenia i konfiguracji serwera raportów usług SQL Server Reporting Services w trybie macierzystym w maszynie wirtualnej platformy Azure. "
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
ms.openlocfilehash: 5e5c11251cd316e8161dbe362b300be76927ac01
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-create-an-azure-vm-with-a-native-mode-report-server"></a><span data-ttu-id="36e63-103">Korzystanie z programu PowerShell do tworzenia maszyny wirtualnej platformy Azure z serwerem raportów pracującym w trybie macierzystym</span><span class="sxs-lookup"><span data-stu-id="36e63-103">Use PowerShell to Create an Azure VM With a Native Mode Report Server</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="36e63-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="36e63-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="36e63-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="36e63-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="36e63-106">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="36e63-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="36e63-107">W tym temacie opisano i przedstawiono wdrożenia i konfiguracji serwera raportów usług SQL Server Reporting Services w trybie macierzystym w maszynie wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="36e63-107">This topic describes and walks you through the deployment and configuration of a SQL Server Reporting Services native mode report server in an Azure Virtual Machine.</span></span> <span data-ttu-id="36e63-108">Kroki opisane w tym dokumencie Użyj kombinację wymagane ręczne wykonanie czynności, aby utworzyć maszynę wirtualną i skrypt programu Windows PowerShell w celu skonfigurowania usług Reporting Services na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e63-108">The steps in this document use a combination of manual steps to create the virtual machine and a Windows PowerShell script to configure Reporting Services on the VM.</span></span> <span data-ttu-id="36e63-109">Skrypt konfiguracji zawiera otwierania portu zapory dla protokołu HTTP lub HTTPs.</span><span class="sxs-lookup"><span data-stu-id="36e63-109">The configuration script includes opening a firewall port for HTTP or HTTPs.</span></span>

> [!NOTE]
> <span data-ttu-id="36e63-110">Jeśli nie wymagają **HTTPS** na serwerze raportów **pominąć krok 2**.</span><span class="sxs-lookup"><span data-stu-id="36e63-110">If you do not require **HTTPS** on the report server, **skip step 2**.</span></span>
> 
> <span data-ttu-id="36e63-111">Po utworzeniu maszyny Wirtualnej w kroku 1, przejdź do sekcji Użyj skryptu do konfigurowania serwera raportów i HTTP.</span><span class="sxs-lookup"><span data-stu-id="36e63-111">After creating the VM in step 1, go to the section Use script to configure the report server and HTTP.</span></span> <span data-ttu-id="36e63-112">Po uruchomieniu skryptu serwera raportów jest gotowa do użycia.</span><span class="sxs-lookup"><span data-stu-id="36e63-112">After you run the script, the report server is ready to use.</span></span>

## <a name="prerequisites-and-assumptions"></a><span data-ttu-id="36e63-113">Wymagania wstępne i założenia</span><span class="sxs-lookup"><span data-stu-id="36e63-113">Prerequisites and Assumptions</span></span>
* <span data-ttu-id="36e63-114">**Subskrypcja platformy Azure**: Sprawdź liczba rdzeni dostępne w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="36e63-114">**Azure Subscription**: Verify the number of cores available in your Azure Subscription.</span></span> <span data-ttu-id="36e63-115">Jeśli utworzysz zalecany rozmiar maszyny Wirtualnej **A3**, należy **4** dostępne rdzenie.</span><span class="sxs-lookup"><span data-stu-id="36e63-115">If you create the recommended VM size of **A3**, you need **4** available cores.</span></span> <span data-ttu-id="36e63-116">Jeśli używasz rozmiar maszyny Wirtualnej **A2**, należy **2** dostępne rdzenie.</span><span class="sxs-lookup"><span data-stu-id="36e63-116">If you use a VM size of **A2**, you need **2** available cores.</span></span>
  
  * <span data-ttu-id="36e63-117">Aby sprawdzić limit rdzeni w ramach subskrypcji w klasycznym portalu Azure, w menu u góry kliknij przycisk Ustawienia w okienku po lewej stronie, a następnie kliknij przycisk użycia.</span><span class="sxs-lookup"><span data-stu-id="36e63-117">To verify the core limit of your subscription, in the Azure classic portal, click SETTINGS in the left pane and then Click USAGE in the top menu.</span></span>
  * <span data-ttu-id="36e63-118">Aby zwiększyć limit przydziału rdzeni, skontaktuj się z [pomocą techniczną platformy Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="36e63-118">To increase the core quota, contact [Azure Support](https://azure.microsoft.com/support/options/).</span></span> <span data-ttu-id="36e63-119">Uzyskać rozmiaru maszyny Wirtualnej, zobacz [rozmiarów maszyn wirtualnych na platformie Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="36e63-119">For VM size information, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="36e63-120">**Windows PowerShell do obsługi skryptów**: temacie założono, że masz podstawową wiedzę na temat pracy programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="36e63-120">**Windows PowerShell Scripting**: The topic assumes that you have a basic working knowledge of Windows PowerShell.</span></span> <span data-ttu-id="36e63-121">Aby uzyskać więcej informacji o korzystaniu z programu Windows PowerShell zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="36e63-121">For more information about using Windows PowerShell, see the following:</span></span>
  
  * [<span data-ttu-id="36e63-122">Uruchamianie środowiska Windows PowerShell w systemie Windows Server</span><span class="sxs-lookup"><span data-stu-id="36e63-122">Starting Windows PowerShell on Windows Server</span></span>](https://technet.microsoft.com/library/hh847814.aspx)
  * [<span data-ttu-id="36e63-123">Wprowadzenie do korzystania z programu Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="36e63-123">Getting Started with Windows PowerShell</span></span>](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a><span data-ttu-id="36e63-124">Krok 1: Udostępnić maszynie wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="36e63-124">Step 1: Provision an Azure Virtual Machine</span></span>
1. <span data-ttu-id="36e63-125">Przejdź do klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="36e63-125">Browse to the Azure classic portal.</span></span>
2. <span data-ttu-id="36e63-126">Kliknij przycisk **maszyn wirtualnych** w okienku po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="36e63-126">Click **Virtual Machines** in the left pane.</span></span>
   
    ![maszyny wirtualne Microsoft azure](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. <span data-ttu-id="36e63-128">Kliknij przycisk **Nowy**.</span><span class="sxs-lookup"><span data-stu-id="36e63-128">Click **New**.</span></span>
   
    ![Przycisk Nowy](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. <span data-ttu-id="36e63-130">Kliknij przycisk **z galerii**.</span><span class="sxs-lookup"><span data-stu-id="36e63-130">Click **From Gallery**.</span></span>
   
    ![Nowa maszyna wirtualna z galerii](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. <span data-ttu-id="36e63-132">Kliknij przycisk **SQL Server 2014 RTM Standard — Windows Server 2012 R2** , a następnie kliknij strzałkę, aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="36e63-132">Click **SQL Server 2014 RTM Standard – Windows Server 2012 R2** and then click the arrow to continue.</span></span>
   
    ![Dalej](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    <span data-ttu-id="36e63-134">Jeśli potrzebujesz danych usług Reporting Services na funkcji subskrypcji, wybierz **programu SQL Server 2014 RTM Enterprise — Windows Server 2012 R2**.</span><span class="sxs-lookup"><span data-stu-id="36e63-134">If you need the Reporting Services data driven subscriptions feature, choose **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span></span> <span data-ttu-id="36e63-135">Aby uzyskać więcej informacji o wersjach programu SQL Server i obsługę funkcji, zobacz [funkcje obsługiwane przez wersje programu SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span><span class="sxs-lookup"><span data-stu-id="36e63-135">For more information on SQL Server editions and feature support, see [Features Supported by the Editions of SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span></span>
6. <span data-ttu-id="36e63-136">Na **konfiguracji maszyny wirtualnej** Edytuj następujące pola:</span><span class="sxs-lookup"><span data-stu-id="36e63-136">On the **Virtual machine configuration** page, edit the following fields:</span></span>
   
   * <span data-ttu-id="36e63-137">Jeśli istnieje więcej niż jeden **Data wydania wersji**, wybierz najnowszą wersję.</span><span class="sxs-lookup"><span data-stu-id="36e63-137">If there is more than one **VERSION RELEASE DATE**, select the most recent version.</span></span>
   * <span data-ttu-id="36e63-138">**Nazwa maszyny wirtualnej**: Nazwa komputera jest używany również na następnej stronie konfiguracji jako domyślną nazwę DNS usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="36e63-138">**Virtual Machine Name**: The machine name is also used on the next configuration page as the default Cloud Service DNS name.</span></span> <span data-ttu-id="36e63-139">Nazwa DNS musi być unikatowa w usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="36e63-139">The DNS name must be unique across the Azure service.</span></span> <span data-ttu-id="36e63-140">Rozważ skonfigurowanie maszyny Wirtualnej z opisujący maszyny Wirtualnej do czego służy nazwą komputera.</span><span class="sxs-lookup"><span data-stu-id="36e63-140">Consider configuring the VM with a computer name that describes what the VM is used for.</span></span> <span data-ttu-id="36e63-141">Na przykład ssrsnativecloud.</span><span class="sxs-lookup"><span data-stu-id="36e63-141">For example ssrsnativecloud.</span></span>
   * <span data-ttu-id="36e63-142">**Warstwa**: standardowy</span><span class="sxs-lookup"><span data-stu-id="36e63-142">**Tier**: Standard</span></span>
   * <span data-ttu-id="36e63-143">**Rozmiar: A3** jest zalecany rozmiar maszyny Wirtualnej dla obciążeń programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="36e63-143">**Size:A3** is the recommended VM size for SQL Server workloads.</span></span> <span data-ttu-id="36e63-144">Jeśli maszyna wirtualna jest używana tylko jako serwer raportów maszyny Wirtualnej o rozmiarze A2 jest wystarczająca, chyba że serwer raportów napotka duże obciążenie.</span><span class="sxs-lookup"><span data-stu-id="36e63-144">If a VM is only used as a report server, a VM size of A2 is sufficient unless the report server experiences a large workload.</span></span> <span data-ttu-id="36e63-145">Dla maszyny Wirtualnej, informacje o cenach, zobacz [cennik maszyn wirtualnych](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="36e63-145">For VM pricing information, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>
   * <span data-ttu-id="36e63-146">**Nową nazwę użytkownika**: podanej nazwie zostanie utworzona jako administrator na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e63-146">**New User Name**: the name you provide is created as an administrator on the VM.</span></span>
   * <span data-ttu-id="36e63-147">**Nowe hasło** i **potwierdzić**.</span><span class="sxs-lookup"><span data-stu-id="36e63-147">**New Password** and **confirm**.</span></span> <span data-ttu-id="36e63-148">To hasło służy do nowego konta administratora i zaleca się, że używasz silne hasło.</span><span class="sxs-lookup"><span data-stu-id="36e63-148">This password is used for the new administrator account and it is recommended you use a strong password.</span></span>
   * <span data-ttu-id="36e63-149">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="36e63-149">Click **Next**.</span></span> <span data-ttu-id="36e63-150">![dalej](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span><span class="sxs-lookup"><span data-stu-id="36e63-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span></span>
7. <span data-ttu-id="36e63-151">Na następnej stronie można edytować następujących pól:</span><span class="sxs-lookup"><span data-stu-id="36e63-151">On the next page, edit the following fields:</span></span>
   
   * <span data-ttu-id="36e63-152">**Usługi w chmurze**: Wybierz **Utwórz nową usługę w chmurze**.</span><span class="sxs-lookup"><span data-stu-id="36e63-152">**Cloud Service**: select **Create a new Cloud Service**.</span></span>
   * <span data-ttu-id="36e63-153">**Nazwa DNS usługi w chmurze**: jest to publiczna nazwa DNS usługa w chmurze, która jest skojarzona z maszyną Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="36e63-153">**Cloud Service DNS Name**: This is the public DNS name of the Cloud Service that is associated with the VM.</span></span> <span data-ttu-id="36e63-154">Domyślna nazwa to nazwa została wpisana nazwa maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e63-154">The default name is the name you typed in for the VM name.</span></span> <span data-ttu-id="36e63-155">Jeśli w kolejnych krokach tego tematu, Utwórz zaufany certyfikat SSL, a następnie nazwa DNS jest używana dla wartości "**wystawiony dla**" certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="36e63-155">If in later steps of the topic, you create a trusted SSL certificate and then the DNS name is used for the value of the “**Issued to**” of the certificate.</span></span>
   * <span data-ttu-id="36e63-156">**Region/koligacji grupy/wirtualnej sieci**: Wybierz region najbliższy użytkownikom końcowym.</span><span class="sxs-lookup"><span data-stu-id="36e63-156">**Region/Affinity Group/Virtual Network**: Choose the region closest to your end users.</span></span>
   * <span data-ttu-id="36e63-157">**Konto magazynu**: Użyj konta magazynu wygenerowanej automatycznie.</span><span class="sxs-lookup"><span data-stu-id="36e63-157">**Storage Account**: Use an automatically generated storage account.</span></span>
   * <span data-ttu-id="36e63-158">**Zestaw dostępności**: Brak.</span><span class="sxs-lookup"><span data-stu-id="36e63-158">**Availability Set**: None.</span></span>
   * <span data-ttu-id="36e63-159">**Punkty końcowe** zachować **pulpitu zdalnego** i **PowerShell** punktów końcowych, a następnie dodaj końcowy HTTP lub HTTPS, w zależności od środowiska.</span><span class="sxs-lookup"><span data-stu-id="36e63-159">**ENDPOINTS** Keep the **Remote Desktop** and **PowerShell** endpoints and then add either an HTTP or HTTPS endpoint, depending on your environment.</span></span>
     
     * <span data-ttu-id="36e63-160">**HTTP**: domyślne porty publiczne i prywatne są **80**.</span><span class="sxs-lookup"><span data-stu-id="36e63-160">**HTTP**: The default public and private ports are **80**.</span></span> <span data-ttu-id="36e63-161">Należy pamiętać, że jeśli korzystanie z prywatnych portu innego niż 80, zmodyfikuj **$HTTPport = 80** w skrypcie http.</span><span class="sxs-lookup"><span data-stu-id="36e63-161">Note that if you use a private port other than 80, modify **$HTTPport = 80** in the http script.</span></span>
     * <span data-ttu-id="36e63-162">**HTTPS**: domyślne porty publiczne i prywatne są **443**.</span><span class="sxs-lookup"><span data-stu-id="36e63-162">**HTTPS**: The default public and private ports are **443**.</span></span> <span data-ttu-id="36e63-163">Ze względów bezpieczeństwa jest zmienić port prywatny i skonfigurować zapory i serwera raportów używać port prywatny.</span><span class="sxs-lookup"><span data-stu-id="36e63-163">A security best practice is to change the private port and configure your firewall and the report server to use the private port.</span></span> <span data-ttu-id="36e63-164">Aby uzyskać więcej informacji dotyczących punktów końcowych, zobacz [jak się komunikacja między z maszyną wirtualną](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="36e63-164">For more information on endpoints, see [How to Set Up Communication with a Virtual Machine](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="36e63-165">Należy pamiętać, że jeśli użyjesz portu innego niż 443, Zmień parametr **$HTTPsport = 443** w skrypcie HTTPS.</span><span class="sxs-lookup"><span data-stu-id="36e63-165">Note that if you use a port other than 443, change the parameter **$HTTPsport = 443** in the HTTPS script.</span></span>
   * <span data-ttu-id="36e63-166">Kliknij przycisk Dalej.</span><span class="sxs-lookup"><span data-stu-id="36e63-166">Click next .</span></span> ![Dalej](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. <span data-ttu-id="36e63-168">Na ostatniej stronie kreatora, zachowaj ustawienie domyślne **Zainstaluj agenta maszyny Wirtualnej** wybrane.</span><span class="sxs-lookup"><span data-stu-id="36e63-168">On the last page of the wizard, keep the default **Install the VM agent** selected.</span></span> <span data-ttu-id="36e63-169">Kroki opisane w tym temacie, nie będą korzystać agenta maszyny Wirtualnej, ale jeśli chcesz zachować tę maszynę Wirtualną, agent maszyny Wirtualnej i rozszerzenia programu umożliwi zwiększenia on CM.</span><span class="sxs-lookup"><span data-stu-id="36e63-169">The steps in this topic do not utilize the VM agent but if you plan to keep this VM, the VM agent and extensions will allow you to enhance he CM.</span></span>  <span data-ttu-id="36e63-170">Aby uzyskać więcej informacji dotyczących agenta maszyny Wirtualnej, zobacz [agenta maszyny Wirtualnej i rozszerzenia — część 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span><span class="sxs-lookup"><span data-stu-id="36e63-170">For more information on the VM agent, see [VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span></span> <span data-ttu-id="36e63-171">Jednym z ad zainstalowanych rozszerzeń domyślne uruchomiona jest rozszerzenie "BGINFO", który wyświetla na pulpicie maszyny Wirtualnej, informacje o systemie, takie jak wewnętrznym adresem IP i wolnego miejsca na dysku.</span><span class="sxs-lookup"><span data-stu-id="36e63-171">One of the default extensions installed ad running is the “BGINFO” extension that displays on the VM desktop, system information such as internal IP and free drive space.</span></span>
9. <span data-ttu-id="36e63-172">Kliknij polecenie ukończone.</span><span class="sxs-lookup"><span data-stu-id="36e63-172">Click complete .</span></span> ![Ok](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. <span data-ttu-id="36e63-174">**Stan** maszyny wirtualnej będzie wyświetlany jako **uruchamianie (inicjowania obsługi administracyjnej)** podczas procesu udostępniania i następnie wyświetlana **systemem** gdy maszyna wirtualna jest inicjowana i są gotowe do użycia.</span><span class="sxs-lookup"><span data-stu-id="36e63-174">The **Status** of the VM displays as **Starting (Provisioning)** during the provision process and then displays as **Running** when the VM is provisioned and ready to use.</span></span>

## <a name="step-2-create-a-server-certificate"></a><span data-ttu-id="36e63-175">Krok 2: Utworzenie certyfikatu serwera</span><span class="sxs-lookup"><span data-stu-id="36e63-175">Step 2: Create a Server Certificate</span></span>
> [!NOTE]
> <span data-ttu-id="36e63-176">Jeśli nie wymagają protokołu HTTPS na serwerze raportów, możesz **pominąć krok 2** i przejdź do sekcji **użyć skryptu, aby skonfigurować serwer raportowania i HTTP**.</span><span class="sxs-lookup"><span data-stu-id="36e63-176">If you do not require HTTPS on the report server, you can **skip step 2** and go to the section **Use script to configure the report server and HTTP**.</span></span> <span data-ttu-id="36e63-177">Użyć skryptu HTTP, aby szybko skonfigurować serwer raportowania i serwer raportów nie będzie gotowe do użycia.</span><span class="sxs-lookup"><span data-stu-id="36e63-177">Use the HTTP script to quickly configure the report server and the report server will be ready to use.</span></span>

<span data-ttu-id="36e63-178">Aby można było używać protokołu HTTPS na maszynie Wirtualnej, należy zaufany certyfikat SSL.</span><span class="sxs-lookup"><span data-stu-id="36e63-178">In order to use HTTPS on the VM, you need a trusted SSL certificate.</span></span> <span data-ttu-id="36e63-179">W zależności od scenariusza można użyć jednej z następujących dwóch metod:</span><span class="sxs-lookup"><span data-stu-id="36e63-179">Depending on your scenario, you can use one of the following two methods:</span></span>

* <span data-ttu-id="36e63-180">Prawidłowy certyfikat SSL wystawiony przez urząd certyfikacji (CA) i zaufany przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="36e63-180">A valid SSL certificate issued by a Certification Authority (CA) and trusted by Microsoft.</span></span> <span data-ttu-id="36e63-181">Certyfikaty głównego urzędu certyfikacji są wymagane za pośrednictwem programu certyfikatów głównych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="36e63-181">The CA root certificates are required to be distributed via the Microsoft Root Certificate Program.</span></span> <span data-ttu-id="36e63-182">Aby uzyskać więcej informacji na temat tego programu, zobacz [systemu Windows i Windows Phone 8 SSL programu certyfikatów głównych (elementu członkowskiego CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) i [wprowadzenie do programu certyfikatów głównych firmy Microsoft](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span><span class="sxs-lookup"><span data-stu-id="36e63-182">For more information about this program, see [Windows and Windows Phone 8 SSL Root Certificate Program (Member CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) and [Introduction to The Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span></span>
* <span data-ttu-id="36e63-183">Certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="36e63-183">A self-signed certificate.</span></span> <span data-ttu-id="36e63-184">Certyfikaty z podpisem własnym nie jest zalecana dla środowisk produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="36e63-184">Self-signed certificates are not recommended for production environments.</span></span>

### <a name="to-use-a-certificate-created-by-a-trusted-certificate-authority-ca"></a><span data-ttu-id="36e63-185">Do korzystania z certyfikatu utworzony przez zaufany urząd certyfikacji</span><span class="sxs-lookup"><span data-stu-id="36e63-185">To use a certificate created by a trusted Certificate Authority (CA)</span></span>
1. <span data-ttu-id="36e63-186">**Żądanie certyfikatu serwera dla witryny sieci Web od urzędu certyfikacji**.</span><span class="sxs-lookup"><span data-stu-id="36e63-186">**Request a server certificate for the website from a certification authority**.</span></span> 
   
    <span data-ttu-id="36e63-187">Generowanie pliku żądania certyfikatu (Certreq.txt), który możesz wysłać do urzędu certyfikacji, lub wygenerować żądanie do urzędu certyfikacji online, można użyć Kreatora certyfikatu serwera sieci Web.</span><span class="sxs-lookup"><span data-stu-id="36e63-187">You can use the Web Server Certificate Wizard either to generate a certificate request file (Certreq.txt) that you send to a certification authority, or to generate a request for an online certification authority.</span></span> <span data-ttu-id="36e63-188">Na przykład usług certyfikatów firmy Microsoft w systemie Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="36e63-188">For example, Microsoft Certificate Services in Windows Server 2012.</span></span> <span data-ttu-id="36e63-189">W zależności od poziomu wiarygodności identyfikacji oferowanego przez dany certyfikat serwera jest kilka dni do kilku miesięcy dla urzędu certyfikacji zatwierdzić Twoje żądanie i wysłanie pliku certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="36e63-189">Depending on the level of identification assurance offered by your server certificate, it is several days to several months for the certification authority to approve your request and send you a certificate file.</span></span> 
   
    <span data-ttu-id="36e63-190">Aby uzyskać więcej informacji na temat żądania certyfikatów serwera zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="36e63-190">For more information about requesting a server certificates, see the following:</span></span> 
   
   * <span data-ttu-id="36e63-191">Użyj [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span><span class="sxs-lookup"><span data-stu-id="36e63-191">Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span></span>
   * <span data-ttu-id="36e63-192">Narzędzia zabezpieczeń do administrowania systemem Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="36e63-192">Security Tools to Administer Windows Server 2012.</span></span>
     
     [<span data-ttu-id="36e63-193">Narzędzia zabezpieczeń do administrowania systemem Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="36e63-193">Security Tools to Administer Windows Server 2012</span></span>](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > <span data-ttu-id="36e63-194">**Wystawiony dla** pola zaufany certyfikat SSL powinna być taka sama jak **nazwa DNS usługi w chmurze** używane dla nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e63-194">The **issued to** field of the trusted SSL certificate should be the same as the **Cloud Service DNS NAME** you used for the new VM.</span></span>

2. <span data-ttu-id="36e63-195">**Zainstaluj certyfikat serwera na serwerze sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="36e63-195">**Install the server certificate on the Web server**.</span></span> <span data-ttu-id="36e63-196">Serwer sieci Web jest w tym przypadku maszyny Wirtualnej, który jest hostem serwera raportów, a witryna internetowa jest tworzona w kolejnych krokach podczas konfigurowania usług Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="36e63-196">The Web server in this case is the VM that hosts the report server and the website is created in later steps when you configure Reporting Services.</span></span> <span data-ttu-id="36e63-197">Aby uzyskać więcej informacji na temat instalowania certyfikatu serwera na serwerze sieci Web za pomocą przystawki MMC certyfikatów, zobacz [zainstalować certyfikat serwera](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="36e63-197">For more information about installing the server certificate on the Web server by using the Certificate MMC snap-in, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
    <span data-ttu-id="36e63-198">Jeśli chcesz użyć skryptu uwzględnionych w tym temacie, aby konfiguracji serwera raportów, wartość certyfikaty **odcisk palca** są wymagane jako parametr skryptu.</span><span class="sxs-lookup"><span data-stu-id="36e63-198">If you want to use the script included with this topic, to configure the report server, the value of the certificates **Thumbprint** is required as a parameter of the script.</span></span> <span data-ttu-id="36e63-199">Zobacz następną sekcję szczegółowe informacje na temat sposobu uzyskania odcisku palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="36e63-199">See the next section for details on how to obtain the thumbprint of the certificate.</span></span>
3. <span data-ttu-id="36e63-200">Przypisz certyfikat serwera na serwerze raportów.</span><span class="sxs-lookup"><span data-stu-id="36e63-200">Assign the server certificate to the report server.</span></span> <span data-ttu-id="36e63-201">Przypisanie jest ukończone w następnej sekcji, podczas konfigurowania serwera raportów.</span><span class="sxs-lookup"><span data-stu-id="36e63-201">The assignment is completed in the next section when you configure the report server.</span></span>

### <a name="to-use-the-virtual-machines-self-signed-certificate"></a><span data-ttu-id="36e63-202">Aby użyć certyfikatu z podpisem własnym maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="36e63-202">To use the Virtual Machines Self-signed Certificate</span></span>
<span data-ttu-id="36e63-203">Certyfikatu z podpisem własnym został utworzony na maszynie Wirtualnej podczas przydzielania został maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e63-203">A self-signed certificate was created on the VM when the VM was provisioned.</span></span> <span data-ttu-id="36e63-204">Certyfikat ma taką samą nazwę jak nazwa DNS maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e63-204">The certificate has the same name as the VM DNS name.</span></span> <span data-ttu-id="36e63-205">W celu uniknięcia błędów certyfikatów, wymagane jest, że certyfikat jest zaufany na samej maszyny Wirtualnej, a także przez wszystkich użytkowników witryny.</span><span class="sxs-lookup"><span data-stu-id="36e63-205">In order to avoid certificate errors, it is required that the certificate is trusted on the VM itself, and also by all users of the site.</span></span>

1. <span data-ttu-id="36e63-206">Aby pochodzi z zaufanego głównego urzędu certyfikacji certyfikatu na lokalnej maszynie Wirtualnej, należy dodać certyfikat do **zaufane główne urzędy certyfikacji**.</span><span class="sxs-lookup"><span data-stu-id="36e63-206">To trust the root CA of the certificate on the Local VM, add the certificate to the **Trusted Root Certification Authorities**.</span></span> <span data-ttu-id="36e63-207">Poniżej znajduje się podsumowanie kroków wymaganych.</span><span class="sxs-lookup"><span data-stu-id="36e63-207">The following is a summary of the steps required.</span></span> <span data-ttu-id="36e63-208">Aby uzyskać szczegółowe instrukcje dotyczące sposobu ufać urzędowi certyfikacji, zobacz [zainstalować certyfikat serwera](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="36e63-208">For detailed steps on how to trust the CA, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
   1. <span data-ttu-id="36e63-209">W klasycznym portalu Azure wybierz maszynę Wirtualną, a następnie kliknij przycisk Połącz.</span><span class="sxs-lookup"><span data-stu-id="36e63-209">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="36e63-210">W zależności od konfiguracji przeglądarki może być monit o zapisanie pliku RDP do połączenia z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="36e63-210">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
      
       ![Połącz z maszyną wirtualną azure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="36e63-212">Użyj nazwy maszyny Wirtualnej użytkownika, nazwę użytkownika i hasło, które zostało skonfigurowane podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e63-212">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
      
       <span data-ttu-id="36e63-213">Na przykład na poniższej ilustracji, Nazwa maszyny Wirtualnej jest **ssrsnativecloud** i nazwa użytkownika jest **testuser**.</span><span class="sxs-lookup"><span data-stu-id="36e63-213">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
      
       ![Nazwa maszyny wirtualnej zawiera logowania](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. <span data-ttu-id="36e63-215">Uruchom mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="36e63-215">Run mmc.exe.</span></span> <span data-ttu-id="36e63-216">Aby uzyskać więcej informacji, zobacz [porady: wyświetlanie certyfikatów w przystawce MMC](https://msdn.microsoft.com/library/ms788967.aspx).</span><span class="sxs-lookup"><span data-stu-id="36e63-216">For more information, see [How to: View Certificates with the MMC Snap-in](https://msdn.microsoft.com/library/ms788967.aspx).</span></span>
   3. <span data-ttu-id="36e63-217">W aplikacji konsoli **pliku** menu Dodaj **certyfikaty** przystawki, wybierz pozycję **konto komputera** po wyświetleniu monitu, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="36e63-217">In the console application **File** menu, add the **Certificates** snap-in, select **Computer Account** when prompted, and then click **Next**.</span></span>
   4. <span data-ttu-id="36e63-218">Wybierz **komputera lokalnego** zarządzać, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="36e63-218">Select **Local Computer** to manage and then click **Finish**.</span></span>
   5. <span data-ttu-id="36e63-219">Kliknij przycisk **Ok** , a następnie rozwiń węzeł **certyfikaty - osobiste** węzłów, a następnie kliknij przycisk **certyfikaty**.</span><span class="sxs-lookup"><span data-stu-id="36e63-219">Click **Ok** and then expand the **Certificates -Personal** nodes and then click **Certificates**.</span></span> <span data-ttu-id="36e63-220">Certyfikat jest nosi nazwę DNS maszyny wirtualnej i kończy **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="36e63-220">The certificate is named after the DNS name of the VM and ends with **cloudapp.net**.</span></span> <span data-ttu-id="36e63-221">Kliknij prawym przyciskiem myszy nazwę certyfikatu, a następnie kliknij przycisk **kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="36e63-221">Right-click the certificate name and click **Copy**.</span></span>
   6. <span data-ttu-id="36e63-222">Rozwiń węzeł **zaufane główne urzędy certyfikacji** węzła, a następnie kliknij prawym przyciskiem myszy **certyfikaty** , a następnie kliknij przycisk **Wklej**.</span><span class="sxs-lookup"><span data-stu-id="36e63-222">Expand the **Trusted Root Certification Authorities** node and then right-click **Certificates** and then click **Paste**.</span></span>
   7. <span data-ttu-id="36e63-223">Aby zweryfikować, kliknij dwukrotnie nazwę certyfikatu w obszarze **zaufane główne urzędy certyfikacji** i sprawdź, czy nie ma żadnych błędów i wyświetlić certyfikat.</span><span class="sxs-lookup"><span data-stu-id="36e63-223">To validate, double click on the certificate name under **Trusted Root Certification Authorities** and verify that there are no errors and you see your certificate.</span></span> <span data-ttu-id="36e63-224">Jeśli chcesz użyć skryptu HTTPS uwzględnionych w tym temacie, aby konfiguracji serwera raportów, wartość certyfikaty **odcisk palca** są wymagane jako parametr skryptu.</span><span class="sxs-lookup"><span data-stu-id="36e63-224">If you want to use the HTTPS script included with this topic, to configure the report server, the value of the certificates **Thumbprint** is required as a parameter of the script.</span></span> <span data-ttu-id="36e63-225">**Aby uzyskać wartość odcisku palca**, wykonaj następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="36e63-225">**To get the thumbprint value**, complete the following.</span></span> <span data-ttu-id="36e63-226">Istnieje również próbkę programu PowerShell do pobrania odcisk palca w sekcji [użyć skryptu, aby skonfigurować serwer raportowania i HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span><span class="sxs-lookup"><span data-stu-id="36e63-226">There is also a PowerShell sample to retrieve the thumbprint in section [Use script to configure the report server and HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span></span>
      
      1. <span data-ttu-id="36e63-227">Kliknij dwukrotnie nazwę certyfikatu, na przykład ssrsnativecloud.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="36e63-227">Double-click the name of the certificate, for example ssrsnativecloud.cloudapp.net.</span></span>
      2. <span data-ttu-id="36e63-228">Kliknij przycisk **szczegóły** kartę.</span><span class="sxs-lookup"><span data-stu-id="36e63-228">Click the **Details** tab.</span></span>
      3. <span data-ttu-id="36e63-229">Kliknij przycisk **odcisk palca**.</span><span class="sxs-lookup"><span data-stu-id="36e63-229">Click **Thumbprint**.</span></span> <span data-ttu-id="36e63-230">Wartość odcisku palca jest wyświetlana w polu szczegółowe informacje, na przykład a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span><span class="sxs-lookup"><span data-stu-id="36e63-230">The value of the thumbprint is displayed in the details field, for example ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span></span>
      4. <span data-ttu-id="36e63-231">Skopiuj odcisk palca i Zapisz wartość do użycia później lub teraz go edytować.</span><span class="sxs-lookup"><span data-stu-id="36e63-231">Copy the thumbprint and save the value for later or edit the script now.</span></span>
      5. <span data-ttu-id="36e63-232">(*) Przed uruchomieniem skryptu Usuń spacje Between par wartości.</span><span class="sxs-lookup"><span data-stu-id="36e63-232">(*) Before you run the script, remove the spaces in between the pairs of values.</span></span> <span data-ttu-id="36e63-233">Na przykład odcisk palca zauważyć przed będzie teraz a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span><span class="sxs-lookup"><span data-stu-id="36e63-233">For example the thumbprint noted before would now be ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span></span>
      6. <span data-ttu-id="36e63-234">Przypisz certyfikat serwera na serwerze raportów.</span><span class="sxs-lookup"><span data-stu-id="36e63-234">Assign the server certificate to the report server.</span></span> <span data-ttu-id="36e63-235">Przypisanie jest ukończone w następnej sekcji, podczas konfigurowania serwera raportów.</span><span class="sxs-lookup"><span data-stu-id="36e63-235">The assignment is completed in the next section when you configure the report server.</span></span>

<span data-ttu-id="36e63-236">Jeśli używasz certyfikatu SSL z podpisem własnym, nazwa certyfikatu już zgodna z nazwą hosta maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e63-236">If you are using a self-signed SSL certificate, the name on the certificate already matches the hostname of the VM.</span></span> <span data-ttu-id="36e63-237">W związku z tym DNS na komputerze jest już zarejestrowany globalnie i jest możliwy za pomocą dowolnego klienta.</span><span class="sxs-lookup"><span data-stu-id="36e63-237">Therefore, the DNS of the machine is already registered globally and can be accessed from any client.</span></span>

## <a name="step-3-configure-the-report-server"></a><span data-ttu-id="36e63-238">Krok 3: Konfigurowanie serwera raportów</span><span class="sxs-lookup"><span data-stu-id="36e63-238">Step 3: Configure the Report Server</span></span>
<span data-ttu-id="36e63-239">Ta sekcja przeprowadzi Cię przez konfigurację maszyny Wirtualnej jako serwera raportów usług Reporting Services w trybie macierzystym.</span><span class="sxs-lookup"><span data-stu-id="36e63-239">This section walks you through configuring the VM as a Reporting Services native mode report server.</span></span> <span data-ttu-id="36e63-240">Jedną z następujących metod umożliwiają skonfigurowanie serwera raportów:</span><span class="sxs-lookup"><span data-stu-id="36e63-240">You can use one of the following methods to configure the report server:</span></span>

* <span data-ttu-id="36e63-241">Użyj skryptu do konfiguracji serwera raportów</span><span class="sxs-lookup"><span data-stu-id="36e63-241">Use the script to configure the report server</span></span>
* <span data-ttu-id="36e63-242">Umożliwia skonfigurowanie serwera raportów programu Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="36e63-242">Use Configuration Manager to Configure the Report Server.</span></span>

<span data-ttu-id="36e63-243">Aby uzyskać bardziej szczegółowe kroki, zobacz sekcję [podłączyć się do maszyny wirtualnej, a następnie uruchom Menedżera konfiguracji usług Reporting Services](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="36e63-243">For more detailed steps, see the section [Connect to the Virtual Machine and Start the Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span></span>

<span data-ttu-id="36e63-244">**Uwierzytelnianie Uwaga:** zalecaną metodą uwierzytelniania jest uwierzytelnianie systemu Windows i jest domyślne uwierzytelnianie usług Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="36e63-244">**Authentication Note:** Windows authentication is the recommended authentication method and it is the default Reporting Services authentication.</span></span> <span data-ttu-id="36e63-245">Tylko użytkownicy, które są skonfigurowane na maszynie Wirtualnej mogą uzyskiwać dostęp do usług Reporting Services i przypisane do ról usług Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="36e63-245">Only users that are configured on the VM can access Reporting Services and assigned to Reporting Services roles.</span></span>

### <a name="use-script-to-configure-the-report-server-and-http"></a><span data-ttu-id="36e63-246">Użyj skryptu do konfigurowania serwera raportów i HTTP</span><span class="sxs-lookup"><span data-stu-id="36e63-246">Use script to configure the report server and HTTP</span></span>
<span data-ttu-id="36e63-247">Aby użyć skryptu programu Windows PowerShell do konfigurowania serwera raportów, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="36e63-247">To use the Windows PowerShell script to configure the report server, complete the following steps.</span></span> <span data-ttu-id="36e63-248">Konfiguracja obejmuje protokołu HTTP, a nie HTTPS:</span><span class="sxs-lookup"><span data-stu-id="36e63-248">The configuration includes HTTP, not HTTPS:</span></span>

1. <span data-ttu-id="36e63-249">W klasycznym portalu Azure wybierz maszynę Wirtualną, a następnie kliknij przycisk Połącz.</span><span class="sxs-lookup"><span data-stu-id="36e63-249">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="36e63-250">W zależności od konfiguracji przeglądarki może być monit o zapisanie pliku RDP do połączenia z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="36e63-250">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
   
    ![Połącz z maszyną wirtualną azure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="36e63-252">Użyj nazwy maszyny Wirtualnej użytkownika, nazwę użytkownika i hasło, które zostało skonfigurowane podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e63-252">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
   
    <span data-ttu-id="36e63-253">Na przykład na poniższej ilustracji, Nazwa maszyny Wirtualnej jest **ssrsnativecloud** i nazwa użytkownika jest **testuser**.</span><span class="sxs-lookup"><span data-stu-id="36e63-253">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
   
    ![Nazwa maszyny wirtualnej zawiera logowania](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="36e63-255">Na Maszynie wirtualnej, należy otworzyć **programu Windows PowerShell ISE** z uprawnieniami administracyjnymi.</span><span class="sxs-lookup"><span data-stu-id="36e63-255">On the VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="36e63-256">PowerShell ISE jest instalowany domyślnie w systemie Windows server 2012.</span><span class="sxs-lookup"><span data-stu-id="36e63-256">The PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="36e63-257">Zaleca się, że używasz zamiast standardowego okna programu Windows PowerShell ISE, aby można wkleić skrypt ISE, zmodyfikuj skrypt, a następnie uruchom skrypt.</span><span class="sxs-lookup"><span data-stu-id="36e63-257">It is recommended you use the ISE instead of a standard Windows PowerShell window so that you can paste the script into the ISE, modify the script, and then run the script.</span></span>
3. <span data-ttu-id="36e63-258">W środowisku Windows PowerShell ISE, kliknij przycisk **widoku** menu, a następnie kliknij przycisk **Pokaż okienko skryptu**.</span><span class="sxs-lookup"><span data-stu-id="36e63-258">In Windows PowerShell ISE, click the **View** menu and then click **Show Script Pane**.</span></span>
4. <span data-ttu-id="36e63-259">Skopiuj poniższy skrypt, a następnie wklej skryptu w okienku skryptów programu Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="36e63-259">Copy the following script, and paste the script into the Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change the value if you used a different port for the private HTTP endpoint when the VM was created.
   
        ## Set PowerShell execution policy to be able to run scripts
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
        ## Change the version portion of the path to "v11" to use the script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting the web service URL ##
        write-host -foregroundcolor green "Setting the web service URL"
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
   
        ## Setting the Database ##
        write-host -foregroundcolor green "Setting the Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating the database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script to create the database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes to sqlserver provider
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
   
        ## Setting the Report Manager URL ##
   
        write-host -foregroundcolor green "Setting the Report Manager URL"
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
5. <span data-ttu-id="36e63-260">Jeśli utworzono maszynę Wirtualną z portem HTTP innych niż 80, zmodyfikuj parametr $HTTPport = 80.</span><span class="sxs-lookup"><span data-stu-id="36e63-260">If you created the VM with an HTTP port other than 80, modify the parameter $HTTPport = 80.</span></span>
6. <span data-ttu-id="36e63-261">Skrypt jest obecnie skonfigurowany dla usług Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="36e63-261">The script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="36e63-262">Jeśli chcesz uruchomić skrypt dla usług Reporting Services, zmodyfikuj wersję część ścieżki do przestrzeni nazw do "v11" w instrukcji Get-WmiObject.</span><span class="sxs-lookup"><span data-stu-id="36e63-262">If you want to run the script for  Reporting Services, modify the version portion of the path to the namespace to “v11”, on the Get-WmiObject statement.</span></span>
7. <span data-ttu-id="36e63-263">Uruchom skrypt.</span><span class="sxs-lookup"><span data-stu-id="36e63-263">Run the script.</span></span>

<span data-ttu-id="36e63-264">**Sprawdzanie poprawności**: Aby sprawdzić, czy działa raportu podstawowe funkcje serwera, zobacz [Sprawdź konfigurację](#verify-the-configuration) później w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="36e63-264">**Validation**: To verify that the basic report server functionality is working, see the [Verify the configuration](#verify-the-configuration) section later in this topic.</span></span>

### <a name="use-script-to-configure-the-report-server-and-https"></a><span data-ttu-id="36e63-265">Użyj skryptu do konfigurowania serwera raportów i HTTPS</span><span class="sxs-lookup"><span data-stu-id="36e63-265">Use script to configure the report server and HTTPS</span></span>
<span data-ttu-id="36e63-266">Aby użyć środowiska Windows PowerShell do konfigurowania serwera raportów, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="36e63-266">To use Windows PowerShell to configure the report server, complete the following steps.</span></span> <span data-ttu-id="36e63-267">Konfiguracja obejmuje protokołu HTTPS, a nie HTTP.</span><span class="sxs-lookup"><span data-stu-id="36e63-267">The configuration includes HTTPS, not HTTP.</span></span>

1. <span data-ttu-id="36e63-268">W klasycznym portalu Azure wybierz maszynę Wirtualną, a następnie kliknij przycisk Połącz.</span><span class="sxs-lookup"><span data-stu-id="36e63-268">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="36e63-269">W zależności od konfiguracji przeglądarki może być monit o zapisanie pliku RDP do połączenia z maszyną wirtualną.</span><span class="sxs-lookup"><span data-stu-id="36e63-269">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
   
    ![Połącz z maszyną wirtualną azure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="36e63-271">Użyj nazwy maszyny Wirtualnej użytkownika, nazwę użytkownika i hasło, które zostało skonfigurowane podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e63-271">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
   
    <span data-ttu-id="36e63-272">Na przykład na poniższej ilustracji, Nazwa maszyny Wirtualnej jest **ssrsnativecloud** i nazwa użytkownika jest **testuser**.</span><span class="sxs-lookup"><span data-stu-id="36e63-272">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
   
    ![Nazwa maszyny wirtualnej zawiera logowania](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="36e63-274">Na Maszynie wirtualnej, należy otworzyć **programu Windows PowerShell ISE** z uprawnieniami administracyjnymi.</span><span class="sxs-lookup"><span data-stu-id="36e63-274">On the VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="36e63-275">PowerShell ISE jest instalowany domyślnie w systemie Windows server 2012.</span><span class="sxs-lookup"><span data-stu-id="36e63-275">The PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="36e63-276">Zaleca się, że używasz zamiast standardowego okna programu Windows PowerShell ISE, aby można wkleić skrypt ISE, zmodyfikuj skrypt, a następnie uruchom skrypt.</span><span class="sxs-lookup"><span data-stu-id="36e63-276">It is recommended you use the ISE instead of a standard Windows PowerShell window so that you can paste the script into the ISE, modify the script, and then run the script.</span></span>
3. <span data-ttu-id="36e63-277">Aby włączyć uruchamianie skryptów, uruchom następujące polecenie programu Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="36e63-277">To enable running scripts, run the following Windows PowerShell command:</span></span>
   
        Set-ExecutionPolicy RemoteSigned
   
    <span data-ttu-id="36e63-278">Następnie możesz uruchomić następujące polecenie, aby zweryfikować zasady:</span><span class="sxs-lookup"><span data-stu-id="36e63-278">You can then run the following to verify the policy:</span></span>
   
        Get-ExecutionPolicy
4. <span data-ttu-id="36e63-279">W **programu Windows PowerShell ISE**, kliknij przycisk **widoku** menu, a następnie kliknij przycisk **Pokaż okienko skryptu**.</span><span class="sxs-lookup"><span data-stu-id="36e63-279">In **Windows PowerShell ISE**, click the **View** menu and then click **Show Script Pane**.</span></span>
5. <span data-ttu-id="36e63-280">Skopiuj poniższy skrypt i wklej go w okienku skryptów programu Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="36e63-280">Copy the following script and paste it into the Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures the report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when the HTTPS endpoint was created.
   
        # You can run the following command to get (.cloudapp.net certificates) so you can copy the thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # The certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # the certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If the certificate is not a wildcard certificate, comment out the following line, and enable the full $DNSNAme reference.
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
   
        write-host "The script will use $DNSNameAndPort as the DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change the version portion of the path to "v11" to use the script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting the web service URL ##
        write-host -foregroundcolor green "Setting the web service URL"
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
   
        ## 2. Setting the Database ##
        write-host -foregroundcolor green "Setting the Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating the database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script to create the database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes to sqlserver provider
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
   
        ## 3. Setting the Report Manager URL ##
   
        write-host -foregroundcolor green "Setting the Report Manager URL"
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
6. <span data-ttu-id="36e63-281">Modyfikowanie **$certificatehash** parametru w skrypcie:</span><span class="sxs-lookup"><span data-stu-id="36e63-281">Modify the **$certificatehash** parameter in the script:</span></span>
   
   * <span data-ttu-id="36e63-282">Jest to **wymagane** parametru.</span><span class="sxs-lookup"><span data-stu-id="36e63-282">This is a **required** parameter.</span></span> <span data-ttu-id="36e63-283">Jeśli nie została zapisana wartość certyfikatu z poprzednich kroków, użyj jednej z następujących metod skopiować wartość skrótu certyfikatu z odciskiem palca certyfikatów.:</span><span class="sxs-lookup"><span data-stu-id="36e63-283">If you did not save the certificate value from the previous steps, use one of the following methods to copy the certificate hash value from the certificates thumbprint.:</span></span>
     
       <span data-ttu-id="36e63-284">Na Maszynie wirtualnej Otwórz program Windows PowerShell ISE, a następnie uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="36e63-284">On the VM, open Windows PowerShell ISE and run the following command:</span></span>
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       <span data-ttu-id="36e63-285">Dane wyjściowe będą podobne do następującego.</span><span class="sxs-lookup"><span data-stu-id="36e63-285">The output will look similar to the following.</span></span> <span data-ttu-id="36e63-286">Jeśli skrypt zwraca pusty wiersz, maszyna wirtualna nie ma certyfikatu skonfigurowanego na przykład, zobacz sekcję [do używania certyfikatu z podpisem własnym maszyn wirtualnych](#to-use-the-virtual-machines-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="36e63-286">If the script returns a blank line, the VM does not have a certificate configured for example, see the section [To use the Virtual Machines Self-signed Certificate](#to-use-the-virtual-machines-self-signed-certificate).</span></span>
     
     <span data-ttu-id="36e63-287">LUB</span><span class="sxs-lookup"><span data-stu-id="36e63-287">OR</span></span>
   * <span data-ttu-id="36e63-288">Uruchom mmc.exe na Maszynie wirtualnej, a następnie dodaj **certyfikaty** przystawki.</span><span class="sxs-lookup"><span data-stu-id="36e63-288">On the VM Run mmc.exe and then add the **Certificates** snap-in.</span></span>
   * <span data-ttu-id="36e63-289">W obszarze **zaufane główne urzędy certyfikacji** węzła kliknij dwukrotnie nazwę certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="36e63-289">Under the **Trusted Root Certificate Authorities** node double-click your certificate name.</span></span> <span data-ttu-id="36e63-290">Jeśli używasz certyfikatu z podpisem własnym maszyny wirtualnej, certyfikat jest nosi nazwę DNS maszyny wirtualnej i kończy **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="36e63-290">If you are using the self-signed certificate of the VM, the certificate is named after the DNS name of the VM and ends with **cloudapp.net**.</span></span>
   * <span data-ttu-id="36e63-291">Kliknij przycisk **szczegóły** kartę.</span><span class="sxs-lookup"><span data-stu-id="36e63-291">Click the **Details** tab.</span></span>
   * <span data-ttu-id="36e63-292">Kliknij przycisk **odcisk palca**.</span><span class="sxs-lookup"><span data-stu-id="36e63-292">Click **Thumbprint**.</span></span> <span data-ttu-id="36e63-293">Wartość odcisku palca jest wyświetlana w polu szczegółowe informacje, na przykład af 11 60 b6 4b 28 8 d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span><span class="sxs-lookup"><span data-stu-id="36e63-293">The value of the thumbprint is displayed in the details field, for example af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span></span>
   * <span data-ttu-id="36e63-294">**Przed uruchomieniem skryptu**, Usuń spacje Between par wartości.</span><span class="sxs-lookup"><span data-stu-id="36e63-294">**Before you run the script**, remove the spaces in between the pairs of values.</span></span> <span data-ttu-id="36e63-295">Na przykład af1160b64b288d890a8212ff6ba9c3664f319048</span><span class="sxs-lookup"><span data-stu-id="36e63-295">For example af1160b64b288d890a8212ff6ba9c3664f319048</span></span>
7. <span data-ttu-id="36e63-296">Modyfikowanie **$httpsport** parametru:</span><span class="sxs-lookup"><span data-stu-id="36e63-296">Modify the **$httpsport** parameter:</span></span> 
   
   * <span data-ttu-id="36e63-297">Jeśli użyto portu 443 dla protokołu HTTPS punktu końcowego nie konieczne zaktualizowanie tego parametru w skrypcie.</span><span class="sxs-lookup"><span data-stu-id="36e63-297">If you used port 443 for the HTTPS endpoint, then you do not need to update this parameter in the script.</span></span> <span data-ttu-id="36e63-298">W przeciwnym razie użyj wartości port wybrany podczas konfigurowania punktu końcowego prywatnej HTTPS na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e63-298">Otherwise use the port value you selected when you configured the HTTPS private endpoint on the VM.</span></span>
8. <span data-ttu-id="36e63-299">Modyfikowanie **$DNSName** parametru:</span><span class="sxs-lookup"><span data-stu-id="36e63-299">Modify the **$DNSName** parameter:</span></span> 
   
   * <span data-ttu-id="36e63-300">Skrypt jest skonfigurowany certyfikat wieloznaczny $DNSName = "+".</span><span class="sxs-lookup"><span data-stu-id="36e63-300">The script is configured for a wild card certificate $DNSName="+".</span></span> <span data-ttu-id="36e63-301">Jeśli to zrobisz, nie ma konfiguracji dla symbolu wieloznacznego powiązanie certyfikatu, komentarz $DNSName ="+"i Włącz następujący wiersz, odwołanie $DNSNAme pełne, ## $DNSName="$server.cloudapp.net".</span><span class="sxs-lookup"><span data-stu-id="36e63-301">If you do no want to configure for a wildcard certificate binding, comment out $DNSName="+" and enable the following line, the full $DNSNAme reference, ##$DNSName="$server.cloudapp.net".</span></span>
     
       <span data-ttu-id="36e63-302">Zmień wartość $DNSName, jeśli nie chcesz użyć nazwy DNS maszyny wirtualnej dla usług Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="36e63-302">Change the $DNSName value if you do not want to use the virtual machine’s DNS name for Reporting Services.</span></span> <span data-ttu-id="36e63-303">Jeśli parametr jest używany, certyfikat musi także użyć tej nazwy i zarejestrować nazwę globalnie na serwerze DNS.</span><span class="sxs-lookup"><span data-stu-id="36e63-303">If you use the parameter, the certificate must also use this name and you register the name globally on a DNS server.</span></span>
9. <span data-ttu-id="36e63-304">Skrypt jest obecnie skonfigurowany dla usług Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="36e63-304">The script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="36e63-305">Jeśli chcesz uruchomić skrypt dla usług Reporting Services, zmodyfikuj wersję część ścieżki do przestrzeni nazw do "v11" w instrukcji Get-WmiObject.</span><span class="sxs-lookup"><span data-stu-id="36e63-305">If you want to run the script for  Reporting Services, modify the version portion of the path to the namespace to “v11”, on the Get-WmiObject statement.</span></span>
10. <span data-ttu-id="36e63-306">Uruchom skrypt.</span><span class="sxs-lookup"><span data-stu-id="36e63-306">Run the script.</span></span>

<span data-ttu-id="36e63-307">**Sprawdzanie poprawności**: Aby sprawdzić, czy działa raportu podstawowe funkcje serwera, zobacz [Sprawdź konfigurację](#verify-the-connection) później w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="36e63-307">**Validation**: To verify that the basic report server functionality is working, see the [Verify the configuration](#verify-the-connection) section later in this topic.</span></span> <span data-ttu-id="36e63-308">Aby zweryfikować certyfikat powiązanie Otwórz wiersz polecenia z uprawnieniami administracyjnymi, a następnie uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="36e63-308">To verify the certificate binding open a command prompt with administrative privileges, and then run the following command:</span></span>

    netsh http show sslcert

<span data-ttu-id="36e63-309">Wynik będzie zawierać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="36e63-309">The result will include the following:</span></span>

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-to-configure-the-report-server"></a><span data-ttu-id="36e63-310">Umożliwia skonfigurowanie serwera raportów programu Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="36e63-310">Use Configuration Manager to Configure the Report Server</span></span>
<span data-ttu-id="36e63-311">Jeśli nie chcesz uruchomić skrypt programu PowerShell do konfigurowania serwera raportów, wykonaj kroki opisane w tej sekcji, aby użyć Menedżera konfiguracji usług Reporting Services w trybie macierzystym do konfiguracji serwera raportów.</span><span class="sxs-lookup"><span data-stu-id="36e63-311">If you do not want to run the PowerShell script to configure the report server, follow the steps in this section to use the Reporting Services native mode configuration manager to configure the report server.</span></span>

1. <span data-ttu-id="36e63-312">W klasycznym portalu Azure wybierz maszynę Wirtualną, a następnie kliknij przycisk Połącz.</span><span class="sxs-lookup"><span data-stu-id="36e63-312">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="36e63-313">Użyj nazwy użytkownika i hasła skonfigurowanego podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e63-313">Use the user name and password you configured when you created the VM.</span></span>
   
    ![Połącz z maszyną wirtualną azure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. <span data-ttu-id="36e63-315">Uruchom usługę Windows update i instalować aktualizacje do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e63-315">Run Windows update and install updates to the VM.</span></span> <span data-ttu-id="36e63-316">Jeśli wymagane jest ponowne uruchomienie maszyny wirtualnej, uruchom ponownie maszynę Wirtualną i ponownie połączyć się z maszyną Wirtualną w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="36e63-316">If a restart of the VM is required, restart the VM and reconnect to the VM from the Azure classic portal.</span></span>
3. <span data-ttu-id="36e63-317">W menu Start na maszynie Wirtualnej, wpisz **usług Reporting Services** , a następnie otwórz **Reporting Services Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="36e63-317">From the Start menu on the VM, type **Reporting Services** and open **Reporting Services Configuration Manager**.</span></span>
4. <span data-ttu-id="36e63-318">Pozostaw wartości domyślne dla **nazwy serwera** i **wystąpienie serwera raportów**.</span><span class="sxs-lookup"><span data-stu-id="36e63-318">Leave the default values for **Server Name** and **Report Server Instance**.</span></span> <span data-ttu-id="36e63-319">Kliknij przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="36e63-319">Click **Connect**.</span></span>
5. <span data-ttu-id="36e63-320">W okienku po lewej stronie kliknij **adres URL usługi sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="36e63-320">In the left pane, click **Web Service URL**.</span></span>
6. <span data-ttu-id="36e63-321">Domyślnie RS jest skonfigurowany dla protokołu HTTP portu 80 z adresem IP "Wszystkie przypisane".</span><span class="sxs-lookup"><span data-stu-id="36e63-321">By default, RS is configured for HTTP port 80 with IP “All Assigned”.</span></span> <span data-ttu-id="36e63-322">Aby dodać HTTPS:</span><span class="sxs-lookup"><span data-stu-id="36e63-322">To add HTTPS:</span></span>
   
   1. <span data-ttu-id="36e63-323">W **certyfikat SSL**: Wybierz certyfikat, którego chcesz użyć, na przykład [Nazwa maszyny Wirtualnej]. cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="36e63-323">In **SSL Certificate**: select the certificate you want to use, for example [VM name].cloudapp.net.</span></span> <span data-ttu-id="36e63-324">Jeśli żadne certyfikaty nie są wyświetlane, zobacz sekcję **krok 2: Utworzenie certyfikatu serwera** informacji na temat instalowania i ufać certyfikatowi na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e63-324">If no certificates are listed, see the section **Step 2: Create a Server Certificate** for information on how to install and trust the certificate on the VM.</span></span>
   2. <span data-ttu-id="36e63-325">W obszarze **SSL Port**: Wybierz 443.</span><span class="sxs-lookup"><span data-stu-id="36e63-325">Under **SSL Port**: choose 443.</span></span> <span data-ttu-id="36e63-326">Jeśli prywatnej punkt końcowy HTTPS jest skonfigurowany w maszynie Wirtualnej z inną port prywatny, w tym miejscu użyć tej wartości.</span><span class="sxs-lookup"><span data-stu-id="36e63-326">If you configured the HTTPS private endpoint in the VM with a different private port, use that value here.</span></span>
   3. <span data-ttu-id="36e63-327">Kliknij przycisk **Zastosuj** i poczekaj na ukończenie tej operacji.</span><span class="sxs-lookup"><span data-stu-id="36e63-327">Click **Apply** and wait for the operation to complete.</span></span>
7. <span data-ttu-id="36e63-328">W okienku po lewej stronie kliknij **bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="36e63-328">In the left pane, click **Database**.</span></span>
   
   1. <span data-ttu-id="36e63-329">Kliknij przycisk **zmienić baza danych**e.</span><span class="sxs-lookup"><span data-stu-id="36e63-329">Click **Change Databas**e.</span></span>
   2. <span data-ttu-id="36e63-330">Kliknij przycisk **Utwórz nową bazę danych serwera raportów** , a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="36e63-330">Click **Create a new report server database** and then click **Next**.</span></span>
   3. <span data-ttu-id="36e63-331">Pozostaw wartość domyślną **nazwy serwera**: co maszyna wirtualna nazwy i pozostaw wartość domyślną **typ uwierzytelniania** jako **bieżącego użytkownika** — **zintegrowane zabezpieczenia**.</span><span class="sxs-lookup"><span data-stu-id="36e63-331">Leave the default **Server Name**: as the VM name and leave the default **Authentication Type** as **Current User** – **Integrated Security**.</span></span> <span data-ttu-id="36e63-332">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="36e63-332">Click **Next**.</span></span>
   4. <span data-ttu-id="36e63-333">Pozostaw wartość domyślną **Nazwa bazy danych** jako **ReportServer** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="36e63-333">Leave the default **Database Name** as **ReportServer** and click **Next**.</span></span>
   5. <span data-ttu-id="36e63-334">Pozostaw wartość domyślną **typ uwierzytelniania** jako **poświadczenia usługi** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="36e63-334">Leave the default **Authentication Type** as **Service Credentials** and click **Next**.</span></span>
   6. <span data-ttu-id="36e63-335">Kliknij przycisk **dalej** na **Podsumowanie** strony.</span><span class="sxs-lookup"><span data-stu-id="36e63-335">Click **Next** on the **Summary** page.</span></span>
   7. <span data-ttu-id="36e63-336">Po zakończeniu konfiguracji kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="36e63-336">When the configuration is complete, click **Finish**.</span></span>
8. <span data-ttu-id="36e63-337">W okienku po lewej stronie kliknij **adres URL Menedżera raportów**.</span><span class="sxs-lookup"><span data-stu-id="36e63-337">In the left pane, click **Report Manager URL**.</span></span> <span data-ttu-id="36e63-338">Pozostaw wartość domyślną **katalogu wirtualnego** jako **raporty** i kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="36e63-338">Leave the default **Virtual Directory** as **Reports** and click **Apply**.</span></span>
9. <span data-ttu-id="36e63-339">Kliknij przycisk **zakończenia** zamknąć Menedżera konfiguracji usług Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="36e63-339">Click **Exit** to close the Reporting Services Configuration Manager.</span></span>

## <a name="step-4-open-windows-firewall-port"></a><span data-ttu-id="36e63-340">Krok 4: Port zapory systemu Windows otwórz</span><span class="sxs-lookup"><span data-stu-id="36e63-340">Step 4: Open Windows Firewall Port</span></span>
> [!NOTE]
> <span data-ttu-id="36e63-341">Jeśli używasz skrypty do konfiguracji serwera raportów można pominąć tę sekcję.</span><span class="sxs-lookup"><span data-stu-id="36e63-341">If you used one of the scripts to configure the report server, you can skip this section.</span></span> <span data-ttu-id="36e63-342">Skrypt uwzględnione krok, aby otworzyć port zapory.</span><span class="sxs-lookup"><span data-stu-id="36e63-342">The script included a step to open the firewall port.</span></span> <span data-ttu-id="36e63-343">Wartość domyślna jest port 80 dla protokołu HTTP i 443 dla protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="36e63-343">The default was port 80 for HTTP and port 443 for HTTPS.</span></span>
> 
> 

<span data-ttu-id="36e63-344">Aby nawiązać połączenie zdalne Menedżera raportów lub serwer raportów na maszynie wirtualnej, punkt końcowy protokołu TCP jest wymagany na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e63-344">To connect remotely to Report Manager or the Report Server on the virtual machine, a TCP Endpoint is required on the VM.</span></span> <span data-ttu-id="36e63-345">Jest wymagany do otwierania tego samego portu w zaporze maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e63-345">It is required to open the same port in the VM’s firewall.</span></span> <span data-ttu-id="36e63-346">Punkt końcowy został utworzony podczas zainicjowano obsługę administracyjną maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e63-346">The endpoint was created when the VM was provisioned.</span></span>

<span data-ttu-id="36e63-347">Ta sekcja zawiera podstawowe informacje dotyczące sposobu otwierania portu zapory.</span><span class="sxs-lookup"><span data-stu-id="36e63-347">This section provides basic information on how to open the firewall port.</span></span> <span data-ttu-id="36e63-348">Aby uzyskać więcej informacji, zobacz [konfigurowania zapory dla dostępu do serwera raportów](https://technet.microsoft.com/library/bb934283.aspx)</span><span class="sxs-lookup"><span data-stu-id="36e63-348">For more information, see [Configure a Firewall for Report Server Access](https://technet.microsoft.com/library/bb934283.aspx)</span></span>

> [!NOTE]
> <span data-ttu-id="36e63-349">Jeśli skrypt jest używany do konfigurowania serwera raportów, możesz pominąć tę sekcję.</span><span class="sxs-lookup"><span data-stu-id="36e63-349">If you used the script to configure the report server, you can skip this section.</span></span> <span data-ttu-id="36e63-350">Skrypt uwzględnione krok, aby otworzyć port zapory.</span><span class="sxs-lookup"><span data-stu-id="36e63-350">The script included a step to open the firewall port.</span></span>
> 
> 

<span data-ttu-id="36e63-351">Jeśli port prywatny jest skonfigurowany do obsługi protokołu HTTPS innego niż 443, zmodyfikuj odpowiednio następujący skrypt.</span><span class="sxs-lookup"><span data-stu-id="36e63-351">If you configured a private port for HTTPS other than 443, modify the following script appropriately.</span></span> <span data-ttu-id="36e63-352">Aby otworzyć port **443** zaporę systemu Windows, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="36e63-352">To open port **443** on the Windows Firewall, complete the following:</span></span>

1. <span data-ttu-id="36e63-353">Otwórz okno programu Windows PowerShell z uprawnieniami administracyjnymi.</span><span class="sxs-lookup"><span data-stu-id="36e63-353">Open a Windows PowerShell window with administrative privileges.</span></span>
2. <span data-ttu-id="36e63-354">Jeśli użyto portu innego niż 443, gdy punkt końcowy HTTPS jest skonfigurowane na maszynie Wirtualnej, Aktualizuj port w następujące polecenie, a następnie uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="36e63-354">If you used a port other than 443 when you configured the HTTPS endpoint on the VM, update the port in the following command and then run the command:</span></span>
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. <span data-ttu-id="36e63-355">Po zakończeniu wykonywania polecenia **Ok** jest wyświetlany w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="36e63-355">When the command completes, **Ok** is displayed in the command prompt.</span></span>

<span data-ttu-id="36e63-356">Aby sprawdzić, czy port jest otwarty, Otwórz okno programu Windows PowerShell i uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="36e63-356">To verify that the port is opened, open a Windows PowerShell window and run the following command:</span></span>

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-the-configuration"></a><span data-ttu-id="36e63-357">Sprawdź konfigurację</span><span class="sxs-lookup"><span data-stu-id="36e63-357">Verify the configuration</span></span>
<span data-ttu-id="36e63-358">Aby sprawdzić, czy raport podstawowe funkcje serwera działa, otwórz przeglądarkę z uprawnieniami administracyjnymi, a następnie przejdź do następujących raportów ad raportu Menedżera serwera adresów URL:</span><span class="sxs-lookup"><span data-stu-id="36e63-358">To verify that the basic report server functionality is now working, open your browser with administrative privileges and then browse to the following report server ad report manager URLS:</span></span>

* <span data-ttu-id="36e63-359">Na Maszynie wirtualnej przejdź do adresu URL serwera raportów:</span><span class="sxs-lookup"><span data-stu-id="36e63-359">On the VM, browse to the report server URL:</span></span>
  
        http://localhost/reportserver
* <span data-ttu-id="36e63-360">Na Maszynie wirtualnej przejdź do adresu URL Menedżera raportów:</span><span class="sxs-lookup"><span data-stu-id="36e63-360">On the VM, browse to the report manger URL:</span></span>
  
        http://localhost/Reports
* <span data-ttu-id="36e63-361">Z komputera lokalnego, przejdź do **zdalnego** raport Manager na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e63-361">From your local computer, browse to the **remote** report Manager on the VM.</span></span> <span data-ttu-id="36e63-362">Aktualizacja nazwy DNS w poniższym przykładzie zależnie od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="36e63-362">Update the DNS name in the following example as appropriate.</span></span> <span data-ttu-id="36e63-363">Po wyświetleniu monitu o podanie hasła, należy użyć poświadczeń administratora utworzony zainicjowano obsługę administracyjną maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e63-363">When prompted for a password, use the administrator credentials you created when the VM was provisioned.</span></span> <span data-ttu-id="36e63-364">Nazwa użytkownika jest [domena]\[nazwa użytkownika] format, w którym domena jest nazwą komputera maszyny Wirtualnej, na przykład ssrsnativecloud\testuser.</span><span class="sxs-lookup"><span data-stu-id="36e63-364">The user name is in the [Domain]\[user name] format, where the domain is the VM computer name, for example ssrsnativecloud\testuser.</span></span> <span data-ttu-id="36e63-365">Jeśli nie używasz HTTP**S**, Usuń **s** w adresie URL.</span><span class="sxs-lookup"><span data-stu-id="36e63-365">If you are not using HTTP**S**, remove the **s** in the URL.</span></span> <span data-ttu-id="36e63-366">W następnej sekcji informacji na temat tworzenia dodatkowych użytkowników na maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e63-366">See the next section for information on creating additional users on VM.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/Reports
* <span data-ttu-id="36e63-367">Z komputera lokalnego przejdź do adresu URL serwera raportów zdalnego.</span><span class="sxs-lookup"><span data-stu-id="36e63-367">From your local computer, browse to the remote report server URL.</span></span> <span data-ttu-id="36e63-368">Aktualizacja nazwy DNS w poniższym przykładzie zależnie od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="36e63-368">Update the DNS name in the following example as appropriate.</span></span> <span data-ttu-id="36e63-369">Jeśli nie używasz protokołu HTTPS, należy usunąć s w adresie URL.</span><span class="sxs-lookup"><span data-stu-id="36e63-369">If you are not using HTTPS, remove the s in the URL.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a><span data-ttu-id="36e63-370">Tworzenie użytkowników i przypisywania ról</span><span class="sxs-lookup"><span data-stu-id="36e63-370">Create Users and Assign Roles</span></span>
<span data-ttu-id="36e63-371">Po konfigurowania i sprawdzania poprawności serwera raportów, typowych zadań administracyjnych jest utworzyć jeden lub więcej użytkowników i przypisywania użytkowników do ról usług Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="36e63-371">After configuring and verifying the report server, a common administrative task is to create one or more users and assign users to Reporting Services roles.</span></span> <span data-ttu-id="36e63-372">Aby uzyskać więcej informacji zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="36e63-372">For more information, see the following:</span></span>

* [<span data-ttu-id="36e63-373">Utwórz konto użytkownika lokalnego</span><span class="sxs-lookup"><span data-stu-id="36e63-373">Create a local user account</span></span>](https://technet.microsoft.com/library/cc770642.aspx)
* <span data-ttu-id="36e63-374">[Przyznaj użytkownikowi dostęp do serwera raportów (Menedżer raportów)](https://msdn.microsoft.com/library/ms156034.aspx))</span><span class="sxs-lookup"><span data-stu-id="36e63-374">[Grant User Access to a Report Server (Report Manager)](https://msdn.microsoft.com/library/ms156034.aspx))</span></span>
* [<span data-ttu-id="36e63-375">Tworzenie i zarządzanie nimi przypisań ról</span><span class="sxs-lookup"><span data-stu-id="36e63-375">Create and Manage Role Assignments</span></span>](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="to-create-and-publish-reports-to-the-azure-virtual-machine"></a><span data-ttu-id="36e63-376">Aby utworzyć i opublikować raporty do maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="36e63-376">To Create and Publish Reports to the Azure Virtual Machine</span></span>
<span data-ttu-id="36e63-377">W poniższej tabeli przedstawiono niektóre opcje, aby opublikować istniejących raportów z komputera lokalnego na serwerze raportów hostowanych na maszynie wirtualnej Microsoft Azure:</span><span class="sxs-lookup"><span data-stu-id="36e63-377">The following table summarizes some of the options available to publish existing reports from an on-premises computer to the report server hosted on the Microsoft Azure Virtual Machine:</span></span>

* <span data-ttu-id="36e63-378">**Skrypt RS.exe**: RS.exe Użyj skryptu, aby skopiować elementy raportu z i istniejącego serwera raportów do maszyny wirtualnej programu Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="36e63-378">**RS.exe script**: Use RS.exe script to copy report items from and existing report server to your Microsoft Azure Virtual Machine.</span></span> <span data-ttu-id="36e63-379">Aby uzyskać więcej informacji, zobacz sekcję "Tryb macierzysty tryb macierzysty — maszyny wirtualnej platformy Microsoft Azure" w [rs.exe usług Reporting Services przykładowy skrypt w celu migracji zawartości między serwerami raportu](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="36e63-379">For more information, see the section “Native mode to Native Mode – Microsoft Azure Virtual Machine” in [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>
* <span data-ttu-id="36e63-380">**Report Builder**: maszyny wirtualnej zawiera kliknięcie — raz wersji programu Microsoft SQL Server Report Builder.</span><span class="sxs-lookup"><span data-stu-id="36e63-380">**Report Builder**: The virtual machine includes the click-once version of Microsoft SQL Server Report Builder.</span></span> <span data-ttu-id="36e63-381">Uruchomienie raportu konstruktora pierwszy na maszynie wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="36e63-381">To start Report builder the first time on the virtual machine:</span></span>
  
  1. <span data-ttu-id="36e63-382">Uruchom przeglądarkę z uprawnieniami administracyjnymi.</span><span class="sxs-lookup"><span data-stu-id="36e63-382">Start your browser with administrative privileges.</span></span>
  2. <span data-ttu-id="36e63-383">Przejdź do Menedżera raportów na maszynie wirtualnej, a następnie kliknij przycisk **Report Builder** na Wstążce.</span><span class="sxs-lookup"><span data-stu-id="36e63-383">Browse to report manager on the virtual machine and click **Report Builder**  in the ribbon.</span></span>
     
     <span data-ttu-id="36e63-384">Aby uzyskać więcej informacji, zobacz [instalowanie, odinstalowywanie i obsługa programu Report Builder](https://technet.microsoft.com/library/dd207038.aspx).</span><span class="sxs-lookup"><span data-stu-id="36e63-384">For more information, see [Installing, Uninstalling, and Supporting Report Builder](https://technet.microsoft.com/library/dd207038.aspx).</span></span>
* <span data-ttu-id="36e63-385">**Programu SQL Server Data Tools: Maszyna wirtualna**: Jeśli utworzono maszynę Wirtualną z programu SQL Server 2012, SQL Server Data Tools jest zainstalowany na maszynie wirtualnej i może służyć do tworzenia **projektów serwera raportów** i raporty na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e63-385">**SQL Server Data Tools: VM**:  If you created the VM with SQL Server 2012, then SQL Server Data Tools is installed on the virtual machine and can be used to create **Report Server Projects** and reports on the virtual machine.</span></span> <span data-ttu-id="36e63-386">SQL Server Data Tools można opublikować raporty do serwera raportów na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e63-386">SQL Server Data Tools can publish the reports to the report server on the virtual machine.</span></span>
  
    <span data-ttu-id="36e63-387">Jeśli utworzono maszynę Wirtualną z programem SQL server 2014, należy zainstalować Biznesowej programu SQL Server Data Tools — dla programu visual Studio.</span><span class="sxs-lookup"><span data-stu-id="36e63-387">If you created the VM with SQL server 2014, you can install SQL Server Data Tools- BI for visual Studio.</span></span> <span data-ttu-id="36e63-388">Aby uzyskać więcej informacji zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="36e63-388">For more information, see the following:</span></span>
  
  * [<span data-ttu-id="36e63-389">Microsoft SQL Server Data Tools - Business Intelligence dla programu Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="36e63-389">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2013</span></span>](https://www.microsoft.com/download/details.aspx?id=42313)
  * [<span data-ttu-id="36e63-390">Microsoft SQL Server Data Tools - Business Intelligence dla programu Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="36e63-390">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012</span></span>](https://www.microsoft.com/download/details.aspx?id=36843)
  * [<span data-ttu-id="36e63-391">SQL Server Data Tools i SQL Server Business Intelligence (SSDT BI)</span><span class="sxs-lookup"><span data-stu-id="36e63-391">SQL Server Data Tools and SQL Server Business Intelligence (SSDT-BI)</span></span>](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* <span data-ttu-id="36e63-392">**Program SQL Server Data Tools: Zdalny**: na komputerze lokalnym, Utwórz projekt usług Reporting Services w programie SQL Server Data Tools, który zawiera raporty usług Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="36e63-392">**SQL Server Data Tools: Remote**:  On your local computer, create a Reporting Services project in SQL Server Data Tools that contains Reporting Services reports.</span></span> <span data-ttu-id="36e63-393">Skonfiguruj projekt w celu nawiązania połączenia adres URL usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="36e63-393">Configure the project to connect to the web service URL.</span></span>
  
    ![Właściwości projektu narzędzia SSDT dla projektu usług SSRS](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* <span data-ttu-id="36e63-395">**Użyj skryptu**: użycie skryptu w celu skopiowania zawartości serwera raportów.</span><span class="sxs-lookup"><span data-stu-id="36e63-395">**Use script**: Use script to copy report server content.</span></span> <span data-ttu-id="36e63-396">Aby uzyskać więcej informacji, zobacz [rs.exe usług Reporting Services przykładowy skrypt w celu migracji zawartości między serwerami raportu](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="36e63-396">For more information, see [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>

## <a name="minimize-cost-if-you-are-not-using-the-vm"></a><span data-ttu-id="36e63-397">Zminimalizować koszty, jeśli nie używasz maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="36e63-397">Minimize cost if you are not using the VM</span></span>
> [!NOTE]
> <span data-ttu-id="36e63-398">Aby zminimalizować koszty dla maszyn wirtualnych platformy Azure nieużywane, zamknij maszynę Wirtualną w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="36e63-398">To minimize charges for your Azure Virtual Machines when not in use, shut down the VM from the Azure classic portal.</span></span> <span data-ttu-id="36e63-399">Jeśli używasz systemu Windows Opcje zasilania wewnątrz maszyny Wirtualnej można zamknąć maszyny Wirtualnej, są nadal naliczane samo dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="36e63-399">If you use the Windows power options inside a VM to shut down the VM, you are still charged the same amount for the VM.</span></span> <span data-ttu-id="36e63-400">Aby zmniejszyć koszty, należy wyłączyć maszynę Wirtualną w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="36e63-400">To reduce charges, you need to shut down the VM in the Azure classic portal.</span></span> <span data-ttu-id="36e63-401">Jeśli maszyna wirtualna nie jest już potrzebny, pamiętaj, aby usunąć maszyny Wirtualnej oraz pliki VHD skojarzonego w celu uniknięcia opłat za magazyn. Aby uzyskać więcej informacji, zobacz sekcję — Często zadawane pytania na [maszyny wirtualne — cennik](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="36e63-401">If you no longer need the VM, remember to delete the VM and the associated .vhd files to avoid storage charges.For more information, see the FAQ section at [Virtual Machines Pricing Details](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>

## <a name="more-information"></a><span data-ttu-id="36e63-402">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="36e63-402">More Information</span></span>
### <a name="resources"></a><span data-ttu-id="36e63-403">Zasoby</span><span class="sxs-lookup"><span data-stu-id="36e63-403">Resources</span></span>
* <span data-ttu-id="36e63-404">Podobne zawartości powiązane z wdrożenia pojedynczego serwera SQL Server Business Intelligence i SharePoint 2013, zobacz [Użyj środowiska Windows PowerShell do tworzenia Azure maszyny Wirtualnej z Biznesowej programu SQL Server i SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span><span class="sxs-lookup"><span data-stu-id="36e63-404">For similar content related to a single server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Use Windows PowerShell to Create an Azure VM With SQL Server BI and SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span></span>
* <span data-ttu-id="36e63-405">Podobne zawartości powiązane do wdrożenia wielu serwerów programu SQL Server Business Intelligence i programu SharePoint 2013, zobacz [wdrożenia programu SQL Server Business Intelligence w maszynach wirtualnych platformy Azure](https://msdn.microsoft.com/library/dn321998.aspx).</span><span class="sxs-lookup"><span data-stu-id="36e63-405">For similar content related to a multi-server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Deploy SQL Server Business Intelligence in Azure Virtual Machines](https://msdn.microsoft.com/library/dn321998.aspx).</span></span>
* <span data-ttu-id="36e63-406">Aby uzyskać informacje ogólne dotyczące wdrożenia programu SQL Server Business Intelligence w maszynach wirtualnych platformy Azure, zobacz [analizy biznesowej programu SQL Server w usłudze Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).</span><span class="sxs-lookup"><span data-stu-id="36e63-406">For General information related to deployments of SQL Server Business Intelligence in Azure Virtual Machines, see [SQL Server Business Intelligence in Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).</span></span>
* <span data-ttu-id="36e63-407">Aby uzyskać więcej informacji o koszt opłat obliczeń platformy Azure, zobacz kartę maszyn wirtualnych [Azure Kalkulator cen](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="36e63-407">For more information about the cost of Azure compute charges, see the Virtual Machines tab of [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span></span>

### <a name="community-content"></a><span data-ttu-id="36e63-408">Zawartość społeczności</span><span class="sxs-lookup"><span data-stu-id="36e63-408">Community Content</span></span>
* <span data-ttu-id="36e63-409">Aby uzyskać instrukcje krok po kroku dotyczące sposobu tworzenia natywnych usług raportowania serwera raportów tryb bez użycia skryptu, zobacz [Hosting usług SQL Reporting Services na maszynie wirtualnej platformy Azure](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span><span class="sxs-lookup"><span data-stu-id="36e63-409">For step by step instructions on how to create a Reporting Services Native mode report server without using script, see [Hosting SQL Reporting Service on Azure Virtual Machine](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span></span>

### <a name="links-to-other-resources-for-sql-server-in-azure-vms"></a><span data-ttu-id="36e63-410">Linki do innych zasobów dla programu SQL Server na maszynach wirtualnych Azure</span><span class="sxs-lookup"><span data-stu-id="36e63-410">Links to other resources for SQL Server in Azure VMs</span></span>
[<span data-ttu-id="36e63-411">Program SQL Server na maszynach wirtualnych platformy Azure — omówienie</span><span class="sxs-lookup"><span data-stu-id="36e63-411">SQL Server on Azure Virtual Machines Overview</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

