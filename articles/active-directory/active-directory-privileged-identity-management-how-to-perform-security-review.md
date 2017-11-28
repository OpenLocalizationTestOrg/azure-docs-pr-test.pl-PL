---
title: "tooperform aaaHow Przegląd dostępu | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooperform przegląd z hello aplikacji Azure Privileged Identity Management."
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
ms.openlocfilehash: 301a5e9f97b68fedfbf4954e0bd7dadb7f0fc510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="990f3-103">Jak tooperform dostępu Przejrzyj w usłudze Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="990f3-103">How tooperform an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="990f3-104">Azure Active Directory (AD) Privileged Identity Management upraszcza sposób przedsiębiorstw Zarządzanie tooresources uprzywilejowanego dostępu w usłudze Azure AD i innych usług online firmy Microsoft, takich jak usługi Office 365 lub Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="990f3-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access tooresources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="990f3-105">Jeśli przypisano rolę administracyjną tooan, administrator ról uprzywilejowanych w organizacji może poprosić tooregularly potwierdzić, że użytkownik nadal tej roli dla zadania.</span><span class="sxs-lookup"><span data-stu-id="990f3-105">If you are assigned tooan administrative role, your organization's privileged role administrator may ask you tooregularly confirm that you still need that role for your job.</span></span> <span data-ttu-id="990f3-106">Może spowodować, że wiadomość e-mail zawierającą łącze lub przejść proste toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="990f3-106">You might get an email that includes a link, or you can go straight toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="990f3-107">Wykonaj kroki hello w tym tooperform artykułu własnym przeglądu przypisane role.</span><span class="sxs-lookup"><span data-stu-id="990f3-107">Follow hello steps in this article tooperform a self-review of your assigned roles.</span></span>

<span data-ttu-id="990f3-108">Jeśli administrator ról uprzywilejowanych zainteresowana przeglądami dostępu, Dowiedz się więcej na [jak toostart dostępu Przejrzyj](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="990f3-108">If you're a privileged role administrator interested in access reviews, get more details at [How toostart an access review](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="add-hello-privileged-identity-management-application"></a><span data-ttu-id="990f3-109">Dodawanie aplikacji Privileged Identity Management hello</span><span class="sxs-lookup"><span data-stu-id="990f3-109">Add hello Privileged Identity Management application</span></span>
<span data-ttu-id="990f3-110">Można użyć hello Azure AD Privileged Identity zarządzania (PIM) aplikacji w hello [portalu Azure](https://portal.azure.com/) tooperform zapoznania się z nimi.</span><span class="sxs-lookup"><span data-stu-id="990f3-110">You can use hello Azure AD Privileged Identity Management (PIM) application in hello [Azure portal](https://portal.azure.com/) tooperform your review.</span></span>  <span data-ttu-id="990f3-111">Jeśli nie masz hello aplikacji Azure AD Privileged Identity Management w portalu sieci należy wykonać te tooget kroki pracy.</span><span class="sxs-lookup"><span data-stu-id="990f3-111">If you don't have hello Azure AD Privileged Identity Management application on your portal, follow these steps tooget started.</span></span>

1. <span data-ttu-id="990f3-112">Zaloguj się toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="990f3-112">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="990f3-113">Wybierz swoją nazwę użytkownika w hello prawym górnym rogu hello portalu Azure i wybierz hello katalogu, której będzie można działać.</span><span class="sxs-lookup"><span data-stu-id="990f3-113">Select your username in hello upper right-hand corner of hello Azure portal, and select hello directory where you will you be operating.</span></span>
3. <span data-ttu-id="990f3-114">Wybierz **więcej usług** i użyj hello filtru pole tekstowe toosearch dla **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="990f3-114">Select **More services** and use hello Filter textbox toosearch for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="990f3-115">Sprawdź **toodashboard numeru Pin** , a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="990f3-115">Check **Pin toodashboard** and then click **Create**.</span></span> <span data-ttu-id="990f3-116">zostanie otwarta Hello aplikacji Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="990f3-116">hello Privileged Identity Management application will open.</span></span>

## <a name="approve-or-deny-access"></a><span data-ttu-id="990f3-117">Zatwierdzenia lub odmowy dostępu</span><span class="sxs-lookup"><span data-stu-id="990f3-117">Approve or deny access</span></span>
<span data-ttu-id="990f3-118">Podczas zatwierdzania lub odmówić dostępu należy jest właśnie informuje recenzenta hello czy możesz nadal używać tej roli lub nie.</span><span class="sxs-lookup"><span data-stu-id="990f3-118">When you approve or deny access, you're just telling hello reviewer whether you still use this role or not.</span></span> <span data-ttu-id="990f3-119">Wybierz **Zatwierdź** Jeśli chcesz toostay w roli hello lub **Odmów** Jeśli użytkownik nie należy hello dostępu już.</span><span class="sxs-lookup"><span data-stu-id="990f3-119">Choose **Approve** if you want toostay in hello role, or **Deny** if you don't need hello access anymore.</span></span> <span data-ttu-id="990f3-120">Stan użytkownika nie zostaną zmienione od razu, dopóki recenzenta hello stosuje hello wyników.</span><span class="sxs-lookup"><span data-stu-id="990f3-120">Your status won't change right away, until hello reviewer applies hello results.</span></span>
<span data-ttu-id="990f3-121">Wykonaj te kroki toofind i ukończyć powitalnych Przegląd dostępu:</span><span class="sxs-lookup"><span data-stu-id="990f3-121">Follow these steps toofind and complete hello access review:</span></span>

1. <span data-ttu-id="990f3-122">W aplikacji PIM hello, wybierz **przeglądu uprzywilejowany dostęp**.</span><span class="sxs-lookup"><span data-stu-id="990f3-122">In hello PIM application, select **Review privileged access**.</span></span> <span data-ttu-id="990f3-123">Jeśli masz wszelkie oczekujące dostępu przeglądy pojawią się one w hello dostępu usługi Azure AD sprawdza bloku.</span><span class="sxs-lookup"><span data-stu-id="990f3-123">If you have any pending access reviews, they appear in hello Azure AD Access reviews blade.</span></span>
2. <span data-ttu-id="990f3-124">Wybierz przeglądu hello ma toocomplete.</span><span class="sxs-lookup"><span data-stu-id="990f3-124">Select hello review you want toocomplete.</span></span>
3. <span data-ttu-id="990f3-125">Chyba że zostaną utworzone hello przeglądu, wyświetlane jako hello tylko użytkownik w przeglądzie hello.</span><span class="sxs-lookup"><span data-stu-id="990f3-125">Unless you created hello review, you appear as hello only user in hello review.</span></span> <span data-ttu-id="990f3-126">Wybierz następny nazwę tooyour hello znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="990f3-126">Select hello check mark next tooyour name.</span></span>
4. <span data-ttu-id="990f3-127">Wybierz **zatwierdzić** lub **odmowy**.</span><span class="sxs-lookup"><span data-stu-id="990f3-127">Choose either **Approve** or **Deny**.</span></span> <span data-ttu-id="990f3-128">Może być konieczne tooinclude przyczynę decyzji w hello **przyczyny** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="990f3-128">You may need tooinclude a reason for your decision in hello **Provide a reason** text box.</span></span>  
5. <span data-ttu-id="990f3-129">Zamknij hello **ról Przegląd usługi Azure AD** bloku.</span><span class="sxs-lookup"><span data-stu-id="990f3-129">Close hello **Review Azure AD roles** blade.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="990f3-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="990f3-130">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
