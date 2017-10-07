---
title: aaa "środowiska PowerShell: klaster Azure HDInsight z usługi Data Lake Store jako magazyn dodatków | Usługi Microsoft Docs": documentationcenter hdinsight dane lake — Magazyn:" Autor: nitinme Menedżera: Edytor jhubbard: cgronlun

MS.AssetID: 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service: ms.devlang data lake magazynu: na ms.topic: artykuł ms.tgt_pltfrm: na ms.workload: danych big data ms.date: ms.author 06/08/2017: nitinme

---
# <a name="use-azure-powershell-toocreate-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a>Użyj programu Azure PowerShell toocreate klastra usługi HDInsight z usługą Data Lake Store (jako dodatkowego magazynu)
> [!div class="op_single_selector"]
> * [Korzystanie z portalu](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Przy użyciu programu PowerShell (do magazynu domyślnego)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Przy użyciu programu PowerShell (dla dodatkowego magazynu)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Za pomocą Menedżera zasobów](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Dowiedz się, jak klaster toouse tooconfigure programu PowerShell usługi Azure HDInsight z usługi Azure Data Lake Store, **jako dodatkowego magazynu**. Aby uzyskać instrukcje dotyczące sposobu toocreate HDInsight klaster z usługi Azure Data Lake Store jako domyślnego magazynu, zobacz [tworzenia klastra usługi HDInsight z usługą Data Lake Store jako domyślny magazyn](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).

> [!NOTE]
> Jeśli zamierzasz toouse Azure Data Lake Store jako dodatkowego magazynu dla klastra usługi HDInsight, zdecydowanie zaleca się to zrobić podczas tworzenia klastra hello zgodnie z opisem w tym artykule. Dodawanie usługi Azure Data Lake Store jako dodatkowego magazynu tooan istniejącym klastrze usługi HDInsight to skomplikowany proces i tooerrors podatnych na błędy.
>

Dla typów obsługiwanych klastra usługi Data Lake Store może służyć jako domyślnego magazynu lub konto dodatkowego miejsca do magazynowania. W przypadku usługi Data Lake Store jako dodatkowego magazynu hello domyślne konto magazynu dla klastrów hello będzie nadal Azure blob Storage (WASB) i hello plików związanych z klastrem (takich jak dzienniki, itp.) są zapisywane nadal toohello domyślny magazyn, podczas danych hello które Chcę tooprocess mogą być przechowywane w ramach konta usługi Data Lake Store. Za pomocą usługi Data Lake Store jako dodatkowego magazynu konta nie wpływa na wydajność lub pamięć masową toohello tooread/zapisu możliwości hello z hello klastra.

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a>W magazynie klastra usługi HDInsight przy użyciu usługi Data Lake Store

Poniżej przedstawiono kilka istotnych kwestii dotyczących z usługą Data Lake Store za pomocą usługi HDInsight:

* Klastry HDInsight toocreate opcji z dostępem do tooData Lake Store jako dodatkowego magazynu jest dostępna dla usługi HDInsight w wersji 3.2, 3.4, 3.5 i 3,6.

Konfigurowanie usługi HDInsight toowork z Data Lake Store za pomocą programu PowerShell obejmuje hello następujące kroki:

* Tworzenie usługi Azure Data Lake Store
* Konfigurowanie uwierzytelniania opartego na rolach dostępu tooData Lake — Magazyn
* Tworzenie klastra usługi HDInsight z usługą uwierzytelniania tooData Lake Store
* Uruchom zadanie testowe w klastrze hello

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego samouczka wymagane są następujące hello:

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Program Azure PowerShell 1.0 lub nowszy**. Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).
* **Zestaw Windows SDK**. Możesz zainstalować ją z [tutaj](https://dev.windows.com/en-us/downloads). Możesz użyć tego toocreate certyfikatu zabezpieczeń.
* **Nazwy głównej usługi Azure Active Directory usługi**. Kroki opisane w tym samouczku zawierają instrukcje na temat toocreate nazwy głównej usługi w usłudze Azure AD. Jednak należy usługi Azure AD administratora toobe stanie toocreate nazwy głównej usługi. Jeśli jesteś administratorem usługi Azure AD, możesz pominąć te wymagania wstępne i kontynuować hello samouczka.

    **Jeśli nie jesteś administratorem usługi Azure AD**, nie będą mogli tooperform hello kroki wymagane toocreate nazwy głównej usługi. W takim przypadku administrator usługi Azure AD należy najpierw utworzyć nazwy głównej usługi przed utworzeniem klastra usługi HDInsight z usługą Data Lake Store. Także hello nazwy głównej usługi muszą zostać utworzone za pomocą certyfikatu, zgodnie z opisem w [Tworzenie nazwy głównej usługi o certyfikat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).

## <a name="create-an-azure-data-lake-store"></a>Tworzenie usługi Azure Data Lake Store
Wykonaj te kroki toocreate usługi Data Lake Store.

1. Na pulpicie otwórz nowe okno programu Azure PowerShell, a następnie wprowadź hello następującego fragmentu. Gdy zostanie wyświetlony monit o toolog, upewnij się, że logujesz się jako jeden właściciel administratora subskrypcji hello:

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > Jeśli zostanie wyświetlony błąd podobny zbyt`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` podczas rejestrowania dostawcy zasobów usługi Data Lake Store hello, istnieje możliwość, że Twoja subskrypcja nie jest białej dla usługi Azure Data Lake Store. Upewnij się, że Włącz subskrypcji platformy Azure dla publicznej wersji zapoznawczej usługi Data Lake Store wykonując te [instrukcje](data-lake-store-get-started-portal.md).
   >
   >
2. Konto usługi Azure Data Lake Store jest skojarzone z grupą zasobów platformy Azure. Rozpocznij od utworzenia grupy zasobów platformy Azure.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    Powinny pojawić się dane wyjściowe podobne to:

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. Utwórz konto usługi Azure Data Lake Store. Konto Hello się, że nazwa użytkownika musi zawierać tylko małe litery i cyfry.

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

5. Przekaż niektóre przykładowe dane tooAzure usługi Data Lake. Użyjemy w dalszej części tego tooverify artykułu, czy dane hello jest dostępny z klastra usługi HDInsight. Jeśli szukasz niektórych tooupload dane przykładowe, możesz pobrać hello **Ambulance Data** folderu z hello [repozytorium Git programu Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path toodata>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a>Konfigurowanie uwierzytelniania opartego na rolach dostępu tooData Lake — Magazyn
Każda subskrypcja platformy Azure jest skojarzony z usługą Azure Active Directory. Użytkowników i usług, które uzyskują dostęp do zasobów przy użyciu hello klasycznego portalu Azure lub interfejsu API usługi Azure Resource Manager subskrypcji hello muszą najpierw zostać uwierzytelnione z tej usługi Azure Active Directory. Dostęp tooAzure subskrypcji i usług przez przypisywanie ich odpowiednią rolę hello na zasobów platformy Azure.  W przypadku usług nazwy głównej usługi identyfikuje usługi hello w hello Azure Active Directory (AAD). W tej części przedstawiono, jak usługa toogrant aplikacji, takich jak usługa HDInsight, tooan dostępu do zasobów platformy Azure (hello utworzonego wcześniej konta usługi Azure Data Lake Store) przez tworzenie nazwy głównej usługi dla aplikacji hello i przypisywanie ról toothat za pośrednictwem usługi Azure Środowiska PowerShell.

tooset się uwierzytelnianie usługi Active Directory dla usługi Azure Data Lake, należy wykonać następujące zadania hello.

* Utwórz certyfikat z podpisem własnym
* Tworzenie aplikacji w usłudze Azure Active Directory i nazwy głównej usługi

### <a name="create-a-self-signed-certificate"></a>Utwórz certyfikat z podpisem własnym
Upewnij się, że masz [zestaw Windows SDK](https://dev.windows.com/en-us/downloads) zainstalowany przed rozpoczęciem powitalne kroki opisane w tej sekcji. Należy także utworzyć katalogu, takie jak **C:\mycertdir**, w której zostanie utworzona hello certyfikatu.

1. W oknie programu PowerShell hello Przejdź toohello lokalizacji, w której zainstalowany zestaw Windows SDK (zazwyczaj `C:\Program Files (x86)\Windows Kits\10\bin\x86` i użyj hello [MakeCert] [ makecert] toocreate narzędzie certyfikatu z podpisem własnym i klucz prywatny. Użyj następującego polecenia hello.

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    Hasło klucza prywatnego hello zostanie wyświetlony monit o tooenter będzie. Po hello polecenie zostało wykonane pomyślnie, powinien zostać wyświetlony **CertFile.cer** i **mykey.pvk** w katalogu certyfikatu hello określona.
2. Użyj hello [Pvk2Pfx] [ pvk2pfx] .pvk hello tooconvert narzędzia i .cer pliki tego pliku pfx utworzony tooa MakeCert. Uruchom następujące polecenie hello.

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    Po wyświetleniu monitu wprowadź hasło klucza z prywatnego hello określone wcześniej. wartość określona dla hello Hello **— po** hello hasło skojarzone z plikiem PFX hello jest parametr. Po pomyślnym zakończeniu hello polecenia, zobacz też CertFile.pfx w katalogu certyfikatu hello, określona.

### <a name="create-an-azure-active-directory-and-a-service-principal"></a>Tworzenie usługi Azure Active Directory i nazwy głównej usługi
W tej sekcji wykonać hello kroki toocreate nazwy głównej usługi dla aplikacji usługi Azure Active Directory, przypisać nazwy głównej usługi roli toohello i Uwierzytelnij się jako nazwy głównej usługi hello zapewniając certyfikatu. Uruchom następujące polecenia toocreate hello aplikacji w usłudze Azure Active Directory.

1. Wklej hello następującego polecenia cmdlet w oknie konsoli programu PowerShell hello. Upewnij się, że wartość hello określona dla hello **— Nazwa wyświetlana** właściwości jest unikatowa. Ponadto hello wartości **— strona główna** i **- IdentiferUris** są symbole zastępcze i nie są weryfikowane.

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
2. Tworzenie nazwy głównej usługi przy użyciu identyfikatora hello aplikacji.

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. Udziel hello usługi głównej dostępu toohello usługi Data Lake Store folderu i pliku hello, dostępnej z klastrem usługi HDInsight hello. Poniższy fragment Hello zapewnia dostęp głównym toohello hello Data Lake Store konta (którego skopiowano hello przykładowy plik danych) i hello sam plik.

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a>Tworzenie klastra usługi HDInsight Linux z usługą Data Lake Store jako dodatkowego miejsca do magazynowania

W tej sekcji utworzymy klastra usługi HDInsight Hadoop Linux z usługą Data Lake Store jako dodatkowego magazynu. W tej wersji hello klaster usługi HDInsight i hello Data Lake — Magazyn musi być w hello tej samej lokalizacji.

1. Zaczynać się podczas pobierania identyfikatora hello subskrypcji dzierżawcy. Który będzie potrzebny później.

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. W tej wersji dla klastra usługi Hadoop, Data Lake Store można użyć tylko jako dodatkowego magazynu hello klastra. Witaj domyślnego magazynu będą nadal hello blob magazynu Azure (WASB). Tak najpierw utworzymy hello kontenery konta i przechowywania magazynu wymaganych dla klastra hello.

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. Tworzenie klastra usługi HDInsight hello. Użyj następującego polecenia cmdlet hello.

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have hello same name for hello cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    Po pomyślnym zakończeniu hello polecenia cmdlet, powinny zostać wyświetlone dane wyjściowe, wyświetlania szczegółów klastra hello.


## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a>Uruchom zadania testowe na powitania HDInsight klastra toouse hello usługi Data Lake Store
Po skonfigurowaniu klastra usługi HDInsight można uruchamiać zadania testowego na powitania klastra tootest tego hello HDInsight klastra mogą uzyskiwać dostęp do usługi Data Lake Store. toodo tak, zostanie uruchomiony przykładowe zadania Hive, która tworzy tabelę przy użyciu hello przykładowych danych, aby przekazać wcześniejszych tooyour Data Lake Store.

W tej sekcji do klastra HDInsight Linux, możesz utworzyć i uruchomić przykładowe zapytanie Hive hello hello będzie SSH.

* Jeśli używasz tooSSH klienta systemu Windows do klastra hello, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight z systemu Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Jeśli używasz tooSSH klient systemu Linux w klastrze hello, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight z systemu Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)

1. Po nawiązaniu połączenia, należy uruchomić hello Hive interfejsu wiersza polecenia przy użyciu hello następujące polecenie:

        hive
2. Używając hello interfejsu wiersza polecenia, wprowadź następujące instrukcje toocreate nowej tabeli o nazwie hello **pojazdów** przy użyciu hello przykładowe dane w hello usługi Data Lake Store:

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    Powinny być widoczne następujące dane wyjściowe podobne toohello:

        1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
        1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
        1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
        1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
        1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
        1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
        1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
        1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
        1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
        1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1

## <a name="access-data-lake-store-using-hdfs-commands"></a>Dostęp Data Lake Store za pomocą poleceń systemu plików HDFS
Po skonfigurowaniu hello HDInsight klastra toouse Data Lake Store można użyć hello systemu plików HDFS powłoki poleceń tooaccess hello magazynu.

W tej sekcji do klastra HDInsight Linux, możesz utworzyć i uruchamiania poleceń systemu plików HDFS hello hello będzie SSH.

* Jeśli używasz tooSSH klienta systemu Windows do klastra hello, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight z systemu Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Jeśli używasz tooSSH klient systemu Linux w klastrze hello, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight z systemu Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)

Po nawiązaniu połączenia użyj hello następujące pliki poleceń systemu plików HDFS hello toolist w hello usługi Data Lake Store.

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

Powinny pojawić się plik hello czy przesłany wcześniejszych toohello Data Lake Store.

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

Można również użyć hello `hdfs dfs -put` polecenia tooupload toohello niektórych plików usługi Data Lake Store, a następnie użyj `hdfs dfs -ls` tooverify czy hello pliki zostały pomyślnie przekazane.

## <a name="see-also"></a>Zobacz też
* [Portal: Tworzenie toouse klastra usługi HDInsight usługi Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
