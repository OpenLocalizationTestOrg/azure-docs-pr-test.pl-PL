---
title: "aaaInstall aplikacji Hadoop innych firm w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooinstall aplikacji Hadoop innych firm w usłudze Azure HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: eaf5904d-41e2-4a5f-8bec-9dde069039c2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/16/2017
ms.author: jgao
ms.openlocfilehash: 00071517c81a17c01dccedf9e8dd5d0cabb38567
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-third-party-hadoop-applications-on-azure-hdinsight"></a>Instalowanie aplikacji platformy Hadoop innych firm w usłudze Azure HDInsight

W tym artykule dowiesz się, jak tooinstall już opublikowanej aplikacji Hadoop innych firm w usłudze Azure HDInsight. Aby uzyskać instrukcje instalowania własnej aplikacji, zobacz [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md) (Instalowanie niestandardowych aplikacji usługi HDInsight).

Aplikacja usługi HDInsight to aplikacja, którą użytkownicy mogą zainstalować w klastrze usługi HDInsight opartym na systemie Linux. Te aplikacje mogą być opracowane przez firmę Microsoft, niezależnych dostawców oprogramowania (ISV) lub samodzielnie.  

Obecnie dostępne są cztery opublikowane aplikacje:

* **DDS DATAIKU w usłudze HDInsight**: Dataiku DSS (Studio nauki danych) jest oprogramowanie, które umożliwia danych tooprototype specjalistów (analityków danych, analitycy biznesowi, deweloperzy...), tworzenie i wdrażanie wysokiej określonych usług, które przetwarzają dane pierwotne w operacje przewidywania dla firm istotna.
* **Datameer**: [Datameer](http://www.datameer.com/documentation/display/DAS50/Home?ls=Partners&lsd=Microsoft&c=Partners&cd=Microsoft) oferuje analitykom toodiscover interakcyjne sposób analizowania i wizualizacja wyników hello danych Big Data. Ściąganie dodatkowych źródeł danych łatwo toodiscover nowe relacje i odpowiedzi hello szybko potrzebne.
* **Moduł zbierający dane Streamsets dla HDnsight** udostępnia kompletne zintegrowane środowisko programistyczne (IDE) umożliwia projektowanie, testowanie, wdrażania i zarządzania dowolny z każdym pozyskiwania potoki, które siatki danych strumienia i partii i zawierać wiele różnych w strumieniu przekształcenia — wszystkie bez toowrite niestandardowego kodu. 
* **Pojemnika transportowego CDAP dla usługi HDInsight** zapewnia hello najpierw ujednolicona platforma integracji dla danych big data, która ogranicza hello tooproduction czasu dla danych aplikacji i danych jeziora o 80%. Ta aplikacja obsługuje tylko standardowe klastry bazy danych HBase 3.4.
* **Analiza sztucznego H2O dla usługi HDInsight (Beta)** H2O musujących wody obsługuje następujące algorytmy rozproszonego hello: GLM, prostym algorytmie Bayesa, lasu losowe rozproszone, gradientu zwiększania maszyny, głębokie sieci neuronowe, bezpośrednich uczenia K-średnich, PCA, Uogólniony niski rangi modeli, wykrywanie anomalii i Autoencoders.
* **Platforma do analiz Kyligence** Kyligence Analytics Platform (KAP) to magazyn danych gotowe enterprise, obsługiwane przez Apache Kylin i Apache Hadoop; upoważnia opóźnienia zapytania podrzędne sekundę na ogromną skalę zestawu danych i upraszcza analiza danych Użytkownicy biznesowi i analityków. 
* **SnapLogic Hadooplex** hello SnapLogic Hadooplex systemem w usłudze HDInsight umożliwia szybsze insights toobusiness tooget klientów przez podanie wprowadzanie danych samoobsługi i przygotowanie z niemal dowolnego źródła toohello chmury Microsoft Azure Platforma.
* **Serwer zadań Spark dla modułu wykonującego Spark KNIME** serwer zadań Spark dla modułu wykonującego Spark KNIME jest używane tooconnect hello KNIME Analytics Platform tooHDInsight klastrów.

Witaj instrukcje podane w tym artykule, użyj portalu Azure. Możesz również Eksportowanie szablonu usługi Azure Resource Manager hello z portalu hello lub uzyskać kopię szablonu usługi Resource Manager powitania od dostawców i użyć programu Azure PowerShell i interfejsu wiersza polecenia Azure toodeploy hello szablonu.  Zobacz [Create Linux-based Hadoop clusters in HDInsight using Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md) (Tworzenie klastrów Hadoop w usłudze HDInsight opartych na systemie Linux przy użyciu szablonów usługi Resource Manager).

## <a name="prerequisites"></a>Wymagania wstępne
Jeśli chcesz tooinstall aplikacji usługi HDInsight w istniejącym klastrze usługi HDInsight, musi mieć klastra usługi HDInsight. Zobacz toocreate, [Tworzenie klastrów](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). Możesz także zainstalować aplikacje usługi HDInsight podczas tworzenia klastra usługi HDInsight.

## <a name="install-applications-tooexisting-clusters"></a>Zainstaluj aplikacje tooexisting klastrów
Witaj poniższej procedurze wyjaśniono, jak tooinstall HDInsight aplikacji tooan istniejącym klastrze usługi HDInsight.

**tooinstall aplikacji usługi HDInsight**

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Kliknij przycisk **klastrów usługi HDInsight** w menu po lewej stronie powitania.  Jeśli jej nie widzisz, kliknij pozycję **Więcej usług**, a następnie kliknij pozycję **Klastry usługi HDInsight**.
3. Kliknij klaster usługi HDInsight.  Jeśli nie masz klastra, musisz go najpierw utworzyć.  Zobacz [Tworzenie klastrów](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).
4. Kliknij przycisk **aplikacji** w obszarze hello **konfiguracje** kategorii. Można wyświetlić listę zainstalowanych aplikacji. Jeśli nie możesz znaleźć aplikacji, oznacza to, że istnieje żadne aplikacje dla tej wersji hello klastra usługi HDInsight.
   
    ![Aplikacje usługi HDInsight — menu portalu](./media/hdinsight-apps-install-applications/hdinsight-apps-portal-menu.png)
5. Kliknij przycisk **Dodaj** hello bloku menu. 
   
    ![Aplikacje usługi HDInsight — zainstalowane aplikacje](./media/hdinsight-apps-install-applications/hdinsight-apps-installed-apps.png)
   
    Zostanie wyświetlona lista istniejących aplikacji usługi HDInsight.
   
    ![Aplikacje usługi HDInsight — dostępne aplikacje](./media/hdinsight-apps-install-applications/hdinsight-apps-list.png)
6. Kliknij jedną z aplikacji hello zaakceptuj postanowienia prawne hello, a następnie kliknij przycisk **wybierz**.

Widać hello stanu instalacji z portalu powiadomienia hello (kliknij ikonę dzwonka hello na górze hello hello portalu). Po hello aplikacja jest zainstalowana, aplikacja hello pojawią się na powitania bloku zainstalowane aplikacje.

## <a name="install-applications-during-cluster-creation"></a>Instalowanie aplikacji podczas tworzenia klastra
Masz aplikacje usługi HDInsight tooinstall opcji hello podczas tworzenia klastra. W trakcie hello aplikacji usługi HDInsight są zainstalowane po utworzeniu klastra hello i znajduje się w hello stanu działania. Witaj poniższej procedurze wyjaśniono, jak aplikacje usługi HDInsight tooinstall podczas tworzenia klastra.

**tooinstall aplikacji usługi HDInsight**

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Kliknij przycisk **NOWY**, kliknij pozycję **Dane i analiza**, a następnie kliknij pozycję **HDInsight**.
3. Wprowadź wartość w polu **Nazwa klastra**: ta nazwa musi być globalnie unikatowa.
4. Kliknij przycisk **subskrypcji** tooselect hello subskrypcji Azure, która jest używana dla hello klastra.
5. Kliknij pozycję **Wybierz typ klastra**, a następnie wybierz następujące opcje:
   
   * **Typ klastra**: Jeśli nie wiesz, jakie toochoose, wybierz **Hadoop**. Jest hello najpopularniejszych typ klastra.
   * **System operacyjny**: wybierz pozycję **Linux**.
   * **Wersja**: Użyj hello domyślnej wersji, jeśli nie wiesz, jakie toochoose. Więcej informacji można znaleźć w temacie [HDInsight cluster versions](hdinsight-component-versioning.md) (Wersje klastrów usługi HDInsight).
   * **Klaster warstwy**: Azure HDInsight zapewnia oferty chmury danych big data hello w dwóch różnych kategoriach: warstwy standardowa i Premium warstwy. Więcej informacji można znaleźć w temacie [Cluster tiers](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers) (Warstwy klastrów).
6. Kliknij przycisk **aplikacji**, kliknij jeden z hello opublikowane aplikacje, a następnie kliknij **wybierz**.
7. Kliknij przycisk **poświadczenia** , a następnie wprowadź hasło dla użytkownika administracyjnego hello. Należy również tooenter **nazwa użytkownika SSH** i **hasło** lub **klucz PUBLICZNY**, które jest używane tooauthenticate hello SSH użytkownika. Za pomocą klucza publicznego jest hello zalecane podejście. Kliknij przycisk **wybierz** na powitania dolnej toosave hello poświadczenia konfiguracji.
8. Kliknij przycisk **źródła danych**, wybierz jedną z istniejących kont magazynu hello lub tworzenia nowych toobe konto magazynu używane jako domyślne konto magazynu hello hello klastra.
9. Kliknij przycisk **grupy zasobów** tooselect istniejący zasób grupy, lub kliknij przycisk **nowy** toocreate nową grupę zasobów
10. Na powitania **nowego klastra usługi HDInsight** bloku, upewnij się, że **tooStartboard numeru Pin** jest zaznaczone, a następnie kliknij przycisk **Utwórz**. 

## <a name="list-installed-hdinsight-apps-and-properties"></a>Lista zainstalowanych aplikacji HDInsight i ich właściwości
Hello portal pokazuje listę hello zainstalowanych aplikacji usługi HDInsight w klastrze i hello właściwości każdej zainstalowanej aplikacji.

**właściwości aplikacji i wyświetlanie HDInsight toolist**

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Kliknij przycisk **klastrów usługi HDInsight** w menu po lewej stronie powitania.  Jeśli jej nie widzisz, kliknij przycisk **Przeglądaj**, a następnie kliknij pozycję **Klastry usługi HDInsight**.
3. Kliknij klaster usługi HDInsight.
4. Z hello **ustawienia** bloku, kliknij przycisk **aplikacji** w obszarze hello **ogólne** kategorii. Blok aplikacje zainstalowane Hello Wyświetla listę wszystkich aplikacji hello zainstalowane. 
   
    ![Aplikacje usługi HDInsight — zainstalowane aplikacje](./media/hdinsight-apps-install-applications/hdinsight-apps-installed-apps-with-apps.png)
5. Kliknij jedną z właściwości hello tooshow aplikacji hello zainstalowane. Witaj list bloku właściwości:
   
   * Nazwa aplikacji: nazwa aplikacji.
   * Stan: stan aplikacji. 
   * Strony sieci Web: hello adres URL aplikacji sieci web hello wdrożono toohello węzła krawędzi. poświadczenie Hello jest taki sam, jak poświadczenia użytkownika hello HTTP, które zostały skonfigurowane dla klastra hello powitalne.
   * Punkt końcowy HTTP: hello poświadczenie jest taki sam, jak poświadczenia użytkownika hello HTTP, które zostały skonfigurowane dla klastra hello hello. 
   * Punkt końcowy SSH: korzystając z węzłem krawędzi toohello tooconnect SSH. poświadczenia SSH Hello są tak samo jak użytkownika SSH hello poświadczenia zostały skonfigurowane dla klastra hello powitalne. Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
6. toodelete aplikacji, kliknij prawym przyciskiem myszy aplikacji hello, a następnie kliknij przycisk **usunąć** z menu kontekstowego hello.

## <a name="connect-toohello-edge-node"></a>Połączenie z węzłem krawędzi toohello
Można połączyć z węzłem krawędzi toohello przy użyciu protokołu HTTP i SSH. informacje o punkcie końcowym Hello można znaleźć z hello [portal](#list-installed-hdinsight-apps-and-properties). Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

poświadczenia punktu końcowego HTTP Hello są poświadczenia użytkownika HTTP hello skonfigurowane do obsługi klastra usługi HDInsight hello; Witaj SSH punktu końcowego poświadczenia są poświadczenia SSH hello, które zostały skonfigurowane dla klastra usługi HDInsight hello.

## <a name="troubleshoot"></a>Rozwiązywanie problemów
Zobacz [rozwiązywania problemów z instalacją hello](hdinsight-apps-install-custom-applications.md#troubleshoot-the-installation).

## <a name="next-steps"></a>Następne kroki
* [Instalowanie niestandardowych aplikacji usługi HDInsight](hdinsight-apps-install-custom-applications.md): Dowiedz się, jak toodeploy nieopublikowane tooHDInsight aplikacji usługi HDInsight.
* [Publikowanie aplikacji usługi HDInsight](hdinsight-apps-publish-applications.md): Dowiedz się, jak toopublish z niestandardowych aplikacji usługi HDInsight tooAzure Marketplace.
* [MSDN: Instalowanie aplikacji usługi HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): Dowiedz się, jak toodefine aplikacji usługi HDInsight.
* [Dostosowywanie klastrów usługi HDInsight opartej na systemie Linux przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md): Dowiedz się, jak toouse akcji skryptu tooinstall dodatkowe aplikacje.
* [Tworzenie klastrów opartych na systemie Linux platformą Hadoop w usłudze HDInsight przy użyciu szablonów usługi Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Dowiedz się, jak toocreate szablony Menedżera zasobów toocall HDInsight clusters.
* [Użyj węzłami pusty krawędzi w usłudze HDInsight](hdinsight-apps-use-edge-node.md): Dowiedz się, jak toouse pustą krawędzi węzła w celu uzyskiwania dostępu do klastra usługi HDInsight, testowanie aplikacji usługi HDInsight i hosting aplikacji usługi HDInsight.

