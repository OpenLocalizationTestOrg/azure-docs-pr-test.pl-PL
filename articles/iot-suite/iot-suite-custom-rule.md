---
title: "Utwórz regułę niestandardową pakietu IoT Azure | Dokumentacja firmy Microsoft"
description: "Jak utworzyć niestandardową regułę w pakiet IoT wstępnie skonfigurowane rozwiązanie."
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
ms.openlocfilehash: d58c27234ea05a82aaa3e8d72f70c1449980df09
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-custom-rule-in-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="1acb4-103">Utwórz regułę niestandardową w zdalnym wstępnie skonfigurowane rozwiązanie monitorowania</span><span class="sxs-lookup"><span data-stu-id="1acb4-103">Create a custom rule in the remote monitoring preconfigured solution</span></span>

## <a name="introduction"></a><span data-ttu-id="1acb4-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="1acb4-104">Introduction</span></span>

<span data-ttu-id="1acb4-105">W przypadku wstępnie skonfigurowanych rozwiązań, można skonfigurować [wartość reguły, które są wyzwalane w razie telemetrii urządzenia osiągnie określony próg][lnk-builtin-rule].</span><span class="sxs-lookup"><span data-stu-id="1acb4-105">In the preconfigured solutions, you can configure [rules that trigger when a telemetry value for a device reaches a specific threshold][lnk-builtin-rule].</span></span> <span data-ttu-id="1acb4-106">[Użyj dynamicznych danych telemetrycznych z monitorowania zdalnego wstępnie skonfigurowane rozwiązanie] [ lnk-dynamic-telemetry] opisuje sposób dodawania wartości niestandardowych telemetrii, takich jak *ExternalTemperature* do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="1acb4-106">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic-telemetry] describes how you can add custom telemetry values, such as *ExternalTemperature* to your solution.</span></span> <span data-ttu-id="1acb4-107">W tym artykule przedstawiono sposób tworzenia reguły niestandardowe dla typów dynamicznych telemetrii w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="1acb4-107">This article shows you how to create custom rule for dynamic telemetry types in your solution.</span></span>

<span data-ttu-id="1acb4-108">W tym samouczku używana proste Node.js symulowane urządzenie można wygenerować dynamiczne telemetrię, aby wysłać do zaplecza wstępnie skonfigurowanego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="1acb4-108">This tutorial uses a simple Node.js simulated device to generate dynamic telemetry to send to the preconfigured solution back end.</span></span> <span data-ttu-id="1acb4-109">Następnie dodaj niestandardowe reguły w **RemoteMonitoring** rozwiązania Visual Studio i wdrażanie tego dostosowane zaplecza do subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1acb4-109">You then add custom rules in the **RemoteMonitoring** Visual Studio solution and deploy this customized back end to your Azure subscription.</span></span>

<span data-ttu-id="1acb4-110">Do ukończenia tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="1acb4-110">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="1acb4-111">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1acb4-111">An active Azure subscription.</span></span> <span data-ttu-id="1acb4-112">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="1acb4-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1acb4-113">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="1acb4-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="1acb4-114">[Node.js] [ lnk-node] wersji 0.12.x lub nowszej, aby utworzyć symulowane urządzenie.</span><span class="sxs-lookup"><span data-stu-id="1acb4-114">[Node.js][lnk-node] version 0.12.x or later to create a simulated device.</span></span>
* <span data-ttu-id="1acb4-115">Visual Studio 2015 lub Visual Studio 2017 zmodyfikować wstępnie skonfigurowane rozwiązanie ponownie kończyć się nowych reguł.</span><span class="sxs-lookup"><span data-stu-id="1acb4-115">Visual Studio 2015 or Visual Studio 2017 to modify the preconfigured solution back end with your new rules.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

<span data-ttu-id="1acb4-116">Zanotuj nazwy rozwiązania, którą wybrano dla danego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="1acb4-116">Make a note of the solution name you chose for your deployment.</span></span> <span data-ttu-id="1acb4-117">Należy to nazwa rozwiązania w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="1acb4-117">You need this solution name later in this tutorial.</span></span>

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

<span data-ttu-id="1acb4-118">Po upewnieniu się, że jest wysyłany, można zatrzymać aplikacji konsoli Node.js **ExternalTemperature** telemetrię, aby wstępnie skonfigurowanych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="1acb4-118">You can stop the Node.js console app when you have verified that it is sending **ExternalTemperature** telemetry to the preconfigured solution.</span></span> <span data-ttu-id="1acb4-119">Nie zamykaj okna konsoli ponieważ ponownie uruchom tę aplikację konsoli Node.js po dodaniu niestandardowej reguły do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="1acb4-119">Keep the console window open because you run this Node.js console app again after you add the custom rule to the solution.</span></span>

## <a name="rule-storage-locations"></a><span data-ttu-id="1acb4-120">Lokalizacje magazynu reguły</span><span class="sxs-lookup"><span data-stu-id="1acb4-120">Rule storage locations</span></span>

<span data-ttu-id="1acb4-121">Informacje o regułach jest utrwalona w dwóch miejscach:</span><span class="sxs-lookup"><span data-stu-id="1acb4-121">Information about rules is persisted in two locations:</span></span>

* <span data-ttu-id="1acb4-122">**DeviceRulesNormalizedTable** tabeli — znormalizowane odwołanie do reguły zdefiniowane przez portal rozwiązania są przechowywane w tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="1acb4-122">**DeviceRulesNormalizedTable** table – This table stores a normalized reference to the rules defined by the solution portal.</span></span> <span data-ttu-id="1acb4-123">Reguły urządzenia są wyświetlane w portalu rozwiązania, wysyła zapytanie tej tabeli definicji reguły.</span><span class="sxs-lookup"><span data-stu-id="1acb4-123">When the solution portal displays device rules, it queries this table for the rule definitions.</span></span>
* <span data-ttu-id="1acb4-124">**DeviceRules** obiektu blob — ten obiekt blob przechowuje wszystkie reguły zdefiniowane dla wszystkich zarejestrowanych urządzeń i jest zdefiniowany jako danych wejściowych do zadania usługi analiza strumienia Azure odwołanie.</span><span class="sxs-lookup"><span data-stu-id="1acb4-124">**DeviceRules** blob – This blob stores all the rules defined for all registered devices and is defined as a reference input to the Azure Stream Analytics jobs.</span></span>
 
<span data-ttu-id="1acb4-125">Podczas aktualizacji istniejącej reguły lub zdefiniuj nowe reguły w portalu rozwiązania, tabelę i obiektów blob są aktualizowane zgodnie ze zmianami.</span><span class="sxs-lookup"><span data-stu-id="1acb4-125">When you update an existing rule or define a new rule in the solution portal, both the table and blob are updated to reflect the changes.</span></span> <span data-ttu-id="1acb4-126">Definicję reguły wyświetlana w portalu jest dostarczany z tabeli magazynu, a Definicja reguły odwołuje się zadania usługi analiza strumienia pochodzi z obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="1acb4-126">The rule definition displayed in the portal comes from the table store, and the rule definition referenced by the Stream Analytics jobs comes from the blob.</span></span> 

## <a name="update-the-remotemonitoring-visual-studio-solution"></a><span data-ttu-id="1acb4-127">Aktualizacji rozwiązania RemoteMonitoring Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1acb4-127">Update the RemoteMonitoring Visual Studio solution</span></span>

<span data-ttu-id="1acb4-128">Poniższe kroki pokazują sposób modyfikowania RemoteMonitoring rozwiązanie programu Visual Studio do uwzględnienia nową regułę, która używa **ExternalTemperature** danych telemetrycznych wysłanych z symulowane urządzenie:</span><span class="sxs-lookup"><span data-stu-id="1acb4-128">The following steps show you how to modify the RemoteMonitoring Visual Studio solution to include a new rule that uses the **ExternalTemperature** telemetry sent from the simulated device:</span></span>

1. <span data-ttu-id="1acb4-129">Jeśli nie zostało to jeszcze zrobione, klonowanie **azure iot — zdalnego monitorowania** repozytorium do odpowiedniej lokalizacji na komputerze lokalnym za pomocą następujących poleceń Git:</span><span class="sxs-lookup"><span data-stu-id="1acb4-129">If you have not already done so, clone the **azure-iot-remote-monitoring** repository to a suitable location on your local machine using the following Git command:</span></span>

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. <span data-ttu-id="1acb4-130">W programie Visual Studio Otwórz plik RemoteMonitoring.sln z lokalną kopię **azure iot — zdalnego monitorowania** repozytorium.</span><span class="sxs-lookup"><span data-stu-id="1acb4-130">In Visual Studio, open the RemoteMonitoring.sln file from your local copy of the **azure-iot-remote-monitoring** repository.</span></span>

3. <span data-ttu-id="1acb4-131">Otwórz plik Infrastructure\Models\DeviceRuleBlobEntity.cs i Dodaj **ExternalTemperature** właściwości w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1acb4-131">Open the file Infrastructure\Models\DeviceRuleBlobEntity.cs and add an **ExternalTemperature** property as follows:</span></span>

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. <span data-ttu-id="1acb4-132">W tym samym pliku Dodaj **ExternalTemperatureRuleOutput** właściwości w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1acb4-132">In the same file, add an **ExternalTemperatureRuleOutput** property as follows:</span></span>

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. <span data-ttu-id="1acb4-133">Otwórz plik Infrastructure\Models\DeviceRuleDataFields.cs i Dodaj następujący **ExternalTemperature** właściwości po istniejącej **wilgotności** właściwości:</span><span class="sxs-lookup"><span data-stu-id="1acb4-133">Open the file Infrastructure\Models\DeviceRuleDataFields.cs and add the following **ExternalTemperature** property after the existing **Humidity** property:</span></span>

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. <span data-ttu-id="1acb4-134">W tym samym pliku, należy zaktualizować **_availableDataFields** metodę w celu uwzględnienia **ExternalTemperature** w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1acb4-134">In the same file, update the **_availableDataFields** method to include **ExternalTemperature** as follows:</span></span>

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. <span data-ttu-id="1acb4-135">Otwórz plik Infrastructure\Repository\DeviceRulesRepository.cs i zmodyfikować **BuildBlobEntityListFromTableRows** metody w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1acb4-135">Open the file Infrastructure\Repository\DeviceRulesRepository.cs and modify the **BuildBlobEntityListFromTableRows** method as follows:</span></span>

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

## <a name="rebuild-and-redeploy-the-solution"></a><span data-ttu-id="1acb4-136">Ponowne skompilowanie i wdrożenie rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="1acb4-136">Rebuild and redeploy the solution.</span></span>

<span data-ttu-id="1acb4-137">Teraz można wdrażać zaktualizowane rozwiązanie z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1acb4-137">You can now deploy the updated solution to your Azure subscription.</span></span>

1. <span data-ttu-id="1acb4-138">Otwórz wiersz polecenia z podwyższonym poziomem uprawnień i przejdź do katalogu głównego kopii lokalnej repozytorium azure iot — zdalnego monitorowania.</span><span class="sxs-lookup"><span data-stu-id="1acb4-138">Open an elevated command prompt and navigate to the root of your local copy of the azure-iot-remote-monitoring repository.</span></span>

2. <span data-ttu-id="1acb4-139">Aby wdrożyć rozwiązanie zaktualizowane, uruchom następujące polecenie podstawiając **{Nazwa wdrożenia}** o nazwie wdrożenia wstępnie skonfigurowane rozwiązanie zanotowany wcześniej:</span><span class="sxs-lookup"><span data-stu-id="1acb4-139">To deploy your updated solution, run the following command substituting **{deployment name}** with the name of your preconfigured solution deployment that you noted previously:</span></span>

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-the-stream-analytics-job"></a><span data-ttu-id="1acb4-140">Aktualizacja zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="1acb4-140">Update the Stream Analytics job</span></span>

<span data-ttu-id="1acb4-141">Po zakończeniu wdrożenia należy zaktualizować zadania usługi analiza strumienia do używania nowych definicji reguły.</span><span class="sxs-lookup"><span data-stu-id="1acb4-141">When the deployment is complete, you can update the Stream Analytics job to use the new rule definitions.</span></span>

1. <span data-ttu-id="1acb4-142">W portalu Azure przejdź do grupy zasobów zawiera zasoby wstępnie skonfigurowanych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="1acb4-142">In the Azure portal, navigate to the resource group that contains your preconfigured solution resources.</span></span> <span data-ttu-id="1acb4-143">Ta grupa zasobów ma taką samą nazwę, określone dla rozwiązania podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="1acb4-143">This resource group has the same name you specified for the solution during the deployment.</span></span>

2. <span data-ttu-id="1acb4-144">Przejdź do {Nazwa wdrożenia}-zadania usługi analiza strumienia reguły.</span><span class="sxs-lookup"><span data-stu-id="1acb4-144">Navigate to the {deployment name}-Rules Stream Analytics job.</span></span> 

3. <span data-ttu-id="1acb4-145">Kliknij przycisk **zatrzymać** zatrzymania zadania usługi analiza strumienia uruchamianie.</span><span class="sxs-lookup"><span data-stu-id="1acb4-145">Click **Stop** to stop the Stream Analytics job from running.</span></span> <span data-ttu-id="1acb4-146">(Należy poczekać na Zatrzymaj, aby można było edytować zapytanie zadania przesyłania strumieniowego).</span><span class="sxs-lookup"><span data-stu-id="1acb4-146">(You must wait for the streaming job to stop before you can edit the query).</span></span>

4. <span data-ttu-id="1acb4-147">Kliknij przycisk **zapytania**.</span><span class="sxs-lookup"><span data-stu-id="1acb4-147">Click **Query**.</span></span> <span data-ttu-id="1acb4-148">Edytuj zapytanie, aby uwzględnić **wybierz** instrukcji dla **ExternalTemperature**.</span><span class="sxs-lookup"><span data-stu-id="1acb4-148">Edit the query to include the **SELECT** statement for **ExternalTemperature**.</span></span> <span data-ttu-id="1acb4-149">Poniższy przykład przedstawia pełną zapytania z nowym **wybierz** instrukcji:</span><span class="sxs-lookup"><span data-stu-id="1acb4-149">The following sample shows the complete query with the new **SELECT** statement:</span></span>

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

5. <span data-ttu-id="1acb4-150">Kliknij przycisk **zapisać** zmienić zaktualizowane reguły zapytania.</span><span class="sxs-lookup"><span data-stu-id="1acb4-150">Click **Save** to change the updated rule query.</span></span>

6. <span data-ttu-id="1acb4-151">Kliknij przycisk **Start** można uruchomić zadania Stream Analytics, ponowne uruchomienie.</span><span class="sxs-lookup"><span data-stu-id="1acb4-151">Click **Start** to start the Stream Analytics job running again.</span></span>

## <a name="add-your-new-rule-in-the-dashboard"></a><span data-ttu-id="1acb4-152">Dodaj nową regułę na pulpicie nawigacyjnym</span><span class="sxs-lookup"><span data-stu-id="1acb4-152">Add your new rule in the dashboard</span></span>

<span data-ttu-id="1acb4-153">Można teraz dodawać **ExternalTemperature** regułę do urządzenia, na pulpicie nawigacyjnym rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="1acb4-153">You can now add the **ExternalTemperature** rule to a device in the solution dashboard.</span></span>

1. <span data-ttu-id="1acb4-154">Przejdź do portalu rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="1acb4-154">Navigate to the solution portal.</span></span>

2. <span data-ttu-id="1acb4-155">Przejdź do **urządzeń** panelu.</span><span class="sxs-lookup"><span data-stu-id="1acb4-155">Navigate to the **Devices** panel.</span></span>

3. <span data-ttu-id="1acb4-156">Zlokalizuj urządzeń niestandardowych utworzony wysyłanej **ExternalTemperature** telemetrii i na **szczegóły urządzenia** panelu, kliknij przycisk **Dodaj regułę**.</span><span class="sxs-lookup"><span data-stu-id="1acb4-156">Locate the custom device you created that sends **ExternalTemperature** telemetry and on the **Device Details** panel, click **Add Rule**.</span></span>

4. <span data-ttu-id="1acb4-157">Wybierz **ExternalTemperature** w **pola danych**.</span><span class="sxs-lookup"><span data-stu-id="1acb4-157">Select **ExternalTemperature** in **Data Field**.</span></span>

5. <span data-ttu-id="1acb4-158">Ustaw **próg** do 56.</span><span class="sxs-lookup"><span data-stu-id="1acb4-158">Set **Threshold** to 56.</span></span> <span data-ttu-id="1acb4-159">Następnie kliknij przycisk **Zapisz i Wyświetl reguły**.</span><span class="sxs-lookup"><span data-stu-id="1acb4-159">Then click **Save and view rules**.</span></span>

6. <span data-ttu-id="1acb4-160">Wróć do pulpitu nawigacyjnego, aby wyświetlić historię alarm.</span><span class="sxs-lookup"><span data-stu-id="1acb4-160">Return to the dashboard to view the alarm history.</span></span>

7. <span data-ttu-id="1acb4-161">W oknie konsoli po lewej, Otwórz, uruchomić aplikację konsoli Node.js, aby rozpocząć wysyłanie **ExternalTemperature** danych telemetrycznych.</span><span class="sxs-lookup"><span data-stu-id="1acb4-161">In the console window you left open, start the Node.js console app to begin sending **ExternalTemperature** telemetry data.</span></span>

8. <span data-ttu-id="1acb4-162">Zwróć uwagę, że **historii Alarm** tabeli przedstawiono nowe alarmy po wyzwoleniu nowej reguły.</span><span class="sxs-lookup"><span data-stu-id="1acb4-162">Notice that the **Alarm History** table shows new alarms when the new rule is triggered.</span></span>
 
## <a name="additional-information"></a><span data-ttu-id="1acb4-163">Dodatkowe informacje</span><span class="sxs-lookup"><span data-stu-id="1acb4-163">Additional information</span></span>

<span data-ttu-id="1acb4-164">Zmiana operator  **>**  jest bardziej złożony i wykracza poza kroki opisane w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="1acb4-164">Changing the operator **>** is more complex and goes beyond the steps outlined in this tutorial.</span></span> <span data-ttu-id="1acb4-165">Chociaż można zmienić zadanie usługi Stream Analytics, aby użyć niezależnie od operatora Ci się podoba, odzwierciedlające operatora w portalu rozwiązania jest bardziej złożonych zadań.</span><span class="sxs-lookup"><span data-stu-id="1acb4-165">While you can change the Stream Analytics job to use whatever operator you like, reflecting that operator in the solution portal is a more complex task.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1acb4-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1acb4-166">Next steps</span></span>
<span data-ttu-id="1acb4-167">Teraz, przedstawiono sposób tworzenia reguł niestandardowych, można dowiedzieć się więcej o wstępnie skonfigurowanych rozwiązań:</span><span class="sxs-lookup"><span data-stu-id="1acb4-167">Now that you've seen how to create custom rules, you can learn more about the preconfigured solutions:</span></span>

- <span data-ttu-id="1acb4-168">[Łączenie aplikacji logiki do rozwiązania Azure IoT pakiet monitorowania zdalnego wstępnie][lnk-logic-app]</span><span class="sxs-lookup"><span data-stu-id="1acb4-168">[Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logic-app]</span></span>
- <span data-ttu-id="1acb4-169">[Urządzenia informacji metadanych do monitorowania zdalnego wstępnie skonfigurowane rozwiązanie][lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="1acb4-169">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md