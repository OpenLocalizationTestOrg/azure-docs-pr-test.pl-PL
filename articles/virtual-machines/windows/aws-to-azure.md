---
title: "aaaMove tooAzure maszyn wirtualnych systemu Windows usług AWS | Dokumentacja firmy Microsoft"
description: "Przenieś tooAzure wystąpienia Windows EC2 Amazon Web Services (AWS) maszyn wirtualnych przy użyciu programu Azure PowerShell."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: cynthn
ms.openlocfilehash: f912c28d3ffe585162c3add715a1318ac3cd4643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-from-amazon-web-services-aws-tooazure-using-powershell"></a><span data-ttu-id="0ec70-103">Przenieś Maszynę wirtualną systemu Windows z tooAzure Amazon Web Services (AWS) przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ec70-103">Move a Windows VM from Amazon Web Services (AWS) tooAzure using PowerShell</span></span>

<span data-ttu-id="0ec70-104">Jeśli dokonujesz oceny maszyn wirtualnych platformy Azure do obsługi obciążeń, można wyeksportować istniejącego wystąpienia maszyny Wirtualnej systemu Windows EC2 Amazon Web Services (AWS). następnie przekaż hello tooAzure wirtualnego dysku twardego (VHD).</span><span class="sxs-lookup"><span data-stu-id="0ec70-104">If you are evaluating Azure virtual machines for hosting your workloads, you can export an existing Amazon Web Services (AWS) EC2 Windows VM instance then upload hello virtual hard disk (VHD) tooAzure.</span></span> <span data-ttu-id="0ec70-105">Raz hello, który jest przekazywany wirtualnego dysku twardego, można utworzyć nowej maszyny Wirtualnej na platformie Azure z hello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="0ec70-105">Once hello VHD is uploaded, you can create a new VM in Azure from hello VHD.</span></span> 

<span data-ttu-id="0ec70-106">W tym temacie omówiono przeniesienie jednej maszyny Wirtualnej z usług AWS tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0ec70-106">This topic covers moving a single VM from AWS tooAzure.</span></span> <span data-ttu-id="0ec70-107">Jeśli chcesz, aby maszyny wirtualne toomove z usług AWS tooAzure na dużą skalę, zobacz [migracji maszyn wirtualnych w tooAzure Amazon Web Services (AWS) z usługą Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="0ec70-107">If you want toomove VMs from AWS tooAzure at scale, see [Migrate virtual machines in Amazon Web Services (AWS) tooAzure with Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span></span>

## <a name="prepare-hello-vm"></a><span data-ttu-id="0ec70-108">Przygotowanie hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="0ec70-108">Prepare hello VM</span></span> 
 
<span data-ttu-id="0ec70-109">Możesz przekazać zarówno ogólnych i specjalnych tooAzure wirtualne dyski twarde.</span><span class="sxs-lookup"><span data-stu-id="0ec70-109">You can upload both generalized and specialized VHDs tooAzure.</span></span> <span data-ttu-id="0ec70-110">Każdy typ wymaga, aby przygotować hello maszyny Wirtualnej przed eksportem z usług AWS.</span><span class="sxs-lookup"><span data-stu-id="0ec70-110">Each type requires that you prepare hello VM before exporting from AWS.</span></span> 

- <span data-ttu-id="0ec70-111">**Uogólniony wirtualny dysk twardy** -uogólniony wirtualny dysk twardy ma wszystkie informacje osobiste Konto usunięte za pomocą programu Sysprep.</span><span class="sxs-lookup"><span data-stu-id="0ec70-111">**Generalized VHD** - a generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="0ec70-112">Jeśli planujesz hello toouse toocreate obrazu wirtualnego dysku twardego nowych maszyn wirtualnych z, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0ec70-112">If you intend toouse hello VHD as an image toocreate new VMs from, you should:</span></span> 
 
    * <span data-ttu-id="0ec70-113">[Przygotowywanie maszyny Wirtualnej systemu Windows](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="0ec70-113">[Prepare a Windows VM](prepare-for-upload-vhd-image.md).</span></span>  
    * <span data-ttu-id="0ec70-114">Generalize hello maszyny wirtualnej za pomocą programu Sysprep.</span><span class="sxs-lookup"><span data-stu-id="0ec70-114">Generalize hello virtual machine using Sysprep.</span></span>  

 
- <span data-ttu-id="0ec70-115">**Specjalizowany wirtualnego dysku twardego** -specjalne wirtualnego dysku twardego przechowuje hello kont użytkowników, aplikacji i innych danych o stanie z oryginalnego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0ec70-115">**Specialized VHD** - a specialized VHD maintains hello user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="0ec70-116">Jeśli planujesz toouse hello wirtualnego dysku twardego — jest toocreate nowej maszyny Wirtualnej, upewnij się, hello następujące kroki zostały zakończone.</span><span class="sxs-lookup"><span data-stu-id="0ec70-116">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span>  
    * <span data-ttu-id="0ec70-117">[Przygotowanie tooAzure tooupload wirtualnego dysku twardego Windows](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="0ec70-117">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md).</span></span> <span data-ttu-id="0ec70-118">**Nie** generalize hello maszyny Wirtualnej przy użyciu narzędzia Sysprep.</span><span class="sxs-lookup"><span data-stu-id="0ec70-118">**Do not** generalize hello VM using Sysprep.</span></span> 
    * <span data-ttu-id="0ec70-119">Usuń wszystkie narzędzia wirtualizacji gościa i agentów, które są zainstalowane na powitania maszyny Wirtualnej (np. narzędzi VMware).</span><span class="sxs-lookup"><span data-stu-id="0ec70-119">Remove any guest virtualization tools and agents that are installed on hello VM (i.e. VMware tools).</span></span> 
    * <span data-ttu-id="0ec70-120">Upewnij się, hello maszyna wirtualna jest skonfigurowana toopull jego adres IP i ustawienia DNS za pośrednictwem protokołu DHCP.</span><span class="sxs-lookup"><span data-stu-id="0ec70-120">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="0ec70-121">To zapewnia, że ten serwer hello uzyskuje adres IP w ramach hello sieci wirtualnej podczas uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="0ec70-121">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span>  


## <a name="export-and-download-hello-vhd"></a><span data-ttu-id="0ec70-122">Eksportowanie i Pobierz hello wirtualnego dysku twardego</span><span class="sxs-lookup"><span data-stu-id="0ec70-122">Export and download hello VHD</span></span> 

<span data-ttu-id="0ec70-123">Wyeksportuj hello EC2 wystąpienia tooa wirtualnego dysku twardego w zasobniku Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="0ec70-123">Export hello EC2 instance tooa VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="0ec70-124">Hello kroków opisanych w temacie dokumentacji Amazon hello [eksportowanie wystąpienia jako maszyny Wirtualnej przy użyciu maszyny Wirtualnej importu/eksportu](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) i wykonywania hello [tworzenie — wystąpienie export zadania](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) polecenia tooexport hello EC2 plik VHD tooa wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="0ec70-124">Follow hello steps described in hello Amazon documentation topic [Exporting an Instance as a VM Using VM Import/Export](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) and run hello [create-instance-export-task](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) command tooexport hello EC2 instance tooa VHD file.</span></span> 

<span data-ttu-id="0ec70-125">Witaj wyeksportowany plik wirtualnego dysku twardego jest zapisywany w zasobniku hello Amazon S3, które określisz.</span><span class="sxs-lookup"><span data-stu-id="0ec70-125">hello exported VHD file is saved in hello Amazon S3 bucket you specify.</span></span> <span data-ttu-id="0ec70-126">Witaj podstawowa składnia eksportowanie hello wirtualnego dysku twardego jest poniżej, po prostu zastąpić tekst zastępczy hello w <brackets> z informacjami.</span><span class="sxs-lookup"><span data-stu-id="0ec70-126">hello basic syntax for exporting hello VHD is below, just replace hello placeholder text in <brackets> with your information.</span></span>

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

<span data-ttu-id="0ec70-127">Po wyeksportowaniu hello wirtualnego dysku twardego, wykonaj te instrukcje hello [sposób pobrać obiektu z przedział S3?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) toodownload hello wirtualnego dysku twardego plik z zasobnika hello S3.</span><span class="sxs-lookup"><span data-stu-id="0ec70-127">Once hello VHD has been exported, follow hello instructions in [How Do I Download an Object from an S3 Bucket?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) toodownload hello VHD file from hello S3 bucket.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="0ec70-128">Usług AWS pobiera opłaty transferu danych do pobrania hello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="0ec70-128">AWS charges data transfer fees for downloading hello VHD.</span></span> <span data-ttu-id="0ec70-129">Zobacz [Amazon S3 cennik](https://aws.amazon.com/s3/pricing/) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="0ec70-129">See [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/) for more information.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0ec70-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0ec70-130">Next steps</span></span>

<span data-ttu-id="0ec70-131">Możesz teraz przekazać hello tooAzure wirtualnego dysku twardego i tworzenie nowej maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0ec70-131">Now you can upload hello VHD tooAzure and create a new VM.</span></span> 

- <span data-ttu-id="0ec70-132">Po przeprowadzeniu programu Sysprep w źródle zbyt**generalize** go przed wykonaniem operacji eksportowania, zobacz [przekazać uogólniony wirtualny dysk twardy i korzystać z niego toocreate nowych maszyn wirtualnych na platformie Azure](upload-generalized-managed.md)</span><span class="sxs-lookup"><span data-stu-id="0ec70-132">If you ran Sysprep on your source too**generalize** it before exporting, see [Upload a generalized VHD and use it toocreate a new VMs in Azure](upload-generalized-managed.md)</span></span>
- <span data-ttu-id="0ec70-133">Jeśli nie zostało uruchomione narzędzie Sysprep przed wykonaniem operacji eksportowania, hello wirtualnego dysku twardego jest traktowany jako **specjalne**, zobacz [przekazywanie specjalne tooAzure wirtualnego dysku twardego i utworzyć nową maszynę Wirtualną](create-vm-specialized.md)</span><span class="sxs-lookup"><span data-stu-id="0ec70-133">If you did not run Sysprep before exporting, hello VHD is considered **specialized**, see [Upload a specialized VHD tooAzure and create a new VM](create-vm-specialized.md)</span></span>

 
