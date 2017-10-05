---
title: "Rozpoczynanie pracy z dostępu warunkowego w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Testowanie dostępu warunkowego za pomocą warunku lokalizacji."
services: active-directory
keywords: "dostęp warunkowy do aplikacji, dostęp warunkowy przy użyciu usługi Azure AD, bezpieczny dostęp do zasobów firmy, zasady dostępu warunkowego"
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
ms.openlocfilehash: cd53e8be32d1e98aaf9f72177895871dba69df86
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-conditional-access-in-azure-active-directory"></a><span data-ttu-id="5a414-104">Rozpoczynanie pracy z dostępu warunkowego w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5a414-104">Get started with conditional access in Azure Active Directory</span></span>

<span data-ttu-id="5a414-105">Dostęp warunkowy jest możliwość usługi Azure Active Directory, który umożliwia zdefiniowanie warunków, w których autoryzowani użytkownicy mają dostęp do Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5a414-105">Conditional access is a capability of Azure Active Directory that enables you to define conditions under which authorized users can access your apps.</span></span> 

<span data-ttu-id="5a414-106">Ten temat zawiera instrukcje dotyczące testowania dostępu warunkowego na podstawie warunku lokalizacji w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="5a414-106">This topic provides you with instructions for testing a conditional access based on a location condition in your environment.</span></span>  


## <a name="scenario-description"></a><span data-ttu-id="5a414-107">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5a414-107">Scenario description</span></span>

<span data-ttu-id="5a414-108">Jednym z typowych wymagań w wielu organizacjach jest wymagane tylko uwierzytelnianie wieloskładnikowe dla dostępu do aplikacji, która nie jest wykonywane od firmowego intranetu.</span><span class="sxs-lookup"><span data-stu-id="5a414-108">One common requirement in many organizations is to only require multi-factor authentication for access to apps that is not performed from the corporate intranet.</span></span> <span data-ttu-id="5a414-109">Z usługą Azure Active Directory można łatwo realizację tego celu, konfigurując zasady dostępu warunkowego na podstawie lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="5a414-109">With Azure Active Directory, you can easily accomplish this goal by configuring a location-based conditional access policy.</span></span> <span data-ttu-id="5a414-110">W tym temacie przedstawiono szczegółowe instrukcje dotyczące konfigurowania pokrewnych zasad.</span><span class="sxs-lookup"><span data-stu-id="5a414-110">This topic provides you with detailed instructions for configuring a related policy.</span></span> <span data-ttu-id="5a414-111">Wykorzystanie zasad [zaufanych adresów IP](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) odróżnienie z firmowej prób dostępu do wszystkich innych lokalizacji w intranecie i.</span><span class="sxs-lookup"><span data-stu-id="5a414-111">The policy leverages [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips) to distinguish between access attempts made from the corporate's intranet and all other locations.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="5a414-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5a414-112">Prerequisites</span></span>

<span data-ttu-id="5a414-113">Scenariusz opisany w tym temacie założono, że znasz pojęcia opisane w [dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5a414-113">The scenario outlined in this topic assumes that you are familiar with the concepts outlined in [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

<span data-ttu-id="5a414-114">Do przetestowania tego scenariusza, należy:</span><span class="sxs-lookup"><span data-stu-id="5a414-114">To test this scenario, you need to:</span></span>

- <span data-ttu-id="5a414-115">Tworzenie użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="5a414-115">Create a test user</span></span> 

- <span data-ttu-id="5a414-116">Przypisywanie licencji usługi Azure AD Premium do użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="5a414-116">Assign an Azure AD Premium license to the test user</span></span>

- <span data-ttu-id="5a414-117">Konfigurowanie zarządzanych aplikacji i przypisać użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="5a414-117">Configure a managed app and assign your test user to it</span></span>

- <span data-ttu-id="5a414-118">Skonfiguruj listę zaufanych adresów IP</span><span class="sxs-lookup"><span data-stu-id="5a414-118">Configure trusted IPs</span></span>

<span data-ttu-id="5a414-119">Aby uzyskać więcej informacji na temat zaufanych adresów IP, zobacz [zaufanych adresów IP](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="5a414-119">If you need more details about Trusted IPs, see [Trusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="policy-configuration-steps"></a><span data-ttu-id="5a414-120">Kroki konfiguracji zasad</span><span class="sxs-lookup"><span data-stu-id="5a414-120">Policy configuration steps</span></span>

<span data-ttu-id="5a414-121">**Aby skonfigurować zasady dostępu warunkowego, należy wykonać:**</span><span class="sxs-lookup"><span data-stu-id="5a414-121">**To configure your conditional access policy, do:**</span></span>

1. <span data-ttu-id="5a414-122">W portalu Azure na lewy pasek nawigacyjny, kliknij przycisk **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5a414-122">In the Azure portal, on the left navbar, click **Azure Active Directory**.</span></span> 

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/01.png)

2. <span data-ttu-id="5a414-124">Na **usługi Azure Active Directory** bloku, w **Zarządzaj** kliknij **dostępu warunkowego**.</span><span class="sxs-lookup"><span data-stu-id="5a414-124">On the **Azure Active Directory** blade, in the **Manage** section, click **Conditional access**.</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/02.png)
 
3. <span data-ttu-id="5a414-126">Na **dostępu warunkowego** bloku, aby otworzyć **nowy** bloku na pasku narzędzi u góry, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="5a414-126">On the **Conditional Access** blade, to open the **New** blade, in the toolbar on the top, click **Add**.</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/03.png)

4. <span data-ttu-id="5a414-128">Na **nowy** bloku, w **nazwa** tekstowym, wpisz nazwę zasady.</span><span class="sxs-lookup"><span data-stu-id="5a414-128">On the **New** blade, in the **Name** textbox, type a name for your policy.</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/04.png)

5. <span data-ttu-id="5a414-130">W **przypisania** kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5a414-130">In the **Assignment** section, click **Users and groups**.</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/05.png)

6. <span data-ttu-id="5a414-132">Na **użytkowników i grup** blok, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5a414-132">On the **Users and groups** blade, perform the following steps:</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/06.png)

    <span data-ttu-id="5a414-134">a.</span><span class="sxs-lookup"><span data-stu-id="5a414-134">a.</span></span> <span data-ttu-id="5a414-135">Kliknij przycisk **Wybierz użytkowników i grupy**.</span><span class="sxs-lookup"><span data-stu-id="5a414-135">Click **Select users and groups**.</span></span>

    <span data-ttu-id="5a414-136">b.</span><span class="sxs-lookup"><span data-stu-id="5a414-136">b.</span></span> <span data-ttu-id="5a414-137">Kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="5a414-137">Click **Select**.</span></span>

    <span data-ttu-id="5a414-138">c.</span><span class="sxs-lookup"><span data-stu-id="5a414-138">c.</span></span> <span data-ttu-id="5a414-139">Na **wybierz** bloku, wybierz użytkownika testowego, a następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="5a414-139">On the **Select** blade, select your test user, and then click **Select**.</span></span>

    <span data-ttu-id="5a414-140">d.</span><span class="sxs-lookup"><span data-stu-id="5a414-140">d.</span></span> <span data-ttu-id="5a414-141">Na **użytkowników i grup** bloku, kliknij przycisk **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="5a414-141">On the **Users and groups** blade, click **Done**.</span></span>

7. <span data-ttu-id="5a414-142">Na **nowy** bloku, aby otworzyć **aplikacji w chmurze** bloku, w **przypisania** kliknij **aplikacji w chmurze**.</span><span class="sxs-lookup"><span data-stu-id="5a414-142">On the **New** blade, to open the **Cloud apps** blade, in the **Assignment** section, click **Cloud apps**.</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/07.png)

8. <span data-ttu-id="5a414-144">Na **aplikacji w chmurze** blok, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5a414-144">On the **Cloud apps** blade, perform the following steps:</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/08.png)

    <span data-ttu-id="5a414-146">a.</span><span class="sxs-lookup"><span data-stu-id="5a414-146">a.</span></span> <span data-ttu-id="5a414-147">Kliknij przycisk **Wybierz aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5a414-147">Click **Select apps**.</span></span>

    <span data-ttu-id="5a414-148">b.</span><span class="sxs-lookup"><span data-stu-id="5a414-148">b.</span></span> <span data-ttu-id="5a414-149">Kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="5a414-149">Click **Select**.</span></span>

    <span data-ttu-id="5a414-150">c.</span><span class="sxs-lookup"><span data-stu-id="5a414-150">c.</span></span> <span data-ttu-id="5a414-151">Na **wybierz** bloku, wybierz aplikacji w chmurze, a następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="5a414-151">On the **Select** blade, select your cloud app, and then click **Select**.</span></span>

    <span data-ttu-id="5a414-152">d.</span><span class="sxs-lookup"><span data-stu-id="5a414-152">d.</span></span> <span data-ttu-id="5a414-153">Na **aplikacji w chmurze** bloku, kliknij przycisk **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="5a414-153">On the **Cloud apps** blade, click **Done**.</span></span>

9. <span data-ttu-id="5a414-154">Na **nowy** bloku, aby otworzyć **warunki** bloku, w **przypisania** kliknij **warunki**.</span><span class="sxs-lookup"><span data-stu-id="5a414-154">On the **New** blade, to open the **Conditions** blade, in the **Assignment** section, click **Conditions**.</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/09.png)

10. <span data-ttu-id="5a414-156">Na **warunki** bloku, aby otworzyć **lokalizacje** bloku, kliknij przycisk **lokalizacje**.</span><span class="sxs-lookup"><span data-stu-id="5a414-156">On the **Conditions** blade, to open the **Locations** blade, click **Locations**.</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/10.png)

11. <span data-ttu-id="5a414-158">Na **lokalizacje** blok, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5a414-158">On the **Locations** blade, perform the following steps:</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/11.png)

    <span data-ttu-id="5a414-160">a.</span><span class="sxs-lookup"><span data-stu-id="5a414-160">a.</span></span> <span data-ttu-id="5a414-161">W obszarze **Konfiguruj**, kliknij przycisk **tak**.</span><span class="sxs-lookup"><span data-stu-id="5a414-161">Under **Configure**, click **Yes**.</span></span>

    <span data-ttu-id="5a414-162">b.</span><span class="sxs-lookup"><span data-stu-id="5a414-162">b.</span></span> <span data-ttu-id="5a414-163">W obszarze **Include**, kliknij przycisk **wszystkie lokalizacje**.</span><span class="sxs-lookup"><span data-stu-id="5a414-163">Under **Include**, click **All locations**.</span></span>

    <span data-ttu-id="5a414-164">c.</span><span class="sxs-lookup"><span data-stu-id="5a414-164">c.</span></span> <span data-ttu-id="5a414-165">Kliknij przycisk **wykluczyć**, a następnie kliknij przycisk **wszystkich zaufanych adresów IP**.</span><span class="sxs-lookup"><span data-stu-id="5a414-165">Click **Exclude**, and then click **All trusted IPs**.</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/12.png)

    <span data-ttu-id="5a414-167">d.</span><span class="sxs-lookup"><span data-stu-id="5a414-167">d.</span></span> <span data-ttu-id="5a414-168">Kliknij przycisk **Gotowe**.</span><span class="sxs-lookup"><span data-stu-id="5a414-168">Click **Done**.</span></span>

12. <span data-ttu-id="5a414-169">Na **warunki** bloku, kliknij przycisk **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="5a414-169">On the **Conditions** blade, click **Done**.</span></span>

13. <span data-ttu-id="5a414-170">Na **nowy** bloku, aby otworzyć **Grant** bloku, w **formanty** kliknij **Grant**.</span><span class="sxs-lookup"><span data-stu-id="5a414-170">On the **New** blade, to open the **Grant** blade, in the **Controls** section, click **Grant**.</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/13.png)

14. <span data-ttu-id="5a414-172">Na **Grant** blok, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5a414-172">On the **Grant** blade, perform the following steps:</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/14.png)

    <span data-ttu-id="5a414-174">a.</span><span class="sxs-lookup"><span data-stu-id="5a414-174">a.</span></span> <span data-ttu-id="5a414-175">Wybierz **wymusić uwierzytelnianie wieloskładnikowe**.</span><span class="sxs-lookup"><span data-stu-id="5a414-175">Select **Require multi-factor authentication**.</span></span>

    <span data-ttu-id="5a414-176">b.</span><span class="sxs-lookup"><span data-stu-id="5a414-176">b.</span></span> <span data-ttu-id="5a414-177">Kliknij pozycję **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="5a414-177">Click **Select**.</span></span>

15. <span data-ttu-id="5a414-178">Na **nowy** bloku, w obszarze **Włącz zasady**, kliknij przycisk **na**.</span><span class="sxs-lookup"><span data-stu-id="5a414-178">On the **New** blade, under **Enable policy**, click **On**.</span></span>

    ![Dostęp warunkowy](./media/active-directory-conditional-access-azure-portal-get-started/15.png)

16. <span data-ttu-id="5a414-180">Na **nowy** bloku, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5a414-180">On the **New** blade, click **Create**.</span></span>


## <a name="testing-the-policy"></a><span data-ttu-id="5a414-181">Testowanie zasad</span><span class="sxs-lookup"><span data-stu-id="5a414-181">Testing the policy</span></span>

<span data-ttu-id="5a414-182">Do testowania zasad, powinien dostęp aplikacji z urządzenia, które:</span><span class="sxs-lookup"><span data-stu-id="5a414-182">To test your policy, you should access your app from a device that:</span></span> 

1. <span data-ttu-id="5a414-183">Ma adres IP, który mieści się w sieci skonfigurowanych zaufanych adresów IP</span><span class="sxs-lookup"><span data-stu-id="5a414-183">Has an IP address that is within your configured Trusted IPs</span></span> 

1. <span data-ttu-id="5a414-184">Ma adres IP, który nie znajduje się w sieci skonfigurowanych zaufanych adresów IP</span><span class="sxs-lookup"><span data-stu-id="5a414-184">Has an IP address that is not within your configured Trusted IPs</span></span>

<span data-ttu-id="5a414-185">Uwierzytelnianie wieloskładnikowe powinny być wymagana tylko podczas próby połączenia zostało utworzone z urządzenia, które nie znajduje się w sieci skonfigurowanych zaufanych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="5a414-185">Multi-factor authentication should only be required during a connection attempt that was made from a device that is not within your configured Trusted IPs.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="5a414-186">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5a414-186">Next steps</span></span>

<span data-ttu-id="5a414-187">Jeśli chcesz dowiedzieć się więcej na temat dostępu warunkowego, zobacz [dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5a414-187">If you would like to learn more about conditional access, see [Azure Active Directory conditional access](active-directory-conditional-access-azure-portal.md).</span></span>

