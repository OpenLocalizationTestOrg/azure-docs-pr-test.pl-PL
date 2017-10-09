---
title: aaaSolutions w Operations Management Suite (OMS) | Dokumentacja firmy Microsoft
description: "Rozwiązania rozszerzyć funkcjonalność hello z Operations Management Suite (OMS), zapewniając scenariusze zarządzania spakowanych dodać obszar roboczy OMS tootheir klientów.  Ten artykuł zawiera szczegółowe informacje na temat niestandardowych rozwiązań utworzonych przez klientom i partnerom."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/01/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5b5a538f1bc4b5577bec94db08bd43668bc6584a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-management-solutions-in-operations-management-suite-oms-preview"></a>Praca z rozwiązaniami do zarządzania w Operations Management Suite (OMS) (wersja zapoznawcza)
> [!NOTE]
> Jest to wstępne dokumentacji dla rozwiązań do zarządzania w OMS, które są obecnie w wersji zapoznawczej.    
> 
> 

Rozwiązania do zarządzania rozszerzyć funkcjonalność hello z Operations Management Suite (OMS), zapewniając scenariusze zarządzania spakowanych dodać środowiska tootheir klientów.  Ponadto zbyt[rozwiązań dostarczonych przez firmę Microsoft](../log-analytics/log-analytics-add-solutions.md), partnerów i klientów można utworzyć toobe rozwiązań do zarządzania w ich środowisku lub wprowadzone toocustomers dostępne za pośrednictwem hello społeczności.

## <a name="finding-and-installing-management-solutions"></a>Znajdowanie i instalowanie rozwiązania do zarządzania
Istnieje wiele metod do lokalizowania i instalowanie rozwiązania do zarządzania, zgodnie z opisem w hello następujące sekcje.

### <a name="azure-marketplace"></a>Azure Marketplace
Rozwiązania do zarządzania są dostarczane przez firmę Microsoft i zaufanych partnerów mogą być zainstalowane z hello Azure Marketplace w hello portalu Azure.

1. Zaloguj się za toohello portalu Azure.
2. Wybierz w okienku po lewej stronie powitania **więcej usług**.
3. Albo przewiń w dół za**rozwiązań** lub typ *rozwiązań* do hello **filtru** okna dialogowego.
4. Kliknij przycisk hello **+ Dodaj** przycisku.
5. Wyszukaj rozwiązania, które interesują Cię przez przeglądanie, klikając hello **filtru** przycisk lub wprowadzając w hello **Everthing wyszukiwania** pole.
6. Kliknij szczegółowe informacje o tooview elementu portalu marketplace.
7. Kliknij przycisk **Utwórz** tooopen hello **Dodaj rozwiązanie** okienka.
8. Będzie toorequired zostanie wyświetlony monit o informacje, takie jak hello [OMS obszaru roboczego i konto automatyzacji](#oms-workspace-and-automation-account) dodatkowo toovalues dla wszystkich parametrów w hello rozwiązania.
9. Kliknij przycisk **Utwórz** tooinstall hello rozwiązania.

### <a name="oms-portal"></a>Portalu OMS
Rozwiązania do zarządzania firmy Microsoft mogą być zainstalowane z hello galerii rozwiązań w portalu OMS hello.

1. Zaloguj się za toohello portalu OMS.
2. Kliknij przycisk hello **galerii rozwiązań** kafelka.
3. Na stronie galerii rozwiązań OMS hello informacje na temat każdego z dostępnych rozwiązań. Kliknij nazwę hello hello rozwiązania, które mają tooadd tooOMS.
4. Na stronie powitania hello rozwiązania, które wybrano są wyświetlane szczegółowe informacje o rozwiązaniu hello. Kliknij pozycję **Dodaj**.
5. Nowy Kafelek rozwiązania hello, dodanego pojawia się na hello strony Przegląd w OMS i możesz rozpocząć korzystanie z niej po hello usługę przetwarzania danych.

### <a name="azure-quickstart-templates"></a>Szablony szybkiego startu platformy Azure
Członkowie społeczności hello można przesłać tooAzure rozwiązań zarządzania szablony szybkiego startu.  Możesz pobrać te szablony do nowszej instalacji lub sprawdzić ich toolearn jak zbyt[tworzenia własnych rozwiązań](#creating-a-solution).

1. Wykonaj hello procesu opisanego w temacie [OMS obszaru roboczego i konto automatyzacji](#oms-workspace-and-automation-account) toolink obszaru roboczego i konta.
2. Przejdź za[szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates/).  
3. Wyszukiwanie rozwiązania, które Cię interesują.
4. Wybierz rozwiązanie hello z tooview wyniki hello jego szczegóły.
5. Kliknij przycisk hello **wdrażanie tooAzure** przycisku.
6. Będzie tooprovide zostanie wyświetlony monit o informacje, takie jak grupy zasobów hello i lokalizację w toovalues dodawania parametrów w rozwiązaniu hello.
7. Kliknij przycisk **zakupu** tooinstall hello rozwiązania.

### <a name="deploy-azure-resource-manager-template"></a>Wdrażanie szablonu usługi Azure Resource Manager
Rozwiązania, które można uzyskać od społeczności hello lub [samodzielnie utworzyć](#creating-a-solution) są zaimplementowane jako szablon Menedżera zasobów i można użyć dowolnego z hello standardowe metody [wdrażania szablonu](../azure-resource-manager/resource-group-template-deploy-portal.md).  Należy pamiętać, że przed zainstalowaniem hello rozwiązanie, należy utworzyć i połączyć hello [OMS obszaru roboczego i konto automatyzacji](#oms-workspace-and-automation-account).

## <a name="oms-workspace-and-automation-account"></a>Obszar roboczy OMS i konta automatyzacji
Większość rozwiązań do zarządzania wymagają [obszarem roboczym pakietu OMS](../log-analytics/log-analytics-manage-access.md) toocontain widoki i [konto automatyzacji](../automation/automation-security-overview.md#automation-account-overview) toocontain elementów runbook i powiązanych zasobów. Witaj obszaru roboczego, a konto musi spełniać następujące wymagania hello.

* Rozwiązanie można używać tylko jeden obszar roboczy OMS i jedno konto automatyzacji.  
* Hello obszarem roboczym pakietu OMS i automatyzacji konta używanego przez rozwiązanie muszą być połączone tooone innego. Obszar roboczy OMS mogą być tylko tooone połączonego konta automatyzacji, a konto usługi Automatyzacja może być tylko połączonego tooone obszarem roboczym pakietu OMS.
* toobe połączone hello obszarem roboczym pakietu OMS i hello automatyzacji, konto musi znajdować się w tej samej grupie zasobów i region.  wyjątek Hello jest obszar roboczy OMS w regionie wschodnie stany USA i i konto usługi Automatyzacja w wschodnie stany USA 2.

### <a name="creating-a-link-between-an-oms-workspace-and-automation-account"></a>Tworzenie połączenia między obszarem roboczym pakietu OMS i konta automatyzacji
Sposób Określ obszar roboczy OMS hello i konto automatyzacji zależy od metody instalacji hello do rozwiązania.

* Po zainstalowaniu rozwiązanie firmy Microsoft za pośrednictwem portalu OMS hello jest zainstalowany w hello bieżący obszar roboczy OMS i żadne konto automatyzacji nie jest wymagane.
* Po zainstalowaniu rozwiązania w ramach hello Azure Marketplace, zostanie wyświetlony monit o obszarem roboczym pakietu OMS i konto usługi Automatyzacja i jest tworzone łącze hello między nimi.  
* Rozwiązania poza hello Azure Marketplace możesz połączyć hello obszarem roboczym pakietu OMS i konto automatyzacji przed zainstalowaniem hello rozwiązania.  Można to zrobić, wybranie dowolnego rozwiązania w portalu Azure Marketplace hello i wybierając obszar roboczy OMS hello i konta automatyzacji.  Nie masz tooactually zainstalować hello rozwiązania, ponieważ zostanie utworzone łącze hello jak zaznaczono hello obszarem roboczym pakietu OMS i konta automatyzacji.  Po utworzeniu łącza hello można ten obszar roboczy OMS i konto automatyzacji dla dowolnego rozwiązania. 

### <a name="verifying-hello-link-between-an-oms-workspace-and-automation-account"></a>Weryfikowanie, czy łącze hello między obszarem roboczym pakietu OMS i konta automatyzacji
Możesz sprawdzić hello łącza między obszarem roboczym pakietu OMS i konto usługi Automatyzacja przy użyciu hello procedury.

1. Wybierz konto Automatyzacja hello w hello portalu Azure.
2. Przewiń w dół toohello hello **ustawienia** okienka.
3. Jeśli jest sekcji o nazwie **zasobów OMS** w hello **ustawienia** okienka, a następnie to konto jest dołączona tooan obszarem roboczym pakietu OMS.
4. Wybierz **obszaru roboczego** tooview szczegóły hello hello obszarem roboczym pakietu OMS połączone toothis konta automatyzacji.

## <a name="listing-management-solutions"></a>Lista rozwiązań do zarządzania
Witaj użyj następującej procedury tootooview hello rozwiązania do zarządzania w hello obszary robocze połączone tooyour subskrypcji platformy Azure.

1. Zaloguj się za toohello portalu Azure.
2. Wybierz w okienku po lewej stronie powitania **więcej usług**.
3. Albo przewiń w dół za**rozwiązań** lub typ *rozwiązań* do hello **filtru** okna dialogowego.
4. Rozwiązania zainstalowane w wszystkie obszary robocze zostaną wyświetlone.

Należy pamiętać, że można wyświetlić tylko rozwiązania firmy Microsoft hello zainstalowane w bieżącym obszarze roboczym hello za pomocą portalu OMS hello.

## <a name="removing-a-management-solution"></a>Usuwanie rozwiązania do zarządzania
Rozwiązanie do zarządzania zostanie usunięty, wszystkie zasoby w rozwiązaniu hello są również usuwane.  

1. Znajdź rozwiązania hello w hello Azure przy użyciu procedury hello w portalu [listę rozwiązań](#listing-solutions).
2. Wybierz rozwiązanie hello ma tooremove.
3. Kliknij przycisk hello **usunąć** przycisku.

## <a name="creating-a-management-solution"></a>Tworzenie rozwiązania do zarządzania
Pełne wskazówki dotyczące tworzenia rozwiązań do zarządzania są dostępne pod adresem [tworzenie rozwiązań w Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md). 

## <a name="next-steps"></a>Następne kroki
* Wyszukiwanie [szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates) przykłady różnych szablonów usługi Resource Manager.
* Utwórz swój własny [rozwiązań do zarządzania](operations-management-suite-solutions-creating.md).

