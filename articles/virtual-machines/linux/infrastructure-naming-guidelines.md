---
title: "zasady — Linux nazewnictwa infrastruktury aaaAzure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat hello klucza projekt i implementację zasady nazewnictwa w usług infrastruktury platformy Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ee4fb1-8297-49a1-8d3f-097880be67c7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 333146e7b2071e43527a5d7dc2ec02ebfb316eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-linux-vms"></a>Zasady nazewnictwa dla maszyn wirtualnych systemu Linux infrastruktury platformy Azure 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Ten artykuł koncentruje się na konfiguracji tooapproach konwencje nazewnictwa dla wszystkich sieci różnych zasobów Azure toobuild a logicznych i identyfikację zasobów w danym środowisku.

## <a name="implementation-guidelines-for-naming-conventions"></a>Implementacja — wskazówki dla konwencje nazewnictwa
Decyzje:

* Co to są konwencji nazewnictwa dla zasobów platformy Azure?

Zadania:

* Zdefiniuj toouse afiksów hello między spójności toomaintain Twojego zasobów.
* Zdefiniuj konto magazynu, że podane nazwy hello wymaganie dla nich toobe globalnie unikatowe.
* Dokument hello toobe konwencji nazewnictwa używane i rozpowszechniają spójności tooensure uczestniczących stron tooall wdrożeń.

## <a name="naming-conventions"></a>Konwencje nazewnictwa
Przed utworzeniem jakichkolwiek na platformie Azure, powinien mieć dobrą konwencji nazewnictwa w miejscu. Konwencja nazewnictwa gwarantuje, że wszystkie zasoby hello przewidywalną nazwy, która pomaga w dolnym hello nakładu prac administracyjnych związane z zarządzaniem tych zasobów.

Możesz wybrać toofollow określonych konwencji nazewnictwa zdefiniowane dla całej organizacji lub dla określonej subskrypcji Azure lub konta. Chociaż jest łatwy do osób w organizacji tooestablish niejawne reguł podczas pracy z zasobami Azure, należy tooscale stanie toobe dla zespołów pracujących razem na platformie Azure.

Zgodę na zestawie konwencji nazewnictwa na początku. Istnieją pewne kwestie dotyczących konwencji nazewnictwa Wytnij między które ustawia zasady.

## <a name="affixes"></a>Umieszcza
Jak wyglądają toodefine konwencji nazewnictwa, decyzji co jest czy Afiks hello na:

* Witaj na początku nazwy hello (prefiks)
* Witaj na końcu nazwy hello (sufiks)

Na przykład poniżej przedstawiono dwa możliwe nazwy grupy zasobów, przy użyciu hello `rg` umieścić:

* Aplikacja zarządcy zasobów sieci Web (prefiks)
* Aplikacja sieci Web zarządcy zasobów (sufiks)

Afiksów mogą odwoływać się toodifferent aspektów, które opisują hello określonych zasobów. Witaj poniższej tabeli przedstawiono kilka przykładów zwykle używane.

| Aspekt | Przykłady | Uwagi |
|:--- |:--- |:--- |
| Środowisko |deweloperów, stg, produkcyjnego |W zależności od celu hello i nazwa każdego środowiska. |
| Lokalizacja |usw (zachodnie stany USA), użyj (wschodnie stany USA 2) |W zależności od regionu hello hello centrum danych lub regionu hello hello organizacji. |
| Składnik Azure, usługi lub produktu |Grupy zasobów dla grupy zasobów, sieci wirtualnej dla sieci wirtualnej |W zależności od produktu hello, dla których hello zasobów zapewnia obsługę. |
| Rola |bazy danych, aplikacji sieci web |W zależności od roli hello hello maszyny wirtualnej. |
| Wystąpienie |01, 02, 03, itp. |Dla zasobów, które mają więcej niż jedno wystąpienie. Na przykład serwery sieci web w usłudze w chmurze zrównoważonym obciążeniu. |

Podczas ustanawiania konwencji nazewnictwa, upewnij się, że ich wyraźnie określają, które umieszcza toouse dla każdego typu zasobu, w jakim położeniu (prefiks vs sufiks).

## <a name="dates"></a>daty
Często jest ważne toodetermine hello Data utworzenia z hello nazwy zasobu. Zalecamy format daty hello RRRRMMDD. Format ten zapewnia nie tylko hello pełna data jest rejestrowane, ale również tego dwa zasoby których nazwy różnią się tylko w dniu hello są posortowane alfabetycznie, w porządku chronologicznym.

## <a name="naming-resources"></a>Nadawanie nazw zasobów
Każdy typ zasobu w konwencji nazewnictwa hello, który powinien mieć reguł określających sposób tooassign nazwy zasobu tooeach który jest tworzony. Te reguły stosowania tooall typów zasobów, na przykład:

* Subskrypcje
* Konta
* Konta magazynu
* Sieci wirtualne
* Podsieci
* Zestawy dostępności
* Grupy zasobów
* Maszyny wirtualne
* Punkty końcowe
* Grupy zabezpieczeń sieci
* Role

tooensure, który hello nazwa zawiera za mało informacji toodetermine toowhich zasób, który odwołuje się, należy użyć nazwy opisowe.

## <a name="computer-names"></a>Nazwy komputerów
Podczas tworzenia maszyny wirtualnej (VM) na platformie Azure wymaga nazwę maszyny Wirtualnej z zapasowej too64 znaków używany do hello Nazwa zasobu. Platforma Azure hello tej samej nazwy dla hello system operacyjny zainstalowany na powitania maszyny Wirtualnej. Jednak te nazwy może nie zawsze być hello tego samego.

Jeśli maszyna wirtualna została utworzona z pliku obrazu vhd zawierającego system operacyjny, hello nazwę maszyny Wirtualnej na platformie Azure mogą się różnić od hello nazwa komputera systemu operacyjnego maszyny Wirtualnej. Takiej sytuacji można dodać stopień trudności tooVM zarządzania, które w związku z tym nie jest zalecane. Przypisz hello hello zasobu maszyny Wirtualnej Azure takie same nazwy jako nazwy komputera hello przypisanie toohello system operacyjny tej maszyny Wirtualnej.

Firma Microsoft zaleca tę nazwę maszyny Wirtualnej Azure hello jest hello taki sam jak hello bazowy nazwa komputera systemu operacyjnego.

## <a name="storage-account-names"></a>Nazwy kont magazynu
Ta sekcja nie ma zastosowania zbyt[dysków zarządzanych Azure](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), ponieważ nie należy tworzyć oddzielnego konta magazynu. Dla niezarządzanego dysków kont magazynu ma specjalne zasady dotyczące ich nazw. Można używać tylko małe litery i cyfry. Aby uzyskać więcej informacji, zobacz [Utwórz konto magazynu](../../storage/storage-create-storage-account.md#create-a-storage-account). Ponadto hello nazwy konta magazynu, z core.windows.net, należy globalnie prawidłową, unikatową nazwę DNS. Na przykład jeśli konto magazynu hello jest nazywane mojekontomagazynu, hello poniższe nazwy DNS wynikowy powinna być unikatowa:

* mystorageaccount.blob.Core.Windows.NET
* mystorageaccount.TABLE.Core.Windows.NET
* mystorageaccount.Queue.Core.Windows.NET

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

