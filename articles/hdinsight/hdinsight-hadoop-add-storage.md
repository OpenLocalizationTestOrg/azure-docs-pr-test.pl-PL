---
title: dodatkowy magazyn Azure aaaAdd kont tooHDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak dodatkowy magazyn Azure tooadd kont tooan istniejącym klastrze usługi HDInsight."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: ce5acfa4b61bf7e83b1fb374d64a1eaa3182fbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-additional-storage-accounts-toohdinsight"></a><span data-ttu-id="31193-103">Dodaj dodatkowy magazyn kont tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="31193-103">Add additional storage accounts tooHDInsight</span></span>

<span data-ttu-id="31193-104">Dowiedz się, jak konta tooHDInsight toouse skryptu akcje tooadd dodatkowe Azure magazynu.</span><span class="sxs-lookup"><span data-stu-id="31193-104">Learn how toouse script actions tooadd additional Azure storage accounts tooHDInsight.</span></span> <span data-ttu-id="31193-105">Witaj kroki opisane w tym dokumencie dodać magazynu konta tooan istniejących HDInsight opartych na systemie Linux klaster.</span><span class="sxs-lookup"><span data-stu-id="31193-105">hello steps in this document add a storage account tooan existing Linux-based HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31193-106">Witaj informacje w tym dokumencie jest o dodawaniu klastra tooa dodatkowego miejsca do magazynowania po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="31193-106">hello information in this document is about adding additional storage tooa cluster after it has been created.</span></span> <span data-ttu-id="31193-107">Aby uzyskać informacje na temat dodawania konta magazynu podczas tworzenia klastra, zobacz [Ustawianie klastrów w usłudze HDInsight Hadoop, Spark, Kafka i](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="31193-107">For information on adding storage accounts during cluster creation, see [Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="how-it-works"></a><span data-ttu-id="31193-108">Jak to działa</span><span class="sxs-lookup"><span data-stu-id="31193-108">How it works</span></span>

<span data-ttu-id="31193-109">Ten skrypt wykonuje hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="31193-109">This script takes hello following parameters:</span></span>

* <span data-ttu-id="31193-110">__Nazwa konta magazynu Azure__: hello nazwę klastra usługi HDInsight toohello tooadd hello magazynu konta.</span><span class="sxs-lookup"><span data-stu-id="31193-110">__Azure storage account name__: hello name of hello storage account tooadd toohello HDInsight cluster.</span></span> <span data-ttu-id="31193-111">Po uruchomieniu skryptu hello, HDInsight można odczytu i zapisu, dane przechowywane na tym koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="31193-111">After running hello script, HDInsight can read and write data stored in this storage account.</span></span>

* <span data-ttu-id="31193-112">__Klucz konta magazynu Azure__: klucz, który daje konta magazynu toohello dostępu.</span><span class="sxs-lookup"><span data-stu-id="31193-112">__Azure storage account key__: A key that grants access toohello storage account.</span></span>

* <span data-ttu-id="31193-113">__-p__ (opcjonalnie): Jeśli zostanie określona, hello klucza nie są szyfrowane i są przechowywane w pliku core-site.xml hello jako zwykły tekst.</span><span class="sxs-lookup"><span data-stu-id="31193-113">__-p__ (optional): If specified, hello key is not encrypted and is stored in hello core-site.xml file as plain text.</span></span>

<span data-ttu-id="31193-114">Podczas przetwarzania skryptu hello wykonuje hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="31193-114">During processing, hello script performs hello following actions:</span></span>

* <span data-ttu-id="31193-115">Jeśli hello konto magazynu już istnieje w konfiguracji core-site.xml hello hello klastra, hello skrypt zakończy pracę, i są wykonywane żadne dalsze akcje.</span><span class="sxs-lookup"><span data-stu-id="31193-115">If hello storage account already exists in hello core-site.xml configuration for hello cluster, hello script exits and no further actions are performed.</span></span>

* <span data-ttu-id="31193-116">Sprawdza, czy konto magazynu hello istnieje i czy jest możliwy przy użyciu klucza hello.</span><span class="sxs-lookup"><span data-stu-id="31193-116">Verifies that hello storage account exists and can be accessed using hello key.</span></span>

* <span data-ttu-id="31193-117">Szyfruje klucz hello przy użyciu poświadczeń klastra hello.</span><span class="sxs-lookup"><span data-stu-id="31193-117">Encrypts hello key using hello cluster credential.</span></span>

* <span data-ttu-id="31193-118">Dodaje pliku core-site.xml toohello konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="31193-118">Adds hello storage account toohello core-site.xml file.</span></span>

* <span data-ttu-id="31193-119">Zatrzymuje i uruchamia ponownie usługi hello Oozie, YARN MapReduce2 i system plików HDFS.</span><span class="sxs-lookup"><span data-stu-id="31193-119">Stops and restarts hello Oozie, YARN, MapReduce2, and HDFS services.</span></span> <span data-ttu-id="31193-120">Zatrzymywanie i uruchamianie tych usług umożliwia im toouse hello nowe konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="31193-120">Stopping and starting these services allows them toouse hello new storage account.</span></span>

> [!WARNING]
> <span data-ttu-id="31193-121">Używanie konta magazynu w innej lokalizacji niż hello klastra usługi HDInsight nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="31193-121">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span>

## <a name="hello-script"></a><span data-ttu-id="31193-122">Witaj skryptu</span><span class="sxs-lookup"><span data-stu-id="31193-122">hello script</span></span>

<span data-ttu-id="31193-123">__Lokalizacja skryptu__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="31193-123">__Script location__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span></span>

<span data-ttu-id="31193-124">__Wymagania dotyczące__:</span><span class="sxs-lookup"><span data-stu-id="31193-124">__Requirements__:</span></span>

* <span data-ttu-id="31193-125">Witaj skryptu muszą być stosowane na powitania __węzły główne__.</span><span class="sxs-lookup"><span data-stu-id="31193-125">hello script must be applied on hello __Head nodes__.</span></span>

## <a name="toouse-hello-script"></a><span data-ttu-id="31193-126">toouse hello skryptu</span><span class="sxs-lookup"><span data-stu-id="31193-126">toouse hello script</span></span>

<span data-ttu-id="31193-127">Ten skrypt można używać z hello portalu Azure, programu Azure PowerShell lub hello Azure CLI w wersji 1.0.</span><span class="sxs-lookup"><span data-stu-id="31193-127">This script can be used from hello Azure portal, Azure PowerShell, or hello Azure CLI 1.0.</span></span> <span data-ttu-id="31193-128">Aby uzyskać więcej informacji, zobacz hello [klastrów usługi HDInsight opartej na dostosowanie systemu Linux przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="31193-128">For more information, see hello [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31193-129">Podczas korzystania z hello z krokami opisanymi w dokumencie dostosowania hello, należy używać hello następujące informacje tooapply ten skrypt:</span><span class="sxs-lookup"><span data-stu-id="31193-129">When using hello steps provided in hello customization document, use hello following information tooapply this script:</span></span>
>
> * <span data-ttu-id="31193-130">Zastąp żadnych akcji skryptu przykład URI hello identyfikatora URI dla tego skryptu (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="31193-130">Replace any example script action URI with hello URI for this script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span></span>
> * <span data-ttu-id="31193-131">Parametry przykład zastąpić nazwę konta magazynu Azure hello i klucz hello magazynu konta toobe dodano toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="31193-131">Replace any example parameters with hello Azure storage account name and key of hello storage account toobe added toohello cluster.</span></span> <span data-ttu-id="31193-132">Jeśli przy użyciu hello portalu Azure, te parametry muszą być oddzielone spacją.</span><span class="sxs-lookup"><span data-stu-id="31193-132">If using hello Azure portal, these parameters must be separated by a space.</span></span>
> * <span data-ttu-id="31193-133">Nie trzeba toomark ten skrypt jako __Persisted__, bezpośrednio aktualizacji konfiguracji Ambari hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="31193-133">You do not need toomark this script as __Persisted__, as it directly updates hello Ambari configuration for hello cluster.</span></span>

## <a name="known-issues"></a><span data-ttu-id="31193-134">Znane problemy</span><span class="sxs-lookup"><span data-stu-id="31193-134">Known issues</span></span>

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a><span data-ttu-id="31193-135">Konta magazynu nie są wyświetlane w portalu Azure lub narzędzia</span><span class="sxs-lookup"><span data-stu-id="31193-135">Storage accounts not displayed in Azure portal or tools</span></span>

<span data-ttu-id="31193-136">Podczas wyświetlania hello HDInsight klaster na powitania portalu Azure, wybierając hello __kont magazynu__ wpis w __właściwości__ kont magazynu dodanego przez tę akcję skryptu nie są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="31193-136">When viewing hello HDInsight cluster in hello Azure portal, selecting hello __Storage Accounts__ entry under __Properties__ does not display storage accounts added through this script action.</span></span> <span data-ttu-id="31193-137">Azure PowerShell i interfejsu wiersza polecenia Azure nie są wyświetlane konta magazynu dodatkowe hello albo.</span><span class="sxs-lookup"><span data-stu-id="31193-137">Azure PowerShell and Azure CLI do not display hello additional storage account either.</span></span>

<span data-ttu-id="31193-138">Hello magazynu informacji nie są wyświetlane, ponieważ skrypt hello tylko Modyfikuje konfigurację core-site.xml hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="31193-138">hello storage information isn't displayed because hello script only modifies hello core-site.xml configuration for hello cluster.</span></span> <span data-ttu-id="31193-139">Te informacje nie jest używany podczas pobierania informacji klastra hello za pomocą interfejsów API zarządzania platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="31193-139">This information is not used when retrieving hello cluster information using Azure management APIs.</span></span>

<span data-ttu-id="31193-140">informacje o koncie magazynu tooview dodać toohello klastra przy użyciu tego skryptu, użyj hello interfejsu API REST Ambari.</span><span class="sxs-lookup"><span data-stu-id="31193-140">tooview storage account information added toohello cluster using this script, use hello Ambari REST API.</span></span> <span data-ttu-id="31193-141">Użyj następującego polecenia tooretrieve hello te informacje dla klastra:</span><span class="sxs-lookup"><span data-stu-id="31193-141">Use hello following commands tooretrieve this information for your cluster:</span></span>

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter hello cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> <span data-ttu-id="31193-142">Ustaw `$clusterName` toohello nazwę hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="31193-142">Set `$clusterName` toohello name of hello HDInsight cluster.</span></span> <span data-ttu-id="31193-143">Ustaw `$storageAccountName` nazwa toohello hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="31193-143">Set `$storageAccountName` toohello name of hello storage account.</span></span> <span data-ttu-id="31193-144">Po wyświetleniu monitu wprowadź hello logowania do klastra (admin) i hasło.</span><span class="sxs-lookup"><span data-stu-id="31193-144">When prompted, enter hello cluster login (admin) and password.</span></span>

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> <span data-ttu-id="31193-145">Ustaw `$PASSWORD` toohello hasło do konta logowania (Administrator) klastra.</span><span class="sxs-lookup"><span data-stu-id="31193-145">Set `$PASSWORD` toohello cluster login (admin) account password.</span></span> <span data-ttu-id="31193-146">Ustaw `$CLUSTERNAME` toohello nazwę hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="31193-146">Set `$CLUSTERNAME` toohello name of hello HDInsight cluster.</span></span> <span data-ttu-id="31193-147">Ustaw `$STORAGEACCOUNTNAME` nazwa toohello hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="31193-147">Set `$STORAGEACCOUNTNAME` toohello name of hello storage account.</span></span>
>
> <span data-ttu-id="31193-148">W tym przykładzie użyto [curl (http://curl.haxx.se/)](http://curl.haxx.se/) i [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve i analizy danych JSON.</span><span class="sxs-lookup"><span data-stu-id="31193-148">This example uses [curl (http://curl.haxx.se/)](http://curl.haxx.se/) and [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve and parse JSON data.</span></span>

<span data-ttu-id="31193-149">Korzystając z tego polecenia, Zastąp __CLUSTERNAME__ o nazwie hello hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="31193-149">When using this command, replace __CLUSTERNAME__ with hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="31193-150">Zastąp __hasło__ hasłem logowania hello HTTP hello klastra.</span><span class="sxs-lookup"><span data-stu-id="31193-150">Replace __PASSWORD__ with hello HTTP login password for hello cluster.</span></span> <span data-ttu-id="31193-151">Zastąp __STORAGEACCOUNT__ hello nazwę konta magazynu hello dodane przy użyciu akcji skryptu.</span><span class="sxs-lookup"><span data-stu-id="31193-151">Replace __STORAGEACCOUNT__ with hello name of hello storage account added using script action.</span></span> <span data-ttu-id="31193-152">Informacje zwrócone z tego polecenia zostanie wyświetlony podobne toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="31193-152">Information returned from this command appears similar toohello following text:</span></span>

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

<span data-ttu-id="31193-153">Ten tekst jest przykładem zaszyfrowanego klucza, który jest używany tooaccess hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="31193-153">This text is an example of an encrypted key, which is used tooaccess hello storage account.</span></span>

### <a name="unable-tooaccess-storage-after-changing-key"></a><span data-ttu-id="31193-154">Magazyn tooaccess po zmianie klucza</span><span class="sxs-lookup"><span data-stu-id="31193-154">Unable tooaccess storage after changing key</span></span>

<span data-ttu-id="31193-155">Jeśli zmienisz hello klucza dla konta magazynu usługi HDInsight dłużej korzystać z konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="31193-155">If you change hello key for a storage account, HDInsight can no longer access hello storage account.</span></span> <span data-ttu-id="31193-156">HDInsight używa pamięci podręcznej kopię klucza hello core-site.xml hello klastra.</span><span class="sxs-lookup"><span data-stu-id="31193-156">HDInsight uses a cached copy of key in hello core-site.xml for hello cluster.</span></span> <span data-ttu-id="31193-157">Ta kopia pamięci podręcznej musi być zaktualizowany toomatch hello nowy klucz.</span><span class="sxs-lookup"><span data-stu-id="31193-157">This cached copy must be updated toomatch hello new key.</span></span>

<span data-ttu-id="31193-158">Uruchomienie akcji skryptu hello ponownie jest __nie__ zaktualizować klucz hello jako hello skrypt sprawdza toosee, jeśli istnieje już wpis dla konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="31193-158">Running hello script action again does __not__ update hello key, as hello script checks toosee if an entry for hello storage account already exists.</span></span> <span data-ttu-id="31193-159">Jeżeli wpis już istnieje, nie powoduje żadnych zmian.</span><span class="sxs-lookup"><span data-stu-id="31193-159">If an entry already exists, it does not make any changes.</span></span>

<span data-ttu-id="31193-160">toowork rozwiązać ten problem, należy usunąć istniejący wpis hello hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="31193-160">toowork around this problem, you must remove hello existing entry for hello storage account.</span></span> <span data-ttu-id="31193-161">Użyj hello następujące kroki tooremove hello istniejący wpis:</span><span class="sxs-lookup"><span data-stu-id="31193-161">Use hello following steps tooremove hello existing entry:</span></span>

1. <span data-ttu-id="31193-162">W przeglądarce sieci web Otwórz hello Interfejsu sieci Web Ambari dla klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="31193-162">In a web browser, open hello Ambari Web UI for your HDInsight cluster.</span></span> <span data-ttu-id="31193-163">Witaj identyfikatora URI jest https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="31193-163">hello URI is https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="31193-164">Zastąp __CLUSTERNAME__ o nazwie hello klastra.</span><span class="sxs-lookup"><span data-stu-id="31193-164">Replace __CLUSTERNAME__ with hello name of your cluster.</span></span>

    <span data-ttu-id="31193-165">Po wyświetleniu monitu wprowadź hello HTTP logowania użytkownika i hasło dla klastra.</span><span class="sxs-lookup"><span data-stu-id="31193-165">When prompted, enter hello HTTP login user and password for your cluster.</span></span>

2. <span data-ttu-id="31193-166">Wybierz z listy hello usług na powitania po lewej stronie powitania __HDFS__.</span><span class="sxs-lookup"><span data-stu-id="31193-166">From hello list of services on hello left of hello page, select __HDFS__.</span></span> <span data-ttu-id="31193-167">Następnie wybierz hello __Configs__ kartę w Centrum hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="31193-167">Then select hello __Configs__ tab in hello center of hello page.</span></span>

3. <span data-ttu-id="31193-168">W hello __filtru...__  wprowadź wartość __fs.azure.account__.</span><span class="sxs-lookup"><span data-stu-id="31193-168">In hello __Filter...__ field, enter a value of __fs.azure.account__.</span></span> <span data-ttu-id="31193-169">To polecenie zwróci wpisy dla wszystkich kont dodatkowego miejsca do magazynowania, które zostały dodane toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="31193-169">This returns entries for any additional storage accounts that have been added toohello cluster.</span></span> <span data-ttu-id="31193-170">Istnieją dwa typy wpisy. __keyprovider__ i __klucza__.</span><span class="sxs-lookup"><span data-stu-id="31193-170">There are two types of entries; __keyprovider__ and __key__.</span></span> <span data-ttu-id="31193-171">Zawierają hello nazwę konta magazynu hello jako część nazwy klucza hello.</span><span class="sxs-lookup"><span data-stu-id="31193-171">Both contain hello name of hello storage account as part of hello key name.</span></span>

    <span data-ttu-id="31193-172">Witaj poniżej przedstawiono przykładowe wpisy dla konta magazynu o nazwie __mystorage__:</span><span class="sxs-lookup"><span data-stu-id="31193-172">hello following are example entries for a storage account named __mystorage__:</span></span>

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. <span data-ttu-id="31193-173">Po zidentyfikowaniu hello kluczy dla konta magazynu hello należy tooremove za pomocą hello red "-" toohello ikona rogu hello wpis toodelete go.</span><span class="sxs-lookup"><span data-stu-id="31193-173">After you have identified hello keys for hello storage account you need tooremove, use hello red '-' icon toohello right of hello entry toodelete it.</span></span> <span data-ttu-id="31193-174">Następnie użyj hello __zapisać__ przycisk toosave zmiany.</span><span class="sxs-lookup"><span data-stu-id="31193-174">Then use hello __Save__ button toosave your changes.</span></span>

5. <span data-ttu-id="31193-175">Po zapisaniu zmian, użyj konta magazynu hello tooadd hello skryptu akcji i nowym klastrze toohello wartość klucza.</span><span class="sxs-lookup"><span data-stu-id="31193-175">After changes have been saved, use hello script action tooadd hello storage account and new key value toohello cluster.</span></span>

### <a name="poor-performance"></a><span data-ttu-id="31193-176">Niska wydajność</span><span class="sxs-lookup"><span data-stu-id="31193-176">Poor performance</span></span>

<span data-ttu-id="31193-177">Jeśli konto magazynu hello znajduje się w regionie innym niż klaster usługi HDInsight hello, może wystąpić pogorszenie wydajności.</span><span class="sxs-lookup"><span data-stu-id="31193-177">If hello storage account is in a different region than hello HDInsight cluster, you may experience poor performance.</span></span> <span data-ttu-id="31193-178">Podczas uzyskiwania dostępu do danych w innym regionie wysyła ruch sieciowy poza centrum danych Azure regionalnych hello i wielu hello publicznej sieci internet, który może powodować opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="31193-178">Accessing data in a different region sends network traffic outside hello regional Azure data center and across hello public internet, which can introduce latency.</span></span>

> [!WARNING]
> <span data-ttu-id="31193-179">Używanie konta magazynu w regionie innym niż klaster usługi HDInsight hello nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="31193-179">Using a storage account in a different region than hello HDInsight cluster is not supported.</span></span>

### <a name="additional-charges"></a><span data-ttu-id="31193-180">Dodatkowe opłaty.</span><span class="sxs-lookup"><span data-stu-id="31193-180">Additional charges</span></span>

<span data-ttu-id="31193-181">W przypadku konta magazynu hello w innym regionie niż hello klastra usługi HDInsight, opłaty za wyjście dodatkowe mogą pojawić się na Azure rozliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="31193-181">If hello storage account is in a different region than hello HDInsight cluster, you may notice additional egress charges on your Azure billing.</span></span> <span data-ttu-id="31193-182">Dodatkowy ruch wychodzący jest stosowana, gdy dane pozostawia centrum danych regionalnych.</span><span class="sxs-lookup"><span data-stu-id="31193-182">An egress charge is applied when data leaves a regional data center.</span></span> <span data-ttu-id="31193-183">Opłata jest stosowany nawet wtedy, gdy ruch hello jest przeznaczony dla innej centrum danych Azure w innym regionie.</span><span class="sxs-lookup"><span data-stu-id="31193-183">This charge is applied even if hello traffic is destined for another Azure data center in a different region.</span></span>

> [!WARNING]
> <span data-ttu-id="31193-184">Używanie konta magazynu w regionie innym niż klaster usługi HDInsight hello nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="31193-184">Using a storage account in a different region than hello HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31193-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="31193-185">Next steps</span></span>

<span data-ttu-id="31193-186">Wiesz już, jak tooadd dodatkowy magazyn kont tooan istniejącym klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="31193-186">You have learned how tooadd additional storage accounts tooan existing HDInsight cluster.</span></span> <span data-ttu-id="31193-187">Aby uzyskać więcej informacji dotyczących akcji skryptu, zobacz [klastrów usługi HDInsight opartej na dostosowanie systemu Linux przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="31193-187">For more information on script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
