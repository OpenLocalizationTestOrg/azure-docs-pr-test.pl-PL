---
title: Umieszczanie maszyn wirtualnych nauki danych Azure jako serwery notesu IPython | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: db1ffb2a226a087ecea2ea6f560c6b803e33d8c7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="provision-azure-data-science-virtual-machines-as-ipython-notebook-servers"></a>Maszyny wirtualne nauki udostępniania danych Azure jako serwery IPython notesu
Instrukcje znajdują się w tym miejscu, który opisano, jak skonfigurować maszyny Wirtualnej platformy Azure i maszyny Wirtualnej platformy Azure z usługą SQL jako serwery IPython notesu. Maszyny wirtualnej systemu Windows jest konfigurowana obsługi narzędzi, takich jak notesu IPython, Eksploratora usługi Storage platformy Azure i AzCopy, a także innych narzędzi, które są przydatne w przypadku projektów analizy danych. Eksplorator usługi Storage platformy Azure i AzCopy, na przykład można podać wygodnie przekazywać dane do magazynu Azure z komputera lokalnego lub pobrać go na komputerze lokalnym, z magazynu. 

To menu zawiera linki do tematów opisujących sposób skonfigurować w różnych środowiskach nauki danych używany przez [zespołu danych nauki procesu (TDSP)](data-science-process-overview.md).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

Kilka typów maszyn wirtualnych platformy Azure można udostępniać oraz skonfigurowana do używania jako część środowiska nauki danych opartych na chmurze. Decyzja o którym podtyp maszyny wirtualnej do użycia zależy od typu i ilość danych należy modelować uczenia maszynowego i docelowej dla tych danych w chmurze. 

* Aby uzyskać wskazówki dotyczące pytania, które należy wziąć pod uwagę podczas tworzenia tej decyzji, zobacz [planowanie Your Azure Learning danych nauki środowiska maszyny](machine-learning-data-science-plan-your-environment.md). 
* Dla katalogu niektóre scenariusze mogą wystąpić podczas wykonywania zaawansowane metody analizy, zobacz [scenariusze zaawansowane procesu analizy i technologii w usłudze Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md)

Dostępne są dwa zestawy instrukcji:

* [Skonfiguruj maszynę wirtualną platformy Azure jako serwer notesu IPython zaawansowana analityka](machine-learning-data-science-setup-virtual-machine.md) pokazano, jak udostępnić maszynie wirtualnej platformy Azure z notesu IPython i inne narzędzia używane do analizy danych w przypadkach, w których można magazyn Azure innych niż SQL używany do przechowywania danych.
* [Konfigurowanie maszyny wirtualnej Azure SQL Server jako serwer notesu IPython zaawansowana analityka](machine-learning-data-science-setup-sql-server-virtual-machine.md) pokazano, jak udostępnić maszynie wirtualnej platformy Azure programu SQL Server z notesu IPython i inne narzędzia używane do analizy danych w przypadkach, w których można bazy danych SQL używany do przechowywania danych.

Po zainicjowana i skonfigurowana, te maszyny wirtualne są gotowe do użycia jako serwery notesu IPython eksploracji i przetwarzania danych oraz inne zadania wymagane w połączeniu z usługi Azure Machine Learning i procesu nauki danych zespołu (TDSP). Następne kroki w procesie nauki danych są mapowane w [ścieżka szkoleniowa dotycząca TDSP](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) i mogą obejmować następujące kroki, które przenoszenia danych do programu SQL Server lub HDInsight, przetwarzania i przykładowe istnieje on w ramach przygotowania do uczenia z danych Azure maszyny Learning.

> [!NOTE]
> Maszyny wirtualne platformy Azure kosztują jako **płać tylko w przypadku należy użyć**. Aby upewnić się, że nie rozliczanych, gdy nie używać sieci maszyny wirtualnej, musi ona być w **zatrzymane (Deallocated)** stanu z [klasycznego portalu Azure](http://manage.windowsazure.com/). Aby uzyskać instrukcje krok po kroku lub jak Cofnij Przydział maszyny wirtualnej, zobacz [zamykania i Cofnij Przydział maszyny wirtualnej nieużywane](machine-learning-data-science-setup-virtual-machine.md#shutdown)
> 
> 

