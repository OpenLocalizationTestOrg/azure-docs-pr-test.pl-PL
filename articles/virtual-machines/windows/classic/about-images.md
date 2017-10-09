---
title: "aaaAbout obrazów maszyn wirtualnych z systemem Windows | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat używania obrazów maszyn wirtualnych systemu Windows na platformie Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 66ff3fab-8e7f-4dff-b8da-ab1c9c9c9af8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cynthn
ms.openlocfilehash: c7cfa1d018a5e99d5b68f559ec9ae1f14e4dec8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="about-images-for-windows-virtual-machines"></a><span data-ttu-id="ef494-103">Informacje o obrazach dla maszyn wirtualnych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="ef494-103">About images for Windows virtual machines</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ef494-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ef494-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ef494-105">W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="ef494-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="ef494-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ef494-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="ef494-107">Uzyskać informacje o znajdowaniu i używanie obrazów w modelu usługi Resource Manager hello, zobacz [tutaj](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ef494-107">For information about finding and using images in hello Resource Manager model, see [here](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a><span data-ttu-id="ef494-108">Praca z obrazami</span><span class="sxs-lookup"><span data-stu-id="ef494-108">Working with images</span></span>

<span data-ttu-id="ef494-109">Można użyć modułu Azure PowerShell hello i hello Azure toomanage portalu hello obrazy dostępne tooyour subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ef494-109">You can use hello Azure PowerShell module and hello Azure portal toomanage hello images available tooyour Azure subscription.</span></span> <span data-ttu-id="ef494-110">modułu Azure PowerShell Hello zawiera więcej opcji polecenia, więc będzie można wyznaczyć dokładnie, co toosee lub wykonaj.</span><span class="sxs-lookup"><span data-stu-id="ef494-110">hello Azure PowerShell module provides more command options, so you can pinpoint exactly what you want toosee or do.</span></span> <span data-ttu-id="ef494-111">Hello Azure portal udostępnia graficznego interfejsu użytkownika dla wielu hello codziennych zadań administracyjnych.</span><span class="sxs-lookup"><span data-stu-id="ef494-111">hello Azure portal provides a GUI for many of hello everyday administrative tasks.</span></span>

<span data-ttu-id="ef494-112">Oto kilka przykładów, korzystających z hello modułu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef494-112">Here are some examples that use hello Azure PowerShell module.</span></span>

* <span data-ttu-id="ef494-113">**Pobierz wszystkie obrazy**:`Get-AzureVMImage`zwraca listę wszystkich dostępnych w ramach Twojej bieżącej subskrypcji obrazów hello: obrazów i udostępnianych przez zespół Azure lub partnerów.</span><span class="sxs-lookup"><span data-stu-id="ef494-113">**Get all images**:`Get-AzureVMImage`returns a list of all hello images available in your current subscription: your images and those provided by Azure or partners.</span></span> <span data-ttu-id="ef494-114">Hello wynikowa lista może być duży.</span><span class="sxs-lookup"><span data-stu-id="ef494-114">hello resulting list could be large.</span></span> <span data-ttu-id="ef494-115">Witaj dalej przykładach pokazano, jak tooget krótszej listy.</span><span class="sxs-lookup"><span data-stu-id="ef494-115">hello next examples show how tooget a shorter list.</span></span>
* <span data-ttu-id="ef494-116">**Pobierz obraz rodzin**:`Get-AzureVMImage | select ImageFamily` pobiera listę rodzin obrazu pokazując ciągów **ImageFamily** właściwości.</span><span class="sxs-lookup"><span data-stu-id="ef494-116">**Get image families**:`Get-AzureVMImage | select ImageFamily` gets a list of image families by showing strings **ImageFamily** property.</span></span>
* <span data-ttu-id="ef494-117">**Pobierz wszystkie obrazy w określonej rodzinie**:`Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span><span class="sxs-lookup"><span data-stu-id="ef494-117">**Get all images in a specific family**: `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span></span>
* <span data-ttu-id="ef494-118">**Znajdź obrazów maszyn wirtualnych**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` polega na filtrowanie hello DataDiskConfiguration właściwość, która ma zastosowanie tylko obrazy tooVM tego polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ef494-118">**Find VM Images**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` This cmdlet works by filtering hello DataDiskConfiguration property, which only applies tooVM Images.</span></span> <span data-ttu-id="ef494-119">W tym przykładzie filtruje także hello tooonly hello etykiety i obrazu nazwy wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="ef494-119">This example also filters hello output tooonly hello label and image name.</span></span>
* <span data-ttu-id="ef494-120">**Zapisz uogólniony obraz**:`Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span><span class="sxs-lookup"><span data-stu-id="ef494-120">**Save a generalized image**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span></span>
* <span data-ttu-id="ef494-121">**Zapisz obraz specjalne**:`Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span><span class="sxs-lookup"><span data-stu-id="ef494-121">**Save a specialized image**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span></span>

  > [!TIP]
  > <span data-ttu-id="ef494-122">Parametr OSState Hello jest wymagana toocreate obrazu maszyny Wirtualnej, która obejmuje hello dysku systemu operacyjnego i dołączone dyski danych.</span><span class="sxs-lookup"><span data-stu-id="ef494-122">hello OSState parameter is required toocreate a VM image, which includes hello operating system disk and attached data disks.</span></span> <span data-ttu-id="ef494-123">Jeśli nie używasz parametru hello hello polecenie cmdlet tworzy obrazu systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="ef494-123">If you don’t use hello parameter, hello cmdlet creates an OS image.</span></span> <span data-ttu-id="ef494-124">wartość Hello hello parametr wskazuje, czy obraz powitania uogólniony lub specjalizowany, oparta na Określa, czy dysk systemu operacyjnego hello zostało przygotowane do ponownego użycia.</span><span class="sxs-lookup"><span data-stu-id="ef494-124">hello value of hello parameter indicates whether hello image is generalized or specialized, based on whether hello operating system disk has been prepared for reuse.</span></span>

* <span data-ttu-id="ef494-125">**Usuń obraz**:`Remove-AzureVMImage –ImageName "MyOldVmImage"`</span><span class="sxs-lookup"><span data-stu-id="ef494-125">**Delete an image**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef494-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ef494-126">Next Steps</span></span>
<span data-ttu-id="ef494-127">Możesz również [Utwórz maszynę z systemem Windows przy użyciu portalu Azure hello](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="ef494-127">You can also [create a Windows machine using hello Azure portal](tutorial.md).</span></span>
