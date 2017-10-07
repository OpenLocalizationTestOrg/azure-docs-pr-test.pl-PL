---
title: "aaaUse obrazów klientów systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: "Jak toouse subskrypcji programu Visual Studio korzysta toodeploy systemu Windows 7, Windows 8 lub Windows 10 w usłudze Azure scenariusze tworzenia/testowania"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 91c3880a-cede-44f1-ae25-f8f9f5b6eaa4
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: 4ac7c3d9872673030f4ea0f0ab38625dd9d9c1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-client-in-azure-for-devtest-scenarios"></a>Używanie klienta systemu Windows na platformie Azure scenariusze tworzenia/testowania
Można użyć systemu Windows 7, Windows 8 lub Windows 10 w usłudze Azure scenariusze tworzenia/testowania, pod warunkiem, że masz odpowiednie subskrypcji programu Visual Studio (dawniej MSDN). W tym artykule opisano hello kwalifikujących się wymagania dotyczące uruchamiania klienta systemu Windows Azure i użyj hello obrazów w galerii Azure.

## <a name="subscription-eligibility"></a>Uprawnienia subskrypcji
Aktywnych subskrybentów usługi Visual Studio (osoby, które zostały nabyte licencji subskrypcji programu Visual Studio) można użyć klienta systemu Windows do projektowania i testowania. Klient systemu Windows może być używany na własnego sprzętu i Azure maszyny wirtualne działające w dowolny typ subskrypcji platformy Azure. Klient systemu Windows nie może być wdrożony tooor używane na platformie Azure do użytku produkcyjnego normalnym lub używane przez różne osoby, których nie ma aktywnych subskrybentów usługi Visual Studio.

Dla wygody użytkownika firma Microsoft udostępnione niektórych obrazów systemu Windows 10 z galerii Azure hello w [oferuje kwalifikujących się tworzenie/testowanie](#eligible-offers). Subskrybentów usługi Visual Studio w obrębie dowolnego typu oferty może również [odpowiednio przygotować i utworzyć](prepare-for-upload-vhd-image.md) 64-bitowego obrazu systemu Windows 7, Windows 8 lub Windows 10, a następnie [przekazać tooAzure](upload-generalized-managed.md). Użyj Hello pozostaje toodev i testowanie ograniczone przez aktywnych subskrybentów usługi Visual Studio.

## <a name="eligible-offers"></a>Kwalifikujące się oferty
powitania po tabeli Szczegóły hello oferują identyfikatory kwalifikujących się toodeploy systemu Windows 10 za pomocą hello galerii Azure. obrazy Hello systemu Windows 10 są tylko widoczne toohello po oferty. Subskrybentów usługi Visual Studio kto należy toorun klienta systemu Windows w typie inną ofertę wymagają zbyt[odpowiednio przygotować i Utwórz](prepare-for-upload-vhd-image.md) 64-bitowego obrazu systemu Windows 7, Windows 8 lub Windows 10 i [następnie przekaż tooAzure](upload-generalized-managed.md).

| Nazwa oferty | Numer oferty | Obrazy dostępne klienta |
|:--- |:---:|:---:|
| [Płatność za rzeczywiste użycie: tworzenie i testowanie](https://azure.microsoft.com/offers/ms-azr-0023p/) |0023P |Windows 10 |
| [Subskrybentów usługi Visual Studio Enterprise (MPN)](https://azure.microsoft.com/offers/ms-azr-0029p/) |0029P |Windows 10 |
| [Subskrybentów usługi Visual Studio Professional](https://azure.microsoft.com/offers/ms-azr-0059p/) |0059P |Windows 10 |
| [Subskrybentów usługi Visual Studio Test Professional](https://azure.microsoft.com/offers/ms-azr-0060p/) |0060P |Windows 10 |
| [Visual Studio Premium z subskrypcją MSDN (asysta)](https://azure.microsoft.com/offers/ms-azr-0061p/) |0061P |Windows 10 |
| [Subskrybentów usługi Visual Studio Enterprise](https://azure.microsoft.com/offers/ms-azr-0063p/) |0063P |Windows 10 |
| [Subskrybentów usługi Visual Studio Enterprise (BizSpark)](https://azure.microsoft.com/offers/ms-azr-0064p/) |0064P |Windows 10 |
| [Enterprise: tworzenie i testowanie](https://azure.microsoft.com/ofers/ms-azr-0148p/) |0148P |Windows 10 |

## <a name="check-your-azure-subscription"></a>Sprawdź subskrypcji platformy Azure
Jeśli nie znasz Identyfikatora oferty, możesz go uzyskać za pośrednictwem hello portalu Azure w jeden z tych dwóch sposobów:  

- W bloku "Subskrypcji" hello:

  ![Szczegóły identyfikator oferty z hello portalu Azure](./media/client-images/offer-id-azure-portal.png) 

- Lub kliknij przycisk **rozliczeń** a następnie kliknij przycisk Twojego identyfikatora subskrypcji. Identyfikator oferty Hello jest wyświetlany w bloku rozliczenia hello.

Można również wyświetlić identyfikator oferty hello hello [kartę "Subskrypcji"](http://account.windowsazure.com/Subscriptions) portalu konta usługi Azure hello:

![Szczegóły identyfikator oferty w portalu konta usługi Azure hello](./media/client-images/offer-id-azure-account-portal.png) 

## <a name="next-steps"></a>Następne kroki
Teraz można wdrożyć maszyn wirtualnych przy użyciu [PowerShell](quick-create-powershell.md), [szablonów Resource Manager](ps-template.md), lub [programu Visual Studio](../../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

