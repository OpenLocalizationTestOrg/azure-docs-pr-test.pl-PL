---
title: 'Samouczek: Integracji Azure Active Directory z Concur | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Concur."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1eee0a5d-24fa-4986-9aef-3c543cfe3296
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 0b44437b3dcf69dae3587529da7d12e7809b9f55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-concur"></a><span data-ttu-id="9a182-103">Samouczek: Integracji Azure Active Directory z Concur</span><span class="sxs-lookup"><span data-stu-id="9a182-103">Tutorial: Azure Active Directory integration with Concur</span></span>

<span data-ttu-id="9a182-104">Z tego samouczka dowiesz się integrowanie Concur z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9a182-104">In this tutorial, you learn how to integrate Concur with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9a182-105">Integracja z usługą Azure AD Concur zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="9a182-105">Integrating Concur with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9a182-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Concur</span><span class="sxs-lookup"><span data-stu-id="9a182-106">You can control in Azure AD who has access to Concur</span></span>
- <span data-ttu-id="9a182-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Concur (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a182-107">You can enable your users to automatically get signed-on to Concur (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9a182-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9a182-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9a182-109">Jeśli chcesz dowiedzieć się więcej informacji na temat integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9a182-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a182-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9a182-110">Prerequisites</span></span>

<span data-ttu-id="9a182-111">Aby skonfigurować integrację usługi Azure AD z Concur, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9a182-111">To configure Azure AD integration with Concur, you need the following items:</span></span>

- <span data-ttu-id="9a182-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a182-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9a182-113">Concur logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9a182-113">A Concur single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9a182-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="9a182-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9a182-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="9a182-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9a182-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="9a182-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9a182-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9a182-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9a182-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="9a182-118">Scenario description</span></span>
<span data-ttu-id="9a182-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="9a182-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9a182-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="9a182-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9a182-121">Dodawanie Concur z galerii</span><span class="sxs-lookup"><span data-stu-id="9a182-121">Adding Concur from the gallery</span></span>
2. <span data-ttu-id="9a182-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9a182-122">Configuring and testing Azure AD single sign-on</span></span>

>[!NOTE]
><span data-ttu-id="9a182-123">Konfiguracja subskrypcji Concur dla federacyjnego logowania jednokrotnego za pośrednictwem SAML jest osobnym zadaniem musisz skontaktować się z [zespołem pomocy technicznej klienta cząstkowe](https://www.concur.co.in/contact) do wykonania.</span><span class="sxs-lookup"><span data-stu-id="9a182-123">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) to perform.</span></span> 

## <a name="adding-concur-from-the-gallery"></a><span data-ttu-id="9a182-124">Dodawanie Concur z galerii</span><span class="sxs-lookup"><span data-stu-id="9a182-124">Adding Concur from the gallery</span></span>
<span data-ttu-id="9a182-125">Aby skonfigurować integrację usługi Azure AD Concur, należy dodać Concur z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="9a182-125">To configure the integration of Concur into Azure AD, you need to add Concur from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9a182-126">**Aby dodać Concur z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9a182-126">**To add Concur from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9a182-127">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9a182-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="9a182-129">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="9a182-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9a182-130">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9a182-130">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="9a182-132">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9a182-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="9a182-134">W polu wyszukiwania wpisz **Concur**.</span><span class="sxs-lookup"><span data-stu-id="9a182-134">In the search box, type **Concur**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-concur-tutorial/tutorial_concur_search.png)

5. <span data-ttu-id="9a182-136">W panelu wyników wybierz **Concur**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="9a182-136">In the results panel, select **Concur**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-concur-tutorial/tutorial_concur_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9a182-138">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9a182-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9a182-139">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Concur na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="9a182-139">In this section, you configure and test Azure AD single sign-on with Concur based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9a182-140">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Concur jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9a182-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Concur is to a user in Azure AD.</span></span> <span data-ttu-id="9a182-141">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Concur musi się.</span><span class="sxs-lookup"><span data-stu-id="9a182-141">In other words, a link relationship between an Azure AD user and the related user in Concur needs to be established.</span></span>

<span data-ttu-id="9a182-142">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Concur.</span><span class="sxs-lookup"><span data-stu-id="9a182-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Concur.</span></span>

<span data-ttu-id="9a182-143">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Concur, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="9a182-143">To configure and test Azure AD single sign-on with Concur, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9a182-144">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="9a182-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9a182-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9a182-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9a182-146">**[Tworzenie użytkownika testowego Concur](#creating-a-concur-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Concur połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9a182-146">**[Creating a Concur test user](#creating-a-concur-test-user)** - to have a counterpart of Britta Simon in Concur that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9a182-147">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9a182-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9a182-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="9a182-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9a182-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9a182-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9a182-150">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Concur.</span><span class="sxs-lookup"><span data-stu-id="9a182-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Concur application.</span></span>

<span data-ttu-id="9a182-151">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Concur, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9a182-151">**To configure Azure AD single sign-on with Concur, perform the following steps:**</span></span>

1. <span data-ttu-id="9a182-152">W portalu Azure na **Concur** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="9a182-152">In the Azure portal, on the **Concur** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="9a182-154">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="9a182-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-concur-tutorial/tutorial_concur_samlbase.png)

3. <span data-ttu-id="9a182-156">Na **cząstkowe domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9a182-156">On the **Concur Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-concur-tutorial/tutorial_concur_url.png)

    <span data-ttu-id="9a182-158">a.</span><span class="sxs-lookup"><span data-stu-id="9a182-158">a.</span></span> <span data-ttu-id="9a182-159">W **Zaloguj się na adres URL** tekstowym, wpisz wartość, przy użyciu następującego wzorca:`https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span><span class="sxs-lookup"><span data-stu-id="9a182-159">In the **Sign on URL** textbox, type the value using the following pattern: `https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span></span>

    <span data-ttu-id="9a182-160">b.</span><span class="sxs-lookup"><span data-stu-id="9a182-160">b.</span></span> <span data-ttu-id="9a182-161">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<customer-domain>.concursolutions.com`</span><span class="sxs-lookup"><span data-stu-id="9a182-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<customer-domain>.concursolutions.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9a182-162">Wartości te nie są rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="9a182-162">These values are not the real.</span></span> <span data-ttu-id="9a182-163">Zaktualizować te wartości przy użyciu rzeczywistego konta na adres URL i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="9a182-163">Update these values with the actual Sign on URL and Identifier.</span></span> <span data-ttu-id="9a182-164">Skontaktuj się z [zespołem pomocy technicznej klienta cząstkowe](https://www.concur.co.in/contact) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="9a182-164">Contact [Concur Client support team](https://www.concur.co.in/contact) to get these values.</span></span> 

4. <span data-ttu-id="9a182-165">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="9a182-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-concur-tutorial/tutorial_concur_certificate.png) 

5. <span data-ttu-id="9a182-167">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9a182-167">Click **Save** button.</span></span>

    <span data-ttu-id="9a182-168">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="9a182-168">![Configure Single Sign-On](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span></span>

6. <span data-ttu-id="9a182-169">Do konfigurowania rejestracji jednokrotnej na **Concur** stronie, musisz wysłać pobrany **XML metadanych** Concur pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="9a182-169">To configure single sign-on on **Concur** side, you need to send the downloaded **Metadata XML** to Concur support.</span></span> <span data-ttu-id="9a182-170">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="9a182-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

  >[!NOTE]
  ><span data-ttu-id="9a182-171">Konfiguracja subskrypcji Concur dla federacyjnego logowania jednokrotnego za pośrednictwem SAML jest osobnym zadaniem musisz skontaktować się z [zespołem pomocy technicznej klienta cząstkowe](https://www.concur.co.in/contact) do wykonania.</span><span class="sxs-lookup"><span data-stu-id="9a182-171">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) to perform.</span></span> 
  
<CE>

> [!TIP]
> <span data-ttu-id="9a182-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="9a182-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9a182-173">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="9a182-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9a182-174">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9a182-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9a182-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a182-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="9a182-176">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9a182-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="9a182-178">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9a182-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9a182-179">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9a182-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9a182-181">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="9a182-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9a182-183">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9a182-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9a182-185">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9a182-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9a182-187">a.</span><span class="sxs-lookup"><span data-stu-id="9a182-187">a.</span></span> <span data-ttu-id="9a182-188">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9a182-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9a182-189">b.</span><span class="sxs-lookup"><span data-stu-id="9a182-189">b.</span></span> <span data-ttu-id="9a182-190">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9a182-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9a182-191">c.</span><span class="sxs-lookup"><span data-stu-id="9a182-191">c.</span></span> <span data-ttu-id="9a182-192">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="9a182-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9a182-193">d.</span><span class="sxs-lookup"><span data-stu-id="9a182-193">d.</span></span> <span data-ttu-id="9a182-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9a182-194">Click **Create**.</span></span>
 
### <a name="creating-a-concur-test-user"></a><span data-ttu-id="9a182-195">Tworzenie użytkownika testowego Concur</span><span class="sxs-lookup"><span data-stu-id="9a182-195">Creating a Concur test user</span></span>

<span data-ttu-id="9a182-196">Aplikacja obsługuje tylko w czasie Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników są tworzone automatycznie w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9a182-196">Application supports the Just in time user provisioning and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9a182-197">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a182-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9a182-198">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Concur.</span><span class="sxs-lookup"><span data-stu-id="9a182-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Concur.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="9a182-200">**Aby przypisać Simona Britta Concur, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="9a182-200">**To assign Britta Simon to Concur, perform the following steps:**</span></span>

1. <span data-ttu-id="9a182-201">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9a182-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="9a182-203">Na liście aplikacji zaznacz **Concur**.</span><span class="sxs-lookup"><span data-stu-id="9a182-203">In the applications list, select **Concur**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-concur-tutorial/tutorial_concur_app.png) 

3. <span data-ttu-id="9a182-205">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="9a182-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="9a182-207">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9a182-207">Click **Add** button.</span></span> <span data-ttu-id="9a182-208">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9a182-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="9a182-210">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="9a182-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9a182-211">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9a182-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9a182-212">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9a182-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9a182-213">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9a182-213">Testing single sign-on</span></span>

<span data-ttu-id="9a182-214">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9a182-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9a182-215">Po kliknięciu kafelka Concur w panelu dostępu, należy pobrać strony logowania Concur aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9a182-215">When you click the Concur tile in the Access Panel, you should get login page of Concur application.</span></span>
<span data-ttu-id="9a182-216">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9a182-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9a182-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="9a182-217">Additional resources</span></span>

* [<span data-ttu-id="9a182-218">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9a182-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9a182-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9a182-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="9a182-220">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="9a182-220">Configure User Provisioning</span></span>](active-directory-saas-concur-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-concur-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-concur-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-concur-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-concur-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-concur-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-concur-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-concur-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-concur-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-concur-tutorial/tutorial_general_203.png

