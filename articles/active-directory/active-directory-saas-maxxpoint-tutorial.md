---
title: 'Samouczek: Integracji Azure Active Directory z MaxxPoint | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i MaxxPoint."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ba026e-96fc-4ae8-b135-0169da810e99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 8a7481b71df5ca407dbed5da3d3cc26991504c82
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-maxxpoint"></a><span data-ttu-id="5d770-103">Samouczek: Integracji Azure Active Directory z MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="5d770-103">Tutorial: Azure Active Directory integration with MaxxPoint</span></span>

<span data-ttu-id="5d770-104">Z tego samouczka dowiesz się integrowanie MaxxPoint z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5d770-104">In this tutorial, you learn how to integrate MaxxPoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5d770-105">Integracja z usługą Azure AD MaxxPoint zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5d770-105">Integrating MaxxPoint with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5d770-106">Można kontrolować w usłudze Azure AD, który ma dostęp do MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="5d770-106">You can control in Azure AD who has access to MaxxPoint</span></span>
- <span data-ttu-id="5d770-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do MaxxPoint (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d770-107">You can enable your users to automatically get signed-on to MaxxPoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5d770-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5d770-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5d770-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5d770-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d770-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5d770-110">Prerequisites</span></span>

<span data-ttu-id="5d770-111">Aby skonfigurować integrację usługi Azure AD z MaxxPoint, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5d770-111">To configure Azure AD integration with MaxxPoint, you need the following items:</span></span>

- <span data-ttu-id="5d770-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d770-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5d770-113">MaxxPoint jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5d770-113">A MaxxPoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5d770-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5d770-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5d770-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5d770-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5d770-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5d770-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="5d770-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5d770-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5d770-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5d770-118">Scenario description</span></span>
<span data-ttu-id="5d770-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5d770-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5d770-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5d770-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5d770-121">Dodawanie MaxxPoint z galerii</span><span class="sxs-lookup"><span data-stu-id="5d770-121">Adding MaxxPoint from the gallery</span></span>
2. <span data-ttu-id="5d770-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5d770-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-maxxpoint-from-the-gallery"></a><span data-ttu-id="5d770-123">Dodawanie MaxxPoint z galerii</span><span class="sxs-lookup"><span data-stu-id="5d770-123">Adding MaxxPoint from the gallery</span></span>
<span data-ttu-id="5d770-124">Aby skonfigurować integrację usługi Azure AD MaxxPoint, należy dodać MaxxPoint z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5d770-124">To configure the integration of MaxxPoint into Azure AD, you need to add MaxxPoint from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5d770-125">**Aby dodać MaxxPoint z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5d770-125">**To add MaxxPoint from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5d770-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5d770-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="5d770-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5d770-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5d770-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5d770-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="5d770-131">Kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego, aby dodać nową aplikację.</span><span class="sxs-lookup"><span data-stu-id="5d770-131">Click **New application** button on the top of dialog to add new application.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="5d770-133">W polu wyszukiwania wpisz **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="5d770-133">In the search box, type **MaxxPoint**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_001.png)

5. <span data-ttu-id="5d770-135">W panelu wyników wybierz **MaxxPoint**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="5d770-135">In the results panel, select **MaxxPoint**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5d770-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5d770-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5d770-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z MaxxPoint w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="5d770-138">In this section, you configure and test Azure AD single sign-on with MaxxPoint based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5d770-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w MaxxPoint jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d770-139">For single sign-on to work, Azure AD needs to know what the counterpart user in MaxxPoint is to a user in Azure AD.</span></span> <span data-ttu-id="5d770-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w MaxxPoint musi się.</span><span class="sxs-lookup"><span data-stu-id="5d770-140">In other words, a link relationship between an Azure AD user and the related user in MaxxPoint needs to be established.</span></span>

<span data-ttu-id="5d770-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="5d770-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in MaxxPoint.</span></span>

<span data-ttu-id="5d770-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z MaxxPoint, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="5d770-142">To configure and test Azure AD single sign-on with MaxxPoint, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5d770-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5d770-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5d770-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5d770-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5d770-145">**[Tworzenie użytkownika testowego MaxxPoint](#creating-a-maxxpoint-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta MaxxPoint połączonego z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d770-145">**[Creating a MaxxPoint test user](#creating-a-maxxpoint-test-user)** - to have a counterpart of Britta Simon in MaxxPoint that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="5d770-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5d770-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5d770-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="5d770-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5d770-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5d770-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5d770-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="5d770-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MaxxPoint application.</span></span>

<span data-ttu-id="5d770-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z MaxxPoint, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5d770-150">**To configure Azure AD single sign-on with MaxxPoint, perform the following steps:**</span></span>

1. <span data-ttu-id="5d770-151">W portalu Azure na **MaxxPoint** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="5d770-151">In the Azure portal, on the **MaxxPoint** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="5d770-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="5d770-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_300.png)

3. <span data-ttu-id="5d770-155">Na **MaxxPoint domeny i adres URL** sekcji, jeśli chcesz skonfigurować aplikację w **IDP zainicjował tryb**, nie trzeba wykonywać żadnych czynności.</span><span class="sxs-lookup"><span data-stu-id="5d770-155">On the **MaxxPoint Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, no need to perform any steps.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_02.png)
    
4. <span data-ttu-id="5d770-157">Na **MaxxPoint domeny i adres URL** sekcji, jeśli chcesz skonfigurować aplikację w **SP zainicjował tryb**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5d770-157">On the **MaxxPoint Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_03.png)

    <span data-ttu-id="5d770-159">a.</span><span class="sxs-lookup"><span data-stu-id="5d770-159">a.</span></span> <span data-ttu-id="5d770-160">Kliknij przycisk **Pokaż zaawansowane ustawienia adresu URL** opcji</span><span class="sxs-lookup"><span data-stu-id="5d770-160">Click **Show advanced URL settings** option</span></span>

    <span data-ttu-id="5d770-161">b.</span><span class="sxs-lookup"><span data-stu-id="5d770-161">b.</span></span> <span data-ttu-id="5d770-162">W **na adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span><span class="sxs-lookup"><span data-stu-id="5d770-162">In the **Sign On URL** textbox, type a URL using the following pattern: `https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5d770-163">Należy pamiętać, że nie jest rzeczywistą wartość.</span><span class="sxs-lookup"><span data-stu-id="5d770-163">Please note that this is not the real value.</span></span> <span data-ttu-id="5d770-164">Należy zaktualizować tę wartość rzeczywista logowania na adres URL.</span><span class="sxs-lookup"><span data-stu-id="5d770-164">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="5d770-165">Wywołanie MaxxPoint zespołu na **888-728-0950** aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="5d770-165">Call MaxxPoint team on **888-728-0950** to get this value.</span></span>

5. <span data-ttu-id="5d770-166">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5d770-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_06.png) 

6. <span data-ttu-id="5d770-168">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5d770-168">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="5d770-170">Uzyskanie logowania jednokrotnego skonfigurowane dla aplikacji, należy wywołać MaxxPoint zespołem pomocy technicznej dla **888-728-0950** i będą pomocne podczas dalszej dostarczania ich pobrany **XML metadanych** pliku.</span><span class="sxs-lookup"><span data-stu-id="5d770-170">To get SSO configured for your application, call MaxxPoint support team on **888-728-0950** and they'll assist you further on how to provide them the downloaded **Metadata XML** file.</span></span> 

> [!TIP]
> <span data-ttu-id="5d770-171">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="5d770-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5d770-172">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="5d770-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5d770-173">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5d770-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5d770-174">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d770-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="5d770-175">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5d770-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="5d770-177">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5d770-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5d770-178">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5d770-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5d770-180">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="5d770-180">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5d770-182">W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5d770-182">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5d770-184">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5d770-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5d770-186">a.</span><span class="sxs-lookup"><span data-stu-id="5d770-186">a.</span></span> <span data-ttu-id="5d770-187">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5d770-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5d770-188">b.</span><span class="sxs-lookup"><span data-stu-id="5d770-188">b.</span></span> <span data-ttu-id="5d770-189">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5d770-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5d770-190">c.</span><span class="sxs-lookup"><span data-stu-id="5d770-190">c.</span></span> <span data-ttu-id="5d770-191">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="5d770-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5d770-192">d.</span><span class="sxs-lookup"><span data-stu-id="5d770-192">d.</span></span> <span data-ttu-id="5d770-193">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5d770-193">Click **Create**.</span></span> 

### <a name="creating-a-maxxpoint-test-user"></a><span data-ttu-id="5d770-194">Tworzenie użytkownika testowego MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="5d770-194">Creating a MaxxPoint test user</span></span>

<span data-ttu-id="5d770-195">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="5d770-195">In this section, you create a user called Britta Simon in MaxxPoint.</span></span> <span data-ttu-id="5d770-196">Skontaktuj się z działem MaxxPoint zespołem pomocy technicznej na **888-728-0950** Aby dodać użytkowników w aplikacji MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="5d770-196">Please call MaxxPoint support team on **888-728-0950** to add the users in the MaxxPoint application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5d770-197">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d770-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5d770-198">W tej sekcji można włączyć Simona Britta do udostępnienia jej MaxxPoint za pomocą usługi Azure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5d770-198">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to MaxxPoint.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="5d770-200">**Aby przypisać Simona Britta MaxxPoint, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5d770-200">**To assign Britta Simon to MaxxPoint, perform the following steps:**</span></span>

1. <span data-ttu-id="5d770-201">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5d770-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5d770-203">Na liście aplikacji zaznacz **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="5d770-203">In the applications list, select **MaxxPoint**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_50.png) 

3. <span data-ttu-id="5d770-205">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5d770-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="5d770-207">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5d770-207">Click **Add** button.</span></span> <span data-ttu-id="5d770-208">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5d770-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="5d770-210">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="5d770-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5d770-211">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5d770-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5d770-212">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5d770-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5d770-213">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5d770-213">Testing single sign-on</span></span>

<span data-ttu-id="5d770-214">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5d770-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5d770-215">Po kliknięciu kafelka MaxxPoint w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="5d770-215">When you click the MaxxPoint tile in the Access Panel, you should get automatically signed-on to your MaxxPoint application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="5d770-216">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5d770-216">Additional resources</span></span>

* [<span data-ttu-id="5d770-217">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d770-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5d770-218">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5d770-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_203.png