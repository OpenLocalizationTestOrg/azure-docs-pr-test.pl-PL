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
# <a name="how-tooreset-local-linux-password-on-azure-vms"></a>Jak hasło lokalne Linux tooreset na maszynach wirtualnych Azure

W tym artykule przedstawiono kilka metod tooreset lokalnych maszyn wirtualnych systemu Linux (VM) hasła. Jeśli konto użytkownika hello wygasło lub chcesz toocreate nowe konto, można użyć hello następujące metody toocreate nowe konto administratora lokalnego i ponowne uzyskanie dostępu toohello maszyny Wirtualnej.

## <a name="symptoms"></a>Objawy

Nie można zalogować się toohello maszyny Wirtualnej i pojawi się komunikat, który wskazuje, że to hasło hello, który został użyty jest niepoprawny. Ponadto nie można użyć VMAgent tooreset hasła na powitania portalu Azure. 

## <a name="manual-password-reset-procedure"></a>Procedury ręcznego resetowania hasła

1.  Usuń hello maszyny Wirtualnej i Zachowaj hello dołączonych dysków.

2.  Dołącz hello dysk systemu operacyjnego jako tooanother dysku danych czasowych maszyny Wirtualnej w ramach hello tej samej lokalizacji.

3.  Uruchom następujące polecenie SSH na powitania tymczasowa maszyna wirtualna toobecome hello nadtypem użytkownika.


    ~~~~
    sudo su
    ~~~~

4.  Uruchom **fdisk -l** lub przyjrzeć hello toofind dzienniki systemu nowo dołączono dysk. Zlokalizuj toomount nazwa dysku hello. Następnie na powitania danych czasowych maszyny Wirtualnej, poszukaj w odpowiednich hello pliku dziennika.

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    Witaj poniżej przedstawiono przykładowe dane wyjściowe polecenia grep hello:

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  Utwórz punkt instalacji o nazwie **tempmount**.

    ~~~~
    mkdir /tempmount
    ~~~~

6.  Zainstaluj dysk hello systemu operacyjnego w punkcie instalacji hello. Zazwyczaj wymaga toomount sdc1 lub sdc2. Zależy to hello hosting partycji w katalogu/etc z hello maszyny uszkodzenie dysku.

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  Wykonaj kopię zapasową przed wprowadzeniem jakichkolwiek zmian:

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  Resetowanie hasła hello użytkownika, które są potrzebne:

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  Przenieś hello zmodyfikowane pliki toohello właściwych lokalizacjach na powitania uszkodzony dysk na komputerze.

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back toohello root and unmount hello disk.

    ~~~~
    dysk CD / umount /tempmount
    ~~~~

11. Detach hello disk from hello management portal.

12. Recreate hello VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk tooanother Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How toodelete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)
