---
title: "Element runbook usługi Automatyzacja Azure z elementu webhook aaaStarting | Dokumentacja firmy Microsoft"
description: "Element webhook umożliwiający toostart klienta elementu runbook automatyzacji Azure z wywołania HTTP.  W tym artykule opisano sposób toocreate elementu webhook i w jaki sposób toocall toostart jednego elementu runbook."
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
ms.openlocfilehash: ca6cde66b3784ceb5d0bc5921cee87aea74cb150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a><span data-ttu-id="3691a-104">Uruchamianie elementu runbook usługi Automatyzacja Azure z elementu webhook</span><span class="sxs-lookup"><span data-stu-id="3691a-104">Starting an Azure Automation runbook with a webhook</span></span>
<span data-ttu-id="3691a-105">A *webhook* pozwala toostart określonego elementu runbook automatyzacji Azure za pomocą pojedynczego żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="3691a-105">A *webhook* allows you toostart a particular runbook in Azure Automation through a single HTTP request.</span></span> <span data-ttu-id="3691a-106">Pozwala to usług zewnętrznych, takich jak Visual Studio Team Services, GitHub, analizy dzienników Microsoft Operations Management Suite lub niestandardowych aplikacji toostart elementów runbook bez wdrażania przy użyciu interfejsu API usługi Automatyzacja Azure hello pełnego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="3691a-106">This allows external services such as Visual Studio Team Services, GitHub, Microsoft Operations Management Suite Log Analytics, or custom applications toostart runbooks without implementing a full solution using hello Azure Automation API.</span></span>  
<span data-ttu-id="3691a-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span><span class="sxs-lookup"><span data-stu-id="3691a-107">![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)</span></span>

<span data-ttu-id="3691a-108">Można porównać elementów webhook tooother metod uruchamiania elementu runbook [uruchamianie elementu runbook automatyzacji Azure](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="3691a-108">You can compare webhooks tooother methods of starting a runbook in [Starting a runbook in Azure Automation](automation-starting-a-runbook.md)</span></span>

## <a name="details-of-a-webhook"></a><span data-ttu-id="3691a-109">Szczegóły elementu webhook</span><span class="sxs-lookup"><span data-stu-id="3691a-109">Details of a webhook</span></span>
<span data-ttu-id="3691a-110">Witaj poniższej tabeli opisano właściwości hello, które należy skonfigurować dla elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="3691a-110">hello following table describes hello properties that you must configure for a webhook.</span></span>

| <span data-ttu-id="3691a-111">Właściwość</span><span class="sxs-lookup"><span data-stu-id="3691a-111">Property</span></span> | <span data-ttu-id="3691a-112">Opis</span><span class="sxs-lookup"><span data-stu-id="3691a-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3691a-113">Nazwa</span><span class="sxs-lookup"><span data-stu-id="3691a-113">Name</span></span> |<span data-ttu-id="3691a-114">Możesz podać dowolną nazwę wybranego dla elementu webhook, ponieważ jest to nie jest uwidaczniana toohello klienta.</span><span class="sxs-lookup"><span data-stu-id="3691a-114">You can provide any name you want for a webhook since this is not exposed toohello client.</span></span>  <span data-ttu-id="3691a-115">Jest używana tylko dla możesz tooidentify hello elementu runbook automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="3691a-115">It is only used for you tooidentify hello runbook in Azure Automation.</span></span> <br>  <span data-ttu-id="3691a-116">Najlepszym rozwiązaniem, należy nadać webhook powitania klienta toohello powiązane nazwy, który zostanie użyty.</span><span class="sxs-lookup"><span data-stu-id="3691a-116">As a best practice, you should give hello webhook a name related toohello client that will use it.</span></span> |
| <span data-ttu-id="3691a-117">ADRES URL</span><span class="sxs-lookup"><span data-stu-id="3691a-117">URL</span></span> |<span data-ttu-id="3691a-118">adres URL elementu webhook hello Hello jest unikatowy adres hello, że klient wywołuje z elementem runbook HTTP POST toostart hello połączone toohello elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="3691a-118">hello URL of hello webhook is hello unique address that a client calls with an HTTP POST toostart hello runbook linked toohello webhook.</span></span>  <span data-ttu-id="3691a-119">Jest ona generowana automatycznie podczas tworzenia elementu webhook hello.</span><span class="sxs-lookup"><span data-stu-id="3691a-119">It is automatically generated when you create hello webhook.</span></span>  <span data-ttu-id="3691a-120">Nie można określić niestandardowy adres URL.</span><span class="sxs-lookup"><span data-stu-id="3691a-120">You cannot specify a custom URL.</span></span> <br> <br>  <span data-ttu-id="3691a-121">Witaj adres URL zawiera token zabezpieczający, który umożliwia hello toobe runbook wywoływany przez system innej firmy bez dalszego uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="3691a-121">hello URL contains a security token that allows hello runbook toobe invoked by a third party system with no further authentication.</span></span> <span data-ttu-id="3691a-122">Z tego powodu powinny być traktowane jak hasło.</span><span class="sxs-lookup"><span data-stu-id="3691a-122">For this reason, it should be treated like a password.</span></span>  <span data-ttu-id="3691a-123">Ze względów bezpieczeństwa możesz tylko hello widoku, adres URL w portalu Azure na powitania czasu hello webhook hello jest tworzona.</span><span class="sxs-lookup"><span data-stu-id="3691a-123">For security reasons, you can only view hello URL in hello Azure portal at hello time hello webhook is created.</span></span> <span data-ttu-id="3691a-124">Należy zauważyć, adres URL hello w bezpiecznej lokalizacji do użytku w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="3691a-124">You should note hello URL in a secure location for future use.</span></span> |
| <span data-ttu-id="3691a-125">Data wygaśnięcia</span><span class="sxs-lookup"><span data-stu-id="3691a-125">Expiration date</span></span> |<span data-ttu-id="3691a-126">Takie jak certyfikat każdy element webhook ma datę wygaśnięcia, które go można już używać.</span><span class="sxs-lookup"><span data-stu-id="3691a-126">Like a certificate, each webhook has an expiration date at which time it can no longer be used.</span></span>  <span data-ttu-id="3691a-127">Ta data wygaśnięcia można zmodyfikować po utworzeniu elementu webhook hello.</span><span class="sxs-lookup"><span data-stu-id="3691a-127">This expiration date can be modified after hello webhook is created.</span></span> |
| <span data-ttu-id="3691a-128">Enabled (Włączony)</span><span class="sxs-lookup"><span data-stu-id="3691a-128">Enabled</span></span> |<span data-ttu-id="3691a-129">Elementu webhook jest domyślnie włączona po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="3691a-129">A webhook is enabled by default when it is created.</span></span>  <span data-ttu-id="3691a-130">Jeśli jest on ustawiany tooDisabled, a następnie nie klient nie będzie możliwe toouse go.</span><span class="sxs-lookup"><span data-stu-id="3691a-130">If you set it tooDisabled, then no client will be able toouse it.</span></span>  <span data-ttu-id="3691a-131">Można ustawić hello **włączone** podczas tworzenia elementu webhook hello lub w każdej chwili po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="3691a-131">You can set hello **Enabled** property when you create hello webhook or anytime once it is created.</span></span> |

### <a name="parameters"></a><span data-ttu-id="3691a-132">Parametry</span><span class="sxs-lookup"><span data-stu-id="3691a-132">Parameters</span></span>
<span data-ttu-id="3691a-133">Elementu webhook można zdefiniować wartości parametrów elementu runbook, które są używane przy uruchamianiu elementu runbook hello przez tego elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="3691a-133">A webhook can define values for runbook parameters that are used when hello runbook is started by that webhook.</span></span> <span data-ttu-id="3691a-134">Element webhook Hello muszą zawierać wartości parametrów obowiązkowych hello runbook i może zawierać wartości parametrów opcjonalnych.</span><span class="sxs-lookup"><span data-stu-id="3691a-134">hello webhook must include values for any mandatory parameters of hello runbook and may include values for optional parameters.</span></span> <span data-ttu-id="3691a-135">Po utworzeniu hello webhoook można zmodyfikować elementu webhook tooa skonfigurowana wartość parametru.</span><span class="sxs-lookup"><span data-stu-id="3691a-135">A parameter value configured tooa webhook can be modified even after creating hello webhoook.</span></span> <span data-ttu-id="3691a-136">Każdy z wielu elementów webhook połączone tooa jednego elementu runbook można użyć wartości innym parametrem.</span><span class="sxs-lookup"><span data-stu-id="3691a-136">Multiple webhooks linked tooa single runbook can each use different parameter values.</span></span>

<span data-ttu-id="3691a-137">Po uruchomieniu elementu runbook za pomocą elementu webhook klient go nie może zastąpić hello wartości parametrów zdefiniowane w hello elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="3691a-137">When a client starts a runbook using a webhook, it cannot override hello parameter values defined in hello webhook.</span></span>  <span data-ttu-id="3691a-138">dane tooreceive od powitania klienta, hello runbook może akceptować jeden parametr o nazwie **$WebhookData** typu [object], która będzie zawierać dane powitania klienta obejmuje hello wysłanie żądania POST.</span><span class="sxs-lookup"><span data-stu-id="3691a-138">tooreceive data from hello client, hello runbook can accept a single parameter called **$WebhookData** of type [object] that will contain data that hello client includes in hello POST request.</span></span>

![Właściwości Webhookdata](media/automation-webhooks/webhook-data-properties.png)

<span data-ttu-id="3691a-140">Witaj **$WebhookData** obiekt będzie miał hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="3691a-140">hello **$WebhookData** object will have hello following properties:</span></span>

| <span data-ttu-id="3691a-141">Właściwość</span><span class="sxs-lookup"><span data-stu-id="3691a-141">Property</span></span> | <span data-ttu-id="3691a-142">Opis</span><span class="sxs-lookup"><span data-stu-id="3691a-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3691a-143">WebhookName</span><span class="sxs-lookup"><span data-stu-id="3691a-143">WebhookName</span></span> |<span data-ttu-id="3691a-144">Nazwa elementu webhook hello Hello.</span><span class="sxs-lookup"><span data-stu-id="3691a-144">hello name of hello webhook.</span></span> |
| <span data-ttu-id="3691a-145">RequestHeader</span><span class="sxs-lookup"><span data-stu-id="3691a-145">RequestHeader</span></span> |<span data-ttu-id="3691a-146">Tabela skrótów zawierająca nagłówki hello hello przychodzącego żądania POST.</span><span class="sxs-lookup"><span data-stu-id="3691a-146">Hash table containing hello headers of hello incoming POST request.</span></span> |
| <span data-ttu-id="3691a-147">requestBody</span><span class="sxs-lookup"><span data-stu-id="3691a-147">RequestBody</span></span> |<span data-ttu-id="3691a-148">Treść Hello hello przychodzącego żądania POST.</span><span class="sxs-lookup"><span data-stu-id="3691a-148">hello body of hello incoming POST request.</span></span>  <span data-ttu-id="3691a-149">To zachowują formatowania, takiego jak ciąg formatu JSON, XML, lub postać zakodowanych danych.</span><span class="sxs-lookup"><span data-stu-id="3691a-149">This will retain any formatting such as string, JSON, XML, or form encoded data.</span></span> <span data-ttu-id="3691a-150">Hello runbook musi być napisana toowork z hello format danych jest oczekiwany.</span><span class="sxs-lookup"><span data-stu-id="3691a-150">hello runbook must be written toowork with hello data format that is expected.</span></span> |

<span data-ttu-id="3691a-151">Nie jest żadna konfiguracja hello toosupport wymaganego elementu webhook hello **$WebhookData** parametru i hello elementu runbook nie jest wymagane tooaccept go.</span><span class="sxs-lookup"><span data-stu-id="3691a-151">There is no configuration of hello webhook required toosupport hello **$WebhookData** parameter, and hello runbook is not required tooaccept it.</span></span>  <span data-ttu-id="3691a-152">Jeśli element runbook hello nie definiuje parametru hello, żadnych szczegółów żądania hello wysłanych z klienta hello jest ignorowana.</span><span class="sxs-lookup"><span data-stu-id="3691a-152">If hello runbook does not define hello parameter, then any details of hello request sent from hello client is ignored.</span></span>

<span data-ttu-id="3691a-153">Jeśli określisz wartości dla $WebhookData podczas tworzenia elementu webhook hello, że wartość będzie zastąpiona uruchomienia elementu webhook hello hello runbook hello danymi z żądania POST powitania klienta, nawet wtedy, gdy w treści żądania hello powitania klienta nie zawiera żadnych danych.</span><span class="sxs-lookup"><span data-stu-id="3691a-153">If you specify a value for $WebhookData when you create hello webhook, that value will be overriden when hello webhook starts hello runbook with hello data from hello client POST request, even if hello client does not include any data in hello request body.</span></span>  <span data-ttu-id="3691a-154">Po uruchomieniu elementu runbook, który ma $WebhookData przy użyciu innej metody niż elementu webhook można podać wartość dla $Webhookdata rozpoznane zostaną przez element runbook hello.</span><span class="sxs-lookup"><span data-stu-id="3691a-154">If you start a runbook that has $WebhookData using a method other than a webhook, you can provide a value for $Webhookdata that will be recognized by hello runbook.</span></span>  <span data-ttu-id="3691a-155">Ta wartość powinna być obiektu z hello tego samego [właściwości](#details-of-a-webhook) jako $Webhookdata tak hello elementu runbook właściwie pracę z nią tak, jakby jego pracy z rzeczywistego WebhookData przekazany przez elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="3691a-155">This value should be an object with hello same [properties](#details-of-a-webhook) as $Webhookdata so that hello runbook can properly work with it as if it was working with actual WebhookData passed by a webhook.</span></span>

<span data-ttu-id="3691a-156">Na przykład Jeśli rozpoczynasz hello następującego elementu runbook z hello portalu Azure i chcesz toopass niektóre przykładowe WebhookData do testowania, ponieważ obiekt jest WebhookData, jego powinien zostać przekazany jako JSON w hello interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3691a-156">For example, if you are starting hello following runbook from hello Azure Portal and want toopass some sample WebhookData for testing, since WebhookData is an object, it should be passed as JSON in hello UI.</span></span>

![Parametr WebhookData z poziomu interfejsu użytkownika](media/automation-webhooks/WebhookData-parameter-from-UI.png)

<span data-ttu-id="3691a-158">Dla hello powyżej elementu runbook, jeśli masz następujące właściwości dla parametru WebhookData hello hello:</span><span class="sxs-lookup"><span data-stu-id="3691a-158">For hello above runbook, if you have hello following properties for hello WebhookData parameter:</span></span>

1. <span data-ttu-id="3691a-159">WebhookName: *MyWebhook*</span><span class="sxs-lookup"><span data-stu-id="3691a-159">WebhookName: *MyWebhook*</span></span>
2. <span data-ttu-id="3691a-160">RequestHeader: *z = użytkownika testowego*</span><span class="sxs-lookup"><span data-stu-id="3691a-160">RequestHeader: *From=Test User*</span></span>
3. <span data-ttu-id="3691a-161">RequestBody: *["VM1", "Maszyny VM2"]*</span><span class="sxs-lookup"><span data-stu-id="3691a-161">RequestBody: *[“VM1”, “VM2”]*</span></span>

<span data-ttu-id="3691a-162">Następnie przejdzie hello następujące wartości JSON w hello interfejsu użytkownika dla parametru WebhookData hello:</span><span class="sxs-lookup"><span data-stu-id="3691a-162">Then you would pass hello following JSON value in hello UI for hello WebhookData parameter:</span></span>  

* <span data-ttu-id="3691a-163">{"WebhookName": "MyWebhook", "RequestHeader": {"Od": "Użytkownik testowy"}, "RequestBody": "[\"VM1\",\"maszyny VM2\"]"}</span><span class="sxs-lookup"><span data-stu-id="3691a-163">{"WebhookName":"MyWebhook", "RequestHeader":{"From":"Test User"}, "RequestBody":"[\"VM1\",\"VM2\"]"}</span></span>

![Uruchom parametr WebhookData z interfejsu użytkownika](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> <span data-ttu-id="3691a-165">Witaj wartości wszystkich parametrów wejściowych są rejestrowane przy hello zadanie elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="3691a-165">hello values of all input parameters are logged with hello runbook job.</span></span>  <span data-ttu-id="3691a-166">Oznacza to, że wszelkie danych wejściowych dostarczonych przez klienta hello w żądaniu webhook hello będą rejestrowane i dostępne tooanyone z zadanie usługi Automatyzacja toohello dostępu.</span><span class="sxs-lookup"><span data-stu-id="3691a-166">This means that any input provided by hello client in hello webhook request will be logged and available tooanyone with access toohello automation job.</span></span>  <span data-ttu-id="3691a-167">Z tego powodu należy zachować ostrożność w wywołaniach elementu webhook w tym poufne informacje.</span><span class="sxs-lookup"><span data-stu-id="3691a-167">For this reason, you should be cautious about including sensitive information in webhook calls.</span></span>
>

## <a name="security"></a><span data-ttu-id="3691a-168">Bezpieczeństwo</span><span class="sxs-lookup"><span data-stu-id="3691a-168">Security</span></span>
<span data-ttu-id="3691a-169">Hello bezpieczeństwa elementu webhook polega na prywatność hello adresu URL, który zawiera token zabezpieczający, który pozwala toobe wywoływane.</span><span class="sxs-lookup"><span data-stu-id="3691a-169">hello security of a webhook relies on hello privacy of its URL which contains a security token that allows it toobe invoked.</span></span> <span data-ttu-id="3691a-170">Automatyzacja Azure nie wykonuje żadnego uwierzytelniania na powitania żądanie tak długo, jak staje się toohello poprawny adres URL.</span><span class="sxs-lookup"><span data-stu-id="3691a-170">Azure Automation does not perform any authentication on hello request as long as it is made toohello correct URL.</span></span> <span data-ttu-id="3691a-171">Z tego powodu nie można używać elementów webhook dla elementów runbook funkcji wysoce poufnymi bez używania alternatywnej metody sprawdzania poprawności żądania hello.</span><span class="sxs-lookup"><span data-stu-id="3691a-171">For this reason, webhooks should not be used for runbooks that perform highly sensitive functions without using an alternate means of validating hello request.</span></span>

<span data-ttu-id="3691a-172">Można uwzględnić logiki w ramach hello toodetermine elementu runbook, czy została wywołana przez elementu webhook, sprawdzając hello **WebhookName** właściwość parametru hello $WebhookData.</span><span class="sxs-lookup"><span data-stu-id="3691a-172">You can include logic within hello runbook toodetermine that it was called by a webhook by checking hello **WebhookName** property of hello $WebhookData parameter.</span></span> <span data-ttu-id="3691a-173">Witaj runbook można wykonać dalsze weryfikacji przez wyszukiwanie szczegółowych informacji w hello **RequestHeader** lub **RequestBody** właściwości.</span><span class="sxs-lookup"><span data-stu-id="3691a-173">hello runbook could perform further validation by looking for particular information in hello **RequestHeader** or **RequestBody** properties.</span></span>

<span data-ttu-id="3691a-174">Toohave jest kolejną strategią hello runbook weryfikowania niektórych warunku zewnętrznych podczas odebrała żądanie elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="3691a-174">Another strategy is toohave hello runbook perform some validation of an external condition when it received a webhook request.</span></span>  <span data-ttu-id="3691a-175">Rozważmy na przykład element runbook, który jest wywoływany przez GitHub, gdy istnieje nowe repozytorium GitHub tooa zatwierdzania.</span><span class="sxs-lookup"><span data-stu-id="3691a-175">For example, consider a runbook that is called by GitHub whenever there is a new commit tooa GitHub repository.</span></span>  <span data-ttu-id="3691a-176">Witaj runbook może się połączyć toovalidate tooGitHub, nowe zatwierdzenia rzeczywista właśnie miał wystąpił przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="3691a-176">hello runbook might connect tooGitHub toovalidate that a new commit had actually just occurred before continuing.</span></span>

## <a name="creating-a-webhook"></a><span data-ttu-id="3691a-177">Tworzenie elementu webhook</span><span class="sxs-lookup"><span data-stu-id="3691a-177">Creating a webhook</span></span>
<span data-ttu-id="3691a-178">Użyj hello następujące procedury toocreate nowy element runbook tooa połączonego elementu webhook w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3691a-178">Use hello following procedure toocreate a new webhook linked tooa runbook in hello Azure portal.</span></span>

1. <span data-ttu-id="3691a-179">Z hello **bloku elementów Runbook** w hello portalu Azure, kliknij przycisk runbook hello hello elementu webhook rozpocznie tooview bloku jej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="3691a-179">From hello **Runbooks blade** in hello Azure portal, click hello runbook that hello webhook will start tooview its detail blade.</span></span>
2. <span data-ttu-id="3691a-180">Kliknij przycisk **Webhook** u góry hello hello bloku tooopen hello **Dodawanie elementu Webhook** bloku.</span><span class="sxs-lookup"><span data-stu-id="3691a-180">Click **Webhook** at hello top of hello blade tooopen hello **Add Webhook** blade.</span></span> <br><span data-ttu-id="3691a-181">
   ![Przycisk elementów Webhook](media/automation-webhooks/webhooks-button.png)</span><span class="sxs-lookup"><span data-stu-id="3691a-181">
![Webhooks button](media/automation-webhooks/webhooks-button.png)</span></span>
3. <span data-ttu-id="3691a-182">Kliknij przycisk **tworzenia nowego elementu webhook** tooopen hello **bloku Utwórz elementu webhook**.</span><span class="sxs-lookup"><span data-stu-id="3691a-182">Click **Create new webhook** tooopen hello **Create webhook blade**.</span></span>
4. <span data-ttu-id="3691a-183">Określ **nazwa**, **Data wygaśnięcia** dla elementu webhook hello i określa, czy powinno być włączone.</span><span class="sxs-lookup"><span data-stu-id="3691a-183">Specify a **Name**, **Expiration Date** for hello webhook and whether it should be enabled.</span></span> <span data-ttu-id="3691a-184">Zobacz [szczegóły elementu webhook](#details-of-a-webhook) Aby uzyskać więcej informacji tych właściwości.</span><span class="sxs-lookup"><span data-stu-id="3691a-184">See [Details of a webhook](#details-of-a-webhook) for more information these properties.</span></span>
5. <span data-ttu-id="3691a-185">Kliknij ikonę kopiowania hello i naciśnij klawisze Ctrl + C toocopy hello adres URL elementu webhook hello.</span><span class="sxs-lookup"><span data-stu-id="3691a-185">Click hello copy icon and press Ctrl+C toocopy hello URL of hello webhook.</span></span>  <span data-ttu-id="3691a-186">Następnie zapisz go w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="3691a-186">Then record it in a safe place.</span></span>  <span data-ttu-id="3691a-187">**Po utworzeniu elementu webhook hello hello adresu URL nie można pobrać ponownie.**</span><span class="sxs-lookup"><span data-stu-id="3691a-187">**Once you create hello webhook, you cannot retrieve hello URL again.**</span></span> <br><span data-ttu-id="3691a-188">
   ![Adres URL elementu Webhook](media/automation-webhooks/copy-webhook-url.png)</span><span class="sxs-lookup"><span data-stu-id="3691a-188">
![Webhook URL](media/automation-webhooks/copy-webhook-url.png)</span></span>
6. <span data-ttu-id="3691a-189">Kliknij przycisk **parametry** tooprovide wartości parametrów elementu runbook hello.</span><span class="sxs-lookup"><span data-stu-id="3691a-189">Click **Parameters** tooprovide values for hello runbook parameters.</span></span>  <span data-ttu-id="3691a-190">Jeśli hello runbook ma parametry obowiązkowe, następnie nie będzie możliwe toocreate hello webhook ile wartości.</span><span class="sxs-lookup"><span data-stu-id="3691a-190">If hello runbook has mandatory parameters, then you will not be able toocreate hello webhook unless values are provided.</span></span>
7. <span data-ttu-id="3691a-191">Kliknij przycisk **Utwórz** toocreate hello webhook.</span><span class="sxs-lookup"><span data-stu-id="3691a-191">Click **Create** toocreate hello webhook.</span></span>

## <a name="using-a-webhook"></a><span data-ttu-id="3691a-192">Przy użyciu elementu webhook</span><span class="sxs-lookup"><span data-stu-id="3691a-192">Using a webhook</span></span>
<span data-ttu-id="3691a-193">toouse elementu webhook po jego utworzeniu aplikacji klienta należy wygenerować HTTP POST z adresem URL hello hello elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="3691a-193">toouse a webhook after it has been created, your client application must issue an HTTP POST with hello URL for hello webhook.</span></span>  <span data-ttu-id="3691a-194">Składnia elementu webhook hello Hello będą hello zgodny z formatem.</span><span class="sxs-lookup"><span data-stu-id="3691a-194">hello syntax of hello webhook will be in hello following format.</span></span>

    http://<Webhook Server>/token?=<Token Value>

<span data-ttu-id="3691a-195">powitania klienta zostanie wyświetlony jeden z poniższych kody powrotu z żądania POST hello hello.</span><span class="sxs-lookup"><span data-stu-id="3691a-195">hello client will receive one of hello following return codes from hello POST request.</span></span>  

| <span data-ttu-id="3691a-196">Kod</span><span class="sxs-lookup"><span data-stu-id="3691a-196">Code</span></span> | <span data-ttu-id="3691a-197">Tekst</span><span class="sxs-lookup"><span data-stu-id="3691a-197">Text</span></span> | <span data-ttu-id="3691a-198">Opis</span><span class="sxs-lookup"><span data-stu-id="3691a-198">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3691a-199">202</span><span class="sxs-lookup"><span data-stu-id="3691a-199">202</span></span> |<span data-ttu-id="3691a-200">Zaakceptowane</span><span class="sxs-lookup"><span data-stu-id="3691a-200">Accepted</span></span> |<span data-ttu-id="3691a-201">Witaj żądanie zostało zaakceptowane, a hello runbook pomyślnie zostało umieszczone w kolejce.</span><span class="sxs-lookup"><span data-stu-id="3691a-201">hello request was accepted, and hello runbook was successfully queued.</span></span> |
| <span data-ttu-id="3691a-202">400</span><span class="sxs-lookup"><span data-stu-id="3691a-202">400</span></span> |<span data-ttu-id="3691a-203">Nieprawidłowe żądanie</span><span class="sxs-lookup"><span data-stu-id="3691a-203">Bad Request</span></span> |<span data-ttu-id="3691a-204">Nie zaakceptowano żądanie Hello jednego hello z następujących powodów.</span><span class="sxs-lookup"><span data-stu-id="3691a-204">hello request was not accepted for one of hello following reasons.</span></span> <ul> <li><span data-ttu-id="3691a-205">Witaj webhook wygasł.</span><span class="sxs-lookup"><span data-stu-id="3691a-205">hello webhook has expired.</span></span></li> <li><span data-ttu-id="3691a-206">Element webhook Hello jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="3691a-206">hello webhook is disabled.</span></span></li> <li><span data-ttu-id="3691a-207">token Hello w adresie URL hello jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="3691a-207">hello token in hello URL is invalid.</span></span></li>  </ul> |
| <span data-ttu-id="3691a-208">404</span><span class="sxs-lookup"><span data-stu-id="3691a-208">404</span></span> |<span data-ttu-id="3691a-209">Nie można odnaleźć</span><span class="sxs-lookup"><span data-stu-id="3691a-209">Not Found</span></span> |<span data-ttu-id="3691a-210">Nie zaakceptowano żądanie Hello jednego hello z następujących powodów.</span><span class="sxs-lookup"><span data-stu-id="3691a-210">hello request was not accepted for one of hello following reasons.</span></span> <ul> <li><span data-ttu-id="3691a-211">Nie można odnaleźć elementu webhook Hello.</span><span class="sxs-lookup"><span data-stu-id="3691a-211">hello webhook was not found.</span></span></li> <li><span data-ttu-id="3691a-212">Nie znaleziono elementu runbook Hello.</span><span class="sxs-lookup"><span data-stu-id="3691a-212">hello runbook was not found.</span></span></li> <li><span data-ttu-id="3691a-213">Nie znaleziono konta Hello.</span><span class="sxs-lookup"><span data-stu-id="3691a-213">hello account was not found.</span></span></li>  </ul> |
| <span data-ttu-id="3691a-214">500</span><span class="sxs-lookup"><span data-stu-id="3691a-214">500</span></span> |<span data-ttu-id="3691a-215">Wewnętrzny błąd serwera</span><span class="sxs-lookup"><span data-stu-id="3691a-215">Internal Server Error</span></span> |<span data-ttu-id="3691a-216">adres URL Hello jest prawidłowy, ale wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="3691a-216">hello URL was valid, but an error occurred.</span></span>  <span data-ttu-id="3691a-217">Prześlij żądanie hello.</span><span class="sxs-lookup"><span data-stu-id="3691a-217">Please resubmit hello request.</span></span> |

<span data-ttu-id="3691a-218">Przy założeniu, że Żądanie hello zakończy się pomyślnie, odpowiedź hello elementu webhook zawiera hello identyfikator zadania w formacie JSON w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="3691a-218">Assuming hello request is successful, hello webhook response contains hello job id in JSON format as follows.</span></span> <span data-ttu-id="3691a-219">Będzie zawierać identyfikator pojedyncze zadanie, ale umożliwia formatu JSON hello potencjalne przyszłe ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="3691a-219">It will contain a single job id, but hello JSON format allows for potential future enhancements.</span></span>

    {"JobIds":["<JobId>"]}  

<span data-ttu-id="3691a-220">Po zakończeniu wykonywania hello zadanie elementu runbook lub jego stanie ukończenia z elementu webhook hello, nie można ustalić powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="3691a-220">hello client cannot determine when hello runbook job completes or its completion status from hello webhook.</span></span>  <span data-ttu-id="3691a-221">Można określić te informacje przy użyciu identyfikatora zadania hello z innej metody takie jak [programu Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) lub hello [interfejsu API usługi Automatyzacja Azure](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span><span class="sxs-lookup"><span data-stu-id="3691a-221">It can determine this information using hello job id with another method such as [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) or hello [Azure Automation API](https://msdn.microsoft.com/library/azure/mt163826.aspx).</span></span>

### <a name="example"></a><span data-ttu-id="3691a-222">Przykład</span><span class="sxs-lookup"><span data-stu-id="3691a-222">Example</span></span>
<span data-ttu-id="3691a-223">Poniższy przykład Hello używa środowiska Windows PowerShell toostart elementu runbook z elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="3691a-223">hello following example uses Windows PowerShell toostart a runbook with a webhook.</span></span>  <span data-ttu-id="3691a-224">Można użyć dowolnego języka, który może zgłaszać żądania HTTP elementu webhook; Środowisko Windows PowerShell jest używany po prostu poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="3691a-224">Note that any language that can make an HTTP request can use a webhook; Windows PowerShell is just used here as an example.</span></span>

<span data-ttu-id="3691a-225">Hello runbook oczekuje listę zapisany w formacie JSON w treści żądania hello hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="3691a-225">hello runbook is expecting a list of virtual machines formatted in JSON in hello body of hello request.</span></span> <span data-ttu-id="3691a-226">Możemy również są wraz z informacjami dotyczącymi który uruchamia hello runbook oraz hello Data i godzina się, że jest uruchamiana w nagłówku hello hello żądania.</span><span class="sxs-lookup"><span data-stu-id="3691a-226">We also are including information about who is starting hello runbook and hello date and time it is being started in hello header of hello request.</span></span>      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


<span data-ttu-id="3691a-227">Witaj poniższy obraz przedstawia informacje o nagłówku hello (przy użyciu [Fiddler](http://www.telerik.com/fiddler) śledzenia) z tego żądania.</span><span class="sxs-lookup"><span data-stu-id="3691a-227">hello following image shows hello header information (using a [Fiddler](http://www.telerik.com/fiddler) trace) from this request.</span></span> <span data-ttu-id="3691a-228">Obejmuje standardowych nagłówków żądania HTTP w toohello dodanie niestandardowa data i z nagłówków, które dodano.</span><span class="sxs-lookup"><span data-stu-id="3691a-228">This includes standard headers of an HTTP request in addition toohello custom Date and From headers that we added.</span></span>  <span data-ttu-id="3691a-229">Każdy z tych wartości jest runbook toohello dostępne w hello **RequestHeaders** właściwość **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="3691a-229">Each of these values is available toohello runbook in hello **RequestHeaders** property of **WebhookData**.</span></span>

![Przycisk elementów Webhook](media/automation-webhooks/webhook-request-headers.png)

<span data-ttu-id="3691a-231">Witaj poniższy obraz przedstawia hello treści żądania hello (przy użyciu [Fiddler](http://www.telerik.com/fiddler) śledzenia) czyli dostępne toohello runbook w programie hello **RequestBody** właściwość **WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="3691a-231">hello following image shows hello body of hello request (using a [Fiddler](http://www.telerik.com/fiddler) trace)  that is available toohello runbook in hello **RequestBody** property of **WebhookData**.</span></span> <span data-ttu-id="3691a-232">To jest w formacie JSON powodu hello formatu, który został uwzględniony w treści hello hello żądania.</span><span class="sxs-lookup"><span data-stu-id="3691a-232">This is formatted as JSON because that was hello format that was included in hello body of hello request.</span></span>     

![Przycisk elementów Webhook](media/automation-webhooks/webhook-request-body.png)

<span data-ttu-id="3691a-234">Witaj poniższy obraz przedstawia hello żądania wysyłane z programu Windows PowerShell i hello wynikowy odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="3691a-234">hello following image shows hello request being sent from Windows PowerShell and hello resulting response.</span></span>  <span data-ttu-id="3691a-235">Identyfikator zadania Hello jest wyodrębniana z hello odpowiedzi i tooa skonwertowany ciąg.</span><span class="sxs-lookup"><span data-stu-id="3691a-235">hello job id is extracted from hello response and converted tooa string.</span></span>

![Przycisk elementów Webhook](media/automation-webhooks/webhook-request-response.png)

<span data-ttu-id="3691a-237">Witaj następujący przykładowy element runbook akceptuje hello poprzednie przykładowe żądanie i uruchamia określony w treści żądania hello maszyn wirtualnych hello.</span><span class="sxs-lookup"><span data-stu-id="3691a-237">hello following sample runbook accepts hello previous example request and starts hello virtual machines specified in hello request body.</span></span>

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

            # Authenticate tooAzure resources
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
            Write-Error "Runbook mean toobe started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-tooazure-alerts"></a><span data-ttu-id="3691a-238">Uruchamianie elementów runbook w odpowiedzi tooAzure alertów</span><span class="sxs-lookup"><span data-stu-id="3691a-238">Starting runbooks in response tooAzure alerts</span></span>
<span data-ttu-id="3691a-239">Włączone elementu Webhook elementów runbook mogą być używane tooreact zbyt[Azure alerty](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="3691a-239">Webhook-enabled runbooks can be used tooreact too[Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="3691a-240">Zasobami na platformie Azure mogą być monitorowane przez zbieranie statystyk hello, takich jak wydajności, dostępności i użyciu za pomocą hello Azure alertów.</span><span class="sxs-lookup"><span data-stu-id="3691a-240">Resources in Azure can be monitored by collecting hello statistics like performance, availability and usage with hello help of Azure alerts.</span></span> <span data-ttu-id="3691a-241">Otrzymasz alert w oparciu metryki monitorowania lub zdarzenia dla zasobów platformy Azure, obecnie kont automatyzacji obsługuje tylko metryki.</span><span class="sxs-lookup"><span data-stu-id="3691a-241">You can receive an alert based on monitoring metrics or events for your Azure resources, currently Automation Accounts support only metrics.</span></span> <span data-ttu-id="3691a-242">Gdy wartość hello określonej metryki przekracza próg hello przypisane lub jeśli hello skonfigurowane zdarzenie zostanie wyzwolone powiadomienie jest wysyłane toohello usługi administratora lub współadministratorzy tooresolve hello alertu, aby uzyskać więcej informacji na temat metryki i zdarzenia można znaleźć zbyt[ Alerty Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="3691a-242">When hello value of a specified metric exceeds hello threshold assigned or if hello configured event is triggered then a notification is sent toohello service admin or co-admins tooresolve hello alert, for more information on metrics and events please refer too[Azure alerts](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="3691a-243">Oprócz za pomocą usługi Azure alerty jako system powiadomień, należy również rozpocząć się poza elementów runbook w tooalerts odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="3691a-243">Besides using Azure alerts as a notification system, you can also kick off runbooks in response tooalerts.</span></span> <span data-ttu-id="3691a-244">Automatyzacja Azure udostępnia hello możliwości toorun włączone elementu webhook elementów runbook z alertami platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3691a-244">Azure Automation provides hello capability toorun webhook-enabled runbooks with Azure alerts.</span></span> <span data-ttu-id="3691a-245">Gdy przekracza metrykę hello skonfigurowany wartość progowa reguły alertu hello staje się aktywny i wyzwalaczy hello webhook usługi Automatyzacja, który z kolei wykonuje hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="3691a-245">When a metric exceeds hello configured threshold value then hello alert rule becomes active and triggers hello automation webhook which in turn executes hello runbook.</span></span>

![elementów webhook](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a><span data-ttu-id="3691a-247">Kontekst alertu</span><span class="sxs-lookup"><span data-stu-id="3691a-247">Alert context</span></span>
<span data-ttu-id="3691a-248">Należy rozważyć zasobów platformy Azure, takich jak maszyny wirtualnej, użycie procesora CPU tego komputera jest jednym z hello metryki wydajności.</span><span class="sxs-lookup"><span data-stu-id="3691a-248">Consider an Azure resource such as a virtual machine, CPU utilization of this machine is one of hello key performance metric.</span></span> <span data-ttu-id="3691a-249">Jeśli hello wykorzystanie procesora CPU jest 100% lub po upływie pewnego przez długi czas, możesz toorestart hello maszyny wirtualnej toofix hello problem.</span><span class="sxs-lookup"><span data-stu-id="3691a-249">If hello CPU utilization is 100% or more than a certain amount for long period of time, you might want toorestart hello virtual machine toofix hello problem.</span></span> <span data-ttu-id="3691a-250">To będzie możliwe przez skonfigurowanie maszyny wirtualnej toohello reguły alertów i procent użycia procesora CPU, jako jego metryka ma ta reguła.</span><span class="sxs-lookup"><span data-stu-id="3691a-250">This can be solved by configuring an alert rule toohello virtual machine and this rule takes CPU percentage as its metric.</span></span> <span data-ttu-id="3691a-251">Procent użycia procesora CPU w tym miejscu jest po prostu wykonywanej na przykład, ale istnieje wiele innych metryk, że możesz skonfigurować tooyour Azure zasobów i ponowne uruchamianie maszyny wirtualnej hello jest akcja, która jest poświęcony toofix ten problem, hello tootake elementu runbook można skonfigurować inne akcje.</span><span class="sxs-lookup"><span data-stu-id="3691a-251">CPU percentage here is just taken as an example but there are many other metrics that you can configure tooyour Azure resources and restarting hello virtual machine is an action that is taken toofix this issue, you can configure hello runbook tootake other actions.</span></span>

<span data-ttu-id="3691a-252">Tę regułę alertów hello staje się aktywny i wyzwalaczy hello włączone elementu webhook elementu runbook, wysyła hello kontekst alertu toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="3691a-252">When this hello alert rule becomes active and triggers hello webhook-enabled runbook, it sends hello alert context toohello runbook.</span></span> <span data-ttu-id="3691a-253">[Kontekst alertu](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) zawiera szczegółowe informacje, łącznie z **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** i **sygnatury czasowej** jest wymagane dla hello runbook tooidentify hello zasobu na którym on być podejmowania działań.</span><span class="sxs-lookup"><span data-stu-id="3691a-253">[Alert context](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) contains details including **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** and **Timestamp** which are required for hello runbook tooidentify hello resource on which it will be taking action.</span></span> <span data-ttu-id="3691a-254">Alert kontekstu jest osadzony w części treści hello hello **WebhookData** obiektu wysłane toohello runbook i jest dostępny z **Webhook.RequestBody** właściwości</span><span class="sxs-lookup"><span data-stu-id="3691a-254">Alert context is embedded in hello body part of hello **WebhookData** object sent toohello runbook and it can be accessed with **Webhook.RequestBody** property</span></span>

### <a name="example"></a><span data-ttu-id="3691a-255">Przykład</span><span class="sxs-lookup"><span data-stu-id="3691a-255">Example</span></span>
<span data-ttu-id="3691a-256">Utwórz maszynę wirtualną platformy Azure w subskrypcji i powiąż [alertów Metryka procent toomonitor Procesora](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="3691a-256">Create an Azure virtual machine in your subscription and associate an [alert toomonitor CPU percentage metric](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span> <span data-ttu-id="3691a-257">Podczas tworzenia alertu hello upewnij się, że wypełnić pole elementu webhook hello z adresem URL elementu webhook hello, który został wygenerowany podczas tworzenia elementu webhook hello hello.</span><span class="sxs-lookup"><span data-stu-id="3691a-257">While creating hello alert make sure you populate hello webhook field with hello URL of hello webhook which was generated while creating hello webhook.</span></span>

<span data-ttu-id="3691a-258">Witaj następujący przykładowy element runbook jest wyzwalane, gdy reguły alertu hello staje się aktywny i zbiera hello parametrów kontekstu alertu, które są wymagane, na którym będzie biorąc pod akcji hello runbook tooidentify hello zasobu.</span><span class="sxs-lookup"><span data-stu-id="3691a-258">hello following sample runbook is triggered when hello alert rule becomes active and it collects hello Alert context parameters which are required for hello runbook tooidentify hello resource on which it will be taking action.</span></span>

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

            # Outputs information on hello webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain hello WebhookBody containing hello AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain hello AlertContext     
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

            # Act on hello AlertContext data, in our case restarting hello VM.
            # Authenticate tooyour Azure subscription using Organization ID toobe able toorestart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check hello status property of hello VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart hello VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant tooonly be started from a webhook."  
        }  
    }



## <a name="next-steps"></a><span data-ttu-id="3691a-259">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3691a-259">Next steps</span></span>
* <span data-ttu-id="3691a-260">Aby uzyskać więcej informacji na różne sposoby toostart elementu runbook, zobacz [uruchamianie elementu Runbook](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="3691a-260">For details on different ways toostart a runbook, see [Starting a Runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="3691a-261">Informacje dotyczące hello wyświetlanie stanu zadania elementu Runbook, można znaleźć zbyt[wykonanie elementu Runbook automatyzacji Azure](automation-runbook-execution.md).</span><span class="sxs-lookup"><span data-stu-id="3691a-261">For information on viewing hello Status of a Runbook Job, refer too[Runbook execution in Azure Automation](automation-runbook-execution.md).</span></span>
* <span data-ttu-id="3691a-262">toolearn toouse akcji tootake usługi Automatyzacja Azure alerty Azure, zobacz temat [skorygować alerty maszyny Wirtualnej Azure z elementu Runbook usługi automatyzacja](automation-azure-vm-alert-integration.md).</span><span class="sxs-lookup"><span data-stu-id="3691a-262">toolearn how toouse Azure Automation tootake action on Azure Alerts, see [Remediate Azure VM Alerts with Automation Runbooks](automation-azure-vm-alert-integration.md).</span></span>
