---
title: "aaaFrequently zadawane pytania dotyczące maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Udostępnia toosome odpowiedzi z hello często zadawane pytania dotyczące maszyn wirtualnych systemu Linux utworzone za pomocą modelu usługi Resource Manager hello."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 3648e09c-1115-4818-93c6-688d7a54a353
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: cynthn
ms.openlocfilehash: 0afd08123dddc408851065c46deedc3146dbec20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a><span data-ttu-id="c0e01-103">Często zadawane pytania dotyczące maszyn wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="c0e01-103">Frequently asked question about Linux Virtual Machines</span></span>
<span data-ttu-id="c0e01-104">W tym artykule opisano często zadawane pytania dotyczące maszyn wirtualnych systemu Linux utworzone na platformie Azure przy użyciu modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="c0e01-104">This article addresses some common questions about Linux virtual machines created in Azure using hello Resource Manager deployment model.</span></span> <span data-ttu-id="c0e01-105">Wersja systemu Windows hello tego tematu dla [często zadawane pytania dotyczące maszyn wirtualnych systemu Windows](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="c0e01-105">For hello Windows version of this topic, see [Frequently asked question about Windows Virtual Machines](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="what-can-i-run-on-an-azure-vm"></a><span data-ttu-id="c0e01-106">Co mogę uruchomić na maszynie wirtualnej platformy Azure?</span><span class="sxs-lookup"><span data-stu-id="c0e01-106">What can I run on an Azure VM?</span></span>
<span data-ttu-id="c0e01-107">Wszyscy subskrybenci mogą uruchomić oprogramowanie serwerowe na maszynie wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c0e01-107">All subscribers can run server software on an Azure virtual machine.</span></span> <span data-ttu-id="c0e01-108">Aby uzyskać więcej informacji, zobacz [systemu Linux na Azure-Endorsed dystrybucji](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="c0e01-108">For more information, see [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a><span data-ttu-id="c0e01-109">Ile pamięci masowej mogę użyć w maszynie wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="c0e01-109">How much storage can I use with a virtual machine?</span></span>
<span data-ttu-id="c0e01-110">Każdy dysk danych można się too1 TB.</span><span class="sxs-lookup"><span data-stu-id="c0e01-110">Each data disk can be up too1 TB.</span></span> <span data-ttu-id="c0e01-111">Witaj liczba dysków z danymi, których można używać zależy od rozmiaru hello hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c0e01-111">hello number of data disks you can use depends on hello size of hello virtual machine.</span></span> <span data-ttu-id="c0e01-112">Aby uzyskać szczegółowe informacje, zobacz [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Rozmiary maszyn wirtualnych).</span><span class="sxs-lookup"><span data-stu-id="c0e01-112">For details, see [Sizes for Virtual Machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="c0e01-113">Konto usługi Azure storage udostępnia magazyn hello dysku systemu operacyjnego i dysków z danymi.</span><span class="sxs-lookup"><span data-stu-id="c0e01-113">An Azure storage account provides storage for hello operating system disk and any data disks.</span></span> <span data-ttu-id="c0e01-114">Każdy dysk jest plikiem VHD przechowywanym jako stronicowy obiekt blob.</span><span class="sxs-lookup"><span data-stu-id="c0e01-114">Each disk is a .vhd file stored as a page blob.</span></span> <span data-ttu-id="c0e01-115">Aby uzyskać szczegółowe informacje o cenach, zobacz [Szczegóły cennika magazynu](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="c0e01-115">For pricing details, see [Storage Pricing Details](https://azure.microsoft.com/pricing/details/storage/).</span></span>

## <a name="how-can-i-access-my-virtual-machine"></a><span data-ttu-id="c0e01-116">Jak można uzyskać dostęp Moja maszyna wirtualna?</span><span class="sxs-lookup"><span data-stu-id="c0e01-116">How can I access my virtual machine?</span></span>
<span data-ttu-id="c0e01-117">Ustanów toolog połączenia zdalnego, na maszynie wirtualnej toohello, przy użyciu protokołu Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="c0e01-117">Establish a remote connection toolog on toohello virtual machine, using Secure Shell (SSH).</span></span> <span data-ttu-id="c0e01-118">Zobacz hello instrukcje na temat tooconnect [z systemu Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub [z systemami Linux i komputerów Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c0e01-118">See hello instructions on how tooconnect [from Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [from Linux and Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="c0e01-119">Domyślnie protokół SSH umożliwia maksymalnie 10 równoczesnych połączeń.</span><span class="sxs-lookup"><span data-stu-id="c0e01-119">By default, SSH allows a maximum of 10 concurrent connections.</span></span> <span data-ttu-id="c0e01-120">Można zwiększyć tę liczbę, edytując hello pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c0e01-120">You can increase this number by editing hello configuration file.</span></span>

<span data-ttu-id="c0e01-121">Jeśli masz problemy, zapoznaj się [Rozwiązywanie problemów z Secure Shell (SSH) połączenia](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c0e01-121">If you’re having problems, check out [Troubleshoot Secure Shell (SSH) connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="can-i-use-hello-temporary-disk-devsdb1-toostore-data"></a><span data-ttu-id="c0e01-122">Można użyć hello dysku tymczasowym (/ dev/sdb1) toostore danych?</span><span class="sxs-lookup"><span data-stu-id="c0e01-122">Can I use hello temporary disk (/dev/sdb1) toostore data?</span></span>
<span data-ttu-id="c0e01-123">Nie używaj hello dysku tymczasowym (/ dev/sdb1) toostore danych.</span><span class="sxs-lookup"><span data-stu-id="c0e01-123">Don't use hello temporary disk (/dev/sdb1) toostore data.</span></span> <span data-ttu-id="c0e01-124">Jest dostępne tylko do tymczasowego przechowywania.</span><span class="sxs-lookup"><span data-stu-id="c0e01-124">It is only there for temporary storage.</span></span> <span data-ttu-id="c0e01-125">Istnieje ryzyko utraty danych, która nie może zostać odzyskany.</span><span class="sxs-lookup"><span data-stu-id="c0e01-125">You risk losing data that can’t be recovered.</span></span>

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a><span data-ttu-id="c0e01-126">Można skopiować lub sklonować istniejącą maszynę Wirtualną platformy Azure?</span><span class="sxs-lookup"><span data-stu-id="c0e01-126">Can I copy or clone an existing Azure VM?</span></span>
<span data-ttu-id="c0e01-127">Tak.</span><span class="sxs-lookup"><span data-stu-id="c0e01-127">Yes.</span></span> <span data-ttu-id="c0e01-128">Aby uzyskać instrukcje, zobacz [jak toocreate kopia maszyny wirtualnej systemu Linux w hello modelu wdrażania usługi Resource Manager](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c0e01-128">For instructions, see [How toocreate a copy of a Linux virtual machine in hello Resource Manager deployment model](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a><span data-ttu-id="c0e01-129">Dlaczego nie widzę centralnej Zjednoczone i Kanada Wschodnia regionów za pośrednictwem usługi Azure Resource Manager?</span><span class="sxs-lookup"><span data-stu-id="c0e01-129">Why am I not seeing Canada Central and Canada East regions through Azure Resource Manager?</span></span>
<span data-ttu-id="c0e01-130">Hello dwóch regionach nowej centralnej Zjednoczone i Kanada Wschodnia nie są automatycznie zarejestrowany dla tworzenia maszyny wirtualnej dla istniejącej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c0e01-130">hello two new regions of Canada Central and Canada East are not automatically registered for virtual machine creation for existing Azure subscriptions.</span></span> <span data-ttu-id="c0e01-131">Rejestracja odbywa się automatycznie podczas wdrażania maszyny wirtualnej za pośrednictwem hello Azure tooany portalu innego regionu przy użyciu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c0e01-131">This registration is done automatically when a virtual machine is deployed through hello Azure portal tooany other region using Azure Resource Manager.</span></span> <span data-ttu-id="c0e01-132">Po maszyny wirtualnej jest wdrożony tooany innego regionu Azure, nowych regionów hello powinny być dostępne dla kolejnych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c0e01-132">After a virtual machine is deployed tooany other Azure region, hello new regions should be available for subsequent virtual machines.</span></span>

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a><span data-ttu-id="c0e01-133">Toomy karty Sieciowej maszyny Wirtualnej można dodać po jej utworzeniu?</span><span class="sxs-lookup"><span data-stu-id="c0e01-133">Can I add a NIC toomy VM after it's created?</span></span>
<span data-ttu-id="c0e01-134">Tak, obecnie jest to możliwe.</span><span class="sxs-lookup"><span data-stu-id="c0e01-134">Yes, this is now possible.</span></span> <span data-ttu-id="c0e01-135">deallocated zatrzymana pierwszy toobe potrzeb Hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c0e01-135">hello VM first needs toobe stopped deallocated.</span></span> <span data-ttu-id="c0e01-136">Następnie można dodać lub usunąć karty Sieciowej (chyba że jest hello ostatniego karty Sieciowej na powitania maszyny Wirtualnej).</span><span class="sxs-lookup"><span data-stu-id="c0e01-136">Then you can add or remove a NIC (unless it's hello last NIC on hello VM).</span></span> 

## <a name="are-there-any-computer-name-requirements"></a><span data-ttu-id="c0e01-137">Czy istnieją wszystkie wymagania dotyczące nazwy komputera?</span><span class="sxs-lookup"><span data-stu-id="c0e01-137">Are there any computer name requirements?</span></span>
<span data-ttu-id="c0e01-138">Tak.</span><span class="sxs-lookup"><span data-stu-id="c0e01-138">Yes.</span></span> <span data-ttu-id="c0e01-139">Witaj, nazwa komputera może zawierać maksymalnie z 64 znaków.</span><span class="sxs-lookup"><span data-stu-id="c0e01-139">hello computer name can be a maximum of 64 characters in length.</span></span> <span data-ttu-id="c0e01-140">Zobacz [nazewnictwa konwencje reguły i ograniczenia](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) uzyskać więcej informacji dotyczących nazw zasobów.</span><span class="sxs-lookup"><span data-stu-id="c0e01-140">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information around naming your resources.</span></span>

## <a name="are-there-any-resource-group-name-requirements"></a><span data-ttu-id="c0e01-141">Czy istnieją dowolnego zasobu wymagania dotyczące nazw grupy?</span><span class="sxs-lookup"><span data-stu-id="c0e01-141">Are there any resource group name requirements?</span></span>
<span data-ttu-id="c0e01-142">Tak.</span><span class="sxs-lookup"><span data-stu-id="c0e01-142">Yes.</span></span> <span data-ttu-id="c0e01-143">Nazwa grupy zasobów Hello może zawierać maksymalnie 90 znaków długości.</span><span class="sxs-lookup"><span data-stu-id="c0e01-143">hello resource group name can be a maximum of 90 characters in length.</span></span> <span data-ttu-id="c0e01-144">Zobacz [nazewnictwa konwencje reguły i ograniczenia](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Aby uzyskać więcej informacji na temat grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="c0e01-144">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about resource groups.</span></span>

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a><span data-ttu-id="c0e01-145">Jakie są wymagania username hello, podczas tworzenia maszyny Wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="c0e01-145">What are hello username requirements when creating a VM?</span></span>
<span data-ttu-id="c0e01-146">Nazwy użytkowników musi być 1 do 64 znaków.</span><span class="sxs-lookup"><span data-stu-id="c0e01-146">Usernames must be 1 - 64 characters in length.</span></span>

<span data-ttu-id="c0e01-147">Witaj następujące nazwy użytkowników nie są dozwolone:</span><span class="sxs-lookup"><span data-stu-id="c0e01-147">hello following usernames are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center"><span data-ttu-id="c0e01-148">Administrator</span><span class="sxs-lookup"><span data-stu-id="c0e01-148">administrator</span></span> </td><td style="text-align:center"> <span data-ttu-id="c0e01-149">Administrator</span><span class="sxs-lookup"><span data-stu-id="c0e01-149">admin</span></span> </td><td style="text-align:center"> <span data-ttu-id="c0e01-150">Użytkownika</span><span class="sxs-lookup"><span data-stu-id="c0e01-150">user</span></span> </td><td style="text-align:center"> <span data-ttu-id="c0e01-151">Użytkownik1</span><span class="sxs-lookup"><span data-stu-id="c0e01-151">user1</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="c0e01-152">Test</span><span class="sxs-lookup"><span data-stu-id="c0e01-152">test</span></span> </td><td style="text-align:center"> <span data-ttu-id="c0e01-153">UŻYTKOWNIK2</span><span class="sxs-lookup"><span data-stu-id="c0e01-153">user2</span></span> </td><td style="text-align:center"> <span data-ttu-id="c0e01-154">Test1</span><span class="sxs-lookup"><span data-stu-id="c0e01-154">test1</span></span> </td><td style="text-align:center"> <span data-ttu-id="c0e01-155">UŻYTKOWNIK3</span><span class="sxs-lookup"><span data-stu-id="c0e01-155">user3</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="c0e01-156">admin1</span><span class="sxs-lookup"><span data-stu-id="c0e01-156">admin1</span></span> </td><td style="text-align:center"> <span data-ttu-id="c0e01-157">1</span><span class="sxs-lookup"><span data-stu-id="c0e01-157">1</span></span> </td><td style="text-align:center"> <span data-ttu-id="c0e01-158">123</span><span class="sxs-lookup"><span data-stu-id="c0e01-158">123</span></span> </td><td style="text-align:center"> <span data-ttu-id="c0e01-159">A</span><span class="sxs-lookup"><span data-stu-id="c0e01-159">a</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="c0e01-160">actuser</span><span class="sxs-lookup"><span data-stu-id="c0e01-160">actuser</span></span>  </td><td style="text-align:center"> <span data-ttu-id="c0e01-161">usługi adm</span><span class="sxs-lookup"><span data-stu-id="c0e01-161">adm</span></span> </td><td style="text-align:center"> <span data-ttu-id="c0e01-162">admin2</span><span class="sxs-lookup"><span data-stu-id="c0e01-162">admin2</span></span> </td><td style="text-align:center"> <span data-ttu-id="c0e01-163">ASPNET</span><span class="sxs-lookup"><span data-stu-id="c0e01-163">aspnet</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="c0e01-164">kopia zapasowa</span><span class="sxs-lookup"><span data-stu-id="c0e01-164">backup</span></span> </td><td style="text-align:center"> <span data-ttu-id="c0e01-165">Konsoli</span><span class="sxs-lookup"><span data-stu-id="c0e01-165">console</span></span> </td><td style="text-align:center"> <span data-ttu-id="c0e01-166">ADAM</span><span class="sxs-lookup"><span data-stu-id="c0e01-166">david</span></span> </td><td style="text-align:center"> <span data-ttu-id="c0e01-167">Gość</span><span class="sxs-lookup"><span data-stu-id="c0e01-167">guest</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="c0e01-168">Jan</span><span class="sxs-lookup"><span data-stu-id="c0e01-168">john</span></span> </td><td style="text-align:center"> <span data-ttu-id="c0e01-169">Właściciel</span><span class="sxs-lookup"><span data-stu-id="c0e01-169">owner</span></span> </td><td style="text-align:center"> <span data-ttu-id="c0e01-170">główny</span><span class="sxs-lookup"><span data-stu-id="c0e01-170">root</span></span> </td><td style="text-align:center"> <span data-ttu-id="c0e01-171">serwer</span><span class="sxs-lookup"><span data-stu-id="c0e01-171">server</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="c0e01-172">SQL</span><span class="sxs-lookup"><span data-stu-id="c0e01-172">sql</span></span> </td><td style="text-align:center"> <span data-ttu-id="c0e01-173">Obsługa</span><span class="sxs-lookup"><span data-stu-id="c0e01-173">support</span></span> </td><td style="text-align:center"> <span data-ttu-id="c0e01-174">support_388945a0</span><span class="sxs-lookup"><span data-stu-id="c0e01-174">support_388945a0</span></span> </td><td style="text-align:center"> <span data-ttu-id="c0e01-175">sys</span><span class="sxs-lookup"><span data-stu-id="c0e01-175">sys</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="c0e01-176">Test2</span><span class="sxs-lookup"><span data-stu-id="c0e01-176">test2</span></span> </td><td style="text-align:center"> <span data-ttu-id="c0e01-177">test3</span><span class="sxs-lookup"><span data-stu-id="c0e01-177">test3</span></span> </td><td style="text-align:center"> <span data-ttu-id="c0e01-178">user4</span><span class="sxs-lookup"><span data-stu-id="c0e01-178">user4</span></span> </td><td style="text-align:center"> <span data-ttu-id="c0e01-179">user5</span><span class="sxs-lookup"><span data-stu-id="c0e01-179">user5</span></span></td>
    </tr>
</table>


## <a name="what-are-hello-password-requirements-when-creating-a-vm"></a><span data-ttu-id="c0e01-180">Jakie są wymagania dotyczące hasła hello podczas tworzenia maszyny Wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="c0e01-180">What are hello password requirements when creating a VM?</span></span>
<span data-ttu-id="c0e01-181">Hasła muszą być 6-72 znaków i spełnić 3 poza hello następujące wymagania dotyczące złożoności 4:</span><span class="sxs-lookup"><span data-stu-id="c0e01-181">Passwords must be 6 - 72 characters in length and meet 3 out of hello following 4 complexity requirements:</span></span>

* <span data-ttu-id="c0e01-182">Mieć niższe znaków</span><span class="sxs-lookup"><span data-stu-id="c0e01-182">Have lower characters</span></span>
* <span data-ttu-id="c0e01-183">Ma górny znaków</span><span class="sxs-lookup"><span data-stu-id="c0e01-183">Have upper characters</span></span>
* <span data-ttu-id="c0e01-184">Zawierać cyfrę</span><span class="sxs-lookup"><span data-stu-id="c0e01-184">Have a digit</span></span>
* <span data-ttu-id="c0e01-185">Ma znak specjalny (wyrażenie regularne zgodne [\W_])</span><span class="sxs-lookup"><span data-stu-id="c0e01-185">Have a special character (Regex match [\W_])</span></span>

<span data-ttu-id="c0e01-186">Witaj następującego hasła nie są dozwolone:</span><span class="sxs-lookup"><span data-stu-id="c0e01-186">hello following passwords are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center"><span data-ttu-id="c0e01-187">P@$$w0rd</span><span class="sxs-lookup"><span data-stu-id="c0e01-187">P@$$w0rd</span></span></td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center"><span data-ttu-id="c0e01-188">Pa$ $word</span><span class="sxs-lookup"><span data-stu-id="c0e01-188">Pa$$word</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center"><span data-ttu-id="c0e01-189">Hasło!</span><span class="sxs-lookup"><span data-stu-id="c0e01-189">Password!</span></span></td>
        <td style="text-align:center"><span data-ttu-id="c0e01-190">Password1</span><span class="sxs-lookup"><span data-stu-id="c0e01-190">Password1</span></span></td>
        <td style="text-align:center"><span data-ttu-id="c0e01-191">Password22</span><span class="sxs-lookup"><span data-stu-id="c0e01-191">Password22</span></span></td>
        <td style="text-align:center"><span data-ttu-id="c0e01-192">ILOVEYOU!</span><span class="sxs-lookup"><span data-stu-id="c0e01-192">iloveyou!</span></span></td>
    </tr>
</table>
