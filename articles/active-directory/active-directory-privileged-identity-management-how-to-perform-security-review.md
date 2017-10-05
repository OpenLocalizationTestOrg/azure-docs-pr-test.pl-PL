---
title: "Jak przeprowadzić przegląd dostępu | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przeprowadzić przegląd aplikacji Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 49ee2feb-7d2e-4acf-82c1-40ff23062862
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: a98ed60221eeba1d9c92df846aeae2deafb8ae60
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-perform-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="dadb3-103">Jak przeprowadzić przegląd dostępu w usłudze Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="dadb3-103">How to perform an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="dadb3-104">Azure Active Directory (AD) Privileged Identity Management upraszcza, jak zarządzać uprzywilejowanego dostępu do zasobów w usłudze Azure AD i innych usług online firmy Microsoft, takich jak usługi Office 365 lub Microsoft Intune w przedsiębiorstwach.</span><span class="sxs-lookup"><span data-stu-id="dadb3-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="dadb3-105">Jeśli użytkownik został przypisany do roli administratora, administrator ról uprzywilejowanych w organizacji może poprosić o regularnie potwierdzić nadal potrzebujesz tej roli dla zadania.</span><span class="sxs-lookup"><span data-stu-id="dadb3-105">If you are assigned to an administrative role, your organization's privileged role administrator may ask you to regularly confirm that you still need that role for your job.</span></span> <span data-ttu-id="dadb3-106">Może spowodować, że wiadomość e-mail zawierającą łącze lub można przejść bezpośrednio do [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dadb3-106">You might get an email that includes a link, or you can go straight to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="dadb3-107">Wykonaj kroki opisane w tym artykule, aby wykonać własnym przeglądu przypisane role.</span><span class="sxs-lookup"><span data-stu-id="dadb3-107">Follow the steps in this article to perform a self-review of your assigned roles.</span></span>

<span data-ttu-id="dadb3-108">Jeśli administrator ról uprzywilejowanych zainteresowana przeglądami dostępu, Dowiedz się więcej na [jak rozpocząć Przegląd dostępu](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="dadb3-108">If you're a privileged role administrator interested in access reviews, get more details at [How to start an access review](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="add-the-privileged-identity-management-application"></a><span data-ttu-id="dadb3-109">Dodawanie aplikacji Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="dadb3-109">Add the Privileged Identity Management application</span></span>
<span data-ttu-id="dadb3-110">Możesz użyć aplikacji Azure AD Privileged Identity zarządzania (PIM) w [portalu Azure](https://portal.azure.com/) przeprowadzić zapoznania się z nimi.</span><span class="sxs-lookup"><span data-stu-id="dadb3-110">You can use the Azure AD Privileged Identity Management (PIM) application in the [Azure portal](https://portal.azure.com/) to perform your review.</span></span>  <span data-ttu-id="dadb3-111">Jeśli nie masz aplikacji usługi Azure AD Privileged Identity Management w portalu sieci, wykonaj następujące kroki, aby rozpocząć.</span><span class="sxs-lookup"><span data-stu-id="dadb3-111">If you don't have the Azure AD Privileged Identity Management application on your portal, follow these steps to get started.</span></span>

1. <span data-ttu-id="dadb3-112">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="dadb3-112">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="dadb3-113">Wybierz swoją nazwę użytkownika w prawym górnym rogu portalu Azure i wybierz katalog, w której będzie można działać.</span><span class="sxs-lookup"><span data-stu-id="dadb3-113">Select your username in the upper right-hand corner of the Azure portal, and select the directory where you will you be operating.</span></span>
3. <span data-ttu-id="dadb3-114">Wybierz polecenie **Więcej usług** i użyj pola tekstowego filtru, aby wyszukać **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="dadb3-114">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="dadb3-115">Zaznacz opcję **Przypnij do pulpitu nawigacyjnego**, a następnie kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="dadb3-115">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="dadb3-116">Zostanie otwarta aplikacja Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="dadb3-116">The Privileged Identity Management application will open.</span></span>

## <a name="approve-or-deny-access"></a><span data-ttu-id="dadb3-117">Zatwierdzenia lub odmowy dostępu</span><span class="sxs-lookup"><span data-stu-id="dadb3-117">Approve or deny access</span></span>
<span data-ttu-id="dadb3-118">Podczas zatwierdzania lub odmówić dostępu należy jest po prostu informuje recenzenta czy możesz nadal używać tej roli lub nie.</span><span class="sxs-lookup"><span data-stu-id="dadb3-118">When you approve or deny access, you're just telling the reviewer whether you still use this role or not.</span></span> <span data-ttu-id="dadb3-119">Wybierz **Zatwierdź** aby pozostać w tej roli, lub **Odmów** Jeśli nie musisz już dostępu.</span><span class="sxs-lookup"><span data-stu-id="dadb3-119">Choose **Approve** if you want to stay in the role, or **Deny** if you don't need the access anymore.</span></span> <span data-ttu-id="dadb3-120">Stan użytkownika nie zostaną zmienione od razu, dopóki recenzenta stosuje wyniki.</span><span class="sxs-lookup"><span data-stu-id="dadb3-120">Your status won't change right away, until the reviewer applies the results.</span></span>
<span data-ttu-id="dadb3-121">Wykonaj te czynności, aby go przejrzeć dostępu:</span><span class="sxs-lookup"><span data-stu-id="dadb3-121">Follow these steps to find and complete the access review:</span></span>

1. <span data-ttu-id="dadb3-122">W aplikacji PIM zaznacz **przeglądu uprzywilejowany dostęp**.</span><span class="sxs-lookup"><span data-stu-id="dadb3-122">In the PIM application, select **Review privileged access**.</span></span> <span data-ttu-id="dadb3-123">Jeśli masz wszelkie oczekujące dostępu przeglądy pojawią się one w bloku przeglądami dostępu usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dadb3-123">If you have any pending access reviews, they appear in the Azure AD Access reviews blade.</span></span>
2. <span data-ttu-id="dadb3-124">Wybierz przeglądu, które chcesz wykonać.</span><span class="sxs-lookup"><span data-stu-id="dadb3-124">Select the review you want to complete.</span></span>
3. <span data-ttu-id="dadb3-125">Jeśli nie utworzono przeglądu, wyświetlane jako jedynym użytkownikiem w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="dadb3-125">Unless you created the review, you appear as the only user in the review.</span></span> <span data-ttu-id="dadb3-126">Zaznacz pole wyboru obok swojej nazwy.</span><span class="sxs-lookup"><span data-stu-id="dadb3-126">Select the check mark next to your name.</span></span>
4. <span data-ttu-id="dadb3-127">Wybierz **zatwierdzić** lub **odmowy**.</span><span class="sxs-lookup"><span data-stu-id="dadb3-127">Choose either **Approve** or **Deny**.</span></span> <span data-ttu-id="dadb3-128">Może być konieczne uwzględnienie Przyczyna decyzji w **przyczyny** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="dadb3-128">You may need to include a reason for your decision in the **Provide a reason** text box.</span></span>  
5. <span data-ttu-id="dadb3-129">Zamknij **ról Przegląd usługi Azure AD** bloku.</span><span class="sxs-lookup"><span data-stu-id="dadb3-129">Close the **Review Azure AD roles** blade.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="dadb3-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dadb3-130">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
