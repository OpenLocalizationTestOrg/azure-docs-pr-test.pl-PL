---
title: "toodelete aaaHow klastra usługi HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Informacje na temat hello różne sposoby, że możesz usunąć klaster usługi HDInsight."
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
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 5b9d9a09eecfdcfaed7a1f5ebab440e13bd358b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-hello-azure-cli"></a>Usuwanie klastra usługi HDInsight przy użyciu przeglądarki, programu PowerShell lub interfejsu wiersza polecenia Azure hello

Karta klastra usługi HDInsight zaczyna się po klastra jest tworzony i zatrzymywana, gdy klaster hello jest usunięty. Są naliczane proporcjonalnie za minutę, więc zawsze należy usunąć klaster, gdy nie jest już używana. W tym dokumencie możesz dowiedzieć się, jak toodelete klastra przy użyciu hello portalu Azure, programu Azure PowerShell i hello Azure CLI w wersji 1.0.

> [!IMPORTANT]
> Usunięcie klastra usługi HDInsight nie powoduje usunięcia konta usługi Azure Storage hello lub Data Lake Store jest skojarzone z hello klastra. Można ponownie użyć danych przechowywanych w tych usług w przyszłości hello.

## <a name="azure-portal"></a>Azure Portal

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com) i wybierz z klastrem usługi HDInsight. Jeśli z klastrem usługi HDInsight nie jest przypięty toohello pulpitu nawigacyjnego, możesz wyszukać jego wg nazwy przy użyciu pola wyszukiwania hello.
   
    ![wyszukiwania portalu](./media/hdinsight-delete-cluster/navbar.png)

2. Gdy zostanie otwarty blok hello hello klastra, wybierz hello **usunąć** ikony. Po wyświetleniu monitu wybierz **tak** toodelete hello klastra.
   
    ![Ikona usuwania](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a>Azure PowerShell

Z wiersza polecenia programu PowerShell Użyj hello następujące polecenie toodelete hello klastra:

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

Zastąp **CLUSTERNAME** o nazwie hello klastra usługi HDInsight.

## <a name="azure-cli-10"></a>Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0

W wierszu Użyj powitania po toodelete hello klastra:

    azure hdinsight cluster delete CLUSTERNAME

Zastąp **CLUSTERNAME** o nazwie hello klastra usługi HDInsight.

> [!NOTE]
> Azure CLI 2.0 nie obsługuje usuwania klastrów usługi HDInsight w tej chwili (31 lipca 2017 r.).