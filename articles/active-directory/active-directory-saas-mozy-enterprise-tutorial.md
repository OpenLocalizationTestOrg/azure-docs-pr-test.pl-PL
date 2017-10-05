---
title: "Samouczek: Integrację usługi Azure Active Directory ze Mozy | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Mozy Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: ac73aadcb8205f24f9d2dbce5af76f53bbcb9753
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a><span data-ttu-id="8f603-103">Samouczek: Integrację usługi Azure Active Directory ze Mozy</span><span class="sxs-lookup"><span data-stu-id="8f603-103">Tutorial: Azure Active Directory integration with Mozy Enterprise</span></span>

<span data-ttu-id="8f603-104">Z tego samouczka dowiesz się integrowanie Mozy przedsiębiorstwa w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8f603-104">In this tutorial, you learn how to integrate Mozy Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8f603-105">Integrowanie Mozy organizacji z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="8f603-105">Integrating Mozy Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8f603-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Mozy przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="8f603-106">You can control in Azure AD who has access to Mozy Enterprise</span></span>
- <span data-ttu-id="8f603-107">Umożliwia użytkownikom automatycznie pobrać zalogowane Mozy przedsiębiorstwem (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f603-107">You can enable your users to automatically get signed-on to Mozy Enterprise (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8f603-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8f603-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8f603-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8f603-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f603-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8f603-110">Prerequisites</span></span>

<span data-ttu-id="8f603-111">Aby skonfigurować integrację usługi Azure AD z Mozy przedsiębiorstwa, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8f603-111">To configure Azure AD integration with Mozy Enterprise, you need the following items:</span></span>

- <span data-ttu-id="8f603-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f603-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8f603-113">Mozy Enterprise logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8f603-113">A Mozy Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8f603-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="8f603-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8f603-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="8f603-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8f603-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="8f603-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8f603-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8f603-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8f603-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="8f603-118">Scenario description</span></span>
<span data-ttu-id="8f603-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="8f603-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8f603-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="8f603-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8f603-121">Dodawanie Mozy przedsiębiorstwa z galerii</span><span class="sxs-lookup"><span data-stu-id="8f603-121">Adding Mozy Enterprise from the gallery</span></span>
2. <span data-ttu-id="8f603-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8f603-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mozy-enterprise-from-the-gallery"></a><span data-ttu-id="8f603-123">Dodawanie Mozy przedsiębiorstwa z galerii</span><span class="sxs-lookup"><span data-stu-id="8f603-123">Adding Mozy Enterprise from the gallery</span></span>
<span data-ttu-id="8f603-124">Aby skonfigurować integrację usługi Azure AD Mozy przedsiębiorstwa, należy dodać Mozy przedsiębiorstwa z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="8f603-124">To configure the integration of Mozy Enterprise into Azure AD, you need to add Mozy Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8f603-125">**Aby dodać Mozy przedsiębiorstwa z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8f603-125">**To add Mozy Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8f603-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8f603-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="8f603-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="8f603-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8f603-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8f603-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="8f603-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8f603-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="8f603-133">W polu wyszukiwania wpisz **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="8f603-133">In the search box, type **Mozy Enterprise**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_search.png)

5. <span data-ttu-id="8f603-135">W panelu wyników wybierz **Mozy Enterprise**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="8f603-135">In the results panel, select **Mozy Enterprise**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8f603-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8f603-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8f603-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z Mozy przedsiębiorstwa w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="8f603-138">In this section, you configure and test Azure AD single sign-on with Mozy Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8f603-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w przedsiębiorstwie Mozy jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f603-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mozy Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="8f603-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w przedsiębiorstwie Mozy musi się.</span><span class="sxs-lookup"><span data-stu-id="8f603-140">In other words, a link relationship between an Azure AD user and the related user in Mozy Enterprise needs to be established.</span></span>

<span data-ttu-id="8f603-141">W przedsiębiorstwie Mozy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="8f603-141">In Mozy Enterprise, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8f603-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Mozy przedsiębiorstwa, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="8f603-142">To configure and test Azure AD single sign-on with Mozy Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8f603-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="8f603-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8f603-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8f603-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8f603-145">**[Tworzenie użytkownika testowego Mozy Enterprise](#creating-a-mozy-enterprise-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Mozy przedsiębiorstwo, które jest połączone z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8f603-145">**[Creating a Mozy Enterprise test user](#creating-a-mozy-enterprise-test-user)** - to have a counterpart of Britta Simon in Mozy Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8f603-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8f603-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8f603-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="8f603-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8f603-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8f603-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8f603-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji przedsiębiorstwa Mozy.</span><span class="sxs-lookup"><span data-stu-id="8f603-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mozy Enterprise application.</span></span>

<span data-ttu-id="8f603-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Mozy przedsiębiorstwa, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8f603-150">**To configure Azure AD single sign-on with Mozy Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="8f603-151">W portalu Azure na **Mozy Enterprise** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="8f603-151">In the Azure portal, on the **Mozy Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="8f603-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="8f603-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_samlbase.png)

3. <span data-ttu-id="8f603-155">Na **Mozy domeny przedsiębiorstwa i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8f603-155">On the **Mozy Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_url.png)

    <span data-ttu-id="8f603-157">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<tenantname>.Mozyenterprise.com`</span><span class="sxs-lookup"><span data-stu-id="8f603-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.Mozyenterprise.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8f603-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="8f603-158">This value is not real.</span></span> <span data-ttu-id="8f603-159">Zaktualizuj tę wartość przy rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="8f603-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="8f603-160">Skontaktuj się z [zespołem pomocy technicznej klienta Enterprise Mozy](http://support.mozy.com/) aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="8f603-160">Contact [Mozy Enterprise Client support team](http://support.mozy.com/) to get this value.</span></span>

4. <span data-ttu-id="8f603-161">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="8f603-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_certificate.png) 

5. <span data-ttu-id="8f603-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8f603-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8f603-165">Na **konfiguracja dla przedsiębiorstw Mozy** , kliknij przycisk **skonfigurować Mozy Enterprise** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="8f603-165">On the **Mozy Enterprise Configuration** section, click **Configure Mozy Enterprise** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8f603-166">Kopiuj **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="8f603-166">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_configure.png) 

7. <span data-ttu-id="8f603-168">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Mozy Enterprise jako administrator.</span><span class="sxs-lookup"><span data-stu-id="8f603-168">In a different web browser window, log into your Mozy Enterprise company site as an administrator.</span></span>

8. <span data-ttu-id="8f603-169">W **konfiguracji** kliknij **zasady uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="8f603-169">In the **Configuration** section, click **Authentication Policy**.</span></span>
   
   <span data-ttu-id="8f603-170">![Zasady uwierzytelniania](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "zasady uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="8f603-170">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Authentication policy")</span></span>

9. <span data-ttu-id="8f603-171">Na **zasady uwierzytelniania** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8f603-171">On the **Authentication Policy** section, perform the following steps:</span></span>
   
   <span data-ttu-id="8f603-172">![Zasady uwierzytelniania](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "zasady uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="8f603-172">![Authentication policy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Authentication policy")</span></span>
   
   <span data-ttu-id="8f603-173">a.</span><span class="sxs-lookup"><span data-stu-id="8f603-173">a.</span></span> <span data-ttu-id="8f603-174">Wybierz **usługi katalogowej** jako **dostawcy**.</span><span class="sxs-lookup"><span data-stu-id="8f603-174">Select **Directory Service** as **Provider**.</span></span>
   
   <span data-ttu-id="8f603-175">b.</span><span class="sxs-lookup"><span data-stu-id="8f603-175">b.</span></span> <span data-ttu-id="8f603-176">Wybierz **wypychania LDAP**.</span><span class="sxs-lookup"><span data-stu-id="8f603-176">Select **Use LDAP Push**.</span></span>
   
   <span data-ttu-id="8f603-177">c.</span><span class="sxs-lookup"><span data-stu-id="8f603-177">c.</span></span> <span data-ttu-id="8f603-178">Kliknij przycisk **uwierzytelnianie SAML** kartę.</span><span class="sxs-lookup"><span data-stu-id="8f603-178">Click the **SAML Authentication** tab.</span></span>
   
   <span data-ttu-id="8f603-179">d.</span><span class="sxs-lookup"><span data-stu-id="8f603-179">d.</span></span> <span data-ttu-id="8f603-180">Wklej **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure do **adres URL uwierzytelniania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8f603-180">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Authentication URL** textbox.</span></span>
   
   <span data-ttu-id="8f603-181">e.</span><span class="sxs-lookup"><span data-stu-id="8f603-181">e.</span></span> <span data-ttu-id="8f603-182">Wklej **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure do **SAML punktu końcowego** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8f603-182">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **SAML Endpoint** textbox.</span></span>
   
   <span data-ttu-id="8f603-183">f.</span><span class="sxs-lookup"><span data-stu-id="8f603-183">f.</span></span> <span data-ttu-id="8f603-184">Otwórz w Notatniku pobrany zakodowanego certyfikatu base-64, skopiuj zawartość go do Schowka, a następnie wklej cały certyfikat do **certyfikatu SAML** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8f603-184">Open your downloaded base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **SAML Certificate** textbox.</span></span>
   
   <span data-ttu-id="8f603-185">g.</span><span class="sxs-lookup"><span data-stu-id="8f603-185">g.</span></span> <span data-ttu-id="8f603-186">Wybierz **włączenia logowania jednokrotnego dla administratorów zalogować się przy użyciu swoich poświadczeń sieciowych**.</span><span class="sxs-lookup"><span data-stu-id="8f603-186">Select **Enable SSO for Admins to log in with their network credentials**.</span></span>
   
   <span data-ttu-id="8f603-187">h.</span><span class="sxs-lookup"><span data-stu-id="8f603-187">h.</span></span> <span data-ttu-id="8f603-188">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="8f603-188">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="8f603-189">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="8f603-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8f603-190">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="8f603-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8f603-191">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8f603-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8f603-192">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f603-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="8f603-193">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8f603-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="8f603-195">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8f603-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8f603-196">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8f603-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8f603-198">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="8f603-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8f603-200">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8f603-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8f603-202">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8f603-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8f603-204">a.</span><span class="sxs-lookup"><span data-stu-id="8f603-204">a.</span></span> <span data-ttu-id="8f603-205">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8f603-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8f603-206">b.</span><span class="sxs-lookup"><span data-stu-id="8f603-206">b.</span></span> <span data-ttu-id="8f603-207">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8f603-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8f603-208">c.</span><span class="sxs-lookup"><span data-stu-id="8f603-208">c.</span></span> <span data-ttu-id="8f603-209">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="8f603-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8f603-210">d.</span><span class="sxs-lookup"><span data-stu-id="8f603-210">d.</span></span> <span data-ttu-id="8f603-211">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8f603-211">Click **Create**.</span></span>
 
### <a name="creating-a-mozy-enterprise-test-user"></a><span data-ttu-id="8f603-212">Tworzenie użytkownika testowego Mozy przedsiębiorstwa</span><span class="sxs-lookup"><span data-stu-id="8f603-212">Creating a Mozy Enterprise test user</span></span>

<span data-ttu-id="8f603-213">Aby włączyć logowanie w przedsiębiorstwie Mozy użytkowników usługi Azure AD, muszą mieć przydzielone Mozy w przedsiębiorstwie.</span><span class="sxs-lookup"><span data-stu-id="8f603-213">In order to enable Azure AD users to log into Mozy Enterprise, they must be provisioned into Mozy Enterprise.</span></span> <span data-ttu-id="8f603-214">W przypadku Mozy przedsiębiorstwa Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="8f603-214">In the case of Mozy Enterprise, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="8f603-215">Możesz użyć innych Mozy Enterprise użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Mozy przedsiębiorstwa do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="8f603-215">You can use any other Mozy Enterprise user account creation tools or APIs provided by Mozy Enterprise to provision AAD user accounts.</span></span>

<span data-ttu-id="8f603-216">**Aby udostępnić konta użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8f603-216">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="8f603-217">Zaloguj się do Twojego **Mozy Enterprise** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="8f603-217">Log in to your **Mozy Enterprise** tenant.</span></span>

2. <span data-ttu-id="8f603-218">Kliknij przycisk **użytkowników**, a następnie kliknij przycisk **Dodaj nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="8f603-218">Click **Users**, and then click **Add New User**.</span></span>
   
   <span data-ttu-id="8f603-219">![Użytkownicy](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="8f603-219">![Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Users")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="8f603-220">**Dodaj nowego użytkownika** tylko wtedy, gdy tylko jest wyświetlana opcja **Mozy** został wybrany jako dostawcy pod **zasady uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="8f603-220">The **Add New User** option is only displayed only if **Mozy** is selected as the provider under **Authentication policy**.</span></span> <span data-ttu-id="8f603-221">Jeśli skonfigurowano uwierzytelnianie SAML, następnie użytkownicy są automatycznie dodawane na ich pierwsze logowanie za pomocą rejestracji jednokrotnej w.</span><span class="sxs-lookup"><span data-stu-id="8f603-221">If SAML Authentication is configured, then the users are added automatically on their first login through Single sign on.</span></span>
    
3. <span data-ttu-id="8f603-222">W oknie dialogowym Nowy użytkownik, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8f603-222">On the new user dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="8f603-223">![Dodawanie użytkowników](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Dodawanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="8f603-223">![Add Users](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "Add Users")</span></span>
   
   <span data-ttu-id="8f603-224">a.</span><span class="sxs-lookup"><span data-stu-id="8f603-224">a.</span></span> <span data-ttu-id="8f603-225">Z **wybierz grupę** listy, wybierz grupę.</span><span class="sxs-lookup"><span data-stu-id="8f603-225">From the **Choose a Group** list, select a group.</span></span>
   
   <span data-ttu-id="8f603-226">b.</span><span class="sxs-lookup"><span data-stu-id="8f603-226">b.</span></span> <span data-ttu-id="8f603-227">Z **jakiego rodzaju użytkownika** listy, wybierz typ.</span><span class="sxs-lookup"><span data-stu-id="8f603-227">From the **What type of user** list, select a type.</span></span>
   
   <span data-ttu-id="8f603-228">c.</span><span class="sxs-lookup"><span data-stu-id="8f603-228">c.</span></span> <span data-ttu-id="8f603-229">W **Username** tekstowym, wpisz nazwę użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f603-229">In the **Username** textbox, type the name of the Azure AD user.</span></span>
   
   <span data-ttu-id="8f603-230">d.</span><span class="sxs-lookup"><span data-stu-id="8f603-230">d.</span></span> <span data-ttu-id="8f603-231">W **E-mail** tekstowym, wpisz adres e-mail użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f603-231">In the **Email** textbox, type the email address of the Azure AD user.</span></span>
   
   <span data-ttu-id="8f603-232">e.</span><span class="sxs-lookup"><span data-stu-id="8f603-232">e.</span></span> <span data-ttu-id="8f603-233">Wybierz **wysyłania wiadomości e-mail z instrukcją użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="8f603-233">Select **Send user instruction email**.</span></span>
   
   <span data-ttu-id="8f603-234">f.</span><span class="sxs-lookup"><span data-stu-id="8f603-234">f.</span></span> <span data-ttu-id="8f603-235">Kliknij przycisk **dodać użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="8f603-235">Click **Add User(s)**.</span></span>

     >[!NOTE]
     > <span data-ttu-id="8f603-236">Po utworzeniu użytkownika, zostanie wysłana wiadomość e-mail do użytkownika usługi Azure AD, która zawiera link do potwierdzenia konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="8f603-236">After creating the user, an email will be sent to the Azure AD user that includes a link to confirm the account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8f603-237">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f603-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8f603-238">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do Mozy przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="8f603-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mozy Enterprise.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="8f603-240">**Aby przypisać Simona Britta Mozy przedsiębiorstwa, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8f603-240">**To assign Britta Simon to Mozy Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="8f603-241">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8f603-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="8f603-243">Na liście aplikacji zaznacz **Mozy Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="8f603-243">In the applications list, select **Mozy Enterprise**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_app.png) 

3. <span data-ttu-id="8f603-245">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8f603-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="8f603-247">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8f603-247">Click **Add** button.</span></span> <span data-ttu-id="8f603-248">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8f603-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="8f603-250">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="8f603-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8f603-251">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8f603-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8f603-252">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8f603-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8f603-253">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8f603-253">Testing single sign-on</span></span>

<span data-ttu-id="8f603-254">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="8f603-254">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8f603-255">Po kliknięciu kafelka Mozy przedsiębiorstwa w panelu dostępu, należy pobrać strony logowania organizacji Mozy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8f603-255">When you click the Mozy Enterprise tile in the Access Panel, you should get login page of Mozy Enterprise application.</span></span>
<span data-ttu-id="8f603-256">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8f603-256">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8f603-257">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8f603-257">Additional resources</span></span>

* [<span data-ttu-id="8f603-258">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8f603-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8f603-259">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8f603-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_203.png

