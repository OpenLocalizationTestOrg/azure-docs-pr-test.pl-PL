---
title: "Wprowadzenie do korzystania z usługi Konfiguracja DSC automatyzacji Azure | Dokumentacja firmy Microsoft"
description: "Objaśnienie i przykłady typowych zadań w żądany stan konfiguracji (Konfiguracja DSC automatyzacji Azure)"
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: a3816593-70a3-403b-9a43-d5555fd2cee2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/21/2016
ms.author: magoedte;eslesar
ms.openlocfilehash: 8a10d961ad7c107c68b57c64ee6c88544ff8832b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a><span data-ttu-id="05951-103">Wprowadzenie do korzystania z usługi Konfiguracja DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="05951-103">Getting started with Azure Automation DSC</span></span>
<span data-ttu-id="05951-104">W tym temacie opisano sposób wykonywania typowych zadań z żądanego stanu konfiguracji (Konfiguracja DSC automatyzacji Azure), takie jak tworzenie, importowanie i konfiguracje, dołączania urządzenia do zarządzania, kompilowanie i wyświetlania raportów.</span><span class="sxs-lookup"><span data-stu-id="05951-104">This topic explains how to do the most common tasks with Azure Automation Desired State Configuration (DSC), such as creating, importing, and compiling configurations, onboarding machines to manage, and viewing reports.</span></span> <span data-ttu-id="05951-105">Omówienie jakie Konfiguracja DSC automatyzacji Azure jest, zobacz [Przegląd usługi Konfiguracja DSC automatyzacji Azure](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="05951-105">For an overview of what Azure Automation DSC is, see [Azure Automation DSC Overview](automation-dsc-overview.md).</span></span> <span data-ttu-id="05951-106">Dokumentacja usługi Konfiguracja DSC w temacie [żądany stan konfiguracji Omówienie środowiska Windows PowerShell](https://msdn.microsoft.com/PowerShell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="05951-106">For DSC documentation, see [Windows PowerShell Desired State Configuration Overview](https://msdn.microsoft.com/PowerShell/dsc/overview).</span></span>

<span data-ttu-id="05951-107">Ten temat zawiera przewodnik krok po kroku przy użyciu usługi Konfiguracja DSC automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="05951-107">This topic provides a step-by-step guide to using Azure Automation DSC.</span></span> <span data-ttu-id="05951-108">Chcąc środowiska próbki, który został już skonfigurowany bez wykonanie kroków opisanych w tym temacie, można użyć [następujący szablon ARM](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span><span class="sxs-lookup"><span data-stu-id="05951-108">If you want a sample environment that is already set up without following the steps described in this topic, you can use [the following ARM template](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span></span> <span data-ttu-id="05951-109">Ten szablon ustawia ukończone środowiska Konfiguracja DSC automatyzacji Azure, łącznie z maszyny Wirtualnej platformy Azure, który jest zarządzany przez Konfiguracja DSC automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="05951-109">This template sets up a completed Azure Automation DSC environment, including an Azure VM that is managed by Azure Automation DSC.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05951-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="05951-110">Prerequisites</span></span>
<span data-ttu-id="05951-111">Aby ukończyć przykłady przedstawione w tym temacie, wymagane są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="05951-111">To complete the examples in this topic, the following are required:</span></span>

* <span data-ttu-id="05951-112">Konto usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="05951-112">An Azure Automation account.</span></span> <span data-ttu-id="05951-113">Aby uzyskać instrukcje dotyczące tworzenia konta automatyzacji Uruchom jako platformy Azure, zobacz [Azure konta Uruchom jako](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="05951-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>
* <span data-ttu-id="05951-114">Maszyna wirtualna Azure Resource Manager (nie klasycznego) systemem Windows Server 2008 R2 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="05951-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span></span> <span data-ttu-id="05951-115">Aby uzyskać instrukcje dotyczące tworzenia maszyny Wirtualnej, zobacz [tworzenie pierwszej maszyny wirtualnej systemu Windows w portalu Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="05951-115">For instructions on creating a VM, see [Create your first Windows virtual machine in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span></span>

## <a name="creating-a-dsc-configuration"></a><span data-ttu-id="05951-116">Tworzenie konfiguracji DSC</span><span class="sxs-lookup"><span data-stu-id="05951-116">Creating a DSC configuration</span></span>
<span data-ttu-id="05951-117">Utworzymy prostą [konfiguracji DSC](https://msdn.microsoft.com/powershell/dsc/configurations) dzięki temu obecności lub braku **serwera sieci Web** Windows funkcji (IIS), w zależności od tego, jak przypisać węzłów.</span><span class="sxs-lookup"><span data-stu-id="05951-117">We will create a simple [DSC configuration](https://msdn.microsoft.com/powershell/dsc/configurations) that ensures either the presence or absence of the **Web-Server** Windows Feature (IIS), depending on how you assign nodes.</span></span>

1. <span data-ttu-id="05951-118">Uruchom program Windows PowerShell ISE (lub dowolnym edytorze tekstów).</span><span class="sxs-lookup"><span data-stu-id="05951-118">Start the Windows PowerShell ISE (or any text editor).</span></span>
2. <span data-ttu-id="05951-119">Wpisz następujący tekst:</span><span class="sxs-lookup"><span data-stu-id="05951-119">Type the following text:</span></span>
   
    ```powershell
    configuration TestConfig
    {
        Node WebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Present'
                Name                 = 'Web-Server'
                IncludeAllSubFeature = $true
   
            }
        }
   
        Node NotWebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Absent'
                Name                 = 'Web-Server'
   
            }
        }
        }
    ```
3. <span data-ttu-id="05951-120">Zapisz plik jako `TestConfig.ps1`.</span><span class="sxs-lookup"><span data-stu-id="05951-120">Save the file as `TestConfig.ps1`.</span></span>

<span data-ttu-id="05951-121">Ta konfiguracja wymaga jednego zasobu w każdym węźle bloku, [WindowsFeature zasobów](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), który zapewnia obecności lub braku **serwera sieci Web** funkcji.</span><span class="sxs-lookup"><span data-stu-id="05951-121">This configuration calls one resource in each node block, the [WindowsFeature resource](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), that ensures either the presence or absence of the **Web-Server** feature.</span></span>

## <a name="importing-a-configuration-into-azure-automation"></a><span data-ttu-id="05951-122">Importowanie konfiguracji usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="05951-122">Importing a configuration into Azure Automation</span></span>
<span data-ttu-id="05951-123">Firma Microsoft będzie następnie importowania konfiguracji, do konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="05951-123">Next, we'll import the configuration into the Automation account.</span></span>

1. <span data-ttu-id="05951-124">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="05951-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="05951-125">W menu centralnym kliknij **wszystkie zasoby** , a następnie nazwę konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="05951-125">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="05951-126">Na **konto automatyzacji** bloku, kliknij przycisk **konfiguracji DSC**.</span><span class="sxs-lookup"><span data-stu-id="05951-126">On the **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="05951-127">Na **konfiguracji DSC** bloku, kliknij przycisk **dodać konfigurację**.</span><span class="sxs-lookup"><span data-stu-id="05951-127">On the **DSC Configurations** blade, click **Add a configuration**.</span></span>
5. <span data-ttu-id="05951-128">Na **konfigurację importu** przejdź do bloku `TestConfig.ps1` plik na komputerze.</span><span class="sxs-lookup"><span data-stu-id="05951-128">On the **Import Configuration** blade, browse to the `TestConfig.ps1` file on your computer.</span></span>
   
    ![Zrzut ekranu przedstawiający ** importowania konfiguracji ** bloku](./media/automation-dsc-getting-started/AddConfig.png)
6. <span data-ttu-id="05951-130">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="05951-130">Click **OK**.</span></span>

## <a name="viewing-a-configuration-in-azure-automation"></a><span data-ttu-id="05951-131">Wyświetlanie konfiguracji w usłudze Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="05951-131">Viewing a configuration in Azure Automation</span></span>
<span data-ttu-id="05951-132">Po zaimportowaniu konfiguracji, można go wyświetlić w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="05951-132">After you have imported a configuration, you can view it in the Azure portal.</span></span>

1. <span data-ttu-id="05951-133">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="05951-133">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="05951-134">W menu centralnym kliknij **wszystkie zasoby** , a następnie nazwę konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="05951-134">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="05951-135">Na **konto automatyzacji** bloku, kliknij przycisk **konfiguracji DSC**</span><span class="sxs-lookup"><span data-stu-id="05951-135">On the **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="05951-136">Na **konfiguracji DSC** bloku, kliknij przycisk **TestConfig** (jest to nazwa konfiguracji zaimportowany w poprzedniej procedurze).</span><span class="sxs-lookup"><span data-stu-id="05951-136">On the **DSC Configurations** blade, click **TestConfig** (this is the name of the configuration you imported in the previous procedure).</span></span>
5. <span data-ttu-id="05951-137">Na **konfiguracji TestConfig** bloku, kliknij przycisk **źródło konfiguracji widoku**.</span><span class="sxs-lookup"><span data-stu-id="05951-137">On the **TestConfig Configuration** blade, click **View configuration source**.</span></span>
   
    ![Zrzut ekranu przedstawiający blok konfiguracji TestConfig](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    <span data-ttu-id="05951-139">A **źródło konfiguracji TestConfig** zostanie otwarty blok zawierający kod programu PowerShell dla konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="05951-139">A **TestConfig Configuration source** blade opens, displaying the PowerShell code for the configuration.</span></span>

## <a name="compiling-a-configuration-in-azure-automation"></a><span data-ttu-id="05951-140">Kompilowanie konfiguracji w usłudze Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="05951-140">Compiling a configuration in Azure Automation</span></span>
<span data-ttu-id="05951-141">Przed żądanego stanu można stosować do węzła, konfiguracji DSC definiowanie tego stanu musi być skompilowany w co najmniej jednej konfiguracji węzła (MOF dokumentu) i umieszczone na serwerze ściągania usługi Konfiguracja DSC automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="05951-141">Before you can apply a desired state to a node, a DSC configuration defining that state must be compiled into one or more node configurations (MOF document), and placed on the Automation DSC Pull Server.</span></span> <span data-ttu-id="05951-142">Aby uzyskać bardziej szczegółowy opis kompilowania konfiguracji DSC automatyzacji Azure, zobacz [kompilowania konfiguracji DSC automatyzacji Azure](automation-dsc-compile.md).</span><span class="sxs-lookup"><span data-stu-id="05951-142">For a more detailed description of compiling configurations in Azure Automation DSC, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md).</span></span> <span data-ttu-id="05951-143">Aby uzyskać więcej informacji o kompilacji konfiguracji, zobacz [konfiguracji DSC](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span><span class="sxs-lookup"><span data-stu-id="05951-143">For more information about compiling configurations, see [DSC Configurations](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span></span>

1. <span data-ttu-id="05951-144">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="05951-144">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="05951-145">W menu centralnym kliknij **wszystkie zasoby** , a następnie nazwę konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="05951-145">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="05951-146">Na **konto automatyzacji** bloku, kliknij przycisk **konfiguracji DSC**</span><span class="sxs-lookup"><span data-stu-id="05951-146">On the **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="05951-147">Na **konfiguracji DSC** bloku, kliknij przycisk **TestConfig** (nazwa poprzednio zaimportowanego konfiguracji).</span><span class="sxs-lookup"><span data-stu-id="05951-147">On the **DSC Configurations** blade, click **TestConfig** (the name of the previously imported configuration).</span></span>
5. <span data-ttu-id="05951-148">Na **konfiguracji TestConfig** bloku, kliknij przycisk **skompilować**, a następnie kliknij przycisk **tak**.</span><span class="sxs-lookup"><span data-stu-id="05951-148">On the **TestConfig Configuration** blade, click **Compile**, and then click **Yes**.</span></span> <span data-ttu-id="05951-149">Spowoduje to uruchomienie zadania kompilacji.</span><span class="sxs-lookup"><span data-stu-id="05951-149">This starts a compilation job.</span></span>
   
    ![Zrzut ekranu przedstawiający blok konfiguracji TestConfig wyróżnianie przycisk kompilacji](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> <span data-ttu-id="05951-151">Podczas kompilowania konfiguracji w automatyzacji Azure automatycznie wdraża żadnej konfiguracji węzła utworzonego za na serwerze ściągania.</span><span class="sxs-lookup"><span data-stu-id="05951-151">When you compile a configuration in Azure Automation, it automatically deploys any created node configuration MOFs to the pull server.</span></span>
> 
> 

## <a name="viewing-a-compilation-job"></a><span data-ttu-id="05951-152">Wyświetlanie zadania kompilacji</span><span class="sxs-lookup"><span data-stu-id="05951-152">Viewing a compilation job</span></span>
<span data-ttu-id="05951-153">Po rozpoczęciu kompilacji, możesz je wyświetlić w **zadań kompilacji** kafelka w **konfiguracji** bloku.</span><span class="sxs-lookup"><span data-stu-id="05951-153">After you start a compilation, you can view it in the **Compilation jobs** tile in the **Configuration** blade.</span></span> <span data-ttu-id="05951-154">**Zadań kompilacji** zawiera obecnie uruchomiona, zakończone oraz zadania zakończone niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="05951-154">The **Compilation jobs** tile shows currently running, completed, and failed jobs.</span></span> <span data-ttu-id="05951-155">Po otwarciu bloku zadania kompilacji zawiera informacje dotyczące tego zadania, w tym wszelkie błędy lub ostrzeżenia napotkał, parametry wejściowe używane w konfiguracji i kompilacja dzienników.</span><span class="sxs-lookup"><span data-stu-id="05951-155">When you open a compilation job blade, it shows information about that job including any errors or warnings encountered, input parameters used in the configuration, and compilation logs.</span></span>

1. <span data-ttu-id="05951-156">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="05951-156">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="05951-157">W menu centralnym kliknij **wszystkie zasoby** , a następnie nazwę konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="05951-157">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="05951-158">Na **konto automatyzacji** bloku, kliknij przycisk **konfiguracji DSC**.</span><span class="sxs-lookup"><span data-stu-id="05951-158">On the **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="05951-159">Na **konfiguracji DSC** bloku, kliknij przycisk **TestConfig** (nazwa poprzednio zaimportowanego konfiguracji).</span><span class="sxs-lookup"><span data-stu-id="05951-159">On the **DSC Configurations** blade, click **TestConfig** (the name of the previously imported configuration).</span></span>
5. <span data-ttu-id="05951-160">Na **zadań kompilacji** kafelku **konfiguracji TestConfig** bloku, kliknij jedną z wymienionych zadań.</span><span class="sxs-lookup"><span data-stu-id="05951-160">On the **Compilation jobs** tile of the **TestConfig Configuration** blade, click on any of the jobs listed.</span></span> <span data-ttu-id="05951-161">A **zadania kompilacji** otwartym bloku z datą rozpoczęcia zadania kompilacji.</span><span class="sxs-lookup"><span data-stu-id="05951-161">A **Compilation Job** blade opens, labeled with the date that the compilation job was started.</span></span>
   
    ![Zrzut ekranu przedstawiający blok zadania kompilacji](./media/automation-dsc-getting-started/CompilationJob.png)
6. <span data-ttu-id="05951-163">Kliknij Kafelek w **zadania kompilacji** bloku, aby zobaczyć więcej szczegółowych informacji o zadaniu.</span><span class="sxs-lookup"><span data-stu-id="05951-163">Click on any tile in the **Compilation Job** blade to see further details about the job.</span></span>

## <a name="viewing-node-configurations"></a><span data-ttu-id="05951-164">Wyświetlanie konfiguracji węzłów</span><span class="sxs-lookup"><span data-stu-id="05951-164">Viewing node configurations</span></span>
<span data-ttu-id="05951-165">Pomyślne zakończenie zadania kompilacji tworzy nowy co najmniej jednej konfiguracji węzła.</span><span class="sxs-lookup"><span data-stu-id="05951-165">Successful completion of a compilation job creates one or more new node configurations.</span></span> <span data-ttu-id="05951-166">Konfiguracja węzła jest dokumentem MOF, który jest wdrożony na serwerze ściągania i są gotowe do można ściągnąć i stosowane przez co najmniej jeden węzeł.</span><span class="sxs-lookup"><span data-stu-id="05951-166">A node configuration is a MOF document that is deployed to the pull server and ready to be pulled and applied by one or more nodes.</span></span> <span data-ttu-id="05951-167">Konfiguracje węzłów można wyświetlić w Twoje konto usługi Automatyzacja w **konfiguracji węzłów DSC** bloku.</span><span class="sxs-lookup"><span data-stu-id="05951-167">You can view the node configurations in your Automation account in the **DSC Node Configurations** blade.</span></span> <span data-ttu-id="05951-168">Konfiguracja węzła ma nazwę w postaci *ConfigurationName*. *NodeName*.</span><span class="sxs-lookup"><span data-stu-id="05951-168">A node configuration has a name with the form *ConfigurationName*.*NodeName*.</span></span>

1. <span data-ttu-id="05951-169">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="05951-169">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="05951-170">W menu centralnym kliknij **wszystkie zasoby** , a następnie nazwę konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="05951-170">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="05951-171">Na **konto automatyzacji** bloku, kliknij przycisk **konfiguracji węzłów DSC**.</span><span class="sxs-lookup"><span data-stu-id="05951-171">On the **Automation account** blade, click **DSC Node Configurations**.</span></span>
   
    ![Zrzut ekranu przedstawiający blok konfiguracji węzłów DSC](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a><span data-ttu-id="05951-173">Dołączanie maszyny Wirtualnej platformy Azure do zarządzania z usługi Konfiguracja DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="05951-173">Onboarding an Azure VM for management with Azure Automation DSC</span></span>
<span data-ttu-id="05951-174">Konfiguracja DSC automatyzacji Azure umożliwia zarządzanie maszynach wirtualnych platformy Azure (Classic i Resource Manager), lokalnych maszyn wirtualnych systemu Linux maszyny, usług AWS maszyn wirtualnych i fizycznych komputerach lokalnych.</span><span class="sxs-lookup"><span data-stu-id="05951-174">You can use Azure Automation DSC to manage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span></span> <span data-ttu-id="05951-175">W tym temacie firma Microsoft opisano jak dołączyć tylko usługi Azure Resource Manager maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="05951-175">In this topic, we cover how to onboard only Azure Resource Manager VMs.</span></span> <span data-ttu-id="05951-176">Uzyskać informacji na temat dołączania innych typów urządzeń, zobacz [dołączania komputerów do zarządzania przez Konfiguracja DSC automatyzacji Azure](automation-dsc-onboarding.md).</span><span class="sxs-lookup"><span data-stu-id="05951-176">For information about onboarding other types of machines, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md).</span></span>

### <a name="to-onboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a><span data-ttu-id="05951-177">Dołączyć maszyny Wirtualnej platformy Azure Resource Manager do zarządzania przez Konfiguracja DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="05951-177">To onboard an Azure Resource Manager VM for management by Azure Automation DSC</span></span>
1. <span data-ttu-id="05951-178">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="05951-178">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="05951-179">W menu centralnym kliknij **wszystkie zasoby** , a następnie nazwę konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="05951-179">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="05951-180">Na **konto automatyzacji** bloku, kliknij przycisk **węzłów DSC**.</span><span class="sxs-lookup"><span data-stu-id="05951-180">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="05951-181">W **węzłów DSC** bloku, kliknij przycisk **dodać maszyny Wirtualnej Azure**.</span><span class="sxs-lookup"><span data-stu-id="05951-181">In the **DSC Nodes** blade, click **Add Azure VM**.</span></span>
   
    ![Zrzut ekranu przedstawiający blok węzłów DSC wyróżnianie przycisku Dodaj maszyny Wirtualnej Azure](./media/automation-dsc-getting-started/OnboardVM.png)
5. <span data-ttu-id="05951-183">W **Dodaj maszyny wirtualne Azure** bloku, kliknij przycisk **wybierz maszyny wirtualne do dołączenia**.</span><span class="sxs-lookup"><span data-stu-id="05951-183">In the **Add Azure VMs** blade, click **Select virtual machines to onboard**.</span></span>
6. <span data-ttu-id="05951-184">W **wybierz maszyny wirtualne** bloku, zaznacz maszyny Wirtualnej chcesz dołączyć i kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="05951-184">In the **Select VMs** blade, select the VM you want to onboard, and click **OK**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="05951-185">Musi to być maszyny Wirtualnej platformy Azure Resource Manager systemem Windows Server 2008 R2 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="05951-185">This must be an Azure Resource Manager VM running Windows Server 2008 R2 or later.</span></span>
   > 
   > 
7. <span data-ttu-id="05951-186">W **Dodaj maszyny wirtualne Azure** bloku, kliknij przycisk **Konfigurowanie danych rejestracji**.</span><span class="sxs-lookup"><span data-stu-id="05951-186">In the **Add Azure VMs** blade, click **Configure registration data**.</span></span>
8. <span data-ttu-id="05951-187">W **rejestracji** bloku, wprowadź nazwę konfiguracji węzła, który chcesz zastosować do maszyny Wirtualnej w ramach **Nazwa konfiguracji węzła** pole.</span><span class="sxs-lookup"><span data-stu-id="05951-187">In the **Registration** blade, enter the name of the node configuration you want to apply to the VM in the **Node Configuration Name** box.</span></span> <span data-ttu-id="05951-188">To musi dokładnie odpowiadać Nazwa konfiguracji węzła, w ramach konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="05951-188">This must exactly match the name of a node configuration in the Automation account.</span></span> <span data-ttu-id="05951-189">W tym momencie podanie nazwy jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="05951-189">Providing a name at this point is optional.</span></span> <span data-ttu-id="05951-190">Można zmienić konfiguracji węzła przypisanej po dołączania węzła.</span><span class="sxs-lookup"><span data-stu-id="05951-190">You can change the assigned node configuration after onboarding the node.</span></span>
   <span data-ttu-id="05951-191">Sprawdź **ponowny rozruch węzła, w razie potrzeby**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="05951-191">Check **Reboot Node if Needed**, and then click **OK**.</span></span>
   
    ![Zrzut ekranu przedstawiający blok rejestracji](./media/automation-dsc-getting-started/RegisterVM.png)
   
    <span data-ttu-id="05951-193">Konfiguracja węzła określonego zostaną zastosowane do maszyny Wirtualnej w odstępach czasu określonych przez **częstotliwość trybu konfiguracji**, a maszyna wirtualna będzie sprawdzać dostępność aktualizacji konfiguracji węzła w odstępach czasu określonych przez  **Częstotliwość odświeżania**.</span><span class="sxs-lookup"><span data-stu-id="05951-193">The node configuration you specified will be applied to the VM at intervals specified by the **Configuration Mode Frequency**, and the VM will check for updates to the node configuration at intervals specified by the **Refresh Frequency**.</span></span> <span data-ttu-id="05951-194">Aby uzyskać więcej informacji na temat korzystania z tych wartości, zobacz [Konfigurowanie lokalny program Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span><span class="sxs-lookup"><span data-stu-id="05951-194">For more information about how these values are used, see [Configuring the Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span></span>
9. <span data-ttu-id="05951-195">W **Dodaj maszyny wirtualne Azure** bloku, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="05951-195">In the **Add Azure VMs** blade, click **Create**.</span></span>

<span data-ttu-id="05951-196">Azure uruchomi proces przechodzenia do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="05951-196">Azure will start the process of onboarding the VM.</span></span> <span data-ttu-id="05951-197">Po zakończeniu maszyny Wirtualnej będą widoczne w **węzłów DSC** bloku na koncie automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="05951-197">When it is complete, the VM will show up in the **DSC Nodes** blade in the Automation account.</span></span>

## <a name="viewing-the-list-of-dsc-nodes"></a><span data-ttu-id="05951-198">Wyświetlanie listy węzłów DSC</span><span class="sxs-lookup"><span data-stu-id="05951-198">Viewing the list of DSC nodes</span></span>
<span data-ttu-id="05951-199">Można wyświetlić listę wszystkich komputerach, które zostały został załadowany do zarządzania na Twoim koncie automatyzacji w **węzłów DSC** bloku.</span><span class="sxs-lookup"><span data-stu-id="05951-199">You can view the list of all machines that have been onboarded for management in your Automation account in the **DSC Nodes** blade.</span></span>

1. <span data-ttu-id="05951-200">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="05951-200">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="05951-201">W menu centralnym kliknij **wszystkie zasoby** , a następnie nazwę konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="05951-201">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="05951-202">Na **konto automatyzacji** bloku, kliknij przycisk **węzłów DSC**.</span><span class="sxs-lookup"><span data-stu-id="05951-202">On the **Automation account** blade, click **DSC Nodes**.</span></span>

## <a name="viewing-reports-for-dsc-nodes"></a><span data-ttu-id="05951-203">Wyświetlanie raportów węzłów DSC</span><span class="sxs-lookup"><span data-stu-id="05951-203">Viewing reports for DSC nodes</span></span>
<span data-ttu-id="05951-204">Zawsze Konfiguracja DSC automatyzacji Azure przeprowadza sprawdzanie spójności na węzeł zarządzany, węzeł wysyła raport o stanie z powrotem do serwera ściągania.</span><span class="sxs-lookup"><span data-stu-id="05951-204">Each time Azure Automation DSC performs a consistency check on a managed node, the node sends a status report back to the pull server.</span></span> <span data-ttu-id="05951-205">Raporty te można wyświetlić w bloku dla tego węzła.</span><span class="sxs-lookup"><span data-stu-id="05951-205">You can view these reports on the blade for that node.</span></span>

1. <span data-ttu-id="05951-206">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="05951-206">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="05951-207">W menu centralnym kliknij **wszystkie zasoby** , a następnie nazwę konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="05951-207">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="05951-208">Na **konto automatyzacji** bloku, kliknij przycisk **węzłów DSC**.</span><span class="sxs-lookup"><span data-stu-id="05951-208">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="05951-209">Na **raporty** kafelka, kliknij dowolną raporty na liście.</span><span class="sxs-lookup"><span data-stu-id="05951-209">On the **Reports** tile, click on any of the reports in the list.</span></span>
   
    ![Zrzut ekranu przedstawiający blok raportu](./media/automation-dsc-getting-started/NodeReport.png)

<span data-ttu-id="05951-211">Na bloku dla konkretnego raportu można wyświetlić następujące informacje o stanie dla odpowiedniego Sprawdzanie spójności:</span><span class="sxs-lookup"><span data-stu-id="05951-211">On the blade for an individual report, you can see the following status information for the corresponding consistency check:</span></span>

* <span data-ttu-id="05951-212">Stan raportu — węzeł jest "Zgodnych" configuration "Niepowodzenie", czy węzeł jest "Nie są zgodne" (gdy węzeł jest w **applyandmonitor** tryb i na komputerze nie jest w żądanym stanie).</span><span class="sxs-lookup"><span data-stu-id="05951-212">The report status — whether the node is "Compliant", the configuration "Failed", or the node is "Not Compliant" (when the node is in **applyandmonitor** mode and the machine is not in the desired state).</span></span>
* <span data-ttu-id="05951-213">Godzina rozpoczęcia Sprawdzanie spójności.</span><span class="sxs-lookup"><span data-stu-id="05951-213">The start time for the consistency check.</span></span>
* <span data-ttu-id="05951-214">Łącznego czasu wykonywania sprawdzania spójności.</span><span class="sxs-lookup"><span data-stu-id="05951-214">The total runtime for the consistency check.</span></span>
* <span data-ttu-id="05951-215">Typ sprawdzania spójności.</span><span class="sxs-lookup"><span data-stu-id="05951-215">The type of consistency check.</span></span>
* <span data-ttu-id="05951-216">Błędy, wraz z kodem błędu oraz komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="05951-216">Any errors, including the error code and error message.</span></span> 
* <span data-ttu-id="05951-217">Zasoby usługi Konfiguracja DSC używane w konfiguracji i stanu każdego zasobu (czy węzeł jest w stanie odpowiednią dla tego zasobu) — możesz kliknąć każdy zasób, aby uzyskać więcej szczegółowych informacji dla tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="05951-217">Any DSC resources used in the configuration, and the state of each resource (whether the node is in the desired state for that resource) — you can click on each resource to get more detailed information for that resource.</span></span>
* <span data-ttu-id="05951-218">Nazwa, adres IP i tryb konfiguracji węzła.</span><span class="sxs-lookup"><span data-stu-id="05951-218">The name, IP address, and configuration mode of the node.</span></span>

<span data-ttu-id="05951-219">Możesz również kliknąć **wyświetlić raport raw** Aby wyświetlić dane, węzeł wysyła do serwera.</span><span class="sxs-lookup"><span data-stu-id="05951-219">You can also click **View raw report** to see the actual data that the node sends to the server.</span></span> <span data-ttu-id="05951-220">Aby uzyskać więcej informacji o korzystaniu z tych danych zobacz [przy użyciu serwera raportu DSC](https://msdn.microsoft.com/powershell/dsc/reportserver).</span><span class="sxs-lookup"><span data-stu-id="05951-220">For more information about using that data, see [Using a DSC report server](https://msdn.microsoft.com/powershell/dsc/reportserver).</span></span>

<span data-ttu-id="05951-221">Może upłynąć trochę czasu, gdy węzeł został załadowany przed pierwszym raport jest dostępny.</span><span class="sxs-lookup"><span data-stu-id="05951-221">It can take some time after a node is onboarded before the first report is available.</span></span> <span data-ttu-id="05951-222">Konieczne może być oczekiwania dla pierwszego raportu do 30 minut po dołączeniu węzła.</span><span class="sxs-lookup"><span data-stu-id="05951-222">You might need to wait up to 30 minutes for the first report after you onboard a node.</span></span>

## <a name="reassigning-a-node-to-a-different-node-configuration"></a><span data-ttu-id="05951-223">Ponowne przypisywanie węzła do innego węzła konfiguracji</span><span class="sxs-lookup"><span data-stu-id="05951-223">Reassigning a node to a different node configuration</span></span>
<span data-ttu-id="05951-224">Można przypisać węzeł, aby użyć konfiguracji węzła innego niż ten, który początkowo przypisana.</span><span class="sxs-lookup"><span data-stu-id="05951-224">You can assign a node to use a different node configuration than the one you initially assigned.</span></span>

1. <span data-ttu-id="05951-225">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="05951-225">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="05951-226">W menu centralnym kliknij **wszystkie zasoby** , a następnie nazwę konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="05951-226">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="05951-227">Na **konto automatyzacji** bloku, kliknij przycisk **węzłów DSC**.</span><span class="sxs-lookup"><span data-stu-id="05951-227">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="05951-228">Na **węzłów DSC** bloku, kliknij nazwę węzła chcesz ponownie przypisać.</span><span class="sxs-lookup"><span data-stu-id="05951-228">On the **DSC Nodes** blade, click on the name of the node you want to reassign.</span></span>
5. <span data-ttu-id="05951-229">W bloku dla tego węzła, kliknij **węzła Przypisz**.</span><span class="sxs-lookup"><span data-stu-id="05951-229">On the blade for that node, click **Assign node**.</span></span>
   
    ![Zrzut ekranu przedstawiający blok węzła wyróżnianie przycisk przypisać węzła](./media/automation-dsc-getting-started/AssignNode.png)
6. <span data-ttu-id="05951-231">Na **przypisać konfiguracji węzła** bloku konfiguracji węzła, do którego chcesz przypisać węzeł, a następnie kliknij przycisk Wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="05951-231">On the **Assign Node Configuration** blade, select the node configuration to which you want to assign the node, and then click **OK**.</span></span>
   
    ![Zrzut ekranu przedstawiający blok przypisać konfiguracji węzła](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a><span data-ttu-id="05951-233">Wyrejestrowywania węzła</span><span class="sxs-lookup"><span data-stu-id="05951-233">Unregistering a node</span></span>
<span data-ttu-id="05951-234">Jeśli nie ma już węzeł ma być zarządzany przez Konfiguracja DSC automatyzacji Azure, możesz go wyrejestrować.</span><span class="sxs-lookup"><span data-stu-id="05951-234">If you no longer want a node to be managed by Azure Automation DSC, you can unregister it.</span></span>

1. <span data-ttu-id="05951-235">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="05951-235">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="05951-236">W menu centralnym kliknij **wszystkie zasoby** , a następnie nazwę konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="05951-236">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="05951-237">Na **konto automatyzacji** bloku, kliknij przycisk **węzłów DSC**.</span><span class="sxs-lookup"><span data-stu-id="05951-237">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="05951-238">Na **węzłów DSC** bloku, kliknij nazwę węzła chcesz wyrejestrować.</span><span class="sxs-lookup"><span data-stu-id="05951-238">On the **DSC Nodes** blade, click on the name of the node you want to unregister.</span></span>
5. <span data-ttu-id="05951-239">W bloku dla tego węzła, kliknij **Unregister**.</span><span class="sxs-lookup"><span data-stu-id="05951-239">On the blade for that node, click **Unregister**.</span></span>
   
    ![Zrzut ekranu przedstawiający blok węzła wyróżnianie przycisk Unregister](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a><span data-ttu-id="05951-241">Pokrewne artykuły</span><span class="sxs-lookup"><span data-stu-id="05951-241">Related Articles</span></span>
* [<span data-ttu-id="05951-242">Omówienie usługi Konfiguracja DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="05951-242">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="05951-243">Dołączania komputerów do zarządzania przez Konfiguracja DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="05951-243">Onboarding machines for management by Azure Automation DSC</span></span>](automation-dsc-onboarding.md)
* [<span data-ttu-id="05951-244">Omówienie stanu konfiguracji żądanego programu Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="05951-244">Windows PowerShell Desired State Configuration Overview</span></span>](https://msdn.microsoft.com/powershell/dsc/overview)
* [<span data-ttu-id="05951-245">Polecenia cmdlet systemu Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="05951-245">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="05951-246">Cennik usługi Konfiguracja DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="05951-246">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)

