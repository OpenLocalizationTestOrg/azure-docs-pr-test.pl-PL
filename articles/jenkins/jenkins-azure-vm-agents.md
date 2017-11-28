---
title: "aaaUse agentów maszyny Wirtualnej platformy Azure dla ciągłej integracji z Wpięć."
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
ms.openlocfilehash: 2388e6919d0280372166fbd325d80dafb00d7550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a><span data-ttu-id="21566-103">Używanie agentów maszyn wirtualnych platformy Azure w celu zapewnienia ciągłej integracji z usługą Jenkins.</span><span class="sxs-lookup"><span data-stu-id="21566-103">Use Azure VM agents for continuous integration with Jenkins.</span></span>

<span data-ttu-id="21566-104">Ta opcja szybkiego startu pokazuje, jak toouse hello toocreate wtyczki Wpięć Azure VM agentów na żądanie agenta systemu Linux (Ubuntu) na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="21566-104">This quickstart shows how toouse hello Jenkins Azure VM Agents plugin toocreate an on-demand Linux (Ubuntu) agent in Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21566-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="21566-105">Prerequisites</span></span>

<span data-ttu-id="21566-106">toocomplete tego przewodnika Szybki Start:</span><span class="sxs-lookup"><span data-stu-id="21566-106">toocomplete this quickstart:</span></span>

* <span data-ttu-id="21566-107">Jeśli nie masz już wzorca Wpięć, można uruchomić z poziomu hello [szablon rozwiązania](install-jenkins-solution-template.md)</span><span class="sxs-lookup"><span data-stu-id="21566-107">If you do not already have a Jenkins master, you can start with hello [Solution Template](install-jenkins-solution-template.md)</span></span> 
* <span data-ttu-id="21566-108">Odwołuje się zbyt[Tworzenie nazwy głównej usługi Azure Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) Jeśli nie masz już nazwę główną usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="21566-108">Refer too[Create an Azure Service principal with Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) if you do not already have an Azure service principal.</span></span>

## <a name="install-azure-vm-agents-plugin"></a><span data-ttu-id="21566-109">Instalowanie wtyczki agentów maszyn wirtualnych platformy Azure</span><span class="sxs-lookup"><span data-stu-id="21566-109">Install Azure VM Agents plugin</span></span>

<span data-ttu-id="21566-110">Jeśli zostanie uruchomione z hello [szablon rozwiązania](install-jenkins-solution-template.md), hello wtyczki Agent maszyny Wirtualnej jest zainstalowany w hello Wpięć wzorca.</span><span class="sxs-lookup"><span data-stu-id="21566-110">If you start from hello [Solution Template](install-jenkins-solution-template.md), hello Azure VM Agent plugin is installed in hello Jenkins master.</span></span>

<span data-ttu-id="21566-111">W przeciwnym razie zainstaluj hello **agentów maszyny Wirtualnej Azure** wtyczki z wewnątrz pulpitu nawigacyjnego Wpięć hello.</span><span class="sxs-lookup"><span data-stu-id="21566-111">Otherwise, install hello **Azure VM Agents** plugin from within hello Jenkins dashboard.</span></span>

## <a name="configure-hello-plugin"></a><span data-ttu-id="21566-112">Skonfiguruj wtyczkę hello</span><span class="sxs-lookup"><span data-stu-id="21566-112">Configure hello plugin</span></span>

* <span data-ttu-id="21566-113">W ramach hello Wpięć pulpitu nawigacyjnego, kliknij przycisk **Wpięć Zarządzanie -> skonfiguruj System ->**.</span><span class="sxs-lookup"><span data-stu-id="21566-113">Within hello Jenkins dashboard, click **Manage Jenkins -> Configure System ->**.</span></span> <span data-ttu-id="21566-114">Przewiń toohello u dołu strony hello i Znajdź sekcję hello z listy rozwijanej hello **Dodaj nowe chmury**.</span><span class="sxs-lookup"><span data-stu-id="21566-114">Scroll toohello bottom of hello page and find hello section with hello dropdown **Add new cloud**.</span></span> <span data-ttu-id="21566-115">Wybierz z hello menu **agentów programu Microsoft Azure maszyny Wirtualnej**</span><span class="sxs-lookup"><span data-stu-id="21566-115">From hello menu, select **Microsoft Azure VM Agents**</span></span>
* <span data-ttu-id="21566-116">Wybierz istniejące konto z listy rozwijanej poświadczenia Azure hello.</span><span class="sxs-lookup"><span data-stu-id="21566-116">Select an existing account from hello Azure Credentials dropdown.</span></span>  <span data-ttu-id="21566-117">tooadd nowy **nazwy głównej usługi Azure firmy Microsoft,** wprowadź hello następujące wartości: identyfikator subskrypcji, Identyfikatora klienta, klucz tajny klienta i końcowym tokenów OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="21566-117">tooadd a new **Microsoft Azure Service Principal,** enter hello following values: Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span>

![Poświadczenia platformy Azure](./media/jenkins-azure-vm-agents/service-principal.png)

* <span data-ttu-id="21566-119">Kliknij przycisk **konfiguracji Sprawdź** toomake się, że hello profilu konfiguracji są poprawne.</span><span class="sxs-lookup"><span data-stu-id="21566-119">Click **Verify configuration** toomake sure that hello profile configuration is correct.</span></span>
* <span data-ttu-id="21566-120">Zapisz konfigurację hello i kontynuować toohello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="21566-120">Save hello configuration, and continue toohello next step.</span></span>

## <a name="template-configuration"></a><span data-ttu-id="21566-121">Konfigurowanie szablonu</span><span class="sxs-lookup"><span data-stu-id="21566-121">Template configuration</span></span>

### <a name="general-configuration"></a><span data-ttu-id="21566-122">Konfiguracja ogólna</span><span class="sxs-lookup"><span data-stu-id="21566-122">General configuration</span></span>
<span data-ttu-id="21566-123">Skonfiguruj szablon do użycia toodefine agenta maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="21566-123">Next, configure a template for use toodefine an Azure VM agent.</span></span> 

* <span data-ttu-id="21566-124">Kliknij przycisk **Dodaj** tooadd szablonu.</span><span class="sxs-lookup"><span data-stu-id="21566-124">Click **Add** tooadd a template.</span></span> 
* <span data-ttu-id="21566-125">Wpisz nazwę nowego szablonu.</span><span class="sxs-lookup"><span data-stu-id="21566-125">Provide a name for your new template.</span></span> 
* <span data-ttu-id="21566-126">Etykiety hello wprowadź "ubuntu."</span><span class="sxs-lookup"><span data-stu-id="21566-126">For hello label, enter  "ubuntu."</span></span> <span data-ttu-id="21566-127">Etykieta jest używany podczas konfigurowania zadania hello.</span><span class="sxs-lookup"><span data-stu-id="21566-127">This label is used during hello job configuration.</span></span>
* <span data-ttu-id="21566-128">Wybierz odpowiedni region hello z hello pola kombi.</span><span class="sxs-lookup"><span data-stu-id="21566-128">Select hello desired region from hello combo box.</span></span>
* <span data-ttu-id="21566-129">Witaj wybierz żądany rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="21566-129">Select hello desired VM size.</span></span>
* <span data-ttu-id="21566-130">Określ nazwę konta usługi Azure Storage hello lub pozostaw nazwę domyślną hello puste toouse "jenkinsarmst."</span><span class="sxs-lookup"><span data-stu-id="21566-130">Specify hello Azure Storage account name or leave it blank toouse hello default name "jenkinsarmst."</span></span>
* <span data-ttu-id="21566-131">Określ czas przechowywania hello w minutach.</span><span class="sxs-lookup"><span data-stu-id="21566-131">Specify hello retention time in minutes.</span></span> <span data-ttu-id="21566-132">To ustawienie określa hello liczbę minut oczekiwania przez Wpięć przed usunięciem automatycznie bezczynności agenta.</span><span class="sxs-lookup"><span data-stu-id="21566-132">This setting defines hello number of minutes Jenkins can wait before automatically deleting an idle agent.</span></span> <span data-ttu-id="21566-133">Określ 0, jeśli nie chcesz toobe bezczynności agentów automatycznie usuwane.</span><span class="sxs-lookup"><span data-stu-id="21566-133">Specify 0 if you do not want idle agents toobe deleted automatically.</span></span>

![Konfiguracja ogólna](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a><span data-ttu-id="21566-135">Konfiguracja obrazu</span><span class="sxs-lookup"><span data-stu-id="21566-135">Image configuration</span></span>

<span data-ttu-id="21566-136">Wybierz toocreate agenta systemu Linux (Ubuntu), **obrazu odniesienia** i użyj powitania po konfiguracji, na przykład.</span><span class="sxs-lookup"><span data-stu-id="21566-136">toocreate a Linux (Ubuntu) agent, select **Image reference** and use hello following configuration as an example.</span></span> <span data-ttu-id="21566-137">Odwołuje się zbyt[portalu Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) hello Azure najnowsze obsługiwanych obrazów.</span><span class="sxs-lookup"><span data-stu-id="21566-137">Refer too[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) for hello latest Azure supported images.</span></span>

* <span data-ttu-id="21566-138">Image Publisher: Canonical</span><span class="sxs-lookup"><span data-stu-id="21566-138">Image Publisher: Canonical</span></span>
* <span data-ttu-id="21566-139">Image Offer: UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="21566-139">Image Offer: UbuntuServer</span></span>
* <span data-ttu-id="21566-140">Image Sku: 14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="21566-140">Image Sku: 14.04.5-LTS</span></span>
* <span data-ttu-id="21566-141">Image version: latest</span><span class="sxs-lookup"><span data-stu-id="21566-141">Image version: latest</span></span>
* <span data-ttu-id="21566-142">OS Type: Linux</span><span class="sxs-lookup"><span data-stu-id="21566-142">OS Type: Linux</span></span>
* <span data-ttu-id="21566-143">Launch method: SSH</span><span class="sxs-lookup"><span data-stu-id="21566-143">Launch method: SSH</span></span>
* <span data-ttu-id="21566-144">Wprowadź poświadczenia administratora</span><span class="sxs-lookup"><span data-stu-id="21566-144">Provide an admin credentials</span></span>
* <span data-ttu-id="21566-145">W przypadku skryptu inicjowania maszyny wirtualnej wpisz:</span><span class="sxs-lookup"><span data-stu-id="21566-145">For VM initialization script, enter:</span></span>
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![Konfiguracja obrazu](./media/jenkins-azure-vm-agents/image-config.png)

* <span data-ttu-id="21566-147">Kliknij przycisk **Sprawdź szablon** tooverify hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="21566-147">Click **Verify Template** tooverify hello configuration.</span></span>
* <span data-ttu-id="21566-148">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="21566-148">Click **Save**.</span></span>

## <a name="create-a-job-in-jenkins"></a><span data-ttu-id="21566-149">Tworzenie zadania w usłudze Jenkins</span><span class="sxs-lookup"><span data-stu-id="21566-149">Create a job in Jenkins</span></span>

* <span data-ttu-id="21566-150">W ramach hello Wpięć pulpitu nawigacyjnego, kliknij przycisk **nowy element**.</span><span class="sxs-lookup"><span data-stu-id="21566-150">Within hello Jenkins dashboard, click **New Item**.</span></span> 
* <span data-ttu-id="21566-151">Wprowadź nazwę, wybierz **Freestyle project** (Projekt Freestyle) i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="21566-151">Enter a name and select **Freestyle project** and click **OK**.</span></span>
* <span data-ttu-id="21566-152">W hello **ogólne** kartę, wybierz "Ograniczenia, gdzie można uruchomić projektu" i typie "ubuntu" w wyrażeniu etykiety.</span><span class="sxs-lookup"><span data-stu-id="21566-152">In hello **General** tab, select "Restrict where project can be run" and type "ubuntu" in Label Expression.</span></span> <span data-ttu-id="21566-153">Pojawi się "ubuntu" w hello listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="21566-153">You now see "ubuntu" in hello dropdown.</span></span>
* <span data-ttu-id="21566-154">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="21566-154">Click **Save**.</span></span>

![Konfigurowanie zadania](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a><span data-ttu-id="21566-156">Tworzenie nowego projektu</span><span class="sxs-lookup"><span data-stu-id="21566-156">Build your new project</span></span>

* <span data-ttu-id="21566-157">Wrócić do poprzedniej strony pulpitu nawigacyjnego Wpięć toohello.</span><span class="sxs-lookup"><span data-stu-id="21566-157">Go back toohello Jenkins dashboard.</span></span>
* <span data-ttu-id="21566-158">Utworzono nowe zadanie powitania kliknij prawym przyciskiem myszy, kliknij przycisk **kompilacji teraz**.</span><span class="sxs-lookup"><span data-stu-id="21566-158">Right-click hello new job you created, then click **Build now**.</span></span> <span data-ttu-id="21566-159">Rozpocznie się kompilowanie.</span><span class="sxs-lookup"><span data-stu-id="21566-159">A build is kicked off.</span></span> 
* <span data-ttu-id="21566-160">Po zakończeniu kompilacji hello Przejdź zbyt**dane wyjściowe konsoli**.</span><span class="sxs-lookup"><span data-stu-id="21566-160">Once hello build is complete, go too**Console output**.</span></span> <span data-ttu-id="21566-161">Możesz sprawdzić, czy hello kompilacji została wykonana zdalnie na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="21566-161">You see that hello build was performed remotely on Azure.</span></span>

![Dane wyjściowe konsoli](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a><span data-ttu-id="21566-163">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="21566-163">Reference</span></span>

* <span data-ttu-id="21566-164">Wideo z cyklu „Piątek z Azure”: [Ciągła integracja z usługą Jenkins przy użyciu agentów maszyn wirtualnych platformy Azure](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span><span class="sxs-lookup"><span data-stu-id="21566-164">Azure Friday video: [Continuous Integration with Jenkins using Azure VM agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span></span>
* <span data-ttu-id="21566-165">Informacje uzupełniające i opcje konfiguracji: [Wiki wtyczki agentów maszyn wirtualnych platformy Azure dla usługi Jenkins](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span><span class="sxs-lookup"><span data-stu-id="21566-165">Support information and configuration options:  [Azure VM Agent Jenkins Plugin Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span></span> 

