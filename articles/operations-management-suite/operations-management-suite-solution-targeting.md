---
title: "aaaSolution elementów docelowych w OMS | Dokumentacja firmy Microsoft"
description: "Rozwiązanie docelowych jest funkcją w operacji pakietu zarządzania (OMS) umożliwiający toolimit zarządzania rozwiązań tooa określony zbiór agentów.  W tym artykule opisano sposób konfiguracji zakresu toocreate i zastosować je tooa rozwiązania."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: bwren
ms.openlocfilehash: 6f8c8109e0d9e282e18724bf8b673b10de8e498a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-solution-targeting-in-operations-management-suite-oms-tooscope-management-solutions-toospecific-agents-preview"></a>Za pomocą rozwiązania elementów docelowych w Operations Management Suite (OMS) agentów toospecific rozwiązań zarządzania tooscope (wersja zapoznawcza)
Po dodaniu tooOMS rozwiązanie automatycznie jest wdrażana przez domyślny tooall systemu Windows i Linux agentów połączonych tooyour obszaru roboczego analizy dzienników.  Możesz toomanage Twojego kosztów i limit hello ilości danych zbieranych dla rozwiązania ograniczając tooa określonego zestawu agentów.  W tym artykule opisano sposób toouse **przeznaczonych dla rozwiązania** czyli funkcję OMS, która pozwala tooapply zakres tooyour rozwiązania.

## <a name="how-tootarget-a-solution"></a>Jak tootarget rozwiązania
Istnieją trzy kroki tootargeting rozwiązanie zgodnie z opisem w hello następujące sekcje.  Należy pamiętać, że konieczne będzie zarówno portalu OMS hello i hello portalu Azure do wykonania różnych kroków w.


### <a name="1-create-a-computer-group"></a>1. Tworzenie grupy komputerów
Określ komputery hello mają tooinclude w zakresie tworząc [grupy komputerów](../log-analytics/log-analytics-computer-groups.md) w analizy dzienników.  Grupa komputerów Hello można oparte na wyszukiwania dziennika lub zaimportowane z innych źródeł, takich jak usługa Active Directory lub grup usług WSUS. Jako [opisanych poniżej](#solutions-and-agents-that-cant-be-targeted), tylko do komputerów, które są bezpośrednio podłączone tooLog Analytics zostaną uwzględnione w zakresie hello.

Po utworzeniu grupy komputerów hello utworzone w obszarze roboczym, następnie chcesz dołączyć go w konfiguracji zakresu, które mogą być zastosowane tooone lub więcej rozwiązań.
 
 
 ### <a name="2-create-a-scope-configuration"></a>2. Utwórz konfigurację zakresu
 A **konfigurację zakresu** zawiera jeden lub więcej grup komputerów i mogą być zastosowane tooone lub więcej rozwiązań. 
 
 Utwórz konfigurację zakresu przy użyciu powitania po procesie.  

 1. W portalu Azure hello kolejno zbyt**analizy dzienników** i wybierz obszar roboczy.
 2. W obszarze roboczym hello hello właściwości **źródeł danych obszaru roboczego** wybierz **konfiguracji zakresu**.
 3. Kliknij przycisk **Dodaj** toocreate nową konfigurację zakresu.
 4. Wpisz **nazwa** hello zakresu konfiguracji.
 5. Kliknij przycisk **wybierz grupy komputerów**.
 6. Wybierz grupy komputerów hello utworzony i opcjonalnie innych grup tooadd toohello konfiguracji.  Kliknij pozycję **Wybierz**.  
 6. Kliknij przycisk **OK** toocreate hello zakresu konfiguracji. 


 ### <a name="3-apply-hello-scope-configuration-tooa-solution"></a>3. Zastosuj hello zakresu konfiguracji tooa rozwiązania.
Po utworzeniu konfiguracji zakresu, a następnie można go zastosować tooone lub więcej rozwiązań.  Należy pamiętać, że podczas konfiguracji jednego zakresu, może być używany z kilku rozwiązań w zakresie, każde rozwiązanie można używać tylko jedną konfigurację zakresu.

Zastosowanie konfiguracji zakresu przy użyciu powitania po procesie.  

 1. W portalu Azure hello kolejno zbyt**analizy dzienników** i wybierz obszar roboczy.
 2. We właściwościach hello hello obszaru roboczego wybierz **rozwiązań**.
 3. Kliknij na powitania rozwiązania mają tooscope.
 4. We właściwościach hello rozwiązania hello w obszarze **źródeł danych obszaru roboczego** wybierz **przeznaczonych dla rozwiązania**.  Jeśli nie jest dostępna opcja hello następnie [tego rozwiązania nie może być celem](#solutions-and-agents-that-cant-be-targeted).
 5. Kliknij przycisk **Dodaj konfigurację zakresu**.  Jeśli masz już rozwiązania toothis zastosowano konfigurację następnie ta opcja będzie niedostępna.  Należy usunąć istniejącą konfigurację hello przed dodaniem kolejnego.
 6. Kliknij pozycję konfiguracja zakresu hello utworzony.
 7. Obejrzyj hello **stan** z hello tooensure konfiguracji, która będzie wyświetlana **zakończyło się pomyślnie**.  Jeśli stan hello wskazuje błąd, kliknij przycisk hello elipsy toohello prawej hello konfigurację i wybierz **konfigurację zakresu edycji** toomake zmiany.

## <a name="solutions-and-agents-that-cant-be-targeted"></a>Rozwiązania i agenci, którzy nie mogą być celem
Poniżej przedstawiono kryteria hello agentów i rozwiązań, które nie można używać z przeznaczonych dla rozwiązania.

- Celem rozwiązanie ma zastosowanie tylko toosolutions, które wdrożyć tooagents.
- Celem rozwiązanie ma zastosowanie tylko toosolutions obsługiwane przez firmę Microsoft.  Nie ma zastosowania toosolutions [utworzony przez siebie lub partnerów](operations-management-suite-solutions-creating.md).
- Można odfiltrować tylko agenci, którzy łączą się bezpośrednio tooLog Analytics.  Rozwiązania zostaną automatycznie wdrożone tooany agentów, które są częścią podłączonej grupy zarządzania programu Operations Manager, czy są one dołączone do konfiguracji zakresu.

### <a name="exceptions"></a>Wyjątki
Przeznaczonych dla rozwiązania nie można używać z powitania po rozwiązań, nawet jeśli mieściły się hello podane kryteria.

- Oceny kondycji agenta

## <a name="next-steps"></a>Następne kroki
- Więcej informacji na temat rozwiązań do zarządzania hello rozwiązań, które są dostępne tooinstall w danym środowisku, w tym [obszar roboczy usługi Analiza dzienników Azure Dodaj management rozwiązań tooyour](../log-analytics/log-analytics-add-solutions.md).
- Dowiedz się więcej o tworzeniu grup komputerów na [grup komputerów w analizy dzienników dziennika wyszukiwania](../log-analytics/log-analytics-computer-groups.md).