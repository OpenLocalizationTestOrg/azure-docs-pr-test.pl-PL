---
title: "aaaAzure omówienie agenta maszyny Wirtualnej systemu Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooinstall i konfigurowanie maszyny wirtualnej interakcji z kontrolerem sieci szkieletowej Azure toomanage agenta systemu Linux (agenta waagent)."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: e41de979-6d56-40b0-8916-895bf215ded6
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: szark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4e08c84d9205f4db7aae6fd1568ec1f15fba395c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-and-using-hello-azure-linux-agent"></a><span data-ttu-id="74473-103">Opis i przy użyciu hello Azure agenta systemu Linux</span><span class="sxs-lookup"><span data-stu-id="74473-103">Understanding and using hello Azure Linux Agent</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a><span data-ttu-id="74473-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="74473-104">Introduction</span></span>
<span data-ttu-id="74473-105">Witaj Linux Agent usługi Microsoft Azure (agenta waagent) zarządza systemu Linux i FreeBSD inicjowania obsługi administracyjnej i maszyny Wirtualnej interakcji z hello Azure kontrolera sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="74473-105">hello Microsoft Azure Linux Agent (waagent) manages Linux & FreeBSD provisioning, and VM interaction with hello Azure Fabric Controller.</span></span> <span data-ttu-id="74473-106">Udostępnia ona następujące funkcje dla wdrożenia systemu Linux i FreeBSD IaaS hello:</span><span class="sxs-lookup"><span data-stu-id="74473-106">It provides hello following functionality for Linux and FreeBSD IaaS deployments:</span></span>

> [!NOTE]
> <span data-ttu-id="74473-107">Zobacz agenta systemu Linux Azure hello [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) dodatkowe szczegóły.</span><span class="sxs-lookup"><span data-stu-id="74473-107">See hello Azure Linux agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) for additional details.</span></span>
> 
> 

* <span data-ttu-id="74473-108">**Inicjowanie obsługi obrazu**</span><span class="sxs-lookup"><span data-stu-id="74473-108">**Image Provisioning**</span></span>
  
  * <span data-ttu-id="74473-109">Tworzenie konta użytkownika</span><span class="sxs-lookup"><span data-stu-id="74473-109">Creation of a user account</span></span>
  * <span data-ttu-id="74473-110">Konfigurowanie typów uwierzytelniania SSH</span><span class="sxs-lookup"><span data-stu-id="74473-110">Configuring SSH authentication types</span></span>
  * <span data-ttu-id="74473-111">Wdrożenie par kluczy i kluczy publicznych SSH</span><span class="sxs-lookup"><span data-stu-id="74473-111">Deployment of SSH public keys and key pairs</span></span>
  * <span data-ttu-id="74473-112">Nazwa hosta hello ustawienia</span><span class="sxs-lookup"><span data-stu-id="74473-112">Setting hello host name</span></span>
  * <span data-ttu-id="74473-113">Platforma toohello nazwy hosta hello publikowania DNS</span><span class="sxs-lookup"><span data-stu-id="74473-113">Publishing hello host name toohello platform DNS</span></span>
  * <span data-ttu-id="74473-114">Platforma toohello klucza odcisk palca hosta raportowania SSH</span><span class="sxs-lookup"><span data-stu-id="74473-114">Reporting SSH host key fingerprint toohello platform</span></span>
  * <span data-ttu-id="74473-115">Zarządzanie zasobami dysku</span><span class="sxs-lookup"><span data-stu-id="74473-115">Resource Disk Management</span></span>
  * <span data-ttu-id="74473-116">Formatowanie i instalowania hello zasobu dysku</span><span class="sxs-lookup"><span data-stu-id="74473-116">Formatting and mounting hello resource disk</span></span>
  * <span data-ttu-id="74473-117">Konfigurowanie obszaru wymiany</span><span class="sxs-lookup"><span data-stu-id="74473-117">Configuring swap space</span></span>
* <span data-ttu-id="74473-118">**Sieć**</span><span class="sxs-lookup"><span data-stu-id="74473-118">**Networking**</span></span>
  
  * <span data-ttu-id="74473-119">Zarządza tras tooimprove zgodność z serwerami DHCP platformy</span><span class="sxs-lookup"><span data-stu-id="74473-119">Manages routes tooimprove compatibility with platform DHCP servers</span></span>
  * <span data-ttu-id="74473-120">Zapewnia stabilność hello Nazwa interfejsu sieciowego hello</span><span class="sxs-lookup"><span data-stu-id="74473-120">Ensures hello stability of hello network interface name</span></span>
* <span data-ttu-id="74473-121">**Jądra**</span><span class="sxs-lookup"><span data-stu-id="74473-121">**Kernel**</span></span>
  
  * <span data-ttu-id="74473-122">Konfiguruje wirtualną architekturę NUMA (Wyłącz dla jądra < 2.6.37)</span><span class="sxs-lookup"><span data-stu-id="74473-122">Configures virtual NUMA (disable for kernel <2.6.37)</span></span>
  * <span data-ttu-id="74473-123">Wykorzystuje entropii funkcji Hyper-V dla /dev/random</span><span class="sxs-lookup"><span data-stu-id="74473-123">Consumes Hyper-V entropy for /dev/random</span></span>
  * <span data-ttu-id="74473-124">Konfiguruje SCSI przekroczeń limitu czasu dla urządzenia głównego hello, (który może być zdalne)</span><span class="sxs-lookup"><span data-stu-id="74473-124">Configures SCSI timeouts for hello root device (which could be remote)</span></span>
* <span data-ttu-id="74473-125">**Diagnostyka**</span><span class="sxs-lookup"><span data-stu-id="74473-125">**Diagnostics**</span></span>
  
  * <span data-ttu-id="74473-126">Port szeregowy toohello przekierowania konsoli</span><span class="sxs-lookup"><span data-stu-id="74473-126">Console redirection toohello serial port</span></span>
* <span data-ttu-id="74473-127">**Wdrożenia programu SCVMM**</span><span class="sxs-lookup"><span data-stu-id="74473-127">**SCVMM Deployments**</span></span>
  
  * <span data-ttu-id="74473-128">Wykrywa i używa do ładowania agenta VMM hello Linux podczas uruchamiania w środowisku programu System Center Virtual Machine Manager 2012 R2</span><span class="sxs-lookup"><span data-stu-id="74473-128">Detects and bootstraps hello VMM agent for Linux when running in a System Center Virtual Machine Manager 2012 R2 environment</span></span>
* <span data-ttu-id="74473-129">**Rozszerzenia maszyny Wirtualnej**</span><span class="sxs-lookup"><span data-stu-id="74473-129">**VM Extension**</span></span>
  
  * <span data-ttu-id="74473-130">Wstaw składnik utworzone przez firmę Microsoft i partnerów do automatyzacji oprogramowania i konfiguracji tooenable maszyny Wirtualnej systemu Linux (IaaS)</span><span class="sxs-lookup"><span data-stu-id="74473-130">Inject component authored by Microsoft and Partners into Linux VM (IaaS) tooenable software and configuration automation</span></span>
  * <span data-ttu-id="74473-131">Implementacja odwołanie rozszerzenia maszyny Wirtualnej na [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span><span class="sxs-lookup"><span data-stu-id="74473-131">VM Extension reference implementation on [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span></span>

## <a name="communication"></a><span data-ttu-id="74473-132">Komunikacja</span><span class="sxs-lookup"><span data-stu-id="74473-132">Communication</span></span>
<span data-ttu-id="74473-133">przepływ informacji Hello hello platformy toohello agenta odbywa się za pośrednictwem dwóch kanałów:</span><span class="sxs-lookup"><span data-stu-id="74473-133">hello information flow from hello platform toohello agent occurs via two channels:</span></span>

* <span data-ttu-id="74473-134">Czas rozruchu dołączonych dysków DVD do wdrożenia IaaS.</span><span class="sxs-lookup"><span data-stu-id="74473-134">A boot-time attached DVD for IaaS deployments.</span></span> <span data-ttu-id="74473-135">Ten dysk DVD zawiera zgodne OVF pliku konfiguracji, który zawiera wszystkie informacje o udostępnianiu niż rzeczywista keypairs SSH hello.</span><span class="sxs-lookup"><span data-stu-id="74473-135">This DVD includes an OVF-compliant configuration file that includes all provisioning information other than hello actual SSH keypairs.</span></span>
* <span data-ttu-id="74473-136">Punkt końcowy protokołu TCP udostępnianie interfejsu API REST używany tooobtain wdrażanie i Konfigurowanie topologii.</span><span class="sxs-lookup"><span data-stu-id="74473-136">A TCP endpoint exposing a REST API used tooobtain deployment and topology configuration.</span></span>

## <a name="requirements"></a><span data-ttu-id="74473-137">Wymagania</span><span class="sxs-lookup"><span data-stu-id="74473-137">Requirements</span></span>
<span data-ttu-id="74473-138">Witaj następujących systemów zostały przetestowane i są znane toowork z hello Azure agenta systemu Linux:</span><span class="sxs-lookup"><span data-stu-id="74473-138">hello following systems have been tested and are known toowork with hello Azure Linux Agent:</span></span>

> [!NOTE]
> <span data-ttu-id="74473-139">Ta lista może się różnić od hello oficjalnego listę obsługiwanych systemów na powitania platformie Microsoft Azure, zgodnie z opisem w tym miejscu: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span><span class="sxs-lookup"><span data-stu-id="74473-139">This list may differ from hello official list of supported systems on hello Microsoft Azure Platform, as described here: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span></span>
> 
> 

* <span data-ttu-id="74473-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="74473-140">CoreOS</span></span>
* <span data-ttu-id="74473-141">CentOS 6.3 +</span><span class="sxs-lookup"><span data-stu-id="74473-141">CentOS 6.3+</span></span>
* <span data-ttu-id="74473-142">Red Hat Enterprise Linux 6.7 +</span><span class="sxs-lookup"><span data-stu-id="74473-142">Red Hat Enterprise Linux 6.7+</span></span>
* <span data-ttu-id="74473-143">Debian 7.0 +</span><span class="sxs-lookup"><span data-stu-id="74473-143">Debian 7.0+</span></span>
* <span data-ttu-id="74473-144">Ubuntu 12.04 +</span><span class="sxs-lookup"><span data-stu-id="74473-144">Ubuntu 12.04+</span></span>
* <span data-ttu-id="74473-145">openSUSE 12.3 +</span><span class="sxs-lookup"><span data-stu-id="74473-145">openSUSE 12.3+</span></span>
* <span data-ttu-id="74473-146">SLES 11 Z DODATKIEM SP3 +</span><span class="sxs-lookup"><span data-stu-id="74473-146">SLES 11 SP3+</span></span>
* <span data-ttu-id="74473-147">Oracle Linux 6.4 +</span><span class="sxs-lookup"><span data-stu-id="74473-147">Oracle Linux 6.4+</span></span>

<span data-ttu-id="74473-148">Inne obsługiwane systemy:</span><span class="sxs-lookup"><span data-stu-id="74473-148">Other Supported Systems:</span></span>

* <span data-ttu-id="74473-149">FreeBSD 10 + (Azure agenta systemu Linux v2.0.10 +)</span><span class="sxs-lookup"><span data-stu-id="74473-149">FreeBSD 10+ (Azure Linux Agent v2.0.10+)</span></span>

<span data-ttu-id="74473-150">agenta systemu Linux Hello jest zależna od niektórych pakietów systemu w kolejności toofunction prawidłowo:</span><span class="sxs-lookup"><span data-stu-id="74473-150">hello Linux agent depends on some system packages in order toofunction properly:</span></span>

* <span data-ttu-id="74473-151">Python 2.6 +</span><span class="sxs-lookup"><span data-stu-id="74473-151">Python 2.6+</span></span>
* <span data-ttu-id="74473-152">Biblioteki OpenSSL 1.0 +</span><span class="sxs-lookup"><span data-stu-id="74473-152">OpenSSL 1.0+</span></span>
* <span data-ttu-id="74473-153">OpenSSH 5.3 +</span><span class="sxs-lookup"><span data-stu-id="74473-153">OpenSSH 5.3+</span></span>
* <span data-ttu-id="74473-154">Narzędzia systemu plików: ulec sfdisk fdisk, mkfs,</span><span class="sxs-lookup"><span data-stu-id="74473-154">Filesystem utilities: sfdisk, fdisk, mkfs, parted</span></span>
* <span data-ttu-id="74473-155">Narzędzia hasło: chpasswd, sudo</span><span class="sxs-lookup"><span data-stu-id="74473-155">Password tools: chpasswd, sudo</span></span>
* <span data-ttu-id="74473-156">Narzędzia do edycji tekstu: mniejszyć, grep</span><span class="sxs-lookup"><span data-stu-id="74473-156">Text processing tools: sed, grep</span></span>
* <span data-ttu-id="74473-157">Narzędzia sieci: trasy ip</span><span class="sxs-lookup"><span data-stu-id="74473-157">Network tools: ip-route</span></span>
* <span data-ttu-id="74473-158">Obsługuje jądra służący do instalowania funkcji zdefiniowanej przez użytkownika, systemy plików.</span><span class="sxs-lookup"><span data-stu-id="74473-158">Kernel support for mounting UDF filesystems.</span></span>

## <a name="installation"></a><span data-ttu-id="74473-159">Instalacja</span><span class="sxs-lookup"><span data-stu-id="74473-159">Installation</span></span>
<span data-ttu-id="74473-160">Instalacja przy użyciu obr. / min lub pakietu DEB z repozytorium pakietów programu dystrybucji jest hello preferowana metoda Instalowanie i uaktualnianie hello Azure agenta systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="74473-160">Installation using an RPM or a DEB package from your distribution's package repository is hello preferred method of installing and upgrading hello Azure Linux Agent.</span></span> <span data-ttu-id="74473-161">Wszystkie hello [zatwierdzone dostawców dystrybucji](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) zintegrować pakiet agenta platformy Azure Linux hello repozytoriami i obrazów.</span><span class="sxs-lookup"><span data-stu-id="74473-161">All hello [endorsed distribution providers](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrate hello Azure Linux agent package into their images and repositories.</span></span>

<span data-ttu-id="74473-162">Zapoznaj się z dokumentacją toohello w hello [repozytorium agenta systemu Linux platformy Azure w serwisie GitHub](https://github.com/Azure/WALinuxAgent) dla zaawansowane opcje instalacji, takich jak instalowanie z lokalizacji źródłowej lub toocustom lub prefiksów.</span><span class="sxs-lookup"><span data-stu-id="74473-162">Refer toohello documentation in hello [Azure Linux Agent repo on GitHub](https://github.com/Azure/WALinuxAgent) for advanced installation options, such as installing from source or toocustom locations or prefixes.</span></span>

## <a name="command-line-options"></a><span data-ttu-id="74473-163">Opcje wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="74473-163">Command Line Options</span></span>
### <a name="flags"></a><span data-ttu-id="74473-164">Flagi</span><span class="sxs-lookup"><span data-stu-id="74473-164">Flags</span></span>
* <span data-ttu-id="74473-165">verbose: Zwiększ poziom szczegółowości określonego polecenia</span><span class="sxs-lookup"><span data-stu-id="74473-165">verbose: Increase verbosity of specified command</span></span>
* <span data-ttu-id="74473-166">Wymuś: Pomiń interakcyjne potwierdzenie dla niektórych poleceń</span><span class="sxs-lookup"><span data-stu-id="74473-166">force: Skip interactive confirmation for some commands</span></span>

### <a name="commands"></a><span data-ttu-id="74473-167">Polecenia</span><span class="sxs-lookup"><span data-stu-id="74473-167">Commands</span></span>
* <span data-ttu-id="74473-168">Pomoc: Wyświetla listę poleceń hello obsługiwane i flagi.</span><span class="sxs-lookup"><span data-stu-id="74473-168">help: Lists hello supported commands and flags.</span></span>
* <span data-ttu-id="74473-169">deprovision: próba tooclean hello systemu i zapewnić ich nadające się do ponownego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="74473-169">deprovision: Attempt tooclean hello system and make it suitable for re-provisioning.</span></span> <span data-ttu-id="74473-170">Ta operacja usunięte hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="74473-170">This operation deleted hello following:</span></span>
  
  * <span data-ttu-id="74473-171">Wszystkie klucze hosta SSH (jeśli Provisioning.RegenerateSshHostKeyPair "y" w pliku konfiguracyjnym hello)</span><span class="sxs-lookup"><span data-stu-id="74473-171">All SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in hello configuration file)</span></span>
  * <span data-ttu-id="74473-172">Konfiguracja serwera nazw w /etc/resolv.conf</span><span class="sxs-lookup"><span data-stu-id="74473-172">Nameserver configuration in /etc/resolv.conf</span></span>
  * <span data-ttu-id="74473-173">Hasła głównego z /etc/shadow (jeśli Provisioning.DeleteRootPassword "y" w pliku konfiguracyjnym hello)</span><span class="sxs-lookup"><span data-stu-id="74473-173">Root password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in hello configuration file)</span></span>
  * <span data-ttu-id="74473-174">Buforowane dzierżawy klientów DHCP</span><span class="sxs-lookup"><span data-stu-id="74473-174">Cached DHCP client leases</span></span>
  * <span data-ttu-id="74473-175">Resetuje hosta toolocalhost.localdomain nazwy</span><span class="sxs-lookup"><span data-stu-id="74473-175">Resets host name toolocalhost.localdomain</span></span>

> [!WARNING]
> <span data-ttu-id="74473-176">Cofanie zastrzegania nie gwarantuje, że ten obraz powitania jest wyczyszczone wszystkie informacje poufne i odpowiedni w przypadku ponownej dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="74473-176">Deprovisioning does not guarantee that hello image is cleared of all sensitive information and suitable for redistribution.</span></span>
> 
> 

* <span data-ttu-id="74473-177">deprovision + użytkownika: wykonuje wszystkie elementy w obszarze - deprovision (powyżej) i również usuwa hello ostatnie konto użytkownika elastycznie (uzyskane z /var/lib/waagent) i skojarzone dane.</span><span class="sxs-lookup"><span data-stu-id="74473-177">deprovision+user: Performs everything under -deprovision (above) and also deletes hello last provisioned user account (obtained from /var/lib/waagent) and associated data.</span></span> <span data-ttu-id="74473-178">Ten parametr jest podczas usuwania inicjowania obsługi administracyjnej z obrazem, który został wcześniej inicjowania obsługi administracyjnej na platformie Azure, mogą być przechwytywane i ponownego użycia.</span><span class="sxs-lookup"><span data-stu-id="74473-178">This parameter is when de-provisioning an image that was previously provisioning on Azure so it may be captured and re-used.</span></span>
* <span data-ttu-id="74473-179">Wersja: Wyświetla hello wersji agenta waagent</span><span class="sxs-lookup"><span data-stu-id="74473-179">version: Displays hello version of waagent</span></span>
* <span data-ttu-id="74473-180">serialconsole: konfiguruje ttyS0 toomark CHODNIKÓW (hello pierwszego portu szeregowego) jako hello rozruchowe konsoli.</span><span class="sxs-lookup"><span data-stu-id="74473-180">serialconsole: Configures GRUB toomark ttyS0 (hello first serial port) as hello boot console.</span></span> <span data-ttu-id="74473-181">Dzięki temu jądra rozruchu dzienniki są wysyłane do portu szeregowego toothe, a udostępnione do debugowania.</span><span class="sxs-lookup"><span data-stu-id="74473-181">This ensures that kernel bootup logs are sent toothe serial port and made available for debugging.</span></span>
* <span data-ttu-id="74473-182">demon: uruchomiono agenta waagent jako demon toomanage interakcji z platformą hello.</span><span class="sxs-lookup"><span data-stu-id="74473-182">daemon: Run waagent as a daemon toomanage interaction with hello platform.</span></span> <span data-ttu-id="74473-183">Ten argument jest toowaagent określonego w skrypcie inicjowania agenta waagent hello.</span><span class="sxs-lookup"><span data-stu-id="74473-183">This argument is specified toowaagent in hello waagent init script.</span></span>
* <span data-ttu-id="74473-184">Rozpocznij: uruchomiono agenta waagent jako proces w tle</span><span class="sxs-lookup"><span data-stu-id="74473-184">start: Run waagent as a background process</span></span>

## <a name="configuration"></a><span data-ttu-id="74473-185">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="74473-185">Configuration</span></span>
<span data-ttu-id="74473-186">Plik konfiguracji (/ etc/waagent.conf) kontrolki hello agenta waagent akcje.</span><span class="sxs-lookup"><span data-stu-id="74473-186">A configuration file (/etc/waagent.conf) controls hello actions of waagent.</span></span> <span data-ttu-id="74473-187">Poniżej przedstawiono przykładowy plik konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="74473-187">A sample configuration file is shown below:</span></span>

    Provisioning.Enabled=y
    Provisioning.DeleteRootPassword=n
    Provisioning.RegenerateSshHostKeyPair=y
    Provisioning.SshHostKeyPairType=rsa
    Provisioning.MonitorHostName=y
    Provisioning.DecodeCustomData=n
    Provisioning.ExecuteCustomData=n
    Provisioning.PasswordCryptId=6
    Provisioning.PasswordCryptSaltLength=10
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.MountOptions=None
    ResourceDisk.EnableSwap=n
    ResourceDisk.SwapSizeMB=0
    LBProbeResponder=y
    Logs.Verbose=n
    OS.RootDeviceScsiTimeout=300
    OS.OpensslPath=None
    HttpProxy.Host=None
    HttpProxy.Port=None

<span data-ttu-id="74473-188">powitalne różne opcje konfiguracji są szczegółowo opisana poniżej.</span><span class="sxs-lookup"><span data-stu-id="74473-188">hello various configuration options are described in detail below.</span></span> <span data-ttu-id="74473-189">Opcje konfiguracji są trzy typy; Wartość logiczna, String lub Integer.</span><span class="sxs-lookup"><span data-stu-id="74473-189">Configuration options are of three types; Boolean, String or Integer.</span></span> <span data-ttu-id="74473-190">Opcje konfiguracji logiczna Hello można określić jako "y" lub "n".</span><span class="sxs-lookup"><span data-stu-id="74473-190">hello Boolean configuration options can be specified as "y" or "n".</span></span> <span data-ttu-id="74473-191">Witaj specjalne — słowo kluczowe "None" mogą być używane w przypadku niektórych ciąg typu konfiguracji wpisów zgodnie z opisem poniżej.</span><span class="sxs-lookup"><span data-stu-id="74473-191">hello special keyword "None" may be used for some string type configuration entries as detailed below.</span></span>

<span data-ttu-id="74473-192">**Provisioning.Enabled:**</span><span class="sxs-lookup"><span data-stu-id="74473-192">**Provisioning.Enabled:**</span></span>  
<span data-ttu-id="74473-193">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="74473-193">Type: Boolean</span></span>  
<span data-ttu-id="74473-194">Domyślne: y</span><span class="sxs-lookup"><span data-stu-id="74473-194">Default: y</span></span>

<span data-ttu-id="74473-195">To umożliwia tooenable użytkownika hello lub wyłącz hello inicjowania obsługi funkcji hello agenta.</span><span class="sxs-lookup"><span data-stu-id="74473-195">This allows hello user tooenable or disable hello provisioning functionality in hello agent.</span></span> <span data-ttu-id="74473-196">Prawidłowe wartości to "y" lub "n".</span><span class="sxs-lookup"><span data-stu-id="74473-196">Valid values are "y" or "n".</span></span> <span data-ttu-id="74473-197">Jeśli Inicjowanie obsługi administracyjnej jest wyłączone, hosta i użytkownika kluczy SSH w obrazie hello są zachowywane i określona w hello Azure API inicjowania obsługi administracyjnej konfiguracja jest ignorowana.</span><span class="sxs-lookup"><span data-stu-id="74473-197">If provisioning is disabled, SSH host and user keys in hello image are preserved and any configuration specified in hello Azure provisioning API is ignored.</span></span>

> [!NOTE]
> <span data-ttu-id="74473-198">Witaj `Provisioning.Enabled` zbyt "n" na Ubuntu chmury obrazów użyj init chmury w celu obsługi domyślne wartości parametrów.</span><span class="sxs-lookup"><span data-stu-id="74473-198">hello `Provisioning.Enabled` parameter defaults too"n" on Ubuntu Cloud Images that use cloud-init for provisioning.</span></span>
> 
> 

<span data-ttu-id="74473-199">**Provisioning.DeleteRootPassword:**</span><span class="sxs-lookup"><span data-stu-id="74473-199">**Provisioning.DeleteRootPassword:**</span></span>  
<span data-ttu-id="74473-200">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="74473-200">Type: Boolean</span></span>  
<span data-ttu-id="74473-201">Domyślne: n</span><span class="sxs-lookup"><span data-stu-id="74473-201">Default: n</span></span>

<span data-ttu-id="74473-202">Jeśli zestaw, hello hasła użytkownika root w hello/etc/pliku w tle zostanie wymazane podczas hello procesu inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="74473-202">If set, hello root password in hello /etc/shadow file is erased during hello provisioning process.</span></span>

<span data-ttu-id="74473-203">**Provisioning.RegenerateSshHostKeyPair:**</span><span class="sxs-lookup"><span data-stu-id="74473-203">**Provisioning.RegenerateSshHostKeyPair:**</span></span>  
<span data-ttu-id="74473-204">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="74473-204">Type: Boolean</span></span>  
<span data-ttu-id="74473-205">Domyślne: y</span><span class="sxs-lookup"><span data-stu-id="74473-205">Default: y</span></span>

<span data-ttu-id="74473-206">Jeśli zestawu i wszystkich hostów par kluczy SSH (ecdsa, dsa i rsa) zostaną usunięte podczas procesu z/etc/ssh/udostępniania hello.</span><span class="sxs-lookup"><span data-stu-id="74473-206">If set, all SSH host key pairs (ecdsa, dsa and rsa) are deleted during hello provisioning process from /etc/ssh/.</span></span> <span data-ttu-id="74473-207">I generowany jest jeden świeże pary kluczy.</span><span class="sxs-lookup"><span data-stu-id="74473-207">And a single fresh key pair is generated.</span></span>

<span data-ttu-id="74473-208">Typ szyfrowania Hello hello świeże pary kluczy jest konfigurowane przez hello Provisioning.SshHostKeyPairType wpisu.</span><span class="sxs-lookup"><span data-stu-id="74473-208">hello encryption type for hello fresh key pair is configurable by hello Provisioning.SshHostKeyPairType entry.</span></span> <span data-ttu-id="74473-209">Należy pamiętać, że niektórych dystrybucji zostaną ponownie utworzone par kluczy SSH dla wszystkich Brak typów szyfrowania, po ponownym uruchomieniu demon SSH hello (na przykład po ponownym rozruchu).</span><span class="sxs-lookup"><span data-stu-id="74473-209">Please note that some distributions will re-create SSH key pairs for any missing encryption types when hello SSH daemon is restarted (for example, upon a reboot).</span></span>

<span data-ttu-id="74473-210">**Provisioning.SshHostKeyPairType:**</span><span class="sxs-lookup"><span data-stu-id="74473-210">**Provisioning.SshHostKeyPairType:**</span></span>  
<span data-ttu-id="74473-211">Typ: ciąg</span><span class="sxs-lookup"><span data-stu-id="74473-211">Type: String</span></span>  
<span data-ttu-id="74473-212">Domyślne: rsa</span><span class="sxs-lookup"><span data-stu-id="74473-212">Default: rsa</span></span>

<span data-ttu-id="74473-213">Typ algorytmu szyfrowania tooan, który jest obsługiwany przez hello demon SSH na maszynie wirtualnej hello można go ustawić.</span><span class="sxs-lookup"><span data-stu-id="74473-213">This can be set tooan encryption algorithm type that is supported by hello SSH daemon on hello virtual machine.</span></span> <span data-ttu-id="74473-214">Hello zwykle obsługiwane wartości to "rsa", "dsa" i "ecdsa".</span><span class="sxs-lookup"><span data-stu-id="74473-214">hello typically supported values are "rsa", "dsa" and "ecdsa".</span></span> <span data-ttu-id="74473-215">Należy pamiętać, że "putty.exe" w systemie Windows nie obsługuje "ecdsa".</span><span class="sxs-lookup"><span data-stu-id="74473-215">Note that "putty.exe" on Windows does not support "ecdsa".</span></span> <span data-ttu-id="74473-216">Tak Jeśli planujesz toouse putty.exe na tooa tooconnect Windows wdrożenia systemu Linux, użyj "rsa" lub "dsa".</span><span class="sxs-lookup"><span data-stu-id="74473-216">So, if you intend toouse putty.exe on Windows tooconnect tooa Linux deployment, please use "rsa" or "dsa".</span></span>

<span data-ttu-id="74473-217">**Provisioning.MonitorHostName:**</span><span class="sxs-lookup"><span data-stu-id="74473-217">**Provisioning.MonitorHostName:**</span></span>  
<span data-ttu-id="74473-218">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="74473-218">Type: Boolean</span></span>  
<span data-ttu-id="74473-219">Domyślne: y</span><span class="sxs-lookup"><span data-stu-id="74473-219">Default: y</span></span>

<span data-ttu-id="74473-220">Jeśli ustawiona, agenta waagent monitorujący maszyny wirtualnej systemu Linux hello zmiany nazwy hosta (jak zwracany przez polecenie "Nazwa hosta" hello) i automatycznie Aktualizuj hello konfiguracji sieci w przypadku zmiany hello tooreflect obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="74473-220">If set, waagent will monitor hello Linux virtual machine for hostname changes (as returned by hello "hostname" command) and automatically update hello networking configuration in hello image tooreflect hello change.</span></span> <span data-ttu-id="74473-221">W nazwie hello toopush kolejności zmienić toohello serwerów DNS, sieci zostanie uruchomiona ponownie w hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="74473-221">In order toopush hello name change toohello DNS servers, networking will be restarted in hello virtual machine.</span></span> <span data-ttu-id="74473-222">Spowoduje to w skrócie utratę łączności z Internetem.</span><span class="sxs-lookup"><span data-stu-id="74473-222">This will result in brief loss of Internet connectivity.</span></span>

<span data-ttu-id="74473-223">**Provisioning.DecodeCustomData**</span><span class="sxs-lookup"><span data-stu-id="74473-223">**Provisioning.DecodeCustomData**</span></span>  
<span data-ttu-id="74473-224">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="74473-224">Type: Boolean</span></span>  
<span data-ttu-id="74473-225">Domyślne: n</span><span class="sxs-lookup"><span data-stu-id="74473-225">Default: n</span></span>

<span data-ttu-id="74473-226">Jeśli zostanie ustawiona, agenta waagent dekodowania CustomData z formatu Base64.</span><span class="sxs-lookup"><span data-stu-id="74473-226">If set, waagent will decode CustomData from Base64.</span></span>

<span data-ttu-id="74473-227">**Provisioning.ExecuteCustomData**</span><span class="sxs-lookup"><span data-stu-id="74473-227">**Provisioning.ExecuteCustomData**</span></span>  
<span data-ttu-id="74473-228">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="74473-228">Type: Boolean</span></span>  
<span data-ttu-id="74473-229">Domyślne: n</span><span class="sxs-lookup"><span data-stu-id="74473-229">Default: n</span></span>

<span data-ttu-id="74473-230">Jeśli ustawiona, agenta waagent wykona CustomData po zainicjowaniu obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="74473-230">If set, waagent will execute CustomData after provisioning.</span></span>

<span data-ttu-id="74473-231">**Provisioning.PasswordCryptId**</span><span class="sxs-lookup"><span data-stu-id="74473-231">**Provisioning.PasswordCryptId**</span></span>  
<span data-ttu-id="74473-232">Typ: ciąg</span><span class="sxs-lookup"><span data-stu-id="74473-232">Type:String</span></span>  
<span data-ttu-id="74473-233">Domyślne: 6</span><span class="sxs-lookup"><span data-stu-id="74473-233">Default:6</span></span>

<span data-ttu-id="74473-234">Algorytm używany przez crypt podczas generowania skrótu hasła.</span><span class="sxs-lookup"><span data-stu-id="74473-234">Algorithm used by crypt when generating password hash.</span></span>  
 <span data-ttu-id="74473-235">1 - MD5</span><span class="sxs-lookup"><span data-stu-id="74473-235">1 - MD5</span></span>  
 <span data-ttu-id="74473-236">2a - Blowfish</span><span class="sxs-lookup"><span data-stu-id="74473-236">2a - Blowfish</span></span>  
 <span data-ttu-id="74473-237">5 - ALGORYTMU SHA-256</span><span class="sxs-lookup"><span data-stu-id="74473-237">5 - SHA-256</span></span>  
 <span data-ttu-id="74473-238">6 - SHA-512</span><span class="sxs-lookup"><span data-stu-id="74473-238">6 - SHA-512</span></span>  

<span data-ttu-id="74473-239">**Provisioning.PasswordCryptSaltLength**</span><span class="sxs-lookup"><span data-stu-id="74473-239">**Provisioning.PasswordCryptSaltLength**</span></span>  
<span data-ttu-id="74473-240">Typ: ciąg</span><span class="sxs-lookup"><span data-stu-id="74473-240">Type:String</span></span>  
<span data-ttu-id="74473-241">Domyślny: 10</span><span class="sxs-lookup"><span data-stu-id="74473-241">Default:10</span></span>

<span data-ttu-id="74473-242">Długość losowe soli używana podczas generowania skrótu hasła.</span><span class="sxs-lookup"><span data-stu-id="74473-242">Length of random salt used when generating password hash.</span></span>

<span data-ttu-id="74473-243">**ResourceDisk.Format:**</span><span class="sxs-lookup"><span data-stu-id="74473-243">**ResourceDisk.Format:**</span></span>  
<span data-ttu-id="74473-244">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="74473-244">Type: Boolean</span></span>  
<span data-ttu-id="74473-245">Domyślne: y</span><span class="sxs-lookup"><span data-stu-id="74473-245">Default: y</span></span>

<span data-ttu-id="74473-246">Jeśli ustawiona, dysk zasobów hello dostarczony przez platformę hello jest formatowany i zainstalowanych w wyniku agenta waagent, jeśli typ filesystem hello żądany przez użytkownika hello w "ResourceDisk.Filesystem" jest inna niż "ntfs".</span><span class="sxs-lookup"><span data-stu-id="74473-246">If set, hello resource disk provided by hello platform will be formatted and mounted by waagent if hello filesystem type requested by hello user in "ResourceDisk.Filesystem" is anything other than "ntfs".</span></span> <span data-ttu-id="74473-247">Jednej partycji typu systemu Linux (83) są udostępniane na powitania dysku.</span><span class="sxs-lookup"><span data-stu-id="74473-247">A single partition of type Linux (83) will be made available on hello disk.</span></span> <span data-ttu-id="74473-248">Należy pamiętać, że ta partycja nie zostanie sformatowana Jeśli można zainstalować pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="74473-248">Note that this partition will not be formatted if it can be successfully mounted.</span></span>

<span data-ttu-id="74473-249">**ResourceDisk.Filesystem:**</span><span class="sxs-lookup"><span data-stu-id="74473-249">**ResourceDisk.Filesystem:**</span></span>  
<span data-ttu-id="74473-250">Typ: ciąg</span><span class="sxs-lookup"><span data-stu-id="74473-250">Type: String</span></span>  
<span data-ttu-id="74473-251">Domyślne: ext4</span><span class="sxs-lookup"><span data-stu-id="74473-251">Default: ext4</span></span>

<span data-ttu-id="74473-252">To określa typ plików hello hello zasobu dysku.</span><span class="sxs-lookup"><span data-stu-id="74473-252">This specifies hello filesystem type for hello resource disk.</span></span> <span data-ttu-id="74473-253">Obsługiwane wartości różnią się dystrybucji systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="74473-253">Supported values vary by Linux distribution.</span></span> <span data-ttu-id="74473-254">Jeśli ciąg hello jest X, następnie mkfs. X powinny znajdować się na powitania Linux obrazu.</span><span class="sxs-lookup"><span data-stu-id="74473-254">If hello string is X, then mkfs.X should be present on hello Linux image.</span></span> <span data-ttu-id="74473-255">SLES 11 obrazów zwykle należy użyć "ext3".</span><span class="sxs-lookup"><span data-stu-id="74473-255">SLES 11 images should typically use 'ext3'.</span></span> <span data-ttu-id="74473-256">Obrazy FreeBSD należy użyć "ufs2" w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="74473-256">FreeBSD images should use 'ufs2' here.</span></span>

<span data-ttu-id="74473-257">**ResourceDisk.MountPoint:**</span><span class="sxs-lookup"><span data-stu-id="74473-257">**ResourceDisk.MountPoint:**</span></span>  
<span data-ttu-id="74473-258">Typ: ciąg</span><span class="sxs-lookup"><span data-stu-id="74473-258">Type: String</span></span>  
<span data-ttu-id="74473-259">Wartość domyślna: / mnt/zasobu</span><span class="sxs-lookup"><span data-stu-id="74473-259">Default: /mnt/resource</span></span> 

<span data-ttu-id="74473-260">Określa ścieżkę hello jaką hello zasobu dysk jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="74473-260">This specifies hello path at which hello resource disk is mounted.</span></span> <span data-ttu-id="74473-261">Ten dysk zasobów hello jest *tymczasowego* na dysku i może opróżnić po anulowaną aprowizacją hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="74473-261">Note that hello resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span>

<span data-ttu-id="74473-262">**ResourceDisk.MountOptions**</span><span class="sxs-lookup"><span data-stu-id="74473-262">**ResourceDisk.MountOptions**</span></span>  
<span data-ttu-id="74473-263">Typ: ciąg</span><span class="sxs-lookup"><span data-stu-id="74473-263">Type: String</span></span>  
<span data-ttu-id="74473-264">Domyślnie: Brak</span><span class="sxs-lookup"><span data-stu-id="74473-264">Default: None</span></span>

<span data-ttu-id="74473-265">Określa opcje instalacji dysku toobe przekazany polecenie -o instalacji toohello.</span><span class="sxs-lookup"><span data-stu-id="74473-265">Specifies disk mount options toobe passed toohello mount -o command.</span></span> <span data-ttu-id="74473-266">Jest to rozdzielana przecinkami lista wartości, np.</span><span class="sxs-lookup"><span data-stu-id="74473-266">This is a comma separated list of values, ex.</span></span> <span data-ttu-id="74473-267">"nodev, nosuid".</span><span class="sxs-lookup"><span data-stu-id="74473-267">'nodev,nosuid'.</span></span> <span data-ttu-id="74473-268">Zobacz mount(8), aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="74473-268">See mount(8) for details.</span></span>

<span data-ttu-id="74473-269">**ResourceDisk.EnableSwap:**</span><span class="sxs-lookup"><span data-stu-id="74473-269">**ResourceDisk.EnableSwap:**</span></span>  
<span data-ttu-id="74473-270">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="74473-270">Type: Boolean</span></span>  
<span data-ttu-id="74473-271">Domyślne: n</span><span class="sxs-lookup"><span data-stu-id="74473-271">Default: n</span></span>

<span data-ttu-id="74473-272">Jeśli ustawiona, plik wymiany (/ swapfile) jest tworzony na powitania zasobu dysku i dodać obszar wymiany toohello systemu.</span><span class="sxs-lookup"><span data-stu-id="74473-272">If set, a swap file (/swapfile) is created on hello resource disk and added toohello system swap space.</span></span>

<span data-ttu-id="74473-273">**ResourceDisk.SwapSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="74473-273">**ResourceDisk.SwapSizeMB:**</span></span>  
<span data-ttu-id="74473-274">Typ: liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="74473-274">Type: Integer</span></span>  
<span data-ttu-id="74473-275">Domyślna: 0</span><span class="sxs-lookup"><span data-stu-id="74473-275">Default: 0</span></span>

<span data-ttu-id="74473-276">rozmiar Hello hello pliku wymiany w megabajtach.</span><span class="sxs-lookup"><span data-stu-id="74473-276">hello size of hello swap file in megabytes.</span></span>

<span data-ttu-id="74473-277">**Logs.Verbose:**</span><span class="sxs-lookup"><span data-stu-id="74473-277">**Logs.Verbose:**</span></span>  
<span data-ttu-id="74473-278">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="74473-278">Type: Boolean</span></span>  
<span data-ttu-id="74473-279">Domyślne: n</span><span class="sxs-lookup"><span data-stu-id="74473-279">Default: n</span></span>

<span data-ttu-id="74473-280">Jeśli jest boosted zestawu, szczegółowości dziennika.</span><span class="sxs-lookup"><span data-stu-id="74473-280">If set, log verbosity is boosted.</span></span> <span data-ttu-id="74473-281">Agenta Waagent dzienniki too/var/log/waagent.log i wykorzystuje hello systemu logrotate funkcji toorotate dzienniki.</span><span class="sxs-lookup"><span data-stu-id="74473-281">Waagent logs too/var/log/waagent.log and leverages hello system logrotate functionality toorotate logs.</span></span>

<span data-ttu-id="74473-282">**SYSTEM OPERACYJNY. EnableRDMA**</span><span class="sxs-lookup"><span data-stu-id="74473-282">**OS.EnableRDMA**</span></span>  
<span data-ttu-id="74473-283">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="74473-283">Type: Boolean</span></span>  
<span data-ttu-id="74473-284">Domyślne: n</span><span class="sxs-lookup"><span data-stu-id="74473-284">Default: n</span></span>

<span data-ttu-id="74473-285">Jeśli ustawiona, hello agent będą podejmować tooinstall, a następnie załadować sterownik jądra RDMA, odpowiadający hello wersji oprogramowania układowego hello na powitania podstawowy sprzęt.</span><span class="sxs-lookup"><span data-stu-id="74473-285">If set, hello agent will attempt tooinstall and then load an RDMA kernel driver that matches hello version of hello firmware on hello underlying hardware.</span></span>

<span data-ttu-id="74473-286">**SYSTEM OPERACYJNY. RootDeviceScsiTimeout:**</span><span class="sxs-lookup"><span data-stu-id="74473-286">**OS.RootDeviceScsiTimeout:**</span></span>  
<span data-ttu-id="74473-287">Typ: liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="74473-287">Type: Integer</span></span>  
<span data-ttu-id="74473-288">Domyślne: 300</span><span class="sxs-lookup"><span data-stu-id="74473-288">Default: 300</span></span>

<span data-ttu-id="74473-289">Spowoduje to skonfigurowanie hello SCSI przekroczenia limitu czasu w sekundach na dyskach dysku i danych hello systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="74473-289">This configures hello SCSI timeout in seconds on hello OS disk and data drives.</span></span> <span data-ttu-id="74473-290">Jeśli nie jest ustawiona, system hello, które będą używane wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="74473-290">If not set, hello system defaults are used.</span></span>

<span data-ttu-id="74473-291">**SYSTEM OPERACYJNY. OpensslPath:**</span><span class="sxs-lookup"><span data-stu-id="74473-291">**OS.OpensslPath:**</span></span>  
<span data-ttu-id="74473-292">Typ: ciąg</span><span class="sxs-lookup"><span data-stu-id="74473-292">Type: String</span></span>  
<span data-ttu-id="74473-293">Domyślnie: Brak</span><span class="sxs-lookup"><span data-stu-id="74473-293">Default: None</span></span>

<span data-ttu-id="74473-294">Może to być toospecify używane ścieżki alternatywnej dla hello toouse binarnych biblioteki openssl dla operacji kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="74473-294">This can be used toospecify an alternate path for hello openssl binary toouse for cryptographic operations.</span></span>

<span data-ttu-id="74473-295">**HttpProxy.Host, HttpProxy.Port**</span><span class="sxs-lookup"><span data-stu-id="74473-295">**HttpProxy.Host, HttpProxy.Port**</span></span>  
<span data-ttu-id="74473-296">Typ: ciąg</span><span class="sxs-lookup"><span data-stu-id="74473-296">Type: String</span></span>  
<span data-ttu-id="74473-297">Domyślnie: Brak</span><span class="sxs-lookup"><span data-stu-id="74473-297">Default: None</span></span>

<span data-ttu-id="74473-298">Jeśli ustawiona, hello agent użyje tego serwera proxy internet hello tooaccess serwera.</span><span class="sxs-lookup"><span data-stu-id="74473-298">If set, hello agent will use this proxy server tooaccess hello internet.</span></span> 

## <a name="ubuntu-cloud-images"></a><span data-ttu-id="74473-299">Obrazy Ubuntu chmury</span><span class="sxs-lookup"><span data-stu-id="74473-299">Ubuntu Cloud Images</span></span>
<span data-ttu-id="74473-300">Należy pamiętać, że korzystanie z obrazów chmury Ubuntu [init chmury](https://launchpad.net/ubuntu/+source/cloud-init) tooperform wiele zadań konfiguracyjnych, które w przeciwnym razie mogłyby być zarządzane przez hello agenta systemu Linux platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="74473-300">Note that Ubuntu Cloud Images utilize [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform many configuration tasks that would otherwise be managed by hello Azure Linux Agent.</span></span>  <span data-ttu-id="74473-301">Należy pamiętać, hello następujące różnice:</span><span class="sxs-lookup"><span data-stu-id="74473-301">Please note hello following differences:</span></span>

* <span data-ttu-id="74473-302">**Provisioning.Enabled** zbyt "n" na obrazów chmury Ubuntu tooperform chmury inicjowania obsługi zadań Użyj ustawień domyślnych.</span><span class="sxs-lookup"><span data-stu-id="74473-302">**Provisioning.Enabled** defaults too"n" on Ubuntu Cloud Images that use cloud-init tooperform provisioning tasks.</span></span>
* <span data-ttu-id="74473-303">Witaj następujące parametry konfiguracji nie mają wpływu na obrazy chmury Ubuntu, używanego init chmury toomanage hello zasobów dysku i zamiany miejsca:</span><span class="sxs-lookup"><span data-stu-id="74473-303">hello following configuration parameters have no effect on Ubuntu Cloud Images that use cloud-init toomanage hello resource disk and swap space:</span></span>
  
  * <span data-ttu-id="74473-304">**ResourceDisk.Format**</span><span class="sxs-lookup"><span data-stu-id="74473-304">**ResourceDisk.Format**</span></span>
  * <span data-ttu-id="74473-305">**ResourceDisk.Filesystem**</span><span class="sxs-lookup"><span data-stu-id="74473-305">**ResourceDisk.Filesystem**</span></span>
  * <span data-ttu-id="74473-306">**ResourceDisk.MountPoint**</span><span class="sxs-lookup"><span data-stu-id="74473-306">**ResourceDisk.MountPoint**</span></span>
  * <span data-ttu-id="74473-307">**ResourceDisk.EnableSwap**</span><span class="sxs-lookup"><span data-stu-id="74473-307">**ResourceDisk.EnableSwap**</span></span>
  * <span data-ttu-id="74473-308">**ResourceDisk.SwapSizeMB**</span><span class="sxs-lookup"><span data-stu-id="74473-308">**ResourceDisk.SwapSizeMB**</span></span>
* <span data-ttu-id="74473-309">Zobacz hello następującego punktu instalacji zasobów tooconfigure hello zasobów dysku i Zamień miejsce na obrazy chmury Ubuntu podczas inicjowania obsługi:</span><span class="sxs-lookup"><span data-stu-id="74473-309">Please see hello following resources tooconfigure hello resource disk mount point and swap space on Ubuntu Cloud Images during provisioning:</span></span>
  
  * [<span data-ttu-id="74473-310">Ubuntu Witryna typu Wiki: Konfigurowanie partycji wymiany</span><span class="sxs-lookup"><span data-stu-id="74473-310">Ubuntu Wiki: Configure Swap Partitions</span></span>](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [<span data-ttu-id="74473-311">Wstrzykiwania niestandardowe dane do maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="74473-311">Injecting Custom Data into an Azure Virtual Machine</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

