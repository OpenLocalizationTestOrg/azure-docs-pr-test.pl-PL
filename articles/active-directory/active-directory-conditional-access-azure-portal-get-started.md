---
title: "aaaGet korzystania z dostępu warunkowego w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Testowanie dostępu warunkowego za pomocą warunku lokalizacji."
services: active-directory
keywords: "tooapps dostępu warunkowego, dostępu warunkowego z usługą Azure AD, bezpieczny dostęp do zasobów toocompany, zasady dostępu warunkowego"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4521f5a34f5882e026f5e58a7127d8c55cba2f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a><span data-ttu-id="78317-104">Rozpoczynanie pracy z dostępu warunkowego w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="78317-104">Get started with conditional access in Azure Active Directory</span></span>

<span data-ttu-id="78317-105">Dostęp warunkowy jest możliwość usługi Azure Active Directory, umożliwiającą możesz toodefine warunki na jakich autoryzowani użytkownicy mają dostęp do Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="78317-105">Conditional access is a capability of Azure Active Directory that enables you toodefine conditions under which authorized users can access your apps.</span></span> 

<span data-ttu-id="78317-106">Ten temat zawiera instrukcje dotyczące testowania dostępu warunkowego na podstawie warunku lokalizacji w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="78317-106">This topic provides you with instructions for testing a conditional access based on a location condition in your environment.</span></span>  


## <a name="scenario-description"></a><span data-ttu-id="78317-107">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="78317-107">Scenario description</span></span>

<span data-ttu-id="78317-108">Jednym z typowych wymagań w wielu organizacjach jest tooonly wymusić uwierzytelnianie wieloskładnikowe dla tooapps dostępu, który nie jest wykonywane z hello firmowego intranetu.</span><span class="sxs-lookup"><span data-stu-id="78317-108">One common requirement in many organizations is tooonly require multi-factor authentication for access tooapps that is not performed from hello corporate intranet.</span></span> <span data-ttu-id="78317-109">Z usługą Azure Active Directory można łatwo realizację tego celu, konfigurując zasady dostępu warunkowego na podstawie lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="78317-109">With Azure Active Directory, you can easily accomplish this goal by configuring a location-based conditional access policy.</span></span> <span data-ttu-id="78317-110">W tym temacie przedstawiono szczegółowe instrukcje dotyczące konfigurowania pokrewnych zasad.</span><span class="sxs-lookup"><span data-stu-id="78317-110">This topic provides you with detailed instructions for configuring a related policy.</span></span> <span data-ttu-id="78317-111">Witaj wykorzystanie zasad [zaufanych adresów IP](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish między próbami dostępu z firmowej hello na wszystkich innych lokalizacji w intranecie i.</span><span class="sxs-lookup"><span data-stu-id="78317-111">hello policy leverages [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) toodistinguish between access attempts made from hello corporate's intranet and all other locations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="78317-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="78317-112">Prerequisites</span></span>

<span data-ttu-id="78317-113">Hello scenariusz opisany w tym temacie przyjęto założenie, że znasz hello pojęcia opisane w [dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="78317-113">hello scenario outlined in this topic assumes that you are familiar with hello concepts outlined in [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

<span data-ttu-id="78317-114">tootest tego scenariusza należy:</span><span class="sxs-lookup"><span data-stu-id="78317-114">tootest this scenario, you need to:</span></span>

- <span data-ttu-id="78317-115">Tworzenie użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="78317-115">Create a test user</span></span> 

- <span data-ttu-id="78317-116">Przypisz użytkownika testowego toohello licencji Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="78317-116">Assign an Azure AD Premium license toohello test user</span></span>

- <span data-ttu-id="78317-117">Konfigurowanie zarządzanych aplikacji i przypisz użytkownika tooit użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="78317-117">Configure a managed app and assign your test user tooit</span></span>

- <span data-ttu-id="78317-118">Skonfiguruj listę zaufanych adresów IP</span><span class="sxs-lookup"><span data-stu-id="78317-118">Configure trusted IPs</span></span>

<span data-ttu-id="78317-119">Aby uzyskać więcej informacji na temat zaufanych adresów IP, zobacz [zaufanych adresów IP](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="78317-119">If you need more details about Trusted IPs, see [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="policy-configuration-steps"></a><span data-ttu-id="78317-120">Kroki konfiguracji zasad</span><span class="sxs-lookup"><span data-stu-id="78317-120">Policy configuration steps</span></span>

<span data-ttu-id="78317-121">**tooconfigure zasady dostępu warunkowego, czy:**</span><span class="sxs-lookup"><span data-stu-id="78317-121">**tooconfigure your conditional access policy, do:**</span></span>

1. <span data-ttu-id="78317-122">W portalu Azure na lewy pasek nawigacyjny hello hello kliknij **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="78317-122">In hello Azure portal, on hello left navbar, click **Azure Active Directory**.</span></span> 

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. <span data-ttu-id="78317-124">Na powitania **usługi Azure Active Directory** bloku w hello **Zarządzaj** kliknij **dostępu warunkowego**.</span><span class="sxs-lookup"><span data-stu-id="78317-124">On hello **Azure Active Directory** blade, in hello **Manage** section, click **Conditional access**.</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. <span data-ttu-id="78317-126">Na powitania **dostępu warunkowego** bloku, tooopen hello **nowy** bloku na powitania narzędzi u góry hello kliknij **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="78317-126">On hello **Conditional Access** blade, tooopen hello **New** blade, in hello toolbar on hello top, click **Add**.</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. <span data-ttu-id="78317-128">Na powitania **nowy** bloku w hello **nazwa** tekstowym, wpisz nazwę zasady.</span><span class="sxs-lookup"><span data-stu-id="78317-128">On hello **New** blade, in hello **Name** textbox, type a name for your policy.</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. <span data-ttu-id="78317-130">W hello **przypisania** kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="78317-130">In hello **Assignment** section, click **Users and groups**.</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. <span data-ttu-id="78317-132">Na powitania **użytkowników i grup** blok, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="78317-132">On hello **Users and groups** blade, perform hello following steps:</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    <span data-ttu-id="78317-134">a.</span><span class="sxs-lookup"><span data-stu-id="78317-134">a.</span></span> <span data-ttu-id="78317-135">Kliknij przycisk **Wybierz użytkowników i grupy**.</span><span class="sxs-lookup"><span data-stu-id="78317-135">Click **Select users and groups**.</span></span>

    <span data-ttu-id="78317-136">b.</span><span class="sxs-lookup"><span data-stu-id="78317-136">b.</span></span> <span data-ttu-id="78317-137">Kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="78317-137">Click **Select**.</span></span>

    <span data-ttu-id="78317-138">c.</span><span class="sxs-lookup"><span data-stu-id="78317-138">c.</span></span> <span data-ttu-id="78317-139">Na powitania **wybierz** bloku, wybierz użytkownika testowego, a następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="78317-139">On hello **Select** blade, select your test user, and then click **Select**.</span></span>

    <span data-ttu-id="78317-140">d.</span><span class="sxs-lookup"><span data-stu-id="78317-140">d.</span></span> <span data-ttu-id="78317-141">Na powitania **użytkowników i grup** bloku, kliknij przycisk **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="78317-141">On hello **Users and groups** blade, click **Done**.</span></span>

7. <span data-ttu-id="78317-142">Na powitania **nowy** bloku, tooopen hello **aplikacji w chmurze** bloku w hello **przypisania** kliknij **aplikacji w chmurze**.</span><span class="sxs-lookup"><span data-stu-id="78317-142">On hello **New** blade, tooopen hello **Cloud apps** blade, in hello **Assignment** section, click **Cloud apps**.</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. <span data-ttu-id="78317-144">Na powitania **aplikacji w chmurze** blok, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="78317-144">On hello **Cloud apps** blade, perform hello following steps:</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    <span data-ttu-id="78317-146">a.</span><span class="sxs-lookup"><span data-stu-id="78317-146">a.</span></span> <span data-ttu-id="78317-147">Kliknij przycisk **Wybierz aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="78317-147">Click **Select apps**.</span></span>

    <span data-ttu-id="78317-148">b.</span><span class="sxs-lookup"><span data-stu-id="78317-148">b.</span></span> <span data-ttu-id="78317-149">Kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="78317-149">Click **Select**.</span></span>

    <span data-ttu-id="78317-150">c.</span><span class="sxs-lookup"><span data-stu-id="78317-150">c.</span></span> <span data-ttu-id="78317-151">Na powitania **wybierz** bloku, wybierz aplikacji w chmurze, a następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="78317-151">On hello **Select** blade, select your cloud app, and then click **Select**.</span></span>

    <span data-ttu-id="78317-152">d.</span><span class="sxs-lookup"><span data-stu-id="78317-152">d.</span></span> <span data-ttu-id="78317-153">Na powitania **aplikacji w chmurze** bloku, kliknij przycisk **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="78317-153">On hello **Cloud apps** blade, click **Done**.</span></span>

9. <span data-ttu-id="78317-154">Na powitania **nowy** bloku, tooopen hello **warunki** bloku w hello **przypisania** kliknij **warunki**.</span><span class="sxs-lookup"><span data-stu-id="78317-154">On hello **New** blade, tooopen hello **Conditions** blade, in hello **Assignment** section, click **Conditions**.</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. <span data-ttu-id="78317-156">Na powitania **warunki** bloku, tooopen hello **lokalizacje** bloku, kliknij przycisk **lokalizacje**.</span><span class="sxs-lookup"><span data-stu-id="78317-156">On hello **Conditions** blade, tooopen hello **Locations** blade, click **Locations**.</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. <span data-ttu-id="78317-158">Na powitania **lokalizacje** blok, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="78317-158">On hello **Locations** blade, perform hello following steps:</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    <span data-ttu-id="78317-160">a.</span><span class="sxs-lookup"><span data-stu-id="78317-160">a.</span></span> <span data-ttu-id="78317-161">W obszarze **Konfiguruj**, kliknij przycisk **tak**.</span><span class="sxs-lookup"><span data-stu-id="78317-161">Under **Configure**, click **Yes**.</span></span>

    <span data-ttu-id="78317-162">b.</span><span class="sxs-lookup"><span data-stu-id="78317-162">b.</span></span> <span data-ttu-id="78317-163">W obszarze **Include**, kliknij przycisk **wszystkie lokalizacje**.</span><span class="sxs-lookup"><span data-stu-id="78317-163">Under **Include**, click **All locations**.</span></span>

    <span data-ttu-id="78317-164">c.</span><span class="sxs-lookup"><span data-stu-id="78317-164">c.</span></span> <span data-ttu-id="78317-165">Kliknij przycisk **wykluczyć**, a następnie kliknij przycisk **wszystkich zaufanych adresów IP**.</span><span class="sxs-lookup"><span data-stu-id="78317-165">Click **Exclude**, and then click **All trusted IPs**.</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    <span data-ttu-id="78317-167">d.</span><span class="sxs-lookup"><span data-stu-id="78317-167">d.</span></span> <span data-ttu-id="78317-168">Kliknij przycisk **Gotowe**.</span><span class="sxs-lookup"><span data-stu-id="78317-168">Click **Done**.</span></span>

12. <span data-ttu-id="78317-169">Na powitania **warunki** bloku, kliknij przycisk **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="78317-169">On hello **Conditions** blade, click **Done**.</span></span>

13. <span data-ttu-id="78317-170">Na powitania **nowy** bloku, tooopen hello **Grant** bloku w hello **formanty** kliknij **Grant**.</span><span class="sxs-lookup"><span data-stu-id="78317-170">On hello **New** blade, tooopen hello **Grant** blade, in hello **Controls** section, click **Grant**.</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. <span data-ttu-id="78317-172">Na powitania **Grant** blok, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="78317-172">On hello **Grant** blade, perform hello following steps:</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    <span data-ttu-id="78317-174">a.</span><span class="sxs-lookup"><span data-stu-id="78317-174">a.</span></span> <span data-ttu-id="78317-175">Wybierz **wymusić uwierzytelnianie wieloskładnikowe**.</span><span class="sxs-lookup"><span data-stu-id="78317-175">Select **Require multi-factor authentication**.</span></span>

    <span data-ttu-id="78317-176">b.</span><span class="sxs-lookup"><span data-stu-id="78317-176">b.</span></span> <span data-ttu-id="78317-177">Kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="78317-177">Click **Select**.</span></span>

15. <span data-ttu-id="78317-178">Na powitania **nowy** bloku, w obszarze **Włącz zasady**, kliknij przycisk **na**.</span><span class="sxs-lookup"><span data-stu-id="78317-178">On hello **New** blade, under **Enable policy**, click **On**.</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. <span data-ttu-id="78317-180">Na powitania **nowy** bloku, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="78317-180">On hello **New** blade, click **Create**.</span></span>


## <a name="testing-hello-policy"></a><span data-ttu-id="78317-181">Zasady testowania hello</span><span class="sxs-lookup"><span data-stu-id="78317-181">Testing hello policy</span></span>

<span data-ttu-id="78317-182">tootest zasad, powinien uzyskiwać dostęp aplikacji z urządzenia który:</span><span class="sxs-lookup"><span data-stu-id="78317-182">tootest your policy, you should access your app from a device that:</span></span> 

1. <span data-ttu-id="78317-183">Ma adres IP, który mieści się w sieci skonfigurowanych zaufanych adresów IP</span><span class="sxs-lookup"><span data-stu-id="78317-183">Has an IP address that is within your configured Trusted IPs</span></span> 

1. <span data-ttu-id="78317-184">Ma adres IP, który nie znajduje się w sieci skonfigurowanych zaufanych adresów IP</span><span class="sxs-lookup"><span data-stu-id="78317-184">Has an IP address that is not within your configured Trusted IPs</span></span>

<span data-ttu-id="78317-185">Uwierzytelnianie wieloskładnikowe powinny być wymagana tylko podczas próby połączenia zostało utworzone z urządzenia, które nie znajduje się w sieci skonfigurowanych zaufanych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="78317-185">Multi-factor authentication should only be required during a connection attempt that was made from a device that is not within your configured Trusted IPs.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="78317-186">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="78317-186">Next steps</span></span>

<span data-ttu-id="78317-187">Jeśli chcesz toolearn więcej informacji na temat dostępu warunkowego, zobacz [dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="78317-187">If you would like toolearn more about conditional access, see [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

