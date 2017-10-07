---
title: aaaAzure pakiet IoT i Logic Apps | Dokumentacja firmy Microsoft
description: "Samouczek dotyczący toohook się tooAzure Logic Apps pakiet IoT dla procesów biznesowych."
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
ms.openlocfilehash: 6ef7311ac38f4e2ddb032cff0fb73591da5f76c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-connect-logic-app-tooyour-azure-iot-suite-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="e45be-103">Samouczek: Łączenie aplikacji logiki tooyour Azure IoT pakiet monitorowania zdalnego wstępnie skonfigurowane rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="e45be-103">Tutorial: Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution</span></span>
<span data-ttu-id="e45be-104">Witaj [pakiet IoT Microsoft Azure] [ lnk-internetofthings] zdalnego wstępnie skonfigurowane rozwiązanie monitorujące tooget doskonały sposób uruchomieniu szybko z zestawem funkcji na trasie exemplifies rozwiązania IoT.</span><span class="sxs-lookup"><span data-stu-id="e45be-104">hello [Microsoft Azure IoT Suite][lnk-internetofthings] remote monitoring preconfigured solution is a great way tooget started quickly with an end-to-end feature set that exemplifies an IoT solution.</span></span> <span data-ttu-id="e45be-105">W tym samouczku przedstawiono sposób tooadd aplikacji logiki tooyour pakiet IoT Microsoft Azure monitorowania zdalnego wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="e45be-105">This tutorial walks you through how tooadd Logic App tooyour Microsoft Azure IoT Suite remote monitoring preconfigured solution.</span></span> <span data-ttu-id="e45be-106">Te kroki pokazują, jak może potrwać jeszcze bardziej rozwiązania IoT łącząc tooa proces biznesowy.</span><span class="sxs-lookup"><span data-stu-id="e45be-106">These steps demonstrate how you can take your IoT solution even further by connecting it tooa business process.</span></span>

<span data-ttu-id="e45be-107">*Jeśli szukasz przewodnik dotyczący sposobu tooprovision monitorowania zdalnego wstępnie skonfigurowane rozwiązanie, zobacz [samouczek: rozpoczynanie pracy z rozwiązania IoT wstępnie hello][lnk-getstarted].*</span><span class="sxs-lookup"><span data-stu-id="e45be-107">*If you’re looking for a walkthrough on how tooprovision a remote monitoring preconfigured solution, see [Tutorial: Get started with hello IoT preconfigured solutions][lnk-getstarted].*</span></span>

<span data-ttu-id="e45be-108">Przed rozpoczęciem tego samouczka, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e45be-108">Before you start this tutorial, you should:</span></span>

* <span data-ttu-id="e45be-109">Monitorowania zdalnego hello należy wstępnie skonfigurowane rozwiązanie w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e45be-109">Provision hello remote monitoring preconfigured solution in your Azure subscription.</span></span>
* <span data-ttu-id="e45be-110">Utwórz tooenable konta SendGrid toosend wiadomości e-mail, które wyzwala procesów biznesowych.</span><span class="sxs-lookup"><span data-stu-id="e45be-110">Create a SendGrid account tooenable you toosend an email that triggers your business process.</span></span> <span data-ttu-id="e45be-111">Użytkownik może Załóż bezpłatne konto próbne w [SendGrid](https://sendgrid.com/) klikając **spróbuj bezpłatnie**.</span><span class="sxs-lookup"><span data-stu-id="e45be-111">You can sign up for a free trial account at [SendGrid](https://sendgrid.com/) by clicking **Try for Free**.</span></span> <span data-ttu-id="e45be-112">Po zarejestrowaniu bezpłatne konto próbne należy toocreate [klucz interfejsu API](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) w SendGrid przyznająca uprawnienia toosend poczty.</span><span class="sxs-lookup"><span data-stu-id="e45be-112">After you have registered for your free trial account, you need toocreate an [API key](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) in SendGrid that grants permissions toosend mail.</span></span> <span data-ttu-id="e45be-113">Należy ten klucz interfejsu API w dalszej części samouczka hello.</span><span class="sxs-lookup"><span data-stu-id="e45be-113">You need this API key later in hello tutorial.</span></span>

<span data-ttu-id="e45be-114">toocomplete tego samouczka, potrzebujesz programu Visual Studio 2015 lub Visual Studio 2017 toomodify hello akcji zaplecza hello wstępnie skonfigurowanego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="e45be-114">toocomplete this tutorial, you need Visual Studio 2015 or Visual Studio 2017 toomodify hello actions in hello preconfigured solution back end.</span></span>

<span data-ttu-id="e45be-115">Zakładając, że została już przydzielona zdalne monitorowanie wstępnie skonfigurowane rozwiązanie, przejdź toohello grupy zasobów dla rozwiązania w hello [portalu Azure][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="e45be-115">Assuming you’ve already provisioned your remote monitoring preconfigured solution, navigate toohello resource group for that solution in hello [Azure portal][lnk-azureportal].</span></span> <span data-ttu-id="e45be-116">Witaj grupa zasobów ma hello sama nazwa hello rozwiązania nazw można wybrać podczas obsługi administracyjnej rozwiązania monitorowania zdalnego.</span><span class="sxs-lookup"><span data-stu-id="e45be-116">hello resource group has hello same name as hello solution name you chose when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="e45be-117">W grupie zasobów hello widać hello wszystkie udostępnione zasoby platformy Azure dla rozwiązania z wyjątkiem hello aplikacji usługi Azure Active Directory, która znajduje się w hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e45be-117">In hello resource group, you can see all hello provisioned Azure resources for your solution except for hello Azure Active Directory application that you can find in hello Azure Classic Portal.</span></span> <span data-ttu-id="e45be-118">Witaj Poniższy zrzut ekranu przedstawia przykład **grupy zasobów** bloku zdalnego monitorowania wstępnie skonfigurowane rozwiązanie:</span><span class="sxs-lookup"><span data-stu-id="e45be-118">hello following screenshot shows an example **Resource group** blade for a remote monitoring preconfigured solution:</span></span>

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

<span data-ttu-id="e45be-119">toobegin, skonfiguruj hello logiki aplikacji toouse z hello wstępnie skonfigurowane rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="e45be-119">toobegin, set up hello logic app toouse with hello preconfigured solution.</span></span>

## <a name="set-up-hello-logic-app"></a><span data-ttu-id="e45be-120">Konfigurowanie hello aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="e45be-120">Set up hello Logic App</span></span>
1. <span data-ttu-id="e45be-121">Kliknij przycisk **Dodaj** u góry bloku grupy zasobów, korzystając z portalu Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="e45be-121">Click **Add** at hello top of your resource group blade in hello Azure portal.</span></span>
2. <span data-ttu-id="e45be-122">Wyszukaj **aplikacji logiki**, zaznacz go, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e45be-122">Search for **Logic App**, select it and then click **Create**.</span></span>
3. <span data-ttu-id="e45be-123">Wypełnianie hello **nazwa** i użyj hello sam **subskrypcji** i **grupy zasobów** użyto podczas przydzielania zdalnego rozwiązanie monitorowania.</span><span class="sxs-lookup"><span data-stu-id="e45be-123">Fill out hello **Name** and use hello same **Subscription** and **Resource group** that you used when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="e45be-124">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e45be-124">Click **Create**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. <span data-ttu-id="e45be-125">Po zakończeniu wdrożenia widać hello jest wyświetlana logiki aplikacji jako zasób w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="e45be-125">When your deployment completes, you can see hello Logic App is listed as a resource in your resource group.</span></span>
5. <span data-ttu-id="e45be-126">Kliknij przycisk bloku aplikacji logiki toonavigate toohello hello aplikacji logiki, wybierz hello **pustą aplikację logiki** hello tooopen szablonu **projektanta aplikacji logiki**.</span><span class="sxs-lookup"><span data-stu-id="e45be-126">Click hello Logic App toonavigate toohello Logic App blade, select hello **Blank Logic App** template tooopen hello **Logic Apps Designer**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. <span data-ttu-id="e45be-127">Wybierz **żądania**.</span><span class="sxs-lookup"><span data-stu-id="e45be-127">Select **Request**.</span></span> <span data-ttu-id="e45be-128">Ta akcja określa, czy przychodzące żądanie HTTP o określonych JSON w formacie ładunku czynności wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="e45be-128">This action specifies that an incoming HTTP request with a specific JSON formatted payload acts as a trigger.</span></span>
7. <span data-ttu-id="e45be-129">Wklej powitania po kodu na powitania żądania schematu JSON treści:</span><span class="sxs-lookup"><span data-stu-id="e45be-129">Paste hello following code into hello Request Body JSON Schema:</span></span>
   
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
   > <span data-ttu-id="e45be-130">Po zapisaniu hello aplikacji logiki, ale najpierw należy dodać akcję, możesz skopiować adres URL hello hello HTTP post.</span><span class="sxs-lookup"><span data-stu-id="e45be-130">You can copy hello URL for hello HTTP post after you save hello logic app, but first you must add an action.</span></span>
   > 
   > 
8. <span data-ttu-id="e45be-131">Kliknij przycisk **+ nowy krok** w obszarze ręczne wyzwalacz.</span><span class="sxs-lookup"><span data-stu-id="e45be-131">Click **+ New step** under your manual trigger.</span></span> <span data-ttu-id="e45be-132">Następnie kliknij przycisk **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="e45be-132">Then click **Add an action**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. <span data-ttu-id="e45be-133">Wyszukaj **SendGrid — wysyłanie wiadomości e-mail** i kliknij ją.</span><span class="sxs-lookup"><span data-stu-id="e45be-133">Search for **SendGrid - Send email** and click it.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. <span data-ttu-id="e45be-134">Wprowadź nazwę połączenia hello, takich jak **SendGridConnection**, wprowadź hello **klucz interfejsu API SendGrid** zostały utworzone podczas konfiguracji konta SendGrid i kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e45be-134">Enter a name for hello connection, such as **SendGridConnection**, enter hello **SendGrid API Key** you created when you set up your SendGrid account, and click **Create**.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. <span data-ttu-id="e45be-135">Dodaj e-mail adresy hello własnych tooboth **z** i **do** pola.</span><span class="sxs-lookup"><span data-stu-id="e45be-135">Add email addresses you own tooboth hello **From** and **To** fields.</span></span> <span data-ttu-id="e45be-136">Dodaj **zdalnego alert monitorowania [DeviceId]** toohello **podmiotu** pola.</span><span class="sxs-lookup"><span data-stu-id="e45be-136">Add **Remote monitoring alert [DeviceId]** toohello **Subject** field.</span></span> <span data-ttu-id="e45be-137">W hello **treść wiadomości E-mail** pól, Dodaj **urządzenia [DeviceId] zgłosił [measurementName] o wartości [measuredValue].**</span><span class="sxs-lookup"><span data-stu-id="e45be-137">In hello **Email Body** field, add **Device [DeviceId] has reported [measurementName] with value [measuredValue].**</span></span> <span data-ttu-id="e45be-138">Możesz dodać **[DeviceId]**, **[measurementName]**, i **[measuredValue]** , klikając w hello **można wstawić danych z poprzednich kroków**sekcji.</span><span class="sxs-lookup"><span data-stu-id="e45be-138">You can add **[DeviceId]**, **[measurementName]**, and **[measuredValue]** by clicking in hello **You can insert data from previous steps** section.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. <span data-ttu-id="e45be-139">Kliknij przycisk **zapisać** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="e45be-139">Click **Save** in hello top menu.</span></span>
13. <span data-ttu-id="e45be-140">Kliknij przycisk hello **żądania** hello wyzwalacza i skopiuj **adres URL toothis Http Post** wartość.</span><span class="sxs-lookup"><span data-stu-id="e45be-140">Click hello **Request** trigger and copy hello **Http Post toothis URL** value.</span></span> <span data-ttu-id="e45be-141">Ten adres URL jest potrzebne w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="e45be-141">You need this URL later in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="e45be-142">Aplikacje logiki włączyć toorun [wiele różnych typów akcji] [ lnk-logic-apps-actions] łącznie z działaniami w usłudze Office 365.</span><span class="sxs-lookup"><span data-stu-id="e45be-142">Logic Apps enable you toorun [many different types of action][lnk-logic-apps-actions] including actions in Office 365.</span></span> 
> 
> 

## <a name="set-up-hello-eventprocessor-web-job"></a><span data-ttu-id="e45be-143">Konfigurowanie hello EventProcessor zadanie sieci Web</span><span class="sxs-lookup"><span data-stu-id="e45be-143">Set up hello EventProcessor Web Job</span></span>
<span data-ttu-id="e45be-144">W tej sekcji można podłączyć toohello Twoje wstępnie skonfigurowane rozwiązanie tworzenia aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="e45be-144">In this section, you connect your preconfigured solution toohello Logic App you created.</span></span> <span data-ttu-id="e45be-145">toocomplete to zadanie, musisz dodać hello adresu URL tootrigger hello aplikacji logiki toohello akcję, która generowane, gdy wartość czujnik urządzenia przekracza próg.</span><span class="sxs-lookup"><span data-stu-id="e45be-145">toocomplete this task, you add hello URL tootrigger hello Logic App toohello action that fires when a device sensor value exceeds a threshold.</span></span>

1. <span data-ttu-id="e45be-146">Użyj programu git klienta tooclone hello najnowszą wersję hello [azure iot — zdalnego monitorowania repozytorium github][lnk-rmgithub].</span><span class="sxs-lookup"><span data-stu-id="e45be-146">Use your git client tooclone hello latest version of hello [azure-iot-remote-monitoring github repository][lnk-rmgithub].</span></span> <span data-ttu-id="e45be-147">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="e45be-147">For example:</span></span>
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. <span data-ttu-id="e45be-148">W programie Visual Studio Otwórz hello **RemoteMonitoring.sln** z hello lokalną kopię hello repozytorium.</span><span class="sxs-lookup"><span data-stu-id="e45be-148">In Visual Studio, open hello **RemoteMonitoring.sln** from hello local copy of hello repository.</span></span>
3. <span data-ttu-id="e45be-149">Otwórz hello **ActionRepository.cs** pliku w hello **infrastruktury\\repozytorium** folderu.</span><span class="sxs-lookup"><span data-stu-id="e45be-149">Open hello **ActionRepository.cs** file in hello **Infrastructure\\Repository** folder.</span></span>
4. <span data-ttu-id="e45be-150">Aktualizacja hello **actionIds** słownik z hello **adres URL toothis Http Post** zanotowane aplikację logiki w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e45be-150">Update hello **actionIds** dictionary with hello **Http Post toothis URL** you noted from your Logic App as follows:</span></span>
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post toothis URL>" },
        { "Raise Alarm", "<Http Post toothis URL>" }
    };
    ```
5. <span data-ttu-id="e45be-151">Zapisz zmiany hello w rozwiązaniu i zamknij Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e45be-151">Save hello changes in solution and exit Visual Studio.</span></span>

## <a name="deploy-from-hello-command-line"></a><span data-ttu-id="e45be-152">Wdrażanie z wiersza polecenia hello</span><span class="sxs-lookup"><span data-stu-id="e45be-152">Deploy from hello command line</span></span>
<span data-ttu-id="e45be-153">W tej sekcji możesz wdrożyć aktualizowaną wersję hello zdalnego monitorowania tooreplace hello wersja rozwiązania aktualnie uruchomione na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e45be-153">In this section, you deploy your updated version of hello remote monitoring solution tooreplace hello version currently running in Azure.</span></span>

1. <span data-ttu-id="e45be-154">Następujące hello [konfiguracji deweloperów] [ lnk-devsetup] instrukcje tooset Twojego środowiska do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="e45be-154">Following hello [dev set-up][lnk-devsetup] instructions tooset up your environment for deployment.</span></span>
2. <span data-ttu-id="e45be-155">Postępuj zgodnie z lokalnie, toodeploy hello [lokalnego wdrożenia] [ lnk-localdeploy] instrukcje.</span><span class="sxs-lookup"><span data-stu-id="e45be-155">toodeploy locally, follow hello [local deployment][lnk-localdeploy] instructions.</span></span>
3. <span data-ttu-id="e45be-156">toodeploy toohello w chmurze i aktualizowanie istniejącego wdrożenia chmury, wykonaj hello [wdrożenie w chmurze] [ lnk-clouddeploy] instrukcje.</span><span class="sxs-lookup"><span data-stu-id="e45be-156">toodeploy toohello cloud and update your existing cloud deployment, follow hello [cloud deployment][lnk-clouddeploy] instructions.</span></span> <span data-ttu-id="e45be-157">Użyj nazwy hello oryginalnego wdrożenia jako nazwa wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="e45be-157">Use hello name of your original deployment as hello deployment name.</span></span> <span data-ttu-id="e45be-158">Na przykład jeśli została wywołana hello oryginalnego wdrożenia **demologicapp**, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="e45be-158">For example if hello original deployment was called **demologicapp**, use hello following command:</span></span>
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   <span data-ttu-id="e45be-159">Podczas hello utworzyć skrypt będzie uruchamiany, należy upewnić się, toouse hello same konta Azure, subskrypcji, regionu i wystąpienie usługi Active Directory, używane podczas przydzielania hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="e45be-159">When hello build script runs, be sure toouse hello same Azure account, subscription, region, and Active Directory instance you used when you provisioned hello solution.</span></span>

## <a name="see-your-logic-app-in-action"></a><span data-ttu-id="e45be-160">Wyświetlanie aplikacji logiki w akcji</span><span class="sxs-lookup"><span data-stu-id="e45be-160">See your Logic App in action</span></span>
<span data-ttu-id="e45be-161">zdalne monitorowanie wstępnie skonfigurowane rozwiązanie Hello ma dwie reguły konfigurowane domyślnie podczas obsługi administracyjnej rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="e45be-161">hello remote monitoring preconfigured solution has two rules set up by default when you provision a solution.</span></span> <span data-ttu-id="e45be-162">Obie zasady są na powitania **SampleDevice001** urządzenia:</span><span class="sxs-lookup"><span data-stu-id="e45be-162">Both rules are on hello **SampleDevice001** device:</span></span>

* <span data-ttu-id="e45be-163">Temperatury > 38.00</span><span class="sxs-lookup"><span data-stu-id="e45be-163">Temperature > 38.00</span></span>
* <span data-ttu-id="e45be-164">Wilgotność > 48.00</span><span class="sxs-lookup"><span data-stu-id="e45be-164">Humidity > 48.00</span></span>

<span data-ttu-id="e45be-165">zasada temperatury Hello wyzwala hello **podnieść Alarm** akcji i hello zasada wilgotności wyzwala hello **SendMessage** akcji.</span><span class="sxs-lookup"><span data-stu-id="e45be-165">hello temperature rule triggers hello **Raise Alarm** action and hello Humidity rule triggers hello **SendMessage** action.</span></span> <span data-ttu-id="e45be-166">Zakładając, że użyto hello tego samego adresu URL dla obu hello akcje **ActionRepository** klasy z wyzwalaczy aplikacji logiki dla każdej reguły.</span><span class="sxs-lookup"><span data-stu-id="e45be-166">Assuming you used hello same URL for both actions hello **ActionRepository** class, your logic app triggers for either rule.</span></span> <span data-ttu-id="e45be-167">Obie reguły użyj toosend SendGrid toohello e-mail **do** adres ze szczegółami alertu hello.</span><span class="sxs-lookup"><span data-stu-id="e45be-167">Both rules use SendGrid toosend an email toohello **To** address with details of hello alert.</span></span>

> [!NOTE]
> <span data-ttu-id="e45be-168">tootrigger Hello aplikacji logiki będzie nadal występować, za każdym razem, gdy zostały spełnione warunki progowe hello.</span><span class="sxs-lookup"><span data-stu-id="e45be-168">hello Logic App continues tootrigger every time hello threshold is met.</span></span> <span data-ttu-id="e45be-169">tooavoid niepotrzebnych wiadomości e-mail, możesz wyłączyć reguły hello w Twoje rozwiązanie portalu lub wyłącz hello aplikacji logiki w hello [portalu Azure][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="e45be-169">tooavoid unnecessary emails, you can either disable hello rules in your solution portal or disable hello Logic App in hello [Azure portal][lnk-azureportal].</span></span>
> 
> 

<span data-ttu-id="e45be-170">Ponadto tooreceiving wiadomości e-mail, zostanie również wyświetlony po uruchomieniu hello aplikacji logiki w portalu hello:</span><span class="sxs-lookup"><span data-stu-id="e45be-170">In addition tooreceiving emails, you can also see when hello Logic App runs in hello portal:</span></span>

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a><span data-ttu-id="e45be-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e45be-171">Next steps</span></span>
<span data-ttu-id="e45be-172">Teraz, gdy proces biznesowy aplikacji logiki tooconnect hello wstępnie skonfigurowane rozwiązanie tooa była używana, można dowiedzieć się więcej o hello opcje dostosowywania hello wstępnie rozwiązań:</span><span class="sxs-lookup"><span data-stu-id="e45be-172">Now that you've used a Logic App tooconnect hello preconfigured solution tooa business process, you can learn more about hello options for customizing hello preconfigured solutions:</span></span>

* <span data-ttu-id="e45be-173">[Dynamiczne telemetrii za pomocą zdalnego wstępnie skonfigurowane rozwiązanie monitorujące hello][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="e45be-173">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="e45be-174">[Urządzenie informacji metadanych w hello zdalne monitorowanie wstępnie skonfigurowane rozwiązanie][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="e45be-174">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo]</span></span>

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
