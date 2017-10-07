---
title: "przy użyciu pamięci podręczne Redis aaaManaging hello Eksploratora Azure dla programu Eclipse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage Twojego redis Azure buforuje przy użyciu hello Eksploratora Azure dla programu Eclipse."
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
ms.openlocfilehash: aa0c38862bda7919a3fc6c53c2fdaf555dd64bff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-redis-caches-using-hello-azure-explorer-for-eclipse"></a>Zarządzanie za pomocą hello Eksploratora Azure dla programu Eclipse pamięci podręczne Redis

Witaj Eksploratora Azure, który jest częścią zestawu narzędzi platformy Azure dla programu Eclipse hello, zapewnia się, że Java deweloperom łatwe w użyciu rozwiązanie do zarządzania redis pamięci podręcznych na koncie Azure z wewnątrz hello Eclipse IDE.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-eclipse"></a>Tworzenie pamięci podręcznej Redis przy użyciu programu Eclipse

Witaj, wykonaj czynności umożliwia przeprowadzenie toocreate kroki hello pamięci podręcznej redis przy użyciu hello Azure Eksploratora.

1. Zaloguj się tooyour konto platformy Azure, wykonując kroki hello w hello [znak w instrukcji hello zestawu narzędzi platformy Azure dla programu Eclipse] artykułu.

1. W hello **Eksploratora Azure** okna narzędzia, a następnie rozwiń hello **Azure** węzła, kliknij prawym przyciskiem myszy **pamięci podręczne Redis**, a następnie kliknij przycisk **Tworzenie pamięci podręcznej Redis**.

   ![Tworzenie Menu pamięci podręcznej Redis][CR01]

1. Gdy hello **nowa pamięć podręczna Redis** zostanie wyświetlone okno dialogowe, określ hello następujące opcje:

   ![Utwórz nowe okno dialogowe pamięci podręcznej Redis][CR02]

   a. **Nazwa DNS**: Określa hello poddomenie DNS dla hello nowej pamięci podręcznej redis pamięci podręcznej, która jest reprezentowana zbyt ". redis.cache.windows .net", na przykład: *wingtiptoys.redis.cache.windows.net*.

   b. **Subskrypcja**: Określa hello subskrypcji platformy Azure ma toouse hello nowej pamięci podręcznej redis.

   c. **Grupa zasobów**: Określa hello grupy zasobów dla pamięci podręcznej redis; należy toochoose hello następujące opcje:
      * **Utwórz nowy**: Określa, że toocreate nową grupę zasobów.
      * **Użyj istniejącego**: Określa, że wybiorą z listy grup zasobów skojarzonych z Twoim kontem platformy Azure.

   d. **Lokalizacja**: Określa lokalizację hello, w których tworzone jest pamięć podręczna redis; na przykład *zachodnie stany USA*.

   e. **Warstwa cenowa**: Określa warstwy cenowej korzysta z pamięci podręcznej redis; to ustawienie określa hello liczbę połączeń klientów. (Aby uzyskać więcej informacji, zobacz [cennik pamięci podręcznej Redis].)

   f. **Port bez protokołu SSL**: Określa, czy pamięć podręczna redis zezwala na połączenia SSL nie; domyślnie są dozwolone tylko na połączenia SSL.

1. Po określeniu wszystkie ustawienia pamięci podręcznej redis, kliknij przycisk **OK**.

Po utworzeniu pamięci podręcznej redis, będzie wyświetlana w hello Eksploratora Azure.

   ![Pamięci podręcznej w Eksploratorze Azure redis][CR03]

> [!NOTE]
>
> Aby uzyskać więcej informacji o konfigurowaniu Azure ustawienia pamięci podręcznej redis, zobacz [jak tooconfigure pamięć podręczna Redis Azure].
>

## <a name="display-hello-properties-for-your-redis-cache-in-eclipse"></a>Wyświetl właściwości powitania dla pamięci podręcznej Redis w środowisku Eclipse

1. Witaj Eksploratora Azure, kliknij prawym przyciskiem myszy pamięć podręczna redis i kliknij przycisk **Pokaż właściwości**.

   ![Azure Explorer właściwości menu kontekstowego toodisplay na potrzeby pamięci podręcznej redis][SP01]

1. Hello Azure Explorer wyświetla hello właściwości pamięci podręcznej redis.

   ![Właściwości pamięci podręcznej Redis][SP02]

## <a name="delete-your-redis-cache-by-using-eclipse"></a>Usuń pamięć podręczną Redis za pomocą programu Eclipse

1. Witaj Eksploratora Azure, kliknij prawym przyciskiem myszy pamięć podręczna redis i kliknij przycisk **usunąć**.

   ![Kontekst menu toodelete pamięci podręcznej redis Azure Explorer][DE01]

1. Kliknij przycisk **OK** po wyświetleniu toodelete pamięci podręcznej redis.

   ![Usuwanie wiersza pamięci podręcznej redis][DE02]

## <a name="next-steps"></a>Następne kroki

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

Aby uzyskać więcej informacji o pamięci podręcznej Azure redis, ustawienia konfiguracji i cenach Zobacz hello następującego łącza:

* [Azure Redis Cache]
* [Dokumentacja pamięci podręcznej redis]
* [cennik pamięci podręcznej Redis]
* [jak tooconfigure pamięć podręczna Redis Azure]

<!-- URL List -->

[cennik pamięci podręcznej Redis]: https://azure.microsoft.com/pricing/details/cache/
[Azure Redis Cache]: https://azure.microsoft.com/services/cache/
[Dokumentacja pamięci podręcznej redis]: ./redis-cache/index.md
[jak tooconfigure pamięć podręczna Redis Azure]: ./redis-cache/cache-configure.md
[znak w instrukcji hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md

<!-- IMG List -->

[CR01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE02.png
