---
title: "Szybki start: Przesyłanie przepływu pracy przy użyciu wielu danych wejściowych | Microsoft Docs"
titleSuffix: Azure
description: "W tym poradniku Szybki start założono, że użytkownik ma zainstalowanego klienta msgen i pomyślnie uruchomił przykładowe dane za pośrednictwem usługi."
services: microsoft-genomics
author: grhuynh
manager: jhubbard
editor: jasonwhowell
ms.author: grhuynh
ms.service: microsoft-genomics
ms.workload: genomics
ms.topic: quickstart
ms.date: 12/07/2017
ms.openlocfilehash: d410516f807b7914e15bed1fb93ee58d3e340d1e
ms.sourcegitcommit: 922687d91838b77c038c68b415ab87d94729555e
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/13/2017
---
# <a name="submit-a-workflow-using-multiple-inputs-from-the-same-sample"></a>Przesyłanie przepływu pracy przy użyciu wielu danych wejściowych z tej samej próbki

Ten poradnik Szybki start przedstawia sposób przesyłania przepływu pracy do usługi Microsoft Genomics, jeśli plik wejściowy to wiele plików FASTQ lub BAM **pochodzących z tej samej próbki**. Należy jednak pamiętać, że **nie można** mieszać plików FASTQ i BAM podczas tego samego przesyłania.

W tym temacie założono, że użytkownik zainstalował i uruchomił klienta `msgen` oraz że zna sposób korzystania z usługi Azure Storage. Po pomyślnym przesłaniu przepływu pracy przy użyciu podanych przykładowych danych masz wszystko gotowe, aby kontynuować pracę z tym poradnikiem Szybki start. 


## <a name="multiple-bam-files"></a>Wiele plików BAM

### <a name="upload-your-input-files-to-azure-storage"></a>Przekazywanie plików wejściowych do magazynu platformy Azure
Załóżmy, że masz wiele plików BAM jako dane wejściowe, *reads.bam*, *additional_reads.bam* oraz *yet_more_reads.bam*, oraz że zostały przekazane do konta magazynu *myaccount* na platformie Azure. Masz adres URL interfejsu API i klucz dostępu. Chcesz uzyskać dane wyjściowe w lokalizacji **https://<span></span>myaccount.blob.core<span></span>.windows<span></span>.net<span></span>/outputs<span></span>**.


### <a name="submit-your-job-to-the-msgen-client"></a>Przesyłanie zadania do klienta `msgen` 

Możesz przesłać wiele plików BAM, przekazując wszystkie ich nazwy do argumentu --input-blob-name-1. Należy pamiętać, że wszystkie pliki powinny pochodzić z tej samej próbki, ale ich kolejność nie jest ważna. Poniżej przedstawiono przykłady przesyłania z wiersza polecenia w systemie Windows, w systemie Unix i przy użyciu pliku konfiguracji. Z myślą o zachowaniu przejrzystości dodano podziały wierszy:


W przypadku systemu Windows:

```
msgen submit ^
  --api-url-base <Genomics API URL> ^
  --access-key <Genomics access key> ^
  --process-args R=b37m1 ^
  --input-storage-account-name myaccount ^
  --input-storage-account-key <storage access key to "myaccount"> ^
  --input-storage-account-container inputs ^
  --input-blob-name-1 reads.bam additional_reads.bam yet_more_reads.bam ^
  --output-storage-account-name myaccount ^
  --output-storage-account-key <storage access key to "myaccount"> ^
  --output-storage-account-container outputs
```


W przypadku systemu Unix

```
msgen submit \
  --api-url-base <Genomics API URL> \
  --access-key <Genomics access key> \
  --process-args R=b37m1 \
  --input-storage-account-name myaccount \
  --input-storage-account-key <storage access key to "myaccount"> \
  --input-storage-account-container inputs \
  --input-blob-name-1 reads.bam additional_reads.bam yet_more_reads.bam \
  --output-storage-account-name myaccount \
  --output-storage-account-key <storage access key to "myaccount"> \
  --output-storage-account-container outputs
```


Jeśli wolisz używać pliku konfiguracji, oto jego zawartość:

``` config.txt
api_url_base:                     <Genomics API URL>
access_key:                       <Genomics access key>
process_args:                     R=b37m1
input_storage_account_name:       myaccount
input_storage_account_key:        <storage access key to "myaccount">
input_storage_account_container:  inputs
input_blob_name_1:                reads.bam additional_reads.bam yet_more_reads.bam
output_storage_account_name:      myaccount
output_storage_account_key:       <storage access key to "myaccount">
output_storage_account_container: outputs
```

Prześlij plik `config.txt` przy użyciu tego wywołania: `msgen submit -f config.txt`


## <a name="multiple-paired-fastq-files"></a>Wiele sparowanych plików FASTQ

### <a name="upload-your-input-files-to-azure-storage"></a>Przekazywanie plików wejściowych do magazynu platformy Azure
Załóżmy, że masz wiele sparowanych plików FASTQ jako dane wejściowe, *reads_1.fq.gz* i *reads_2.fq.gz*,  *additional_reads_1.fq.gz* i *additional_reads_2.fq.gz* i *yet_more_reads_1.fq.gz* oraz *yet_more_reads_2.fq.gz*. Zostały one przekazane do konta magazynu *myaccount* na platformie Azure oraz masz adres URL interfejsu API i klucz dostępu. Chcesz uzyskać dane wyjściowe w lokalizacji **https://<span></span>myaccount.blob.core<span></span>.windows<span></span>.net<span></span>/outputs<span></span>**.


### <a name="submit-your-job-to-the-msgen-client"></a>Przesyłanie zadania do klienta `msgen` 

Sparowane pliki FASTQ muszą pochodzić z tych samych przykładowych danych oraz muszą być przetwarzane wspólnie.  Kolejność nazw plików ma znaczenie, gdy są przekazywane jako argumenty do obiektów --input-blob-name-1 i --input-blob-name-2. 

Poniżej przedstawiono przykłady przesyłania z wiersza polecenia w systemie Windows, w systemie Unix i przy użyciu pliku konfiguracji. Z myślą o zachowaniu przejrzystości dodano podziały wierszy:


W przypadku systemu Windows:

```
msgen submit ^
  --api-url-base <Genomics API URL> ^
  --access-key <Genomics access key> ^
  --process-args R=b37m1 ^
  --input-storage-account-name myaccount ^
  --input-storage-account-key <storage access key to "myaccount"> ^
  --input-storage-account-container inputs ^
  --input-blob-name-1 reads_1.fastq.gz additional_reads_1.fastq.gz yet_more_reads_1.fastq.gz ^
  --input-blob-name-2 reads_2.fastq.gz additional_reads_2.fastq.gz yet_more_reads_2.fastq.gz ^
  --output-storage-account-name myaccount ^
  --output-storage-account-key <storage access key to "myaccount"> ^
  --output-storage-account-container outputs
```


W przypadku systemu Unix:

```
msgen submit \
  --api-url-base <Genomics API URL> \
  --access-key <Genomics access key> \
  --process-args R=b37m1 \
  --input-storage-account-name myaccount \
  --input-storage-account-key <storage access key to "myaccount"> \
  --input-storage-account-container inputs \
  --input-blob-name-1 reads_1.fastq.gz additional_reads_1.fastq.gz yet_more_reads_1.fastq.gz \
  --input-blob-name-2 reads_2.fastq.gz additional_reads_2.fastq.gz yet_more_reads_2.fastq.gz \
  --output-storage-account-name myaccount \
  --output-storage-account-key <storage access key to "myaccount"> \
  --output-storage-account-container outputs
```


Jeśli wolisz używać pliku konfiguracji, oto jego zawartość:

```
api_url_base:                     <Genomics API URL>
access_key:                       <Genomics access key>
process_args:                     R=b37m1
input_storage_account_name:       myaccount
input_storage_account_key:        <storage access key to "myaccount">
input_storage_account_container:  inputs
input_blob_name_1:                reads_1.fq.gz additional_reads_1.fastq.gz yet_more_reads_1.fastq.gz
input_blob_name_2:                reads_2.fq.gz additional_reads_2.fastq.gz yet_more_reads_2.fastq.gz
output_storage_account_name:      myaccount
output_storage_account_key:       <storage access key to "myaccount">
output_storage_account_container: outputs
```

Prześlij plik `config.txt` przy użyciu tego wywołania: `msgen submit -f config.txt`

## <a name="next-steps"></a>Następne kroki
W tym artykule przekazano wiele plików BAM lub sparowanych plików FASTQ do usługi Azure Storage oraz przesłano przepływ pracy do usługi Microsoft Genomics za pośrednictwem klienta `msgen` Python. Aby uzyskać dodatkowe informacje o przesyłaniu przepływów pracy i innych poleceniach, których możesz użyć wraz z usługą Microsoft Genomics, zobacz [często zadawane pytania](frequently-asked-questions-genomics.md). 