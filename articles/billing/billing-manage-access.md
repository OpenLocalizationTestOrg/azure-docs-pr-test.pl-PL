---
title: "tooAzure dostępu aaaManage rozliczeń, za pomocą ról | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 5937fac5ffa5ca204eb03a1dcbc5e800b3d5eb74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-toobilling-information-for-azure-using-role-based-access-control"></a><span data-ttu-id="73d82-102">Zarządzanie informacjami o toobilling dostępu na platformie Azure przy użyciu kontroli dostępu opartej na rolach</span><span class="sxs-lookup"><span data-stu-id="73d82-102">Manage access toobilling information for Azure using role-based access control</span></span>

<span data-ttu-id="73d82-103">Przypisując jedną powitania po subskrypcji tooyour ról użytkowników można przyznać dostęp dla platformy Azure rozliczeń toomembers informacji zespołu: konto administratora, administratora usługi, administratora współpracującego, właściciela, współautora, czytnika i rozliczeń czytnika.</span><span class="sxs-lookup"><span data-stu-id="73d82-103">You can grant access for Azure billing information toomembers of your team by assigning one of hello following user roles tooyour subscription: Account Administrator, Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader.</span></span> <span data-ttu-id="73d82-104">Mają oni dostęp do informacji toobilling w hello [portalu Azure](https://portal.azure.com/), oraz mogą używać hello [rozliczeń interfejsów API](billing-usage-rate-card-overview.md) tooprogrammatically uzyskać faktury (raz nie zgłoszono — ruch przychodzący) i szczegóły użycia.</span><span class="sxs-lookup"><span data-stu-id="73d82-104">They would have access toobilling information in hello [Azure portal](https://portal.azure.com/), and they can use hello [Billing APIs](billing-usage-rate-card-overview.md) tooprogrammatically get invoices (once opted-in) and usage details.</span></span> <span data-ttu-id="73d82-105">Aby uzyskać więcej informacji o który Przyznaj ról, a role można zrobić, zobacz [role w programie Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="73d82-105">For more information about who can grant roles, and which roles can do what, see [Roles in Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span></span>

## <span data-ttu-id="73d82-106"><a name="opt-in"></a>Stosowanie dodatkowych użytkowników tooaccess faktury</span><span class="sxs-lookup"><span data-stu-id="73d82-106"><a name="opt-in"></a> Allowing additional users tooaccess invoices</span></span>

<span data-ttu-id="73d82-107">Witaj konto administratora musi włączyć przy użyciu hello [portalu Azure](https://portal.azure.com/) Zezwalaj tooinvoices dostęp inni użytkownicy i za pomocą interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="73d82-107">hello Account Administrator must opt in using hello [Azure portal](https://portal.azure.com/) allow access tooinvoices for other users and via API.</span></span>

1. <span data-ttu-id="73d82-108">Witaj administratora konta, wybierz subskrypcję z hello [bloku subskrypcje](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="73d82-108">As hello Account Administrator, select your subscription from hello [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="73d82-109">Wybierz **faktury** , a następnie **dostępu tooinvoices**.</span><span class="sxs-lookup"><span data-stu-id="73d82-109">Select **Invoices** and then **Access tooinvoices**.</span></span>

    ![Zrzut ekranu pokazuje, jak toodelegate dostępu tooinvoices](./media/billing-manage-access/AA-optin.png)

1. <span data-ttu-id="73d82-111">Włącz **na** dostępu hello następuje zapisywania zmian hello, użytkownicy tooallow fakturze toodownload zakresie ról subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="73d82-111">Turn **On** hello access followed by saving hello changes, tooallow users in subscription scoped roles toodownload invoice.</span></span>

    ![Zrzut ekranu przedstawia tooinvoice dostępu toodelegate — wyłączone](./media/billing-manage-access/AA-optinAllow.png)

<span data-ttu-id="73d82-113">Zgodzie na rozwiązanie umożliwia administratora usługi, administratora współpracującego właściciela, współautora, czytnika i rozliczeń czytnika na powitania subskrypcji toodownload PDF faktury w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="73d82-113">Opting in allows Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader on hello subscription toodownload PDF invoices in hello Azure portal.</span></span> <span data-ttu-id="73d82-114">Faktury starsze niż grudnia 2016 są jednak dostępne toohello tylko Administrator konta teraz.</span><span class="sxs-lookup"><span data-stu-id="73d82-114">However, invoices older than December 2016 are available only toohello Account Administrator for now.</span></span>

<span data-ttu-id="73d82-115">Witaj administratora konta można również skonfigurować faktury toohave wysyłane za pośrednictwem poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="73d82-115">hello Account Administrator can also configure toohave invoices sent via email.</span></span> <span data-ttu-id="73d82-116">toolearn więcej, zobacz [uzyskać potwierdzenia w wiadomości e-mail](billing-download-azure-invoice-daily-usage-date.md).</span><span class="sxs-lookup"><span data-stu-id="73d82-116">toolearn more, see [Get your invoice in email](billing-download-azure-invoice-daily-usage-date.md).</span></span>

## <a name="adding-users-toohello-billing-reader-role"></a><span data-ttu-id="73d82-117">Dodawanie użytkowników toohello rozliczeń czytnika roli</span><span class="sxs-lookup"><span data-stu-id="73d82-117">Adding users toohello Billing Reader role</span></span>

<span data-ttu-id="73d82-118">Hello rozliczeń czytnika rola ma dostęp tylko do odczytu toosubscription informacji dotyczących rozliczeń w portalu Azure, a nie tooservices dostępu, takich jak konta magazynu i maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="73d82-118">hello Billing Reader role has read-only access toosubscription billing information in Azure portal, and no access tooservices such as VMs and storage accounts.</span></span> <span data-ttu-id="73d82-119">Przypisz hello rozliczeń czytnika roli toosomeone musi uzyskać dostępu do informacji dotyczących rozliczeń toohello subskrypcji, ale nie hello toomanage możliwości usługi Azure usługi.</span><span class="sxs-lookup"><span data-stu-id="73d82-119">Assign hello Billing Reader role toosomeone that needs access toohello subscription billing information but not hello ability toomanage Azure services.</span></span> <span data-ttu-id="73d82-120">Ta rola jest odpowiednia dla użytkowników w organizacji, którzy finansowych i kosztów zarządzania należy wykonać tylko dla subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="73d82-120">This role is appropriate for users in an organization who only perform financial and cost management for Azure subscriptions.</span></span>

1. <span data-ttu-id="73d82-121">Wybierz subskrypcję z hello [bloku subskrypcje](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="73d82-121">Select your subscription from hello [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="73d82-122">Wybierz **(IAM) kontroli dostępu** , a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="73d82-122">Select **Access control (IAM)** and then click **Add**.</span></span>

    ![Zrzut ekranu przedstawia IAM w bloku subskrypcji hello](./media/billing-manage-access/select-iam.PNG)

1. <span data-ttu-id="73d82-124">Wybierz **rozliczeń czytnika** w hello **wybierz rolę** strony.</span><span class="sxs-lookup"><span data-stu-id="73d82-124">Choose **Billing Reader** in hello **Select a role** page.</span></span>

    ![Zrzut ekranu przedstawia rozliczeń czytnika w widoku podręcznego hello](./media/billing-manage-access/select-roles.PNG)

1. <span data-ttu-id="73d82-126">Wpisz hello e-mail dla użytkownika hello tooinvite, a następnie kliknij przycisk **OK** toosend hello zaproszenia.</span><span class="sxs-lookup"><span data-stu-id="73d82-126">Type hello email for hello user you want tooinvite, then click **OK** toosend hello invitation.</span></span>

    ![Zrzut ekranu pokazujący tooenter tooinvite poczty e-mail, ktoś](./media/billing-manage-access/add-user.PNG)

1. <span data-ttu-id="73d82-128">Wykonaj instrukcje hello zaproszenia e-mail toolog w jako czytnik rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="73d82-128">Follow instructions in hello invite email toolog in as a Billing Reader.</span></span>

    ![Zrzut ekranu pokazujący, co hello czytnika rozliczeń można zobaczyć w portalu Azure](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> <span data-ttu-id="73d82-130">funkcja rozliczeń czytnika Hello jest w wersji zapoznawczej i jeszcze nie obsługuje subskrypcji enterprise (EA) lub nieglobalna chmury.</span><span class="sxs-lookup"><span data-stu-id="73d82-130">hello Billing Reader feature is in preview, and does not yet support enterprise (EA) subscriptions or non-global clouds.</span></span>

## <a name="adding-users-tooother-roles"></a><span data-ttu-id="73d82-131">Dodawanie ról tooother użytkowników</span><span class="sxs-lookup"><span data-stu-id="73d82-131">Adding users tooother roles</span></span>

<span data-ttu-id="73d82-132">Dostęp użytkownicy w innych ról, takich jak właścicielem lub współautorem, nie tylko rozliczeniowymi, ale również usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="73d82-132">Users in other roles, such as Owner or Contributor, can access not just billing information, but Azure services as well.</span></span> <span data-ttu-id="73d82-133">Zobacz te role toomanage [Dodawanie lub zmienianie role administratora platformy Azure, zarządzających hello subskrypcji lub usługi](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="73d82-133">toomanage these roles, see [Add or change Azure administrator roles that manage hello subscription or services](billing-add-change-azure-subscription-administrator.md).</span></span>

## <a name="who-can-access-hello-account-centerhttpsaccountwindowsazurecom"></a><span data-ttu-id="73d82-134">Kto ma dostęp do hello [Centrum konta](https://account.windowsazure.com)?</span><span class="sxs-lookup"><span data-stu-id="73d82-134">Who can access hello [Account Center](https://account.windowsazure.com)?</span></span>

<span data-ttu-id="73d82-135">Hello tylko Administrator konta może rejestrować się w Centrum konta toohello.</span><span class="sxs-lookup"><span data-stu-id="73d82-135">Only hello Account Administrator can log in toohello Account center.</span></span> <span data-ttu-id="73d82-136">Hello konto administratora jest hello prawnym właścicielem hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="73d82-136">hello Account Administrator is hello legal owner of hello subscription.</span></span> <span data-ttu-id="73d82-137">Domyślnie osoba hello utworzył konto na lub zakupiono hello subskrypcji platformy Azure jest hello administratora konta, chyba że hello [przeniesienia własności subskrypcji](billing-subscription-transfer.md) toosomebody else.</span><span class="sxs-lookup"><span data-stu-id="73d82-137">By default, hello person who signed up for or bought hello Azure subscription is hello Account Administrator, unless hello [subscription ownership was transferred](billing-subscription-transfer.md) toosomebody else.</span></span> <span data-ttu-id="73d82-138">Hello administratora konta można tworzyć subskrypcje, anulowanie subskrypcji, zmienić hello adres rozliczeń dla subskrypcji i zarządzanie zasadami dostępu dla subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="73d82-138">hello Account Administrator can create subscriptions, cancel subscriptions, change hello billing address for a subscription, and manage access policies for hello subscription.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="73d82-139">Potrzebujesz pomocy?</span><span class="sxs-lookup"><span data-stu-id="73d82-139">Need help?</span></span> <span data-ttu-id="73d82-140">Skontaktuj się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="73d82-140">Contact support.</span></span>

<span data-ttu-id="73d82-141">Jeśli masz więcej pytań, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget szybkie rozwiązanie problemu.</span><span class="sxs-lookup"><span data-stu-id="73d82-141">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
