---
title: "Zarządzanie dostępem do rozliczeń, za pomocą ról platformy Azure | Dokumentacja firmy Microsoft"
description: 
services: 
documentationcenter: 
author: vikramdesai01
manager: vikdesai
editor: 
tags: billing
ms.assetid: e4c4d136-2826-4938-868f-a7e67ff6b025
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: vikdesai
ms.openlocfilehash: c70904097f139bc2178feed83f1cf1274f3c738d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-access-to-billing-information-for-azure-using-role-based-access-control"></a><span data-ttu-id="6777a-102">Zarządzanie dostępem do informacji dotyczących rozliczeń dla platformy Azure przy użyciu kontroli dostępu opartej na rolach</span><span class="sxs-lookup"><span data-stu-id="6777a-102">Manage access to billing information for Azure using role-based access control</span></span>

<span data-ttu-id="6777a-103">Można przyznać dostęp do informacji dotyczących rozliczeń platformy Azure do członków zespołu przypisując jedną z następujących ról użytkownika do subskrypcji: konto administratora, administratora usługi, administratora współpracującego, właściciela, współautora, czytnika i rozliczeń czytnika.</span><span class="sxs-lookup"><span data-stu-id="6777a-103">You can grant access for Azure billing information to members of your team by assigning one of the following user roles to your subscription: Account Administrator, Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader.</span></span> <span data-ttu-id="6777a-104">Mają oni dostęp do informacji dotyczących rozliczeń w [portalu Azure](https://portal.azure.com/), oraz mogą używać [rozliczeń interfejsów API](billing-usage-rate-card-overview.md) programowo uzyskać faktury (raz nie zgłoszono — ruch przychodzący) i szczegóły użycia.</span><span class="sxs-lookup"><span data-stu-id="6777a-104">They would have access to billing information in the [Azure portal](https://portal.azure.com/), and they can use the [Billing APIs](billing-usage-rate-card-overview.md) to programmatically get invoices (once opted-in) and usage details.</span></span> <span data-ttu-id="6777a-105">Aby uzyskać więcej informacji o który Przyznaj ról, a role można zrobić, zobacz [role w programie Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="6777a-105">For more information about who can grant roles, and which roles can do what, see [Roles in Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span></span>

## <span data-ttu-id="6777a-106"><a name="opt-in"></a>Zezwolenie dodatkowym użytkownikom na dostęp do faktury</span><span class="sxs-lookup"><span data-stu-id="6777a-106"><a name="opt-in"></a> Allowing additional users to access invoices</span></span>

<span data-ttu-id="6777a-107">Administrator konta musi włączyć za pomocą [portalu Azure](https://portal.azure.com/) zezwolić na dostęp do faktury dla innych użytkowników, jak i za pomocą interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="6777a-107">The Account Administrator must opt in using the [Azure portal](https://portal.azure.com/) allow access to invoices for other users and via API.</span></span>

1. <span data-ttu-id="6777a-108">Jako administratora konta, wybierz subskrypcję z [bloku subskrypcje](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6777a-108">As the Account Administrator, select your subscription from the [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="6777a-109">Wybierz **faktury** , a następnie **dostęp do faktury**.</span><span class="sxs-lookup"><span data-stu-id="6777a-109">Select **Invoices** and then **Access to invoices**.</span></span>

    ![Zrzut ekranu pokazuje, jak delegować dostęp do faktury](./media/billing-manage-access/AA-optin.png)

1. <span data-ttu-id="6777a-111">Włącz **na** role, aby pobrać faktury zakres dostępu następuje zapisywania zmian, aby umożliwić użytkownikom w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6777a-111">Turn **On** the access followed by saving the changes, to allow users in subscription scoped roles to download invoice.</span></span>

    ![Zrzut ekranu przedstawia na — wyłączone na delegowany dostęp na potrzeby faktury](./media/billing-manage-access/AA-optinAllow.png)

<span data-ttu-id="6777a-113">Zgodzie na rozwiązanie umożliwia administratora usługi, administratora współpracującego właściciela, współautora, czytnika i rozliczeń czytnika na subskrypcję, aby pobierać faktury PDF w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6777a-113">Opting in allows Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader on the subscription to download PDF invoices in the Azure portal.</span></span> <span data-ttu-id="6777a-114">Jednak faktury starsze niż grudnia 2016 są dostępne tylko do konta administratora teraz.</span><span class="sxs-lookup"><span data-stu-id="6777a-114">However, invoices older than December 2016 are available only to the Account Administrator for now.</span></span>

<span data-ttu-id="6777a-115">Administrator konta można również skonfigurować mają faktury wysyłane za pośrednictwem poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="6777a-115">The Account Administrator can also configure to have invoices sent via email.</span></span> <span data-ttu-id="6777a-116">Aby dowiedzieć się więcej, zobacz [uzyskać potwierdzenia w wiadomości e-mail](billing-download-azure-invoice-daily-usage-date.md).</span><span class="sxs-lookup"><span data-stu-id="6777a-116">To learn more, see [Get your invoice in email](billing-download-azure-invoice-daily-usage-date.md).</span></span>

## <a name="adding-users-to-the-billing-reader-role"></a><span data-ttu-id="6777a-117">Dodawanie użytkowników do roli Czytelnik rozliczeń</span><span class="sxs-lookup"><span data-stu-id="6777a-117">Adding users to the Billing Reader role</span></span>

<span data-ttu-id="6777a-118">Rola rozliczeń czytnik ma dostęp tylko do odczytu do informacji dotyczących rozliczeń subskrypcję w portalu Azure i Brak dostępu do usług, takich jak konta magazynu i maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="6777a-118">The Billing Reader role has read-only access to subscription billing information in Azure portal, and no access to services such as VMs and storage accounts.</span></span> <span data-ttu-id="6777a-119">Przypisać rolę czytelnika rozliczeń osobie, która potrzebuje dostępu do informacji dotyczących rozliczeń subskrypcji, ale nie umożliwia zarządzanie usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="6777a-119">Assign the Billing Reader role to someone that needs access to the subscription billing information but not the ability to manage Azure services.</span></span> <span data-ttu-id="6777a-120">Ta rola jest odpowiednia dla użytkowników w organizacji, którzy finansowych i kosztów zarządzania należy wykonać tylko dla subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6777a-120">This role is appropriate for users in an organization who only perform financial and cost management for Azure subscriptions.</span></span>

1. <span data-ttu-id="6777a-121">Wybierz subskrypcję z [bloku subskrypcje](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6777a-121">Select your subscription from the [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="6777a-122">Wybierz **(IAM) kontroli dostępu** , a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="6777a-122">Select **Access control (IAM)** and then click **Add**.</span></span>

    ![Zrzut ekranu przedstawia IAM w bloku subskrypcji](./media/billing-manage-access/select-iam.PNG)

1. <span data-ttu-id="6777a-124">Wybierz **rozliczeń czytnika** w **wybierz rolę** strony.</span><span class="sxs-lookup"><span data-stu-id="6777a-124">Choose **Billing Reader** in the **Select a role** page.</span></span>

    ![Zrzut ekranu przedstawia rozliczeń czytnika w widoku menu podręczne](./media/billing-manage-access/select-roles.PNG)

1. <span data-ttu-id="6777a-126">Wpisz adres e-mail użytkownika, aby zaprosić, a następnie kliknij przycisk **OK** można wysłać zaproszenia.</span><span class="sxs-lookup"><span data-stu-id="6777a-126">Type the email for the user you want to invite, then click **OK** to send the invitation.</span></span>

    ![Zrzut ekranu pokazujący wprowadzenia wiadomości e-mail z zaproszeniem ktoś](./media/billing-manage-access/add-user.PNG)

1. <span data-ttu-id="6777a-128">Wykonaj instrukcje w wiadomości e-mail zaproszenia, aby zalogować się jako czytnik rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="6777a-128">Follow instructions in the invite email to log in as a Billing Reader.</span></span>

    ![Zrzut ekranu pokazujący jakie dane może wyświetlać czytnika rozliczeń w portalu Azure](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> <span data-ttu-id="6777a-130">Funkcja rozliczeń czytnik jest w wersji zapoznawczej i jeszcze nie obsługuje subskrypcji enterprise (EA) lub nieglobalna chmury.</span><span class="sxs-lookup"><span data-stu-id="6777a-130">The Billing Reader feature is in preview, and does not yet support enterprise (EA) subscriptions or non-global clouds.</span></span>

## <a name="adding-users-to-other-roles"></a><span data-ttu-id="6777a-131">Dodawanie użytkowników do innych ról</span><span class="sxs-lookup"><span data-stu-id="6777a-131">Adding users to other roles</span></span>

<span data-ttu-id="6777a-132">Dostęp użytkownicy w innych ról, takich jak właścicielem lub współautorem, nie tylko rozliczeniowymi, ale również usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6777a-132">Users in other roles, such as Owner or Contributor, can access not just billing information, but Azure services as well.</span></span> <span data-ttu-id="6777a-133">Aby zarządzać tymi rolami, zobacz [Dodawanie lub zmienianie ról administrator usługi Azure, które zarządzają subskrypcji lub usługi](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="6777a-133">To manage these roles, see [Add or change Azure administrator roles that manage the subscription or services](billing-add-change-azure-subscription-administrator.md).</span></span>

## <a name="who-can-access-the-account-centerhttpsaccountwindowsazurecom"></a><span data-ttu-id="6777a-134">Kto ma dostęp do [Centrum konta](https://account.windowsazure.com)?</span><span class="sxs-lookup"><span data-stu-id="6777a-134">Who can access the [Account Center](https://account.windowsazure.com)?</span></span>

<span data-ttu-id="6777a-135">Tylko Administrator konta może zalogować się do Centrum konta.</span><span class="sxs-lookup"><span data-stu-id="6777a-135">Only the Account Administrator can log in to the Account center.</span></span> <span data-ttu-id="6777a-136">Administrator konta jest prawnym właścicielem subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6777a-136">The Account Administrator is the legal owner of the subscription.</span></span> <span data-ttu-id="6777a-137">Domyślnie osoba, która utworzył konto na lub zakupiono subskrypcję platformy Azure jest administratorem konta, chyba że [przeniesienia własności subskrypcji](billing-subscription-transfer.md) do innej osoby.</span><span class="sxs-lookup"><span data-stu-id="6777a-137">By default, the person who signed up for or bought the Azure subscription is the Account Administrator, unless the [subscription ownership was transferred](billing-subscription-transfer.md) to somebody else.</span></span> <span data-ttu-id="6777a-138">Administrator konta można tworzyć subskrypcje, anulowanie subskrypcji, zmienić adres do rozliczeń dla subskrypcji i zarządzanie zasadami dostępu dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6777a-138">The Account Administrator can create subscriptions, cancel subscriptions, change the billing address for a subscription, and manage access policies for the subscription.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="6777a-139">Potrzebujesz pomocy?</span><span class="sxs-lookup"><span data-stu-id="6777a-139">Need help?</span></span> <span data-ttu-id="6777a-140">Skontaktuj się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="6777a-140">Contact support.</span></span>

<span data-ttu-id="6777a-141">Jeśli masz więcej pytań, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) uzyskać szybkie rozwiązanie problemu.</span><span class="sxs-lookup"><span data-stu-id="6777a-141">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>
