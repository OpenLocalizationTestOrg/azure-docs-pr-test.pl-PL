---
title: "Używanie agentów maszyn wirtualnych platformy Azure w celu zapewnienia ciągłej integracji z usługą Jenkins."
description: "Agenty maszyn wirtualnych platformy Azure jako elementy podrzędne usługi Jenkins."
services: multiple
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 0b22a559fbc03158a6d4398603d1a7d2874d7b67
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a><span data-ttu-id="35355-103">Używanie agentów maszyn wirtualnych platformy Azure w celu zapewnienia ciągłej integracji z usługą Jenkins.</span><span class="sxs-lookup"><span data-stu-id="35355-103">Use Azure VM agents for continuous integration with Jenkins.</span></span>

<span data-ttu-id="35355-104">Ten przewodnik Szybki start opisuje, jak przy użyciu wtyczki agentów maszyn wirtualnych platformy Azure dla usługi Jenkins utworzyć agenta systemu Linux (Ubuntu) na platformie Azure na żądanie.</span><span class="sxs-lookup"><span data-stu-id="35355-104">This quickstart shows how to use the Jenkins Azure VM Agents plugin to create an on-demand Linux (Ubuntu) agent in Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35355-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="35355-105">Prerequisites</span></span>

<span data-ttu-id="35355-106">Aby ukończyć ten przewodnik Szybki start:</span><span class="sxs-lookup"><span data-stu-id="35355-106">To complete this quickstart:</span></span>

* <span data-ttu-id="35355-107">Jeśli nie masz jeszcze wzorca usługi Jenkins, możesz na początek użyć [szablonu rozwiązania](install-jenkins-solution-template.md).</span><span class="sxs-lookup"><span data-stu-id="35355-107">If you do not already have a Jenkins master, you can start with the [Solution Template](install-jenkins-solution-template.md)</span></span> 
* <span data-ttu-id="35355-108">Jeśli nie masz jeszcze jednostki usługi Azure, zobacz artykuł [Tworzenie jednostki usługi platformy Azure za pomocą interfejsu wiersza polecenia platformy Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="35355-108">Refer to [Create an Azure Service principal with Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) if you do not already have an Azure service principal.</span></span>

## <a name="install-azure-vm-agents-plugin"></a><span data-ttu-id="35355-109">Instalowanie wtyczki agentów maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="35355-109">Install Azure VM Agents plugin</span></span>

<span data-ttu-id="35355-110">Jeśli używasz [szablonu rozwiązania](install-jenkins-solution-template.md), wtyczka agentów maszyn wirtualnych platformy Azure jest zainstalowana we wzorcu usługi Jenkins.</span><span class="sxs-lookup"><span data-stu-id="35355-110">If you start from the [Solution Template](install-jenkins-solution-template.md), the Azure VM Agent plugin is installed in the Jenkins master.</span></span>

<span data-ttu-id="35355-111">W innym przypadku zainstaluj wtyczkę **agentów maszyn wirtualnych platformy Azure** z poziomu pulpitu nawigacyjnego usługi Jenkins.</span><span class="sxs-lookup"><span data-stu-id="35355-111">Otherwise, install the **Azure VM Agents** plugin from within the Jenkins dashboard.</span></span>

## <a name="configure-the-plugin"></a><span data-ttu-id="35355-112">Konfigurowanie wtyczki</span><span class="sxs-lookup"><span data-stu-id="35355-112">Configure the plugin</span></span>

* <span data-ttu-id="35355-113">Na pulpicie nawigacyjnym usługi Jenkins kliknij **Manage Jenkins -> Configure System** (Zarządzanie usługą Jenkins -> Konfiguracja systemu).</span><span class="sxs-lookup"><span data-stu-id="35355-113">Within the Jenkins dashboard, click **Manage Jenkins -> Configure System ->**.</span></span> <span data-ttu-id="35355-114">Przewiń do dołu strony i znajdź sekcję z listą rozwijaną **Add new cloud** (Dodaj nową chmurę).</span><span class="sxs-lookup"><span data-stu-id="35355-114">Scroll to the bottom of the page and find the section with the dropdown **Add new cloud**.</span></span> <span data-ttu-id="35355-115">Wybierz z menu opcję **Microsoft Azure VM Agents** (Agenty maszyn wirtualnych platformy Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="35355-115">From the menu, select **Microsoft Azure VM Agents**</span></span>
* <span data-ttu-id="35355-116">Wybierz istniejące konto z listy rozwijanej Azure Credentials (Poświadczenia platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="35355-116">Select an existing account from the Azure Credentials dropdown.</span></span>  <span data-ttu-id="35355-117">Aby dodać nową jednostkę usługi Microsoft Azure (**Microsoft Azure Service Principal**), wprowadź następujące wartości: Subscription ID (Identyfikator subskrypcji), Client ID (Identyfikator klienta), Client Secret (Klucz tajny klienta) i OAuth 2.0 Token Endpoint (Punkt końcowy tokenu OAuth 2.0).</span><span class="sxs-lookup"><span data-stu-id="35355-117">To add a new **Microsoft Azure Service Principal,** enter the following values: Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span>

![Poświadczenia platformy Azure](./media/jenkins-azure-vm-agents/service-principal.png)

* <span data-ttu-id="35355-119">Kliknij przycisk **Verify configuration** (Sprawdź konfigurację), aby upewnić się, że konfiguracja profilu jest prawidłowa.</span><span class="sxs-lookup"><span data-stu-id="35355-119">Click **Verify configuration** to make sure that the profile configuration is correct.</span></span>
* <span data-ttu-id="35355-120">Zapisz konfigurację i przejdź do następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="35355-120">Save the configuration, and continue to the next step.</span></span>

## <a name="template-configuration"></a><span data-ttu-id="35355-121">Konfigurowanie szablonu</span><span class="sxs-lookup"><span data-stu-id="35355-121">Template configuration</span></span>

### <a name="general-configuration"></a><span data-ttu-id="35355-122">Konfiguracja ogólna</span><span class="sxs-lookup"><span data-stu-id="35355-122">General configuration</span></span>
<span data-ttu-id="35355-123">Następnie skonfiguruj szablon używany do definiowania agenta maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="35355-123">Next, configure a template for use to define an Azure VM agent.</span></span> 

* <span data-ttu-id="35355-124">Kliknij przycisk **Add** (Dodaj), aby dodać szablon.</span><span class="sxs-lookup"><span data-stu-id="35355-124">Click **Add** to add a template.</span></span> 
* <span data-ttu-id="35355-125">Wpisz nazwę nowego szablonu.</span><span class="sxs-lookup"><span data-stu-id="35355-125">Provide a name for your new template.</span></span> 
* <span data-ttu-id="35355-126">Jako etykietę wprowadź wartość „ubuntu”.</span><span class="sxs-lookup"><span data-stu-id="35355-126">For the label, enter  "ubuntu."</span></span> <span data-ttu-id="35355-127">Ta etykieta jest używana podczas konfigurowania zadania.</span><span class="sxs-lookup"><span data-stu-id="35355-127">This label is used during the job configuration.</span></span>
* <span data-ttu-id="35355-128">Wybierz region z pola kombi.</span><span class="sxs-lookup"><span data-stu-id="35355-128">Select the desired region from the combo box.</span></span>
* <span data-ttu-id="35355-129">Wybierz rozmiar maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="35355-129">Select the desired VM size.</span></span>
* <span data-ttu-id="35355-130">Określ nazwę konta Azure Storage lub pozostaw to pole puste, aby użyć domyślnej nazwy „jenkinsarmst”.</span><span class="sxs-lookup"><span data-stu-id="35355-130">Specify the Azure Storage account name or leave it blank to use the default name "jenkinsarmst."</span></span>
* <span data-ttu-id="35355-131">Określ czas przechowywania w minutach.</span><span class="sxs-lookup"><span data-stu-id="35355-131">Specify the retention time in minutes.</span></span> <span data-ttu-id="35355-132">To ustawienie określa liczbę minut, po jakiej usługa Jenkins automatycznie usunie bezczynnego agenta.</span><span class="sxs-lookup"><span data-stu-id="35355-132">This setting defines the number of minutes Jenkins can wait before automatically deleting an idle agent.</span></span> <span data-ttu-id="35355-133">Wpisz 0, jeśli nie chcesz, aby bezczynne agenty były automatycznie usuwane.</span><span class="sxs-lookup"><span data-stu-id="35355-133">Specify 0 if you do not want idle agents to be deleted automatically.</span></span>

![Konfiguracja ogólna](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a><span data-ttu-id="35355-135">Konfiguracja obrazu</span><span class="sxs-lookup"><span data-stu-id="35355-135">Image configuration</span></span>

<span data-ttu-id="35355-136">Aby utworzyć agenta systemu Linux (Ubuntu), wybierz **Image reference** (Obraz odniesienia) i użyj poniższej konfiguracji jako przykładu.</span><span class="sxs-lookup"><span data-stu-id="35355-136">To create a Linux (Ubuntu) agent, select **Image reference** and use the following configuration as an example.</span></span> <span data-ttu-id="35355-137">Najnowsze obrazy obsługiwane przez platformę Azure znajdziesz w portalu [Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1).</span><span class="sxs-lookup"><span data-stu-id="35355-137">Refer to [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) for the latest Azure supported images.</span></span>

* <span data-ttu-id="35355-138">Image Publisher: Canonical</span><span class="sxs-lookup"><span data-stu-id="35355-138">Image Publisher: Canonical</span></span>
* <span data-ttu-id="35355-139">Image Offer: UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="35355-139">Image Offer: UbuntuServer</span></span>
* <span data-ttu-id="35355-140">Image Sku: 14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="35355-140">Image Sku: 14.04.5-LTS</span></span>
* <span data-ttu-id="35355-141">Image version: latest</span><span class="sxs-lookup"><span data-stu-id="35355-141">Image version: latest</span></span>
* <span data-ttu-id="35355-142">OS Type: Linux</span><span class="sxs-lookup"><span data-stu-id="35355-142">OS Type: Linux</span></span>
* <span data-ttu-id="35355-143">Launch method: SSH</span><span class="sxs-lookup"><span data-stu-id="35355-143">Launch method: SSH</span></span>
* <span data-ttu-id="35355-144">Wprowadź poświadczenia administratora</span><span class="sxs-lookup"><span data-stu-id="35355-144">Provide an admin credentials</span></span>
* <span data-ttu-id="35355-145">W przypadku skryptu inicjowania maszyny wirtualnej wpisz:</span><span class="sxs-lookup"><span data-stu-id="35355-145">For VM initialization script, enter:</span></span>
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![Konfiguracja obrazu](./media/jenkins-azure-vm-agents/image-config.png)

* <span data-ttu-id="35355-147">Kliknij przycisk **Verify template** (Sprawdź szablon), aby sprawdzić konfigurację.</span><span class="sxs-lookup"><span data-stu-id="35355-147">Click **Verify Template** to verify the configuration.</span></span>
* <span data-ttu-id="35355-148">Kliknij przycisk **Save** (Zapisz).</span><span class="sxs-lookup"><span data-stu-id="35355-148">Click **Save**.</span></span>

## <a name="create-a-job-in-jenkins"></a><span data-ttu-id="35355-149">Tworzenie zadania w usłudze Jenkins</span><span class="sxs-lookup"><span data-stu-id="35355-149">Create a job in Jenkins</span></span>

* <span data-ttu-id="35355-150">Na pulpicie nawigacyjnym usługi Jenkins kliknij **New Item** (Nowy element).</span><span class="sxs-lookup"><span data-stu-id="35355-150">Within the Jenkins dashboard, click **New Item**.</span></span> 
* <span data-ttu-id="35355-151">Wprowadź nazwę, wybierz **Freestyle project** (Projekt Freestyle) i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="35355-151">Enter a name and select **Freestyle project** and click **OK**.</span></span>
* <span data-ttu-id="35355-152">Na karcie **General** (Ogólne) wybierz opcję „Restrict where project can be run” (Ogranicz miejsca uruchomienia projektu) i wpisz „ubuntu” w polu Label Expression (Wyrażenie etykiety).</span><span class="sxs-lookup"><span data-stu-id="35355-152">In the **General** tab, select "Restrict where project can be run" and type "ubuntu" in Label Expression.</span></span> <span data-ttu-id="35355-153">Na liście rozwijanej pojawi się pozycja „ubuntu”.</span><span class="sxs-lookup"><span data-stu-id="35355-153">You now see "ubuntu" in the dropdown.</span></span>
* <span data-ttu-id="35355-154">Kliknij przycisk **Save** (Zapisz).</span><span class="sxs-lookup"><span data-stu-id="35355-154">Click **Save**.</span></span>

![Konfigurowanie zadania](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a><span data-ttu-id="35355-156">Tworzenie nowego projektu</span><span class="sxs-lookup"><span data-stu-id="35355-156">Build your new project</span></span>

* <span data-ttu-id="35355-157">Wróć do pulpitu nawigacyjnego usługi Jenkins.</span><span class="sxs-lookup"><span data-stu-id="35355-157">Go back to the Jenkins dashboard.</span></span>
* <span data-ttu-id="35355-158">Kliknij prawym przyciskiem myszy nowo utworzone zadanie, a następnie kliknij przycisk **Build now** (Skompiluj teraz).</span><span class="sxs-lookup"><span data-stu-id="35355-158">Right-click the new job you created, then click **Build now**.</span></span> <span data-ttu-id="35355-159">Rozpocznie się kompilowanie.</span><span class="sxs-lookup"><span data-stu-id="35355-159">A build is kicked off.</span></span> 
* <span data-ttu-id="35355-160">Po ukończeniu kompilacji przejdź do obszaru **Console output** (Dane wyjściowe konsoli).</span><span class="sxs-lookup"><span data-stu-id="35355-160">Once the build is complete, go to **Console output**.</span></span> <span data-ttu-id="35355-161">Będzie widać, że kompilacja została wykonana zdalnie na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="35355-161">You see that the build was performed remotely on Azure.</span></span>

![Dane wyjściowe konsoli](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a><span data-ttu-id="35355-163">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="35355-163">Reference</span></span>

* <span data-ttu-id="35355-164">Wideo z cyklu „Piątek z Azure”: [Ciągła integracja z usługą Jenkins przy użyciu agentów maszyn wirtualnych platformy Azure](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span><span class="sxs-lookup"><span data-stu-id="35355-164">Azure Friday video: [Continuous Integration with Jenkins using Azure VM agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span></span>
* <span data-ttu-id="35355-165">Informacje uzupełniające i opcje konfiguracji: [Wiki wtyczki agentów maszyn wirtualnych platformy Azure dla usługi Jenkins](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span><span class="sxs-lookup"><span data-stu-id="35355-165">Support information and configuration options:  [Azure VM Agent Jenkins Plugin Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span></span> 

