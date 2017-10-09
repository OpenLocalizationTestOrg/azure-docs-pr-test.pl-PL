---
title: Maszyny wirtualne Azure danych nauki jako serwery notesu IPython aaaProvision | Dokumentacja firmy Microsoft
description: "Ustaw zapasowych danych maszyny wirtualnej nauki jako serwer notesu IPython wraz z pomocniczymi narzędzia."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 95e1fa87-794a-4d03-80a4-af4f3f3ac31e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: 7c0abcbcb822918332f76a9f16690a72b90f4b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="provision-azure-data-science-virtual-machines-as-ipython-notebook-servers"></a>Maszyny wirtualne nauki udostępniania danych Azure jako serwery IPython notesu
Instrukcje są podane w tym miejscu opisano sposób tooset maszyny Wirtualnej platformy Azure i maszyny Wirtualnej platformy Azure z usługą SQL jako serwery IPython notesu. maszyny wirtualnej systemu Windows Hello jest skonfigurowany z obsługi narzędzi, takich jak notesu IPython, Eksploratora usługi Storage platformy Azure i AzCopy, a także innych narzędzi, które są przydatne w przypadku projektów analizy danych. Eksplorator usługi Storage platformy Azure i AzCopy, na przykład można podać wygodnie tooupload tooAzure pamięci masowej z komputera lokalnego lub toodownload go tooyour komputera lokalnego z magazynu. 

W tym menu łączy tootopics, które opisują sposób tooset się hello różnych środowiskach nauki danych przez hello [zespołu danych nauki procesu (TDSP)](data-science-process-overview.md).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

Kilka typów maszyn wirtualnych platformy Azure można udostępnić i skonfigurować toobe używany jako część środowiska nauki danych opartych na chmurze. decyzja Hello, o które podtyp maszyny wirtualnej toouse zależy od typu hello i ilość danych toobe modelowane uczenia maszynowego i hello docelowej dla tych danych w chmurze hello. 

* Aby uzyskać wskazówki dotyczące hello pytania tooconsider podczas tworzenia tej decyzji, zobacz [planowanie Your Azure Learning danych nauki środowiska maszyny](machine-learning-data-science-plan-your-environment.md). 
* Dla katalogu niektórych hello scenariusze mogą wystąpić podczas wykonywania zaawansowane metody analizy, zobacz [scenariusze hello zaawansowane procesu analizy i technologii w usłudze Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md)

Dostępne są dwa zestawy instrukcji:

* [Skonfiguruj maszynę wirtualną platformy Azure jako serwer notesu IPython zaawansowana analityka](machine-learning-data-science-setup-virtual-machine.md) pokazuje, jak tooprovision maszyny wirtualnej platformy Azure z notesu IPython i inne narzędzia używane nauki danych toodo przypadki, w którym magazyn Azure innych niż SQL może być używane toostore hello danych.
* [Konfigurowanie maszyny wirtualnej Azure SQL Server jako serwer notesu IPython zaawansowana analityka](machine-learning-data-science-setup-sql-server-virtual-machine.md) pokazano, jak użyć tooprovision maszyny wirtualnej platformy Azure programu SQL Server z notesu IPython i inne narzędzia analizy danych toodo przypadki, w którym bazy danych SQL może być używane toostore hello danych.

Po zainicjowana i skonfigurowana, te maszyny wirtualne są gotowe do użycia jako serwery notesu IPython hello eksploracji i przetwarzania danych oraz inne zadania wymagane w połączeniu z usługi Azure Machine Learning i hello zespołu danych nauki procesu (TDSP). Witaj kolejne kroki w procesie nauki danych hello są mapowane w hello [ścieżka szkoleniowa dotycząca TDSP](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) i mogą obejmować następujące kroki, które przenoszenia danych do programu SQL Server lub HDInsight, przetwarzania i przykładowe istnieje on w ramach przygotowania do uczenia z danych hello Azure Uczenie maszynowe.

> [!NOTE]
> Maszyny wirtualne platformy Azure kosztują jako **płać tylko w przypadku należy użyć**. tooensure, które nie są rozliczane, gdy nie używać sieci maszyny wirtualnej, ma toobe w hello **zatrzymane (Deallocated)** stanu z hello [klasycznego portalu Azure](http://manage.windowsazure.com/). Instrukcje krok po kroku lub jak toodeallocate użytkownik maszyny wirtualnej, zobacz [zamykania i Cofnij Przydział maszyny wirtualnej nieużywane](machine-learning-data-science-setup-virtual-machine.md#shutdown)
> 
> 

