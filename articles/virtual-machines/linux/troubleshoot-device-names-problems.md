---
title: "nazwy urządzenia aaaLinux maszyny Wirtualnej są zmieniane na platformie Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono hello Dlaczego nazwy urządzenia zostaną zmienione i stanowią rozwiązanie tego problemu."
services: virtual-machines-linux
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: 
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 4d3a5853d61edd2c8e8b85ab69e5ed3b3bc00bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a><span data-ttu-id="8dd61-103">Rozwiązywanie problemów: Nazwy urządzenia maszyny Wirtualnej systemu Linux są zmieniane.</span><span class="sxs-lookup"><span data-stu-id="8dd61-103">Troubleshooting: Linux VM device names are changed</span></span>

<span data-ttu-id="8dd61-104">Artykuł Hello wyjaśnia, dlaczego nazwy urządzenia są zmieniane po ponownego uruchomienia maszyny wirtualnej systemu Linux (VM), lub podłącz hello dysków.</span><span class="sxs-lookup"><span data-stu-id="8dd61-104">hello article explains why device names are changed after you restart a Linux virtual machine (VM), or reattach hello disks.</span></span> <span data-ttu-id="8dd61-105">Umożliwia także hello rozwiązania tego problemu.</span><span class="sxs-lookup"><span data-stu-id="8dd61-105">It also provides hello solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="8dd61-106">Objaw</span><span class="sxs-lookup"><span data-stu-id="8dd61-106">Symptom</span></span>

<span data-ttu-id="8dd61-107">Mogą wystąpić następujące problemy podczas uruchamiania maszyn wirtualnych systemu Linux na platformie Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8dd61-107">You may experience hello following problems when running Linux VMs in Microsoft Azure.</span></span>

- <span data-ttu-id="8dd61-108">Witaj maszyny Wirtualnej nie powiedzie się tooboot po ponownym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="8dd61-108">hello VM fails tooboot after a restart.</span></span>

- <span data-ttu-id="8dd61-109">Jeśli dyski danych są odłączyć i ponownie nałożona, hello nazwy urządzenia dla dysków są zmieniane.</span><span class="sxs-lookup"><span data-stu-id="8dd61-109">If data disks are detached and reattached, hello devices names for disks are changed.</span></span>

- <span data-ttu-id="8dd61-110">Aplikacja lub skrypt, który odwołuje się do dysku przy użyciu nazwy urządzenia nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="8dd61-110">An application or script that references a disk by using device name fails.</span></span> <span data-ttu-id="8dd61-111">Okaże się, że hello zmiany nazwy urządzenia hello dysku.</span><span class="sxs-lookup"><span data-stu-id="8dd61-111">You find that hello device name of hello disk is changed.</span></span>

## <a name="cause"></a><span data-ttu-id="8dd61-112">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="8dd61-112">Cause</span></span>

<span data-ttu-id="8dd61-113">Ścieżki urządzeń w systemie Linux nie ma gwarancji toobe spójne uruchomieniach.</span><span class="sxs-lookup"><span data-stu-id="8dd61-113">Device paths in Linux are not guaranteed toobe consistent across restarts.</span></span> <span data-ttu-id="8dd61-114">Nazwy urządzenia składają się z głównej (litera) i numery pomocniczych.</span><span class="sxs-lookup"><span data-stu-id="8dd61-114">Device names consist of major (letter) and minor numbers.</span></span>  <span data-ttu-id="8dd61-115">Sterownik urządzenia pamięci masowej Linux hello wykrycie nowego urządzenia przypisuje tooit numery główne i pomocnicze urządzenia z przedziału hello.</span><span class="sxs-lookup"><span data-stu-id="8dd61-115">When hello Linux storage device driver detects a new device, it assigns major and minor device numbers tooit from hello available range.</span></span> <span data-ttu-id="8dd61-116">Po usunięciu urządzenia, numery hello są zwalniane toobe ponownie później.</span><span class="sxs-lookup"><span data-stu-id="8dd61-116">When a device is removed, hello device numbers are freed toobe reused later.</span></span>

<span data-ttu-id="8dd61-117">Witaj problem występuje, ponieważ hello urządzenia skanowanie w systemie Linux zaplanowane przez podsystem SCSI hello sytuacji asynchronicznie.</span><span class="sxs-lookup"><span data-stu-id="8dd61-117">hello problem occurs because hello device scanning in Linux scheduled by hello SCSI subsystem happens asynchronously.</span></span> <span data-ttu-id="8dd61-118">Hello urządzenia ostateczne ścieżka nazw może się różnić uruchomieniach.</span><span class="sxs-lookup"><span data-stu-id="8dd61-118">hello final device path naming may vary across restarts.</span></span> 

## <a name="solution"></a><span data-ttu-id="8dd61-119">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="8dd61-119">Solution</span></span>

<span data-ttu-id="8dd61-120">tooresolve ten problem, Użyj trwałego nazewnictwa.</span><span class="sxs-lookup"><span data-stu-id="8dd61-120">tooresolve this problem, use persistent naming.</span></span> <span data-ttu-id="8dd61-121">Istnieją cztery metody toopersistent nazewnictwa - przez system plików etykietę, przez identyfikator uuid, według identyfikatora i ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="8dd61-121">There are four methods toopersistent naming - by filesystem label, by uuid, by id and by path.</span></span> <span data-ttu-id="8dd61-122">Zalecamy hello filesystem etykiety i metody UUID dla maszyn wirtualnych systemu Linux platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8dd61-122">We recommend hello filesystem label and UUID methods for Azure Linux VMs.</span></span> 

<span data-ttu-id="8dd61-123">Większości dystrybucji zapewniają również albo hello **nofail** lub **nobootwait** fstab opcje.</span><span class="sxs-lookup"><span data-stu-id="8dd61-123">Most distributions also provide either hello **nofail** or **nobootwait** fstab options.</span></span> <span data-ttu-id="8dd61-124">Te opcje włączyć tooboot systemu, nawet w przypadku awarii dysku hello toomount podczas uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="8dd61-124">These options enable a system tooboot even if hello disk fails toomount at startup.</span></span> <span data-ttu-id="8dd61-125">Sprawdź dystrybucji hello dokumentację, aby uzyskać więcej informacji na temat tych parametrów.</span><span class="sxs-lookup"><span data-stu-id="8dd61-125">Check hello distribution's documentation for more information about these parameters.</span></span> <span data-ttu-id="8dd61-126">Aby uzyskać więcej informacji na temat tooconfigure toouse maszyny Wirtualnej systemu Linux UUID po dodaniu dysku danych, zobacz temat [połączyć toohello maszyny Wirtualnej systemu Linux toomount hello nowy dysk](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="8dd61-126">For more information about how tooconfigure a Linux VM toouse a UUID when you add a data disk, see [Connect toohello Linux VM toomount hello new disk](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> 

<span data-ttu-id="8dd61-127">Po zainstalowaniu agenta systemu Linux Azure hello na maszynie Wirtualnej używa tooconstruct reguły Udev zestaw łącza symbolicznego pod **/dev/disk/azure**.</span><span class="sxs-lookup"><span data-stu-id="8dd61-127">When hello Azure Linux agent is installed on a VM, it uses Udev rules tooconstruct a set of symbolic links under **/dev/disk/azure**.</span></span> <span data-ttu-id="8dd61-128">Te reguły Udev mogą być używane przez aplikacje i skrypty tooidentify dyski są dołączone toohello maszyny Wirtualnej, ich typ i hello jednostki LUN.</span><span class="sxs-lookup"><span data-stu-id="8dd61-128">These Udev rules can be used by applications and scripts tooidentify disks are attached toohello VM, their type, and hello LUN.</span></span>

## <a name="more-information"></a><span data-ttu-id="8dd61-129">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="8dd61-129">More information</span></span>

### <a name="identify-disk-luns"></a><span data-ttu-id="8dd61-130">Identyfikowanie jednostek LUN dysku</span><span class="sxs-lookup"><span data-stu-id="8dd61-130">Identify disk LUNs</span></span>

<span data-ttu-id="8dd61-131">Aplikacja może użyć toofind jednostek LUN wszystkich hello dołączonych dysków i tworzenia łącza symbolicznego.</span><span class="sxs-lookup"><span data-stu-id="8dd61-131">An application can use LUNs toofind all hello attached disks and constructing symbolic links.</span></span> <span data-ttu-id="8dd61-132">agent systemu Linux Azure Hello zawiera teraz udev reguł, które skonfigurowane linki symboliczne z urządzeń toohello jednostki LUN, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="8dd61-132">hello Azure Linux agent now includes udev rules that set up symbolic links from a LUN toohello devices, as follows:</span></span>

    $ tree /dev/disk/azure

    /dev/disk/azure
    ├── resource -> ../../sdb
    ├── resource-part1 -> ../../sdb1
    ├── root -> ../../sda
    ├── root-part1 -> ../../sda1
    └── scsi1
        ├── lun0 -> ../../../sdc
        ├── lun0-part1 -> ../../../sdc1
        ├── lun1 -> ../../../sdd
        ├── lun1-part1 -> ../../../sdd1
        ├── lun1-part2 -> ../../../sdd2
        └── lun1-part3 -> ../../../sdd3                                    
                                 

<span data-ttu-id="8dd61-133">Informacje o jednostce LUN również można pobrać z hello Linux gościa za pomocą lsscsi lub podobne w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="8dd61-133">LUN information can also be retrieved from hello Linux guest using lsscsi or similar tool as follows.</span></span>

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

<span data-ttu-id="8dd61-134">Informacje o jednostce LUN to gościa może służyć z subskrypcji platformy Azure metadanych tooidentify hello lokalizacją w magazynie Azure hello wirtualnego dysku twardego, która przechowuje dane partycji hello.</span><span class="sxs-lookup"><span data-stu-id="8dd61-134">This guest LUN information can be used with Azure subscription metadata tooidentify hello location in Azure storage of hello VHD which stores hello partition data.</span></span> <span data-ttu-id="8dd61-135">Na przykład użyć hello az interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="8dd61-135">For example, use hello az cli:</span></span>

    $ az vm show --resource-group testVM --name testVM | jq -r .storageProfile.dataDisks                                        
    [                                                                                                                                                                  
    {                                                                                                                                                                  
    "caching": "None",                                                                                                                                              
      "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 1023,                                                                                                                                             
      "image": null,                                                                                                                                                   
    "lun": 0,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-114353",                                                                                                                    
    "vhd": {                                                                                                                                                          
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-114353.vhd"                                                       
    }                                                                                                                                                              
    },                                                                                                                                                                
    {                                                                                                                                                                   
    "caching": "None",                                                                                                                                               
    "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 512,                                                                                                                                              
    "image": null,                                                                                                                                                   
    "lun": 1,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-121516",                                                                                                                    
    "vhd": {                                                                                                                                                           
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-121516.vhd"                                                       
      }                                                                                                                                                             
      }                                                                                                                                                             
    ]

### <a name="discover-filesystem-uuids-by-using-blkid"></a><span data-ttu-id="8dd61-136">Odnajdywanie UUID systemu plików za pomocą blkid</span><span class="sxs-lookup"><span data-stu-id="8dd61-136">Discover filesystem UUIDs by using blkid</span></span>

<span data-ttu-id="8dd61-137">Skryptu lub aplikacji może odczytywać dane wyjściowe hello blkid lub podobne źródeł informacji i utworzyć łącza symbolicznego w **/dev** do użycia.</span><span class="sxs-lookup"><span data-stu-id="8dd61-137">A script or application can read hello output of blkid, or similar sources of information, and construct symbolic links in **/dev** for use.</span></span> <span data-ttu-id="8dd61-138">dane wyjściowe Hello pojawi się oznaczenie hello UUID wszystkich dysków dołączonych toohello maszyny Wirtualnej i hello urządzenia pliku toowhich są one powiązane:</span><span class="sxs-lookup"><span data-stu-id="8dd61-138">hello output will show hello UUIDs of all disks attached toohello VM and hello device file toowhich they are associated:</span></span>

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

<span data-ttu-id="8dd61-139">reguły udev agenta waagent Hello utworzyć zestaw łącza symbolicznego pod **/dev/disk/azure**:</span><span class="sxs-lookup"><span data-stu-id="8dd61-139">hello waagent udev rules construct a set of symbolic links under **/dev/disk/azure**:</span></span>


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


<span data-ttu-id="8dd61-140">Aplikacja Hello tym informacjom można zidentyfikować urządzenia dysku rozruchowego hello i hello (efemeryczne) zasobu dysku.</span><span class="sxs-lookup"><span data-stu-id="8dd61-140">hello application can use this information identify hello boot disk device and hello resource (ephemeral) disk.</span></span> <span data-ttu-id="8dd61-141">Na platformie Azure aplikacje powinny odwoływać się za**/dev/disk/azure/root-part1** lub **/dev/disk/azure-resource-part1** toodiscover tych partycji.</span><span class="sxs-lookup"><span data-stu-id="8dd61-141">In Azure, applications should refer too**/dev/disk/azure/root-part1** or **/dev/disk/azure-resource-part1** toodiscover these partitions.</span></span>

<span data-ttu-id="8dd61-142">Jeśli są dodatkowe partycje z listy blkid hello, znajdują się one na dysk z danymi.</span><span class="sxs-lookup"><span data-stu-id="8dd61-142">If there are additional partitions from hello blkid list, they reside on a data disk.</span></span> <span data-ttu-id="8dd61-143">Aplikacje można zachować hello UUID dla tych partycji i użyj ścieżki, takie jak hello poniżej nazwy urządzenia hello toodiscover w czasie wykonywania:</span><span class="sxs-lookup"><span data-stu-id="8dd61-143">Applications can maintain hello UUID for these partitions and use a path like hello below toodiscover hello device name at runtime:</span></span>

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-hello-latest-azure-storage-rules"></a><span data-ttu-id="8dd61-144">Pobierz najnowsze zasady usługi Azure storage hello</span><span class="sxs-lookup"><span data-stu-id="8dd61-144">Get hello latest Azure storage rules</span></span>

<span data-ttu-id="8dd61-145">toohello najnowsze zasady usługi Azure storage, uruchom następujące polecenia th:</span><span class="sxs-lookup"><span data-stu-id="8dd61-145">toohello latest Azure storage rules, run th following commands:</span></span>

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


<span data-ttu-id="8dd61-146">Aby uzyskać więcej informacji zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="8dd61-146">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="8dd61-147">Ubuntu: Przy użyciu identyfikatora UUID</span><span class="sxs-lookup"><span data-stu-id="8dd61-147">Ubuntu: Using UUID</span></span>](https://help.ubuntu.com/community/UsingUUID)

- [<span data-ttu-id="8dd61-148">Red Hat: Stałe nazewnictwa</span><span class="sxs-lookup"><span data-stu-id="8dd61-148">Red Hat: Persistent Naming</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)

- [<span data-ttu-id="8dd61-149">Linux: Identyfikatory UUID czynności dla Ciebie</span><span class="sxs-lookup"><span data-stu-id="8dd61-149">Linux: What UUIDs can do for you</span></span>](https://www.linux.com/news/what-uuids-can-do-you)

- [<span data-ttu-id="8dd61-150">Udev: Wprowadzenie tooDevice zarządzania w nowoczesnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="8dd61-150">Udev: Introduction tooDevice Management In Modern Linux System</span></span>](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

