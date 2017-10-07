---
title: "aaaSelecting nazwy użytkownika dla systemu Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak nazwa użytkownika tooselect maszyny wirtualnej systemu Linux na platformie Azure."
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
ms.openlocfilehash: c65e2ac46f40bb8c9d74cccbaf248a070c0fa6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a><span data-ttu-id="3d31f-103">Wybieranie nazw użytkowników dla systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="3d31f-103">Selecting User Names for Linux on Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="3d31f-104">Podczas obsługi administracyjnej maszyny wirtualnej systemu Linux na platformie Azure należy określić nazwę hello użytkownika głównego nie mógł później użyć toolog do hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3d31f-104">When you provision a Linux virtual machine on Azure you must specify hello name of a non-root user that you can later use toolog into hello VM.</span></span> <span data-ttu-id="3d31f-105">Możesz wybrać nazwę hello hello nowego użytkownika, lub jeśli Inicjowanie obsługi za pomocą hello klasycznego portalu Azure możesz zaakceptować domyślną hello name "azureuser".</span><span class="sxs-lookup"><span data-stu-id="3d31f-105">You may choose hello name of hello new user, or if provisioning via hello Azure classic portal you can accept hello default name "azureuser".</span></span>

<span data-ttu-id="3d31f-106">W większości przypadków tego użytkownika nie istnieje na podstawowy obraz powitania i zostanie utworzony podczas procesu udostępniania hello.</span><span class="sxs-lookup"><span data-stu-id="3d31f-106">In most cases this user won't exist on hello base image and will be created during hello provisioning process.</span></span> <span data-ttu-id="3d31f-107">Jeśli hello użytkownika znajduje się na podstawowy obraz maszyny Wirtualnej hello, agenta systemu Linux Azure hello po prostu skonfiguruje hello hasła lub klucza SSH dla tego użytkownika na podstawie informacji hello, określone podczas tworzenia hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="3d31f-107">If hello user exists on hello base VM image, then hello Azure Linux agent simply configures hello password and/or SSH key for that user based on hello information you specified when creating hello VM.</span></span>

<span data-ttu-id="3d31f-108">**Jednak**, Linux definiuje zestaw nazwy użytkownika, które nie powinny być używane.</span><span class="sxs-lookup"><span data-stu-id="3d31f-108">**However**, Linux defines a set of user names that should not be used.</span></span> <span data-ttu-id="3d31f-109">Hello inicjowania obsługi będzie procesu **niepowodzenie** przy próbie tooprovision maszyny Wirtualnej systemu Linux przy użyciu istniejącego użytkownika system, który jest zdefiniowany jako użytkownik z UID 0-99.</span><span class="sxs-lookup"><span data-stu-id="3d31f-109">hello provisioning process will **fail** if you try tooprovision a Linux VM using an existing system user, which is defined as a user with UID 0-99.</span></span> <span data-ttu-id="3d31f-110">Typowym przykładem jest hello `root` użytkownika, który ma UID 0.</span><span class="sxs-lookup"><span data-stu-id="3d31f-110">A typical example is hello `root` user, which has UID 0.</span></span>

* <span data-ttu-id="3d31f-111">Zobacz też: [Linux Standard Base - zakresy identyfikator użytkownika](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span><span class="sxs-lookup"><span data-stu-id="3d31f-111">See also: [Linux Standard Base - User ID Ranges](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span></span>

<span data-ttu-id="3d31f-112">Witaj poniżej znajduje się lista typowych użytkowników wbudowanych systemu CentOS i Ubuntu, że należy unikać używania podczas inicjowania obsługi administracyjnej maszyny wirtualnej systemu Linux na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3d31f-112">hello following is a list of common built-in system users for CentOS and Ubuntu that you should avoid using when provisioning a Linux virtual machine on Azure.</span></span> <span data-ttu-id="3d31f-113">Ta lista jest tylko przykładem, zobacz dokumentację toohello dla Twojego tooensure dystrybucji tej nazwie użytkownika hello wybranych nie powoduje konfliktu z istniejącym użytkownikiem systemu.</span><span class="sxs-lookup"><span data-stu-id="3d31f-113">This list is just an example, please refer toohello documentation for your distribution tooensure that hello username you choose does not conflict with an existing system user.</span></span>

## <a name="centos"></a><span data-ttu-id="3d31f-114">CentOS</span><span class="sxs-lookup"><span data-stu-id="3d31f-114">CentOS</span></span>
* <span data-ttu-id="3d31f-115">abrt</span><span class="sxs-lookup"><span data-stu-id="3d31f-115">abrt</span></span>
* <span data-ttu-id="3d31f-116">usługi adm</span><span class="sxs-lookup"><span data-stu-id="3d31f-116">adm</span></span>
* <span data-ttu-id="3d31f-117">audio</span><span class="sxs-lookup"><span data-stu-id="3d31f-117">audio</span></span>
* <span data-ttu-id="3d31f-118">bin</span><span class="sxs-lookup"><span data-stu-id="3d31f-118">bin</span></span>
* <span data-ttu-id="3d31f-119">CDROM</span><span class="sxs-lookup"><span data-stu-id="3d31f-119">cdrom</span></span>
* <span data-ttu-id="3d31f-120">cgred</span><span class="sxs-lookup"><span data-stu-id="3d31f-120">cgred</span></span>
* <span data-ttu-id="3d31f-121">demon</span><span class="sxs-lookup"><span data-stu-id="3d31f-121">daemon</span></span>
* <span data-ttu-id="3d31f-122">dbus</span><span class="sxs-lookup"><span data-stu-id="3d31f-122">dbus</span></span>
* <span data-ttu-id="3d31f-123">inicjowania połączeń</span><span class="sxs-lookup"><span data-stu-id="3d31f-123">dialout</span></span>
* <span data-ttu-id="3d31f-124">DIP</span><span class="sxs-lookup"><span data-stu-id="3d31f-124">dip</span></span>
* <span data-ttu-id="3d31f-125">dysku</span><span class="sxs-lookup"><span data-stu-id="3d31f-125">disk</span></span>
* <span data-ttu-id="3d31f-126">dyskietek</span><span class="sxs-lookup"><span data-stu-id="3d31f-126">floppy</span></span>
* <span data-ttu-id="3d31f-127">FTP</span><span class="sxs-lookup"><span data-stu-id="3d31f-127">ftp</span></span>
* <span data-ttu-id="3d31f-128">FTP</span><span class="sxs-lookup"><span data-stu-id="3d31f-128">ftp</span></span>
* <span data-ttu-id="3d31f-129">gry</span><span class="sxs-lookup"><span data-stu-id="3d31f-129">games</span></span>
* <span data-ttu-id="3d31f-130">Gopher</span><span class="sxs-lookup"><span data-stu-id="3d31f-130">gopher</span></span>
* <span data-ttu-id="3d31f-131">haldaemon</span><span class="sxs-lookup"><span data-stu-id="3d31f-131">haldaemon</span></span>
* <span data-ttu-id="3d31f-132">zatrzymanie</span><span class="sxs-lookup"><span data-stu-id="3d31f-132">halt</span></span>
* <span data-ttu-id="3d31f-133">kmem</span><span class="sxs-lookup"><span data-stu-id="3d31f-133">kmem</span></span>
* <span data-ttu-id="3d31f-134">blokady</span><span class="sxs-lookup"><span data-stu-id="3d31f-134">lock</span></span>
* <span data-ttu-id="3d31f-135">LP</span><span class="sxs-lookup"><span data-stu-id="3d31f-135">lp</span></span>
* <span data-ttu-id="3d31f-136">Poczty</span><span class="sxs-lookup"><span data-stu-id="3d31f-136">mail</span></span>
* <span data-ttu-id="3d31f-137">Man</span><span class="sxs-lookup"><span data-stu-id="3d31f-137">man</span></span>
* <span data-ttu-id="3d31f-138">pamięci</span><span class="sxs-lookup"><span data-stu-id="3d31f-138">mem</span></span>
* <span data-ttu-id="3d31f-139">nfsnobody</span><span class="sxs-lookup"><span data-stu-id="3d31f-139">nfsnobody</span></span>
* <span data-ttu-id="3d31f-140">nikt nie</span><span class="sxs-lookup"><span data-stu-id="3d31f-140">nobody</span></span>
* <span data-ttu-id="3d31f-141">NTP</span><span class="sxs-lookup"><span data-stu-id="3d31f-141">ntp</span></span>
* <span data-ttu-id="3d31f-142">Operator</span><span class="sxs-lookup"><span data-stu-id="3d31f-142">operator</span></span>
* <span data-ttu-id="3d31f-143">oprofile</span><span class="sxs-lookup"><span data-stu-id="3d31f-143">oprofile</span></span>
* <span data-ttu-id="3d31f-144">postdrop</span><span class="sxs-lookup"><span data-stu-id="3d31f-144">postdrop</span></span>
* <span data-ttu-id="3d31f-145">Operatory przyrostka</span><span class="sxs-lookup"><span data-stu-id="3d31f-145">postfix</span></span>
* <span data-ttu-id="3d31f-146">qpidd</span><span class="sxs-lookup"><span data-stu-id="3d31f-146">qpidd</span></span>
* <span data-ttu-id="3d31f-147">główny</span><span class="sxs-lookup"><span data-stu-id="3d31f-147">root</span></span>
* <span data-ttu-id="3d31f-148">RPC</span><span class="sxs-lookup"><span data-stu-id="3d31f-148">rpc</span></span>
* <span data-ttu-id="3d31f-149">rpcuser</span><span class="sxs-lookup"><span data-stu-id="3d31f-149">rpcuser</span></span>
* <span data-ttu-id="3d31f-150">saslauth</span><span class="sxs-lookup"><span data-stu-id="3d31f-150">saslauth</span></span>
* <span data-ttu-id="3d31f-151">Zamknięcie</span><span class="sxs-lookup"><span data-stu-id="3d31f-151">shutdown</span></span>
* <span data-ttu-id="3d31f-152">slocate</span><span class="sxs-lookup"><span data-stu-id="3d31f-152">slocate</span></span>
* <span data-ttu-id="3d31f-153">sshd</span><span class="sxs-lookup"><span data-stu-id="3d31f-153">sshd</span></span>
* <span data-ttu-id="3d31f-154">stapdev</span><span class="sxs-lookup"><span data-stu-id="3d31f-154">stapdev</span></span>
* <span data-ttu-id="3d31f-155">stapusr</span><span class="sxs-lookup"><span data-stu-id="3d31f-155">stapusr</span></span>
* <span data-ttu-id="3d31f-156">Synchronizacji</span><span class="sxs-lookup"><span data-stu-id="3d31f-156">sync</span></span>
* <span data-ttu-id="3d31f-157">sys</span><span class="sxs-lookup"><span data-stu-id="3d31f-157">sys</span></span>
* <span data-ttu-id="3d31f-158">taśmy</span><span class="sxs-lookup"><span data-stu-id="3d31f-158">tape</span></span>
* <span data-ttu-id="3d31f-159">Test</span><span class="sxs-lookup"><span data-stu-id="3d31f-159">test</span></span>
* <span data-ttu-id="3d31f-160">tcpdump</span><span class="sxs-lookup"><span data-stu-id="3d31f-160">tcpdump</span></span>
* <span data-ttu-id="3d31f-161">usługi TTY</span><span class="sxs-lookup"><span data-stu-id="3d31f-161">tty</span></span>
* <span data-ttu-id="3d31f-162">użytkownicy</span><span class="sxs-lookup"><span data-stu-id="3d31f-162">users</span></span>
* <span data-ttu-id="3d31f-163">utempter</span><span class="sxs-lookup"><span data-stu-id="3d31f-163">utempter</span></span>
* <span data-ttu-id="3d31f-164">utmp</span><span class="sxs-lookup"><span data-stu-id="3d31f-164">utmp</span></span>
* <span data-ttu-id="3d31f-165">UUCP</span><span class="sxs-lookup"><span data-stu-id="3d31f-165">uucp</span></span>
* <span data-ttu-id="3d31f-166">vcsa</span><span class="sxs-lookup"><span data-stu-id="3d31f-166">vcsa</span></span>
* <span data-ttu-id="3d31f-167">wideo</span><span class="sxs-lookup"><span data-stu-id="3d31f-167">video</span></span>
* <span data-ttu-id="3d31f-168">koło</span><span class="sxs-lookup"><span data-stu-id="3d31f-168">wheel</span></span>

## <a name="ubuntu"></a><span data-ttu-id="3d31f-169">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="3d31f-169">Ubuntu</span></span>
* <span data-ttu-id="3d31f-170">usługi adm</span><span class="sxs-lookup"><span data-stu-id="3d31f-170">adm</span></span>
* <span data-ttu-id="3d31f-171">Administrator</span><span class="sxs-lookup"><span data-stu-id="3d31f-171">admin</span></span>
* <span data-ttu-id="3d31f-172">audio</span><span class="sxs-lookup"><span data-stu-id="3d31f-172">audio</span></span>
* <span data-ttu-id="3d31f-173">kopia zapasowa</span><span class="sxs-lookup"><span data-stu-id="3d31f-173">backup</span></span>
* <span data-ttu-id="3d31f-174">bin</span><span class="sxs-lookup"><span data-stu-id="3d31f-174">bin</span></span>
* <span data-ttu-id="3d31f-175">CDROM</span><span class="sxs-lookup"><span data-stu-id="3d31f-175">cdrom</span></span>
* <span data-ttu-id="3d31f-176">crontab</span><span class="sxs-lookup"><span data-stu-id="3d31f-176">crontab</span></span>
* <span data-ttu-id="3d31f-177">demon</span><span class="sxs-lookup"><span data-stu-id="3d31f-177">daemon</span></span>
* <span data-ttu-id="3d31f-178">inicjowania połączeń</span><span class="sxs-lookup"><span data-stu-id="3d31f-178">dialout</span></span>
* <span data-ttu-id="3d31f-179">DIP</span><span class="sxs-lookup"><span data-stu-id="3d31f-179">dip</span></span>
* <span data-ttu-id="3d31f-180">dysku</span><span class="sxs-lookup"><span data-stu-id="3d31f-180">disk</span></span>
* <span data-ttu-id="3d31f-181">Faksów</span><span class="sxs-lookup"><span data-stu-id="3d31f-181">fax</span></span>
* <span data-ttu-id="3d31f-182">dyskietek</span><span class="sxs-lookup"><span data-stu-id="3d31f-182">floppy</span></span>
* <span data-ttu-id="3d31f-183">Łączenie</span><span class="sxs-lookup"><span data-stu-id="3d31f-183">fuse</span></span>
* <span data-ttu-id="3d31f-184">gry</span><span class="sxs-lookup"><span data-stu-id="3d31f-184">games</span></span>
* <span data-ttu-id="3d31f-185">gnats</span><span class="sxs-lookup"><span data-stu-id="3d31f-185">gnats</span></span>
* <span data-ttu-id="3d31f-186">IRC</span><span class="sxs-lookup"><span data-stu-id="3d31f-186">irc</span></span>
* <span data-ttu-id="3d31f-187">kmem</span><span class="sxs-lookup"><span data-stu-id="3d31f-187">kmem</span></span>
* <span data-ttu-id="3d31f-188">orientacji poziomej</span><span class="sxs-lookup"><span data-stu-id="3d31f-188">landscape</span></span>
* <span data-ttu-id="3d31f-189">libuuid</span><span class="sxs-lookup"><span data-stu-id="3d31f-189">libuuid</span></span>
* <span data-ttu-id="3d31f-190">Lista</span><span class="sxs-lookup"><span data-stu-id="3d31f-190">list</span></span>
* <span data-ttu-id="3d31f-191">LP</span><span class="sxs-lookup"><span data-stu-id="3d31f-191">lp</span></span>
* <span data-ttu-id="3d31f-192">Poczty</span><span class="sxs-lookup"><span data-stu-id="3d31f-192">mail</span></span>
* <span data-ttu-id="3d31f-193">Man</span><span class="sxs-lookup"><span data-stu-id="3d31f-193">man</span></span>
* <span data-ttu-id="3d31f-194">messagebus</span><span class="sxs-lookup"><span data-stu-id="3d31f-194">messagebus</span></span>
* <span data-ttu-id="3d31f-195">mlocate</span><span class="sxs-lookup"><span data-stu-id="3d31f-195">mlocate</span></span>
* <span data-ttu-id="3d31f-196">netdev</span><span class="sxs-lookup"><span data-stu-id="3d31f-196">netdev</span></span>
* <span data-ttu-id="3d31f-197">Grupy dyskusyjne</span><span class="sxs-lookup"><span data-stu-id="3d31f-197">news</span></span>
* <span data-ttu-id="3d31f-198">nikt nie</span><span class="sxs-lookup"><span data-stu-id="3d31f-198">nobody</span></span>
* <span data-ttu-id="3d31f-199">nogroup</span><span class="sxs-lookup"><span data-stu-id="3d31f-199">nogroup</span></span>
* <span data-ttu-id="3d31f-200">Operator</span><span class="sxs-lookup"><span data-stu-id="3d31f-200">operator</span></span>
* <span data-ttu-id="3d31f-201">plugdev</span><span class="sxs-lookup"><span data-stu-id="3d31f-201">plugdev</span></span>
* <span data-ttu-id="3d31f-202">Serwer proxy</span><span class="sxs-lookup"><span data-stu-id="3d31f-202">proxy</span></span>
* <span data-ttu-id="3d31f-203">główny</span><span class="sxs-lookup"><span data-stu-id="3d31f-203">root</span></span>
* <span data-ttu-id="3d31f-204">SASL</span><span class="sxs-lookup"><span data-stu-id="3d31f-204">sasl</span></span>
* <span data-ttu-id="3d31f-205">Cień</span><span class="sxs-lookup"><span data-stu-id="3d31f-205">shadow</span></span>
* <span data-ttu-id="3d31f-206">src</span><span class="sxs-lookup"><span data-stu-id="3d31f-206">src</span></span>
* <span data-ttu-id="3d31f-207">SSH</span><span class="sxs-lookup"><span data-stu-id="3d31f-207">ssh</span></span>
* <span data-ttu-id="3d31f-208">sshd</span><span class="sxs-lookup"><span data-stu-id="3d31f-208">sshd</span></span>
* <span data-ttu-id="3d31f-209">personel</span><span class="sxs-lookup"><span data-stu-id="3d31f-209">staff</span></span>
* <span data-ttu-id="3d31f-210">sudo</span><span class="sxs-lookup"><span data-stu-id="3d31f-210">sudo</span></span>
* <span data-ttu-id="3d31f-211">Synchronizacji</span><span class="sxs-lookup"><span data-stu-id="3d31f-211">sync</span></span>
* <span data-ttu-id="3d31f-212">sys</span><span class="sxs-lookup"><span data-stu-id="3d31f-212">sys</span></span>
* <span data-ttu-id="3d31f-213">syslog</span><span class="sxs-lookup"><span data-stu-id="3d31f-213">syslog</span></span>
* <span data-ttu-id="3d31f-214">taśmy</span><span class="sxs-lookup"><span data-stu-id="3d31f-214">tape</span></span>
* <span data-ttu-id="3d31f-215">usługi TTY</span><span class="sxs-lookup"><span data-stu-id="3d31f-215">tty</span></span>
* <span data-ttu-id="3d31f-216">użytkownicy</span><span class="sxs-lookup"><span data-stu-id="3d31f-216">users</span></span>
* <span data-ttu-id="3d31f-217">utmp</span><span class="sxs-lookup"><span data-stu-id="3d31f-217">utmp</span></span>
* <span data-ttu-id="3d31f-218">UUCP</span><span class="sxs-lookup"><span data-stu-id="3d31f-218">uucp</span></span>
* <span data-ttu-id="3d31f-219">wideo</span><span class="sxs-lookup"><span data-stu-id="3d31f-219">video</span></span>
* <span data-ttu-id="3d31f-220">głosu</span><span class="sxs-lookup"><span data-stu-id="3d31f-220">voice</span></span>
* <span data-ttu-id="3d31f-221">whoopsie</span><span class="sxs-lookup"><span data-stu-id="3d31f-221">whoopsie</span></span>
* <span data-ttu-id="3d31f-222">dane www</span><span class="sxs-lookup"><span data-stu-id="3d31f-222">www-data</span></span>

