---
title: "Powiadomienia o raportach usługi Azure Active Directory"
description: "Jak używać usługi Azure Active Directory raportowania powiadomienia o podejrzanych znak dodatków."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ae6d4b0e-5931-4cb3-98bf-9be91b381c92
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.custom: oldportal
ms.reviewer: dhanyahk
ms.openlocfilehash: f4632bd2af802b10c8c64972e8c605d7ad7c0eaf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-reporting-notifications"></a><span data-ttu-id="37165-103">Powiadomienia o raportach usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37165-103">Azure Active Directory Reporting Notifications</span></span>
## <a name="what-reports-generate-email-notifications"></a><span data-ttu-id="37165-104">Jakie raporty generowanie powiadomień e-mail</span><span class="sxs-lookup"><span data-stu-id="37165-104">What reports generate email notifications</span></span>
<span data-ttu-id="37165-105">W tej chwili nieregularne logowania wyzwalaczy raport aktywności wiadomości e-mail z powiadomieniami.</span><span class="sxs-lookup"><span data-stu-id="37165-105">At this time, only the Irregular Sign in Activity report triggers email notifications.</span></span>

## <a name="what-is-an-irregular-sign-in"></a><span data-ttu-id="37165-106">Co to jest "nieregularne logowania"?</span><span class="sxs-lookup"><span data-stu-id="37165-106">What is an "Irregular Sign in"?</span></span>
<span data-ttu-id="37165-107">Nieregularne logowania są tymi, które zostały zidentyfikowane przez naszych algorytmów, na podstawie warunku "niemożliwa podróż", w połączeniu z nietypowych lokalizacji logowania i urządzenia uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="37165-107">Irregular sign-ins are those that have been identified by our machine learning algorithms, on the basis of an "impossible travel" condition combined with an anomalous sign-in location and device.</span></span> <span data-ttu-id="37165-108">Może to oznaczać, że haker próbuje zalogować się przy użyciu tego konta.</span><span class="sxs-lookup"><span data-stu-id="37165-108">This may indicate that a hacker has been trying to sign in using this account.</span></span>

## <a name="who-receives-the-email-notifications"></a><span data-ttu-id="37165-109">Kto otrzymuje powiadomienia e-mail?</span><span class="sxs-lookup"><span data-stu-id="37165-109">Who receives the email notifications?</span></span>
<span data-ttu-id="37165-110">Wiadomości e-mail są wysyłane do wszystkich administratorów globalnych, którzy zostali przypisani licencji usługi Active Directory — wersja Premium.</span><span class="sxs-lookup"><span data-stu-id="37165-110">The email is sent to all global admins who have been assigned an Active Directory Premium license.</span></span> <span data-ttu-id="37165-111">Aby upewnić się, że dostarczeniu, wyślemy go do administratorów alternatywny adres E-mail, jak również.</span><span class="sxs-lookup"><span data-stu-id="37165-111">To ensure it is delivered, we send it to the admins Alternate Email Address as well.</span></span> <span data-ttu-id="37165-112">Administratorzy powinna zawierać aad-alerts-noreply@mail.windowsazure.com na liście bezpiecznych, nie zostaną pominięte wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="37165-112">Admins should include aad-alerts-noreply@mail.windowsazure.com in their safe senders list so they don’t miss the email.</span></span>

## <a name="how-often-are-these-emails-sent"></a><span data-ttu-id="37165-113">Jak często są te wiadomości e-mail wysyłanych?</span><span class="sxs-lookup"><span data-stu-id="37165-113">How often are these emails sent?</span></span>
<span data-ttu-id="37165-114">Wiadomości e-mail są wysyłane, jeśli 10 nowych nieregularne logowania działań występuje w ciągu ostatnich 30 dni lub od momentu ostatniego wiadomość e-mail została wysłana, ta wartość jest mniejsza.</span><span class="sxs-lookup"><span data-stu-id="37165-114">The email is sent if 10 new irregular sign-in activities occur in the last 30 days, or since the last email was sent, whichever is less.</span></span>

## <a name="how-do-i-access-the-report-mentioned-in-the-email"></a><span data-ttu-id="37165-115">Jak uzyskać dostępu do raportów wymienionych w wiadomości e-mail</span><span class="sxs-lookup"><span data-stu-id="37165-115">How do I access the report mentioned in the email?</span></span>
<span data-ttu-id="37165-116">Po kliknięciu łącza nastąpi przekierowanie do strony raportu w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="37165-116">When you click on the link, you will be redirected to the report page within the Azure classic portal.</span></span> <span data-ttu-id="37165-117">Aby uzyskać dostęp do raportu, musisz być:</span><span class="sxs-lookup"><span data-stu-id="37165-117">In order to access the report, you need to be both:</span></span>

* <span data-ttu-id="37165-118">Administrator lub współadministratora subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="37165-118">An admin or co-admin of your Azure subscription</span></span>
* <span data-ttu-id="37165-119">Administrator globalny w katalogu i przypisaniu licencji usługi Active Directory — wersja Premium.</span><span class="sxs-lookup"><span data-stu-id="37165-119">A global administrator in the directory, and assigned an Active Directory Premium license.</span></span> <span data-ttu-id="37165-120">Aby uzyskać więcej informacji, zobacz [Wersje usługi Azure Active Directory](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="37165-120">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="can-i-turn-off-these-emails"></a><span data-ttu-id="37165-121">Można wyłączyć te wiadomości e-mail?</span><span class="sxs-lookup"><span data-stu-id="37165-121">Can I turn off these emails?</span></span>
<span data-ttu-id="37165-122">Tak, aby wyłączyć powiadomienia dotyczące nietypowe logowania w klasycznym portalu Azure, kliknij przycisk **Konfiguruj**, a następnie wybierz **wyłączone** w obszarze **powiadomienia** sekcji.</span><span class="sxs-lookup"><span data-stu-id="37165-122">Yes, to turn off notifications related to anomalous sign-ins within the Azure classic portal, click **Configure**, and then select **Disabled** under the **Notifications** section.</span></span>

## <a name="whats-next"></a><span data-ttu-id="37165-123">Co dalej</span><span class="sxs-lookup"><span data-stu-id="37165-123">What's next</span></span>
* <span data-ttu-id="37165-124">Zastanawiasz się, jak zabezpieczeń, inspekcji i raporty dotyczące działań są dostępne?</span><span class="sxs-lookup"><span data-stu-id="37165-124">Curious about what security, audit, and activity reports are available?</span></span> <span data-ttu-id="37165-125">Zapoznaj się z [zabezpieczeń platformy Azure AD, inspekcji i raporty dotyczące działań](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="37165-125">Check out [Azure AD Security, Audit, and Activity Reports](active-directory-view-access-usage-reports.md)</span></span>
* [<span data-ttu-id="37165-126">Wprowadzenie do usługi Azure Active Directory — wersja Premium</span><span class="sxs-lookup"><span data-stu-id="37165-126">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="37165-127">Dodawanie znakowania firmowego do stron logowania i panelu dostępu</span><span class="sxs-lookup"><span data-stu-id="37165-127">Add company branding to your Sign In and Access Panel pages</span></span>](active-directory-add-company-branding.md)

