---
title: "Zasady — Windows nazewnictwa infrastruktury platformy Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat klucza projekt i implementację wskazówki dotyczące nazewnictwa w usług infrastruktury platformy Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 660765fa-4d42-49cb-a9c6-8c596d26d221
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70a595d5c2f0316b5214af7b8939f1af8da187ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-windows-vms"></a>Zasady nazewnictwa dla maszyn wirtualnych systemu Windows infrastruktury platformy Azure

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Ten artykuł koncentruje się na sposób podejścia konwencje nazewnictwa dla wszystkich różnych zasobów platformy Azure można utworzyć logicznych i identyfikację zestaw zasobów w danym środowisku.

## <a name="implementation-guidelines-for-naming-conventions"></a>Implementacja — wskazówki dla konwencje nazewnictwa
Decyzje:

* Co to są konwencji nazewnictwa dla zasobów platformy Azure?

Zadania:

* Zdefiniuj afiksów służące do zapewniania spójności między zasobami.
* Zdefiniuj podane wymagania dla nich być globalnie unikatowe nazwy konta magazynu.
* Następnie należy udokumentować konwencji nazewnictwa, można użyć do rozpowszechniania wśród wszystkich uczestniczących w celu zapewnienia spójności we wszystkich wdrożeniach.

## <a name="naming-conventions"></a>Konwencje nazewnictwa
Przed utworzeniem jakichkolwiek na platformie Azure, powinien mieć dobrą konwencji nazewnictwa w miejscu. Konwencja nazewnictwa gwarantuje, że wszystkie zasoby przewidywalną nazwy, co pomaga zmniejszyć obciążenie administracyjne związane z zarządzaniem tych zasobów.

Można wykonać określonych konwencji nazewnictwa zdefiniowane dla całej organizacji lub dla określonej subskrypcji Azure lub konta. Chociaż jest łatwe dla użytkowników indywidualnych w ramach organizacji ustanowienie reguł niejawnych podczas pracy z zasobów platformy Azure, gdy zespół wymaga do pracy nad projektem na platformie Azure, modelu trudności w kontekście skalowania.

Zgodę na zestawie konwencji nazewnictwa na początku. Istnieją pewne kwestie dotyczące konwencji nazewnictwa Wytnij przez ten zestaw reguł.

## <a name="affixes"></a>Umieszcza
Jak wyglądają na definiowanie konwencji nazewnictwa, jeden decyzji pochodzi czy Afiks znajduje się na:

* Na początku nazwy (prefiks)
* Końcowa kropka (sufiks)

Na przykład poniżej przedstawiono dwa możliwe nazwy grupy zasobów przy użyciu `rg` umieścić:

* Aplikacja zarządcy zasobów sieci Web (prefiks)
* Aplikacja sieci Web zarządcy zasobów (sufiks)

Afiksów mogą odwoływać się do różnych aspektów, które opisują określonych zasobów. W poniższej tabeli przedstawiono kilka przykładów zwykle używane.

| Aspekt | Przykłady | Uwagi |
|:--- |:--- |:--- |
| Środowisko |deweloperów, stg, produkcyjnego |W zależności od przeznaczenia i nazwa każdego środowiska. |
| Lokalizacja |usw (zachodnie stany USA), użyj (wschodnie stany USA 2) |W zależności od regionu centrum danych lub regionu, w organizacji. |
| Składnik Azure, usługi lub produktu |Grupy zasobów dla grupy zasobów, sieci wirtualnej dla sieci wirtualnej |W zależności od produktu, którego zasobu zapewnia obsługę. |
| Rola |SQL, ora, sp, usługi iis |W zależności od roli maszyny wirtualnej. |
| Wystąpienie |01, 02, 03, itp. |Dla zasobów, które mają więcej niż jedno wystąpienie. Na przykład serwery sieci web w usłudze w chmurze zrównoważonym obciążeniu. |

Podczas ustanawiania konwencji nazewnictwa, upewnij się, czy one wyraźnie określają, które afiksów do użycia dla każdego typu zasobu, w jakim położeniu (prefiks vs sufiks).

## <a name="dates"></a>daty
Często jest to ważne jest określenie daty utworzenia od nazwy zasobu. Zalecamy format daty RRRRMMDD. Ten format gwarantuje, że nie tylko pełną datę jest rejestrowane, ale również tego dwa zasoby których nazwy różnią się tylko w dniu jest sortowana alfabetycznie, w porządku chronologicznym w tym samym czasie.

## <a name="naming-resources"></a>Nadawanie nazw zasobów
Zdefiniuj każdego typu zasobu w konwencji nazewnictwa, która ma reguł określających, jak przypisać nazwy do każdego zasobu, która jest tworzona. Te reguły stosuje się do wszystkich typów zasobów, na przykład:

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

Aby upewnić się, że nazwa zawiera wystarczających informacji do ustalenia, do którego odnosi się zasobu, należy używać nazwy opisowej.

## <a name="computer-names"></a>Nazwy komputerów
Podczas tworzenia maszyny wirtualnej (VM), Microsoft Azure wymaga nazwę maszyny Wirtualnej z maksymalnie 15 znaków używany dla nazwy zasobu. Azure korzysta z tej samej nazwy dla system operacyjny zainstalowany na maszynie wirtualnej. Jednak te nazwy może nie zawsze być takie same.

W przypadku maszyny Wirtualnej jest tworzona na podstawie pliku obrazu vhd zawierającego system operacyjny, nazwę maszyny Wirtualnej na platformie Azure mogą się różnić od nazwy komputera systemu operacyjnego maszyny Wirtualnej. Do maszyny Wirtualnej zarządzania, dlatego nie zaleca się takiej sytuacji można dodać stopień trudności. Przydziel zasób maszyny Wirtualnej Azure taką samą nazwę jak nazwa komputera, przypisane do tej maszyny Wirtualnej systemu operacyjnego.

Zaleca się, że nazwa maszyny Wirtualnej platformy Azure jest taka sama jak nazwa komputera źródłowego systemu operacyjnego.

## <a name="storage-account-names"></a>Nazwy kont magazynu
Ta sekcja nie ma zastosowania do [dysków zarządzanych Azure](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), ponieważ nie należy tworzyć oddzielnego konta magazynu. Dla niezarządzanego dysków kont magazynu ma specjalne zasady dotyczące ich nazw. Można używać tylko małe litery i cyfry. Aby uzyskać więcej informacji, zobacz [Utwórz konto magazynu](../../storage/storage-create-storage-account.md#create-a-storage-account). Ponadto nazwa konta magazynu, wraz z core.windows.net, należy globalnie prawidłową, unikatową nazwę DNS. Na przykład jeśli konto magazynu jest nazywane mojekontomagazynu, wynikowy poniższe nazwy DNS powinien być unikatowy:

* mystorageaccount.blob.Core.Windows.NET
* mystorageaccount.TABLE.Core.Windows.NET
* mystorageaccount.Queue.Core.Windows.NET

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

