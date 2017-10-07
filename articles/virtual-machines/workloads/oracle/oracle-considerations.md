---
title: "aaaOracle rozwiązań w systemie Microsoft Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat obsługiwanych konfiguracji i ograniczenia Oracle rozwiązań w systemie Microsoft Azure."
services: virtual-machines-linux
documentationcenter: 
manager: timlt
author: rickstercdn
tags: azure-resource-management
ms.assetid: 5d71886b-463a-43ae-b61f-35c6fc9bae25
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: rclaus
ms.openlocfilehash: 54dc62e76129535da7fb6f131af90c83adfec6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="oracle-solutions-and-their-deployment-on-microsoft-azure"></a>Rozwiązania programu Oracle i wdrażania ich w systemie Microsoft Azure
W tym artykule omówiono informacje wymagane toosuccesfully wdrażanie różnych rozwiązań Oracle w systemie Microsoft Azure. Te rozwiązania są oparte na opublikowane przez firmę Oracle w portalu Azure Marketplace hello obrazy maszyny wirtualnej. tooget listę aktualnie dostępnych obrazów, uruchom następujące polecenie hello:
```azurecli-interactive
az vm image list --publisher oracle -o table --all
```
Począwszy od 6-16-2017 hello listy obrazów są następujące hello:
```bash
Offer                   Publisher    Sku                     Urn                                                          Version
----------------------  -----------  ----------------------  -----------------------------------------------------------  -------------
Oracle-Database-Ee      Oracle       12.1.0.2                Oracle:Oracle-Database-Ee:12.1.0.2:12.1.20170202             12.1.20170202
Oracle-Database-Se      Oracle       12.1.0.2                Oracle:Oracle-Database-Se:12.1.0.2:12.1.20170202             12.1.20170202
Oracle-Linux            Oracle       6.4                     Oracle:Oracle-Linux:6.4:6.4.20141206                         6.4.20141206
Oracle-Linux            Oracle       6.7                     Oracle:Oracle-Linux:6.7:6.7.20161007                         6.7.20161007
Oracle-Linux            Oracle       6.8                     Oracle:Oracle-Linux:6.8:6.8.20161020                         6.8.20161020
Oracle-Linux            Oracle       6.9                     Oracle:Oracle-Linux:6.9:6.9.20170406                         6.9.20170406
Oracle-Linux            Oracle       7.0                     Oracle:Oracle-Linux:7.0:7.0.20141217                         7.0.20141217
Oracle-Linux            Oracle       7.2                     Oracle:Oracle-Linux:7.2:7.2.20161020                         7.2.20161020
Oracle-Linux            Oracle       7.3                     Oracle:Oracle-Linux:7.3:7.3.20170320                         7.3.20170320
Oracle-WebLogic-Server  Oracle       Oracle-WebLogic-Server  Oracle:Oracle-WebLogic-Server:Oracle-WebLogic-Server:12.1.2  12.1.2
```

Te obrazy są traktowane jako "Bring Your Own License" i jako taki można będzie obciążana dla zasobów obliczeniowych, magazynu i sieci kosztów ponoszonych przez uruchomienie maszyny Wirtualnej.  Zakłada się, czy toouse prawidłowo licencjonowane oprogramowanie Oracle i mieć bieżącej umowy pomocy technicznej w miejscu z programu Oracle. Oracle ma gwarancji przenośność licencji z lokalnymi tooAzure. Zobacz hello opublikowane [Oracle i Microsoft](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html) Uwaga szczegółowe informacje na temat przenośność licencji. 

Osoby można również wybrać toobase ich rozwiązania na niestandardowych obrazów, utworzyć od podstaw na platformie Azure lub Przekaż niestandardowych obrazów z ich w środowiskach lokalnych.

## <a name="support-for-jd-edwards"></a>Obsługa Dyszkiewicz JD
Zgodnie z tooOracle Obsługa Uwaga [2178595.1 identyfikator Doc](https://support.oracle.com/epmos/faces/DocumentDisplay?_afrLoop=573435677515785&id=2178595.1&_afrWindowMode=0&_adf.ctrl-state=o852dw7d_4) , EnterpriseOne Dyszkiewicz JD wersjami 9.2 i nowszej są obsługiwane w **publicznych chmury oferty** spełniające ich właściwe `Minimum Technical Requirements` (MTR).  Konieczne będzie toocreate niestandardowych obrazów, które spełnia ich wymagań MTR dla systemu operacyjnego i oprogramowania zgodności aplikacji. 

## <a name="oracle-database-virtual-machine-images"></a>Obrazy maszyny wirtualnej bazy danych programu Oracle
Oracle obsługuje uruchomione wersje Oracle DB 12.1 Standard i Enterprise na platformie Azure w oparciu Oracle Linux obrazy maszyny wirtualnej.  Hello najlepszej wydajności dla obciążeń produkcyjnych z bazy danych programu Oracle na platformie Azure można się tooproperly rozmiar hello obrazu maszyny Wirtualnej i użyj zarządzanych dysków, które bazują na magazyn w warstwie Premium. Aby uzyskać instrukcje dotyczące sposobu tooquickly uzyskiwania bazy danych programu Oracle do pracy w platformie Azure przy użyciu hello Oracle opublikowane obrazu maszyny Wirtualnej, [spróbuj Przewodnik Szybki Start bazy danych Oracle hello](oracle-database-quick-create.md).

### <a name="attached-disk-configuration-options"></a>Opcje konfiguracji dysku dołączonym

Dołączonych dysków polegają na powitania usługi magazynu obiektów Blob platformy Azure. Każdy dysk standardowy jest w stanie teoretyczna maksymalna około 500 operacji wejścia/wyjścia na sekundę (IOPS). Nasze oferty dysku premium jest preferowane w przypadku obciążeń bazy danych wysokiej wydajności i można osiągnąć się too5000 IOps dla każdego dysku. Za pomocą jednego dysku, jeśli spełniające wydajność musi — hello skuteczne IOPS wydajności można zwiększyć, jeśli wiele dysków dołączonych, rozmieszczenie do ich dane z bazy danych, a następnie użyj Oracle automatyczne zarządzanie magazynu (ASM). Zobacz [Oracle automatyczne magazynowania — omówienie](http://www.oracle.com/technetwork/database/index-100339.html) Aby uzyskać więcej informacji określonych funkcji ASM Oracle. Na przykład jak tooinstall i skonfigurować Oracle ASM na Maszynę wirtualną systemu Linux platformy Azure — możesz spróbować hello [Instalowanie i konfigurowanie programu Oracle automatycznego zarządzania magazynem](configure-oracle-asm.md) samouczka.

### <a name="oracle-realtime-application-cluster-rac"></a>Oracle czasu rzeczywistego aplikacji klastra (RAC)
Oracle RAC jest zaprojektowana toomitigate hello awarii jednego węzła w konfiguracji klastra wielowęzłowego lokalnymi.  Opiera się na dwie technologie lokalnej nie będących środowisk chmury publicznej natywnego skalowania toohyper: rzutowanie wiele sieci i udostępnionego dysku. Są tworzone przez producentów rozwiązań innych firm [takich jak FlashGrid](https://www.flashgrid.io/oracle-rac-in-azure/) który emulować tych technologii, jeśli potrzebujesz toodeploy RAC Oracle na platformie Azure. 

### <a name="high-availability-and-disaster-recovery-considerations"></a>Zagadnienia wysoką dostępność i odzyskiwaniem po awarii
Korzystając z bazami danych Oracle na platformie Azure, jest odpowiedzialny za wdrażanie wysokiej dostępności i awaryjnego odzyskiwania rozwiązania tooavoid żadnych przestojów. 

Wysoka dostępność i odzyskiwanie po awarii dla Oracle bazy danych Enterprise Edition (bez RAC) na platformie Azure można osiągnąć za pomocą [Data Guard, ochrona danych Active](http://www.oracle.com/technetwork/articles/oem/dataguardoverview-083155.html), lub [Oracle Golden bramy](http://www.oracle.com/technetwork/middleware/goldengate), z dwóch baz danych w dwa odrębne maszyn wirtualnych. Obydwie maszyny wirtualne powinny być w hello sam [sieci wirtualnej](https://azure.microsoft.com/documentation/services/virtual-network/) tooensure one siebie dostęp za pośrednictwem prywatnego trwałe adresu IP hello.  Ponadto zaleca się umieszczanie maszyn wirtualnych hello w hello tego samego zestawu danych o dostępności tooallow Azure tooplace je do oddzielnego fault domen i domen uaktualnienia.  Należy ma nadmiarowość-toohave geograficzna — może mieć te dwie bazy danych replikacji między dwóch różnych regionach i połącz dwa wystąpienia hello z bramą sieci VPN.

Mamy samouczek "[DataGuard Oracle wdrożenie na platformie Azure](configure-oracle-dataguard.md)" który przeprowadzi Cię przez kolejne hello podstawowa konfiguracja procedury tootrial to na platformie Azure.  

Przy użyciu funkcji Guard danych Oracle, można osiągnąć wysoką dostępność z podstawowej bazy danych w jednej maszyny wirtualnej, pomocniczej bazy danych (rezerwy) w innej maszyny wirtualnej i jednokierunkowe replikacja między nimi. wynik Hello jest dostęp do odczytu toohello kopię bazy danych hello. GoldenGate Oracle można skonfigurować dwukierunkowe replikacji między Witaj dwie bazy danych. toolearn tooset się rozwiązania wysokiej dostępności dla baz danych za pomocą tych narzędzi, zobacz temat [Active Data Guard](http://www.oracle.com/technetwork/database/features/availability/data-guard-documentation-152848.html) i [GoldenGate](http://docs.oracle.com/goldengate/1212/gg-winux/index.html) dokumentacji w witrynie sieci Web hello Oracle. Jeśli użytkownik należy odczytu i zapisu dostępu toohello kopię bazy danych hello, możesz użyć [Active Oracle Data Guard](http://www.oracle.com/uk/products/database/options/active-data-guard/overview/index.html).

Mamy samouczek "[GoldenGate Oracle wdrożenie na platformie Azure](configure-oracle-golden-gate.md)" który przeprowadzi Cię przez kolejne hello seup podstawowe procedury tootrial to na platformie Azure.

Pomimo o wysokiej dostępności i odzyskiwania po awarii rozwiązania zaprojektowana na platformie Azure, można tooensure masz strategii tworzenia kopii zapasowej w miejscu toorestore bazy danych.  Mamy samouczek [kopii zapasowej i odzyskiwanie bazy danych programu Oracle](oracle-backup-recovery.md) który przeprowadzi Cię przez kolejne hello podstawowe procedury do utworzenia kopii zapasowej consistant.

## <a name="oracle-weblogic-server-virtual-machine-images"></a>Oracle WebLogic Server maszyny wirtualnej obrazów
* **Klaster jest obsługiwana w wersji Enterprise tylko.** Są licencjonowane toouse WebLogic klastra tylko wtedy, gdy przy użyciu hello Enterprise Edition WebLogic Server. Nie używaj klastrowanie WebLogic Server Standard Edition.
* **Multiemisji UDP nie jest obsługiwane.** Azure obsługuje emisji pojedynczej protokołu UDP, ale nie multiemisji lub emisji. Serwer WebLogic jest stanie toorely Azure UDP możliwości emisji pojedynczej. Aby najlepiej wyniki polegania na emisji pojedynczej protokołu UDP, firma Microsoft zaleca, że rozmiar klastra WebLogic hello zachowane statycznych, lub zachowane z nie więcej niż 10 zarządzanych serwerów znajdujących się na powitania klastra.
* **WebLogic Server oczekuje hello toobe portów publicznego i prywatnego takie same dla T3 dostęp (na przykład w przypadku używania JavaBeans przedsiębiorstwa).** Rozważmy scenariusz wielowarstwowych, gdzie aplikacja warstwy (EJB) usługi jest uruchomiona w klastrze serwerów WebLogic, składające się z co najmniej dwóch maszyn wirtualnych w sieci wirtualnej o nazwie **SLWLS**. powitania klienta warstwy znajduje się w innej podsieci w hello tej samej sieci wirtualnej, systemem prosty program Java w trakcie toocall EJB w hello warstwy usług. Warstwy usług hello saldo niezbędne tooload, dlatego publiczny punkt końcowy o zrównoważonym obciążeniu musi toobe utworzone dla hello maszyn wirtualnych w hello WebLogic klastra. W przypadku hello port prywatny, który określisz różni się od portu publicznego hello (na przykład 7006:7008), takie jak następujące hello błędu:

       [java] javax.naming.CommunicationException [Root exception is java.net.ConnectException: t3://example.cloudapp.net:7006:

       Bootstrap to: example.cloudapp.net/138.91.142.178:7006' over: 't3' got an error or timed out]

   Jest to spowodowane żadnych dostępu zdalnego T3 WebLogic Server oczekuje portu usługi równoważenia obciążenia hello i hello WebLogic zarządzanego serwera portu toobe hello takie same. W hello powyżej case powitania klienta uzyskuje dostęp do portu 7006 (port usługi równoważenia obciążenia hello) i serwera zarządzanego hello nasłuchuje 7008 (port prywatny hello). To ograniczenie ma zastosowanie tylko w przypadku dostępu T3, a nie HTTP.

   tooavoid ten problem, użyj hello następujące rozwiązania:

  * Użyj hello sam prywatnych i numery portów: publicznego obciążenia zrównoważonym dostępu tooT3 punktów końcowych w wersji dedykowanej.
  * Dołącz hello następującego parametru JVM podczas uruchamiania serwera WebLogic:

         -Dweblogic.rjvm.enableprotocolswitch=true

Powiązane informacje, zobacz artykuł bazy wiedzy **860340.1** w <http://support.oracle.com>.

* **Dynamiczne klastra i równoważenia obciążenia ograniczenia.** Załóżmy, że mają toouse dynamicznej klastra WebLogic Server i udostępnić go za pośrednictwem jednej, publiczny równoważeniem obciążenia punktu końcowego w usłudze Azure. Będzie to możliwe tak długo, jak używać numeru portu stałej dla każdego z hello zarządzane serwery (nie dynamicznie przypisywane z zakresu) i nie uruchamiaj więcej serwerów zarządzanych niż maszyny administratora hello służy do śledzenia (to znaczy nie więcej niż jednego zarządzane na virt serwera Usługa rejestrowania dostępu użytkowników komputera). Jeśli konfiguracji powoduje więcej serwerów WebLogic uruchomienia niż maszyny wirtualne (oznacza to, gdzie wiele wystąpień WebLogic udział hello tej samej maszyny wirtualnej), a następnie nie jest możliwe w dla więcej niż jeden z tych wystąpień serwera WebLogic Podany numer portu — hello innych na tej maszynie wirtualnej zakończą się tooa toobind serwerów.

   Na powitania drugiej strony, jeśli konfigurujesz hello administratora serwera tooautomatically przypisać unikatowe numery portu tooits zarządzanych serwerów, a następnie równoważenia obciążenia nie jest możliwe, ponieważ Azure nie obsługuje mapowania z jednego portu publicznego toomultiple prywatnych portów, jak będzie wymagany dla tej konfiguracji.
* **Wiele wystąpień serwera Weblogic na maszynie wirtualnej.** W zależności od wymagań danego wdrożenia, należy rozważyć możliwość hello uruchamianie wielu wystąpień WebLogic serwera na powitania tej samej maszyny wirtualnej, jeśli maszyna wirtualna hello jest wystarczająco duży. Na przykład na maszynie wirtualnej średnim rozmiarze, który zawiera dwa rdzenie, można wybrać toorun dwa wystąpienia WebLogic serwera. Należy jednak pamiętać, nadal zaleca się unikać wprowadzenie do architektury, które byłyby przypadku hello, jeśli użyto tylko jednej maszyny wirtualnej, która jest uruchamianie wielu wystąpień serwera WebLogic pojedynczych punktów awarii. Przy użyciu co najmniej dwóch maszyn wirtualnych może być lepszym rozwiązaniem, a każdy z tych maszyn wirtualnych następnie może uruchomić wiele wystąpień WebLogic serwera. Każdy z tych wystąpień WebLogic Server może być częścią hello nadal tego samego klastra. Uwaga, jednak obecnie nie jest możliwe toouse Azure saldo tooload punktów końcowych, które są dostępne w takich wdrożeniach WebLogic Server w ramach hello tej samej maszyny wirtualnej, ponieważ usługa równoważenia obciążenia Azure wymaga toobe serwerów z równoważeniem obciążenia hello rozdzielona Unikatowy maszyn wirtualnych.

## <a name="oracle-jdk-virtual-machine-images"></a>Obrazy maszyny wirtualnej JDK Oracle
* **JDK 6 i 7 najnowsze aktualizacje.** Gdy firma Microsoft zaleca używanie hello najnowszych publicznego obsługiwanych wersji języka Java (obecnie Java 8), Azure również udostępnia JDK 6 i 7 obrazów. Ta wartość jest przeznaczona dla starszych aplikacji, które nie są jeszcze gotowy toobe uaktualnione tooJDK 8. Podczas aktualizacji tooprevious JDK obrazów nie może być publicznie dostępny toohello, podany hello Microsoft współpraca z Oracle, hello JDK 6 i 7 obrazy dostarczany przez platformę Azure są przeznaczone toocontain nowszą aktualizację niepubliczne, zwykle oferowanych w usłudze Oracle tooonly grupę Oracle firmy obsługiwane klientów. Nowe wersje obrazów JDK hello zostanie udostępniona w zależności od zaktualizowanych wersji JDK 6 i 7.

   Hello JDK dostępne w tym JDK 6 i 7 obrazów i hello maszyn wirtualnych i obrazy pochodząca z nich, można używać tylko w obrębie platformy Azure.
* **JDK 64-bitowych.** obrazy maszyny wirtualnej programu Oracle WebLogic Server Hello i obrazy maszyny wirtualnej Oracle JDK hello dostarczany przez platformę Azure zawierają hello 64-bitowe wersje systemów Windows Server, jak i hello JDK.

## <a name="next-steps"></a>Następne kroki
Omówienie bieżącego rozwiązania firmy Oracle jest teraz dostępna w systemie Microsoft Azure. Następnym krokiem jest toogo i wdrażanie pierwszą bazę danych programu Oracle na platformie Azure.
- Spróbuj hello [tworzenie bazy danych programu Oracle na platformie Azure](oracle-database-quick-create.md) samouczka tooget uruchomiona.
