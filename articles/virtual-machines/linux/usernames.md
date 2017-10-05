---
title: "Wybieranie nazwy użytkownika dla systemu Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wybrać nazwy użytkownika dla maszyny wirtualnej systemu Linux na platformie Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 33b50c97-92f1-46c9-a623-e37f67459c5c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 1874d72e5f88816036667932371ff28704d186c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a><span data-ttu-id="3ddb2-103">Wybieranie nazw użytkowników dla systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="3ddb2-103">Selecting User Names for Linux on Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="3ddb2-104">Podczas obsługi administracyjnej maszyny wirtualnej systemu Linux na platformie Azure należy określić nazwę użytkownika z systemem innym niż główny, który mógł później użyć do zalogowania się do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3ddb2-104">When you provision a Linux virtual machine on Azure you must specify the name of a non-root user that you can later use to log into the VM.</span></span> <span data-ttu-id="3ddb2-105">Można wybrać nazwę nowego użytkownika lub inicjowania obsługi administracyjnej za pośrednictwem klasycznego portalu Azure możesz zaakceptować domyślną nazwę "azureuser".</span><span class="sxs-lookup"><span data-stu-id="3ddb2-105">You may choose the name of the new user, or if provisioning via the Azure classic portal you can accept the default name "azureuser".</span></span>

<span data-ttu-id="3ddb2-106">W większości przypadków tego użytkownika nie istnieje na podstawowy obraz i zostanie utworzony podczas procesu inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="3ddb2-106">In most cases this user won't exist on the base image and will be created during the provisioning process.</span></span> <span data-ttu-id="3ddb2-107">Jeśli użytkownik istnieje na podstawowy obraz maszyny Wirtualnej, a następnie agenta systemu Linux platformy Azure po prostu konfiguruje hasła lub klucza SSH dla tego użytkownika na podstawie informacji, które można określić podczas tworzenia maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3ddb2-107">If the user exists on the base VM image, then the Azure Linux agent simply configures the password and/or SSH key for that user based on the information you specified when creating the VM.</span></span>

<span data-ttu-id="3ddb2-108">**Jednak**, Linux definiuje zestaw nazwy użytkownika, które nie powinny być używane.</span><span class="sxs-lookup"><span data-stu-id="3ddb2-108">**However**, Linux defines a set of user names that should not be used.</span></span> <span data-ttu-id="3ddb2-109">Proces inicjowania obsługi administracyjnej zostanie **niepowodzenie** próba udostępnienia maszyny Wirtualnej systemu Linux przy użyciu istniejącego użytkownika system, który jest zdefiniowany jako użytkownik z UID 0-99.</span><span class="sxs-lookup"><span data-stu-id="3ddb2-109">The provisioning process will **fail** if you try to provision a Linux VM using an existing system user, which is defined as a user with UID 0-99.</span></span> <span data-ttu-id="3ddb2-110">Typowym przykładem jest `root` użytkownika, który ma UID 0.</span><span class="sxs-lookup"><span data-stu-id="3ddb2-110">A typical example is the `root` user, which has UID 0.</span></span>

* <span data-ttu-id="3ddb2-111">Zobacz też: [Linux Standard Base - zakresy identyfikator użytkownika](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span><span class="sxs-lookup"><span data-stu-id="3ddb2-111">See also: [Linux Standard Base - User ID Ranges](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span></span>

<span data-ttu-id="3ddb2-112">Poniżej znajduje się lista typowych użytkowników wbudowanych systemu CentOS i Ubuntu, że należy unikać używania podczas inicjowania obsługi administracyjnej maszyny wirtualnej systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3ddb2-112">The following is a list of common built-in system users for CentOS and Ubuntu that you should avoid using when provisioning a Linux virtual machine on Azure.</span></span> <span data-ttu-id="3ddb2-113">Ta lista jest tylko przykładem, zapoznaj się z dokumentacją dotyczącą Twojej dystrybucji upewnić się, że wybrana nazwa użytkownika nie powoduje konfliktu z istniejącym użytkownikiem systemu.</span><span class="sxs-lookup"><span data-stu-id="3ddb2-113">This list is just an example, please refer to the documentation for your distribution to ensure that the username you choose does not conflict with an existing system user.</span></span>

## <a name="centos"></a><span data-ttu-id="3ddb2-114">CentOS</span><span class="sxs-lookup"><span data-stu-id="3ddb2-114">CentOS</span></span>
* <span data-ttu-id="3ddb2-115">abrt</span><span class="sxs-lookup"><span data-stu-id="3ddb2-115">abrt</span></span>
* <span data-ttu-id="3ddb2-116">usługi adm</span><span class="sxs-lookup"><span data-stu-id="3ddb2-116">adm</span></span>
* <span data-ttu-id="3ddb2-117">audio</span><span class="sxs-lookup"><span data-stu-id="3ddb2-117">audio</span></span>
* <span data-ttu-id="3ddb2-118">bin</span><span class="sxs-lookup"><span data-stu-id="3ddb2-118">bin</span></span>
* <span data-ttu-id="3ddb2-119">CDROM</span><span class="sxs-lookup"><span data-stu-id="3ddb2-119">cdrom</span></span>
* <span data-ttu-id="3ddb2-120">cgred</span><span class="sxs-lookup"><span data-stu-id="3ddb2-120">cgred</span></span>
* <span data-ttu-id="3ddb2-121">demon</span><span class="sxs-lookup"><span data-stu-id="3ddb2-121">daemon</span></span>
* <span data-ttu-id="3ddb2-122">dbus</span><span class="sxs-lookup"><span data-stu-id="3ddb2-122">dbus</span></span>
* <span data-ttu-id="3ddb2-123">inicjowania połączeń</span><span class="sxs-lookup"><span data-stu-id="3ddb2-123">dialout</span></span>
* <span data-ttu-id="3ddb2-124">DIP</span><span class="sxs-lookup"><span data-stu-id="3ddb2-124">dip</span></span>
* <span data-ttu-id="3ddb2-125">dysku</span><span class="sxs-lookup"><span data-stu-id="3ddb2-125">disk</span></span>
* <span data-ttu-id="3ddb2-126">dyskietek</span><span class="sxs-lookup"><span data-stu-id="3ddb2-126">floppy</span></span>
* <span data-ttu-id="3ddb2-127">FTP</span><span class="sxs-lookup"><span data-stu-id="3ddb2-127">ftp</span></span>
* <span data-ttu-id="3ddb2-128">FTP</span><span class="sxs-lookup"><span data-stu-id="3ddb2-128">ftp</span></span>
* <span data-ttu-id="3ddb2-129">gry</span><span class="sxs-lookup"><span data-stu-id="3ddb2-129">games</span></span>
* <span data-ttu-id="3ddb2-130">Gopher</span><span class="sxs-lookup"><span data-stu-id="3ddb2-130">gopher</span></span>
* <span data-ttu-id="3ddb2-131">haldaemon</span><span class="sxs-lookup"><span data-stu-id="3ddb2-131">haldaemon</span></span>
* <span data-ttu-id="3ddb2-132">zatrzymanie</span><span class="sxs-lookup"><span data-stu-id="3ddb2-132">halt</span></span>
* <span data-ttu-id="3ddb2-133">kmem</span><span class="sxs-lookup"><span data-stu-id="3ddb2-133">kmem</span></span>
* <span data-ttu-id="3ddb2-134">blokady</span><span class="sxs-lookup"><span data-stu-id="3ddb2-134">lock</span></span>
* <span data-ttu-id="3ddb2-135">LP</span><span class="sxs-lookup"><span data-stu-id="3ddb2-135">lp</span></span>
* <span data-ttu-id="3ddb2-136">Poczty</span><span class="sxs-lookup"><span data-stu-id="3ddb2-136">mail</span></span>
* <span data-ttu-id="3ddb2-137">Man</span><span class="sxs-lookup"><span data-stu-id="3ddb2-137">man</span></span>
* <span data-ttu-id="3ddb2-138">pamięci</span><span class="sxs-lookup"><span data-stu-id="3ddb2-138">mem</span></span>
* <span data-ttu-id="3ddb2-139">nfsnobody</span><span class="sxs-lookup"><span data-stu-id="3ddb2-139">nfsnobody</span></span>
* <span data-ttu-id="3ddb2-140">nikt nie</span><span class="sxs-lookup"><span data-stu-id="3ddb2-140">nobody</span></span>
* <span data-ttu-id="3ddb2-141">NTP</span><span class="sxs-lookup"><span data-stu-id="3ddb2-141">ntp</span></span>
* <span data-ttu-id="3ddb2-142">Operator</span><span class="sxs-lookup"><span data-stu-id="3ddb2-142">operator</span></span>
* <span data-ttu-id="3ddb2-143">oprofile</span><span class="sxs-lookup"><span data-stu-id="3ddb2-143">oprofile</span></span>
* <span data-ttu-id="3ddb2-144">postdrop</span><span class="sxs-lookup"><span data-stu-id="3ddb2-144">postdrop</span></span>
* <span data-ttu-id="3ddb2-145">Operatory przyrostka</span><span class="sxs-lookup"><span data-stu-id="3ddb2-145">postfix</span></span>
* <span data-ttu-id="3ddb2-146">qpidd</span><span class="sxs-lookup"><span data-stu-id="3ddb2-146">qpidd</span></span>
* <span data-ttu-id="3ddb2-147">główny</span><span class="sxs-lookup"><span data-stu-id="3ddb2-147">root</span></span>
* <span data-ttu-id="3ddb2-148">RPC</span><span class="sxs-lookup"><span data-stu-id="3ddb2-148">rpc</span></span>
* <span data-ttu-id="3ddb2-149">rpcuser</span><span class="sxs-lookup"><span data-stu-id="3ddb2-149">rpcuser</span></span>
* <span data-ttu-id="3ddb2-150">saslauth</span><span class="sxs-lookup"><span data-stu-id="3ddb2-150">saslauth</span></span>
* <span data-ttu-id="3ddb2-151">Zamknięcie</span><span class="sxs-lookup"><span data-stu-id="3ddb2-151">shutdown</span></span>
* <span data-ttu-id="3ddb2-152">slocate</span><span class="sxs-lookup"><span data-stu-id="3ddb2-152">slocate</span></span>
* <span data-ttu-id="3ddb2-153">sshd</span><span class="sxs-lookup"><span data-stu-id="3ddb2-153">sshd</span></span>
* <span data-ttu-id="3ddb2-154">stapdev</span><span class="sxs-lookup"><span data-stu-id="3ddb2-154">stapdev</span></span>
* <span data-ttu-id="3ddb2-155">stapusr</span><span class="sxs-lookup"><span data-stu-id="3ddb2-155">stapusr</span></span>
* <span data-ttu-id="3ddb2-156">Synchronizacji</span><span class="sxs-lookup"><span data-stu-id="3ddb2-156">sync</span></span>
* <span data-ttu-id="3ddb2-157">sys</span><span class="sxs-lookup"><span data-stu-id="3ddb2-157">sys</span></span>
* <span data-ttu-id="3ddb2-158">taśmy</span><span class="sxs-lookup"><span data-stu-id="3ddb2-158">tape</span></span>
* <span data-ttu-id="3ddb2-159">Test</span><span class="sxs-lookup"><span data-stu-id="3ddb2-159">test</span></span>
* <span data-ttu-id="3ddb2-160">tcpdump</span><span class="sxs-lookup"><span data-stu-id="3ddb2-160">tcpdump</span></span>
* <span data-ttu-id="3ddb2-161">usługi TTY</span><span class="sxs-lookup"><span data-stu-id="3ddb2-161">tty</span></span>
* <span data-ttu-id="3ddb2-162">użytkownicy</span><span class="sxs-lookup"><span data-stu-id="3ddb2-162">users</span></span>
* <span data-ttu-id="3ddb2-163">utempter</span><span class="sxs-lookup"><span data-stu-id="3ddb2-163">utempter</span></span>
* <span data-ttu-id="3ddb2-164">utmp</span><span class="sxs-lookup"><span data-stu-id="3ddb2-164">utmp</span></span>
* <span data-ttu-id="3ddb2-165">UUCP</span><span class="sxs-lookup"><span data-stu-id="3ddb2-165">uucp</span></span>
* <span data-ttu-id="3ddb2-166">vcsa</span><span class="sxs-lookup"><span data-stu-id="3ddb2-166">vcsa</span></span>
* <span data-ttu-id="3ddb2-167">wideo</span><span class="sxs-lookup"><span data-stu-id="3ddb2-167">video</span></span>
* <span data-ttu-id="3ddb2-168">koło</span><span class="sxs-lookup"><span data-stu-id="3ddb2-168">wheel</span></span>

## <a name="ubuntu"></a><span data-ttu-id="3ddb2-169">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="3ddb2-169">Ubuntu</span></span>
* <span data-ttu-id="3ddb2-170">usługi adm</span><span class="sxs-lookup"><span data-stu-id="3ddb2-170">adm</span></span>
* <span data-ttu-id="3ddb2-171">Administrator</span><span class="sxs-lookup"><span data-stu-id="3ddb2-171">admin</span></span>
* <span data-ttu-id="3ddb2-172">audio</span><span class="sxs-lookup"><span data-stu-id="3ddb2-172">audio</span></span>
* <span data-ttu-id="3ddb2-173">kopia zapasowa</span><span class="sxs-lookup"><span data-stu-id="3ddb2-173">backup</span></span>
* <span data-ttu-id="3ddb2-174">bin</span><span class="sxs-lookup"><span data-stu-id="3ddb2-174">bin</span></span>
* <span data-ttu-id="3ddb2-175">CDROM</span><span class="sxs-lookup"><span data-stu-id="3ddb2-175">cdrom</span></span>
* <span data-ttu-id="3ddb2-176">crontab</span><span class="sxs-lookup"><span data-stu-id="3ddb2-176">crontab</span></span>
* <span data-ttu-id="3ddb2-177">demon</span><span class="sxs-lookup"><span data-stu-id="3ddb2-177">daemon</span></span>
* <span data-ttu-id="3ddb2-178">inicjowania połączeń</span><span class="sxs-lookup"><span data-stu-id="3ddb2-178">dialout</span></span>
* <span data-ttu-id="3ddb2-179">DIP</span><span class="sxs-lookup"><span data-stu-id="3ddb2-179">dip</span></span>
* <span data-ttu-id="3ddb2-180">dysku</span><span class="sxs-lookup"><span data-stu-id="3ddb2-180">disk</span></span>
* <span data-ttu-id="3ddb2-181">Faksów</span><span class="sxs-lookup"><span data-stu-id="3ddb2-181">fax</span></span>
* <span data-ttu-id="3ddb2-182">dyskietek</span><span class="sxs-lookup"><span data-stu-id="3ddb2-182">floppy</span></span>
* <span data-ttu-id="3ddb2-183">Łączenie</span><span class="sxs-lookup"><span data-stu-id="3ddb2-183">fuse</span></span>
* <span data-ttu-id="3ddb2-184">gry</span><span class="sxs-lookup"><span data-stu-id="3ddb2-184">games</span></span>
* <span data-ttu-id="3ddb2-185">gnats</span><span class="sxs-lookup"><span data-stu-id="3ddb2-185">gnats</span></span>
* <span data-ttu-id="3ddb2-186">IRC</span><span class="sxs-lookup"><span data-stu-id="3ddb2-186">irc</span></span>
* <span data-ttu-id="3ddb2-187">kmem</span><span class="sxs-lookup"><span data-stu-id="3ddb2-187">kmem</span></span>
* <span data-ttu-id="3ddb2-188">orientacji poziomej</span><span class="sxs-lookup"><span data-stu-id="3ddb2-188">landscape</span></span>
* <span data-ttu-id="3ddb2-189">libuuid</span><span class="sxs-lookup"><span data-stu-id="3ddb2-189">libuuid</span></span>
* <span data-ttu-id="3ddb2-190">Lista</span><span class="sxs-lookup"><span data-stu-id="3ddb2-190">list</span></span>
* <span data-ttu-id="3ddb2-191">LP</span><span class="sxs-lookup"><span data-stu-id="3ddb2-191">lp</span></span>
* <span data-ttu-id="3ddb2-192">Poczty</span><span class="sxs-lookup"><span data-stu-id="3ddb2-192">mail</span></span>
* <span data-ttu-id="3ddb2-193">Man</span><span class="sxs-lookup"><span data-stu-id="3ddb2-193">man</span></span>
* <span data-ttu-id="3ddb2-194">messagebus</span><span class="sxs-lookup"><span data-stu-id="3ddb2-194">messagebus</span></span>
* <span data-ttu-id="3ddb2-195">mlocate</span><span class="sxs-lookup"><span data-stu-id="3ddb2-195">mlocate</span></span>
* <span data-ttu-id="3ddb2-196">netdev</span><span class="sxs-lookup"><span data-stu-id="3ddb2-196">netdev</span></span>
* <span data-ttu-id="3ddb2-197">Grupy dyskusyjne</span><span class="sxs-lookup"><span data-stu-id="3ddb2-197">news</span></span>
* <span data-ttu-id="3ddb2-198">nikt nie</span><span class="sxs-lookup"><span data-stu-id="3ddb2-198">nobody</span></span>
* <span data-ttu-id="3ddb2-199">nogroup</span><span class="sxs-lookup"><span data-stu-id="3ddb2-199">nogroup</span></span>
* <span data-ttu-id="3ddb2-200">Operator</span><span class="sxs-lookup"><span data-stu-id="3ddb2-200">operator</span></span>
* <span data-ttu-id="3ddb2-201">plugdev</span><span class="sxs-lookup"><span data-stu-id="3ddb2-201">plugdev</span></span>
* <span data-ttu-id="3ddb2-202">Serwer proxy</span><span class="sxs-lookup"><span data-stu-id="3ddb2-202">proxy</span></span>
* <span data-ttu-id="3ddb2-203">główny</span><span class="sxs-lookup"><span data-stu-id="3ddb2-203">root</span></span>
* <span data-ttu-id="3ddb2-204">SASL</span><span class="sxs-lookup"><span data-stu-id="3ddb2-204">sasl</span></span>
* <span data-ttu-id="3ddb2-205">Cień</span><span class="sxs-lookup"><span data-stu-id="3ddb2-205">shadow</span></span>
* <span data-ttu-id="3ddb2-206">src</span><span class="sxs-lookup"><span data-stu-id="3ddb2-206">src</span></span>
* <span data-ttu-id="3ddb2-207">SSH</span><span class="sxs-lookup"><span data-stu-id="3ddb2-207">ssh</span></span>
* <span data-ttu-id="3ddb2-208">sshd</span><span class="sxs-lookup"><span data-stu-id="3ddb2-208">sshd</span></span>
* <span data-ttu-id="3ddb2-209">personel</span><span class="sxs-lookup"><span data-stu-id="3ddb2-209">staff</span></span>
* <span data-ttu-id="3ddb2-210">sudo</span><span class="sxs-lookup"><span data-stu-id="3ddb2-210">sudo</span></span>
* <span data-ttu-id="3ddb2-211">Synchronizacji</span><span class="sxs-lookup"><span data-stu-id="3ddb2-211">sync</span></span>
* <span data-ttu-id="3ddb2-212">sys</span><span class="sxs-lookup"><span data-stu-id="3ddb2-212">sys</span></span>
* <span data-ttu-id="3ddb2-213">syslog</span><span class="sxs-lookup"><span data-stu-id="3ddb2-213">syslog</span></span>
* <span data-ttu-id="3ddb2-214">taśmy</span><span class="sxs-lookup"><span data-stu-id="3ddb2-214">tape</span></span>
* <span data-ttu-id="3ddb2-215">usługi TTY</span><span class="sxs-lookup"><span data-stu-id="3ddb2-215">tty</span></span>
* <span data-ttu-id="3ddb2-216">użytkownicy</span><span class="sxs-lookup"><span data-stu-id="3ddb2-216">users</span></span>
* <span data-ttu-id="3ddb2-217">utmp</span><span class="sxs-lookup"><span data-stu-id="3ddb2-217">utmp</span></span>
* <span data-ttu-id="3ddb2-218">UUCP</span><span class="sxs-lookup"><span data-stu-id="3ddb2-218">uucp</span></span>
* <span data-ttu-id="3ddb2-219">wideo</span><span class="sxs-lookup"><span data-stu-id="3ddb2-219">video</span></span>
* <span data-ttu-id="3ddb2-220">głosu</span><span class="sxs-lookup"><span data-stu-id="3ddb2-220">voice</span></span>
* <span data-ttu-id="3ddb2-221">whoopsie</span><span class="sxs-lookup"><span data-stu-id="3ddb2-221">whoopsie</span></span>
* <span data-ttu-id="3ddb2-222">dane www</span><span class="sxs-lookup"><span data-stu-id="3ddb2-222">www-data</span></span>

