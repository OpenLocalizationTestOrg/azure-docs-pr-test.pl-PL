---
title: "Jak usunąć klaster usługi HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Informacje na różne sposoby, że możesz usunąć klaster usługi HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 55f7838b-9786-47ff-96db-1b64437bd0bb
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2018
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 04b89b2cceb18a0e3c88d0d1deada1a05b8187f6
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/18/2018
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-the-azure-cli"></a>Usuwanie klastra usługi HDInsight przy użyciu przeglądarki, programu PowerShell lub wiersza polecenia platformy Azure

Karta klastra usługi HDInsight zaczyna się po klastra jest tworzony i zatrzymuje po usunięciu klastra. Opłaty są naliczane za minutę, więc jeśli klaster nie jest używany, należy go usunąć. W tym dokumencie Dowiedz się jak usunąć klaster za pomocą portalu Azure, programu Azure PowerShell i Azure CLI 1.0.

> [!IMPORTANT]
> Usunięcie klastra usługi HDInsight nie powoduje usunięcia konta magazynu Azure lub usługi Data Lake Store jest skojarzone z klastrem. Można ponownie użyć danych przechowywanych w tych usług w przyszłości.

## <a name="azure-portal"></a>Azure Portal

1. Zaloguj się do [portalu Azure](https://portal.azure.com) i wybierz z klastrem usługi HDInsight. Jeśli z klastrem usługi HDInsight nie jest przypięty do pulpitu nawigacyjnego, możesz wyszukać jego według nazwy, korzystając z pola wyszukiwania.
   
    ![wyszukiwania portalu](./media/hdinsight-delete-cluster/navbar.png)

2. Wybierz z ustawień klastra **usunąć** ikony. Po wyświetleniu monitu wybierz **tak** można usunąć klastra.
   
    ![Ikona usuwania](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a>Azure PowerShell

Z wiersza polecenia programu PowerShell wpisz następujące polecenie, aby usunąć klaster:

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

Zastąp **CLUSTERNAME** nazwą klastra usługi HDInsight:

## <a name="azure-cli-10"></a>Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0

W wierszu należy użyć następującego można usunąć klastra:

    azure hdinsight cluster delete CLUSTERNAME

Zastąp **CLUSTERNAME** nazwą klastra usługi HDInsight:

> [!NOTE]
> Azure CLI 2.0 nie obsługuje usuwania klastrów usługi HDInsight w tej chwili (23 października 2017 r.).