---
title: aaaCreate aplikacji funkcji z hello portalu Azure | Dokumentacja firmy Microsoft
description: "Tworzenie nowej aplikacji funkcji w usłudze Azure App Service przy użyciu portalu hello."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/11/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c531fc71c798edf22e25a5f4b79c15413809dc86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-from-hello-azure-portal"></a>Tworzenie aplikacji funkcji z hello portalu Azure

Aplikacje platformy Azure funkcji używa hello infrastruktury usługi Azure App Service. W tym temacie opisano sposób toocreate aplikacji funkcji w hello portalu Azure. Aplikacja funkcji jest hello obsługujący wykonanie hello poszczególnych funkcji. Po utworzeniu aplikacji funkcji w hostingu planu usługi aplikacji hello aplikacji funkcji można korzystać ze wszystkich funkcji hello usługi App Service.

## <a name="create-a-function-app"></a>Tworzenie aplikacji funkcji

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

Podczas tworzenia aplikacji funkcji, podaj prawidłową **Nazwa aplikacji**, która może zawierać tylko litery, cyfry i łączniki. Podkreślenie (**_**) nie jest dozwolonym znakiem.

Nazwy kont usługi Magazyn muszą mieć długość od 3 do 24 znaków i mogą zawierać tylko cyfry i małe litery. Nazwa konta magazynu musi być unikatowa w obrębie platformy Azure. 

Po utworzeniu hello funkcji aplikacji, można utworzyć pojedynczych funkcji w różnych językach co najmniej jeden. Tworzenie funkcji [przy użyciu portalu hello](functions-create-first-azure-function.md#create-function), [ciągłe wdrażanie](functions-continuous-deployment.md), lub [przekazywanie z FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).

## <a name="service-plans"></a>Plany usługi

Usługa Azure Functions oferuje dwa pakiety różnych usług: plan zużycia i plan usługi aplikacji. plan zużycie Hello automatycznie przydzieli moc obliczeniową, gdy kod działa, możliwość skalowania w poziomie jako niezbędne toohandle obciążenia, a następnie skali w kodu nie jest uruchomiona. plan usługi aplikacji Hello zapewnia funkcji urządzeniami hello tooall dostępu aplikacji usługi App Service. Musisz wybrać plan usługi po utworzeniu aplikacji funkcji, a obecnie nie można zmienić. Aby uzyskać więcej informacji, zobacz [wybierz usługi Azure Functions plan hostingu](functions-scale.md).

Jeśli planujesz funkcji JavaScript toorun plan usługi aplikacji, należy wybrać plan o mniejszej liczby rdzeni. Aby uzyskać więcej informacji, zobacz hello [JavaScript — odwołanie do funkcji](functions-reference-node.md#choose-single-core-app-service-plans).

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a>Wymagania dotyczące konta magazynu

Podczas tworzenia aplikacji funkcji w usłudze App Service, należy utworzyć lub połączyć tooa ogólnego przeznaczenia konta usługi Magazyn Azure obsługującym magazynu obiektów Blob, kolejki i tabeli. Wewnętrznie funkcji używa magazynu dla operacji, takich jak zarządzanie wyzwalaczy i rejestrowanie wykonania funkcji. Niektóre konta magazynu nie obsługują kolejek i tabel, takich jak konta magazynu tylko do obiektów blob, usługa Azure Premium Storage i kont magazynu ogólnego przeznaczenia z replikacją ZRS. Te konta są filtrowane z z hello bloku konto magazynu podczas tworzenia aplikacji funkcji.

>[!NOTE]
>Podczas korzystania z planu obsługi zużycia hello, plików konfiguracji kod i powiązanie funkcji są przechowywane w na koncie magazynu głównego hello usługi Magazyn plików Azure. Podczas usuwania konta magazynu głównego hello ta zawartość zostanie usunięta i nie może zostać odzyskany.

toolearn więcej informacji na temat typów kont magazynu, zobacz [wprowadzenie do usług magazynu Azure hello](../storage/common/storage-introduction.md#introducing-the-azure-storage-services). 

## <a name="next-steps"></a>Następne kroki

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



