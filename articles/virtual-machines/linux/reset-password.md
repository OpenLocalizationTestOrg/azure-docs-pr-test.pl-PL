---
title: "aaaHow tooreset Linux hasła lokalnego na maszynach wirtualnych Azure | Dokumentacja firmy Microsoft"
description: "Wprowadzenie hello kroki tooreset hello Linux hasła lokalnego na maszynie Wirtualnej Azure"
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: delhan
ms.openlocfilehash: b28a679a36bf93c6881633eefa03aef3cd33e804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-linux-password-on-azure-vms"></a><span data-ttu-id="66fe2-103">Jak hasło lokalne Linux tooreset na maszynach wirtualnych Azure</span><span class="sxs-lookup"><span data-stu-id="66fe2-103">How tooreset local Linux password on Azure VMs</span></span>

<span data-ttu-id="66fe2-104">W tym artykule przedstawiono kilka metod tooreset lokalnych maszyn wirtualnych systemu Linux (VM) hasła.</span><span class="sxs-lookup"><span data-stu-id="66fe2-104">This article introduces several methods tooreset local Linux Virtual Machine (VM) passwords.</span></span> <span data-ttu-id="66fe2-105">Jeśli konto użytkownika hello wygasło lub chcesz toocreate nowe konto, można użyć hello następujące metody toocreate nowe konto administratora lokalnego i ponowne uzyskanie dostępu toohello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="66fe2-105">If hello user account is expired or you just want toocreate a new account, you can use hello following methods toocreate a new local admin account and re-gain access toohello VM.</span></span>

## <a name="symptoms"></a><span data-ttu-id="66fe2-106">Objawy</span><span class="sxs-lookup"><span data-stu-id="66fe2-106">Symptoms</span></span>

<span data-ttu-id="66fe2-107">Nie można zalogować się toohello maszyny Wirtualnej i pojawi się komunikat, który wskazuje, że to hasło hello, który został użyty jest niepoprawny.</span><span class="sxs-lookup"><span data-stu-id="66fe2-107">You can't log in toohello VM, and you receive a message that indicates that hello password that you used is incorrect.</span></span> <span data-ttu-id="66fe2-108">Ponadto nie można użyć VMAgent tooreset hasła na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="66fe2-108">Additionally, you can't use VMAgent tooreset your password on hello Azure Portal.</span></span> 

## <a name="manual-password-reset-procedure"></a><span data-ttu-id="66fe2-109">Procedury ręcznego resetowania hasła</span><span class="sxs-lookup"><span data-stu-id="66fe2-109">Manual Password Reset procedure</span></span>

1.  <span data-ttu-id="66fe2-110">Usuń hello maszyny Wirtualnej i Zachowaj hello dołączonych dysków.</span><span class="sxs-lookup"><span data-stu-id="66fe2-110">Delete hello VM and keep hello attached disks.</span></span>

2.  <span data-ttu-id="66fe2-111">Dołącz hello dysk systemu operacyjnego jako tooanother dysku danych czasowych maszyny Wirtualnej w ramach hello tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="66fe2-111">Attach hello OS Drive as a data disk tooanother temporal VM in hello same location.</span></span>

3.  <span data-ttu-id="66fe2-112">Uruchom następujące polecenie SSH na powitania tymczasowa maszyna wirtualna toobecome hello nadtypem użytkownika.</span><span class="sxs-lookup"><span data-stu-id="66fe2-112">Run hello following SSH command on hello temporal VM toobecome a super-user.</span></span>


    ~~~~
    sudo su
    ~~~~

4.  <span data-ttu-id="66fe2-113">Uruchom **fdisk -l** lub przyjrzeć hello toofind dzienniki systemu nowo dołączono dysk.</span><span class="sxs-lookup"><span data-stu-id="66fe2-113">Run **fdisk -l** or look at system logs toofind hello newly attached disk.</span></span> <span data-ttu-id="66fe2-114">Zlokalizuj toomount nazwa dysku hello.</span><span class="sxs-lookup"><span data-stu-id="66fe2-114">Locate hello drive name toomount.</span></span> <span data-ttu-id="66fe2-115">Następnie na powitania danych czasowych maszyny Wirtualnej, poszukaj w odpowiednich hello pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="66fe2-115">Then on hello temporal VM, look in hello relevant log file.</span></span>

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    <span data-ttu-id="66fe2-116">Witaj poniżej przedstawiono przykładowe dane wyjściowe polecenia grep hello:</span><span class="sxs-lookup"><span data-stu-id="66fe2-116">hello following is example output of hello grep command:</span></span>

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  <span data-ttu-id="66fe2-117">Utwórz punkt instalacji o nazwie **tempmount**.</span><span class="sxs-lookup"><span data-stu-id="66fe2-117">Create a mount point called **tempmount**.</span></span>

    ~~~~
    mkdir /tempmount
    ~~~~

6.  <span data-ttu-id="66fe2-118">Zainstaluj dysk hello systemu operacyjnego w punkcie instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="66fe2-118">Mount hello OS disk on hello mount point.</span></span> <span data-ttu-id="66fe2-119">Zazwyczaj wymaga toomount sdc1 lub sdc2.</span><span class="sxs-lookup"><span data-stu-id="66fe2-119">You usually need toomount sdc1 or sdc2.</span></span> <span data-ttu-id="66fe2-120">Zależy to hello hosting partycji w katalogu/etc z hello maszyny uszkodzenie dysku.</span><span class="sxs-lookup"><span data-stu-id="66fe2-120">This will depend on hello hosting partition in /etc directory from hello broken machine disk.</span></span>

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  <span data-ttu-id="66fe2-121">Wykonaj kopię zapasową przed wprowadzeniem jakichkolwiek zmian:</span><span class="sxs-lookup"><span data-stu-id="66fe2-121">Perform a backup before making any changes:</span></span>

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  <span data-ttu-id="66fe2-122">Resetowanie hasła hello użytkownika, które są potrzebne:</span><span class="sxs-lookup"><span data-stu-id="66fe2-122">Reset hello user’s password that you need:</span></span>

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  <span data-ttu-id="66fe2-123">Przenieś hello zmodyfikowane pliki toohello właściwych lokalizacjach na powitania uszkodzony dysk na komputerze.</span><span class="sxs-lookup"><span data-stu-id="66fe2-123">Move hello modified files toohello correct location on hello broken machine's disk.</span></span>

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back toohello root and unmount hello disk.

    ~~~~
    <span data-ttu-id="66fe2-124">dysk CD / umount /tempmount</span><span class="sxs-lookup"><span data-stu-id="66fe2-124">cd / umount /tempmount</span></span>
    ~~~~

11. Detach hello disk from hello management portal.

12. Recreate hello VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk tooanother Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How toodelete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)
