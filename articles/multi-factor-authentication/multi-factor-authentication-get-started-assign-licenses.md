---
title: "Przypisywanie licencji na usługę Azure MFA | Microsoft Docs"
description: "Dowiedz się, jak przypisywać użytkownikom licencje na usługę Microsoft Azure Multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 514ef423-8ee6-4987-8a4e-80d5dc394cf9
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/13/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ROBOTS: NOINDEX
ms.openlocfilehash: 45522bf526c4aeab1d6ccc8891a55a0436ff9320
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="assigning-an-azure-mfa-azure-ad-premium-or-enterprise-mobility-license-to-users"></a><span data-ttu-id="9f7ec-103">Przypisywanie użytkownikom licencji usługi Azure MFA, usługi Azure AD w wersji Premium lub pakietu Enterprise Mobility</span><span class="sxs-lookup"><span data-stu-id="9f7ec-103">Assigning an Azure MFA, Azure AD Premium, or Enterprise Mobility license to users</span></span>
<span data-ttu-id="9f7ec-104">Jeśli zakupiono licencję usługi Azure MFA, usługi Azure AD w wersji Premium lub pakietu Enterprise Mobility Suite, nie trzeba tworzyć dostawcy usługi Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="9f7ec-104">If you have purchased Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses, you do not need to create a Multi-Factor Auth provider.</span></span> <span data-ttu-id="9f7ec-105">Po przypisaniu licencji użytkownikom będzie można umożliwić im korzystanie z usługi MFA.</span><span class="sxs-lookup"><span data-stu-id="9f7ec-105">Once you assign the licenses to your users, you can begin enabling them for MFA.</span></span>

## <a name="to-assign-a-license"></a><span data-ttu-id="9f7ec-106">Aby przypisać licencję</span><span class="sxs-lookup"><span data-stu-id="9f7ec-106">To assign a license</span></span>
1. <span data-ttu-id="9f7ec-107">Zaloguj się do [klasycznego portalu Azure](https://manage.windowsazure.com) jako administrator.</span><span class="sxs-lookup"><span data-stu-id="9f7ec-107">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an administrator.</span></span>
2. <span data-ttu-id="9f7ec-108">W obszarze po lewej stronie wybierz pozycję **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9f7ec-108">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="9f7ec-109">Na stronie usługi Active Directory kliknij dwukrotnie katalog zawierający użytkowników, których chcesz włączyć.</span><span class="sxs-lookup"><span data-stu-id="9f7ec-109">On the Active Directory page, double-click the directory that has the users you wish to enable.</span></span>
4. <span data-ttu-id="9f7ec-110">W górnej części strony katalogu wybierz pozycję **Licencje**.</span><span class="sxs-lookup"><span data-stu-id="9f7ec-110">At the top of the directory page, select **Licenses**.</span></span>
   <span data-ttu-id="9f7ec-111">![Przypisywanie licencji](./media/multi-factor-authentication-get-started-assign-licenses/assign1.png)</span><span class="sxs-lookup"><span data-stu-id="9f7ec-111">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign1.png)</span></span>
5. <span data-ttu-id="9f7ec-112">Na stronie Licencje wybierz pozycję **Azure Multi-Factor Authentication**, **Active Directory Premium** lub **Enterprise Mobility Suite**.</span><span class="sxs-lookup"><span data-stu-id="9f7ec-112">On the Licenses page, select **Azure Multi-Factor Authentication**, **Active Directory Premium**, or **Enterprise Mobility Suite**.</span></span>  <span data-ttu-id="9f7ec-113">Jeśli masz tylko jedną licencję, powinna ona zostać wybrana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="9f7ec-113">If you only have one, then it should be selected automatically.</span></span>
6. <span data-ttu-id="9f7ec-114">W dolnej części strony kliknij pozycję **Przypisz**.</span><span class="sxs-lookup"><span data-stu-id="9f7ec-114">At the bottom of the page, click **Assign**.</span></span>
   <span data-ttu-id="9f7ec-115">![Przypisywanie licencji](./media/multi-factor-authentication-get-started-assign-licenses/assign3.png)</span><span class="sxs-lookup"><span data-stu-id="9f7ec-115">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign3.png)</span></span>
7. <span data-ttu-id="9f7ec-116">W wyświetlonym oknie kliknij obok użytkowników lub grup, którym chcesz przypisać licencje.</span><span class="sxs-lookup"><span data-stu-id="9f7ec-116">In the box that comes up, click next to the users or groups you want to assign licenses to.</span></span>  <span data-ttu-id="9f7ec-117">Zostanie wyświetlony zielony znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="9f7ec-117">You should see a green check mark appear.</span></span>
8. <span data-ttu-id="9f7ec-118">Kliknij ikonę znacznika wyboru, aby zapisać zmiany.</span><span class="sxs-lookup"><span data-stu-id="9f7ec-118">Click the check mark icon to save the changes.</span></span>
   <span data-ttu-id="9f7ec-119">![Przypisywanie licencji](./media/multi-factor-authentication-get-started-assign-licenses/assign4.png)</span><span class="sxs-lookup"><span data-stu-id="9f7ec-119">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign4.png)</span></span>
9. <span data-ttu-id="9f7ec-120">Pojawi się komunikat z informacją o liczbie przypisanych licencji i liczbie ewentualnych niepowodzeń przypisań licencji.</span><span class="sxs-lookup"><span data-stu-id="9f7ec-120">You should see a message saying how many licenses were assigned and how many may have failed.</span></span>  <span data-ttu-id="9f7ec-121">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="9f7ec-121">Click **Ok**.</span></span>
   <span data-ttu-id="9f7ec-122">![Przypisywanie licencji](./media/multi-factor-authentication-get-started-assign-licenses/assign5.png)</span><span class="sxs-lookup"><span data-stu-id="9f7ec-122">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign5.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f7ec-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9f7ec-123">Next steps</span></span>

- <span data-ttu-id="9f7ec-124">Aby uzyskać więcej informacji, zobacz [What is Microsoft Azure Active Directory licensing?](../active-directory/active-directory-licensing-what-is.md) (Co to jest licencjonowanie usługi Microsoft Azure Active Directory?)</span><span class="sxs-lookup"><span data-stu-id="9f7ec-124">For more information, see [What is Microsoft Azure Active Directory licensing?](../active-directory/active-directory-licensing-what-is.md)</span></span>
