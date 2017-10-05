---
title: "Samouczek: Integracji Azure Active Directory z usługi New Relic | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i usługi New Relic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3186b9a8-f4d8-45e2-ad82-6275f95e7aa6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 605e85c23a849f70fcc0237361d7a891f716ca3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-new-relic"></a><span data-ttu-id="d4d0d-103">Samouczek: Integracji Azure Active Directory z usługi New Relic</span><span class="sxs-lookup"><span data-stu-id="d4d0d-103">Tutorial: Azure Active Directory integration with New Relic</span></span>

<span data-ttu-id="d4d0d-104">Z tego samouczka dowiesz się Integrowanie usługi New Relic w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d4d0d-104">In this tutorial, you learn how to integrate New Relic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d4d0d-105">Integrowanie usługi New Relic z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d4d0d-105">Integrating New Relic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d4d0d-106">Można kontrolować w usłudze Azure AD, który ma dostęp do usługi New Relic</span><span class="sxs-lookup"><span data-stu-id="d4d0d-106">You can control in Azure AD who has access to New Relic</span></span>
- <span data-ttu-id="d4d0d-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do usługi New Relic (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4d0d-107">You can enable your users to automatically get signed-on to New Relic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d4d0d-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d4d0d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d4d0d-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d4d0d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4d0d-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d4d0d-110">Prerequisites</span></span>

<span data-ttu-id="d4d0d-111">Aby skonfigurować integrację usługi Azure AD z usługi New Relic, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d4d0d-111">To configure Azure AD integration with New Relic, you need the following items:</span></span>

- <span data-ttu-id="d4d0d-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4d0d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d4d0d-113">Usługi New Relic logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d4d0d-113">A New Relic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d4d0d-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d4d0d-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d4d0d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d4d0d-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d4d0d-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d4d0d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d4d0d-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d4d0d-118">Scenario description</span></span>
<span data-ttu-id="d4d0d-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d4d0d-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d4d0d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d4d0d-121">Dodawanie usługi New Relic w galerii</span><span class="sxs-lookup"><span data-stu-id="d4d0d-121">Adding New Relic from the gallery</span></span>
2. <span data-ttu-id="d4d0d-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d4d0d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-new-relic-from-the-gallery"></a><span data-ttu-id="d4d0d-123">Dodawanie usługi New Relic w galerii</span><span class="sxs-lookup"><span data-stu-id="d4d0d-123">Adding New Relic from the gallery</span></span>
<span data-ttu-id="d4d0d-124">Aby skonfigurować integrację usługi New Relic w usłudze Azure Active Directory, należy dodać usługi New Relic w galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-124">To configure the integration of New Relic into Azure AD, you need to add New Relic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d4d0d-125">**Aby dodać usługi New Relic w galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d4d0d-125">**To add New Relic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d4d0d-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="d4d0d-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d4d0d-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="d4d0d-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="d4d0d-133">W polu wyszukiwania wpisz **usługi New Relic**.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-133">In the search box, type **New Relic**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_search.png)

5. <span data-ttu-id="d4d0d-135">W panelu wyników wybierz **usługi New Relic**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-135">In the results panel, select **New Relic**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d4d0d-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d4d0d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d4d0d-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługi New Relic w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-138">In this section, you configure and test Azure AD single sign-on with New Relic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d4d0d-139">Do rejestracji jednokrotnej do pracy usługi Azure AD musi ustalić użytkownika odpowiednika w usługi New Relic dla użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in New Relic is to a user in Azure AD.</span></span> <span data-ttu-id="d4d0d-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w usługi New Relic.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-140">In other words, a link relationship between an Azure AD user and the related user in New Relic needs to be established.</span></span>

<span data-ttu-id="d4d0d-141">Usługi New Relic, przypisywanie wartości **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-141">In New Relic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d4d0d-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługi New Relic, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="d4d0d-142">To configure and test Azure AD single sign-on with New Relic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d4d0d-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d4d0d-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d4d0d-145">**[Tworzenie użytkownika testowego usługi New Relic](#creating-a-new-relic-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta usługi New Relic jest połączony z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-145">**[Creating a New Relic test user](#creating-a-new-relic-test-user)** - to have a counterpart of Britta Simon in New Relic that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d4d0d-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d4d0d-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d4d0d-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d4d0d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d4d0d-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne do aplikacji usługi New Relic.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your New Relic application.</span></span>

<span data-ttu-id="d4d0d-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z usługi New Relic, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d4d0d-150">**To configure Azure AD single sign-on with New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="d4d0d-151">W portalu Azure na **usługi New Relic** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-151">In the Azure portal, on the **New Relic** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="d4d0d-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_samlbase.png)

3. <span data-ttu-id="d4d0d-155">Na **adresy URL i nowej domeny Relic** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d4d0d-155">On the **New Relic Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_url.png)

    <span data-ttu-id="d4d0d-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.newrelic.com`</span><span class="sxs-lookup"><span data-stu-id="d4d0d-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.newrelic.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d4d0d-158">Wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-158">The value is not real.</span></span> <span data-ttu-id="d4d0d-159">Zaktualizuj tę wartość z adresem URL logowania rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="d4d0d-160">Skontaktuj się z [zespołem pomocy technicznej nowego klienta Relic](https://support.newrelic.com/) można uzyskać wartość.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-160">Contact [New Relic Client support team](https://support.newrelic.com/) to get the value.</span></span> 
 
4. <span data-ttu-id="d4d0d-161">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_certificate.png) 

5. <span data-ttu-id="d4d0d-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-new-relic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d4d0d-165">Na **nowej konfiguracji Relic** kliknij **skonfigurować usługi New Relic** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-165">On the **New Relic Configuration** section, click **Configure New Relic** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d4d0d-166">Kopiuj **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="d4d0d-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_configure.png) 

7. <span data-ttu-id="d4d0d-168">W oknie przeglądarki innej witryny sieci web, zaloguj się na Twojej **usługi New Relic** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-168">In a different web browser window, sign on to your **New Relic** company site as administrator.</span></span>

8. <span data-ttu-id="d4d0d-169">W menu u góry kliknij **ustawienia konta**.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-169">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="d4d0d-170">![Ustawienia konta](./media/active-directory-saas-new-relic-tutorial/ic797036.png "ustawienia konta")</span><span class="sxs-lookup"><span data-stu-id="d4d0d-170">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Account Settings")</span></span>

9. <span data-ttu-id="d4d0d-171">Kliknij przycisk **zabezpieczeń i uwierzytelniania** , a następnie kliknij pozycję **jednokrotne** kartę.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-171">Click the **Security and authentication** tab, and then click the **Single sign on** tab.</span></span>
   
    <span data-ttu-id="d4d0d-172">![Logowanie jednokrotne](./media/active-directory-saas-new-relic-tutorial/ic797037.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="d4d0d-172">![Single Sign-On](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Single Sign-On")</span></span>

10. <span data-ttu-id="d4d0d-173">Na stronie okna dialogowego SAML wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d4d0d-173">On the SAML dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="d4d0d-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="d4d0d-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span></span>
   
   <span data-ttu-id="d4d0d-175">a.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-175">a.</span></span> <span data-ttu-id="d4d0d-176">Kliknij przycisk **wybierz plik** przekazać pobrany certyfikat usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-176">Click **Choose File** to upload your downloaded Azure Active Directory certificate.</span></span>

   <span data-ttu-id="d4d0d-177">b.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-177">b.</span></span> <span data-ttu-id="d4d0d-178">W **adres URL logowania zdalnego** pole tekstowe, Wklej wartość **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-178">In the **Remote login URL** textbox,  paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="d4d0d-179">c.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-179">c.</span></span> <span data-ttu-id="d4d0d-180">W **lądowanie adresu URL wylogowania** pole tekstowe, Wklej wartość **Sign-Out adres URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-180">In the **Logout landing URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

   <span data-ttu-id="d4d0d-181">d.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-181">d.</span></span> <span data-ttu-id="d4d0d-182">Kliknij przycisk **Zapisz moje zmiany**.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-182">Click **Save my changes**.</span></span>

> [!TIP]
> <span data-ttu-id="d4d0d-183">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="d4d0d-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d4d0d-184">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d4d0d-185">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d4d0d-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d4d0d-186">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4d0d-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="d4d0d-187">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="d4d0d-189">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d4d0d-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d4d0d-190">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d4d0d-192">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d4d0d-194">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d4d0d-196">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d4d0d-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d4d0d-198">a.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-198">a.</span></span> <span data-ttu-id="d4d0d-199">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d4d0d-200">b.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-200">b.</span></span> <span data-ttu-id="d4d0d-201">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d4d0d-202">c.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-202">c.</span></span> <span data-ttu-id="d4d0d-203">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d4d0d-204">d.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-204">d.</span></span> <span data-ttu-id="d4d0d-205">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-205">Click **Create**.</span></span>
 
### <a name="creating-a-new-relic-test-user"></a><span data-ttu-id="d4d0d-206">Tworzenie użytkownika testowego usługi New Relic</span><span class="sxs-lookup"><span data-stu-id="d4d0d-206">Creating a New Relic test user</span></span>

<span data-ttu-id="d4d0d-207">Aby włączyć usługi Azure Active Directory użytkownikom na logowanie się do usługi New Relic, musi być przygotowana do usługi New Relic.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-207">In order to enable Azure Active Directory users to log in to New Relic, they must be provisioned into New Relic.</span></span> <span data-ttu-id="d4d0d-208">W przypadku usługi New Relic Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-208">In the case of New Relic, provisioning is a manual task.</span></span>

<span data-ttu-id="d4d0d-209">**Aby udostępnić konta użytkownika do usługi New Relic, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d4d0d-209">**To provision a user account to New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="d4d0d-210">Zaloguj się do Twojego **usługi New Relic** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-210">Log in to your **New Relic** company site as administrator.</span></span>

2. <span data-ttu-id="d4d0d-211">W menu u góry kliknij **ustawienia konta**.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-211">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="d4d0d-212">![Ustawienia konta](./media/active-directory-saas-new-relic-tutorial/ic797040.png "ustawienia konta")</span><span class="sxs-lookup"><span data-stu-id="d4d0d-212">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Account Settings")</span></span>

3. <span data-ttu-id="d4d0d-213">W **konta** w okienku po lewej stronie kliknij **Podsumowanie**, a następnie kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-213">In the **Account** pane on the left side, click **Summary**, and then click **Add user**.</span></span>
   
    <span data-ttu-id="d4d0d-214">![Ustawienia konta](./media/active-directory-saas-new-relic-tutorial/ic797041.png "ustawienia konta")</span><span class="sxs-lookup"><span data-stu-id="d4d0d-214">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Account Settings")</span></span>

4. <span data-ttu-id="d4d0d-215">Na **aktywni użytkownicy** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d4d0d-215">On the **Active users** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="d4d0d-216">![Aktywni użytkownicy](./media/active-directory-saas-new-relic-tutorial/ic797042.png "aktywni użytkownicy")</span><span class="sxs-lookup"><span data-stu-id="d4d0d-216">![Active Users](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Active Users")</span></span>
   
    <span data-ttu-id="d4d0d-217">a.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-217">a.</span></span> <span data-ttu-id="d4d0d-218">W **E-mail** tekstowym, wpisz adres e-mail chcesz udostępnić prawidłowym użytkownikiem usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-218">In the **Email** textbox, type the email address of a valid Azure Active Directory user you want to provision.</span></span>

    <span data-ttu-id="d4d0d-219">b.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-219">b.</span></span> <span data-ttu-id="d4d0d-220">Jako **roli** wybierz **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-220">As **Role** select **User**.</span></span>

    <span data-ttu-id="d4d0d-221">c.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-221">c.</span></span> <span data-ttu-id="d4d0d-222">Kliknij przycisk **Dodaj tego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-222">Click **Add this user**.</span></span>

>[!NOTE]
><span data-ttu-id="d4d0d-223">Można użyć dowolnego inne usługi New Relic użytkownika konta narzędzia do tworzenia lub interfejsów API dostarczonych przez usługi New Relic do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-223">You can use any other New Relic user account creation tools or APIs provided by New Relic to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d4d0d-224">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4d0d-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d4d0d-225">W tej sekcji musisz włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udzielanie dostępu do usługi New Relic.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to New Relic.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="d4d0d-227">**Aby przypisać Simona Britta do usługi New Relic, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d4d0d-227">**To assign Britta Simon to New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="d4d0d-228">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d4d0d-230">Na liście aplikacji zaznacz **usługi New Relic**.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-230">In the applications list, select **New Relic**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_app.png) 

3. <span data-ttu-id="d4d0d-232">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="d4d0d-234">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-234">Click **Add** button.</span></span> <span data-ttu-id="d4d0d-235">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="d4d0d-237">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d4d0d-238">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d4d0d-239">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d4d0d-240">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d4d0d-240">Testing single sign-on</span></span>

<span data-ttu-id="d4d0d-241">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-241">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d4d0d-242">Po kliknięciu kafelka usługi New Relic w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji usługi New Relic.</span><span class="sxs-lookup"><span data-stu-id="d4d0d-242">When you click the New Relic tile in the Access Panel, you should get automatically signed-on to your New Relic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d4d0d-243">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d4d0d-243">Additional resources</span></span>

* [<span data-ttu-id="d4d0d-244">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d4d0d-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d4d0d-245">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d4d0d-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_203.png

