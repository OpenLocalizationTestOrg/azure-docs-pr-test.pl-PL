---
title: "aaaAzure wysoką dostępność usług Analysis Services | Dokumentacja firmy Microsoft"
description: "Zapewnienie wysokiej dostępności usług Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 6e09536c5bd7dc7f88f9b662e1a9f42d2b8c969b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analysis-services-high-availability"></a>Wysoka dostępność usługi analizy
W tym artykule opisano, zapewniając wysoką dostępność dla serwerów usług Azure Analysis Services. 


## <a name="assuring-high-availability-during-a-service-disruption"></a>Zapewnienie wysokiej dostępności podczas przerw w działaniu usługi
Gdy przypadkach centrum danych platformy Azure mogą mieć awarii. W przypadku wystąpienia awarii powoduje zakłócenia biznesowych, może trwać kilka minut lub może trwać godzin. Wysoka dostępność najczęściej jest to osiągane z nadmiarowością serwera. Z usług Azure Analysis Services można osiągnąć nadmiarowość przez utworzenie dodatkowych, pomocnicze serwery w regionach co najmniej jeden. Podczas tworzenia nadmiarowych serwerów, tooassure hello danych i metadanych na tych serwerach jest zsynchronizowana z serwerem hello w regionie, który przeszedł do trybu offline, można wykonywać następujące czynności:

* Wdrażanie serwerów tooredundant modeli w różnych regionach. Ta metoda wymaga przetwarzania danych na serwerze podstawowym i nadmiarowego serwerów w równolegle, zapewniając wszystkie serwery są w synchronizacji.

* Wykonaj kopię zapasową baz danych z serwera podstawowego i przywracania na serwerach nadmiarowe. Na przykład można zautomatyzować magazynu tooAzure kopii zapasowych w nocy i przywrócić tooother nadmiarowe serwerami w różnych regionach. 

W obu przypadkach Jeśli serwer podstawowy ulegnie awarii, należy zmienić hello parametry połączenia w programie reporting server toohello tooconnect klientów w różnych regionalnych centrach danych. Tej zmiany należy traktować jako ostateczność i występuje tylko w przypadku awarii centrum danych w wyniku katastrofy regionalne. Jest bardziej prawdopodobne, awarii centrum danych podstawowego serwera hostingu przybyły trybu online przed można zaktualizować połączenia na wszystkich klientach. 



## <a name="related-information"></a>Informacje pokrewne
[Kopia zapasowa i przywracanie](analysis-services-backup.md)   
[Zarządzanie usług Azure Analysis Services](analysis-services-manage.md) 

