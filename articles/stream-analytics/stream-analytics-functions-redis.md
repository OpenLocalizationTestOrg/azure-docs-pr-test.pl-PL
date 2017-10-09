---
title: "Przetwarzanie aaaStream analizy w czasie rzeczywistym dla usługi Azure Functions | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse funkcji platformy Azure połączony z kolejką usługi Service Bus, toopopulate pamięć podręczna Redis Azure z hello dane wyjściowe zadania usługi analiza strumienia."
keywords: "strumień danych, pamięć podręczna redis, kolejką usługi service bus"
services: stream-analytics
author: ryancrawcour
manager: jhubbard
documentationcenter: 
ms.assetid: d428bb33-4244-4001-b93d-c77bed816527
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/28/2017
ms.author: ryancraw
ms.openlocfilehash: 5ef4fe76c2cadf896a80eeaf421f010c315918af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostore-data-from-azure-stream-analytics-in-an-azure-redis-cache-using-azure-functions"></a><span data-ttu-id="bcb1f-104">Jak toostore dane z usługi Azure Stream Analytics w pamięci podręcznej Redis Azure za pomocą usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="bcb1f-104">How toostore data from Azure Stream Analytics in an Azure Redis Cache using Azure Functions</span></span>
<span data-ttu-id="bcb1f-105">Usługa Azure Stream Analytics umożliwia szybkie tworzenie i wdrażanie wgląd w czasie rzeczywistym toogain niskokosztowych rozwiązań z urządzeń, czujników, infrastruktury i aplikacji lub dowolny strumień danych.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-105">Azure Stream Analytics lets you rapidly develop and deploy low-cost solutions toogain real-time insights from devices, sensors, infrastructure, and applications, or any stream of data.</span></span> <span data-ttu-id="bcb1f-106">Umożliwia on różnych przypadków użycia, np. w czasie rzeczywistym zarządzania i monitorowania, polecenia kontroli, wykrywanie oszustw, połączonych samochodów i wiele innych.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-106">It enables various use cases such as real-time management and monitoring, command and control, fraud detection, connected cars and many more.</span></span> <span data-ttu-id="bcb1f-107">W wielu scenariuszach takich można toostore danych wyjściowych z usługi Azure Stream Analytics do magazynu danych rozproszonych, takich jak pamięć podręczna Azure Redis.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-107">In many such scenarios, you may want toostore data outputted by Azure Stream Analytics into a distributed data store such as an Azure Redis cache.</span></span>

<span data-ttu-id="bcb1f-108">Załóżmy, że są częścią telekomunikacyjnych firmy.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-108">Suppose you are part of a telecommunications company.</span></span> <span data-ttu-id="bcb1f-109">Próbujesz toodetect SIM oszustwa, gdzie wiele wywołań pochodzące z hello tej samej tożsamości, na hello sam czasu, ale w różnych geograficznie lokalizacje.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-109">You are trying toodetect SIM fraud where multiple calls coming from hello same identity, at hello same time, but in different geographically locations.</span></span> <span data-ttu-id="bcb1f-110">Możesz są zlecił mu przechowywania wszystkich hello potencjalnych fałszywych rozmów telefonicznych w pamięci podręcznej Azure Redis.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-110">You are tasked with storing all hello potential fraudulent phone calls in an Azure Redis cache.</span></span> <span data-ttu-id="bcb1f-111">W tym wpisie udostępniamy wskazówki na jak łatwo można wykonać zadanie.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-111">In this blog, we provide guidance on how you can easily complete your task.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bcb1f-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bcb1f-112">Prerequisites</span></span>
<span data-ttu-id="bcb1f-113">Zakończenie hello [wykrywanie oszustw w czasie rzeczywistym] [ fraud-detection] przewodnika dla ASA</span><span class="sxs-lookup"><span data-stu-id="bcb1f-113">Complete hello [Real-time Fraud Detection][fraud-detection] walk-through for ASA</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="bcb1f-114">Przegląd architektury</span><span class="sxs-lookup"><span data-stu-id="bcb1f-114">Architecture Overview</span></span>
![Zrzut ekranu przedstawiający architektury](./media/stream-analytics-functions-redis/architecture-overview.png)

<span data-ttu-id="bcb1f-116">Jak pokazano na powyższej ilustracji hello, Stream Analytics umożliwia przesyłanie strumieniowe danych wejściowych toobe zbadać i wysyłane tooan danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-116">As shown in hello preceding figure, Stream Analytics allows streaming input data toobe queried and sent tooan output.</span></span> <span data-ttu-id="bcb1f-117">W oparciu o dane wyjściowe hello, usługi Azure Functions można wyzwolić pewien typ zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-117">Based on hello output, Azure Functions can then trigger some type of event.</span></span> 

<span data-ttu-id="bcb1f-118">W tym wpisie możemy skupić się na powitania usługi Azure Functions częścią tego potoku lub dokładniej hello wyzwolenie zdarzenia, które przechowuje w pamięci podręcznej hello fałszywych danych.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-118">In this blog, we focus on hello Azure Functions part of this pipeline, or more specifically hello triggering of an event that stores fraudulent data into hello cache.</span></span>
<span data-ttu-id="bcb1f-119">Po zakończeniu hello [wykrywanie oszustw w czasie rzeczywistym] [ fraud-detection] samouczek, masz danych wejściowych (Centrum zdarzeń), kwerendy i danych wyjściowych (magazynu obiektów blob) już skonfigurowane i uruchomione.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-119">After completing hello [Real-time Fraud Detection][fraud-detection] tutorial, you have an input (an event hub), a query, and an output (blob storage) already configured and running.</span></span> <span data-ttu-id="bcb1f-120">W tym wpisie zamiast tego zmienić toouse dane wyjściowe hello kolejką usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-120">In this blog, we change hello output toouse a Service Bus Queue instead.</span></span> <span data-ttu-id="bcb1f-121">Po wykonaniu tej połączymy kolejki toothis funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-121">After that, we connect an Azure Function toothis queue.</span></span> 

## <a name="create-and-connect-a-service-bus-queue-output"></a><span data-ttu-id="bcb1f-122">Tworzenie i łączenie wyjściowego kolejką usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="bcb1f-122">Create and connect a Service Bus Queue output</span></span>
<span data-ttu-id="bcb1f-123">toocreate kolejką usługi Service Bus, wykonaj kroki 1 i 2 hello .NET części [Rozpoczynanie pracy z kolejek usługi Service Bus][servicebus-getstarted].</span><span class="sxs-lookup"><span data-stu-id="bcb1f-123">toocreate a Service Bus Queue, follow steps 1 and 2 of hello .NET section in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span>
<span data-ttu-id="bcb1f-124">Teraz załóżmy połączyć zadanie usługi Stream Analytics toohello kolejki hello, który został utworzony w hello wcześniejszych przewodnika wykrywanie oszustw.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-124">Now let's connect hello queue toohello Stream Analytics job that was created in hello earlier fraud detection walk-through.</span></span>

1. <span data-ttu-id="bcb1f-125">W hello portalu Azure, przejdź do pozycji toohello **dane wyjściowe** bloku zadania i wybierz **Dodaj** u góry hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-125">In hello Azure portal, go toohello **Outputs** blade of your job and select **Add** at hello top of hello page.</span></span>
   
    ![Dodawanie danych wyjściowych](./media/stream-analytics-functions-redis/adding-outputs.png)
2. <span data-ttu-id="bcb1f-127">Wybierz **kolejką usługi Service Bus** jako hello **Sink** i wykonaj instrukcje hello na ekranie powitania.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-127">Choose **Service Bus Queue** as hello **Sink** and follow hello instructions on hello screen.</span></span> <span data-ttu-id="bcb1f-128">Czy toochoose hello przestrzeń nazw hello kolejką usługi Service Bus można utworzyć w [Rozpoczynanie pracy z kolejek usługi Service Bus][servicebus-getstarted].</span><span class="sxs-lookup"><span data-stu-id="bcb1f-128">Be sure toochoose hello namespace of hello Service Bus Queue you created in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span> <span data-ttu-id="bcb1f-129">Kliknij przycisk "prawa" hello, po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-129">Click hello "right" button when you are finished.</span></span>
3. <span data-ttu-id="bcb1f-130">Określ hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="bcb1f-130">Specify hello following values:</span></span>
   
   * <span data-ttu-id="bcb1f-131">**Format serializator zdarzeń**: JSON</span><span class="sxs-lookup"><span data-stu-id="bcb1f-131">**Event Serializer Format**: JSON</span></span>
   * <span data-ttu-id="bcb1f-132">**Kodowanie**: UTF8</span><span class="sxs-lookup"><span data-stu-id="bcb1f-132">**Encoding**: UTF8</span></span>
   * <span data-ttu-id="bcb1f-133">**FORMAT**: rozdzielone</span><span class="sxs-lookup"><span data-stu-id="bcb1f-133">**FORMAT**: Line separated</span></span>
4. <span data-ttu-id="bcb1f-134">Kliknij przycisk hello **Utwórz** przycisk tooadd tego źródła i czy Stream Analytics może pomyślnie połączyć z konta magazynu toohello tooverify.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-134">Click hello **Create** button tooadd this source and tooverify that Stream Analytics can successfully connect toohello storage account.</span></span>
5. <span data-ttu-id="bcb1f-135">W hello **zapytania** karcie, Zastąp następujące hello hello bieżącego zapytania.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-135">In hello **Query** tab, replace hello current query with hello following.</span></span> <span data-ttu-id="bcb1f-136">Zastąp * [YOUR SERVICE BUS NAME] * o nazwie dane wyjściowe hello utworzonego w kroku 3.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-136">Replace *[YOUR SERVICE BUS NAME] * with hello output name you created in step 3.</span></span> 
   
    ```    
   
        SELECT 
            System.Timestamp as Time, CS1.CallingIMSI, CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, CS1.SwitchNum as Switch1, CS2.SwitchNum as Switch2
   
        INTO [YOUR SERVICE BUS NAME]
   
        FROM CallStream CS1 TIMESTAMP BY CallRecTime
        JOIN CallStream CS2 TIMESTAMP BY CallRecTime
            ON CS1.CallingIMSI = CS2.CallingIMSI AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5
   
        WHERE CS1.SwitchNum != CS2.SwitchNum
   
    ```

## <a name="create-an-azure-redis-cache"></a><span data-ttu-id="bcb1f-137">Tworzenie usługi Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="bcb1f-137">Create an Azure Redis Cache</span></span>
<span data-ttu-id="bcb1f-138">Utwórz pamięci podręcznej Azure Redis, wykonując hello .NET części [jak tooUse pamięć podręczna Redis Azure] [ use-rediscache] dopóki hello sekcji o nazwie ***Konfigurowanie klientów pamięci podręcznej hello***.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-138">Create an Azure Redis cache by following hello .NET section in [How tooUse Azure Redis Cache][use-rediscache] until hello section called ***Configure hello cache clients***.</span></span>
<span data-ttu-id="bcb1f-139">Po wykonaniu tych czynności należy nowej pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-139">Once complete, you have a new Redis Cache.</span></span> <span data-ttu-id="bcb1f-140">W obszarze **wszystkie ustawienia**, wybierz pozycję **klucze dostępu** i zanotuj hello ***parametry połączenia podstawowej***.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-140">Under **All settings**, select **Access keys** and note down hello ***Primary connection string***.</span></span>

![Zrzut ekranu przedstawiający architektury](./media/stream-analytics-functions-redis/redis-cache-keys.png)

## <a name="create-an-azure-function"></a><span data-ttu-id="bcb1f-142">Tworzenie funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="bcb1f-142">Create an Azure Function</span></span>
<span data-ttu-id="bcb1f-143">Postępuj zgodnie z [tworzenie pierwszej funkcji platformy Azure] [ functions-getstarted] tooget samouczka Wprowadzenie do usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-143">Follow [Create your first Azure Function][functions-getstarted] tutorial tooget started with Azure Functions.</span></span> <span data-ttu-id="bcb1f-144">Jeśli masz już funkcję platformy Azure będzie toouse, takich jak następnie przejść od razu zbyt[zapisywania tooRedis pamięci podręcznej](#Writing-to-Redis-Cache)</span><span class="sxs-lookup"><span data-stu-id="bcb1f-144">If you already have an Azure function you would like toouse, then skip ahead too[Writing tooRedis Cache](#Writing-to-Redis-Cache)</span></span>

1. <span data-ttu-id="bcb1f-145">W portalu hello wybierać usługi aplikacji hello nawigacji po lewej stronie, a następnie kliknij witrynę sieci Web z funkcji Azure app nazwa tooget toohello funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-145">In hello portal, select App Services from hello left-hand navigation, then click your Azure function app name tooget toohello Function's app website.</span></span>
    <span data-ttu-id="bcb1f-146">![Zrzut ekranu przedstawiający listę funkcji usług aplikacji](./media/stream-analytics-functions-redis/app-services-function-list.png)</span><span class="sxs-lookup"><span data-stu-id="bcb1f-146">![Screenshot of app services function list](./media/stream-analytics-functions-redis/app-services-function-list.png)</span></span>
2. <span data-ttu-id="bcb1f-147">Kliknij przycisk **nową funkcję > ServiceBusQueueTrigger — C#**.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-147">Click **New Function > ServiceBusQueueTrigger – C#**.</span></span> <span data-ttu-id="bcb1f-148">Hello następujących pól, wykonaj te instrukcje:</span><span class="sxs-lookup"><span data-stu-id="bcb1f-148">For hello following fields, follow these instructions:</span></span>
   
   * <span data-ttu-id="bcb1f-149">**Nazwa kolejki**: hello takie same nazwy jako nazwy hello wprowadzona podczas tworzenia kolejki hello w [Rozpoczynanie pracy z kolejek usługi Service Bus] [ servicebus-getstarted] (nie nazwę hello hello service Bus).</span><span class="sxs-lookup"><span data-stu-id="bcb1f-149">**Queue name**: hello same name as hello name you entered when you created hello queue in [Get Started with Service Bus Queues][servicebus-getstarted] (not hello name of hello service bus).</span></span> <span data-ttu-id="bcb1f-150">Upewnij się, że używasz hello kolejki, który jest połączony toohello, którego analiza strumienia wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-150">Make sure you use hello queue that is connected toohello Stream Analytics output.</span></span>
   * <span data-ttu-id="bcb1f-151">**Połączenia magistrali usług**: Wybierz **dodać parametry połączenia**.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-151">**Service Bus connection**: Select **Add a connection string**.</span></span> <span data-ttu-id="bcb1f-152">Wybierz parametry połączenia hello toofind, przejdź toohello klasycznego portalu **usługi Service Bus**, hello usługi service bus został utworzony, i **informacje o połączeniu** u dołu hello hello ekranu.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-152">toofind hello connection string, go toohello classic portal, select **Service Bus**, hello service bus you created, and **CONNECTION INFORMATION** at hello bottom of hello screen.</span></span> <span data-ttu-id="bcb1f-153">Upewnij się, że znajdują się na ekranie głównym hello na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-153">Make sure you are on hello main screen on this page.</span></span> <span data-ttu-id="bcb1f-154">Skopiuj i Wklej parametry połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-154">Copy and paste hello connection string.</span></span> <span data-ttu-id="bcb1f-155">Możesz tooenter wolne dowolna nazwa połączenia.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-155">Feel free tooenter any connection name.</span></span>
     
       ![Zrzut ekranu przedstawiający połączenia magistrali usług](./media/stream-analytics-functions-redis/servicebus-connection.png)
   * <span data-ttu-id="bcb1f-157">**AccessRights**: Wybierz **zarządzania**</span><span class="sxs-lookup"><span data-stu-id="bcb1f-157">**AccessRights**: Choose **Manage**</span></span>
3. <span data-ttu-id="bcb1f-158">Kliknij przycisk **Utwórz**</span><span class="sxs-lookup"><span data-stu-id="bcb1f-158">Click **Create**</span></span>

## <a name="writing-tooredis-cache"></a><span data-ttu-id="bcb1f-159">Zapisywanie tooRedis pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="bcb1f-159">Writing tooRedis Cache</span></span>
<span data-ttu-id="bcb1f-160">Teraz utworzono funkcji platformy Azure, która odczytuje z kolejką usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-160">We have now created an Azure Function that reads from a Service Bus Queue.</span></span> <span data-ttu-id="bcb1f-161">Pozostało toodo jest użyć naszych toowrite funkcja tego toohello danych pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-161">All that is left toodo is use our Function toowrite this data toohello Redis Cache.</span></span> 

1. <span data-ttu-id="bcb1f-162">Wybierz nowo utworzony **ServiceBusQueueTrigger**i kliknij przycisk **funkcji ustawienia aplikacji** na powitania prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-162">Select your newly created **ServiceBusQueueTrigger**, and click **Function app settings** on hello top right corner.</span></span> <span data-ttu-id="bcb1f-163">Wybierz **Przejdź ustawień usługi tooApp > Ustawienia > Ustawienia aplikacji**</span><span class="sxs-lookup"><span data-stu-id="bcb1f-163">Select **Go tooApp Service Settings > Settings > Application settings**</span></span>
2. <span data-ttu-id="bcb1f-164">W hello sekcji ciągów połączenia, Utwórz nazwę w hello **nazwa** sekcji.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-164">In hello Connection strings section, create a name in hello **Name** section.</span></span> <span data-ttu-id="bcb1f-165">Wklej parametry połączenia podstawowej hello znaleziony w hello **Tworzenie pamięci podręcznej Redis** Wkrocz do hello **wartość** sekcji.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-165">Paste hello primary connection string you found in hello **Create a Redis Cache** step into hello **Value** section.</span></span> <span data-ttu-id="bcb1f-166">Wybierz **niestandardowy** gdzie mówi **bazy danych SQL**.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-166">Select **Custom** where it says **SQL Database**.</span></span>
3. <span data-ttu-id="bcb1f-167">Kliknij przycisk **zapisać** u góry hello.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-167">Click **Save** at hello top.</span></span>
   
    ![Zrzut ekranu przedstawiający połączenia magistrali usług](./media/stream-analytics-functions-redis/function-connection-string.png)
4. <span data-ttu-id="bcb1f-169">Teraz wróć toohello aplikacji usługi ustawień i wybierz **Narzędzia > Edytor usług aplikacji (wersja zapoznawcza) > na > Przejdź**.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-169">Now go back toohello App Service Settings and select **Tools > App Service Editor (Preview) > On > Go**.</span></span>
   
    ![Zrzut ekranu przedstawiający połączenia magistrali usług](./media/stream-analytics-functions-redis/app-service-editor.png)
5. <span data-ttu-id="bcb1f-171">W wybranym edytorze, Utwórz plik JSON o nazwie **project.json** z hello po i zapisaniu tooyour dysku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-171">In an editor of your choice, create a JSON file named **project.json** with hello following and save it tooyour local disk.</span></span>
   
        {
            "frameworks": {
                "net46": {
                    "dependencies": {
                        "StackExchange.Redis":"1.1.603",
                        "Newtonsoft.Json": "9.0.1"
                    }
                }
            }
        }
6. <span data-ttu-id="bcb1f-172">Przekazywanie tego pliku w katalogu głównym hello funkcji (nie WWWROOT).</span><span class="sxs-lookup"><span data-stu-id="bcb1f-172">Upload this file into hello root directory of your function (not WWWROOT).</span></span> <span data-ttu-id="bcb1f-173">Powinny pojawić się w pliku o nazwie **plikiem project.lock.json** pojawiają się automatycznie, potwierdzenie, że hello Nuget "Programie StackExchange.Redis" i "Newtonsoft.Json" importowaniu pakietów.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-173">You should see a file named **project.lock.json** automatically appear, confirming that hello Nuget packages “StackExchange.Redis” and “Newtonsoft.Json” have been imported.</span></span>
7. <span data-ttu-id="bcb1f-174">W hello **run.csx** pliku, Zastąp hello wstępnie wygenerowanego kodu hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-174">In hello **run.csx** file, replace hello pre-generated code with hello following code.</span></span> <span data-ttu-id="bcb1f-175">W funkcji lazyConnection hello, zastąp "POŁ NAME" o nazwie hello utworzonego w kroku 2 **przechowywania danych w pamięci podręcznej Redis hello**.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-175">In hello lazyConnection function, replace “CONN NAME” with hello name you created in step 2 of **Store data into hello Redis cache**.</span></span>

````

    using System;
    using System.Threading.Tasks;
    using StackExchange.Redis;
    using Newtonsoft.Json;
    using System.Configuration;

    public static void Run(string myQueueItem, TraceWriter log)
    {
        log.Info($"Function processed message: {myQueueItem}");

        // Connection refers tooa property that returns a ConnectionMultiplexer
        IDatabase db = Connection.GetDatabase();
        log.Info($"Created database {db}");

        // Parse JSON and extract hello time
        var message = JsonConvert.DeserializeObject<dynamic>(myQueueItem);
        string time = message.time;
        string callingnum1 = message.callingnum1;

        // Perform cache operations using hello cache object...
        // Simple put of integral data types into hello cache
        string key = time + " - " + callingnum1;
        db.StringSet(key, myQueueItem);
        log.Info($"Object put in database. Key is {key} and value is {myQueueItem}");

        // Simple get of data types from hello cache
        string value = db.StringGet(key);
        log.Info($"Database got: {value}"); 
    }

    // Connect toohello Service Bus
    private static Lazy<ConnectionMultiplexer> lazyConnection = 
        new Lazy<ConnectionMultiplexer>(() =>
            {
                var cnn = ConfigurationManager.ConnectionStrings["CONN NAME"].ConnectionString
                return ConnectionMultiplexer.Connect();
            });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

````

## <a name="start-hello-stream-analytics-job"></a><span data-ttu-id="bcb1f-176">Uruchom zadanie usługi Stream Analytics hello</span><span class="sxs-lookup"><span data-stu-id="bcb1f-176">Start hello Stream Analytics job</span></span>
1. <span data-ttu-id="bcb1f-177">Uruchom aplikację telcodatagen.exe hello.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-177">Start hello telcodatagen.exe application.</span></span> <span data-ttu-id="bcb1f-178">Użycie Hello jest następujący:````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span><span class="sxs-lookup"><span data-stu-id="bcb1f-178">hello usage is as follows: ````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span></span>
2. <span data-ttu-id="bcb1f-179">W bloku zadania usługi analiza strumienia hello w portalu powitania kliknij **Start** u góry hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-179">From hello Stream Analytics Job blade in hello portal, click **Start** at hello top of hello page.</span></span>
   
    ![Zrzut ekranu przedstawiający zadanie rozpoczęcia](./media/stream-analytics-functions-redis/starting-job.png)
3. <span data-ttu-id="bcb1f-181">W hello **rozpoczęcia zadania** wyświetlonym bloku, wybierz **teraz** , a następnie kliknij przycisk hello **Start** przycisk u dołu hello hello ekranu.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-181">In hello **Start job** blade that appears, select **Now** and then click hello **Start** button at hello bottom of hello screen.</span></span> <span data-ttu-id="bcb1f-182">Stan zadania Hello zmienia tooStarting i po czasie niektóre tooRunning zmiany.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-182">hello job status changes tooStarting and after some time changes tooRunning.</span></span>
   
    ![Zrzut ekranu przedstawiający wybór godziny rozpoczęcia zadania](./media/stream-analytics-functions-redis/start-job-time.png)

## <a name="run-solution-and-check-results"></a><span data-ttu-id="bcb1f-184">Uruchamianie rozwiązania i wyniki sprawdzenia</span><span class="sxs-lookup"><span data-stu-id="bcb1f-184">Run solution and check results</span></span>
<span data-ttu-id="bcb1f-185">Cofnięcie tooyour **ServiceBusQueueTrigger** strony, powinien zostać wyświetlony dziennika instrukcje.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-185">Going back tooyour **ServiceBusQueueTrigger** page, you should now see log statements.</span></span> <span data-ttu-id="bcb1f-186">Te dzienniki pokazują, że coś uzyskanego od hello kolejką usługi Service Bus, umieść ją do bazy danych hello, oraz pobranych go się przy użyciu czasu hello jako klucz hello!</span><span class="sxs-lookup"><span data-stu-id="bcb1f-186">These logs show that you got something from hello Service Bus Queue, put it into hello database, and fetched it out using hello time as hello key!</span></span>

<span data-ttu-id="bcb1f-187">tooverify, które dane są w pamięci podręcznej Redis, przejdź strony pamięci podręcznej Redis tooyour hello nowego portalu (jak pokazano w poprzednim hello [Tworzenie pamięci podręcznej Redis Azure](#Create-an-Azure-Redis-Cache) krok) i wybierz konsoli.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-187">tooverify that your data is in your Redis cache, go tooyour Redis cache page in hello new portal (as shown in hello preceding [Create an Azure Redis Cache](#Create-an-Azure-Redis-Cache) step) and select Console.</span></span>

<span data-ttu-id="bcb1f-188">Teraz można napisać tooconfirm polecenia Redis dane znajdują się w pamięci podręcznej hello w rzeczywistości.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-188">Now you can write Redis commands tooconfirm that data is in fact in hello cache.</span></span>

![Zrzut ekranu konsoli pamięci podręcznej Redis](./media/stream-analytics-functions-redis/redis-console.png)

## <a name="next-steps"></a><span data-ttu-id="bcb1f-190">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bcb1f-190">Next steps</span></span>
<span data-ttu-id="bcb1f-191">Firma Microsoft Cieszymy się o nowościach hello Azure Functions Stream analytics można zrobić ze sobą i mamy nadzieję, że to zyskujesz dzięki nowych możliwości.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-191">We’re excited about hello new things Azure Functions and Stream analytics can do together, and we hope this unlocks new possibilities for you.</span></span> <span data-ttu-id="bcb1f-192">Jeśli masz opinię na następny mają uznać hello wolnego toouse [witryny Azure UserVoice](https://feedback.azure.com/forums/270577-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="bcb1f-192">If you have any feedback on what you want next, feel free toouse hello [Azure UserVoice site](https://feedback.azure.com/forums/270577-stream-analytics).</span></span>

<span data-ttu-id="bcb1f-193">Jeśli nowy Microsoft Azure, zachęcamy tootry go przez skorzystania [bezpłatnego konta wersji próbnej Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bcb1f-193">If you are new Microsoft Azure, we invite you tootry it out by signing up for a [free Azure trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="bcb1f-194">Jeśli są nowe tooStream Analytics, a następnie zachęcamy zbyt[utworzyć swoją pierwszą pracę Stream Analytics](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="bcb1f-194">If you are new tooStream Analytics, then we invite you too[create your first Stream Analytics job](stream-analytics-create-a-job.md).</span></span>

<span data-ttu-id="bcb1f-195">Jeśli potrzebujesz żadnego pomocy lub masz pytania, opublikuj wpis na [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) lub [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) forach.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-195">If you need any help or have questions, post on [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) or [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) forums.</span></span> 

<span data-ttu-id="bcb1f-196">Można również wyświetlić hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="bcb1f-196">You can also see hello following resources:</span></span>

* [<span data-ttu-id="bcb1f-197">Dokumentacja usługi Azure Functions dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="bcb1f-197">Azure Functions developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="bcb1f-198">Azure dokumentacja dla deweloperów funkcje C#</span><span class="sxs-lookup"><span data-stu-id="bcb1f-198">Azure Functions C# developer reference</span></span>](../azure-functions/functions-reference-csharp.md)
* [<span data-ttu-id="bcb1f-199">Azure dokumentacja dla deweloperów funkcje F #</span><span class="sxs-lookup"><span data-stu-id="bcb1f-199">Azure Functions F# developer reference</span></span>](../azure-functions/functions-reference-fsharp.md)
* [<span data-ttu-id="bcb1f-200">Dokumentacja dla deweloperów NodeJS funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="bcb1f-200">Azure Functions NodeJS developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="bcb1f-201">Azure funkcje wyzwalaczy i powiązań</span><span class="sxs-lookup"><span data-stu-id="bcb1f-201">Azure Functions triggers and bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
* [<span data-ttu-id="bcb1f-202">Jak toomonitor Azure pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="bcb1f-202">How toomonitor Azure Redis Cache</span></span>](../redis-cache/cache-how-to-monitor.md)

<span data-ttu-id="bcb1f-203">Wykonaj toostay aktualne we wszystkich najnowsze wiadomości powitania i funkcje, [ @AzureStreaming ](https://twitter.com/AzureStreaming) w serwisie Twitter.</span><span class="sxs-lookup"><span data-stu-id="bcb1f-203">toostay up-to-date on all hello latest news and features, follow [@AzureStreaming](https://twitter.com/AzureStreaming) on Twitter.</span></span>

[fraud-detection]: stream-analytics-real-time-fraud-detection.md
[servicebus-getstarted]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[use-rediscache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md
[functions-getstarted]: ../azure-functions/functions-create-first-azure-function.md
