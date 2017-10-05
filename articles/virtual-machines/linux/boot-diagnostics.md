---
title: Rozruch diagnostyki dla maszyn wirtualnych systemu Linux na platformie Azure | Doc firmy Microsoft
description: "Omówienie dwóch funkcji debugowania dla maszyn wirtualnych systemu Linux na platformie Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: Deland-Han
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: delhan
ms.openlocfilehash: 70254d39b5c6326166f7e29fdfc99533835502f9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-boot-diagnostics-to-troubleshoot-linux-virtual-machines-in-azure"></a><span data-ttu-id="c78ab-103">Rozwiązywanie problemów z maszyn wirtualnych systemu Linux na platformie Azure przy użyciu diagnostyki rozruchu</span><span class="sxs-lookup"><span data-stu-id="c78ab-103">How to use boot diagnostics to troubleshoot Linux virtual machines in Azure</span></span>

<span data-ttu-id="c78ab-104">Na platformie Azure jest teraz dostępna obsługa dwóch funkcji debugowania: obsługa danych wyjściowych konsoli i zrzutu ekranu dla modelu wdrażania przy użyciu usługi Azure Virtual Machines Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c78ab-104">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="c78ab-105">Podczas korzystania z własnego obrazu na platformie Azure, a nawet wykonywania rozruchu jednego z obrazów platformy, może wystąpić wiele przyczyn przejścia maszyny wirtualnej do stanu uniemożliwiającego rozruch.</span><span class="sxs-lookup"><span data-stu-id="c78ab-105">When bringing your own image to Azure or even booting one of the platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="c78ab-106">Te funkcje umożliwiają łatwe diagnozowanie i odzyskiwanie maszyn wirtualnych po niepowodzeniach rozruchu.</span><span class="sxs-lookup"><span data-stu-id="c78ab-106">These features enable you to easily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="c78ab-107">Dla maszyn wirtualnych z systemem Linux można łatwo wyświetlić dane wyjściowe konsoli dziennika za pomocą portalu:</span><span class="sxs-lookup"><span data-stu-id="c78ab-107">For Linux Virtual Machines, you can easily view the output of your console log from the Portal:</span></span>

![Azure Portal](./media/boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="c78ab-109">Jednak zarówno dla maszyn wirtualnych z systemem Linux, jak i Windows, platforma Azure umożliwia również wyświetlenie zrzutu ekranu maszyny wirtualnej za pomocą funkcji hypervisor:</span><span class="sxs-lookup"><span data-stu-id="c78ab-109">However, for both Windows and Linux Virtual Machines, Azure also enables you to see a screenshot of the VM from the hypervisor:</span></span>

![Błąd](./media/boot-diagnostics/screenshot2.png)

<span data-ttu-id="c78ab-111">Obie te funkcje są obsługiwane dla maszyn wirtualnych platformy Azure we wszystkich regionach.</span><span class="sxs-lookup"><span data-stu-id="c78ab-111">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="c78ab-112">Należy pamiętać, że może minąć do 10 minut, zanim zrzuty ekranu i dane wyjściowe pojawią się na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="c78ab-112">Note, screenshots, and output can take up to 10 minutes to appear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="c78ab-113">Typowe błędy rozruchu</span><span class="sxs-lookup"><span data-stu-id="c78ab-113">Common boot errors</span></span>

- [<span data-ttu-id="c78ab-114">Zagadnienia dotyczące systemu plików</span><span class="sxs-lookup"><span data-stu-id="c78ab-114">File system issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [<span data-ttu-id="c78ab-115">Problemy z jądra</span><span class="sxs-lookup"><span data-stu-id="c78ab-115">Kernel Issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [<span data-ttu-id="c78ab-116">Błędy FSTAB</span><span class="sxs-lookup"><span data-stu-id="c78ab-116">FSTAB errors</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="c78ab-117">Włączanie diagnostyki na nowej maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c78ab-117">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="c78ab-118">Podczas tworzenia nowej maszyny wirtualnej w portalu w wersji zapoznawczej wybierz pozycję **Azure Resource Manager** z listy rozwijanej modelu wdrażania:</span><span class="sxs-lookup"><span data-stu-id="c78ab-118">When creating a new Virtual Machine from the Preview Portal, select the **Azure Resource Manager** from the deployment model dropdown:</span></span>
 
    ![Resource Manager](./media/boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="c78ab-120">Skonfiguruj opcję Monitorowanie, aby wybrać konto magazynu, w którym chcesz umieścić te pliki diagnostyczne.</span><span class="sxs-lookup"><span data-stu-id="c78ab-120">Configure the Monitoring option to select the storage account where you would like to place these diagnostic files.</span></span>
 
    ![Tworzenie maszyny wirtualnej](./media/boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="c78ab-122">Jeśli wykonujesz wdrożenie z szablonu usługi Azure Resource Manager, przejdź do zasobu maszyny wirtualnej i dołącz sekcję profilu diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="c78ab-122">If you are deploying from an Azure Resource Manager template, navigate to your Virtual Machine resource and append the diagnostics profile section.</span></span> <span data-ttu-id="c78ab-123">Pamiętaj, aby użyć nagłówka wersji interfejsu API „2015-06-15”.</span><span class="sxs-lookup"><span data-stu-id="c78ab-123">Remember to use the “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="c78ab-124">Profil diagnostyki umożliwia wybranie konta magazynu, na którym chcesz umieścić te dzienniki.</span><span class="sxs-lookup"><span data-stu-id="c78ab-124">The diagnostics profile enables you to select the storage account where you want to put these logs.</span></span>

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="c78ab-125">Aktualizowanie istniejącej maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c78ab-125">Update an existing virtual machine</span></span>

<span data-ttu-id="c78ab-126">Aby włączyć diagnostyki rozruchu za pośrednictwem portalu, należy zaktualizować istniejącej maszyny wirtualnej za pośrednictwem portalu.</span><span class="sxs-lookup"><span data-stu-id="c78ab-126">To enable boot diagnostics through the portal, you can also update an existing virtual machine through the portal.</span></span> <span data-ttu-id="c78ab-127">Wybierz opcję Diagnostyka rozruchu i kliknij ikonę Zapisz.</span><span class="sxs-lookup"><span data-stu-id="c78ab-127">Select the Boot Diagnostics option and Save.</span></span> <span data-ttu-id="c78ab-128">Uruchom ponownie maszynę wirtualną, aby zmiany zaczęły obowiązywać.</span><span class="sxs-lookup"><span data-stu-id="c78ab-128">Restart the VM to take effect.</span></span>

![Aktualizowanie istniejącej maszyny wirtualnej](./media/boot-diagnostics/screenshot5.png)