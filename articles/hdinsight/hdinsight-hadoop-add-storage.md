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
# <a name="add-additional-storage-accounts-toohdinsight"></a>Dodaj dodatkowy magazyn kont tooHDInsight

Dowiedz się, jak konta tooHDInsight toouse skryptu akcje tooadd dodatkowe Azure magazynu. Witaj kroki opisane w tym dokumencie dodać magazynu konta tooan istniejących HDInsight opartych na systemie Linux klaster.

> [!IMPORTANT]
> Witaj informacje w tym dokumencie jest o dodawaniu klastra tooa dodatkowego miejsca do magazynowania po jego utworzeniu. Aby uzyskać informacje na temat dodawania konta magazynu podczas tworzenia klastra, zobacz [Ustawianie klastrów w usłudze HDInsight Hadoop, Spark, Kafka i](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="how-it-works"></a>Jak to działa

Ten skrypt wykonuje hello następujące parametry:

* __Nazwa konta magazynu Azure__: hello nazwę klastra usługi HDInsight toohello tooadd hello magazynu konta. Po uruchomieniu skryptu hello, HDInsight można odczytu i zapisu, dane przechowywane na tym koncie magazynu.

* __Klucz konta magazynu Azure__: klucz, który daje konta magazynu toohello dostępu.

* __-p__ (opcjonalnie): Jeśli zostanie określona, hello klucza nie są szyfrowane i są przechowywane w pliku core-site.xml hello jako zwykły tekst.

Podczas przetwarzania skryptu hello wykonuje hello następujące akcje:

* Jeśli hello konto magazynu już istnieje w konfiguracji core-site.xml hello hello klastra, hello skrypt zakończy pracę, i są wykonywane żadne dalsze akcje.

* Sprawdza, czy konto magazynu hello istnieje i czy jest możliwy przy użyciu klucza hello.

* Szyfruje klucz hello przy użyciu poświadczeń klastra hello.

* Dodaje pliku core-site.xml toohello konta magazynu hello.

* Zatrzymuje i uruchamia ponownie usługi hello Oozie, YARN MapReduce2 i system plików HDFS. Zatrzymywanie i uruchamianie tych usług umożliwia im toouse hello nowe konto magazynu.

> [!WARNING]
> Używanie konta magazynu w innej lokalizacji niż hello klastra usługi HDInsight nie jest obsługiwane.

## <a name="hello-script"></a>Witaj skryptu

__Lokalizacja skryptu__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)

__Wymagania dotyczące__:

* Witaj skryptu muszą być stosowane na powitania __węzły główne__.

## <a name="toouse-hello-script"></a>toouse hello skryptu

Ten skrypt można używać z hello portalu Azure, programu Azure PowerShell lub hello Azure CLI w wersji 1.0. Aby uzyskać więcej informacji, zobacz hello [klastrów usługi HDInsight opartej na dostosowanie systemu Linux przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) dokumentu.

> [!IMPORTANT]
> Podczas korzystania z hello z krokami opisanymi w dokumencie dostosowania hello, należy używać hello następujące informacje tooapply ten skrypt:
>
> * Zastąp żadnych akcji skryptu przykład URI hello identyfikatora URI dla tego skryptu (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).
> * Parametry przykład zastąpić nazwę konta magazynu Azure hello i klucz hello magazynu konta toobe dodano toohello klastra. Jeśli przy użyciu hello portalu Azure, te parametry muszą być oddzielone spacją.
> * Nie trzeba toomark ten skrypt jako __Persisted__, bezpośrednio aktualizacji konfiguracji Ambari hello hello klastra.

## <a name="known-issues"></a>Znane problemy

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a>Konta magazynu nie są wyświetlane w portalu Azure lub narzędzia

Podczas wyświetlania hello HDInsight klaster na powitania portalu Azure, wybierając hello __kont magazynu__ wpis w __właściwości__ kont magazynu dodanego przez tę akcję skryptu nie są wyświetlane. Azure PowerShell i interfejsu wiersza polecenia Azure nie są wyświetlane konta magazynu dodatkowe hello albo.

Hello magazynu informacji nie są wyświetlane, ponieważ skrypt hello tylko Modyfikuje konfigurację core-site.xml hello hello klastra. Te informacje nie jest używany podczas pobierania informacji klastra hello za pomocą interfejsów API zarządzania platformy Azure.

informacje o koncie magazynu tooview dodać toohello klastra przy użyciu tego skryptu, użyj hello interfejsu API REST Ambari. Użyj następującego polecenia tooretrieve hello te informacje dla klastra:

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter hello cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> Ustaw `$clusterName` toohello nazwę hello klastra usługi HDInsight. Ustaw `$storageAccountName` nazwa toohello hello konta magazynu. Po wyświetleniu monitu wprowadź hello logowania do klastra (admin) i hasło.

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> Ustaw `$PASSWORD` toohello hasło do konta logowania (Administrator) klastra. Ustaw `$CLUSTERNAME` toohello nazwę hello klastra usługi HDInsight. Ustaw `$STORAGEACCOUNTNAME` nazwa toohello hello konta magazynu.
>
> W tym przykładzie użyto [curl (http://curl.haxx.se/)](http://curl.haxx.se/) i [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve i analizy danych JSON.

Korzystając z tego polecenia, Zastąp __CLUSTERNAME__ o nazwie hello hello klastra usługi HDInsight. Zastąp __hasło__ hasłem logowania hello HTTP hello klastra. Zastąp __STORAGEACCOUNT__ hello nazwę konta magazynu hello dodane przy użyciu akcji skryptu. Informacje zwrócone z tego polecenia zostanie wyświetlony podobne toohello następującego tekstu:

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

Ten tekst jest przykładem zaszyfrowanego klucza, który jest używany tooaccess hello konta magazynu.

### <a name="unable-tooaccess-storage-after-changing-key"></a>Magazyn tooaccess po zmianie klucza

Jeśli zmienisz hello klucza dla konta magazynu usługi HDInsight dłużej korzystać z konta magazynu hello. HDInsight używa pamięci podręcznej kopię klucza hello core-site.xml hello klastra. Ta kopia pamięci podręcznej musi być zaktualizowany toomatch hello nowy klucz.

Uruchomienie akcji skryptu hello ponownie jest __nie__ zaktualizować klucz hello jako hello skrypt sprawdza toosee, jeśli istnieje już wpis dla konta magazynu hello. Jeżeli wpis już istnieje, nie powoduje żadnych zmian.

toowork rozwiązać ten problem, należy usunąć istniejący wpis hello hello konta magazynu. Użyj hello następujące kroki tooremove hello istniejący wpis:

1. W przeglądarce sieci web Otwórz hello Interfejsu sieci Web Ambari dla klastra usługi HDInsight. Witaj identyfikatora URI jest https://CLUSTERNAME.azurehdinsight.net. Zastąp __CLUSTERNAME__ o nazwie hello klastra.

    Po wyświetleniu monitu wprowadź hello HTTP logowania użytkownika i hasło dla klastra.

2. Wybierz z listy hello usług na powitania po lewej stronie powitania __HDFS__. Następnie wybierz hello __Configs__ kartę w Centrum hello hello strony.

3. W hello __filtru...__  wprowadź wartość __fs.azure.account__. To polecenie zwróci wpisy dla wszystkich kont dodatkowego miejsca do magazynowania, które zostały dodane toohello klastra. Istnieją dwa typy wpisy. __keyprovider__ i __klucza__. Zawierają hello nazwę konta magazynu hello jako część nazwy klucza hello.

    Witaj poniżej przedstawiono przykładowe wpisy dla konta magazynu o nazwie __mystorage__:

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. Po zidentyfikowaniu hello kluczy dla konta magazynu hello należy tooremove za pomocą hello red "-" toohello ikona rogu hello wpis toodelete go. Następnie użyj hello __zapisać__ przycisk toosave zmiany.

5. Po zapisaniu zmian, użyj konta magazynu hello tooadd hello skryptu akcji i nowym klastrze toohello wartość klucza.

### <a name="poor-performance"></a>Niska wydajność

Jeśli konto magazynu hello znajduje się w regionie innym niż klaster usługi HDInsight hello, może wystąpić pogorszenie wydajności. Podczas uzyskiwania dostępu do danych w innym regionie wysyła ruch sieciowy poza centrum danych Azure regionalnych hello i wielu hello publicznej sieci internet, który może powodować opóźnienia.

> [!WARNING]
> Używanie konta magazynu w regionie innym niż klaster usługi HDInsight hello nie jest obsługiwane.

### <a name="additional-charges"></a>Dodatkowe opłaty.

W przypadku konta magazynu hello w innym regionie niż hello klastra usługi HDInsight, opłaty za wyjście dodatkowe mogą pojawić się na Azure rozliczeniowego. Dodatkowy ruch wychodzący jest stosowana, gdy dane pozostawia centrum danych regionalnych. Opłata jest stosowany nawet wtedy, gdy ruch hello jest przeznaczony dla innej centrum danych Azure w innym regionie.

> [!WARNING]
> Używanie konta magazynu w regionie innym niż klaster usługi HDInsight hello nie jest obsługiwane.

## <a name="next-steps"></a>Następne kroki

Wiesz już, jak tooadd dodatkowy magazyn kont tooan istniejącym klastrze usługi HDInsight. Aby uzyskać więcej informacji dotyczących akcji skryptu, zobacz [klastrów usługi HDInsight opartej na dostosowanie systemu Linux przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md)
