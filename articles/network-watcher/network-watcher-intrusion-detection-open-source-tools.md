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
# <a name="perform-network-intrusion-detection-with-network-watcher-and-open-source-tools"></a><span data-ttu-id="df93e-103">Wykonaj włamań sieci z obserwatora sieciowego i narzędzi typu open source</span><span class="sxs-lookup"><span data-stu-id="df93e-103">Perform network intrusion detection with Network Watcher and open source tools</span></span>

<span data-ttu-id="df93e-104">Pakiet przechwyconych obrazów są kluczowym elementem za zaimplementowanie systemów wykrywania nieautoryzowanego dostępu sieciowego (ID) i przeprowadzanie monitorowania zabezpieczeń sieci (NSM).</span><span class="sxs-lookup"><span data-stu-id="df93e-104">Packet captures are a key component for implementing network intrusion detection systems (IDS) and performing Network Security Monitoring (NSM).</span></span> <span data-ttu-id="df93e-105">Istnieje kilka narzędzi identyfikatorów typu open source, które przetwarzają przechwytywania pakietów i poszukaj podpisami sieci atakami złośliwych działań.</span><span class="sxs-lookup"><span data-stu-id="df93e-105">There are several open source IDS tools that process packet captures and look for signatures of possible network intrusions and malicious activity.</span></span> <span data-ttu-id="df93e-106">Przechwytywanie pakietów hello udostępniane przez obserwatora sieciowego można analizować sieci wtargnięcia szkodliwe lub luk w zabezpieczeniach.</span><span class="sxs-lookup"><span data-stu-id="df93e-106">Using hello packet captures provided by Network Watcher, you can analyze your network for any harmful intrusions or vulnerabilities.</span></span>

<span data-ttu-id="df93e-107">Jednym takich narzędzi typu open source jest Suricata, aparat Identyfikatory, który używa ruchu sieciowego toomonitor zestawów reguł i wyzwala alerty, gdy występują podejrzane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="df93e-107">One such open source tool is Suricata, an IDS engine that uses rulesets toomonitor network traffic and triggers alerts whenever suspicious events occur.</span></span> <span data-ttu-id="df93e-108">Suricata oferuje wielowątkowych aparatu, co oznacza, że można wykonać analizy ruchu sieciowego z zwiększenie szybkości i wydajności.</span><span class="sxs-lookup"><span data-stu-id="df93e-108">Suricata offers a multi-threaded engine, meaning it can perform network traffic analysis with increased speed and efficiency.</span></span> <span data-ttu-id="df93e-109">Aby uzyskać więcej informacji na temat Suricata i jego możliwości odwiedź stronę ich https://suricata-ids.org/ witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="df93e-109">For more details about Suricata and its capabilities, visit their website at https://suricata-ids.org/.</span></span>

## <a name="scenario"></a><span data-ttu-id="df93e-110">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="df93e-110">Scenario</span></span>

<span data-ttu-id="df93e-111">W tym artykule opisano sposób tooset się tooperform Twojego środowiska sieci za pomocą Monitora sieci, Suricata, wykrywania nieautoryzowanego dostępu i hello elastycznej stosu.</span><span class="sxs-lookup"><span data-stu-id="df93e-111">This article explains how tooset up your environment tooperform network intrusion detection using Network Watcher, Suricata, and hello Elastic Stack.</span></span> <span data-ttu-id="df93e-112">Zawiera obserwatora sieciowego z pakietów hello przechwytuje tooperform używane sieci włamań.</span><span class="sxs-lookup"><span data-stu-id="df93e-112">Network Watcher provides you with hello packet captures used tooperform network intrusion detection.</span></span> <span data-ttu-id="df93e-113">Przechwytywanie pakietów hello procesy Suricata i wyzwalacza alerty na podstawie pakietów spełniających jego dany zestaw reguł zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="df93e-113">Suricata processes hello packet captures and trigger alerts based on packets that match its given ruleset of threats.</span></span> <span data-ttu-id="df93e-114">Te alerty są przechowywane w pliku dziennika na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="df93e-114">These alerts are stored in a log file on your local machine.</span></span> <span data-ttu-id="df93e-115">Przy użyciu hello stosu elastycznych, hello dzienniki generowane przez Suricata mogą być indeksowane i używać toocreate Kibana pulpitu nawigacyjnego, zapewniając wizualną reprezentację hello dzienniki i oznacza tooquickly korzyści insights toopotential sieci luk w zabezpieczeniach.</span><span class="sxs-lookup"><span data-stu-id="df93e-115">Using hello Elastic Stack, hello logs generated by Suricata can be indexed and used toocreate a Kibana dashboard, providing you with a visual representation of hello logs and a means tooquickly gain insights toopotential network vulnerabilities.</span></span>  

![Scenariusz aplikacji sieci web proste][1]

<span data-ttu-id="df93e-117">Zarówno narzędzi typu open source można skonfigurować na maszynie Wirtualnej platformy Azure, dzięki czemu tooperform analiza w środowisku sieci platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="df93e-117">Both open source tools can be set up on an Azure VM, allowing you tooperform this analysis within your own Azure network environment.</span></span>

## <a name="steps"></a><span data-ttu-id="df93e-118">Kroki</span><span class="sxs-lookup"><span data-stu-id="df93e-118">Steps</span></span>

### <a name="install-suricata"></a><span data-ttu-id="df93e-119">Zainstaluj Suricata</span><span class="sxs-lookup"><span data-stu-id="df93e-119">Install Suricata</span></span>

<span data-ttu-id="df93e-120">Dla wszystkich innych metod instalacji odwiedź stronę http://suricata.readthedocs.io/en/latest/install.html</span><span class="sxs-lookup"><span data-stu-id="df93e-120">For all other methods of installation, visit http://suricata.readthedocs.io/en/latest/install.html</span></span>

1. <span data-ttu-id="df93e-121">W terminalu wiersza polecenia hello maszyny wirtualnej Uruchom hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="df93e-121">In hello command-line terminal of your VM run hello following commands:</span></span>

    ```
    sudo add-apt-repository ppa:oisf/suricata-stable
    sudo apt-get update
    sudo sudo apt-get install suricata
    ```

1. <span data-ttu-id="df93e-122">tooverify instalację, uruchom polecenie hello `suricata -h` toosee hello pełną listę poleceń.</span><span class="sxs-lookup"><span data-stu-id="df93e-122">tooverify your installation, run hello command `suricata -h` toosee hello full list of commands.</span></span>

### <a name="download-hello-emerging-threats-ruleset"></a><span data-ttu-id="df93e-123">Pobierz zestaw reguł zagrożenia pojawiające się hello</span><span class="sxs-lookup"><span data-stu-id="df93e-123">Download hello Emerging Threats ruleset</span></span>

<span data-ttu-id="df93e-124">Na tym etapie nie ma żadnych reguł dla Suricata toorun.</span><span class="sxs-lookup"><span data-stu-id="df93e-124">At this stage, we do not have any rules for Suricata toorun.</span></span> <span data-ttu-id="df93e-125">Można utworzyć własne reguły, jeśli są określone zagrożenia tooyour sieci chcesz toodetect lub możesz również Użyj rozwinięte zestawy reguł z wielu dostawców, takie jak zagrożenia pojawiające się lub reguły VRT z Snort.</span><span class="sxs-lookup"><span data-stu-id="df93e-125">You can create your own rules if there are specific threats tooyour network you would like toodetect, or you can also use developed rule sets from a number of providers, such as Emerging Threats, or VRT rules from Snort.</span></span> <span data-ttu-id="df93e-126">Zestaw reguł zagrożenia pojawiające się ogólnie dostępne hello używana tutaj:</span><span class="sxs-lookup"><span data-stu-id="df93e-126">We use hello freely accessible Emerging Threats ruleset here:</span></span>

<span data-ttu-id="df93e-127">Pobierz zestaw reguł hello i skopiuj je do katalogu hello:</span><span class="sxs-lookup"><span data-stu-id="df93e-127">Download hello rule set and copy them into hello directory:</span></span>

```
wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz
tar zxf emerging.rules.tar.gz
sudo cp -r rules /etc/suricata/
```

### <a name="process-packet-captures-with-suricata"></a><span data-ttu-id="df93e-128">Przechwytywanie pakietów procesu z Suricata</span><span class="sxs-lookup"><span data-stu-id="df93e-128">Process packet captures with Suricata</span></span>

<span data-ttu-id="df93e-129">Przechwytywanie pakietów tooprocess przy użyciu Suricata, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="df93e-129">tooprocess packet captures using Suricata, run hello following command:</span></span>

```
sudo suricata -c /etc/suricata/suricata.yaml -r <location_of_pcapfile>
```
<span data-ttu-id="df93e-130">toocheck hello wynikowy alerty, odczytać pliku fast.log hello:</span><span class="sxs-lookup"><span data-stu-id="df93e-130">toocheck hello resulting alerts, read hello fast.log file:</span></span>
```
tail -f /var/log/suricata/fast.log
```

### <a name="set-up-hello-elastic-stack"></a><span data-ttu-id="df93e-131">Konfigurowanie hello elastycznej stosu</span><span class="sxs-lookup"><span data-stu-id="df93e-131">Set up hello Elastic Stack</span></span>

<span data-ttu-id="df93e-132">Dzienniki hello, które tworzy Suricata zawierają cenne informacje o tym, co dzieje się w naszej sieci, te pliki dziennika nie są tooread najprostszym hello i zrozumieć.</span><span class="sxs-lookup"><span data-stu-id="df93e-132">While hello logs that Suricata produces contain valuable information about what’s happening on our network, these log files aren’t hello easiest tooread and understand.</span></span> <span data-ttu-id="df93e-133">Łącząc Suricata z hello stosu elastycznych, możemy utworzyć pulpit nawigacyjny Kibana, co pozwala nam toosearch, wykres, analizowanie i pochodzi z naszych dzienników szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="df93e-133">By connecting Suricata with hello Elastic Stack, we can create a Kibana dashboard what allows us toosearch, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="df93e-134">Zainstaluj Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="df93e-134">Install Elasticsearch</span></span>

1. <span data-ttu-id="df93e-135">Witaj stosu elastycznych w wersji 5.0 i nowszych wymaga Java 8.</span><span class="sxs-lookup"><span data-stu-id="df93e-135">hello Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="df93e-136">Uruchom polecenie hello `java -version` toocheck wersji.</span><span class="sxs-lookup"><span data-stu-id="df93e-136">Run hello command `java -version` toocheck your version.</span></span> <span data-ttu-id="df93e-137">Jeśli nie masz java instalacji, zapoznaj się toodocumentation na [witryny sieci Web programu Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="df93e-137">If you do not have java install, refer toodocumentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="df93e-138">Pobierz hello poprawne binarnych systemu:</span><span class="sxs-lookup"><span data-stu-id="df93e-138">Download hello correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="df93e-139">Inne metody instalacji można znaleźć w folderze [Elasticsearch instalacji](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span><span class="sxs-lookup"><span data-stu-id="df93e-139">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="df93e-140">Sprawdź, czy Elasticsearch jest uruchomiona za pomocą polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="df93e-140">Verify that Elasticsearch is running with hello command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="df93e-141">Powinny pojawić się odpowiedzi toothis podobne:</span><span class="sxs-lookup"><span data-stu-id="df93e-141">You should see a response similar toothis:</span></span>

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

<span data-ttu-id="df93e-142">Dodatkowe instrukcje dotyczące instalowania elastycznej wyszukiwania, można znaleźć strony toohello [instalacji](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span><span class="sxs-lookup"><span data-stu-id="df93e-142">For further instructions on installing Elastic search, refer toohello page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="df93e-143">Zainstaluj Logstash</span><span class="sxs-lookup"><span data-stu-id="df93e-143">Install Logstash</span></span>

1. <span data-ttu-id="df93e-144">tooinstall hello Logstash, uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="df93e-144">tooinstall Logstash run hello following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="df93e-145">Następnie muszą tooread Logstash tooconfigure z danych wyjściowych hello eve.json pliku.</span><span class="sxs-lookup"><span data-stu-id="df93e-145">Next we need tooconfigure Logstash tooread from hello output of eve.json file.</span></span> <span data-ttu-id="df93e-146">Tworzenie pliku logstash.conf przy użyciu:</span><span class="sxs-lookup"><span data-stu-id="df93e-146">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="df93e-147">Dodaj poniższe plik zawartości toohello hello (Upewnij się, że hello ścieżki toohello eve.json pliku jest poprawna):</span><span class="sxs-lookup"><span data-stu-id="df93e-147">Add hello following content toohello file (make sure that hello path toohello eve.json file is correct):</span></span>

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

1. <span data-ttu-id="df93e-148">Upewnij się, że plik eve.json toohello odpowiednie uprawnienia toogive hello tak, aby Logstash może obsługiwać hello pliku.</span><span class="sxs-lookup"><span data-stu-id="df93e-148">Make sure toogive hello correct permissions toohello eve.json file so that Logstash can ingest hello file.</span></span>
    
    ```
    sudo chmod 775 /var/log/suricata/eve.json
    ```

1. <span data-ttu-id="df93e-149">toostart Logstash, uruchom polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="df93e-149">toostart Logstash run hello command:</span></span>

    ```
    sudo /etc/init.d/logstash start
    ```

<span data-ttu-id="df93e-150">Aby uzyskać dalsze instrukcje na temat instalowania Logstash można znaleźć toohello [oficjalnej dokumentacji](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="df93e-150">For further instructions on installing Logstash, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="df93e-151">Zainstaluj Kibana</span><span class="sxs-lookup"><span data-stu-id="df93e-151">Install Kibana</span></span>

1. <span data-ttu-id="df93e-152">Uruchom następujące polecenia tooinstall Kibana hello:</span><span class="sxs-lookup"><span data-stu-id="df93e-152">Run hello following commands tooinstall Kibana:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
    tar xzvf kibana-5.2.0-linux-x86_64.tar.gz

    ```
1. <span data-ttu-id="df93e-153">toorun Kibana przy użyciu poleceń hello:</span><span class="sxs-lookup"><span data-stu-id="df93e-153">toorun Kibana use hello commands:</span></span>

    ```
    cd kibana-5.2.0-linux-x86_64/
    ./bin/kibana
    ```

1. <span data-ttu-id="df93e-154">tooview sieci web Kibana interfejsu kolejno zbyt`http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="df93e-154">tooview your Kibana web interface, navigate too`http://localhost:5601`</span></span>
1. <span data-ttu-id="df93e-155">W tym scenariuszu jest wzorzec indeksu hello używany dla hello rejestruje Suricata "logstash-*"</span><span class="sxs-lookup"><span data-stu-id="df93e-155">For this scenario, hello index pattern used for hello Suricata logs is "logstash-*"</span></span>

1. <span data-ttu-id="df93e-156">Pulpit nawigacyjny Kibana hello tooview zdalnie, utworzyć regułę ruchu przychodzącego grupy NSG zezwalania na dostęp za**portu 5601**.</span><span class="sxs-lookup"><span data-stu-id="df93e-156">If you want tooview hello Kibana dashboard remotely, create an inbound NSG rule allowing access too**port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="df93e-157">Utwórz pulpit nawigacyjny Kibana</span><span class="sxs-lookup"><span data-stu-id="df93e-157">Create a Kibana dashboard</span></span>

<span data-ttu-id="df93e-158">W tym artykule firma Microsoft umieściła przykładowy pulpit nawigacyjny dla Ciebie tooview trendów i szczegóły w alerty.</span><span class="sxs-lookup"><span data-stu-id="df93e-158">For this article, we have provided a sample dashboard for you tooview trends and details in your alerts.</span></span>

1. <span data-ttu-id="df93e-159">Pobierz plik pulpitu nawigacyjnego hello [tutaj](https://aka.ms/networkwatchersuricatadashboard), plik wizualizacji hello [tutaj](https://aka.ms/networkwatchersuricatavisualization)i hello zapisane wyszukiwania pliku [tutaj](https://aka.ms/networkwatchersuricatasavedsearch).</span><span class="sxs-lookup"><span data-stu-id="df93e-159">Download hello dashboard file [here](https://aka.ms/networkwatchersuricatadashboard), hello visualization file [here](https://aka.ms/networkwatchersuricatavisualization), and hello saved search file [here](https://aka.ms/networkwatchersuricatasavedsearch).</span></span>

1. <span data-ttu-id="df93e-160">W obszarze hello **zarządzania** kartę z Kibana, przejdź zbyt**zapisane obiektów** i zaimportować wszystkie trzy pliki.</span><span class="sxs-lookup"><span data-stu-id="df93e-160">Under hello **Management** tab of Kibana, navigate too**Saved Objects** and import all three files.</span></span> <span data-ttu-id="df93e-161">Następnie z hello **pulpitu nawigacyjnego** można otworzyć kartę i obciążenia hello przykładowy pulpit nawigacyjny.</span><span class="sxs-lookup"><span data-stu-id="df93e-161">Then from hello **Dashboard** tab you can open and load hello sample dashboard.</span></span>

<span data-ttu-id="df93e-162">Można również utworzyć własne wizualizacje i pulpity nawigacyjne dostosowane do metryki użytkownika.</span><span class="sxs-lookup"><span data-stu-id="df93e-162">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="df93e-163">Przeczytaj więcej na temat tworzenia wizualizacje Kibana z jego Kibana [oficjalnej dokumentacji](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span><span class="sxs-lookup"><span data-stu-id="df93e-163">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

![pulpit nawigacyjny kibana][2]

### <a name="visualize-ids-alert-logs"></a><span data-ttu-id="df93e-165">Wizualizuj dzienniki alertu Identyfikatory</span><span class="sxs-lookup"><span data-stu-id="df93e-165">Visualize IDS alert logs</span></span>

<span data-ttu-id="df93e-166">Witaj przykładowy pulpit nawigacyjny zawiera kilka wizualizacje hello Suricata alertu dzienników:</span><span class="sxs-lookup"><span data-stu-id="df93e-166">hello sample dashboard provides several visualizations of hello Suricata alert logs:</span></span>

1. <span data-ttu-id="df93e-167">Alerty według GeoIP — mapa przedstawiająca hello dystrybucji alertów według kraju pochodzenia na podstawie lokalizacji geograficznej (według adresu IP)</span><span class="sxs-lookup"><span data-stu-id="df93e-167">Alerts by GeoIP – a map showing hello distribution of alerts by their country of origin based on geographic location (determined by IP)</span></span>

    ![Geo ip][3]

1. <span data-ttu-id="df93e-169">Pierwszych 10 alertów — Podsumowanie alertów hello 10 najczęściej wyzwalane i ich opisy.</span><span class="sxs-lookup"><span data-stu-id="df93e-169">Top 10 Alerts – a summary of hello 10 most frequent triggered alerts and their description.</span></span> <span data-ttu-id="df93e-170">Kliknięcie przycisku alert indywidualny filtruje dół hello pulpit nawigacyjny toohello informacje dotyczące toothat określony alert.</span><span class="sxs-lookup"><span data-stu-id="df93e-170">Clicking an individual alert filters down hello dashboard toohello information pertaining toothat specific alert.</span></span>

    ![Obraz 4][4]

1. <span data-ttu-id="df93e-172">Liczba alertów — Witaj łącznej liczby alertów wyzwalanych przez zestaw reguł hello</span><span class="sxs-lookup"><span data-stu-id="df93e-172">Number of Alerts – hello total count of alerts triggered by hello ruleset</span></span>

    ![Obraz 5][5]

1. <span data-ttu-id="df93e-174">Pierwsza 20. wg adresów IP źródłowego i docelowego/porty — wykresy kołowe przedstawiający hello górny 20 adresów IP i portów, które alerty wyzwolone na.</span><span class="sxs-lookup"><span data-stu-id="df93e-174">Top 20 Source/Destination IPs/Ports - pie charts showing hello top 20 IPs and ports that alerts were triggered on.</span></span> <span data-ttu-id="df93e-175">Możesz filtrować w dół na określone adresy IP/portów toosee liczbę i typy alertów są inicjowane.</span><span class="sxs-lookup"><span data-stu-id="df93e-175">You can filter down on specific IPs/ports toosee how many and what kind of alerts are being triggered.</span></span>

    ![Obraz 6][6]

1. <span data-ttu-id="df93e-177">Podsumowanie alertu — tabelę podsumowania szczegółowe informacje dotyczące każdego alert indywidualny.</span><span class="sxs-lookup"><span data-stu-id="df93e-177">Alert Summary – a table summarizing specific details of each individual alert.</span></span> <span data-ttu-id="df93e-178">Inne parametry istotnych dla każdego alertu można dostosować tooshow tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="df93e-178">You can customize this table tooshow other parameters of interest for each alert.</span></span>

    ![Obraz 7][7]

<span data-ttu-id="df93e-180">Aby uzyskać więcej dokumentacji na temat tworzenia niestandardowych wizualizacje i pulpity nawigacyjne, zobacz [Kibana w oficjalnej dokumentacji](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span><span class="sxs-lookup"><span data-stu-id="df93e-180">For more documentation on creating custom visualizations and dashboards, see [Kibana’s official documentation](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span></span>

## <a name="conclusion"></a><span data-ttu-id="df93e-181">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="df93e-181">Conclusion</span></span>

<span data-ttu-id="df93e-182">Dzięki połączeniu pakietu przechwytuje dostarczane przez obserwatora sieciowego oraz narzędzia identyfikatorów typu open source, takie jak Suricata, można wykonać wykrywania nieautoryzowanego dostępu sieciowego dla szerokiego zakresu zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="df93e-182">By combining packet captures provided by Network Watcher and open source IDS tools such as Suricata, you can perform network intrusion detection for a wide range of threats.</span></span> <span data-ttu-id="df93e-183">Te pulpity nawigacyjne Zezwalaj, możesz tooquickly dodatkowych trendów i anomalii w sieci, również odnajdywać do powitalne danych toodiscover główne przyczyny alertów, takie jak agentów złośliwy użytkownik lub narażone portów.</span><span class="sxs-lookup"><span data-stu-id="df93e-183">These dashboards allow you tooquickly spot trends and anomalies within your network, as well dig into hello data toodiscover root causes of alerts such as malicious user agents or vulnerable ports.</span></span> <span data-ttu-id="df93e-184">Z tym wyodrębnione dane świadomych decyzji jak tooreact tooand chronić sieć przed atakami wszelkie szkodliwe nieautoryzowanego dostępu i tworzenia reguł tooprevent przyszłych wtargnięcia tooyour sieci.</span><span class="sxs-lookup"><span data-stu-id="df93e-184">With this extracted data, you can make informed decisions on how tooreact tooand protect your network from any harmful intrusion attempts, and create rules tooprevent future intrusions tooyour network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df93e-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="df93e-185">Next steps</span></span>

<span data-ttu-id="df93e-186">Dowiedz się, jak przechwytywanie alerty na podstawie pakietów tootrigger odwiedzając [Użyj pakietów przechwytywania toodo aktywnego monitorowania sieci w środowisku Azure Functions](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="df93e-186">Learn how tootrigger packet captures based on alerts by visiting [Use packet capture toodo proactive network monitoring with Azure Functions](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="df93e-187">Dowiedz się, jak toovisualize Twojego przepływu NSG dzienniki przy użyciu usługi Power BI odwiedzając [wizualizacji NSG przepływa dzienników przy użyciu usługi Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="df93e-187">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>



<!-- images -->
[1]: ./media/network-watcher-intrusion-detection-open-source-tools/figure1.png
[2]: ./media/network-watcher-intrusion-detection-open-source-tools/figure2.png
[3]: ./media/network-watcher-intrusion-detection-open-source-tools/figure3.png
[4]: ./media/network-watcher-intrusion-detection-open-source-tools/figure4.png
[5]: ./media/network-watcher-intrusion-detection-open-source-tools/figure5.png
[6]: ./media/network-watcher-intrusion-detection-open-source-tools/figure6.png
[7]: ./media/network-watcher-intrusion-detection-open-source-tools/figure7.png
