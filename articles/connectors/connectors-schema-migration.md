---
title: aaaHow toomigrate logiki aplikacji tooschema wersji 2015-08-01-preview | Dokumentacja firmy Microsoft
description: "Możesz łatwo przeprowadzić migrację z najnowszej wersji schematu logic apps toohello. Wystarczy wykonać poniższe czynności."
services: logic-apps
documentationcenter: 
author: MSFTMAN
manager: erikre
editor: 
tags: connectors
ms.assetid: 3e177e49-fd69-43e9-9b9b-218abb250c31
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2016
ms.author: deonhe
ms.openlocfilehash: c7b42aaec547eddd28b0c649a3c0625047f9f805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-logic-apps-tooschema-version-2015-08-01-preview"></a>Jak toomigrate logiki aplikacji tooschema wersji 2015-08-01-preview
toomove istniejącego logic apps toohello nowego schematu, hello następujące:  

1. Otwórz aplikację logiki w hello portalu Azure  
2. Kliknij pozycję Aktualizuj schemat:
   
   ![Ikona interfejsu API][step1]   
   Strona aktualizacja schematu Hello Wyświetla oraz dokument tooa łącza zawierają szczegółowe informacje dotyczące hello ulepszeń w nowym schematem hello: ![Ikona interfejsu API][step2]

> [!NOTE]
> Po wybraniu **Aktualizuj schemat**, firma Microsoft automatycznie uruchomić hello kroków migracji i podaj hello kod wyjścia. Można użyć tego tooupdate definicję, jednak, należy przestrzegać dobrych praktyk kodowania, takich jak te opisane w hello **najlepsze rozwiązania** poniższej sekcji.
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-toohello-latest-schema-version"></a>Najważniejsze wskazówki dotyczące migrowania z najnowszej wersji schematu Logic apps toohello:
* Kopia hello migracji skryptu tooa nowe logiki aplikacji — nie zastępuj hello stare, dopóki nie przeprowadzisz migrowanych aplikacji testowych i potwierdzone hello działają zgodnie z oczekiwaniami.
* Przetestuj aplikację logiki **przed** użyciem jej w środowisku produkcyjnym.
* Po zakończeniu migracji Rozpocznij aktualizowanie Twojej hello toouse aplikacje logiki [zarządzanych interfejsów API](apis-list.md) w miarę możliwości. Na przykład możesz zacząć używać interfejsu DropBox 2 tam, gdzie jest używany interfejs DropBox 1.

## <a name="whats-next"></a>Co dalej
* [Dowiedz się, jak toomanually migrować aplikacje logiki](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: ./media/connectors-schema-migration/migrateschema1.png
[step2]: ./media/connectors-schema-migration/migrateschema2.png






