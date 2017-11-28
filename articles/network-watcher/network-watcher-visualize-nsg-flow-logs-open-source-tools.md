---
title: "Wizualizuj dzienników przepływu NSG obserwatora sieci Azure przy użyciu narzędzi typu open source | Dokumentacja firmy Microsoft"
description: "Ta strona informacje dotyczące używania narzędzi typu open source do wizualizacji dzienniki przepływu NSG."
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
ms.openlocfilehash: 20f60ccd9108a7473705c2368f28d3152d0dd614
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a><span data-ttu-id="aa2df-103">Wizualizuj dzienników przepływu NSG obserwatora sieci Azure przy użyciu narzędzi typu open source</span><span class="sxs-lookup"><span data-stu-id="aa2df-103">Visualize Azure Network Watcher NSG flow logs using open source tools</span></span>

<span data-ttu-id="aa2df-104">Dzienniki przepływu sieciowej grupy zabezpieczeń zapewniają informacje, które mogą być używane zrozumieć przychodzące i wychodzące ruchu IP na grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="aa2df-104">Network Security Group flow logs provide information that can be used understand ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="aa2df-105">Te dzienniki przepływu Pokaż przepływów wychodzącego i przychodzącego na podstawie reguły na, przepływ ma zastosowanie do karty Sieciowej, 5 informacji spójnej kolekcji o przepływie (źródłowego i docelowego adresu IP, portu źródłowego i docelowego protokołu), oraz czy ruch został dozwolony lub niedozwolony.</span><span class="sxs-lookup"><span data-stu-id="aa2df-105">These flow logs show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5 tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="aa2df-106">Te dzienniki przepływu może być trudne ręcznie przeanalizować i uzyskaj informacje z.</span><span class="sxs-lookup"><span data-stu-id="aa2df-106">These flow logs can be difficult to manually parse and gain insights from.</span></span> <span data-ttu-id="aa2df-107">Istnieje jednak kilka narzędzi typu open source, które ułatwiają wizualizowanie tych danych.</span><span class="sxs-lookup"><span data-stu-id="aa2df-107">However, there are several open source tools that can help visualize this data.</span></span> <span data-ttu-id="aa2df-108">W tym artykule umożliwi rozwiązanie w celu wizualizacji tych dzienników przy użyciu elastycznej stosu, co umożliwi szybkie indeksu i wizualizacji z przepływu dzienniki na pulpicie nawigacyjnym Kibana.</span><span class="sxs-lookup"><span data-stu-id="aa2df-108">This article will provide a solution to visualize these logs using the Elastic Stack, which will allow you to quickly index and visualize your flow logs on a Kibana dashboard.</span></span>

## <a name="scenario"></a><span data-ttu-id="aa2df-109">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="aa2df-109">Scenario</span></span>

<span data-ttu-id="aa2df-110">W tym artykule skonfigurujemy rozwiązania, które umożliwia wizualizowanie sieciowej grupy zabezpieczeń przepływu dzienników przy użyciu elastycznej stosu.</span><span class="sxs-lookup"><span data-stu-id="aa2df-110">In this article, we will set up a solution that will allow you to visualize Network Security Group flow logs using the Elastic Stack.</span></span>  <span data-ttu-id="aa2df-111">Dodatek wejściowych Logstash uzyska dzienniki przepływu bezpośrednio z obiektu blob magazynu skonfigurowane do przechowywania dzienników przepływu.</span><span class="sxs-lookup"><span data-stu-id="aa2df-111">A Logstash input plugin will obtain the flow logs directly from the storage blob configured for containing the flow logs.</span></span> <span data-ttu-id="aa2df-112">Następnie przy użyciu elastycznej stosu, przepływ dzienniki będą indeksowane i pozwala utworzyć pulpit nawigacyjny Kibana do wizualizacji danych.</span><span class="sxs-lookup"><span data-stu-id="aa2df-112">Then, using the Elastic Stack, the flow logs will be indexed and used to create a Kibana dashboard to visualize the information.</span></span>

![scenariusz][scenario]

## <a name="steps"></a><span data-ttu-id="aa2df-114">Kroki</span><span class="sxs-lookup"><span data-stu-id="aa2df-114">Steps</span></span>

### <a name="enable-network-security-group-flow-logging"></a><span data-ttu-id="aa2df-115">Rejestrowanie przepływu włączyć grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="aa2df-115">Enable Network Security Group flow logging</span></span>
<span data-ttu-id="aa2df-116">W tym scenariuszu muszą mieć sieci grupy przepływu rejestrowanie zabezpieczeń włączone na co najmniej jedną grupę zabezpieczeń sieci w ramach Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="aa2df-116">For this scenario, you must have Network Security Group Flow Logging enabled on at least one Network Security Group in your account.</span></span> <span data-ttu-id="aa2df-117">Instrukcje dotyczące włączania dzienniki przepływu zabezpieczeń sieciowych, można znaleźć w artykule [wprowadzenie do przepływu rejestrowania dla grup zabezpieczeń sieci](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aa2df-117">For instructions on enabling Network Security Flow Logs, refer to the following article [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>


### <a name="set-up-the-elastic-stack"></a><span data-ttu-id="aa2df-118">Konfigurowanie elastycznej stosu</span><span class="sxs-lookup"><span data-stu-id="aa2df-118">Set up the Elastic Stack</span></span>
<span data-ttu-id="aa2df-119">Łącząc dzienniki przepływu NSG do stosu elastycznych, możemy utworzyć pulpit nawigacyjny Kibana co pozwala wyszukiwania, wykresy, analizowanie i pochodzi z naszych dzienników szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="aa2df-119">By connecting NSG flow logs with the Elastic Stack, we can create a Kibana dashboard what allows us to search, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="aa2df-120">Zainstaluj Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="aa2df-120">Install Elasticsearch</span></span>

1. <span data-ttu-id="aa2df-121">Elastyczne stosu w wersji 5.0 i nowszych wymaga Java 8.</span><span class="sxs-lookup"><span data-stu-id="aa2df-121">The Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="aa2df-122">Uruchom polecenie `java -version` do sprawdź wersję.</span><span class="sxs-lookup"><span data-stu-id="aa2df-122">Run the command `java -version` to check your version.</span></span> <span data-ttu-id="aa2df-123">Jeśli nie masz java instalacji, zapoznaj się z dokumentacją na [witryny sieci Web programu Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="aa2df-123">If you do not have java install, refer to documentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="aa2df-124">Pobierz poprawny pakiet binarnych systemu:</span><span class="sxs-lookup"><span data-stu-id="aa2df-124">Download the correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="aa2df-125">Inne metody instalacji można znaleźć w folderze [Elasticsearch instalacji](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span><span class="sxs-lookup"><span data-stu-id="aa2df-125">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="aa2df-126">Sprawdź, czy Elasticsearch działa przy użyciu polecenia:</span><span class="sxs-lookup"><span data-stu-id="aa2df-126">Verify that Elasticsearch is running with the command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="aa2df-127">Powinna zostać wyświetlona odpowiedź podobną do poniższego:</span><span class="sxs-lookup"><span data-stu-id="aa2df-127">You should see a response similar to this:</span></span>

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

<span data-ttu-id="aa2df-128">Dodatkowe instrukcje dotyczące instalowania elastycznej wyszukiwania, można znaleźć na stronie [instalacji](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span><span class="sxs-lookup"><span data-stu-id="aa2df-128">For further instructions on installing Elastic search, refer to the page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="aa2df-129">Zainstaluj Logstash</span><span class="sxs-lookup"><span data-stu-id="aa2df-129">Install Logstash</span></span>

1. <span data-ttu-id="aa2df-130">Aby zainstalować Logstash, uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="aa2df-130">To install Logstash run the following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="aa2df-131">Obok należy skonfigurować Logstash dostępu i analizować dzienniki przepływu.</span><span class="sxs-lookup"><span data-stu-id="aa2df-131">Next we need to configure Logstash to access and parse the flow logs.</span></span> <span data-ttu-id="aa2df-132">Tworzenie pliku logstash.conf przy użyciu:</span><span class="sxs-lookup"><span data-stu-id="aa2df-132">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="aa2df-133">Dodaj następującą zawartość do pliku:</span><span class="sxs-lookup"><span data-stu-id="aa2df-133">Add the following content to the file:</span></span>

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

<span data-ttu-id="aa2df-134">Aby uzyskać dalsze instrukcje na temat instalowania Logstash odwoływać się do [oficjalnej dokumentacji](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="aa2df-134">For further instructions on installing Logstash, refer to the [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-the-logstash-input-plugin-for-azure-blob-storage"></a><span data-ttu-id="aa2df-135">Instalowanie wtyczki wejściowych Logstash magazynu obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="aa2df-135">Install the Logstash input plugin for Azure blob storage</span></span>

<span data-ttu-id="aa2df-136">Ten dodatek plug-in Logstash pozwoli uzyskać bezpośredniego dostępu do dzienników przepływu ze swojego konta magazynu wyznaczonego.</span><span class="sxs-lookup"><span data-stu-id="aa2df-136">This Logstash plugin will allow you to directly access the flow logs from their designated storage account.</span></span> <span data-ttu-id="aa2df-137">Aby zainstalować ten dodatek plug-in, z poziomu katalogu instalacyjnego Logstash domyślnej (w tym /usr/share/logstash/bin przypadków), uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="aa2df-137">To install this plugin, from the default Logstash installation directory (in this case /usr/share/logstash/bin) run the command:</span></span>

```
logstash-plugin install logstash-input-azureblob
```

<span data-ttu-id="aa2df-138">Aby uruchomić Logstash, uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="aa2df-138">To start Logstash run the command:</span></span>

```
sudo /etc/init.d/logstash start
```

<span data-ttu-id="aa2df-139">Aby uzyskać więcej informacji na temat tej wtyczki, zajrzyj do dokumentacji [tutaj](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span><span class="sxs-lookup"><span data-stu-id="aa2df-139">For more information about this plugin, refer to documentation [here](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="aa2df-140">Zainstaluj Kibana</span><span class="sxs-lookup"><span data-stu-id="aa2df-140">Install Kibana</span></span>

1. <span data-ttu-id="aa2df-141">Uruchom następujące polecenia, aby zainstalować Kibana:</span><span class="sxs-lookup"><span data-stu-id="aa2df-141">Run the following commands to install Kibana:</span></span>

  ```
  curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
  tar xzvf kibana-5.2.0-linux-x86_64.tar.gz
  ```

1. <span data-ttu-id="aa2df-142">Aby uruchomić Kibana należy użyć polecenia:</span><span class="sxs-lookup"><span data-stu-id="aa2df-142">To run Kibana use the commands:</span></span>

  ```
  cd kibana-5.2.0-linux-x86_64/
  ./bin/kibana
  ```

1. <span data-ttu-id="aa2df-143">Aby wyświetlić Kibana interfejsu sieci web, przejdź do`http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="aa2df-143">To view your Kibana web interface, navigate to `http://localhost:5601`</span></span>
1. <span data-ttu-id="aa2df-144">W tym scenariuszu wzorzec indeksu, używany dla dzienników przepływu jest "nsg przepływu dzienniki".</span><span class="sxs-lookup"><span data-stu-id="aa2df-144">For this scenario, the index pattern used for the flow logs is "nsg-flow-logs".</span></span> <span data-ttu-id="aa2df-145">Wzór indeksu w sekcji "wyjściowej" w pliku logstash.conf mogą ulec zmianie.</span><span class="sxs-lookup"><span data-stu-id="aa2df-145">You may change the index pattern in the "output" section of your logstash.conf file.</span></span>

1. <span data-ttu-id="aa2df-146">Jeśli chcesz wyświetlić pulpit nawigacyjny Kibana zdalnie, Utwórz regułę ruchu przychodzącego grupy NSG zezwalania na dostęp do **portu 5601**.</span><span class="sxs-lookup"><span data-stu-id="aa2df-146">If you want to view the Kibana dashboard remotely, create an inbound NSG rule allowing access to **port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="aa2df-147">Utwórz pulpit nawigacyjny Kibana</span><span class="sxs-lookup"><span data-stu-id="aa2df-147">Create a Kibana dashboard</span></span>

<span data-ttu-id="aa2df-148">W tym artykule firma Microsoft umieściła przykładowy pulpit nawigacyjny do wyświetlania trendów i informacji w alerty.</span><span class="sxs-lookup"><span data-stu-id="aa2df-148">For this article, we have provided a sample dashboard for you to view trends and details in your alerts.</span></span>

![rysunek 1][1]

1. <span data-ttu-id="aa2df-150">Pobierz plik pulpitu nawigacyjnego [tutaj](https://aka.ms/networkwatchernsgflowlogdashboard), plik wizualizacji [tutaj](https://aka.ms/networkwatchernsgflowlogvisualizations), a plikiem zapisanego wyszukiwania [tutaj](https://aka.ms/networkwatchernsgflowlogsearch).</span><span class="sxs-lookup"><span data-stu-id="aa2df-150">Download the dashboard file [here](https://aka.ms/networkwatchernsgflowlogdashboard), the visualization file [here](https://aka.ms/networkwatchernsgflowlogvisualizations), and the saved search file [here](https://aka.ms/networkwatchernsgflowlogsearch).</span></span>

1. <span data-ttu-id="aa2df-151">W obszarze **zarządzania** kartę z Kibana, przejdź do **zapisane obiektów** i zaimportować wszystkie trzy pliki.</span><span class="sxs-lookup"><span data-stu-id="aa2df-151">Under the **Management** tab of Kibana, navigate to **Saved Objects** and import all three files.</span></span> <span data-ttu-id="aa2df-152">Następnie z **pulpitu nawigacyjnego** kartę można otwierać i załadować przykładowy pulpit nawigacyjny.</span><span class="sxs-lookup"><span data-stu-id="aa2df-152">Then from the **Dashboard** tab you can open and load the sample dashboard.</span></span>

<span data-ttu-id="aa2df-153">Można również utworzyć własne wizualizacje i pulpity nawigacyjne dostosowane do metryki użytkownika.</span><span class="sxs-lookup"><span data-stu-id="aa2df-153">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="aa2df-154">Przeczytaj więcej na temat tworzenia wizualizacje Kibana z jego Kibana [oficjalnej dokumentacji](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span><span class="sxs-lookup"><span data-stu-id="aa2df-154">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

### <a name="visualize-nsg-flow-logs"></a><span data-ttu-id="aa2df-155">Wizualizuj dzienniki przepływu NSG</span><span class="sxs-lookup"><span data-stu-id="aa2df-155">Visualize NSG flow logs</span></span>

<span data-ttu-id="aa2df-156">Przykładowy pulpit nawigacyjny udostępnia kilka wizualizacje dzienników przepływu:</span><span class="sxs-lookup"><span data-stu-id="aa2df-156">The sample dashboard provides several visualizations of the flow logs:</span></span>

1. <span data-ttu-id="aa2df-157">Przechodzi przez kierunku/decyzji w miarę upływu czasu — czas serii wykresów wyświetlana jest liczba przepływów w przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="aa2df-157">Flows by Decision/Direction Over Time - time series graphs showing the number of flows over the time period.</span></span> <span data-ttu-id="aa2df-158">Jednostka czasu i zakres obu tych wizualizacje można edytować.</span><span class="sxs-lookup"><span data-stu-id="aa2df-158">You can edit the unit of time and span of both these visualizations.</span></span> <span data-ttu-id="aa2df-159">Przepływy decyzją zawiera część akceptować lub odrzucać decyzje, podczas gdy przepływów przez kierunek część ruchu przychodzącego i wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="aa2df-159">Flows by Decision shows the proportion of allow or deny decisions made, while Flows by Direction shows the proportion of inbound and outbound traffic.</span></span> <span data-ttu-id="aa2df-160">Z tych elementów wizualnych można zbadać ruchu trendów w czasie i poszukaj nagłego ani nietypowe wzorce.</span><span class="sxs-lookup"><span data-stu-id="aa2df-160">With these visuals you can examine traffic trends over time and look for any spikes or unusual patterns.</span></span>

  ![Rysunek 2][2]

1. <span data-ttu-id="aa2df-162">Przechodzi przez Port docelowy/źródłowy — wykresy kołowe przedstawiający podział przepływów do odpowiednich portów.</span><span class="sxs-lookup"><span data-stu-id="aa2df-162">Flows by Destination/Source Port – pie charts showing the breakdown of flows to their respective ports.</span></span> <span data-ttu-id="aa2df-163">Z tym widokiem widać z najczęściej używane porty.</span><span class="sxs-lookup"><span data-stu-id="aa2df-163">With this view you can see your most commonly used ports.</span></span> <span data-ttu-id="aa2df-164">Jeśli klikniesz przycisk na określonym porcie w obrębie wykresu kołowego, pozostałej części pulpitu nawigacyjnego zostanie odfiltrowana do przepływów tego portu.</span><span class="sxs-lookup"><span data-stu-id="aa2df-164">If you click on a specific port within the pie chart, the rest of the dashboard will filter down to flows of that port.</span></span>

  ![figure3][3]

1. <span data-ttu-id="aa2df-166">Liczba przepływów i najwcześniejszą godzinę dziennika — pokazuje liczbę przepływów rejestrowane i Data najwcześniejszą dziennika przechwycone metryki.</span><span class="sxs-lookup"><span data-stu-id="aa2df-166">Number of Flows and Earliest Log Time – metrics showing you the number of flows recorded and the date of the earliest log captured.</span></span>

  ![figure4][4]

1. <span data-ttu-id="aa2df-168">Przepływy NSG i reguła — wykres słupkowy pokazywania podział przepływów w poszczególnych grupach NSG, a także dystrybucji reguły w poszczególnych grupach NSG.</span><span class="sxs-lookup"><span data-stu-id="aa2df-168">Flows by NSG and Rule – a bar graph showing you the distribution of flows within each NSG, as well as the distribution of rules within each NSG.</span></span> <span data-ttu-id="aa2df-169">W tym miejscu widać, które NSG i reguły generowane najczęściej ruchu.</span><span class="sxs-lookup"><span data-stu-id="aa2df-169">From here you can see which NSG and rules generated the most traffic.</span></span>

  ![figure5][5]

1. <span data-ttu-id="aa2df-171">Pierwszych 10 lokalizacja źródłowa/docelowa adresy IP — wykresy słupkowe przedstawiający 10 pierwszych źródłowe i docelowe adresy IP.</span><span class="sxs-lookup"><span data-stu-id="aa2df-171">Top 10 Source/Destination IPs – bar charts showing the top 10 source and destination IPs.</span></span> <span data-ttu-id="aa2df-172">Można dostosować te wykresy, aby wyświetlić więcej lub mniej top adresów IP.</span><span class="sxs-lookup"><span data-stu-id="aa2df-172">You can adjust these charts to show more or less top IPs.</span></span> <span data-ttu-id="aa2df-173">W tym miejscu zobaczysz, najczęściej występujących adresów IP, a także decyzja ruchu (zezwalania lub odmowy) wysyłanych do każdego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="aa2df-173">From here you can see the most commonly occurring IPs as well as the traffic decision (allow or deny) being made towards each IP.</span></span>

  ![figure6][6]

1. <span data-ttu-id="aa2df-175">Przepływ krotek — ta tabela zawiera informacje zawarte w każdej krotki przepływu, a także odpowiednie NGS i reguły.</span><span class="sxs-lookup"><span data-stu-id="aa2df-175">Flow Tuples – this table shows you the information contained within each flow tuple, as well as its corresponding NGS and rule.</span></span>

  ![figure7][7]

<span data-ttu-id="aa2df-177">Używanie paska zapytania w górnej części pulpitu nawigacyjnego, można filtrować dół pulpit nawigacyjny, zależnie od żadnego parametru przepływów, takich jak identyfikator subskrypcji, grupy zasobów, reguły lub innej zmiennej zainteresowań.</span><span class="sxs-lookup"><span data-stu-id="aa2df-177">Using the query bar at the top of the dashboard, you can filter down the dashboard based on any parameter of the flows, such as subscription ID, resource groups, rule, or any other variable of interest.</span></span> <span data-ttu-id="aa2df-178">Więcej informacji na temat kwerend i filtrów w Kibana, można znaleźć w temacie [oficjalnej dokumentacji](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span><span class="sxs-lookup"><span data-stu-id="aa2df-178">For more about Kibana's queries and filters, refer to the [official documentation](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)</span></span>

## <a name="conclusion"></a><span data-ttu-id="aa2df-179">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="aa2df-179">Conclusion</span></span>

<span data-ttu-id="aa2df-180">Łącząc dzienniki przepływu sieciową grupę zabezpieczeń z elastycznej stosu, mają uzyskujemy zaawansowanego, można dostosować sposób wizualizacji naszych ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="aa2df-180">By combining the Network Security Group flow logs with the Elastic Stack, we have come up with powerful and customizable way to visualize our network traffic.</span></span> <span data-ttu-id="aa2df-181">Te pulpity nawigacyjne pozwala szybko uzyskać i udostępniać informacji na temat ruchu sieciowego, jak również filtru w dół i badanie na wszelkich potencjalnych nieprawidłowości.</span><span class="sxs-lookup"><span data-stu-id="aa2df-181">These dashboards allow you to quickly gain and share insights about your network traffic, as well as filter down and investigate on any potential anomalies.</span></span> <span data-ttu-id="aa2df-182">Przy użyciu Kibana, można dostosować te pulpity nawigacyjne i tworzenie wizualizacji określonych potrzeb żadnych zabezpieczeń, inspekcji i zgodności.</span><span class="sxs-lookup"><span data-stu-id="aa2df-182">Using Kibana, you can tailor these dashboards and create specific visualizations to meet any security, audit, and compliance needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa2df-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="aa2df-183">Next steps</span></span>

<span data-ttu-id="aa2df-184">Dowiedz się, jak wizualizacji NSG dzienników przepływu z usługi Power BI, odwiedzając [wizualizacji NSG przepływa dzienników przy użyciu usługi Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="aa2df-184">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
