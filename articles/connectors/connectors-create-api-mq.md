---
title: "aaaLearn jak toouse hello łącznik MQ w programie Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Podłącz tooan lokalnymi lub serwer Azure MQ z Twojej toobrowse przepływu pracy aplikacji logiki, odbierania i wysyłania wiadomości tooWebSphere MQ"
services: logic-apps
author: valthom
manager: anneta
documentationcenter: 
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 06/01/2017
ms.author: valthom; ladocs
ms.openlocfilehash: 8b36d53b457ced1a7461c229aecfcf8e4ae668a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-ibm-mq-server-from-logic-apps-using-hello-mq-connector"></a><span data-ttu-id="ee6a0-103">Łączenie z tooan IBM MQ serwera z aplikacji logiki przy użyciu łącznika MQ hello</span><span class="sxs-lookup"><span data-stu-id="ee6a0-103">Connect tooan IBM MQ server from logic apps using hello MQ connector</span></span> 

<span data-ttu-id="ee6a0-104">Microsoft Connector dla programu MQ wysyła i pobiera wiadomości przechowywanych w MQ serwera lokalnego lub na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-104">Microsoft Connector for MQ sends and retrieves messages stored in an MQ Server on-premises, or in Azure.</span></span> <span data-ttu-id="ee6a0-105">Ten łącznik obejmuje klienta MQ firmy Microsoft, który komunikuje się ze zdalnym serwerem IBM MQ w sieci TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-105">This connector includes a Microsoft MQ client that communicates with a remote IBM MQ server across a TCP/IP network.</span></span> <span data-ttu-id="ee6a0-106">Ten dokument jest łącznikiem starter przewodnik toouse hello MQ.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-106">This document is a starter guide toouse hello MQ connector.</span></span> <span data-ttu-id="ee6a0-107">Zaleca się rozpocząć przechodząc pojedynczej wiadomości w kolejce, a następnie próby hello inne akcje.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-107">We recommended you begin by browsing a single message on a queue, and then trying hello other actions.</span></span>    

<span data-ttu-id="ee6a0-108">Łącznik MQ Hello obejmuje hello następujące akcje.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-108">hello MQ connector includes hello following actions.</span></span> <span data-ttu-id="ee6a0-109">Nie ma żadnych wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-109">There are no triggers.</span></span>

-   <span data-ttu-id="ee6a0-110">Przeglądaj pojedynczą wiadomość bez usuwania wiadomości powitania od hello IBM MQ serwera</span><span class="sxs-lookup"><span data-stu-id="ee6a0-110">Browse a single message without deleting hello message from hello IBM MQ Server</span></span>
-   <span data-ttu-id="ee6a0-111">Przeglądaj komunikaty zbiorczo, bez usuwania wiadomości powitania od hello IBM MQ serwera</span><span class="sxs-lookup"><span data-stu-id="ee6a0-111">Browse a batch of messages without deleting hello messages from hello IBM MQ Server</span></span>
-   <span data-ttu-id="ee6a0-112">Pojedynczy komunikat o błędzie i Usuń wiadomości powitania od hello IBM MQ serwera</span><span class="sxs-lookup"><span data-stu-id="ee6a0-112">Receive a single message and delete hello message from hello IBM MQ Server</span></span>
-   <span data-ttu-id="ee6a0-113">Odbieranie partię komunikatów i usuwanie wiadomości powitania od hello IBM MQ serwera</span><span class="sxs-lookup"><span data-stu-id="ee6a0-113">Receive a batch of messages and delete hello messages from hello IBM MQ Server</span></span>
-   <span data-ttu-id="ee6a0-114">Wysyłanie wiadomości toohello IBM MQ serwera</span><span class="sxs-lookup"><span data-stu-id="ee6a0-114">Send a single message toohello IBM MQ Server</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ee6a0-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ee6a0-115">Prerequisites</span></span>

* <span data-ttu-id="ee6a0-116">Jeśli za pomocą lokalnego serwera MQ [instalowanie bramy danych lokalne powitania](../logic-apps/logic-apps-gateway-install.md) na serwerze w sieci.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-116">If using an on-premises MQ server, [install hello on-premises data gateway](../logic-apps/logic-apps-gateway-install.md) on a server within your network.</span></span> <span data-ttu-id="ee6a0-117">W przypadku powitania serwera MQ publicznie dostępne, lub dostępne w systemie Azure, brama danych hello jest nie używane lub wymagane.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-117">If hello MQ Server is publicly available, or available within Azure, then hello data gateway is not used or required.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ee6a0-118">Serwer Hello gdzie hello jest zainstalowana brama lokalna danych musi mieć również .net Framework 4.6 zainstalowane dla hello toofunction łącznika MQ.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-118">hello server where hello On-Premises Data Gateway is installed must also have .Net Framework 4.6 installed for hello MQ Connector toofunction.</span></span>

* <span data-ttu-id="ee6a0-119">Utwórz hello zasobów platformy Azure dla bramy danych lokalne powitania - [Konfigurowanie połączenia bramy danych hello](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="ee6a0-119">Create hello Azure resource for hello on-premises data gateway - [Set up hello data gateway connection](../logic-apps/logic-apps-gateway-connection.md).</span></span>

* <span data-ttu-id="ee6a0-120">Oficjalnie obsługiwane wersje programu IBM WebSphere MQ:</span><span class="sxs-lookup"><span data-stu-id="ee6a0-120">Officially supported IBM WebSphere MQ versions:</span></span>
   * <span data-ttu-id="ee6a0-121">MQ W WERSJI 7.5</span><span class="sxs-lookup"><span data-stu-id="ee6a0-121">MQ 7.5</span></span>
   * <span data-ttu-id="ee6a0-122">MQ 8.0</span><span class="sxs-lookup"><span data-stu-id="ee6a0-122">MQ 8.0</span></span>

## <a name="create-a-logic-app"></a><span data-ttu-id="ee6a0-123">Tworzenie aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="ee6a0-123">Create a logic app</span></span>

1. <span data-ttu-id="ee6a0-124">W hello **Azure start tablicy**, wybierz pozycję  **+**  (znak plus) **sieci Web i mobilność**, a następnie **aplikacji logiki**.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-124">In hello **Azure start board**, select **+** (plus sign), **Web + Mobile**, and then **Logic App**.</span></span> 
2. <span data-ttu-id="ee6a0-125">Wprowadź hello **nazwa**, takich jak MQTestApp, **subskrypcji**, **grupy zasobów**, i **lokalizacji** (Użyj lokalizacji hello gdzie hello połączenie bramy danych lokalnych jest skonfigurowane).</span><span class="sxs-lookup"><span data-stu-id="ee6a0-125">Enter hello **Name**, such as MQTestApp, **Subscription**, **Resource group**, and **Location** (use hello location where hello on-premises Data Gateway connection is configured).</span></span> <span data-ttu-id="ee6a0-126">Wybierz **toodashboard numeru Pin**i wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-126">Select **Pin toodashboard**, and select **Create**.</span></span>  
<span data-ttu-id="ee6a0-127">![Tworzenie aplikacji logiki](media/connectors-create-api-mq/Create_Logic_App.png)</span><span class="sxs-lookup"><span data-stu-id="ee6a0-127">![Create Logic App](media/connectors-create-api-mq/Create_Logic_App.png)</span></span>

## <a name="add-a-trigger"></a><span data-ttu-id="ee6a0-128">Dodaj wyzwalacz</span><span class="sxs-lookup"><span data-stu-id="ee6a0-128">Add a trigger</span></span>

> [!NOTE]
> <span data-ttu-id="ee6a0-129">Hello MQ łącznika nie ma żadnych wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-129">hello MQ Connector does not have any triggers.</span></span> <span data-ttu-id="ee6a0-130">Tak, użyj innego toostart wyzwalacza aplikację logiki, takich jak hello **cyklu** wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-130">So, use another trigger toostart your logic app, such as hello **Recurrence** trigger.</span></span> 

1. <span data-ttu-id="ee6a0-131">Hello **projektanta aplikacji logiki** zostanie otwarta, wybierz opcję **cyklu** liście hello wspólnej wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-131">hello **Logic Apps Designer** opens, select **Recurrence** in hello list of common triggers.</span></span>
2. <span data-ttu-id="ee6a0-132">Wybierz **Edytuj** w hello cyklu wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-132">Select **Edit** within hello Recurrence Trigger.</span></span> 
3. <span data-ttu-id="ee6a0-133">Zestaw hello **częstotliwość** zbyt**dzień**i zestaw hello **interwał** za**7**.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-133">Set hello **Frequency** too**Day**, and set hello **Interval** too**7**.</span></span> 

## <a name="browse-a-single-message"></a><span data-ttu-id="ee6a0-134">Przeglądaj w pojedynczym komunikacie</span><span class="sxs-lookup"><span data-stu-id="ee6a0-134">Browse a single message</span></span>
1. <span data-ttu-id="ee6a0-135">Wybierz **+ nowy krok**i wybierz **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-135">Select **+ New step**, and select **Add an action**.</span></span>
2. <span data-ttu-id="ee6a0-136">W polu wyszukiwania hello wpisz `mq`, a następnie wybierz **MQ - przeglądania wiadomości**.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-136">In hello search box, type `mq`, and then select **MQ - Browse message**.</span></span>  
<span data-ttu-id="ee6a0-137">![Przeglądaj wiadomości](media/connectors-create-api-mq/Browse_message.png)</span><span class="sxs-lookup"><span data-stu-id="ee6a0-137">![Browse message](media/connectors-create-api-mq/Browse_message.png)</span></span>

3. <span data-ttu-id="ee6a0-138">Jeśli nie ma istniejącego połączenia MQ, należy utworzyć połączenie hello:</span><span class="sxs-lookup"><span data-stu-id="ee6a0-138">If there isn't an existing MQ connection, then create hello connection:</span></span>  

    1. <span data-ttu-id="ee6a0-139">Wybierz **Połącz za pośrednictwem bramy danych lokalnych**, a następnie wprowadź właściwości powitania serwera MQ.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-139">Select **Connect via on-premises data gateway**, and enter hello properties of your MQ server.</span></span>  
    <span data-ttu-id="ee6a0-140">Aby uzyskać **serwera**, wprowadź nazwę serwera MQ hello, lub wprowadź adres IP hello następuje dwukropek i hello numer portu.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-140">For **Server**, you can enter hello MQ server name, or enter hello IP address followed by a colon and hello port number.</span></span> 
    2. <span data-ttu-id="ee6a0-141">Witaj **bramy** lista rozwijana zawiera listę istniejących połączeń bramy, które zostały skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-141">hello **gateway** dropdown lists any existing gateway connections that have been configured.</span></span> <span data-ttu-id="ee6a0-142">Wybierz bramę.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-142">Select your gateway.</span></span>
    3. <span data-ttu-id="ee6a0-143">Wybierz **Utwórz** po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-143">Select **Create** when finished.</span></span> <span data-ttu-id="ee6a0-144">Połączenie wygląda podobnie toohello następujące:</span><span class="sxs-lookup"><span data-stu-id="ee6a0-144">Your connection looks similar toohello following:</span></span>   
    <span data-ttu-id="ee6a0-145">![Właściwości połączenia](media/connectors-create-api-mq/Connection_Properties.png)</span><span class="sxs-lookup"><span data-stu-id="ee6a0-145">![Connection Properties](media/connectors-create-api-mq/Connection_Properties.png)</span></span>

4. <span data-ttu-id="ee6a0-146">W oknie dialogowym właściwości akcji hello można:</span><span class="sxs-lookup"><span data-stu-id="ee6a0-146">In hello action properties, you can:</span></span>  

    * <span data-ttu-id="ee6a0-147">Użyj hello **kolejki** właściwości tooaccess nazwę kolejki innego niż zdefiniowana w hello połączenia</span><span class="sxs-lookup"><span data-stu-id="ee6a0-147">Use hello **Queue** property tooaccess a different queue name than what is defined in hello connection</span></span>
    * <span data-ttu-id="ee6a0-148">Użyj hello **MessageId**, **CorrelationId**, **GroupId**i inne właściwości toobrowse wiadomości oparte na różne właściwości MQ wiadomość hello</span><span class="sxs-lookup"><span data-stu-id="ee6a0-148">Use hello **MessageId**, **CorrelationId**, **GroupId**, and other properties toobrowse for a message based on hello different MQ message properties</span></span>
    * <span data-ttu-id="ee6a0-149">Ustaw **IncludeInfo** za**True** tooinclude komunikat dodatkowych informacji w danych wyjściowych hello.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-149">Set **IncludeInfo** too**True** tooinclude additional message information in hello output.</span></span> <span data-ttu-id="ee6a0-150">Lub ustaw ją za**False** toonot zawierają informacje dodatkowe wiadomość hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-150">Or, set it too**False** toonot include additional message information in hello output.</span></span>
    * <span data-ttu-id="ee6a0-151">Wprowadź **limitu czasu** toodetermine wartość jak długo toowait dla tooarrive wiadomości w pustej kolejce.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-151">Enter a **Timeout** value toodetermine how long toowait for a message tooarrive in an empty queue.</span></span> <span data-ttu-id="ee6a0-152">Jeśli nic nie zostanie wprowadzona, hello pierwszej wiadomości w kolejce hello są pobierane i nie ma żadnych czas oczekiwania na tooappear wiadomości.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-152">If nothing is entered, hello first message in hello queue is retrieved, and there is no time spent waiting for a message tooappear.</span></span>  
    <span data-ttu-id="ee6a0-153">![Przeglądaj właściwości wiadomości](media/connectors-create-api-mq/Browse_message_Props.png)</span><span class="sxs-lookup"><span data-stu-id="ee6a0-153">![Browse Message Properties](media/connectors-create-api-mq/Browse_message_Props.png)</span></span>

5. <span data-ttu-id="ee6a0-154">**Zapisz** zmiany, a następnie **Uruchom** aplikację logiki:</span><span class="sxs-lookup"><span data-stu-id="ee6a0-154">**Save** your changes, and then **Run** your logic app:</span></span>  
<span data-ttu-id="ee6a0-155">![Zapisz i uruchom](media/connectors-create-api-mq/Save_Run.png)</span><span class="sxs-lookup"><span data-stu-id="ee6a0-155">![Save and run](media/connectors-create-api-mq/Save_Run.png)</span></span>

6. <span data-ttu-id="ee6a0-156">Po kilku sekundach przedstawiono kroki hello hello Uruchom, a można przyjrzeć się hello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-156">After a few seconds, hello steps of hello run are shown, and you can look at hello output.</span></span> <span data-ttu-id="ee6a0-157">Wybierz hello zielonym znacznikiem wyboru toosee szczegóły każdego kroku.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-157">Select hello green checkmark toosee details of each step.</span></span> <span data-ttu-id="ee6a0-158">Wybierz **Zobacz nieprzetworzone dane wyjściowe** toosee dodatkowe szczegóły dotyczące hello dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-158">Select **See raw outputs** toosee additional details on hello output data.</span></span>  
<span data-ttu-id="ee6a0-159">![Przeglądaj dane wyjściowe komunikatu](media/connectors-create-api-mq/Browse_message_output.png)</span><span class="sxs-lookup"><span data-stu-id="ee6a0-159">![Browse message output](media/connectors-create-api-mq/Browse_message_output.png)</span></span>  

    <span data-ttu-id="ee6a0-160">Nieprzetworzone dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="ee6a0-160">Raw output:</span></span>  
    ![Przeglądaj nieprzetworzone dane wyjściowe komunikatu](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. <span data-ttu-id="ee6a0-162">Gdy hello **IncludeInfo** wartość tootrue, zostanie wyświetlony hello następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="ee6a0-162">When hello **IncludeInfo** option is set tootrue, hello following output is displayed:</span></span>  
<span data-ttu-id="ee6a0-163">![Przeglądaj wiadomości zawierają informacje o](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span><span class="sxs-lookup"><span data-stu-id="ee6a0-163">![Browse message include info](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span></span>

## <a name="browse-multiple-messages"></a><span data-ttu-id="ee6a0-164">Przeglądaj wiele komunikatów</span><span class="sxs-lookup"><span data-stu-id="ee6a0-164">Browse multiple messages</span></span>
<span data-ttu-id="ee6a0-165">Witaj **Przeglądaj wiadomości** akcja zawiera **BatchSize** tooindicate opcji powinny być zwracane ile komunikatów z kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-165">hello **Browse messages** action includes a **BatchSize** option tooindicate how many messages should be returned from hello queue.</span></span>  <span data-ttu-id="ee6a0-166">Jeśli **BatchSize** nie ma wpisu, zwracane są wszystkie komunikaty.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-166">If **BatchSize** has no entry, all messages are returned.</span></span> <span data-ttu-id="ee6a0-167">Witaj zwracany wyjściem jest tablica komunikatów.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-167">hello returned output is an array of messages.</span></span>

1. <span data-ttu-id="ee6a0-168">Podczas dodawania hello **Przeglądaj wiadomości** akcji, hello pierwszego połączenia, który jest skonfigurowany jest domyślnie zaznaczona.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-168">When adding hello **Browse messages** action, hello first connection that is configured is selected by default.</span></span> <span data-ttu-id="ee6a0-169">Wybierz **zmienić połączenie** toocreate nowe połączenie, lub wybierz inne połączenie.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-169">Select **Change connection** toocreate a new connection, or select a different connection.</span></span>

2. <span data-ttu-id="ee6a0-170">dane wyjściowe Hello przeglądania wiadomości pokazuje:</span><span class="sxs-lookup"><span data-stu-id="ee6a0-170">hello output of Browse messages shows:</span></span>  
![Przeglądaj wiadomości w danych wyjściowych](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a><span data-ttu-id="ee6a0-172">Pojedynczy komunikat o błędzie</span><span class="sxs-lookup"><span data-stu-id="ee6a0-172">Receive a single message</span></span>
<span data-ttu-id="ee6a0-173">Witaj **odbieranie wiadomości** akcji ma hello tego samego wejściami i wyjściami jako hello **przeglądania wiadomości** akcji.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-173">hello **Receive message** action has hello same inputs and outputs as hello **Browse message** action.</span></span> <span data-ttu-id="ee6a0-174">Korzystając z **odbieranie wiadomości**, wiadomość hello jest usuwane z kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-174">When using **Receive message**, hello message is deleted from hello queue.</span></span>

## <a name="receive-multiple-messages"></a><span data-ttu-id="ee6a0-175">Wiele komunikaty</span><span class="sxs-lookup"><span data-stu-id="ee6a0-175">Receive multiple messages</span></span>
<span data-ttu-id="ee6a0-176">Hello **komunikaty** akcji ma hello tego samego wejściami i wyjściami jako hello **Przeglądaj wiadomości** akcji.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-176">hello **Receive messages** action has hello same inputs and outputs as hello **Browse messages** action.</span></span> <span data-ttu-id="ee6a0-177">Korzystając z **komunikaty**, wiadomości powitania są usuwane z kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-177">When using **Receive messages**, hello messages are deleted from hello queue.</span></span>

<span data-ttu-id="ee6a0-178">Jeśli w nie ma żadnych wiadomości powitania kolejki podczas przeglądania lub receive, krok hello kończy się niepowodzeniem z hello następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="ee6a0-178">If there are no messages in hello queue when doing a browse or a receive, hello step fails with hello following output:</span></span>  
![Błąd wiadomości nie MQ](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a><span data-ttu-id="ee6a0-180">Wysyłanie komunikatu</span><span class="sxs-lookup"><span data-stu-id="ee6a0-180">Send a message</span></span>
1. <span data-ttu-id="ee6a0-181">Podczas dodawania hello **wysyła komunikat** akcji, hello pierwszego połączenia, który jest skonfigurowany jest domyślnie zaznaczona.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-181">When adding hello **Send message** action, hello first connection that is configured is selected by default.</span></span> <span data-ttu-id="ee6a0-182">Wybierz **zmienić połączenie** toocreate nowe połączenie, lub wybierz inne połączenie.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-182">Select **Change connection** toocreate a new connection, or select a different connection.</span></span> <span data-ttu-id="ee6a0-183">Nieprawidłowa Hello **typów komunikatów** są **Datagram**, **odpowiedzi**, lub **żądania**.</span><span class="sxs-lookup"><span data-stu-id="ee6a0-183">hello valid **Message Types** are **Datagram**, **Reply**, or **Request**.</span></span>  
<span data-ttu-id="ee6a0-184">![Wyślij Msg właściwości](media/connectors-create-api-mq/Send_Msg_Props.png)</span><span class="sxs-lookup"><span data-stu-id="ee6a0-184">![Send Msg Props](media/connectors-create-api-mq/Send_Msg_Props.png)</span></span>

2. <span data-ttu-id="ee6a0-185">Witaj dane wyjściowe wysyła komunikat wygląda hello:</span><span class="sxs-lookup"><span data-stu-id="ee6a0-185">hello output of Send message looks like hello following:</span></span>  
![Wyślij dane wyjściowe Msg](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a><span data-ttu-id="ee6a0-187">Szczegóły dotyczące łącznika</span><span class="sxs-lookup"><span data-stu-id="ee6a0-187">Connector-specific details</span></span>

<span data-ttu-id="ee6a0-188">Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/mq/).</span><span class="sxs-lookup"><span data-stu-id="ee6a0-188">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/mq/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee6a0-189">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ee6a0-189">Next steps</span></span>
<span data-ttu-id="ee6a0-190">[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ee6a0-190">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="ee6a0-191">Eksploruj hello innych dostępnych łączników w aplikacjach logiki w naszym [listy interfejsów API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="ee6a0-191">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
