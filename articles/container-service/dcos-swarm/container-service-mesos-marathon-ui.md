---
title: "aaaManage Azure DC/OS klastra przy użyciu interfejsu użytkownika platformy Marathon | Dokumentacja firmy Microsoft"
description: "Wdrażanie usługi klastra usługi kontenera platformy Azure tooan kontenerów przy użyciu hello interfejsu użytkownika sieci web Marathon."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, kontenery, mikrousługi, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: a90180e1b4763e6d2ddfa699ed4b7269f209f728
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-hello-marathon-web-ui"></a>Zarządzanie klastrem usługi kontenera platformy Azure DC/OS za pośrednictwem sieci web Marathon hello interfejsu użytkownika
DC/OS udostępnia środowisko wdrażania i skalowania obciążeń klastrowanych, zapewniając jednocześnie abstrakcyjność sprzętu źródłowego hello. Ponad systemem DC/OS istnieje platforma, która zarządza planowaniem i wykonywaniem obciążeń obliczeniowych.

Platformy są dostępne dla wielu popularnych zadań, w tym dokumencie opisano sposób uruchamiania tooget wdrażanie kontenerów przy użyciu platformy Marathon. 


## <a name="prerequisites"></a>Wymagania wstępne
Przed przystąpieniem do pracy nad tymi przykładami będziesz potrzebować klastra DC/OS skonfigurowanego w usłudze kontenera platformy Azure. Należy również toohave łączności zdalnej toothis klastra. Aby uzyskać więcej informacji na temat tych elementów zobacz następujące artykuły hello:

* [Wdrażanie klastra usługi Azure Container Service](container-service-deployment.md)
* [Połącz tooan klastra usługi kontenera platformy Azure](../container-service-connect.md)

> [!NOTE]
> W tym artykule przyjęto założenie, że tunelowanie korzysta klastra DC/OS toohello za pośrednictwem lokalnego portu 80.
>

## <a name="explore-hello-dcos-ui"></a>Eksploruj hello interfejsu użytkownika DC/OS
Z tunel Secure Shell (SSH) [ustanowić](../container-service-connect.md), Przeglądaj toohttp://localhost/. Ładuje hello interfejsu użytkownika sieci web platformy DC/OS i zawiera informacje o klastrze hello, takich jak używanych zasobów, aktywnych agentów i uruchomione usługi.

![Interfejs użytkownika platformy DC/OS](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-hello-marathon-ui"></a>Eksploruj hello interfejs użytkownika platformy Marathon
Witaj toosee interfejs użytkownika platformy Marathon, przejdź toohttp://localhost/marathon. Na tym ekranie można uruchomić w klastrze usługi kontenera platformy Azure DC/OS hello nowy kontener lub inną aplikację. Możesz również sprawdzić informacje dotyczące działających kontenerów i aplikacji.  

![Interfejs użytkownika platformy Marathon](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a>Wdrażanie kontenera w formacie programu Docker
toodeploy nowy kontener przy użyciu platformy Marathon, kliknij przycisk **tworzenie aplikacji**, a następnie wprowadź następujące informacje na kartach formularza hello hello:

| Pole | Wartość |
| --- | --- |
| ID |nginx |
| Memory (Pamięć) | 32 |
| Image (Obraz) |nginx |
| Network (Sieć) |Bridged (Pomostowa) |
| Host Port (Port hosta) |80 |
| Protocol (Protokół) |TCP |

![Interfejs użytkownika New Application (Nowa aplikacja) — General (Ogólne)](./media/container-service-mesos-marathon-ui/dcos4.png)

![Interfejs użytkownika New Application (Nowa aplikacja) — Docker Container (Kontener Docker)](./media/container-service-mesos-marathon-ui/dcos5.png)

![Interfejs użytkownika New Application (Nowa aplikacja) — Ports and Service Discovery (Porty i odnajdowanie usług)](./media/container-service-mesos-marathon-ui/dcos6.png)

Jeśli chcesz toostatically mapy hello port kontenera tooa portu na agencie hello, należy toouse trybu JSON. toodo tak, Przełącz Kreatora nowej aplikacji hello zbyt**tryb JSON** za pomocą przełącznika hello. Następnie wprowadź następujące ustawienia w obszarze hello hello `portMappings` sekcji hello definicji aplikacji. W tym przykładzie wiąże hello kontenera tooport 80 agenta DC/OS hello port 80. Po wprowadzeniu tej zmiany możesz wyłączyć tryb JSON w kreatorze.

```none
"hostPort": 80,
```

![Interfejs użytkownika New Application (Nowa aplikacja) — przykładowy port 80](./media/container-service-mesos-marathon-ui/dcos13.png)

Kontrole kondycji tooenable należy ustawić ścieżkę na powitania **sprawdza kondycji** kartę.

![Interfejs użytkownika New Application (Nowa aplikacja) — kontrole kondycji](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

Witaj klastra DC/OS jest wdrażany z zestawem agentów prywatnych i publicznych. Witaj klastra toobe tooaccess stanie aplikacji hello Internet należy agenta publicznego tooa aplikacji hello toodeploy. toodo należy wybrać hello **opcjonalnie** kartę hello Kreatora nowej aplikacji, a następnie wprowadź **slave_public** dla hello **zaakceptowane role zasobów**.

Następnie kliknij przycisk **Create Application** (Utwórz aplikację).

![Interfejs użytkownika New Application (Nowa aplikacja) — ustawienia agenta publicznego](./media/container-service-mesos-marathon-ui/dcos14.png)

Do strony głównej platformy Marathon hello zobacz temat hello stan wdrożenia kontenera hello. Początkowo będzie widoczny stan **Deploying** (Wdrażanie). Po pomyślnym wdrożeniu hello zmiany stanu zbyt**systemem**.

![Strona główna interfejsu użytkownika platformy Marathon — stan wdrożenia kontenera](./media/container-service-mesos-marathon-ui/dcos7.png)

Przełącznik sieci web platformy DC/OS wstecz toohello interfejsu użytkownika (http://localhost/), zobacz, czy zadanie (w tym przypadku kontener w formacie programu Docker) jest uruchomiona w klastrze DC/OS hello.

![Interfejs użytkownika — zadanie uruchomione w klastrze hello sieci web platformy DC/OS](./media/container-service-mesos-marathon-ui/dcos8.png)

węzeł klastra hello toosee, który hello zadań jest uruchomiona na, kliknij przycisk hello **węzłów** kartę.

![Interfejs użytkownika sieci Web platformy DC/OS — węzeł klastra zadania](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-hello-container"></a>Osiągnąć hello kontenera

W tym przykładzie aplikacja hello jest uruchomiona w węźle agenta publicznego. Zostanie wyświetlona aplikacja hello z hello internet przechodząc agenta toohello nazwę FQDN klastra hello: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, gdzie:

* **DNSPREFIX** jest hello prefiks DNS podany podczas wdrażania klastra hello.
* **REGION** jest hello regionu, w którym znajduje się w grupie zasobów.

    ![Nginx z Internetu](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a>Następne kroki
* [Praca z DC/OS i hello interfejsu API platformy Marathon](container-service-mesos-marathon-rest.md)

* Nowości dotyczące hello usługi kontenera platformy Azure z Mesos

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
