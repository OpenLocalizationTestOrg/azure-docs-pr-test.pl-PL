---
title: 'Samouczek: Integracji Azure Active Directory z Fuze | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Fuze."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9780b4bf-1fd1-48c1-9ceb-f750225ae08a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: c7f7b095aac6202a7ec5248ee2bbb109615287a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuze"></a><span data-ttu-id="aeb29-103">Samouczek: Integracji Azure Active Directory z Fuze</span><span class="sxs-lookup"><span data-stu-id="aeb29-103">Tutorial: Azure Active Directory integration with Fuze</span></span>

<span data-ttu-id="aeb29-104">Z tego samouczka dowiesz się integrowanie Fuze z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="aeb29-104">In this tutorial, you learn how to integrate Fuze with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="aeb29-105">Integracja z usługą Azure AD Fuze zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="aeb29-105">Integrating Fuze with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="aeb29-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Fuze</span><span class="sxs-lookup"><span data-stu-id="aeb29-106">You can control in Azure AD who has access to Fuze</span></span>
- <span data-ttu-id="aeb29-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Fuze (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="aeb29-107">You can enable your users to automatically get signed-on to Fuze (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="aeb29-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="aeb29-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="aeb29-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="aeb29-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aeb29-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="aeb29-110">Prerequisites</span></span>

<span data-ttu-id="aeb29-111">Aby skonfigurować integrację usługi Azure AD z Fuze, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="aeb29-111">To configure Azure AD integration with Fuze, you need the following items:</span></span>

- <span data-ttu-id="aeb29-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="aeb29-112">An Azure AD subscription</span></span>
- <span data-ttu-id="aeb29-113">Fuze jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="aeb29-113">A Fuze single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="aeb29-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="aeb29-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="aeb29-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="aeb29-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aeb29-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="aeb29-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="aeb29-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aeb29-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="aeb29-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="aeb29-118">Scenario description</span></span>
<span data-ttu-id="aeb29-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="aeb29-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="aeb29-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="aeb29-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aeb29-121">Dodawanie Fuze z galerii</span><span class="sxs-lookup"><span data-stu-id="aeb29-121">Adding Fuze from the gallery</span></span>
2. <span data-ttu-id="aeb29-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="aeb29-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-fuze-from-the-gallery"></a><span data-ttu-id="aeb29-123">Dodawanie Fuze z galerii</span><span class="sxs-lookup"><span data-stu-id="aeb29-123">Adding Fuze from the gallery</span></span>
<span data-ttu-id="aeb29-124">Aby skonfigurować integrację usługi Azure AD Fuze, należy dodać Fuze z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="aeb29-124">To configure the integration of Fuze into Azure AD, you need to add Fuze from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="aeb29-125">**Aby dodać Fuze z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="aeb29-125">**To add Fuze from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="aeb29-126">W  **[portalu zarządzania Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="aeb29-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="aeb29-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="aeb29-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="aeb29-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="aeb29-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="aeb29-131">Kliknij przycisk **Dodaj** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="aeb29-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="aeb29-133">W polu wyszukiwania wpisz **Fuze**.</span><span class="sxs-lookup"><span data-stu-id="aeb29-133">In the search box, type **Fuze**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_000.png)

5. <span data-ttu-id="aeb29-135">W panelu wyników wybierz **Fuze**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="aeb29-135">In the results panel, select **Fuze**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="aeb29-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="aeb29-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="aeb29-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Fuze w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="aeb29-138">In this section, you configure and test Azure AD single sign-on with Fuze based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="aeb29-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Fuze jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aeb29-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Fuze is to a user in Azure AD.</span></span> <span data-ttu-id="aeb29-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Fuze musi się.</span><span class="sxs-lookup"><span data-stu-id="aeb29-140">In other words, a link relationship between an Azure AD user and the related user in Fuze needs to be established.</span></span>

<span data-ttu-id="aeb29-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Fuze.</span><span class="sxs-lookup"><span data-stu-id="aeb29-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Fuze.</span></span>

<span data-ttu-id="aeb29-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Fuze, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="aeb29-142">To configure and test Azure AD single sign-on with Fuze, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="aeb29-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="aeb29-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="aeb29-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="aeb29-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aeb29-145">**[Tworzenie użytkownika testowego Fuze](#creating-a-fuze-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Fuze połączonego z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="aeb29-145">**[Creating a Fuze test user](#creating-a-fuze-test-user)** - to have a counterpart of Britta Simon in Fuze that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="aeb29-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="aeb29-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aeb29-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="aeb29-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="aeb29-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="aeb29-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="aeb29-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure i skonfigurować logowanie jednokrotne w aplikacji Fuze.</span><span class="sxs-lookup"><span data-stu-id="aeb29-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Fuze application.</span></span>

<span data-ttu-id="aeb29-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Fuze, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="aeb29-150">**To configure Azure AD single sign-on with Fuze, perform the following steps:**</span></span>

1. <span data-ttu-id="aeb29-151">W portalu zarządzania Azure na **Fuze** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="aeb29-151">In the Azure Management portal, on the **Fuze** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="aeb29-153">Na **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** Włącz funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="aeb29-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_01.png)

3. <span data-ttu-id="aeb29-155">Na **Fuze domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="aeb29-155">On the **Fuze Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_020.png)
    
    <span data-ttu-id="aeb29-157">W **Zaloguj się na adres URL** pole tekstowe, wprowadź znak na adres URL jako:`https://www.thinkingphones.com/jetspeed/portal/`</span><span class="sxs-lookup"><span data-stu-id="aeb29-157">In the **Sign on URL** textbox, type the Sign-on URL as: `https://www.thinkingphones.com/jetspeed/portal/`</span></span>

4.  <span data-ttu-id="aeb29-158">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="aeb29-158">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-fuze-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="aeb29-160">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik xml na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="aeb29-160">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the xml file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_05.png) 

6. <span data-ttu-id="aeb29-162">Skonfigurować logowanie jednokrotne w **Fuze** stronie, musisz wysłać pobrany **XML metadanych** do [zespołem pomocy technicznej Fuze](https://www.fuze.com/support).</span><span class="sxs-lookup"><span data-stu-id="aeb29-162">To configure single sign-on on **Fuze** side, you need to send the downloaded **Metadata XML** to [Fuze support team](https://www.fuze.com/support).</span></span> <span data-ttu-id="aeb29-163">One będzie skonfigurowanie tego numeru w celu połączenia logowania jednokrotnego SAML prawidłowo po obu stronach.</span><span class="sxs-lookup"><span data-stu-id="aeb29-163">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="aeb29-164">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="aeb29-164">Creating an Azure AD test user</span></span>
<span data-ttu-id="aeb29-165">Celem tej sekcji jest tworzenie użytkownika testowego w portalu zarządzania Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="aeb29-165">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="aeb29-167">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="aeb29-167">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="aeb29-168">W **portalu zarządzania Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="aeb29-168">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="aeb29-170">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="aeb29-170">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="aeb29-172">W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="aeb29-172">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="aeb29-174">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="aeb29-174">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-fuze-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="aeb29-176">a.</span><span class="sxs-lookup"><span data-stu-id="aeb29-176">a.</span></span> <span data-ttu-id="aeb29-177">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="aeb29-177">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="aeb29-178">b.</span><span class="sxs-lookup"><span data-stu-id="aeb29-178">b.</span></span> <span data-ttu-id="aeb29-179">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="aeb29-179">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="aeb29-180">c.</span><span class="sxs-lookup"><span data-stu-id="aeb29-180">c.</span></span> <span data-ttu-id="aeb29-181">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="aeb29-181">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="aeb29-182">d.</span><span class="sxs-lookup"><span data-stu-id="aeb29-182">d.</span></span> <span data-ttu-id="aeb29-183">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="aeb29-183">Click **Create**.</span></span> 


### <a name="creating-a-fuze-test-user"></a><span data-ttu-id="aeb29-184">Tworzenie użytkownika testowego Fuze</span><span class="sxs-lookup"><span data-stu-id="aeb29-184">Creating a Fuze test user</span></span>

<span data-ttu-id="aeb29-185">Aplikacja fuze obsługuje zaraz pełna rezerw użytkownika czasu, użytkownicy będą tworzone automatycznie podczas ich logowania.</span><span class="sxs-lookup"><span data-stu-id="aeb29-185">Fuze application supports full Just in time user provision, so users will get created automatically when they sign-in.</span></span> <span data-ttu-id="aeb29-186">Dla innych wyjaśnienie, skontaktuj się z Fuze [obsługuje](https://www.fuze.com/support).</span><span class="sxs-lookup"><span data-stu-id="aeb29-186">For any other clarification, please contact Fuze [support](https://www.fuze.com/support).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="aeb29-187">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="aeb29-187">Assigning the Azure AD test user</span></span>

<span data-ttu-id="aeb29-188">W tej sekcji można włączyć Simona Britta do udostępnienia jej Fuze za pomocą usługi Azure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="aeb29-188">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Fuze.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="aeb29-190">**Aby przypisać Simona Britta Fuze, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="aeb29-190">**To assign Britta Simon to Fuze, perform the following steps:**</span></span>

1. <span data-ttu-id="aeb29-191">Otwórz widok aplikacji w portalu zarządzania Azure, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="aeb29-191">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="aeb29-193">Na liście aplikacji zaznacz **Fuze**.</span><span class="sxs-lookup"><span data-stu-id="aeb29-193">In the applications list, select **Fuze**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-fuze-tutorial/tutorial_fuze_50.png) 

3. <span data-ttu-id="aeb29-195">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="aeb29-195">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="aeb29-197">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="aeb29-197">Click **Add** button.</span></span> <span data-ttu-id="aeb29-198">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="aeb29-198">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="aeb29-200">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="aeb29-200">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="aeb29-201">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="aeb29-201">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aeb29-202">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="aeb29-202">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="testing-single-sign-on"></a><span data-ttu-id="aeb29-203">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="aeb29-203">Testing single sign-on</span></span>

<span data-ttu-id="aeb29-204">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="aeb29-204">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="aeb29-205">Po kliknięciu kafelka Fuze w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Fuze.</span><span class="sxs-lookup"><span data-stu-id="aeb29-205">When you click the Fuze tile in the Access Panel, you should get automatically signed-on to your Fuze application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="aeb29-206">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="aeb29-206">Additional resources</span></span>

* [<span data-ttu-id="aeb29-207">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aeb29-207">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aeb29-208">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="aeb29-208">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuze-tutorial/tutorial_general_203.png