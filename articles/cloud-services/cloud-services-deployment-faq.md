---
title: "problemy z aaaDeployment Microsoft Azure Cloud Services często zadawane pytania | Dokumentacja firmy Microsoft"
description: "W tym artykule wymieniono hello często zadawane pytania dotyczące wdrażania usługi w chmurze Microsoft Azure."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 8d67e36aa87fb5794d358e5cc235123ac7286028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Problemy z wdrażaniem usług Azure Cloud Services: często zadawane pytania (FAQ)

Ten artykuł zawiera często zadawane pytania dotyczące problemów dotyczących wdrożenia dla [usługi w chmurze Microsoft Azure](https://azure.microsoft.com/services/cloud-services). Można również znaleźć hello [strony rozmiar maszyny Wirtualnej usługi w chmurze](cloud-services-sizes-specs.md) dla informacji o rozmiarze.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-does-deploying-a-cloud-service-toohello-staging-slot-sometimes-fail-with-a-resource-allocation-error-if-there-is-already-an-existing-deployment-in-hello-production-slot"></a>Dlaczego wdrażanie toohello usługi chmury czasami przemieszczania miejsca nie powiodło się z powodu błędu alokacji zasobów Jeśli istnieje już istniejące wdrożenie w gnieździe produkcyjnym hello?
Jeśli usługa w chmurze ma wdrożenia w każdym miejscu, usługa w chmurze całego hello jest przypięty tooa konkretnego klastra. Oznacza to, że jeśli wdrożenia już istnieje w gnieździe produkcyjnym hello, nowe wdrożenie przemieszczania może zostać przydzielone tylko w hello sam klastra jako hello miejsca produkcji.

Błędy alokacji wystąpić, gdy klastra hello, w którym znajduje się usługa w chmurze nie ma wystarczającej liczby fizycznych obliczeniowe toosatisfy zasobów żądania wdrożenia.

Aby uzyskać pomoc zmniejszenia takie błędy alokacji, zobacz [błąd alokacji usługi w chmurze: rozwiązań](cloud-services-allocation-failures.md#solutions).

## <a name="why-does-scaling-up-or-scaling-out-a-cloud-service-deployment-sometimes-result-in-allocation-failure"></a>Dlaczego skalowanie w i skalowania w poziomie wdrożenie usługi chmury jest czasem spowodować niepowodzenie alokacji?
Po wdrożeniu usługi w chmurze pobiera zwykle przypiętych tooa konkretnego klastra. Oznacza to, że skalowanie w / out istniejącej chmurze usługi należy przydzielić nowych wystąpień w hello tego samego klastra. Jeśli klaster hello zbliża się do pojemności lub hello potrzeby maszyny Wirtualnej rozmiar i typ nie jest dostępna, Żądanie hello może zakończyć się niepowodzeniem.

Aby uzyskać pomoc zmniejszenia takie błędy alokacji, zobacz [błąd alokacji usługi w chmurze: rozwiązań](cloud-services-allocation-failures.md#solutions).

## <a name="why-does-deploying-a-cloud-service-into-an-affinity-group-sometimes-result-in-allocation-failure"></a>Dlaczego wdrażania usługi w chmurze w grupie koligacji czasami powoduje błąd alokacji?
Nową usługę chmury pusty tooan wdrożenia mogą zostać przydzieleni przez sieci szkieletowej hello w dowolnego klastra w danym regionie, chyba że usługa w chmurze hello jest przypięty tooan grupy koligacji. Toohello wdrożeń w tej samej grupie koligacji, zostanie podjęta na powitania tego samego klastra. Jeśli klaster hello zbliża się do pojemności, Żądanie hello może zakończyć się niepowodzeniem.

Aby uzyskać pomoc zmniejszenia takie błędy alokacji, zobacz [błąd alokacji usługi w chmurze: rozwiązań](cloud-services-allocation-failures.md#solutions).

## <a name="why-does-changing-vm-size-or-adding-a-new-vm-tooan-existing-cloud-service-sometimes-result-in-allocation-failure"></a>Dlaczego zmianę rozmiaru maszyny Wirtualnej lub dodanie nowej maszyny Wirtualnej tooan istniejącej usługi w chmurze czasami powoduje błąd alokacji?
klastry Hello w centrum danych mogą mieć różne konfiguracje typów maszyny (np. serii Av2 serii, D serii, Dv2 serii, serii G, H serii, itp.). Ale nie wszystkich klastrach hello niekoniecznie musi wszelkiego rodzaju hello maszyn wirtualnych. Na przykład Jeśli spróbujesz tooadd serii D usługa chmury tooa maszyny Wirtualnej, która została już wdrożona w klastrze tylko do serii A wystąpią błąd alokacji. To również nastąpi próba się, że rozmiary toochange SKU maszyny Wirtualnej (np. zmiana typu zapytania z serii tooa D serii A).

Aby uzyskać pomoc zmniejszenia takie błędy alokacji, zobacz [błąd alokacji usługi w chmurze: rozwiązań](cloud-services-allocation-failures.md#solutions).

toocheck hello rozmiarów dostępnych w danym regionie, zobacz [Microsoft Azure: produkty, które są dostępne w regionie](https://azure.microsoft.com/regions/services).

## <a name="why-does-deploying-a-cloud-service-sometime-fail-due-toolimitsquotasconstraints-on-my-subscription-or-service"></a>Dlaczego wdrożeniem chmury usługi pewnym czasie zakończyć się niepowodzeniem z powodu toolimits/przydziały/ograniczenia dotyczące mojej subskrypcji lub usługi?
Wdrożenia usługi w chmurze może zakończyć się niepowodzeniem, jeśli hello zasoby, które są wymagane toobe przydzielone przekracza hello domyślnej lub maksymalny limit przydziału, o których usługi na poziomie hello region/centrum danych. Aby uzyskać więcej informacji, zobacz [ogranicza usługi w chmurze](../azure-subscription-service-limits.md#cloud-services-limits).

Można także śledzić hello bieżącego/przydział użycia dla Twojej subskrypcji w portalu hello: Azure Portal = > Subskrypcje = > \<odpowiednie subskrypcji > = > "Użycia + limitu przydziału".

Można również pobrać informacji związanych z użycia/zużycie zasobów za pomocą hello interfejsów API usługi Azure rozliczeń. Zobacz [użycia zasobów platformy Azure (wersja zapoznawcza) interfejsu API](../billing/billing-usage-rate-card-overview.md#azure-resource-usage-api-preview).

## <a name="how-can-i-change-hello-size-of-a-deployed-cloud-service-vm-without-redeploying-it"></a>Jak zmienić rozmiar hello usługi w chmurze wdrożonej maszyny Wirtualnej bez jego ponowne wdrożenie?
Nie można zmienić hello rozmiar maszyny Wirtualnej usługi w chmurze wdrożonej bez jego ponowne wdrożenie. Witaj rozmiar maszyny Wirtualnej jest wbudowana w hello CSDEF, które można zaktualizować tylko z Wdróż go ponownie.

Aby uzyskać więcej informacji, zobacz [jak tooupdate usługi w chmurze](cloud-services-update-azure-service.md).

 
