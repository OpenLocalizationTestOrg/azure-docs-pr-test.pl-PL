---
title: "Samouczek: Integracji Azure Active Directory z zbijają się | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i zbijają się."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8389ba4c-f5f8-4ede-b2f4-32eae844ceb0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 59d4019545d39ec76bf401696338140f430630c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-huddle"></a><span data-ttu-id="358e0-103">Samouczek: Integracji Azure Active Directory z zbijają się</span><span class="sxs-lookup"><span data-stu-id="358e0-103">Tutorial: Azure Active Directory integration with Huddle</span></span>

<span data-ttu-id="358e0-104">Z tego samouczka dowiesz się integrowanie zbijają się w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="358e0-104">In this tutorial, you learn how to integrate Huddle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="358e0-105">Integrowanie zbijają się z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="358e0-105">Integrating Huddle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="358e0-106">Można kontrolować w usłudze Azure AD, który ma dostęp do zbijają się</span><span class="sxs-lookup"><span data-stu-id="358e0-106">You can control in Azure AD who has access to Huddle</span></span>
- <span data-ttu-id="358e0-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do zbijają się (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="358e0-107">You can enable your users to automatically get signed-on to Huddle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="358e0-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="358e0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="358e0-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="358e0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="358e0-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="358e0-110">Prerequisites</span></span>

<span data-ttu-id="358e0-111">Aby skonfigurować integrację usługi Azure AD z zbijają się, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="358e0-111">To configure Azure AD integration with Huddle, you need the following items:</span></span>

- <span data-ttu-id="358e0-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="358e0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="358e0-113">Zbijają się logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="358e0-113">A Huddle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="358e0-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="358e0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="358e0-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="358e0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="358e0-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="358e0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="358e0-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="358e0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="358e0-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="358e0-118">Scenario description</span></span>

<span data-ttu-id="358e0-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="358e0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="358e0-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="358e0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="358e0-121">Dodawanie zbijają się z galerii</span><span class="sxs-lookup"><span data-stu-id="358e0-121">Adding Huddle from the gallery</span></span>
2. <span data-ttu-id="358e0-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="358e0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-huddle-from-the-gallery"></a><span data-ttu-id="358e0-123">Dodawanie zbijają się z galerii</span><span class="sxs-lookup"><span data-stu-id="358e0-123">Adding Huddle from the gallery</span></span>
<span data-ttu-id="358e0-124">Aby skonfigurować integrację zbijają się do usługi Azure AD, należy dodać zbijają się z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="358e0-124">To configure the integration of Huddle into Azure AD, you need to add Huddle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="358e0-125">**Aby dodać zbijają się z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="358e0-125">**To add Huddle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="358e0-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="358e0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="358e0-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="358e0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="358e0-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="358e0-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="358e0-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="358e0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="358e0-133">W polu wyszukiwania wpisz **zbijają się**.</span><span class="sxs-lookup"><span data-stu-id="358e0-133">In the search box, type **Huddle**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_search.png)

5. <span data-ttu-id="358e0-135">W panelu wyników wybierz **zbijają się**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="358e0-135">In the results panel, select **Huddle**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="358e0-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="358e0-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="358e0-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z zbijają się na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="358e0-138">In this section, you configure and test Azure AD single sign-on with Huddle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="358e0-139">Do rejestracji jednokrotnej do pracy usługi Azure AD musi ustalić użytkownika odpowiednika w zbijają się do użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="358e0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Huddle is to a user in Azure AD.</span></span> <span data-ttu-id="358e0-140">Innymi słowy łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w zbijają się potrzeba ustanowienia.</span><span class="sxs-lookup"><span data-stu-id="358e0-140">In other words, a link relationship between an Azure AD user and the related user in Huddle needs to be established.</span></span>

<span data-ttu-id="358e0-141">W zbijają się, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="358e0-141">In Huddle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="358e0-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z zbijają się, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="358e0-142">To configure and test Azure AD single sign-on with Huddle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="358e0-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="358e0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>

2. <span data-ttu-id="358e0-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="358e0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>

3. <span data-ttu-id="358e0-145">**[Tworzenie użytkownika testowego zbijają się](#creating-a-huddle-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta zbijają się połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="358e0-145">**[Creating a Huddle test user](#creating-a-huddle-test-user)** - to have a counterpart of Britta Simon in Huddle that is linked to the Azure AD representation of user.</span></span>

4. <span data-ttu-id="358e0-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="358e0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>

5. <span data-ttu-id="358e0-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="358e0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="358e0-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="358e0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="358e0-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji zbijają się.</span><span class="sxs-lookup"><span data-stu-id="358e0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Huddle application.</span></span>

<span data-ttu-id="358e0-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z zbijają się, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="358e0-150">**To configure Azure AD single sign-on with Huddle, perform the following steps:**</span></span>

1. <span data-ttu-id="358e0-151">W portalu Azure na **zbijają się** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="358e0-151">In the Azure portal, on the **Huddle** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="358e0-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="358e0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_samlbase.png)

3. <span data-ttu-id="358e0-155">Na **zbijają się w domenie i adresy URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="358e0-155">On the **Huddle Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_url.png)

    <span data-ttu-id="358e0-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`http://<company name>.huddle.com`</span><span class="sxs-lookup"><span data-stu-id="358e0-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<company name>.huddle.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="358e0-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="358e0-158">This value is not real.</span></span> <span data-ttu-id="358e0-159">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="358e0-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="358e0-160">Skontaktuj się z [klienta zbijają się z pomocą techniczną](https://huddle.zendesk.com) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="358e0-160">Contact [Huddle Client support team](https://huddle.zendesk.com) to get this value.</span></span> 

4. <span data-ttu-id="358e0-161">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="358e0-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_certificate.png) 

5. <span data-ttu-id="358e0-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="358e0-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-huddle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="358e0-165">Na **zbijają się konfiguracji** , kliknij przycisk **skonfigurować zbijają się** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="358e0-165">On the **Huddle Configuration** section, click **Configure Huddle** to open **Configure sign-on** window.</span></span> <span data-ttu-id="358e0-166">Kopiuj **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="358e0-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_configure.png) 
    
7. <span data-ttu-id="358e0-168">Aby skonfigurować rejestrację jednokrotną zbijają się strony, musisz wysłać pobrany **certyfikatu**, **SAML pojedynczy znak na adres URL usługi**, i **identyfikator jednostki SAML** do [klienta zbijają się z pomocą techniczną](https://huddle.zendesk.com).</span><span class="sxs-lookup"><span data-stu-id="358e0-168">To configure single sign-on on Huddle side, you need to send the downloaded  **Certificate**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** to [Huddle Client support team](https://huddle.zendesk.com).</span></span> <span data-ttu-id="358e0-169">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="358e0-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>  
   
    >[!NOTE]
    > <span data-ttu-id="358e0-170">Logowania jednokrotnego musi być włączona przez zbijają się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="358e0-170">Single sign-on needs to be enabled by the Huddle support team.</span></span> <span data-ttu-id="358e0-171">Otrzymasz powiadomienie po zakończeniu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="358e0-171">You get a notification when the configuration has been completed.</span></span> 
    > 

> [!TIP]
> <span data-ttu-id="358e0-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="358e0-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="358e0-173">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="358e0-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="358e0-174">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="358e0-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
   
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="358e0-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="358e0-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="358e0-176">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="358e0-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="358e0-178">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="358e0-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="358e0-179">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="358e0-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="358e0-181">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="358e0-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="358e0-183">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="358e0-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="358e0-185">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="358e0-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="358e0-187">a.</span><span class="sxs-lookup"><span data-stu-id="358e0-187">a.</span></span> <span data-ttu-id="358e0-188">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="358e0-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="358e0-189">b.</span><span class="sxs-lookup"><span data-stu-id="358e0-189">b.</span></span> <span data-ttu-id="358e0-190">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="358e0-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="358e0-191">c.</span><span class="sxs-lookup"><span data-stu-id="358e0-191">c.</span></span> <span data-ttu-id="358e0-192">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="358e0-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="358e0-193">d.</span><span class="sxs-lookup"><span data-stu-id="358e0-193">d.</span></span> <span data-ttu-id="358e0-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="358e0-194">Click **Create**.</span></span>
 
### <a name="creating-a-huddle-test-user"></a><span data-ttu-id="358e0-195">Tworzenie użytkownika testowego zbijają się</span><span class="sxs-lookup"><span data-stu-id="358e0-195">Creating a Huddle test user</span></span>

<span data-ttu-id="358e0-196">Aby umożliwić użytkownikom usługi Azure AD zalogować się do zbijają się, muszą mieć przydzielone do zbijają się.</span><span class="sxs-lookup"><span data-stu-id="358e0-196">To enable Azure AD users to log in to Huddle, they must be provisioned into Huddle.</span></span> <span data-ttu-id="358e0-197">W przypadku zbijają się inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="358e0-197">In the case of Huddle, provisioning is a manual task.</span></span>

<span data-ttu-id="358e0-198">**Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="358e0-198">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="358e0-199">Zaloguj się do Twojego **zbijają się** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="358e0-199">Log in to your **Huddle** company site as administrator.</span></span>
2. <span data-ttu-id="358e0-200">Kliknij przycisk **obszaru roboczego**.</span><span class="sxs-lookup"><span data-stu-id="358e0-200">Click **Workspace**.</span></span>
3. <span data-ttu-id="358e0-201">Kliknij przycisk **osób \> Zaproś inne osoby**.</span><span class="sxs-lookup"><span data-stu-id="358e0-201">Click **People \> Invite People**.</span></span>
   
   <span data-ttu-id="358e0-202">![Osoby](./media/active-directory-saas-huddle-tutorial/IC787838.png "osób")</span><span class="sxs-lookup"><span data-stu-id="358e0-202">![People](./media/active-directory-saas-huddle-tutorial/IC787838.png "People")</span></span>

4. <span data-ttu-id="358e0-203">W **utworzyć nowe zaproszenie** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="358e0-203">In the **Create a new invitation** section, perform the following steps:</span></span>
   
   <span data-ttu-id="358e0-204">![Nowe zaproszenie](./media/active-directory-saas-huddle-tutorial/IC787839.png "nowe zaproszenie")</span><span class="sxs-lookup"><span data-stu-id="358e0-204">![New Invitation](./media/active-directory-saas-huddle-tutorial/IC787839.png "New Invitation")</span></span>
   
   <span data-ttu-id="358e0-205">a.</span><span class="sxs-lookup"><span data-stu-id="358e0-205">a.</span></span> <span data-ttu-id="358e0-206">W **wybierz zespołowi zapraszanie osób do** listy, wybierz **zespołu**.</span><span class="sxs-lookup"><span data-stu-id="358e0-206">In the **Choose a team to invite people to join** list, select **team**.</span></span>

   <span data-ttu-id="358e0-207">b.</span><span class="sxs-lookup"><span data-stu-id="358e0-207">b.</span></span> <span data-ttu-id="358e0-208">Typ **adres E-mail** prawidłowy Azure AD konta chcesz udostępnić w celu **wprowadź adres e-mail osoby, które chcesz zaprosić** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="358e0-208">Type the **Email Address** of a valid Azure AD account you want to provision in to **Enter email address for people you'd like to invite** textbox.</span></span>

   <span data-ttu-id="358e0-209">c.</span><span class="sxs-lookup"><span data-stu-id="358e0-209">c.</span></span> <span data-ttu-id="358e0-210">Kliknij przycisk **zaprosić**.</span><span class="sxs-lookup"><span data-stu-id="358e0-210">Click **Invite**.</span></span>   
   
    >[!NOTE]
    > <span data-ttu-id="358e0-211">Właściciel konta usługi Azure AD zostanie wysłana wiadomość e-mail, łącznie z łączem do potwierdzenia konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="358e0-211">The Azure AD account holder will receive an email including a link to confirm the account before it becomes active.</span></span> 
    > 

>[!NOTE]
><span data-ttu-id="358e0-212">Inne zbijają się narzędzia tworzenia konta użytkownika lub interfejsów API dostarczonych przez zbijają się służy do obsługi administracyjnej kont użytkowników usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="358e0-212">You can use any other Huddle user account creation tools or APIs provided by Huddle to provision Azure AD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="358e0-213">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="358e0-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="358e0-214">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do zbijają się.</span><span class="sxs-lookup"><span data-stu-id="358e0-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Huddle.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="358e0-216">**Aby przypisać Simona Britta zbijają się, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="358e0-216">**To assign Britta Simon to Huddle, perform the following steps:**</span></span>

1. <span data-ttu-id="358e0-217">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="358e0-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="358e0-219">Na liście aplikacji zaznacz **zbijają się**.</span><span class="sxs-lookup"><span data-stu-id="358e0-219">In the applications list, select **Huddle**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_app.png) 

3. <span data-ttu-id="358e0-221">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="358e0-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="358e0-223">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="358e0-223">Click **Add** button.</span></span> <span data-ttu-id="358e0-224">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="358e0-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="358e0-226">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="358e0-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="358e0-227">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="358e0-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="358e0-228">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="358e0-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="358e0-229">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="358e0-229">Testing single sign-on</span></span>

<span data-ttu-id="358e0-230">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="358e0-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="358e0-231">Po kliknięciu kafelka zbijają się w panelu dostępu, należy uzyskać automatycznie strony logowania zbijają się w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="358e0-231">When you click the Huddle tile in the Access Panel, you should get automatically login page of Huddle application.</span></span>
<span data-ttu-id="358e0-232">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="358e0-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="358e0-233">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="358e0-233">Additional resources</span></span>

* [<span data-ttu-id="358e0-234">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="358e0-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="358e0-235">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="358e0-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_203.png
