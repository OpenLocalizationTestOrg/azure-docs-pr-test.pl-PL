---
title: "Witaj aaaDeploy usługi mobilności odzyskiwania lokacji z usługi Konfiguracja DSC automatyzacji Azure | Dokumentacja firmy Microsoft"
description: "Opisuje, jak tooautomatically Konfiguracja DSC automatyzacji Azure toouse wdrożyć usługę mobilności odzyskiwania lokacji Azure hello oraz agenta platformy Azure dla maszyny Wirtualnej VMware i tooAzure replikacji serwera fizycznego"
services: site-recovery
documentationcenter: 
author: krnese
manager: lorenr
editor: 
ms.assetid: 1f8cd3ac-0522-48eb-a5f0-679ee9192ddb
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: krnese
ms.openlocfilehash: 52cdd13ceb61718a21137180c55db86919af5929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a><span data-ttu-id="d8d9c-103">Wdrażanie usługi mobilności hello usłudze Konfiguracja DSC automatyzacji Azure replikacji maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d8d9c-103">Deploy hello Mobility service with Azure Automation DSC for replication of VM</span></span>
<span data-ttu-id="d8d9c-104">W programie Operations Management Suite możemy umożliwiają kompleksowe tworzenie kopii zapasowych i rozwiązanie odzyskiwania po awarii, których mogą używać jako część planu zapewnienia ciągłości działalności.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-104">In Operations Management Suite, we provide you with a comprehensive backup and disaster recovery solution that you can use as part of your business continuity plan.</span></span>

<span data-ttu-id="d8d9c-105">Ten przebieg razem z funkcją Hyper-V firma Microsoft uruchomiona przy użyciu funkcji Hyper-V Replica.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-105">We started this journey together with Hyper-V by using Hyper-V Replica.</span></span> <span data-ttu-id="d8d9c-106">Ale mamy rozwinięte toosupport heterogenicznych Instalatora ponieważ klienci mają wiele funkcji hypervisor i platform w ich chmury.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-106">But we have expanded toosupport a heterogeneous setup because customers have multiple hypervisors and platforms in their clouds.</span></span>

<span data-ttu-id="d8d9c-107">Jeśli używasz obciążeń VMware i/lub serwerów fizycznych dzisiaj, serwer zarządzania wszystkich hello składniki usługi Azure Site Recovery w Twoje środowisko toohandle hello komunikacji i danych replikacji z platformy Azure, jest uruchamiane przy Azure folderu docelowego.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-107">If you are running VMware workloads and/or physical servers today, a management server runs all of hello Azure Site Recovery components in your environment toohandle hello communication and data replication with Azure, when Azure is your destination.</span></span>

## <a name="deploy-hello-site-recovery-mobility-service-by-using-automation-dsc"></a><span data-ttu-id="d8d9c-108">Wdrażanie usługi mobilności odzyskiwania lokacji hello przy użyciu usługi Konfiguracja DSC automatyzacji</span><span class="sxs-lookup"><span data-stu-id="d8d9c-108">Deploy hello Site Recovery Mobility service by using Automation DSC</span></span>
<span data-ttu-id="d8d9c-109">Zacznijmy wykonując szybki podział czego ten serwer zarządzania.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-109">Let's start by doing a quick breakdown of what this management server does.</span></span>

<span data-ttu-id="d8d9c-110">Serwer zarządzania Hello uruchamia kilka ról serwera.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-110">hello management server runs several server roles.</span></span> <span data-ttu-id="d8d9c-111">Jedną z tych ról jest *konfiguracji*, która koordynuje komunikacji i zarządza procesami replikacji i odzyskiwania danych.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-111">One of these roles is *configuration*, which coordinates communication and manages data replication and recovery processes.</span></span>

<span data-ttu-id="d8d9c-112">Ponadto hello *procesu* roli działa jako brama replikacji.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-112">In addition, hello *process* role acts as a replication gateway.</span></span> <span data-ttu-id="d8d9c-113">Ta rola odbiera dane replikacji z chronionych maszyn źródłowych, optymalizuje je przy użyciu pamięci podręcznej, kompresji i szyfrowania, a następnie wysyła on tooan kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-113">This role receives replication data from protected source machines, optimizes it with caching, compression, and encryption, and then sends it tooan Azure storage account.</span></span> <span data-ttu-id="d8d9c-114">Jedna hello funkcji dla roli proces hello jest również instalacji toopush hello mobilności usługi tooprotected maszyn i automatyczne odnajdywanie maszyn wirtualnych VMware.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-114">One of hello functions for hello process role is also toopush installation of hello Mobility service tooprotected machines and perform automatic discovery of VMware VMs.</span></span>

<span data-ttu-id="d8d9c-115">W przypadku powrotu po awarii z platformy Azure, hello *główny cel* roli będzie obsługiwać hello replikacji danych w ramach tej operacji.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-115">If there's a failback from Azure, hello *master target* role will handle hello replication data as part of this operation.</span></span>

<span data-ttu-id="d8d9c-116">Hello chronione maszyny, możemy polegać na powitania *usługi mobilności*.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-116">For hello protected machines, we rely on hello *Mobility service*.</span></span> <span data-ttu-id="d8d9c-117">Ten składnik jest maszyną wdrożonej tooevery (maszyny Wirtualnej VMware lub serwerów fizycznych), które mają tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-117">This component is deployed tooevery machine (VMware VM or physical server) that you want tooreplicate tooAzure.</span></span> <span data-ttu-id="d8d9c-118">On przechwytywania zapisów danych na komputerze hello i przekazuje je toohello serwera zarządzania (rola w procesie).</span><span class="sxs-lookup"><span data-stu-id="d8d9c-118">It captures data writes on hello machine and forwards them toohello management server (process role).</span></span>

<span data-ttu-id="d8d9c-119">W przypadku zajmujące ciągłość prowadzenia działalności biznesowej, jest ważne toounderstand obciążeń z infrastruktury i hello składniki zaangażowane.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-119">When you're dealing with business continuity, it's important toounderstand your workloads, your infrastructure, and hello components involved.</span></span> <span data-ttu-id="d8d9c-120">Można następnie spełniać wymagania hello w celu czasu odzyskiwania (RTO) i cel punktu odzyskiwania (RPO).</span><span class="sxs-lookup"><span data-stu-id="d8d9c-120">You can then meet hello requirements for your recovery time objective (RTO) and recovery point objective (RPO).</span></span> <span data-ttu-id="d8d9c-121">W tym kontekście hello usługa mobilności jest tooensuring kluczy chronionych obciążeń zgodnie z regułami.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-121">In this context, hello Mobility service is key tooensuring that your workloads are protected as you would expect.</span></span>

<span data-ttu-id="d8d9c-122">W jaki sposób, w sposób zoptymalizowane zapewnić że niezawodnej Instalatora chronionych za pomocą z niektórych składników usługi Operations Management Suite?</span><span class="sxs-lookup"><span data-stu-id="d8d9c-122">So how can you, in an optimized way, ensure that you have a reliable protected setup with help from some Operations Management Suite components?</span></span>

<span data-ttu-id="d8d9c-123">W tym artykule przedstawiono przykład używania żądanego stanu konfiguracji (Konfiguracja DSC automatyzacji Azure), wraz z usługi Site Recovery tooensure który:</span><span class="sxs-lookup"><span data-stu-id="d8d9c-123">This article provides an example of how you can use Azure Automation Desired State Configuration (DSC), together with Site Recovery, tooensure that:</span></span>

* <span data-ttu-id="d8d9c-124">agent maszyny Wirtualnej platformy Azure i usługi mobilności Hello są toohello wdrożonej maszyny z systemem Windows, które mają tooprotect.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-124">hello Mobility service and Azure VM agent are deployed toohello Windows machines that you want tooprotect.</span></span>
* <span data-ttu-id="d8d9c-125">agent maszyny Wirtualnej platformy Azure i usługi mobilności Hello zawsze działają w przypadku Azure to hello lokalizacją docelową replikacji.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-125">hello Mobility service and Azure VM agent are always running when Azure is hello replication target.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8d9c-126">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d8d9c-126">Prerequisites</span></span>
* <span data-ttu-id="d8d9c-127">Instalacja wymagana hello toostore repozytorium</span><span class="sxs-lookup"><span data-stu-id="d8d9c-127">A repository toostore hello required setup</span></span>
* <span data-ttu-id="d8d9c-128">Witaj toostore repozytorium wymagane hasło tooregister z serwerem zarządzania hello</span><span class="sxs-lookup"><span data-stu-id="d8d9c-128">A repository toostore hello required passphrase tooregister with hello management server</span></span>

  > [!NOTE]
  > <span data-ttu-id="d8d9c-129">Unikatowe hasło jest generowane dla każdego serwera zarządzania.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-129">A unique passphrase is generated for each management server.</span></span> <span data-ttu-id="d8d9c-130">Jeśli ma toodeploy wiele serwerów zarządzania, należy tooensure tego hello prawidłowe hasło jest przechowywane w pliku passphrase.txt hello.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-130">If you are going toodeploy multiple management servers, you have tooensure that hello correct passphrase is stored in hello passphrase.txt file.</span></span>
  >
  >
* <span data-ttu-id="d8d9c-131">Windows Management Framework (WMF) zainstalowany na komputerach hello mają tooenable ochrony (wymagania dotyczące usługi Konfiguracja DSC automatyzacji) w wersji 5.0</span><span class="sxs-lookup"><span data-stu-id="d8d9c-131">Windows Management Framework (WMF) 5.0 installed on hello machines that you want tooenable for protection (a requirement for Automation DSC)</span></span>

  > [!NOTE]
  > <span data-ttu-id="d8d9c-132">Jeśli chcesz toouse maszyny DSC dla systemu Windows, które mają zainstalowaną WMF 4.0, zobacz sekcję hello [DSC użytku w środowiskach rozłączonych](## Use DSC in disconnected environments).</span><span class="sxs-lookup"><span data-stu-id="d8d9c-132">If you want toouse DSC for Windows machines that have WMF 4.0 installed, see hello section [Use DSC in disconnected environments](## Use DSC in disconnected environments).</span></span>
  

<span data-ttu-id="d8d9c-133">usługi mobilności Hello można zainstalować za pomocą wiersza polecenia hello i przyjmuje wiele argumentów.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-133">hello Mobility service can be installed through hello command line and accepts several arguments.</span></span> <span data-ttu-id="d8d9c-134">Dlatego należy plików binarnych hello toohave (po wyodrębnianie je z ustawień) i przechowywać je w miejscu, gdzie można je odzyskać za pomocą konfiguracji DSC.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-134">That’s why you need toohave hello binaries (after extracting them from your setup) and store them in a place where you can retrieve them by using a DSC configuration.</span></span>

## <a name="step-1-extract-binaries"></a><span data-ttu-id="d8d9c-135">Krok 1: Pliki binarne wyodrębniania</span><span class="sxs-lookup"><span data-stu-id="d8d9c-135">Step 1: Extract binaries</span></span>
1. <span data-ttu-id="d8d9c-136">potrzebne dla tej instalacji, pliki hello tooextract Przeglądaj toohello następującego katalogu na serwerze zarządzania:</span><span class="sxs-lookup"><span data-stu-id="d8d9c-136">tooextract hello files that you need for this setup, browse toohello following directory on your management server:</span></span>

    <span data-ttu-id="d8d9c-137">**\Microsoft azure lokacji Recovery\home\svsystems\pushinstallsvc\repository**</span><span class="sxs-lookup"><span data-stu-id="d8d9c-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span></span>

    <span data-ttu-id="d8d9c-138">W tym folderze powinien zostać wyświetlony plik MSI o nazwie:</span><span class="sxs-lookup"><span data-stu-id="d8d9c-138">In this folder, you should see an MSI file named:</span></span>

    <span data-ttu-id="d8d9c-139">**ASR_UA_version_Windows_GA_date_Release.exe firmy Microsoft**</span><span class="sxs-lookup"><span data-stu-id="d8d9c-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span></span>

    <span data-ttu-id="d8d9c-140">Witaj Użyj następującego polecenia tooextract hello Instalatora:</span><span class="sxs-lookup"><span data-stu-id="d8d9c-140">Use hello following command tooextract hello installer:</span></span>

    <span data-ttu-id="d8d9c-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span><span class="sxs-lookup"><span data-stu-id="d8d9c-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span></span>
2. <span data-ttu-id="d8d9c-142">Zaznacz wszystkie pliki i wysyłać je tooa skompresowanego folderu (zip).</span><span class="sxs-lookup"><span data-stu-id="d8d9c-142">Select all files and send them tooa compressed (zipped) folder.</span></span>

<span data-ttu-id="d8d9c-143">Masz teraz hello plików binarnych muszą tooautomate ustawienia hello hello usługi mobilności przy użyciu usługi Konfiguracja DSC automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-143">You now have hello binaries that you need tooautomate hello setup of hello Mobility service by using Automation DSC.</span></span>

### <a name="passphrase"></a><span data-ttu-id="d8d9c-144">Hasło</span><span class="sxs-lookup"><span data-stu-id="d8d9c-144">Passphrase</span></span>
<span data-ttu-id="d8d9c-145">Następnie należy toodetermine miejscu tooplace tego folderu zip.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-145">Next, you need toodetermine where you want tooplace this zipped folder.</span></span> <span data-ttu-id="d8d9c-146">Konto magazynu platformy Azure, można użyć jako pokazano później, toostore hello hasło, które należy hello instalacji.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-146">You can use an Azure storage account, as shown later, toostore hello passphrase that you need for hello setup.</span></span> <span data-ttu-id="d8d9c-147">następnie zarejestruje Hello agenta z serwerem zarządzania hello jako część procesu hello.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-147">hello agent will then register with hello management server as part of hello process.</span></span>

<span data-ttu-id="d8d9c-148">Witaj hasło, które uzyskano podczas wdrażania serwera zarządzania hello mogą zostać zapisane jako passphrase.txt tooa pliku tekstowego.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-148">hello passphrase that you got when you deployed hello management server can be saved tooa text file as passphrase.txt.</span></span>

<span data-ttu-id="d8d9c-149">Umieść zarówno hello folderu zip, jak i hasło hello w dedykowanych kontenera w hello kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-149">Place both hello zipped folder and hello passphrase in a dedicated container in hello Azure storage account.</span></span>

![Lokalizacja folderu](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

<span data-ttu-id="d8d9c-151">Jeśli wolisz tookeep tych plików w udziale w sieci, możesz to zrobić.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-151">If you prefer tookeep these files on a share on your network, you can do so.</span></span> <span data-ttu-id="d8d9c-152">Wystarczy tooensure że hello DSC zasobu, która będzie używana później ma dostęp i można uzyskać Instalator hello i hasło.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-152">You just need tooensure that hello DSC resource that you will be using later has access and can get hello setup and passphrase.</span></span>

## <a name="step-2-create-hello-dsc-configuration"></a><span data-ttu-id="d8d9c-153">Krok 2: Tworzenie konfiguracji hello DSC</span><span class="sxs-lookup"><span data-stu-id="d8d9c-153">Step 2: Create hello DSC configuration</span></span>
<span data-ttu-id="d8d9c-154">Instalator Hello zależy od WMF 5.0.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-154">hello setup depends on WMF 5.0.</span></span> <span data-ttu-id="d8d9c-155">Witaj maszyny toosuccessfully zastosować hello konfiguracji za pomocą usługi Konfiguracja DSC automatyzacji, WMF 5.0 musi toobe obecny.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-155">For hello machine toosuccessfully apply hello configuration through Automation DSC, WMF 5.0 needs toobe present.</span></span>

<span data-ttu-id="d8d9c-156">środowisko Hello używa powitania po Przykładowa konfiguracja DSC:</span><span class="sxs-lookup"><span data-stu-id="d8d9c-156">hello environment uses hello following example DSC configuration:</span></span>

```powershell
configuration ASRMobilityService {

    $RemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    $RemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    $RemoteAzureAgent = 'http://go.microsoft.com/fwlink/p/?LinkId=394789'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node localhost {

        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
```
<span data-ttu-id="d8d9c-157">Konfiguracja Hello będzie wykonywać następujące hello:</span><span class="sxs-lookup"><span data-stu-id="d8d9c-157">hello configuration will do hello following:</span></span>

* <span data-ttu-id="d8d9c-158">zmienne Hello poinformuje hello konfiguracji, gdzie tooget hello pliki binarne usługi mobilności hello i hello agenta maszyny Wirtualnej Azure, gdzie tooget hello hasło, a dane wyjściowe toostore hello.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-158">hello variables will tell hello configuration where tooget hello binaries for hello Mobility service and hello Azure VM agent, where tooget hello passphrase, and where toostore hello output.</span></span>
* <span data-ttu-id="d8d9c-159">Hello konfiguracji zaimportuje hello xPSDesiredStateConfiguration DSC zasobów, dzięki czemu można używać `xRemoteFile` toodownload hello pliki z repozytorium hello.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-159">hello configuration will import hello xPSDesiredStateConfiguration DSC resource, so that you can use `xRemoteFile` toodownload hello files from hello repository.</span></span>
* <span data-ttu-id="d8d9c-160">Konfiguracja Hello utworzy katalog, w którym ma pliki binarne hello toostore.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-160">hello configuration will create a directory where you want toostore hello binaries.</span></span>
* <span data-ttu-id="d8d9c-161">Witaj archiwum zasobów zostanie Wyodrębnij pliki hello z folderu zip hello.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-161">hello archive resource will extract hello files from hello zipped folder.</span></span>
* <span data-ttu-id="d8d9c-162">zasób instalacji pakietu Hello zainstaluje usługi mobilności hello z hello UNIFIEDAGENT. Wywołanie pliku EXE Instalatora hello określonych argumentów.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-162">hello package Install resource will install hello Mobility service from hello UNIFIEDAGENT.EXE installer with hello specific arguments.</span></span> <span data-ttu-id="d8d9c-163">(hello zmiennych, które skonstruować argumenty hello konieczne tooreflect toobe zmienić środowiska).</span><span class="sxs-lookup"><span data-stu-id="d8d9c-163">(hello variables that construct hello arguments need toobe changed tooreflect your environment.)</span></span>
* <span data-ttu-id="d8d9c-164">Hello pakietu zasobów AzureAgent spowoduje zainstalowanie agenta maszyny Wirtualnej Azure hello, co jest zalecane na każdej maszynie Wirtualnej, która działa na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-164">hello package AzureAgent resource will install hello Azure VM agent, which is recommended on every VM that runs in Azure.</span></span> <span data-ttu-id="d8d9c-165">agent maszyny Wirtualnej Azure Hello ułatwia też możliwe tooadd toohello rozszerzenia maszyny Wirtualnej po pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-165">hello Azure VM agent also makes it possible tooadd extensions toohello VM after failover.</span></span>
* <span data-ttu-id="d8d9c-166">Witaj usługi lub zasobów zapewnia, że hello powiązane usługi mobilności i hello usług platformy Azure są zawsze uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-166">hello service resource or resources will ensure that hello related Mobility services and hello Azure services are always running.</span></span>

<span data-ttu-id="d8d9c-167">Zapisz konfigurację hello **ASRMobilityService**.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-167">Save hello configuration as **ASRMobilityService**.</span></span>

> [!NOTE]
> <span data-ttu-id="d8d9c-168">Należy pamiętać hello tooreplace CSIP na serwerze konfiguracji tooreflect hello rzeczywiste Zarządzanie tak, aby hello agent zostanie poprawnie podłączone i użyje hello poprawne hasło.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-168">Remember tooreplace hello CSIP in your configuration tooreflect hello actual management server, so that hello agent will be connected correctly and will use hello correct passphrase.</span></span>
>
>

## <a name="step-3-upload-tooautomation-dsc"></a><span data-ttu-id="d8d9c-169">Krok 3: Przekaż tooAutomation DSC</span><span class="sxs-lookup"><span data-stu-id="d8d9c-169">Step 3: Upload tooAutomation DSC</span></span>
<span data-ttu-id="d8d9c-170">Ponieważ konfiguracji hello DSC wprowadzone zaimportuje wymagane moduł zasobów DSC (xPSDesiredStateConfiguration), należy tooimport ten moduł w automatyzacji przed przekazaniem konfiguracji hello DSC.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-170">Because hello DSC configuration that you made will import a required DSC resource module (xPSDesiredStateConfiguration), you need tooimport that module in Automation before you upload hello DSC configuration.</span></span>

<span data-ttu-id="d8d9c-171">Logowanie tooyour konta automatyzacji Przeglądaj zbyt**zasoby** > **modułów**i kliknij przycisk **galerii przeglądania**.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-171">Sign in tooyour Automation account, browse too**Assets** > **Modules**, and click **Browse Gallery**.</span></span>

<span data-ttu-id="d8d9c-172">W tym miejscu można znaleźć modułu hello i zaimportuj go tooyour konta.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-172">Here you can search for hello module and import it tooyour account.</span></span>

![Importowanie modułu](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

<span data-ttu-id="d8d9c-174">Po zakończeniu, przejdź tooyour maszyny, gdzie masz hello Azure Resource Manager modułów zainstalowanych i kontynuować konfiguracji DSC tooimport hello nowo utworzony.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-174">When you finish this, go tooyour machine where you have hello Azure Resource Manager modules installed and proceed tooimport hello newly created DSC configuration.</span></span>

### <a name="import-cmdlets"></a><span data-ttu-id="d8d9c-175">Poleceń cmdlet importu</span><span class="sxs-lookup"><span data-stu-id="d8d9c-175">Import cmdlets</span></span>
<span data-ttu-id="d8d9c-176">W programie PowerShell Zaloguj tooyour subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-176">In PowerShell, sign in tooyour Azure subscription.</span></span> <span data-ttu-id="d8d9c-177">Modyfikowanie hello tooreflect poleceń cmdlet środowiska i przechwycić informacje o koncie automatyzacji w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="d8d9c-177">Modify hello cmdlets tooreflect your environment and capture your Automation account information in a variable:</span></span>

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

<span data-ttu-id="d8d9c-178">Przekaż hello konfiguracji tooAutomation DSC za pomocą następującego polecenia cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="d8d9c-178">Upload hello configuration tooAutomation DSC by using hello following cmdlet:</span></span>

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-hello-configuration-in-automation-dsc"></a><span data-ttu-id="d8d9c-179">Kompiluj hello konfiguracji DSC automatyzacji</span><span class="sxs-lookup"><span data-stu-id="d8d9c-179">Compile hello configuration in Automation DSC</span></span>
<span data-ttu-id="d8d9c-180">Następnie należy toocompile hello konfiguracji DSC automatyzacji tak, aby uruchomić tooregister tooit węzłów.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-180">Next, you need toocompile hello configuration in Automation DSC, so that you can start tooregister nodes tooit.</span></span> <span data-ttu-id="d8d9c-181">Możesz osiągnąć, uruchamiając następujące polecenie cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="d8d9c-181">You achieve that by running hello following cmdlet:</span></span>

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

<span data-ttu-id="d8d9c-182">Może to zająć kilka minut, ponieważ jest wdrażany zasadniczo hello konfiguracji toohello hostowanej DSC ściągania usługi.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-182">This can take a few minutes, because you're basically deploying hello configuration toohello hosted DSC pull service.</span></span>

<span data-ttu-id="d8d9c-183">Po skompilowaniu hello konfiguracji mogą pobierać informacje zadania hello przy użyciu programu PowerShell (Get-AzureRmAutomationDscCompilationJob) lub za pomocą hello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d8d9c-183">After you compile hello configuration, you can retrieve hello job information by using PowerShell (Get-AzureRmAutomationDscCompilationJob) or by using hello [Azure portal](https://portal.azure.com/).</span></span>

![Pobieranie zadania](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

<span data-ttu-id="d8d9c-185">Teraz pomyślnie opublikowany i przekazać Twojej tooAutomation konfiguracji DSC usługi Konfiguracja DSC.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-185">You have now successfully published and uploaded your DSC configuration tooAutomation DSC.</span></span>

## <a name="step-4-onboard-machines-tooautomation-dsc"></a><span data-ttu-id="d8d9c-186">Krok 4: Dołączenia maszyny tooAutomation DSC</span><span class="sxs-lookup"><span data-stu-id="d8d9c-186">Step 4: Onboard machines tooAutomation DSC</span></span>
> [!NOTE]
> <span data-ttu-id="d8d9c-187">Jednym z wymagań wstępnych hello wykonywania czynności opisanych w tym scenariuszu jest czy maszynach z systemem Windows są aktualizowane przy użyciu najnowszej wersji platformy WMF hello.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-187">One of hello prerequisites for completing this scenario is that your Windows machines are updated with hello latest version of WMF.</span></span> <span data-ttu-id="d8d9c-188">Można pobrać i zainstalować poprawną wersję powitania dla danej platformy z hello [Centrum pobierania](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="d8d9c-188">You can download and install hello correct version for your platform from hello [Download Center](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>
>
>

<span data-ttu-id="d8d9c-189">Teraz utworzysz metaconfig zastosuje tooyour węzłów DSC.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-189">You will now create a metaconfig for DSC that you will apply tooyour nodes.</span></span> <span data-ttu-id="d8d9c-190">toosucceed z tym, należy tooretrieve hello punktu końcowego adresu URL i hello klucz podstawowy dla wybranego konta automatyzacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-190">toosucceed with this, you need tooretrieve hello endpoint URL and hello primary key for your selected Automation account in Azure.</span></span> <span data-ttu-id="d8d9c-191">Te wartości można znaleźć **klucze** na powitania **wszystkie ustawienia** bloku hello konta automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-191">You can find these values under **Keys** on hello **All settings** blade for hello Automation account.</span></span>

![Wartości klucza](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

<span data-ttu-id="d8d9c-193">W tym przykładzie masz serwera fizycznego systemu Windows Server 2012 R2, które mają tooprotect przy użyciu usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-193">In this example, you have a Windows Server 2012 R2 physical server that you want tooprotect by using Site Recovery.</span></span>

### <a name="check-for-any-pending-file-rename-operations-in-hello-registry"></a><span data-ttu-id="d8d9c-194">Sprawdź, czy wszystkie oczekujące operacje zmiany nazwy pliku w rejestrze hello</span><span class="sxs-lookup"><span data-stu-id="d8d9c-194">Check for any pending file rename operations in hello registry</span></span>
<span data-ttu-id="d8d9c-195">Przed rozpoczęciem tooassociate powitania serwera z punktem końcowym usługi Konfiguracja DSC automatyzacji hello zaleca się sprawdzanie wszelkie oczekujące operacje zmiany nazwy pliku w rejestrze hello.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-195">Before you start tooassociate hello server with hello Automation DSC endpoint, we recommend that you check for any pending file rename operations in hello registry.</span></span> <span data-ttu-id="d8d9c-196">One może zabrania hello Instalator zakończył powodu tooa oczekujące na ponowny rozruch.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-196">They might prohibit hello setup from finishing due tooa pending reboot.</span></span>

<span data-ttu-id="d8d9c-197">Uruchom następujące polecenia cmdlet tooverify nie oczekuje na ponowne uruchomienie na powitania serwera istnieje hello:</span><span class="sxs-lookup"><span data-stu-id="d8d9c-197">Run hello following cmdlet tooverify that there’s no pending reboot on hello server:</span></span>

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
<span data-ttu-id="d8d9c-198">Jeśli ten pokazuje puste, to OK tooproceed.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-198">If this shows empty, you are OK tooproceed.</span></span> <span data-ttu-id="d8d9c-199">Jeśli nie, należy spełnić to przez ponowny rozruch serwera hello w oknie obsługi.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-199">If not, you should address this by rebooting hello server during a maintenance window.</span></span>

<span data-ttu-id="d8d9c-200">tooapply hello konfiguracji na serwerze hello rozpoczęciem hello PowerShell Integrated Scripting Environment (ISE) i uruchom hello następującego skryptu.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-200">tooapply hello configuration on hello server, start hello PowerShell Integrated Scripting Environment (ISE) and run hello following script.</span></span> <span data-ttu-id="d8d9c-201">Jest to zasadniczo lokalnej konfiguracji DSC poinstruować hello lokalny program Configuration Manager aparat tooregister z hello usługi Konfiguracja DSC automatyzacji i pobrać hello określonej konfiguracji (ASRMobilityService.localhost).</span><span class="sxs-lookup"><span data-stu-id="d8d9c-201">This is essentially a DSC local configuration that will instruct hello Local Configuration Manager engine tooregister with hello Automation DSC service and retrieve hello specific configuration (ASRMobilityService.localhost).</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration metaconfig {
    param (
        $URL,
        $Key
    )
    node localhost {
        Settings {
            RefreshFrequencyMins = '30'
            RebootNodeIfNeeded = $true
            RefreshMode = 'PULL'
            ActionAfterReboot = 'ContinueConfiguration'
            ConfigurationMode = 'ApplyAndMonitor'
            AllowModuleOverwrite = $true
        }

        ResourceRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }

        ConfigurationRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
            ConfigurationNames = 'ASRMobilityService.localhost'
        }

        ReportServerWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }
    }
}
metaconfig -URL 'https://we-agentservice-prod-1.azure-automation.net/accounts/<YOURAAAccountID>' -Key '<YOURAAAccountKey>'

Set-DscLocalConfigurationManager .\metaconfig -Force -Verbose
```

<span data-ttu-id="d8d9c-202">Ta konfiguracja spowoduje tooregister aparatu, sama hello lokalny program Configuration Manager z usługi Konfiguracja DSC automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-202">This configuration will cause hello Local Configuration Manager engine tooregister itself with Automation DSC.</span></span> <span data-ttu-id="d8d9c-203">Również określi, jak powinien działać aparat hello, co jego zrobić, jeśli istnieje kilka konfiguracji (ApplyAndAutoCorrect) i jak go należy kontynuować konfiguracji hello Jeśli ponowne uruchomienie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-203">It will also determine how hello engine should operate, what it should do if there's a configuration drift (ApplyAndAutoCorrect), and how it should proceed with hello configuration if a reboot is required.</span></span>

<span data-ttu-id="d8d9c-204">Po uruchomieniu tego skryptu węzła hello powinien się rozpoczynać tooregister usługi Konfiguracja DSC automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-204">After you run this script, hello node should start tooregister with Automation DSC.</span></span>

![Trwa rejestrowanie węzła](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

<span data-ttu-id="d8d9c-206">Wróć toohello portalu Azure widać tego węzła do nowo zarejestrowanych hello okazało się teraz w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-206">If you go back toohello Azure portal, you can see that hello newly registered node has now appeared in hello portal.</span></span>

![Zarejestrowany węzła w portalu hello](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

<span data-ttu-id="d8d9c-208">Na serwerze hello można uruchomić następującego środowiska PowerShell zostały poprawnie zarejestrowane tooverify polecenia cmdlet, które hello węzła hello:</span><span class="sxs-lookup"><span data-stu-id="d8d9c-208">On hello server, you can run hello following PowerShell cmdlet tooverify that hello node has been registered correctly:</span></span>

```powershell
Get-DscLocalConfigurationManager
```

<span data-ttu-id="d8d9c-209">Po konfiguracji hello został pobrany i stosowane toohello serwera, można to sprawdzić, uruchamiając następujące polecenie cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="d8d9c-209">After hello configuration has been pulled and applied toohello server, you can verify this by running hello following cmdlet:</span></span>

```powershell
Get-DscConfigurationStatus
```

<span data-ttu-id="d8d9c-210">dane wyjściowe Hello pokazuje powitania serwera został pomyślnie pobierane jego konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="d8d9c-210">hello output shows that hello server has successfully pulled its configuration:</span></span>

![Dane wyjściowe](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

<span data-ttu-id="d8d9c-212">Ponadto instalacji usługi mobilności hello ma własny dziennik, który znajduje się w temacie *SystemDrive*\ProgramData\ASRSetupLogs.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-212">In addition, hello Mobility service setup has its own log that can be found at *SystemDrive*\ProgramData\ASRSetupLogs.</span></span>

<span data-ttu-id="d8d9c-213">To wszystko.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-213">That’s it.</span></span> <span data-ttu-id="d8d9c-214">Teraz pomyślnie wdrożone i zarejestrowane hello usługi mobilności na maszynie hello mają tooprotect przy użyciu usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-214">You have now successfully deployed and registered hello Mobility service on hello machine that you want tooprotect by using Site Recovery.</span></span> <span data-ttu-id="d8d9c-215">DSC będzie upewnij się, czy zawsze są uruchomione usługi hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-215">DSC will make sure that hello required services are always running.</span></span>

![Pomyślne wdrożenie](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

<span data-ttu-id="d8d9c-217">Po serwera zarządzania hello wykryje hello pomyślne wdrożenie, można skonfigurować ochrony i włączyć replikację na maszynie hello przy użyciu usługi Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-217">After hello management server detects hello successful deployment, you can configure protection and enable replication on hello machine by using Site Recovery.</span></span>

## <a name="use-dsc-in-disconnected-environments"></a><span data-ttu-id="d8d9c-218">Użyj usługi Konfiguracja DSC w środowiskach rozłączonych</span><span class="sxs-lookup"><span data-stu-id="d8d9c-218">Use DSC in disconnected environments</span></span>
<span data-ttu-id="d8d9c-219">Jeśli komputery nie są toohello połączenia internetowego, można nadal zależą od DSC toodeploy i skonfigurować usługi mobilności hello na powitania obciążeń, które mają tooprotect.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-219">If your machines aren’t connected toohello Internet, you can still rely on DSC toodeploy and configure hello Mobility service on hello workloads that you want tooprotect.</span></span>

<span data-ttu-id="d8d9c-220">Możliwe jest utworzenie własnych serwera ściągania usługi Konfiguracja DSC w danym środowisku tooessentially Podaj hello takie same możliwości, które można uzyskać z usługi Konfiguracja DSC automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-220">You can instantiate your own DSC pull server in your environment tooessentially provide hello same capabilities that you get from Automation DSC.</span></span> <span data-ttu-id="d8d9c-221">Oznacza to klientom Witaj będzie pobierać hello konfiguracji (po jej zarejestrowaniu) toohello DSC punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-221">That is, hello clients will pull hello configuration (after it's registered) toohello DSC endpoint.</span></span> <span data-ttu-id="d8d9c-222">Innym rozwiązaniem jest jednak toomanually wypychania hello DSC konfiguracji tooyour maszyny lokalnie lub zdalnie.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-222">However, another option is toomanually push hello DSC configuration tooyour machines, either locally or remotely.</span></span>

<span data-ttu-id="d8d9c-223">Należy pamiętać, że w tym przykładzie dodano parametr dla nazwy komputera hello.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-223">Note that in this example, there's an added parameter for hello computer name.</span></span> <span data-ttu-id="d8d9c-224">pliki zdalne Hello teraz znajdują się w udziale zdalnym, który powinien być dostępny przez hello maszyny, które mają tooprotect.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-224">hello remote files are now located on a remote share that should be accessible by hello machines that you want tooprotect.</span></span> <span data-ttu-id="d8d9c-225">Witaj na końcu skryptu hello enacts hello konfiguracji, a następnie uruchamia komputer docelowy toohello konfiguracji DSC tooapply hello.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-225">hello end of hello script enacts hello configuration and then starts tooapply hello DSC configuration toohello target computer.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="d8d9c-226">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d8d9c-226">Prerequisites</span></span>
<span data-ttu-id="d8d9c-227">Upewnij się, że zainstalowano ten moduł programu PowerShell xPSDesiredStateConfiguration hello.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-227">Make sure that hello xPSDesiredStateConfiguration PowerShell module is installed.</span></span> <span data-ttu-id="d8d9c-228">Dla komputerów z systemem Windows zainstalowaną WMF 5.0 można zainstalować moduł xPSDesiredStateConfiguration hello, uruchamiając następujące polecenia cmdlet na komputerach docelowych hello hello:</span><span class="sxs-lookup"><span data-stu-id="d8d9c-228">For Windows machines where WMF 5.0 is installed, you can install hello xPSDesiredStateConfiguration module by running hello following cmdlet on hello target machines:</span></span>

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

<span data-ttu-id="d8d9c-229">Można również pobrać i zapisać hello modułu, w razie potrzeby toodistribute on tooWindows maszyny, które mają WMF 4.0.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-229">You can also download and save hello module in case you need toodistribute it tooWindows machines that have WMF 4.0.</span></span> <span data-ttu-id="d8d9c-230">Uruchom to polecenie cmdlet na komputerze, w którym występuje PowerShellGet (WMF 5.0):</span><span class="sxs-lookup"><span data-stu-id="d8d9c-230">Run this cmdlet on a machine where PowerShellGet (WMF 5.0) is present:</span></span>

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

<span data-ttu-id="d8d9c-231">Dla WMF 4.0, upewnij się również, że hello [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) jest zainstalowane na maszynie hello.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-231">Also for WMF 4.0, ensure that hello [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) is installed on hello machines.</span></span>

<span data-ttu-id="d8d9c-232">Witaj następującej konfiguracji może zostać umieszczony tooWindows maszyny, które mają WMF 5.0 i programu WMF 4.0:</span><span class="sxs-lookup"><span data-stu-id="d8d9c-232">hello following configuration can be pushed tooWindows machines that have WMF 5.0 and WMF 4.0:</span></span>

```powershell
configuration ASRMobilityService {
    param (
        [Parameter(Mandatory=$true)]
        [ValidateNotNullOrEmpty()]
        [System.String] $ComputerName
    )

    $RemoteFile = '\\myfileserver\share\asr.zip'
    $RemotePassphrase = '\\myfileserver\share\passphrase.txt'
    $RemoteAzureAgent = '\\myfileserver\share\AzureVmAgent.msi'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node $ComputerName {      
        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
ASRMobilityService -ComputerName 'MyTargetComputerName'

Start-DscConfiguration .\ASRMobilityService -Wait -Force -Verbose
```

<span data-ttu-id="d8d9c-233">Tooinstantiate własne serwera ściągania usługi Konfiguracja DSC na możliwości hello toomimic sieci firmowej, które można pobrać z usługi Konfiguracja DSC automatyzacji, zobacz [ustawienie serwera ściągania usługi Konfiguracja DSC sieci web](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="d8d9c-233">If you want tooinstantiate your own DSC pull server on your corporate network toomimic hello capabilities that you can get from Automation DSC, see [Setting up a DSC web pull server](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span></span>

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a><span data-ttu-id="d8d9c-234">Opcjonalnie: Wdrażanie konfiguracji DSC przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d8d9c-234">Optional: Deploy a DSC configuration by using an Azure Resource Manager template</span></span>
<span data-ttu-id="d8d9c-235">Ten artykuł ma fokus w sposób tworzenia własnych tooautomatically konfiguracji DSC wdrażania usługi mobilności hello i hello Agent maszyny Wirtualnej — oraz upewnij się, że działają na maszynach hello, które mają tooprotect.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-235">This article has focused on how you can create your own DSC configuration tooautomatically deploy hello Mobility service and hello Azure VM Agent--and ensure that they are running on hello machines that you want tooprotect.</span></span> <span data-ttu-id="d8d9c-236">Mamy także szablonu usługi Azure Resource Manager, który zostanie wdrożona tego DSC konfiguracji tooa nowe lub istniejące konto usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-236">We also have an Azure Resource Manager template that will deploy this DSC configuration tooa new or existing Azure Automation account.</span></span> <span data-ttu-id="d8d9c-237">Szablon Hello będzie używać parametrów wejściowych toocreate automatyzacji zasoby zawierające hello zmienne dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-237">hello template will use input parameters toocreate Automation assets that will contain hello variables for your environment.</span></span>

<span data-ttu-id="d8d9c-238">Po wdrożeniu hello szablonu można po prostu odwołać toostep 4 w tym tooonboard przewodnik maszynach.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-238">After you deploy hello template, you can simply refer toostep 4 in this guide tooonboard your machines.</span></span>

<span data-ttu-id="d8d9c-239">Szablon Hello wykona następujące hello:</span><span class="sxs-lookup"><span data-stu-id="d8d9c-239">hello template will do hello following:</span></span>

1. <span data-ttu-id="d8d9c-240">Użyj istniejącego konta automatyzacji lub Utwórz nową</span><span class="sxs-lookup"><span data-stu-id="d8d9c-240">Use an existing Automation account or create a new one</span></span>
2. <span data-ttu-id="d8d9c-241">Przeprowadzanie parametrów wejściowych:</span><span class="sxs-lookup"><span data-stu-id="d8d9c-241">Take input parameters for:</span></span>
   * <span data-ttu-id="d8d9c-242">ASRRemoteFile--hello lokalizacji, gdzie są przechowywane instalacji usługi mobilności hello</span><span class="sxs-lookup"><span data-stu-id="d8d9c-242">ASRRemoteFile--hello location where you have stored hello Mobility service setup</span></span>
   * <span data-ttu-id="d8d9c-243">ASRPassphrase--hello lokalizacji, gdzie są przechowywane hello passphrase.txt pliku</span><span class="sxs-lookup"><span data-stu-id="d8d9c-243">ASRPassphrase--hello location where you have stored hello passphrase.txt file</span></span>
   * <span data-ttu-id="d8d9c-244">ASRCSEndpoint — Witaj adres IP serwera zarządzania</span><span class="sxs-lookup"><span data-stu-id="d8d9c-244">ASRCSEndpoint--hello IP address of your management server</span></span>
3. <span data-ttu-id="d8d9c-245">Zaimportuj moduł programu PowerShell xPSDesiredStateConfiguration hello</span><span class="sxs-lookup"><span data-stu-id="d8d9c-245">Import hello xPSDesiredStateConfiguration PowerShell module</span></span>
4. <span data-ttu-id="d8d9c-246">Tworzenie i kompilacja hello konfiguracji DSC</span><span class="sxs-lookup"><span data-stu-id="d8d9c-246">Create and compile hello DSC configuration</span></span>

<span data-ttu-id="d8d9c-247">Witaj wszystkich poprzednich krokach nastąpi w odpowiedniej kolejności hello, tak aby można było uruchomić dołączania maszynach do ochrony.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-247">All hello preceding steps will happen in hello right order, so that you can start onboarding your machines for protection.</span></span>

<span data-ttu-id="d8d9c-248">Szablon Hello, instrukcje dotyczące wdrażania, znajduje się na [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span><span class="sxs-lookup"><span data-stu-id="d8d9c-248">hello template, with instructions for deployment, is located on [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span></span>

<span data-ttu-id="d8d9c-249">Wdrażanie szablonu hello przy użyciu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d8d9c-249">Deploy hello template by using PowerShell:</span></span>

```powershell
$RGDeployArgs = @{
    Name = 'DSC3'
    ResourceGroupName = 'KNOMS'
    TemplateFile = 'https://raw.githubusercontent.com/krnese/AzureDeploy/master/OMS/MSOMS/DSC/azuredeploy.json'
    OMSAutomationAccountName = 'KNOMSAA'
    ASRRemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    ASRRemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    ASRCSEndpoint = '10.0.0.115'
    DSCJobGuid = [System.Guid]::NewGuid().ToString()
}
New-AzureRmResourceGroupDeployment @RGDeployArgs -Verbose
```

## <a name="next-steps"></a><span data-ttu-id="d8d9c-250">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d8d9c-250">Next steps</span></span>
<span data-ttu-id="d8d9c-251">Po wdrożeniu agentów usługa mobilności hello można [włączyć replikację](site-recovery-vmware-to-azure.md) hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="d8d9c-251">After you deploy hello Mobility service agents, you can [enable replication](site-recovery-vmware-to-azure.md) for hello virtual machines.</span></span>
