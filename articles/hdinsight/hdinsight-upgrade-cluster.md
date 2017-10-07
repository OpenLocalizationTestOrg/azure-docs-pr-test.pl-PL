---
title: "wersja nowsza tooa klastra usługi HDInsight aaaUpgrade-Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooUpgrade HDInsight cluster tooa nowszej wersji."
services: hdinsight
documentationcenter: 
author: bhanupr
manager: asadk
editor: bhanupr
ms.assetid: 60eb573c-e639-4815-9fc6-ea8b106d8dbc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: bhanupr
ms.openlocfilehash: 5fff3c9bc88dfbcbc1ccb0188accdfbbec3a62f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hdinsight-cluster-tooa-newer-version"></a>Uaktualnij tooa klastra usługi HDInsight w nowszej wersji
Zaletą tootake hello najnowszych funkcji usługi HDInsight, zaleca się klastrów usługi HDInsight toolatest uaktualnionej wersji. Wykonaj hello poniżej tooupgrade wskazówki dotyczące Twojej wersji klastra usługi HDInsight.

> [!NOTE]
> Klastry usługi HDInsight w wersji 3.2 lub 3.3 zbliża się Data wycofania. Aby uzyskać informacji na temat obsługiwanych wersji usługi hdinsight, zobacz [wersji składnika usługi HDInsight](hdinsight-component-versioning.md#supported-hdinsight-versions).
>
>

## <a name="upgrade-tasks"></a>Zadania uaktualniania
Witaj przepływu pracy tooupgrade klastra usługi HDInsight ma następującą składnię.

![Diagram przepływu pracy uaktualniania](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. Przeczytaj sekcję tego dokumentu toounderstand zmiany, które mogą być wymagane w przypadku uaktualniania z klastrem usługi HDInsight.
2. Tworzenie klastra jako środowiska gwarancji testu/jakości. Aby uzyskać więcej informacji na temat tworzenia klastra, zobacz [Dowiedz się, jak toocreate opartych na systemie Linux klastrów usługi HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
3. Kopia istniejącego zadania, źródła danych i wychwytywanie toohello nowego środowiska. Zobacz [tooTest skopiować dane środowisko](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) więcej szczegółów.
4. Sprawdzania poprawności testowania toomake się upewnić, że zadaniach działać zgodnie z oczekiwaniami w nowym klastrze hello.


Po upewnieniu się, że wszystko działa zgodnie z oczekiwaniami, należy zaplanować przestój hello migracji. Podczas tego przestoju hello następujących czynności:

1.  Utwórz kopię zapasową przejściowej dane przechowywane lokalnie na hello węzłów klastra. Jeśli na przykład dane przechowywane bezpośrednio na węzła głównego.
2.  Usuń hello istniejącego klastra.
3.  Tworzenie klastra w hello hello tej samej sieci Wirtualnej podsieci o najnowszych (lub obsługiwanych) HDI wersji przy użyciu tego samego magazynu danych domyślne hello poprzedniego klastra używane. Dzięki temu hello nowego klastra toocontinue rywalizacja istniejących danych produkcyjnych.
4.  Importuj wszystkie przejściowej dane kopii zapasowej.
5.  Uruchom zadania/Kontynuuj przetwarzania przy użyciu hello nowego klastra.

## <a name="next-steps"></a>Następne kroki
* [Dowiedz się, jak toocreate opartych na systemie Linux klastrów usługi HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Połącz tooHDInsight przy użyciu protokołu SSH](hdinsight-hadoop-linux-use-ssh-unix.md)
* [Zarządzanie klastrem opartych na systemie Linux przy użyciu narzędzia Ambari](hdinsight-hadoop-manage-ambari.md)

