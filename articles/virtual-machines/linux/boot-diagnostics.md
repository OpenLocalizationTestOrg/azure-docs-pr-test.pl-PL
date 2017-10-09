---
title: Diagnostyka aaaBoot dla maszyn wirtualnych systemu Linux na platformie Azure | Doc firmy Microsoft
description: "Omówienie Witaj dwie funkcje debugowania dla maszyn wirtualnych systemu Linux na platformie Azure"
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
ms.openlocfilehash: d355d512de09d2f1d7a2718e3db3fb99c9dd9e24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-boot-diagnostics-tootroubleshoot-linux-virtual-machines-in-azure"></a><span data-ttu-id="8be3e-103">Jak toouse rozruchu maszyn wirtualnych systemu Linux tootroubleshoot Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="8be3e-103">How toouse boot diagnostics tootroubleshoot Linux virtual machines in Azure</span></span>

<span data-ttu-id="8be3e-104">Na platformie Azure jest teraz dostępna obsługa dwóch funkcji debugowania: obsługa danych wyjściowych konsoli i zrzutu ekranu dla modelu wdrażania przy użyciu usługi Azure Virtual Machines Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8be3e-104">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="8be3e-105">Podczas przełączania tooAzure własny obraz lub nawet rozruch jeden z obrazów platformy hello, może istnieć wiele przyczyn, dlaczego pobiera maszynę wirtualną do stanu rozruchowego.</span><span class="sxs-lookup"><span data-stu-id="8be3e-105">When bringing your own image tooAzure or even booting one of hello platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="8be3e-106">Te funkcje włączenia należy tooeasily diagnozowanie i odzyskiwanie po błędach rozruchu maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="8be3e-106">These features enable you tooeasily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="8be3e-107">Dla maszyn wirtualnych systemu Linux można łatwo przeglądać dane wyjściowe hello dziennika konsoli z hello portalu:</span><span class="sxs-lookup"><span data-stu-id="8be3e-107">For Linux Virtual Machines, you can easily view hello output of your console log from hello Portal:</span></span>

![Azure Portal](./media/boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="8be3e-109">Jednak dla systemów Windows i maszyn wirtualnych systemu Linux Azure umożliwia również toosee hello maszyny Wirtualnej z funkcji hypervisor hello zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="8be3e-109">However, for both Windows and Linux Virtual Machines, Azure also enables you toosee a screenshot of hello VM from hello hypervisor:</span></span>

![Błąd](./media/boot-diagnostics/screenshot2.png)

<span data-ttu-id="8be3e-111">Obie te funkcje są obsługiwane dla maszyn wirtualnych platformy Azure we wszystkich regionach.</span><span class="sxs-lookup"><span data-stu-id="8be3e-111">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="8be3e-112">Uwaga, zrzuty ekranu i danych wyjściowych może potrwać too10 tooappear minut na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="8be3e-112">Note, screenshots, and output can take up too10 minutes tooappear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="8be3e-113">Typowe błędy rozruchu</span><span class="sxs-lookup"><span data-stu-id="8be3e-113">Common boot errors</span></span>

- [<span data-ttu-id="8be3e-114">Zagadnienia dotyczące systemu plików</span><span class="sxs-lookup"><span data-stu-id="8be3e-114">File system issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [<span data-ttu-id="8be3e-115">Problemy z jądra</span><span class="sxs-lookup"><span data-stu-id="8be3e-115">Kernel Issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [<span data-ttu-id="8be3e-116">Błędy FSTAB</span><span class="sxs-lookup"><span data-stu-id="8be3e-116">FSTAB errors</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="8be3e-117">Włączanie diagnostyki na nowej maszynie wirtualnej</span><span class="sxs-lookup"><span data-stu-id="8be3e-117">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="8be3e-118">Podczas tworzenia nowej maszyny wirtualnej z hello portalu w wersji zapoznawczej, wybierz hello **usługi Azure Resource Manager** z listy rozwijanej modelu wdrażania hello:</span><span class="sxs-lookup"><span data-stu-id="8be3e-118">When creating a new Virtual Machine from hello Preview Portal, select hello **Azure Resource Manager** from hello deployment model dropdown:</span></span>
 
    ![Resource Manager](./media/boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="8be3e-120">Skonfiguruj te pliki diagnostyczne hello miejsce chcesz tooplace monitorowanie opcja tooselect hello magazynu konta.</span><span class="sxs-lookup"><span data-stu-id="8be3e-120">Configure hello Monitoring option tooselect hello storage account where you would like tooplace these diagnostic files.</span></span>
 
    ![Tworzenie maszyny wirtualnej](./media/boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="8be3e-122">Jeśli wdrażasz za pomocą szablonu usługi Azure Resource Manager, przejdź tooyour zasobu maszyny wirtualnej i Dołącz sekcji profilu diagnostyki hello.</span><span class="sxs-lookup"><span data-stu-id="8be3e-122">If you are deploying from an Azure Resource Manager template, navigate tooyour Virtual Machine resource and append hello diagnostics profile section.</span></span> <span data-ttu-id="8be3e-123">Należy pamiętać, nagłówek wersji interfejsu API toouse hello "2015-06-15".</span><span class="sxs-lookup"><span data-stu-id="8be3e-123">Remember toouse hello “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="8be3e-124">profilu diagnostyki Hello umożliwia konta magazynu hello tooselect miejscu tooput tych dzienników.</span><span class="sxs-lookup"><span data-stu-id="8be3e-124">hello diagnostics profile enables you tooselect hello storage account where you want tooput these logs.</span></span>

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

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="8be3e-125">Aktualizowanie istniejącej maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="8be3e-125">Update an existing virtual machine</span></span>

<span data-ttu-id="8be3e-126">diagnostyki rozruchu tooenable za pośrednictwem portalu hello, można także zaktualizować istniejącej maszyny wirtualnej za pośrednictwem portalu hello.</span><span class="sxs-lookup"><span data-stu-id="8be3e-126">tooenable boot diagnostics through hello portal, you can also update an existing virtual machine through hello portal.</span></span> <span data-ttu-id="8be3e-127">Wybierz hello diagnostyki rozruchu opcji i Zapisz.</span><span class="sxs-lookup"><span data-stu-id="8be3e-127">Select hello Boot Diagnostics option and Save.</span></span> <span data-ttu-id="8be3e-128">Uruchom ponownie hello wirtualna tootake efekt.</span><span class="sxs-lookup"><span data-stu-id="8be3e-128">Restart hello VM tootake effect.</span></span>

![Aktualizowanie istniejącej maszyny wirtualnej](./media/boot-diagnostics/screenshot5.png)