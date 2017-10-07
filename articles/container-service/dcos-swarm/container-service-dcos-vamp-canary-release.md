---
title: Wersja aaaCanary z Vamp w klastrze Azure DC/OS | Dokumentacja firmy Microsoft
description: "Jak toouse Vamp toocanary wersji usług i zastosować filtrowanie w klastrze usługi kontenera platformy Azure DC/OS inteligentne ruchu"
services: container-service
author: gggina
manager: rasquill
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/17/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: e7b8658a161a7cddcf718e3e1c12a889a330d3d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a>Mikrousług mozgi wersji z Vamp w klastrze usługi kontenera platformy Azure DC/OS

W tym przewodniku skonfigurujemy Vamp na usługi kontenera platformy Azure z klastrem DC/OS. Możemy mozgi Zwolnij hello Vamp pokaz usługi "sava", a następnie Rozwiąż niezgodności hello usługi z przeglądarki Firefox, stosując filtrowanie ruchu inteligentne. 

> [!TIP] 
> W tym przewodniku Vamp działa w klastrze DC/OS, ale umożliwia także Vamp z Kubernetes jako hello orchestrator.
>

## <a name="about-canary-releases-and-vamp"></a>Temat element canary zwalnia i Vamp


[Zwalnianie mozgi](https://martinfowler.com/bliki/CanaryRelease.html) jest stosowane przez innowacyjnych organizacjami, takimi jak Netflix, Facebook i serwis Spotify strategii wdrażania inteligentne. Jest to sens, ponieważ zmniejsza problemy, wprowadza bezpieczeństwa sieci i zwiększa innowacji podejście. Dlaczego nie wszystkie firmy przy użyciu go? Rozszerzanie tooinclude potoku CI/CD mozgi strategii dodaje złożoność i wymaga devops dużej wiedzy i doświadczenia. To za mało tooblock mniejszych firmami i przedsiębiorstwami podobne przed ich nawet rozpocząć pracę. 

[Vamp](http://vamp.io/) jest tooease systemu open source przeznaczona ten proces przejścia i przełączyć mozgi zwolnić harmonogramu kontenera tooyour preferowany funkcji. Funkcje mozgi vamp firmy wykracza poza wdrożeniach opartych na procentach. Można filtrować ruch i podziału na szeroki zakres warunków, na przykład tootarget określonych użytkowników, zakresy adresów IP lub urządzeń. Vamp śledzi i analizuje metryki wydajności, co pozwala na automatyzację na podstawie danych rzeczywistych. Konfigurowanie automatycznego wycofywania na błędy lub skalować wariantów pojedynczej usługi na podstawie obciążenia lub opóźnienia.

## <a name="set-up-azure-container-service-with-dcos"></a>Konfigurowanie usługi kontenera platformy Azure z DC/OS



1. [Wdrażanie klastra DC/OS](container-service-deployment.md) jeden z nich i dwaj agenci domyślny rozmiar. 

2. [Tworzenie tunelu SSH](../container-service-connect.md) klastra DC/OS toohello tooconnect. W tym artykule przyjęto założenie, że tunelowania toohello klastra lokalnego portu 80.


## <a name="set-up-vamp"></a>Konfigurowanie Vamp

Teraz, gdy masz uruchomiony klastra DC/OS Vamp można zainstalować z hello interfejsu użytkownika DC/OS (http://localhost:80). 

![Interfejs użytkownika platformy DC/OS](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

Instalacja jest przeprowadzana w dwóch etapach:

1. **Wdrażanie Elasticsearch**.

2. Następnie **wdrażanie Vamp** instalując hello Vamp DC/OS universe pakietu.

### <a name="deploy-elasticsearch"></a>Wdrażanie Elasticsearch

Vamp wymaga Elasticsearch zbierania metryk i agregacji. Można użyć hello [obrazy usługi Docker magneticio](https://hub.docker.com/r/magneticio/elastic/) toodeploy zgodne stosu Vamp Elasticsearch.

1. W hello interfejsu użytkownika DC/OS, przejdź do pozycji zbyt**usług** i kliknij przycisk **wdrażanie usługi**.

2. Wybierz **tryb JSON** z hello **wdrożenia nowej usługi** wyskakujących.

  ![Wybierz tryb JSON](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. Wklej hello następującego formatu JSON. Ta konfiguracja jest uruchamiany kontenera hello z 1 GB pamięci RAM i sprawdzenie kondycji podstawowe na porcie Elasticsearch hello.
  
  ```JSON
  {
    "id": "elasticsearch",
    "instances": 1,
    "cpus": 0.2,
    "mem": 1024.0,
    "container": {
      "docker": {
        "image": "magneticio/elastic:2.2",
        "network": "HOST",
        "forcePullImage": true
      }
    },
    "healthChecks": [
      {
        "protocol": "TCP",
        "gracePeriodSeconds": 30,
        "intervalSeconds": 10,
        "timeoutSeconds": 5,
        "port": 9200,
        "maxConsecutiveFailures": 0
      }
    ]
  }
  ```
  

3. Kliknij przycisk **wdrażanie**.

  DC/OS wdraża hello Elasticsearch kontenera. Możesz śledzić postępy na powitania **usług** strony.  

  ![Wdrażanie e? Elasticsearch](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a>Wdrażanie Vamp

Po Elasticsearch raporty jako **systemem**, można dodać hello Vamp Universe DC/OS pakietu. 

1. Przejdź za**Universe** i wyszukaj **vamp**. 
  ![Vamp na universe DC/OS](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)

2. Kliknij przycisk **zainstalować** toohello dalej vamp pakietu, a następnie wybierz pozycję **zaawansowane instalacji**.

3. Przewiń w dół, a następnie wprowadź hello następującego adresu url elasticsearch: `http://elasticsearch.marathon.mesos:9200`. 

  ![Wprowadź adres URL Elasticsearch](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. Kliknij przycisk **Przejrzyj i zainstaluj**, następnie kliknij przycisk **zainstalować** toostart hello wdrożenia.  

  DC/OS wdraża wszystkich wymaganych składników Vamp. Możesz śledzić postępy na powitania **usług** strony.
  
  ![Wdrażanie Vamp jako pakiet universe](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. Po zakończeniu wdrażania, aby dostęp do hello Vamp interfejsu użytkownika:

  ![Usługa vamp na DC/OS](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![Vamp interfejsu użytkownika](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a>Wdrażanie w ramach pierwszej usługi

Teraz tego Vamp jest uruchomiona, należy wdrożyć usługę z planu. 

W najprostszej postaci [planu Vamp](http://vamp.io/documentation/using-vamp/blueprints/) opisuje hello punktów końcowych (bramy), klastrami i toodeploy usług. Vamp używa klastrów toogroup różnych wariantów hello same usługi na grupy logiczne mozgi zwalniania lub A / B testowania.  

W tym scenariuszu przykładowej aplikacji wbudowanymi o nazwie [ **sava**](https://github.com/magneticio/sava), które jest w wersji 1.0. monolityczna Hello jest spakowany w kontenerze Docker, który znajduje się w Centrum Docker w obszarze magneticio/sava:1.0.0. Aplikacja Hello jest uruchamiana normalnie portu 8080, ale ma tooexpose 9050 go w porcie w takim przypadku. Wdrażanie aplikacji hello za pośrednictwem Vamp przy użyciu prostego planu.

1. Przejdź za**wdrożeń**.

2. Kliknij pozycję **Dodaj**.

3. Wklej w hello następującego planu yaml programu. Ten plan zawiera jednego klastra z tylko jedną usługę variant, który możemy zmienić w późniejszym kroku:

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster toocreate
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. Kliknij pozycję **Zapisz**. Vamp inicjuje hello wdrożenia.

Witaj wdrożenia znajduje się na powitania **wdrożeń** strony. Kliknij przycisk toomonitor wdrożenia hello jego stan.

![Vamp interfejsu użytkownika — wdrażanie sava](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![Usługa sava w Vamp interfejsu użytkownika](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

Bramy są tworzone, które są wymienione na powitania **bram** strony:

* Witaj tooaccess stabilna punktu końcowego, usługą (port 9050) 
* zarządzane Vamp wewnętrzny bramy (więcej informacji na temat tej bramy później). 

![Vamp interfejsu użytkownika — sava bram](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

teraz wdrożono Hello sava usługi, ale nie masz dostępu do jego zewnętrznie ponieważ hello modułu równoważenia obciążenia Azure nie może ustalić tooit ruchu tooforward jeszcze. tooaccess hello usługi aktualizacji hello Azure konfiguracji sieci.


## <a name="update-hello-azure-network-configuration"></a>Zaktualizuj konfigurację sieci platformy Azure hello

Usługa sava hello vamp wdrożonych na węzłach agenta DC/OS hello udostępnianie stabilna punktu końcowego w porcie 9050. Usługa hello tooaccess z poza hello klastra DC/OS, tworzy powitania po konfiguracji sieci Azure toohello zmiany we wdrożeniu klastra: 

1. **Skonfiguruj hello modułu równoważenia obciążenia Azure** hello agentów (hello zasób o nazwie **dcos-agent-lb-xxxx**) z sondy kondycji i ruchu tooforward reguły portu 9050 toohello sava wystąpień. 

2. **Grupy zabezpieczeń sieci hello aktualizacji** dla agentów publicznych hello (hello zasób o nazwie **XXXX-agent publicznego nsg-XXXX**) tooallow ruch na porcie 9050.

Aby uzyskać szczegółowy opis kroków toocomplete tych zadań za pomocą hello Azure portalu, zobacz [włączyć aplikacji usługi kontenera platformy Azure tooan dostępu publicznego](container-service-enable-public-access.md). Określ port 9050 dla wszystkich ustawień portu.


Po utworzeniu wszystko Przejdź toohello **omówienie** bloku hello modułu równoważenia obciążenia agenta DC/OS (hello zasób o nazwie **dcos-agent-lb-xxxx**). Znajdź hello **publicznego adresu IP**i użyj hello adres tooaccess sava w porcie 9050.

![Portal Azure — Pobierz publiczny adres IP](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a>Uruchom mozgi zlecenia

Załóżmy, że masz nową wersję tej aplikacji, które mają toocanary wydania do produkcji. Została ona konteneryzowanych jako magneticio/sava:1.1.0 i są gotowe toogo. Vamp umożliwia łatwe dodawanie nowych toohello usługi uruchamiania wdrożenia. Te usługi "scalonych" są wdrożone równolegle z istniejącymi usługami hello w klastrze hello i przypisano wagę % 0. Żaden ruch jest kierowany tooa nowo scalić usługi dostosować hello Dystrybucja ruchu. suwak wagi Hello w hello Vamp interfejsu użytkownika umożliwia pełną kontrolę nad dystrybucji hello, umożliwiające przyrostowe dostosowań (wersja mozgi) lub błyskawicznych wycofywania.

### <a name="merge-a-new-service-variant"></a>Scal nowy wariant usługi

toomerge hello nowej sava 1.1 usługi z hello systemem wdrażania:

1. W hello Vamp interfejsu użytkownika, kliknij przycisk **plany**.

2. Kliknij przycisk **Dodaj** i Wklej w hello następującego planu yaml programu: ten plan zawiera opis nowych toodeploy variant (sava: 1.1.0) usługi w istniejącym klastrze hello (sava_cluster).

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster tooupdate
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint tooupdate
  ```
  
3. Kliknij pozycję **Zapisz**. Plan Hello są przechowywane i wyświetlane na powitania **plany** strony.

4. Menu Akcja Otwórz hello na powitania sava: 1.1 planu, a następnie kliknij przycisk **scalić**.

  ![Vamp interfejsu użytkownika — plany](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. Wybierz hello **sava** wdrożenia i kliknij przycisk **scalania**.

  ![Vamp interfejsu użytkownika — scalania toodeployment planu](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

Vamp wdraża hello nowy sava: 1.1.0 usługi wariant opisanego w plan hello obok sava: 1.0.0 w hello **sava_cluster** z hello uruchamiania wdrożenia. 

![Vamp interfejsu użytkownika — wdrażania sava aktualizacji](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

Witaj **sava/sava_cluster/webport** bramy (punktu końcowego klastra hello) zostaje również zaktualizowany, dodawanie toohello trasy nowo wdrożone sava: 1.1.0. W tym momencie nie ruch jest przekierowywany tutaj (hello **wagi** ustawiono too0%).

![Vamp interfejsu użytkownika — klastra bramy](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a>Mozgi zlecenia

Obie wersje sava wdrożone w hello sam klastra, dostosować hello Dystrybucja ruchu między nimi za pomocą przenoszenia hello **wagi** suwaka.

1. Kliknij przycisk ![Vamp interfejsu użytkownika — Edytuj](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) dalej zbyt**wagi**.

2. Ustaw hello wagi dystrybucji too50%/50% i kliknij przycisk **zapisać**.

  ![Vamp interfejsu użytkownika — suwak wagi bramy](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. Przejdź wstecz tooyour przeglądarki i Odśwież stronę sava hello kilka razy. Teraz aplikacja Hello sava przełącza między strony sava: 1.0 i strony sava: 1.1.

  ![naprzemiennych sava1.0 i sava1.1 usługi](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > Tego wyrażenia warunkowe hello strony działa najlepiej z hello "Incognito" lub "Anonimowo" Tryb przeglądarki z powodu hello buforowanie zasoby statyczne.
  >

### <a name="filter-traffic"></a>Filtrowanie ruchu

Po wdrożeniu Załóżmy, że wykrywane niezgodności w sava: 1.1.0, że powoduje problemy z wyświetlaniem w przeglądarki Firefox. Można ustawić ruch przychodzący toofilter Vamp i bezpośrednie, wszyscy użytkownicy Firefox kopii toohello znane stabilna sava: 1.0.0. Ten filtr natychmiast rozwiązuje hello przerw w działaniu Firefox użytkowników, gdy każdy inny nadal tooenjoy hello zalet hello zwiększona sava: 1.1.0.

Vamp używa **warunki** toofilter ruch między trasy w bramy. Ruch jest najpierw filtrowane i kierowane zgodnie z toohello warunki tooeach trasy. Wszystkie pozostałe ruchu jest dystrybuowane zgodnie z ustawieniem wagi bramy toohello.

Można utworzyć toofilter warunku wszyscy użytkownicy Firefox i kierowania ich toohello starego sava: 1.0.0:

1. Na powitania sava/sava_cluster/webport **bram** kliknij przycisk ![Vamp interfejsu użytkownika — Edytuj](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd **WARUNKU** toohello sava/sava_cluster/sava:1.0.0/webport trasy. 

2. Wprowadź warunek hello **agenta użytkownika przeglądarki Firefox ==** i kliknij przycisk ![Vamp interfejsu użytkownika — Zapisz](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).

  Vamp dodaje warunek hello siły domyślne % 0. filtrowanie ruchu toostart należy tooadjust hello warunku siły.

3. Kliknij przycisk ![Vamp interfejsu użytkownika — Edytuj](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **siły** stosowane toohello warunku.
 
4. Zestaw hello **siły** too100% i kliknij przycisk ![Vamp interfejsu użytkownika — Zapisz](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.

  Vamp teraz wysyła cały ruch dopasowania hello toosava:1.0.0 warunku (wszyscy użytkownicy Firefox).

  ![Vamp UI - zastosowanie toogateway warunku](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. Na koniec należy dostosować hello bramy wagi toosend wszystkie pozostałe ruchu (wszyscy użytkownicy z systemem innym niż Firefox) toohello nowe sava: 1.1.0. Kliknij przycisk ![Vamp interfejsu użytkownika — Edytuj](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) dalej zbyt**wagi** i ustawić dystrybucja wag hello, tak aby toohello bezpośrednie trasy sava/sava_cluster/sava:1.1.0/webport wynosi 100%.

  Cały ruch, które nie są filtrowane według warunku hello jest teraz ukierunkowanej toohello nowe sava: 1.1.0.

6. toosee hello filtru akcji, otwórz dwóch różnych przeglądarkach (jeden Firefox i inną przeglądarkę) i uzyskać dostępu do usługi sava hello z obu. Wszystkie żądania Firefox wysyłane toosava:1.0.0, podczas ukierunkowanych toosava:1.1.0 wszystkich innych przeglądarek.

  ![Vamp interfejsu użytkownika — filtrowania ruchu](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a>Podsumowanie

Ten artykuł został tooVamp szybkie wprowadzenie w klastrze DC/OS. Po pierwsze otrzymano Vamp i systemem w sieci Azure kontenera DC/OS usługi klastra, wdrożyć usługi za pomocą planu Vamp i dostęp do niego w punkcie końcowym hello udostępniane (bramy).

Możemy również dotknięciu na niektóre zaawansowane funkcje Vamp: scalanie nowej usługi variant toohello uruchamiania wdrożenia i wprowadzenie do przyrostowo, a następnie filtrowania ruchu tooresolve znane niezgodności.


## <a name="next-steps"></a>Następne kroki

* Więcej informacji o zarządzaniu Vamp akcji za pomocą hello [Vamp interfejsu API REST](http://vamp.io/documentation/api/api-reference/).

* Tworzenie skryptów automatyzacji Vamp w środowisku Node.js i uruchom je jako [Vamp przepływy pracy](http://vamp.io/documentation/tutorials/create-a-workflow/).

* Zobacz dodatkowe [samouczki VAMP](http://vamp.io/documentation/tutorials/overview/).

