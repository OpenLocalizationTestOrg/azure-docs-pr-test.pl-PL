---
title: 'Samouczek: Integracji Azure Active Directory z Gigya | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Gigya."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2c7d200b-9242-44a5-ac8a-ab3214a78e41
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: b65a33989a045a3e0b57fda522a9bc3b0770c7f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gigya"></a><span data-ttu-id="2db03-103">Samouczek: Integracji Azure Active Directory z Gigya</span><span class="sxs-lookup"><span data-stu-id="2db03-103">Tutorial: Azure Active Directory integration with Gigya</span></span>

<span data-ttu-id="2db03-104">Z tego samouczka dowiesz się integrowanie Gigya z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2db03-104">In this tutorial, you learn how to integrate Gigya with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2db03-105">Integracja z usługą Azure AD Gigya zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="2db03-105">Integrating Gigya with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2db03-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Gigya</span><span class="sxs-lookup"><span data-stu-id="2db03-106">You can control in Azure AD who has access to Gigya</span></span>
- <span data-ttu-id="2db03-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Gigya (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2db03-107">You can enable your users to automatically get signed-on to Gigya (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2db03-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="2db03-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2db03-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2db03-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2db03-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2db03-110">Prerequisites</span></span>

<span data-ttu-id="2db03-111">Aby skonfigurować integrację usługi Azure AD z Gigya, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="2db03-111">To configure Azure AD integration with Gigya, you need the following items:</span></span>

- <span data-ttu-id="2db03-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2db03-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2db03-113">Gigya logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2db03-113">A Gigya single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2db03-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="2db03-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2db03-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="2db03-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2db03-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="2db03-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2db03-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2db03-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2db03-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="2db03-118">Scenario description</span></span>
<span data-ttu-id="2db03-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="2db03-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2db03-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="2db03-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2db03-121">Dodawanie Gigya z galerii</span><span class="sxs-lookup"><span data-stu-id="2db03-121">Adding Gigya from the gallery</span></span>
2. <span data-ttu-id="2db03-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="2db03-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gigya-from-the-gallery"></a><span data-ttu-id="2db03-123">Dodawanie Gigya z galerii</span><span class="sxs-lookup"><span data-stu-id="2db03-123">Adding Gigya from the gallery</span></span>
<span data-ttu-id="2db03-124">Aby skonfigurować integrację usługi Azure AD Gigya, należy dodać Gigya z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="2db03-124">To configure the integration of Gigya into Azure AD, you need to add Gigya from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2db03-125">**Aby dodać Gigya z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="2db03-125">**To add Gigya from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2db03-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="2db03-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="2db03-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="2db03-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2db03-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="2db03-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="2db03-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2db03-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="2db03-133">W polu wyszukiwania wpisz **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="2db03-133">In the search box, type **Gigya**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_search.png)

5. <span data-ttu-id="2db03-135">W panelu wyników wybierz **Gigya**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="2db03-135">In the results panel, select **Gigya**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2db03-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="2db03-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2db03-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Gigya w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="2db03-138">In this section, you configure and test Azure AD single sign-on with Gigya based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2db03-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Gigya jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2db03-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Gigya is to a user in Azure AD.</span></span> <span data-ttu-id="2db03-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Gigya musi się.</span><span class="sxs-lookup"><span data-stu-id="2db03-140">In other words, a link relationship between an Azure AD user and the related user in Gigya needs to be established.</span></span>

<span data-ttu-id="2db03-141">W Gigya, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="2db03-141">In Gigya, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2db03-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Gigya, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="2db03-142">To configure and test Azure AD single sign-on with Gigya, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2db03-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="2db03-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2db03-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="2db03-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2db03-145">**[Tworzenie użytkownika testowego Gigya](#creating-a-gigya-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Gigya połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2db03-145">**[Creating a Gigya test user](#creating-a-gigya-test-user)** - to have a counterpart of Britta Simon in Gigya that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2db03-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="2db03-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2db03-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="2db03-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2db03-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2db03-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2db03-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Gigya.</span><span class="sxs-lookup"><span data-stu-id="2db03-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Gigya application.</span></span>

<span data-ttu-id="2db03-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Gigya, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="2db03-150">**To configure Azure AD single sign-on with Gigya, perform the following steps:**</span></span>

1. <span data-ttu-id="2db03-151">W portalu Azure na **Gigya** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="2db03-151">In the Azure portal, on the **Gigya** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="2db03-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="2db03-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_samlbase.png)

3. <span data-ttu-id="2db03-155">Na **Gigya domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2db03-155">On the **Gigya Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_url.png)

    <span data-ttu-id="2db03-157">a.</span><span class="sxs-lookup"><span data-stu-id="2db03-157">a.</span></span> <span data-ttu-id="2db03-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`http://<companyname>.gigya.com`</span><span class="sxs-lookup"><span data-stu-id="2db03-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<companyname>.gigya.com`</span></span>

    <span data-ttu-id="2db03-159">b.</span><span class="sxs-lookup"><span data-stu-id="2db03-159">b.</span></span> <span data-ttu-id="2db03-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://fidm.gigya.com/saml/v2.0/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="2db03-160">In the **Identifier** textbox, type a URL using the following pattern: `https://fidm.gigya.com/saml/v2.0/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2db03-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="2db03-161">These values are not real.</span></span> <span data-ttu-id="2db03-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="2db03-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2db03-163">Skontaktuj się z [zespołem pomocy technicznej klienta Gigya](https://www.gigya.com/support-policy/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="2db03-163">Contact [Gigya Client support team](https://www.gigya.com/support-policy/) to get these values.</span></span> 
 
4. <span data-ttu-id="2db03-164">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="2db03-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_certificate.png) 

5. <span data-ttu-id="2db03-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2db03-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-gigya-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2db03-168">Na **konfiguracji Gigya** , kliknij przycisk **skonfigurować Gigya** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="2db03-168">On the **Gigya Configuration** section, click **Configure Gigya** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2db03-169">Kopiuj **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="2db03-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_configure.png) 

7. <span data-ttu-id="2db03-171">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Gigya jako administrator.</span><span class="sxs-lookup"><span data-stu-id="2db03-171">In a different web browser window, log into your Gigya company site as an administrator.</span></span>

8. <span data-ttu-id="2db03-172">Przejdź do **ustawienia \> logowania SAML**, a następnie kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2db03-172">Go to **Settings \> SAML Login**, and then click the **Add** button.</span></span>
   
    <span data-ttu-id="2db03-173">![Logowania SAML](./media/active-directory-saas-gigya-tutorial/ic789532.png "logowania SAML")</span><span class="sxs-lookup"><span data-stu-id="2db03-173">![SAML Login](./media/active-directory-saas-gigya-tutorial/ic789532.png "SAML Login")</span></span>

9. <span data-ttu-id="2db03-174">W **logowania SAML** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2db03-174">In the **SAML Login** section, perform the following steps:</span></span>
   
    <span data-ttu-id="2db03-175">![Konfiguracja SAML](./media/active-directory-saas-gigya-tutorial/ic789533.png "Konfiguracja SAML")</span><span class="sxs-lookup"><span data-stu-id="2db03-175">![SAML Configuration](./media/active-directory-saas-gigya-tutorial/ic789533.png "SAML Configuration")</span></span>
   
    <span data-ttu-id="2db03-176">a.</span><span class="sxs-lookup"><span data-stu-id="2db03-176">a.</span></span> <span data-ttu-id="2db03-177">W **nazwa** tekstowym, wpisz nazwę dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="2db03-177">In the **Name** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="2db03-178">b.</span><span class="sxs-lookup"><span data-stu-id="2db03-178">b.</span></span> <span data-ttu-id="2db03-179">W **wystawcy** pole tekstowe, Wklej wartość **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2db03-179">In **Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure Portal.</span></span> 
   
    <span data-ttu-id="2db03-180">c.</span><span class="sxs-lookup"><span data-stu-id="2db03-180">c.</span></span> <span data-ttu-id="2db03-181">W **pojedynczy znak na adres URL usługi** pole tekstowe, Wklej wartość **pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2db03-181">In **Single Sign-On Service URL** textbox, paste the value of **Single Sign-On Service URL** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="2db03-182">d.</span><span class="sxs-lookup"><span data-stu-id="2db03-182">d.</span></span> <span data-ttu-id="2db03-183">W **Format Identyfikatora nazwy** pole tekstowe, Wklej wartość **Format identyfikatora nazwy** , które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2db03-183">In **Name ID Format** textbox, paste the value of **Name Identifier Format** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="2db03-184">e.</span><span class="sxs-lookup"><span data-stu-id="2db03-184">e.</span></span> <span data-ttu-id="2db03-185">Otwórz w Notatniku pobrany z portalu Azure certyfikatu zakodowanego base-64, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikatu X.509** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="2db03-185">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="2db03-186">f.</span><span class="sxs-lookup"><span data-stu-id="2db03-186">f.</span></span> <span data-ttu-id="2db03-187">Kliknij przycisk **Zapisz ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="2db03-187">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="2db03-188">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="2db03-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2db03-189">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="2db03-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2db03-190">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2db03-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2db03-191">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2db03-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="2db03-192">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="2db03-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="2db03-194">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="2db03-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2db03-195">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="2db03-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2db03-197">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="2db03-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2db03-199">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2db03-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2db03-201">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2db03-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-gigya-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2db03-203">a.</span><span class="sxs-lookup"><span data-stu-id="2db03-203">a.</span></span> <span data-ttu-id="2db03-204">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2db03-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2db03-205">b.</span><span class="sxs-lookup"><span data-stu-id="2db03-205">b.</span></span> <span data-ttu-id="2db03-206">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2db03-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2db03-207">c.</span><span class="sxs-lookup"><span data-stu-id="2db03-207">c.</span></span> <span data-ttu-id="2db03-208">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="2db03-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2db03-209">d.</span><span class="sxs-lookup"><span data-stu-id="2db03-209">d.</span></span> <span data-ttu-id="2db03-210">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="2db03-210">Click **Create**.</span></span>
 
### <a name="creating-a-gigya-test-user"></a><span data-ttu-id="2db03-211">Tworzenie użytkownika testowego Gigya</span><span class="sxs-lookup"><span data-stu-id="2db03-211">Creating a Gigya test user</span></span>

<span data-ttu-id="2db03-212">Aby włączyć użytkowników usługi Azure AD zalogować się do Gigya, musi być przygotowana do Gigya.</span><span class="sxs-lookup"><span data-stu-id="2db03-212">In order to enable Azure AD users to log into Gigya, they must be provisioned into Gigya.</span></span>  
<span data-ttu-id="2db03-213">W przypadku Gigya Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="2db03-213">In the case of Gigya, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="2db03-214">Aby udostępnić konta użytkowników, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2db03-214">To provision a user accounts, perform the following steps:</span></span>

1. <span data-ttu-id="2db03-215">Zaloguj się do Twojego **Gigya** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="2db03-215">Log in to your **Gigya** company site as an administrator.</span></span>

2. <span data-ttu-id="2db03-216">Przejdź do **Admin \> Zarządzanie użytkownikami**, a następnie kliknij przycisk **zaprosić użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="2db03-216">Go to **Admin \> Manage Users**, and then click **Invite Users**.</span></span>
   
    <span data-ttu-id="2db03-217">![Zarządzaj użytkownikami](./media/active-directory-saas-gigya-tutorial/ic789535.png "Zarządzanie użytkownikami")</span><span class="sxs-lookup"><span data-stu-id="2db03-217">![Manage Users](./media/active-directory-saas-gigya-tutorial/ic789535.png "Manage Users")</span></span>

3. <span data-ttu-id="2db03-218">W oknie dialogowym zaprosić użytkowników wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2db03-218">On the Invite Users dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="2db03-219">![Zaprosić użytkowników](./media/active-directory-saas-gigya-tutorial/ic789536.png "zaprosić użytkowników")</span><span class="sxs-lookup"><span data-stu-id="2db03-219">![Invite Users](./media/active-directory-saas-gigya-tutorial/ic789536.png "Invite Users")</span></span>
   
    <span data-ttu-id="2db03-220">a.</span><span class="sxs-lookup"><span data-stu-id="2db03-220">a.</span></span> <span data-ttu-id="2db03-221">W **E-mail** tekstowym, wpisz alias e-mail prawidłowe konto usługi Azure Active Directory, aby udostępnić.</span><span class="sxs-lookup"><span data-stu-id="2db03-221">In the **Email** textbox, type the email alias of a valid Azure Active Directory account you want to provision.</span></span>
    
    <span data-ttu-id="2db03-222">b.</span><span class="sxs-lookup"><span data-stu-id="2db03-222">b.</span></span> <span data-ttu-id="2db03-223">Kliknij przycisk **zaprosić użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="2db03-223">Click **Invite User**.</span></span>
      
    > [!NOTE]
    > <span data-ttu-id="2db03-224">Właściciel konta usługi Azure Active Directory otrzyma wiadomość e-mail zawierającą łącze do potwierdzenia konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="2db03-224">The Azure Active Directory account holder will receive an email that includes a link to confirm the account before it becomes active.</span></span>
    > 
    

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2db03-225">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2db03-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2db03-226">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Gigya.</span><span class="sxs-lookup"><span data-stu-id="2db03-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Gigya.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="2db03-228">**Aby przypisać Simona Britta Gigya, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="2db03-228">**To assign Britta Simon to Gigya, perform the following steps:**</span></span>

1. <span data-ttu-id="2db03-229">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="2db03-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="2db03-231">Na liście aplikacji zaznacz **Gigya**.</span><span class="sxs-lookup"><span data-stu-id="2db03-231">In the applications list, select **Gigya**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_app.png) 

3. <span data-ttu-id="2db03-233">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="2db03-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="2db03-235">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2db03-235">Click **Add** button.</span></span> <span data-ttu-id="2db03-236">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2db03-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="2db03-238">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="2db03-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2db03-239">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2db03-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2db03-240">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2db03-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2db03-241">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2db03-241">Testing single sign-on</span></span>

<span data-ttu-id="2db03-242">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="2db03-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="2db03-243">Po kliknięciu kafelka Gigya w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Gigya.</span><span class="sxs-lookup"><span data-stu-id="2db03-243">When you click the Gigya tile in the Access Panel, you should get automatically signed-on to your Gigya application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2db03-244">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="2db03-244">Additional resources</span></span>

* [<span data-ttu-id="2db03-245">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2db03-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2db03-246">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2db03-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_203.png

