---
title: "aaaMonitor klaster Azure DC/OS - stosu ŁOSI | Dokumentacja firmy Microsoft"
description: "Monitorowanie klastra DC/OS w klastrze usługi kontenera platformy Azure z ŁOSI (Elasticsearch Logstash i Kibana)."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Kontenery, DC/OS, Azure, monitorowanie, łosi"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 8d81c5342616ec14880d38803cdf95f5845a669b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a>Monitor klastra usługi kontenera platformy Azure z ŁOSI
W tym artykule przedstawiony sposób stosu hello toodeploy ŁOSI (Elasticsearch, Logstash, Kibana) w klastrze DC/OS usługi kontenera platformy Azure. 

## <a name="prerequisites"></a>Wymagania wstępne
[Wdrażanie](container-service-deployment.md) i [połączyć](../container-service-connect.md) klastra DC/OS konfigurowane za pomocą usługi kontenera platformy Azure. Eksploruj pulpitu nawigacyjnego DC/OS hello i usługi Marathon [tutaj](container-service-mesos-marathon-ui.md). Zainstaluj również hello [modułu równoważenia obciążenia platformy Marathon](container-service-load-balancing.md).


## <a name="elk-elasticsearch-logstash-kibana"></a>ŁOSI (Elasticsearch, Logstash, Kibana)
Stos ŁOSI jest kombinacją Elasticsearch, Logstash, i Kibana udostępniający stosu tooend zakończenia mogą być używane toomonitor i analizowanie dzienników w klastrze.

## <a name="configure-hello-elk-stack-on-a-dcos-cluster"></a>Skonfiguruj hello ŁOSI stosu w klastrze DC/OS
Dostęp za pośrednictwem interfejsu użytkownika DC/OS [http://localhost:80 /](http://localhost:80/) raz w hello interfejsu użytkownika DC/OS Przejdź zbyt**Universe**. Wyszukiwanie i instalowanie Elasticsearch, Logstash i Kibana z hello Universe DC/OS i w tej kolejności. Więcej informacji o konfiguracji przejście toohello **instalacji zaawansowanym** łącza.

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

Raz hello ŁOSI kontenery i czy do pracy, należy uzyskać przy użyciu platformy Marathon-LB toobe Kibana tooenable. Przejdź za **usług** > **kibana**i kliknij przycisk **Edytuj** jak pokazano poniżej.

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


Przełącz zbyt**tryb JSON** i przewiń w dół do sekcji etykiety toohello.
Należy tooadd `"HAPROXY_GROUP": "external"` wpis tutaj jak pokazano poniżej.
Po kliknięciu **wdrażać zmiany**, ponownym uruchomieniu kontenera.

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


Jeśli chcesz, aby tooverify tego Kibana jest zarejestrowany jako usługa na pulpicie nawigacyjnym HAPROXY hello, należy tooopen portu 9090 w klastrze agenta hello jak HAPROXY działa na porcie 9090.
Domyślnie możemy otworzyć porty 80, 8080 i 443 w hello klastra agenta DC/OS.
Instrukcje tooopen portu i podaj oceny publicznego są udostępniane [tutaj](container-service-enable-public-access.md).

tooaccess hello HAPROXY pulpitu nawigacyjnego, otwórz hello warstwa Marathon-LB interfejsu administracyjnego na: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.
Po przejściu toohello adres URL powinien zostać wyświetlony pulpit nawigacyjny HAPROXY hello w sposób przedstawiony poniżej i powinna być widoczna dla Kibana wpisu usługi.

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


tooaccess hello Kibana dashboard, który jest wdrażana na porcie 5601, należy portu tooopen 5601. Postępuj zgodnie z instrukcjami [tutaj](container-service-enable-public-access.md). Następnie otwórz pulpit nawigacyjny Kibana hello w: `http://localhost:5601`.

## <a name="next-steps"></a>Następne kroki

* Dla dziennika systemu i aplikacji przekazywania i ustawień, zobacz [zarządzanie dziennikiem w DC/OS z ŁOSI](https://docs.mesosphere.com/1.8/administration/logging/elk/).

* Zobacz dzienniki toofilter [filtrowania dzienniki z ŁOSI](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/). 

 

