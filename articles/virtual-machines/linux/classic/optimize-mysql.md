---
title: "aaaOptimize MySQL wydajności w systemie Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toooptimize MySQL uruchomionych na maszynie wirtualnej platformy Azure (VM) systemem Linux."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0c1c7fc5-a528-4d84-b65d-2df225f2233f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: ningk
ms.openlocfilehash: 9e6458723233721e06f30b9de33635d403eefcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a><span data-ttu-id="b3bb3-103">Optymalizowanie MySQL na maszynach wirtualnych systemu Linux platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b3bb3-103">Optimize MySQL Performance on Azure Linux VMs</span></span>
<span data-ttu-id="b3bb3-104">Istnieje wiele czynników, które mają wpływ na wydajność MySQL na platformie Azure, zarówno w wybór sprzęt wirtualny i konfiguracji oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-104">There are many factors that affect MySQL performance on Azure, both in virtual hardware selection and software configuration.</span></span> <span data-ttu-id="b3bb3-105">Ten artykuł dotyczy Optymalizacja wydajności za pomocą magazynu, systemu i konfiguracje bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-105">This article focuses on optimizing performance through storage, system, and database configurations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b3bb3-106">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager](../../../resource-manager-deployment-model.md) i klasycznym.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="b3bb3-107">W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-107">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="b3bb3-108">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="b3bb3-109">Informacje o optymalizacji maszyny Wirtualnej systemu Linux z modelu Resource Manager hello, zobacz [optymalizacji sieci maszyny Wirtualnej systemu Linux na platformie Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b3bb3-109">For information about Linux VM optimizations with hello Resource Manager model, see [Optimize your Linux VM on Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="utilize-raid-on-an-azure-virtual-machine"></a><span data-ttu-id="b3bb3-110">Korzystanie z RAID na maszynie wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b3bb3-110">Utilize RAID on an Azure virtual machine</span></span>
<span data-ttu-id="b3bb3-111">Magazyn jest hello kluczowym czynnikiem wpływającym na wydajność bazy danych w środowisku chmury.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-111">Storage is hello key factor that affects database performance in cloud environments.</span></span> <span data-ttu-id="b3bb3-112">Jeden dysk w porównaniu tooa RAID zapewnia szybszy dostęp za pośrednictwem współbieżności.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-112">Compared tooa single disk, RAID can provide faster access via concurrency.</span></span> <span data-ttu-id="b3bb3-113">Aby uzyskać więcej informacji, zobacz [poziomy RAID standardowe](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span><span class="sxs-lookup"><span data-stu-id="b3bb3-113">For more information, see [Standard RAID levels](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span></span>   

<span data-ttu-id="b3bb3-114">Można zwiększyć przepływność We/Wy dysku i czas odpowiedzi operacji We/Wy na platformie Azure za pomocą macierzy RAID.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-114">Disk I/O throughput and I/O response time in Azure can be improved through RAID.</span></span> <span data-ttu-id="b3bb3-115">Nasze testy laboratorium wskazują, że przepustowość operacji We/Wy dysku może być podwójny i czas odpowiedzi operacji We/Wy, można zmniejszyć o połowę średnio po hello liczba dysków RAID jest podwójny (od toofour dwa, cztery tooeight itp.).</span><span class="sxs-lookup"><span data-stu-id="b3bb3-115">Our lab tests show that disk I/O throughput can be doubled and I/O response time can be reduced by half on average when hello number of RAID disks is doubled (from two toofour, four tooeight, etc.).</span></span> <span data-ttu-id="b3bb3-116">Zobacz [dodatek a.](#AppendixA) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-116">See [Appendix A](#AppendixA) for details.</span></span>  

<span data-ttu-id="b3bb3-117">Ponadto toodisk we/wy, MySQL wydajności poprawia wraz ze zwiększeniem hello poziom RAID.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-117">In addition toodisk I/O, MySQL performance improves when you increase hello RAID level.</span></span>  <span data-ttu-id="b3bb3-118">Zobacz [dodatek B](#AppendixB) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-118">See [Appendix B](#AppendixB) for details.</span></span>  

<span data-ttu-id="b3bb3-119">Można także rozmiar fragmentu hello tooconsider.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-119">You might also want tooconsider hello chunk size.</span></span> <span data-ttu-id="b3bb3-120">Ogólnie rzecz biorąc Jeśli masz większy rozmiar fragmentu otrzymasz niższe nakładów pracy, zwłaszcza w przypadku dużych operacji zapisu.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-120">In general, when you have a larger chunk size, you get lower overhead, especially for large writes.</span></span> <span data-ttu-id="b3bb3-121">Jednak gdy rozmiar fragmentu hello jest zbyt duży, może dodawać dodatkowe obciążenie, który uniemożliwia wykorzystaniu RAID.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-121">However, when hello chunk size is too large, it might add additional overhead that prevents you from taking advantage of RAID.</span></span> <span data-ttu-id="b3bb3-122">Bieżący rozmiar domyślny Hello jest 512 KB, który jest sprawdzone toobe optymalne dla większości środowisk produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-122">hello current default size is 512 KB, which is proven toobe optimal for most general production environments.</span></span> <span data-ttu-id="b3bb3-123">Zobacz [dodatku C](#AppendixC) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-123">See [Appendix C](#AppendixC) for details.</span></span>   

<span data-ttu-id="b3bb3-124">Istnieją ograniczenia liczby dysków dla typów inną maszynę wirtualną można dodać.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-124">There are limits on how many disks you can add for different virtual machine types.</span></span> <span data-ttu-id="b3bb3-125">Te limity wyszczególnione w [maszyny wirtualnej i w chmurze rozmiary usługi Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="b3bb3-125">These limits are detailed in [Virtual machine and cloud service sizes for Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span> <span data-ttu-id="b3bb3-126">Konieczne będzie cztery danych dołączonych dysków toofollow RAID przykład Witaj w tym artykule, chociaż można wybrać tooset się RAID z mniejszą liczbę dysków.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-126">You will need four attached data disks toofollow hello RAID example in this article, although you can choose tooset up RAID with fewer disks.</span></span>  

<span data-ttu-id="b3bb3-127">W tym artykule przyjęto założenie, zostały już utworzone maszyny wirtualnej systemu Linux i MYSQL zainstalowany i skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-127">This article assumes you have already created a Linux virtual machine and have MYSQL installed and configured.</span></span> <span data-ttu-id="b3bb3-128">Aby uzyskać więcej informacji na wprowadzenie, zobacz temat jak tooinstall MySQL na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-128">For more information on getting started, see How tooinstall MySQL on Azure.</span></span>  

### <a name="set-up-raid-on-azure"></a><span data-ttu-id="b3bb3-129">— Konfiguracja RAID na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="b3bb3-129">Set up RAID on Azure</span></span>
<span data-ttu-id="b3bb3-130">Witaj poniższej procedurze pokazano, jak RAID toocreate na platformie Azure przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-130">hello following steps show how toocreate RAID on Azure by using hello Azure portal.</span></span> <span data-ttu-id="b3bb3-131">Można również skonfigurować RAID za pomocą skryptów środowiska Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-131">You can also set up RAID by using Windows PowerShell scripts.</span></span>
<span data-ttu-id="b3bb3-132">W tym przykładzie będzie skonfigurowanie RAID 0 z czterech dysków.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-132">In this example, we will configure RAID 0 with four disks.</span></span>  

#### <a name="add-a-data-disk-tooyour-virtual-machine"></a><span data-ttu-id="b3bb3-133">Dodaj maszynę wirtualną tooyour dysk danych</span><span class="sxs-lookup"><span data-stu-id="b3bb3-133">Add a data disk tooyour virtual machine</span></span>
<span data-ttu-id="b3bb3-134">W hello portalu Azure przejdź do pulpitu nawigacyjnego toohello i wybierz hello toowhich maszyny wirtualnej ma tooadd dysk z danymi.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-134">In hello Azure portal, go toohello dashboard and select hello virtual machine toowhich you want tooadd a data disk.</span></span> <span data-ttu-id="b3bb3-135">W tym przykładzie maszyna wirtualna hello jest mysqlnode1.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-135">In this example, hello virtual machine is mysqlnode1.</span></span>  

<!--![Virtual machines][1]-->

<span data-ttu-id="b3bb3-136">Kliknij przycisk **dysków** , a następnie kliknij przycisk **dołączyć nowy**.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-136">Click **Disks** and then click **Attach New**.</span></span>

![Maszyny wirtualne, Dodaj dysk](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

<span data-ttu-id="b3bb3-138">Utwórz nowy dysk 500 GB.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-138">Create a new 500 GB disk.</span></span> <span data-ttu-id="b3bb3-139">Upewnij się, że **hosta pamięci podręcznej preferencji** ustawiono zbyt**Brak**.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-139">Make sure that **Host Cache Preference** is set too**None**.</span></span>  <span data-ttu-id="b3bb3-140">Po zakończeniu kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-140">When you're finished, click **OK**.</span></span>

![Dołącz pusty dysk](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


<span data-ttu-id="b3bb3-142">Spowoduje to dodanie jednego pusty dysk do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-142">This adds one empty disk into your virtual machine.</span></span> <span data-ttu-id="b3bb3-143">Powtórz ten krok trzy razy, aby mieć cztery dyski danych macierzy RAID.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-143">Repeat this step three more times so that you have four data disks for RAID.</span></span>  

<span data-ttu-id="b3bb3-144">Zostanie wyświetlony hello dodane dyski na maszynie wirtualnej hello analizując hello jądra wiadomości dziennika.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-144">You can see hello added drives in hello virtual machine by looking at hello kernel message log.</span></span> <span data-ttu-id="b3bb3-145">Na przykład toosee to na Ubuntu, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="b3bb3-145">For example, toosee this on Ubuntu, use hello following command:</span></span>  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-hello-additional-disks"></a><span data-ttu-id="b3bb3-146">Utwórz RAID z hello dodatkowych dysków</span><span class="sxs-lookup"><span data-stu-id="b3bb3-146">Create RAID with hello additional disks</span></span>
<span data-ttu-id="b3bb3-147">Witaj poniższych krokach opisano sposób zbyt[należy skonfigurować oprogramowanie RAID w systemie Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b3bb3-147">hello following steps describe how too[configure software RAID on Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="b3bb3-148">Jeśli używasz systemu plików XFS hello wykonać powitania po utworzeniu RAID wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-148">If you are using hello XFS file system, execute hello following steps after you have created RAID.</span></span>
>
>

<span data-ttu-id="b3bb3-149">tooinstall XFS na Debian, Ubuntu lub mennic Linux hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="b3bb3-149">tooinstall XFS on Debian, Ubuntu, or Linux Mint, use hello following command:</span></span>  

    apt-get -y install xfsprogs  

<span data-ttu-id="b3bb3-150">tooinstall XFS na Fedora, CentOS lub RHEL, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="b3bb3-150">tooinstall XFS on Fedora, CentOS, or RHEL, use hello following command:</span></span>  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a><span data-ttu-id="b3bb3-151">Konfigurowanie nowej ścieżki do magazynu</span><span class="sxs-lookup"><span data-stu-id="b3bb3-151">Set up a new storage path</span></span>
<span data-ttu-id="b3bb3-152">Witaj Użyj następującego polecenia tooset ścieżkę nowego magazynu:</span><span class="sxs-lookup"><span data-stu-id="b3bb3-152">Use hello following command tooset up a new storage path:</span></span>  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-hello-original-data-toohello-new-storage-path"></a><span data-ttu-id="b3bb3-153">Skopiuj hello oryginalne dane toohello nowej ścieżki do magazynu</span><span class="sxs-lookup"><span data-stu-id="b3bb3-153">Copy hello original data toohello new storage path</span></span>
<span data-ttu-id="b3bb3-154">Witaj Użyj następującego polecenia toocopy danych toohello nowej ścieżki do magazynu:</span><span class="sxs-lookup"><span data-stu-id="b3bb3-154">Use hello following command toocopy data toohello new storage path:</span></span>  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-hello-data-disk"></a><span data-ttu-id="b3bb3-155">Modyfikowanie uprawnień dostępu do MySQL (odczytu i zapisu) hello dysk danych</span><span class="sxs-lookup"><span data-stu-id="b3bb3-155">Modify permissions so MySQL can access (read and write) hello data disk</span></span>
<span data-ttu-id="b3bb3-156">Użyj następujących uprawnień toomodify polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="b3bb3-156">Use hello following command toomodify permissions:</span></span>  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-hello-disk-io-scheduling-algorithm"></a><span data-ttu-id="b3bb3-157">Dostosuj planowania algorytm we/wy hello dysku</span><span class="sxs-lookup"><span data-stu-id="b3bb3-157">Adjust hello disk I/O scheduling algorithm</span></span>
<span data-ttu-id="b3bb3-158">Linux implementuje cztery typy operacji We/Wy planowania algorytmów:</span><span class="sxs-lookup"><span data-stu-id="b3bb3-158">Linux implements four types of I/O scheduling algorithms:</span></span>  

* <span data-ttu-id="b3bb3-159">Operacja algorytm (operacja: No)</span><span class="sxs-lookup"><span data-stu-id="b3bb3-159">NOOP algorithm (No Operation)</span></span>
* <span data-ttu-id="b3bb3-160">Algorytm ostateczny termin (terminu)</span><span class="sxs-lookup"><span data-stu-id="b3bb3-160">Deadline algorithm (Deadline)</span></span>
* <span data-ttu-id="b3bb3-161">Całkowicie odpowiedniego algorytmu kolejkowania wiadomości (CFQ)</span><span class="sxs-lookup"><span data-stu-id="b3bb3-161">Completely fair queuing algorithm (CFQ)</span></span>
* <span data-ttu-id="b3bb3-162">Algorytm okresu budżetu (Anticipatory)</span><span class="sxs-lookup"><span data-stu-id="b3bb3-162">Budget period algorithm (Anticipatory)</span></span>  

<span data-ttu-id="b3bb3-163">Można wybrać różne planiści we/wy w różnych scenariuszy toooptimize wydajności.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-163">You can select different I/O schedulers under different scenarios toooptimize performance.</span></span> <span data-ttu-id="b3bb3-164">W środowisku dostępu losowy nie istnieje znacząca różnica między hello CFQ i algorytmy terminu wydajności.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-164">In a completely random access environment, there is not a significant difference between hello CFQ and Deadline algorithms for performance.</span></span> <span data-ttu-id="b3bb3-165">Firma Microsoft zaleca ustawienie hello MySQL bazy danych środowiska tooDeadline stabilności.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-165">We recommend that you set hello MySQL database environment tooDeadline for stability.</span></span> <span data-ttu-id="b3bb3-166">W przypadku partii sekwencyjnych operacji We/Wy, CFQ może zmniejszyć wydajność We/Wy dysku.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-166">If there is a lot of sequential I/O, CFQ might reduce disk I/O performance.</span></span>   

<span data-ttu-id="b3bb3-167">Dysków SSD i innych urządzeń operacja lub ostatecznego terminu można osiągnąć lepszą wydajność niż hello domyślnego harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-167">For SSD and other equipment, NOOP or Deadline can achieve better performance than hello default scheduler.</span></span>   

<span data-ttu-id="b3bb3-168">Wcześniejsze toohello jądra 2.5, planowania algorytm hello domyślne we/wy jest terminu.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-168">Prior toohello kernel 2.5, hello default I/O scheduling algorithm is Deadline.</span></span> <span data-ttu-id="b3bb3-169">Począwszy od jądra hello 2.6.18 CFQ stał się we/wy hello domyślny algorytm planowania.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-169">Starting with hello kernel 2.6.18, CFQ became hello default I/O scheduling algorithm.</span></span>  <span data-ttu-id="b3bb3-170">Można określić tego ustawienia w czasie rozruchu jądra lub dynamicznie zmodyfikować to ustawienie, gdy hello w systemie.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-170">You can specify this setting at kernel boot time or dynamically modify this setting when hello system is running.</span></span>  

<span data-ttu-id="b3bb3-171">Witaj poniższy przykład pokazuje, jak domyślny harmonogram toohello operacja algorytm rodziny Debian dystrybucji hello hello toocheck i zestawu.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-171">hello following example demonstrates how toocheck and set hello default scheduler toohello NOOP algorithm in hello Debian distribution family.</span></span>  

### <a name="view-hello-current-io-scheduler"></a><span data-ttu-id="b3bb3-172">Widok hello bieżącego harmonogramu we/wy</span><span class="sxs-lookup"><span data-stu-id="b3bb3-172">View hello current I/O scheduler</span></span>
<span data-ttu-id="b3bb3-173">Harmonogram hello tooview Uruchom hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b3bb3-173">tooview hello scheduler run hello following command:</span></span>  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

<span data-ttu-id="b3bb3-174">Zostaną wyświetlone następujące dane wyjściowe, co oznacza hello bieżącego harmonogramu:</span><span class="sxs-lookup"><span data-stu-id="b3bb3-174">You will see following output, which indicates hello current scheduler:</span></span>  

    noop [deadline] cfq


### <a name="change-hello-current-device-devsda-of-hello-io-scheduling-algorithm"></a><span data-ttu-id="b3bb3-175">Zmień hello bieżącego urządzenia (/ dev/sda) algorytmu planowania hello we/wy</span><span class="sxs-lookup"><span data-stu-id="b3bb3-175">Change hello current device (/dev/sda) of hello I/O scheduling algorithm</span></span>
<span data-ttu-id="b3bb3-176">Uruchom następujące polecenia toochange hello bieżącego urządzenia hello:</span><span class="sxs-lookup"><span data-stu-id="b3bb3-176">Run hello following commands toochange hello current device:</span></span>  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> <span data-ttu-id="b3bb3-177">Ustawienie to dla /dev/sda nie jest użyteczne.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-177">Setting this for /dev/sda alone is not useful.</span></span> <span data-ttu-id="b3bb3-178">Należy ją ustawić na wszystkich dyskach danych lokalizację hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-178">It must be set on all data disks where hello database resides.</span></span>  
>
>

<span data-ttu-id="b3bb3-179">Powinny pojawić się hello następujące dane wyjściowe, wskazując, że grub.cfg został przebudowany pomyślnie i tym hello domyślny harmonogram został zaktualizowany tooNOOP:</span><span class="sxs-lookup"><span data-stu-id="b3bb3-179">You should see hello following output, indicating that grub.cfg has been rebuilt successfully and that hello default scheduler has been updated tooNOOP:</span></span>  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

<span data-ttu-id="b3bb3-180">Dla hello Red Hat dystrybucji rodziny należy tylko hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b3bb3-180">For hello Red Hat distribution family, you need only hello following command:</span></span>

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a><span data-ttu-id="b3bb3-181">Skonfiguruj ustawienia operacji pliku systemu</span><span class="sxs-lookup"><span data-stu-id="b3bb3-181">Configure system file operations settings</span></span>
<span data-ttu-id="b3bb3-182">Jeden najlepszym rozwiązaniem jest toodisable hello *atime* funkcji rejestrowania w systemie plików hello.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-182">One best practice is toodisable hello *atime* logging feature on hello file system.</span></span> <span data-ttu-id="b3bb3-183">Atime jest hello czas ostatniego dostępu do pliku.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-183">Atime is hello last file access time.</span></span> <span data-ttu-id="b3bb3-184">Zawsze, gdy plik jest dostępny, rekordy systemu plików hello hello sygnatury czasowej w dzienniku hello.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-184">Whenever a file is accessed, hello file system records hello timestamp in hello log.</span></span> <span data-ttu-id="b3bb3-185">Jednak te informacje jest rzadko używana.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-185">However, this information is rarely used.</span></span> <span data-ttu-id="b3bb3-186">Można ją wyłączyć, jeśli nie jest potrzebna, co zmniejsza całkowity czas dostępu do dysku.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-186">You can disable it if you don't need it, which will reduce overall disk access time.</span></span>  

<span data-ttu-id="b3bb3-187">toodisable atime rejestrowanie, należy toomodify hello pliku system konfiguracji plik/etc / fstab i dodać hello **noatime** opcji.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-187">toodisable atime logging, you need toomodify hello file system configuration file /etc/ fstab and add hello **noatime** option.</span></span>  

<span data-ttu-id="b3bb3-188">Na przykład Edytuj plik /etc/fstab vim hello Dodawanie hello noatime, jak pokazano w hello następujące przykładowe:</span><span class="sxs-lookup"><span data-stu-id="b3bb3-188">For example, edit hello vim /etc/fstab file, adding hello noatime as shown in hello following sample:</span></span>  

    # CLOUD_IMG: This file was created/modified by hello Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add hello “noatime” option below toodisable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

<span data-ttu-id="b3bb3-189">Następnie zainstaluj system plików hello z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b3bb3-189">Then, remount hello file system with hello following command:</span></span>  

    mount -o remount /RAID0

<span data-ttu-id="b3bb3-190">Test hello zmodyfikować wyniku.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-190">Test hello modified result.</span></span> <span data-ttu-id="b3bb3-191">Po zmodyfikowaniu pliku testowego hello hello czas dostępu nie jest aktualizowana.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-191">When you modify hello test file, hello access time is not updated.</span></span> <span data-ttu-id="b3bb3-192">Witaj w następujących przykładach, jaki kod hello wygląda przed i po modyfikacji.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-192">hello following examples show what hello code looks like before and after modification.</span></span>

<span data-ttu-id="b3bb3-193">Przed:</span><span class="sxs-lookup"><span data-stu-id="b3bb3-193">Before:</span></span>        

![Kod przed modyfikacją dostępu][5]

<span data-ttu-id="b3bb3-195">Po:</span><span class="sxs-lookup"><span data-stu-id="b3bb3-195">After:</span></span>

![Kod po modyfikacji dostępu][6]

## <a name="increase-hello-maximum-number-of-system-handles-for-high-concurrency"></a><span data-ttu-id="b3bb3-197">Zwiększ hello maksymalną liczbę systemu obsługuje dla wysokiej współbieżności</span><span class="sxs-lookup"><span data-stu-id="b3bb3-197">Increase hello maximum number of system handles for high concurrency</span></span>
<span data-ttu-id="b3bb3-198">MySQL jest wysoka współbieżności bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-198">MySQL is a high concurrency database.</span></span> <span data-ttu-id="b3bb3-199">Hello domyślna liczba równoczesnych dojścia jest 1024 dla systemu Linux, które nie zawsze jest wystarczające.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-199">hello default number of concurrent handles is 1024 for Linux, which is not always sufficient.</span></span> <span data-ttu-id="b3bb3-200">Użyj hello następujące kroki tooincrease hello maksymalną równoczesnych uchwyty hello systemu toosupport wysokiej współbieżności MySQL.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-200">Use hello following steps tooincrease hello maximum concurrent handles of hello system toosupport high concurrency of MySQL.</span></span>

### <a name="modify-hello-limitsconf-file"></a><span data-ttu-id="b3bb3-201">Modyfikowanie pliku limits.conf hello</span><span class="sxs-lookup"><span data-stu-id="b3bb3-201">Modify hello limits.conf file</span></span>
<span data-ttu-id="b3bb3-202">tooincrease hello maksymalna dozwolona współbieżnych dojść, Dodaj następujące cztery wiersze w pliku /etc/security/limits.conf hello hello.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-202">tooincrease hello maximum allowed concurrent handles, add hello following four lines in hello /etc/security/limits.conf file.</span></span> <span data-ttu-id="b3bb3-203">Należy pamiętać, że 65536 hello maksymalną liczbę obsługujących hello systemu.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-203">Note that 65536 is hello maximum number that hello system can support.</span></span>   

    * <span data-ttu-id="b3bb3-204">elastyczne nofile 65536</span><span class="sxs-lookup"><span data-stu-id="b3bb3-204">soft nofile 65536</span></span>
    * <span data-ttu-id="b3bb3-205">twarde nofile 65536</span><span class="sxs-lookup"><span data-stu-id="b3bb3-205">hard nofile 65536</span></span>
    * <span data-ttu-id="b3bb3-206">elastyczne nproc 65536</span><span class="sxs-lookup"><span data-stu-id="b3bb3-206">soft nproc 65536</span></span>
    * <span data-ttu-id="b3bb3-207">twarde nproc 65536</span><span class="sxs-lookup"><span data-stu-id="b3bb3-207">hard nproc 65536</span></span>

### <a name="update-hello-system-for-hello-new-limits"></a><span data-ttu-id="b3bb3-208">Zaktualizuj system hello hello nowych limitów</span><span class="sxs-lookup"><span data-stu-id="b3bb3-208">Update hello system for hello new limits</span></span>
<span data-ttu-id="b3bb3-209">tooupdate hello systemu, uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="b3bb3-209">tooupdate hello system, run hello following commands:</span></span>  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-hello-limits-are-updated-at-boot-time"></a><span data-ttu-id="b3bb3-210">Upewnij się, że limity hello są aktualizowane w czasie rozruchu</span><span class="sxs-lookup"><span data-stu-id="b3bb3-210">Ensure that hello limits are updated at boot time</span></span>
<span data-ttu-id="b3bb3-211">Umieść powitania po uruchamiania poleceń w pliku /etc/rc.local hello tak zacznie obowiązywać w czasie rozruchu.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-211">Put hello following startup commands in hello /etc/rc.local file so it will take effect at boot time.</span></span>  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a><span data-ttu-id="b3bb3-212">Optymalizacja bazy danych MySQL</span><span class="sxs-lookup"><span data-stu-id="b3bb3-212">MySQL database optimization</span></span>
<span data-ttu-id="b3bb3-213">tooconfigure MySQL na platformie Azure, można użyć hello tej samej strategii dostrajania wydajności używany na maszynie lokalnej.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-213">tooconfigure MySQL on Azure, you can use hello same performance-tuning strategy you use on an on-premises machine.</span></span>  

<span data-ttu-id="b3bb3-214">Witaj głównego we/wy optymalizacji reguły są następujące:</span><span class="sxs-lookup"><span data-stu-id="b3bb3-214">hello main I/O optimization rules are:</span></span>   

* <span data-ttu-id="b3bb3-215">Zwiększ rozmiar pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-215">Increase hello cache size.</span></span>
* <span data-ttu-id="b3bb3-216">Zmniejsz we/wy, czas odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-216">Reduce I/O response time.</span></span>  

<span data-ttu-id="b3bb3-217">ustawienia serwera MySQL toooptimize, należy zaktualizować hello my.cnf pliku, który jest hello domyślny plik konfiguracji dla komputerów klienckich i serwera.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-217">toooptimize MySQL server settings, you can update hello my.cnf file, which is hello default configuration file for both server and client computers.</span></span>  

<span data-ttu-id="b3bb3-218">Witaj konfiguracji są następujące elementy hello główne czynniki wpływające na wydajność MySQL:</span><span class="sxs-lookup"><span data-stu-id="b3bb3-218">hello following configuration items are hello main factors that affect MySQL performance:</span></span>  

* <span data-ttu-id="b3bb3-219">**innodb_buffer_pool_size**: hello Pula buforów zawiera buforowane dane i hello indeksu.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-219">**innodb_buffer_pool_size**: hello buffer pool contains buffered data and hello index.</span></span> <span data-ttu-id="b3bb3-220">Jest to zwykle ustawione too70 procent pamięci fizycznej.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-220">This is usually set too70 percent of physical memory.</span></span>
* <span data-ttu-id="b3bb3-221">**innodb_log_file_size**: rozmiar dziennika Powtórz hello.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-221">**innodb_log_file_size**: This is hello redo log size.</span></span> <span data-ttu-id="b3bb3-222">Możesz użyć Powtórz tooensure dzienniki, czy operacje zapisu są szybkie, niezawodne i możliwe do odzyskania po awarii.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-222">You use redo logs tooensure that write operations are fast, reliable, and recoverable after a crash.</span></span> <span data-ttu-id="b3bb3-223">To jest ustawienie too512 MB, co zapewni wystarczająco dużo miejsca do rejestrowania operacji zapisu.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-223">This is set too512 MB, which will give you plenty of space for logging write operations.</span></span>
* <span data-ttu-id="b3bb3-224">**max_connections**: czasami aplikacje nie zamykaj połączeń poprawnie.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-224">**max_connections**: Sometimes applications do not close connections properly.</span></span> <span data-ttu-id="b3bb3-225">Im większa wartość zapewni powitania serwera więcej czasu toorecycle idled połączenia.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-225">A larger value will give hello server more time toorecycle idled connections.</span></span> <span data-ttu-id="b3bb3-226">Maksymalna liczba połączeń Hello jest 10 000, ale hello zaleca się, że liczba maksymalna to 5000.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-226">hello maximum number of connections is 10,000, but hello recommended maximum is 5,000.</span></span>
* <span data-ttu-id="b3bb3-227">**Innodb_file_per_table**: to ustawienie włącza lub wyłącza możliwość hello InnoDB toostore tabel w oddzielnych plikach.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-227">**Innodb_file_per_table**: This setting enables or disables hello ability of InnoDB toostore tables in separate files.</span></span> <span data-ttu-id="b3bb3-228">Włącz tooensure opcji hello wydajnie zastosować kilka operacji zaawansowane administracji.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-228">Turn on hello option tooensure that several advanced administration operations can be applied efficiently.</span></span> <span data-ttu-id="b3bb3-229">Z punktu widzenia wydajności można przyspieszyć hello tabeli miejsca transmisji i optymalizowanie zarządzania pozostałości hello.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-229">From a performance point of view, it can speed up hello table space transmission and optimize hello debris management performance.</span></span> <span data-ttu-id="b3bb3-230">Witaj zaleca się, że ustawienie dla tej opcji jest włączone.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-230">hello recommended setting for this option is ON.</span></span></br></br>
<span data-ttu-id="b3bb3-231">Z MySQL 5.6 hello domyślne ustawienie ma wartość ON, więc nie jest wymagana żadna akcja.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-231">From MySQL 5.6, hello default setting is ON, so no action is required.</span></span> <span data-ttu-id="b3bb3-232">We wcześniejszych wersjach hello domyślne ustawienie ma wartość OFF.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-232">For earlier versions, hello default setting is OFF.</span></span> <span data-ttu-id="b3bb3-233">Ustawienie Hello należy zmienić przed załadowaniem danych, ponieważ dotyczy tylko tabele nowo utworzony.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-233">hello setting should be changed before data is loaded, because only newly created tables are affected.</span></span>
* <span data-ttu-id="b3bb3-234">**innodb_flush_log_at_trx_commit**: hello wartość domyślna to 1, z hello zakresu Ustaw too0 ~ 2.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-234">**innodb_flush_log_at_trx_commit**: hello default value is 1, with hello scope set too0~2.</span></span> <span data-ttu-id="b3bb3-235">Wartość domyślna Hello jest hello najbardziej odpowiednią opcją do autonomicznej bazy danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-235">hello default value is hello most suitable option for standalone MySQL DB.</span></span> <span data-ttu-id="b3bb3-236">Ustawienie Hello 2 umożliwia hello większości integralność danych i nadaje się do głównego w klaster programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-236">hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL Cluster.</span></span> <span data-ttu-id="b3bb3-237">Ustawienie Hello 0 umożliwia utraty danych, które mogą wpłynąć na niezawodność (w niektórych przypadkach z lepszą wydajność) i nadaje się do podrzędnych w klaster programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-237">hello setting of 0 allows data loss, which can affect reliability (in some cases with better performance), and is suitable for Slave in MySQL Cluster.</span></span>
* <span data-ttu-id="b3bb3-238">**Innodb_log_buffer_size**: hello dziennika buforu umożliwia toorun transakcji bez konieczności tooflush hello dziennika toodisk przed hello transakcji zatwierdzania.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-238">**Innodb_log_buffer_size**: hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit.</span></span> <span data-ttu-id="b3bb3-239">Jednak jeśli istnieje dużego obiektu binarnego lub pola tekstowego, hello pamięci podręcznej będą działały szybko i we/wy dysku częste zostanie wyzwolony.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-239">However, if there is large binary object or text field, hello cache will be consumed quickly and frequent disk I/O will be triggered.</span></span> <span data-ttu-id="b3bb3-240">Jest lepiej Zwiększ rozmiar buforu hello, jeśli Innodb_log_waits zmiennej stanu nie jest 0.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-240">It is better increase hello buffer size if Innodb_log_waits state variable is not 0.</span></span>
* <span data-ttu-id="b3bb3-241">**query_cache_size**: hello najlepszym rozwiązaniem jest toodisable go z początku hello.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-241">**query_cache_size**: hello best option is toodisable it from hello outset.</span></span> <span data-ttu-id="b3bb3-242">Ustaw too0 query_cache_size (jest to domyślne ustawienie hello MySQL 5.6) i używać innych metod toospeed się zapytania.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-242">Set query_cache_size too0 (this is hello default setting in MySQL 5.6) and use other methods toospeed up queries.</span></span>  

<span data-ttu-id="b3bb3-243">Zobacz [dodatku D](#AppendixD) porównanie wydajności przed i po hello optymalizacji.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-243">See [Appendix D](#AppendixD) for a comparison of performance before and after hello optimization.</span></span>

## <a name="turn-on-hello-mysql-slow-query-log-for-analyzing-hello-performance-bottleneck"></a><span data-ttu-id="b3bb3-244">Włącz dziennik powolne zapytań MySQL hello do analizowania hello wąskie gardło</span><span class="sxs-lookup"><span data-stu-id="b3bb3-244">Turn on hello MySQL slow query log for analyzing hello performance bottleneck</span></span>
<span data-ttu-id="b3bb3-245">Dziennik zapytań powolne MySQL Hello pomaga określić hello powolne zapytania dla programu MySQL.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-245">hello MySQL slow query log can help you identify hello slow queries for MySQL.</span></span> <span data-ttu-id="b3bb3-246">Po włączeniu dziennika powolne zapytania MySQL hello, można użyć narzędzia MySQL, takie jak **mysqldumpslow** tooidentify hello wąskie gardło.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-246">After enabling hello MySQL slow query log, you can use MySQL tools like **mysqldumpslow** tooidentify hello performance bottleneck.</span></span>  

<span data-ttu-id="b3bb3-247">Domyślnie to nie jest włączona.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-247">By default, this is not enabled.</span></span> <span data-ttu-id="b3bb3-248">Włączanie dziennika powolne zapytania hello może używać niektórych zasobów Procesora.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-248">Turning on hello slow query log might consume some CPU resources.</span></span> <span data-ttu-id="b3bb3-249">Zaleca się włączenie to tymczasowo do rozwiązywania problemów wąskich gardeł wydajności.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-249">We recommend that you enable this temporarily for troubleshooting performance bottlenecks.</span></span> <span data-ttu-id="b3bb3-250">tooturn na dziennik powolne zapytań hello:</span><span class="sxs-lookup"><span data-stu-id="b3bb3-250">tooturn on hello slow query log:</span></span>

1. <span data-ttu-id="b3bb3-251">Zmodyfikuj hello my.cnf przez dodanie hello zakończenia toohello wiersze:</span><span class="sxs-lookup"><span data-stu-id="b3bb3-251">Modify hello my.cnf file by adding hello following lines toohello end:</span></span>

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. <span data-ttu-id="b3bb3-252">Uruchom ponownie serwer MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-252">Restart hello MySQL server.</span></span>

        service  mysql  restart

3. <span data-ttu-id="b3bb3-253">Sprawdź, czy ustawienie hello jest wpływają przy użyciu hello **Pokaż** polecenia.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-253">Check whether hello setting is taking effect by using hello **show** command.</span></span>

![Powolna zapytania dziennika na][7]   

![Powolna zapytania dziennika wyników][8]

<span data-ttu-id="b3bb3-256">W tym przykładzie można zauważyć, że tej funkcji powolne zapytania hello został włączony.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-256">In this example, you can see that hello slow query feature has been turned on.</span></span> <span data-ttu-id="b3bb3-257">Następnie można użyć hello **mysqldumpslow** narzędzia toodetermine wąskich gardeł wydajności i optymalizacji wydajności, takie jak dodanie indeksów.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-257">You can then use hello **mysqldumpslow** tool toodetermine performance bottlenecks and optimize performance, such as adding indexes.</span></span>

## <a name="appendices"></a><span data-ttu-id="b3bb3-258">Dodatki</span><span class="sxs-lookup"><span data-stu-id="b3bb3-258">Appendices</span></span>
<span data-ttu-id="b3bb3-259">Witaj poniżej przedstawiono przykładowe wydajności testu dane utworzone w środowisku laboratoryjnym docelowych.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-259">hello following are sample performance test data produced in a targeted lab environment.</span></span> <span data-ttu-id="b3bb3-260">Zapewniają ogólne na trend danych wydajności hello z różnych dostrajanie podejścia wydajności.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-260">They provide general background on hello performance data trend with different performance tuning approaches.</span></span> <span data-ttu-id="b3bb3-261">wyniki Hello mogą różnić się w różnych wersjach środowiska lub produkt.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-261">hello results might vary under different environment or product versions.</span></span>

### <span data-ttu-id="b3bb3-262"><a name="AppendixA"></a>Dodatek A</span><span class="sxs-lookup"><span data-stu-id="b3bb3-262"><a name="AppendixA"></a>Appendix A</span></span>  
<span data-ttu-id="b3bb3-263">**Wydajność dysku (IOPS) z różnych poziomów macierzy RAID**</span><span class="sxs-lookup"><span data-stu-id="b3bb3-263">**Disk performance (IOPS) with different RAID levels**</span></span>

![Dysk IOPS z różnych poziomów macierzy RAID][9]

<span data-ttu-id="b3bb3-265">**Polecenia testu**</span><span class="sxs-lookup"><span data-stu-id="b3bb3-265">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> <span data-ttu-id="b3bb3-266">Obciążenie Hello tego testu używa 64 wątki w trakcie tooreach hello górny limit RAID.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-266">hello workload of this test uses 64 threads, trying tooreach hello upper limit of RAID.</span></span>
>
>

### <span data-ttu-id="b3bb3-267"><a name="AppendixB"></a>Dodatek B</span><span class="sxs-lookup"><span data-stu-id="b3bb3-267"><a name="AppendixB"></a>Appendix B</span></span>  
<span data-ttu-id="b3bb3-268">**Porównanie wydajności (przepływność) MySQL z różnych poziomów macierzy RAID** </span><span class="sxs-lookup"><span data-stu-id="b3bb3-268">**MySQL performance (throughput) comparison with different RAID levels** </span></span>  
<span data-ttu-id="b3bb3-269">(XFS w systemie plików)</span><span class="sxs-lookup"><span data-stu-id="b3bb3-269">(XFS file system)</span></span>

![Porównanie wydajności MySQL z różnych poziomów macierzy RAID][10]  
![Porównanie wydajności MySQL z różnych poziomów macierzy RAID][11]

<span data-ttu-id="b3bb3-272">**Polecenia testu**</span><span class="sxs-lookup"><span data-stu-id="b3bb3-272">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

<span data-ttu-id="b3bb3-273">**Porównanie wydajności (OLTP) MySQL z różnych poziomów macierzy RAID**</span><span class="sxs-lookup"><span data-stu-id="b3bb3-273">**MySQL performance (OLTP) comparison with different RAID levels**</span></span>  
<span data-ttu-id="b3bb3-274">![Porównanie wydajności (OLTP) MySQL z różnych poziomów macierzy RAID][12]</span><span class="sxs-lookup"><span data-stu-id="b3bb3-274">![MySQL performance (OLTP) comparison with different RAID levels][12]</span></span>

<span data-ttu-id="b3bb3-275">**Polecenia testu**</span><span class="sxs-lookup"><span data-stu-id="b3bb3-275">**Test commands**</span></span>

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <span data-ttu-id="b3bb3-276"><a name="AppendixC"></a>Dodatek C</span><span class="sxs-lookup"><span data-stu-id="b3bb3-276"><a name="AppendixC"></a>Appendix C</span></span>   
<span data-ttu-id="b3bb3-277">**Dysk porównanie wydajności (IOPS) dla różnych rozmiarach**</span><span class="sxs-lookup"><span data-stu-id="b3bb3-277">**Disk performance (IOPS) comparison for different chunk sizes**</span></span>  
<span data-ttu-id="b3bb3-278">(XFS w systemie plików)</span><span class="sxs-lookup"><span data-stu-id="b3bb3-278">(XFS file system)</span></span>

![][13]

<span data-ttu-id="b3bb3-279">**Polecenia testu**</span><span class="sxs-lookup"><span data-stu-id="b3bb3-279">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

<span data-ttu-id="b3bb3-280">rozmiary plików Hello używać do testowania tego 30 GB i 1 GB, odpowiednio, macierz RAID 0 (4 dyski) XFS systemu plików.</span><span class="sxs-lookup"><span data-stu-id="b3bb3-280">hello file sizes used for this testing are 30 GB and 1 GB, respectively, with RAID 0 (4 disks) XFS file system.</span></span>

### <span data-ttu-id="b3bb3-281"><a name="AppendixD"></a>Dodatek D</span><span class="sxs-lookup"><span data-stu-id="b3bb3-281"><a name="AppendixD"></a>Appendix D</span></span>  
<span data-ttu-id="b3bb3-282">**Porównanie wydajności (przepływność) MySQL przed i po optymalizacji**</span><span class="sxs-lookup"><span data-stu-id="b3bb3-282">**MySQL performance (throughput) comparison before and after optimization**</span></span>  
<span data-ttu-id="b3bb3-283">(XFS File System)</span><span class="sxs-lookup"><span data-stu-id="b3bb3-283">(XFS File System)</span></span>

![Porównanie wydajności (przepływność) MySQL przed i po optymalizacji][14]

<span data-ttu-id="b3bb3-285">**Polecenia testu**</span><span class="sxs-lookup"><span data-stu-id="b3bb3-285">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

<span data-ttu-id="b3bb3-286">**Ustawienie konfiguracji Hello w domyślnej i optymalizacji wygląda następująco:**</span><span class="sxs-lookup"><span data-stu-id="b3bb3-286">**hello configuration setting for default and optimization is as follows:**</span></span>

| <span data-ttu-id="b3bb3-287">Parametry</span><span class="sxs-lookup"><span data-stu-id="b3bb3-287">Parameters</span></span> | <span data-ttu-id="b3bb3-288">Domyślne</span><span class="sxs-lookup"><span data-stu-id="b3bb3-288">Default</span></span> | <span data-ttu-id="b3bb3-289">Optymalizacja</span><span class="sxs-lookup"><span data-stu-id="b3bb3-289">Optimization</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b3bb3-290">**innodb_buffer_pool_size**</span><span class="sxs-lookup"><span data-stu-id="b3bb3-290">**innodb_buffer_pool_size**</span></span> |<span data-ttu-id="b3bb3-291">Brak</span><span class="sxs-lookup"><span data-stu-id="b3bb3-291">None</span></span> |<span data-ttu-id="b3bb3-292">7 GB</span><span class="sxs-lookup"><span data-stu-id="b3bb3-292">7 GB</span></span> |
| <span data-ttu-id="b3bb3-293">**innodb_log_file_size**</span><span class="sxs-lookup"><span data-stu-id="b3bb3-293">**innodb_log_file_size**</span></span> |<span data-ttu-id="b3bb3-294">5 MB</span><span class="sxs-lookup"><span data-stu-id="b3bb3-294">5 MB</span></span> |<span data-ttu-id="b3bb3-295">512 MB</span><span class="sxs-lookup"><span data-stu-id="b3bb3-295">512 MB</span></span> |
| <span data-ttu-id="b3bb3-296">**max_connections**</span><span class="sxs-lookup"><span data-stu-id="b3bb3-296">**max_connections**</span></span> |<span data-ttu-id="b3bb3-297">100</span><span class="sxs-lookup"><span data-stu-id="b3bb3-297">100</span></span> |<span data-ttu-id="b3bb3-298">5000</span><span class="sxs-lookup"><span data-stu-id="b3bb3-298">5000</span></span> |
| <span data-ttu-id="b3bb3-299">**innodb_file_per_table**</span><span class="sxs-lookup"><span data-stu-id="b3bb3-299">**innodb_file_per_table**</span></span> |<span data-ttu-id="b3bb3-300">0</span><span class="sxs-lookup"><span data-stu-id="b3bb3-300">0</span></span> |<span data-ttu-id="b3bb3-301">1</span><span class="sxs-lookup"><span data-stu-id="b3bb3-301">1</span></span> |
| <span data-ttu-id="b3bb3-302">**innodb_flush_log_at_trx_commit**</span><span class="sxs-lookup"><span data-stu-id="b3bb3-302">**innodb_flush_log_at_trx_commit**</span></span> |<span data-ttu-id="b3bb3-303">1</span><span class="sxs-lookup"><span data-stu-id="b3bb3-303">1</span></span> |<span data-ttu-id="b3bb3-304">2</span><span class="sxs-lookup"><span data-stu-id="b3bb3-304">2</span></span> |
| <span data-ttu-id="b3bb3-305">**innodb_log_buffer_size**</span><span class="sxs-lookup"><span data-stu-id="b3bb3-305">**innodb_log_buffer_size**</span></span> |<span data-ttu-id="b3bb3-306">8 MB</span><span class="sxs-lookup"><span data-stu-id="b3bb3-306">8 MB</span></span> |<span data-ttu-id="b3bb3-307">128 MB</span><span class="sxs-lookup"><span data-stu-id="b3bb3-307">128 MB</span></span> |
| <span data-ttu-id="b3bb3-308">**query_cache_size**</span><span class="sxs-lookup"><span data-stu-id="b3bb3-308">**query_cache_size**</span></span> |<span data-ttu-id="b3bb3-309">16 MB</span><span class="sxs-lookup"><span data-stu-id="b3bb3-309">16 MB</span></span> |<span data-ttu-id="b3bb3-310">0</span><span class="sxs-lookup"><span data-stu-id="b3bb3-310">0</span></span> |

<span data-ttu-id="b3bb3-311">Aby uzyskać bardziej szczegółowe [parametry konfiguracji optymalizacji](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), można znaleźć toohello [instrukcje oficjalnego MySQL](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span><span class="sxs-lookup"><span data-stu-id="b3bb3-311">For more detailed [optimization configuration parameters](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), refer toohello [MySQL official instructions](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span></span>  

  <span data-ttu-id="b3bb3-312">**Środowisko testowe**</span><span class="sxs-lookup"><span data-stu-id="b3bb3-312">**Test environment**</span></span>  

| <span data-ttu-id="b3bb3-313">Sprzęt</span><span class="sxs-lookup"><span data-stu-id="b3bb3-313">Hardware</span></span> | <span data-ttu-id="b3bb3-314">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="b3bb3-314">Details</span></span> |
| --- | --- |
| <span data-ttu-id="b3bb3-315">Procesor CPU</span><span class="sxs-lookup"><span data-stu-id="b3bb3-315">CPU</span></span> |<span data-ttu-id="b3bb3-316">AMD Opteron(tm) procesora 4171 HE / 4 rdzenie</span><span class="sxs-lookup"><span data-stu-id="b3bb3-316">AMD Opteron(tm) Processor 4171 HE/4 cores</span></span> |
| <span data-ttu-id="b3bb3-317">Memory (Pamięć)</span><span class="sxs-lookup"><span data-stu-id="b3bb3-317">Memory</span></span> |<span data-ttu-id="b3bb3-318">14 GB</span><span class="sxs-lookup"><span data-stu-id="b3bb3-318">14 GB</span></span> |
| <span data-ttu-id="b3bb3-319">Dysk</span><span class="sxs-lookup"><span data-stu-id="b3bb3-319">Disk</span></span> |<span data-ttu-id="b3bb3-320">10 GB/dysku</span><span class="sxs-lookup"><span data-stu-id="b3bb3-320">10 GB/disk</span></span> |
| <span data-ttu-id="b3bb3-321">System operacyjny</span><span class="sxs-lookup"><span data-stu-id="b3bb3-321">OS</span></span> |<span data-ttu-id="b3bb3-322">Ubuntu 14.04.1 LTS</span><span class="sxs-lookup"><span data-stu-id="b3bb3-322">Ubuntu 14.04.1 LTS</span></span> |

[1]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-01.png
[2]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-02.png
[3]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-03.png
[4]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-04.png
[5]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-05.png
[6]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-06.png
[7]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-07.png
[8]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-08.png
[9]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-09.png
[10]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-10.png
[11]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-11.png
[12]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-12.png
[13]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-13.png
[14]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-14.png

