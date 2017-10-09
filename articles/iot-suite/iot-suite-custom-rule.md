---
title: "reguły niestandardowej w pakiet IoT Azure aaaCreate | Dokumentacja firmy Microsoft"
description: "Jak toocreate reguły niestandardowej w pakiet IoT wstępnie skonfigurowane rozwiązanie."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 6c5bb2ca54f3f17b99ad482e727c8e9fa28d7fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-rule-in-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="ae169-103">Utwórz regułę niestandardową w hello zdalne monitorowanie wstępnie skonfigurowane rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="ae169-103">Create a custom rule in hello remote monitoring preconfigured solution</span></span>

## <a name="introduction"></a><span data-ttu-id="ae169-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="ae169-104">Introduction</span></span>

<span data-ttu-id="ae169-105">W rozwiązaniach hello wstępnie skonfigurowane, można skonfigurować [wartość reguły, które są wyzwalane w razie telemetrii urządzenia osiągnie określony próg][lnk-builtin-rule].</span><span class="sxs-lookup"><span data-stu-id="ae169-105">In hello preconfigured solutions, you can configure [rules that trigger when a telemetry value for a device reaches a specific threshold][lnk-builtin-rule].</span></span> <span data-ttu-id="ae169-106">[Dynamiczne telemetrii za pomocą zdalnego wstępnie skonfigurowane rozwiązanie monitorujące hello] [ lnk-dynamic-telemetry] opisuje sposób dodawania wartości niestandardowych telemetrii, takich jak *ExternalTemperature* tooyour rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ae169-106">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic-telemetry] describes how you can add custom telemetry values, such as *ExternalTemperature* tooyour solution.</span></span> <span data-ttu-id="ae169-107">W tym artykule opisano, jak typy toocreate niestandardową regułę dynamiczne telemetrii w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="ae169-107">This article shows you how toocreate custom rule for dynamic telemetry types in your solution.</span></span>

<span data-ttu-id="ae169-108">W tym samouczku korzysta z prostego Node.js symulowane urządzenie toogenerate dynamiczne telemetrii toosend toohello wstępnie skonfigurowane rozwiązanie zaplecze.</span><span class="sxs-lookup"><span data-stu-id="ae169-108">This tutorial uses a simple Node.js simulated device toogenerate dynamic telemetry toosend toohello preconfigured solution back end.</span></span> <span data-ttu-id="ae169-109">Następnie dodaj niestandardowe reguły w hello **RemoteMonitoring** rozwiązania Visual Studio i wdrażanie tego tooyour dostosowane zaplecza subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ae169-109">You then add custom rules in hello **RemoteMonitoring** Visual Studio solution and deploy this customized back end tooyour Azure subscription.</span></span>

<span data-ttu-id="ae169-110">toocomplete tego samouczka należy:</span><span class="sxs-lookup"><span data-stu-id="ae169-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="ae169-111">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ae169-111">An active Azure subscription.</span></span> <span data-ttu-id="ae169-112">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="ae169-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ae169-113">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="ae169-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="ae169-114">[Node.js] [ lnk-node] wersji 0.12.x lub nowszej toocreate symulowane urządzenie.</span><span class="sxs-lookup"><span data-stu-id="ae169-114">[Node.js][lnk-node] version 0.12.x or later toocreate a simulated device.</span></span>
* <span data-ttu-id="ae169-115">Visual Studio 2015 lub Visual Studio 2017 toomodify hello wstępnie zaplecze rozwiązania nowej reguły.</span><span class="sxs-lookup"><span data-stu-id="ae169-115">Visual Studio 2015 or Visual Studio 2017 toomodify hello preconfigured solution back end with your new rules.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

<span data-ttu-id="ae169-116">Zanotuj hello Nazwa rozwiązania, którą wybrano dla danego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="ae169-116">Make a note of hello solution name you chose for your deployment.</span></span> <span data-ttu-id="ae169-117">Należy to nazwa rozwiązania w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="ae169-117">You need this solution name later in this tutorial.</span></span>

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

<span data-ttu-id="ae169-118">Po upewnieniu się, że jest wysyłany, można zatrzymać aplikacji konsoli Node.js hello **ExternalTemperature** toohello telemetrii wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="ae169-118">You can stop hello Node.js console app when you have verified that it is sending **ExternalTemperature** telemetry toohello preconfigured solution.</span></span> <span data-ttu-id="ae169-119">Nie zamykaj okna konsoli hello ponieważ ponownie uruchom tę aplikację konsoli Node.js po dodaniu hello reguły niestandardowej toohello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ae169-119">Keep hello console window open because you run this Node.js console app again after you add hello custom rule toohello solution.</span></span>

## <a name="rule-storage-locations"></a><span data-ttu-id="ae169-120">Lokalizacje magazynu reguły</span><span class="sxs-lookup"><span data-stu-id="ae169-120">Rule storage locations</span></span>

<span data-ttu-id="ae169-121">Informacje o regułach jest utrwalona w dwóch miejscach:</span><span class="sxs-lookup"><span data-stu-id="ae169-121">Information about rules is persisted in two locations:</span></span>

* <span data-ttu-id="ae169-122">**DeviceRulesNormalizedTable** tabeli — w tej tabeli są przechowywane znormalizowane odwołania toohello reguł zdefiniowanych hello rozwiązanie portalu.</span><span class="sxs-lookup"><span data-stu-id="ae169-122">**DeviceRulesNormalizedTable** table – This table stores a normalized reference toohello rules defined by hello solution portal.</span></span> <span data-ttu-id="ae169-123">Reguły urządzenia są wyświetlane w portalu rozwiązania hello, wysyła zapytanie tej tabeli hello definicji reguły.</span><span class="sxs-lookup"><span data-stu-id="ae169-123">When hello solution portal displays device rules, it queries this table for hello rule definitions.</span></span>
* <span data-ttu-id="ae169-124">**DeviceRules** obiektu blob — ten obiekt blob przechowuje wszystkie reguły hello zdefiniowana dla wszystkich zarejestrowanych urządzeń i jest zdefiniowany jako zadania usługi analiza strumienia Azure wejściowych toohello odwołania.</span><span class="sxs-lookup"><span data-stu-id="ae169-124">**DeviceRules** blob – This blob stores all hello rules defined for all registered devices and is defined as a reference input toohello Azure Stream Analytics jobs.</span></span>
 
<span data-ttu-id="ae169-125">Podczas aktualizacji istniejącej reguły lub zdefiniuj nową regułę w portalu rozwiązania hello hello tabeli oraz obiektów blob są zaktualizowane tooreflect hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="ae169-125">When you update an existing rule or define a new rule in hello solution portal, both hello table and blob are updated tooreflect hello changes.</span></span> <span data-ttu-id="ae169-126">Reguła Hello definicji wyświetlana w portalu hello pochodzi z hello tabeli magazynu i reguł hello definicji odwołuje się zadania usługi analiza strumienia hello pochodzi z obiektu blob hello.</span><span class="sxs-lookup"><span data-stu-id="ae169-126">hello rule definition displayed in hello portal comes from hello table store, and hello rule definition referenced by hello Stream Analytics jobs comes from hello blob.</span></span> 

## <a name="update-hello-remotemonitoring-visual-studio-solution"></a><span data-ttu-id="ae169-127">Zaktualizuj hello RemoteMonitoring rozwiązania Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ae169-127">Update hello RemoteMonitoring Visual Studio solution</span></span>

<span data-ttu-id="ae169-128">Witaj poniższej procedurze pokazano, jak toomodify hello tooinclude rozwiązania RemoteMonitoring Visual Studio nową regułę, która używa hello **ExternalTemperature** danych telemetrycznych wysłanych z hello symulowane urządzenie:</span><span class="sxs-lookup"><span data-stu-id="ae169-128">hello following steps show you how toomodify hello RemoteMonitoring Visual Studio solution tooinclude a new rule that uses hello **ExternalTemperature** telemetry sent from hello simulated device:</span></span>

1. <span data-ttu-id="ae169-129">Jeśli użytkownik ma nie zrobiono, hello w klonowania **azure iot — zdalnego monitorowania** repozytorium tooa odpowiedniej lokalizacji na komputerze lokalnym za pomocą następującego polecenia Git hello:</span><span class="sxs-lookup"><span data-stu-id="ae169-129">If you have not already done so, clone hello **azure-iot-remote-monitoring** repository tooa suitable location on your local machine using hello following Git command:</span></span>

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. <span data-ttu-id="ae169-130">W programie Visual Studio Otwórz plik RemoteMonitoring.sln hello z kopii lokalnej hello **azure iot — zdalnego monitorowania** repozytorium.</span><span class="sxs-lookup"><span data-stu-id="ae169-130">In Visual Studio, open hello RemoteMonitoring.sln file from your local copy of hello **azure-iot-remote-monitoring** repository.</span></span>

3. <span data-ttu-id="ae169-131">Otwórz plik hello Infrastructure\Models\DeviceRuleBlobEntity.cs i Dodaj **ExternalTemperature** właściwości w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ae169-131">Open hello file Infrastructure\Models\DeviceRuleBlobEntity.cs and add an **ExternalTemperature** property as follows:</span></span>

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. <span data-ttu-id="ae169-132">W hello tego samego pliku, należy dodać **ExternalTemperatureRuleOutput** właściwości w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ae169-132">In hello same file, add an **ExternalTemperatureRuleOutput** property as follows:</span></span>

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. <span data-ttu-id="ae169-133">Otwórz plik hello Infrastructure\Models\DeviceRuleDataFields.cs i dodaj następujące hello **ExternalTemperature** właściwości po istniejących hello **wilgotności** właściwości:</span><span class="sxs-lookup"><span data-stu-id="ae169-133">Open hello file Infrastructure\Models\DeviceRuleDataFields.cs and add hello following **ExternalTemperature** property after hello existing **Humidity** property:</span></span>

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. <span data-ttu-id="ae169-134">W hello tego samego pliku, zaktualizuj hello **_availableDataFields** tooinclude metody **ExternalTemperature** w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ae169-134">In hello same file, update hello **_availableDataFields** method tooinclude **ExternalTemperature** as follows:</span></span>

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. <span data-ttu-id="ae169-135">Otwórz plik hello Infrastructure\Repository\DeviceRulesRepository.cs i zmodyfikować hello **BuildBlobEntityListFromTableRows** metody w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ae169-135">Open hello file Infrastructure\Repository\DeviceRulesRepository.cs and modify hello **BuildBlobEntityListFromTableRows** method as follows:</span></span>

    ```csharp
    else if (rule.DataField == DeviceRuleDataFields.Humidity)
    {
        entity.Humidity = rule.Threshold;
        entity.HumidityRuleOutput = rule.RuleOutput;
    }
    else if (rule.DataField == DeviceRuleDataFields.ExternalTemperature)
    {
      entity.ExternalTemperature = rule.Threshold;
      entity.ExternalTemperatureRuleOutput = rule.RuleOutput;
    }
    ```

## <a name="rebuild-and-redeploy-hello-solution"></a><span data-ttu-id="ae169-136">Ponowne skompilowanie i wdrożenie rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="ae169-136">Rebuild and redeploy hello solution.</span></span>

<span data-ttu-id="ae169-137">Teraz można wdrożyć tooyour rozwiązania hello zaktualizować subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ae169-137">You can now deploy hello updated solution tooyour Azure subscription.</span></span>

1. <span data-ttu-id="ae169-138">Otwórz wiersz polecenia z podwyższonym poziomem uprawnień i przejdź toohello głównym kopii lokalnej hello azure iot — zdalnego monitorowania repozytorium.</span><span class="sxs-lookup"><span data-stu-id="ae169-138">Open an elevated command prompt and navigate toohello root of your local copy of hello azure-iot-remote-monitoring repository.</span></span>

2. <span data-ttu-id="ae169-139">toodeploy rozwiązania zaktualizowane, uruchom następujące polecenie, zastępując hello **{Nazwa wdrożenia}** o nazwie hello wdrożenia wstępnie skonfigurowane rozwiązanie zanotowany wcześniej:</span><span class="sxs-lookup"><span data-stu-id="ae169-139">toodeploy your updated solution, run hello following command substituting **{deployment name}** with hello name of your preconfigured solution deployment that you noted previously:</span></span>

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-hello-stream-analytics-job"></a><span data-ttu-id="ae169-140">Zadanie Stream Analytics hello aktualizacji</span><span class="sxs-lookup"><span data-stu-id="ae169-140">Update hello Stream Analytics job</span></span>

<span data-ttu-id="ae169-141">Po zakończeniu wdrażania hello, możesz je zaktualizować hello analiza strumienia zadania toouse hello nowej reguły.</span><span class="sxs-lookup"><span data-stu-id="ae169-141">When hello deployment is complete, you can update hello Stream Analytics job toouse hello new rule definitions.</span></span>

1. <span data-ttu-id="ae169-142">W hello portalu Azure Przejdź toohello grupę zasobów, która zawiera zasoby wstępnie skonfigurowanych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="ae169-142">In hello Azure portal, navigate toohello resource group that contains your preconfigured solution resources.</span></span> <span data-ttu-id="ae169-143">Ta grupa zasobów ma hello sama nazwa określona dla hello rozwiązania podczas wdrażania hello.</span><span class="sxs-lookup"><span data-stu-id="ae169-143">This resource group has hello same name you specified for hello solution during hello deployment.</span></span>

2. <span data-ttu-id="ae169-144">Przejdź toohello {Nazwa wdrożenia}-zadania usługi analiza strumienia reguły.</span><span class="sxs-lookup"><span data-stu-id="ae169-144">Navigate toohello {deployment name}-Rules Stream Analytics job.</span></span> 

3. <span data-ttu-id="ae169-145">Kliknij przycisk **zatrzymać** zadanie usługi Stream Analytics hello toostop uruchamianie.</span><span class="sxs-lookup"><span data-stu-id="ae169-145">Click **Stop** toostop hello Stream Analytics job from running.</span></span> <span data-ttu-id="ae169-146">(Należy poczekać hello toostop zadania przesyłania strumieniowego, zanim będzie można edytować zapytania hello).</span><span class="sxs-lookup"><span data-stu-id="ae169-146">(You must wait for hello streaming job toostop before you can edit hello query).</span></span>

4. <span data-ttu-id="ae169-147">Kliknij przycisk **zapytania**.</span><span class="sxs-lookup"><span data-stu-id="ae169-147">Click **Query**.</span></span> <span data-ttu-id="ae169-148">Edytuj hello zapytania tooinclude hello **wybierz** instrukcji dla **ExternalTemperature**.</span><span class="sxs-lookup"><span data-stu-id="ae169-148">Edit hello query tooinclude hello **SELECT** statement for **ExternalTemperature**.</span></span> <span data-ttu-id="ae169-149">Hello poniższy przykład przedstawia hello pełne zapytanie z hello nowe **wybierz** instrukcji:</span><span class="sxs-lookup"><span data-stu-id="ae169-149">hello following sample shows hello complete query with hello new **SELECT** statement:</span></span>

    ```
    WITH AlarmsData AS 
    (
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Temperature' as ReadingType,
         Stream.Temperature as Reading,
         Ref.Temperature as Threshold,
         Ref.TemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Humidity' as ReadingType,
         Stream.Humidity as Reading,
         Ref.Humidity as Threshold,
         Ref.HumidityRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'ExternalTemperature' as ReadingType,
         Stream.ExternalTemperature as Reading,
         Ref.ExternalTemperature as Threshold,
         Ref.ExternalTemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.ExternalTemperature IS NOT null AND Stream.ExternalTemperature > Ref.ExternalTemperature
    )
     
    SELECT *
    INTO DeviceRulesMonitoring
    FROM AlarmsData
     
    SELECT *
    INTO DeviceRulesHub
    FROM AlarmsData
    ```

5. <span data-ttu-id="ae169-150">Kliknij przycisk **zapisać** toochange hello zaktualizować reguły zapytania.</span><span class="sxs-lookup"><span data-stu-id="ae169-150">Click **Save** toochange hello updated rule query.</span></span>

6. <span data-ttu-id="ae169-151">Kliknij przycisk **Start** zadanie usługi Stream Analytics hello toostart ponowne uruchomienie.</span><span class="sxs-lookup"><span data-stu-id="ae169-151">Click **Start** toostart hello Stream Analytics job running again.</span></span>

## <a name="add-your-new-rule-in-hello-dashboard"></a><span data-ttu-id="ae169-152">Dodaj nową regułę na pulpicie nawigacyjnym hello</span><span class="sxs-lookup"><span data-stu-id="ae169-152">Add your new rule in hello dashboard</span></span>

<span data-ttu-id="ae169-153">Można teraz dodawać hello **ExternalTemperature** urządzenia tooa reguły na pulpicie nawigacyjnym rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="ae169-153">You can now add hello **ExternalTemperature** rule tooa device in hello solution dashboard.</span></span>

1. <span data-ttu-id="ae169-154">Przejdź toohello rozwiązanie portalu.</span><span class="sxs-lookup"><span data-stu-id="ae169-154">Navigate toohello solution portal.</span></span>

2. <span data-ttu-id="ae169-155">Przejdź toohello **urządzeń** panelu.</span><span class="sxs-lookup"><span data-stu-id="ae169-155">Navigate toohello **Devices** panel.</span></span>

3. <span data-ttu-id="ae169-156">Zlokalizuj hello urządzeń niestandardowych utworzony wysyłanej **ExternalTemperature** telemetrii i na powitania **szczegóły urządzenia** panelu, kliknij przycisk **Dodaj regułę**.</span><span class="sxs-lookup"><span data-stu-id="ae169-156">Locate hello custom device you created that sends **ExternalTemperature** telemetry and on hello **Device Details** panel, click **Add Rule**.</span></span>

4. <span data-ttu-id="ae169-157">Wybierz **ExternalTemperature** w **pola danych**.</span><span class="sxs-lookup"><span data-stu-id="ae169-157">Select **ExternalTemperature** in **Data Field**.</span></span>

5. <span data-ttu-id="ae169-158">Ustaw **próg** too56.</span><span class="sxs-lookup"><span data-stu-id="ae169-158">Set **Threshold** too56.</span></span> <span data-ttu-id="ae169-159">Następnie kliknij przycisk **Zapisz i Wyświetl reguły**.</span><span class="sxs-lookup"><span data-stu-id="ae169-159">Then click **Save and view rules**.</span></span>

6. <span data-ttu-id="ae169-160">Zwraca toohello pulpitu nawigacyjnego tooview hello alarm historii.</span><span class="sxs-lookup"><span data-stu-id="ae169-160">Return toohello dashboard tooview hello alarm history.</span></span>

7. <span data-ttu-id="ae169-161">Po lewej, Otwórz okno konsoli hello start wysyłania hello Node.js konsoli aplikacji toobegin **ExternalTemperature** danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="ae169-161">In hello console window you left open, start hello Node.js console app toobegin sending **ExternalTemperature** telemetry data.</span></span>

8. <span data-ttu-id="ae169-162">Zwróć uwagę, że hello **historii Alarm** tabeli przedstawiono nowe alarmy po wyzwoleniu hello nowej reguły.</span><span class="sxs-lookup"><span data-stu-id="ae169-162">Notice that hello **Alarm History** table shows new alarms when hello new rule is triggered.</span></span>
 
## <a name="additional-information"></a><span data-ttu-id="ae169-163">Dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="ae169-163">Additional information</span></span>

<span data-ttu-id="ae169-164">Zmiana operator hello  **>**  jest bardziej złożony i wykracza poza hello kroki opisane w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="ae169-164">Changing hello operator **>** is more complex and goes beyond hello steps outlined in this tutorial.</span></span> <span data-ttu-id="ae169-165">Można zmienić toouse zadania usługi analiza strumienia hello niezależnie od operatora Ci się podoba, odzwierciedlający operatora w portalu rozwiązania hello jest bardziej złożone zadania.</span><span class="sxs-lookup"><span data-stu-id="ae169-165">While you can change hello Stream Analytics job toouse whatever operator you like, reflecting that operator in hello solution portal is a more complex task.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ae169-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ae169-166">Next steps</span></span>
<span data-ttu-id="ae169-167">Teraz, w tym samouczku jak toocreate reguły niestandardowe, możesz dowiedzieć się więcej o rozwiązaniach hello wstępnie:</span><span class="sxs-lookup"><span data-stu-id="ae169-167">Now that you've seen how toocreate custom rules, you can learn more about hello preconfigured solutions:</span></span>

- <span data-ttu-id="ae169-168">[Łączenie aplikacji logiki tooyour Azure IoT pakiet monitorowania zdalnego wstępnie skonfigurowane rozwiązanie][lnk-logic-app]</span><span class="sxs-lookup"><span data-stu-id="ae169-168">[Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logic-app]</span></span>
- <span data-ttu-id="ae169-169">[Urządzenie informacji metadanych w monitorowania zdalnego hello wstępnie skonfigurowane rozwiązanie][lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="ae169-169">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md