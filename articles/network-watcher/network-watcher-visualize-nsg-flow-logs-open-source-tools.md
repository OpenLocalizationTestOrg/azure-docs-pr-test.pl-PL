---
title: "rejestruje aaaVisualize przepływu NSG obserwatora sieci Azure przy użyciu narzędzi typu open source | Dokumentacja firmy Microsoft"
description: "Na tej stronie opisano, jak toouse otworzyć źródła narzędzia toovisualize NSG przepływu dzienników."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e9b2dcad-4da4-4d6b-aee2-6d0afade0cb8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 47cb529d4a1e00e8c4c0fa6885cbf72aed3e74c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a>Wizualizuj dzienników przepływu NSG obserwatora sieci Azure przy użyciu narzędzi typu open source

Dzienniki przepływu sieciowej grupy zabezpieczeń zapewniają informacje, które mogą być używane zrozumieć przychodzące i wychodzące ruchu IP na grupy zabezpieczeń sieci. Te dzienniki przepływu Pokaż wychodzących i przepływów przychodzących na podstawie reguł na, hello przepływu hello kart dotyczy, 5 krotki informacje hello przepływu (źródłowego i docelowego adresu IP, portu źródłowego i docelowego protokołu), i jeśli ruch hello został dozwolony lub odrzucany.

Te dzienniki przepływu można analizy toomanually trudne i uzyskaj informacje z. Istnieje jednak kilka narzędzi typu open source, które ułatwiają wizualizowanie tych danych. W tym artykule będzie zawierał te dzienniki przy użyciu hello stosu elastycznych, które będą pozwalają tooquickly indeksu i wizualizacji dzienników przepływu na pulpicie nawigacyjnym Kibana toovisualize rozwiązania.

## <a name="scenario"></a>Scenariusz

W tym artykule skonfigurujemy rozwiązania, które umożliwi dzienników przepływu sieciowej grupy zabezpieczeń toovisualize przy użyciu hello elastycznej stosu.  Dodatek wejściowych Logstash uzyska hello przepływu dzienniki bezpośrednio z obiektu blob magazynu hello skonfigurowane dla zawierający hello przepływu dzienników. Następnie przy użyciu hello stosu elastycznych, hello przepływu dzienniki zostaną zindeksowane i używane toocreate Kibana pulpit nawigacyjny toovisualize hello informacje.

![scenariusz][scenario]

## <a name="steps"></a>Kroki

### <a name="enable-network-security-group-flow-logging"></a>Rejestrowanie przepływu włączyć grupy zabezpieczeń sieci
W tym scenariuszu muszą mieć sieci grupy przepływu rejestrowanie zabezpieczeń włączone na co najmniej jedną grupę zabezpieczeń sieci w ramach Twojego konta. Aby uzyskać instrukcje dotyczące włączania dzienniki przepływu zabezpieczeń sieci, można znaleźć toohello poniższego artykułu [wprowadzenie tooflow rejestrowania dla grup zabezpieczeń sieci](network-watcher-nsg-flow-logging-overview.md).


### <a name="set-up-hello-elastic-stack"></a>Konfigurowanie hello elastycznej stosu
Łącząc NSG przepływu dzienniki z hello stosu elastycznych, możemy utworzyć pulpit nawigacyjny Kibana, co pozwala nam toosearch, wykres, analizowanie i pochodzi z naszych dzienników szczegółowych informacji.

#### <a name="install-elasticsearch"></a>Zainstaluj Elasticsearch

1. Witaj stosu elastycznych w wersji 5.0 i nowszych wymaga Java 8. Uruchom polecenie hello `java -version` toocheck wersji. Jeśli nie masz java instalacji, zapoznaj się toodocumentation na [witryny sieci Web programu Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)
1. Pobierz hello poprawne binarnych systemu:

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    Inne metody instalacji można znaleźć w folderze [Elasticsearch instalacji](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)

1. Sprawdź, czy Elasticsearch jest uruchomiona za pomocą polecenia hello:

    ```
    curl http://127.0.0.1:9200
    ```

    Powinny pojawić się odpowiedzi toothis podobne:

    ```
    {
    "name" : "Angela Del Toro",
    "cluster_name" : "elasticsearch",
    "version" : {
        "number" : "5.2.0",
        "build_hash" : "8ff36d139e16f8720f2947ef62c8167a888992fe",
        "build_timestamp" : "2016-01-27T13:32:39Z",
        "build_snapshot" : false,
        "lucene_version" : "6.1.0"
    },
    "tagline" : "You Know, for Search"
    }
    ```

Dodatkowe instrukcje dotyczące instalowania elastycznej wyszukiwania, można znaleźć strony toohello [instalacji](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)

### <a name="install-logstash"></a>Zainstaluj Logstash

1. tooinstall hello Logstash, uruchom następujące polecenia:

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. Następnie firma Microsoft muszą tooconfigure Logstash tooaccess i analizy dzienników przepływu hello. Tworzenie pliku logstash.conf przy użyciu:

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. Dodaj poniższe plik zawartości toohello hello:

  ```
    input {
      azureblob
        {
            storage_account_name => "mystorageaccount"
            storage_access_key => "storageaccesskey"
            container => "nsgflowlogContainerName"
            codec => "json"
        }
      }

      filter {
        split { field => "[records]" }
        split { field => "[records][properties][flows]"}
        split { field => "[records][properties][flows][flows]"}
        split { field => "[records][properties][flows][flows][flowTuples]"}

     mutate{
      split => { "[records][resourceId]" => "/"}
      add_field => {"Subscription" => "%{[records][resourceId][2]}"
                    "ResourceGroup" => "%{[records][resourceId][4]}"
                    "NetworkSecurityGroup" => "%{[records][resourceId][8]}"}
      convert => {"Subscription" => "string"}
      convert => {"ResourceGroup" => "string"}
      convert => {"NetworkSecurityGroup" => "string"}
      split => { "[records][properties][flows][flows][flowTuples]" => ","}
      add_field => {
                  "unixtimestamp" => "%{[records][properties][flows][flows][flowTuples][0]}"
                  "srcIp" => "%{[records][properties][flows][flows][flowTuples][1]}"
                  "destIp" => "%{[records][properties][flows][flows][flowTuples][2]}"
                  "srcPort" => "%{[records][properties][flows][flows][flowTuples][3]}"
                  "destPort" => "%{[records][properties][flows][flows][flowTuples][4]}"
                  "protocol" => "%{[records][properties][flows][flows][flowTuples][5]}"
                  "trafficflow" => "%{[records][properties][flows][flows][flowTuples][6]}"
                  "traffic" => "%{[records][properties][flows][flows][flowTuples][7]}"
                   }
      convert => {"unixtimestamp" => "integer"}
      convert => {"srcPort" => "integer"}
      convert => {"destPort" => "integer"}        
     }

     date{
       match => ["unixtimestamp" , "UNIX"]
     }
    }

    output {
      stdout { codec => rubydebug }
      elasticsearch {
        hosts => "localhost"
        index => "nsg-flow-logs"
      }
    }  

  ```

Aby uzyskać dalsze instrukcje na temat instalowania Logstash można znaleźć toohello [oficjalnej dokumentacji](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)

### <a name="install-hello-logstash-input-plugin-for-azure-blob-storage"></a>Instalowanie wtyczki wejściowych Logstash hello magazynu obiektów blob platformy Azure

Ten dodatek plug-in Logstash pozwoli dzienników przepływu hello dostępu toodirectly ze swojego konta magazynu wyznaczonego. tooinstall tej wtyczki z katalogu instalacyjnego Logstash domyślne hello (w tym wielkość /usr/share/logstash/bin) uruchom polecenie hello:

```
logstash-plugin install logstash-input-azureblob
```

toostart Logstash, uruchom polecenie hello:

```
sudo /etc/init.d/logstash start
```

Aby uzyskać więcej informacji na temat tej wtyczki można znaleźć toodocumentation [tutaj](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)

### <a name="install-kibana"></a>Zainstaluj Kibana

1. Uruchom następujące polecenia tooinstall Kibana hello:

  ```
  curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
  tar xzvf kibana-5.2.0-linux-x86_64.tar.gz
  ```

1. toorun Kibana przy użyciu poleceń hello:

  ```
  cd kibana-5.2.0-linux-x86_64/
  ./bin/kibana
  ```

1. tooview sieci web Kibana interfejsu kolejno zbyt`http://localhost:5601`
1. W tym scenariuszu wzorzec indeksu hello używany dla dzienników przepływu hello jest "Grupa nsg przepływu dzienniki". Wzorzec indeksu hello w sekcji "wyjściowej" hello pliku logstash.conf mogą ulec zmianie.

1. Pulpit nawigacyjny Kibana hello tooview zdalnie, utworzyć regułę ruchu przychodzącego grupy NSG zezwalania na dostęp za**portu 5601**.

### <a name="create-a-kibana-dashboard"></a>Utwórz pulpit nawigacyjny Kibana

W tym artykule firma Microsoft umieściła przykładowy pulpit nawigacyjny dla Ciebie tooview trendów i szczegóły w alerty.

![rysunek 1][1]

1. Pobierz plik pulpitu nawigacyjnego hello [tutaj](https://aka.ms/networkwatchernsgflowlogdashboard), plik wizualizacji hello [tutaj](https://aka.ms/networkwatchernsgflowlogvisualizations)i hello zapisane wyszukiwania pliku [tutaj](https://aka.ms/networkwatchernsgflowlogsearch).

1. W obszarze hello **zarządzania** kartę z Kibana, przejdź zbyt**zapisane obiektów** i zaimportować wszystkie trzy pliki. Następnie z hello **pulpitu nawigacyjnego** można otworzyć kartę i obciążenia hello przykładowy pulpit nawigacyjny.

Można również utworzyć własne wizualizacje i pulpity nawigacyjne dostosowane do metryki użytkownika. Przeczytaj więcej na temat tworzenia wizualizacje Kibana z jego Kibana [oficjalnej dokumentacji](https://www.elastic.co/guide/en/kibana/current/visualize.html).

### <a name="visualize-nsg-flow-logs"></a>Wizualizuj dzienniki przepływu NSG

Witaj przykładowy pulpit nawigacyjny zapewnia kilka wizualizacje hello przepływu dzienników:

1. Przechodzi przez kierunku/decyzji w miarę upływu czasu — czas serii wykresów przedstawiający hello liczba przepływów w hello przedziale czasu. Można edytować hello jednostka czasu i zakres obu tych wizualizacji. Przepływy przez decyzji pokazuje hello część akceptować lub odrzucać decyzji podjętych podczas przepływów przez kierunek pokazuje hello część ruchu przychodzącego i wychodzącego. Z tych elementów wizualnych można zbadać ruchu trendów w czasie i poszukaj nagłego ani nietypowe wzorce.

  ![Rysunek 2][2]

1. Przechodzi przez Port docelowy/źródłowy — wykresy kołowe przedstawiający podział hello przepływów tootheir odpowiednie porty. Z tym widokiem widać z najczęściej używane porty. Kliknięcie na określonym porcie w obrębie wykresu kołowego hello hello pozostałej części pulpitu nawigacyjnego hello spowoduje filtrowanie dół tooflows tego portu.

  ![figure3][3]

1. Liczba przepływów i najwcześniejszą godzinę dziennika — metryki, wyświetlając hello liczba przepływów i Data hello hello najwcześniejszą dziennika przechwycone.

  ![figure4][4]

1. Przepływy NSG i reguła — wykres słupkowy, wyświetlając dystrybucji hello przepływów w poszczególnych grupach NSG, a także hello dystrybucji reguły w poszczególnych grupach NSG. W tym miejscu można sprawdzić, które grupy NSG i reguły wygenerowany hello większość ruchu.

  ![figure5][5]

1. 10 pierwszych lokalizacja źródłowa/docelowa adresy IP — wykresy słupkowe przedstawiający hello 10 pierwszych źródłowe i docelowe adresy IP. Można dostosować te tooshow wykresy więcej lub mniej top adresów IP. W tym miejscu można Zobacz hello najczęściej występujących adresów IP oraz jak hello decyzji ruchu (zezwalania lub odmowy) wysyłanych do każdego adresu IP.

  ![figure6][6]

1. Przepływ krotek — w poniższej tabeli przedstawiono hello informacji zawartych w poszczególne krotki przepływu, a także jej odpowiednie NGS i reguły.

  ![figure7][7]

Używanie paska zapytania hello u góry hello hello pulpitu nawigacyjnego, można filtrować dół pulpit nawigacyjny hello, zależnie od żadnego parametru przepływów hello, takich jak identyfikator subskrypcji, grupy zasobów, reguły lub innej zmiennej zainteresowań. Aby uzyskać więcej informacji o jego Kibana zapytania i filtrów można znaleźć toohello [oficjalnej dokumentacji](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)

## <a name="conclusion"></a>Podsumowanie

Łącząc hello sieciowej grupy zabezpieczeń przepływu dzienniki z hello elastycznej stosu, mają uzyskujemy toovisualize zaawansowanego, można dostosować sposób naszych ruchu sieciowego. Te pulpity nawigacyjne pozwalają tooquickly korzyści i udostępniać informacji na temat ruchu sieciowego, jak również filtru w dół i zbadaj na wszelkich potencjalnych nieprawidłowości. Przy użyciu Kibana, można dostosować te pulpity nawigacyjne i tworzyć toomeet wizualizacje określonych potrzeb żadnych zabezpieczeń, inspekcji i zgodności.

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak toovisualize Twojego przepływu NSG dzienniki przy użyciu usługi Power BI odwiedzając [wizualizacji NSG przepływa dzienników przy użyciu usługi Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
