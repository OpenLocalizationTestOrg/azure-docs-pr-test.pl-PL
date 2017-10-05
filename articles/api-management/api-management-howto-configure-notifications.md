---
title: "Konfigurowanie powiadomień i szablonów w usłudze Azure API Management wiadomości e-mail | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować powiadomienia i szablonów w usłudze Azure API Management wiadomości e-mail."
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
ms.openlocfilehash: 3d8b74e32059cfc1a4c3a8fc7d3bd04676ee80c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-notifications-and-email-templates-in-azure-api-management"></a><span data-ttu-id="920fc-103">How to configure notifications and email templates in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="920fc-103">How to configure notifications and email templates in Azure API Management</span></span>
<span data-ttu-id="920fc-104">Zarządzanie interfejsami API pozwala, aby skonfigurować powiadomienia dla określonych zdarzeń i konfigurowania szablonów wiadomości e-mail, które są używane do komunikacji z Administratorzy i deweloperzy wystąpienia interfejsu API zarządzania.</span><span class="sxs-lookup"><span data-stu-id="920fc-104">API Management provides the ability to configure notifications for specific events, and to configure the email templates that are used to communicate with the administrators and developers of an API Management instance.</span></span> <span data-ttu-id="920fc-105">W tym temacie pokazano, jak skonfigurować powiadomienia o zdarzeniach dostępny i zawiera omówienie konfigurowania szablonów wiadomości e-mail używany dla tych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="920fc-105">This topic shows how to configure notifications for the available events, and provides an overview of configuring the email templates used for these events.</span></span>

## <span data-ttu-id="920fc-106"><a name="publisher-notifications"></a>Skonfigurować powiadomienia o wydawcy</span><span class="sxs-lookup"><span data-stu-id="920fc-106"><a name="publisher-notifications"> </a>Configure publisher notifications</span></span>
<span data-ttu-id="920fc-107">Kliknij, aby skonfigurować powiadomienia **portal wydawcy** w portalu Azure usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="920fc-107">To configure notifications, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="920fc-108">Spowoduje to przejście do portalu wydawcy usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="920fc-108">This takes you to the API Management publisher portal.</span></span>

![Portal wydawcy][api-management-management-console]

> [!NOTE] 
> <span data-ttu-id="920fc-110">Jeśli jeszcze nie masz utworzonego wystąpienia usługi API Management, zobacz [Tworzenie wystąpienia usługi API Management][Create an API Management service instance] w samouczku [Wprowadzenie do usługi Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="920fc-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

<span data-ttu-id="920fc-111">Kliknij przycisk **powiadomienia** z **zarządzanie interfejsami API** menu po lewej stronie, aby wyświetlić dostępnych powiadomień.</span><span class="sxs-lookup"><span data-stu-id="920fc-111">Click **Notifications** from the **API Management** menu on the left to view the available notifications.</span></span>

![Wydawcy powiadomień][api-management-publisher-notifications]

<span data-ttu-id="920fc-113">Poniższa lista zdarzeń można skonfigurować dla powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="920fc-113">The following list of events can be configured for notifications.</span></span>

* <span data-ttu-id="920fc-114">**Żądania subskrypcji (wymaganie zatwierdzenia)** -adresatów wiadomości e-mail określonego i użytkowników będzie otrzymywał powiadomienia e-mail o żądaniach subskrypcji dla produktów interfejsu API, wymaganie zatwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="920fc-114">**Subscription requests (requiring approval)** - The specified email recipients and users will receive email notifications about subscription requests for API products requiring approval.</span></span>
* <span data-ttu-id="920fc-115">**Nowe subskrypcje** -adresatów wiadomości e-mail określonego i użytkowników będzie otrzymywał powiadomienia e-mail o nowe subskrypcje produktu interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="920fc-115">**New subscriptions** - The specified email recipients and users will receive email notifications about new API product subscriptions.</span></span>
* <span data-ttu-id="920fc-116">**Żądania galerii aplikacji** -adresatów wiadomości e-mail określonego i użytkowników będzie otrzymywał powiadomienia e-mail, gdy nowe aplikacje są przesyłane do galerii aplikacji.</span><span class="sxs-lookup"><span data-stu-id="920fc-116">**Application gallery requests** - The specified email recipients and users will receive email notifications when new applications are submitted to the application gallery.</span></span>
* <span data-ttu-id="920fc-117">**UDW** -adresatów wiadomości e-mail określonego i użytkownicy otrzymają wiadomość e-mail kopie wszystkich wiadomości e-mail wysyłanych do deweloperów.</span><span class="sxs-lookup"><span data-stu-id="920fc-117">**BCC** - The specified email recipients and users will receive email blind carbon copies of all emails sent to developers.</span></span>
* <span data-ttu-id="920fc-118">**Nowy problem lub komentarz** — adresatów wiadomości e-mail określonego i użytkownicy będą otrzymywać powiadomienia e-mail, gdy nowy problem lub komentarz jest przesyłany w portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="920fc-118">**New issue or comment** - The specified email recipients and users will receive email notifications when a new issue or comment is submitted on the developer portal.</span></span>
* <span data-ttu-id="920fc-119">**Komunikat zamknięcia konta** -adresatów wiadomości e-mail określony i użytkownicy będą otrzymywać powiadomienia e-mail, po zamknięciu konta.</span><span class="sxs-lookup"><span data-stu-id="920fc-119">**Close account message** - The specified email recipients and users will receive email notifications when an account is closed.</span></span>
* <span data-ttu-id="920fc-120">**Limit przydziału subskrypcji o** -następujących adresatów wiadomości e-mail i użytkowników będzie otrzymywał powiadomienia e-mail, gdy użycie subskrypcji pobiera możliwości wykorzystania przydziału użycia.</span><span class="sxs-lookup"><span data-stu-id="920fc-120">**Approaching subscription quota limit** - The following email recipients and users will receive email notifications when subscription usage gets close to usage quota.</span></span>

<span data-ttu-id="920fc-121">Dla każdego zdarzenia można określić adresatów wiadomości e-mail w polu tekstowym adres e-mail lub użytkownicy mogą wybrać z listy.</span><span class="sxs-lookup"><span data-stu-id="920fc-121">For each event, you can specify email recipients using the email address text box or you can select users from a list.</span></span>

<span data-ttu-id="920fc-122">Aby określić adresy e-mail, aby otrzymywać powiadomienia, wprowadź je w polu tekstowym adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="920fc-122">To specify the email addresses to be notified, enter them in the email address text box.</span></span> <span data-ttu-id="920fc-123">Jeśli masz wiele adresów e-mail, oddzielając je przecinkami.</span><span class="sxs-lookup"><span data-stu-id="920fc-123">If you have multiple email addresses, separate them using commas.</span></span>

![Adresatów powiadomień][api-management-email-addresses]

<span data-ttu-id="920fc-125">Aby określić należy powiadomić użytkowników, kliknij przycisk **Dodaj adresata**, zaznacz pole obok użytkowników, aby otrzymywać powiadomienia, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="920fc-125">To specify the users to be notified, click **add recipient**, check the box beside the users to be notified, and click **OK**.</span></span>

> [!NOTE] 
> <span data-ttu-id="920fc-126">Tylko administratorzy są wyświetlane na liście.</span><span class="sxs-lookup"><span data-stu-id="920fc-126">Only administrators are displayed in the list.</span></span>


<span data-ttu-id="920fc-127">Po skonfigurowaniu odbiorców powiadomień, kliknij przycisk **zapisać** dotyczyć odbiorców powiadomień zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="920fc-127">After configuring the notification recipients, click **Save** to apply the updated notification recipients.</span></span>

> [!NOTE] 
> <span data-ttu-id="920fc-128">Jeśli oddalisz się od **wydawcy powiadomień** kartę portalu wydawcy generuje alert, jeśli istnieją niezapisane zmiany.</span><span class="sxs-lookup"><span data-stu-id="920fc-128">If you navigate away from the **Publisher Notifications** tab the publisher portal alerts you if there are unsaved changes.</span></span>


## <span data-ttu-id="920fc-129"><a name="email-templates"></a>Konfigurowanie szablonów wiadomości e-mail</span><span class="sxs-lookup"><span data-stu-id="920fc-129"><a name="email-templates"> </a>Configure email templates</span></span>
<span data-ttu-id="920fc-130">Zarządzanie interfejsami API udostępnia szablony wiadomości e-mail dla wiadomości e-mail, które są wysyłane w ramach zarządzania i korzystania z usługi.</span><span class="sxs-lookup"><span data-stu-id="920fc-130">API Management provides email templates for the email messages that are sent in the course of administering and using the service.</span></span> <span data-ttu-id="920fc-131">Znajdują się następujące szablony wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="920fc-131">The following email templates are provided.</span></span>

* <span data-ttu-id="920fc-132">Zatwierdzone przesyłanie galerii aplikacji</span><span class="sxs-lookup"><span data-stu-id="920fc-132">Application gallery submission approved</span></span>
* <span data-ttu-id="920fc-133">Litera farewell Developer</span><span class="sxs-lookup"><span data-stu-id="920fc-133">Developer farewell letter</span></span>
* <span data-ttu-id="920fc-134">Limit przydziału Developer zbliża się powiadomień</span><span class="sxs-lookup"><span data-stu-id="920fc-134">Developer quota limit approaching notification</span></span>
* <span data-ttu-id="920fc-135">Zaproś użytkownika</span><span class="sxs-lookup"><span data-stu-id="920fc-135">Invite user</span></span>
* <span data-ttu-id="920fc-136">Nowy komentarz dodany do problemu</span><span class="sxs-lookup"><span data-stu-id="920fc-136">New comment added to an issue</span></span>
* <span data-ttu-id="920fc-137">Nowy problem odebranych</span><span class="sxs-lookup"><span data-stu-id="920fc-137">New issue received</span></span>
* <span data-ttu-id="920fc-138">Nowa subskrypcja aktywowany</span><span class="sxs-lookup"><span data-stu-id="920fc-138">New subscription activated</span></span>
* <span data-ttu-id="920fc-139">Potwierdzenie odnowić subskrypcję</span><span class="sxs-lookup"><span data-stu-id="920fc-139">Subscription renewed confirmation</span></span>
* <span data-ttu-id="920fc-140">Odrzuci to żądanie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="920fc-140">Subscription request declines</span></span>
* <span data-ttu-id="920fc-141">Odebrano żądanie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="920fc-141">Subscription request received</span></span>

<span data-ttu-id="920fc-142">Te szablony mogą być modyfikowane pożądane.</span><span class="sxs-lookup"><span data-stu-id="920fc-142">These templates can be modified as desired.</span></span>

<span data-ttu-id="920fc-143">Kliknij, aby wyświetlić i skonfigurować szablony wiadomości e-mail dla swojego wystąpienia usługi API Management **powiadomienia** z **zarządzanie interfejsami API** menu po lewej stronie, a następnie wybierz **szablony wiadomości E-mail**kartę.</span><span class="sxs-lookup"><span data-stu-id="920fc-143">To view and configure the email templates for your API Management instance, click **Notifications** from the **API Management** menu on the left, and select the **Email Templates** tab.</span></span>

![Szablony wiadomości e-mail][api-management-email-templates]

<span data-ttu-id="920fc-145">Aby wyświetlić lub zmodyfikować szablon, wybierz go z **szablony** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="920fc-145">To view or modify a specific template, select it from the **Templates** drop-down list.</span></span>

![Lista szablonów wiadomości e-mail][api-management-email-templates-list]

<span data-ttu-id="920fc-147">Każdy szablon wiadomości e-mail ma podmiotu w postaci zwykłego tekstu i definicji treści w formacie HTML.</span><span class="sxs-lookup"><span data-stu-id="920fc-147">Each email template has a subject in plain text, and a body definition in HTML format.</span></span> <span data-ttu-id="920fc-148">Każdy element można dostosować pożądane.</span><span class="sxs-lookup"><span data-stu-id="920fc-148">Each item can be customized as desired.</span></span>

![Edytor szablonu wiadomości e-mail][api-management-email-template]

<span data-ttu-id="920fc-150">**Parametry** lista zawiera listę parametrów, służący wstawione do tematu lub treści, zostanie zastąpiony wyznaczonej wartości, po wysłaniu wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="920fc-150">The **Parameters** list contains a list of parameters, which when inserted into the subject or body, will be replaced the designated value when the email is sent.</span></span> <span data-ttu-id="920fc-151">Aby wstawić parametru, umieść kursor, który mają parametr, aby przejść, a następnie kliknij przycisk strzałki w lewo nazwę parametru.</span><span class="sxs-lookup"><span data-stu-id="920fc-151">To insert a parameter, place the cursor where you wish the parameter to go, and click the arrow to the left of the parameter name.</span></span>

<span data-ttu-id="920fc-152">Kliknij przycisk **Podgląd** lub **wysłać teście** aby zobaczyć, jak wiadomości e-mail będą wyglądać lub Wyślij testową wiadomość e-mail.</span><span class="sxs-lookup"><span data-stu-id="920fc-152">Click **Preview** or **Send a test** to see how the email will look or send a test email.</span></span>

> [!NOTE] 
> <span data-ttu-id="920fc-153">Parametry nie są zastępowane rzeczywistymi wartościami podczas przeglądania lub wysyłanie testu.</span><span class="sxs-lookup"><span data-stu-id="920fc-153">The parameters are not replaced with actual values when previewing or sending a test.</span></span>

<span data-ttu-id="920fc-154">Aby zapisać zmiany szablonu wiadomości e-mail, kliknij polecenie **zapisać**, lub Anuluj zmiany kliknij **anulować**.</span><span class="sxs-lookup"><span data-stu-id="920fc-154">To save the changes to the email template, click **Save**, or to cancel the changes click **Cancel**.</span></span>
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
