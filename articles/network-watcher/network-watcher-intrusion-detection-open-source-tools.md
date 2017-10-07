---
title: "aaaPerform sieci włamań obserwatora sieciowego Azure i narzędzi typu open source | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toouse obserwatora sieciowego Azure i tooperform narzędzi typu open source sieci wykrywania nieautoryzowanego dostępu"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0f043f08-19e1-4125-98b0-3e335ba69681
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b5a909b827ab32ad6b2fd8e2911a944fd940249e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="perform-network-intrusion-detection-with-network-watcher-and-open-source-tools"></a>Wykonaj włamań sieci z obserwatora sieciowego i narzędzi typu open source

Pakiet przechwyconych obrazów są kluczowym elementem za zaimplementowanie systemów wykrywania nieautoryzowanego dostępu sieciowego (ID) i przeprowadzanie monitorowania zabezpieczeń sieci (NSM). Istnieje kilka narzędzi identyfikatorów typu open source, które przetwarzają przechwytywania pakietów i poszukaj podpisami sieci atakami złośliwych działań. Przechwytywanie pakietów hello udostępniane przez obserwatora sieciowego można analizować sieci wtargnięcia szkodliwe lub luk w zabezpieczeniach.

Jednym takich narzędzi typu open source jest Suricata, aparat Identyfikatory, który używa ruchu sieciowego toomonitor zestawów reguł i wyzwala alerty, gdy występują podejrzane zdarzenia. Suricata oferuje wielowątkowych aparatu, co oznacza, że można wykonać analizy ruchu sieciowego z zwiększenie szybkości i wydajności. Aby uzyskać więcej informacji na temat Suricata i jego możliwości odwiedź stronę ich https://suricata-ids.org/ witryny sieci Web.

## <a name="scenario"></a>Scenariusz

W tym artykule opisano sposób tooset się tooperform Twojego środowiska sieci za pomocą Monitora sieci, Suricata, wykrywania nieautoryzowanego dostępu i hello elastycznej stosu. Zawiera obserwatora sieciowego z pakietów hello przechwytuje tooperform używane sieci włamań. Przechwytywanie pakietów hello procesy Suricata i wyzwalacza alerty na podstawie pakietów spełniających jego dany zestaw reguł zagrożeń. Te alerty są przechowywane w pliku dziennika na komputerze lokalnym. Przy użyciu hello stosu elastycznych, hello dzienniki generowane przez Suricata mogą być indeksowane i używać toocreate Kibana pulpitu nawigacyjnego, zapewniając wizualną reprezentację hello dzienniki i oznacza tooquickly korzyści insights toopotential sieci luk w zabezpieczeniach.  

![Scenariusz aplikacji sieci web proste][1]

Zarówno narzędzi typu open source można skonfigurować na maszynie Wirtualnej platformy Azure, dzięki czemu tooperform analiza w środowisku sieci platformy Azure.

## <a name="steps"></a>Kroki

### <a name="install-suricata"></a>Zainstaluj Suricata

Dla wszystkich innych metod instalacji odwiedź stronę http://suricata.readthedocs.io/en/latest/install.html

1. W terminalu wiersza polecenia hello maszyny wirtualnej Uruchom hello następującego polecenia:

    ```
    sudo add-apt-repository ppa:oisf/suricata-stable
    sudo apt-get update
    sudo sudo apt-get install suricata
    ```

1. tooverify instalację, uruchom polecenie hello `suricata -h` toosee hello pełną listę poleceń.

### <a name="download-hello-emerging-threats-ruleset"></a>Pobierz zestaw reguł zagrożenia pojawiające się hello

Na tym etapie nie ma żadnych reguł dla Suricata toorun. Można utworzyć własne reguły, jeśli są określone zagrożenia tooyour sieci chcesz toodetect lub możesz również Użyj rozwinięte zestawy reguł z wielu dostawców, takie jak zagrożenia pojawiające się lub reguły VRT z Snort. Zestaw reguł zagrożenia pojawiające się ogólnie dostępne hello używana tutaj:

Pobierz zestaw reguł hello i skopiuj je do katalogu hello:

```
wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz
tar zxf emerging.rules.tar.gz
sudo cp -r rules /etc/suricata/
```

### <a name="process-packet-captures-with-suricata"></a>Przechwytywanie pakietów procesu z Suricata

Przechwytywanie pakietów tooprocess przy użyciu Suricata, uruchom następujące polecenie hello:

```
sudo suricata -c /etc/suricata/suricata.yaml -r <location_of_pcapfile>
```
toocheck hello wynikowy alerty, odczytać pliku fast.log hello:
```
tail -f /var/log/suricata/fast.log
```

### <a name="set-up-hello-elastic-stack"></a>Konfigurowanie hello elastycznej stosu

Dzienniki hello, które tworzy Suricata zawierają cenne informacje o tym, co dzieje się w naszej sieci, te pliki dziennika nie są tooread najprostszym hello i zrozumieć. Łącząc Suricata z hello stosu elastycznych, możemy utworzyć pulpit nawigacyjny Kibana, co pozwala nam toosearch, wykres, analizowanie i pochodzi z naszych dzienników szczegółowych informacji.

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
1. Następnie muszą tooread Logstash tooconfigure z danych wyjściowych hello eve.json pliku. Tworzenie pliku logstash.conf przy użyciu:

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. Dodaj poniższe plik zawartości toohello hello (Upewnij się, że hello ścieżki toohello eve.json pliku jest poprawna):

    ```ruby
    input {
    file {
        path => ["/var/log/suricata/eve.json"]
        codec =>  "json"
        type => "SuricataIDPS"
    }

    }

    filter {
    if [type] == "SuricataIDPS" {
        date {
        match => [ "timestamp", "ISO8601" ]
        }
        ruby {
        code => "
            if event.get('[event_type]') == 'fileinfo'
            event.set('[fileinfo][type]', event.get('[fileinfo][magic]').to_s.split(',')[0])
            end
        "
        }

        ruby{
        code => "
            if event.get('[event_type]') == 'alert'
            sp = event.get('[alert][signature]').to_s.split(' group ')
            if (sp.length == 2) and /\A\d+\z/.match(sp[1])
                event.set('[alert][signature]', sp[0])
            end
            end
            "
        }
    }

    if [src_ip]  {
        geoip {
        source => "src_ip"
        target => "geoip"
        #database => "/opt/logstash/vendor/geoip/GeoLiteCity.dat"
        add_field => [ "[geoip][coordinates]", "%{[geoip][longitude]}" ]
        add_field => [ "[geoip][coordinates]", "%{[geoip][latitude]}"  ]
        }
        mutate {
        convert => [ "[geoip][coordinates]", "float" ]
        }
        if ![geoip.ip] {
        if [dest_ip]  {
            geoip {
            source => "dest_ip"
            target => "geoip"
            #database => "/opt/logstash/vendor/geoip/GeoLiteCity.dat"
            add_field => [ "[geoip][coordinates]", "%{[geoip][longitude]}" ]
            add_field => [ "[geoip][coordinates]", "%{[geoip][latitude]}"  ]
            }
            mutate {
            convert => [ "[geoip][coordinates]", "float" ]
            }
        }
        }
    }
    }

    output {
    elasticsearch {
        hosts => "localhost"
    }
    }
    ```

1. Upewnij się, że plik eve.json toohello odpowiednie uprawnienia toogive hello tak, aby Logstash może obsługiwać hello pliku.
    
    ```
    sudo chmod 775 /var/log/suricata/eve.json
    ```

1. toostart Logstash, uruchom polecenie hello:

    ```
    sudo /etc/init.d/logstash start
    ```

Aby uzyskać dalsze instrukcje na temat instalowania Logstash można znaleźć toohello [oficjalnej dokumentacji](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)

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
1. W tym scenariuszu jest wzorzec indeksu hello używany dla hello rejestruje Suricata "logstash-*"

1. Pulpit nawigacyjny Kibana hello tooview zdalnie, utworzyć regułę ruchu przychodzącego grupy NSG zezwalania na dostęp za**portu 5601**.

### <a name="create-a-kibana-dashboard"></a>Utwórz pulpit nawigacyjny Kibana

W tym artykule firma Microsoft umieściła przykładowy pulpit nawigacyjny dla Ciebie tooview trendów i szczegóły w alerty.

1. Pobierz plik pulpitu nawigacyjnego hello [tutaj](https://aka.ms/networkwatchersuricatadashboard), plik wizualizacji hello [tutaj](https://aka.ms/networkwatchersuricatavisualization)i hello zapisane wyszukiwania pliku [tutaj](https://aka.ms/networkwatchersuricatasavedsearch).

1. W obszarze hello **zarządzania** kartę z Kibana, przejdź zbyt**zapisane obiektów** i zaimportować wszystkie trzy pliki. Następnie z hello **pulpitu nawigacyjnego** można otworzyć kartę i obciążenia hello przykładowy pulpit nawigacyjny.

Można również utworzyć własne wizualizacje i pulpity nawigacyjne dostosowane do metryki użytkownika. Przeczytaj więcej na temat tworzenia wizualizacje Kibana z jego Kibana [oficjalnej dokumentacji](https://www.elastic.co/guide/en/kibana/current/visualize.html).

![pulpit nawigacyjny kibana][2]

### <a name="visualize-ids-alert-logs"></a>Wizualizuj dzienniki alertu Identyfikatory

Witaj przykładowy pulpit nawigacyjny zawiera kilka wizualizacje hello Suricata alertu dzienników:

1. Alerty według GeoIP — mapa przedstawiająca hello dystrybucji alertów według kraju pochodzenia na podstawie lokalizacji geograficznej (według adresu IP)

    ![Geo ip][3]

1. Pierwszych 10 alertów — Podsumowanie alertów hello 10 najczęściej wyzwalane i ich opisy. Kliknięcie przycisku alert indywidualny filtruje dół hello pulpit nawigacyjny toohello informacje dotyczące toothat określony alert.

    ![Obraz 4][4]

1. Liczba alertów — Witaj łącznej liczby alertów wyzwalanych przez zestaw reguł hello

    ![Obraz 5][5]

1. Pierwsza 20. wg adresów IP źródłowego i docelowego/porty — wykresy kołowe przedstawiający hello górny 20 adresów IP i portów, które alerty wyzwolone na. Możesz filtrować w dół na określone adresy IP/portów toosee liczbę i typy alertów są inicjowane.

    ![Obraz 6][6]

1. Podsumowanie alertu — tabelę podsumowania szczegółowe informacje dotyczące każdego alert indywidualny. Inne parametry istotnych dla każdego alertu można dostosować tooshow tej tabeli.

    ![Obraz 7][7]

Aby uzyskać więcej dokumentacji na temat tworzenia niestandardowych wizualizacje i pulpity nawigacyjne, zobacz [Kibana w oficjalnej dokumentacji](https://www.elastic.co/guide/en/kibana/current/introduction.html).

## <a name="conclusion"></a>Podsumowanie

Dzięki połączeniu pakietu przechwytuje dostarczane przez obserwatora sieciowego oraz narzędzia identyfikatorów typu open source, takie jak Suricata, można wykonać wykrywania nieautoryzowanego dostępu sieciowego dla szerokiego zakresu zagrożeń. Te pulpity nawigacyjne Zezwalaj, możesz tooquickly dodatkowych trendów i anomalii w sieci, również odnajdywać do powitalne danych toodiscover główne przyczyny alertów, takie jak agentów złośliwy użytkownik lub narażone portów. Z tym wyodrębnione dane świadomych decyzji jak tooreact tooand chronić sieć przed atakami wszelkie szkodliwe nieautoryzowanego dostępu i tworzenia reguł tooprevent przyszłych wtargnięcia tooyour sieci.

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak przechwytywanie alerty na podstawie pakietów tootrigger odwiedzając [Użyj pakietów przechwytywania toodo aktywnego monitorowania sieci w środowisku Azure Functions](network-watcher-alert-triggered-packet-capture.md)

Dowiedz się, jak toovisualize Twojego przepływu NSG dzienniki przy użyciu usługi Power BI odwiedzając [wizualizacji NSG przepływa dzienników przy użyciu usługi Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)



<!-- images -->
[1]: ./media/network-watcher-intrusion-detection-open-source-tools/figure1.png
[2]: ./media/network-watcher-intrusion-detection-open-source-tools/figure2.png
[3]: ./media/network-watcher-intrusion-detection-open-source-tools/figure3.png
[4]: ./media/network-watcher-intrusion-detection-open-source-tools/figure4.png
[5]: ./media/network-watcher-intrusion-detection-open-source-tools/figure5.png
[6]: ./media/network-watcher-intrusion-detection-open-source-tools/figure6.png
[7]: ./media/network-watcher-intrusion-detection-open-source-tools/figure7.png
