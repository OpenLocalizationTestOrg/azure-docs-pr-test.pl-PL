---
title: aaaCustomize Hadoop clusters dla hello proces nauki danych Team | Dokumentacja firmy Microsoft
description: "Udostępniona w niestandardowych usługi Azure HDInsight Hadoop klastrów popularnych modułów środowiska Python."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0c115dca-2565-4e7a-9536-6002af5c786a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: e192542dd39f71bccbb5163382b4050d0f12ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-hello-team-data-science-process"></a>Dostosowywanie klastrów usługi Azure HDInsight Hadoop dla hello proces nauki danych Team
W tym artykule opisano sposób toocustomize HDInsight Hadoop cluster instalując Anaconda 64-bitowych (Python 2.7) na każdym węźle po zainicjowaniu obsługi klastra hello jako usługi HDInsight. Pokazuje też, jak tooaccess hello headnode toosubmit zadania niestandardowe toohello klastra. Takie dostosowanie sprawia, że wielu popularnych modułów środowiska Python, które są objęte Anaconda, łatwo dostępne dla użytkowników funkcji zdefiniowanej (UDF), które są zaprojektowane tooprocess rekordów gałęzi w klastrze hello. Aby uzyskać instrukcje dotyczące procedur hello używaną w tym scenariuszu, zobacz [jak zapytań programu Hive toosubmit](machine-learning-data-science-move-hive-tables.md#submit).

Witaj menu następujących łączy tootopics, które opisują sposób tooset się hello różnych środowiskach nauki danych przez hello [zespołu danych nauki procesu (TDSP)](data-science-process-overview.md).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <a name="customize"></a>Dostosowywanie klastra usługi Hadoop w usłudze Azure HDInsight
Uruchom toocreate dostosowane klastra usługi HDInsight Hadoop, logując się za[**klasycznego portalu Azure**](https://manage.windowsazure.com/), kliknij przycisk **nowy** w lewo hello dolnego rogu, a następnie wybierz usługi danych -> HDINSIGHT -> **Utwórz niestandardowy** toobring się hello **szczegółów klastra** okna. 

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

Wprowadź nazwę hello hello toobe klastra utworzone na stronie konfiguracji 1, a następnie zaakceptuj wartości domyślne dla hello innych pól. Kliknij przycisk hello Strzałka toogo toohello następnej konfiguracji strony. 

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

Na stronie konfiguracji 2, wprowadź numer hello **węzły danych**, wybierz pozycję hello **REGION/WIRTUALNEJ sieci**i wybierz rozmiary hello hello **HEAD, węzła** i hello **Węzeł danych**. Kliknij przycisk hello Strzałka toogo toohello następnej konfiguracji strony.

> [!NOTE]
> Witaj **REGION/WIRTUALNEJ sieci** ma toobe hello sam jako region hello hello konta magazynu, które będzie używane dla klastra usługi HDInsight Hadoop hello toobe. W przeciwnym razie w czwartej stronie konfiguracji hello hello konta magazynu nie będą wyświetlane na liście rozwijanej hello **nazwa konta**.
> 
> 

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

Na stronie konfiguracji 3 Podaj nazwę użytkownika i hasło dla hello klastra usługi HDInsight Hadoop. **Nie** wybierz hello *hello Enter potrzeby magazynu metadanych Hive/Oozie*. Następnie kliknij przycisk hello Strzałka toogo toohello następnej konfiguracji strony. 

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

Na stronie konfiguracji 4 należy określić nazwę konta magazynu hello, kontener domyślny hello hello klastra usługi HDInsight Hadoop. W przypadku wybrania *Utwórz domyślny kontener* w hello **domyślny KONTENER** listy rozwijanej, kontener z hello takie same nazwy jako hello klastra zostaną utworzone. Kliknij przycisk hello Strzałka toogo toohello ostatniej strony konfiguracji.

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

Na powitania końcowego **akcji skryptu** strony konfiguracji, kliknij przycisk **dodać akcję skryptu** przycisk i wypełnienie pól tekstowych hello hello następujące wartości.

* **Nazwa** -dowolnego ciągu jako nazwy hello tej akcji skryptu
* **Typ węzła** — wybierz tę opcję **wszystkie węzły**
* **Identyfikator URI skryptu** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1* 
  * *publicscripts* jest publicznego kontenera na koncie magazynu hello 
  * *getgoing* używamy pracy tooshare PowerShell skryptu pliki toofacilitate użytkowników na platformie Azure
* **Parametry** -(puste)

Na koniec kliknij hello znacznik wyboru toostart hello tworzenia klastra usługi HDInsight Hadoop hello dostosowane. 

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <a name="headnode"></a>Witaj dostępu Head węzeł z klastra usługi Hadoop
Należy włączyć dostępu zdalnego klastra usługi Hadoop toohello na platformie Azure, aby hello węzła głównego klastra usługi Hadoop hello są dostępne za pośrednictwem protokołu RDP. 

1. Zaloguj się za toohello [ **klasycznego portalu Azure**](https://manage.windowsazure.com/), wybierz pozycję **HDInsight** powitania po lewej stronie, wybierz klaster Hadoop z listy hello klastrów, kliknij przycisk hello  **Konfiguracja** , a następnie kliknij pozycję hello **Włącz zdalne** ikona u dołu hello hello strony.
   
    ![Tworzenie obszaru roboczego](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. W hello **Konfigurowanie pulpitu zdalnego** okna, wprowadź hello nazwy użytkownika i HASŁA pola i wybierz datę wygaśnięcia hello dostępu zdalnego. Następnie kliknij przycisk hello znacznik wyboru tooenable hello dostępu zdalnego toohello węzła głównego klastra usługi Hadoop hello.
   
    ![Tworzenie obszaru roboczego](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> Hello nazwę użytkownika i hasło dla dostępu zdalnego hello nie są hello nazwy użytkownika i hasła, który jest używany podczas tworzenia klastra usługi Hadoop hello. Jest to osobny zestaw poświadczeń. Ponadto Data wygaśnięcia hello hello dostępu zdalnego ma toobe w ciągu 7 dni od hello bieżącą datę.
> 
> 

Po włączeniu dostępu zdalnego, kliknij przycisk **CONNECT** u dołu hello hello tooremote strony do hello węzła głównego. Logowania toohello węzła głównego klastra usługi Hadoop hello wprowadzając hello poświadczeń dla użytkownika dostępu zdalnego hello, określony wcześniej.

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

Witaj kolejne kroki w hello zaawansowane analizy procesu są mapowane w hello [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) i mogą obejmować następujące kroki, które przenoszenie danych do usługi HDInsight, a następnie przetworzyć i przykładowe go w ramach przygotowania do uczenia z danych hello przy użyciu usługi Azure Machine Learning.

Zobacz [jak zapytań programu Hive toosubmit](machine-learning-data-science-move-hive-tables.md#submit) instrukcje dotyczące sposobu tooaccess hello modułów środowiska Python, które są objęte Anaconda z hello węzła głównego klastra hello w funkcji zdefiniowanej przez użytkownika (UDF), które są używane tooprocess Hive rekordów w klastrze hello.

