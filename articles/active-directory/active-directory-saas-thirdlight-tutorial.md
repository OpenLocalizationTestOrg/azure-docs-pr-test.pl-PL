---
title: 'Samouczek: Integracji Azure Active Directory z ThirdLight | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i ThirdLight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 168aae9a-54ee-4c2b-ab12-650a2c62b901
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: ee7710cfea3a13907c0cc940a98c875bf83607a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thirdlight"></a><span data-ttu-id="857d7-103">Samouczek: Integracji Azure Active Directory z ThirdLight</span><span class="sxs-lookup"><span data-stu-id="857d7-103">Tutorial: Azure Active Directory integration with ThirdLight</span></span>

<span data-ttu-id="857d7-104">Z tego samouczka dowiesz się integrowanie ThirdLight z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="857d7-104">In this tutorial, you learn how to integrate ThirdLight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="857d7-105">Integracja z usługą Azure AD ThirdLight zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="857d7-105">Integrating ThirdLight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="857d7-106">Można kontrolować w usłudze Azure AD, który ma dostęp do ThirdLight</span><span class="sxs-lookup"><span data-stu-id="857d7-106">You can control in Azure AD who has access to ThirdLight</span></span>
- <span data-ttu-id="857d7-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do ThirdLight (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="857d7-107">You can enable your users to automatically get signed-on to ThirdLight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="857d7-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="857d7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="857d7-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="857d7-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="857d7-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="857d7-110">Prerequisites</span></span>

<span data-ttu-id="857d7-111">Aby skonfigurować integrację usługi Azure AD z ThirdLight, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="857d7-111">To configure Azure AD integration with ThirdLight, you need the following items:</span></span>

- <span data-ttu-id="857d7-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="857d7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="857d7-113">ThirdLight jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="857d7-113">A ThirdLight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="857d7-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="857d7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="857d7-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="857d7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="857d7-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="857d7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="857d7-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="857d7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="857d7-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="857d7-118">Scenario description</span></span>
<span data-ttu-id="857d7-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="857d7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="857d7-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="857d7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="857d7-121">Dodawanie ThirdLight z galerii</span><span class="sxs-lookup"><span data-stu-id="857d7-121">Adding ThirdLight from the gallery</span></span>
2. <span data-ttu-id="857d7-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="857d7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thirdlight-from-the-gallery"></a><span data-ttu-id="857d7-123">Dodawanie ThirdLight z galerii</span><span class="sxs-lookup"><span data-stu-id="857d7-123">Adding ThirdLight from the gallery</span></span>
<span data-ttu-id="857d7-124">Aby skonfigurować integrację usługi Azure AD ThirdLight, należy dodać ThirdLight z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="857d7-124">To configure the integration of ThirdLight into Azure AD, you need to add ThirdLight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="857d7-125">**Aby dodać ThirdLight z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="857d7-125">**To add ThirdLight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="857d7-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="857d7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="857d7-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="857d7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="857d7-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="857d7-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="857d7-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="857d7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="857d7-133">W polu wyszukiwania wpisz **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="857d7-133">In the search box, type **ThirdLight**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_search.png)

5. <span data-ttu-id="857d7-135">W panelu wyników wybierz **ThirdLight**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="857d7-135">In the results panel, select **ThirdLight**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="857d7-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="857d7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="857d7-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ThirdLight na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="857d7-138">In this section, you configure and test Azure AD single sign-on with ThirdLight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="857d7-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w ThirdLight jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="857d7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ThirdLight is to a user in Azure AD.</span></span> <span data-ttu-id="857d7-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w ThirdLight musi się.</span><span class="sxs-lookup"><span data-stu-id="857d7-140">In other words, a link relationship between an Azure AD user and the related user in ThirdLight needs to be established.</span></span>

<span data-ttu-id="857d7-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="857d7-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ThirdLight.</span></span>

<span data-ttu-id="857d7-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ThirdLight, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="857d7-142">To configure and test Azure AD single sign-on with ThirdLight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="857d7-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="857d7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="857d7-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="857d7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="857d7-145">**[Tworzenie użytkownika testowego ThirdLight](#creating-a-thirdlight-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta ThirdLight połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="857d7-145">**[Creating a ThirdLight test user](#creating-a-thirdlight-test-user)** - to have a counterpart of Britta Simon in ThirdLight that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="857d7-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="857d7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="857d7-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="857d7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="857d7-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="857d7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="857d7-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="857d7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ThirdLight application.</span></span>

<span data-ttu-id="857d7-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z ThirdLight, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="857d7-150">**To configure Azure AD single sign-on with ThirdLight, perform the following steps:**</span></span>

1. <span data-ttu-id="857d7-151">W portalu Azure na **ThirdLight** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="857d7-151">In the Azure portal, on the **ThirdLight** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="857d7-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="857d7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_samlbase.png)

3. <span data-ttu-id="857d7-155">Na **ThirdLight domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="857d7-155">On the **ThirdLight Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_url.png)

    <span data-ttu-id="857d7-157">a.</span><span class="sxs-lookup"><span data-stu-id="857d7-157">a.</span></span> <span data-ttu-id="857d7-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.thirdlight.com/`</span><span class="sxs-lookup"><span data-stu-id="857d7-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.thirdlight.com/`</span></span>

    <span data-ttu-id="857d7-159">b.</span><span class="sxs-lookup"><span data-stu-id="857d7-159">b.</span></span> <span data-ttu-id="857d7-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.thirdlight.com/saml/sp`</span><span class="sxs-lookup"><span data-stu-id="857d7-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.thirdlight.com/saml/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="857d7-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="857d7-161">These values are not real.</span></span> <span data-ttu-id="857d7-162">Rzeczywisty adres URL logowania i Identiifer, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="857d7-162">Update these values with the actual Sign-On URL and Identiifer.</span></span> <span data-ttu-id="857d7-163">Skontaktuj się z [zespołem pomocy technicznej klienta ThirdLight](https://www.thirdlight.com/support) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="857d7-163">Contact [ThirdLight Client support team](https://www.thirdlight.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="857d7-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="857d7-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_certificate.png) 

5. <span data-ttu-id="857d7-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="857d7-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thirdlight-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="857d7-168">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="857d7-168">In a different web browser window, log in to your ThirdLight company site as an administrator.</span></span>

7. <span data-ttu-id="857d7-169">Przejdź do **konfiguracji \> Administracja systemu**, a następnie kliknij przycisk **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="857d7-169">Go to **Configuration \> System Administration**, and then click **SAML2**.</span></span>
   
    <span data-ttu-id="857d7-170">![Administrowanie systemem](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "administracji systemu")</span><span class="sxs-lookup"><span data-stu-id="857d7-170">![System Administration](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "System Administration")</span></span>

8. <span data-ttu-id="857d7-171">W sekcji konfiguracji SAML2 wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="857d7-171">In the SAML2 configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="857d7-172">![SAML logowania jednokrotnego](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "SAML logowania jednokrotnego")</span><span class="sxs-lookup"><span data-stu-id="857d7-172">![SAML Single Sign-On](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "SAML Single Sign-On")</span></span>   

     <span data-ttu-id="857d7-173">a.</span><span class="sxs-lookup"><span data-stu-id="857d7-173">a.</span></span> <span data-ttu-id="857d7-174">Wybierz **włączyć SAML2 rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="857d7-174">Select **Enable SAML2 Single Sign-On**.</span></span>
 
     <span data-ttu-id="857d7-175">b.</span><span class="sxs-lookup"><span data-stu-id="857d7-175">b.</span></span> <span data-ttu-id="857d7-176">Jako **źródła metadanych IdP**, wybierz pozycję **obciążenia IdP metadanych z pliku XML**.</span><span class="sxs-lookup"><span data-stu-id="857d7-176">As **Source for IdP Metadata**, select **Load IdP Metadata from XML**.</span></span>
 
     <span data-ttu-id="857d7-177">c.</span><span class="sxs-lookup"><span data-stu-id="857d7-177">c.</span></span> <span data-ttu-id="857d7-178">Otwórz plik metadanych pobranych, skopiuj zawartość, a następnie wklej go do **XML metadanych IdP** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="857d7-178">Open the downloaded metadata file, copy the content, and then paste it into the **IdP Metadata XML** textbox.</span></span> 
     
     <span data-ttu-id="857d7-179">d.</span><span class="sxs-lookup"><span data-stu-id="857d7-179">d.</span></span> <span data-ttu-id="857d7-180">Kliknij przycisk **SAML2 Zapisz ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="857d7-180">Click **Save SAML2 settings**.</span></span>

> [!TIP]
> <span data-ttu-id="857d7-181">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="857d7-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="857d7-182">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="857d7-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="857d7-183">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="857d7-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="857d7-184">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="857d7-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="857d7-185">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="857d7-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="857d7-187">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="857d7-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="857d7-188">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="857d7-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="857d7-190">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="857d7-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="857d7-192">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="857d7-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="857d7-194">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="857d7-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="857d7-196">a.</span><span class="sxs-lookup"><span data-stu-id="857d7-196">a.</span></span> <span data-ttu-id="857d7-197">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="857d7-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="857d7-198">b.</span><span class="sxs-lookup"><span data-stu-id="857d7-198">b.</span></span> <span data-ttu-id="857d7-199">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="857d7-199">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="857d7-200">c.</span><span class="sxs-lookup"><span data-stu-id="857d7-200">c.</span></span> <span data-ttu-id="857d7-201">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="857d7-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="857d7-202">d.</span><span class="sxs-lookup"><span data-stu-id="857d7-202">d.</span></span> <span data-ttu-id="857d7-203">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="857d7-203">Click **Create**.</span></span>
 
### <a name="creating-a-thirdlight-test-user"></a><span data-ttu-id="857d7-204">Tworzenie użytkownika testowego ThirdLight</span><span class="sxs-lookup"><span data-stu-id="857d7-204">Creating a ThirdLight test user</span></span>

<span data-ttu-id="857d7-205">Aby umożliwić użytkownikom usługi Azure AD zalogować się do ThirdLight, musi być przygotowana do ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="857d7-205">To enable Azure AD users to log in to ThirdLight, they must be provisioned into ThirdLight.</span></span>  
<span data-ttu-id="857d7-206">W przypadku ThirdLight Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="857d7-206">In the case of ThirdLight, provisioning is a manual task.</span></span>

<span data-ttu-id="857d7-207">**Aby udostępnić konta użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="857d7-207">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="857d7-208">Zaloguj się do Twojego **ThirdLight** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="857d7-208">Log in to your **ThirdLight** company site as an administrator.</span></span>

2. <span data-ttu-id="857d7-209">Przejdź do **użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="857d7-209">Go to **Users** tab.</span></span>

3. <span data-ttu-id="857d7-210">Wybierz **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="857d7-210">Select **Users and Groups**.</span></span>

4. <span data-ttu-id="857d7-211">Kliknij przycisk **Dodaj nowego użytkownika** przycisku.</span><span class="sxs-lookup"><span data-stu-id="857d7-211">Click **Add new User** button.</span></span>

5. <span data-ttu-id="857d7-212">Wprowadź **nazwy użytkownika, nazwa lub opis, poczty E-mail, wybierz ustawienie wstępne lub grupy nowych członków** chcesz udostępnić poprawnego konta usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="857d7-212">Enter **the Username, Name or Description, Email, Choose a Preset or Group of New Members** of a valid AAD account you want to provision.</span></span>

6. <span data-ttu-id="857d7-213">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="857d7-213">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="857d7-214">Możesz użyć innych Thirdlight użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Thirdlight do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="857d7-214">You can use any other Thirdlight user account creation tools or APIs provided by Thirdlight to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="857d7-215">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="857d7-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="857d7-216">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="857d7-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ThirdLight.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="857d7-218">**Aby przypisać Simona Britta ThirdLight, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="857d7-218">**To assign Britta Simon to ThirdLight, perform the following steps:**</span></span>

1. <span data-ttu-id="857d7-219">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="857d7-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="857d7-221">Na liście aplikacji zaznacz **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="857d7-221">In the applications list, select **ThirdLight**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_app.png) 

3. <span data-ttu-id="857d7-223">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="857d7-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="857d7-225">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="857d7-225">Click **Add** button.</span></span> <span data-ttu-id="857d7-226">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="857d7-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="857d7-228">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="857d7-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="857d7-229">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="857d7-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="857d7-230">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="857d7-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="857d7-231">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="857d7-231">Testing single sign-on</span></span>

<span data-ttu-id="857d7-232">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="857d7-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="857d7-233">Po kliknięciu kafelka ThirdLight w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="857d7-233">When you click the ThirdLight tile in the Access Panel, you should get automatically signed-on to your ThirdLight application.</span></span>
<span data-ttu-id="857d7-234">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="857d7-234">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="857d7-235">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="857d7-235">Additional resources</span></span>

* [<span data-ttu-id="857d7-236">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="857d7-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="857d7-237">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="857d7-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_203.png

