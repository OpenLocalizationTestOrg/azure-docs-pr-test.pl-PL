---
title: klaster Azure DC/OS aaaMonitor - Operations Management | Dokumentacja firmy Microsoft
description: "Monitorowanie klastra usługi kontenera platformy Azure DC/OS z programu Microsoft Operations Management Suite."
services: container-service
documentationcenter: 
author: keikhara
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 11/17/2016
ms.author: keikhara
ms.custom: mvc
ms.openlocfilehash: 0ebfa3ba3cef8f0205b15731b0e91f5b304bc8fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a>Monitor klastra usługi kontenera platformy Azure DC/OS w usłudze Operations Management Suite

Pakiet Microsoft Operations Management Suite (OMS) to oparte na chmurze rozwiązanie firmy Microsoft do zarządzania systemami IT, które ułatwia zarządzanie infrastrukturą lokalną i chmurową oraz jej ochronę. Kontener rozwiązanie to rozwiązanie w OMS Log Analytics, który pomaga w widoku hello kontenera magazynu, wydajności i dzienniki w jednej lokalizacji. Można inspekcji, rozwiązywanie problemów z kontenerów, wyświetlając hello dzienniki w centralnej lokalizacji oraz znaleźć zakłócenia, wykorzystywanie nadmiarowe kontenera na hoście.

![](media/container-service-monitoring-oms/image1.png)

Aby uzyskać więcej informacji o rozwiązaniu kontenera, zobacz toothe [analizy dzienników rozwiązania kontenera](../../log-analytics/log-analytics-containers.md).

## <a name="setting-up-oms-from-hello-dcos-universe"></a>Konfigurowanie OMS z hello DC/OS universe


W tym artykule założono, że skonfigurowano DC/OS i wdrożeniu aplikacji kontenera sieci web prostego na powitania klastra.

### <a name="pre-requisite"></a>Wymagania wstępne
- [Subskrypcja usługi Microsoft Azure](https://azure.microsoft.com/free/) — można uzyskać tę bezpłatnie.  
- Instalator obszar roboczy Microsoft OMS — zobacz "Krok 3" poniżej
- [Interfejs wiersza polecenia DC/OS](https://dcos.io/docs/1.8/usage/cli/install/) zainstalowane.

1. Na pulpicie nawigacyjnym DC/OS hello kliknij Universe i wyszukaj "OMS", jak pokazano poniżej.

![](media/container-service-monitoring-oms/image2.png)

2. Kliknij pozycję **Zainstaluj**. Zobaczysz punktu obecności się z informacjami o wersji OMS hello i **zainstaluj pakiet** lub **instalacji zaawansowanym** przycisku. Po kliknięciu **zaawansowane instalacji**, który poprowadzi Cię toohello **OMS określonej konfiguracji właściwości** strony.

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. W tym miejscu, konieczne będzie podanie tooenter hello `wsid` (hello identyfikator obszaru roboczego OMS) i `wskey` (hello OMS klucz podstawowy dla hello identyfikator obszaru roboczego). tooget zarówno `wsid` i `wskey` toocreate potrzebne jest konto OMS na <https://mms.microsoft.com>. Wykonaj hello kroki toocreate konta. Po zakończeniu tworzenia konta hello należy tooobtain Twojego `wsid` i `wskey` klikając **ustawienia**, następnie **połączonych źródeł**, a następnie **serwerów z systemem Linux** , jak pokazano poniżej.

 ![](media/container-service-monitoring-oms/image5.png)

4. Wybierz hello numer możesz OMS wystąpienia i kliknij przycisk "Przejrzyj i zainstaluj" hello. Zazwyczaj można toohave hello liczby OMS wystąpień równy toohello maszyny Wirtualnej w klastrze agenta. Agent pakietu OMS dla systemu Linux jest instaluje poszczególnych kontenerów na każdej maszynie Wirtualnej, że chce toocollect informacje dotyczące monitorowania i rejestrowania informacji.

## <a name="setting-up-a-simple-oms-dashboard"></a>Skonfigurowanie prostego pulpit nawigacyjny OMS

Po zainstalowaniu hello Agent pakietu OMS dla systemu Linux na maszynach wirtualnych hello, następnym krokiem jest tooset się hello OMS z pulpitu nawigacyjnego. Istnieją dwa sposoby toodo to: portalu OMS lub portalu Azure.

### <a name="oms-portal"></a>Portalu OMS 

Zaloguj się w portalu OMS toohello (<https://mms.microsoft.com>) i przejdź toohello **galerii rozwiązań**.

![](media/container-service-monitoring-oms/image6.png)

Po przejściu do hello **galerii rozwiązań**, wybierz pozycję **kontenery**.

![](media/container-service-monitoring-oms/image7.png)

Po wybraniu hello rozwiązania kontenera, zobaczysz hello kafelka na stronie pulpitu nawigacyjnego przeglądu OMS hello. Po dane w kontenerze hello pozyskanych jest indeksowana, zostanie wyświetlona kafelka hello wypełnione informacjami na kafelkach widoku rozwiązania.

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a>Azure Portal 

Portal tooAzure logowania w <https://portal.microsoft.com/>. Przejdź do **Marketplace**, wybierz pozycję **monitorowanie i zarządzanie** i kliknij przycisk **Zobacz wszystkie**. Następnie wpisz `containers` wyszukiwania. Zostanie wyświetlone "kontenery" w wynikach wyszukiwania hello. Wybierz **kontenery** i kliknij przycisk **Utwórz**.

![](media/container-service-monitoring-oms/image9.png)

Po kliknięciu **Utwórz**, jego wyświetli monit dla obszaru roboczego. Wybierz obszar roboczy lub jeśli nie istnieje, Utwórz nowy obszar roboczy.

![](media/container-service-monitoring-oms/image10.PNG)

Po wybraniu obszaru roboczego kliknij **Utwórz**.

![](media/container-service-monitoring-oms/image11.png)

Aby uzyskać więcej informacji na temat hello OMS kontenera rozwiązania, zobacz toothe [analizy dzienników rozwiązania kontenera](../../log-analytics/log-analytics-containers.md).

### <a name="how-tooscale-oms-agent-with-acs-dcos"></a>Jak tooscale Agent pakietu OMS z ACS DC/OS 

W przypadku należy toohave zainstalowany agent pakietu OMS jest zbyt mała liczba rzeczywista węzłów hello lub skalowaniu VMSS, dodając więcej maszyny Wirtualnej, możesz to zrobić przez skalowanie hello `msoms` usługi.

Można go tooMarathon lub hello na karcie usług interfejsu użytkownika DC/OS i skalowanie w górę liczba węzłów.

![](media/container-service-monitoring-oms/image12.PNG)

To spowoduje wdrożenie tooother węzły, które nie zostały jeszcze wdrożone hello agent pakietu OMS.

## <a name="uninstall-ms-oms"></a>Odinstaluj MS OMS

toouninstall MS OMS wprowadź hello następujące polecenie:

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a>Daj nam znać!
Co to działa? Czego brakuje? Co potrzebujesz dla tego toobe przydatne dla Ciebie? Daj nam znać w <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.

## <a name="next-steps"></a>Następne kroki

 Teraz, po skonfigurowaniu OMS toomonitor kontenerów,[Zobacz Pulpit nawigacyjny kontenera](../../log-analytics/log-analytics-containers.md).
