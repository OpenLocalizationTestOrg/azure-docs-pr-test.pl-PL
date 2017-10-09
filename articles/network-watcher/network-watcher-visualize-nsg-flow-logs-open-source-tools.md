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
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a><span data-ttu-id="3b785-103">Wizualizuj dzienników przepływu NSG obserwatora sieci Azure przy użyciu narzędzi typu open source</span><span class="sxs-lookup"><span data-stu-id="3b785-103">Visualize Azure Network Watcher NSG flow logs using open source tools</span></span>

<span data-ttu-id="3b785-104">Dzienniki przepływu sieciowej grupy zabezpieczeń zapewniają informacje, które mogą być używane zrozumieć przychodzące i wychodzące ruchu IP na grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="3b785-104">Network Security Group flow logs provide information that can be used understand ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="3b785-105">Te dzienniki przepływu Pokaż wychodzących i przepływów przychodzących na podstawie reguł na, hello przepływu hello kart dotyczy, 5 krotki informacje hello przepływu (źródłowego i docelowego adresu IP, portu źródłowego i docelowego protokołu), i jeśli ruch hello został dozwolony lub odrzucany.</span><span class="sxs-lookup"><span data-stu-id="3b785-105">These flow logs show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5 tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="3b785-106">Te dzienniki przepływu można analizy toomanually trudne i uzyskaj informacje z.</span><span class="sxs-lookup"><span data-stu-id="3b785-106">These flow logs can be difficult toomanually parse and gain insights from.</span></span> <span data-ttu-id="3b785-107">Istnieje jednak kilka narzędzi typu open source, które ułatwiają wizualizowanie tych danych.</span><span class="sxs-lookup"><span data-stu-id="3b785-107">However, there are several open source tools that can help visualize this data.</span></span> <span data-ttu-id="3b785-108">W tym artykule będzie zawierał te dzienniki przy użyciu hello stosu elastycznych, które będą pozwalają tooquickly indeksu i wizualizacji dzienników przepływu na pulpicie nawigacyjnym Kibana toovisualize rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="3b785-108">This article will provide a solution toovisualize these logs using hello Elastic Stack, which will allow you tooquickly index and visualize your flow logs on a Kibana dashboard.</span></span>

## <a name="scenario"></a><span data-ttu-id="3b785-109">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="3b785-109">Scenario</span></span>

<span data-ttu-id="3b785-110">W tym artykule skonfigurujemy rozwiązania, które umożliwi dzienników przepływu sieciowej grupy zabezpieczeń toovisualize przy użyciu hello elastycznej stosu.</span><span class="sxs-lookup"><span data-stu-id="3b785-110">In this article, we will set up a solution that will allow you toovisualize Network Security Group flow logs using hello Elastic Stack.</span></span>  <span data-ttu-id="3b785-111">Dodatek wejściowych Logstash uzyska hello przepływu dzienniki bezpośrednio z obiektu blob magazynu hello skonfigurowane dla zawierający hello przepływu dzienników.</span><span class="sxs-lookup"><span data-stu-id="3b785-111">A Logstash input plugin will obtain hello flow logs directly from hello storage blob configured for containing hello flow logs.</span></span> <span data-ttu-id="3b785-112">Następnie przy użyciu hello stosu elastycznych, hello przepływu dzienniki zostaną zindeksowane i używane toocreate Kibana pulpit nawigacyjny toovisualize hello informacje.</span><span class="sxs-lookup"><span data-stu-id="3b785-112">Then, using hello Elastic Stack, hello flow logs will be indexed and used toocreate a Kibana dashboard toovisualize hello information.</span></span>

![scenariusz][scenario]

## <a name="steps"></a><span data-ttu-id="3b785-114">Kroki</span><span class="sxs-lookup"><span data-stu-id="3b785-114">Steps</span></span>

### <a name="enable-network-security-group-flow-logging"></a><span data-ttu-id="3b785-115">Rejestrowanie przepływu włączyć grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="3b785-115">Enable Network Security Group flow logging</span></span>
<span data-ttu-id="3b785-116">W tym scenariuszu muszą mieć sieci grupy przepływu rejestrowanie zabezpieczeń włączone na co najmniej jedną grupę zabezpieczeń sieci w ramach Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="3b785-116">For this scenario, you must have Network Security Group Flow Logging enabled on at least one Network Security Group in your account.</span></span> <span data-ttu-id="3b785-117">Aby uzyskać instrukcje dotyczące włączania dzienniki przepływu zabezpieczeń sieci, można znaleźć toohello poniższego artykułu [wprowadzenie tooflow rejestrowania dla grup zabezpieczeń sieci](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3b785-117">For instructions on enabling Network Security Flow Logs, refer toohello following article [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>


### <a name="set-up-hello-elastic-stack"></a><span data-ttu-id="3b785-118">Konfigurowanie hello elastycznej stosu</span><span class="sxs-lookup"><span data-stu-id="3b785-118">Set up hello Elastic Stack</span></span>
<span data-ttu-id="3b785-119">Łącząc NSG przepływu dzienniki z hello stosu elastycznych, możemy utworzyć pulpit nawigacyjny Kibana, co pozwala nam toosearch, wykres, analizowanie i pochodzi z naszych dzienników szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="3b785-119">By connecting NSG flow logs with hello Elastic Stack, we can create a Kibana dashboard what allows us toosearch, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="3b785-120">Zainstaluj Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="3b785-120">Install Elasticsearch</span></span>

1. <span data-ttu-id="3b785-121">Witaj stosu elastycznych w wersji 5.0 i nowszych wymaga Java 8.</span><span class="sxs-lookup"><span data-stu-id="3b785-121">hello Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="3b785-122">Uruchom polecenie hello `java -version` toocheck wersji.</span><span class="sxs-lookup"><span data-stu-id="3b785-122">Run hello command `java -version` toocheck your version.</span></span> <span data-ttu-id="3b785-123">Jeśli nie masz java instalacji, zapoznaj się toodocumentation na [witryny sieci Web programu Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="3b785-123">If you do not have java install, refer toodocumentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="3b785-124">Pobierz hello poprawne binarnych systemu:</span><span class="sxs-lookup"><span data-stu-id="3b785-124">Download hello correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="3b785-125">Inne metody instalacji można znaleźć w folderze [Elasticsearch instalacji](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span><span class="sxs-lookup"><span data-stu-id="3b785-125">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="3b785-126">Sprawdź, czy Elasticsearch jest uruchomiona za pomocą polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="3b785-126">Verify that Elasticsearch is running with hello command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="3b785-127">Powinny pojawić się odpowiedzi toothis podobne:</span><span class="sxs-lookup"><span data-stu-id="3b785-127">You should see a response similar toothis:</span></span>

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

<span data-ttu-id="3b785-128">Dodatkowe instrukcje dotyczące instalowania elastycznej wyszukiwania, można znaleźć strony toohello [instalacji](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span><span class="sxs-lookup"><span data-stu-id="3b785-128">For further instructions on installing Elastic search, refer toohello page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="3b785-129">Zainstaluj Logstash</span><span class="sxs-lookup"><span data-stu-id="3b785-129">Install Logstash</span></span>

1. <span data-ttu-id="3b785-130">tooinstall hello Logstash, uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="3b785-130">tooinstall Logstash run hello following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="3b785-131">Następnie firma Microsoft muszą tooconfigure Logstash tooaccess i analizy dzienników przepływu hello.</span><span class="sxs-lookup"><span data-stu-id="3b785-131">Next we need tooconfigure Logstash tooaccess and parse hello flow logs.</span></span> <span data-ttu-id="3b785-132">Tworzenie pliku logstash.conf przy użyciu:</span><span class="sxs-lookup"><span data-stu-id="3b785-132">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="3b785-133">Dodaj poniższe plik zawartości toohello hello:</span><span class="sxs-lookup"><span data-stu-id="3b785-133">Add hello following content toohello file:</span></span>

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

<span data-ttu-id="3b785-134">Aby uzyskać dalsze instrukcje na temat instalowania Logstash można znaleźć toohello [oficjalnej dokumentacji](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="3b785-134">For further instructions on installing Logstash, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-hello-logstash-input-plugin-for-azure-blob-storage"></a><span data-ttu-id="3b785-135">Instalowanie wtyczki wejściowych Logstash hello magazynu obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3b785-135">Install hello Logstash input plugin for Azure blob storage</span></span>

<span data-ttu-id="3b785-136">Ten dodatek plug-in Logstash pozwoli dzienników przepływu hello dostępu toodirectly ze swojego konta magazynu wyznaczonego.</span><span class="sxs-lookup"><span data-stu-id="3b785-136">This Logstash plugin will allow you toodirectly access hello flow logs from their designated storage account.</span></span> <span data-ttu-id="3b785-137">tooinstall tej wtyczki z katalogu instalacyjnego Logstash domyślne hello (w tym wielkość /usr/share/logstash/bin) uruchom polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="3b785-137">tooinstall this plugin, from hello default Logstash installation directory (in this case /usr/share/logstash/bin) run hello command:</span></span>

```
logstash-plugin install logstash-input-azureblob
```

<span data-ttu-id="3b785-138">toostart Logstash, uruchom polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="3b785-138">toostart Logstash run hello command:</span></span>

```
sudo /etc/init.d/logstash start
```

<span data-ttu-id="3b785-139">Aby uzyskać więcej informacji na temat tej wtyczki można znaleźć toodocumentation [tutaj](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span><span class="sxs-lookup"><span data-stu-id="3b785-139">For more information about this plugin, refer toodocumentation [here](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="3b785-140">Zainstaluj Kibana</span><span class="sxs-lookup"><span data-stu-id="3b785-140">Install Kibana</span></span>

1. <span data-ttu-id="3b785-141">Uruchom następujące polecenia tooinstall Kibana hello:</span><span class="sxs-lookup"><span data-stu-id="3b785-141">Run hello following commands tooinstall Kibana:</span></span>

  ```
  curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
  tar xzvf kibana-5.2.0-linux-x86_64.tar.gz
  ```

1. <span data-ttu-id="3b785-142">toorun Kibana przy użyciu poleceń hello:</span><span class="sxs-lookup"><span data-stu-id="3b785-142">toorun Kibana use hello commands:</span></span>

  ```
  cd kibana-5.2.0-linux-x86_64/
  ./bin/kibana
  ```

1. <span data-ttu-id="3b785-143">tooview sieci web Kibana interfejsu kolejno zbyt`http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="3b785-143">tooview your Kibana web interface, navigate too`http://localhost:5601`</span></span>
1. <span data-ttu-id="3b785-144">W tym scenariuszu wzorzec indeksu hello używany dla dzienników przepływu hello jest "Grupa nsg przepływu dzienniki".</span><span class="sxs-lookup"><span data-stu-id="3b785-144">For this scenario, hello index pattern used for hello flow logs is "nsg-flow-logs".</span></span> <span data-ttu-id="3b785-145">Wzorzec indeksu hello w sekcji "wyjściowej" hello pliku logstash.conf mogą ulec zmianie.</span><span class="sxs-lookup"><span data-stu-id="3b785-145">You may change hello index pattern in hello "output" section of your logstash.conf file.</span></span>

1. <span data-ttu-id="3b785-146">Pulpit nawigacyjny Kibana hello tooview zdalnie, utworzyć regułę ruchu przychodzącego grupy NSG zezwalania na dostęp za**portu 5601**.</span><span class="sxs-lookup"><span data-stu-id="3b785-146">If you want tooview hello Kibana dashboard remotely, create an inbound NSG rule allowing access too**port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="3b785-147">Utwórz pulpit nawigacyjny Kibana</span><span class="sxs-lookup"><span data-stu-id="3b785-147">Create a Kibana dashboard</span></span>

<span data-ttu-id="3b785-148">W tym artykule firma Microsoft umieściła przykładowy pulpit nawigacyjny dla Ciebie tooview trendów i szczegóły w alerty.</span><span class="sxs-lookup"><span data-stu-id="3b785-148">For this article, we have provided a sample dashboard for you tooview trends and details in your alerts.</span></span>

![rysunek 1][1]

1. <span data-ttu-id="3b785-150">Pobierz plik pulpitu nawigacyjnego hello [tutaj](https://aka.ms/networkwatchernsgflowlogdashboard), plik wizualizacji hello [tutaj](https://aka.ms/networkwatchernsgflowlogvisualizations)i hello zapisane wyszukiwania pliku [tutaj](https://aka.ms/networkwatchernsgflowlogsearch).</span><span class="sxs-lookup"><span data-stu-id="3b785-150">Download hello dashboard file [here](https://aka.ms/networkwatchernsgflowlogdashboard), hello visualization file [here](https://aka.ms/networkwatchernsgflowlogvisualizations), and hello saved search file [here](https://aka.ms/networkwatchernsgflowlogsearch).</span></span>

1. <span data-ttu-id="3b785-151">W obszarze hello **zarządzania** kartę z Kibana, przejdź zbyt**zapisane obiektów** i zaimportować wszystkie trzy pliki.</span><span class="sxs-lookup"><span data-stu-id="3b785-151">Under hello **Management** tab of Kibana, navigate too**Saved Objects** and import all three files.</span></span> <span data-ttu-id="3b785-152">Następnie z hello **pulpitu nawigacyjnego** można otworzyć kartę i obciążenia hello przykładowy pulpit nawigacyjny.</span><span class="sxs-lookup"><span data-stu-id="3b785-152">Then from hello **Dashboard** tab you can open and load hello sample dashboard.</span></span>

<span data-ttu-id="3b785-153">Można również utworzyć własne wizualizacje i pulpity nawigacyjne dostosowane do metryki użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3b785-153">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="3b785-154">Przeczytaj więcej na temat tworzenia wizualizacje Kibana z jego Kibana [oficjalnej dokumentacji](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span><span class="sxs-lookup"><span data-stu-id="3b785-154">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

### <a name="visualize-nsg-flow-logs"></a><span data-ttu-id="3b785-155">Wizualizuj dzienniki przepływu NSG</span><span class="sxs-lookup"><span data-stu-id="3b785-155">Visualize NSG flow logs</span></span>

<span data-ttu-id="3b785-156">Witaj przykładowy pulpit nawigacyjny zapewnia kilka wizualizacje hello przepływu dzienników:</span><span class="sxs-lookup"><span data-stu-id="3b785-156">hello sample dashboard provides several visualizations of hello flow logs:</span></span>

1. <span data-ttu-id="3b785-157">Przechodzi przez kierunku/decyzji w miarę upływu czasu — czas serii wykresów przedstawiający hello liczba przepływów w hello przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="3b785-157">Flows by Decision/Direction Over Time - time series graphs showing hello number of flows over hello time period.</span></span> <span data-ttu-id="3b785-158">Można edytować hello jednostka czasu i zakres obu tych wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="3b785-158">You can edit hello unit of time and span of both these visualizations.</span></span> <span data-ttu-id="3b785-159">Przepływy przez decyzji pokazuje hello część akceptować lub odrzucać decyzji podjętych podczas przepływów przez kierunek pokazuje hello część ruchu przychodzącego i wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="3b785-159">Flows by Decision shows hello proportion of allow or deny decisions made, while Flows by Direction shows hello proportion of inbound and outbound traffic.</span></span> <span data-ttu-id="3b785-160">Z tych elementów wizualnych można zbadać ruchu trendów w czasie i poszukaj nagłego ani nietypowe wzorce.</span><span class="sxs-lookup"><span data-stu-id="3b785-160">With these visuals you can examine traffic trends over time and look for any spikes or unusual patterns.</span></span>

  ![Rysunek 2][2]

1. <span data-ttu-id="3b785-162">Przechodzi przez Port docelowy/źródłowy — wykresy kołowe przedstawiający podział hello przepływów tootheir odpowiednie porty.</span><span class="sxs-lookup"><span data-stu-id="3b785-162">Flows by Destination/Source Port – pie charts showing hello breakdown of flows tootheir respective ports.</span></span> <span data-ttu-id="3b785-163">Z tym widokiem widać z najczęściej używane porty.</span><span class="sxs-lookup"><span data-stu-id="3b785-163">With this view you can see your most commonly used ports.</span></span> <span data-ttu-id="3b785-164">Kliknięcie na określonym porcie w obrębie wykresu kołowego hello hello pozostałej części pulpitu nawigacyjnego hello spowoduje filtrowanie dół tooflows tego portu.</span><span class="sxs-lookup"><span data-stu-id="3b785-164">If you click on a specific port within hello pie chart, hello rest of hello dashboard will filter down tooflows of that port.</span></span>

  ![figure3][3]

1. <span data-ttu-id="3b785-166">Liczba przepływów i najwcześniejszą godzinę dziennika — metryki, wyświetlając hello liczba przepływów i Data hello hello najwcześniejszą dziennika przechwycone.</span><span class="sxs-lookup"><span data-stu-id="3b785-166">Number of Flows and Earliest Log Time – metrics showing you hello number of flows recorded and hello date of hello earliest log captured.</span></span>

  ![figure4][4]

1. <span data-ttu-id="3b785-168">Przepływy NSG i reguła — wykres słupkowy, wyświetlając dystrybucji hello przepływów w poszczególnych grupach NSG, a także hello dystrybucji reguły w poszczególnych grupach NSG.</span><span class="sxs-lookup"><span data-stu-id="3b785-168">Flows by NSG and Rule – a bar graph showing you hello distribution of flows within each NSG, as well as hello distribution of rules within each NSG.</span></span> <span data-ttu-id="3b785-169">W tym miejscu można sprawdzić, które grupy NSG i reguły wygenerowany hello większość ruchu.</span><span class="sxs-lookup"><span data-stu-id="3b785-169">From here you can see which NSG and rules generated hello most traffic.</span></span>

  ![figure5][5]

1. <span data-ttu-id="3b785-171">10 pierwszych lokalizacja źródłowa/docelowa adresy IP — wykresy słupkowe przedstawiający hello 10 pierwszych źródłowe i docelowe adresy IP.</span><span class="sxs-lookup"><span data-stu-id="3b785-171">Top 10 Source/Destination IPs – bar charts showing hello top 10 source and destination IPs.</span></span> <span data-ttu-id="3b785-172">Można dostosować te tooshow wykresy więcej lub mniej top adresów IP.</span><span class="sxs-lookup"><span data-stu-id="3b785-172">You can adjust these charts tooshow more or less top IPs.</span></span> <span data-ttu-id="3b785-173">W tym miejscu można Zobacz hello najczęściej występujących adresów IP oraz jak hello decyzji ruchu (zezwalania lub odmowy) wysyłanych do każdego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="3b785-173">From here you can see hello most commonly occurring IPs as well as hello traffic decision (allow or deny) being made towards each IP.</span></span>

  ![figure6][6]

1. <span data-ttu-id="3b785-175">Przepływ krotek — w poniższej tabeli przedstawiono hello informacji zawartych w poszczególne krotki przepływu, a także jej odpowiednie NGS i reguły.</span><span class="sxs-lookup"><span data-stu-id="3b785-175">Flow Tuples – this table shows you hello information contained within each flow tuple, as well as its corresponding NGS and rule.</span></span>

  ![figure7][7]

<span data-ttu-id="3b785-177">Używanie paska zapytania hello u góry hello hello pulpitu nawigacyjnego, można filtrować dół pulpit nawigacyjny hello, zależnie od żadnego parametru przepływów hello, takich jak identyfikator subskrypcji, grupy zasobów, reguły lub innej zmiennej zainteresowań.</span><span class="sxs-lookup"><span data-stu-id="3b785-177">Using hello query bar at hello top of hello dashboard, you can filter down hello dashboard based on any parameter of hello flows, such as subscription ID, resource groups, rule, or any other variable of interest.</span></span> <span data-ttu-id="3b785-178">Aby uzyskać więcej informacji o jego Kibana zapytania i filtrów można znaleźć toohello [oficjalnej dokumentacji](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span><span class="sxs-lookup"><span data-stu-id="3b785-178">For more about Kibana's queries and filters, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span></span>

## <a name="conclusion"></a><span data-ttu-id="3b785-179">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="3b785-179">Conclusion</span></span>

<span data-ttu-id="3b785-180">Łącząc hello sieciowej grupy zabezpieczeń przepływu dzienniki z hello elastycznej stosu, mają uzyskujemy toovisualize zaawansowanego, można dostosować sposób naszych ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="3b785-180">By combining hello Network Security Group flow logs with hello Elastic Stack, we have come up with powerful and customizable way toovisualize our network traffic.</span></span> <span data-ttu-id="3b785-181">Te pulpity nawigacyjne pozwalają tooquickly korzyści i udostępniać informacji na temat ruchu sieciowego, jak również filtru w dół i zbadaj na wszelkich potencjalnych nieprawidłowości.</span><span class="sxs-lookup"><span data-stu-id="3b785-181">These dashboards allow you tooquickly gain and share insights about your network traffic, as well as filter down and investigate on any potential anomalies.</span></span> <span data-ttu-id="3b785-182">Przy użyciu Kibana, można dostosować te pulpity nawigacyjne i tworzyć toomeet wizualizacje określonych potrzeb żadnych zabezpieczeń, inspekcji i zgodności.</span><span class="sxs-lookup"><span data-stu-id="3b785-182">Using Kibana, you can tailor these dashboards and create specific visualizations toomeet any security, audit, and compliance needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b785-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3b785-183">Next steps</span></span>

<span data-ttu-id="3b785-184">Dowiedz się, jak toovisualize Twojego przepływu NSG dzienniki przy użyciu usługi Power BI odwiedzając [wizualizacji NSG przepływa dzienników przy użyciu usługi Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="3b785-184">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
