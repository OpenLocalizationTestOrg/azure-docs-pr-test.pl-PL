---
title: repozytoria rejestru kontenera aaaAzure | Dokumentacja firmy Microsoft
description: "Jak toouse magazynach rejestru kontenera Azure obrazy usługi Docker"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: cristyg
ms.openlocfilehash: 06172a63465838a78a607f268da116d8158789ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a>Repozytoria rejestru kontenera platformy Azure

Rejestry organizacji IANA kontenera platformy Azure są zgodne z wieloma usługami i orchestrators. toomake go łatwiejsze tootrack hello źródła usługi i agentów, na których jest używane ACR, możemy uruchomiony przy użyciu pola nagłówka Docker hello w pliku Docker.config hello.



## <a name="viewing-repositories-in-hello-portal"></a>Wyświetlanie repozytoria w hello portalu

nagłówki ACR Hello wykonaj hello format:
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* Chmury: Azure, Azure stosu, lub inne dla instytucji rządowych lub chmury Azure określonego kraju. Mimo że stosu Azure i dla instytucji rządowych chmury nie są obecnie obsługiwane, ten parametr umożliwia wsparcia w przyszłości.
* Usługi: Nazwa hello usługi.
* Optionalservicename: opcjonalny parametr dla usług z subservices lub toospecify jednostki SKU (przykład: aplikacje sieci web odpowiada/app-service/aplikacje sieci web Azure).

Partner usługi i orchestrators są zachęcani toouse określonego nagłówka wartości toohelp z naszych danych telemetrycznych. Użytkownicy, można również zmodyfikować wartość hello przekazanego toohello nagłówka, jeśli potrzebna jest tak.

chcemy ACR partnerów toouse toopopulate hello "X-Meta-źródła-Client" pole wartości Hello jest poniżej:

| Nazwa usługi              | Nagłówek                                |
| ------------------------- | ------------------------------------- |
| Azure Container Service   | / compute/azure usługi kontenera platformy Azure — |
| Usługi aplikacji — aplikacje sieci Web    | / app-service/aplikacje sieci web Azure            |
| Usługi aplikacji — aplikacje logiki  | Azure/app-service / — aplikacje logiki          |
| Batch                     | / compute/partii zadań Azure                   |
| Cloud Console             | Azure/chmurze konsoli                   |
| Funkcje                 | Azure/obliczeniowych               |
| Internet rzeczy - Centrum  | Centrum Azure/iot                         |
| HDInsight                 | hdinsight-Azure/danych                  |
| Jenkins                   | Azure/wpięć                         |
| Usługa Machine Learning          | Azure/data/machile-learning           |
| Service Fabric            | / compute /-sieć szkieletowa usług Azure          |
| VSTS                      | Azure/vsts                            |


## <a name="next-steps"></a>Następne kroki
[Dowiedz się więcej o rejestrów i hello obsługiwane usługi i orchestrators](container-registry-intro.md)
