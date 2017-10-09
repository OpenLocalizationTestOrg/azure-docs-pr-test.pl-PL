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
# <a name="how-toomigrate-logic-apps-tooschema-version-2015-08-01-preview"></a><span data-ttu-id="a4c87-104">Jak toomigrate logiki aplikacji tooschema wersji 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="a4c87-104">How toomigrate logic apps tooschema version 2015-08-01-preview</span></span>
<span data-ttu-id="a4c87-105">toomove istniejącego logic apps toohello nowego schematu, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="a4c87-105">toomove your existing logic apps toohello new schema, do hello following:</span></span>  

1. <span data-ttu-id="a4c87-106">Otwórz aplikację logiki w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a4c87-106">Open your logic app in hello Azure portal</span></span>  
2. <span data-ttu-id="a4c87-107">Kliknij pozycję Aktualizuj schemat:</span><span class="sxs-lookup"><span data-stu-id="a4c87-107">Click Update Schema:</span></span>
   
   <span data-ttu-id="a4c87-108">![Ikona interfejsu API][step1] </span><span class="sxs-lookup"><span data-stu-id="a4c87-108">![API Icon][step1] </span></span>  
   <span data-ttu-id="a4c87-109">Strona aktualizacja schematu Hello Wyświetla oraz dokument tooa łącza zawierają szczegółowe informacje dotyczące hello ulepszeń w nowym schematem hello: ![Ikona interfejsu API][step2]</span><span class="sxs-lookup"><span data-stu-id="a4c87-109">hello Update Schema page displays and provides a link tooa document that provide details on hello improvements in hello new schema: ![API Icon][step2]</span></span>

> [!NOTE]
> <span data-ttu-id="a4c87-110">Po wybraniu **Aktualizuj schemat**, firma Microsoft automatycznie uruchomić hello kroków migracji i podaj hello kod wyjścia.</span><span class="sxs-lookup"><span data-stu-id="a4c87-110">When you select **Update Schema**, we automatically run hello migration steps and provide hello code output for you.</span></span> <span data-ttu-id="a4c87-111">Można użyć tego tooupdate definicję, jednak, należy przestrzegać dobrych praktyk kodowania, takich jak te opisane w hello **najlepsze rozwiązania** poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="a4c87-111">You can use this tooupdate your definition, however, ensure you follow good coding practices such as those outlined in hello **Best practices** section below.</span></span>
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-toohello-latest-schema-version"></a><span data-ttu-id="a4c87-112">Najważniejsze wskazówki dotyczące migrowania z najnowszej wersji schematu Logic apps toohello:</span><span class="sxs-lookup"><span data-stu-id="a4c87-112">Best practices when migrating your Logic apps toohello latest schema version:</span></span>
* <span data-ttu-id="a4c87-113">Kopia hello migracji skryptu tooa nowe logiki aplikacji — nie zastępuj hello stare, dopóki nie przeprowadzisz migrowanych aplikacji testowych i potwierdzone hello działają zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="a4c87-113">Copy hello migrated script tooa new Logic App - don't overwrite hello old one until you've completed your testing and confirmed hello migrated app works as expected.</span></span>
* <span data-ttu-id="a4c87-114">Przetestuj aplikację logiki **przed** użyciem jej w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="a4c87-114">Test your Logic app **before** putting in production</span></span>
* <span data-ttu-id="a4c87-115">Po zakończeniu migracji Rozpocznij aktualizowanie Twojej hello toouse aplikacje logiki [zarządzanych interfejsów API](apis-list.md) w miarę możliwości.</span><span class="sxs-lookup"><span data-stu-id="a4c87-115">After migration completes, start updating your Logic apps toouse hello [managed APIs](apis-list.md) where possible.</span></span> <span data-ttu-id="a4c87-116">Na przykład możesz zacząć używać interfejsu DropBox 2 tam, gdzie jest używany interfejs DropBox 1.</span><span class="sxs-lookup"><span data-stu-id="a4c87-116">For example, you can start using Dropbox v2, whereever you are using DropBox v1.</span></span>

## <a name="whats-next"></a><span data-ttu-id="a4c87-117">Co dalej</span><span class="sxs-lookup"><span data-stu-id="a4c87-117">What's next</span></span>
* [<span data-ttu-id="a4c87-118">Dowiedz się, jak toomanually migrować aplikacje logiki</span><span class="sxs-lookup"><span data-stu-id="a4c87-118">Learn how toomanually migrate your Logic apps</span></span>](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: ./media/connectors-schema-migration/migrateschema1.png
[step2]: ./media/connectors-schema-migration/migrateschema2.png






