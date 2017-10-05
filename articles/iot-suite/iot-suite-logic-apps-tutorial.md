---
title: Pakiet Azure IoT i Logic Apps | Dokumentacja firmy Microsoft
description: "Samouczek dotyczący sposobu podłączanie aplikacji logiki, aby pakiet IoT Azure dla procesu biznesowego."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4629a7af-56ca-4b21-a769-5fa18bc3ab07
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: corywink
ms.openlocfilehash: 2e7997e2a8bdeeec6083d40acb55e653f87e140b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-connect-logic-app-to-your-azure-iot-suite-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="33b2d-103">Samouczek: Łączenie aplikacji logiki do rozwiązania Azure IoT pakiet monitorowania zdalnego wstępnie</span><span class="sxs-lookup"><span data-stu-id="33b2d-103">Tutorial: Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution</span></span>
<span data-ttu-id="33b2d-104">[Pakiet IoT Microsoft Azure] [ lnk-internetofthings] zdalnego wstępnie skonfigurowane rozwiązanie monitorujące, jest to dobry sposób na szybkie rozpoczęcie pracy z zestawem funkcji na trasie exemplifies rozwiązania IoT.</span><span class="sxs-lookup"><span data-stu-id="33b2d-104">The [Microsoft Azure IoT Suite][lnk-internetofthings] remote monitoring preconfigured solution is a great way to get started quickly with an end-to-end feature set that exemplifies an IoT solution.</span></span> <span data-ttu-id="33b2d-105">W tym samouczku przedstawiono sposób dodawania aplikacji logiki do firmy Microsoft Azure IoT pakietu zdalne monitorowanie wstępnie skonfigurowanych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="33b2d-105">This tutorial walks you through how to add Logic App to your Microsoft Azure IoT Suite remote monitoring preconfigured solution.</span></span> <span data-ttu-id="33b2d-106">Te kroki pokazują, jak może potrwać jeszcze bardziej rozwiązania IoT, łącząc go z procesu biznesowego.</span><span class="sxs-lookup"><span data-stu-id="33b2d-106">These steps demonstrate how you can take your IoT solution even further by connecting it to a business process.</span></span>

<span data-ttu-id="33b2d-107">*Jeśli szukasz wskazówki na temat sposobu monitorowania zdalnego wstępnie skonfigurowane rozwiązanie udostępniania, zobacz [samouczek: rozpoczynanie pracy z rozwiązania IoT wstępnie][lnk-getstarted].*</span><span class="sxs-lookup"><span data-stu-id="33b2d-107">*If you’re looking for a walkthrough on how to provision a remote monitoring preconfigured solution, see [Tutorial: Get started with the IoT preconfigured solutions][lnk-getstarted].*</span></span>

<span data-ttu-id="33b2d-108">Przed rozpoczęciem tego samouczka, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="33b2d-108">Before you start this tutorial, you should:</span></span>

* <span data-ttu-id="33b2d-109">Monitorowania zdalnego należy wstępnie skonfigurowane rozwiązanie w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="33b2d-109">Provision the remote monitoring preconfigured solution in your Azure subscription.</span></span>
* <span data-ttu-id="33b2d-110">Utwórz konto SendGrid umożliwia wysłanie wiadomości e-mail, które wyzwala procesów biznesowych.</span><span class="sxs-lookup"><span data-stu-id="33b2d-110">Create a SendGrid account to enable you to send an email that triggers your business process.</span></span> <span data-ttu-id="33b2d-111">Użytkownik może Załóż bezpłatne konto próbne w [SendGrid](https://sendgrid.com/) klikając **spróbuj bezpłatnie**.</span><span class="sxs-lookup"><span data-stu-id="33b2d-111">You can sign up for a free trial account at [SendGrid](https://sendgrid.com/) by clicking **Try for Free**.</span></span> <span data-ttu-id="33b2d-112">Po zarejestrowaniu bezpłatne konto próbne, musisz utworzyć [klucz interfejsu API](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) w SendGrid, który przyznaje uprawnienia do wysyłania wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="33b2d-112">After you have registered for your free trial account, you need to create an [API key](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) in SendGrid that grants permissions to send mail.</span></span> <span data-ttu-id="33b2d-113">Należy ten klucz interfejsu API w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="33b2d-113">You need this API key later in the tutorial.</span></span>

<span data-ttu-id="33b2d-114">Do ukończenia tego samouczka, potrzebujesz programu Visual Studio 2015 lub Visual Studio 2017 r, aby zmodyfikować akcje w wewnętrznej wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="33b2d-114">To complete this tutorial, you need Visual Studio 2015 or Visual Studio 2017 to modify the actions in the preconfigured solution back end.</span></span>

<span data-ttu-id="33b2d-115">Zakładając, że została już przydzielona zdalne monitorowanie wstępnie skonfigurowane rozwiązanie, przejdź do grupy zasobów dla rozwiązania w [portalu Azure][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="33b2d-115">Assuming you’ve already provisioned your remote monitoring preconfigured solution, navigate to the resource group for that solution in the [Azure portal][lnk-azureportal].</span></span> <span data-ttu-id="33b2d-116">Grupa zasobów ma taką samą nazwę jak nazwa rozwiązania została wybrana opcja podczas obsługi administracyjnej zdalnego rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="33b2d-116">The resource group has the same name as the solution name you chose when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="33b2d-117">W grupie zasobów zostaną wyświetlone wszystkie aprowizowane zasoby platformy Azure rozwiązania z wyjątkiem aplikacji usługi Azure Active Directory, który można znaleźć w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="33b2d-117">In the resource group, you can see all the provisioned Azure resources for your solution except for the Azure Active Directory application that you can find in the Azure Classic Portal.</span></span> <span data-ttu-id="33b2d-118">Poniższy zrzut ekranu przedstawia przykład **grupy zasobów** bloku zdalnego monitorowania wstępnie skonfigurowane rozwiązanie:</span><span class="sxs-lookup"><span data-stu-id="33b2d-118">The following screenshot shows an example **Resource group** blade for a remote monitoring preconfigured solution:</span></span>

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

<span data-ttu-id="33b2d-119">Aby rozpocząć, skonfigurować aplikację logiki, do korzystania z wstępnie skonfigurowanych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="33b2d-119">To begin, set up the logic app to use with the preconfigured solution.</span></span>

## <a name="set-up-the-logic-app"></a><span data-ttu-id="33b2d-120">Konfigurowanie aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="33b2d-120">Set up the Logic App</span></span>
1. <span data-ttu-id="33b2d-121">Kliknij przycisk **Dodaj** w górnej części bloku grupy zasobów, korzystając z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="33b2d-121">Click **Add** at the top of your resource group blade in the Azure portal.</span></span>
2. <span data-ttu-id="33b2d-122">Wyszukaj **aplikacji logiki**, zaznacz go, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="33b2d-122">Search for **Logic App**, select it and then click **Create**.</span></span>
3. <span data-ttu-id="33b2d-123">Wypełnianie **nazwa** i używać tego samego **subskrypcji** i **grupy zasobów** użyto podczas przydzielania zdalnego rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="33b2d-123">Fill out the **Name** and use the same **Subscription** and **Resource group** that you used when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="33b2d-124">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="33b2d-124">Click **Create**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. <span data-ttu-id="33b2d-125">Po zakończeniu wdrożenia, można zauważyć, że aplikację logiki jest wymieniony jako zasób w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="33b2d-125">When your deployment completes, you can see the Logic App is listed as a resource in your resource group.</span></span>
5. <span data-ttu-id="33b2d-126">Kliknij aplikację logiki, aby przejść do bloku aplikacji logiki, wybierz opcję **pustą aplikację logiki** szablonu, aby otworzyć **projektanta aplikacji logiki**.</span><span class="sxs-lookup"><span data-stu-id="33b2d-126">Click the Logic App to navigate to the Logic App blade, select the **Blank Logic App** template to open the **Logic Apps Designer**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. <span data-ttu-id="33b2d-127">Wybierz **żądania**.</span><span class="sxs-lookup"><span data-stu-id="33b2d-127">Select **Request**.</span></span> <span data-ttu-id="33b2d-128">Ta akcja określa, czy przychodzące żądanie HTTP o określonych JSON w formacie ładunku czynności wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="33b2d-128">This action specifies that an incoming HTTP request with a specific JSON formatted payload acts as a trigger.</span></span>
7. <span data-ttu-id="33b2d-129">Wklej następujący kod do schematu JSON treści żądania:</span><span class="sxs-lookup"><span data-stu-id="33b2d-129">Paste the following code into the Request Body JSON Schema:</span></span>
   
    ```json
    {
      "$schema": "http://json-schema.org/draft-04/schema#",
      "id": "/",
      "properties": {
        "DeviceId": {
          "id": "DeviceId",
          "type": "string"
        },
        "measuredValue": {
          "id": "measuredValue",
          "type": "integer"
        },
        "measurementName": {
          "id": "measurementName",
          "type": "string"
        }
      },
      "required": [
        "DeviceId",
        "measurementName",
        "measuredValue"
      ],
      "type": "object"
    }
    ```
   
   > [!NOTE]
   > <span data-ttu-id="33b2d-130">Po zapisaniu aplikację logiki, ale najpierw należy dodać akcję, możesz skopiować adres URL HTTP post.</span><span class="sxs-lookup"><span data-stu-id="33b2d-130">You can copy the URL for the HTTP post after you save the logic app, but first you must add an action.</span></span>
   > 
   > 
8. <span data-ttu-id="33b2d-131">Kliknij przycisk **+ nowy krok** w obszarze ręczne wyzwalacz.</span><span class="sxs-lookup"><span data-stu-id="33b2d-131">Click **+ New step** under your manual trigger.</span></span> <span data-ttu-id="33b2d-132">Następnie kliknij przycisk **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="33b2d-132">Then click **Add an action**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. <span data-ttu-id="33b2d-133">Wyszukaj **SendGrid — wysyłanie wiadomości e-mail** i kliknij ją.</span><span class="sxs-lookup"><span data-stu-id="33b2d-133">Search for **SendGrid - Send email** and click it.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. <span data-ttu-id="33b2d-134">Wprowadź nazwę połączenia, na przykład **SendGridConnection**, wprowadź **klucz interfejsu API SendGrid** zostały utworzone podczas konfiguracji konta SendGrid i kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="33b2d-134">Enter a name for the connection, such as **SendGridConnection**, enter the **SendGrid API Key** you created when you set up your SendGrid account, and click **Create**.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. <span data-ttu-id="33b2d-135">Dodaj adresy e-mail, musisz być właścicielem zarówno do **z** i **do** pola.</span><span class="sxs-lookup"><span data-stu-id="33b2d-135">Add email addresses you own to both the **From** and **To** fields.</span></span> <span data-ttu-id="33b2d-136">Dodaj **zdalnego alert monitorowania [DeviceId]** do **podmiotu** pola.</span><span class="sxs-lookup"><span data-stu-id="33b2d-136">Add **Remote monitoring alert [DeviceId]** to the **Subject** field.</span></span> <span data-ttu-id="33b2d-137">W **treść wiadomości E-mail** pól, Dodaj **urządzenia [DeviceId] zgłosił [measurementName] o wartości [measuredValue].**</span><span class="sxs-lookup"><span data-stu-id="33b2d-137">In the **Email Body** field, add **Device [DeviceId] has reported [measurementName] with value [measuredValue].**</span></span> <span data-ttu-id="33b2d-138">Możesz dodać **[DeviceId]**, **[measurementName]**, i **[measuredValue]** , klikając w **można wstawić danych z poprzednich kroków** sekcja.</span><span class="sxs-lookup"><span data-stu-id="33b2d-138">You can add **[DeviceId]**, **[measurementName]**, and **[measuredValue]** by clicking in the **You can insert data from previous steps** section.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. <span data-ttu-id="33b2d-139">Kliknij przycisk **zapisać** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="33b2d-139">Click **Save** in the top menu.</span></span>
13. <span data-ttu-id="33b2d-140">Kliknij przycisk **żądania** wyzwalacza i skopiuj **Http Post do tego adresu URL** wartość.</span><span class="sxs-lookup"><span data-stu-id="33b2d-140">Click the **Request** trigger and copy the **Http Post to this URL** value.</span></span> <span data-ttu-id="33b2d-141">Ten adres URL jest potrzebne w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="33b2d-141">You need this URL later in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="33b2d-142">Aplikacje logiki umożliwiają uruchamianie [wiele różnych typów akcji] [ lnk-logic-apps-actions] łącznie z działaniami w usłudze Office 365.</span><span class="sxs-lookup"><span data-stu-id="33b2d-142">Logic Apps enable you to run [many different types of action][lnk-logic-apps-actions] including actions in Office 365.</span></span> 
> 
> 

## <a name="set-up-the-eventprocessor-web-job"></a><span data-ttu-id="33b2d-143">Konfigurowanie EventProcessor zadanie sieci Web</span><span class="sxs-lookup"><span data-stu-id="33b2d-143">Set up the EventProcessor Web Job</span></span>
<span data-ttu-id="33b2d-144">W tej sekcji łączysz wstępnie skonfigurowanego rozwiązania do tworzenia aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="33b2d-144">In this section, you connect your preconfigured solution to the Logic App you created.</span></span> <span data-ttu-id="33b2d-145">Aby wykonać to zadanie, należy dodać adres URL do aplikacji logiki do akcji, która generowane, gdy wartość czujnik urządzenia przekracza próg wyzwolenia.</span><span class="sxs-lookup"><span data-stu-id="33b2d-145">To complete this task, you add the URL to trigger the Logic App to the action that fires when a device sensor value exceeds a threshold.</span></span>

1. <span data-ttu-id="33b2d-146">Klonowanie najnowszej wersji za pomocą klienta programu git [azure iot — zdalnego monitorowania repozytorium github][lnk-rmgithub].</span><span class="sxs-lookup"><span data-stu-id="33b2d-146">Use your git client to clone the latest version of the [azure-iot-remote-monitoring github repository][lnk-rmgithub].</span></span> <span data-ttu-id="33b2d-147">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="33b2d-147">For example:</span></span>
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. <span data-ttu-id="33b2d-148">W programie Visual Studio Otwórz **RemoteMonitoring.sln** z lokalną kopię repozytorium.</span><span class="sxs-lookup"><span data-stu-id="33b2d-148">In Visual Studio, open the **RemoteMonitoring.sln** from the local copy of the repository.</span></span>
3. <span data-ttu-id="33b2d-149">Otwórz **ActionRepository.cs** w pliku **infrastruktury\\repozytorium** folderu.</span><span class="sxs-lookup"><span data-stu-id="33b2d-149">Open the **ActionRepository.cs** file in the **Infrastructure\\Repository** folder.</span></span>
4. <span data-ttu-id="33b2d-150">Aktualizacja **actionIds** słownik z **Http Post do tego adresu URL** zanotowane aplikację logiki w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="33b2d-150">Update the **actionIds** dictionary with the **Http Post to this URL** you noted from your Logic App as follows:</span></span>
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post to this URL>" },
        { "Raise Alarm", "<Http Post to this URL>" }
    };
    ```
5. <span data-ttu-id="33b2d-151">Zapisz zmiany w rozwiązaniu i zamknij Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="33b2d-151">Save the changes in solution and exit Visual Studio.</span></span>

## <a name="deploy-from-the-command-line"></a><span data-ttu-id="33b2d-152">Wdrażanie z wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="33b2d-152">Deploy from the command line</span></span>
<span data-ttu-id="33b2d-153">W tej sekcji możesz wdrożyć aktualizowaną wersję zdalnego rozwiązanie monitorowania, aby zamienić wersję aktualnie uruchomione na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="33b2d-153">In this section, you deploy your updated version of the remote monitoring solution to replace the version currently running in Azure.</span></span>

1. <span data-ttu-id="33b2d-154">Po [konfiguracji deweloperów] [ lnk-devsetup] instrukcje dotyczące konfigurowania środowiska do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="33b2d-154">Following the [dev set-up][lnk-devsetup] instructions to set up your environment for deployment.</span></span>
2. <span data-ttu-id="33b2d-155">Aby wdrożyć lokalnie, wykonaj [lokalnego wdrożenia] [ lnk-localdeploy] instrukcje.</span><span class="sxs-lookup"><span data-stu-id="33b2d-155">To deploy locally, follow the [local deployment][lnk-localdeploy] instructions.</span></span>
3. <span data-ttu-id="33b2d-156">Aby wdrażać w chmurze i zaktualizować istniejące wdrożenia chmury, wykonaj [wdrożenie w chmurze] [ lnk-clouddeploy] instrukcje.</span><span class="sxs-lookup"><span data-stu-id="33b2d-156">To deploy to the cloud and update your existing cloud deployment, follow the [cloud deployment][lnk-clouddeploy] instructions.</span></span> <span data-ttu-id="33b2d-157">Użyj nazwy oryginalnego wdrożenia jako nazwa wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="33b2d-157">Use the name of your original deployment as the deployment name.</span></span> <span data-ttu-id="33b2d-158">Na przykład jeśli została wywołana oryginalnego wdrożenia **demologicapp**, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="33b2d-158">For example if the original deployment was called **demologicapp**, use the following command:</span></span>
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   <span data-ttu-id="33b2d-159">Po uruchomieniu skryptu kompilacji, należy użyć tego samego konta platformy Azure, subskrypcji, regionu i wystąpieniem usługi Active Directory, które jest używane podczas przydzielania rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="33b2d-159">When the build script runs, be sure to use the same Azure account, subscription, region, and Active Directory instance you used when you provisioned the solution.</span></span>

## <a name="see-your-logic-app-in-action"></a><span data-ttu-id="33b2d-160">Wyświetlanie aplikacji logiki w akcji</span><span class="sxs-lookup"><span data-stu-id="33b2d-160">See your Logic App in action</span></span>
<span data-ttu-id="33b2d-161">Zdalny wstępnie skonfigurowane rozwiązanie monitorowania ma dwie reguły konfigurowane domyślnie podczas obsługi administracyjnej rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="33b2d-161">The remote monitoring preconfigured solution has two rules set up by default when you provision a solution.</span></span> <span data-ttu-id="33b2d-162">Obie zasady są na **SampleDevice001** urządzenia:</span><span class="sxs-lookup"><span data-stu-id="33b2d-162">Both rules are on the **SampleDevice001** device:</span></span>

* <span data-ttu-id="33b2d-163">Temperatury > 38.00</span><span class="sxs-lookup"><span data-stu-id="33b2d-163">Temperature > 38.00</span></span>
* <span data-ttu-id="33b2d-164">Wilgotność > 48.00</span><span class="sxs-lookup"><span data-stu-id="33b2d-164">Humidity > 48.00</span></span>

<span data-ttu-id="33b2d-165">Wyzwalacze Reguły temperatury **podnieść Alarm** akcji i wilgotność reguły wyzwalaczy **SendMessage** akcji.</span><span class="sxs-lookup"><span data-stu-id="33b2d-165">The temperature rule triggers the **Raise Alarm** action and the Humidity rule triggers the **SendMessage** action.</span></span> <span data-ttu-id="33b2d-166">Zakładając, że używasz tego samego adresu URL dla obu akcje **ActionRepository** klasy z wyzwalaczy aplikacji logiki dla każdej reguły.</span><span class="sxs-lookup"><span data-stu-id="33b2d-166">Assuming you used the same URL for both actions the **ActionRepository** class, your logic app triggers for either rule.</span></span> <span data-ttu-id="33b2d-167">Obie reguły umożliwia wysłanie wiadomości e-mail do SendGrid **do** adres ze szczegółami alertu.</span><span class="sxs-lookup"><span data-stu-id="33b2d-167">Both rules use SendGrid to send an email to the **To** address with details of the alert.</span></span>

> [!NOTE]
> <span data-ttu-id="33b2d-168">Aplikację logiki w dalszym ciągu wyzwolenia za każdym razem, ze osiągnięty jest próg.</span><span class="sxs-lookup"><span data-stu-id="33b2d-168">The Logic App continues to trigger every time the threshold is met.</span></span> <span data-ttu-id="33b2d-169">Aby uniknąć niepotrzebnych wiadomości e-mail, można wyłączyć reguły w portalu rozwiązania lub wyłączyć aplikację logiki w [portalu Azure][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="33b2d-169">To avoid unnecessary emails, you can either disable the rules in your solution portal or disable the Logic App in the [Azure portal][lnk-azureportal].</span></span>
> 
> 

<span data-ttu-id="33b2d-170">Oprócz odbierania wiadomości e-mail, zostanie również wyświetlony po uruchomieniu aplikacji logiki w portalu:</span><span class="sxs-lookup"><span data-stu-id="33b2d-170">In addition to receiving emails, you can also see when the Logic App runs in the portal:</span></span>

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a><span data-ttu-id="33b2d-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="33b2d-171">Next steps</span></span>
<span data-ttu-id="33b2d-172">Teraz, gdy aplikacja logiki już używane do połączenia z wstępnie skonfigurowane rozwiązanie proces biznesowy, użytkownik może dowiedzieć się więcej o opcje dostosowywania wstępnie skonfigurowanych rozwiązań:</span><span class="sxs-lookup"><span data-stu-id="33b2d-172">Now that you've used a Logic App to connect the preconfigured solution to a business process, you can learn more about the options for customizing the preconfigured solutions:</span></span>

* <span data-ttu-id="33b2d-173">[Dynamiczne telemetrii za pomocą zdalnego wstępnie skonfigurowane rozwiązanie monitorowania][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="33b2d-173">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="33b2d-174">[Urządzenie informacji metadanych w zdalnym wstępnie skonfigurowane rozwiązanie monitorowania][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="33b2d-174">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo]</span></span>

[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk-internetofthings]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-getstarted]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-azureportal]: https://portal.azure.com
[lnk-logic-apps-actions]: ../connectors/apis-list.md
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-devsetup]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/dev-setup.md
[lnk-localdeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/local-deployment.md
[lnk-clouddeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
