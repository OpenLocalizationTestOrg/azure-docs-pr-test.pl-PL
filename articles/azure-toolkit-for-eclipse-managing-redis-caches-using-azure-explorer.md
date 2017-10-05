---
title: "Zarządzanie za pomocą Eksploratora Azure dla programu Eclipse pamięci podręczne Redis | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zarządzać pamięci podręczne Azure redis za pomocą Eksploratora Azure dla programu Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/14/2017
ms.author: robmcm
ms.openlocfilehash: dc1ed15cb83e6ddc8cf84f5c52a0482231f75e40
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="managing-redis-caches-using-the-azure-explorer-for-eclipse"></a>Zarządzanie za pomocą Eksploratora Azure dla programu Eclipse pamięci podręczne Redis

Eksploratora Azure, która jest częścią zestawu narzędzi platformy Azure dla programu Eclipse, zapewnia się, że Java deweloperom łatwe w użyciu rozwiązanie do zarządzania redis pamięci podręcznych na koncie Azure z poziomu środowiska Eclipse IDE.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-eclipse"></a>Tworzenie pamięci podręcznej Redis przy użyciu programu Eclipse

W poniższych krokach objaśniono kroków w celu tworzenia pamięci podręcznej redis przy użyciu Eksploratora Azure.

1. Zaloguj się do konta platformy Azure, korzystając z procedury w [znak w instrukcji dla zestawu narzędzi platformy Azure dla programu Eclipse] artykułu.

1. W **Eksploratora Azure** okna narzędzia, a następnie rozwiń **Azure** węzła, kliknij prawym przyciskiem myszy **pamięci podręczne Redis**, a następnie kliknij przycisk **Tworzenie pamięci podręcznej Redis**.

   ![Tworzenie Menu pamięci podręcznej Redis][CR01]

1. Gdy **nowa pamięć podręczna Redis** zostanie wyświetlone okno dialogowe, określ następujące opcje:

   ![Utwórz nowe okno dialogowe pamięci podręcznej Redis][CR02]

   a. **Nazwa DNS**: Określa poddomenie DNS nowej pamięci podręcznej redis, który jest dołączany na początku ". redis.cache.windows.net", na przykład: *wingtiptoys.redis.cache.windows.net*.

   b. **Subskrypcja**: Określa subskrypcji platformy Azure, którego chcesz użyć dla nowej pamięci podręcznej redis.

   c. **Grupa zasobów**: Określa grupę zasobów dla pamięci podręcznej redis; musisz wybrać jedną z następujących opcji:
      * **Utwórz nowy**: Określa, czy chcesz utworzyć nową grupę zasobów.
      * **Użyj istniejącego**: Określa, że wybiorą z listy grup zasobów skojarzonych z Twoim kontem platformy Azure.

   d. **Lokalizacja**: Określa lokalizację, w której utworzono pamięć podręczną redis; na przykład *zachodnie stany USA*.

   e. **Warstwa cenowa**: Określa warstwy cenowej korzysta z pamięci podręcznej redis; to ustawienie określa liczbę połączeń klientów. (Aby uzyskać więcej informacji, zobacz [cennik pamięci podręcznej Redis].)

   f. **Port bez protokołu SSL**: Określa, czy pamięć podręczna redis zezwala na połączenia SSL nie; domyślnie są dozwolone tylko na połączenia SSL.

1. Po określeniu wszystkie ustawienia pamięci podręcznej redis, kliknij przycisk **OK**.

Po utworzeniu pamięci podręcznej redis, będzie on wyświetlany w Eksploratorze Azure.

   ![Pamięci podręcznej w Eksploratorze Azure redis][CR03]

> [!NOTE]
>
> Aby uzyskać więcej informacji o konfigurowaniu Azure ustawienia pamięci podręcznej redis, zobacz [Konfigurowanie pamięci podręcznej Redis Azure].
>

## <a name="display-the-properties-for-your-redis-cache-in-eclipse"></a>Wyświetl właściwości dla pamięci podręcznej Redis w środowisku Eclipse

1. W Eksploratorze Azure, kliknij prawym przyciskiem myszy pamięci podręcznej redis, a następnie kliknij przycisk **Pokaż właściwości**.

   ![Azure menu kontekstowe Eksploratora, aby wyświetlić właściwości pamięci podręcznej redis][SP01]

1. W Eksploratorze Azure Wyświetla właściwości dla pamięci podręcznej redis.

   ![Właściwości pamięci podręcznej Redis][SP02]

## <a name="delete-your-redis-cache-by-using-eclipse"></a>Usuń pamięć podręczną Redis za pomocą programu Eclipse

1. W Eksploratorze Azure, kliknij prawym przyciskiem myszy pamięci podręcznej redis, a następnie kliknij przycisk **usunąć**.

   ![Azure menu kontekstowego Eksploratora można usunąć pamięci podręcznej redis][DE01]

1. Kliknij przycisk **OK** po wyświetleniu monitu, aby usunąć pamięć podręczną redis.

   ![Usuwanie wiersza pamięci podręcznej redis][DE02]

## <a name="next-steps"></a>Następne kroki

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

Aby uzyskać więcej informacji o pamięci podręcznej Azure redis, ustawienia konfiguracji i cenach zobacz następujące linki:

* [Azure Redis Cache]
* [Dokumentacja pamięci podręcznej redis]
* [cennik pamięci podręcznej Redis]
* [Konfigurowanie pamięci podręcznej Redis Azure]

<!-- URL List -->

[cennik pamięci podręcznej Redis]: https://azure.microsoft.com/pricing/details/cache/
[Azure Redis Cache]: https://azure.microsoft.com/services/cache/
[Dokumentacja pamięci podręcznej redis]: ./redis-cache/index.md
[Konfigurowanie pamięci podręcznej Redis Azure]: ./redis-cache/cache-configure.md
[znak w instrukcji dla zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md (Instrukcje logowania dotyczące zestawu narzędzi platformy Azure dla środowiska Eclipse)

<!-- IMG List -->

[CR01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE02.png
