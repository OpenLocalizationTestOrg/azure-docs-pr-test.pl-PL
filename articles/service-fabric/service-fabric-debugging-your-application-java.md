---
title: "aaaDebug aplikację usługi Azure Service Fabric w środowisku Eclipse | Dokumentacja firmy Microsoft"
description: "Zwiększyć hello niezawodność i wydajność usług przez opracowywania i debugowania ich w środowisku Eclipse na lokalny klaster projektowy."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/10/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: ab86254a5c312db40fd631746c89aab0bbb9d1a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a>Debugowanie aplikacji Java sieci szkieletowej usług za pomocą programu Eclipse
> [!div class="op_single_selector"]
> * [Visual Studio/CSharp](service-fabric-debugging-your-application.md) 
> * [Eclipse/Java](service-fabric-debugging-your-application-java.md)
> 

1. Uruchom lokalnego klastra projektowego, wykonując kroki hello w [konfigurowania środowiska deweloperskiego sieci szkieletowej usług](service-fabric-get-started-linux.md).

2. Zaktualizuj entryPoint.sh hello usługi ma toodebug, tak aby był uruchamiany z parametrami zdalnego debugowania procesu java hello. Ten plik znajduje się w następującej lokalizacji hello: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``. Port 8001 jest ustawiony do debugowania w tym przykładzie.

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. Zaktualizuj Manifest aplikacji hello ustawiając hello liczbę wystąpień lub hello liczbie repliki usługi hello, który jest debugowany too1. To ustawienie pozwala uniknąć konfliktów hello port używany do debugowania. Na przykład w przypadku usług bezstanowych ustawić ``InstanceCount="1"`` i usługi stanowej hello zestaw docelowy i min repliki Ustaw rozmiary too1 w następujący sposób: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.

4. Wdrażanie aplikacji hello.

5. Hello Eclipse IDE, wybierz **Uruchom -> debugowanie konfiguracji -> zdalnego aplikacji Java i wprowadź właściwości połączenia** i ustaw właściwości hello w następujący sposób:

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  Ustaw punkty przerwania w punktach żądaną i debugowanie aplikacji hello.

Jeśli aplikacja hello uległa awarii, również można tooenable coredumps. Wykonanie ``ulimit -c`` w powłoce i zwraca 0, a następnie coredumps nie są włączone. tooenable nieograniczone coredumps wykonania hello następującego polecenia: ``ulimit -c unlimited``. Można również sprawdzić stan hello za pomocą polecenia hello ``ulimit -a``.  Jeśli potrzebujesz tooupdate hello coredump generowania ścieżka wykonywania ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``. 

### <a name="next-steps"></a>Następne kroki

* [Zbieranie dzienników przy użyciu diagnostyki Azure Linux](service-fabric-diagnostics-how-to-setup-lad.md).
* [Monitorowanie i diagnozowania usług lokalnie](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).
