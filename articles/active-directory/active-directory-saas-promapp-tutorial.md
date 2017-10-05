---
title: 'Samouczek: Integracji Azure Active Directory z Promapp | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Promapp."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 418d0601-6e7a-4997-a683-73fa30a2cfb5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 27013ca9724cf2f57fc85f5f4ccb71921ca57a3b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-promapp"></a><span data-ttu-id="e36a0-103">Samouczek: Integracji Azure Active Directory z Promapp</span><span class="sxs-lookup"><span data-stu-id="e36a0-103">Tutorial: Azure Active Directory integration with Promapp</span></span>

<span data-ttu-id="e36a0-104">Z tego samouczka dowiesz się integrowanie Promapp z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e36a0-104">In this tutorial, you learn how to integrate Promapp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e36a0-105">Integracja z usługą Azure AD Promapp zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e36a0-105">Integrating Promapp with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e36a0-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Promapp</span><span class="sxs-lookup"><span data-stu-id="e36a0-106">You can control in Azure AD who has access to Promapp</span></span>
- <span data-ttu-id="e36a0-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Promapp (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e36a0-107">You can enable your users to automatically get signed-on to Promapp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e36a0-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e36a0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e36a0-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e36a0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e36a0-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e36a0-110">Prerequisites</span></span>

<span data-ttu-id="e36a0-111">Aby skonfigurować integrację usługi Azure AD z Promapp, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e36a0-111">To configure Azure AD integration with Promapp, you need the following items:</span></span>

- <span data-ttu-id="e36a0-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e36a0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e36a0-113">Promapp logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e36a0-113">A Promapp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e36a0-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e36a0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e36a0-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="e36a0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e36a0-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e36a0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e36a0-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e36a0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e36a0-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="e36a0-118">Scenario description</span></span>
<span data-ttu-id="e36a0-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="e36a0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e36a0-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="e36a0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e36a0-121">Dodawanie Promapp z galerii</span><span class="sxs-lookup"><span data-stu-id="e36a0-121">Adding Promapp from the gallery</span></span>
2. <span data-ttu-id="e36a0-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e36a0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-promapp-from-the-gallery"></a><span data-ttu-id="e36a0-123">Dodawanie Promapp z galerii</span><span class="sxs-lookup"><span data-stu-id="e36a0-123">Adding Promapp from the gallery</span></span>
<span data-ttu-id="e36a0-124">Aby skonfigurować integrację usługi Azure AD Promapp, należy dodać Promapp z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="e36a0-124">To configure the integration of Promapp into Azure AD, you need to add Promapp from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e36a0-125">**Aby dodać Promapp z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e36a0-125">**To add Promapp from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e36a0-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e36a0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="e36a0-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e36a0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e36a0-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e36a0-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="e36a0-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e36a0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="e36a0-133">W polu wyszukiwania wpisz **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="e36a0-133">In the search box, type **Promapp**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_search.png)

5. <span data-ttu-id="e36a0-135">W panelu wyników wybierz **Promapp**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="e36a0-135">In the results panel, select **Promapp**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e36a0-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e36a0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e36a0-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Promapp w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="e36a0-138">In this section, you configure and test Azure AD single sign-on with Promapp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e36a0-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Promapp jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e36a0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Promapp is to a user in Azure AD.</span></span> <span data-ttu-id="e36a0-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Promapp musi się.</span><span class="sxs-lookup"><span data-stu-id="e36a0-140">In other words, a link relationship between an Azure AD user and the related user in Promapp needs to be established.</span></span>

<span data-ttu-id="e36a0-141">W Promapp, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="e36a0-141">In Promapp, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e36a0-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Promapp, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="e36a0-142">To configure and test Azure AD single sign-on with Promapp, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e36a0-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e36a0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e36a0-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e36a0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e36a0-145">**[Tworzenie użytkownika testowego Promapp](#creating-a-promapp-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Promapp połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e36a0-145">**[Creating a Promapp test user](#creating-a-promapp-test-user)** - to have a counterpart of Britta Simon in Promapp that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e36a0-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e36a0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e36a0-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="e36a0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e36a0-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e36a0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e36a0-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Promapp.</span><span class="sxs-lookup"><span data-stu-id="e36a0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Promapp application.</span></span>

<span data-ttu-id="e36a0-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Promapp, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e36a0-150">**To configure Azure AD single sign-on with Promapp, perform the following steps:**</span></span>

1. <span data-ttu-id="e36a0-151">W portalu Azure na **Promapp** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e36a0-151">In the Azure portal, on the **Promapp** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="e36a0-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="e36a0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_samlbase.png)

3. <span data-ttu-id="e36a0-155">Na **Promapp domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e36a0-155">On the **Promapp Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_url.png)

    <span data-ttu-id="e36a0-157">a.</span><span class="sxs-lookup"><span data-stu-id="e36a0-157">a.</span></span> <span data-ttu-id="e36a0-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span><span class="sxs-lookup"><span data-stu-id="e36a0-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span></span>

    <span data-ttu-id="e36a0-159">b.</span><span class="sxs-lookup"><span data-stu-id="e36a0-159">b.</span></span> <span data-ttu-id="e36a0-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://DOMAINNAME.promapp.com/TENANTNAME`</span><span class="sxs-lookup"><span data-stu-id="e36a0-160">In the **Identifier** textbox, type a URL using the following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e36a0-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="e36a0-161">These values are not real.</span></span> <span data-ttu-id="e36a0-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="e36a0-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e36a0-163">Skontaktuj się z [zespołem pomocy technicznej klienta Promapp](https://www.promapp.com/about-us/contact-us/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="e36a0-163">Contact [Promapp Client support team](https://www.promapp.com/about-us/contact-us/) to get these values.</span></span>

4. <span data-ttu-id="e36a0-164">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e36a0-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_certificate.png) 

5. <span data-ttu-id="e36a0-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e36a0-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-promapp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e36a0-168">Na **konfiguracji Promapp** , kliknij przycisk **skonfigurować Promapp** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="e36a0-168">On the **Promapp Configuration** section, click **Configure Promapp** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e36a0-169">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="e36a0-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_configure.png) 

7. <span data-ttu-id="e36a0-171">Logowanie do witryny firmy Promapp jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e36a0-171">Sign-on to your Promapp company site as administrator.</span></span> 

8. <span data-ttu-id="e36a0-172">W menu u góry kliknij **Admin**.</span><span class="sxs-lookup"><span data-stu-id="e36a0-172">In the menu on the top, click **Admin**.</span></span> 
   
    ![Azure AD rejestracji jednokrotnej][12]

9. <span data-ttu-id="e36a0-174">Kliknij pozycję **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="e36a0-174">Click **Configure**.</span></span> 
   
    ![Azure AD rejestracji jednokrotnej][13]

10. <span data-ttu-id="e36a0-176">Na **zabezpieczeń** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e36a0-176">On the **Security** dialog, perform the following steps:</span></span>
   
    ![Azure AD rejestracji jednokrotnej][14]
    
    <span data-ttu-id="e36a0-178">a.</span><span class="sxs-lookup"><span data-stu-id="e36a0-178">a.</span></span> <span data-ttu-id="e36a0-179">Wklej **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure do **adres URL logowania jednokrotnego logowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="e36a0-179">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **SSO-Login URL** textbox.</span></span>
    
    <span data-ttu-id="e36a0-180">b.</span><span class="sxs-lookup"><span data-stu-id="e36a0-180">b.</span></span> <span data-ttu-id="e36a0-181">Jako **logowania jednokrotnego — tryb rejestracji jednokrotnej**, wybierz pozycję **opcjonalnie**, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="e36a0-181">As **SSO - Single Sign-on Mode**, select **Optional**, and then click **Save**.</span></span>

    <span data-ttu-id="e36a0-182">c.</span><span class="sxs-lookup"><span data-stu-id="e36a0-182">c.</span></span> <span data-ttu-id="e36a0-183">Otwórz pobranego certyfikatu w programie Notatnik, skopiuj zawartość certyfikatu bez pierwszego wiersza (---BEGIN CERTIFICATE---) i ostatniego wiersza (---koniec certyfikat---) Wklej ją do **certyfikatu x.509 logowania jednokrotnego** pola tekstowego, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="e36a0-183">Open the downloaded certificate in notepad, copy the certificate content without the first line (-----BEGIN CERTIFICATE-----) and the last line (-----END CERTIFICATE-----), paste it into the **SSO-x.509 Certificate** textbox, and then click **Save**.</span></span>
        
> [!TIP]
> <span data-ttu-id="e36a0-184">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="e36a0-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e36a0-185">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="e36a0-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e36a0-186">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e36a0-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e36a0-187">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e36a0-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="e36a0-188">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e36a0-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="e36a0-190">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e36a0-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e36a0-191">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e36a0-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e36a0-193">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="e36a0-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e36a0-195">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e36a0-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e36a0-197">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e36a0-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e36a0-199">a.</span><span class="sxs-lookup"><span data-stu-id="e36a0-199">a.</span></span> <span data-ttu-id="e36a0-200">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e36a0-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e36a0-201">b.</span><span class="sxs-lookup"><span data-stu-id="e36a0-201">b.</span></span> <span data-ttu-id="e36a0-202">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e36a0-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e36a0-203">c.</span><span class="sxs-lookup"><span data-stu-id="e36a0-203">c.</span></span> <span data-ttu-id="e36a0-204">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="e36a0-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e36a0-205">d.</span><span class="sxs-lookup"><span data-stu-id="e36a0-205">d.</span></span> <span data-ttu-id="e36a0-206">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e36a0-206">Click **Create**.</span></span>
 
### <a name="creating-a-promapp-test-user"></a><span data-ttu-id="e36a0-207">Tworzenie użytkownika testowego Promapp</span><span class="sxs-lookup"><span data-stu-id="e36a0-207">Creating a Promapp test user</span></span>

<span data-ttu-id="e36a0-208">Aplikacja Promapp obsługuje Just in Time inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="e36a0-208">The Promapp application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="e36a0-209">Oznacza to konto użytkownika jest tworzone automatycznie w razie potrzeby podczas próby uzyskania dostępu do aplikacji za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="e36a0-209">This means, a user account is automatically created if necessary during an attempt to access the application using the Access Panel.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e36a0-210">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e36a0-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e36a0-211">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Promapp.</span><span class="sxs-lookup"><span data-stu-id="e36a0-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Promapp.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="e36a0-213">**Aby przypisać Simona Britta Promapp, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="e36a0-213">**To assign Britta Simon to Promapp, perform the following steps:**</span></span>

1. <span data-ttu-id="e36a0-214">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e36a0-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="e36a0-216">Na liście aplikacji zaznacz **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="e36a0-216">In the applications list, select **Promapp**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_app.png) 

3. <span data-ttu-id="e36a0-218">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e36a0-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="e36a0-220">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e36a0-220">Click **Add** button.</span></span> <span data-ttu-id="e36a0-221">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e36a0-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="e36a0-223">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="e36a0-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e36a0-224">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e36a0-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e36a0-225">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e36a0-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e36a0-226">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e36a0-226">Testing single sign-on</span></span>

<span data-ttu-id="e36a0-227">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="e36a0-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="e36a0-228">Po kliknięciu kafelka Promapp w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Promapp.</span><span class="sxs-lookup"><span data-stu-id="e36a0-228">When you click the Promapp tile in the Access Panel, you should get automatically signed-on to your Promapp application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e36a0-229">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e36a0-229">Additional resources</span></span>

* [<span data-ttu-id="e36a0-230">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e36a0-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e36a0-231">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e36a0-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_05.png
[13]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_06.png
[14]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_07.png

[100]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_203.png

