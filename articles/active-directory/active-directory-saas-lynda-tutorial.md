---
title: 'Samouczek: Integracji Azure Active Directory z witryny Lynda.com | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i witryny Lynda.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6c92789-8b64-4049-bac9-8cb928398433
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 84ed2adcc2d49ddbb6bd2e9cc3b93b967ebed063
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lyndacom"></a><span data-ttu-id="d2523-103">Samouczek: Integracji Azure Active Directory z witryny Lynda.com</span><span class="sxs-lookup"><span data-stu-id="d2523-103">Tutorial: Azure Active Directory integration with Lynda.com</span></span>

<span data-ttu-id="d2523-104">Z tego samouczka dowiesz się integrowanie witryny Lynda.com z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d2523-104">In this tutorial, you learn how to integrate Lynda.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d2523-105">Integracja z usługą Azure AD witryny Lynda.com zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d2523-105">Integrating Lynda.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d2523-106">Można kontrolować w usłudze Azure AD, który ma dostęp do witryny Lynda.com</span><span class="sxs-lookup"><span data-stu-id="d2523-106">You can control in Azure AD who has access to Lynda.com</span></span>
- <span data-ttu-id="d2523-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do witryny Lynda.com (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2523-107">You can enable your users to automatically get signed-on to Lynda.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d2523-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d2523-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d2523-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d2523-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2523-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d2523-110">Prerequisites</span></span>

<span data-ttu-id="d2523-111">Aby skonfigurować integrację usługi Azure AD z witryny Lynda.com, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d2523-111">To configure Azure AD integration with Lynda.com, you need the following items:</span></span>

- <span data-ttu-id="d2523-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2523-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d2523-113">Witryny Lynda.com jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d2523-113">A Lynda.com single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d2523-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d2523-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d2523-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d2523-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d2523-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d2523-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d2523-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d2523-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d2523-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d2523-118">Scenario description</span></span>
<span data-ttu-id="d2523-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d2523-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d2523-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d2523-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d2523-121">Dodawanie witryny Lynda.com z galerii</span><span class="sxs-lookup"><span data-stu-id="d2523-121">Adding Lynda.com from the gallery</span></span>
2. <span data-ttu-id="d2523-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d2523-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lyndacom-from-the-gallery"></a><span data-ttu-id="d2523-123">Dodawanie witryny Lynda.com z galerii</span><span class="sxs-lookup"><span data-stu-id="d2523-123">Adding Lynda.com from the gallery</span></span>
<span data-ttu-id="d2523-124">Aby skonfigurować integrację witryny Lynda.com do usługi Azure AD, należy dodać witryny Lynda.com z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d2523-124">To configure the integration of Lynda.com into Azure AD, you need to add Lynda.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d2523-125">**Aby dodać witryny Lynda.com z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d2523-125">**To add Lynda.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d2523-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d2523-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="d2523-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="d2523-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d2523-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d2523-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="d2523-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d2523-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="d2523-133">W polu wyszukiwania wpisz **witryny Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="d2523-133">In the search box, type **Lynda.com**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_search.png)

5. <span data-ttu-id="d2523-135">W panelu wyników wybierz **witryny Lynda.com**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="d2523-135">In the results panel, select **Lynda.com**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d2523-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d2523-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d2523-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z witryny Lynda.com oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="d2523-138">In this section, you configure and test Azure AD single sign-on with Lynda.com based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d2523-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w witryny Lynda.com jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2523-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lynda.com is to a user in Azure AD.</span></span> <span data-ttu-id="d2523-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w witryny Lynda.com musi się.</span><span class="sxs-lookup"><span data-stu-id="d2523-140">In other words, a link relationship between an Azure AD user and the related user in Lynda.com needs to be established.</span></span>

<span data-ttu-id="d2523-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w witryny Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="d2523-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Lynda.com.</span></span>

<span data-ttu-id="d2523-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z witryny Lynda.com, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="d2523-142">To configure and test Azure AD single sign-on with Lynda.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d2523-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d2523-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d2523-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d2523-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d2523-145">**[Tworzenie użytkownika testowego witryny Lynda.com](#creating-a-lyndacom-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta witryny Lynda.com połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d2523-145">**[Creating a Lynda.com test user](#creating-a-lyndacom-test-user)** - to have a counterpart of Britta Simon in Lynda.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d2523-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d2523-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d2523-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="d2523-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d2523-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d2523-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d2523-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne do aplikacji witryny Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="d2523-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lynda.com application.</span></span>

<span data-ttu-id="d2523-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z witryny Lynda.com, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d2523-150">**To configure Azure AD single sign-on with Lynda.com, perform the following steps:**</span></span>

1. <span data-ttu-id="d2523-151">W portalu Azure na **witryny Lynda.com** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="d2523-151">In the Azure portal, on the **Lynda.com** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="d2523-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="d2523-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_samlbase.png)

3. <span data-ttu-id="d2523-155">Na **witryny Lynda.com domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d2523-155">On the **Lynda.com Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_url.png)

    <span data-ttu-id="d2523-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span><span class="sxs-lookup"><span data-stu-id="d2523-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d2523-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="d2523-158">This value is not real.</span></span> <span data-ttu-id="d2523-159">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="d2523-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="d2523-160">Skontaktuj się z [zespołem pomocy technicznej witryny Lynda.com klienta](https://www.linkedin.com/help/lynda/ask) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="d2523-160">Contact [Lynda.com Client support team](https://www.linkedin.com/help/lynda/ask) to get these values.</span></span> 
 
4. <span data-ttu-id="d2523-161">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d2523-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_certificate.png) 

5. <span data-ttu-id="d2523-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d2523-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lynda-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d2523-165">Aby skonfigurować logowanie jednokrotne w **witryny Lynda.com** stronie, musisz wysłać pobrany **XML metadanych** [pomocy technicznej witryny Lynda.com](https://www.linkedin.com/help/lynda/ask).</span><span class="sxs-lookup"><span data-stu-id="d2523-165">To configure single sign-on on **Lynda.com** side, you need to send the downloaded **Metadata XML** [Lynda.com support](https://www.linkedin.com/help/lynda/ask).</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d2523-166">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2523-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="d2523-167">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d2523-167">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="d2523-169">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d2523-169">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d2523-170">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d2523-170">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d2523-172">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d2523-172">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d2523-174">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d2523-174">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d2523-176">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d2523-176">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d2523-178">a.</span><span class="sxs-lookup"><span data-stu-id="d2523-178">a.</span></span> <span data-ttu-id="d2523-179">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d2523-179">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d2523-180">b.</span><span class="sxs-lookup"><span data-stu-id="d2523-180">b.</span></span> <span data-ttu-id="d2523-181">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d2523-181">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d2523-182">c.</span><span class="sxs-lookup"><span data-stu-id="d2523-182">c.</span></span> <span data-ttu-id="d2523-183">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="d2523-183">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d2523-184">d.</span><span class="sxs-lookup"><span data-stu-id="d2523-184">d.</span></span> <span data-ttu-id="d2523-185">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d2523-185">Click **Create**.</span></span>
 
### <a name="creating-a-lyndacom-test-user"></a><span data-ttu-id="d2523-186">Tworzenie użytkownika testowego witryny Lynda.com</span><span class="sxs-lookup"><span data-stu-id="d2523-186">Creating a Lynda.com test user</span></span>

<span data-ttu-id="d2523-187">Nie ma elementu akcji do skonfigurowania inicjowania obsługi administracyjnej witryny Lynda.com użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d2523-187">There is no action item for you to configure user provisioning to Lynda.com.</span></span>  
<span data-ttu-id="d2523-188">Gdy przypisany użytkownik próbuje zalogować się do witryny Lynda.com za pomocą panelu dostępu, witryny Lynda.com sprawdza, czy użytkownik istnieje.</span><span class="sxs-lookup"><span data-stu-id="d2523-188">When an assigned user tries to log in to Lynda.com using the access panel, Lynda.com checks whether the user exists.</span></span>  

<span data-ttu-id="d2523-189">Jeśli nie jest Brak konta użytkownika dostępny jeszcze, są tworzone przez witryny Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="d2523-189">If there is no user account available yet, it is automatically created by Lynda.com.</span></span>

>[!NOTE]
><span data-ttu-id="d2523-190">Możesz użyć innych witryny Lynda.com użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez witryny Lynda.com do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="d2523-190">You can use any other Lynda.com user account creation tools or APIs provided by Lynda.com to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d2523-191">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2523-191">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d2523-192">W tej sekcji musisz włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udzielanie dostępu do witryny Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="d2523-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lynda.com.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="d2523-194">**Aby przypisać Simona Britta witryny Lynda.com, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d2523-194">**To assign Britta Simon to Lynda.com, perform the following steps:**</span></span>

1. <span data-ttu-id="d2523-195">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d2523-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d2523-197">Na liście aplikacji zaznacz **witryny Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="d2523-197">In the applications list, select **Lynda.com**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_app.png) 

3. <span data-ttu-id="d2523-199">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d2523-199">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="d2523-201">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d2523-201">Click **Add** button.</span></span> <span data-ttu-id="d2523-202">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d2523-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="d2523-204">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="d2523-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d2523-205">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d2523-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d2523-206">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d2523-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d2523-207">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d2523-207">Testing single sign-on</span></span>

<span data-ttu-id="d2523-208">Jeśli chcesz przetestować jednego ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="d2523-208">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="d2523-209">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d2523-209">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d2523-210">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d2523-210">Additional resources</span></span>

* [<span data-ttu-id="d2523-211">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d2523-211">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d2523-212">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d2523-212">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_203.png

