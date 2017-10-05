---
title: 'Samouczek: Integracji Azure Active Directory z mianowicie | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory, a mianowicie."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9541d5c4-4c82-4b5b-b01a-6a3f75a2b7a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 1d7e8fbcfc757853ab909bbb05522f3dc387715d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-namely"></a><span data-ttu-id="4ed39-103">Samouczek: Integracji Azure Active Directory z mianowicie</span><span class="sxs-lookup"><span data-stu-id="4ed39-103">Tutorial: Azure Active Directory integration with Namely</span></span>

<span data-ttu-id="4ed39-104">Z tego samouczka dowiesz się mianowicie Integracja z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4ed39-104">In this tutorial, you learn how to integrate Namely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4ed39-105">To znaczy integracji z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="4ed39-105">Integrating Namely with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4ed39-106">Można kontrolować w usłudze Azure AD, który ma dostęp do:</span><span class="sxs-lookup"><span data-stu-id="4ed39-106">You can control in Azure AD who has access to Namely</span></span>
- <span data-ttu-id="4ed39-107">Można umożliwić użytkownikom automatycznie pobrać zalogowane do mianowicie (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ed39-107">You can enable your users to automatically get signed-on to Namely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4ed39-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4ed39-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="4ed39-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4ed39-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ed39-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4ed39-110">Prerequisites</span></span>

<span data-ttu-id="4ed39-111">Aby skonfigurować usługi Azure AD integracji z mianowicie, możesz potrzebne są następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="4ed39-111">To configure Azure AD integration with Namely, you need the following items:</span></span>

- <span data-ttu-id="4ed39-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ed39-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4ed39-113">To znaczy logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="4ed39-113">A Namely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4ed39-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="4ed39-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4ed39-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="4ed39-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4ed39-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="4ed39-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4ed39-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4ed39-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4ed39-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="4ed39-118">Scenario description</span></span>
<span data-ttu-id="4ed39-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="4ed39-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4ed39-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="4ed39-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4ed39-121">Dodawanie mianowicie z galerii</span><span class="sxs-lookup"><span data-stu-id="4ed39-121">Adding Namely from the gallery</span></span>
2. <span data-ttu-id="4ed39-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="4ed39-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-namely-from-the-gallery"></a><span data-ttu-id="4ed39-123">Dodawanie mianowicie z galerii</span><span class="sxs-lookup"><span data-stu-id="4ed39-123">Adding Namely from the gallery</span></span>
<span data-ttu-id="4ed39-124">Aby skonfigurować integrację mianowicie do usługi Azure AD, należy dodać mianowicie z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="4ed39-124">To configure the integration of Namely into Azure AD, you need to add Namely from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4ed39-125">**Aby dodać mianowicie z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4ed39-125">**To add Namely from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4ed39-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4ed39-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="4ed39-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="4ed39-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4ed39-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4ed39-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="4ed39-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4ed39-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="4ed39-133">W polu wyszukiwania wpisz **mianowicie**.</span><span class="sxs-lookup"><span data-stu-id="4ed39-133">In the search box, type **Namely**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-namely-tutorial/tutorial_namely_search.png)

5. <span data-ttu-id="4ed39-135">W panelu wyników wybierz **mianowicie**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="4ed39-135">In the results panel, select **Namely**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-namely-tutorial/tutorial_namely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4ed39-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="4ed39-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4ed39-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z, a mianowicie w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="4ed39-138">In this section, you configure and test Azure AD single sign-on with Namely based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4ed39-139">Do rejestracji jednokrotnej do pracy usługi Azure AD musi ustalić użytkownika odpowiednika w mianowicie do użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ed39-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Namely is to a user in Azure AD.</span></span> <span data-ttu-id="4ed39-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w musi mianowicie określone.</span><span class="sxs-lookup"><span data-stu-id="4ed39-140">In other words, a link relationship between an Azure AD user and the related user in Namely needs to be established.</span></span>

<span data-ttu-id="4ed39-141">To znaczy, przypisywanie wartości **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącze.</span><span class="sxs-lookup"><span data-stu-id="4ed39-141">In Namely, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4ed39-142">Do konfigurowania i testowania usługi Azure AD rejestracji jednokrotnej z mianowicie, możesz, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="4ed39-142">To configure and test Azure AD single sign-on with Namely, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4ed39-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="4ed39-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4ed39-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="4ed39-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4ed39-145">**[Tworzenie mianowicie użytkownik testowy](#creating-a-namely-test-user)**  — aby odpowiednikiem Simona Britta w mianowicie połączonego użytkownika reprezentacja usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4ed39-145">**[Creating a Namely test user](#creating-a-namely-test-user)** - to have a counterpart of Britta Simon in Namely that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4ed39-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="4ed39-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4ed39-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="4ed39-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4ed39-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4ed39-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4ed39-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w mianowicie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4ed39-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Namely application.</span></span>

<span data-ttu-id="4ed39-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z mianowicie, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4ed39-150">**To configure Azure AD single sign-on with Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="4ed39-151">W portalu Azure na **mianowicie** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="4ed39-151">In the Azure portal, on the **Namely** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="4ed39-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="4ed39-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_namely_samlbase.png)

3. <span data-ttu-id="4ed39-155">Na **mianowicie domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4ed39-155">On the **Namely Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_namely_url.png)

    <span data-ttu-id="4ed39-157">a.</span><span class="sxs-lookup"><span data-stu-id="4ed39-157">a.</span></span> <span data-ttu-id="4ed39-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.namely.com`</span><span class="sxs-lookup"><span data-stu-id="4ed39-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.namely.com`</span></span>

    <span data-ttu-id="4ed39-159">b.</span><span class="sxs-lookup"><span data-stu-id="4ed39-159">b.</span></span> <span data-ttu-id="4ed39-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.namely.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="4ed39-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.namely.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4ed39-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="4ed39-161">These values are not real.</span></span> <span data-ttu-id="4ed39-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="4ed39-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4ed39-163">Skontaktuj się z [zespół obsługi klienta a mianowicie](https://www.namely.com/contact/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="4ed39-163">Contact [Namely Client support team](https://www.namely.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="4ed39-164">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="4ed39-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_namely_certificate.png) 

5. <span data-ttu-id="4ed39-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4ed39-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4ed39-168">Na **mianowicie konfiguracji** kliknij **skonfigurować mianowicie** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="4ed39-168">On the **Namely Configuration** section, click **Configure Namely** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4ed39-169">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="4ed39-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_namely_configure.png) 

7. <span data-ttu-id="4ed39-171">W innym oknie przeglądarki, zaloguj się na Twoje mianowicie witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="4ed39-171">In another browser window, sign on to your Namely company site as an administrator.</span></span>

8. <span data-ttu-id="4ed39-172">Na pasku narzędzi u góry kliknij **firmy**.</span><span class="sxs-lookup"><span data-stu-id="4ed39-172">In the toolbar on the top, click **Company**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_namely_06.png) 

9. <span data-ttu-id="4ed39-174">Kliknij kartę **Ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="4ed39-174">Click the **Settings** tab.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_namely_07.png) 

10. <span data-ttu-id="4ed39-176">Kliknij przycisk **SAML**.</span><span class="sxs-lookup"><span data-stu-id="4ed39-176">Click **SAML**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_namely_08.png) 

11. <span data-ttu-id="4ed39-178">Na **ustawienia SAML** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4ed39-178">On the **SAML Settings** page, perform the following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_namely_09.png)
 
    <span data-ttu-id="4ed39-180">a.</span><span class="sxs-lookup"><span data-stu-id="4ed39-180">a.</span></span> <span data-ttu-id="4ed39-181">Kliknij przycisk **Włącz SAML**.</span><span class="sxs-lookup"><span data-stu-id="4ed39-181">Click **Enable SAML**.</span></span> 

    <span data-ttu-id="4ed39-182">b.</span><span class="sxs-lookup"><span data-stu-id="4ed39-182">b.</span></span> <span data-ttu-id="4ed39-183">W **adres url logowania jednokrotnego dostawcy tożsamości** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4ed39-183">In the **Identity provider SSO url** textbox,  paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="4ed39-184">c.</span><span class="sxs-lookup"><span data-stu-id="4ed39-184">c.</span></span> <span data-ttu-id="4ed39-185">Otwórz w Notatniku pobranego certyfikatu, skopiuj zawartość, a następnie wklej go do **certyfikat dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="4ed39-185">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Identity provider certificate** textbox.</span></span>
     
    <span data-ttu-id="4ed39-186">d.</span><span class="sxs-lookup"><span data-stu-id="4ed39-186">d.</span></span> <span data-ttu-id="4ed39-187">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="4ed39-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="4ed39-188">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="4ed39-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4ed39-189">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="4ed39-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4ed39-190">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4ed39-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4ed39-191">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ed39-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="4ed39-192">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="4ed39-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="4ed39-194">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4ed39-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4ed39-195">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4ed39-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4ed39-197">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="4ed39-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4ed39-199">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4ed39-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4ed39-201">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4ed39-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4ed39-203">a.</span><span class="sxs-lookup"><span data-stu-id="4ed39-203">a.</span></span> <span data-ttu-id="4ed39-204">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4ed39-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4ed39-205">b.</span><span class="sxs-lookup"><span data-stu-id="4ed39-205">b.</span></span> <span data-ttu-id="4ed39-206">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4ed39-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4ed39-207">c.</span><span class="sxs-lookup"><span data-stu-id="4ed39-207">c.</span></span> <span data-ttu-id="4ed39-208">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="4ed39-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="4ed39-209">d.</span><span class="sxs-lookup"><span data-stu-id="4ed39-209">d.</span></span> <span data-ttu-id="4ed39-210">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4ed39-210">Click **Create**.</span></span>
 
### <a name="creating-a-namely-test-user"></a><span data-ttu-id="4ed39-211">Tworzenie mianowicie użytkownik testowy</span><span class="sxs-lookup"><span data-stu-id="4ed39-211">Creating a Namely test user</span></span>

<span data-ttu-id="4ed39-212">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w mianowicie.</span><span class="sxs-lookup"><span data-stu-id="4ed39-212">The objective of this section is to create a user called Britta Simon in Namely.</span></span>

<span data-ttu-id="4ed39-213">**Aby utworzyć użytkownika o nazwie Simona Britta w mianowicie, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4ed39-213">**To create a user called Britta Simon in Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="4ed39-214">Logowanie do Twojej mianowicie witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="4ed39-214">Sign-on to your Namely company site as an administrator.</span></span>

2. <span data-ttu-id="4ed39-215">Na pasku narzędzi u góry kliknij **osób**.</span><span class="sxs-lookup"><span data-stu-id="4ed39-215">In the toolbar on the top, click **People**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_namely_10.png) 

3. <span data-ttu-id="4ed39-217">Kliknij przycisk **katalogu** kartę.</span><span class="sxs-lookup"><span data-stu-id="4ed39-217">Click the **Directory** tab.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_namely_11.png) 

4. <span data-ttu-id="4ed39-219">Kliknij przycisk **Dodawanie nowej osoby**.</span><span class="sxs-lookup"><span data-stu-id="4ed39-219">Click **Add New Person**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_namely_12.png)

5. <span data-ttu-id="4ed39-221">Na **Dodawanie nowej osoby** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4ed39-221">On the **Add New Person** dialog, perform the following steps:</span></span>

    <span data-ttu-id="4ed39-222">a.</span><span class="sxs-lookup"><span data-stu-id="4ed39-222">a.</span></span> <span data-ttu-id="4ed39-223">W **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="4ed39-223">In the **First name** textbox, type **Britta**.</span></span>

    <span data-ttu-id="4ed39-224">b.</span><span class="sxs-lookup"><span data-stu-id="4ed39-224">b.</span></span> <span data-ttu-id="4ed39-225">W **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="4ed39-225">In the **Last name** textbox, type **Simon**.</span></span>

    <span data-ttu-id="4ed39-226">c.</span><span class="sxs-lookup"><span data-stu-id="4ed39-226">c.</span></span> <span data-ttu-id="4ed39-227">W **E-mail** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4ed39-227">In the **Email** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4ed39-228">d.</span><span class="sxs-lookup"><span data-stu-id="4ed39-228">d.</span></span> <span data-ttu-id="4ed39-229">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="4ed39-229">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="4ed39-230">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4ed39-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="4ed39-231">W tej sekcji można włączyć Simona Britta do użycia Azure logowania jednokrotnego za udzielanie dostępu do:.</span><span class="sxs-lookup"><span data-stu-id="4ed39-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Namely.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="4ed39-233">**Aby przypisać Simona Britta do mianowicie, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="4ed39-233">**To assign Britta Simon to Namely, perform the following steps:**</span></span>

1. <span data-ttu-id="4ed39-234">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4ed39-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="4ed39-236">Na liście aplikacji zaznacz **mianowicie**.</span><span class="sxs-lookup"><span data-stu-id="4ed39-236">In the applications list, select **Namely**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-namely-tutorial/tutorial_namely_app.png) 

3. <span data-ttu-id="4ed39-238">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="4ed39-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="4ed39-240">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4ed39-240">Click **Add** button.</span></span> <span data-ttu-id="4ed39-241">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4ed39-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="4ed39-243">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="4ed39-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4ed39-244">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4ed39-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4ed39-245">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4ed39-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4ed39-246">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4ed39-246">Testing single sign-on</span></span>

<span data-ttu-id="4ed39-247">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="4ed39-247">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="4ed39-248">Po kliknięciu kafelka mianowicie w panelu dostępu, użytkownik powinien pobrać automatycznie podpisany w przypadku mianowicie aplikacji</span><span class="sxs-lookup"><span data-stu-id="4ed39-248">When you click the Namely tile in the Access Panel, you should get automatically signed-on to your Namely application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4ed39-249">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="4ed39-249">Additional resources</span></span>

* [<span data-ttu-id="4ed39-250">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4ed39-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4ed39-251">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4ed39-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-namely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-namely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-namely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-namely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-namely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-namely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-namely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-namely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-namely-tutorial/tutorial_general_203.png

