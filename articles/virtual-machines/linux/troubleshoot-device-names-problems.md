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
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a>Rozwiązywanie problemów: Nazwy urządzenia maszyny Wirtualnej systemu Linux są zmieniane.

Artykuł Hello wyjaśnia, dlaczego nazwy urządzenia są zmieniane po ponownego uruchomienia maszyny wirtualnej systemu Linux (VM), lub podłącz hello dysków. Umożliwia także hello rozwiązania tego problemu.

## <a name="symptom"></a>Objaw

Mogą wystąpić następujące problemy podczas uruchamiania maszyn wirtualnych systemu Linux na platformie Microsoft Azure hello.

- Witaj maszyny Wirtualnej nie powiedzie się tooboot po ponownym uruchomieniu.

- Jeśli dyski danych są odłączyć i ponownie nałożona, hello nazwy urządzenia dla dysków są zmieniane.

- Aplikacja lub skrypt, który odwołuje się do dysku przy użyciu nazwy urządzenia nie powiedzie się. Okaże się, że hello zmiany nazwy urządzenia hello dysku.

## <a name="cause"></a>Przyczyna

Ścieżki urządzeń w systemie Linux nie ma gwarancji toobe spójne uruchomieniach. Nazwy urządzenia składają się z głównej (litera) i numery pomocniczych.  Sterownik urządzenia pamięci masowej Linux hello wykrycie nowego urządzenia przypisuje tooit numery główne i pomocnicze urządzenia z przedziału hello. Po usunięciu urządzenia, numery hello są zwalniane toobe ponownie później.

Witaj problem występuje, ponieważ hello urządzenia skanowanie w systemie Linux zaplanowane przez podsystem SCSI hello sytuacji asynchronicznie. Hello urządzenia ostateczne ścieżka nazw może się różnić uruchomieniach. 

## <a name="solution"></a>Rozwiązanie

tooresolve ten problem, Użyj trwałego nazewnictwa. Istnieją cztery metody toopersistent nazewnictwa - przez system plików etykietę, przez identyfikator uuid, według identyfikatora i ścieżkę. Zalecamy hello filesystem etykiety i metody UUID dla maszyn wirtualnych systemu Linux platformy Azure. 

Większości dystrybucji zapewniają również albo hello **nofail** lub **nobootwait** fstab opcje. Te opcje włączyć tooboot systemu, nawet w przypadku awarii dysku hello toomount podczas uruchamiania. Sprawdź dystrybucji hello dokumentację, aby uzyskać więcej informacji na temat tych parametrów. Aby uzyskać więcej informacji na temat tooconfigure toouse maszyny Wirtualnej systemu Linux UUID po dodaniu dysku danych, zobacz temat [połączyć toohello maszyny Wirtualnej systemu Linux toomount hello nowy dysk](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk). 

Po zainstalowaniu agenta systemu Linux Azure hello na maszynie Wirtualnej używa tooconstruct reguły Udev zestaw łącza symbolicznego pod **/dev/disk/azure**. Te reguły Udev mogą być używane przez aplikacje i skrypty tooidentify dyski są dołączone toohello maszyny Wirtualnej, ich typ i hello jednostki LUN.

## <a name="more-information"></a>Więcej informacji

### <a name="identify-disk-luns"></a>Identyfikowanie jednostek LUN dysku

Aplikacja może użyć toofind jednostek LUN wszystkich hello dołączonych dysków i tworzenia łącza symbolicznego. agent systemu Linux Azure Hello zawiera teraz udev reguł, które skonfigurowane linki symboliczne z urządzeń toohello jednostki LUN, w następujący sposób:

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
                                 

Informacje o jednostce LUN również można pobrać z hello Linux gościa za pomocą lsscsi lub podobne w następujący sposób.

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

Informacje o jednostce LUN to gościa może służyć z subskrypcji platformy Azure metadanych tooidentify hello lokalizacją w magazynie Azure hello wirtualnego dysku twardego, która przechowuje dane partycji hello. Na przykład użyć hello az interfejsu wiersza polecenia:

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

### <a name="discover-filesystem-uuids-by-using-blkid"></a>Odnajdywanie UUID systemu plików za pomocą blkid

Skryptu lub aplikacji może odczytywać dane wyjściowe hello blkid lub podobne źródeł informacji i utworzyć łącza symbolicznego w **/dev** do użycia. dane wyjściowe Hello pojawi się oznaczenie hello UUID wszystkich dysków dołączonych toohello maszyny Wirtualnej i hello urządzenia pliku toowhich są one powiązane:

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

reguły udev agenta waagent Hello utworzyć zestaw łącza symbolicznego pod **/dev/disk/azure**:


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


Aplikacja Hello tym informacjom można zidentyfikować urządzenia dysku rozruchowego hello i hello (efemeryczne) zasobu dysku. Na platformie Azure aplikacje powinny odwoływać się za**/dev/disk/azure/root-part1** lub **/dev/disk/azure-resource-part1** toodiscover tych partycji.

Jeśli są dodatkowe partycje z listy blkid hello, znajdują się one na dysk z danymi. Aplikacje można zachować hello UUID dla tych partycji i użyj ścieżki, takie jak hello poniżej nazwy urządzenia hello toodiscover w czasie wykonywania:

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-hello-latest-azure-storage-rules"></a>Pobierz najnowsze zasady usługi Azure storage hello

toohello najnowsze zasady usługi Azure storage, uruchom następujące polecenia th:

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


Aby uzyskać więcej informacji zobacz następujące artykuły hello:

- [Ubuntu: Przy użyciu identyfikatora UUID](https://help.ubuntu.com/community/UsingUUID)

- [Red Hat: Stałe nazewnictwa](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html)

- [Linux: Identyfikatory UUID czynności dla Ciebie](https://www.linux.com/news/what-uuids-can-do-you)

- [Udev: Wprowadzenie tooDevice zarządzania w nowoczesnych systemu Linux](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

