---
title: 'Samouczek: Integracji Azure Active Directory z Novatus | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Novatus."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2f13779-bdb7-4408-9738-be67ed3de4e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2017
ms.author: jeedes
ms.openlocfilehash: ec67e96309a8877e6fb65b30da1501e4f34a9ee4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-novatus"></a><span data-ttu-id="bf882-103">Samouczek: Integracji Azure Active Directory z Novatus</span><span class="sxs-lookup"><span data-stu-id="bf882-103">Tutorial: Azure Active Directory integration with Novatus</span></span>

<span data-ttu-id="bf882-104">Z tego samouczka dowiesz się integrowanie Novatus z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bf882-104">In this tutorial, you learn how to integrate Novatus with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bf882-105">Integracja z usługą Azure AD Novatus zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="bf882-105">Integrating Novatus with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bf882-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Novatus</span><span class="sxs-lookup"><span data-stu-id="bf882-106">You can control in Azure AD who has access to Novatus</span></span>
- <span data-ttu-id="bf882-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Novatus (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf882-107">You can enable your users to automatically get signed-on to Novatus (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bf882-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bf882-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bf882-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bf882-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf882-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bf882-110">Prerequisites</span></span>

<span data-ttu-id="bf882-111">Aby skonfigurować integrację usługi Azure AD z Novatus, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="bf882-111">To configure Azure AD integration with Novatus, you need the following items:</span></span>

- <span data-ttu-id="bf882-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf882-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bf882-113">Novatus logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="bf882-113">A Novatus single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bf882-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="bf882-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bf882-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="bf882-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bf882-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="bf882-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bf882-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bf882-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bf882-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="bf882-118">Scenario description</span></span>
<span data-ttu-id="bf882-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="bf882-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bf882-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="bf882-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bf882-121">Dodawanie Novatus z galerii</span><span class="sxs-lookup"><span data-stu-id="bf882-121">Adding Novatus from the gallery</span></span>
2. <span data-ttu-id="bf882-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bf882-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-novatus-from-the-gallery"></a><span data-ttu-id="bf882-123">Dodawanie Novatus z galerii</span><span class="sxs-lookup"><span data-stu-id="bf882-123">Adding Novatus from the gallery</span></span>
<span data-ttu-id="bf882-124">Aby skonfigurować integrację usługi Azure AD Novatus, należy dodać Novatus z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="bf882-124">To configure the integration of Novatus into Azure AD, you need to add Novatus from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bf882-125">**Aby dodać Novatus z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bf882-125">**To add Novatus from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bf882-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bf882-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="bf882-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="bf882-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bf882-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bf882-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="bf882-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bf882-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="bf882-133">W polu wyszukiwania wpisz **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="bf882-133">In the search box, type **Novatus**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_search.png)

5. <span data-ttu-id="bf882-135">W panelu wyników wybierz **Novatus**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="bf882-135">In the results panel, select **Novatus**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bf882-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bf882-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bf882-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Novatus w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="bf882-138">In this section, you configure and test Azure AD single sign-on with Novatus based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bf882-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Novatus jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf882-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Novatus is to a user in Azure AD.</span></span> <span data-ttu-id="bf882-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Novatus musi się.</span><span class="sxs-lookup"><span data-stu-id="bf882-140">In other words, a link relationship between an Azure AD user and the related user in Novatus needs to be established.</span></span>

<span data-ttu-id="bf882-141">W Novatus, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="bf882-141">In Novatus, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bf882-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Novatus, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="bf882-142">To configure and test Azure AD single sign-on with Novatus, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bf882-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="bf882-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bf882-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bf882-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bf882-145">**[Tworzenie użytkownika testowego Novatus](#creating-a-novatus-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Novatus połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bf882-145">**[Creating a Novatus test user](#creating-a-novatus-test-user)** - to have a counterpart of Britta Simon in Novatus that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bf882-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="bf882-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bf882-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="bf882-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bf882-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bf882-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bf882-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Novatus.</span><span class="sxs-lookup"><span data-stu-id="bf882-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Novatus application.</span></span>

<span data-ttu-id="bf882-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Novatus, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bf882-150">**To configure Azure AD single sign-on with Novatus, perform the following steps:**</span></span>

1. <span data-ttu-id="bf882-151">W portalu Azure na **Novatus** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="bf882-151">In the Azure portal, on the **Novatus** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="bf882-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="bf882-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_samlbase.png)

3. <span data-ttu-id="bf882-155">Na **Novatus domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bf882-155">On the **Novatus Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_url.png)

     <span data-ttu-id="bf882-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://sso.novatuscontracts.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="bf882-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.novatuscontracts.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bf882-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="bf882-158">This value is not real.</span></span> <span data-ttu-id="bf882-159">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="bf882-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="bf882-160">Skontaktuj się z [zespołem pomocy technicznej klienta Novatus](mailto:jvinci@novatusinc.com) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="bf882-160">Contact [Novatus Client support team](mailto:jvinci@novatusinc.com) to get this value.</span></span> 
 


4. <span data-ttu-id="bf882-161">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="bf882-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_certificate.png) 

5. <span data-ttu-id="bf882-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bf882-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-novatus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bf882-165">Na **konfiguracji Novatus** , kliknij przycisk **skonfigurować Novatus** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="bf882-165">On the **Novatus Configuration** section, click **Configure Novatus** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bf882-166">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="bf882-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_configure.png) 

7. <span data-ttu-id="bf882-168">Aby uzyskać logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z Twojego [Novatus obsługuje team](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="bf882-168">To get SSO configured for your application, contact your [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> <span data-ttu-id="bf882-169">Dołącz **pobrany certyfikat** pliku poczty i udziału **adresy URL metadanych** (**Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi**) z zespołem Novatus w celu konfigurowania rejestracji Jednokrotnej w bok.</span><span class="sxs-lookup"><span data-stu-id="bf882-169">Attach the **downloaded certificate** file to your mail and share the **metadata urls** (**Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL**) with Novatus team to set up SSO on their side.</span></span>

> [!TIP]
> <span data-ttu-id="bf882-170">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="bf882-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bf882-171">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="bf882-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bf882-172">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bf882-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bf882-173">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf882-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="bf882-174">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bf882-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="bf882-176">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bf882-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bf882-177">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bf882-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bf882-179">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="bf882-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bf882-181">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bf882-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bf882-183">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="bf882-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-novatus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bf882-185">a.</span><span class="sxs-lookup"><span data-stu-id="bf882-185">a.</span></span> <span data-ttu-id="bf882-186">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bf882-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bf882-187">b.</span><span class="sxs-lookup"><span data-stu-id="bf882-187">b.</span></span> <span data-ttu-id="bf882-188">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bf882-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bf882-189">c.</span><span class="sxs-lookup"><span data-stu-id="bf882-189">c.</span></span> <span data-ttu-id="bf882-190">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="bf882-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bf882-191">d.</span><span class="sxs-lookup"><span data-stu-id="bf882-191">d.</span></span> <span data-ttu-id="bf882-192">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="bf882-192">Click **Create**.</span></span>
 
### <a name="creating-a-novatus-test-user"></a><span data-ttu-id="bf882-193">Tworzenie użytkownika testowego Novatus</span><span class="sxs-lookup"><span data-stu-id="bf882-193">Creating a Novatus test user</span></span>

<span data-ttu-id="bf882-194">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Novatus.</span><span class="sxs-lookup"><span data-stu-id="bf882-194">The objective of this section is to create a user called Britta Simon in Novatus.</span></span> <span data-ttu-id="bf882-195">Novatus obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="bf882-195">Novatus supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="bf882-196">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="bf882-196">There is no action item for you in this section.</span></span> <span data-ttu-id="bf882-197">Nowy użytkownik zostanie utworzony podczas próby dostępu Novatus, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="bf882-197">A new user will be created during an attempt to access Novatus if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="bf882-198">Jeśli trzeba ręcznie utworzyć użytkownika, należy skontaktować się [Novatus obsługuje zespołu](mailto:jvinci@novatusinc.com).</span><span class="sxs-lookup"><span data-stu-id="bf882-198">If you need to create an user manually, you need to contact the [Novatus support team](mailto:jvinci@novatusinc.com).</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bf882-199">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf882-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bf882-200">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Novatus.</span><span class="sxs-lookup"><span data-stu-id="bf882-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Novatus.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="bf882-202">**Aby przypisać Simona Britta Novatus, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="bf882-202">**To assign Britta Simon to Novatus, perform the following steps:**</span></span>

1. <span data-ttu-id="bf882-203">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bf882-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="bf882-205">Na liście aplikacji zaznacz **Novatus**.</span><span class="sxs-lookup"><span data-stu-id="bf882-205">In the applications list, select **Novatus**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-novatus-tutorial/tutorial_novatus_app.png) 

3. <span data-ttu-id="bf882-207">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="bf882-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="bf882-209">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bf882-209">Click **Add** button.</span></span> <span data-ttu-id="bf882-210">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bf882-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="bf882-212">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="bf882-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bf882-213">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bf882-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bf882-214">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bf882-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bf882-215">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bf882-215">Testing single sign-on</span></span>

<span data-ttu-id="bf882-216">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="bf882-216">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bf882-217">Po kliknięciu kafelka Novatus w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Novatus.</span><span class="sxs-lookup"><span data-stu-id="bf882-217">When you click the Novatus tile in the Access Panel, you should get automatically signed-on to your Novatus application.</span></span> <span data-ttu-id="bf882-218">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bf882-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bf882-219">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="bf882-219">Additional resources</span></span>

* [<span data-ttu-id="bf882-220">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bf882-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bf882-221">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bf882-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-novatus-tutorial/tutorial_general_203.png

