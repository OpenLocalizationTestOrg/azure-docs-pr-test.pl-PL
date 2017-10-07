---
title: "aaaCreate Hadoop clusters przy użyciu szablonów - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate klastrów dla usługi HDInsight przy użyciu szablonów usługi Resource Manager"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00a80dea-011f-44f0-92a4-25d09db9d996
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: jgao
ms.openlocfilehash: 92a6c1d888e401a11537dba34f188245ac17f448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a>Tworzenie klastrów Hadoop w usłudze HDInsight przy użyciu szablonów usługi Resource Manager
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

W tym artykule dowiesz się na kilka sposobów toocreate Azure HDInsight clusters przy użyciu szablonów usługi Azure Resource Manager. Aby uzyskać więcej informacji, zobacz [wdrażania aplikacji przy użyciu szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). toolearn o inne narzędzia do tworzenia klastra i funkcje, kliknij selektor karty hello na powitania początku tej strony lub zobacz [metody tworzenia klastrów](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).

## <a name="prerequisites"></a>Wymagania wstępne
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

toofollow hello instrukcje w tym artykule, będą potrzebne:

* [Subskrypcji platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Program Azure PowerShell i/lub Azure CLI.

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a>Szablony usługi Resource Manager
Szablonu usługi Resource Manager umożliwia łatwe toocreate powitania po aplikacji w jednej, skoordynowanej operacji:
* Klastry usługi HDInsight i ich zasoby zależne (takie jak hello domyślne konto magazynu)
* Inne zasoby (na przykład baza danych SQL Azure toouse Apache Sqoop)

W szablonie hello należy zdefiniować hello zasoby, które są wymagane dla aplikacji hello. Należy także określić wartości tooinput parametrów wdrożenia dla różnych środowisk. Szablon Hello składa się z kodu JSON i wyrażeń, użyj wartości tooconstruct dla danego wdrożenia.

Można znaleźć przykłady szablonu usługi HDInsight w [szablonów Szybki Start Azure](https://azure.microsoft.com/resources/templates/?term=hdinsight). Użyj wielu platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) z hello [rozszerzenia usługi Resource Manager](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) lub w szablonie hello toosave Edytor tekstu do pliku na stację roboczą. Dowiedz się, jak toocall hello szablonu przy użyciu różnych metod.

Aby uzyskać więcej informacji na temat szablonów usługi Resource Manager zobacz następujące artykuły hello:

* [Tworzenie szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)
* [Wdrażanie aplikacji przy użyciu szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a>Generowanie szablonów

Za pomocą hello portalu Azure, można skonfigurować wszystkie właściwości hello klastra, a następnie zapisz hello szablon przed jego wdrożeniem. Następnie można ponownie użyć hello szablonu.

**toogenerate szablonu przy użyciu hello portalu Azure**

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Kliknij przycisk **nowy** w menu po lewej stronie powitania kliknij **analizy i analiza**, a następnie kliknij przycisk **HDInsight**.
3. Wykonaj hello instrukcje tooenter właściwości. Można użyć albo hello **szybkie tworzenie** lub hello **niestandardowy** opcji.
4. Na powitania **Podsumowanie** , kliknij pozycję **Pobierz szablon i parametry**:

    ![Pobieranie szablonu usługi Resource Manager klastra tworzenia HDInsight Hadoop](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    Możesz wyświetlić listę hello pliku szablonu, pliku parametrów i kod próbek używanych toodeploy hello szablonu:

    ![HDInsight Hadoop tworzenia klastra opcje pobierania szablonu usługi Resource Manager](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    W tym miejscu można pobrać szablonu hello, bibliotekę szablonu tooyour zapisać lub wdrażanie szablonu hello.

    tooaccess szablon w bibliotece, kliknij przycisk **więcej usług** z menu po lewej stronie powitania, a następnie kliknij przycisk **szablony** (w obszarze hello **innych** kategorii).

    > [!Note]
    > Witaj pliku szablonu i parametry muszą być używane razem. W przeciwnym razie może uzyskać nieoczekiwane wyniki. Na przykład Witaj domyślne **clusterKind** wartość właściwości jest zawsze **hadoop**, pomimo należy określić przed pobraniem hello szablonu.



## <a name="deploy-with-powershell"></a>Wdrażanie przy użyciu programu PowerShell

Ta procedura powoduje utworzenie klastra usługi Hadoop w usłudze HDInsight.

1. Zapisz plik JSON hello w hello [dodatku](#appx-a-arm-template) tooyour stacji roboczej. W hello skrypt programu PowerShell, nazwa pliku hello jest `C:\HDITutorials-ARM\hdinsight-arm-template.json`.
2. W razie potrzeby wybierz hello parametry i zmienne.
3. Uruchom hello szablonu przy użyciu hello następującego skryptu programu PowerShell:

        ####################################
        # Set these variables
        ####################################
        #region - used for creating Azure service names
        $nameToken = "<Enter an Alias>"
        $templateFile = "C:\HDITutorials-ARM\hdinsight-arm-template.json"
        #endregion

        ####################################
        # Service names and variables
        ####################################
        #region - service names
        $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

        $resourceGroupName = $namePrefix + "rg"
        $hdinsightClusterName = $namePrefix + "hdi"
        $defaultStorageAccountName = $namePrefix + "store"
        $defaultBlobContainerName = $hdinsightClusterName

        $location = "East US 2"

        $armDeploymentName = $namePrefix
        #endregion

        ####################################
        # Connect tooAzure
        ####################################
        #region - Connect tooAzure subscription
        Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and hello dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    Witaj skrypt programu PowerShell konfiguruje tylko nazwę klastra hello. Nazwa konta magazynu Hello jest ustalony w szablonie hello. To hasło użytkownika klastra hello zostanie wyświetlony monit o tooenter. (hello domyślna nazwa użytkownika to **admin**.) Ma również hasło użytkownika SSH hello zostanie wyświetlony monit o tooenter. (nazwa użytkownika SSH domyślne hello jest **sshuser**.)  

Aby uzyskać więcej informacji, zobacz [wdrażanie przy użyciu programu PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).

## <a name="deploy-with-cli"></a>Rozmieszczanie za pomocą interfejsu wiersza polecenia
następujące przykładowe Hello używa Azure interfejsu wiersza polecenia (CLI). Tworzy klastra i jego zależne konto magazynu i kontener wywołując szablonu usługi Resource Manager:

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

Jesteś tooenter monitem:
* Nazwa klastra Hello.
* Witaj hasło użytkownika klastra. (hello domyślna nazwa użytkownika to **admin**.)
* hasło użytkownika SSH Hello. (nazwa użytkownika SSH domyślne hello jest **sshuser**.)

Hello następującego kodu zawiera wbudowany parametry:

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-hello-rest-api"></a>Wdrażanie z hello interfejsu API REST
Zobacz [Rozmieszczanie za pomocą interfejsu API REST hello](../azure-resource-manager/resource-group-template-deploy-rest.md).

## <a name="deploy-with-visual-studio"></a>Wdrażanie za pomocą programu Visual Studio
 Użyj programu Visual Studio toocreate projekt grupy zasobów i wdrożyć ją tooAzure za pomocą interfejsu użytkownika hello. Wybrany typ hello tooinclude zasobów w projekcie. Te zasoby są automatycznie dodawane toohello szablonu usługi Resource Manager. Projekt Hello udostępnia również szablonu hello toodeploy skrypt programu PowerShell.

Do wprowadzenia toousing programu Visual Studio z grupami zasobów, zobacz [tworzenie i wdrażanie grup zasobów platformy Azure za pomocą programu Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

## <a name="troubleshoot"></a>Rozwiązywanie problemów

W razie problemów podczas tworzenia klastrów usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Następne kroki
W tym artykule uzyskanych kilka sposobów toocreate klastra usługi HDInsight. toolearn więcej, zobacz następujące artykuły hello:

* Na przykład wdrażania zasobów za pomocą biblioteki klienta .NET hello zobacz [wdrażanie zasobów przy użyciu bibliotek .NET oraz szablonu](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Szczegółowy przykład wdrażania aplikacji, zobacz [udostępniania i wdrażanie mikrousług przewidywalnego na platformie Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).
* Aby uzyskać wskazówki dotyczące wdrażania środowiska toodifferent rozwiązania, zobacz [środowisk projektowania i testowania na platformie Microsoft Azure](../solution-dev-test-environments.md).
* toolearn o sekcje hello hello szablonu usługi Azure Resource Manager, zobacz [tworzenia szablonów](../azure-resource-manager/resource-group-authoring-templates.md).
* Listę funkcji hello można użyć w szablonie usługi Azure Resource Manager, zobacz [szablonu funkcji](../azure-resource-manager/resource-group-template-functions.md).

## <a name="appendix-resource-manager-template-toocreate-a-hadoop-cluster"></a>Dodatek: Menedżer zasobów szablonu toocreate klastra usługi Hadoop
Witaj następującego szablonu usługi Azure Resource Manager tworzy opartą na systemie Linux platformą Hadoop klaster z hello zależne konto magazynu Azure.

> [!NOTE]
> Ten przykład zawiera informacje o konfiguracji na potrzeby magazynu metadanych Hive i potrzeby magazynu metadanych Oozie. Usuwanie sekcji hello lub skonfiguruj sekcji hello przed użyciem hello szablonu.
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "hello name of hello HDInsight cluster toocreate."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used tooremotely access hello cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "location": {
        "type": "string",
        "defaultValue": "East US",
        "allowedValues": [
            "East US",
            "East US 2",
            "North Central US",
            "South Central US",
            "West US",
            "North Europe",
            "West Europe",
            "East Asia",
            "Southeast Asia",
            "Japan East",
            "Japan West",
            "Australia East",
            "Australia Southeast"
        ],
        "metadata": {
            "description": "hello location where all azure resources will be deployed."
        }
        },
        "clusterType": {
        "type": "string",
        "defaultValue": "hadoop",
        "allowedValues": [
            "hadoop",
            "hbase",
            "storm",
            "spark"
        ],
        "metadata": {
            "description": "hello type of hello HDInsight cluster toocreate."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "hello number of nodes in hello HDInsight cluster."
        }
        }
    },
    "variables": {
        "defaultApiVersion": "2015-05-01-preview",
        "clusterApiVersion": "2015-03-01-preview",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
        {
        "name": "[parameters('clusterName')]",
        "type": "Microsoft.HDInsight/clusters",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('clusterApiVersion')]",
        "dependsOn": [ "[concat('Microsoft.Storage/storageAccounts/',variables('clusterStorageAccountName'))]" ],
        "tags": {

        },
        "properties": {
            "clusterVersion": "3.4",
            "osType": "Linux",
            "tier": "standard",
            "clusterDefinition": {
            "kind": "[parameters('clusterType')]",
            "configurations": {
                "gateway": {
                "restAuthCredential.isEnabled": true,
                "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                },
                "hive-site": {
                    "javax.jdo.option.ConnectionDriverName": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "javax.jdo.option.ConnectionURL": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "javax.jdo.option.ConnectionUserName": "johndole",
                    "javax.jdo.option.ConnectionPassword": "myPassword$"
                },
                "hive-env": {
                    "hive_database": "Existing MSSQL Server database with SQL authentication",
                    "hive_database_name": "myhive20160901",
                    "hive_database_type": "mssql",
                    "hive_existing_mssql_server_database": "myhive20160901",
                    "hive_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "hive_hostname": "myadla0901dbserver.database.windows.net"
                },
                "oozie-site": {
                    "oozie.service.JPAService.jdbc.driver": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "oozie.service.JPAService.jdbc.url": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "oozie.service.JPAService.jdbc.username": "johndole",
                    "oozie.service.JPAService.jdbc.password": "myPassword$",
                    "oozie.db.schema.name": "oozie"
                },
                "oozie-env": {
                    "oozie_database": "Existing MSSQL Server database with SQL authentication",
                    "oozie_database_name": "myhive20160901",
                    "oozie_database_type": "mssql",
                    "oozie_existing_mssql_server_database": "myhive20160901",
                    "oozie_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "oozie_hostname": "myadla0901dbserver.database.windows.net"
                }            
            }
            },
            "storageProfile": {
            "storageaccounts": [
                {
                "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                "isDefault": true,
                "container": "[parameters('clusterName')]",
                "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                }
            ]
            },
            "computeProfile": {
            "roles": [
                {
                "name": "headnode",
                "targetInstanceCount": "2",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                },
                {
                "name": "workernode",
                "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                }
            ]
            }
        }
        }
    ],
    "outputs": {
        "cluster": {
        "type": "object",
        "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
        }
    }
    }

## <a name="appendix-resource-manager-template-toocreate-a-spark-cluster"></a>Dodatek: Menedżer zasobów szablonu toocreate klastra Spark

Ta sekcja zawiera szablonu usługi Resource Manager służy toocreate klastra Spark w usłudze HDInsight. Ten szablon obejmuje konfiguracje `spark-defaults` i `spark-thrift-sparkconf` (dla klastry Spark 1.6) i `spark2-defaults` i `spark2-thrift-sparkconf` (dla klastry Spark 2). Ponadto toothis, HDInsight jest obliczana i ustawia konfiguracje, takie jak `spark.executor.instances`, `spark.executor.memory`, i `spark.executor.cores` na podstawie hello rozmiaru klastra. 

Jeśli ustawisz wszystkie jeden parametr w sekcji jako część szablonu hello HDInsight nie obliczenia i ustaw hello inne parametry hello tej samej sekcji. Na przykład parametr `spark.executor.instances` w hello `spark-defaults` konfiguracji. Jeśli ustawisz parametr innego (na przykład `spark.yarn.exector.memoryOverhead`) w hello `spark-defaults` konfiguracji, HDInsight nie obliczenia i ustaw hello `spark.executor.instances` również parametr.

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "hello name of hello HDInsight cluster toocreate."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "hello location where all azure resources will be deployed."
            }
        },
        "clusterVersion": {
            "type": "string",
            "defaultValue": "3.5",
            "metadata": {
                "description": "HDInsight cluster version."
            }
        },
        "clusterWorkerNodeCount": {
            "type": "int",
            "defaultValue": 4,
            "metadata": {
                "description": "hello number of nodes in hello HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "hello type of hello HDInsight cluster toocreate."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used tooremotely access hello cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        }
    },
    "variables": {
        "defaultApiVersion": "2017-06-01",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
    {
            "apiVersion": "2015-03-01-preview",
            "name": "[parameters('clusterName')]",
            "type": "Microsoft.HDInsight/clusters",
            "location": "[parameters('location')]",
            "dependsOn": [],
            "properties": {
                "clusterVersion": "[parameters('clusterVersion')]",
                "osType": "Linux",
                "tier": "standard",
                "clusterDefinition": {
                    "kind": "[parameters('clusterKind')]",
                    "configurations": {
                        "gateway": {
                            "restAuthCredential.isEnabled": true,
                            "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                            "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                        },
                        "spark-defaults": {
                            "spark.executor.cores": "2"
                        },
                        "spark-thrift-sparkconf": {
                            "spark.yarn.executor.memoryOverhead": "896"
                        }
                    }
                },
                "storageProfile": {
                    "storageaccounts": [
                        {
                            "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                            "isDefault": true,
                            "container": "[parameters('clusterName')]",
                            "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                        }
                    ]
                },
                "computeProfile": {
                    "roles": [
                        {
                            "name": "headnode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 2,
                            "hardwareProfile": {
                                "vmSize": "Standard_D12"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                }
                            },
                            "virtualNetworkProfile": null,
                            "scriptActions": []
                        },
                        {
                            "name": "workernode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 4,
                            "hardwareProfile": {
                                "vmSize": "Standard_D4"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                    }
                                },
                                "virtualNetworkProfile": null,
                                "scriptActions": []
                            }
                        ]
                    }
                }
            }
        ]
    }
