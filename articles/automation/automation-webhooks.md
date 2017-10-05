---
title: "Uruchamianie elementu runbook usługi Automatyzacja Azure z elementu webhook | Dokumentacja firmy Microsoft"
description: "Element webhook, która umożliwia klientowi uruchomienia elementu runbook automatyzacji Azure z wywołania HTTP.  W tym artykule opisano sposób tworzenia elementu webhook i wywoływanie jednego uruchomienia elementu runbook."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9b20237c-a593-4299-bbdc-35c47ee9e55d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: 6c65427fcd18e41a90dfb872aa9525f758b17b87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a><span data-ttu-id="1d06b-104">Uruchamianie elementu runbook usługi Automatyzacja Azure z elementu webhook</span><span class="sxs-lookup"><span data-stu-id="1d06b-104">Starting an Azure Automation runbook with a webhook</span></span>
<span data-ttu-id="1d06b-105">A *webhook* umożliwia uruchomienie określonego elementu runbook automatyzacji Azure za pomocą pojedynczego żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="1d06b-105">A *webhook* allows you to start a particular runbook in Azure Automation through a single HTTP request.</span></span> <span data-ttu-id="1d06b-106">Dzięki temu usług zewnętrznych, takich jak Visual Studio Team Services, GitHub, analizy dzienników Microsoft Operations Management Suite lub niestandardowych aplikacji do uruchamiania elementów runbook bez wdrażania pełnego rozwiązania przy użyciu interfejsu API usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="1d06b-106">This allows external services such as Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics, or custom applications to start runbooks without implementing a full solution using the Azure Automation API.</span></span>  
<span data-ttu-id="1d06b-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span><span class="sxs-lookup"><span data-stu-id="1d06b-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span></span>

<span data-ttu-id="1d06b-108">Można porównać elementów webhook do innych metod uruchamianie elementu runbook [uruchamianie elementu runbook automatyzacji Azure](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="1d06b-108">You can compare webhooks to other methods of starting a runbook in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md)</span></span>

## <a name="details-of-a-webhook"></a><span data-ttu-id="1d06b-109">Szczegóły elementu webhook</span><span class="sxs-lookup"><span data-stu-id="1d06b-109">Details of a webhook</span></span>
<span data-ttu-id="1d06b-110">W poniższej tabeli opisano właściwości, które należy skonfigurować dla elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-110">The following table describes the properties that you must configure for a webhook.</span></span>

| <span data-ttu-id="1d06b-111">Właściwość</span><span class="sxs-lookup"><span data-stu-id="1d06b-111">Property</span></span> | <span data-ttu-id="1d06b-112">Opis</span><span class="sxs-lookup"><span data-stu-id="1d06b-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1d06b-113">Nazwa</span><span class="sxs-lookup"><span data-stu-id="1d06b-113">Name</span></span> |<span data-ttu-id="1d06b-114">Możesz podać dowolną nazwę wybranego dla elementu webhook, ponieważ to nie jest widoczne dla klientów.</span><span class="sxs-lookup"><span data-stu-id="1d06b-114">You can provide any name you want for a webhook since this is not exposed to the client.</span></span>  <span data-ttu-id="1d06b-115">Tylko służy do należy do identyfikacji elementu runbook automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="1d06b-115">It is only used for you to identify the runbook in Azure Automation.</span></span> <br>  <span data-ttu-id="1d06b-116">Najlepszym rozwiązaniem należy nadać elementu webhook nazwę związane z klienta, który zostanie użyty.</span><span class="sxs-lookup"><span data-stu-id="1d06b-116">As a best practice, you should give the webhook a name related to the client that will use it.</span></span> |
| <span data-ttu-id="1d06b-117">ADRES URL</span><span class="sxs-lookup"><span data-stu-id="1d06b-117">URL</span></span> |<span data-ttu-id="1d06b-118">Adres URL elementu webhook jest unikatowy adres, który klient wywołuje z POST protokołu HTTP, aby uruchomić element runbook połączone z elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-118">The URL of the webhook is the unique address that a client calls with an HTTP POST to start the runbook linked to the webhook.</span></span>  <span data-ttu-id="1d06b-119">Jest ona generowana automatycznie podczas tworzenia elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-119">It is automatically generated when you create the webhook.</span></span>  <span data-ttu-id="1d06b-120">Nie można określić niestandardowy adres URL.</span><span class="sxs-lookup"><span data-stu-id="1d06b-120">You cannot specify a custom URL.</span></span> <br> <br>  <span data-ttu-id="1d06b-121">Adres URL zawiera token zabezpieczający, który umożliwia elementu runbook do wywołania przez system innej firmy bez dalszego uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="1d06b-121">The URL contains a security token that allows the runbook to be invoked by a third party system with no further authentication.</span></span> <span data-ttu-id="1d06b-122">Z tego powodu powinny być traktowane jak hasło.</span><span class="sxs-lookup"><span data-stu-id="1d06b-122">For this reason, it should be treated like a password.</span></span>  <span data-ttu-id="1d06b-123">Ze względów bezpieczeństwa możesz jedynie wyświetlić adres URL w portalu Azure w czasie tworzenia elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-123">For security reasons, you can only view the URL in the Azure portal at the time the webhook is created.</span></span> <span data-ttu-id="1d06b-124">Należy zauważyć, adres URL w bezpiecznej lokalizacji do użytku w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="1d06b-124">You should note the URL in a secure location for future use.</span></span> |
| <span data-ttu-id="1d06b-125">Data wygaśnięcia</span><span class="sxs-lookup"><span data-stu-id="1d06b-125">Expiration date</span></span> |<span data-ttu-id="1d06b-126">Takie jak certyfikat każdy element webhook ma datę wygaśnięcia, które go można już używać.</span><span class="sxs-lookup"><span data-stu-id="1d06b-126">Like a certificate, each webhook has an expiration date at which time it can no longer be used.</span></span>  <span data-ttu-id="1d06b-127">Ta data wygaśnięcia można zmodyfikować po utworzeniu elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-127">This expiration date can be modified after the webhook is created.</span></span> |
| <span data-ttu-id="1d06b-128">Enabled (Włączony)</span><span class="sxs-lookup"><span data-stu-id="1d06b-128">Enabled</span></span> |<span data-ttu-id="1d06b-129">Elementu webhook jest domyślnie włączona po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="1d06b-129">A webhook is enabled by default when it is created.</span></span>  <span data-ttu-id="1d06b-130">Jeśli zostanie ustawiona na wyłączone, a następnie klienta nie będzie można go użyć.</span><span class="sxs-lookup"><span data-stu-id="1d06b-130">If you set it to Disabled, then no client will be able to use it.</span></span>  <span data-ttu-id="1d06b-131">Można ustawić **włączone** właściwości po utworzeniu elementu webhook lub w każdej chwili po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="1d06b-131">You can set the **Enabled** property when you create the webhook or anytime once it is created.</span></span> |

### <a name="parameters"></a><span data-ttu-id="1d06b-132">Parametry</span><span class="sxs-lookup"><span data-stu-id="1d06b-132">Parameters</span></span>
<span data-ttu-id="1d06b-133">Elementu webhook można zdefiniować wartości parametrów elementu runbook, które będą używane po uruchomieniu elementu runbook przez ten element webhook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-133">A webhook can define values for runbook parameters that are used when the runbook is started by that webhook.</span></span> <span data-ttu-id="1d06b-134">Element webhook muszą zawierać wartości parametrów obowiązkowych elementu runbook i może zawierać wartości parametrów opcjonalnych.</span><span class="sxs-lookup"><span data-stu-id="1d06b-134">The webhook must include values for any mandatory parameters of the runbook and may include values for optional parameters.</span></span> <span data-ttu-id="1d06b-135">Po utworzeniu webhoook można zmodyfikować wartość parametru skonfigurowany do elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-135">A parameter value configured to a webhook can be modified even after creating the webhoook.</span></span> <span data-ttu-id="1d06b-136">Każdy z wielu elementów webhook połączone z jednego elementu runbook można użyć wartości innym parametrem.</span><span class="sxs-lookup"><span data-stu-id="1d06b-136">Multiple webhooks linked to a single runbook can each use different parameter values.</span></span>

<span data-ttu-id="1d06b-137">Po uruchomieniu elementu runbook za pomocą elementu webhook klient go nie można zastąpić wartości parametrów zdefiniowanych w elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-137">When a client starts a runbook using a webhook, it cannot override the parameter values defined in the webhook.</span></span>  <span data-ttu-id="1d06b-138">Na odbieranie danych z klientem, element runbook może akceptować jeden parametr o nazwie **$WebhookData** typu [object], który będzie zawierać dane, które klient dołącza w żądaniu POST.</span><span class="sxs-lookup"><span data-stu-id="1d06b-138">To receive data from the client, the runbook can accept a single parameter called **$WebhookData** of type [object] that will contain data that the client includes in the POST request.</span></span>

![Właściwości Webhookdata](media/automation-webhooks/webhook-data-properties.png)

<span data-ttu-id="1d06b-140">**$WebhookData** obiektu będzie mieć następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="1d06b-140">The **$WebhookData** object will have the following properties:</span></span>

| <span data-ttu-id="1d06b-141">Właściwość</span><span class="sxs-lookup"><span data-stu-id="1d06b-141">Property</span></span> | <span data-ttu-id="1d06b-142">Opis</span><span class="sxs-lookup"><span data-stu-id="1d06b-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1d06b-143">WebhookName</span><span class="sxs-lookup"><span data-stu-id="1d06b-143">WebhookName</span></span> |<span data-ttu-id="1d06b-144">Nazwa elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-144">The name of the webhook.</span></span> |
| <span data-ttu-id="1d06b-145">RequestHeader</span><span class="sxs-lookup"><span data-stu-id="1d06b-145">RequestHeader</span></span> |<span data-ttu-id="1d06b-146">Tabela skrótów zawierająca nagłówki przychodzącego żądania POST.</span><span class="sxs-lookup"><span data-stu-id="1d06b-146">Hash table containing the headers of the incoming POST request.</span></span> |
| <span data-ttu-id="1d06b-147">requestBody</span><span class="sxs-lookup"><span data-stu-id="1d06b-147">RequestBody</span></span> |<span data-ttu-id="1d06b-148">Treść żądania POST przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="1d06b-148">The body of the incoming POST request.</span></span>  <span data-ttu-id="1d06b-149">To zachowują formatowania, takiego jak ciąg formatu JSON, XML, lub postać zakodowanych danych.</span><span class="sxs-lookup"><span data-stu-id="1d06b-149">This will retain any formatting such as string, JSON, XML, or form encoded data.</span></span> <span data-ttu-id="1d06b-150">Element runbook musi być przystosowana do pracy z formatem danych, która oczekuje.</span><span class="sxs-lookup"><span data-stu-id="1d06b-150">The runbook must be written to work with the data format that is expected.</span></span> |

<span data-ttu-id="1d06b-151">Nie jest żadna konfiguracja elementu webhook wymagany do obsługi **$WebhookData** parametr, a element runbook nie jest wymagane go zaakceptować.</span><span class="sxs-lookup"><span data-stu-id="1d06b-151">There is no configuration of the webhook required to support the **$WebhookData** parameter, and the runbook is not required to accept it.</span></span>  <span data-ttu-id="1d06b-152">Jeśli element runbook nie definiuje parametru, żadnych szczegółów żądania wysłanych z klienta zostanie zignorowany.</span><span class="sxs-lookup"><span data-stu-id="1d06b-152">If the runbook does not define the parameter, then any details of the request sent from the client is ignored.</span></span>

<span data-ttu-id="1d06b-153">Jeśli musisz określić wartość dla $WebhookData podczas tworzenia elementu webhook, że wartość będzie zastąpiona podczas elementu webhook uruchamiania elementu runbook przy użyciu danych z żądania POST klienta, nawet jeśli klient nie ma żadnych danych w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="1d06b-153">If you specify a value for $WebhookData when you create the webhook, that value will be overriden when the webhook starts the runbook with the data from the client POST request, even if the client does not include any data in the request body.</span></span>  <span data-ttu-id="1d06b-154">Po uruchomieniu elementu runbook, który ma $WebhookData przy użyciu innej metody niż elementu webhook należy podać wartość dla $Webhookdata rozpoznane zostaną przez element runbook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-154">If you start a runbook that has $WebhookData using a method other than a webhook, you can provide a value for $Webhookdata that will be recognized by the runbook.</span></span>  <span data-ttu-id="1d06b-155">Ta wartość powinna być obiekt o takim samym [właściwości](#details-of-a-webhook) jako $Webhookdata tak, aby element runbook właściwie pracę z nią tak, jakby jego pracy z rzeczywistego WebhookData przekazany przez elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-155">This value should be an object with the same [properties](#details-of-a-webhook) as $Webhookdata so that the runbook can properly work with it as if it was working with actual WebhookData passed by a webhook.</span></span>

<span data-ttu-id="1d06b-156">Na przykład Jeśli rozpoczynasz następujący element runbook w portalu Azure i przekazać niektóre przykładowe WebhookData do testowania, ponieważ obiekt jest WebhookData, powinien zostać przekazany jako dane JSON w Interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1d06b-156">For example, if you are starting the following runbook from the Azure Portal and want to pass some sample WebhookData for testing, since WebhookData is an object, it should be passed as JSON in the UI.</span></span>

![Parametr WebhookData z poziomu interfejsu użytkownika](media/automation-webhooks/WebhookData-parameter-from-UI.png)

<span data-ttu-id="1d06b-158">Powyżej elementu runbook, jeśli masz następujące właściwości dla parametru WebhookData:</span><span class="sxs-lookup"><span data-stu-id="1d06b-158">For the above runbook, if you have the following properties for the WebhookData parameter:</span></span>

1. <span data-ttu-id="1d06b-159">WebhookName: *MyWebhook*</span><span class="sxs-lookup"><span data-stu-id="1d06b-159">WebhookName: *MyWebhook*</span></span>
2. <span data-ttu-id="1d06b-160">RequestHeader: *z = użytkownika testowego*</span><span class="sxs-lookup"><span data-stu-id="1d06b-160">RequestHeader: *From=Test User*</span></span>
3. <span data-ttu-id="1d06b-161">RequestBody: *["VM1", "Maszyny VM2"]*</span><span class="sxs-lookup"><span data-stu-id="1d06b-161">RequestBody: *[“VM1”, “VM2”]*</span></span>

<span data-ttu-id="1d06b-162">Następnie przejdzie następującą wartość JSON w Interfejsie użytkownika dla parametru WebhookData:</span><span class="sxs-lookup"><span data-stu-id="1d06b-162">Then you would pass the following JSON value in the UI for the WebhookData parameter:</span></span>  

* <span data-ttu-id="1d06b-163">{"WebhookName": "MyWebhook", "RequestHeader": {"Od": "Użytkownik testowy"}, "RequestBody": "[\"VM1\",\"maszyny VM2\"]"}</span><span class="sxs-lookup"><span data-stu-id="1d06b-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span></span>

![Uruchom parametr WebhookData z interfejsu użytkownika](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> <span data-ttu-id="1d06b-165">Wartości wszystkich parametrów wejściowych są rejestrowane za pomocą zadania elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-165">The values of all input parameters are logged with the runbook job.</span></span>  <span data-ttu-id="1d06b-166">Oznacza to, że wszelkie danych wejściowych dostarczonych przez klienta w żądaniu elementu webhook jest rejestrowane i dostępną dla wszystkich użytkowników z dostępem do zadanie usługi Automatyzacja.</span><span class="sxs-lookup"><span data-stu-id="1d06b-166">This means that any input provided by the client in the webhook request will be logged and available to anyone with access to the automation job.</span></span>  <span data-ttu-id="1d06b-167">Z tego powodu należy zachować ostrożność w wywołaniach elementu webhook w tym poufne informacje.</span><span class="sxs-lookup"><span data-stu-id="1d06b-167">For this reason, you should be cautious about including sensitive information in webhook calls.</span></span>
>

## <a name="security"></a><span data-ttu-id="1d06b-168">Bezpieczeństwo</span><span class="sxs-lookup"><span data-stu-id="1d06b-168">Security</span></span>
<span data-ttu-id="1d06b-169">Zabezpieczenia elementu webhook polega na prywatność adresu URL, który zawiera token zabezpieczający, który umożliwi można wywołać.</span><span class="sxs-lookup"><span data-stu-id="1d06b-169">The security of a webhook relies on the privacy of its URL which contains a security token that allows it to be invoked.</span></span> <span data-ttu-id="1d06b-170">Automatyzacja Azure nie wykonuje żadnego uwierzytelniania na żądanie tak długo, jak staje się poprawny adres URL.</span><span class="sxs-lookup"><span data-stu-id="1d06b-170">Azure Automation does not perform any authentication on the request as long as it is made to the correct URL.</span></span> <span data-ttu-id="1d06b-171">Z tego powodu nie można używać elementów webhook dla elementów runbook, które bardzo ważne zmiany funkcji bez używania alternatywnej metody sprawdzania poprawności żądania.</span><span class="sxs-lookup"><span data-stu-id="1d06b-171">For this reason, webhooks should not be used for runbooks that perform highly sensitive functions without using an alternate means of validating the request.</span></span>

<span data-ttu-id="1d06b-172">Można uwzględnić logiki w ramach elementu runbook w celu określenia, czy została wywołana przez elementu webhook, sprawdzając **WebhookName** właściwość parametru $WebhookData.</span><span class="sxs-lookup"><span data-stu-id="1d06b-172">You can include logic within the runbook to determine that it was called by a webhook by checking the **WebhookName** property of the $WebhookData parameter.</span></span> <span data-ttu-id="1d06b-173">Element runbook można wykonać dalsze weryfikacji przez wyszukiwanie szczegółowych informacji w **RequestHeader** lub **RequestBody** właściwości.</span><span class="sxs-lookup"><span data-stu-id="1d06b-173">The runbook could perform further validation by looking for particular information in the **RequestHeader** or **RequestBody** properties.</span></span>

<span data-ttu-id="1d06b-174">Kolejną strategią jest runbook weryfikowania niektórych warunków zewnętrznych podczas odebrała żądanie elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-174">Another strategy is to have the runbook perform some validation of an external condition when it received a webhook request.</span></span>  <span data-ttu-id="1d06b-175">Rozważmy na przykład element runbook, który jest wywoływany przez GitHub, gdy istnieje nowy zatwierdzeń do repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="1d06b-175">For example, consider a runbook that is called by GitHub whenever there is a new commit to a GitHub repository.</span></span>  <span data-ttu-id="1d06b-176">Element runbook może się połączyć GitHub, aby sprawdzić, czy nowe zatwierdzenia rzeczywista właśnie nastąpiło przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="1d06b-176">The runbook might connect to GitHub to validate that a new commit had actually just occurred before continuing.</span></span>

## <a name="creating-a-webhook"></a><span data-ttu-id="1d06b-177">Tworzenie elementu webhook</span><span class="sxs-lookup"><span data-stu-id="1d06b-177">Creating a webhook</span></span>
<span data-ttu-id="1d06b-178">Użyj poniższej procedury, aby utworzyć nowy element webhook powiązany element runbook w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1d06b-178">Use the following procedure to create a new webhook linked to a runbook in the Azure portal.</span></span>

1. <span data-ttu-id="1d06b-179">Z **bloku elementów Runbook** w portalu Azure kliknij element runbook, aby wyświetlić jego szczegóły blok uruchomienia elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-179">From the **Runbooks blade** in the Azure portal, click the runbook that the webhook will start to view its detail blade.</span></span>
2. <span data-ttu-id="1d06b-180">Kliknij przycisk **Webhook** w górnej części bloku, aby otworzyć **Dodawanie elementu Webhook** bloku.</span><span class="sxs-lookup"><span data-stu-id="1d06b-180">Click **Webhook** at the top of the blade to open the **Add Webhook** blade.</span></span> <br><span data-ttu-id="1d06b-181">
   ![Przycisk elementów Webhook](media/automation-webhooks/webhooks-button.png)</span><span class="sxs-lookup"><span data-stu-id="1d06b-181">
![Webhooks button](media/automation-webhooks/webhooks-button.png)</span></span>
3. <span data-ttu-id="1d06b-182">Kliknij przycisk **tworzenia nowego elementu webhook** otworzyć **bloku Utwórz elementu webhook**.</span><span class="sxs-lookup"><span data-stu-id="1d06b-182">Click **Create new webhook** to open the **Create webhook blade**.</span></span>
4. <span data-ttu-id="1d06b-183">Określ **nazwa**, **Data wygaśnięcia** dla elementu webhook i określa, czy powinno być włączone.</span><span class="sxs-lookup"><span data-stu-id="1d06b-183">Specify a **Name**, **Expiration Date** for the webhook and whether it should be enabled.</span></span> <span data-ttu-id="1d06b-184">Zobacz [szczegóły elementu webhook](#details-of-a-webhook) Aby uzyskać więcej informacji tych właściwości.</span><span class="sxs-lookup"><span data-stu-id="1d06b-184">See [Details of a webhook](#details-of-a-webhook) for more information these properties.</span></span>
5. <span data-ttu-id="1d06b-185">Kliknij ikonę kopiowania, a następnie naciśnij klawisze Ctrl + C, aby skopiować adres URL elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-185">Click the copy icon and press Ctrl+C to copy the URL of the webhook.</span></span>  <span data-ttu-id="1d06b-186">Następnie zapisz go w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="1d06b-186">Then record it in a safe place.</span></span>  <span data-ttu-id="1d06b-187">**Po utworzeniu elementu webhook nie można ponownie pobrać adresu URL.**</span><span class="sxs-lookup"><span data-stu-id="1d06b-187">**Once you create the webhook, you cannot retrieve the URL again.**</span></span> <br><span data-ttu-id="1d06b-188">
   ![Adres URL elementu Webhook](media/automation-webhooks/copy-webhook-url.png)</span><span class="sxs-lookup"><span data-stu-id="1d06b-188">
![Webhook URL](media/automation-webhooks/copy-webhook-url.png)</span></span>
6. <span data-ttu-id="1d06b-189">Kliknij przycisk **parametry** podać wartości parametrów elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-189">Click **Parameters** to provide values for the runbook parameters.</span></span>  <span data-ttu-id="1d06b-190">Jeśli element runbook ma parametry obowiązkowe, następnie nie można utworzyć elementu webhook, chyba że znajdują się wartości.</span><span class="sxs-lookup"><span data-stu-id="1d06b-190">If the runbook has mandatory parameters, then you will not be able to create the webhook unless values are provided.</span></span>
7. <span data-ttu-id="1d06b-191">Kliknij przycisk **Utwórz** można utworzyć elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-191">Click **Create** to create the webhook.</span></span>

## <a name="using-a-webhook"></a><span data-ttu-id="1d06b-192">Przy użyciu elementu webhook</span><span class="sxs-lookup"><span data-stu-id="1d06b-192">Using a webhook</span></span>
<span data-ttu-id="1d06b-193">Aby użyć elementu webhook po jego utworzeniu, aplikacja kliencka należy wygenerować HTTP POST z adresem URL dla elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-193">To use a webhook after it has been created, your client application must issue an HTTP POST with the URL for the webhook.</span></span>  <span data-ttu-id="1d06b-194">Składnia elementu webhook będzie w następującym formacie.</span><span class="sxs-lookup"><span data-stu-id="1d06b-194">The syntax of the webhook will be in the following format.</span></span>

    http://<Webhook Server>/token?=<Token Value>

<span data-ttu-id="1d06b-195">Klient zostanie wyświetlony jeden z następujących kody powrotu z żądania POST.</span><span class="sxs-lookup"><span data-stu-id="1d06b-195">The client will receive one of the following return codes from the POST request.</span></span>  

| <span data-ttu-id="1d06b-196">Kod</span><span class="sxs-lookup"><span data-stu-id="1d06b-196">Code</span></span> | <span data-ttu-id="1d06b-197">Tekst</span><span class="sxs-lookup"><span data-stu-id="1d06b-197">Text</span></span> | <span data-ttu-id="1d06b-198">Opis</span><span class="sxs-lookup"><span data-stu-id="1d06b-198">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="1d06b-199">202</span><span class="sxs-lookup"><span data-stu-id="1d06b-199">202</span></span> |<span data-ttu-id="1d06b-200">Zaakceptowane</span><span class="sxs-lookup"><span data-stu-id="1d06b-200">Accepted</span></span> |<span data-ttu-id="1d06b-201">Żądanie zostało zaakceptowane, a element runbook został pomyślnie w kolejce.</span><span class="sxs-lookup"><span data-stu-id="1d06b-201">The request was accepted, and the runbook was successfully queued.</span></span> |
| <span data-ttu-id="1d06b-202">400</span><span class="sxs-lookup"><span data-stu-id="1d06b-202">400</span></span> |<span data-ttu-id="1d06b-203">Nieprawidłowe żądanie</span><span class="sxs-lookup"><span data-stu-id="1d06b-203">Bad Request</span></span> |<span data-ttu-id="1d06b-204">Nie zaakceptowano żądanie dla jednego z następujących powodów.</span><span class="sxs-lookup"><span data-stu-id="1d06b-204">The request was not accepted for one of the following reasons.</span></span> <ul> <li><span data-ttu-id="1d06b-205">Element webhook wygasł.</span><span class="sxs-lookup"><span data-stu-id="1d06b-205">The webhook has expired.</span></span></li> <li><span data-ttu-id="1d06b-206">Elementu webhook jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="1d06b-206">The webhook is disabled.</span></span></li> <li><span data-ttu-id="1d06b-207">Token w adresie URL jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="1d06b-207">The token in the URL is invalid.</span></span></li>  </ul> |
| <span data-ttu-id="1d06b-208">404</span><span class="sxs-lookup"><span data-stu-id="1d06b-208">404</span></span> |<span data-ttu-id="1d06b-209">Nie można odnaleźć</span><span class="sxs-lookup"><span data-stu-id="1d06b-209">Not Found</span></span> |<span data-ttu-id="1d06b-210">Nie zaakceptowano żądanie dla jednego z następujących powodów.</span><span class="sxs-lookup"><span data-stu-id="1d06b-210">The request was not accepted for one of the following reasons.</span></span> <ul> <li><span data-ttu-id="1d06b-211">Nie można odnaleźć elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-211">The webhook was not found.</span></span></li> <li><span data-ttu-id="1d06b-212">Nie znaleziono elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-212">The runbook was not found.</span></span></li> <li><span data-ttu-id="1d06b-213">Nie można odnaleźć konta.</span><span class="sxs-lookup"><span data-stu-id="1d06b-213">The account was not found.</span></span></li>  </ul> |
| <span data-ttu-id="1d06b-214">500</span><span class="sxs-lookup"><span data-stu-id="1d06b-214">500</span></span> |<span data-ttu-id="1d06b-215">Wewnętrzny błąd serwera</span><span class="sxs-lookup"><span data-stu-id="1d06b-215">Internal Server Error</span></span> |<span data-ttu-id="1d06b-216">Adres URL jest prawidłowy, ale wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="1d06b-216">The URL was valid, but an error occurred.</span></span>  <span data-ttu-id="1d06b-217">Prześlij żądanie.</span><span class="sxs-lookup"><span data-stu-id="1d06b-217">Please resubmit the request.</span></span> |

<span data-ttu-id="1d06b-218">Zakładając, że żądanie zakończy się pomyślnie, odpowiedzi elementu webhook zawiera identyfikator zadania w formacie JSON w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="1d06b-218">Assuming the request is successful, the webhook response contains the job id in JSON format as follows.</span></span> <span data-ttu-id="1d06b-219">Będzie zawierać identyfikator pojedyncze zadanie, ale umożliwia potencjalne przyszłe ulepszenia formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="1d06b-219">It will contain a single job id, but the JSON format allows for potential future enhancements.</span></span>

    {"JobIds":["<JobId>"]}  

<span data-ttu-id="1d06b-220">Klient nie może określić po zakończeniu zadania elementu runbook lub jego stanie ukończenia z elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-220">The client cannot determine when the runbook job completes or its completion status from the webhook.</span></span>  <span data-ttu-id="1d06b-221">Można określić te informacje przy użyciu identyfikatora zadania przy użyciu innej metody takie jak [programu Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) lub [interfejsu API usługi Automatyzacja Azure](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d06b-221">It can determine this information using the job id with another method such as [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) or the [Azure Automation API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span></span>

### <a name="example"></a><span data-ttu-id="1d06b-222">Przykład</span><span class="sxs-lookup"><span data-stu-id="1d06b-222">Example</span></span>
<span data-ttu-id="1d06b-223">W poniższym przykładzie użyto programu Windows PowerShell do uruchamiania elementu runbook z elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-223">The following example uses Windows PowerShell to start a runbook with a webhook.</span></span>  <span data-ttu-id="1d06b-224">Można użyć dowolnego języka, który może zgłaszać żądania HTTP elementu webhook; Środowisko Windows PowerShell jest używany po prostu poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="1d06b-224">Note that any language that can make an HTTP request can use a webhook; Windows PowerShell is just used here as an example.</span></span>

<span data-ttu-id="1d06b-225">Element runbook jest Oczekiwano listy maszyn wirtualnych zapisany w formacie JSON w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="1d06b-225">The runbook is expecting a list of virtual machines formatted in JSON in the body of the request.</span></span> <span data-ttu-id="1d06b-226">Możemy także są w tym informacje o który uruchamia element runbook oraz datę i godzinę, które jest uruchamiana w nagłówku żądania.</span><span class="sxs-lookup"><span data-stu-id="1d06b-226">We also are including information about who is starting the runbook and the date and time it is being started in the header of the request.</span></span>      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


<span data-ttu-id="1d06b-227">Na poniższej ilustracji przedstawiono informacje o nagłówku (przy użyciu [Fiddler](http://www.telerik.com/fiddler) śledzenia) z tego żądania.</span><span class="sxs-lookup"><span data-stu-id="1d06b-227">The following image shows the header information (using a [Fiddler](http://www.telerik.com/fiddler) trace) from this request.</span></span> <span data-ttu-id="1d06b-228">W tym standardowych nagłówków żądania HTTP, oprócz niestandardowa data i z nagłówków, które dodano.</span><span class="sxs-lookup"><span data-stu-id="1d06b-228">This includes standard headers of an HTTP request in addition to the custom Date and From headers that we added.</span></span>  <span data-ttu-id="1d06b-229">Każdy z tych wartości jest dostępny dla elementu runbook w **RequestHeaders** właściwość **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="1d06b-229">Each of these values is available to the runbook in the **RequestHeaders** property of **WebhookData**.</span></span>

![Przycisk elementów Webhook](media/automation-webhooks/webhook-request-headers.png)

<span data-ttu-id="1d06b-231">Na poniższej ilustracji przedstawiono treść żądania (przy użyciu [Fiddler](http://www.telerik.com/fiddler) śledzenia) dostępnej do elementu runbook w **RequestBody** właściwość **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="1d06b-231">The following image shows the body of the request (using a [Fiddler](http://www.telerik.com/fiddler) trace)  that is available to the runbook in the **RequestBody** property of **WebhookData**.</span></span> <span data-ttu-id="1d06b-232">To jest w formacie JSON powodu formatu, który został uwzględniony w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="1d06b-232">This is formatted as JSON because that was the format that was included in the body of the request.</span></span>     

![Przycisk elementów Webhook](media/automation-webhooks/webhook-request-body.png)

<span data-ttu-id="1d06b-234">Na poniższej ilustracji przedstawiono żądania wysyłane z programu Windows PowerShell i wynikowy odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="1d06b-234">The following image shows the request being sent from Windows PowerShell and the resulting response.</span></span>  <span data-ttu-id="1d06b-235">Identyfikator zadania jest wyodrębniana z odpowiedzi i konwertowana na ciąg.</span><span class="sxs-lookup"><span data-stu-id="1d06b-235">The job id is extracted from the response and converted to a string.</span></span>

![Przycisk elementów Webhook](media/automation-webhooks/webhook-request-response.png)

<span data-ttu-id="1d06b-237">Następujący przykładowy element runbook akceptuje poprzednie przykładowe żądanie i uruchamiania maszyn wirtualnych, określona w treści żądania.</span><span class="sxs-lookup"><span data-stu-id="1d06b-237">The following sample runbook accepts the previous example request and starts the virtual machines specified in the request body.</span></span>

    workflow Test-StartVirtualMachinesFromWebhook
    {
        param (
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {

            # Collect properties of WebhookData
            $WebhookName     =     $WebhookData.WebhookName
            $WebhookHeaders =     $WebhookData.RequestHeader
            $WebhookBody     =     $WebhookData.RequestBody

            # Collect individual headers. VMList converted from JSON.
            $From = $WebhookHeaders.From
            $VMList = ConvertFrom-Json -InputObject $WebhookBody
            Write-Output "Runbook started from webhook $WebhookName by $From."

            # Authenticate to Azure resources
            $Cred = Get-AutomationPSCredential -Name 'MyAzureCredential'
            Add-AzureAccount -Credential $Cred

            # Start each virtual machine
            foreach ($VM in $VMList)
            {
                $VMName = $VM.Name
                Write-Output "Starting $VMName"
                Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName
            }
        }
        else {
            Write-Error "Runbook mean to be started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-to-azure-alerts"></a><span data-ttu-id="1d06b-238">Uruchamianie elementów runbook w odpowiedzi na alerty Azure</span><span class="sxs-lookup"><span data-stu-id="1d06b-238">Starting runbooks in response to Azure alerts</span></span>
<span data-ttu-id="1d06b-239">Włączone elementu Webhook elementów runbook może służyć do reagowania na [Azure alerty](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="1d06b-239">Webhook-enabled runbooks can be used to react to [Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="1d06b-240">Zasobami na platformie Azure mogą być monitorowane przez zbieranie statystyk, takich jak wydajności, dostępności i użyciu za pomocą usługi Azure alerty.</span><span class="sxs-lookup"><span data-stu-id="1d06b-240">Resources in Azure can be monitored by collecting the statistics like performance, availability and usage with the help of Azure alerts.</span></span> <span data-ttu-id="1d06b-241">Otrzymasz alert w oparciu metryki monitorowania lub zdarzenia dla zasobów platformy Azure, obecnie kont automatyzacji obsługuje tylko metryki.</span><span class="sxs-lookup"><span data-stu-id="1d06b-241">You can receive an alert based on monitoring metrics or events for your Azure resources, currently Automation Accounts support only metrics.</span></span> <span data-ttu-id="1d06b-242">Jeśli wartość określonej metryki przekracza próg przypisane lub skonfigurowany zdarzenie jest wyzwalane, a następnie powiadomienie jest wysyłane do administratora usługi lub współadministratorzy Aby rozwiązać alert, aby uzyskać więcej informacji na temat metryki i zdarzenia zapoznaj się [ Alerty Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="1d06b-242">When the value of a specified metric exceeds the threshold assigned or if the configured event is triggered then a notification is sent to the service admin or co-admins to resolve the alert, for more information on metrics and events please refer to [Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="1d06b-243">Oprócz za pomocą usługi Azure alerty jako system powiadomień, należy również rozpocząć się poza elementów runbook w odpowiedzi na alerty.</span><span class="sxs-lookup"><span data-stu-id="1d06b-243">Besides using Azure alerts as a notification system, you can also kick off runbooks in response to alerts.</span></span> <span data-ttu-id="1d06b-244">Automatyzacja Azure oferuje możliwość uruchamiania włączone elementu webhook elementów runbook z alertami platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1d06b-244">Azure Automation provides the capability to run webhook-enabled runbooks with Azure alerts.</span></span> <span data-ttu-id="1d06b-245">Jeśli Metryka przekracza wartość skonfigurowany próg następnie reguły alertu staje się aktywny i wyzwala webhook usługi Automatyzacja, który z kolei wykonuje element runbook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-245">When a metric exceeds the configured threshold value then the alert rule becomes active and triggers the automation webhook which in turn executes the runbook.</span></span>

![elementów webhook](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a><span data-ttu-id="1d06b-247">Kontekst alertu</span><span class="sxs-lookup"><span data-stu-id="1d06b-247">Alert context</span></span>
<span data-ttu-id="1d06b-248">Należy rozważyć zasobów platformy Azure, takich jak maszyny wirtualnej, użycie procesora CPU tego komputera jest jednym z metryki wydajności.</span><span class="sxs-lookup"><span data-stu-id="1d06b-248">Consider an Azure resource such as a virtual machine, CPU utilization of this machine is one of the key performance metric.</span></span> <span data-ttu-id="1d06b-249">Jeśli wykorzystanie procesora CPU jest 100% lub więcej niż określonym przez długi czas, możesz uruchomić ponownie maszynę wirtualną, aby rozwiązać ten problem.</span><span class="sxs-lookup"><span data-stu-id="1d06b-249">If the CPU utilization is 100% or more than a certain amount for long period of time, you might want to restart the virtual machine to fix the problem.</span></span> <span data-ttu-id="1d06b-250">To będzie możliwe przez skonfigurowanie reguły alertu do maszyny wirtualnej i procent użycia procesora CPU, jako jego metryka ma ta reguła.</span><span class="sxs-lookup"><span data-stu-id="1d06b-250">This can be solved by configuring an alert rule to the virtual machine and this rule takes CPU percentage as its metric.</span></span> <span data-ttu-id="1d06b-251">Procent użycia procesora CPU w tym miejscu jest po prostu wykonywanej na przykład, ale istnieje wiele innych metryk, które można skonfigurować do zasobów platformy Azure i ponownego uruchamiania maszyny wirtualnej jest akcja, która jest wykonywana, aby rozwiązać ten problem, można skonfigurować element runbook, aby wykonywać inne czynności.</span><span class="sxs-lookup"><span data-stu-id="1d06b-251">CPU percentage here is just taken as an example but there are many other metrics that you can configure to your Azure resources and restarting the virtual machine is an action that is taken to fix this issue, you can configure the runbook to take other actions.</span></span>

<span data-ttu-id="1d06b-252">Gdy to reguły alertu staje się aktywny i wyzwala runbook włączone elementu webhook wysyła kontekst alertu w elemencie runbook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-252">When this the alert rule becomes active and triggers the webhook-enabled runbook, it sends the alert context to the runbook.</span></span> <span data-ttu-id="1d06b-253">[Kontekst alertu](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) zawiera szczegółowe informacje, łącznie z **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** i **sygnatury czasowej** jest wymagane dla elementu runbook do identyfikacji zasobu, na którym będzie biorąc pod akcji.</span><span class="sxs-lookup"><span data-stu-id="1d06b-253">[Alert context](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contains details including **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** and **Timestamp** which are required for the runbook to identify the resource on which it will be taking action.</span></span> <span data-ttu-id="1d06b-254">Alert kontekstu jest osadzony w części treści **WebhookData** obiektu wysyłanego do elementu runbook i jest dostępny z **Webhook.RequestBody** właściwości</span><span class="sxs-lookup"><span data-stu-id="1d06b-254">Alert context is embedded in the body part of the **WebhookData** object sent to the runbook and it can be accessed with **Webhook.RequestBody** property</span></span>

### <a name="example"></a><span data-ttu-id="1d06b-255">Przykład</span><span class="sxs-lookup"><span data-stu-id="1d06b-255">Example</span></span>
<span data-ttu-id="1d06b-256">Utwórz maszynę wirtualną platformy Azure w subskrypcji i powiąż [alert, aby monitorować metryki procent procesora CPU](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="1d06b-256">Create an Azure virtual machine in your subscription and associate an [alert to monitor CPU percentage metric](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="1d06b-257">Podczas tworzenia alertu upewnij się, że wypełnić pole elementu webhook z adresem URL elementu webhook, który został wygenerowany podczas tworzenia elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="1d06b-257">While creating the alert make sure you populate the webhook field with the URL of the webhook which was generated while creating the webhook.</span></span>

<span data-ttu-id="1d06b-258">Następujący przykładowy element runbook jest wyzwalane, gdy reguła alertu staje się aktywny i zbiera parametrów kontekstu alertu, które są wymagane dla elementu runbook do identyfikacji zasobu, na którym będzie biorąc pod akcji.</span><span class="sxs-lookup"><span data-stu-id="1d06b-258">The following sample runbook is triggered when the alert rule becomes active and it collects the Alert context parameters which are required for the runbook to identify the resource on which it will be taking action.</span></span>

    workflow Invoke-RunbookUsingAlerts
    {
        param (      
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {   
            # Collect properties of WebhookData.
            $WebhookName    =   $WebhookData.WebhookName
            $WebhookBody    =   $WebhookData.RequestBody
            $WebhookHeaders =   $WebhookData.RequestHeader

            # Outputs information on the webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain the WebhookBody containing the AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain the AlertContext     
            $AlertContext = [object]$WebhookBody.context

            # Some selected AlertContext information
            Write-Output "`nALERT CONTEXT DATA"
            Write-Output "==================="
            Write-Output $AlertContext.name
            Write-Output $AlertContext.subscriptionId
            Write-Output $AlertContext.resourceGroupName
            Write-Output $AlertContext.resourceName
            Write-Output $AlertContext.resourceType
            Write-Output $AlertContext.resourceId
            Write-Output $AlertContext.timestamp

            # Act on the AlertContext data, in our case restarting the VM.
            # Authenticate to your Azure subscription using Organization ID to be able to restart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check the status property of the VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart the VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant to only be started from a webhook."  
        }  
    }



## <a name="next-steps"></a><span data-ttu-id="1d06b-259">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1d06b-259">Next steps</span></span>
* <span data-ttu-id="1d06b-260">Aby uzyskać więcej informacji na różne sposoby uruchamiania elementu runbook, zobacz [uruchamianie elementu Runbook](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="1d06b-260">For details on different ways to start a runbook, see [Starting a Runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="1d06b-261">Aby uzyskać informacje o wyświetlaniu stanu zadania elementu Runbook, zapoznaj się [wykonanie elementu Runbook automatyzacji Azure](automation-runbook-execution.md).</span><span class="sxs-lookup"><span data-stu-id="1d06b-261">For information on viewing the Status of a Runbook Job, refer to [Runbook execution in Azure Automation](automation-runbook-execution.md).</span></span>
* <span data-ttu-id="1d06b-262">Aby dowiedzieć się, jak używać usługi Automatyzacja Azure do wykonania akcji na alerty Azure, zobacz [skorygować alerty maszyny Wirtualnej Azure z elementu Runbook usługi automatyzacja](automation-azure-vm-alert-integration.md).</span><span class="sxs-lookup"><span data-stu-id="1d06b-262">To learn how to use Azure Automation to take action on Azure Alerts, see [Remediate Azure VM Alerts with Automation Runbooks](automation-azure-vm-alert-integration.md).</span></span>
