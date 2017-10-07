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
# <a name="frequently-asked-question-about-linux-virtual-machines"></a>Często zadawane pytania dotyczące maszyn wirtualnych systemu Linux
W tym artykule opisano często zadawane pytania dotyczące maszyn wirtualnych systemu Linux utworzone na platformie Azure przy użyciu modelu wdrażania usługi Resource Manager hello. Wersja systemu Windows hello tego tematu dla [często zadawane pytania dotyczące maszyn wirtualnych systemu Windows](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="what-can-i-run-on-an-azure-vm"></a>Co mogę uruchomić na maszynie wirtualnej platformy Azure?
Wszyscy subskrybenci mogą uruchomić oprogramowanie serwerowe na maszynie wirtualnej platformy Azure. Aby uzyskać więcej informacji, zobacz [systemu Linux na Azure-Endorsed dystrybucji](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a>Ile pamięci masowej mogę użyć w maszynie wirtualnej?
Każdy dysk danych można się too1 TB. Witaj liczba dysków z danymi, których można używać zależy od rozmiaru hello hello maszyny wirtualnej. Aby uzyskać szczegółowe informacje, zobacz [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Rozmiary maszyn wirtualnych).

Konto usługi Azure storage udostępnia magazyn hello dysku systemu operacyjnego i dysków z danymi. Każdy dysk jest plikiem VHD przechowywanym jako stronicowy obiekt blob. Aby uzyskać szczegółowe informacje o cenach, zobacz [Szczegóły cennika magazynu](https://azure.microsoft.com/pricing/details/storage/).

## <a name="how-can-i-access-my-virtual-machine"></a>Jak można uzyskać dostęp Moja maszyna wirtualna?
Ustanów toolog połączenia zdalnego, na maszynie wirtualnej toohello, przy użyciu protokołu Secure Shell (SSH). Zobacz hello instrukcje na temat tooconnect [z systemu Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub [z systemami Linux i komputerów Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Domyślnie protokół SSH umożliwia maksymalnie 10 równoczesnych połączeń. Można zwiększyć tę liczbę, edytując hello pliku konfiguracji.

Jeśli masz problemy, zapoznaj się [Rozwiązywanie problemów z Secure Shell (SSH) połączenia](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="can-i-use-hello-temporary-disk-devsdb1-toostore-data"></a>Można użyć hello dysku tymczasowym (/ dev/sdb1) toostore danych?
Nie używaj hello dysku tymczasowym (/ dev/sdb1) toostore danych. Jest dostępne tylko do tymczasowego przechowywania. Istnieje ryzyko utraty danych, która nie może zostać odzyskany.

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a>Można skopiować lub sklonować istniejącą maszynę Wirtualną platformy Azure?
Tak. Aby uzyskać instrukcje, zobacz [jak toocreate kopia maszyny wirtualnej systemu Linux w hello modelu wdrażania usługi Resource Manager](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a>Dlaczego nie widzę centralnej Zjednoczone i Kanada Wschodnia regionów za pośrednictwem usługi Azure Resource Manager?
Hello dwóch regionach nowej centralnej Zjednoczone i Kanada Wschodnia nie są automatycznie zarejestrowany dla tworzenia maszyny wirtualnej dla istniejącej subskrypcji platformy Azure. Rejestracja odbywa się automatycznie podczas wdrażania maszyny wirtualnej za pośrednictwem hello Azure tooany portalu innego regionu przy użyciu usługi Azure Resource Manager. Po maszyny wirtualnej jest wdrożony tooany innego regionu Azure, nowych regionów hello powinny być dostępne dla kolejnych maszyn wirtualnych.

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a>Toomy karty Sieciowej maszyny Wirtualnej można dodać po jej utworzeniu?
Tak, obecnie jest to możliwe. deallocated zatrzymana pierwszy toobe potrzeb Hello maszyny Wirtualnej. Następnie można dodać lub usunąć karty Sieciowej (chyba że jest hello ostatniego karty Sieciowej na powitania maszyny Wirtualnej). 

## <a name="are-there-any-computer-name-requirements"></a>Czy istnieją wszystkie wymagania dotyczące nazwy komputera?
Tak. Witaj, nazwa komputera może zawierać maksymalnie z 64 znaków. Zobacz [nazewnictwa konwencje reguły i ograniczenia](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) uzyskać więcej informacji dotyczących nazw zasobów.

## <a name="are-there-any-resource-group-name-requirements"></a>Czy istnieją dowolnego zasobu wymagania dotyczące nazw grupy?
Tak. Nazwa grupy zasobów Hello może zawierać maksymalnie 90 znaków długości. Zobacz [nazewnictwa konwencje reguły i ograniczenia](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Aby uzyskać więcej informacji na temat grup zasobów.

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a>Jakie są wymagania username hello, podczas tworzenia maszyny Wirtualnej?
Nazwy użytkowników musi być 1 do 64 znaków.

Witaj następujące nazwy użytkowników nie są dozwolone:

<table>
    <tr>
        <td style="text-align:center">Administrator </td><td style="text-align:center"> Administrator </td><td style="text-align:center"> Użytkownika </td><td style="text-align:center"> Użytkownik1</td>
    </tr>
    <tr>
        <td style="text-align:center">Test </td><td style="text-align:center"> UŻYTKOWNIK2 </td><td style="text-align:center"> Test1 </td><td style="text-align:center"> UŻYTKOWNIK3</td>
    </tr>
    <tr>
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
Hasła muszą być 6-72 znaków i spełnić 3 poza hello następujące wymagania dotyczące złożoności 4:

* Mieć niższe znaków
* Ma górny znaków
* Zawierać cyfrę
* Ma znak specjalny (wyrażenie regularne zgodne [\W_])

Witaj następującego hasła nie są dozwolone:

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center">P@$$w0rd</td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center">Pa$ $word</td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center">Hasło!</td>
        <td style="text-align:center">Password1</td>
        <td style="text-align:center">Password22</td>
        <td style="text-align:center">ILOVEYOU!</td>
    </tr>
</table>
