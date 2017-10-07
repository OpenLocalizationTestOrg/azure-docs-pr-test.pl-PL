---
title: "toocreating aaaGuide szablon rozwiązania hello Marketplace | Dokumentacja firmy Microsoft"
description: "Szczegółowe instrukcje sposobu toocreate, certyfikować i wdrażanie szablonu rozwiązania obrazu wielu maszyn wirtualnych na zakupu na hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e14e05f2-2385-4ce0-b351-0747cb74ba19
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: b0e7067176337dd0d3f6f6ec04c963f80f706ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-solution-template-for-azure-marketplace"></a>Przewodnik toocreate szablon rozwiązania do portalu Azure Marketplace
Po ukończeniu kroku 1, [o tworzeniu konta i rejestracji][link-acct-creation], możemy przewodnikiem po utworzeniu hello Azure zgodnego szablonu rozwiązania na [techniczne wymagania wstępne dotyczące tworzenia Szablon rozwiązania](marketplace-publishing-solution-template-creation-prerequisites.md). Obecnie firma Microsoft przeprowadzi Cię przez kroki tworzenia szablonu rozwiązanie dla wielu maszyn wirtualnych na powitania hello [Portal publikowania] [ link-pubportal] dla hello Azure Marketplace.

## <a name="create-your-solution-template-offer-in-hello-publishing-portal"></a>Utwórz ofertę szablon rozwiązania w hello Portal publikowania
Przejdź za [https://publish.windowsazure.com](http://publish.windowsazure.com). Podczas rejestrowania się w pierwszym toohello czasu hello [Portal publikowania](https://publish.windowsazure.com/), hello Użyj tego samego konta z został zarejestrowany w firmie sprzedawcy profilu. Później możesz dodać każdy pracownik firmy jako współadministrator w hello Portal publikowania.

### <a name="1-select-solution-templates"></a>1. Wybierz opcję "Szablony rozwiązań"
  ![Rysowanie][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a>2. Utwórz nowy szablon rozwiązania
  ![Rysowanie][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a>3. Rozpoczynać się od topologii
Szablon rozwiązania jest tooall "elementu nadrzędnego", jego topologii. Można zdefiniować wiele topologii w jednym szablonie oferty/rozwiązania. Gdy oferta zostanie przeniesiona toostaging, spoczywa z wszystkich jego topologii. Wykonaj kroki hello poniżej toodefine ofertę:     

* Utworzyć topologię: "Identyfikator topologii" jest zazwyczaj nazwą hello topologii hello hello szablon rozwiązania. identyfikator topologii Hello jest używany w adresie URL hello, jak pokazano poniżej:

  Witrynę Azure Marketplace: http://azure.microsoft.com/marketplace/partners/ {PublisherNamespace} / {OfferIdentifier} {TopologyIdentifier}

  Portalu Azure: https://portal.azure.com/#gallery/ {PublisherNamespace}. {OfferIdentifier} {TopologyIdentifier}
* Dodaj nową wersję.

### <a name="4-get-your-topology-versions-certified"></a>4. Pobieranie Twojej wersji topologii certyfikowane
Przekaż plik zip, który zawiera wszystkie wymagane pliki tooprovision tej konkretnej wersji hello topologii. Ten plik zip musi zawierać następujące hello:

* *mainTemplate.json* i *createUiDefinition.json* pliku w katalogu głównym.
* Szablony połączone i wszystkie wymagane skrypty.

  > [!TIP]
  > Podczas pracy deweloperów na temat tworzenia rozwiązania hello topologie szablonu i pobieranie ich certyfikowane, hello business działu marketingu i/lub prawnych firmy może pracować na powitania marketing i prawnych zawartości.
  >
  >

## <a name="next-steps"></a>Następne kroki
Teraz, gdy zostanie utworzony szablon rozwiązania i przekazać plik zip hello, wykonaj instrukcje hello hello [Marketplace Przewodnik po zawartości marketingowej](marketplace-publishing-push-to-staging.md) przed wypchnięciem toostaging oferta hello. toosee hello pełny zestaw marketplace publikowanie artykułów, odwiedź stronę [wprowadzenie: jak toopublish toohello oferta portalu Azure Marketplace](marketplace-publishing-getting-started.md).

Być może zainteresuje te pokrewne artykuły:

* Obrazów maszyn wirtualnych: [o obrazy maszyny wirtualnej na platformie Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)
* Rozszerzenia maszyny Wirtualnej: [omówienie rozszerzeń maszyny Wirtualnej i Agent maszyny Wirtualnej](https://msdn.microsoft.com/library/azure/dn832621.aspx) i [rozszerzeń maszyny Wirtualnej platformy Azure i funkcje](https://msdn.microsoft.com/library/azure/dn606311.aspx)
* Usługa Azure Resource Manager: [tworzenia szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) i [przykłady prostego szablonu](https://github.com/rjmax/ArmExamples)
* Ogranicza konta magazynu: [jak tooMonitor dla ograniczania konta magazynu](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) i [magazyn w warstwie Premium](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
