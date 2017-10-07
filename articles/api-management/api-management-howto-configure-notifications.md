---
title: "powiadomienia aaaConfigure i szablonów w usłudze Azure API Management wiadomości e-mail | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure powiadomienia i szablonów w usłudze Azure API Management wiadomości e-mail."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: ee25f26d-4752-433b-af9c-3817db38aed5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: dc23289c25a1641992b73cb955099b3f207b6968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-notifications-and-email-templates-in-azure-api-management"></a><span data-ttu-id="547b7-103">Jak tooconfigure powiadomienia i szablonów w usłudze Azure API Management wiadomości e-mail</span><span class="sxs-lookup"><span data-stu-id="547b7-103">How tooconfigure notifications and email templates in Azure API Management</span></span>
<span data-ttu-id="547b7-104">Zarządzanie interfejsami API umożliwia określenie hello tooconfigure powiadomienia dla określonych zdarzeń i tooconfigure hello e-mail szablonów, które są używane toocommunicate z hello Administratorzy i deweloperzy wystąpienia interfejsu API zarządzania.</span><span class="sxs-lookup"><span data-stu-id="547b7-104">API Management provides hello ability tooconfigure notifications for specific events, and tooconfigure hello email templates that are used toocommunicate with hello administrators and developers of an API Management instance.</span></span> <span data-ttu-id="547b7-105">W tym temacie pokazano, jak tooconfigure powiadomienia dla hello zdarzenia dostępne i zawiera omówienie konfigurowania hello szablonów wiadomości e-mail używany dla tych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="547b7-105">This topic shows how tooconfigure notifications for hello available events, and provides an overview of configuring hello email templates used for these events.</span></span>

## <span data-ttu-id="547b7-106"><a name="publisher-notifications"></a>Skonfigurować powiadomienia o wydawcy</span><span class="sxs-lookup"><span data-stu-id="547b7-106"><a name="publisher-notifications"> </a>Configure publisher notifications</span></span>
<span data-ttu-id="547b7-107">tooconfigure powiadomień, kliknij przycisk **portal wydawcy** w hello portalu Azure usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="547b7-107">tooconfigure notifications, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="547b7-108">Trwa toohello zarządzanie interfejsami API wydawcy portalu.</span><span class="sxs-lookup"><span data-stu-id="547b7-108">This takes you toohello API Management publisher portal.</span></span>

![Portal wydawcy][api-management-management-console]

> [!NOTE] 
> <span data-ttu-id="547b7-110">Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.</span><span class="sxs-lookup"><span data-stu-id="547b7-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

<span data-ttu-id="547b7-111">Kliknij przycisk **powiadomienia** z hello **zarządzanie interfejsami API** menu na powitania pozostałych tooview hello dostępnych powiadomień.</span><span class="sxs-lookup"><span data-stu-id="547b7-111">Click **Notifications** from hello **API Management** menu on hello left tooview hello available notifications.</span></span>

![Wydawcy powiadomień][api-management-publisher-notifications]

<span data-ttu-id="547b7-113">Witaj Poniższa lista zdarzeń można skonfigurować dla powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="547b7-113">hello following list of events can be configured for notifications.</span></span>

* <span data-ttu-id="547b7-114">**Żądania subskrypcji (wymaganie zatwierdzenia)** — Witaj adresatów wiadomości e-mail określonego i użytkownicy będą otrzymywać powiadomienia e-mail o żądaniach subskrypcji dla produktów interfejsu API, wymaganie zatwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="547b7-114">**Subscription requests (requiring approval)** - hello specified email recipients and users will receive email notifications about subscription requests for API products requiring approval.</span></span>
* <span data-ttu-id="547b7-115">**Nowe subskrypcje** — Witaj adresatów wiadomości e-mail określonego i użytkownicy będą otrzymywać powiadomienia e-mail o nowe subskrypcje produktu interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="547b7-115">**New subscriptions** - hello specified email recipients and users will receive email notifications about new API product subscriptions.</span></span>
* <span data-ttu-id="547b7-116">**Żądania galerii aplikacji** — Witaj adresatów wiadomości e-mail określonego i użytkownicy będą otrzymywać powiadomienia e-mail, gdy nowe aplikacje są przesłane toohello galerii aplikacji.</span><span class="sxs-lookup"><span data-stu-id="547b7-116">**Application gallery requests** - hello specified email recipients and users will receive email notifications when new applications are submitted toohello application gallery.</span></span>
* <span data-ttu-id="547b7-117">**UDW** — Witaj adresatów wiadomości e-mail określonego i użytkownicy będą otrzymywać wiadomości e-mail kopie z wszystkich wiadomości e-mail wysyłanych toodevelopers.</span><span class="sxs-lookup"><span data-stu-id="547b7-117">**BCC** - hello specified email recipients and users will receive email blind carbon copies of all emails sent toodevelopers.</span></span>
* <span data-ttu-id="547b7-118">**Nowy problem lub komentarz** — Witaj adresatów wiadomości e-mail określonego i użytkownicy będą otrzymywać powiadomienia e-mail, gdy nowy problem lub komentarz jest przesyłane na powitania portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="547b7-118">**New issue or comment** - hello specified email recipients and users will receive email notifications when a new issue or comment is submitted on hello developer portal.</span></span>
* <span data-ttu-id="547b7-119">**Komunikat zamknięcia konta** — Witaj adresatów wiadomości e-mail określonego i użytkownicy będą otrzymywać powiadomienia pocztą e-mail, po zamknięciu konta.</span><span class="sxs-lookup"><span data-stu-id="547b7-119">**Close account message** - hello specified email recipients and users will receive email notifications when an account is closed.</span></span>
* <span data-ttu-id="547b7-120">**Limit przydziału subskrypcji o** — Witaj następujących adresatów wiadomości e-mail, a użytkownicy otrzymają powiadomienia e-mail, gdy użycie subskrypcji pobiera przydział toousage Zamknij.</span><span class="sxs-lookup"><span data-stu-id="547b7-120">**Approaching subscription quota limit** - hello following email recipients and users will receive email notifications when subscription usage gets close toousage quota.</span></span>

<span data-ttu-id="547b7-121">Dla każdego zdarzenia można określić adresatów wiadomości e-mail przy użyciu pole tekstowe adresu e-mail hello lub użytkownicy mogą wybrać z listy.</span><span class="sxs-lookup"><span data-stu-id="547b7-121">For each event, you can specify email recipients using hello email address text box or you can select users from a list.</span></span>

<span data-ttu-id="547b7-122">toospecify hello e-mail adresy toobe powiadomienie, wprowadź je w polu tekstowym adres e-mail hello.</span><span class="sxs-lookup"><span data-stu-id="547b7-122">toospecify hello email addresses toobe notified, enter them in hello email address text box.</span></span> <span data-ttu-id="547b7-123">Jeśli masz wiele adresów e-mail, oddzielając je przecinkami.</span><span class="sxs-lookup"><span data-stu-id="547b7-123">If you have multiple email addresses, separate them using commas.</span></span>

![Adresatów powiadomień][api-management-email-addresses]

<span data-ttu-id="547b7-125">toobe użytkowników hello toospecify powiadomienie, kliknij przycisk **Dodaj adresata**hello pole obok toobe użytkowników hello powiadomienie wyboru i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="547b7-125">toospecify hello users toobe notified, click **add recipient**, check hello box beside hello users toobe notified, and click **OK**.</span></span>

> [!NOTE] 
> <span data-ttu-id="547b7-126">Tylko administratorzy są wyświetlane na liście hello.</span><span class="sxs-lookup"><span data-stu-id="547b7-126">Only administrators are displayed in hello list.</span></span>


<span data-ttu-id="547b7-127">Po skonfigurowaniu hello odbiorców powiadomień, kliknij przycisk **zapisać** tooapply hello zaktualizować odbiorców powiadomień.</span><span class="sxs-lookup"><span data-stu-id="547b7-127">After configuring hello notification recipients, click **Save** tooapply hello updated notification recipients.</span></span>

> [!NOTE] 
> <span data-ttu-id="547b7-128">Jeśli opuścisz hello **wydawcy powiadomień** portal wydawcy hello kartę alerty, jeśli istnieją niezapisane zmiany.</span><span class="sxs-lookup"><span data-stu-id="547b7-128">If you navigate away from hello **Publisher Notifications** tab hello publisher portal alerts you if there are unsaved changes.</span></span>


## <span data-ttu-id="547b7-129"><a name="email-templates"></a>Konfigurowanie szablonów wiadomości e-mail</span><span class="sxs-lookup"><span data-stu-id="547b7-129"><a name="email-templates"> </a>Configure email templates</span></span>
<span data-ttu-id="547b7-130">Zarządzanie interfejsami API udostępnia szablony wiadomości e-mail dla hello wiadomości e-mail, które są wysyłane w toku hello zarządzania i korzystania z usługi hello.</span><span class="sxs-lookup"><span data-stu-id="547b7-130">API Management provides email templates for hello email messages that are sent in hello course of administering and using hello service.</span></span> <span data-ttu-id="547b7-131">podano Hello następujące szablony wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="547b7-131">hello following email templates are provided.</span></span>

* <span data-ttu-id="547b7-132">Zatwierdzone przesyłanie galerii aplikacji</span><span class="sxs-lookup"><span data-stu-id="547b7-132">Application gallery submission approved</span></span>
* <span data-ttu-id="547b7-133">Litera farewell Developer</span><span class="sxs-lookup"><span data-stu-id="547b7-133">Developer farewell letter</span></span>
* <span data-ttu-id="547b7-134">Limit przydziału Developer zbliża się powiadomień</span><span class="sxs-lookup"><span data-stu-id="547b7-134">Developer quota limit approaching notification</span></span>
* <span data-ttu-id="547b7-135">Zaproś użytkownika</span><span class="sxs-lookup"><span data-stu-id="547b7-135">Invite user</span></span>
* <span data-ttu-id="547b7-136">Nowy komentarz dodany tooan problem</span><span class="sxs-lookup"><span data-stu-id="547b7-136">New comment added tooan issue</span></span>
* <span data-ttu-id="547b7-137">Nowy problem odebranych</span><span class="sxs-lookup"><span data-stu-id="547b7-137">New issue received</span></span>
* <span data-ttu-id="547b7-138">Nowa subskrypcja aktywowany</span><span class="sxs-lookup"><span data-stu-id="547b7-138">New subscription activated</span></span>
* <span data-ttu-id="547b7-139">Potwierdzenie odnowić subskrypcję</span><span class="sxs-lookup"><span data-stu-id="547b7-139">Subscription renewed confirmation</span></span>
* <span data-ttu-id="547b7-140">Odrzuci to żądanie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="547b7-140">Subscription request declines</span></span>
* <span data-ttu-id="547b7-141">Odebrano żądanie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="547b7-141">Subscription request received</span></span>

<span data-ttu-id="547b7-142">Te szablony mogą być modyfikowane pożądane.</span><span class="sxs-lookup"><span data-stu-id="547b7-142">These templates can be modified as desired.</span></span>

<span data-ttu-id="547b7-143">tooview i skonfigurować hello szablonów wiadomości e-mail dla swojego wystąpienia usługi API Management, kliknij **powiadomienia** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie wybierz hello **szablony wiadomości E-mail**  kartę.</span><span class="sxs-lookup"><span data-stu-id="547b7-143">tooview and configure hello email templates for your API Management instance, click **Notifications** from hello **API Management** menu on hello left, and select hello **Email Templates** tab.</span></span>

![Szablony wiadomości e-mail][api-management-email-templates]

<span data-ttu-id="547b7-145">tooview lub zmodyfikować szablon, wybierz ją z hello **szablony** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="547b7-145">tooview or modify a specific template, select it from hello **Templates** drop-down list.</span></span>

![Lista szablonów wiadomości e-mail][api-management-email-templates-list]

<span data-ttu-id="547b7-147">Każdy szablon wiadomości e-mail ma podmiotu w postaci zwykłego tekstu i definicji treści w formacie HTML.</span><span class="sxs-lookup"><span data-stu-id="547b7-147">Each email template has a subject in plain text, and a body definition in HTML format.</span></span> <span data-ttu-id="547b7-148">Każdy element można dostosować pożądane.</span><span class="sxs-lookup"><span data-stu-id="547b7-148">Each item can be customized as desired.</span></span>

![Edytor szablonu wiadomości e-mail][api-management-email-template]

<span data-ttu-id="547b7-150">Witaj **parametry** lista zawiera listę parametrów, służący do hello tematu ani treści, będzie wartość zastąpionego Witaj wyznaczone, po wysłaniu wiadomości e-mail hello.</span><span class="sxs-lookup"><span data-stu-id="547b7-150">hello **Parameters** list contains a list of parameters, which when inserted into hello subject or body, will be replaced hello designated value when hello email is sent.</span></span> <span data-ttu-id="547b7-151">tooinsert parametr, umieść kursor hello, której chcesz hello toogo parametru, a następnie kliknij hello Strzałka toohello po lewej stronie powitania parametru nazwy.</span><span class="sxs-lookup"><span data-stu-id="547b7-151">tooinsert a parameter, place hello cursor where you wish hello parameter toogo, and click hello arrow toohello left of hello parameter name.</span></span>

<span data-ttu-id="547b7-152">Kliknij przycisk **Podgląd** lub **wysłać teście** toosee jak hello poczty e-mail będzie wyglądać lub Wyślij testową wiadomość e-mail.</span><span class="sxs-lookup"><span data-stu-id="547b7-152">Click **Preview** or **Send a test** toosee how hello email will look or send a test email.</span></span>

> [!NOTE] 
> <span data-ttu-id="547b7-153">Parametry Hello nie są zastępowane rzeczywistymi wartościami podczas przeglądania lub wysyłanie testu.</span><span class="sxs-lookup"><span data-stu-id="547b7-153">hello parameters are not replaced with actual values when previewing or sending a test.</span></span>

<span data-ttu-id="547b7-154">toohello szablon wiadomości e-mail toosave hello zmiany, kliknij przycisk **Zapisz**, lub kliknij przycisk zmiany hello toocancel **anulować**.</span><span class="sxs-lookup"><span data-stu-id="547b7-154">toosave hello changes toohello email template, click **Save**, or toocancel hello changes click **Cancel**.</span></span>
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
