---
title: "toomigrate aaaHow z sieci Wirtualnej usługi RemoteApp tooan sieci Wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomigrate z sieci Wirtualnej usługi RemoteApp tooan sieci Wirtualnej Azure"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: baea5d29-353b-48f8-b47f-806f2163e067
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: c0f8617556c6f1e33eca8322febf67ff33937ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-a-hybrid-collection-from-a-remoteapp-vnet-tooan-azure-vnet"></a>Jak toomigrate kolekcji hybrydowej z sieci Wirtualnej usługi RemoteApp tooan sieci Wirtualnej Azure
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Dobre wieści! Firma Microsoft włączono kolekcji usługi RemoteApp hybrydowego toodeploy bezpośrednio do użytkownika istniejących sieci wirtualnych platformy Azure (sieci wirtualne) zamiast tworzenia sieci wirtualnych specyficzne dla usługi RemoteApp. Dzięki temu można wykorzystać hello najnowszych funkcji sieciami Wirtualnymi (na przykład ExpressRoute) i nadaj z hybrydowego kolekcje sieci bezpośredniego dostępu tooother usług platformy Azure i maszyny wirtualne wdrażane toothat sieci Wirtualnej.  (To pozwala lepszą wydajność i Instalator łatwiejsze niż konfiguracje sieci Wirtualnej do sieci Wirtualnej).

Załóżmy, że zostały już utworzone kolekcji usługi RemoteApp hybrydowe o nazwie *OriginalCollection* z sieci Wirtualnej usługi RemoteApp o nazwie *RemoteAppVNET*. Poniżej przedstawiono toomigrate kroki hello go tooa nowej sieci Wirtualnej platformy Azure o nazwie *AzureVNET*.

1. Na powitania **sieci** kartę w hello [portalu zarządzania](http://manage.windowsazure.com/), utworzyć sieć Wirtualną o nazwie *AzureVNET*za pomocą hello tej samej lokalizacji, konfiguracji serwera DNS i przestrzeń adresową (dla co najmniej jednego z hello *AzureVNET* podsieci) jako użyte do *RemoteAppVNET*.
2. Skonfiguruj *AzureVNET* tooeither hosta lub wdrożenie usługi Active Directory toohello łączności sieciowej który *OriginalCollection* jest przyłączonych do domeny do.
3. Na powitania **nimi** pozycję Utwórz kolekcję RemoteApp o nazwie *nowej kolekcji*. (Użyj hello **Utwórz z sieci Wirtualnej** opcję nie **szybkie tworzenie**.)
4. Skonfiguruj *NewCollection* toobe wdrożone podsieci tooa *AzureVNET*.
5. Skonfiguruj *NewCollection* toouse hello takiego samego obrazu i informacji dotyczących przyłączania domeny jako użyte do *OriginalCollection*.
6. Po kilku godzinach *NewCollection* będą widoczne na liście kolekcji o stanie aktywnym.

Teraz Jeśli nie potrzebujesz toomigrate informacje o użytkowniku z hello oryginalnej kolekcji toohello nową kolekcję, zrobić dalej następujące kroki:

1. Usuń *OriginalCollection*.
2. Usuń *RemoteAppVNET*.

I gotowe!

Alternatywnie Jeśli potrzebujesz informacji o użytkowniku toomigrate z hello oryginalnej kolekcji toohello nową kolekcję, zrobić dalej następujące kroki:

1. Wyślij wiadomość e-mail zbyt[ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) z Identyfikatorem subskrypcji platformy Azure Witaj nazwy oryginalnego kolekcji i hello nazwę nowej kolekcji i poproś o toomigrate informacje o użytkowniku.
2. W ciągu 2 dni roboczych hello RemoteApp team zostaną przeniesione listy dostępu użytkownika hello wszystkich dokumentów użytkownika i ustawień użytkownika z hello oryginalnej kolekcji toohello nowej kolekcji.
3. Usuń *OriginalCollection*.
4. Usuń *RemoteAppVNET*.

I teraz wszystko gotowe!

Jeśli masz pytania lub potrzebujesz pomocy specjalne, Wyślij wiadomość e-mail [ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).

