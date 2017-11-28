---
title: 'Samouczek: Integracji Azure Active Directory z Bime | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Bime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdcf0729-c880-4c95-b739-0f6345b17dd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 8f46ff1265d302ab114747b4b45227e58718166b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bime"></a><span data-ttu-id="f2a23-103">Samouczek: Integracji Azure Active Directory z Bime</span><span class="sxs-lookup"><span data-stu-id="f2a23-103">Tutorial: Azure Active Directory integration with Bime</span></span>

<span data-ttu-id="f2a23-104">Z tego samouczka dowiesz się integrowanie Bime z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f2a23-104">In this tutorial, you learn how to integrate Bime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f2a23-105">Integracja z usługą Azure AD Bime zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="f2a23-105">Integrating Bime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f2a23-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Bime</span><span class="sxs-lookup"><span data-stu-id="f2a23-106">You can control in Azure AD who has access to Bime</span></span>
- <span data-ttu-id="f2a23-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Bime (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f2a23-107">You can enable your users to automatically get signed-on to Bime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f2a23-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f2a23-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f2a23-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f2a23-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2a23-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f2a23-110">Prerequisites</span></span>

<span data-ttu-id="f2a23-111">Aby skonfigurować integrację usługi Azure AD z Bime, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f2a23-111">To configure Azure AD integration with Bime, you need the following items:</span></span>

- <span data-ttu-id="f2a23-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f2a23-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f2a23-113">Bime logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="f2a23-113">A Bime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f2a23-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="f2a23-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f2a23-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="f2a23-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f2a23-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="f2a23-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f2a23-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f2a23-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f2a23-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="f2a23-118">Scenario description</span></span>
<span data-ttu-id="f2a23-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="f2a23-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f2a23-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="f2a23-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f2a23-121">Dodawanie Bime z galerii</span><span class="sxs-lookup"><span data-stu-id="f2a23-121">Adding Bime from the gallery</span></span>
2. <span data-ttu-id="f2a23-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f2a23-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bime-from-the-gallery"></a><span data-ttu-id="f2a23-123">Dodawanie Bime z galerii</span><span class="sxs-lookup"><span data-stu-id="f2a23-123">Adding Bime from the gallery</span></span>
<span data-ttu-id="f2a23-124">Aby skonfigurować integrację usługi Azure AD Bime, należy dodać Bime z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="f2a23-124">To configure the integration of Bime into Azure AD, you need to add Bime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f2a23-125">**Aby dodać Bime z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f2a23-125">**To add Bime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f2a23-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f2a23-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="f2a23-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="f2a23-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f2a23-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f2a23-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="f2a23-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f2a23-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="f2a23-133">W polu wyszukiwania wpisz **Bime**.</span><span class="sxs-lookup"><span data-stu-id="f2a23-133">In the search box, type **Bime**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bime-tutorial/tutorial_bime_search.png)

5. <span data-ttu-id="f2a23-135">W panelu wyników wybierz **Bime**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="f2a23-135">In the results panel, select **Bime**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bime-tutorial/tutorial_bime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f2a23-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f2a23-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f2a23-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Bime w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="f2a23-138">In this section, you configure and test Azure AD single sign-on with Bime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f2a23-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Bime jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f2a23-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bime is to a user in Azure AD.</span></span> <span data-ttu-id="f2a23-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Bime musi się.</span><span class="sxs-lookup"><span data-stu-id="f2a23-140">In other words, a link relationship between an Azure AD user and the related user in Bime needs to be established.</span></span>

<span data-ttu-id="f2a23-141">W Bime, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="f2a23-141">In Bime, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f2a23-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Bime, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="f2a23-142">To configure and test Azure AD single sign-on with Bime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f2a23-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="f2a23-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f2a23-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f2a23-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f2a23-145">**[Tworzenie użytkownika testowego Bime](#creating-a-bime-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Bime połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f2a23-145">**[Creating a Bime test user](#creating-a-bime-test-user)** - to have a counterpart of Britta Simon in Bime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f2a23-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f2a23-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f2a23-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="f2a23-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f2a23-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f2a23-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f2a23-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Bime.</span><span class="sxs-lookup"><span data-stu-id="f2a23-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bime application.</span></span>

<span data-ttu-id="f2a23-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Bime, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f2a23-150">**To configure Azure AD single sign-on with Bime, perform the following steps:**</span></span>

1. <span data-ttu-id="f2a23-151">W portalu Azure na **Bime** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="f2a23-151">In the Azure portal, on the **Bime** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="f2a23-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="f2a23-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bime-tutorial/tutorial_bime_samlbase.png)

3. <span data-ttu-id="f2a23-155">Na **Bime domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f2a23-155">On the **Bime Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bime-tutorial/tutorial_bime_url.png)

    <span data-ttu-id="f2a23-157">a.</span><span class="sxs-lookup"><span data-stu-id="f2a23-157">a.</span></span> <span data-ttu-id="f2a23-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="f2a23-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    <span data-ttu-id="f2a23-159">b.</span><span class="sxs-lookup"><span data-stu-id="f2a23-159">b.</span></span> <span data-ttu-id="f2a23-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="f2a23-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f2a23-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="f2a23-161">These values are not real.</span></span> <span data-ttu-id="f2a23-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="f2a23-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f2a23-163">Skontaktuj się z [zespołem pomocy technicznej klienta Bime](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="f2a23-163">Contact [Bime Client support team](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) to get these values.</span></span> 
 
4. <span data-ttu-id="f2a23-164">Na **certyfikat podpisywania SAML** sekcji, skopiuj **odcisk PALCA** wartości z certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="f2a23-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bime-tutorial/tutorial_bime_certificate.png) 

5. <span data-ttu-id="f2a23-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f2a23-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f2a23-168">Na **konfiguracji Bime** , kliknij przycisk **skonfigurować Bime** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="f2a23-168">On the **Bime Configuration** section, click **Configure Bime** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f2a23-169">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="f2a23-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bime-tutorial/tutorial_bime_configure.png) 

7. <span data-ttu-id="f2a23-171">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Bime jako administrator.</span><span class="sxs-lookup"><span data-stu-id="f2a23-171">In a different web browser window, log into your Bime company site as an administrator.</span></span>

8. <span data-ttu-id="f2a23-172">Na pasku narzędzi, kliknij przycisk **Admin**, a następnie **konta**.</span><span class="sxs-lookup"><span data-stu-id="f2a23-172">In the toolbar, click **Admin**, and then **Account**.</span></span>
   
    <span data-ttu-id="f2a23-173">![Administrator](./media/active-directory-saas-bime-tutorial/ic775558.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="f2a23-173">![Admin](./media/active-directory-saas-bime-tutorial/ic775558.png "Admin")</span></span>

9. <span data-ttu-id="f2a23-174">Na stronie konfiguracji konta wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f2a23-174">On the account configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="f2a23-175">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bime-tutorial/ic775559.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="f2a23-175">![Configure Single Sign-On](./media/active-directory-saas-bime-tutorial/ic775559.png "Configure Single Sign-On")</span></span>
   
    <span data-ttu-id="f2a23-176">a.</span><span class="sxs-lookup"><span data-stu-id="f2a23-176">a.</span></span> <span data-ttu-id="f2a23-177">Wybierz **uwierzytelnianie Włącz SAML**.</span><span class="sxs-lookup"><span data-stu-id="f2a23-177">Select **Enable SAML authentication**.</span></span>

    <span data-ttu-id="f2a23-178">b.</span><span class="sxs-lookup"><span data-stu-id="f2a23-178">b.</span></span> <span data-ttu-id="f2a23-179">W **zdalnego adresu URL logowania** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f2a23-179">In the **Remote Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="f2a23-180">c.</span><span class="sxs-lookup"><span data-stu-id="f2a23-180">c.</span></span>  <span data-ttu-id="f2a23-181">Wklej **odcisk palca** wartość z portalu Azure do **odcisk palca certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="f2a23-181">Paste the **Thumbprint** value from Azure portal into the **Certificate Fingerprint** textbox.</span></span>       
   
    <span data-ttu-id="f2a23-182">d.</span><span class="sxs-lookup"><span data-stu-id="f2a23-182">d.</span></span> <span data-ttu-id="f2a23-183">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="f2a23-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="f2a23-184">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="f2a23-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f2a23-185">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="f2a23-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f2a23-186">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f2a23-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f2a23-187">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f2a23-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="f2a23-188">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f2a23-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="f2a23-190">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f2a23-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f2a23-191">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f2a23-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f2a23-193">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="f2a23-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f2a23-195">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f2a23-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f2a23-197">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f2a23-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f2a23-199">a.</span><span class="sxs-lookup"><span data-stu-id="f2a23-199">a.</span></span> <span data-ttu-id="f2a23-200">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f2a23-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f2a23-201">b.</span><span class="sxs-lookup"><span data-stu-id="f2a23-201">b.</span></span> <span data-ttu-id="f2a23-202">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f2a23-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f2a23-203">c.</span><span class="sxs-lookup"><span data-stu-id="f2a23-203">c.</span></span> <span data-ttu-id="f2a23-204">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="f2a23-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f2a23-205">d.</span><span class="sxs-lookup"><span data-stu-id="f2a23-205">d.</span></span> <span data-ttu-id="f2a23-206">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f2a23-206">Click **Create**.</span></span>
 
### <a name="creating-a-bime-test-user"></a><span data-ttu-id="f2a23-207">Tworzenie użytkownika testowego Bime</span><span class="sxs-lookup"><span data-stu-id="f2a23-207">Creating a Bime test user</span></span>

<span data-ttu-id="f2a23-208">Aby umożliwić użytkownikom zalogować się do Bime usługi Azure AD, musi być przygotowana do Bime.</span><span class="sxs-lookup"><span data-stu-id="f2a23-208">In order to enable Azure AD users to log in to Bime, they must be provisioned into Bime.</span></span> <span data-ttu-id="f2a23-209">W przypadku Bime Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="f2a23-209">In the case of Bime, provisioning is a manual task.</span></span>

<span data-ttu-id="f2a23-210">**Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f2a23-210">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="f2a23-211">Zaloguj się do Twojego **Bime** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="f2a23-211">Log in to your **Bime** tenant.</span></span>

2. <span data-ttu-id="f2a23-212">Na pasku narzędzi, kliknij przycisk **Admin**, a następnie **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="f2a23-212">In the toolbar, click **Admin**, and then **Users**.</span></span>
   
    <span data-ttu-id="f2a23-213">![Administrator](./media/active-directory-saas-bime-tutorial/ic775561.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="f2a23-213">![Admin](./media/active-directory-saas-bime-tutorial/ic775561.png "Admin")</span></span>

3. <span data-ttu-id="f2a23-214">W **listy użytkowników**, kliknij przycisk **Dodaj nowego użytkownika** ("+").</span><span class="sxs-lookup"><span data-stu-id="f2a23-214">In the **Users List**, click **Add New User** (“+”).</span></span>
   
    <span data-ttu-id="f2a23-215">![Użytkownicy](./media/active-directory-saas-bime-tutorial/ic775562.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="f2a23-215">![Users](./media/active-directory-saas-bime-tutorial/ic775562.png "Users")</span></span>

4. <span data-ttu-id="f2a23-216">Na **szczegóły użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f2a23-216">On the **User Details** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="f2a23-217">![Szczegóły użytkownika](./media/active-directory-saas-bime-tutorial/ic775563.png "szczegóły użytkownika")</span><span class="sxs-lookup"><span data-stu-id="f2a23-217">![User Details](./media/active-directory-saas-bime-tutorial/ic775563.png "User Details")</span></span>
   
    <span data-ttu-id="f2a23-218">a.</span><span class="sxs-lookup"><span data-stu-id="f2a23-218">a.</span></span> <span data-ttu-id="f2a23-219">W **imię** pole tekstowe, wprowadź imię użytkownika, takich jak **Britta**.</span><span class="sxs-lookup"><span data-stu-id="f2a23-219">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="f2a23-220">b.</span><span class="sxs-lookup"><span data-stu-id="f2a23-220">b.</span></span> <span data-ttu-id="f2a23-221">W **nazwisko** pole tekstowe, wprowadź nazwisko użytkownika, takich jak **Simona**.</span><span class="sxs-lookup"><span data-stu-id="f2a23-221">In the **Last name** textbox, enter the last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="f2a23-222">c.</span><span class="sxs-lookup"><span data-stu-id="f2a23-222">c.</span></span> <span data-ttu-id="f2a23-223">W **E-mail** pole tekstowe, wprowadź adres e-mail użytkownika, takich jak  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="f2a23-223">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="f2a23-224">d.</span><span class="sxs-lookup"><span data-stu-id="f2a23-224">d.</span></span> <span data-ttu-id="f2a23-225">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="f2a23-225">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="f2a23-226">Możesz użyć innych Bime użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Bime do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="f2a23-226">You can use any other Bime user account creation tools or APIs provided by Bime to provision AAD user accounts.</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f2a23-227">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f2a23-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f2a23-228">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Bime.</span><span class="sxs-lookup"><span data-stu-id="f2a23-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bime.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="f2a23-230">**Aby przypisać Simona Britta Bime, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="f2a23-230">**To assign Britta Simon to Bime, perform the following steps:**</span></span>

1. <span data-ttu-id="f2a23-231">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f2a23-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="f2a23-233">Na liście aplikacji zaznacz **Bime**.</span><span class="sxs-lookup"><span data-stu-id="f2a23-233">In the applications list, select **Bime**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bime-tutorial/tutorial_bime_app.png) 

3. <span data-ttu-id="f2a23-235">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="f2a23-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="f2a23-237">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f2a23-237">Click **Add** button.</span></span> <span data-ttu-id="f2a23-238">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f2a23-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="f2a23-240">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="f2a23-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f2a23-241">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f2a23-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f2a23-242">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f2a23-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f2a23-243">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f2a23-243">Testing single sign-on</span></span>

<span data-ttu-id="f2a23-244">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="f2a23-244">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f2a23-245">Po kliknięciu kafelka Bime w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Bime.</span><span class="sxs-lookup"><span data-stu-id="f2a23-245">When you click the Bime tile in the Access Panel, you should get automatically signed-on to your Bime application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f2a23-246">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="f2a23-246">Additional resources</span></span>

* [<span data-ttu-id="f2a23-247">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f2a23-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f2a23-248">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f2a23-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bime-tutorial/tutorial_general_203.png

