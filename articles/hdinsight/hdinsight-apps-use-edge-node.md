---
title: "aaaUse pusty krawędzi węzły klastrów platformy Hadoop w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Jak tooadd tooan węzła krawędzi pusty HDInsight klastra, który może być używany jako klient, a następnie/hosta testów aplikacji usługi HDInsight."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: cdc7d1b4-15d7-4d4d-a13f-c7d3a694b4fb
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: 9c910905b51f2fe92e6e5d47d86a32bd5247c2cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-empty-edge-nodes-on-hadoop-clusters-in-hdinsight"></a>Użyj węzłami pusty edge na klastrów platformy Hadoop w usłudze HDInsight

Dowiedz się, jak tooadd pustą krawędzi klastra usługi HDInsight tooan węzła. Węzeł krawędzi pusty jest maszyny wirtualnej systemu Linux hello tych samych narzędzi klienta zainstalowany i skonfigurowany tak jak hello headnodes, ale żadne uruchomione usługi Hadoop. Za pomocą węzła krawędzi hello dla uzyskiwania dostępu do klastra hello, testowanie aplikacji klienckich i hosting aplikacji klienta. 

Podczas tworzenia klastra hello można dodać krawędzi pustego węzła tooan istniejącym klastrze usługi HDInsight, tooa nowego klastra. Dodawanie węzła krawędzi pusty jest wykonywane przy użyciu szablonu usługi Azure Resource Manager.  Witaj poniższy przykład pokazuje, jak jest wykonywane przy użyciu szablonu:

    "resources": [
        {
            "name": "[concat(parameters('clusterName'),'/', variables('applicationName'))]",
            "type": "Microsoft.HDInsight/clusters/applications",
            "apiVersion": "2015-03-01-preview",
            "dependsOn": [ "[concat('Microsoft.HDInsight/clusters/',parameters('clusterName'))]" ],
            "properties": {
                "marketPlaceIdentifier": "EmptyNode",
                "computeProfile": {
                    "roles": [{
                        "name": "edgenode",
                        "targetInstanceCount": 1,
                        "hardwareProfile": {
                            "vmSize": "Standard_D3"
                        }
                    }]
                },
                "installScriptActions": [{
                    "name": "[concat('emptynode','-' ,uniquestring(variables('applicationName')))]",
                    "uri": "[parameters('installScriptAction')]",
                    "roles": ["edgenode"]
                }],
                "uninstallScriptActions": [],
                "httpsEndpoints": [],
                "applicationType": "CustomApplication"
            }
        }
    ],

Jak pokazano w przykładzie hello, opcjonalnie można wywołać [akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md) tooperform dodatkowej konfiguracji, takich jak instalowanie [Apache Hue](hdinsight-hadoop-hue-linux.md) w hello węzła krawędzi. Witaj skryptu akcji skryptu musi być dostępny publicznie w sieci web hello.  Na przykład jeśli skrypt hello jest przechowywany w magazynie Azure, użyj publiczne kontenery lub publiczne obiekty BLOB.

rozmiar maszyny wirtualnej węzła krawędzi Hello musi spełniać wymagania rozmiar maszyny wirtualnej węzła procesu roboczego hello HDInsight klastra. Dla hello zalecane procesu roboczego węzła rozmiarów maszyn wirtualnych, zobacz [klastrów utworzyć Hadoop w HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).

Po utworzeniu węzeł krawędzi, można połączyć z węzłem krawędzi toohello przy użyciu protokołu SSH, a klientem klastra usługi Hadoop hello tooaccess narzędzia w usłudze HDInsight.

> [!WARNING] 
> Przy użyciu węzła krawędzi pusta w usłudze HDInsight jest obecnie w wersji zapoznawczej. Niestandardowe składniki, które są zainstalowane w węźle krawędzi hello otrzymywania uzasadnione ekonomicznie pomocy technicznej firmy Microsoft. Może to spowodować w rozwiązywaniu problemów występujących u użytkownika. Lub może być toocommunity określonego zasobów, aby uzyskać dalszą pomoc. Witaj poniżej przedstawiono niektóre hello w większości witryn aktywny uzyskiwania pomocy od społeczności hello:
>
> * [Forum MSDN dla usługi HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)
> * [http://StackOverflow.com](http://stackoverflow.com).
>
> Jeśli korzystasz z technologii Apache, może być możliwe toofind pomoc za pośrednictwem hello Apache witryny projektu na [http://apache.org](http://apache.org), takich jak hello [Hadoop](http://hadoop.apache.org/) lokacji.

## <a name="add-an-edge-node-tooan-existing-cluster"></a>Dodaj istniejącego klastra tooan węzła krawędzi
W tej sekcji służy tooadd szablonu usługi Resource Manager krawędzi węzła tooan istniejącego klastra usługi HDInsight.  Witaj szablonu usługi Resource Manager można znaleźć w [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/). Szablon usługi Resource Manager Hello wywołuje znajdujący się w https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh akcji skryptu. skrypt Hello nie wykonywać żadnych akcji.  Jest toodemonstrate wywoływania akcji skryptu z szablonem usługi Resource Manager.

**tooadd krawędzi pustego węzła tooan istniejącego klastra**

1. Tworzenie klastra usługi HDInsight, jeśli nie masz jeszcze.  Zobacz [samouczek Hadoop: rozpoczynanie pracy z platformą Hadoop w usłudze HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).
2. Kliknij przycisk hello toosign obrazu w tooAzure i hello Otwórz szablon usługi Azure Resource Manager w hello portalu Azure. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-add-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. Skonfiguruj hello następujące właściwości:
   
   * **Subskrypcja**: Wybierz subskrypcję platformy Azure używana do tworzenia klastra hello.
   * **Grupa zasobów**: grupy zasobów wybierz hello hello istniejącego klastra usługi HDInsight.
   * **Lokalizacja**: Wybierz lokalizację hello hello istniejącym klastrze usługi HDInsight.
   * **Nazwa klastra**: Wprowadź nazwę hello istniejącego klastra usługi HDInsight.
   * **Rozmiar węzła krawędzi**: Wybierz jedno z hello rozmiarów maszyn wirtualnych. rozmiar maszyny wirtualnej Hello musi spełniać wymagania dotyczące rozmiaru maszyny wirtualnej węzła procesu roboczego hello. Dla hello zalecane procesu roboczego węzła rozmiarów maszyn wirtualnych, zobacz [klastrów utworzyć Hadoop w HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).
   * **Krawędzi prefiksu węzła**: hello wartość domyślna to **nowe**.  Przy użyciu wartości domyślnej hello, jest nazwa węzła krawędzi hello **nowe edgenode**.  Prefiks hello hello portalu można dostosować. Można również dostosować hello imię i nazwisko z hello szablonu.

4. Sprawdź **zgadzam się toohello warunki i postanowienia, o których wspomniano**, a następnie kliknij przycisk **zakupu** węzła krawędzi hello toocreate.

>[!IMPORTANT]
> Upewnij się, że grupa zasobów Azure hello tooselect dla hello istniejącym klastrze usługi HDInsight.  W przeciwnym razie błąd hello komunikat "nie można wykonać żądanej operacji dla zasobu zagnieżdżonego. Zasobu nadrzędnego "&lt;ClusterName >' nie znaleziono."

## <a name="add-an-edge-node-when-creating-a-cluster"></a>Dodaj węzeł krawędzi, podczas tworzenia klastra
W tej sekcji użyjesz klastra usługi HDInsight toocreate szablonu usługi Resource Manager z węzłem krawędzi.  Witaj szablonu usługi Resource Manager można znaleźć w hello [galerię szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/). Szablon usługi Resource Manager Hello wywołuje znajdujący się w https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh akcji skryptu. skrypt Hello nie wykonywać żadnych akcji.  Jest toodemonstrate wywoływania akcji skryptu z szablonem usługi Resource Manager.

**tooadd krawędzi pustego węzła tooan istniejącego klastra**

1. Tworzenie klastra usługi HDInsight, jeśli nie masz jeszcze.  Zobacz [rozpocząć korzystanie z platformy Hadoop w usłudze HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).
2. Kliknij przycisk hello toosign obrazu w tooAzure i hello Otwórz szablon usługi Azure Resource Manager w hello portalu Azure. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. Skonfiguruj hello następujące właściwości:
   
   * **Subskrypcja**: Wybierz subskrypcję platformy Azure używana do tworzenia klastra hello.
   * **Grupa zasobów**: Utwórz nową grupę zasobów klastra hello.
   * **Lokalizacja**: Wybierz lokalizację dla grupy zasobów hello.
   * **Nazwa klastra**: Wprowadź nazwę dla nowego toocreate klastra hello.
   * **Nazwa użytkownika logowania klastra**: Wprowadź nazwę użytkownika Hadoop HTTP hello.  Nazwa domyślnej Hello jest **admin**.
   * **Hasło logowania klastra**: Wprowadź hasło użytkownika hello HTTP platformy Hadoop.
   * **SSH nazwy użytkownika**: Wprowadź nazwę użytkownika SSH hello. Nazwa domyślnej Hello jest **sshuser**.
   * **SSH hasła**: Wprowadź hasło użytkownika SSH hello.
   * **Zainstaluj akcji skryptu**: zachować wartość domyślną hello pośrednictwa w tym samouczku.
     
     Niektóre właściwości zostały zapisane na stałe w szablonie hello: typ klastra, liczba węzłów procesu roboczego klastra rozmiaru węzła krawędzi i nazwa węzła krawędzi.
4. Sprawdź **zgadzam się toohello warunki i postanowienia, o których wspomniano**, a następnie kliknij przycisk **zakupu** toocreate hello klastra z węzłem krawędzi hello.

## <a name="access-an-edge-node"></a>Dostęp do węzła krawędzi
węzeł brzegowy Hello ssh punkt końcowy jest &lt;EdgeNodeName >.&lt; ClusterName >-ssh.azurehdinsight.net:22.  Na przykład nowy edgenode.myedgenode0914-ssh.azurehdinsight.net:22.

węzeł krawędzi Hello jest wyświetlany jako aplikacja na powitania portalu Azure.  zapewnia portalu Hello hello hello tooaccess informacji krawędzi węzła przy użyciu protokołu SSH.

**punkt końcowy SSH węzła tooverify hello krawędzi**

1. Zaloguj się na toohello [portalu Azure](https://portal.azure.com).
2. Otwórz klaster usługi HDInsight hello z węzłem krawędzi.
3. Kliknij przycisk **aplikacji** z hello bloku klastra. Zostanie wyświetlona hello węzła krawędzi.  Nazwa domyślnej Hello jest **nowe edgenode**.
4. Kliknij węzeł krawędzi hello. Punkt końcowy SSH hello jest wyświetlona.

**w węźle krawędzi hello gałąź rejestru toouse**

1. Za pomocą węzła krawędzi toohello tooconnect SSH. Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Po podłączeniu węzła krawędzi toohello przy użyciu protokołu SSH, należy użyć hello następujące polecenia tooopen hello Hive konsoli:
   
        hive
3. Uruchom następujące polecenie tooshow tabele programu Hive w klastrze hello hello:
   
        show tables;

## <a name="delete-an-edge-node"></a>Usuń węzeł krawędzi
Możesz usunąć węzeł krawędzi, z hello portalu Azure.

**tooaccess węzła krawędzi**

1. Zaloguj się na toohello [portalu Azure](https://portal.azure.com).
2. Otwórz klaster usługi HDInsight hello z węzłem krawędzi.
3. Kliknij przycisk **aplikacji** z hello bloku klastra. Zostanie wyświetlona lista węzłów krawędzi.  
4. Kliknij prawym przyciskiem myszy węzeł brzegowy hello toodelete, a następnie kliknij przycisk **usunąć**.
5. Kliknij przycisk **tak** tooconfirm.

## <a name="next-steps"></a>Następne kroki
W tym artykule wiesz już, jak tooadd węzła krawędzi i jak tooaccess hello węzła krawędzi. toolearn więcej, zobacz następujące artykuły hello:

* [Instalowanie aplikacji usługi HDInsight](hdinsight-apps-install-applications.md): Dowiedz się, jak klastrów tooinstall tooyour aplikacji usługi HDInsight.
* [Instalowanie niestandardowych aplikacji usługi HDInsight](hdinsight-apps-install-custom-applications.md): Dowiedz się, jak toodeploy nieopublikowane tooHDInsight aplikacji usługi HDInsight.
* [Publikowanie aplikacji usługi HDInsight](hdinsight-apps-publish-applications.md): Dowiedz się, jak toopublish z niestandardowych aplikacji usługi HDInsight tooAzure Marketplace.
* [MSDN: Instalowanie aplikacji usługi HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): Dowiedz się, jak toodefine aplikacji usługi HDInsight.
* [Dostosowywanie klastrów usługi HDInsight opartej na systemie Linux przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md): Dowiedz się, jak toouse akcji skryptu tooinstall dodatkowe aplikacje.
* [Tworzenie klastrów opartych na systemie Linux platformą Hadoop w usłudze HDInsight przy użyciu szablonów usługi Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Dowiedz się, jak toocreate szablony Menedżera zasobów toocall HDInsight clusters.

