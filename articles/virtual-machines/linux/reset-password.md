---
title: "Jak można zresetować hasła lokalnego systemu Linux na maszynach wirtualnych Azure | Dokumentacja firmy Microsoft"
description: "Wprowadzenie czynności, aby zresetować hasło lokalne systemu Linux na maszynie Wirtualnej Azure"
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
ms.openlocfilehash: bd48128a078821b7a4baa02d5d7ceecc6de99608
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-reset-local-linux-password-on-azure-vms"></a><span data-ttu-id="698e4-103">Jak można zresetować hasła lokalnego systemu Linux na maszynach wirtualnych Azure</span><span class="sxs-lookup"><span data-stu-id="698e4-103">How to reset local Linux password on Azure VMs</span></span>

<span data-ttu-id="698e4-104">W tym artykule przedstawiono kilka metod resetowania haseł usługi lokalnej maszyny wirtualnej systemu Linux (VM).</span><span class="sxs-lookup"><span data-stu-id="698e4-104">This article introduces several methods to reset local Linux Virtual Machine (VM) passwords.</span></span> <span data-ttu-id="698e4-105">Jeśli konto użytkownika wygasło lub po prostu chcesz utworzyć nowe konto, można użyć następujących metod, Utwórz nowe konto administratora lokalnego i ponownie uzyskać dostęp do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="698e4-105">If the user account is expired or you just want to create a new account, you can use the following methods to create a new local admin account and re-gain access to the VM.</span></span>

## <a name="symptoms"></a><span data-ttu-id="698e4-106">Objawy</span><span class="sxs-lookup"><span data-stu-id="698e4-106">Symptoms</span></span>

<span data-ttu-id="698e4-107">Nie można zalogować się do maszyny Wirtualnej, i pojawi się komunikat informujący o tym, że hasło używane jest nieprawidłowa.</span><span class="sxs-lookup"><span data-stu-id="698e4-107">You can't log in to the VM, and you receive a message that indicates that the password that you used is incorrect.</span></span> <span data-ttu-id="698e4-108">Ponadto nie można użyć VMAgent resetowania hasła w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="698e4-108">Additionally, you can't use VMAgent to reset your password on the Azure Portal.</span></span> 

## <a name="manual-password-reset-procedure"></a><span data-ttu-id="698e4-109">Procedury ręcznego resetowania hasła</span><span class="sxs-lookup"><span data-stu-id="698e4-109">Manual Password Reset procedure</span></span>

1.  <span data-ttu-id="698e4-110">Usuń maszynę Wirtualną i Zachowaj dołączonych dysków.</span><span class="sxs-lookup"><span data-stu-id="698e4-110">Delete the VM and keep the attached disks.</span></span>

2.  <span data-ttu-id="698e4-111">Dołączanie dysku systemu operacyjnego jako dysku danych do innego danych czasowych maszyny Wirtualnej w tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="698e4-111">Attach the OS Drive as a data disk to another temporal VM in the same location.</span></span>

3.  <span data-ttu-id="698e4-112">Uruchom następujące polecenie SSH na danych czasowych maszyny Wirtualnej, aby stać się nadtypem użytkownika.</span><span class="sxs-lookup"><span data-stu-id="698e4-112">Run the following SSH command on the temporal VM to become a super-user.</span></span>


    ~~~~
    sudo su
    ~~~~

4.  <span data-ttu-id="698e4-113">Uruchom **fdisk -l** lub przyjrzeć się dzienniki systemowe, aby znaleźć nowo dołączonego dysku.</span><span class="sxs-lookup"><span data-stu-id="698e4-113">Run **fdisk -l** or look at system logs to find the newly attached disk.</span></span> <span data-ttu-id="698e4-114">Znajdź nazwę dysku do zainstalowania.</span><span class="sxs-lookup"><span data-stu-id="698e4-114">Locate the drive name to mount.</span></span> <span data-ttu-id="698e4-115">Na Maszynie wirtualnej danych czasowych, poszukaj w odpowiedni plik dziennika.</span><span class="sxs-lookup"><span data-stu-id="698e4-115">Then on the temporal VM, look in the relevant log file.</span></span>

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    <span data-ttu-id="698e4-116">Poniżej przedstawiono przykładowe dane wyjściowe polecenia grep:</span><span class="sxs-lookup"><span data-stu-id="698e4-116">The following is example output of the grep command:</span></span>

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  <span data-ttu-id="698e4-117">Utwórz punkt instalacji o nazwie **tempmount**.</span><span class="sxs-lookup"><span data-stu-id="698e4-117">Create a mount point called **tempmount**.</span></span>

    ~~~~
    mkdir /tempmount
    ~~~~

6.  <span data-ttu-id="698e4-118">Zainstaluj dysk systemu operacyjnego w punkcie instalacji.</span><span class="sxs-lookup"><span data-stu-id="698e4-118">Mount the OS disk on the mount point.</span></span> <span data-ttu-id="698e4-119">Zazwyczaj należy sdc1 instalacji lub sdc2.</span><span class="sxs-lookup"><span data-stu-id="698e4-119">You usually need to mount sdc1 or sdc2.</span></span> <span data-ttu-id="698e4-120">Zależy to hostingu partycji w katalogu/etc z dysku komputera przerwane.</span><span class="sxs-lookup"><span data-stu-id="698e4-120">This will depend on the hosting partition in /etc directory from the broken machine disk.</span></span>

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  <span data-ttu-id="698e4-121">Wykonaj kopię zapasową przed wprowadzeniem jakichkolwiek zmian:</span><span class="sxs-lookup"><span data-stu-id="698e4-121">Perform a backup before making any changes:</span></span>

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  <span data-ttu-id="698e4-122">Resetowania hasła użytkownika, które są potrzebne:</span><span class="sxs-lookup"><span data-stu-id="698e4-122">Reset the user’s password that you need:</span></span>

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  <span data-ttu-id="698e4-123">Przenieś zmodyfikowane pliki do poprawnej lokalizacji na dysku komputera przerwane.</span><span class="sxs-lookup"><span data-stu-id="698e4-123">Move the modified files to the correct location on the broken machine's disk.</span></span>

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back to the root and unmount the disk.

    ~~~~
    <span data-ttu-id="698e4-124">dysk CD / umount /tempmount</span><span class="sxs-lookup"><span data-stu-id="698e4-124">cd / umount /tempmount</span></span>
    ~~~~

11. Detach the disk from the management portal.

12. Recreate the VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk to another Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How to delete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)