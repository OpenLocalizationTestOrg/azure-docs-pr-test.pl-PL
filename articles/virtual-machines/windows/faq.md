---
title: aaaFAQ o maszyn wirtualnych systemu Windows na platformie Azure | Dokumentacja firmy Microsoft
description: "Udostępnia toosome odpowiedzi z hello często zadawane pytania dotyczące systemu Windows maszyny wirtualne utworzone za pomocą modelu usługi Resource Manager hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 757da816-a050-4889-a010-6f75d7978eb7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: cynthn
ms.openlocfilehash: ee366a04bda347ce2be07bde4fc6bad306cc1da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-windows-virtual-machines"></a>Często zadawane pytania dotyczące maszyn wirtualnych systemu Windows
W tym artykule opisano często zadawane pytania dotyczące utworzona na platformie Azure przy użyciu modelu wdrażania usługi Resource Manager hello maszyn wirtualnych systemu Windows. Wersja systemu Linux hello tego tematu dla [często zadawane pytania dotyczące maszyn wirtualnych systemu Linux](../linux/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="what-can-i-run-on-an-azure-vm"></a>Co mogę uruchomić na maszynie wirtualnej platformy Azure?
Wszyscy subskrybenci mogą uruchomić oprogramowanie serwerowe na maszynie wirtualnej platformy Azure. Informacje hello zasady udzielania pomocy technicznej dla uruchomione oprogramowanie serwera firmy Microsoft na platformie Azure, zobacz [obsługi oprogramowania Microsoft server maszyn wirtualnych platformy Azure](https://support.microsoft.com/kb/2721672)

Określonych wersji systemu Windows 7, Windows 8.1 i Windows 10 są dostępne tooMSDN Azure korzyści subskrybentów i subskrybentów MSDN: Programowanie i testowanie płatność za rzeczywiste użycie, dla zadań tworzenia i testowania. Aby uzyskać szczegółowe informacje, łącznie z instrukcjami i ograniczeniami, zobacz [Windows Client images for MSDN subscribers](http://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/) (Obrazy klienta systemu Windows dla subskrybentów MSDN). 

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>Ile pamięci masowej mogę użyć w maszynie wirtualnej?
Każdy dysk danych można się too1 TB. Witaj liczba dysków z danymi, których można używać zależy od rozmiaru hello hello maszyny wirtualnej. Aby uzyskać szczegółowe informacje, zobacz [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Rozmiary maszyn wirtualnych).

Dyskach zarządzanych platformy Azure są hello nowy i zalecane dysku magazynu ofert do użytku z maszyn wirtualnych platformy Azure dla trwałego magazynu danych. W każdej maszynie wirtualnej możesz używać wielu dysków Managed Disks. Usługa Managed Disks oferuje dwa typy opcji magazynu trwałego: dyski Managed Disks w warstwie Premium i Standardowa. Aby uzyskać informacje o cenach, zobacz [zarządzane cennik dysków](https://azure.microsoft.com/pricing/details/managed-disks).

Konta magazynu platformy Azure można również magazynowanie hello dysku systemu operacyjnego i dysków z danymi. Każdy dysk jest plikiem VHD przechowywanym jako stronicowy obiekt blob. Aby uzyskać szczegółowe informacje o cenach, zobacz [Szczegóły cennika magazynu](https://azure.microsoft.com/pricing/details/storage/).

## <a name="how-can-i-access-my-virtual-machine"></a>Jak można uzyskać dostęp Moja maszyna wirtualna?
Ustanowić połączenia zdalnego przy użyciu usługi Podłączanie pulpitu zdalnego (RDP) dla maszyny Wirtualnej systemu Windows. Aby uzyskać instrukcje, zobacz [jak dziennika na tooan wirtualnej platformy Azure i tooconnect maszyny, systemem operacyjnym Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Obsługuje maksymalnie dwóch jednoczesnych połączeń, chyba że hello serwer jest skonfigurowany jako host sesji usług pulpitu zdalnego.  

Jeśli masz problemy z pulpitu zdalnego, zobacz [tooa połączeń pulpitu zdalnego Rozwiązywanie problemów z maszyny wirtualnej z systemem Windows Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Jeśli znasz funkcji Hyper-V, zapoznają się dla narzędzia tooVMConnect podobne. Azure nie oferuje podobne narzędzie, ponieważ maszyna wirtualna tooa dostępu do konsoli nie jest obsługiwana.

## <a name="can-i-use-hello-temporary-disk-hello-d-drive-by-default-toostore-data"></a>Można użyć hello dysku tymczasowym (hello dysku D: domyślnie) toostore danych?
Nie używaj hello dysku tymczasowym toostore danych. Jest tylko magazyn tymczasowy, czy istnieje ryzyko utraty danych, która nie może zostać odzyskany. Podczas przenoszenia maszyny wirtualnej hello tooa inny host, może wystąpić utrata danych. Zmiana rozmiaru maszyny wirtualnej, aktualizowania hosta hello lub awaria sprzętu na hoście hello są niektóre przyczyny hello może przenieść maszynę wirtualną.

Jeśli masz aplikację, która wymaga litery dysku D: hello toouse, tak aby hello dysku tymczasowym używane inną niż D: można ponownie przypisać litery dysku. Aby uzyskać instrukcje, zobacz [zmiany hello literę dysku tymczasowym systemu Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).


## <a name="how-can-i-change-hello-drive-letter-of-hello-temporary-disk"></a>Jak zmienić hello litera dysku tymczasowego hello?
Można zmienić literę dysku hello przez przenoszenie pliku strony hello i ponowne przypisywanie litery dysku, ale należy toomake się, że hello kroki w określonej kolejności. Aby uzyskać instrukcje, zobacz [zmiany hello literę dysku tymczasowym systemu Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="can-i-add-an-existing-vm-tooan-availability-set"></a>Można dodać istniejącego zestawu dostępności tooan maszyny Wirtualnej?
Nie. Jeśli chcesz, aby maszyna wirtualna z toobe częścią zestawu dostępności, należy toocreate hello maszyny Wirtualnej w zestawie hello. Obecnie nie ma tooadd sposób dostępności tooan maszyny Wirtualnej, po jego utworzeniu.

## <a name="can-i-upload-a-virtual-machine-tooazure"></a>Można przekazać tooAzure maszyny wirtualnej?
Tak. Aby uzyskać instrukcje, zobacz [Migrowanie lokalnych maszyn wirtualnych tooAzure](on-prem-to-azure.md).

## <a name="can-i-resize-hello-os-disk"></a>Czy można zmienić rozmiar dysku systemu operacyjnego hello?
Tak. Aby uzyskać instrukcje, zobacz [jak tooexpand hello dysku systemu operacyjnego maszyny wirtualnej w grupie zasobów Azure](expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a>Można skopiować lub sklonować istniejącą maszynę Wirtualną platformy Azure?
Tak. Przy użyciu zarządzanych obrazów, można utworzyć obrazu maszyny wirtualnej, a następnie użyć toobuild obraz powitania wiele nowych maszyn wirtualnych. Aby uzyskać instrukcje, zobacz [utworzyć niestandardowy obraz maszyny wirtualnej](tutorial-custom-images.md).

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a>Dlaczego nie widzę centralnej Zjednoczone i Kanada Wschodnia regionów za pośrednictwem usługi Azure Resource Manager?

Hello dwóch regionach nowej centralnej Zjednoczone i Kanada Wschodnia nie są automatycznie zarejestrowany dla tworzenia maszyny wirtualnej dla istniejącej subskrypcji platformy Azure. Rejestracja odbywa się automatycznie podczas wdrażania maszyny wirtualnej za pośrednictwem hello Azure tooany portalu innego regionu przy użyciu usługi Azure Resource Manager. Po maszyny wirtualnej jest wdrożony tooany innego regionu Azure, nowych regionów hello powinny być dostępne dla kolejnych maszyn wirtualnych.

## <a name="does-azure-support-linux-vms"></a>Azure obsługuje maszyn wirtualnych systemu Linux?
Tak. tootry maszyny Wirtualnej systemu Linux, wychodzących, zobacz Tworzenie tooquickly [Utwórz Maszynę wirtualną systemu Linux na platformie Azure przy użyciu hello Portal](../linux/quick-create-portal.md).

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a>Toomy karty Sieciowej maszyny Wirtualnej można dodać po jej utworzeniu?
Tak, obecnie jest to możliwe. deallocated zatrzymana pierwszy toobe potrzeb Hello maszyny Wirtualnej. Następnie można dodać lub usunąć karty Sieciowej (chyba że jest hello ostatniego karty Sieciowej na powitania maszyny Wirtualnej). 

## <a name="are-there-any-computer-name-requirements"></a>Czy istnieją wszystkie wymagania dotyczące nazwy komputera?
Tak. Witaj, nazwa komputera może zawierać maksymalnie 15 znaków. Zobacz [nazewnictwa konwencje reguły i ograniczenia](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) uzyskać więcej informacji dotyczących nazw zasobów.

## <a name="are-there-any-resource-group-name-requirements"></a>Czy istnieją dowolnego zasobu wymagania dotyczące nazw grupy?
Tak. Nazwa grupy zasobów Hello może zawierać maksymalnie 90 znaków długości. Zobacz [nazewnictwa konwencje reguły i ograniczenia](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Aby uzyskać więcej informacji na temat grup zasobów.

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a>Jakie są wymagania username hello, podczas tworzenia maszyny Wirtualnej?

Nazwy użytkowników nie może przekraczać 20 znaków długości i nie może kończyć się kropką ("."). 


Witaj następujące nazwy użytkowników nie są dozwolone:
<table>
    <tr>
        <td style="text-align:center">Administrator </td><td style="text-align:center"> Administrator </td><td style="text-align:center"> Użytkownika </td><td style="text-align:center"> Użytkownik1</td>
    </tr>
    <tr>
        <td style="text-align:center">Test </td><td style="text-align:center"> UŻYTKOWNIK2 </td><td style="text-align:center"> Test1 </td><td style="text-align:center"> UŻYTKOWNIK3</td>
    </tr>    <tr>
        <td style="text-align:center">admin1 </td><td style="text-align:center"> 1 </td><td style="text-align:center"> 123 </td><td style="text-align:center"> A</td>
    </tr>
    <tr>
        <td style="text-align:center">actuser  </td><td style="text-align:center"> usługi adm </td><td style="text-align:center"> admin2 </td><td style="text-align:center"> ASPNET</td>
    </tr>
    <tr>
        <td style="text-align:center">kopia zapasowa </td><td style="text-align:center"> Konsoli </td><td style="text-align:center"> ADAM </td><td style="text-align:center"> Gość</td>
    </tr>
    <tr>
        <td style="text-align:center">Jan </td><td style="text-align:center"> Właściciel </td><td style="text-align:center"> główny </td><td style="text-align:center"> serwer</td>
    </tr>
    <tr>
        <td style="text-align:center">SQL </td><td style="text-align:center"> Obsługa </td><td style="text-align:center"> support_388945a0 </td><td style="text-align:center"> sys</td>
    </tr>
    <tr>
        <td style="text-align:center">Test2 </td><td style="text-align:center"> test3 </td><td style="text-align:center"> user4 </td><td style="text-align:center"> user5</td>
    </tr>
</table>

## <a name="what-are-hello-password-requirements-when-creating-a-vm"></a>Jakie są wymagania dotyczące hasła hello podczas tworzenia maszyny Wirtualnej?
Hasła muszą być 12 123 znaków długości i spełnić 3 poza hello następujące wymagania dotyczące złożoności 4:

* Mieć niższe znaków
* Ma górny znaków
* Zawierać cyfrę
* Ma znak specjalny (wyrażenie regularne zgodne [\W_])

Witaj następującego hasła nie są dozwolone:

<table>
    <tr>
        <td>abc@123 </td>
        <td>P@$$w0rd </td>
        <td>P@ssw0rd </td>
        <td>P@ssword123 </td>
        <td>Pa$ $word </td>
    </tr>
    <tr>
        <td>pass@word1 </td>
        <td>Hasło! </td>
        <td>Password1 </td>
        <td>Password22 </td>
        <td>ILOVEYOU! </td>
    </tr>
</table>
