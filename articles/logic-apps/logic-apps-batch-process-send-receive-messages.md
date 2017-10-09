---
title: "aaaBatch przetwarzania komunikatów przez grupę lub kolekcji — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Wysyłanie i odbieranie wiadomości dla przetwarzania wsadowego w aplikacji logiki"
keywords: partii, przetwarzanie wsadowe
author: jonfancey
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/7/2017
ms.author: LADocs; estfan; jonfan
ms.openlocfilehash: 2603db71ee0659d5b6bf5ce3d32f1b0d13c34194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="send-receive-and-batch-process-messages-in-logic-apps"></a><span data-ttu-id="978b1-104">Wyślij, odbierania i partii przetwarzania komunikatów w aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="978b1-104">Send, receive, and batch process messages in logic apps</span></span>

<span data-ttu-id="978b1-105">komunikaty tooprocess razem w grupach, możesz wysłać tooa danych zapasów lub komunikatów, *partii*, a następnie przetwarzania tych elementów jako plik wsadowy.</span><span class="sxs-lookup"><span data-stu-id="978b1-105">tooprocess messages together in groups, you can send data items, or messages, tooa *batch*, and then process those items as a batch.</span></span> <span data-ttu-id="978b1-106">Takie rozwiązanie jest przydatne, jeśli chcesz toomake się, że elementy danych są grupowane w szczególny sposób i wspólnego przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="978b1-106">This approach is useful when you want toomake sure data items are grouped in a specific way and are processed together.</span></span> 

<span data-ttu-id="978b1-107">Można tworzyć aplikacje logiki, które odbierają elementów jako plik wsadowy przy użyciu hello **partii** wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="978b1-107">You can create logic apps that receive items as a batch by using hello **Batch** trigger.</span></span> <span data-ttu-id="978b1-108">Umożliwia tworzenie aplikacji logiki, które wysyłania partii tooa elementów przy użyciu hello **partii** akcji.</span><span class="sxs-lookup"><span data-stu-id="978b1-108">You can then create logic apps that send items tooa batch by using hello **Batch** action.</span></span>

<span data-ttu-id="978b1-109">W tym temacie pokazano, jak można tworzyć przetwarzanie wsadowe rozwiązanie, wykonując następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="978b1-109">This topic shows how you can build a batching solution by performing these tasks:</span></span> 

* <span data-ttu-id="978b1-110">[Tworzenie aplikacji logiki, która odbiera i zbiera elementów jako plik wsadowy](#batch-receiver).</span><span class="sxs-lookup"><span data-stu-id="978b1-110">[Create a logic app that receives and collects items as a batch](#batch-receiver).</span></span> <span data-ttu-id="978b1-111">Ta aplikacja logiki "partii odbiorcy" Określa hello partii nazwa i wersja kryteria toomeet przed aplikacji logiki odbiornika hello zwalnia i przetwarza elementy.</span><span class="sxs-lookup"><span data-stu-id="978b1-111">This "batch receiver" logic app specifies hello batch name and release criteria toomeet before hello receiver logic app releases and processes items.</span></span> 

* <span data-ttu-id="978b1-112">[Tworzenie aplikacji logiki wysyłanej partii tooa elementów](#batch-sender).</span><span class="sxs-lookup"><span data-stu-id="978b1-112">[Create a logic app that sends items tooa batch](#batch-sender).</span></span> <span data-ttu-id="978b1-113">Ta aplikacja logiki "partii sender" Określa, gdzie toosend elementów, które muszą być istniejących aplikacji logiki odbiornika partii.</span><span class="sxs-lookup"><span data-stu-id="978b1-113">This "batch sender" logic app specifies where toosend items, which must be an existing batch receiver logic app.</span></span> <span data-ttu-id="978b1-114">Można również określić unikatowy klucz, takich jak numer klienta, za "partycji" lub dzielenia partii docelowy hello na podzbiory na podstawie tego klucza.</span><span class="sxs-lookup"><span data-stu-id="978b1-114">You can also specify a unique key, like a customer number, too"partition", or divide, hello target batch into subsets based on that key.</span></span> <span data-ttu-id="978b1-115">W ten sposób wszystkie elementy z tego klucza są zbierane i przetwarzane razem.</span><span class="sxs-lookup"><span data-stu-id="978b1-115">That way, all items with that key are collected and processed together.</span></span> 

## <a name="requirements"></a><span data-ttu-id="978b1-116">Wymagania</span><span class="sxs-lookup"><span data-stu-id="978b1-116">Requirements</span></span>

<span data-ttu-id="978b1-117">toofollow w tym przykładzie potrzebne następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="978b1-117">toofollow this example, you need these items:</span></span>

* <span data-ttu-id="978b1-118">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="978b1-118">An Azure subscription.</span></span> <span data-ttu-id="978b1-119">Jeśli nie masz subskrypcji, możesz [rozpocząć pracę z bezpłatnym kontem platformy Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="978b1-119">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="978b1-120">W przeciwnym razie możesz [skorzystać z subskrypcji z płatnością zgodnie z rzeczywistym użyciem](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="978b1-120">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

* <span data-ttu-id="978b1-121">Podstawową wiedzę na temat o [jak toocreate logic apps](../logic-apps/logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="978b1-121">Basic knowledge about [how toocreate logic apps](../logic-apps/logic-apps-create-a-logic-app.md)</span></span> 

* <span data-ttu-id="978b1-122">Konto e-mail ze wszystkimi [dostawcy poczty e-mail obsługiwane przez usługi Azure Logic Apps](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="978b1-122">An email account with any [email provider supported by Azure Logic Apps](../connectors/apis-list.md)</span></span>

<a name="batch-receiver"></a>

## <a name="create-logic-apps-that-receive-messages-as-a-batch"></a><span data-ttu-id="978b1-123">Tworzenie aplikacji logiki, który odbiera komunikaty jako partii</span><span class="sxs-lookup"><span data-stu-id="978b1-123">Create logic apps that receive messages as a batch</span></span>

<span data-ttu-id="978b1-124">Przed wysłaniem wiadomości tooa partii, należy najpierw utworzyć aplikację logiki "partii odbiornika" z hello **partii** wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="978b1-124">Before you can send messages tooa batch, you must first create a "batch receiver" logic app with hello **Batch** trigger.</span></span> <span data-ttu-id="978b1-125">W ten sposób można wybrać tę aplikację logiki odbiornika podczas tworzenia aplikacji logiki hello nadawcy.</span><span class="sxs-lookup"><span data-stu-id="978b1-125">That way, you can select this receiver logic app when you create hello sender logic app.</span></span> <span data-ttu-id="978b1-126">Dla odbiornika hello należy określić nazwę usługi partia zadań hello, kryteriów wersji i inne ustawienia.</span><span class="sxs-lookup"><span data-stu-id="978b1-126">For hello receiver, you specify hello batch name, release criteria, and other settings.</span></span> 

<span data-ttu-id="978b1-127">Aplikacje logiki nadawcy musi wiedzieć, gdzie elementów toosend, podczas gdy aplikacje logiki odbiorcy nie muszą tooknow cokolwiek o nadawcy hello.</span><span class="sxs-lookup"><span data-stu-id="978b1-127">Sender logic apps need know where toosend items, while receiver logic apps don't need tooknow anything about hello senders.</span></span>

1. <span data-ttu-id="978b1-128">W hello [portalu Azure](https://portal.azure.com), tworzenie aplikacji logiki o tej nazwie: "BatchReceiver"</span><span class="sxs-lookup"><span data-stu-id="978b1-128">In hello [Azure portal](https://portal.azure.com), create a logic app with this name: "BatchReceiver"</span></span> 

2. <span data-ttu-id="978b1-129">W Projektancie aplikacji logiki, Dodaj hello **partii** wyzwalacza, która uruchamia przepływ pracy aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="978b1-129">In Logic Apps Designer, add hello **Batch** trigger, which starts your logic app workflow.</span></span> <span data-ttu-id="978b1-130">W polu wyszukiwania hello wprowadź "partii" jako filtr.</span><span class="sxs-lookup"><span data-stu-id="978b1-130">In hello search box, enter "batch" as your filter.</span></span> <span data-ttu-id="978b1-131">Wybierz ten wyzwalacz: **partii — komunikaty wsadowe**</span><span class="sxs-lookup"><span data-stu-id="978b1-131">Select this trigger: **Batch – Batch messages**</span></span>

   ![Dodaj wyzwalacza partii](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. <span data-ttu-id="978b1-133">Podaj nazwę dla partii hello i określ kryteria za zwolnienie hello partii, na przykład:</span><span class="sxs-lookup"><span data-stu-id="978b1-133">Provide a name for hello batch, and specify criteria for releasing hello batch, for example:</span></span>

   * <span data-ttu-id="978b1-134">**Nazwa partii**: hello nazwę używaną tooidentify hello partii, czyli "TestBatch" w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="978b1-134">**Batch Name**: hello name used tooidentify hello batch, which is "TestBatch" in this example.</span></span>
   * <span data-ttu-id="978b1-135">**Liczba komunikatów**: hello liczbę wiadomości toohold jako partii przed zwolnieniem do przetwarzania, czyli "5" w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="978b1-135">**Message Count**: hello number of messages toohold as a batch before releasing for processing, which is "5" in this example.</span></span>

   ![Podaj szczegóły wyzwalacza partii](./media/logic-apps-batch-process-send-receive-messages/receive-batch-trigger-details.png)

4. <span data-ttu-id="978b1-137">Dodaj inną akcję, która wysyła wiadomość e-mail, gdy hello partii wyzwalacz.</span><span class="sxs-lookup"><span data-stu-id="978b1-137">Add another action that sends an email when hello batch trigger fires.</span></span> <span data-ttu-id="978b1-138">Każdej z partii hello czasu ma pięć elementów, aplikację logiki hello wysyła wiadomość e-mail.</span><span class="sxs-lookup"><span data-stu-id="978b1-138">Each time hello batch has five items, hello logic app sends an email.</span></span>

   1. <span data-ttu-id="978b1-139">W obszarze hello partii wyzwalacza, wybierz **+ nowy krok** > **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="978b1-139">Under hello batch trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="978b1-140">W polu wyszukiwania hello wprowadź "e-mail" jako filtr.</span><span class="sxs-lookup"><span data-stu-id="978b1-140">In hello search box, enter "email" as your filter.</span></span>
   <span data-ttu-id="978b1-141">W oparciu o dostawcę poczty e-mail, wybierz łącznik poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="978b1-141">Based on your email provider, select an email connector.</span></span>
   
      <span data-ttu-id="978b1-142">Na przykład jeśli masz konto służbowe, wybierz hello łącznika programu Outlook pakietu Office 365.</span><span class="sxs-lookup"><span data-stu-id="978b1-142">For example, if you have a work or school account, select hello Office 365 Outlook connector.</span></span> 
      <span data-ttu-id="978b1-143">Jeśli masz konto usługi Gmail, wybierz łącznik usługi Gmail hello.</span><span class="sxs-lookup"><span data-stu-id="978b1-143">If you have a Gmail account, select hello Gmail connector.</span></span>

   3. <span data-ttu-id="978b1-144">Wybierz tę akcję dla Twojego łącznika:  **{*dostawcy e-mail*} — Wyślij e-mail **</span><span class="sxs-lookup"><span data-stu-id="978b1-144">Select this action for your connector: **{*email provider*} - Send an email**</span></span>

      <span data-ttu-id="978b1-145">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="978b1-145">For example:</span></span>

      ![Wybierz akcję "Wyślij wiadomość e-mail" dla dostawcy usługi poczty e-mail](./media/logic-apps-batch-process-send-receive-messages/add-send-email-action.png)

5. <span data-ttu-id="978b1-147">Jeśli wcześniej nie utworzono połączenia dla dostawcy usługi poczty e-mail, wprowadź swoje poświadczenia poczty e-mail dla uwierzytelniania po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="978b1-147">If you didn't previously create a connection for your email provider, provide your email credentials for authentication when prompted.</span></span> <span data-ttu-id="978b1-148">Dowiedz się więcej o [uwierzytelniania poświadczeń e-mail](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="978b1-148">Learn more about [authenticating your email credentials](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

6. <span data-ttu-id="978b1-149">Ustaw właściwości hello akcji hello, który właśnie został dodany.</span><span class="sxs-lookup"><span data-stu-id="978b1-149">Set hello properties for hello action you just added.</span></span>

   * <span data-ttu-id="978b1-150">W hello **do** wprowadź adres e-mail adresata hello.</span><span class="sxs-lookup"><span data-stu-id="978b1-150">In hello **To** box, enter hello recipient's email address.</span></span> 
   <span data-ttu-id="978b1-151">Do celów testowych, można użyć adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="978b1-151">For testing purposes, you can use your own email address.</span></span>

   * <span data-ttu-id="978b1-152">W hello **podmiotu** polu, gdy hello **zawartości dynamicznej** zostanie wyświetlona lista, wybierz hello **nazwa partycji** pola.</span><span class="sxs-lookup"><span data-stu-id="978b1-152">In hello **Subject** box, when hello **Dynamic content** list appears, select hello **Partition Name** field.</span></span>

     ![Z listy "Zawartość dynamiczna" hello wybierz "Nazwa partycji"](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     <span data-ttu-id="978b1-154">W dalszej części artykułu można określić klucz partycji unikatowy czy bez reszty hello partii docelowych do logicznego ustawia toowhere można wysyłać wiadomości.</span><span class="sxs-lookup"><span data-stu-id="978b1-154">In a later section, you can specify a unique partition key that divides hello target batch into logical sets toowhere you can send messages.</span></span> 
     <span data-ttu-id="978b1-155">Każdy zestaw ma unikatowy numer, który jest generowany przez aplikację logiki hello nadawcy.</span><span class="sxs-lookup"><span data-stu-id="978b1-155">Each set has a unique number that's generated by hello sender logic app.</span></span> 
     <span data-ttu-id="978b1-156">Ta funkcja umożliwia pojedyncza partia za pomocą wielu podzestawy i zdefiniować każdy podzbiór o nazwie hello, podane.</span><span class="sxs-lookup"><span data-stu-id="978b1-156">This capability lets you use a single batch with multiple subsets and define each subset with hello name that you provide.</span></span>

   * <span data-ttu-id="978b1-157">W hello **treści** polu, gdy hello **zawartości dynamicznej** zostanie wyświetlona lista, wybierz hello **identyfikator komunikatu** pola.</span><span class="sxs-lookup"><span data-stu-id="978b1-157">In hello **Body** box, when hello **Dynamic content** list appears, select hello **Message Id** field.</span></span>

     !["Identyfikator komunikatu" Wybierz "Treść"](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

     <span data-ttu-id="978b1-159">Ponieważ dane wejściowe hello hello wysyłania wiadomości e-mail akcji jest tablicą, Projektant hello automatycznie dodaje **dla każdego** pętlę wokół hello **wysłać wiadomość e-mail** akcji.</span><span class="sxs-lookup"><span data-stu-id="978b1-159">Because hello input for hello send email action is an array, hello designer automatically adds a **For each** loop around hello **Send an email** action.</span></span> 
     <span data-ttu-id="978b1-160">Ta pętla wykonuje akcję wewnętrzny hello każdego elementu w partii hello.</span><span class="sxs-lookup"><span data-stu-id="978b1-160">This loop performs hello inner action on each item in hello batch.</span></span> 
     <span data-ttu-id="978b1-161">Tak z zestawu elementów toofive hello wsadowych wyzwalacza, otrzymasz pięć wiadomości e-mail, które każdy czas hello wyzwalacza.</span><span class="sxs-lookup"><span data-stu-id="978b1-161">So, with hello batch trigger set toofive items, you get five emails each time hello trigger fires.</span></span>

7.  <span data-ttu-id="978b1-162">Teraz, gdy utworzono aplikacji logiki odbiornika partii, Zapisz aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="978b1-162">Now that you created a batch receiver logic app, save your logic app.</span></span>

    ![Zapisywanie aplikacji logiki](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

<a name="batch-sender"></a>

## <a name="create-logic-apps-that-send-messages-tooa-batch"></a><span data-ttu-id="978b1-164">Tworzenie aplikacji logiki, wysyłających komunikaty tooa partii</span><span class="sxs-lookup"><span data-stu-id="978b1-164">Create logic apps that send messages tooa batch</span></span>

<span data-ttu-id="978b1-165">Teraz należy utworzyć co najmniej jedną aplikację logiki, wysyłających partii toohello elementy zdefiniowane przez aplikację logiki hello odbiornika.</span><span class="sxs-lookup"><span data-stu-id="978b1-165">Now create one or more logic apps that send items toohello batch defined by hello receiver logic app.</span></span> <span data-ttu-id="978b1-166">Dla hello nadawcy należy określić aplikację logiki odbiornika hello i nazwa usługi partia zadań, zawartość komunikatu i inne ustawienia.</span><span class="sxs-lookup"><span data-stu-id="978b1-166">For hello sender, you specify hello receiver logic app and batch name, message content, and any other settings.</span></span> <span data-ttu-id="978b1-167">Opcjonalnie można podać partii partycji unikatowy kluczy toodivide hello na podzestawy toocollect elementy z tego klucza.</span><span class="sxs-lookup"><span data-stu-id="978b1-167">You can optionally provide a unique partition key toodivide hello batch into subsets toocollect items with that key.</span></span>

<span data-ttu-id="978b1-168">Aplikacje logiki nadawcy musi wiedzieć, gdzie elementów toosend, podczas gdy aplikacje logiki odbiorcy nie muszą tooknow cokolwiek o nadawcy hello.</span><span class="sxs-lookup"><span data-stu-id="978b1-168">Sender logic apps need know where toosend items, while receiver logic apps don't need tooknow anything about hello senders.</span></span>

1. <span data-ttu-id="978b1-169">Tworzenie aplikacji logiki innej o tej nazwie: "BatchSender"</span><span class="sxs-lookup"><span data-stu-id="978b1-169">Create another logic app with this name: "BatchSender"</span></span>

   1. <span data-ttu-id="978b1-170">W polu wyszukiwania hello wprowadź "cyklu" jako filtr.</span><span class="sxs-lookup"><span data-stu-id="978b1-170">In hello search box, enter "recurrence" as your filter.</span></span> 
   <span data-ttu-id="978b1-171">Wybierz ten wyzwalacz: **harmonogram - cyklu**</span><span class="sxs-lookup"><span data-stu-id="978b1-171">Select this trigger: **Schedule - Recurrence**</span></span>

      ![Dodaj wyzwalacza hello "Harmonogram cyklu"](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-receiver.png)

   2. <span data-ttu-id="978b1-173">Ustaw częstotliwość hello i aplikacji logiki nadawcy hello toorun interwał co minutę.</span><span class="sxs-lookup"><span data-stu-id="978b1-173">Set hello frequency and interval toorun hello sender logic app every minute.</span></span>

      ![Ustaw częstotliwość i interwał cyklu wyzwalacza](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-receiver-details.png)

2. <span data-ttu-id="978b1-175">Dodaj nowy krok do wysyłania wiadomości tooa partii.</span><span class="sxs-lookup"><span data-stu-id="978b1-175">Add a new step for sending messages tooa batch.</span></span>

   1. <span data-ttu-id="978b1-176">W obszarze hello cyklu wyzwalacza, wybierz **+ nowy krok** > **Dodaj akcję**.</span><span class="sxs-lookup"><span data-stu-id="978b1-176">Under hello recurrence trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="978b1-177">W polu wyszukiwania hello wprowadź "partii" jako filtr.</span><span class="sxs-lookup"><span data-stu-id="978b1-177">In hello search box, enter "batch" as your filter.</span></span> 

   3. <span data-ttu-id="978b1-178">Wybierz tę akcję: **wysyłania wiadomości toobatch — wybierz przepływ pracy aplikacji logiki z wyzwalaczem partii**</span><span class="sxs-lookup"><span data-stu-id="978b1-178">Select this action: **Send messages toobatch – Choose a Logic Apps workflow with batch trigger**</span></span>

      ![Zaznacz pole wyboru "Wyślij wiadomości toobatch"](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   4. <span data-ttu-id="978b1-180">Teraz wybierz "BatchReceiver" aplikację logiki utworzony wcześniej, która jest teraz wyświetlany jako akcja.</span><span class="sxs-lookup"><span data-stu-id="978b1-180">Now select your "BatchReceiver" logic app that you previously created, which now appears as an action.</span></span>

      ![Wybierz aplikację logiki "partii odbiornika"](./media/logic-apps-batch-process-send-receive-messages/send-batch-select-batch-receiver.png)

      > [!NOTE]
      > <span data-ttu-id="978b1-182">Lista Hello zawiera również wszystkie inne aplikacje logiki mających wyzwalaczy partii.</span><span class="sxs-lookup"><span data-stu-id="978b1-182">hello list also shows any other logic apps that have batch triggers.</span></span>

3. <span data-ttu-id="978b1-183">Ustaw właściwości partii hello.</span><span class="sxs-lookup"><span data-stu-id="978b1-183">Set hello batch properties.</span></span>

   * <span data-ttu-id="978b1-184">**Nazwa partii**: Nazwa instancji hello zdefiniowane przez aplikację logiki odbiornika Witaj, "TestBatch" w tym przykładzie i sprawdzania poprawności w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="978b1-184">**Batch Name**: hello batch name defined by hello receiver logic app, which is "TestBatch" in this example and is validated at runtime.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="978b1-185">Upewnij się, nie zmieniać hello partii nazwy, która musi odpowiadać nazwie partii hello, określonym przez aplikację logiki hello odbiornika.</span><span class="sxs-lookup"><span data-stu-id="978b1-185">Make sure that you don't change hello batch name, which must match hello batch name that's specified by hello receiver logic app.</span></span>
     > <span data-ttu-id="978b1-186">Zmiana nazwy partii hello powoduje, że nadawca hello toofail aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="978b1-186">Changing hello batch name causes hello sender logic app toofail.</span></span>

   * <span data-ttu-id="978b1-187">**Zawartość komunikatu**: hello treści wiadomości, które mają toosend.</span><span class="sxs-lookup"><span data-stu-id="978b1-187">**Message Content**: hello message content that you want toosend.</span></span> 
   <span data-ttu-id="978b1-188">Na przykład dodać to wyrażenie, że wstawia hello bieżącą datę i godzinę do zawartości, że wysyłania partii toohello wiadomość hello:</span><span class="sxs-lookup"><span data-stu-id="978b1-188">For this example, add this expression that inserts hello current date and time into hello message content that you send toohello batch:</span></span>

     1. <span data-ttu-id="978b1-189">Gdy hello **zawartości dynamicznej** zostanie wyświetlona lista, wybierz **wyrażenia**.</span><span class="sxs-lookup"><span data-stu-id="978b1-189">When hello **Dynamic content** list appears, choose **Expression**.</span></span> 
     2. <span data-ttu-id="978b1-190">Wprowadź wyrażenie hello **utcnow()**i wybierz polecenie **OK**.</span><span class="sxs-lookup"><span data-stu-id="978b1-190">Enter hello expression **utcnow()**, and choose **OK**.</span></span> 

        ![W "Zawartość komunikatu" Wybierz opcję "Wyrażenie".](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details.png)

4. <span data-ttu-id="978b1-193">Teraz należy skonfigurować partycji dla partii hello.</span><span class="sxs-lookup"><span data-stu-id="978b1-193">Now set up a partition for hello batch.</span></span> <span data-ttu-id="978b1-194">Akcja "BatchReceiver" hello, wybierz **Pokaż zaawansowane opcje**.</span><span class="sxs-lookup"><span data-stu-id="978b1-194">In hello "BatchReceiver" action, choose **Show advanced options**.</span></span>

   * <span data-ttu-id="978b1-195">**Nazwa partycji**: toouse klucza partycji unikatowy opcjonalne rozdzielania hello docelowy partii.</span><span class="sxs-lookup"><span data-stu-id="978b1-195">**Partition Name**: An optional unique partition key toouse for dividing hello target batch.</span></span> <span data-ttu-id="978b1-196">Na przykład Dodaj wyrażenie, które generuje losową liczbę między jeden a pięć.</span><span class="sxs-lookup"><span data-stu-id="978b1-196">For this example, add an expression that generates a random number between one and five.</span></span>
   
     1. <span data-ttu-id="978b1-197">Gdy hello **zawartości dynamicznej** zostanie wyświetlona lista, wybierz **wyrażenia**.</span><span class="sxs-lookup"><span data-stu-id="978b1-197">When hello **Dynamic content** list appears, choose **Expression**.</span></span>
     2. <span data-ttu-id="978b1-198">Wprowadź wyrażenie: **rand(1,6)**</span><span class="sxs-lookup"><span data-stu-id="978b1-198">Enter this expression: **rand(1,6)**</span></span>

        ![Konfigurowanie partycji dla partii użytkownika docelowego](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-partition-advanced-options.png)

        <span data-ttu-id="978b1-200">To **rand** funkcja generuje do zakresu od jednej do pięciu.</span><span class="sxs-lookup"><span data-stu-id="978b1-200">This **rand** function generates a number between one and five.</span></span> 
        <span data-ttu-id="978b1-201">Dlatego są podzielenie tej partii na pięć numerowane partycje, które dynamicznie ustawia tego wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="978b1-201">So you are dividing this batch into five numbered partitions, which this expression dynamically sets.</span></span>

   * <span data-ttu-id="978b1-202">**Identyfikator wiadomości**: identyfikator komunikatu opcjonalne i jest generowanym identyfikatorze GUID, gdy parametr jest pusty.</span><span class="sxs-lookup"><span data-stu-id="978b1-202">**Message Id**: An optional message identifier and is a generated GUID when empty.</span></span> 
   <span data-ttu-id="978b1-203">W tym przykładzie pozostaw to pole puste.</span><span class="sxs-lookup"><span data-stu-id="978b1-203">For this example, leave this box blank.</span></span>

5. <span data-ttu-id="978b1-204">Zapisz aplikację logiki.</span><span class="sxs-lookup"><span data-stu-id="978b1-204">Save your logic app.</span></span> <span data-ttu-id="978b1-205">Aplikację logiki nadawcy wyglądają teraz podobny przykład toothis:</span><span class="sxs-lookup"><span data-stu-id="978b1-205">Your sender logic app now looks similar toothis example:</span></span>

   ![Zapisz aplikację logiki nadawcy](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details-finished.png)

## <a name="test-your-logic-apps"></a><span data-ttu-id="978b1-207">Testowanie aplikacji logiki</span><span class="sxs-lookup"><span data-stu-id="978b1-207">Test your logic apps</span></span>

<span data-ttu-id="978b1-208">tootest Twojego przetwarzanie wsadowe rozwiązania, pozostaw aplikacje logiki uruchomione kilka minut.</span><span class="sxs-lookup"><span data-stu-id="978b1-208">tootest your batching solution, leave your logic apps running for a few minutes.</span></span> <span data-ttu-id="978b1-209">Po chwili uruchamiania uzyskiwania wiadomości e-mail w grupach pięć, wszystkie z hello partycji sam klucz.</span><span class="sxs-lookup"><span data-stu-id="978b1-209">Soon, you start getting emails in groups of five, all with hello same partition key.</span></span>

<span data-ttu-id="978b1-210">Aplikację logiki BatchSender co minutę, generuje losową liczbę między jeden a pięć, korzysta to generowany numer jako klucza partycji hello partii docelowy hello wysyłania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="978b1-210">Your BatchSender logic app runs every minute, generates a random number between one and five, and uses this generated number as hello partition key for hello target batch where messages are sent.</span></span> <span data-ttu-id="978b1-211">Zawsze partii hello zawiera pięć elementy z hello tym samym kluczem partycji aplikacji logiki BatchReceiver generowane i wysyła poczty dla każdego komunikatu.</span><span class="sxs-lookup"><span data-stu-id="978b1-211">Each time hello batch has five items with hello same partition key, your BatchReceiver logic app fires and sends mail for each message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="978b1-212">Po zakończeniu testowania, sprawdź, czy wyłączyć wysyłanie wiadomości powitania BatchSender logiki aplikacji toostop i nie przeciążać skrzynki odbiorczej.</span><span class="sxs-lookup"><span data-stu-id="978b1-212">When you're done testing, make sure that you disable hello BatchSender logic app toostop sending messages and avoid overloading your inbox.</span></span>

## <a name="next-steps"></a><span data-ttu-id="978b1-213">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="978b1-213">Next steps</span></span>

* [<span data-ttu-id="978b1-214">Tworzenie w definicji aplikacji logiki za pomocą formatu JSON</span><span class="sxs-lookup"><span data-stu-id="978b1-214">Build on logic app definitions by using JSON</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="978b1-215">Tworzenie aplikacji bez serwera w programie Visual Studio z usługi Azure Logic Apps i funkcje</span><span class="sxs-lookup"><span data-stu-id="978b1-215">Build a serverless app in Visual Studio with Azure Logic Apps and Functions</span></span>](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [<span data-ttu-id="978b1-216">Obsługa wyjątków i rejestrowania błędów dla usługi logic apps</span><span class="sxs-lookup"><span data-stu-id="978b1-216">Exception handling and error logging for logic apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
