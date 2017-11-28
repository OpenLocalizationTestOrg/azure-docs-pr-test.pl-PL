---
title: 'Samouczek: Integracji Azure Active Directory z Samanage | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Samanage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c8edc29f113b8088438618a731e97c0f4f155b9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a><span data-ttu-id="f8081-103">Samouczek: Integracji Azure Active Directory z Samanage</span><span class="sxs-lookup"><span data-stu-id="f8081-103">Tutorial: Azure Active Directory integration with Samanage</span></span>

<span data-ttu-id="f8081-104">Z tego samouczka, dowiesz się, jak toointegrate Samanage w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f8081-104">In this tutorial, you learn how toointegrate Samanage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f8081-105">Integracja z usługą Azure AD Samanage zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="f8081-105">Integrating Samanage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f8081-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooSamanage</span><span class="sxs-lookup"><span data-stu-id="f8081-106">You can control in Azure AD who has access tooSamanage</span></span>
- <span data-ttu-id="f8081-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSamanage (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8081-107">You can enable your users tooautomatically get signed-on tooSamanage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f8081-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f8081-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f8081-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f8081-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8081-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f8081-110">Prerequisites</span></span>

<span data-ttu-id="f8081-111">tooconfigure integracji z usługą Azure AD z Samanage należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f8081-111">tooconfigure Azure AD integration with Samanage, you need hello following items:</span></span>

- <span data-ttu-id="f8081-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8081-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f8081-113">Samanage logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="f8081-113">A Samanage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f8081-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="f8081-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f8081-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="f8081-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f8081-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="f8081-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f8081-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f8081-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f8081-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="f8081-118">Scenario description</span></span>
<span data-ttu-id="f8081-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="f8081-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f8081-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="f8081-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f8081-121">Dodawanie Samanage z galerii hello</span><span class="sxs-lookup"><span data-stu-id="f8081-121">Adding Samanage from hello gallery</span></span>
2. <span data-ttu-id="f8081-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f8081-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-samanage-from-hello-gallery"></a><span data-ttu-id="f8081-123">Dodawanie Samanage z galerii hello</span><span class="sxs-lookup"><span data-stu-id="f8081-123">Adding Samanage from hello gallery</span></span>
<span data-ttu-id="f8081-124">tooconfigure hello integracji Samanage do usługi Azure AD, należy tooadd Samanage z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="f8081-124">tooconfigure hello integration of Samanage into Azure AD, you need tooadd Samanage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f8081-125">**tooadd Samanage z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="f8081-125">**tooadd Samanage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8081-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f8081-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="f8081-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="f8081-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f8081-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f8081-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="f8081-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f8081-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="f8081-133">W polu wyszukiwania hello wpisz **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="f8081-133">In hello search box, type **Samanage**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_search.png)

5. <span data-ttu-id="f8081-135">W panelu wyników hello zaznacz **Samanage**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="f8081-135">In hello results panel, select **Samanage**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f8081-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="f8081-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f8081-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Samanage w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="f8081-138">In this section, you configure and test Azure AD single sign-on with Samanage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f8081-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Samanage jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f8081-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Samanage is tooa user in Azure AD.</span></span> <span data-ttu-id="f8081-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Samanage musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="f8081-140">In other words, a link relationship between an Azure AD user and hello related user in Samanage needs toobe established.</span></span>

<span data-ttu-id="f8081-141">W Samanage, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="f8081-141">In Samanage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="f8081-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Samanage, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="f8081-142">tooconfigure and test Azure AD single sign-on with Samanage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f8081-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="f8081-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f8081-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f8081-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f8081-145">**[Tworzenie użytkownika testowego Samanage](#creating-a-samanage-test-user)**  -toohave odpowiednikiem Simona Britta w Samanage, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f8081-145">**[Creating a Samanage test user](#creating-a-samanage-test-user)** - toohave a counterpart of Britta Simon in Samanage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f8081-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f8081-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f8081-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="f8081-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f8081-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f8081-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f8081-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Samanage.</span><span class="sxs-lookup"><span data-stu-id="f8081-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Samanage application.</span></span>

<span data-ttu-id="f8081-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Samanage, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="f8081-150">**tooconfigure Azure AD single sign-on with Samanage, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8081-151">W portalu Azure na powitania hello **Samanage** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="f8081-151">In hello Azure portal, on hello **Samanage** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="f8081-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f8081-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_samlbase.png)

3. <span data-ttu-id="f8081-155">Na powitania **Samanage domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="f8081-155">On hello **Samanage Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_url.png)

    <span data-ttu-id="f8081-157">a.</span><span class="sxs-lookup"><span data-stu-id="f8081-157">a.</span></span> <span data-ttu-id="f8081-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<Company Name>.samanage.com/saml_login/<Company Name>`</span><span class="sxs-lookup"><span data-stu-id="f8081-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<Company Name>.samanage.com/saml_login/<Company Name>`</span></span>

    <span data-ttu-id="f8081-159">b.</span><span class="sxs-lookup"><span data-stu-id="f8081-159">b.</span></span> <span data-ttu-id="f8081-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<Company Name>.samanage.com`</span><span class="sxs-lookup"><span data-stu-id="f8081-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<Company Name>.samanage.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f8081-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="f8081-161">These values are not real.</span></span> <span data-ttu-id="f8081-162">Witaj rzeczywisty adres URL logowania i identyfikator, który znajduje się w dalszej części samouczka hello, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="f8081-162">Update these values with hello actual Sign-on URL and Identifier, which is explained later in hello tutorial.</span></span> <span data-ttu-id="f8081-163">Więcej informacji skontaktuj się z [zespołem pomocy technicznej klienta Samanage](https://www.samanage.com/support).</span><span class="sxs-lookup"><span data-stu-id="f8081-163">For more details contact [Samanage Client support team](https://www.samanage.com/support).</span></span>    
 
4. <span data-ttu-id="f8081-164">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="f8081-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_certificate.png) 

5. <span data-ttu-id="f8081-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f8081-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samanage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f8081-168">Na powitania **konfiguracji Samanage** kliknij **skonfigurować Samanage** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="f8081-168">On hello **Samanage Configuration** section, click **Configure Samanage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="f8081-169">Kopia hello **Sign-Out adresu URL i identyfikator jednostki SAML** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="f8081-169">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_configure.png) 

7. <span data-ttu-id="f8081-171">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Samanage jako administrator.</span><span class="sxs-lookup"><span data-stu-id="f8081-171">In a different web browser window, log into your Samanage company site as an administrator.</span></span>

8. <span data-ttu-id="f8081-172">Kliknij przycisk **pulpitu nawigacyjnego** i wybierz **Instalator** w lewym okienku nawigacji.</span><span class="sxs-lookup"><span data-stu-id="f8081-172">Click **Dashboard** and select **Setup** in left navigation pane.</span></span>
   
    <span data-ttu-id="f8081-173">![Pulpit nawigacyjny](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "pulpitu nawigacyjnego")</span><span class="sxs-lookup"><span data-stu-id="f8081-173">![Dashboard](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Dashboard")</span></span>

9. <span data-ttu-id="f8081-174">Kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="f8081-174">Click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="f8081-175">![Logowanie jednokrotne](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="f8081-175">![Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Single Sign-On")</span></span>

10. <span data-ttu-id="f8081-176">Przejdź za**logowania za pomocą protokołu SAML** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="f8081-176">Navigate too**Login using SAML** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="f8081-177">![Zaloguj się przy użyciu SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "logowania za pomocą protokołu SAML")</span><span class="sxs-lookup"><span data-stu-id="f8081-177">![Login using SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Login using SAML")</span></span>
 
    <span data-ttu-id="f8081-178">a.</span><span class="sxs-lookup"><span data-stu-id="f8081-178">a.</span></span> <span data-ttu-id="f8081-179">Kliknij przycisk **włączyć logowanie jednokrotne z SAML**.</span><span class="sxs-lookup"><span data-stu-id="f8081-179">Click **Enable Single Sign-On with SAML**.</span></span>  
 
    <span data-ttu-id="f8081-180">b.</span><span class="sxs-lookup"><span data-stu-id="f8081-180">b.</span></span> <span data-ttu-id="f8081-181">W hello **adres URL dostawcy tożsamości** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f8081-181">In hello **Identity Provider URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>    
 
    <span data-ttu-id="f8081-182">c.</span><span class="sxs-lookup"><span data-stu-id="f8081-182">c.</span></span> <span data-ttu-id="f8081-183">Potwierdź hello **adres URL logowania** hello dopasowań **na adres URL logowania** z **Samanage domeny i adres URL** sekcji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f8081-183">Confirm hello **Login URL** matches hello **Sign On URL** of **Samanage Domain and URLs** section in Azure portal.</span></span>
 
    <span data-ttu-id="f8081-184">d.</span><span class="sxs-lookup"><span data-stu-id="f8081-184">d.</span></span> <span data-ttu-id="f8081-185">W hello **adresu URL wylogowania** pole tekstowe, wprowadź wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f8081-185">In hello **Logout URL** textbox, enter hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="f8081-186">e.</span><span class="sxs-lookup"><span data-stu-id="f8081-186">e.</span></span> <span data-ttu-id="f8081-187">W hello **wystawcy SAML** pole tekstowe, ustawiony typ hello aplikacji identyfikator URI w dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="f8081-187">In hello **SAML Issuer** textbox, type hello app id URI set in your identity provider.</span></span>
 
    <span data-ttu-id="f8081-188">f.</span><span class="sxs-lookup"><span data-stu-id="f8081-188">f.</span></span> <span data-ttu-id="f8081-189">Otwórz base-64 zakodowany certyfikat pobrany z portalu Azure w programie Notatnik hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **Wklej dostawcy tożsamości x.509 szyfrowany poniżej certyfikat** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="f8081-189">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **Paste your Identity Provider x.509 Certificate below** textbox.</span></span>
 
    <span data-ttu-id="f8081-190">g.</span><span class="sxs-lookup"><span data-stu-id="f8081-190">g.</span></span> <span data-ttu-id="f8081-191">Kliknij przycisk **tworzenie użytkowników, jeśli nie istnieją w Samanage**.</span><span class="sxs-lookup"><span data-stu-id="f8081-191">Click **Create users if they do not exist in Samanage**.</span></span>
 
    <span data-ttu-id="f8081-192">h.</span><span class="sxs-lookup"><span data-stu-id="f8081-192">h.</span></span> <span data-ttu-id="f8081-193">Kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="f8081-193">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="f8081-194">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="f8081-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f8081-195">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="f8081-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f8081-196">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f8081-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f8081-197">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8081-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="f8081-198">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="f8081-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="f8081-200">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="f8081-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8081-201">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="f8081-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f8081-203">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="f8081-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f8081-205">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f8081-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f8081-207">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f8081-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f8081-209">a.</span><span class="sxs-lookup"><span data-stu-id="f8081-209">a.</span></span> <span data-ttu-id="f8081-210">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f8081-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f8081-211">b.</span><span class="sxs-lookup"><span data-stu-id="f8081-211">b.</span></span> <span data-ttu-id="f8081-212">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f8081-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f8081-213">c.</span><span class="sxs-lookup"><span data-stu-id="f8081-213">c.</span></span> <span data-ttu-id="f8081-214">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="f8081-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f8081-215">d.</span><span class="sxs-lookup"><span data-stu-id="f8081-215">d.</span></span> <span data-ttu-id="f8081-216">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f8081-216">Click **Create**.</span></span>
 
### <a name="creating-a-samanage-test-user"></a><span data-ttu-id="f8081-217">Tworzenie użytkownika testowego Samanage</span><span class="sxs-lookup"><span data-stu-id="f8081-217">Creating a Samanage test user</span></span>

<span data-ttu-id="f8081-218">toolog użytkowników tooenable usługi Azure AD w tooSamanage, muszą mieć przydzielone do Samanage.</span><span class="sxs-lookup"><span data-stu-id="f8081-218">tooenable Azure AD users toolog in tooSamanage, they must be provisioned into Samanage.</span></span>  
<span data-ttu-id="f8081-219">W przypadku hello Samanage Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="f8081-219">In hello case of Samanage, provisioning is a manual task.</span></span>

<span data-ttu-id="f8081-220">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="f8081-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8081-221">Zaloguj się do witryny firmy Samanage jako administrator.</span><span class="sxs-lookup"><span data-stu-id="f8081-221">Log into your Samanage company site as an administrator.</span></span>

2. <span data-ttu-id="f8081-222">Kliknij przycisk **pulpitu nawigacyjnego** i wybierz **Instalator** w przesuwanie nawigacji po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="f8081-222">Click **Dashboard** and select **Setup** in left navigation pan.</span></span>
   
    <span data-ttu-id="f8081-223">![Instalator](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Instalatora")</span><span class="sxs-lookup"><span data-stu-id="f8081-223">![Setup](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Setup")</span></span>

3. <span data-ttu-id="f8081-224">Kliknij przycisk hello **użytkowników** kartę</span><span class="sxs-lookup"><span data-stu-id="f8081-224">Click hello **Users** tab</span></span>
   
    <span data-ttu-id="f8081-225">![Użytkownicy](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="f8081-225">![Users](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Users")</span></span>

4. <span data-ttu-id="f8081-226">Kliknij przycisk **nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="f8081-226">Click **New User**.</span></span>
   
    <span data-ttu-id="f8081-227">![Nowy użytkownik](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="f8081-227">![New User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "New User")</span></span>

5. <span data-ttu-id="f8081-228">Typ hello **nazwa** i hello **adres E-mail** konta usługi Azure Active Directory tooprovision i kliknij **tworzenia użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="f8081-228">Type hello **Name** and hello **Email Address** of an Azure Active Directory account you want tooprovision and click **Create user**.</span></span>
   
    <span data-ttu-id="f8081-229">![Utwórz użytkownika](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Tworzenie użytkownika")</span><span class="sxs-lookup"><span data-stu-id="f8081-229">![Create User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Create User")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="f8081-230">właścicielem konta usługi Azure Active Directory Hello będzie otrzymywać wiadomości e-mail i postępuj zgodnie tooconfirm łącze swojego konta przed staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="f8081-230">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span> <span data-ttu-id="f8081-231">Możesz użyć innych Samanage użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision Samanage usługi Azure Active Directory kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f8081-231">You can use any other Samanage user account creation tools or APIs provided by Samanage tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f8081-232">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8081-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f8081-233">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSamanage.</span><span class="sxs-lookup"><span data-stu-id="f8081-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSamanage.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="f8081-235">**tooassign tooSamanage Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="f8081-235">**tooassign Britta Simon tooSamanage, perform hello following steps:**</span></span>

1. <span data-ttu-id="f8081-236">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f8081-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="f8081-238">Z listy aplikacji hello wybierz **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="f8081-238">In hello applications list, select **Samanage**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_app.png) 

3. <span data-ttu-id="f8081-240">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="f8081-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="f8081-242">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f8081-242">Click **Add** button.</span></span> <span data-ttu-id="f8081-243">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f8081-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="f8081-245">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f8081-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f8081-246">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f8081-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f8081-247">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="f8081-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f8081-248">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f8081-248">Testing single sign-on</span></span>

<span data-ttu-id="f8081-249">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="f8081-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f8081-250">Po kliknięciu kafelka Samanage hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Samanage aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f8081-250">When you click hello Samanage tile in hello Access Panel, you should get automatically signed-on tooyour Samanage application.</span></span>
<span data-ttu-id="f8081-251">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f8081-251">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f8081-252">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="f8081-252">Additional resources</span></span>

* [<span data-ttu-id="f8081-253">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f8081-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f8081-254">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f8081-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_203.png

