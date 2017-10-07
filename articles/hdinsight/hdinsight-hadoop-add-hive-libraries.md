---
title: "Tworzenie - Azure klastra aaaAdd bibliotek technologii Hive w usłudze HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak bibliotek technologii Hive tooadd (pliki jar) tooan HDInsight klastra podczas tworzenia klastra."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 2fd74b8d-c006-45c6-a9e2-72ff5d2d978a
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 2e028a07c3248205def0789af2c262a0774a8f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a>Dodawanie niestandardowych bibliotek technologii Hive, podczas tworzenia klastra usługi HDInsight

Jeśli masz bibliotek, które są często używane z Hive w usłudze HDInsight ten dokument zawiera informacji na temat używania biblioteki hello obciążenia toopre akcji skryptu podczas tworzenia klastra. Biblioteki dodane przy użyciu hello kroków w tym dokumencie są globalnie dostępną w gałęzi — nie toouse bez konieczności [dodać JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload je.

## <a name="how-it-works"></a>Jak to działa

Podczas tworzenia klastra, można opcjonalnie określić akcję skryptu, który uruchamia skrypt w węzłach klastra hello podczas ich tworzenia. skrypt Hello w tym dokumencie akceptuje pojedynczy parametr to lokalizacja WASB zawierający toobe bibliotek (przechowywane jako pliki jar) hello wstępnie załadowane.

Podczas tworzenia klastra skryptu hello wylicza hello pliki, kopiuje je toohello `/usr/lib/customhivelibs/` katalogu w węzłach head i proces roboczy, następnie dodanie ich toohello `hive.aux.jars.path` właściwości w hello `core-site.xml` pliku. W klastrach opartych na systemie Linux, aktualizuje również hello `hive-env.sh` pliku z lokalizacji hello hello plików.

> [!NOTE]
> Za pomocą akcji skryptu hello w tym artykule udostępnia biblioteki hello w hello następujące scenariusze:
>
> * **HDInsight opartych na systemie Linux** — przy użyciu hello klientowi Hive **WebHCat**, i **serwera HiveServer2**.
> * **HDInsight opartych na systemie Windows** — za pomocą powitania klienta Hive i **WebHCat**.

## <a name="hello-script"></a>Witaj skryptu

**Lokalizacja skryptu**

Aby uzyskać **opartych na systemie Linux klastrów**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)

Aby uzyskać **klastry z systemem Windows**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)

> [!IMPORTANT]
> Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

**Wymagania**

* skrypty Hello musi być zastosowany tooboth hello **węzły główne** i **węzłów procesu roboczego**.

* Witaj słoików mają tooinstall musi być przechowywany w magazynie obiektów Blob Azure w **jeden kontener**.

* Konto magazynu Hello zawierające biblioteki hello plików jar **musi** się podczas tworzenia klastra usługi HDInsight toohello połączone. Musi być hello domyślne konto magazynu lub dodać konta za pośrednictwem __konfiguracji opcjonalnej__.

* Witaj WASB ścieżka toohello kontenera muszą być określone jako parametr toohello akcji skryptu. Na przykład, jeśli hello słoików są przechowywane w kontenerze o nazwie **libs** na konto magazynu o nazwie **mystorage**, będzie parametru hello  **wasb://libs@mystorage.blob.core.windows.net/** .

  > [!NOTE]
  > Tym dokumencie przyjęto założenie, ma już utworzenie konta magazynu, kontenera obiektów blob i przekazane hello tooit plików.
  >
  > Jeśli nie utworzono konto magazynu, możesz to zrobić za pomocą hello [portalu Azure](https://portal.azure.com). Następnie można użyć narzędzia takie jak [Eksploratora usługi Storage Azure](http://storageexplorer.com/) toocreate kontenera w hello konta i przekazywanie plików tooit.

## <a name="create-a-cluster-using-hello-script"></a>Tworzenie klastra przy użyciu skryptu hello

> [!NOTE]
> Hello następujące kroki tworzenia klastra usługi HDInsight opartej na systemie Linux. Wybierz toocreate klastra z systemem Windows, **Windows** jako hello klastra systemu operacyjnego, podczas tworzenia klastra hello, a następnie użyć skryptu systemu Windows (PowerShell) hello zamiast hello bash skryptu.
>
> Można również użyć programu Azure PowerShell lub hello zestawu .NET SDK HDInsight toocreate klastra przy użyciu tego skryptu. Aby uzyskać więcej informacji o używaniu tych metod, zobacz [Dostosowywanie klastrów usługi HDInsight z akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).

1. Uruchom inicjowania obsługi klastra za pomocą kroków hello w [Obsługa administracyjna klastrów HDInsight w systemie Linux](hdinsight-hadoop-provision-linux-clusters.md), kroków inicjowania obsługi administracyjnej.

2. Na powitania **konfiguracji opcjonalnej** bloku, wybierz opcję **akcji skryptu**i podaj hello następujących informacji:

   * **Nazwa**: Wprowadź przyjazną nazwę dla hello akcji skryptu.

   * **Identyfikator URI skryptu**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh

   * **HEAD**: Zaznaczenie tego pola wyboru.

   * **Proces ROBOCZY**: Zaznaczenie tego pola wyboru.

   * **DOZORCY**: to pole pozostanie puste.

   * **Parametry**: Wprowadź hello WASB adres toohello kontenera i konto magazynu zawierającego słoików hello. Na przykład  **wasb://libs@mystorage.blob.core.windows.net/** .

3. U dołu hello hello **akcji skryptu**, użyj hello **wybierz** przycisk toosave hello konfiguracji.

4. Na powitania **konfiguracji opcjonalnej** bloku, wybierz opcję **połączonych kontach magazynu** i wybierz hello **Dodaj klucz magazynu** łącza. Wybierz konto magazynu hello, który zawiera słoików hello, a następnie użyj hello **wybierz** ustawienia toosave przycisków i zwracany hello **konfiguracji opcjonalnej** bloku.

5. Użyj hello **wybierz** u dołu hello hello **konfiguracji opcjonalnej** bloku toosave hello konfiguracji opcjonalnej informacji.

6. Kontynuuj, inicjowania obsługi klastra hello zgodnie z opisem w [Obsługa administracyjna klastrów HDInsight w systemie Linux](hdinsight-hadoop-provision-linux-clusters.md).

Po zakończeniu tworzenia klastra są słoików hello toouse stanie dodane za pomocą tego skryptu z gałęzi bez konieczności toouse hello `ADD JAR` instrukcji.

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat pracy z Hive, zobacz [używanie Hive z usługą HDInsight](hdinsight-use-hive.md)
