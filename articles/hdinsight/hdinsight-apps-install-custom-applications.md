---
title: "aaaInstall własne niestandardowe aplikacje platformy Hadoop w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak aplikacje usługi HDInsight tooinstall na aplikacje usługi HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e556b29c-8176-4bc5-a90b-aa01abfd3aee
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ed3148f2c4d4d2b568d84e44fa6d76bb5a001902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-custom-hadoop-applications-on-azure-hdinsight"></a>Instalowanie niestandardowych aplikacji platformy Hadoop w usłudze Azure HDInsight

W tym artykule dowiesz się, jak tooinstall aplikacją platformy Hadoop w usłudze Azure HDInsight, który nie został opublikowany toohello portalu Azure. Aplikacja Hello zostanie zainstalowany w tym artykule jest [Hue](http://gethue.com/).

Aplikacja usługi HDInsight to aplikacja, którą użytkownicy mogą zainstalować w klastrze usługi HDInsight opartym na systemie Linux.  Te aplikacje mogą być opracowane przez firmę Microsoft, niezależnych dostawców oprogramowania (ISV) lub samodzielnie.  

Inne pokrewne artykuły:

* [Instalowanie aplikacji usługi HDInsight](hdinsight-apps-install-applications.md): Dowiedz się, jak klastrów tooinstall tooyour aplikacji usługi HDInsight.
* [Publikowanie aplikacji usługi HDInsight](hdinsight-apps-publish-applications.md): Dowiedz się, jak toopublish z niestandardowych aplikacji usługi HDInsight tooAzure Marketplace.
* [MSDN: Instalowanie aplikacji usługi HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): Dowiedz się, jak toodefine aplikacji usługi HDInsight.

## <a name="prerequisites"></a>Wymagania wstępne
Jeśli chcesz tooinstall aplikacji usługi HDInsight w istniejącym klastrze usługi HDInsight, musi mieć klastra usługi HDInsight. Zobacz toocreate, [Tworzenie klastrów](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). Możesz także zainstalować aplikacje usługi HDInsight podczas tworzenia klastra usługi HDInsight.

## <a name="install-hdinsight-applications"></a>Instalowanie aplikacji usługi HDInsight
Podczas tworzenia klastra lub tooan istniejącym klastrze usługi HDInsight można zainstalować aplikacje usługi HDInsight. Definiowanie szablonów usługi Azure Resource Manager opisano w temacie [MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx) (MSDN: instalowanie aplikacji usługi HDInsight).

Witaj pliki potrzebne do wdrożenia tej aplikacji (Hue):

* [azuredeploy.JSON](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/azuredeploy.json): hello szablonu usługi Resource Manager do instalowania aplikacji usługi HDInsight. Aby utworzyć własny szablon usługi Resource Manager, zobacz [MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx) (MSDN: instalowanie aplikacji usługi HDInsight).
* [HUE-install_v0.sh](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/scripts/Hue-install_v0.sh): hello Akcja skryptu wywoływana przez szablon usługi Resource Manager hello konfigurowania hello węzła krawędzi.
* [HUE-binaries.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz): plik binarny aplikacji hue hello wywoływany ze skryptu hui-install_v0.sh.
* [HUE-plików binarnych-14-04.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz): plik binarny aplikacji hue hello wywoływany ze skryptu hui-install_v0.sh.
* [webwasb-tomcat.tar.gz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/webwasb-tomcat.tar.gz): przykładowa aplikacja sieci Web (Tomcat) wywoływana ze skryptu hui-install_v0.sh.

**tooinstall Hue tooan istniejącym klastrze usługi HDInsight**

1. Kliknij przycisk hello toosign obrazu w tooAzure i otwórz hello szablonu usługi Resource Manager w hello portalu Azure.

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2FIaas-Applications%2Fmaster%2FHue%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-install-custom-applications/deploy-to-azure.png" alt="Deploy tooAzure"></a>

    Ten przycisk otwiera szablon Menedżera zasobów na powitania portalu Azure.  Witaj szablonu usługi Resource Manager znajduje się pod adresem [https://github.com/hdinsight/Iaas-Applications/tree/master/Hue](https://github.com/hdinsight/Iaas-Applications/tree/master/Hue).  toolearn jak toowrite tego szablonu usługi Resource Manager, zobacz [MSDN: Instalowanie aplikacji usługi HDInsight](https://msdn.microsoft.com/library/mt706515.aspx).
2. Z hello **parametry** bloku, wprowadź następujące hello:

   * **ClusterName**: Wprowadź nazwę hello hello klastra, w której mają tooinstall hello aplikacji. Musi to być istniejący klaster.
3. Kliknij przycisk **OK** toosave hello parametrów.
4. Z hello **wdrożenie niestandardowe** bloku, wprowadź **grupy zasobów**.  Witaj grupa zasobów jest kontenerem, który grupuje klaster hello, hello zależne konto magazynu i inne zasoby. Jest to wymagane toouse hello tej samej grupie zasobów co hello klastra.
5. Kliknij opcję **Postanowienia prawne**, a następnie kliknij przycisk **Utwórz**.
6. Sprawdź hello **toodashboard numeru Pin** pole wyboru jest zaznaczone, a następnie kliknij przycisk **Utwórz**. Możesz zobaczyć stan instalacji hello z pulpitu nawigacyjnego portalu toohello przypiętych kafelków hello i hello powiadomieniu portalu (kliknij ikonę dzwonka hello na górze hello hello portalu).  Trwa około 10 minut tooinstall hello aplikacji.

**tooinstall Hue podczas tworzenia klastra**

1. Kliknij przycisk hello toosign obrazu w tooAzure i otwórz hello szablonu usługi Resource Manager w hello portalu Azure.

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhdinsightapps%2Fcreate-linux-based-hadoop-cluster-in-hdinsight.json" target="_blank"><img src="./media/hdinsight-apps-install-custom-applications/deploy-to-azure.png" alt="Deploy tooAzure"></a>

    Ten przycisk otwiera szablon Menedżera zasobów na powitania portalu Azure.  Witaj szablonu usługi Resource Manager znajduje się pod adresem [https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json](https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json).  toolearn jak toowrite tego szablonu usługi Resource Manager, zobacz [MSDN: Instalowanie aplikacji usługi HDInsight](https://msdn.microsoft.com/library/mt706515.aspx).
2. Wykonaj hello instrukcji toocreate klaster i zainstalować aplikację Hue. Aby uzyskać więcej informacji na temat tworzenia klastrów usługi HDInsight, zobacz temat [Tworzenie opartych na systemie Linux klastrów Hadoop w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

Ponadto toohello portalu Azure umożliwia również [programu Azure PowerShell](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-powershell) i [interfejsu wiersza polecenia Azure](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-cli) toocall szablony Menedżera zasobów.

## <a name="validate-hello-installation"></a>Sprawdź poprawność instalacji hello
Istnieje możliwość sprawdzenia stanu aplikacji hello na powitania instalacji aplikacji hello toovalidate portalu Azure. Ponadto można zweryfikować wszystkie punkty końcowe HTTP zostały się zgodnie z oczekiwaniami i hello strony sieci Web, jeśli istnieje:

**portalu Hue hello tooopen**

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Kliknij przycisk **klastrów usługi HDInsight** w menu po lewej stronie powitania.  Jeśli jej nie widzisz, kliknij przycisk **Przeglądaj**, a następnie kliknij pozycję **Klastry usługi HDInsight**.
3. Kliknij klaster hello zainstalowaną aplikacji hello.
4. Z hello **ustawienia** bloku, kliknij przycisk **aplikacji** w obszarze hello **ogólne** kategorii. Powinna zostać wyświetlona **hue** na liście hello **zainstalowane aplikacje** bloku.
5. Kliknij przycisk **hue** z hello listy toolist hello właściwości.  
6. Kliknij przycisk hello strony sieci Web łącza toovalidate hello witryny sieci Web; Otwórz punkt końcowy hello HTTP w przeglądarce toovalidate hello Hue interfejsu użytkownika sieci web, punkt końcowy SSH hello otwarty przy użyciu protokołu SSH. Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="troubleshoot-hello-installation"></a>Rozwiązywania problemów z instalacją hello
Można sprawdzić stan instalacji aplikacji hello z hello powiadomieniu portalu (kliknij ikonę dzwonka hello na górze hello hello portalu).

Jeśli instalacja aplikacji nie powiodła się, można wyświetlić komunikaty o błędach hello i informacje debugowania w miejscach 3:

* Aplikacje usługi HDInsight: ogólne informacje o błędach.

    Otwórz klaster hello hello portalu, a następnie kliknij przycisk aplikacji hello bloku ustawienia:

    ![błąd instalacji aplikacji usługi hdinsight](./media/hdinsight-apps-install-applications/hdinsight-apps-error.png)
* Akcja skryptu HDInsight: Jeśli komunikat o błędzie aplikacji usługi HDInsight hello wskazuje niepowodzenie akcji skryptu, więcej informacji na temat błędu skryptu hello będą wyświetlane w okienku akcji skryptu hello.

    Kliknij akcję skryptu w bloku ustawienia hello. Historia akcji skryptu zawiera komunikaty o błędach hello

    ![błąd akcji skryptu aplikacji usługi hdinsight](./media/hdinsight-apps-install-applications/hdinsight-apps-script-action-error.png)
* Ambari Web UI: Jeśli skrypt instalacji hello hello przyczynę błędu na powitania, użyj Interfejsu sieci Web Ambari toocheck pełnych dzienników dotyczących skryptów instalacji hello.

    Aby uzyskać więcej informacji, zobacz temat [Rozwiązywanie problemów](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting).

## <a name="remove-hdinsight-applications"></a>Usuwanie aplikacji usługi HDInsight
Istnieje kilka sposobów toodelete HDInsight aplikacji.

### <a name="use-portal"></a>Korzystanie z portalu
**tooremove aplikacji przy użyciu portalu hello**

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Kliknij przycisk **klastrów usługi HDInsight** w menu po lewej stronie powitania.  Jeśli jej nie widzisz, kliknij przycisk **Przeglądaj**, a następnie kliknij pozycję **Klastry usługi HDInsight**.
3. Kliknij klaster hello zainstalowaną aplikacji hello.
4. Z hello **ustawienia** bloku, kliknij przycisk **aplikacji** w obszarze hello **ogólne** kategorii. Powinna zostać wyświetlona lista zainstalowanych aplikacji. W tym samouczku **hue** na liście hello **zainstalowane aplikacje** bloku.
5. Kliknij prawym przyciskiem myszy aplikacji hello tooremove, a następnie kliknij przycisk **usunąć**.
6. Kliknij przycisk **tak** tooconfirm.

Z hello portalu możesz usunąć klaster hello lub usunąć grupę zasobów hello, który zawiera aplikacji hello.

### <a name="use-azure-powershell"></a>Korzystanie z programu Azure PowerShell
Przy użyciu programu Azure PowerShell, możesz usunąć klaster hello lub usunąć grupę zasobów hello. Zobacz temat [Usuwanie klastrów przy użyciu programu PowerShell systemu Azure](hdinsight-administer-use-powershell.md#delete-clusters).

### <a name="use-azure-cli"></a>Interfejs wiersza polecenia platformy Azure
Przy użyciu wiersza polecenia platformy Azure, możesz usunąć klaster hello lub usunąć grupę zasobów hello. Zobacz temat [Usuwanie klastrów przy użyciu interfejsu wiersza polecenia platformy Azure](hdinsight-administer-use-command-line.md#delete-clusters).

## <a name="next-steps"></a>Następne kroki
* [MSDN: Instalowanie aplikacji usługi HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): Dowiedz się, jak toodevelop szablony Menedżera zasobów dotyczące wdrażania aplikacji usługi HDInsight.
* [Instalowanie aplikacji usługi HDInsight](hdinsight-apps-install-applications.md): Dowiedz się, jak klastrów tooinstall tooyour aplikacji usługi HDInsight.
* [Publikowanie aplikacji usługi HDInsight](hdinsight-apps-publish-applications.md): Dowiedz się, jak toopublish z niestandardowych aplikacji usługi HDInsight tooAzure Marketplace.
* [Dostosowywanie klastrów usługi HDInsight opartej na systemie Linux przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md): Dowiedz się, jak toouse akcji skryptu tooinstall dodatkowe aplikacje.
* [Tworzenie klastrów opartych na systemie Linux platformą Hadoop w usłudze HDInsight przy użyciu szablonów usługi Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Dowiedz się, jak toocreate szablony Menedżera zasobów toocall HDInsight clusters.
* [Użyj węzłami pusty krawędzi w usłudze HDInsight](hdinsight-apps-use-edge-node.md): Dowiedz się, jak toouse pustą krawędzi węzła w celu uzyskiwania dostępu do klastra usługi HDInsight, testowanie aplikacji usługi HDInsight i hosting aplikacji usługi HDInsight.
