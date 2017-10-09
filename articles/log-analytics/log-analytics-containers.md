---
title: "aaaContainer monitorowanie rozwiązania Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Hello monitorowania kontenera rozwiązania analizy dzienników ułatwia wyświetlanie i zarządzanie Docker i Windows hostów kontenera w jednym miejscu."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e1e4b52b-92d5-4bfa-8a09-ff8c6b5a9f78
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte;banders
ms.openlocfilehash: 2eed1dd81c22faef78a375fca3ebece9e5300c09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a>Kontener rozwiązania monitorowanie analizy dzienników

![Symbol kontenerów](./media/log-analytics-containers/containers-symbol.png)

W tym artykule opisano, jak monitorowanie kontenera rozwiązania analizy dzienników, która ułatwia wyświetlanie i zarządzanie Docker i Windows hello tooset się i użyj hostów kontenera w jednym miejscu. Docker jest systemu wirtualizacji oprogramowania używane toocreate kontenerów, które automatyzują tootheir wdrożenia oprogramowania IT infrastruktury.

Witaj rozwiązania wyświetlany działają kontenery, obrazów kontenera nich uruchomiony, i gdy działają kontenery. Można wyświetlić szczegółowe informacje o inspekcji przedstawiający poleceń używanych przez kontenery. I rozwiązywać kontenery wyświetlanie i wyszukując scentralizowane dzienniki bez konieczności widoku tooremotely Docker lub hosty z systemem Windows. Można znaleźć kontenerów, które mogą być zakłócenia i spójniejsze nadmiarowe zasobów na hoście. I można wyświetlić scentralizowane procesora CPU, pamięci, magazynu i użycia i wydajności informacje o sieci dla kontenerów. Na komputerach z systemem Windows, można scentralizować i porównaj dzienniki systemu Windows Server, Hyper-V i kontenery Docker. rozwiązanie Hello obsługuje powitania po orchestrators kontenera:

- Docker Swarm
- DC/OS
- Kubernetes
- Service Fabric
- Red Hat OpenShift


Witaj Poniższy diagram przedstawia relacje hello różnych hostów kontenera i agentów z usługą OMS.

![Diagram kontenerów](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a>Wymagania systemowe

Przed rozpoczęciem należy przejrzeć następujące szczegóły tooverify spełnia wymagania wstępne hello hello.

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a>Rozwiązanie monitorowania kontener obsługuje platformy Docker Orchestrator i systemu operacyjnego
Witaj poniższej tabeli przedstawiono hello aranżacji Docker i systemu operacyjnego monitorowania obsługę kontenera magazynu, wydajności i dzienniki z analizy dzienników.   

| | ACS | Linux | Windows | Kontener<br>Spis | Image (Obraz)<br>Spis | Węzeł<br>Spis | Kontener<br>Wydajność | Kontener<br>Wydarzenie | Wydarzenie<br>Log | Kontener<br>Log |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| Kubernetes | &#8226; | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; |
| Mesosphere<br>DC/OS | &#8226; | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226;| &#8226; | &#8226; | &#8226; |
| Docker<br>Swarm | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |
| Usługa<br>Sieć szkieletowa | | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; |
| Red Hat Otwórz<br>SHIFT | | &#8226; | | &#8226; | &#8226;| &#8226; | &#8226; | &#8226; | | &#8226; |
| Windows Server<br>(autonomiczna) | | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |
| Serwer systemu Linux<br>(autonomiczna) | | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |


### <a name="docker-versions-supported-on-linux"></a>Wersje docker obsługiwane w systemie Linux

- Too1.13 docker 1.11
- V17.06 docker CE i EE

### <a name="x64-linux-distributions-supported-as-container-hosts"></a>x64 dystrybucje systemu Linux obsługiwane jako hosty kontenera

- Ubuntu 14.04 LTS i 16.04 LTS
- CoreOS(stable)
- Amazon Linux 2016.09.0
- openSUSE 13.2
- openSUSE LEAP 42.2
- CentOS 7.2 i 7.3
- SLES 12
- RHEL 7.2 i 7.3
- Red Hat OpenShift kontenera platformy (OCP) 3.4 i 3.5
- Too1.8.8 DC/OS 1.7.3 ACS Mesosphere
- Too1.6 ACS Kubernetes 1.4.5
- Usługi ACS Docker Swarm

### <a name="supported-windows-operating-system"></a>Obsługiwany system operacyjny Windows

- Windows Server 2016
- Windows 10 Anniversary Edition (Professional lub Enterprise)

### <a name="docker-versions-supported-on-windows"></a>Wersje docker obsługiwane w systemie Windows

- Docker 1.12 i 1.13
- Docker 17.03.0 i nowsze

## <a name="installing-and-configuring-hello-solution"></a>Instalowanie i konfigurowanie hello rozwiązania
Użyj powitania po tooinstall informacji i skonfiguruj hello rozwiązania.

1. Dodaj hello monitorowania kontenera rozwiązania tooyour obszar roboczy OMS z [witrynę Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) lub za pomocą hello procesu opisanego w temacie [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).

2. Zainstalować i korzystać z agentem pakietu OMS Docker.  Oparte na systemie operacyjnym, możesz wybrać z hello następujące metody:

  * W obsługiwanych systemach operacyjnych Linux, zainstaluj i uruchom Docker, a następnie zainstaluj i skonfiguruj hello [Agent pakietu OMS Linux](log-analytics-agent-linux.md).  
  * Na CoreOS nie można uruchomić hello Agent pakietu OMS dla systemu Linux. Zamiast tego należy uruchomić konteneryzowanych wersji hello Agent pakietu OMS dla systemu Linux. Przegląd [hostów kontenera systemu Linux, w tym CoreOS](#for-all-linux-container-hosts-including-coreos) lub [hostów kontenera platformy Azure dla instytucji rządowych Linux, w tym CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) podczas pracy z kontenerami w chmurze Azure dla instytucji rządowych.
  * W systemie Windows Server 2016 i Windows 10 zainstalować hello aparatem platformy Docker i klienta, a następnie połączyć informacje toogather agenta i wysłać tooLog Analytics.  

### <a name="container-services"></a>Kontener usług

- Jeśli masz środowisko Red Hat OpenShift przejrzeć [skonfigurować agenta pakietu OMS dla Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).
- Jeśli masz klaster Kubernetes za pomocą hello usługi kontenera platformy Azure, przejrzyj [monitorować klastra usługi kontenera platformy Azure z Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).
- W przypadku klastra usługi kontenera platformy Azure DC/OS więcej w [monitorować klastra usługi kontenera platformy Azure DC/OS w usłudze Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).
- Jeśli masz środowisku trybu Docker Swarm, dowiedzieć się więcej o [skonfigurować agenta pakietu OMS dla rozwiązania Docker Swarm](#configure-an-oms-agent-for-docker-swarm).
- Jeśli używasz kontenery z sieci szkieletowej usług dowiedzieć się więcej na [Omówienie usługi Azure Service Fabric](../service-fabric/service-fabric-overview.md).
- Przejrzyj hello [aparatem platformy Docker w systemie Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) artykuł, aby uzyskać dodatkowe informacje na temat tooinstall i skonfigurować silnik Docker na komputerach z systemem Windows.

> [!IMPORTANT]
> Musi być uruchomiona docker **przed** zainstalować hello [Agent pakietu OMS Linux](log-analytics-agent-linux.md) na hostach kontenera. Po zainstalowaniu agenta hello przed zainstalowaniem Docker, należy najpierw hello tooreinstall Agent pakietu OMS dla systemu Linux. Aby uzyskać więcej informacji na temat rozwiązania Docker Zobacz hello [Docker witryny sieci Web](https://www.docker.com).


## <a name="linux-container-hosts"></a>Hosty kontenera systemu Linux

Po zainstalowaniu Docker Użyj hello następujące ustawienia dla agenta hello tooconfigure hosta kontenera do użycia z Docker. Najpierw należy OMS identyfikator i klucz, który można znaleźć w portalu Azure hello. W obszarze roboczym, kliknij przycisk **Szybki Start** > **komputerów** tooview Twojego **identyfikator obszaru roboczego** i **klucz podstawowy**.  Skopiuj i Wklej zarówno do Twojego ulubionego edytora.

### <a name="for-all-linux-container-hosts-except-coreos"></a>Dla wszystkich hostów kontenera systemu Linux, z wyjątkiem CoreOS

- Aby uzyskać więcej informacji i kroki na jak tooinstall hello Agent pakietu OMS dla systemu Linux, zobacz [połączenia z komputerów z systemem Linux tooOperations Management Suite (OMS)](log-analytics-agent-linux.md).

### <a name="for-all-linux-container-hosts-including-coreos"></a>Dla wszystkich hostów kontenera systemu Linux, łącznie z CoreOS

Uruchom hello OMS kontenera, które mają toomonitor. Zmodyfikuj i użyj hello poniższy przykład:

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a>Dla wszystkich hostów kontenera Azure dla instytucji rządowych Linux, łącznie z CoreOS

Uruchom hello OMS kontenera, które mają toomonitor. Zmodyfikuj i użyj hello poniższy przykład:

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-tooone-in-a-container"></a>Zmiana typu zapytania z przy użyciu zainstalowanych tooone agenta systemu Linux w kontenerze
Jeśli wcześniej używana hello bezpośrednio zainstalować agenta i chcesz Użyj tooinstead agenta uruchomionego w kontenerze, należy najpierw usunąć hello Agent pakietu OMS dla systemu Linux. Zobacz [hello odinstalowywanie agenta pakietu OMS Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand, jak odinstalować toosuccessfully hello agenta.  

### <a name="configure-an-oms-agent-for-docker-swarm"></a>Konfigurowanie agenta pakietu OMS dla rozwiązania Docker Swarm

Witaj Agent pakietu OMS można uruchomić jako usługę globalnej na Docker Swarm. Użyj hello następujące informacje toocreate usługi agenta pakietu OMS. Należy tooinsert OMS identyfikator i klucz podstawowy.

- Uruchom następujące hello na powitania węzła głównego.

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a>Konfigurowanie agenta pakietu OMS dla OpenShift Red Hat
Istnieją trzy sposoby tooadd hello Agent pakietu OMS tooRed Hat OpenShift toostart zbieranie kontenera danych monitorowania.

* [Zainstaluj dla systemu Linux hello Agent pakietu OMS](log-analytics-agent-linux.md) bezpośrednio w każdym węźle OpenShift  
* [Włączanie rozszerzenia maszyny Wirtualnej analizy dziennika](log-analytics-azure-vm-extension.md) w każdym węźle OpenShift znajdującej się na platformie Azure  
* Zainstaluj agenta pakietu OMS hello jako zestaw demon OpenShift  

W tej sekcji możemy obejmuje jako zbiór demon OpenShift hello kroki wymagane tooinstall hello Agent pakietu OMS.  

1. Zaloguj się na toohello OpenShift głównego węzła i skopiuj hello yaml programu pliku [ocp omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) z usługi GitHub tooyour głównego węzła i zmodyfikować wartość hello za pomocą Identyfikatora obszar roboczy OMS i kluczem podstawowym.
2. Uruchom następujące polecenia toocreate hello projektu dla OMS i ustaw hello konta użytkownika.

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. toodeploy hello demon set, uruchom następujące hello:

    `oc create -f ocp-omsagent.yaml`

5. tooverify, który jest skonfigurowany i działa poprawnie, należy wpisać następujące hello:

    `oc describe daemonset omsagent`  

    i przypominało wyjścia hello:

    ```
    [ocpadmin@khm-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

Toosecure kluczy tajnych toouse OMS identyfikator i klucz podstawowy podczas korzystania z pliku zestawu demon yaml programu Agent pakietu OMS hello, wykonać hello następujące kroki.

1. Zaloguj się na toohello OpenShift głównego węzła i skopiuj hello yaml programu pliku [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) i klucz tajny Generowanie skryptu [ocp secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) z usługi GitHub.  Ten skrypt wygeneruje hello kluczy tajnych yaml programu w pliku klucza podstawowego i identyfikator obszaru roboczego OMS toosecure Twojego secrete informacji.  
2. Uruchom następujące polecenia toocreate hello projektu dla OMS i ustaw hello konta użytkownika. klucz tajny Hello Generowanie skryptu poprosi o podanie Identyfikatora obszar roboczy OMS <WSID> i klucz podstawowy <KEY> i po jego ukończeniu, tworzy plik ocp secret.yaml hello.  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. Wdróż plik tajny hello, uruchamiając następujące hello:

    `oc create -f ocp-secret.yaml`

5. Sprawdź wdrożenia, uruchamiając następujące hello:

    `oc describe secret omsagent-secret`  

    i przypominało wyjścia hello:  

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

6. Wdróż plik zestawu demon yaml programu Agent pakietu OMS hello, uruchamiając następujące hello:

    `oc create -f ocp-ds-omsagent.yaml`  

7. Sprawdź wdrożenia, uruchamiając następujące hello:

    `oc describe ds oms`

    i przypominało wyjścia hello:

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe secret omsagent-secret  
    Name:           omsagent-secret  
    Namespace:      omslogging  
    Labels:         <none>  
    Annotations:    <none>  

    Type:   Opaque  

     Data  
     ====  
     KEY:    89 bytes  
     WSID:   37 bytes  
    ```

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a>Zabezpieczanie tajnych informacji o Docker Swarm i Kubernetes

Dla usługi kontenera Kubernetes i Docker Swarm można zabezpieczyć tajny identyfikator OMS i kluczy podstawowych.

#### <a name="secure-secrets-for-docker-swarm"></a>Bezpiecznego hasła dla rozwiązania Docker Swarm

Dla rozwiązania Docker Swarm, po klucz tajny hello identyfikator obszaru roboczego i klucz podstawowy został utworzony, można uruchomić hello hello usługi Docker dla OMSagent tworzenia. Użyj powitania po toocreate informacji tajnych informacji.

1. Uruchom następujące hello na powitania węzła głównego.

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. Sprawdź, czy klucze tajne zostały utworzone prawidłowo.

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. Witaj uruchom następujące polecenia toomount hello kluczy tajnych toohello konteneryzowanych Agent pakietu OMS.

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a>Bezpiecznego hasła dla Kubernetes z plikami yaml programu

Dla Kubernetes możesz użyć pliku skryptu toogenerate hello kluczy tajnych yaml programu dla identyfikator i klucz podstawowy. Na powitania [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) są dostępne pliki korzystające z lub bez tajnych informacji.

- Witaj domyślne DaemonSet Agent pakietu OMS nie ma tajnych informacji (omsagent.yaml)
- Plik yaml programu DaemonSet Agent pakietu OMS Hello używa tajnych informacji (omsagent-ds-secrets.yaml) z tajny generowania skryptów toogenerate hello kluczy tajnych yaml programu (omsagentsecret.yaml) pliku.

Możesz wybrać omsagent toocreate DaemonSets z lub bez kluczy tajnych.

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a>Domyślny OMSagent DaemonSet yaml programu plik bez hasła

- Hello domyślne DaemonSet Agent pakietu OMS yaml programu pliku, Zastąp hello `<WSID>` i `<KEY>` tooyour WSID i klucza. Skopiuj hello węzła głównego tooyour plików i hello wykonywania następujących czynności:

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a>Domyślny OMSagent DaemonSet yaml programu plik z kluczy tajnych

1. toouse DaemonSet Agent pakietu OMS przy użyciu tajnych informacji kluczy tajnych hello najpierw utworzyć.
    1. Skopiuj skrypt hello i tajne szablonu i upewnij się, że są one na powitania tego samego katalogu.
        - Generowanie skryptu - gen.sh klucz tajny klucz tajny
        - Szablon tajne — template.yaml klucz tajny
    2. Uruchom skrypt hello, takich jak hello poniższy przykład. Hello wyświetleniu zapytania o hello OMS identyfikator i klucz podstawowy i po wprowadzeniu ich hello skrypt tworzy plik tajny yaml programu, dlatego może być uruchomiony.   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. Utwórz pod kluczy tajnych hello, uruchamiając następujące hello:
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. tooverify, uruchom następujące hello:

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        Dane wyjściowe powinny wyglądać:

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        Dane wyjściowe powinny wyglądać:

        ```
        Name:           omsagent-secret
        Namespace:      default
        Labels:         <none>
        Annotations:    <none>

        Type:   Opaque

        Data
        ====
        WSID:   36 bytes
        KEY:    88 bytes
        ```

    5. Tworzenie sieci omsagent demon set, uruchamiając``` sudo kubectl create -f omsagent-ds-secrets.yaml ```

2. Sprawdź, że powitalne DaemonSet Agent pakietu OMS jest uruchomiona, podobne toohello po:

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


Dla Kubernetes należy użyć pliku skryptu toogenerate hello kluczy tajnych yaml programu dla klucza podstawowego i identyfikator obszaru roboczego. Witaj Użyj następujących informacji w przykładzie z hello [pliku yaml programu omsagent](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure tajnych informacji.

```
keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
Name:           omsagent-secret
Namespace:      default
Labels:         <none>
Annotations:    <none>

Type:   Opaque

Data
====
WSID:   36 bytes
KEY:    88 bytes
```

## <a name="windows-container-hosts"></a>Hosty kontenera systemu Windows

### <a name="preparation-before-installing-windows-agents"></a>Przygotowanie przed zainstalowaniem agentów systemu Windows

Aby zainstalować agentów na komputerach z systemem Windows, należy tooconfigure hello Docker usługi. Konfiguracja Hello pozwala hello Windows agenta lub hello analizy dzienników maszyny wirtualnej rozszerzenia toouse hello gniazda Docker TCP, dzięki czemu agenci hello dostęp zdalnie demon Docker hello i toocapture danych monitorowania.

#### <a name="toostart-docker-and-verify-its-configuration"></a>toostart Docker i sprawdzić jego konfigurację

Istnieją tooset kroki niezbędne w górę TCP nazwany potok dla systemu Windows Server:

1. W programie Windows PowerShell umożliwiają potoku TCP i nazwanego potoku.

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. Konfigurowanie Docker z pliku konfiguracyjnego hello potoku TCP i nazwany potok. plik konfiguracji Hello znajduje się w C:\ProgramData\docker\config\daemon.json.

    W pliku daemon.json hello potrzebne są następujące hello:

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

Aby uzyskać więcej informacji na temat konfiguracji demon Docker hello używane z kontenerami systemu Windows, temacie [aparatem platformy Docker w systemie Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).


### <a name="install-windows-agents"></a>Zainstaluj agentów systemu Windows

tooenable systemu Windows i kontener funkcji Hyper-V, monitorowanie, należy zainstalować hello Microsoft Monitoring Agent (MMA) na komputerach z systemem Windows, które są hostami kontenera. Na komputerach z systemem Windows w środowisku lokalnym, zobacz [tooLog komputerów Windows połączyć Analytics](log-analytics-windows-agents.md). W przypadku maszyn wirtualnych działających na platformie Azure, podłącz je tooLog Analytics przy użyciu hello [rozszerzenie maszyny wirtualnej](log-analytics-azure-vm-extension.md).

Można monitorować kontenery systemu Windows uruchomiona na sieć szkieletowa usług. Jednak tylko [maszyn wirtualnych działających na platformie Azure](log-analytics-azure-vm-extension.md) i [komputery z systemem Windows w środowisku lokalnym](log-analytics-windows-agents.md) są obecnie obsługiwane dla sieci szkieletowej usług.

Możesz sprawdzić, czy ten hello rozwiązanie monitorowanie kontenera jest prawidłowo dla systemu Windows. toocheck czy pakiet administracyjny hello pobierania został poprawnie, wyszukaj *ContainerManagement.xxx*. pliki Hello powinny być w folderze C:\Program Files\Microsoft Monitoring Agent\Agent\Health usługi State\Management pakietów hello.


## <a name="solution-components"></a>Składniki rozwiązania

Jeśli korzystasz z agentów systemu Windows, następnie hello następujący pakiet administracyjny jest zainstalowany na każdym komputerze z agentem po dodaniu tego rozwiązania. Jest niezbędny hello pakietu administracyjnego nie konfiguracji lub konserwacji.

- *ContainerManagement.xxx* zainstalowane w C:\Program Files\Microsoft Monitoring Agent\Agent\Health usługi State\Management pakietów

## <a name="container-data-collection-details"></a>Szczegóły pobierania danych kontenera
Hello rozwiązanie monitorowanie kontenera zbiera różne metryki i dziennika dane dotyczące wydajności z kontenera hostów i kontenerów przy użyciu agentów, które można włączyć.

Dane są gromadzone co 3 minuty przez hello następujące typy agenta.

- [Agent pakietu OMS dla systemu Linux](log-analytics-linux-agents.md)
- [Agent systemu Windows](log-analytics-windows-agents.md)
- [Rozszerzenia maszyny Wirtualnej analizy dzienników](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a>Rejestruje kontenera

Witaj poniższej tabeli przedstawiono przykłady rekordów zebrane przez rozwiązanie monitorowanie kontenera hello i hello typów danych, które są wyświetlane w wynikach wyszukiwania dziennika.

| Typ danych | Typ danych w dzienniku wyszukiwania | Pola |
| --- | --- | --- |
| Wydajność dla hostów i kontenerów | `Type=Perf` | Komputer, nazwa obiektu, CounterName &#40; czas procesora (%), dysk odczytuje MB, dysku zapisuje MB, użycie pamięć (MB), sieci odbieranie bajtów, sieci wysyłania w bajtach, procesor s użycia sieci &#41; równowartości, TimeGenerated, Ścieżka_licznika, SourceSystem |
| Kontener magazynu | `Type=ContainerInventory` | TimeGenerated, komputera, nazwę kontenera, ContainerHostname, obraz, ImageTag, ContainerState, ExitCode, EnvironmentVar, polecenia, CreatedTime, StartedTime, FinishedTime, SourceSystem, identyfikatora kontenera, ImageID |
| Kontener magazynu obrazu | `Type=ContainerImageInventory` | TimeGenerated, komputer, obraz, ImageTag, ImageSize, VirtualSize, działa wstrzymana, zatrzymana, nie powiodło się, SourceSystem, ImageID, TotalContainer |
| Kontener dziennika | `Type=ContainerLog` | TimeGenerated, komputer, identyfikator obrazu, nazwy kontenera, LogEntrySource, LogEntry, SourceSystem, identyfikatora kontenera |
| Dziennik usługi kontenera | `Type=ContainerServiceLog`  | TimeGenerated, komputer, TimeOfCommand, obraz, polecenia, SourceSystem, identyfikatora kontenera |
| Kontener węzła magazynu | `Type=ContainerNodeInventory_CL`| TimeGenerated, komputer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem|
| Kubernetes spisu | `Type=KubePodInventory_CL` | TimeGenerated, komputer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem |
| Proces kontenera | `Type=ContainerProcess_CL` | TimeGenerated, komputer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem |
| Zdarzenia Kubernetes | `Type=KubeEvents_CL` | TimeGenerated, komputer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, komunikatów |

Etykiety dołączany zbyt*PodLabel* typy danych są etykiet niestandardowych. Witaj dołączany PodLabel etykiety tabelą hello znajdują się przykłady. Tak `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` różnią się w zestawie danych w danym środowisku, a objęty przypominać `PodLabel_yourlabel_s`.


## <a name="monitor-containers"></a>Kontenery monitora
Po utworzeniu rozwiązania hello włączone w portalu OMS hello hello **kontenery** kafelka zawiera podsumowanie informacji o hostach kontenera i kontenery hello uruchomione na hostach.

![Kontenery kafelka](./media/log-analytics-containers/containers-title.png)

Kafelek Hello przedstawiono przegląd liczbę kontenerów masz w środowisku hello i czy jest nie, uruchamiania i zatrzymywana.

### <a name="using-hello-containers-dashboard"></a>Przy użyciu pulpitu nawigacyjnego kontenery hello
Kliknij przycisk hello **kontenery** kafelka. Z tego miejsca zobaczysz widoki uporządkowane według:

- **Kontenery zdarzeń** -pokazuje stan kontenera i komputerów z kontenerami nie powiodło się.
- **Dzienniki kontenera** — przedstawia wykres kontenera pliki dziennika wygenerowane przez czas i listę komputerów z hello największa liczba plików dziennika.
- **Zdarzenia Kubernetes** — przedstawia wykres Kubernetes zdarzenia generowane przez czas i listę przyczyn hello Dlaczego stanowiskami wygenerowany hello zdarzenia. *Ten zestaw danych jest używany tylko w środowiskach Linux.*
- **Spis Namespace Kubernetes** — pokazuje liczbę hello obszary nazw i stanowiskami i przedstawiono ich hierarchii. *Ten zestaw danych jest używany tylko w środowiskach Linux.*
- **Kontener węzeł spisu** — pokazuje liczbę hello typów aranżacji używanych na hosty węzłów kontenera. hosty węzłów komputera Hello są również wyświetlane według hello liczbę kontenerów. *Ten zestaw danych jest używany tylko w środowiskach Linux.*
- **Kontener obrazów spisu** -pokazuje hello całkowita liczba kontenera obrazy używane oraz liczbę typów obrazów. Hello liczbę obrazów są również wyświetlane według hello tag obrazu.
- **Stan kontenery** — przedstawia hello łączna liczba kontenera Komputery węzłów/hosta uruchomionych kontenerów. Komputery są także wyświetlane według liczby hello systemem hostów.
- **Proces kontenera** — przedstawia wykres liniowy procesów kontenera działających w czasie. Kontenery znajdują się przez uruchomienie polecenia procesu w kontenerach. *Ten zestaw danych jest używany tylko w środowiskach Linux.*
- **Wydajność Procesora kontenera** — przedstawia wykres liniowy w hello średnie wykorzystanie procesora CPU wraz z upływem czasu hosty węzłów komputera. Również komputera hello listy węzłów/hostów na podstawie średniego użycia Procesora.
- **Kontener wydajności pamięci** — przedstawia wykres liniowy użycia pamięci w czasie. Zawiera także listę wykorzystania opartego na nazwie wystąpienia pamięci komputera.
- **Wydajność komputera** — zawiera wykresy liniowe hello procent wydajności Procesora w czasie, procent użycia pamięci przez czas i megabajtów wolnego miejsca na dysku wraz z upływem czasu. Aktywuj przez dowolny wiersz tooview wykresu więcej szczegółów.


Każdy obszar pulpitu nawigacyjnego hello jest wizualną reprezentację wyszukiwania, które jest uruchamiane na zebranych danych.

![Kontenery pulpitu nawigacyjnego](./media/log-analytics-containers/containers-dash01.png)

![Kontenery pulpitu nawigacyjnego](./media/log-analytics-containers/containers-dash02.png)

W hello **stan kontenera** obszarze kliknij górny obszar hello, jak pokazano poniżej.

![Stan kontenerów](./media/log-analytics-containers/containers-status.png)

Otwiera dziennik wyszukiwania, wyświetlania informacji o stanie hello kontenerów.

![Dziennik wyszukiwania dla kontenerów](./media/log-analytics-containers/containers-log-search.png)

W tym miejscu można edytować toomodify zapytania wyszukiwania hello go toofind hello określone informacje Cię interesują. Aby uzyskać więcej informacji na temat wyszukiwania dziennika, zobacz [Zaloguj wyszukiwania analizy dzienników](log-analytics-log-searches.md).

## <a name="troubleshoot-by-finding-a-failed-container"></a>Rozwiązywanie problemów z znajdując kontenera nie powiodło się

Analiza dzienników oznacza kontener jako **nie powiodło się** Jeśli został zakończony z kodem zakończenia inną niż zero. Można zapoznać się z omówieniem hello błędów i awarii w środowisku hello w hello **nie powiodło się kontenery** obszaru.

### <a name="toofind-failed-containers"></a>kontenery toofind nie powiodło się
1. Kliknij przycisk hello **stan kontenera** obszaru.  
   ![Stan kontenerów](./media/log-analytics-containers/containers-status.png)
2. Dziennik wyszukiwania otwiera i wyświetla stan hello kontenerów, podobne toohello następujące.  
   ![Stan kontenerów](./media/log-analytics-containers/containers-log-search.png)
3. Następnie kliknij przycisk hello agregowane wartości dodatkowych informacji tooview kontenery nie powiodło się. Rozwiń węzeł **Pokaż więcej** identyfikator tooview hello obrazu.  
   ![kontenery nie powiodło się](./media/log-analytics-containers/containers-state-failed.png)  
4. Następnie wpisz następujące hello hello zapytania wyszukiwania. `Type=ContainerInventory <ImageID>`Szczegóły toosee obraz powitania, takich jak rozmiar obrazu i Liczba obrazów zatrzymane, a nie powiodło się.  
   ![kontenery nie powiodło się](./media/log-analytics-containers/containers-failed04.png)

## <a name="search-logs-for-container-data"></a>Dzienniki wyszukiwania danych kontenera
W przypadku Rozwiązywanie problemów z określonego błędu, ułatwia toosee, gdzie występuje w danym środowisku. następujące typy dziennika Hello pomoże Ci tworzenie zapytań tooreturn hello informacje, które mają.


- **ContainerImageInventory** — Użyj tego typu, jeśli próbujesz informacji toofind uporządkowane według obrazu i tooview informacje obrazu, takie jak identyfikatorów obrazów lub rozmiary.
- **ContainerInventory** — tego typu należy używać informacji o lokalizację kontenera, ich nazwy są i jakie obrazy są na nich uruchomione.
- **ContainerLog** — tego typu należy używać toofind błędu dziennika informacji i zapisów.
- **ContainerNodeInventory_CL** tego typu należy używać hello informacji o hoście/węzła gdzie są znajdującej się kontenerów. Umożliwia Docker wersji, typ aranżacji magazynu i informacje o sieci.
- **ContainerProcess_CL** proces hello uruchomiony w kontenerze hello Zobacz Użyj tooquickly tego typu.
- **ContainerServiceLog** — Użyj tego typu, jeśli próbujesz toofind informacji o dzienniku inspekcji dla hello demona Docker, jak uruchamianie, zatrzymywanie, usunąć lub poleceń ściągnięcia.
- **KubeEvents_CL** korzysta z tego typu toosee hello Kubernetes zdarzeń.
- **KubePodInventory_CL** tego typu należy używać toounderstand hello klastra hierarchii informacji.


### <a name="toosearch-logs-for-container-data"></a>toosearch dzienniki dla kontenera danych
* Wybierz obraz, który ostatnio nie powiodło się i znaleźć hello w dzienniku błędów. Uruchom znajdując nazwę kontenera, która działa obrazu z **ContainerInventory** wyszukiwania. Na przykład wyszukaj`Type=ContainerInventory ubuntu Failed`  
    ![Wyszukaj kontenery Ubuntu](./media/log-analytics-containers/search-ubuntu.png)

  Witaj nazwa kontenera hello obok zbyt**nazwa**i poszukaj tych dzienników. W tym przykładzie jest to `Type=ContainerLog cranky_stonebreaker`.

**Wyświetlanie informacji o wydajności**

Gdy jest począwszy od tooconstruct zapytania, może pomóc toosee co to jest możliwe najpierw. Na przykład toosee, które przeszukiwać wszystkie dane dotyczące wydajności, spróbuj hello szerokie zapytania, wpisując następujące zapytanie.

```
Type=Perf
```

![kontenery wydajności](./media/log-analytics-containers/containers-perf01.png)

Zakres danych wydajności hello występują tooa określonego kontenera, wpisując jej nazwę hello toohello prawo do zapytania można określić.

```
Type=Perf <containerName>
```

Który lista hello metryki wydajności, które są zbierane dla poszczególnych kontenera.

![kontenery wydajności](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a>Przykładowe zapytania wyszukiwania dziennika
Toobuild często przydatne jego kwerendę rozpoczynające się przykładem lub dwóch i modyfikuje je po toofit środowiska. Jako punkt początkowy, możesz eksperymentować z hello **przykładowe zapytania** toohelp obszaru tworzenie bardziej zaawansowanych zapytań.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Kontenery zapytań](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a>Zapisywanie dziennika zapytania wyszukiwania
Zapisywanie zapytań jest standardowa funkcja Log Analytics. Zapisując je, należy te, które zostały znalezione przydatne przydatne do użytku w przyszłości.

Po utworzeniu kwerendę, która jest użyteczna, zapisz go, klikając **ulubione** u góry strony wyszukiwania dziennika hello hello. Następnie możesz z łatwością później z hello **Mój pulpit nawigacyjny** strony.

## <a name="next-steps"></a>Następne kroki
* [Wyszukaj dzienniki](log-analytics-log-searches.md) tooview szczegółowe kontenera rekordów danych.
