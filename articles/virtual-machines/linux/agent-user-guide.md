---
title: "Omówienie agenta maszyny Wirtualnej systemu Linux platformy Azure | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie instalowania i konfigurowania agenta systemu Linux (agenta waagent) do zarządzania na komputerze wirtualnym interakcji z kontrolerem sieci szkieletowej Azure."
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
ms.openlocfilehash: 486ad6bb148583a957fb82b7954ff94f853b12cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="understanding-and-using-the-azure-linux-agent"></a><span data-ttu-id="a85a5-103">Opis i przy użyciu agenta systemu Linux platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a85a5-103">Understanding and using the Azure Linux Agent</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a><span data-ttu-id="a85a5-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="a85a5-104">Introduction</span></span>
<span data-ttu-id="a85a5-105">Agent systemu Linux usługi Microsoft Azure (agenta waagent) zarządza systemu Linux i FreeBSD inicjowania obsługi administracyjnej i maszyny Wirtualnej interakcji z kontrolera sieci szkieletowej Azure.</span><span class="sxs-lookup"><span data-stu-id="a85a5-105">The Microsoft Azure Linux Agent (waagent) manages Linux & FreeBSD provisioning, and VM interaction with the Azure Fabric Controller.</span></span> <span data-ttu-id="a85a5-106">Udostępnia ona następujące funkcje dla systemów Linux i FreeBSD IaaS wdrożenia:</span><span class="sxs-lookup"><span data-stu-id="a85a5-106">It provides the following functionality for Linux and FreeBSD IaaS deployments:</span></span>

> [!NOTE]
> <span data-ttu-id="a85a5-107">Zobacz agenta systemu Linux Azure [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) dodatkowe szczegóły.</span><span class="sxs-lookup"><span data-stu-id="a85a5-107">See the Azure Linux agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) for additional details.</span></span>
> 
> 

* <span data-ttu-id="a85a5-108">**Inicjowanie obsługi obrazu**</span><span class="sxs-lookup"><span data-stu-id="a85a5-108">**Image Provisioning**</span></span>
  
  * <span data-ttu-id="a85a5-109">Tworzenie konta użytkownika</span><span class="sxs-lookup"><span data-stu-id="a85a5-109">Creation of a user account</span></span>
  * <span data-ttu-id="a85a5-110">Konfigurowanie typów uwierzytelniania SSH</span><span class="sxs-lookup"><span data-stu-id="a85a5-110">Configuring SSH authentication types</span></span>
  * <span data-ttu-id="a85a5-111">Wdrożenie par kluczy i kluczy publicznych SSH</span><span class="sxs-lookup"><span data-stu-id="a85a5-111">Deployment of SSH public keys and key pairs</span></span>
  * <span data-ttu-id="a85a5-112">Ustawienie nazwy hosta</span><span class="sxs-lookup"><span data-stu-id="a85a5-112">Setting the host name</span></span>
  * <span data-ttu-id="a85a5-113">Publikowanie nazwy hosta DNS platformy</span><span class="sxs-lookup"><span data-stu-id="a85a5-113">Publishing the host name to the platform DNS</span></span>
  * <span data-ttu-id="a85a5-114">Raportowanie odcisku klucza SSH hosta do platformy</span><span class="sxs-lookup"><span data-stu-id="a85a5-114">Reporting SSH host key fingerprint to the platform</span></span>
  * <span data-ttu-id="a85a5-115">Zarządzanie zasobami dysku</span><span class="sxs-lookup"><span data-stu-id="a85a5-115">Resource Disk Management</span></span>
  * <span data-ttu-id="a85a5-116">Formatowanie i Instalowanie zasobu dysku</span><span class="sxs-lookup"><span data-stu-id="a85a5-116">Formatting and mounting the resource disk</span></span>
  * <span data-ttu-id="a85a5-117">Konfigurowanie obszaru wymiany</span><span class="sxs-lookup"><span data-stu-id="a85a5-117">Configuring swap space</span></span>
* <span data-ttu-id="a85a5-118">**Sieć**</span><span class="sxs-lookup"><span data-stu-id="a85a5-118">**Networking**</span></span>
  
  * <span data-ttu-id="a85a5-119">Zarządza trasy, aby zwiększyć zgodność z serwerów DHCP platformy</span><span class="sxs-lookup"><span data-stu-id="a85a5-119">Manages routes to improve compatibility with platform DHCP servers</span></span>
  * <span data-ttu-id="a85a5-120">Zapewnia stabilność Nazwa interfejsu sieciowego</span><span class="sxs-lookup"><span data-stu-id="a85a5-120">Ensures the stability of the network interface name</span></span>
* <span data-ttu-id="a85a5-121">**Jądra**</span><span class="sxs-lookup"><span data-stu-id="a85a5-121">**Kernel**</span></span>
  
  * <span data-ttu-id="a85a5-122">Konfiguruje wirtualną architekturę NUMA (Wyłącz dla jądra < 2.6.37)</span><span class="sxs-lookup"><span data-stu-id="a85a5-122">Configures virtual NUMA (disable for kernel <2.6.37)</span></span>
  * <span data-ttu-id="a85a5-123">Wykorzystuje entropii funkcji Hyper-V dla /dev/random</span><span class="sxs-lookup"><span data-stu-id="a85a5-123">Consumes Hyper-V entropy for /dev/random</span></span>
  * <span data-ttu-id="a85a5-124">Konfiguruje SCSI przekroczeń limitu czasu dla urządzenia katalogu głównego (który może być zdalne)</span><span class="sxs-lookup"><span data-stu-id="a85a5-124">Configures SCSI timeouts for the root device (which could be remote)</span></span>
* <span data-ttu-id="a85a5-125">**Diagnostyka**</span><span class="sxs-lookup"><span data-stu-id="a85a5-125">**Diagnostics**</span></span>
  
  * <span data-ttu-id="a85a5-126">Przekierowywanie konsoli do portu szeregowego</span><span class="sxs-lookup"><span data-stu-id="a85a5-126">Console redirection to the serial port</span></span>
* <span data-ttu-id="a85a5-127">**Wdrożenia programu SCVMM**</span><span class="sxs-lookup"><span data-stu-id="a85a5-127">**SCVMM Deployments**</span></span>
  
  * <span data-ttu-id="a85a5-128">Wykrywa i używa do ładowania agenta programu VMM dla systemu Linux podczas uruchamiania w środowisku programu System Center Virtual Machine Manager 2012 R2</span><span class="sxs-lookup"><span data-stu-id="a85a5-128">Detects and bootstraps the VMM agent for Linux when running in a System Center Virtual Machine Manager 2012 R2 environment</span></span>
* <span data-ttu-id="a85a5-129">**Rozszerzenia maszyny Wirtualnej**</span><span class="sxs-lookup"><span data-stu-id="a85a5-129">**VM Extension**</span></span>
  
  * <span data-ttu-id="a85a5-130">Wstaw składnik utworzone przez firmę Microsoft i partnerów do maszyny Wirtualnej systemu Linux (IaaS) umożliwiające oprogramowania i konfiguracji automatyzacji</span><span class="sxs-lookup"><span data-stu-id="a85a5-130">Inject component authored by Microsoft and Partners into Linux VM (IaaS) to enable software and configuration automation</span></span>
  * <span data-ttu-id="a85a5-131">Implementacja odwołanie rozszerzenia maszyny Wirtualnej na [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span><span class="sxs-lookup"><span data-stu-id="a85a5-131">VM Extension reference implementation on [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span></span>

## <a name="communication"></a><span data-ttu-id="a85a5-132">Komunikacja</span><span class="sxs-lookup"><span data-stu-id="a85a5-132">Communication</span></span>
<span data-ttu-id="a85a5-133">Przepływ informacji od platformy do agenta odbywa się za pośrednictwem dwóch kanałów:</span><span class="sxs-lookup"><span data-stu-id="a85a5-133">The information flow from the platform to the agent occurs via two channels:</span></span>

* <span data-ttu-id="a85a5-134">Czas rozruchu dołączonych dysków DVD do wdrożenia IaaS.</span><span class="sxs-lookup"><span data-stu-id="a85a5-134">A boot-time attached DVD for IaaS deployments.</span></span> <span data-ttu-id="a85a5-135">Ten dysk DVD zawiera zgodne OVF pliku konfiguracji, który zawiera wszystkie informacje o udostępnianiu niż rzeczywista keypairs SSH.</span><span class="sxs-lookup"><span data-stu-id="a85a5-135">This DVD includes an OVF-compliant configuration file that includes all provisioning information other than the actual SSH keypairs.</span></span>
* <span data-ttu-id="a85a5-136">Punkt końcowy protokołu TCP udostępnianie interfejsu API REST używany do uzyskania wdrażanie i Konfigurowanie topologii.</span><span class="sxs-lookup"><span data-stu-id="a85a5-136">A TCP endpoint exposing a REST API used to obtain deployment and topology configuration.</span></span>

## <a name="requirements"></a><span data-ttu-id="a85a5-137">Wymagania</span><span class="sxs-lookup"><span data-stu-id="a85a5-137">Requirements</span></span>
<span data-ttu-id="a85a5-138">Poniższe systemy zostały przetestowane i są znane, aby pracować z agenta systemu Linux platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="a85a5-138">The following systems have been tested and are known to work with the Azure Linux Agent:</span></span>

> [!NOTE]
> <span data-ttu-id="a85a5-139">Ta lista może się różnić od oficjalnego listę obsługiwanych systemów na platformie Microsoft Azure, zgodnie z opisem w tym miejscu: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span><span class="sxs-lookup"><span data-stu-id="a85a5-139">This list may differ from the official list of supported systems on the Microsoft Azure Platform, as described here: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span></span>
> 
> 

* <span data-ttu-id="a85a5-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="a85a5-140">CoreOS</span></span>
* <span data-ttu-id="a85a5-141">CentOS 6.3 +</span><span class="sxs-lookup"><span data-stu-id="a85a5-141">CentOS 6.3+</span></span>
* <span data-ttu-id="a85a5-142">Red Hat Enterprise Linux 6.7 +</span><span class="sxs-lookup"><span data-stu-id="a85a5-142">Red Hat Enterprise Linux 6.7+</span></span>
* <span data-ttu-id="a85a5-143">Debian 7.0 +</span><span class="sxs-lookup"><span data-stu-id="a85a5-143">Debian 7.0+</span></span>
* <span data-ttu-id="a85a5-144">Ubuntu 12.04 +</span><span class="sxs-lookup"><span data-stu-id="a85a5-144">Ubuntu 12.04+</span></span>
* <span data-ttu-id="a85a5-145">openSUSE 12.3 +</span><span class="sxs-lookup"><span data-stu-id="a85a5-145">openSUSE 12.3+</span></span>
* <span data-ttu-id="a85a5-146">SLES 11 Z DODATKIEM SP3 +</span><span class="sxs-lookup"><span data-stu-id="a85a5-146">SLES 11 SP3+</span></span>
* <span data-ttu-id="a85a5-147">Oracle Linux 6.4 +</span><span class="sxs-lookup"><span data-stu-id="a85a5-147">Oracle Linux 6.4+</span></span>

<span data-ttu-id="a85a5-148">Inne obsługiwane systemy:</span><span class="sxs-lookup"><span data-stu-id="a85a5-148">Other Supported Systems:</span></span>

* <span data-ttu-id="a85a5-149">FreeBSD 10 + (Azure agenta systemu Linux v2.0.10 +)</span><span class="sxs-lookup"><span data-stu-id="a85a5-149">FreeBSD 10+ (Azure Linux Agent v2.0.10+)</span></span>

<span data-ttu-id="a85a5-150">Agent systemu Linux jest zależna od niektórych pakietów systemu prawidłowego działania:</span><span class="sxs-lookup"><span data-stu-id="a85a5-150">The Linux agent depends on some system packages in order to function properly:</span></span>

* <span data-ttu-id="a85a5-151">Python 2.6 +</span><span class="sxs-lookup"><span data-stu-id="a85a5-151">Python 2.6+</span></span>
* <span data-ttu-id="a85a5-152">Biblioteki OpenSSL 1.0 +</span><span class="sxs-lookup"><span data-stu-id="a85a5-152">OpenSSL 1.0+</span></span>
* <span data-ttu-id="a85a5-153">OpenSSH 5.3 +</span><span class="sxs-lookup"><span data-stu-id="a85a5-153">OpenSSH 5.3+</span></span>
* <span data-ttu-id="a85a5-154">Narzędzia systemu plików: ulec sfdisk fdisk, mkfs,</span><span class="sxs-lookup"><span data-stu-id="a85a5-154">Filesystem utilities: sfdisk, fdisk, mkfs, parted</span></span>
* <span data-ttu-id="a85a5-155">Narzędzia hasło: chpasswd, sudo</span><span class="sxs-lookup"><span data-stu-id="a85a5-155">Password tools: chpasswd, sudo</span></span>
* <span data-ttu-id="a85a5-156">Narzędzia do edycji tekstu: mniejszyć, grep</span><span class="sxs-lookup"><span data-stu-id="a85a5-156">Text processing tools: sed, grep</span></span>
* <span data-ttu-id="a85a5-157">Narzędzia sieci: trasy ip</span><span class="sxs-lookup"><span data-stu-id="a85a5-157">Network tools: ip-route</span></span>
* <span data-ttu-id="a85a5-158">Obsługuje jądra służący do instalowania funkcji zdefiniowanej przez użytkownika, systemy plików.</span><span class="sxs-lookup"><span data-stu-id="a85a5-158">Kernel support for mounting UDF filesystems.</span></span>

## <a name="installation"></a><span data-ttu-id="a85a5-159">Instalacja</span><span class="sxs-lookup"><span data-stu-id="a85a5-159">Installation</span></span>
<span data-ttu-id="a85a5-160">Instalacja przy użyciu obr. / min lub pakietu DEB z repozytorium pakietów z dystrybucji jest preferowaną metodą instalacji i uaktualniania agenta systemu Linux platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a85a5-160">Installation using an RPM or a DEB package from your distribution's package repository is the preferred method of installing and upgrading the Azure Linux Agent.</span></span> <span data-ttu-id="a85a5-161">Wszystkie [zatwierdzone dostawców dystrybucji](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integracji pakiet agenta systemu Linux platformy Azure z repozytoriami i obrazów.</span><span class="sxs-lookup"><span data-stu-id="a85a5-161">All the [endorsed distribution providers](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrate the Azure Linux agent package into their images and repositories.</span></span>

<span data-ttu-id="a85a5-162">Zapoznaj się z dokumentacją w [repozytorium agenta systemu Linux platformy Azure w serwisie GitHub](https://github.com/Azure/WALinuxAgent) dla zaawansowane opcje instalacji, takich jak instalowanie ze źródła lub niestandardowe lokalizacje lub prefiksów.</span><span class="sxs-lookup"><span data-stu-id="a85a5-162">Refer to the documentation in the [Azure Linux Agent repo on GitHub](https://github.com/Azure/WALinuxAgent) for advanced installation options, such as installing from source or to custom locations or prefixes.</span></span>

## <a name="command-line-options"></a><span data-ttu-id="a85a5-163">Opcje wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="a85a5-163">Command Line Options</span></span>
### <a name="flags"></a><span data-ttu-id="a85a5-164">Flagi</span><span class="sxs-lookup"><span data-stu-id="a85a5-164">Flags</span></span>
* <span data-ttu-id="a85a5-165">verbose: Zwiększ poziom szczegółowości określonego polecenia</span><span class="sxs-lookup"><span data-stu-id="a85a5-165">verbose: Increase verbosity of specified command</span></span>
* <span data-ttu-id="a85a5-166">Wymuś: Pomiń interakcyjne potwierdzenie dla niektórych poleceń</span><span class="sxs-lookup"><span data-stu-id="a85a5-166">force: Skip interactive confirmation for some commands</span></span>

### <a name="commands"></a><span data-ttu-id="a85a5-167">Polecenia</span><span class="sxs-lookup"><span data-stu-id="a85a5-167">Commands</span></span>
* <span data-ttu-id="a85a5-168">Pomoc: Wyświetla listę obsługiwanych poleceń i flagi.</span><span class="sxs-lookup"><span data-stu-id="a85a5-168">help: Lists the supported commands and flags.</span></span>
* <span data-ttu-id="a85a5-169">deprovision: próba oczyszczeniu systemu i zapewnić ich nadające się do ponownego inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="a85a5-169">deprovision: Attempt to clean the system and make it suitable for re-provisioning.</span></span> <span data-ttu-id="a85a5-170">Ta operacja usunięte następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a85a5-170">This operation deleted the following:</span></span>
  
  * <span data-ttu-id="a85a5-171">Wszystkie klucze hosta SSH (jeśli Provisioning.RegenerateSshHostKeyPair "y" w pliku konfiguracji)</span><span class="sxs-lookup"><span data-stu-id="a85a5-171">All SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in the configuration file)</span></span>
  * <span data-ttu-id="a85a5-172">Konfiguracja serwera nazw w /etc/resolv.conf</span><span class="sxs-lookup"><span data-stu-id="a85a5-172">Nameserver configuration in /etc/resolv.conf</span></span>
  * <span data-ttu-id="a85a5-173">Hasła głównego z /etc/shadow (jeśli Provisioning.DeleteRootPassword "y" w pliku konfiguracji)</span><span class="sxs-lookup"><span data-stu-id="a85a5-173">Root password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in the configuration file)</span></span>
  * <span data-ttu-id="a85a5-174">Buforowane dzierżawy klientów DHCP</span><span class="sxs-lookup"><span data-stu-id="a85a5-174">Cached DHCP client leases</span></span>
  * <span data-ttu-id="a85a5-175">Zresetowanie nazwy hosta na wartość localhost.localdomain</span><span class="sxs-lookup"><span data-stu-id="a85a5-175">Resets host name to localhost.localdomain</span></span>

> [!WARNING]
> <span data-ttu-id="a85a5-176">Cofanie zastrzegania nie gwarantuje, że obraz jest wyczyszczone wszystkie informacje poufne i nadaje się do ponownej dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="a85a5-176">Deprovisioning does not guarantee that the image is cleared of all sensitive information and suitable for redistribution.</span></span>
> 
> 

* <span data-ttu-id="a85a5-177">deprovision + użytkownika: wykonuje wszystkie elementy w obszarze - deprovision (powyżej) i również usuwa ostatnie konto użytkownika elastycznie (uzyskane z /var/lib/waagent) i skojarzone dane.</span><span class="sxs-lookup"><span data-stu-id="a85a5-177">deprovision+user: Performs everything under -deprovision (above) and also deletes the last provisioned user account (obtained from /var/lib/waagent) and associated data.</span></span> <span data-ttu-id="a85a5-178">Ten parametr jest podczas usuwania inicjowania obsługi administracyjnej z obrazem, który został wcześniej inicjowania obsługi administracyjnej na platformie Azure, mogą być przechwytywane i ponownego użycia.</span><span class="sxs-lookup"><span data-stu-id="a85a5-178">This parameter is when de-provisioning an image that was previously provisioning on Azure so it may be captured and re-used.</span></span>
* <span data-ttu-id="a85a5-179">Wersja: Wyświetla wersję agenta waagent</span><span class="sxs-lookup"><span data-stu-id="a85a5-179">version: Displays the version of waagent</span></span>
* <span data-ttu-id="a85a5-180">serialconsole: konfiguruje CHODNIKÓW, aby oznaczyć ttyS0 (pierwszy port szeregowy) jako konsoli rozruchu.</span><span class="sxs-lookup"><span data-stu-id="a85a5-180">serialconsole: Configures GRUB to mark ttyS0 (the first serial port) as the boot console.</span></span> <span data-ttu-id="a85a5-181">Dzięki temu, że jądra rozruchu dzienniki są wysyłane do portu szeregowego i udostępnione do debugowania.</span><span class="sxs-lookup"><span data-stu-id="a85a5-181">This ensures that kernel bootup logs are sent to the serial port and made available for debugging.</span></span>
* <span data-ttu-id="a85a5-182">demon: uruchomiono agenta waagent jako demon do interakcji z platformą zarządzania.</span><span class="sxs-lookup"><span data-stu-id="a85a5-182">daemon: Run waagent as a daemon to manage interaction with the platform.</span></span> <span data-ttu-id="a85a5-183">Ten argument zostanie określony do agenta waagent w skrypcie inicjowania agenta waagent.</span><span class="sxs-lookup"><span data-stu-id="a85a5-183">This argument is specified to waagent in the waagent init script.</span></span>
* <span data-ttu-id="a85a5-184">Rozpocznij: uruchomiono agenta waagent jako proces w tle</span><span class="sxs-lookup"><span data-stu-id="a85a5-184">start: Run waagent as a background process</span></span>

## <a name="configuration"></a><span data-ttu-id="a85a5-185">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="a85a5-185">Configuration</span></span>
<span data-ttu-id="a85a5-186">Plik konfiguracji (/ etc/waagent.conf) steruje agenta waagent akcje.</span><span class="sxs-lookup"><span data-stu-id="a85a5-186">A configuration file (/etc/waagent.conf) controls the actions of waagent.</span></span> <span data-ttu-id="a85a5-187">Poniżej przedstawiono przykładowy plik konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="a85a5-187">A sample configuration file is shown below:</span></span>

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

<span data-ttu-id="a85a5-188">Różne opcje konfiguracji opisano szczegółowo poniżej.</span><span class="sxs-lookup"><span data-stu-id="a85a5-188">The various configuration options are described in detail below.</span></span> <span data-ttu-id="a85a5-189">Opcje konfiguracji są trzy typy; Wartość logiczna, String lub Integer.</span><span class="sxs-lookup"><span data-stu-id="a85a5-189">Configuration options are of three types; Boolean, String or Integer.</span></span> <span data-ttu-id="a85a5-190">Opcje konfiguracji logicznych można określić jako "y" lub "n".</span><span class="sxs-lookup"><span data-stu-id="a85a5-190">The Boolean configuration options can be specified as "y" or "n".</span></span> <span data-ttu-id="a85a5-191">Specjalne słowo kluczowe "None" mogą być używane w przypadku niektórych ciąg typu konfiguracji wpisów zgodnie z opisem poniżej.</span><span class="sxs-lookup"><span data-stu-id="a85a5-191">The special keyword "None" may be used for some string type configuration entries as detailed below.</span></span>

<span data-ttu-id="a85a5-192">**Provisioning.Enabled:**</span><span class="sxs-lookup"><span data-stu-id="a85a5-192">**Provisioning.Enabled:**</span></span>  
<span data-ttu-id="a85a5-193">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="a85a5-193">Type: Boolean</span></span>  
<span data-ttu-id="a85a5-194">Domyślne: y</span><span class="sxs-lookup"><span data-stu-id="a85a5-194">Default: y</span></span>

<span data-ttu-id="a85a5-195">Dzięki temu użytkownik włączyć lub wyłączyć funkcję inicjowania obsługi administracyjnej w agencie.</span><span class="sxs-lookup"><span data-stu-id="a85a5-195">This allows the user to enable or disable the provisioning functionality in the agent.</span></span> <span data-ttu-id="a85a5-196">Prawidłowe wartości to "y" lub "n".</span><span class="sxs-lookup"><span data-stu-id="a85a5-196">Valid values are "y" or "n".</span></span> <span data-ttu-id="a85a5-197">Jeśli Inicjowanie obsługi administracyjnej jest wyłączone, hosta i użytkownika kluczy SSH w obrazie zostaną zachowane i określona na platformie Azure, inicjowanie obsługi interfejsu API konfiguracja jest ignorowana.</span><span class="sxs-lookup"><span data-stu-id="a85a5-197">If provisioning is disabled, SSH host and user keys in the image are preserved and any configuration specified in the Azure provisioning API is ignored.</span></span>

> [!NOTE]
> <span data-ttu-id="a85a5-198">`Provisioning.Enabled` Jest domyślnie "n" na Ubuntu chmury obrazów użyj init chmury w celu obsługi.</span><span class="sxs-lookup"><span data-stu-id="a85a5-198">The `Provisioning.Enabled` parameter defaults to "n" on Ubuntu Cloud Images that use cloud-init for provisioning.</span></span>
> 
> 

<span data-ttu-id="a85a5-199">**Provisioning.DeleteRootPassword:**</span><span class="sxs-lookup"><span data-stu-id="a85a5-199">**Provisioning.DeleteRootPassword:**</span></span>  
<span data-ttu-id="a85a5-200">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="a85a5-200">Type: Boolean</span></span>  
<span data-ttu-id="a85a5-201">Domyślne: n</span><span class="sxs-lookup"><span data-stu-id="a85a5-201">Default: n</span></span>

<span data-ttu-id="a85a5-202">Jeśli podczas procesu inicjowania obsługi administracyjnej jest usuwane zestawu, w pliku/etc/tle hasła głównego.</span><span class="sxs-lookup"><span data-stu-id="a85a5-202">If set, the root password in the /etc/shadow file is erased during the provisioning process.</span></span>

<span data-ttu-id="a85a5-203">**Provisioning.RegenerateSshHostKeyPair:**</span><span class="sxs-lookup"><span data-stu-id="a85a5-203">**Provisioning.RegenerateSshHostKeyPair:**</span></span>  
<span data-ttu-id="a85a5-204">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="a85a5-204">Type: Boolean</span></span>  
<span data-ttu-id="a85a5-205">Domyślne: y</span><span class="sxs-lookup"><span data-stu-id="a85a5-205">Default: y</span></span>

<span data-ttu-id="a85a5-206">Jeśli zestawu i wszystkich hostów par kluczy SSH (ecdsa, dsa i rsa) zostaną usunięte podczas procesu inicjowania obsługi administracyjnej z/etc/ssh /.</span><span class="sxs-lookup"><span data-stu-id="a85a5-206">If set, all SSH host key pairs (ecdsa, dsa and rsa) are deleted during the provisioning process from /etc/ssh/.</span></span> <span data-ttu-id="a85a5-207">I generowany jest jeden świeże pary kluczy.</span><span class="sxs-lookup"><span data-stu-id="a85a5-207">And a single fresh key pair is generated.</span></span>

<span data-ttu-id="a85a5-208">Można skonfigurować we wpisie Provisioning.SshHostKeyPairType jest typ szyfrowania dla świeże pary kluczy.</span><span class="sxs-lookup"><span data-stu-id="a85a5-208">The encryption type for the fresh key pair is configurable by the Provisioning.SshHostKeyPairType entry.</span></span> <span data-ttu-id="a85a5-209">Należy pamiętać, że niektóre dystrybucje zostaną ponownie utworzone par kluczy SSH dla wszystkich Brak typów szyfrowania, podczas ponownego uruchamiania demona SSH (na przykład po ponownym rozruchu).</span><span class="sxs-lookup"><span data-stu-id="a85a5-209">Please note that some distributions will re-create SSH key pairs for any missing encryption types when the SSH daemon is restarted (for example, upon a reboot).</span></span>

<span data-ttu-id="a85a5-210">**Provisioning.SshHostKeyPairType:**</span><span class="sxs-lookup"><span data-stu-id="a85a5-210">**Provisioning.SshHostKeyPairType:**</span></span>  
<span data-ttu-id="a85a5-211">Typ: ciąg</span><span class="sxs-lookup"><span data-stu-id="a85a5-211">Type: String</span></span>  
<span data-ttu-id="a85a5-212">Domyślne: rsa</span><span class="sxs-lookup"><span data-stu-id="a85a5-212">Default: rsa</span></span>

<span data-ttu-id="a85a5-213">To może należeć do typu algorytmu szyfrowania, który jest obsługiwany przez demon SSH na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a85a5-213">This can be set to an encryption algorithm type that is supported by the SSH daemon on the virtual machine.</span></span> <span data-ttu-id="a85a5-214">Zazwyczaj obsługiwane wartości to "rsa", "dsa" i "ecdsa".</span><span class="sxs-lookup"><span data-stu-id="a85a5-214">The typically supported values are "rsa", "dsa" and "ecdsa".</span></span> <span data-ttu-id="a85a5-215">Należy pamiętać, że "putty.exe" w systemie Windows nie obsługuje "ecdsa".</span><span class="sxs-lookup"><span data-stu-id="a85a5-215">Note that "putty.exe" on Windows does not support "ecdsa".</span></span> <span data-ttu-id="a85a5-216">Tak Jeśli zamierzasz używać putty.exe w systemie Windows do nawiązania połączenia wdrożenia systemu Linux, użyj "rsa" lub "dsa".</span><span class="sxs-lookup"><span data-stu-id="a85a5-216">So, if you intend to use putty.exe on Windows to connect to a Linux deployment, please use "rsa" or "dsa".</span></span>

<span data-ttu-id="a85a5-217">**Provisioning.MonitorHostName:**</span><span class="sxs-lookup"><span data-stu-id="a85a5-217">**Provisioning.MonitorHostName:**</span></span>  
<span data-ttu-id="a85a5-218">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="a85a5-218">Type: Boolean</span></span>  
<span data-ttu-id="a85a5-219">Domyślne: y</span><span class="sxs-lookup"><span data-stu-id="a85a5-219">Default: y</span></span>

<span data-ttu-id="a85a5-220">Jeśli ustawiona, agenta waagent monitorujący maszyny wirtualnej systemu Linux zmiany nazwy hosta (jak zwracany przez polecenie "Nazwa hosta") i automatycznie zaktualizować konfiguracji sieci w obrazie w celu odzwierciedlenia zmian.</span><span class="sxs-lookup"><span data-stu-id="a85a5-220">If set, waagent will monitor the Linux virtual machine for hostname changes (as returned by the "hostname" command) and automatically update the networking configuration in the image to reflect the change.</span></span> <span data-ttu-id="a85a5-221">Aby wypchnąć zmiany nazwy do serwerów DNS, sieci zostanie ponownie uruchomiony na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a85a5-221">In order to push the name change to the DNS servers, networking will be restarted in the virtual machine.</span></span> <span data-ttu-id="a85a5-222">Spowoduje to w skrócie utratę łączności z Internetem.</span><span class="sxs-lookup"><span data-stu-id="a85a5-222">This will result in brief loss of Internet connectivity.</span></span>

<span data-ttu-id="a85a5-223">**Provisioning.DecodeCustomData**</span><span class="sxs-lookup"><span data-stu-id="a85a5-223">**Provisioning.DecodeCustomData**</span></span>  
<span data-ttu-id="a85a5-224">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="a85a5-224">Type: Boolean</span></span>  
<span data-ttu-id="a85a5-225">Domyślne: n</span><span class="sxs-lookup"><span data-stu-id="a85a5-225">Default: n</span></span>

<span data-ttu-id="a85a5-226">Jeśli zostanie ustawiona, agenta waagent dekodowania CustomData z formatu Base64.</span><span class="sxs-lookup"><span data-stu-id="a85a5-226">If set, waagent will decode CustomData from Base64.</span></span>

<span data-ttu-id="a85a5-227">**Provisioning.ExecuteCustomData**</span><span class="sxs-lookup"><span data-stu-id="a85a5-227">**Provisioning.ExecuteCustomData**</span></span>  
<span data-ttu-id="a85a5-228">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="a85a5-228">Type: Boolean</span></span>  
<span data-ttu-id="a85a5-229">Domyślne: n</span><span class="sxs-lookup"><span data-stu-id="a85a5-229">Default: n</span></span>

<span data-ttu-id="a85a5-230">Jeśli ustawiona, agenta waagent wykona CustomData po zainicjowaniu obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="a85a5-230">If set, waagent will execute CustomData after provisioning.</span></span>

<span data-ttu-id="a85a5-231">**Provisioning.PasswordCryptId**</span><span class="sxs-lookup"><span data-stu-id="a85a5-231">**Provisioning.PasswordCryptId**</span></span>  
<span data-ttu-id="a85a5-232">Typ: ciąg</span><span class="sxs-lookup"><span data-stu-id="a85a5-232">Type:String</span></span>  
<span data-ttu-id="a85a5-233">Domyślne: 6</span><span class="sxs-lookup"><span data-stu-id="a85a5-233">Default:6</span></span>

<span data-ttu-id="a85a5-234">Algorytm używany przez crypt podczas generowania skrótu hasła.</span><span class="sxs-lookup"><span data-stu-id="a85a5-234">Algorithm used by crypt when generating password hash.</span></span>  
 <span data-ttu-id="a85a5-235">1 - MD5</span><span class="sxs-lookup"><span data-stu-id="a85a5-235">1 - MD5</span></span>  
 <span data-ttu-id="a85a5-236">2a - Blowfish</span><span class="sxs-lookup"><span data-stu-id="a85a5-236">2a - Blowfish</span></span>  
 <span data-ttu-id="a85a5-237">5 - ALGORYTMU SHA-256</span><span class="sxs-lookup"><span data-stu-id="a85a5-237">5 - SHA-256</span></span>  
 <span data-ttu-id="a85a5-238">6 - SHA-512</span><span class="sxs-lookup"><span data-stu-id="a85a5-238">6 - SHA-512</span></span>  

<span data-ttu-id="a85a5-239">**Provisioning.PasswordCryptSaltLength**</span><span class="sxs-lookup"><span data-stu-id="a85a5-239">**Provisioning.PasswordCryptSaltLength**</span></span>  
<span data-ttu-id="a85a5-240">Typ: ciąg</span><span class="sxs-lookup"><span data-stu-id="a85a5-240">Type:String</span></span>  
<span data-ttu-id="a85a5-241">Domyślny: 10</span><span class="sxs-lookup"><span data-stu-id="a85a5-241">Default:10</span></span>

<span data-ttu-id="a85a5-242">Długość losowe soli używana podczas generowania skrótu hasła.</span><span class="sxs-lookup"><span data-stu-id="a85a5-242">Length of random salt used when generating password hash.</span></span>

<span data-ttu-id="a85a5-243">**ResourceDisk.Format:**</span><span class="sxs-lookup"><span data-stu-id="a85a5-243">**ResourceDisk.Format:**</span></span>  
<span data-ttu-id="a85a5-244">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="a85a5-244">Type: Boolean</span></span>  
<span data-ttu-id="a85a5-245">Domyślne: y</span><span class="sxs-lookup"><span data-stu-id="a85a5-245">Default: y</span></span>

<span data-ttu-id="a85a5-246">Jeśli ustawiona, dysk zasobu dostarczone przez platformę zostanie sformatowany i zainstalowanych w wyniku agenta waagent, jeśli typ filesystem żądanej przez użytkownika w "ResourceDisk.Filesystem" jest inna niż "ntfs".</span><span class="sxs-lookup"><span data-stu-id="a85a5-246">If set, the resource disk provided by the platform will be formatted and mounted by waagent if the filesystem type requested by the user in "ResourceDisk.Filesystem" is anything other than "ntfs".</span></span> <span data-ttu-id="a85a5-247">Jednej partycji typu systemu Linux (83) będą dostępne na dysku.</span><span class="sxs-lookup"><span data-stu-id="a85a5-247">A single partition of type Linux (83) will be made available on the disk.</span></span> <span data-ttu-id="a85a5-248">Należy pamiętać, że ta partycja nie zostanie sformatowana Jeśli można zainstalować pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="a85a5-248">Note that this partition will not be formatted if it can be successfully mounted.</span></span>

<span data-ttu-id="a85a5-249">**ResourceDisk.Filesystem:**</span><span class="sxs-lookup"><span data-stu-id="a85a5-249">**ResourceDisk.Filesystem:**</span></span>  
<span data-ttu-id="a85a5-250">Typ: ciąg</span><span class="sxs-lookup"><span data-stu-id="a85a5-250">Type: String</span></span>  
<span data-ttu-id="a85a5-251">Domyślne: ext4</span><span class="sxs-lookup"><span data-stu-id="a85a5-251">Default: ext4</span></span>

<span data-ttu-id="a85a5-252">To ustawienie określa typ systemu plików dla zasobu dysku.</span><span class="sxs-lookup"><span data-stu-id="a85a5-252">This specifies the filesystem type for the resource disk.</span></span> <span data-ttu-id="a85a5-253">Obsługiwane wartości różnią się dystrybucji systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="a85a5-253">Supported values vary by Linux distribution.</span></span> <span data-ttu-id="a85a5-254">Jeśli ciąg jest następnie mkfs X. X powinny znajdować się w obrazie systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="a85a5-254">If the string is X, then mkfs.X should be present on the Linux image.</span></span> <span data-ttu-id="a85a5-255">SLES 11 obrazów zwykle należy użyć "ext3".</span><span class="sxs-lookup"><span data-stu-id="a85a5-255">SLES 11 images should typically use 'ext3'.</span></span> <span data-ttu-id="a85a5-256">Obrazy FreeBSD należy użyć "ufs2" w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="a85a5-256">FreeBSD images should use 'ufs2' here.</span></span>

<span data-ttu-id="a85a5-257">**ResourceDisk.MountPoint:**</span><span class="sxs-lookup"><span data-stu-id="a85a5-257">**ResourceDisk.MountPoint:**</span></span>  
<span data-ttu-id="a85a5-258">Typ: ciąg</span><span class="sxs-lookup"><span data-stu-id="a85a5-258">Type: String</span></span>  
<span data-ttu-id="a85a5-259">Wartość domyślna: / mnt/zasobu</span><span class="sxs-lookup"><span data-stu-id="a85a5-259">Default: /mnt/resource</span></span> 

<span data-ttu-id="a85a5-260">Określa ścieżkę, w którym jest zainstalowany dysk zasobu.</span><span class="sxs-lookup"><span data-stu-id="a85a5-260">This specifies the path at which the resource disk is mounted.</span></span> <span data-ttu-id="a85a5-261">Należy zauważyć, że zasób dysku *tymczasowego* na dysku i może opróżnić, gdy maszyna wirtualna jest anulowana.</span><span class="sxs-lookup"><span data-stu-id="a85a5-261">Note that the resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span>

<span data-ttu-id="a85a5-262">**ResourceDisk.MountOptions**</span><span class="sxs-lookup"><span data-stu-id="a85a5-262">**ResourceDisk.MountOptions**</span></span>  
<span data-ttu-id="a85a5-263">Typ: ciąg</span><span class="sxs-lookup"><span data-stu-id="a85a5-263">Type: String</span></span>  
<span data-ttu-id="a85a5-264">Domyślnie: Brak</span><span class="sxs-lookup"><span data-stu-id="a85a5-264">Default: None</span></span>

<span data-ttu-id="a85a5-265">Określa opcje instalacji dysku do przekazania do polecenia -o instalacji.</span><span class="sxs-lookup"><span data-stu-id="a85a5-265">Specifies disk mount options to be passed to the mount -o command.</span></span> <span data-ttu-id="a85a5-266">Jest to rozdzielana przecinkami lista wartości, np.</span><span class="sxs-lookup"><span data-stu-id="a85a5-266">This is a comma separated list of values, ex.</span></span> <span data-ttu-id="a85a5-267">"nodev, nosuid".</span><span class="sxs-lookup"><span data-stu-id="a85a5-267">'nodev,nosuid'.</span></span> <span data-ttu-id="a85a5-268">Zobacz mount(8), aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="a85a5-268">See mount(8) for details.</span></span>

<span data-ttu-id="a85a5-269">**ResourceDisk.EnableSwap:**</span><span class="sxs-lookup"><span data-stu-id="a85a5-269">**ResourceDisk.EnableSwap:**</span></span>  
<span data-ttu-id="a85a5-270">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="a85a5-270">Type: Boolean</span></span>  
<span data-ttu-id="a85a5-271">Domyślne: n</span><span class="sxs-lookup"><span data-stu-id="a85a5-271">Default: n</span></span>

<span data-ttu-id="a85a5-272">Jeśli ustawiona, plik wymiany (/ swapfile) jest utworzony na dysku zasobów i dodana do obszaru wymiany w systemie.</span><span class="sxs-lookup"><span data-stu-id="a85a5-272">If set, a swap file (/swapfile) is created on the resource disk and added to the system swap space.</span></span>

<span data-ttu-id="a85a5-273">**ResourceDisk.SwapSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="a85a5-273">**ResourceDisk.SwapSizeMB:**</span></span>  
<span data-ttu-id="a85a5-274">Typ: liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="a85a5-274">Type: Integer</span></span>  
<span data-ttu-id="a85a5-275">Domyślna: 0</span><span class="sxs-lookup"><span data-stu-id="a85a5-275">Default: 0</span></span>

<span data-ttu-id="a85a5-276">Rozmiar pliku wymiany w megabajtach.</span><span class="sxs-lookup"><span data-stu-id="a85a5-276">The size of the swap file in megabytes.</span></span>

<span data-ttu-id="a85a5-277">**Logs.Verbose:**</span><span class="sxs-lookup"><span data-stu-id="a85a5-277">**Logs.Verbose:**</span></span>  
<span data-ttu-id="a85a5-278">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="a85a5-278">Type: Boolean</span></span>  
<span data-ttu-id="a85a5-279">Domyślne: n</span><span class="sxs-lookup"><span data-stu-id="a85a5-279">Default: n</span></span>

<span data-ttu-id="a85a5-280">Jeśli jest boosted zestawu, szczegółowości dziennika.</span><span class="sxs-lookup"><span data-stu-id="a85a5-280">If set, log verbosity is boosted.</span></span> <span data-ttu-id="a85a5-281">Agenta Waagent rejestruje /var/log/waagent.log i korzysta z funkcji logrotate systemu w celu obracania dzienników.</span><span class="sxs-lookup"><span data-stu-id="a85a5-281">Waagent logs to /var/log/waagent.log and leverages the system logrotate functionality to rotate logs.</span></span>

<span data-ttu-id="a85a5-282">**SYSTEM OPERACYJNY. EnableRDMA**</span><span class="sxs-lookup"><span data-stu-id="a85a5-282">**OS.EnableRDMA**</span></span>  
<span data-ttu-id="a85a5-283">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="a85a5-283">Type: Boolean</span></span>  
<span data-ttu-id="a85a5-284">Domyślne: n</span><span class="sxs-lookup"><span data-stu-id="a85a5-284">Default: n</span></span>

<span data-ttu-id="a85a5-285">Jeśli ustawiona, agent podejmie próbę instalacji, a następnie załadować sterownik jądra RDMA, zgodna z wersją oprogramowania sprzętowego używanego sprzętu.</span><span class="sxs-lookup"><span data-stu-id="a85a5-285">If set, the agent will attempt to install and then load an RDMA kernel driver that matches the version of the firmware on the underlying hardware.</span></span>

<span data-ttu-id="a85a5-286">**SYSTEM OPERACYJNY. RootDeviceScsiTimeout:**</span><span class="sxs-lookup"><span data-stu-id="a85a5-286">**OS.RootDeviceScsiTimeout:**</span></span>  
<span data-ttu-id="a85a5-287">Typ: liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="a85a5-287">Type: Integer</span></span>  
<span data-ttu-id="a85a5-288">Domyślne: 300</span><span class="sxs-lookup"><span data-stu-id="a85a5-288">Default: 300</span></span>

<span data-ttu-id="a85a5-289">Spowoduje to skonfigurowanie SCSI limit czasu w sekundach na dyskach systemu operacyjnego dysku i danych.</span><span class="sxs-lookup"><span data-stu-id="a85a5-289">This configures the SCSI timeout in seconds on the OS disk and data drives.</span></span> <span data-ttu-id="a85a5-290">Jeśli nie jest ustawiony, systemu, które będą używane wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="a85a5-290">If not set, the system defaults are used.</span></span>

<span data-ttu-id="a85a5-291">**SYSTEM OPERACYJNY. OpensslPath:**</span><span class="sxs-lookup"><span data-stu-id="a85a5-291">**OS.OpensslPath:**</span></span>  
<span data-ttu-id="a85a5-292">Typ: ciąg</span><span class="sxs-lookup"><span data-stu-id="a85a5-292">Type: String</span></span>  
<span data-ttu-id="a85a5-293">Domyślnie: Brak</span><span class="sxs-lookup"><span data-stu-id="a85a5-293">Default: None</span></span>

<span data-ttu-id="a85a5-294">Może to służyć do określenia ścieżki alternatywnej dla biblioteki openssl binarnego do użycia dla operacji kryptograficznych.</span><span class="sxs-lookup"><span data-stu-id="a85a5-294">This can be used to specify an alternate path for the openssl binary to use for cryptographic operations.</span></span>

<span data-ttu-id="a85a5-295">**HttpProxy.Host, HttpProxy.Port**</span><span class="sxs-lookup"><span data-stu-id="a85a5-295">**HttpProxy.Host, HttpProxy.Port**</span></span>  
<span data-ttu-id="a85a5-296">Typ: ciąg</span><span class="sxs-lookup"><span data-stu-id="a85a5-296">Type: String</span></span>  
<span data-ttu-id="a85a5-297">Domyślnie: Brak</span><span class="sxs-lookup"><span data-stu-id="a85a5-297">Default: None</span></span>

<span data-ttu-id="a85a5-298">Jeśli ustawiona, będzie używane przez agenta ten serwer proxy do uzyskania dostępu do Internetu.</span><span class="sxs-lookup"><span data-stu-id="a85a5-298">If set, the agent will use this proxy server to access the internet.</span></span> 

## <a name="ubuntu-cloud-images"></a><span data-ttu-id="a85a5-299">Obrazy Ubuntu chmury</span><span class="sxs-lookup"><span data-stu-id="a85a5-299">Ubuntu Cloud Images</span></span>
<span data-ttu-id="a85a5-300">Należy pamiętać, że korzystanie z obrazów chmury Ubuntu [init chmury](https://launchpad.net/ubuntu/+source/cloud-init) do wykonywania wielu zadań konfiguracji, które w przeciwnym razie będą zarządzane przez agenta systemu Linux platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a85a5-300">Note that Ubuntu Cloud Images utilize [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) to perform many configuration tasks that would otherwise be managed by the Azure Linux Agent.</span></span>  <span data-ttu-id="a85a5-301">Należy pamiętać, następujące różnice:</span><span class="sxs-lookup"><span data-stu-id="a85a5-301">Please note the following differences:</span></span>

* <span data-ttu-id="a85a5-302">**Provisioning.Enabled** wartość domyślna to "n" na Ubuntu chmury obrazów użyj init chmury do wykonywania zadań inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="a85a5-302">**Provisioning.Enabled** defaults to "n" on Ubuntu Cloud Images that use cloud-init to perform provisioning tasks.</span></span>
* <span data-ttu-id="a85a5-303">Poniższe parametry konfiguracji nie mają wpływu na obrazy chmury Ubuntu, używanym do zarządzania dyskami zasobów i obszar wymiany init chmury:</span><span class="sxs-lookup"><span data-stu-id="a85a5-303">The following configuration parameters have no effect on Ubuntu Cloud Images that use cloud-init to manage the resource disk and swap space:</span></span>
  
  * <span data-ttu-id="a85a5-304">**ResourceDisk.Format**</span><span class="sxs-lookup"><span data-stu-id="a85a5-304">**ResourceDisk.Format**</span></span>
  * <span data-ttu-id="a85a5-305">**ResourceDisk.Filesystem**</span><span class="sxs-lookup"><span data-stu-id="a85a5-305">**ResourceDisk.Filesystem**</span></span>
  * <span data-ttu-id="a85a5-306">**ResourceDisk.MountPoint**</span><span class="sxs-lookup"><span data-stu-id="a85a5-306">**ResourceDisk.MountPoint**</span></span>
  * <span data-ttu-id="a85a5-307">**ResourceDisk.EnableSwap**</span><span class="sxs-lookup"><span data-stu-id="a85a5-307">**ResourceDisk.EnableSwap**</span></span>
  * <span data-ttu-id="a85a5-308">**ResourceDisk.SwapSizeMB**</span><span class="sxs-lookup"><span data-stu-id="a85a5-308">**ResourceDisk.SwapSizeMB**</span></span>
* <span data-ttu-id="a85a5-309">Zobacz następujące zasoby do konfigurowania punktu instalacji zasobów dysku i Zamień miejsce na obrazy chmury Ubuntu podczas inicjowania obsługi:</span><span class="sxs-lookup"><span data-stu-id="a85a5-309">Please see the following resources to configure the resource disk mount point and swap space on Ubuntu Cloud Images during provisioning:</span></span>
  
  * [<span data-ttu-id="a85a5-310">Ubuntu Witryna typu Wiki: Konfigurowanie partycji wymiany</span><span class="sxs-lookup"><span data-stu-id="a85a5-310">Ubuntu Wiki: Configure Swap Partitions</span></span>](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [<span data-ttu-id="a85a5-311">Wstrzykiwania niestandardowe dane do maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a85a5-311">Injecting Custom Data into an Azure Virtual Machine</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

