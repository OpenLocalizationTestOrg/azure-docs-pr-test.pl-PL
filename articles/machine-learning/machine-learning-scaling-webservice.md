---
title: "Współbieżność tooincrease aaaHow usługi sieci web Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooincrease współbieżności usługi Azure Machine Learning usługi sieci web przez dodanie dodatkowych punktów końcowych."
services: machine-learning
documentationcenter: 
author: neerajkh
manager: srikants
editor: cgronlun
keywords: "Azure uczenia maszynowego, usług sieci web operationalization skalowania, punkt końcowy, współbieżności"
ms.assetid: c2c51d7f-fd2d-4f03-bc51-bf47e6969296
ms.service: machine-learning
ms.devlang: NA
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/23/2017
ms.author: neerajkh
ms.openlocfilehash: e2ad16ec766820a64f36c31232f6a33a79196af4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a>Skalowanie usługi sieci web Azure Machine Learning, dodając dodatkowe punkty końcowe
> [!NOTE]
> W tym temacie opisano techniki stosowane tooa **klasycznego** usługi Machine Learning w sieci Web. 
> 
> 

Domyślnie poszczególnych opublikowanych usług sieci Web jest skonfigurowana toosupport 20 równoczesnych żądań i może być możliwie jak 200 równoczesnych żądań. Witaj klasyczny portal Azure udostępnia tooset sposób tę wartość, uczenie maszynowe Azure automatycznie optymalizuje hello ustawienie tooprovide hello najlepszą wydajność usługi sieci web i hello portalu wartość jest ignorowana. 

Jeśli planujesz API hello toocall z obciążeniem wyższa niż wartość maksymalnej liczby równoczesnych wywołań 200 będzie obsługiwać, należy utworzyć wiele punktów końcowych na powitania tej samej usługi sieci Web. Następnie można losowo dystrybucji obciążenia we wszystkich z nich.

Witaj skalowanie usługi sieci Web jest typowych zadań. Niektóre przyczyny tooscale są toosupport ponad 200 równoczesnych żądań, zwiększyć dostępność za pośrednictwem wiele punktów końcowych lub podaj oddzielne punkty końcowe dla usługi sieci web hello. Skala hello można zwiększyć przez dodanie dodatkowych punktów końcowych dla hello tej samej usługi sieci Web za pośrednictwem [klasycznego portalu Azure](https://manage.windowsazure.com/) lub hello [Usługa sieci Web systemu Azure Machine Learning](https://services.azureml.net/) portalu.

Aby uzyskać więcej informacji na temat dodawania nowych punktów końcowych, zobacz [tworzenie punktów końcowych](machine-learning-create-endpoint.md).

Należy zwrócić uwagę przy użyciu liczba wysokiej współbieżności mogą być szkodliwe, jeśli nie jest wywoływany hello interfejsu API z odpowiednio wysoki współczynnik. Sporadyczne przekroczeń limitu czasu i/lub nagłego mogą zobaczyć w opóźnienia hello umieszczenie stosunkowo niska obciążenia na interfejs API skonfigurowane dla wysokie obciążenie.

powitalne synchroniczne interfejsy API są zazwyczaj używane w sytuacjach, w których jest potrzebne małe opóźnienia. W tym miejscu opóźnienia oznacza czas hello przyjmuje dla jednego żądania toocomplete hello interfejsu API, a nie konto do wszelkich opóźnień sieci. Załóżmy, że masz interfejsu API z opóźnieniem 50 ms. toofully stosowanie hello dostępnej pojemności z poziomu ograniczania wysokiej i maksymalnej liczby równoczesnych wywołań = 20, należy toocall ten interfejs API 20 * 1000 / 50 = 400 razy na sekundę. Dalsze to rozszerzenie, maksymalnej liczby równoczesnych wywołań 200 umożliwia możesz toocall hello 4000 interfejsu API razy na sekundę, przy założeniu opóźnienia 50 ms.

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
