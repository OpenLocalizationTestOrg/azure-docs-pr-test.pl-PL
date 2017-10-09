---
title: "za pomocą akcji skryptu - Azure klastrów usługi HDInsight aaaCustomize | Dokumentacja firmy Microsoft"
description: "Dodawanie niestandardowych składników, które klastrów usługi HDInsight opartej na tooLinux za pomocą akcji skryptu. Akcje skryptu to skrypty Bash, które można konfiguracji klastra hello toocustomize używane lub dodać dodatkowych usług i narzędzi, takich jak Hue, Solr lub R."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48e85f53-87c1-474f-b767-ca772238cc13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: ff22680a8a50b21985f6941f1edaf1dcf863d13f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a>Dostosowywanie klastrów usługi HDInsight opartej na systemie Linux przy użyciu akcji skryptu

HDInsight zapewnia opcję konfiguracji o nazwie **akcji skryptu** który wywołuje niestandardowe skrypty umożliwiające dostosowanie hello klastra. Skrypty te są używane tooinstall dodatkowe składniki i zmienić ustawienia konfiguracji. Akcje skryptu można podczas lub po utworzeniu klastra.

> [!IMPORTANT]
> Akcje skryptu toouse możliwości Hello w klastrze już uruchomiona jest dostępna tylko dla klastrów usługi HDInsight opartych na systemie Linux.
>
> Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

Akcje skryptu można także toohello opublikowane w portalu Azure Marketplace jako aplikacji usługi HDInsight. Niektóre przykłady hello w tym dokumencie widoczne sposobem instalowania aplikacji usługi HDInsight przy użyciu polecenia akcji skryptu środowiska PowerShell i hello zestawu .NET SDK. Aby uzyskać więcej informacji na temat aplikacji w usłudze HDInsight, zobacz [publikować aplikacje usługi HDInsight w portalu Azure Marketplace hello](hdinsight-apps-publish-applications.md).

## <a name="permissions"></a>Uprawnienia

Jeśli korzystasz z klastra usługi HDInsight przyłączonych do domeny, istnieją dwa uprawnienia Ambari, które są wymagane w przypadku klastra hello za pomocą akcji skryptu:

* **NARZĘDZIA AMBARI. Uruchom\_niestandardowy\_polecenia**: rola administratora Ambari hello domyślnie ma to uprawnienie.
* **KLASTER. Uruchom\_niestandardowy\_polecenia**: zarówno hello administratora klastra usługi HDInsight i administratora Ambari to uprawnienie mają domyślnie.

Aby uzyskać więcej informacji na temat pracy z uprawnieniami przyłączonych do domeny usługi HDInsight, zobacz [zarządzania klastrami HDInsight przyłączonych do domeny](hdinsight-domain-joined-manage.md).

## <a name="access-control"></a>Kontrola dostępu

Jeśli nie jesteś administratorem hello/właścicieli subskrypcji platformy Azure, jego konto musi mieć co najmniej **współautora** grupę zasobów toohello dostępu, która zawiera hello klastra usługi HDInsight.

Ponadto podczas tworzenia klastra usługi HDInsight, ktoś z co najmniej **współautora** toohello dostępu do subskrypcji platformy Azure musi zostały wcześniej zarejestrowane hello dostawcy dla usługi HDInsight. Rejestracja dostawcy odbywa się po utworzeniu przez użytkownika z subskrypcją toohello dostępu współautora zasobu na powitania po raz pierwszy na powitania subskrypcji. Można to osiągnąć również bez tworzenia zasobu, [rejestrując dostawcę za pomocą interfejsu REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).

Aby uzyskać więcej informacji na temat pracy z zarządzania dostępem Zobacz hello w następujących dokumentach:

* [Wprowadzenie do zarządzania dostępem w hello portalu Azure](../active-directory/role-based-access-control-what-is.md)
* [Użyj roli przypisania toomanage dostępu tooyour subskrypcji platformy Azure zasobów](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a>Opis akcji skryptu

Akcja skryptu jest po prostu Podaj identyfikator URI do skryptu Bash i parametry. Witaj skrypt jest uruchamiany na węzłach w klastrze usługi HDInsight hello. Witaj poniżej przedstawiono cechy i funkcje akcji skryptu.

* Muszą być przechowywane na identyfikator URI, który jest dostępny z klastra usługi HDInsight hello. Lokalizacje magazynu możliwe są następujące Hello:

    * **Azure Data Lake Store** konta, który jest dostępny dla klastra usługi HDInsight hello. Aby uzyskać informacje na temat używania usługi Azure Data Lake Store z usługą HDInsight, zobacz [tworzenia klastra usługi HDInsight z usługą Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

        Podczas używania skryptu przechowywane w usłudze Data Lake Store, format identyfikatora URI hello jest `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.

        > [!NOTE]
        > Hello usługi głównej HDInsight używa tooaccess Data Lake — Magazyn musi mieć dostęp do odczytu toohello skryptu.

    * Obiekt blob w **konta magazynu Azure** to albo hello konto podstawowego lub dodatkowego magazynu dla klastra usługi HDInsight hello. HDInsight udzielono dostępu tooboth tego typu konta magazynu podczas tworzenia klastra.

    * Plik publicznego udostępniania usługi takie jak obiektów Blob platformy Azure, GitHub, usługi OneDrive, Dropbox itp.

        Na przykład identyfikatory URI, zobacz hello [przykładowe skrypty akcji skryptu](#example-script-action-scripts) sekcji.

        > [!WARNING]
        > HDInsight obsługuje tylko __ogólnego przeznaczenia__ konta usługi Azure Storage. Nie obsługuje obecnie hello __magazynu obiektów Blob__ typ konta.

* Można ograniczyć za**uruchomienia dla niektórych typów węzła**, na przykład węzłów głównych lub węzłów procesu roboczego.

  > [!NOTE]
  > W przypadku użycia z HDInsight Premium, można określić, czy skrypt hello powinien być używany w hello węzła krawędzi.

* Może być **utrwalone** lub **ad hoc**.

    **Utrwalone** skrypty są zastosowane tooworker węzłów dodanych toohello klastra po uruchomieniu skryptu hello. Na przykład podczas skalowania w górę hello klastra.

    Utrwalony skrypt może również zastosować zmiany tooanother węzła typu, na przykład węzła głównego.

  > [!IMPORTANT]
  > Akcji utrwalonego skryptu musi mieć unikatową nazwę.

    **Ad hoc** skryptów nie są zachowywane. Nie są zastosowane tooworker węzłów dodanych toohello klastra po hello skryptu ma został uruchomiony. Następnie Podwyższ poziom tooa skryptów ad hoc utrwalony skrypt lub obniżyć poziom skryptów ad hoc tooan utrwalonych skryptów.

  > [!IMPORTANT]
  > Akcje skryptu używane podczas tworzenia klastra automatycznie są zachowywane.
  >
  > Skrypty, które nie są niepowodzenie utrwalone, nawet jeśli w szczególności wskazują one powinna być.

* Można zaakceptować **parametry** używane przez skrypt hello podczas wykonywania.
* Uruchom z **głównego poziomu uprawnień** hello węzłów klastra.
* Mogą być używane za pośrednictwem hello **portalu Azure**, **programu Azure PowerShell**, **interfejsu wiersza polecenia Azure**, lub **zestawu .NET SDK usługi HDInsight**

klaster Hello przechowuje historię wszystkie skrypty, które zostały uruchomione. Historia Hello jest przydatne, gdy potrzebny jest identyfikator hello toofind skryptu dla operacji podwyższenia poziomu lub obniżania poziomu.

> [!IMPORTANT]
> Nie istnieje żadne tooundo automatyczny sposób hello zmiany wprowadzone przez akcji skryptu. Należy ręcznie cofnąć zmiany hello lub Podaj skrypt, który odwraca je.


### <a name="script-action-in-hello-cluster-creation-process"></a>Akcja skryptu w procesie tworzenia klastra hello

Akcje skryptu używane podczas tworzenia klastra są nieco inne niż skryptu, który akcje został uruchomiony w istniejącym klastrze:

* skrypt Hello jest **automatycznie utrwalonego**.
* A **błąd** w hello skryptu może spowodować toofail procesu tworzenia klastra hello.

Witaj poniższym diagramie przedstawiono podczas wykonywania akcji skryptu podczas procesu tworzenia hello:

![Dostosowywanie klastrów usługi HDInsight i etapy podczas tworzenia klastra][img-hdi-cluster-states]

Witaj skrypt jest uruchamiany, gdy skonfigurowano usługi HDInsight. Na tym etapie hello skrypt będzie uruchamiany równolegle na wszystkich hello określonych węzłów w klastrze hello i jest uruchamiany z uprawnieniami głównego na węzłach hello.

> [!NOTE]
> Ponieważ hello skrypt jest uruchamiany z uprawnieniami poziomu głównego na powitania węzłów klastra, można wykonywać operacje, takie jak zatrzymanie i uruchomienie usług, w tym usług związanych z usługi Hadoop. Zatrzymanie usługi, upewnij się, czy hello Ambari usługi i innych usług związanych z Hadoop są gotowe do działania przed skryptu hello zakończeniu. Te usługi są wymagane toosuccessfully określić hello kondycję i stan hello klastra podczas jego tworzenia.


Podczas tworzenia klastra można użyć jednocześnie wiele akcji skryptu. Skrypty te są wywoływane w kolejności hello, w jakiej zostały określone.

> [!IMPORTANT]
> Akcje skryptu należy wykonać w ciągu 60 minut lub limitu czasu. Podczas inicjowania obsługi klastra hello skrypt jest uruchamiany równocześnie z innymi procesami instalacji i konfiguracji. Konkurowanie o zasoby, takie jak czas lub sieci przepustowości Procesora może powodować hello skryptu tootake dłużej toofinish niż w środowisku projektowania.
>
> toominimize hello czasu zajmuje toorun hello skryptu, należy unikać zadań, takich jak pobieranie i kompilowanie aplikacji ze źródła. Wstępnie skompilować aplikacje i przechowywać dane binarne hello w usłudze Azure Storage.


### <a name="script-action-on-a-running-cluster"></a>Akcja skryptu w klastrze uruchomione

W przeciwieństwie do skryptu, który akcje używane podczas tworzenia klastra, błąd skryptu uruchomionego na już działającego klastra nie powoduje automatycznego hello klastra toochange tooa nie powiodło się stan. Po ukończeniu działania skryptu hello klastra powinna zwrócić tooa "uruchomiona".

> [!IMPORTANT]
> Nawet jeśli hello klastra ma stan "uruchomiona", hello skryptu nie powiodło się mogą zawierać uszkodzone elementy. Na przykład skrypt można usunąć pliki wymagane przez hello klastra.
>
> Skrypty akcje uruchamiane z uprawnieniami głównego, dlatego należy się zapoznać przed zastosowaniem klastra tooyour działania skryptu.

Podczas stosowania klastra tooa skryptu, hello klastra stan zmieni się toofrom **systemem** za**zaakceptowane**, następnie **konfiguracji HDInsight**, a na koniec z powrotem zbyt**Systemem** skryptów powiodło się. Stan skryptu Hello jest rejestrowane w historii akcji skryptu hello i za pomocą tego toodetermine informacji czy skrypt hello powodzeniem lub niepowodzeniem. Na przykład Witaj `Get-AzureRmHDInsightScriptActionHistory` polecenia cmdlet programu PowerShell może być używane tooview hello stanu skryptu. Zwraca informacje toohello podobne następującego tekstu:

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> Jeśli zmienisz hasło użytkownika (Administrator) klastra powitania po utworzeniu klastra hello, skryptów, które akcje przeprowadzony na ten klaster może zakończyć się niepowodzeniem. Jeśli masz żadnych akcji utrwalonego skryptu tej docelowej węzłów procesu roboczego, te skrypty może zakończyć się niepowodzeniem podczas skalowania hello klastra.

## <a name="example-script-action-scripts"></a>Przykładowe skrypty akcji skryptu

Skrypt skrypty akcji mogą być używane za pośrednictwem hello następujące narzędzia:

* Azure Portal
* Azure PowerShell
* Interfejs wiersza polecenia platformy Azure
* Zestaw SDK dla platformy .NET usługi HDInsight

Usługa HDInsight zapewnia następujące składniki w klastrach HDInsight hello tooinstall skrypty:

| Nazwa | Skrypt |
| --- | --- |
| **Dodaj konto usługi Azure Storage** |https://hdiconfigactions.blob.Core.Windows.NET/linuxaddstorageaccountv01/Add-Storage-Account-v01.sh. Zobacz [klastra usługi HDInsight tooan dodatkowego magazynu Dodaj](hdinsight-hadoop-add-storage.md). |
| **Instalowanie aplikacji Hue** |https://hdiconfigactions.blob.Core.Windows.NET/linuxhueconfigactionv02/Install-Hue-Uber-v02.sh. Zobacz [instalacji i używania aplikacji Hue w usłudze HDInsight clusters](hdinsight-hadoop-hue-linux.md). |
| **Zainstaluj Presto** |https://RAW.githubusercontent.com/hdinsight/Presto-hdinsight/Master/installpresto.sh. Zobacz [instalacji i używania Presto w usłudze HDInsight clusters](hdinsight-hadoop-install-presto.md). |
| **Zainstaluj Solr** |https://hdiconfigactions.blob.Core.Windows.NET/linuxsolrconfigactionv01/solr-Installer-v01.sh. Zobacz [instalacji i używania Solr w usłudze HDInsight clusters](hdinsight-hadoop-solr-install-linux.md). |
| **Zainstaluj Giraph** |https://hdiconfigactions.blob.Core.Windows.NET/linuxgiraphconfigactionv01/giraph-Installer-v01.sh. Zobacz [instalacji i używania Giraph w usłudze HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md). |
| **Wstępne ładowanie bibliotek technologii Hive** |https://hdiconfigactions.blob.Core.Windows.NET/linuxsetupcustomhivelibsv01/Setup-customhivelibs-v01.sh. Zobacz [dodać Hive bibliotek w klastrach HDInsight](hdinsight-hadoop-add-hive-libraries.md). |
| **Instalowanie i aktualizowanie środowiska Mono** | https://hdiconfigactions.blob.Core.Windows.NET/Install-mono/Install-mono.bash. Zobacz [instalacji lub aktualizacji Mono w usłudze HDInsight](hdinsight-hadoop-install-mono.md). |

## <a name="use-a-script-action-during-cluster-creation"></a>Użyć akcji skryptu podczas tworzenia klastra

Ta sekcja zawiera przykłady na różne sposoby hello akcji skryptu można użyć podczas tworzenia klastra usługi HDInsight.

### <a name="use-a-script-action-during-cluster-creation-from-hello-azure-portal"></a>Użyć akcji skryptu podczas tworzenia klastra z hello portalu Azure

1. Rozpocznij tworzenie klastra, zgodnie z opisem w [klastrów utworzyć Hadoop w HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Zatrzymać po osiągnięciu hello __klastra Podsumowanie__ sekcji.

2. Z hello __klastra Podsumowanie__ sekcji, wybierz hello __Edytuj__ łączy dla __Zaawansowane ustawienia__.

    ![Łącze Ustawienia zaawansowane](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. Z hello __Zaawansowane ustawienia__ zaznacz __skryptu akcji__. Z hello __skryptu akcje__ zaznacz __+ nowy przesyłania__

    ![Przedstawia nowa akcja skryptu](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. Użyj hello __wybierz skrypt__ tooselect wpis wstępnie przygotowanych skryptu. Wybierz toouse skryptu niestandardowego __niestandardowych__ , a następnie wprowadź hello __nazwa__ i __Bash skryptu identyfikatora URI__ skryptu.

    ![Dodawanie skryptu w formie skryptu wybierz hello](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    Witaj w poniższej tabeli opisano elementy hello w formularzu hello:

    | Właściwość | Wartość |
    | --- | --- |
    | Wybierz skrypt | toouse własnego skryptu, wybierz opcję __niestandardowy__. W przeciwnym razie wybierz hello podane skryptów. |
    | Nazwa |Określ nazwę hello akcji skryptu. |
    | Skrypt bash identyfikatora URI |Określ hello URI toohello skrypt, który jest wywołana toocustomize hello klastra. |
    | Dozorcy HEAD/procesu roboczego |Określ węzły hello (**Head**, **procesu roboczego**, lub **dozorcy**) na których dostosowanie hello skrypt jest uruchamiany. |
    | Parametry |Określ parametry hello, jeśli są wymagane przez skrypt hello. |

    Użyj hello __Utrwal tę akcję skryptu__ tooensure wpis, który hello skryptu jest stosowany podczas operacji skalowania.

5. Wybierz __Utwórz__ toosave hello skryptu. Następnie można użyć __+ przesyłania nowych__ tooadd inny skrypt.

    ![Wiele akcji skryptu](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    Po zakończeniu dodawania skryptów, użyj hello __wybierz__ przycisk, a następnie hello __dalej__ toohello tooreturn przycisk __klastra Podsumowanie__ sekcji.

3. toocreate hello klastra, wybierz opcję __Utwórz__ z hello __klastra Podsumowanie__ zaznaczenia.

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a>Użyć akcji skryptu z szablonów usługi Azure Resource Manager

Przykłady Hello w tej sekcji pokazują, jak toouse skryptu akcji przy użyciu szablonów usługi Azure Resource Manager.

#### <a name="before-you-begin"></a>Przed rozpoczęciem

* Aby uzyskać informacji na temat konfigurowania stacji roboczej toorun poleceń cmdlet programu Powershell w usłudze HDInsight, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).
* Aby uzyskać instrukcje na temat szablonów toocreate, zobacz [szablonów Authoring Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).
* Jeśli nie były wcześniej używane programu Azure PowerShell z usługą Resource Manager, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).

#### <a name="create-clusters-using-script-action"></a>Tworzenie klastrów za pomocą akcji skryptu

1. Skopiuj hello następującego szablonu tooa lokalizacji na komputerze. Ten szablon instaluje Giraph hello headnodes i proces roboczy węzłach klastra hello. Możesz również sprawdzić, czy szablon JSON hello jest prawidłowy. Wklej szablon zawartości do [JSONLint](http://jsonlint.com/), narzędzie sprawdzania poprawności online JSON.

            {
            "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
            "contentVersion": "1.0.0.0",
            "parameters": {
                "clusterLocation": {
                    "type": "string",
                    "defaultValue": "West US",
                    "allowedValues": [ "West US" ]
                },
                "clusterName": {
                    "type": "string"
                },
                "clusterUserName": {
                    "type": "string",
                    "defaultValue": "admin"
                },
                "clusterUserPassword": {
                    "type": "securestring"
                },
                "sshUserName": {
                    "type": "string",
                    "defaultValue": "username"
                },
                "sshPassword": {
                    "type": "securestring"
                },
                "clusterStorageAccountName": {
                    "type": "string"
                },
                "clusterStorageAccountResourceGroup": {
                    "type": "string"
                },
                "clusterStorageType": {
                    "type": "string",
                    "defaultValue": "Standard_LRS",
                    "allowedValues": [
                        "Standard_LRS",
                        "Standard_GRS",
                        "Standard_ZRS"
                    ]
                },
                "clusterStorageAccountContainer": {
                    "type": "string"
                },
                "clusterHeadNodeCount": {
                    "type": "int",
                    "defaultValue": 1
                },
                "clusterWorkerNodeCount": {
                    "type": "int",
                    "defaultValue": 2
                }
            },
            "variables": {
            },
            "resources": [
                {
                    "name": "[parameters('clusterStorageAccountName')]",
                    "type": "Microsoft.Storage/storageAccounts",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-05-01-preview",
                    "dependsOn": [ ],
                    "tags": { },
                    "properties": {
                        "accountType": "[parameters('clusterStorageType')]"
                    }
                },
                {
                    "name": "[parameters('clusterName')]",
                    "type": "Microsoft.HDInsight/clusters",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-03-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Storage/storageAccounts/', parameters('clusterStorageAccountName'))]"
                    ],
                    "tags": { },
                    "properties": {
                        "clusterVersion": "3.2",
                        "osType": "Linux",
                        "clusterDefinition": {
                            "kind": "hadoop",
                            "configurations": {
                                "gateway": {
                                    "restAuthCredential.isEnabled": true,
                                    "restAuthCredential.username": "[parameters('clusterUserName')]",
                                    "restAuthCredential.password": "[parameters('clusterUserPassword')]"
                                }
                            }
                        },
                        "storageProfile": {
                            "storageaccounts": [
                                {
                                    "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                                    "isDefault": true,
                                    "container": "[parameters('clusterStorageAccountContainer')]",
                                    "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), '2015-05-01-preview').key1]"
                                }
                            ]
                        },
                        "computeProfile": {
                            "roles": [
                                {
                                    "name": "headnode",
                                    "targetInstanceCount": "[parameters('clusterHeadNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installGiraph",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                },
                                {
                                    "name": "workernode",
                                    "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installR",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                }
            ],
            "outputs": {
                "cluster":{
                    "type" : "object",
                    "value" : "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                }
            }
        }
2. Uruchom program Azure PowerShell i logowania tooyour konto platformy Azure. Po podaniu poświadczeń, hello polecenie zwraca informacje o Twoim koncie.

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. Jeśli masz wiele subskrypcji, podaj identyfikator subskrypcji hello mają toouse dla wdrożenia.

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > Można użyć `Get-AzureRmSubscription` tooget listę wszystkich subskrypcji skojarzonych z Twoim kontem, w tym hello identyfikator subskrypcji dla każdej z nich.

4. Jeśli nie masz istniejącej grupy zasobów, należy utworzyć grupę zasobów. Podaj nazwę hello hello grupy zasobów i lokalizacji, która należy do rozwiązania. Zwracany jest podsumowanie hello nową grupę zasobów.

        New-AzureRmResourceGroup -Name myresourcegroup -Location "West US"

        ResourceGroupName : myresourcegroup
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/######/resourceGroups/ExampleResourceGroup

5. toocreate wdrożenia dla grupy zasobów, uruchom hello **AzureRmResourceGroupDeployment nowy** poleceń i podaj hello wymaganych parametrów. Parametry Hello zawierają hello następujące dane:

    * Nazwa wdrożenia
    * Witaj nazwę grupy zasobów
    * Ścieżka Hello lub utworzony szablon toohello adresu URL.

  Jeśli szablon wymaga parametrów, należy podać także tych parametrów. W takim przypadku tooinstall akcji skryptu hello R w klastrze hello nie wymaga żadnych parametrów.

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    Jesteś tooprovide zostanie wyświetlony monit o wartości parametrów hello zdefiniowane w szablonie hello.

1. Po wdrożeniu grupy zasobów hello zostanie wyświetlone podsumowanie wdrożenia hello.

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. Jeśli wdrożenie nie powiedzie się, można użyć następującego polecenia cmdlet tooget informacje o niepowodzeniach hello hello.

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a>Użyć akcji skryptu podczas tworzenia klastra z programu Azure PowerShell

W tej sekcji użyjesz hello [AzureRmHDInsightScriptAction Dodaj](https://msdn.microsoft.com/library/mt603527.aspx) skrypty tooinvoke polecenia cmdlet, za pomocą akcji skryptu toocustomize klastra. Przed kontynuowaniem upewnij się, zainstalowaniu i skonfigurowaniu programu Azure PowerShell. Aby uzyskać informacji na temat konfigurowania stacji roboczej toorun poleceń cmdlet programu PowerShell w usłudze HDInsight, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

Witaj poniższy skrypt pokazuje, jak tooapply akcji skryptu podczas tworzenia klastra przy użyciu programu PowerShell:

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

Może upłynąć kilka minut przed utworzeniem klastra hello.

### <a name="use-a-script-action-during-cluster-creation-from-hello-hdinsight-net-sdk"></a>Użyć akcji skryptu podczas tworzenia klastra z hello zestawu .NET SDK usługi HDInsight

Witaj zestawu .NET SDK usługi HDInsight zapewnia bibliotek klienckich, które umożliwia łatwiejsze toowork z usługą HDInsight z poziomu aplikacji .NET. Przykładowy kod [opartych na systemie Linux z tworzenia klastrów w usłudze HDInsight przy użyciu hello zestawu .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).

## <a name="apply-a-script-action-tooa-running-cluster"></a>Zastosuj tooa akcji skryptu, z klastra

W tej sekcji Dowiedz się, jak tooapply skryptu tooa akcji uruchamiania klastra.

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-portal"></a>Zastosuj tooa akcji skryptu, uruchamiając klastra z hello portalu Azure

1. Z hello [portalu Azure](https://portal.azure.com), wybierz z klastrem usługi HDInsight.

2. Omówienie klastrów HDInsight hello, zaznacz hello **akcji skryptu** kafelka.

    ![Kafelek akcji skryptu](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > Możesz też wybrać **wszystkie ustawienia** , a następnie wybierz **akcji skryptu** z hello w sekcji Ustawienia.

3. Z góry hello hello sekcji akcji skryptu, wybierz **przesyłania nowych**.

    ![Dodaj tooa skryptu, z klastra](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. Użyj hello __wybierz skrypt__ tooselect wpis wstępnie przygotowanych skryptu. Wybierz toouse skryptu niestandardowego __niestandardowych__ , a następnie wprowadź hello __nazwa__ i __Bash skryptu identyfikatora URI__ skryptu.

    ![Dodawanie skryptu w formie skryptu wybierz hello](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    Witaj w poniższej tabeli opisano elementy hello w formularzu hello:

    | Właściwość | Wartość |
    | --- | --- |
    | Wybierz skrypt | toouse własnego skryptu, wybierz opcję __niestandardowych__. W przeciwnym razie wybierz udostępnionego skryptu. |
    | Nazwa |Określ nazwę hello akcji skryptu. |
    | Skrypt bash identyfikatora URI |Określ hello URI toohello skrypt, który jest wywołana toocustomize hello klastra. |
    | Dozorcy HEAD/procesu roboczego |Określ węzły hello (**Head**, **procesu roboczego**, lub **dozorcy**) na których dostosowanie hello skrypt jest uruchamiany. |
    | Parametry |Określ parametry hello, jeśli są wymagane przez skrypt hello. |

    Użyj hello __Utrwal tę akcję skryptu__ wpis toomake się, że skrypt hello jest stosowany podczas operacji skalowania.

5. Na koniec użyj hello **Utwórz** przycisk tooapply hello skryptu toohello klastra.

### <a name="apply-a-script-action-tooa-running-cluster-from-azure-powershell"></a>Zastosuj tooa akcji skryptu, uruchamiając klastra z programu Azure PowerShell

Przed kontynuowaniem upewnij się, zainstalowaniu i skonfigurowaniu programu Azure PowerShell. Aby uzyskać informacji na temat konfigurowania stacji roboczej toorun poleceń cmdlet programu PowerShell w usłudze HDInsight, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

Witaj poniższym przykładzie pokazano, jak tooapply klastra uruchomione tooa akcji skryptu:

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

Po zakończeniu operacji hello, pojawi się informacji toohello podobne następującego tekstu:

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-cli"></a>Zastosuj tooa akcji skryptu, uruchamiając klastra z hello wiersza polecenia platformy Azure

Przed kontynuowaniem upewnij się, zostanie zainstalowany i skonfigurowany hello wiersza polecenia platformy Azure. Aby uzyskać więcej informacji, zobacz [hello instalowanie interfejsu wiersza polecenia Azure](../cli-install-nodejs.md).

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. tooAzure tooswitch tryb usługi Resource Manager, użyj hello następujące polecenie w wierszu polecenia hello:

        azure config mode arm

2. Użyj powitania po tooyour tooauthenticate subskrypcji platformy Azure.

        azure login

3. Użyj hello następujące polecenia tooapply tooa akcji skryptu, z klastra

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    W przypadku pominięcia parametrów dla tego polecenia, zostanie wyświetlony monit o ich. Jeśli hello skryptu z `-u` akceptuje parametry, można określić je przy użyciu hello `-p` parametru.

    Nieprawidłowy węzeł typy `headnode`, `workernode`, i `zookeeper`. Jeśli skrypt hello powinno być zastosowane toomultiple typy węzłów, określić typy hello oddzielone ";". Na przykład `-n headnode;workernode`.

    toopersist hello skryptu, Dodaj hello `--persistOnSuccess`. Można również utrwalić skryptu hello później za pomocą `azure hdinsight script-action persisted set`.

    Po zakończeniu zadania hello, pojawi się toohello podobne dane wyjściowe następującego tekstu:

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-tooa-running-cluster-using-rest-api"></a>Zastosuj tooa akcji skryptu, systemem klastra przy użyciu interfejsu API REST

Zobacz [uruchomienia akcji skryptu w klastrze uruchomione](https://msdn.microsoft.com/library/azure/mt668441.aspx).

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-hdinsight-net-sdk"></a>Zastosuj tooa akcji skryptu, uruchamiając klastra z hello zestawu .NET SDK usługi HDInsight

Na przykład przy użyciu hello zestawu .NET SDK tooapply skrypty tooa klastra, zobacz [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).

## <a name="view-history-promote-and-demote-script-actions"></a>Wyświetlanie historii, wspierania i obniżyć poziom akcji skryptu

### <a name="using-hello-azure-portal"></a>Przy użyciu hello portalu Azure

1. Z hello [portalu Azure](https://portal.azure.com), wybierz z klastrem usługi HDInsight.

2. Omówienie klastrów HDInsight hello, zaznacz hello **akcji skryptu** kafelka.

    ![Kafelek akcji skryptu](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > Możesz też wybrać **wszystkie ustawienia** , a następnie wybierz **akcji skryptu** z hello w sekcji Ustawienia.

4. Historia skryptów dla tego klastra jest wyświetlany na powitania sekcji akcji skryptu. Informacje te obejmują listę utrwalonych skryptów. Poniższy zrzut ekranu hello zawiera ten powitalne Solr skryptu zostało uruchomione w tym klastrze. Zrzut ekranu Hello nie są wyświetlane wszystkie skrypty utrwalonych.

    ![Sekcji działania skryptu](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. Wybranie skryptu z historii hello powoduje wyświetlenie sekcja właściwości hello w ramach tego skryptu. Z góry hello ekranu hello można ponownie uruchomić skrypt hello lub Podwyższ go.

    ![Właściwości działania skryptu](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. Można również użyć hello **...**  toohello prawo do wpisów na powitania akcji skryptu sekcji tooperform akcje.

    ![Skrypt akcje... użycia](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a>Korzystanie z programu Azure PowerShell

| Użyj następujących hello... | zbyt... |
| --- | --- |
| Get-AzureRmHDInsightPersistedScriptAction |Pobieranie informacji na temat akcji utrwalonego skryptu |
| Get-AzureRmHDInsightScriptActionHistory |Pobierz historię skryptu akcje zastosowane toohello klastra lub szczegółów dla określonego skryptu |
| Set-AzureRmHDInsightPersistedScriptAction |Zamienia ad hoc tooa akcji skryptów trwale akcji skryptu |
| Remove-AzureRmHDInsightPersistedScriptAction |Przenosi akcji ad hoc tooan akcji utrwalonego skryptu |

> [!IMPORTANT]
> Przy użyciu `Remove-AzureRmHDInsightPersistedScriptAction` nie cofa hello akcje wykonywane przez skrypt. To polecenie cmdlet usuwa tylko hello utrwalonego flagę.

powitania po przykładowy skrypt pokazuje przy użyciu hello toopromote poleceń cmdlet, a następnie obniżenia poziomu skryptu.

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-hello-azure-cli"></a>Przy użyciu hello wiersza polecenia platformy Azure

| Użyj następujących hello... | zbyt... |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |Pobierz listę akcji utrwalonego skryptu |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |Pobieranie informacji na temat akcji określonych utrwalonego skryptu |
| `azure hdinsight script-action history list <clustername>` |Pobierz historię skryptu akcje zastosowane toohello klastra |
| `azure hdinsight script-action history show <clustername> <scriptname>` |Pobieranie informacji na temat działań określonego skryptu |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |Zamienia ad hoc tooa akcji skryptów trwale akcji skryptu |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |Przenosi akcji ad hoc tooan akcji utrwalonego skryptu |

> [!IMPORTANT]
> Przy użyciu `azure hdinsight script-action persisted delete` nie cofa hello akcje wykonywane przez skrypt. To polecenie cmdlet usuwa tylko hello utrwalonego flagę.

### <a name="using-hello-hdinsight-net-sdk"></a>Przy użyciu zestawu .NET SDK HDInsight hello

Na przykład za pomocą historii hello zestawu .NET SDK tooretrieve skryptu z klastra, podwyższyć poziom lub obniżyć poziom skryptów, zobacz [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).

> [!NOTE]
> Również w przykładzie pokazano, jak tooinstall aplikacji usługi HDInsight przy użyciu hello zestawu .NET SDK.

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a>Obsługa oprogramowania typu open source używane w klastrach HDInsight

Witaj usługi Microsoft Azure HDInsight używa ekosystem technologii open source utworzona wokół Hadoop. Microsoft Azure udostępnia ogólnego poziomu wsparcia dla technologii open source. Aby uzyskać więcej informacji, zobacz hello **zakres obsługi** sekcji hello [witryny sieci Web pomocy technicznej platformy Azure — często zadawane pytania](https://azure.microsoft.com/support/faq/). Witaj usługa HDInsight zapewnia dodatkowy poziom obsługi wbudowanych składników.

Istnieją dwa typy składników open source, które są dostępne w hello usługi HDInsight:

* **Wbudowanych składników** — te składniki są wstępnie zainstalowane w klastrach HDInsight i podaj podstawowych funkcji programu hello klastra. Na przykład YARN ResourceManager, język zapytań Hive hello (HiveQL) i biblioteki Mahout hello należy toothis kategorii. Pełna lista składniki klastra jest dostępna w [nowości w wersjach klastra Hadoop hello dostarczanych z usługą HDInsight](hdinsight-component-versioning.md).
* **Niestandardowe składniki** -, jako użytkownik hello klastra, można zainstalować lub użyć w obciążenie jakiegokolwiek składnika dostępne w społeczności hello lub utworzone przez użytkownika.

> [!WARNING]
> Składniki dostarczony z klastrem usługi HDInsight hello są w pełni obsługiwane. Microsoft Support pomaga tooisolate i rozwiąż problemy toothese powiązane składniki.
>
> Niestandardowe składniki odbierania toohelp Obsługa uzasadnione ekonomicznie toofurther należy rozwiązać problem hello. Pomocy technicznej firmy Microsoft może być możliwe tooresolve hello problem lub ich może zapytać tooengage dostępne kanały o technologiach typu open source hello wykryto głębokie doświadczenia z tej technologii. Na przykład istnieje wiele witryn społeczności, które mogą być używane, takie jak: [forum MSDN dla usługi HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Projekty Apache mieć witryny projektu na [http://apache.org](http://apache.org), na przykład: [Hadoop](http://hadoop.apache.org/).

Witaj usługi HDInsight udostępnia kilka metod toouse niestandardowych składników. Witaj, który dotyczy tego samego poziomu wsparcia, niezależnie od tego, jak używać lub zainstalowany w klastrze hello składnika. Witaj Poniższa lista zawiera opis hello Najczęstszym z niestandardowych składników można używać w klastrach HDInsight:

1. Przesyłanie zadań — usługi Hadoop i innych typów zadań, które wykonać albo użyć niestandardowych składników mogą być przesłane toohello klastra.

2. Dostosowywanie klastra — podczas tworzenia klastra, można określić dodatkowe ustawienia i niestandardowe składniki, które są zainstalowane na węzłach klastra hello.

3. Próbek - dla popularnych niestandardowych składników, firma Microsoft i inne osoby mogą powodować przykłady sposobu użycia tych składników na powitania klastrów usługi HDInsight. Te przykłady są udostępniane bez obsługi.

## <a name="troubleshooting"></a>Rozwiązywanie problemów

Można użyć narzędzia Ambari web interfejsu użytkownika tooview informacji rejestrowanych przez akcji skryptu. W przypadku niepowodzenia podczas tworzenia klastra skryptu hello hello dzienniki dostępne są również hello domyślnego konta magazynu skojarzone z klastrem hello. Ta sekcja zawiera informacje dotyczące sposobu tooretrieve hello logowania za pomocą obu tych opcji.

### <a name="using-hello-ambari-web-ui"></a>Przy użyciu hello Interfejsu sieci Web Ambari

1. W przeglądarce Przejdź toohttps://CLUSTERNAME.azurehdinsight.net. Zamień NAZWAKLASTRA hello nazwę klastra usługi HDInsight.

    Po wyświetleniu monitu wprowadź nazwę konta administratora hello (Administrator) i hasło klastra hello. Masz poświadczenia administratora hello tooreenter w formularzu sieci web.

2. Pasek hello u góry strony hello hello, zaznacz hello **ops** wpisu. Zostanie wyświetlona lista bieżące i poprzednie operacje wykonywane na powitania klastra za pomocą narzędzia Ambari.

    ![Pasek interfejsu użytkownika sieci web Ambari z ops wybrane](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. Znajdź hello wpisów, które mają **Uruchom\_customscriptaction** w hello **operacji** kolumny. Te wpisy są tworzone przy uruchamianiu hello akcji skryptu.

    ![Zrzut ekranu przedstawiający operacji](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    tooview hello STDOUT i STDERR dane wyjściowe, wybierz wpis run\customscriptaction hello i przejść za pośrednictwem łącza hello. Te dane wyjściowe jest generowany po uruchomieniu skryptu hello i mogą zawierać przydatne informacje.

### <a name="access-logs-from-hello-default-storage-account"></a>Dzienniki dostępu z hello domyślne konto magazynu

W przypadku niepowodzenia tworzenia klastra hello ze względu na błąd akcji skryptu tooa hello dzienniki są dostępne z konta magazynu klastra hello.

* Witaj dzienniki magazynu są dostępne pod adresem `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.

    ![Zrzut ekranu przedstawiający operacji](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    W tym katalogu dzienników hello są zorganizowane oddzielnie headnode, workernode i węzły dozorcy. Przykłady to:

    * **Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`

    * **Węzła procesu roboczego** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`

    * **Węzeł dozorcy** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`

* Wszystkie stdout i stderr hello odpowiedniego hosta jest przekazywane toohello konta magazynu. Istnieje **dane wyjściowe -\*.txt** i **błędy -\*.txt** dla każdej akcji skryptu. Plik wyjściowy *.txt Hello zawiera informacje o hello identyfikatora URI hello skryptu, który został uruchomiony na hoście hello. Na przykład:

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* Istnieje możliwość wielokrotnie utworzyć klaster akcji skryptu z hello tej samej nazwy. W takim przypadku można odróżnić hello dzienniki odpowiednie na podstawie nazwy folderu Data hello. Na przykład hello struktura folderów dla klastra (mycluster) utworzone w różnych terminach zostaną wyświetlone podobne toohello następujące wpisy dziennika:

    `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`

* Po utworzeniu klastra akcji skryptu z hello sama nazwa na powitania sam dzień, można użyć hello unikatowy prefiks tooidentify hello odpowiednich plików dziennika.

* Po utworzeniu klastra w pobliżu 00:00:00 (północ), jest to możliwe, że pliki dziennika hello obejmują przez dwa dni. W takich przypadkach, zobacz dwa foldery inną datę dla hello tego samego klastra.

* Przekazywanie dzienników pliki toohello domyślny kontener może potrwać too5 min, zwłaszcza w przypadku dużych klastrów. Tak Jeśli chcesz tooaccess hello dzienniki, nie należy natychmiast usuwać klastra hello Jeśli zawodzi Akcja skryptu.

### <a name="ambari-watchdog"></a>Ambari programu alarmowego

> [!WARNING]
> Nie należy zmieniać hasła hello hello Ambari programu alarmowego (hdinsightwatchdog) w klastrze usługi HDInsight opartej na systemie Linux. Zmiany hasła hello na tym koncie dzieli hello możliwości toorun nowych skrypt akcji w klastrze usługi HDInsight hello.

### <a name="cant-import-name-blobservice"></a>Nie można zaimportować nazwa BlobService

__Objawy__: hello skryptu kończy się niepowodzeniem. Tekst toohello podobne następujący błąd jest wyświetlany podczas przeglądania operacji hello w Ambari:

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

__Przyczyna__: ten błąd występuje podczas uaktualniania klienta magazynu Azure Python hello, dostępnej z klastrem usługi HDInsight hello. HDInsight oczekuje klienta usługi Azure Storage 0.20.0.

__Rozdzielczość__: tooresolve ten błąd, ręcznie połączyć za pomocą węzła klastra tooeach `ssh` i hello Użyj następującego polecenia tooreinstall hello poprawne magazynu klient w wersji:

```
sudo pip install azure-storage==0.20.0
```

Aby uzyskać informacji na temat łączenia toohello klastra przy użyciu protokołu SSH, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a>Historia nie wyświetla skrypty używane podczas tworzenia klastra

Jeśli klaster został utworzony przed 15 marca 2016 r nie miało wpis w historii akcji skryptu. Jeśli rozmiar klastra powitania po 15 marca 2016 r skrypty hello przy użyciu podczas tworzenia klastra pojawiają się w historii zgodnie z ich stosowania toonew węzłów w klastrze hello jako część hello operacja zmiany rozmiaru.

Istnieją jednak dwa wyjątki:

* Jeśli klaster został utworzony przed 1 września 2015 r. Ta data jest w przypadku akcji skryptu zostały wprowadzone. Dowolnego klastra utworzone przed tą datą nie ma użyć akcji skryptu do tworzenia klastra.

* Jeśli można użyć wielu akcji skryptu podczas tworzenia klastra i hello tej samej nazwy dla wielu skryptów lub hello takie same nazwy, tym samym identyfikatorze URI, ale różne parametry dla wielu skryptów. W takich przypadkach jest wyświetlany hello następujący błąd:

    Skryptu nowych akcji może być uruchomione w tym klastrze powodu tooconflicting skryptu nazw w istniejących skryptów. Nazwy skrypt podanych w klastrze utworzyć musi być unikatowe. Istniejące skrypty są uruchomione na zmiany rozmiaru.

## <a name="next-steps"></a>Następne kroki

* [Tworzenie skryptów akcji skryptu dla usługi HDInsight](hdinsight-hadoop-script-actions-linux.md)
* [Zainstalować i używać Solr w klastrach HDInsight](hdinsight-hadoop-solr-install-linux.md)
* [Zainstalować i używać Giraph w klastrach HDInsight](hdinsight-hadoop-giraph-install-linux.md)
* [Dodaj klaster usługi HDInsight tooan dodatkowego miejsca do magazynowania](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Etapy podczas tworzenia klastra"
