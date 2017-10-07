---
title: "Harmonogram stosowania poprawek aaaConfigure systemu operacyjnego dla opartych na systemie Linux klastrów usługi HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak harmonogram stosowania poprawek tooconfigure systemu operacyjnego dla usługi HDInsight opartej na systemie Linux klastrów."
services: hdinsight
documentationcenter: 
author: bprakash
manager: asadk
editor: bprakash
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: bhanupr
ms.openlocfilehash: 1598d64e594d7e8a68573fc63dd86051a5a9d025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="os-patching-for-hdinsight"></a>Poprawki dla usługi HDInsight systemu operacyjnego 
Jako zarządzanej usługi Hadoop HDInsight zapewnia obsługę poprawki hello systemu operacyjnego hello podstawowej maszyn wirtualnych używanych przez klastry usługi HDInsight. Począwszy od 1 sierpnia 2016 zmieniono zasady stosowania poprawek systemu operacyjnego gościa powitania dla opartych na systemie Linux klastrów usługi HDInsight (w wersji 3.4 lub nowszej). Celem Hello hello nowych zasad jest toosignificantly zmniejszyć hello liczby ponownych uruchomień komputera toopatching ukończenia. Witaj nowych zasad będą nadal toopatch maszynach wirtualnych (VM) w systemie Linux klastrów każdego poniedziałek i czwartek, zaczynając od 00: 00 czasu UTC, w sposób rozłożone w węzłach żadnego danego klastra. Jednak żadnej danej maszyny Wirtualnej zostanie uruchomiony tylko co najwyżej raz na 30 dni powodu poprawki tooguest systemu operacyjnego. Ponadto hello ponownym nowo utworzony klaster nie nastąpi szybciej niż 30 dni od daty utworzenia hello klastra. Poprawki zostaną zastosowane po hello maszyny wirtualne są ponownie uruchamiane.

## <a name="how-tooconfigure-hello-os-patching-schedule-for-linux-based-hdinsight-clusters"></a>Jak tooconfigure hello harmonogram stosowania poprawek systemu operacyjnego dla klastrów usługi HDInsight opartych na systemie Linux
Witaj maszyny wirtualne w klastrze HDInsight muszą toobe od czasu do czasu ponownego uruchomienia, dzięki czemu można zainstalować poprawki zabezpieczeń ważne. Począwszy od 1 sierpnia 2016 nowych klastrów usługi HDInsight opartej na systemie Linux (w wersji 3.4 lub nowszego) są ponownie uruchamiane przy użyciu hello według harmonogramu:

1. Maszyny wirtualnej w klastrze hello można tylko ponownego uruchomienia dla poprawek co najwyżej jeden raz w ciągu 30-dniowego okresu.
2. ponowne uruchomienie Hello występuje, zaczynając od 00: 00 czasu UTC.
3. proces ponownego uruchomienia Hello jest rozłożona między maszynami wirtualnymi w klastrze hello, tak klastra hello jest nadal dostępny podczas procesu ponownego uruchomienia hello.
4. Witaj ponownym nowo utworzony klaster nie nastąpi szybciej niż 30 dni od daty utworzenia klastra hello.

Za pomocą akcji skryptu hello opisane w tym artykule, można zmodyfikować harmonogram stosowania poprawek hello systemu operacyjnego w następujący sposób:
1. Włącz lub wyłącz automatyczne ponowne uruchomienie
2. Ustaw częstotliwość hello rozruchu (w dniach od ponownego uruchomienia)
3. Ustaw hello dzień tygodnia powitania po wystąpieniu ponowny rozruch

> [!NOTE]
> Ta akcja skryptu działa tylko z klastrami HDInsight opartych na systemie Linux utworzone po 1 sierpnia 2016. Poprawki zostaną zastosowane tylko wtedy, gdy maszyny wirtualne są ponownie uruchamiane. 
>

## <a name="how-toouse-hello-script"></a>Jak toouse hello skryptu 

Kiedy za pomocą tego skryptu wymaga hello następujących informacji:
1. Lokalizacja skryptu Hello: https://hdiconfigactions.blob.core.windows.net/linuxospatchingrebootconfigv01/os-patching-reboot-config.sh.  HDInsight używa tego identyfikatora URI toofind i uruchom skrypt hello na wszystkich maszynach wirtualnych hello hello klastra.
  
2. typy węzłów klastra, zastosowane do skryptu hello Hello: headnode, workernode, dozorcy. Ten skrypt musi być zastosowany tooall typy węzłów w klastrze hello. Jeśli nie jest typu węzła tooa zastosowane, a następnie hello wirtualnej maszyny dla tego typu węzła będzie toouse hello poprzedni harmonogram stosowania poprawek.


3.  Parametr: Ten skrypt akceptuje trzy parametry liczbowe:

    | Parametr | Definicja |
    | --- | --- |
    | Włączanie/wyłączanie automatycznego ponownego uruchamiania |0 lub 1. Wartość 0 wyłącza automatyczne ponowne uruchomienie, gdy 1 umożliwia automatyczne ponowne uruchomienie. |
    | częstotliwość |too90 7 (włącznie). Liczba Hello toowait dni przed ponownym rozruchem hello maszyn wirtualnych do poprawki, które wymagają ponownego uruchomienia komputera. |
    | Dzień tygodnia |1 too7 (włącznie). Wartość 1 oznacza ponowny rozruch hello powinna wystąpić w poniedziałek i 7 wskazuje przykładzie Sunday.For przy użyciu parametrów 2 60 1 powoduje automatyczne ponowne uruchomienie co 60 dni (maksymalnie) wtorek. |
    | Trwałość |Podczas stosowania istniejącego klastra tooan akcji skryptu, skrypt hello mogą zostać oznaczone jako utrwalone. Utrwalonych skryptów są stosowane po dodaniu nowego workernodes toohello klastra za pomocą operacji skalowania. |

> [!NOTE]
> Ten skrypt musi zostać oznaczone jako zachowywane w przypadku stosowania tooan istniejącego klastra. W przeciwnym razie wszelkie nowe węzły został utworzony za pomocą operacji skalowania użyje domyślnego hello poprawki harmonogramu.
Jeśli stosujesz hello skryptu w ramach procesu tworzenia klastra hello jest trwały automatycznie.
>

## <a name="next-steps"></a>Następne kroki

Do wykonania określonych kroków przy użyciu akcji skryptu hello, zobacz następujące sekcje w hello hello [klastrów usługi HDInsight opartej na Linuz dostosować za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md):

* [Za pomocą akcji skryptu, podczas tworzenia klastra](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation)
* [Zastosuj tooa akcji skryptu, z klastra](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster)
