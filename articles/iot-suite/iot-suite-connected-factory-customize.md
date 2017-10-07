---
title: "Fabryka połączenia aaaCustomize pakiet IoT Azure | Dokumentacja firmy Microsoft"
description: "Opis sposób zachowania hello toocustomize hello połączenia fabryki wstępnie skonfigurowane rozwiązanie."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: c#
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 53f2fef7a76b5d8e6ad023945a7812dc7fabd12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-how-hello-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a><span data-ttu-id="f4e94-103">Dostosuj sposób hello połączenia fabryki rozwiązania wyświetla dane z serwerów OPC UA</span><span class="sxs-lookup"><span data-stu-id="f4e94-103">Customize how hello connected factory solution displays data from your OPC UA servers</span></span>

## <a name="introduction"></a><span data-ttu-id="f4e94-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="f4e94-104">Introduction</span></span>

<span data-ttu-id="f4e94-105">Hello połączonych fabryki rozwiązanie agreguje i wyświetla dane z hello OPC UA serwerów połączonych toohello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f4e94-105">hello connected factory solution aggregates and displays data from hello OPC UA servers connected toohello solution.</span></span> <span data-ttu-id="f4e94-106">Można wybrać i wysyłać polecenia toohello OPC UA serwerów w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="f4e94-106">You can browse and send commands toohello OPC UA servers in your solution.</span></span> <span data-ttu-id="f4e94-107">Aby uzyskać więcej informacji na temat OPC UA Zobacz hello [połączone fabryki — często zadawane pytania](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="f4e94-107">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

<span data-ttu-id="f4e94-108">Przykładami zagregowane dane w rozwiązaniu hello hello ogólną wydajność sprzętu (OEE) i kluczowych wskaźników wydajności (KPI) widoczne na pulpicie nawigacyjnym hello na poziomach stacji, wiersza i hello fabryki.</span><span class="sxs-lookup"><span data-stu-id="f4e94-108">Examples of aggregated data in hello solution include hello Overall Equipment Efficiency (OEE) and Key Performance Indicators (KPIs) that you can view in hello dashboard at hello factory, line, and station levels.</span></span> <span data-ttu-id="f4e94-109">Witaj Poniższy zrzut ekranu przedstawia hello OEE i KPI wartości hello **zestawu** stacji na **wiersza produkcyjnym 1**, w hello **we Wrocławiu** fabryki:</span><span class="sxs-lookup"><span data-stu-id="f4e94-109">hello following screenshot shows hello OEE and KPI values for hello **Assembly** station, on **Production line 1**, in hello **Munich** factory:</span></span>

![Przykładowe wartości OEE i wskaźnika KPI w rozwiązaniu hello][img-oee-kpi]

<span data-ttu-id="f4e94-111">umożliwia rozwiązanie Hello możesz tooview szczegółowych informacji z elementów określonych danych z hello OPC UA serwery, nazywane *stacji*.</span><span class="sxs-lookup"><span data-stu-id="f4e94-111">hello solution enables you tooview detailed information from specific data items from hello OPC UA servers, called *stations*.</span></span> <span data-ttu-id="f4e94-112">Witaj Poniższy zrzut ekranu przedstawia powierzchni hello liczba wyprodukowanych elementów z określonym stacji:</span><span class="sxs-lookup"><span data-stu-id="f4e94-112">hello following screenshot shows plots of hello number of manufactured items from a specific station:</span></span>

![Liczba elementów wyprodukowanych wykresy][img-manufactured-items]

<span data-ttu-id="f4e94-114">Kliknięcie wykresy hello można eksplorować danych hello za pomocą czasu serii Insights (TSI):</span><span class="sxs-lookup"><span data-stu-id="f4e94-114">If you click one of hello graphs, you can explore hello data further using Time Series Insights (TSI):</span></span>

![Eksploruj dane przy użyciu czasu serii Insights][img-tsi]

<span data-ttu-id="f4e94-116">W tym artykule opisano:</span><span class="sxs-lookup"><span data-stu-id="f4e94-116">This article describes:</span></span>

- <span data-ttu-id="f4e94-117">Jak hello danych następuje toohello dostępne różne widoki w rozwiązaniu hello.</span><span class="sxs-lookup"><span data-stu-id="f4e94-117">How hello data is made available toohello various views in hello solution.</span></span>
- <span data-ttu-id="f4e94-118">Jak można dostosować hello sposób hello rozwiązanie przedstawia hello dane.</span><span class="sxs-lookup"><span data-stu-id="f4e94-118">How you can customize hello way hello solution displays hello data.</span></span>

## <a name="data-sources"></a><span data-ttu-id="f4e94-119">Źródła danych</span><span class="sxs-lookup"><span data-stu-id="f4e94-119">Data sources</span></span>

<span data-ttu-id="f4e94-120">Witaj rozwiązania połączonych fabryki wyświetlane dane z hello OPC UA serwerów połączonych toohello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f4e94-120">hello connected factory solution displays data from hello OPC UA servers connected toohello solution.</span></span> <span data-ttu-id="f4e94-121">Witaj domyślna instalacja obejmuje kilka serwerów OPC UA systemem symulacji fabryki.</span><span class="sxs-lookup"><span data-stu-id="f4e94-121">hello default installation includes several OPC UA servers running a factory simulation.</span></span> <span data-ttu-id="f4e94-122">Można dodać serwery OPC UA który [łączenie się za pośrednictwem bramy] [ lnk-connect-cf] tooyour rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f4e94-122">You can add your own OPC UA servers that [connect through a gateway][lnk-connect-cf] tooyour solution.</span></span>

<span data-ttu-id="f4e94-123">Możesz przeglądać elementy danych hello podłączony serwer OPC Agent użytkownika może wysyłać rozwiązania tooyour na pulpicie nawigacyjnym hello:</span><span class="sxs-lookup"><span data-stu-id="f4e94-123">You can browse hello data items that a connected OPC UA server can send tooyour solution in hello dashboard:</span></span>

1. <span data-ttu-id="f4e94-124">Przejdź toohello **wybierz serwer OPC UA** widoku:</span><span class="sxs-lookup"><span data-stu-id="f4e94-124">Navigate toohello **Select an OPC UA server** view:</span></span>

    ![Przejdź toohello wybierz Widok serwera OPC UA][img-select-server]

1. <span data-ttu-id="f4e94-126">Wybierz serwer i kliknij przycisk **Connect**.</span><span class="sxs-lookup"><span data-stu-id="f4e94-126">Select a server and click **Connect**.</span></span> <span data-ttu-id="f4e94-127">Kliknij przycisk **Kontynuuj** gdy pojawi się ostrzeżenie o zabezpieczeniach hello.</span><span class="sxs-lookup"><span data-stu-id="f4e94-127">Click **Proceed** when hello security warning appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f4e94-128">To ostrzeżenie występuje raz dla każdego serwera i tylko ustanawia relację zaufania między hello pulpit nawigacyjny rozwiązania i powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="f4e94-128">This warning only appears once for each server and establishes a trust relationship between hello solution dashboard and hello server.</span></span>

1. <span data-ttu-id="f4e94-129">Możesz teraz elementów danych hello przeglądania hello serwer może wysyłać toohello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f4e94-129">You can now browse hello data items that hello server can send toohello solution.</span></span> <span data-ttu-id="f4e94-130">Elementy, które są wysyłane toohello rozwiązania mają zielony znacznik wyboru:</span><span class="sxs-lookup"><span data-stu-id="f4e94-130">Items that are being sent toohello solution have a green check mark:</span></span>

    ![Opublikowane elementy][img-published]

1. <span data-ttu-id="f4e94-132">Jeśli jesteś *administratora* hello rozwiązania, można wybrać toopublish toomake elementu danych ich w hello połączone fabryki rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f4e94-132">If you are an *Administrator* in hello solution, you can choose toopublish a data item toomake it available in hello connected factory solution.</span></span> <span data-ttu-id="f4e94-133">Jako Administrator możesz zmienić wartość hello elementów danych i wywoływać metod w hello OPC UA serwera.</span><span class="sxs-lookup"><span data-stu-id="f4e94-133">As an Administrator, you can also change hello value of data items and call methods in hello OPC UA server.</span></span>

## <a name="map-hello-data"></a><span data-ttu-id="f4e94-134">Dane mapy hello</span><span class="sxs-lookup"><span data-stu-id="f4e94-134">Map hello data</span></span>

<span data-ttu-id="f4e94-135">Hello połączone fabryki rozwiązania map i hello zagregowanych danych elementy opublikowanych danych z hello toohello serwera OPC UA różne widoki w rozwiązaniu hello.</span><span class="sxs-lookup"><span data-stu-id="f4e94-135">hello connected factory solution maps and aggregates hello published data items from hello OPC UA server toohello various views in hello solution.</span></span> <span data-ttu-id="f4e94-136">Hello rozwiązania połączonych fabryki wdraża tooyour konta Azure podczas obsługi administracyjnej hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f4e94-136">hello connected factory solution deploys tooyour Azure account when you provision hello solution.</span></span> <span data-ttu-id="f4e94-137">Plik JSON w hello Visual Studio połączone fabryki rozwiązania przechowuje informacje o mapowaniu.</span><span class="sxs-lookup"><span data-stu-id="f4e94-137">A JSON file in hello Visual Studio connected factory solution stores this mapping information.</span></span> <span data-ttu-id="f4e94-138">Można wyświetlać i modyfikować tego pliku konfiguracji JSON w fabryce połączonych hello rozwiązania Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f4e94-138">You can view and modify this JSON configuration file in hello connected factory Visual Studio solution.</span></span> <span data-ttu-id="f4e94-139">Po wprowadzeniu zmiany można wdrożyć ponownie hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f4e94-139">You can redeploy hello solution after you make a change.</span></span>

<span data-ttu-id="f4e94-140">Program hello pliku konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="f4e94-140">You can use hello configuration file to:</span></span>

- <span data-ttu-id="f4e94-141">Edytowanie istniejącego fabryki symulowane hello, linii produkcyjnych i stacji.</span><span class="sxs-lookup"><span data-stu-id="f4e94-141">Edit hello existing simulated factories, production lines, and stations.</span></span>
- <span data-ttu-id="f4e94-142">Mapowanie danych z rzeczywistego serwerów OPC UA połączyć z toohello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f4e94-142">Map data from real OPC UA servers that you connect toohello solution.</span></span>

<span data-ttu-id="f4e94-143">tooclone kopię hello połączone fabryki rozwiązania Visual Studio, hello Użyj następujących poleceń git:</span><span class="sxs-lookup"><span data-stu-id="f4e94-143">tooclone a copy of hello connected factory Visual Studio solution, use hello following git command:</span></span>

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

<span data-ttu-id="f4e94-144">Plik Hello **ContosoTopologyDescription.json** definiuje hello elementów toohello widoki na pulpicie nawigacyjnym rozwiązania połączonych fabryki hello mapowania z hello OPC UA danych serwera.</span><span class="sxs-lookup"><span data-stu-id="f4e94-144">hello file **ContosoTopologyDescription.json** defines hello mapping from hello OPC UA server data items toohello views in hello connected factory solution dashboard.</span></span> <span data-ttu-id="f4e94-145">Ten plik konfiguracji można znaleźć w hello **Contoso\Topology** folderu w hello **aplikacji sieci Web** projektu w hello rozwiązania Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f4e94-145">You can find this configuration file in hello **Contoso\Topology** folder in hello **WebApp** project in hello Visual Studio solution.</span></span>

<span data-ttu-id="f4e94-146">Hello zawartość pliku JSON hello jest zorganizowana jako hierarchię fabryki, wiersza produkcyjnym i węzły stacji.</span><span class="sxs-lookup"><span data-stu-id="f4e94-146">hello content of hello JSON file is organized as a hierarchy of factory, production line, and station nodes.</span></span> <span data-ttu-id="f4e94-147">Ta hierarchia definiuje hierarchii nawigacji hello hello fabryki połączonych w pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="f4e94-147">This hierarchy defines hello navigation hierarchy in hello connected factory dashboard.</span></span> <span data-ttu-id="f4e94-148">Wartości w każdym węźle hierarchii hello określają hello informacje wyświetlane na pulpicie nawigacyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="f4e94-148">Values at each node of hello hierarchy determine hello information displayed in hello dashboard.</span></span> <span data-ttu-id="f4e94-149">Na przykład plik JSON hello zawiera hello następujące wartości hello fabryki we Wrocławiu:</span><span class="sxs-lookup"><span data-stu-id="f4e94-149">For example, hello JSON file contains hello following values for hello Munich factory:</span></span>

```json
"Guid": "73B534AE-7C7E-4877-B826-F1C0EA339F65",
"Name": "Munich",
"Description": "Braking system",
"Location": {
    "City": "Munich",
    "Country": "Germany",
    "Latitude": 48.13641,
    "Longitude": 11.57754
},
"Image": "munich.jpg"
```

<span data-ttu-id="f4e94-150">Hello nazwę, opis oraz lokalizację są wyświetlane w tym widoku na pulpicie nawigacyjnym hello:</span><span class="sxs-lookup"><span data-stu-id="f4e94-150">hello name, description, and location appear on this view in hello dashboard:</span></span>

![Dane we Wrocławiu na pulpicie nawigacyjnym hello][img-munich]

<span data-ttu-id="f4e94-152">Każdej fabryki wiersza produkcyjnym i stacji mają właściwość obrazu.</span><span class="sxs-lookup"><span data-stu-id="f4e94-152">Each factory, production line, and station have an image property.</span></span> <span data-ttu-id="f4e94-153">Te pliki JPEG można znaleźć w hello **Content\img** folderu w hello **aplikacji sieci Web** projektu.</span><span class="sxs-lookup"><span data-stu-id="f4e94-153">You can find these JPEG files in hello **Content\img** folder in hello **WebApp** project.</span></span> <span data-ttu-id="f4e94-154">Te pliki obrazów wyświetlane na pulpicie nawigacyjnym połączonych fabryki hello.</span><span class="sxs-lookup"><span data-stu-id="f4e94-154">These image files display in hello connected factory dashboard.</span></span>

<span data-ttu-id="f4e94-155">Każda stacja obejmuje kilka szczegółowe właściwości, które definiują hello mapowanie z hello OPC UA elementów danych.</span><span class="sxs-lookup"><span data-stu-id="f4e94-155">Each station includes several detailed properties that define hello mapping from hello OPC UA data items.</span></span> <span data-ttu-id="f4e94-156">Te właściwości są opisane w hello następujące sekcje:</span><span class="sxs-lookup"><span data-stu-id="f4e94-156">These properties are described in hello following sections:</span></span>

### <a name="opcuri"></a><span data-ttu-id="f4e94-157">OpcUri</span><span class="sxs-lookup"><span data-stu-id="f4e94-157">OpcUri</span></span>

<span data-ttu-id="f4e94-158">Witaj **OpcUri** wartość jest hello OPC UA aplikacji URI, który unikatowo identyfikuje hello OPC UA serwera.</span><span class="sxs-lookup"><span data-stu-id="f4e94-158">hello **OpcUri** value is hello OPC UA Application URI that uniquely identifies hello OPC UA server.</span></span> <span data-ttu-id="f4e94-159">Na przykład Witaj **OpcUri** wartość dla stacji zestawu hello wiersza produkcyjnym 1 w we Wrocławiu wygląda hello: **urn: scada2194:ua:munich:productionline0:assemblystation**.</span><span class="sxs-lookup"><span data-stu-id="f4e94-159">For example, hello **OpcUri** value for hello assembly station on production line 1 in Munich looks like hello following: **urn:scada2194:ua:munich:productionline0:assemblystation**.</span></span>

<span data-ttu-id="f4e94-160">Hello identyfikatorów URI hello połączone OPC UA serwerów można wyświetlić na pulpicie nawigacyjnym rozwiązania hello:</span><span class="sxs-lookup"><span data-stu-id="f4e94-160">You can view hello URIs of hello connected OPC UA servers in hello solution dashboard:</span></span>

![Wyświetl OPC UA serwer identyfikatorów URI][img-server-uris]

### <a name="simulation"></a><span data-ttu-id="f4e94-162">Symulacja</span><span class="sxs-lookup"><span data-stu-id="f4e94-162">Simulation</span></span>

<span data-ttu-id="f4e94-163">informacje zawarte w hello Hello **symulacji** węzeł jest określonych toohello symulacji OPC UA, uruchomionego na powitania OPC UA serwerów, które są udostępniane domyślnie.</span><span class="sxs-lookup"><span data-stu-id="f4e94-163">hello information in hello **Simulation** node is specific toohello OPC UA simulation that runs in hello OPC UA servers that are provisioned by default.</span></span> <span data-ttu-id="f4e94-164">Nie służy do rzeczywistego serwera OPC UA.</span><span class="sxs-lookup"><span data-stu-id="f4e94-164">It is not used for a real OPC UA server.</span></span>

### <a name="kpi1-and-kpi2"></a><span data-ttu-id="f4e94-165">Kpi1 i Kpi2</span><span class="sxs-lookup"><span data-stu-id="f4e94-165">Kpi1 and Kpi2</span></span>

<span data-ttu-id="f4e94-166">Te węzły opisano, jak dane ze stacji hello wspiera toohello dwóch wartości wskaźnika KPI w hello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="f4e94-166">These nodes describe how data from hello station contributes toohello two KPI values in hello dashboard.</span></span> <span data-ttu-id="f4e94-167">We wdrożeniu domyślne wartości tych wskaźników KPI są jednostki na godzinę i kWh na godzinę.</span><span class="sxs-lookup"><span data-stu-id="f4e94-167">In a default deployment, these KPI values are units per hour and kWh per hour.</span></span> <span data-ttu-id="f4e94-168">rozwiązanie Hello oblicza vales wskaźnik KPI na poziomie hello stacji i agregowanie ich na poziomie wiersza produkcyjnym hello i fabryki.</span><span class="sxs-lookup"><span data-stu-id="f4e94-168">hello solution calculates KPI vales at hello level of a station and aggregates them at hello production line and factory levels.</span></span>

<span data-ttu-id="f4e94-169">Każdy wskaźnik KPI ma minimum, maksimum i wartości docelowej.</span><span class="sxs-lookup"><span data-stu-id="f4e94-169">Each KPI has a minimum, maximum, and target value.</span></span> <span data-ttu-id="f4e94-170">Każda wartość wskaźnika KPI można również zdefiniować akcje alertu dla tooperform rozwiązania fabryki hello połączony.</span><span class="sxs-lookup"><span data-stu-id="f4e94-170">Each KPI value can also define alert actions for hello connected factory solution tooperform.</span></span> <span data-ttu-id="f4e94-171">Hello poniższy fragment kodu przedstawia hello KPI definicje dla stacji zestawu hello wiersza produkcyjnym 1 w we Wrocławiu:</span><span class="sxs-lookup"><span data-stu-id="f4e94-171">hello following snippet shows hello KPI definitions for hello assembly station on production line 1 in Munich:</span></span>

```json
"Kpi1": {
  "Minimum": 150,
  "Target": 300,
  "Maximum": 600
},
"Kpi2": {
  "Minimum": 50,
  "Target": 100,
  "Maximum": 200,
  "MinimumAlertActions": [
    {
      "Type": "None"
    }
  ]
}
```

<span data-ttu-id="f4e94-172">Witaj Poniższy zrzut ekranu przedstawia hello KPI dane na pulpicie nawigacyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="f4e94-172">hello following screenshot shows hello KPI data in hello dashboard.</span></span>

![Informacje dotyczące KPI na pulpicie nawigacyjnym hello][lnk-kpi]

### <a name="opcnodes"></a><span data-ttu-id="f4e94-174">OpcNodes</span><span class="sxs-lookup"><span data-stu-id="f4e94-174">OpcNodes</span></span>

<span data-ttu-id="f4e94-175">Hello **OpcNodes** zidentyfikować węzłów hello elementy opublikowanych danych z hello OPC UA serwera i określ sposób tooprocess tych danych.</span><span class="sxs-lookup"><span data-stu-id="f4e94-175">hello **OpcNodes** nodes identify hello published data items from hello OPC UA server and specify how tooprocess that data.</span></span>

<span data-ttu-id="f4e94-176">Witaj **ID. węzła** wartość identyfikuje hello określonych ID. UA OPC węzła z hello OPC UA serwera.</span><span class="sxs-lookup"><span data-stu-id="f4e94-176">hello **NodeId** value identifies hello specific OPC UA NodeID from hello OPC UA server.</span></span> <span data-ttu-id="f4e94-177">Witaj pierwszego węzła w stacji zestawu hello wiersza produkcyjnym 1 w we Wrocławiu ma wartość **ns = 2; i = 385**.</span><span class="sxs-lookup"><span data-stu-id="f4e94-177">hello first node in hello assembly station for production line 1 in Munich has a value **ns=2;i=385**.</span></span> <span data-ttu-id="f4e94-178">A **ID. węzła** wartość określa hello danych elementu tooread z hello OPC UA serwera i hello **SymbolicName** zapewnia toouse przyjazną dla użytkownika nazwę, na pulpicie nawigacyjnym hello tych danych.</span><span class="sxs-lookup"><span data-stu-id="f4e94-178">A **NodeId** value specifies hello data item tooread from hello OPC UA server, and hello **SymbolicName** provides a user-friendly name toouse in hello dashboard for that data.</span></span>

<span data-ttu-id="f4e94-179">Witaj w poniższej tabeli przedstawiono inne wartości skojarzone z każdym węźle:</span><span class="sxs-lookup"><span data-stu-id="f4e94-179">Other values associated with each node are summarized in hello following table:</span></span>

| <span data-ttu-id="f4e94-180">Wartość</span><span class="sxs-lookup"><span data-stu-id="f4e94-180">Value</span></span> | <span data-ttu-id="f4e94-181">Opis</span><span class="sxs-lookup"><span data-stu-id="f4e94-181">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="f4e94-182">Trafność</span><span class="sxs-lookup"><span data-stu-id="f4e94-182">Relevance</span></span>  | <span data-ttu-id="f4e94-183">wartości wskaźnika KPI i OEE Hello wspiera tych danych.</span><span class="sxs-lookup"><span data-stu-id="f4e94-183">hello KPI and OEE values this data contributes to.</span></span> |
| <span data-ttu-id="f4e94-184">Kod operacji</span><span class="sxs-lookup"><span data-stu-id="f4e94-184">OpCode</span></span>     | <span data-ttu-id="f4e94-185">Jak hello są agregowane.</span><span class="sxs-lookup"><span data-stu-id="f4e94-185">How hello data is aggregated.</span></span> |
| <span data-ttu-id="f4e94-186">Jednostki</span><span class="sxs-lookup"><span data-stu-id="f4e94-186">Units</span></span>      | <span data-ttu-id="f4e94-187">Witaj toouse jednostki hello w pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="f4e94-187">hello units toouse in hello dashboard.</span></span>  |
| <span data-ttu-id="f4e94-188">Widoczne</span><span class="sxs-lookup"><span data-stu-id="f4e94-188">Visible</span></span>    | <span data-ttu-id="f4e94-189">Czy toodisplay, ta wartość w hello pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="f4e94-189">Whether toodisplay this value in hello dashboard.</span></span> <span data-ttu-id="f4e94-190">Niektóre wartości są używane w obliczeniach, ale nie wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="f4e94-190">Some values are used in calculations but not displayed.</span></span>  |
| <span data-ttu-id="f4e94-191">Maksymalna</span><span class="sxs-lookup"><span data-stu-id="f4e94-191">Maximum</span></span>    | <span data-ttu-id="f4e94-192">Witaj maksymalna wartość wyzwalania alertu na pulpicie nawigacyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="f4e94-192">hello maximum value that triggers an alert in hello dashboard.</span></span> |
| <span data-ttu-id="f4e94-193">MaximumAlertActions</span><span class="sxs-lookup"><span data-stu-id="f4e94-193">MaximumAlertActions</span></span> | <span data-ttu-id="f4e94-194">Tootake akcji w odpowiedzi tooan alertu.</span><span class="sxs-lookup"><span data-stu-id="f4e94-194">An action tootake in response tooan alert.</span></span> <span data-ttu-id="f4e94-195">Na przykład wysyłać polecenia tooa stacji.</span><span class="sxs-lookup"><span data-stu-id="f4e94-195">For example, send a command tooa station.</span></span> |
| <span data-ttu-id="f4e94-196">ConstValue</span><span class="sxs-lookup"><span data-stu-id="f4e94-196">ConstValue</span></span> | <span data-ttu-id="f4e94-197">Stała wartość używana w obliczeniach.</span><span class="sxs-lookup"><span data-stu-id="f4e94-197">A constant value used in a calculation.</span></span> |

## <a name="deploy-hello-changes"></a><span data-ttu-id="f4e94-198">Wdrażanie hello zmiany</span><span class="sxs-lookup"><span data-stu-id="f4e94-198">Deploy hello changes</span></span>

<span data-ttu-id="f4e94-199">Po zakończeniu wprowadzania zmian toohello **ContosoTopologyDescription.json** pliku, należy ponownie wdrożyć hello połączone fabryki rozwiązania tooyour konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f4e94-199">When you have finished making changes toohello **ContosoTopologyDescription.json** file, you must redeploy hello connected factory solution tooyour Azure account.</span></span>

<span data-ttu-id="f4e94-200">Witaj **azure iot — połączony fabryka** repozytorium zawiera **build.ps1** skrypt programu PowerShell, można użyć toorebuild i wdrożyć rozwiązanie hello.</span><span class="sxs-lookup"><span data-stu-id="f4e94-200">hello **azure-iot-connected-factory** repository includes a **build.ps1** PowerShell script you can use toorebuild and deploy hello solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4e94-201">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f4e94-201">Next Steps</span></span>

<span data-ttu-id="f4e94-202">Dowiedz się więcej o hello połączone fabryki wstępnie skonfigurowane rozwiązanie przez hello czytania następujących artykułów:</span><span class="sxs-lookup"><span data-stu-id="f4e94-202">Learn more about hello connected factory preconfigured solution by reading hello following articles:</span></span>

* <span data-ttu-id="f4e94-203">[Przewodnik po wstępnie skonfigurowanym rozwiązaniu połączonej fabryki][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="f4e94-203">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="f4e94-204">[Wdrażanie bramy dla połączonych fabryki][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="f4e94-204">[Deploy a gateway for connected factory][lnk-connect-cf]</span></span>
* <span data-ttu-id="f4e94-205">[Uprawnienia w witrynie azureiotsuite.com hello][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="f4e94-205">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="f4e94-206">Często zadawane pytania dotyczące połączonej fabryki</span><span class="sxs-lookup"><span data-stu-id="f4e94-206">Connected factory FAQ</span></span>](iot-suite-faq-cf.md)
* <span data-ttu-id="f4e94-207">[FAQ][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="f4e94-207">[FAQ][lnk-faq]</span></span>


[img-oee-kpi]: ./media/iot-suite-connected-factory-customize/oeenadkpi.png
[img-manufactured-items]: ./media/iot-suite-connected-factory-customize/manufactured.png
[img-tsi]: ./media/iot-suite-connected-factory-customize/tsi.png
[img-select-server]: ./media/iot-suite-connected-factory-customize/selectserver.png
[img-published]: ./media/iot-suite-connected-factory-customize/published.png
[img-munich]: ./media/iot-suite-connected-factory-customize/munich.png
[img-server-uris]: ./media/iot-suite-connected-factory-customize/serveruris.png
[lnk-kpi]: ./media/iot-suite-connected-factory-customize/kpidisplay.png

[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md