---
title: aaaSubscription i konta dla maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat hello klucza projekt i implementację wytyczne dotyczące subskrypcji oraz konta na platformie Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 19343826-7eef-42a1-98be-4ec65b0f377a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9025a40783c008310ebd0f674deb4a9001ae974a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-linux-vms"></a>Azure subskrypcją i kontami wytyczne dotyczące maszyn wirtualnych systemu Linux

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Ten artykuł koncentruje się na sposób zwiększania rozmiaru tooapproach subskrypcji oraz konta zarządzania jako swojego środowiska i użytkownika podstawowej.

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a>Implementacja — wskazówki dla subskrypcji i konta
Decyzje:

* Jaki zestaw subskrypcji i potrzebujesz toohost infrastruktury i obciążenia IT?
* Jak toobreak dół hello toofit hierarchii organizacji?

Zadania:

* Zdefiniuj hierarchii logiczna organizacji ma się toomanage go z poziomu subskrypcji.
* toomatch tej hierarchii logiczne, zdefiniuj hello konta wymagane i subskrypcje w ramach poszczególnych kont.
* Utwórz zestaw hello subskrypcje i kont za pomocą Konwencja nazewnictwa.

## <a name="subscriptions-and-accounts"></a>Subskrypcje i konta
toowork z platformy Azure, należy co najmniej jedna subskrypcja platformy Azure. Zasoby, na przykład maszynach wirtualnych (VM) lub sieci wirtualne istnieją w tych subskrypcji.

* Klienci korporacyjni zwykle mają rejestracji Enterprise, która jest hello najwyższy zasobów w hierarchii hello, a skojarzone tooone lub więcej kont.
* Dla konsumentów i klientów bez rejestracji Enterprise zasób najwyższy hello jest hello konta.
* Subskrypcje są skojarzone tooaccounts i mogą istnieć co najmniej jedna subskrypcja dla danego konta. Rozliczeń informacji na poziomie subskrypcji hello Azure rekordów.

Powodu limit toohello poziomów hierarchii dwóch hello relacji konta/subskrypcji jest ważne tooalign hello konwencją nazewnictwa toohello konta i subskrypcji, rozliczeń potrzeb. Na przykład jeśli globalne firma korzysta z platformy Azure, ich może wybrać konto toohave jeden na region, a ma zarządzać subskrypcjami w hello poziom regionu:

![](media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

Na przykład można użyć hello następujące struktury:

![](media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

Jeśli region decyduje toohave więcej niż jedną subskrypcję skojarzone tooa określonej grupy, hello konwencji nazewnictwa powinien dołączyć do nich tooencode sposób hello dodatkowe dane na konto hello lub hello nazwę subskrypcji. Ta organizacja pozwala massaging rozliczeń danych toogenerate hello nowe poziomy hierarchii podczas rozliczeń raportów:

![](media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

Witaj organizacji może wyglądać hello poniższy przykład:

![](media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

Firma Microsoft udostępnia szczegółowy rozliczeń za pośrednictwem plików do pobrania dla jednego konta lub dla wszystkich kont w umowy enterprise agreement.

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

