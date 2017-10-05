---
title: "Wykonaj włamań sieci z obserwatora sieciowego Azure i narzędzi typu open source | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób używania obserwatora sieciowego Azure i otworzyć narzędzia źródła do wykonywania wykrywania nieautoryzowanego dostępu sieciowego"
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
ms.openlocfilehash: 82d5e525859ebe03b152c63e4debbae469049c12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="perform-network-intrusion-detection-with-network-watcher-and-open-source-tools"></a><span data-ttu-id="d93af-103">Wykonaj włamań sieci z obserwatora sieciowego i narzędzi typu open source</span><span class="sxs-lookup"><span data-stu-id="d93af-103">Perform network intrusion detection with Network Watcher and open source tools</span></span>

<span data-ttu-id="d93af-104">Pakiet przechwyconych obrazów są kluczowym elementem za zaimplementowanie systemów wykrywania nieautoryzowanego dostępu sieciowego (ID) i przeprowadzanie monitorowania zabezpieczeń sieci (NSM).</span><span class="sxs-lookup"><span data-stu-id="d93af-104">Packet captures are a key component for implementing network intrusion detection systems (IDS) and performing Network Security Monitoring (NSM).</span></span> <span data-ttu-id="d93af-105">Istnieje kilka narzędzi identyfikatorów typu open source, które przetwarzają przechwytywania pakietów i poszukaj podpisami sieci atakami złośliwych działań.</span><span class="sxs-lookup"><span data-stu-id="d93af-105">There are several open source IDS tools that process packet captures and look for signatures of possible network intrusions and malicious activity.</span></span> <span data-ttu-id="d93af-106">Za pomocą pakietu znajdują się pod warunkiem przez obserwatora sieciowego można analizować wtargnięcia szkodliwe lub luk w zabezpieczeniach sieci.</span><span class="sxs-lookup"><span data-stu-id="d93af-106">Using the packet captures provided by Network Watcher, you can analyze your network for any harmful intrusions or vulnerabilities.</span></span>

<span data-ttu-id="d93af-107">Jednym takich narzędzi typu open source jest Suricata, aparat Identyfikatory, który używa zestawów reguł do monitorowania ruchu sieciowego i wyzwala alerty, gdy występują podejrzane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="d93af-107">One such open source tool is Suricata, an IDS engine that uses rulesets to monitor network traffic and triggers alerts whenever suspicious events occur.</span></span> <span data-ttu-id="d93af-108">Suricata oferuje wielowątkowych aparatu, co oznacza, że można wykonać analizy ruchu sieciowego z zwiększenie szybkości i wydajności.</span><span class="sxs-lookup"><span data-stu-id="d93af-108">Suricata offers a multi-threaded engine, meaning it can perform network traffic analysis with increased speed and efficiency.</span></span> <span data-ttu-id="d93af-109">Aby uzyskać więcej informacji na temat Suricata i jego możliwości odwiedź stronę ich https://suricata-ids.org/ witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d93af-109">For more details about Suricata and its capabilities, visit their website at https://suricata-ids.org/.</span></span>

## <a name="scenario"></a><span data-ttu-id="d93af-110">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="d93af-110">Scenario</span></span>

<span data-ttu-id="d93af-111">W tym artykule opisano sposób konfigurowania środowiska w celu wykonania wykrywania nieautoryzowanego dostępu sieciowego przy użyciu obserwatora sieciowego, Suricata i elastyczny stosu.</span><span class="sxs-lookup"><span data-stu-id="d93af-111">This article explains how to set up your environment to perform network intrusion detection using Network Watcher, Suricata, and the Elastic Stack.</span></span> <span data-ttu-id="d93af-112">Obserwatora sieciowego umożliwia przechwytywanie pakietów używane w celu wykonania wykrywania nieautoryzowanego dostępu w sieci.</span><span class="sxs-lookup"><span data-stu-id="d93af-112">Network Watcher provides you with the packet captures used to perform network intrusion detection.</span></span> <span data-ttu-id="d93af-113">Suricata przetwarza przechwytywania pakietów i wyzwalacza alerty oparte na pakietów, które spełniają jego dany zestaw reguł zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="d93af-113">Suricata processes the packet captures and trigger alerts based on packets that match its given ruleset of threats.</span></span> <span data-ttu-id="d93af-114">Te alerty są przechowywane w pliku dziennika na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="d93af-114">These alerts are stored in a log file on your local machine.</span></span> <span data-ttu-id="d93af-115">Przy użyciu elastycznej stosu, dzienniki generowane przez Suricata może być indeksowana i pozwala utworzyć pulpit nawigacyjny Kibana, zapewniając wizualną reprezentację dzienniki i sposób, aby szybko uzyskać wgląd do potencjalnych luk w zabezpieczeniach sieci.</span><span class="sxs-lookup"><span data-stu-id="d93af-115">Using the Elastic Stack, the logs generated by Suricata can be indexed and used to create a Kibana dashboard, providing you with a visual representation of the logs and a means to quickly gain insights to potential network vulnerabilities.</span></span>  

![Scenariusz aplikacji sieci web proste][1]

<span data-ttu-id="d93af-117">Zarówno narzędzi typu open source można skonfigurować na maszynie Wirtualnej platformy Azure, co umożliwia wykonywanie tej analizy w ramach własnego środowiska sieci platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d93af-117">Both open source tools can be set up on an Azure VM, allowing you to perform this analysis within your own Azure network environment.</span></span>

## <a name="steps"></a><span data-ttu-id="d93af-118">Kroki</span><span class="sxs-lookup"><span data-stu-id="d93af-118">Steps</span></span>

### <a name="install-suricata"></a><span data-ttu-id="d93af-119">Zainstaluj Suricata</span><span class="sxs-lookup"><span data-stu-id="d93af-119">Install Suricata</span></span>

<span data-ttu-id="d93af-120">Dla wszystkich innych metod instalacji odwiedź stronę http://suricata.readthedocs.io/en/latest/install.html</span><span class="sxs-lookup"><span data-stu-id="d93af-120">For all other methods of installation, visit http://suricata.readthedocs.io/en/latest/install.html</span></span>

1. <span data-ttu-id="d93af-121">Z poziomu wiersza polecenia terminala z maszyną Wirtualną, uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="d93af-121">In the command-line terminal of your VM run the following commands:</span></span>

    ```
    sudo add-apt-repository ppa:oisf/suricata-stable
    sudo apt-get update
    sudo sudo apt-get install suricata
    ```

1. <span data-ttu-id="d93af-122">Aby zweryfikować instalację, uruchom polecenie `suricata -h` aby zobaczyć pełną listę poleceń.</span><span class="sxs-lookup"><span data-stu-id="d93af-122">To verify your installation, run the command `suricata -h` to see the full list of commands.</span></span>

### <a name="download-the-emerging-threats-ruleset"></a><span data-ttu-id="d93af-123">Pobierz zestaw reguł nowych zagrożeń</span><span class="sxs-lookup"><span data-stu-id="d93af-123">Download the Emerging Threats ruleset</span></span>

<span data-ttu-id="d93af-124">Na tym etapie nie ma żadnych reguł dla Suricata do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="d93af-124">At this stage, we do not have any rules for Suricata to run.</span></span> <span data-ttu-id="d93af-125">Można utworzyć własne reguły, jeśli są określone zagrożenia do sieci, które chcesz wykryć, lub możesz również Użyj rozwinięte zestawy reguł z wielu dostawców, takie jak zagrożenia pojawiające się lub reguły VRT z Snort.</span><span class="sxs-lookup"><span data-stu-id="d93af-125">You can create your own rules if there are specific threats to your network you would like to detect, or you can also use developed rule sets from a number of providers, such as Emerging Threats, or VRT rules from Snort.</span></span> <span data-ttu-id="d93af-126">Ogólnie dostępne ruleset zagrożenia pojawiające się używana tutaj:</span><span class="sxs-lookup"><span data-stu-id="d93af-126">We use the freely accessible Emerging Threats ruleset here:</span></span>

<span data-ttu-id="d93af-127">Pobierz zestaw reguł i skopiuj je do tego katalogu:</span><span class="sxs-lookup"><span data-stu-id="d93af-127">Download the rule set and copy them into the directory:</span></span>

```
wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz
tar zxf emerging.rules.tar.gz
sudo cp -r rules /etc/suricata/
```

### <a name="process-packet-captures-with-suricata"></a><span data-ttu-id="d93af-128">Przechwytywanie pakietów procesu z Suricata</span><span class="sxs-lookup"><span data-stu-id="d93af-128">Process packet captures with Suricata</span></span>

<span data-ttu-id="d93af-129">Przetwarzania pakietu znajdują się za pomocą Suricata, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d93af-129">To process packet captures using Suricata, run the following command:</span></span>

```
sudo suricata -c /etc/suricata/suricata.yaml -r <location_of_pcapfile>
```
<span data-ttu-id="d93af-130">Aby sprawdzić alerty wynikowy, odczytać pliku fast.log:</span><span class="sxs-lookup"><span data-stu-id="d93af-130">To check the resulting alerts, read the fast.log file:</span></span>
```
tail -f /var/log/suricata/fast.log
```

### <a name="set-up-the-elastic-stack"></a><span data-ttu-id="d93af-131">Konfigurowanie elastycznej stosu</span><span class="sxs-lookup"><span data-stu-id="d93af-131">Set up the Elastic Stack</span></span>

<span data-ttu-id="d93af-132">Podczas dzienniki, które tworzy Suricata zawierają cenne informacje o tym, co dzieje się w naszej sieci, te pliki dziennika nie są najłatwiejsze do przeczytane i zrozumiane.</span><span class="sxs-lookup"><span data-stu-id="d93af-132">While the logs that Suricata produces contain valuable information about what’s happening on our network, these log files aren’t the easiest to read and understand.</span></span> <span data-ttu-id="d93af-133">Łącząc Suricata stosu elastycznych, możemy utworzyć pulpit nawigacyjny Kibana co pozwala wyszukiwania, wykresy, analizowanie i pochodzi z naszych dzienników szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="d93af-133">By connecting Suricata with the Elastic Stack, we can create a Kibana dashboard what allows us to search, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="d93af-134">Zainstaluj Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="d93af-134">Install Elasticsearch</span></span>

1. <span data-ttu-id="d93af-135">Elastyczne stosu w wersji 5.0 i nowszych wymaga Java 8.</span><span class="sxs-lookup"><span data-stu-id="d93af-135">The Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="d93af-136">Uruchom polecenie `java -version` do sprawdź wersję.</span><span class="sxs-lookup"><span data-stu-id="d93af-136">Run the command `java -version` to check your version.</span></span> <span data-ttu-id="d93af-137">Jeśli nie masz java instalacji, zapoznaj się z dokumentacją na [witryny sieci Web programu Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="d93af-137">If you do not have java install, refer to documentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="d93af-138">Pobierz poprawny pakiet binarnych systemu:</span><span class="sxs-lookup"><span data-stu-id="d93af-138">Download the correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="d93af-139">Inne metody instalacji można znaleźć w folderze [Elasticsearch instalacji](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span><span class="sxs-lookup"><span data-stu-id="d93af-139">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="d93af-140">Sprawdź, czy Elasticsearch działa przy użyciu polecenia:</span><span class="sxs-lookup"><span data-stu-id="d93af-140">Verify that Elasticsearch is running with the command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="d93af-141">Powinna zostać wyświetlona odpowiedź podobną do poniższego:</span><span class="sxs-lookup"><span data-stu-id="d93af-141">You should see a response similar to this:</span></span>

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

<span data-ttu-id="d93af-142">Dodatkowe instrukcje dotyczące instalowania elastycznej wyszukiwania, można znaleźć na stronie [instalacji](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span><span class="sxs-lookup"><span data-stu-id="d93af-142">For further instructions on installing Elastic search, refer to the page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="d93af-143">Zainstaluj Logstash</span><span class="sxs-lookup"><span data-stu-id="d93af-143">Install Logstash</span></span>

1. <span data-ttu-id="d93af-144">Aby zainstalować Logstash, uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="d93af-144">To install Logstash run the following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="d93af-145">Należy skonfigurować Logstash można odczytać z danych wyjściowych pliku eve.json dalej.</span><span class="sxs-lookup"><span data-stu-id="d93af-145">Next we need to configure Logstash to read from the output of eve.json file.</span></span> <span data-ttu-id="d93af-146">Tworzenie pliku logstash.conf przy użyciu:</span><span class="sxs-lookup"><span data-stu-id="d93af-146">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="d93af-147">Dodaj następującą zawartość do pliku (Upewnij się, że ścieżka do pliku eve.json jest poprawna):</span><span class="sxs-lookup"><span data-stu-id="d93af-147">Add the following content to the file (make sure that the path to the eve.json file is correct):</span></span>

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

1. <span data-ttu-id="d93af-148">Upewnij się udzielić odpowiednich uprawnień do pliku eve.json tak, aby Logstash może obsługiwać pliku.</span><span class="sxs-lookup"><span data-stu-id="d93af-148">Make sure to give the correct permissions to the eve.json file so that Logstash can ingest the file.</span></span>
    
    ```
    sudo chmod 775 /var/log/suricata/eve.json
    ```

1. <span data-ttu-id="d93af-149">Aby uruchomić Logstash, uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="d93af-149">To start Logstash run the command:</span></span>

    ```
    sudo /etc/init.d/logstash start
    ```

<span data-ttu-id="d93af-150">Aby uzyskać dalsze instrukcje na temat instalowania Logstash odwoływać się do [oficjalnej dokumentacji](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="d93af-150">For further instructions on installing Logstash, refer to the [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="d93af-151">Zainstaluj Kibana</span><span class="sxs-lookup"><span data-stu-id="d93af-151">Install Kibana</span></span>

1. <span data-ttu-id="d93af-152">Uruchom następujące polecenia, aby zainstalować Kibana:</span><span class="sxs-lookup"><span data-stu-id="d93af-152">Run the following commands to install Kibana:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
    tar xzvf kibana-5.2.0-linux-x86_64.tar.gz

    ```
1. <span data-ttu-id="d93af-153">Aby uruchomić Kibana należy użyć polecenia:</span><span class="sxs-lookup"><span data-stu-id="d93af-153">To run Kibana use the commands:</span></span>

    ```
    cd kibana-5.2.0-linux-x86_64/
    ./bin/kibana
    ```

1. <span data-ttu-id="d93af-154">Aby wyświetlić Kibana interfejsu sieci web, przejdź do`http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="d93af-154">To view your Kibana web interface, navigate to `http://localhost:5601`</span></span>
1. <span data-ttu-id="d93af-155">W tym scenariuszu jest używane dla dzienników Suricata wzorzec indeksu "logstash-*"</span><span class="sxs-lookup"><span data-stu-id="d93af-155">For this scenario, the index pattern used for the Suricata logs is "logstash-*"</span></span>

1. <span data-ttu-id="d93af-156">Jeśli chcesz wyświetlić pulpit nawigacyjny Kibana zdalnie, Utwórz regułę ruchu przychodzącego grupy NSG zezwalania na dostęp do **portu 5601**.</span><span class="sxs-lookup"><span data-stu-id="d93af-156">If you want to view the Kibana dashboard remotely, create an inbound NSG rule allowing access to **port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="d93af-157">Utwórz pulpit nawigacyjny Kibana</span><span class="sxs-lookup"><span data-stu-id="d93af-157">Create a Kibana dashboard</span></span>

<span data-ttu-id="d93af-158">W tym artykule firma Microsoft umieściła przykładowy pulpit nawigacyjny do wyświetlania trendów i informacji w alerty.</span><span class="sxs-lookup"><span data-stu-id="d93af-158">For this article, we have provided a sample dashboard for you to view trends and details in your alerts.</span></span>

1. <span data-ttu-id="d93af-159">Pobierz plik pulpitu nawigacyjnego [tutaj](https://aka.ms/networkwatchersuricatadashboard), plik wizualizacji [tutaj](https://aka.ms/networkwatchersuricatavisualization), a plikiem zapisanego wyszukiwania [tutaj](https://aka.ms/networkwatchersuricatasavedsearch).</span><span class="sxs-lookup"><span data-stu-id="d93af-159">Download the dashboard file [here](https://aka.ms/networkwatchersuricatadashboard), the visualization file [here](https://aka.ms/networkwatchersuricatavisualization), and the saved search file [here](https://aka.ms/networkwatchersuricatasavedsearch).</span></span>

1. <span data-ttu-id="d93af-160">W obszarze **zarządzania** kartę z Kibana, przejdź do **zapisane obiektów** i zaimportować wszystkie trzy pliki.</span><span class="sxs-lookup"><span data-stu-id="d93af-160">Under the **Management** tab of Kibana, navigate to **Saved Objects** and import all three files.</span></span> <span data-ttu-id="d93af-161">Następnie z **pulpitu nawigacyjnego** kartę można otwierać i załadować przykładowy pulpit nawigacyjny.</span><span class="sxs-lookup"><span data-stu-id="d93af-161">Then from the **Dashboard** tab you can open and load the sample dashboard.</span></span>

<span data-ttu-id="d93af-162">Można również utworzyć własne wizualizacje i pulpity nawigacyjne dostosowane do metryki użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d93af-162">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="d93af-163">Przeczytaj więcej na temat tworzenia wizualizacje Kibana z jego Kibana [oficjalnej dokumentacji](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span><span class="sxs-lookup"><span data-stu-id="d93af-163">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

![pulpit nawigacyjny kibana][2]

### <a name="visualize-ids-alert-logs"></a><span data-ttu-id="d93af-165">Wizualizuj dzienniki alertu Identyfikatory</span><span class="sxs-lookup"><span data-stu-id="d93af-165">Visualize IDS alert logs</span></span>

<span data-ttu-id="d93af-166">Przykładowy pulpit nawigacyjny udostępnia kilka wizualizacje Suricata dzienniki alertu:</span><span class="sxs-lookup"><span data-stu-id="d93af-166">The sample dashboard provides several visualizations of the Suricata alert logs:</span></span>

1. <span data-ttu-id="d93af-167">Alerty według GeoIP — mapa przedstawiająca dystrybucji alertów według kraju pochodzenia na podstawie lokalizacji geograficznej (według adresu IP)</span><span class="sxs-lookup"><span data-stu-id="d93af-167">Alerts by GeoIP – a map showing the distribution of alerts by their country of origin based on geographic location (determined by IP)</span></span>

    ![Geo ip][3]

1. <span data-ttu-id="d93af-169">Pierwszych 10 alertów — podsumowanie 10 najczęściej alertów wyzwalanych i ich opisy.</span><span class="sxs-lookup"><span data-stu-id="d93af-169">Top 10 Alerts – a summary of the 10 most frequent triggered alerts and their description.</span></span> <span data-ttu-id="d93af-170">Kliknięcie przycisku alert indywidualny filtruje dół pulpitu nawigacyjnego do informacji dotyczących tego określony alert.</span><span class="sxs-lookup"><span data-stu-id="d93af-170">Clicking an individual alert filters down the dashboard to the information pertaining to that specific alert.</span></span>

    ![Obraz 4][4]

1. <span data-ttu-id="d93af-172">Liczba alertów — łączna liczba alertów wyzwalanych przez zestaw reguł</span><span class="sxs-lookup"><span data-stu-id="d93af-172">Number of Alerts – the total count of alerts triggered by the ruleset</span></span>

    ![Obraz 5][5]

1. <span data-ttu-id="d93af-174">Wyzwolone na najwyższym 20 lokalizacja źródłowa/docelowa adresy IP/porty — wykresy kołowe przedstawiający górnego 20 adresów IP i portów tego alerty.</span><span class="sxs-lookup"><span data-stu-id="d93af-174">Top 20 Source/Destination IPs/Ports - pie charts showing the top 20 IPs and ports that alerts were triggered on.</span></span> <span data-ttu-id="d93af-175">Można filtrować są inicjowane w dół na określone adresy IP/porty, aby wyświetlić liczbę i typy alertów.</span><span class="sxs-lookup"><span data-stu-id="d93af-175">You can filter down on specific IPs/ports to see how many and what kind of alerts are being triggered.</span></span>

    ![Obraz 6][6]

1. <span data-ttu-id="d93af-177">Podsumowanie alertu — tabelę podsumowania szczegółowe informacje dotyczące każdego alert indywidualny.</span><span class="sxs-lookup"><span data-stu-id="d93af-177">Alert Summary – a table summarizing specific details of each individual alert.</span></span> <span data-ttu-id="d93af-178">Można dostosować tej tabeli, aby wyświetlić inne parametry istotnych dla każdego alertu.</span><span class="sxs-lookup"><span data-stu-id="d93af-178">You can customize this table to show other parameters of interest for each alert.</span></span>

    ![Obraz 7][7]

<span data-ttu-id="d93af-180">Aby uzyskać więcej dokumentacji na temat tworzenia niestandardowych wizualizacje i pulpity nawigacyjne, zobacz [Kibana w oficjalnej dokumentacji](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span><span class="sxs-lookup"><span data-stu-id="d93af-180">For more documentation on creating custom visualizations and dashboards, see [Kibana’s official documentation](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span></span>

## <a name="conclusion"></a><span data-ttu-id="d93af-181">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="d93af-181">Conclusion</span></span>

<span data-ttu-id="d93af-182">Dzięki połączeniu pakietu przechwytuje dostarczane przez obserwatora sieciowego oraz narzędzia identyfikatorów typu open source, takie jak Suricata, można wykonać wykrywania nieautoryzowanego dostępu sieciowego dla szerokiego zakresu zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="d93af-182">By combining packet captures provided by Network Watcher and open source IDS tools such as Suricata, you can perform network intrusion detection for a wide range of threats.</span></span> <span data-ttu-id="d93af-183">Te pulpity nawigacyjne umożliwiają szybkie wychwycenia trendów i anomalii w sieci, jak dobrze dig do danych, aby dowiedzieć się, że główne przyczyny alertów, takie jak agentów złośliwy użytkownik lub narażone portów.</span><span class="sxs-lookup"><span data-stu-id="d93af-183">These dashboards allow you to quickly spot trends and anomalies within your network, as well dig into the data to discover root causes of alerts such as malicious user agents or vulnerable ports.</span></span> <span data-ttu-id="d93af-184">Z tym wyodrębnione dane można podejmowania świadomych decyzji na temat reagowania na ochronę sieci przed atakami wszelkie szkodliwe nieautoryzowanego dostępu i tworzyć reguły uniemożliwia przyszłych dostęp do sieci.</span><span class="sxs-lookup"><span data-stu-id="d93af-184">With this extracted data, you can make informed decisions on how to react to and protect your network from any harmful intrusion attempts, and create rules to prevent future intrusions to your network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d93af-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d93af-185">Next steps</span></span>

<span data-ttu-id="d93af-186">Dowiedz się, jak można wyzwolić przechwytywania pakietów, na podstawie alertów, odwiedzając [celu sieci aktywnego monitorowania za pomocą usługi Azure Functions Użyj przechwytywania pakietów](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="d93af-186">Learn how to trigger packet captures based on alerts by visiting [Use packet capture to do proactive network monitoring with Azure Functions](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="d93af-187">Dowiedz się, jak wizualizacji NSG dzienników przepływu z usługi Power BI, odwiedzając [wizualizacji NSG przepływa dzienników przy użyciu usługi Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="d93af-187">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>



<!-- images -->
[1]: ./media/network-watcher-intrusion-detection-open-source-tools/figure1.png
[2]: ./media/network-watcher-intrusion-detection-open-source-tools/figure2.png
[3]: ./media/network-watcher-intrusion-detection-open-source-tools/figure3.png
[4]: ./media/network-watcher-intrusion-detection-open-source-tools/figure4.png
[5]: ./media/network-watcher-intrusion-detection-open-source-tools/figure5.png
[6]: ./media/network-watcher-intrusion-detection-open-source-tools/figure6.png
[7]: ./media/network-watcher-intrusion-detection-open-source-tools/figure7.png
