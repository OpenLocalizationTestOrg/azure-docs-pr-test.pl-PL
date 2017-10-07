---
title: "wprowadzenie do usługi Konfiguracja DSC automatyzacji Azure aaaGetting | Dokumentacja firmy Microsoft"
description: "Objaśnienie i przykłady typowych zadań hello w żądany stan konfiguracji (Konfiguracja DSC automatyzacji Azure)"
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
ms.openlocfilehash: 82910c96e928b9264c2e1b52a5c98dc47273dcc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a><span data-ttu-id="a5b4c-103">Wprowadzenie do korzystania z usługi Konfiguracja DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="a5b4c-103">Getting started with Azure Automation DSC</span></span>
<span data-ttu-id="a5b4c-104">W tym temacie wyjaśniono, jak toodo hello najbardziej typowych zadań z żądanego stanu konfiguracji (Konfiguracja DSC automatyzacji Azure), takie jak tworzenie, importowanie i kompilowanie konfiguracje, dołączania za zarządzanie nimi maszyn i wyświetlania raportów.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-104">This topic explains how toodo hello most common tasks with Azure Automation Desired State Configuration (DSC), such as creating, importing, and compiling configurations, onboarding machines too manage, and viewing reports.</span></span> <span data-ttu-id="a5b4c-105">Omówienie jakie Konfiguracja DSC automatyzacji Azure jest, zobacz [Przegląd usługi Konfiguracja DSC automatyzacji Azure](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a5b4c-105">For an overview of what Azure Automation DSC is, see [Azure Automation DSC Overview](automation-dsc-overview.md).</span></span> <span data-ttu-id="a5b4c-106">Dokumentacja usługi Konfiguracja DSC w temacie [żądany stan konfiguracji Omówienie środowiska Windows PowerShell](https://msdn.microsoft.com/PowerShell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="a5b4c-106">For DSC documentation, see [Windows PowerShell Desired State Configuration Overview](https://msdn.microsoft.com/PowerShell/dsc/overview).</span></span>

<span data-ttu-id="a5b4c-107">Ten temat zawiera przewodnik krok po kroku toousing Konfiguracja DSC automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-107">This topic provides a step-by-step guide toousing Azure Automation DSC.</span></span> <span data-ttu-id="a5b4c-108">Chcąc środowiska próbki, który został już skonfigurowany bez hello wykonaj czynności opisane w tym temacie, można użyć [hello następujący szablon ARM](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span><span class="sxs-lookup"><span data-stu-id="a5b4c-108">If you want a sample environment that is already set up without following hello steps described in this topic, you can use [hello following ARM template](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span></span> <span data-ttu-id="a5b4c-109">Ten szablon ustawia ukończone środowiska Konfiguracja DSC automatyzacji Azure, łącznie z maszyny Wirtualnej platformy Azure, który jest zarządzany przez Konfiguracja DSC automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-109">This template sets up a completed Azure Automation DSC environment, including an Azure VM that is managed by Azure Automation DSC.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5b4c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a5b4c-110">Prerequisites</span></span>
<span data-ttu-id="a5b4c-111">toocomplete hello przykłady w tym temacie, wymagane są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="a5b4c-111">toocomplete hello examples in this topic, hello following are required:</span></span>

* <span data-ttu-id="a5b4c-112">Konto usługi Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-112">An Azure Automation account.</span></span> <span data-ttu-id="a5b4c-113">Aby uzyskać instrukcje dotyczące tworzenia konta Uruchom jako usługi Azure Automation, zobacz [Konto Uruchom jako platformy Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="a5b4c-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>
* <span data-ttu-id="a5b4c-114">Maszyna wirtualna Azure Resource Manager (nie klasycznego) systemem Windows Server 2008 R2 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span></span> <span data-ttu-id="a5b4c-115">Aby uzyskać instrukcje dotyczące tworzenia maszyny Wirtualnej, zobacz [tworzenie pierwszej maszyny wirtualnej systemu Windows w hello portalu Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="a5b4c-115">For instructions on creating a VM, see [Create your first Windows virtual machine in hello Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span></span>

## <a name="creating-a-dsc-configuration"></a><span data-ttu-id="a5b4c-116">Tworzenie konfiguracji DSC</span><span class="sxs-lookup"><span data-stu-id="a5b4c-116">Creating a DSC configuration</span></span>
<span data-ttu-id="a5b4c-117">Utworzymy prostą [konfiguracji DSC](https://msdn.microsoft.com/powershell/dsc/configurations) dzięki temu hello obecności lub braku hello **serwera sieci Web** Windows funkcji (IIS), w zależności od tego, jak przypisać węzłów.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-117">We will create a simple [DSC configuration](https://msdn.microsoft.com/powershell/dsc/configurations) that ensures either hello presence or absence of hello **Web-Server** Windows Feature (IIS), depending on how you assign nodes.</span></span>

1. <span data-ttu-id="a5b4c-118">Uruchom hello programu Windows PowerShell ISE (lub dowolnym edytorze tekstów).</span><span class="sxs-lookup"><span data-stu-id="a5b4c-118">Start hello Windows PowerShell ISE (or any text editor).</span></span>
2. <span data-ttu-id="a5b4c-119">Wpisz hello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="a5b4c-119">Type hello following text:</span></span>
   
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
3. <span data-ttu-id="a5b4c-120">Zapisz plik hello jako `TestConfig.ps1`.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-120">Save hello file as `TestConfig.ps1`.</span></span>

<span data-ttu-id="a5b4c-121">Ta konfiguracja wymaga jednego zasobu w każdym węźle bloku, hello [zasobów WindowsFeature](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), dzięki temu hello obecności lub braku hello **serwera sieci Web** funkcji.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-121">This configuration calls one resource in each node block, hello [WindowsFeature resource](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), that ensures either hello presence or absence of hello **Web-Server** feature.</span></span>

## <a name="importing-a-configuration-into-azure-automation"></a><span data-ttu-id="a5b4c-122">Importowanie konfiguracji usługi Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="a5b4c-122">Importing a configuration into Azure Automation</span></span>
<span data-ttu-id="a5b4c-123">Następnie konfiguracji hello firma Microsoft będzie zaimportować hello konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-123">Next, we'll import hello configuration into hello Automation account.</span></span>

1. <span data-ttu-id="a5b4c-124">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5b4c-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a5b4c-125">W menu Centrum powitania kliknij **wszystkie zasoby** , a następnie hello nazwa konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-125">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="a5b4c-126">Na powitania **konto automatyzacji** bloku, kliknij przycisk **konfiguracji DSC**.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-126">On hello **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="a5b4c-127">Na powitania **konfiguracji DSC** bloku, kliknij przycisk **dodać konfigurację**.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-127">On hello **DSC Configurations** blade, click **Add a configuration**.</span></span>
5. <span data-ttu-id="a5b4c-128">Na powitania **konfigurację importu** bloku, przeglądania toohello `TestConfig.ps1` plik na komputerze.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-128">On hello **Import Configuration** blade, browse toohello `TestConfig.ps1` file on your computer.</span></span>
   
    ![Zrzut ekranu przedstawiający hello ** importowania konfiguracji ** bloku](./media/automation-dsc-getting-started/AddConfig.png)
6. <span data-ttu-id="a5b4c-130">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-130">Click **OK**.</span></span>

## <a name="viewing-a-configuration-in-azure-automation"></a><span data-ttu-id="a5b4c-131">Wyświetlanie konfiguracji w usłudze Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="a5b4c-131">Viewing a configuration in Azure Automation</span></span>
<span data-ttu-id="a5b4c-132">Po zaimportowaniu konfiguracji, można go wyświetlić w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-132">After you have imported a configuration, you can view it in hello Azure portal.</span></span>

1. <span data-ttu-id="a5b4c-133">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5b4c-133">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a5b4c-134">W menu Centrum powitania kliknij **wszystkie zasoby** , a następnie hello nazwa konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-134">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="a5b4c-135">Na powitania **konto automatyzacji** bloku, kliknij przycisk **konfiguracji DSC**</span><span class="sxs-lookup"><span data-stu-id="a5b4c-135">On hello **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="a5b4c-136">Na powitania **konfiguracji DSC** bloku, kliknij przycisk **TestConfig** (jest to nazwa hello konfiguracji hello zaimportowane w poprzedniej procedurze hello).</span><span class="sxs-lookup"><span data-stu-id="a5b4c-136">On hello **DSC Configurations** blade, click **TestConfig** (this is hello name of hello configuration you imported in hello previous procedure).</span></span>
5. <span data-ttu-id="a5b4c-137">Na powitania **konfiguracji TestConfig** bloku, kliknij przycisk **źródło konfiguracji widoku**.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-137">On hello **TestConfig Configuration** blade, click **View configuration source**.</span></span>
   
    ![Zrzut ekranu przedstawiający blok konfiguracji TestConfig hello](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    <span data-ttu-id="a5b4c-139">A **źródło konfiguracji TestConfig** zostanie otwarty blok, wyświetlanie kod programu PowerShell hello hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-139">A **TestConfig Configuration source** blade opens, displaying hello PowerShell code for hello configuration.</span></span>

## <a name="compiling-a-configuration-in-azure-automation"></a><span data-ttu-id="a5b4c-140">Kompilowanie konfiguracji w usłudze Automatyzacja Azure</span><span class="sxs-lookup"><span data-stu-id="a5b4c-140">Compiling a configuration in Azure Automation</span></span>
<span data-ttu-id="a5b4c-141">Przed zastosowaniem węzła tooa pożądanego stanu, konfiguracji DSC definiowanie tego stanu muszą można skompilowany w co najmniej jednej konfiguracji węzła (MOF dokumentu), a umieszczane na powitania serwera ściągania usługi Konfiguracja DSC automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-141">Before you can apply a desired state tooa node, a DSC configuration defining that state must be compiled into one or more node configurations (MOF document), and placed on hello Automation DSC Pull Server.</span></span> <span data-ttu-id="a5b4c-142">Aby uzyskać bardziej szczegółowy opis kompilowania konfiguracji DSC automatyzacji Azure, zobacz [kompilowania konfiguracji DSC automatyzacji Azure](automation-dsc-compile.md).</span><span class="sxs-lookup"><span data-stu-id="a5b4c-142">For a more detailed description of compiling configurations in Azure Automation DSC, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md).</span></span> <span data-ttu-id="a5b4c-143">Aby uzyskać więcej informacji o kompilacji konfiguracji, zobacz [konfiguracji DSC](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span><span class="sxs-lookup"><span data-stu-id="a5b4c-143">For more information about compiling configurations, see [DSC Configurations](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span></span>

1. <span data-ttu-id="a5b4c-144">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5b4c-144">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a5b4c-145">W menu Centrum powitania kliknij **wszystkie zasoby** , a następnie hello nazwa konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-145">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="a5b4c-146">Na powitania **konto automatyzacji** bloku, kliknij przycisk **konfiguracji DSC**</span><span class="sxs-lookup"><span data-stu-id="a5b4c-146">On hello **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="a5b4c-147">Na powitania **konfiguracji DSC** bloku, kliknij przycisk **TestConfig** (nazwa hello hello wcześniej zaimportowane konfiguracji).</span><span class="sxs-lookup"><span data-stu-id="a5b4c-147">On hello **DSC Configurations** blade, click **TestConfig** (hello name of hello previously imported configuration).</span></span>
5. <span data-ttu-id="a5b4c-148">Na powitania **konfiguracji TestConfig** bloku, kliknij przycisk **skompilować**, a następnie kliknij przycisk **tak**.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-148">On hello **TestConfig Configuration** blade, click **Compile**, and then click **Yes**.</span></span> <span data-ttu-id="a5b4c-149">Spowoduje to uruchomienie zadania kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-149">This starts a compilation job.</span></span>
   
    ![Zrzut ekranu przedstawiający blok konfiguracji TestConfig hello wyróżnianie przycisk kompilacji](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> <span data-ttu-id="a5b4c-151">Podczas kompilowania konfiguracji w automatyzacji Azure automatycznie wdraża dowolnego serwera ściągania toohello za utworzony węzła konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-151">When you compile a configuration in Azure Automation, it automatically deploys any created node configuration MOFs toohello pull server.</span></span>
> 
> 

## <a name="viewing-a-compilation-job"></a><span data-ttu-id="a5b4c-152">Wyświetlanie zadania kompilacji</span><span class="sxs-lookup"><span data-stu-id="a5b4c-152">Viewing a compilation job</span></span>
<span data-ttu-id="a5b4c-153">Po rozpoczęciu kompilacji mógł być wyświetlany w hello **zadań kompilacji** kafelka w hello **konfiguracji** bloku.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-153">After you start a compilation, you can view it in hello **Compilation jobs** tile in hello **Configuration** blade.</span></span> <span data-ttu-id="a5b4c-154">Witaj **zadań kompilacji** zawiera obecnie uruchomiona, zakończone oraz zadania zakończone niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-154">hello **Compilation jobs** tile shows currently running, completed, and failed jobs.</span></span> <span data-ttu-id="a5b4c-155">Po otwarciu bloku zadania kompilacji zawiera informacje dotyczące tego zadania, w tym wszelkie błędy lub ostrzeżenia napotkał, parametry wejściowe używane w konfiguracji hello i kompilacja dzienników.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-155">When you open a compilation job blade, it shows information about that job including any errors or warnings encountered, input parameters used in hello configuration, and compilation logs.</span></span>

1. <span data-ttu-id="a5b4c-156">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5b4c-156">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a5b4c-157">W menu Centrum powitania kliknij **wszystkie zasoby** , a następnie hello nazwa konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-157">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="a5b4c-158">Na powitania **konto automatyzacji** bloku, kliknij przycisk **konfiguracji DSC**.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-158">On hello **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="a5b4c-159">Na powitania **konfiguracji DSC** bloku, kliknij przycisk **TestConfig** (nazwa hello hello wcześniej zaimportowane konfiguracji).</span><span class="sxs-lookup"><span data-stu-id="a5b4c-159">On hello **DSC Configurations** blade, click **TestConfig** (hello name of hello previously imported configuration).</span></span>
5. <span data-ttu-id="a5b4c-160">Na powitania **zadań kompilacji** kafelka hello **konfiguracji TestConfig** bloku, kliknij na dowolnym hello zadań.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-160">On hello **Compilation jobs** tile of hello **TestConfig Configuration** blade, click on any of hello jobs listed.</span></span> <span data-ttu-id="a5b4c-161">A **zadania kompilacji** zostanie otwarty blok, oznaczenie daty hello hello zadania kompilacji został uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-161">A **Compilation Job** blade opens, labeled with hello date that hello compilation job was started.</span></span>
   
    ![Zrzut ekranu przedstawiający blok zadania kompilacji hello](./media/automation-dsc-getting-started/CompilationJob.png)
6. <span data-ttu-id="a5b4c-163">Kliknij Kafelek w hello **zadania kompilacji** toosee bloku więcej szczegółowych informacji o hello zadania.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-163">Click on any tile in hello **Compilation Job** blade toosee further details about hello job.</span></span>

## <a name="viewing-node-configurations"></a><span data-ttu-id="a5b4c-164">Wyświetlanie konfiguracji węzłów</span><span class="sxs-lookup"><span data-stu-id="a5b4c-164">Viewing node configurations</span></span>
<span data-ttu-id="a5b4c-165">Pomyślne zakończenie zadania kompilacji tworzy nowy co najmniej jednej konfiguracji węzła.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-165">Successful completion of a compilation job creates one or more new node configurations.</span></span> <span data-ttu-id="a5b4c-166">Konfiguracja węzła jest dokumentem MOF, który jest serwerem ściągania toohello wdrożone i gotowe toobe ściągnąć i stosowane przez co najmniej jeden węzeł.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-166">A node configuration is a MOF document that is deployed toohello pull server and ready toobe pulled and applied by one or more nodes.</span></span> <span data-ttu-id="a5b4c-167">Konfiguracje węzłów hello można wyświetlić w Twoje konto usługi Automatyzacja w hello **konfiguracji węzłów DSC** bloku.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-167">You can view hello node configurations in your Automation account in hello **DSC Node Configurations** blade.</span></span> <span data-ttu-id="a5b4c-168">Konfiguracja węzła ma nazwę w postaci hello *ConfigurationName*. *NodeName*.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-168">A node configuration has a name with hello form *ConfigurationName*.*NodeName*.</span></span>

1. <span data-ttu-id="a5b4c-169">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5b4c-169">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a5b4c-170">W menu Centrum powitania kliknij **wszystkie zasoby** , a następnie hello nazwa konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-170">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="a5b4c-171">Na powitania **konto automatyzacji** bloku, kliknij przycisk **konfiguracji węzłów DSC**.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-171">On hello **Automation account** blade, click **DSC Node Configurations**.</span></span>
   
    ![Zrzut ekranu przedstawiający blok konfiguracji węzłów DSC hello](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a><span data-ttu-id="a5b4c-173">Dołączanie maszyny Wirtualnej platformy Azure do zarządzania z usługi Konfiguracja DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="a5b4c-173">Onboarding an Azure VM for management with Azure Automation DSC</span></span>
<span data-ttu-id="a5b4c-174">Można użyć Konfiguracja DSC automatyzacji Azure toomanage Azure VMs (Classic i Resource Manager), lokalnych maszyn wirtualnych systemu Linux maszyny, usług AWS maszyn wirtualnych i fizycznych komputerach lokalnych.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-174">You can use Azure Automation DSC toomanage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span></span> <span data-ttu-id="a5b4c-175">W tym temacie firma Microsoft opisano sposób tooonboard tylko Menedżera zasobów maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-175">In this topic, we cover how tooonboard only Azure Resource Manager VMs.</span></span> <span data-ttu-id="a5b4c-176">Uzyskać informacji na temat dołączania innych typów urządzeń, zobacz [dołączania komputerów do zarządzania przez Konfiguracja DSC automatyzacji Azure](automation-dsc-onboarding.md).</span><span class="sxs-lookup"><span data-stu-id="a5b4c-176">For information about onboarding other types of machines, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md).</span></span>

### <a name="tooonboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a><span data-ttu-id="a5b4c-177">tooonboard maszyny Wirtualnej platformy Azure Resource Manager do zarządzania przez Konfiguracja DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="a5b4c-177">tooonboard an Azure Resource Manager VM for management by Azure Automation DSC</span></span>
1. <span data-ttu-id="a5b4c-178">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5b4c-178">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a5b4c-179">W menu Centrum powitania kliknij **wszystkie zasoby** , a następnie hello nazwa konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-179">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="a5b4c-180">Na powitania **konto automatyzacji** bloku, kliknij przycisk **węzłów DSC**.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-180">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="a5b4c-181">W hello **węzłów DSC** bloku, kliknij przycisk **dodać maszyny Wirtualnej Azure**.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-181">In hello **DSC Nodes** blade, click **Add Azure VM**.</span></span>
   
    ![Zrzut ekranu przedstawiający blok węzłów DSC hello wyróżnianie hello przycisku Dodaj maszyny Wirtualnej Azure](./media/automation-dsc-getting-started/OnboardVM.png)
5. <span data-ttu-id="a5b4c-183">W hello **Dodaj maszyny wirtualne Azure** bloku, kliknij przycisk **wybierz maszyny wirtualne tooonboard**.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-183">In hello **Add Azure VMs** blade, click **Select virtual machines tooonboard**.</span></span>
6. <span data-ttu-id="a5b4c-184">W hello **wybierz maszyny wirtualne** bloku, wybierz hello wirtualna tooonboard i kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-184">In hello **Select VMs** blade, select hello VM you want tooonboard, and click **OK**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="a5b4c-185">Musi to być maszyny Wirtualnej platformy Azure Resource Manager systemem Windows Server 2008 R2 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-185">This must be an Azure Resource Manager VM running Windows Server 2008 R2 or later.</span></span>
   > 
   > 
7. <span data-ttu-id="a5b4c-186">W hello **Dodaj maszyny wirtualne Azure** bloku, kliknij przycisk **Konfigurowanie danych rejestracji**.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-186">In hello **Add Azure VMs** blade, click **Configure registration data**.</span></span>
8. <span data-ttu-id="a5b4c-187">W hello **rejestracji** bloku, wprowadź nazwę hello konfiguracji węzła hello ma tooapply toohello maszyny Wirtualnej w hello **Nazwa konfiguracji węzła** pole.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-187">In hello **Registration** blade, enter hello name of hello node configuration you want tooapply toohello VM in hello **Node Configuration Name** box.</span></span> <span data-ttu-id="a5b4c-188">To musi dokładnie odpowiadać nazwie hello konfiguracji węzła w hello konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-188">This must exactly match hello name of a node configuration in hello Automation account.</span></span> <span data-ttu-id="a5b4c-189">W tym momencie podanie nazwy jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-189">Providing a name at this point is optional.</span></span> <span data-ttu-id="a5b4c-190">Można zmienić konfiguracji węzła hello przypisane po węźle hello dołączania.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-190">You can change hello assigned node configuration after onboarding hello node.</span></span>
   <span data-ttu-id="a5b4c-191">Sprawdź **ponowny rozruch węzła, w razie potrzeby**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-191">Check **Reboot Node if Needed**, and then click **OK**.</span></span>
   
    ![Zrzut ekranu przedstawiający blok rejestracji hello](./media/automation-dsc-getting-started/RegisterVM.png)
   
    <span data-ttu-id="a5b4c-193">Określona konfiguracja węzła Hello będzie zastosowane toohello maszyny Wirtualnej w odstępach czasu określonych przez hello **częstotliwość trybu konfiguracji**, i hello maszyny Wirtualnej będzie sprawdzać dostępność aktualizacji konfiguracji węzła toohello w odstępach czasu określonych przez hello  **Częstotliwość odświeżania**.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-193">hello node configuration you specified will be applied toohello VM at intervals specified by hello **Configuration Mode Frequency**, and hello VM will check for updates toohello node configuration at intervals specified by hello **Refresh Frequency**.</span></span> <span data-ttu-id="a5b4c-194">Aby uzyskać więcej informacji na temat korzystania z tych wartości, zobacz [hello Konfigurowanie lokalny program Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span><span class="sxs-lookup"><span data-stu-id="a5b4c-194">For more information about how these values are used, see [Configuring hello Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span></span>
9. <span data-ttu-id="a5b4c-195">W hello **Dodaj maszyny wirtualne Azure** bloku, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-195">In hello **Add Azure VMs** blade, click **Create**.</span></span>

<span data-ttu-id="a5b4c-196">Azure rozpocznie się proces hello hello dołączania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-196">Azure will start hello process of onboarding hello VM.</span></span> <span data-ttu-id="a5b4c-197">Po zakończeniu hello maszyny Wirtualnej pojawi się na powitania **węzłów DSC** bloku w hello konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-197">When it is complete, hello VM will show up in hello **DSC Nodes** blade in hello Automation account.</span></span>

## <a name="viewing-hello-list-of-dsc-nodes"></a><span data-ttu-id="a5b4c-198">Wyświetlanie listy hello węzłów DSC</span><span class="sxs-lookup"><span data-stu-id="a5b4c-198">Viewing hello list of DSC nodes</span></span>
<span data-ttu-id="a5b4c-199">Można wyświetlić listy hello wszystkie komputery, które zostały został załadowany do zarządzania na Twoim koncie automatyzacji w hello **węzłów DSC** bloku.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-199">You can view hello list of all machines that have been onboarded for management in your Automation account in hello **DSC Nodes** blade.</span></span>

1. <span data-ttu-id="a5b4c-200">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5b4c-200">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a5b4c-201">W menu Centrum powitania kliknij **wszystkie zasoby** , a następnie hello nazwa konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-201">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="a5b4c-202">Na powitania **konto automatyzacji** bloku, kliknij przycisk **węzłów DSC**.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-202">On hello **Automation account** blade, click **DSC Nodes**.</span></span>

## <a name="viewing-reports-for-dsc-nodes"></a><span data-ttu-id="a5b4c-203">Wyświetlanie raportów węzłów DSC</span><span class="sxs-lookup"><span data-stu-id="a5b4c-203">Viewing reports for DSC nodes</span></span>
<span data-ttu-id="a5b4c-204">Zawsze Konfiguracja DSC automatyzacji Azure przeprowadza sprawdzanie spójności na węzeł zarządzany, węzeł hello wysyła stanu serwera ściągania wstecz toohello raportów.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-204">Each time Azure Automation DSC performs a consistency check on a managed node, hello node sends a status report back toohello pull server.</span></span> <span data-ttu-id="a5b4c-205">Można wyświetlać te raporty na powitania bloku dla tego węzła.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-205">You can view these reports on hello blade for that node.</span></span>

1. <span data-ttu-id="a5b4c-206">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5b4c-206">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a5b4c-207">W menu Centrum powitania kliknij **wszystkie zasoby** , a następnie hello nazwa konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-207">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="a5b4c-208">Na powitania **konto automatyzacji** bloku, kliknij przycisk **węzłów DSC**.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-208">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="a5b4c-209">Na powitania **raporty** kafelka, kliknij dowolną raportów hello hello na liście.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-209">On hello **Reports** tile, click on any of hello reports in hello list.</span></span>
   
    ![Zrzut ekranu przedstawiający blok raportu hello](./media/automation-dsc-getting-started/NodeReport.png)

<span data-ttu-id="a5b4c-211">W bloku hello pojedynczy raport można wyświetlić hello następujące informacje o stanie spójności odpowiednich hello Sprawdź:</span><span class="sxs-lookup"><span data-stu-id="a5b4c-211">On hello blade for an individual report, you can see hello following status information for hello corresponding consistency check:</span></span>

* <span data-ttu-id="a5b4c-212">Witaj raportowanie stanu — węzeł hello jest "Zgodnych" hello konfiguracji "Niepowodzenie", czy węzeł hello jest "Nie są zgodne" (gdy węzeł hello jest w **applyandmonitor** trybu i hello komputer nie jest w stanie hello potrzeby).</span><span class="sxs-lookup"><span data-stu-id="a5b4c-212">hello report status — whether hello node is "Compliant", hello configuration "Failed", or hello node is "Not Compliant" (when hello node is in **applyandmonitor** mode and hello machine is not in hello desired state).</span></span>
* <span data-ttu-id="a5b4c-213">Godzina rozpoczęcia Hello hello Sprawdzanie spójności.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-213">hello start time for hello consistency check.</span></span>
* <span data-ttu-id="a5b4c-214">Sprawdź Hello łącznego czasu wykonywania hello spójności.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-214">hello total runtime for hello consistency check.</span></span>
* <span data-ttu-id="a5b4c-215">Sprawdź typ Hello spójności.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-215">hello type of consistency check.</span></span>
* <span data-ttu-id="a5b4c-216">Wszelkie błędy, w tym hello błąd kodu i komunikatu o błędzie.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-216">Any errors, including hello error code and error message.</span></span> 
* <span data-ttu-id="a5b4c-217">Zasoby usługi Konfiguracja DSC używane w konfiguracji hello i hello stanu każdego zasobu (czy hello węzeł jest w stanie hello potrzebne dla tego zasobu) — możesz kliknąć na każdym tooget zasobów bardziej szczegółowe informacje dla tego zasobu.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-217">Any DSC resources used in hello configuration, and hello state of each resource (whether hello node is in hello desired state for that resource) — you can click on each resource tooget more detailed information for that resource.</span></span>
* <span data-ttu-id="a5b4c-218">Witaj nazwa, adres IP i tryb konfiguracji węzła hello.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-218">hello name, IP address, and configuration mode of hello node.</span></span>

<span data-ttu-id="a5b4c-219">Możesz również kliknąć **wyświetlić raport raw** toosee hello rzeczywiste dane, które hello węzła wysyła toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-219">You can also click **View raw report** toosee hello actual data that hello node sends toohello server.</span></span> <span data-ttu-id="a5b4c-220">Aby uzyskać więcej informacji o korzystaniu z tych danych zobacz [przy użyciu serwera raportu DSC](https://msdn.microsoft.com/powershell/dsc/reportserver).</span><span class="sxs-lookup"><span data-stu-id="a5b4c-220">For more information about using that data, see [Using a DSC report server](https://msdn.microsoft.com/powershell/dsc/reportserver).</span></span>

<span data-ttu-id="a5b4c-221">Może upłynąć trochę czasu, po węzeł został załadowany przed hello pierwszy raport jest dostępny.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-221">It can take some time after a node is onboarded before hello first report is available.</span></span> <span data-ttu-id="a5b4c-222">Konieczne może toowait się minut too30 hello pierwszego raportu po dołączeniu węzła.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-222">You might need toowait up too30 minutes for hello first report after you onboard a node.</span></span>

## <a name="reassigning-a-node-tooa-different-node-configuration"></a><span data-ttu-id="a5b4c-223">Ponowne przypisywanie konfiguracji inny węzeł tooa węzła</span><span class="sxs-lookup"><span data-stu-id="a5b4c-223">Reassigning a node tooa different node configuration</span></span>
<span data-ttu-id="a5b4c-224">Można przypisać toouse węzła konfiguracji inny węzeł niż hello jedną, która początkowo przypisana.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-224">You can assign a node toouse a different node configuration than hello one you initially assigned.</span></span>

1. <span data-ttu-id="a5b4c-225">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5b4c-225">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a5b4c-226">W menu Centrum powitania kliknij **wszystkie zasoby** , a następnie hello nazwa konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-226">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="a5b4c-227">Na powitania **konto automatyzacji** bloku, kliknij przycisk **węzłów DSC**.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-227">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="a5b4c-228">Na powitania **węzłów DSC** bloku, kliknij na nazwie hello hello węzła ma tooreassign.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-228">On hello **DSC Nodes** blade, click on hello name of hello node you want tooreassign.</span></span>
5. <span data-ttu-id="a5b4c-229">W bloku powitania dla tego węzła, kliknij **węzła Przypisz**.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-229">On hello blade for that node, click **Assign node**.</span></span>
   
    ![Zrzut ekranu przedstawiający blok węzła hello wyróżnianie hello przypisać węzła przycisku](./media/automation-dsc-getting-started/AssignNode.png)
6. <span data-ttu-id="a5b4c-231">Na powitania **przypisać konfiguracji węzła** bloku, wybierz hello węzła konfiguracji toowhich mają tooassign hello węzeł, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-231">On hello **Assign Node Configuration** blade, select hello node configuration toowhich you want tooassign hello node, and then click **OK**.</span></span>
   
    ![Zrzut ekranu przedstawiający blok przypisać konfiguracji węzła hello](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a><span data-ttu-id="a5b4c-233">Wyrejestrowywania węzła</span><span class="sxs-lookup"><span data-stu-id="a5b4c-233">Unregistering a node</span></span>
<span data-ttu-id="a5b4c-234">Jeśli nie chcesz już toobe węzła, zarządza Konfiguracja DSC automatyzacji Azure, możesz go wyrejestrować.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-234">If you no longer want a node toobe managed by Azure Automation DSC, you can unregister it.</span></span>

1. <span data-ttu-id="a5b4c-235">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5b4c-235">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a5b4c-236">W menu Centrum powitania kliknij **wszystkie zasoby** , a następnie hello nazwa konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-236">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="a5b4c-237">Na powitania **konto automatyzacji** bloku, kliknij przycisk **węzłów DSC**.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-237">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="a5b4c-238">Na powitania **węzłów DSC** bloku, kliknij na nazwie hello hello węzła ma toounregister.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-238">On hello **DSC Nodes** blade, click on hello name of hello node you want toounregister.</span></span>
5. <span data-ttu-id="a5b4c-239">W bloku powitania dla tego węzła, kliknij **Unregister**.</span><span class="sxs-lookup"><span data-stu-id="a5b4c-239">On hello blade for that node, click **Unregister**.</span></span>
   
    ![Zrzut ekranu przedstawiający blok węzła hello wyróżnianie hello Unregister przycisku](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a><span data-ttu-id="a5b4c-241">Pokrewne artykuły</span><span class="sxs-lookup"><span data-stu-id="a5b4c-241">Related Articles</span></span>
* [<span data-ttu-id="a5b4c-242">Omówienie usługi Konfiguracja DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="a5b4c-242">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="a5b4c-243">Dołączania komputerów do zarządzania przez Konfiguracja DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="a5b4c-243">Onboarding machines for management by Azure Automation DSC</span></span>](automation-dsc-onboarding.md)
* [<span data-ttu-id="a5b4c-244">Omówienie stanu konfiguracji żądanego programu Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5b4c-244">Windows PowerShell Desired State Configuration Overview</span></span>](https://msdn.microsoft.com/powershell/dsc/overview)
* [<span data-ttu-id="a5b4c-245">Polecenia cmdlet systemu Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="a5b4c-245">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="a5b4c-246">Cennik usługi Konfiguracja DSC automatyzacji Azure</span><span class="sxs-lookup"><span data-stu-id="a5b4c-246">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)

