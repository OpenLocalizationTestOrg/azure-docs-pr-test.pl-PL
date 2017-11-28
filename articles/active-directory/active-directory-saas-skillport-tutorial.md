---
title: 'Samouczek: Integracji Azure Active Directory z Skillport | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Skillport."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4df349b2-a73f-4b88-a077-ec0fbfc26527
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 668fc5ae4f964bd776904c3a9dbc2b203689d50c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skillport"></a><span data-ttu-id="035b3-103">Samouczek: Integracji Azure Active Directory z Skillport</span><span class="sxs-lookup"><span data-stu-id="035b3-103">Tutorial: Azure Active Directory integration with Skillport</span></span>

<span data-ttu-id="035b3-104">Z tego samouczka dowiesz się integrowanie Skillport z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="035b3-104">In this tutorial, you learn how to integrate Skillport with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="035b3-105">Integracja z usługą Azure AD Skillport zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="035b3-105">Integrating Skillport with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="035b3-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Skillport</span><span class="sxs-lookup"><span data-stu-id="035b3-106">You can control in Azure AD who has access to Skillport</span></span>
- <span data-ttu-id="035b3-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Skillport (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="035b3-107">You can enable your users to automatically get signed-on to Skillport (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="035b3-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="035b3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="035b3-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="035b3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="035b3-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="035b3-110">Prerequisites</span></span>

<span data-ttu-id="035b3-111">Aby skonfigurować integrację usługi Azure AD z Skillport, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="035b3-111">To configure Azure AD integration with Skillport, you need the following items:</span></span>

- <span data-ttu-id="035b3-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="035b3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="035b3-113">Skillport jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="035b3-113">A Skillport single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="035b3-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="035b3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="035b3-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="035b3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="035b3-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="035b3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="035b3-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="035b3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="035b3-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="035b3-118">Scenario description</span></span>
<span data-ttu-id="035b3-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="035b3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="035b3-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="035b3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="035b3-121">Dodawanie Skillport z galerii</span><span class="sxs-lookup"><span data-stu-id="035b3-121">Adding Skillport from the gallery</span></span>
2. <span data-ttu-id="035b3-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="035b3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skillport-from-the-gallery"></a><span data-ttu-id="035b3-123">Dodawanie Skillport z galerii</span><span class="sxs-lookup"><span data-stu-id="035b3-123">Adding Skillport from the gallery</span></span>
<span data-ttu-id="035b3-124">Aby skonfigurować integrację usługi Azure AD Skillport, należy dodać Skillport z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="035b3-124">To configure the integration of Skillport into Azure AD, you need to add Skillport from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="035b3-125">**Aby dodać Skillport z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="035b3-125">**To add Skillport from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="035b3-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="035b3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="035b3-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="035b3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="035b3-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="035b3-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="035b3-131">Kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="035b3-131">Click **New Application** button on the top of the dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="035b3-133">W polu wyszukiwania wpisz **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="035b3-133">In the search box, type **Skillport**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_search.png)

5. <span data-ttu-id="035b3-135">W panelu wyników wybierz **Skillport**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="035b3-135">In the results panel, select **Skillport**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="035b3-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="035b3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="035b3-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Skillport w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="035b3-138">In this section, you configure and test Azure AD single sign-on with Skillport based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="035b3-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Skillport jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="035b3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Skillport is to a user in Azure AD.</span></span> <span data-ttu-id="035b3-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Skillport musi się.</span><span class="sxs-lookup"><span data-stu-id="035b3-140">In other words, a link relationship between an Azure AD user and the related user in Skillport needs to be established.</span></span>

<span data-ttu-id="035b3-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Skillport.</span><span class="sxs-lookup"><span data-stu-id="035b3-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Skillport.</span></span>

<span data-ttu-id="035b3-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Skillport, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="035b3-142">To configure and test Azure AD single sign-on with Skillport, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="035b3-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="035b3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="035b3-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="035b3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="035b3-145">**[Tworzenie użytkownika testowego Skillport](#creating-a-skillport-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Skillport połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="035b3-145">**[Creating a Skillport test user](#creating-a-skillport-test-user)** - to have a counterpart of Britta Simon in Skillport that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="035b3-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="035b3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="035b3-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="035b3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="035b3-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="035b3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="035b3-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Skillport.</span><span class="sxs-lookup"><span data-stu-id="035b3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Skillport application.</span></span>

<span data-ttu-id="035b3-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Skillport, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="035b3-150">**To configure Azure AD single sign-on with Skillport, perform the following steps:**</span></span>

1. <span data-ttu-id="035b3-151">W portalu Azure na **Skillport** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="035b3-151">In the Azure  portal, on the **Skillport** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="035b3-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="035b3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_samlbase.png)

3. <span data-ttu-id="035b3-155">Na **Skillport domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="035b3-155">On the **Skillport Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_url.png)

    <span data-ttu-id="035b3-157">a.</span><span class="sxs-lookup"><span data-stu-id="035b3-157">a.</span></span> <span data-ttu-id="035b3-158">W **adres URL logowania** tekstowym, wpisz adres URL za pomocą następujących wzorców:</span><span class="sxs-lookup"><span data-stu-id="035b3-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span>
      
      <span data-ttu-id="035b3-159">Europa centrum danych:`https://<subdomain>.skillport.eu`</span><span class="sxs-lookup"><span data-stu-id="035b3-159">EU Datacenter: `https://<subdomain>.skillport.eu`</span></span>
   
      <span data-ttu-id="035b3-160">Centrum danych Stanów Zjednoczonych:`https://<subdomain>.skillport.com`</span><span class="sxs-lookup"><span data-stu-id="035b3-160">US Datacenter: `https://<subdomain>.skillport.com`</span></span>
   
    <span data-ttu-id="035b3-161">b.</span><span class="sxs-lookup"><span data-stu-id="035b3-161">b.</span></span> <span data-ttu-id="035b3-162">W **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą następujących wzorców:</span><span class="sxs-lookup"><span data-stu-id="035b3-162">In the **Reply URL** textbox, type a URL using the following patterns:</span></span>
    
      <span data-ttu-id="035b3-163">Europa centrum danych:`https://<subdomain>.skillport.eu/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="035b3-163">EU Datacenter: `https://<subdomain>.skillport.eu/adfs/ls/`</span></span>
    
      <span data-ttu-id="035b3-164">Centrum danych Stanów Zjednoczonych:`https://<subdomain>.skillport.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="035b3-164">US Datacenter: `https://<subdomain>.skillport.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="035b3-165">Wartości te nie są rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="035b3-165">These values are not the real.</span></span> <span data-ttu-id="035b3-166">Rzeczywisty adres URL odpowiedzi i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="035b3-166">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="035b3-167">Skontaktuj się z [zespołem pomocy technicznej klienta Skillport](https://www.skillsoft.com/contact.asp) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="035b3-167">Contact [Skillport Client support team](https://www.skillsoft.com/contact.asp) to get these values.</span></span>
 
4. <span data-ttu-id="035b3-168">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="035b3-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_certificate.png) 

5. <span data-ttu-id="035b3-170">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="035b3-170">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skillport-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="035b3-172">Skonfigurować logowanie jednokrotne w **Skillport** stronie, musisz wysłać pobrany **XML metadanych** do [zespołem pomocy technicznej Skillport](https://www.skillsoft.com/contact.asp).</span><span class="sxs-lookup"><span data-stu-id="035b3-172">To configure single sign-on on **Skillport** side, you need to send the downloaded **Metadata XML** to [Skillport support team](https://www.skillsoft.com/contact.asp).</span></span> <span data-ttu-id="035b3-173">One skonfiguruje ją połączenia logowania jednokrotnego SAML prawidłowo po obu stronach.</span><span class="sxs-lookup"><span data-stu-id="035b3-173">They will set it up to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="035b3-174">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="035b3-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="035b3-175">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="035b3-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="035b3-177">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="035b3-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="035b3-178">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="035b3-178">In the **Azure  portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="035b3-180">Przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** do wyświetlenia na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="035b3-180">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="035b3-182">W górnej części okna dialogowego, kliknij przycisk **Dodaj** otworzyć **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="035b3-182">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="035b3-184">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="035b3-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="035b3-186">a.</span><span class="sxs-lookup"><span data-stu-id="035b3-186">a.</span></span> <span data-ttu-id="035b3-187">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="035b3-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="035b3-188">b.</span><span class="sxs-lookup"><span data-stu-id="035b3-188">b.</span></span> <span data-ttu-id="035b3-189">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="035b3-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="035b3-190">c.</span><span class="sxs-lookup"><span data-stu-id="035b3-190">c.</span></span> <span data-ttu-id="035b3-191">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="035b3-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="035b3-192">d.</span><span class="sxs-lookup"><span data-stu-id="035b3-192">d.</span></span> <span data-ttu-id="035b3-193">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="035b3-193">Click **Create**.</span></span>
 
### <a name="creating-a-skillport-test-user"></a><span data-ttu-id="035b3-194">Tworzenie użytkownika testowego Skillport</span><span class="sxs-lookup"><span data-stu-id="035b3-194">Creating a Skillport test user</span></span>

<span data-ttu-id="035b3-195">Aby utworzyć użytkownika testowego Skillport, należy skontaktować się [zespołem pomocy technicznej Skillport](https://www.skillsoft.com/contact.asp) ma wiele scenariuszy biznesowych zgodnie z wymaganiami użytkownika końcowego.</span><span class="sxs-lookup"><span data-stu-id="035b3-195">In order to create Skillport test user, you need to contact [Skillport support team](https://www.skillsoft.com/contact.asp) as they have multiple business scenarios according to the requirement of end user.</span></span> <span data-ttu-id="035b3-196">Firma chce skonfigurować go po dyskusji z użytkownikami.</span><span class="sxs-lookup"><span data-stu-id="035b3-196">They will configure it after discussion with the users.</span></span>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="035b3-197">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="035b3-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="035b3-198">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Skillport.</span><span class="sxs-lookup"><span data-stu-id="035b3-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Skillport.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="035b3-200">**Aby przypisać Simona Britta Skillport, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="035b3-200">**To assign Britta Simon to Skillport, perform the following steps:**</span></span>

1. <span data-ttu-id="035b3-201">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="035b3-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="035b3-203">Na liście aplikacji zaznacz **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="035b3-203">In the applications list, select **Skillport**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_app.png) 

3. <span data-ttu-id="035b3-205">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="035b3-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="035b3-207">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="035b3-207">Click **Add** button.</span></span> <span data-ttu-id="035b3-208">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="035b3-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="035b3-210">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="035b3-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="035b3-211">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="035b3-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="035b3-212">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="035b3-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="035b3-213">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="035b3-213">Testing single sign-on</span></span>

<span data-ttu-id="035b3-214">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="035b3-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="035b3-215">Po kliknięciu kafelka Skillport w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Skillport.</span><span class="sxs-lookup"><span data-stu-id="035b3-215">When you click the Skillport tile in the Access Panel, you should get automatically signed-on to your Skillport application.</span></span>
<span data-ttu-id="035b3-216">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="035b3-216">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="035b3-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="035b3-217">Additional resources</span></span>

* [<span data-ttu-id="035b3-218">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="035b3-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="035b3-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="035b3-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_203.png

