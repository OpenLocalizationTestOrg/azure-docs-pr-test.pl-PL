---
title: 'Samouczek: Integracji Azure Active Directory z Inkling | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Inkling."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 64c7ee45-ee8a-42f7-bf04-fd0e00833ea9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 7b0639c6515298731f88346c2e4ca82664653a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-inkling"></a><span data-ttu-id="323db-103">Samouczek: Integracji Azure Active Directory z Inkling</span><span class="sxs-lookup"><span data-stu-id="323db-103">Tutorial: Azure Active Directory integration with Inkling</span></span>

<span data-ttu-id="323db-104">Z tego samouczka dowiesz się integrowanie Inkling z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="323db-104">In this tutorial, you learn how to integrate Inkling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="323db-105">Integracja z usługą Azure AD Inkling zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="323db-105">Integrating Inkling with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="323db-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Inkling</span><span class="sxs-lookup"><span data-stu-id="323db-106">You can control in Azure AD who has access to Inkling</span></span>
- <span data-ttu-id="323db-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Inkling (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="323db-107">You can enable your users to automatically get signed-on to Inkling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="323db-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="323db-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="323db-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="323db-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="323db-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="323db-110">Prerequisites</span></span>

<span data-ttu-id="323db-111">Aby skonfigurować integrację usługi Azure AD z Inkling, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="323db-111">To configure Azure AD integration with Inkling, you need the following items:</span></span>

- <span data-ttu-id="323db-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="323db-112">An Azure AD subscription</span></span>
- <span data-ttu-id="323db-113">Inkling jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="323db-113">An Inkling single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="323db-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="323db-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="323db-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="323db-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="323db-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="323db-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="323db-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="323db-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="323db-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="323db-118">Scenario description</span></span>
<span data-ttu-id="323db-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="323db-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="323db-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="323db-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="323db-121">Dodawanie Inkling z galerii</span><span class="sxs-lookup"><span data-stu-id="323db-121">Adding Inkling from the gallery</span></span>
2. <span data-ttu-id="323db-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="323db-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-inkling-from-the-gallery"></a><span data-ttu-id="323db-123">Dodawanie Inkling z galerii</span><span class="sxs-lookup"><span data-stu-id="323db-123">Adding Inkling from the gallery</span></span>
<span data-ttu-id="323db-124">Aby skonfigurować integrację usługi Azure AD Inkling, należy dodać Inkling z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="323db-124">To configure the integration of Inkling into Azure AD, you need to add Inkling from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="323db-125">**Aby dodać Inkling z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="323db-125">**To add Inkling from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="323db-126">W  **[portalu zarządzania Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="323db-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="323db-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="323db-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="323db-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="323db-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="323db-131">Kliknij przycisk **Dodaj** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="323db-131">Click **Add** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="323db-133">W polu wyszukiwania wpisz **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="323db-133">In the search box, type **Inkling**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_001.png)

5. <span data-ttu-id="323db-135">W panelu wyników wybierz **Inkling**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="323db-135">In the results panel, select **Inkling**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="323db-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="323db-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="323db-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Inkling w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="323db-138">In this section, you configure and test Azure AD single sign-on with Inkling based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="323db-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Inkling jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="323db-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Inkling is to a user in Azure AD.</span></span> <span data-ttu-id="323db-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Inkling musi się.</span><span class="sxs-lookup"><span data-stu-id="323db-140">In other words, a link relationship between an Azure AD user and the related user in Inkling needs to be established.</span></span>

<span data-ttu-id="323db-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Inkling.</span><span class="sxs-lookup"><span data-stu-id="323db-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Inkling.</span></span>

<span data-ttu-id="323db-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Inkling, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="323db-142">To configure and test Azure AD single sign-on with Inkling, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="323db-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="323db-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="323db-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="323db-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="323db-145">**[Tworzenie użytkownika testowego Inkling](#creating-an-inkling-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Inkling połączonego z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="323db-145">**[Creating an Inkling test user](#creating-an-inkling-test-user)** - to have a counterpart of Britta Simon in Inkling that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="323db-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="323db-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="323db-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="323db-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="323db-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="323db-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="323db-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure i skonfigurować logowanie jednokrotne w aplikacji Inkling.</span><span class="sxs-lookup"><span data-stu-id="323db-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Inkling application.</span></span>

<span data-ttu-id="323db-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Inkling, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="323db-150">**To configure Azure AD single sign-on with Inkling, perform the following steps:**</span></span>

1. <span data-ttu-id="323db-151">W portalu zarządzania Azure na **Inkling** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="323db-151">In the Azure Management portal, on the **Inkling** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="323db-153">Na **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** Włącz funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="323db-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-inkling-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="323db-155">Na **Inkling domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="323db-155">On the **Inkling Domain and URLs** section, perform the following steps:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_01.png)

    <span data-ttu-id="323db-157">a.</span><span class="sxs-lookup"><span data-stu-id="323db-157">a.</span></span> <span data-ttu-id="323db-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://api.inkling.com/saml/v2/metadata/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="323db-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/metadata/<user-id>`</span></span>

    <span data-ttu-id="323db-159">b.</span><span class="sxs-lookup"><span data-stu-id="323db-159">b.</span></span> <span data-ttu-id="323db-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://api.inkling.com/saml/v2/acs/<user-id>`</span><span class="sxs-lookup"><span data-stu-id="323db-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.inkling.com/saml/v2/acs/<user-id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="323db-161">Należy pamiętać, że nie są one rzeczywiste wartości.</span><span class="sxs-lookup"><span data-stu-id="323db-161">Please note that these are not the real values.</span></span> <span data-ttu-id="323db-162">Należy zaktualizować te wartości z rzeczywistego identyfikatora i adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="323db-162">You have to update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="323db-163">Skontaktuj się z [zespołem pomocy technicznej Inkling](mailto:press@inkling.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="323db-163">Contact [Inkling support team](mailto:press@inkling.com) to get these values.</span></span>

4. <span data-ttu-id="323db-164">Na **certyfikat podpisywania SAML** kliknij **Utwórz nowy certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="323db-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-inkling-tutorial/tutorial_general_400.png)    

5. <span data-ttu-id="323db-166">Na **Tworzenie nowego świadectwa** okna dialogowego, kliknij ikonę kalendarza i wybierz **Data wygaśnięcia**.</span><span class="sxs-lookup"><span data-stu-id="323db-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="323db-167">Następnie kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="323db-167">Then click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-inkling-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="323db-169">Na **certyfikat podpisywania SAML** wybierz opcję **uaktywnić nowego świadectwa** i kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="323db-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_02.png)

7. <span data-ttu-id="323db-171">W oknie podręcznym **certyfikat przerzucania** okna, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="323db-171">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-inkling-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="323db-173">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="323db-173">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_03.png) 

9. <span data-ttu-id="323db-175">Aby uzyskać logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z [Inkling zespołem pomocy technicznej](mailto:press@inkling.com) i udostępniać je z pobrane **metadanych**.</span><span class="sxs-lookup"><span data-stu-id="323db-175">To get SSO configured for your application, contact [Inkling support team](mailto:press@inkling.com) and provide them with downloaded **metadata**.</span></span> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="323db-176">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="323db-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="323db-177">Celem tej sekcji jest tworzenie użytkownika testowego w portalu zarządzania Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="323db-177">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="323db-179">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="323db-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="323db-180">W **portalu zarządzania Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="323db-180">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="323db-182">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="323db-182">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="323db-184">W górnej części okna dialogowego kliknij **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="323db-184">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="323db-186">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="323db-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-inkling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="323db-188">a.</span><span class="sxs-lookup"><span data-stu-id="323db-188">a.</span></span> <span data-ttu-id="323db-189">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="323db-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="323db-190">b.</span><span class="sxs-lookup"><span data-stu-id="323db-190">b.</span></span> <span data-ttu-id="323db-191">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="323db-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="323db-192">c.</span><span class="sxs-lookup"><span data-stu-id="323db-192">c.</span></span> <span data-ttu-id="323db-193">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="323db-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="323db-194">d.</span><span class="sxs-lookup"><span data-stu-id="323db-194">d.</span></span> <span data-ttu-id="323db-195">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="323db-195">Click **Create**.</span></span> 



### <a name="creating-an-inkling-test-user"></a><span data-ttu-id="323db-196">Tworzenie użytkownika testowego Inkling</span><span class="sxs-lookup"><span data-stu-id="323db-196">Creating an Inkling test user</span></span>

<span data-ttu-id="323db-197">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Inkling.</span><span class="sxs-lookup"><span data-stu-id="323db-197">In this section, you create a user called Britta Simon in Inkling.</span></span> <span data-ttu-id="323db-198">We współpracy z [zespołem pomocy technicznej Inkling](mailto:press@inkling.com) Aby dodać użytkowników do platformy Inkling.</span><span class="sxs-lookup"><span data-stu-id="323db-198">Please work with [Inkling support team](mailto:press@inkling.com) to add the users in the Inkling platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="323db-199">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="323db-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="323db-200">W tej sekcji można włączyć Simona Britta do udostępnienia jej Inkling za pomocą usługi Azure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="323db-200">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Inkling.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="323db-202">**Aby przypisać Simona Britta Inkling, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="323db-202">**To assign Britta Simon to Inkling, perform the following steps:**</span></span>

1. <span data-ttu-id="323db-203">Otwórz widok aplikacji w portalu zarządzania Azure, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="323db-203">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="323db-205">Na liście aplikacji zaznacz **Inkling**.</span><span class="sxs-lookup"><span data-stu-id="323db-205">In the applications list, select **Inkling**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-inkling-tutorial/tutorial_inkling_50.png) 

3. <span data-ttu-id="323db-207">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="323db-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="323db-209">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="323db-209">Click **Add** button.</span></span> <span data-ttu-id="323db-210">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="323db-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="323db-212">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="323db-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="323db-213">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="323db-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="323db-214">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="323db-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="323db-215">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="323db-215">Testing single sign-on</span></span>

<span data-ttu-id="323db-216">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="323db-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="323db-217">Po kliknięciu kafelka Inkling w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Inkling.</span><span class="sxs-lookup"><span data-stu-id="323db-217">When you click the Inkling tile in the Access Panel, you should get automatically signed-on to your Inkling application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="323db-218">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="323db-218">Additional resources</span></span>

* [<span data-ttu-id="323db-219">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="323db-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="323db-220">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="323db-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-inkling-tutorial/tutorial_general_203.png