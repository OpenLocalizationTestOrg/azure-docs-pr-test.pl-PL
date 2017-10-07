---
title: aaaAzure Active Directory powiadomienia o raportach
description: "Jak toouse hello powiadomienia raportowania usługi Azure Active Directory dla podejrzanych znak dodatków."
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
ms.openlocfilehash: 3843c45eaf9d68e671943bfdbc7ab68933f38fbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-notifications"></a><span data-ttu-id="da33d-103">Powiadomienia o raportach usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="da33d-103">Azure Active Directory Reporting Notifications</span></span>
## <a name="what-reports-generate-email-notifications"></a><span data-ttu-id="da33d-104">Jakie raporty generowanie powiadomień e-mail</span><span class="sxs-lookup"><span data-stu-id="da33d-104">What reports generate email notifications</span></span>
<span data-ttu-id="da33d-105">W tej chwili tylko hello nieregularne znak w wyzwalaczy raport aktywności wiadomości e-mail z powiadomieniami.</span><span class="sxs-lookup"><span data-stu-id="da33d-105">At this time, only hello Irregular Sign in Activity report triggers email notifications.</span></span>

## <a name="what-is-an-irregular-sign-in"></a><span data-ttu-id="da33d-106">Co to jest "nieregularne logowania"?</span><span class="sxs-lookup"><span data-stu-id="da33d-106">What is an "Irregular Sign in"?</span></span>
<span data-ttu-id="da33d-107">Nieregularne logowania są tymi, które zostały zidentyfikowane przez naszych algorytmów, na podstawie hello warunku "niemożliwa podróż", w połączeniu z nietypowych lokalizacji logowania i urządzenia uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="da33d-107">Irregular sign-ins are those that have been identified by our machine learning algorithms, on hello basis of an "impossible travel" condition combined with an anomalous sign-in location and device.</span></span> <span data-ttu-id="da33d-108">Może to oznaczać, że haker zostały próby toosign za pomocą tego konta.</span><span class="sxs-lookup"><span data-stu-id="da33d-108">This may indicate that a hacker has been trying toosign in using this account.</span></span>

## <a name="who-receives-hello-email-notifications"></a><span data-ttu-id="da33d-109">Kto otrzymuje powiadomienia e-mail hello?</span><span class="sxs-lookup"><span data-stu-id="da33d-109">Who receives hello email notifications?</span></span>
<span data-ttu-id="da33d-110">Witaj poczty e-mail są wysyłane tooall administratorów globalnych, który został przypisany do licencji usługi Active Directory — wersja Premium.</span><span class="sxs-lookup"><span data-stu-id="da33d-110">hello email is sent tooall global admins who have been assigned an Active Directory Premium license.</span></span> <span data-ttu-id="da33d-111">tooensure on jest przeprowadzane, możemy wysyłać go również toohello Administratorzy alternatywny adres E-mail.</span><span class="sxs-lookup"><span data-stu-id="da33d-111">tooensure it is delivered, we send it toohello admins Alternate Email Address as well.</span></span> <span data-ttu-id="da33d-112">Administratorzy powinna zawierać aad-alerts-noreply@mail.windowsazure.com na liście bezpiecznych, nie zostaną pominięte hello poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="da33d-112">Admins should include aad-alerts-noreply@mail.windowsazure.com in their safe senders list so they don’t miss hello email.</span></span>

## <a name="how-often-are-these-emails-sent"></a><span data-ttu-id="da33d-113">Jak często są te wiadomości e-mail wysyłanych?</span><span class="sxs-lookup"><span data-stu-id="da33d-113">How often are these emails sent?</span></span>
<span data-ttu-id="da33d-114">Hello wiadomość e-mail jest wysyłana, gdy 10 nowych nieregularne logowania działań występują w hello ostatnich 30 dni lub ponieważ hello ostatnią wiadomość e-mail została wysłana, ta wartość jest mniejsza.</span><span class="sxs-lookup"><span data-stu-id="da33d-114">hello email is sent if 10 new irregular sign-in activities occur in hello last 30 days, or since hello last email was sent, whichever is less.</span></span>

## <a name="how-do-i-access-hello-report-mentioned-in-hello-email"></a><span data-ttu-id="da33d-115">Jak uzyskać dostępu do raportu hello wspomnianego hello poczty e-mail?</span><span class="sxs-lookup"><span data-stu-id="da33d-115">How do I access hello report mentioned in hello email?</span></span>
<span data-ttu-id="da33d-116">Po kliknięciu łącza hello będzie przekierowany toohello strony raportu w hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="da33d-116">When you click on hello link, you will be redirected toohello report page within hello Azure classic portal.</span></span> <span data-ttu-id="da33d-117">W kolejności tooaccess hello raport, należy toobe zarówno:</span><span class="sxs-lookup"><span data-stu-id="da33d-117">In order tooaccess hello report, you need toobe both:</span></span>

* <span data-ttu-id="da33d-118">Administrator lub współadministratora subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="da33d-118">An admin or co-admin of your Azure subscription</span></span>
* <span data-ttu-id="da33d-119">Administrator globalny w katalogu hello i przypisaniu licencji usługi Active Directory — wersja Premium.</span><span class="sxs-lookup"><span data-stu-id="da33d-119">A global administrator in hello directory, and assigned an Active Directory Premium license.</span></span> <span data-ttu-id="da33d-120">Aby uzyskać więcej informacji, zobacz [Wersje usługi Azure Active Directory](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="da33d-120">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="can-i-turn-off-these-emails"></a><span data-ttu-id="da33d-121">Można wyłączyć te wiadomości e-mail?</span><span class="sxs-lookup"><span data-stu-id="da33d-121">Can I turn off these emails?</span></span>
<span data-ttu-id="da33d-122">Tak, tooturn wyłączyć powiadomienia dotyczące logowania tooanomalous w hello klasycznego portalu Azure, kliknij przycisk **Konfiguruj**, a następnie wybierz **wyłączone** w obszarze hello **powiadomienia**sekcji.</span><span class="sxs-lookup"><span data-stu-id="da33d-122">Yes, tooturn off notifications related tooanomalous sign-ins within hello Azure classic portal, click **Configure**, and then select **Disabled** under hello **Notifications** section.</span></span>

## <a name="whats-next"></a><span data-ttu-id="da33d-123">Co dalej</span><span class="sxs-lookup"><span data-stu-id="da33d-123">What's next</span></span>
* <span data-ttu-id="da33d-124">Zastanawiasz się, jak zabezpieczeń, inspekcji i raporty dotyczące działań są dostępne?</span><span class="sxs-lookup"><span data-stu-id="da33d-124">Curious about what security, audit, and activity reports are available?</span></span> <span data-ttu-id="da33d-125">Zapoznaj się z [zabezpieczeń platformy Azure AD, inspekcji i raporty dotyczące działań](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="da33d-125">Check out [Azure AD Security, Audit, and Activity Reports](active-directory-view-access-usage-reports.md)</span></span>
* [<span data-ttu-id="da33d-126">Wprowadzenie do usługi Azure Active Directory — wersja Premium</span><span class="sxs-lookup"><span data-stu-id="da33d-126">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="da33d-127">Dodawanie znakowania firmowego tooyour logowania i panelu dostępu do stron</span><span class="sxs-lookup"><span data-stu-id="da33d-127">Add company branding tooyour Sign In and Access Panel pages</span></span>](active-directory-add-company-branding.md)

