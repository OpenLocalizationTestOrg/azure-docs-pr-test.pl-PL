---
title: "klastry aaaCreate HDInsight z usługą Data Lake Store jako domyślny magazyn przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Użyj programu Azure PowerShell toocreate i klastry usługi HDInsight za pomocą usługi Azure Data Lake Store"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8917af15-8e37-46cf-87ad-4e6d5d67ecdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/08/2017
ms.author: nitinme
ms.openlocfilehash: a5c0ad416da6ad9bd07204af2ebb6b7470916085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a>Tworzenie klastrów usługi HDInsight z usługą Data Lake Store jako domyślny magazyn przy użyciu programu PowerShell
> [!div class="op_single_selector"]
> * [Użyj hello portalu Azure](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Przy użyciu programu PowerShell (do magazynu domyślnego)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Przy użyciu programu PowerShell (dla dodatkowego magazynu)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Użyj Menedżera zasobów](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

Dowiedz się, jak toouse tooconfigure programu Azure PowerShell Azure HDInsight clusters z usługi Azure Data Lake Store jako domyślnego magazynu. Aby uzyskać instrukcje dotyczące tworzenia klastra usługi HDInsight z usługą Data Lake Store jako dodatkowego miejsca do magazynowania, zobacz [tworzenia klastra usługi HDInsight z usługą Data Lake Store jako dodatkowego magazynu](data-lake-store-hdinsight-hadoop-use-powershell.md).

Poniżej przedstawiono kilka istotnych kwestii dotyczących z usługą Data Lake Store za pomocą usługi HDInsight:

* klastry usługi HDInsight toocreate opcji Hello z dostępem do tooData Lake Store jako domyślny magazyn jest dostępny dla usługi HDInsight w wersji 3.5 i 3,6.

* toocreate opcja Hello klastrów usługi HDInsight z dostęp tooData Lake Store jako domyślnego magazynu jest *nie jest dostępny* klastrów HDInsight Premium.

tooconfigure toowork HDInsight z usługą Data Lake Store za pomocą programu PowerShell, wykonaj instrukcje hello w sekcjach następnych pięciu hello.

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka, upewnij się, czy zostały spełnione następujące wymagania hello:

* **Subskrypcja platformy Azure**: Przejdź zbyt[Azure Pobierz bezpłatną wersję próbną](https://azure.microsoft.com/pricing/free-trial/).
* **Program Azure PowerShell 1.0 lub nowszego**: zobacz [jak tooinstall i konfigurowanie programu PowerShell](/powershell/azure/overview).
* **Windows Software Development Kit (SDK)**: tooinstall zestaw Windows SDK, przejdź zbyt[pliki do pobrania i narzędzi dla systemu Windows 10](https://dev.windows.com/en-us/downloads). Witaj zestawu SDK jest używane toocreate certyfikatu zabezpieczeń.
* **Nazwy głównej usługi Azure Active Directory**: w tym samouczku opisano sposób toocreate nazwy głównej usługi w usłudze Azure Active Directory (Azure AD). Jednak toocreate nazwy głównej usługi, musisz być administratorem usługi Azure AD. Jeśli jesteś administratorem, możesz pominąć te wymagania wstępne i kontynuować hello samouczka.

    >[!NOTE]
    >Usługi można utworzyć podmiot, tylko wtedy, gdy administrator usługi Azure AD. Administrator usługi Azure AD należy utworzyć usługę podmiotu zabezpieczeń przed utworzeniem klastra usługi HDInsight z usługą Data Lake Store. Witaj nazwy głównej usługi należy utworzyć przy użyciu certyfikatu zgodnie z opisem w [Tworzenie nazwy głównej usługi o certyfikat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).
    >

## <a name="create-a-data-lake-store-account"></a>Tworzenie konta usługi Data Lake Store
Konto usługi Data Lake Store toocreate hello następujące:

1. Na pulpicie otwórz okno programu PowerShell, a następnie wprowadź poniższe fragmenty kodu hello. Jeśli jesteś zostanie wyświetlony monit o toosign w Zaloguj się jako jeden z administratorów subskrypcji hello lub właścicieli. 

        # Sign in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > Jeśli rejestrowanie dostawcy zasobów usługi Data Lake Store hello i komunikat o błędzie podobny zbyt`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, subskrypcja może nie być białej dla usługi Data Lake Store. tooenable subskrypcji platformy Azure hello usługi Data Lake Store publicznej wersji zapoznawczej, wykonaj te instrukcje hello [wprowadzenie do usługi Azure Data Lake Store za pomocą portalu Azure hello](data-lake-store-get-started-portal.md).
    >

2. Konto usługi Data Lake Store jest skojarzona z grupą zasobów platformy Azure. Rozpocznij od utworzenia grupy zasobów.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    Powinny pojawić się dane wyjściowe podobne to:

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. Utwórz konto usługi Data Lake Store. Konto Hello nazwa musi zawierać tylko małe litery i cyfry.

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    Powinny pojawić się dane wyjściowe podobne do następujących hello:

        ...
        ProvisioningState           : Succeeded
        State                       : Active
        CreationTime                : 5/5/2017 10:53:56 PM
        EncryptionState             : Enabled
        ...
        LastModifiedTime            : 5/5/2017 10:53:56 PM
        Endpoint                    : hdiadlstore.azuredatalakestore.net
        DefaultGroup                :
        Id                          : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp/providers/Microsoft.DataLakeStore/accounts/hdiadlstore
        Name                        : hdiadlstore
        Type                        : Microsoft.DataLakeStore/accounts
        Location                    : East US 2
        Tags                        : {}

4. Za pomocą usługi Data Lake Store jako domyślny magazyn wymaga toospecify możesz plików specyficznych dla klastra głównego ścieżki toowhich hello zostały skopiowane podczas tworzenia klastra. Ścieżka katalogu głównego, który jest toocreate **/klastrów/hdiadlcluster** we fragmencie hello, użyj następującego polecenia cmdlet hello:

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a>Konfigurowanie uwierzytelniania opartego na rolach dostępu tooData Lake — Magazyn
Każda subskrypcja platformy Azure jest skojarzony z jednostką usługi Azure AD. Użytkowników i usług, czy dostęp do zasobów subskrypcji przy użyciu portalu Azure hello lub hello interfejsu API usługi Azure Resource Manager muszą najpierw uwierzytelnić w usłudze Azure AD. Dostęp tooAzure subskrypcji i usług przez przypisywanie ich odpowiednią rolę hello na zasobów platformy Azure. W przypadku usług nazwy głównej usługi identyfikuje hello usługi w usłudze Azure AD.

W tej części przedstawiono, jak usługa toogrant aplikacji, takich jak usługi HDInsight, tooan dostępu do zasobów platformy Azure (hello utworzone wcześniej konto usługi Data Lake Store). Można to zrobić, tworząc usługi głównej aplikacji hello i przypisywania ról tooit za pomocą programu PowerShell.

tooset się uwierzytelnianie usługi Active Directory dla usługi Azure Data Lake wykonywanie zadań hello w hello następujące dwie sekcje.

### <a name="create-a-self-signed-certificate"></a>Utwórz certyfikat z podpisem własnym
Upewnij się, że masz [zestaw Windows SDK](https://dev.windows.com/en-us/downloads) zainstalowany przed rozpoczęciem powitalne kroki opisane w tej sekcji. Należy także utworzyć katalogu, takie jak *C:\mycertdir*, w którym można utworzyć certyfikatu hello.

1. W oknie programu PowerShell hello przejść toohello lokalizacji, w której zainstalowany zestaw Windows SDK (zazwyczaj *\Windows Kits\10\bin\x86 C:\Program Files (x86)*) i używać hello [MakeCert] [ makecert] toocreate narzędzie certyfikatu z podpisem własnym oraz klucza prywatnego. Witaj Użyj następującego polecenia:

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    Hasło klucza prywatnego hello zostanie wyświetlony monit o tooenter będzie. Po pomyślnym wykonaniu polecenia hello, powinien zostać wyświetlony **CertFile.cer** i **mykey.pvk** w katalogu certyfikatu hello określonym.
2. Użyj hello [Pvk2Pfx] [ pvk2pfx] .pvk hello tooconvert narzędzia i .cer pliki tego pliku pfx utworzony tooa MakeCert. Uruchom następujące polecenie hello:

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    Po wyświetleniu monitu wprowadź hello hasło klucza prywatnego określone wcześniej. wartość określona dla hello Hello **— po** parametru jest hello hasło skojarzone z pliku PFX hello. Po polecenie hello zostało pomyślnie ukończone, należy również wyświetlić **CertFile.pfx** w katalogu certyfikatu hello określonym.

### <a name="create-an-azure-ad-and-a-service-principal"></a>Tworzenie usługi Azure AD i nazwy głównej usługi
W tej sekcji Tworzenie nazwy głównej usługi dla aplikacji usługi Azure AD, przypisz nazwy głównej usługi roli toohello i Uwierzytelnij się jako nazwy głównej usługi hello zapewniając certyfikatu. toocreate aplikacji w usłudze Azure AD, uruchom następujące polecenia hello:

1. Wklej hello następującego polecenia cmdlet w oknie konsoli programu PowerShell hello. Upewnij się, tę wartość hello Określ hello **— Nazwa wyświetlana** właściwości jest unikatowa. Witaj wartości **— strona główna** i **- IdentiferUris** są symbole zastępcze i nie są weryfikowane.

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter hello password" # This is hello password you specified for hello .pfx file

        $certificatePFX = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($certificateFilePath, $password)

        $rawCertificateData = $certificatePFX.GetRawCertData()

        $credential = [System.Convert]::ToBase64String($rawCertificateData)

        $application = New-AzureRmADApplication `
            -DisplayName "HDIADL" `
            -HomePage "https://contoso.com" `
            -IdentifierUris "https://mycontoso.com" `
            -CertValue $credential  `
            -StartDate $certificatePFX.NotBefore  `
            -EndDate $certificatePFX.NotAfter

        $applicationId = $application.ApplicationId
2. Tworzenie nazwy głównej usługi za pomocą identyfikatora aplikacji hello

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. Udziel katalogu głównego usługi Data Lake Store toohello hello usługi dostępu głównej i wszystkich folderów hello hello ścieżki katalogu głównego, określony wcześniej. Użyj następującego polecenia cmdlet hello:

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-hello-default-storage"></a>Tworzenie klastra usługi HDInsight Linux z usługą Data Lake Store jako hello domyślny magazyn

W tej sekcji utworzysz klaster usługi HDInsight Hadoop Linux z usługą Data Lake Store jako hello domyślny magazyn. W tej wersji hello klastra usługi HDInsight i Data Lake — Magazyn musi być w hello tej samej lokalizacji.

1. Pobierz identyfikator dzierżawy subskrypcji hello i zapisać go toouse później.

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. Tworzenie klastra usługi HDInsight hello za pomocą następującego polecenia cmdlet hello:

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster `
               -ClusterType Hadoop `
               -OSType Linux `
               -ClusterSizeInNodes $clusterNodes `
               -ResourceGroupName $resourceGroupName `
               -ClusterName $clusterName `
               -HttpCredential $httpCredentials `
               -Location $location `
               -DefaultStorageAccountType AzureDataLakeStore `
               -DefaultStorageAccountName "$storageAccountName.azuredatalakestore.net" `
               -DefaultStorageRootPath $storageRootPath `
               -Version "3.6" `
               -SshCredential $sshCredentials `
               -AadTenantId $tenantId `
               -ObjectId $objectId `
               -CertificateFilePath $certificateFilePath `
               -CertificatePassword $password

    Po pomyślnym zakończeniu hello polecenia cmdlet powinny być widoczne dane wyjściowe z listą hello szczegółów klastra.

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-data-lake-store"></a>Uruchom zadania testowe na toouse klastra usługi HDInsight hello usługi Data Lake Store
Po skonfigurowaniu klastra usługi HDInsight można uruchomić zadania testowe na nim tooensure, że można uzyskać dostępu do usługi Data Lake Store. toodo tak, uruchom toocreate zadania Hive przykładowej tabeli, która używa hello przykładowych danych, który jest już dostępne w usłudze Data Lake Store w  *<cluster root>/example/data/sample.log*.

W tej sekcji należy utworzyć połączenie Secure Shell (SSH) do hello utworzonego klastra usługi HDInsight w systemie Linux, a następnie uruchom przykładowe zapytanie Hive.

* Jeśli korzystasz z systemu Windows klienta toomake połączenie SSH do klastra hello, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight z systemu Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Jeśli korzystasz z systemu Linux toomake klienta połączenia SSH do klastra hello, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight w systemie Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).

1. Po dokonaniu hello połączenia, należy uruchomić hello gałąź o interfejsu wiersza polecenia (CLI) przy użyciu hello następujące polecenie:

        hive
2. Użyj hello CLI tooenter hello następujące instrukcje toocreate nowej tabeli o nazwie **pojazdów** przy użyciu hello przykładowych danych w usłudze Data Lake Store:

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    W konsoli SSH hello powinna zostać wyświetlona hello wyników zapytania.

    >[!NOTE]
    >Witaj ścieżki toohello przykładowe dane w hello poprzedzających polecenia CREATE TABLE jest `adl:///example/data/`, gdzie `adl:///` jest hello klastra głównego. Następujący przykład hello hello głównego klastra, który jest określony w tym samouczku, polecenie hello jest `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`. Można użyć zamiast krótszą hello lub podaj hello pełną ścieżkę toohello klastra głównego.
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a>Dostęp do usługi Data Lake Store za pomocą poleceń systemu plików HDFS
Po skonfigurowaniu hello HDInsight klastra toouse Data Lake Store, można użyć systemu plików rozproszonych Hadoop (HDFS) powłoki poleceń tooaccess hello magazynu.

W tej sekcji podczas nawiązywania połączenia SSH do hello utworzonego klastra usługi HDInsight w systemie Linux, a następnie uruchom hello poleceń systemu plików HDFS.

* Jeśli korzystasz z systemu Windows klienta toomake połączenie SSH do klastra hello, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight z systemu Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Jeśli korzystasz z systemu Linux toomake klienta połączenia SSH do klastra hello, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight w systemie Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).

Po utworzeniu połączenia hello, listy hello plików w usłudze Data Lake Store za pomocą następującego polecenia systemu plików HDFS hello.

    hdfs dfs -ls adl:///

Można również użyć hello `hdfs dfs -put` polecenia tooupload niektóre pliki tooData Lake — magazyn, a następnie użyj `hdfs dfs -ls` tooverify czy hello pliki zostały pomyślnie przekazane.

## <a name="see-also"></a>Zobacz też
* [Portalu Azure: Utwórz toouse klastra usługi HDInsight usługi Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
