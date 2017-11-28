---
title: 'Samouczek: Integracji Azure Active Directory z Kintone | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Kintone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 4f61fb95c643743504699b175beeff06e01c95c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a><span data-ttu-id="e85ef-103">Samouczek: Integracji Azure Active Directory z Kintone</span><span class="sxs-lookup"><span data-stu-id="e85ef-103">Tutorial: Azure Active Directory integration with Kintone</span></span>

<span data-ttu-id="e85ef-104">Z tego samouczka, dowiesz się, jak toointegrate Kintone w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e85ef-104">In this tutorial, you learn how toointegrate Kintone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e85ef-105">Integracja z usługą Azure AD Kintone zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e85ef-105">Integrating Kintone with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e85ef-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooKintone</span><span class="sxs-lookup"><span data-stu-id="e85ef-106">You can control in Azure AD who has access tooKintone</span></span>
- <span data-ttu-id="e85ef-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooKintone (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e85ef-107">You can enable your users tooautomatically get signed-on tooKintone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e85ef-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e85ef-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e85ef-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e85ef-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e85ef-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e85ef-110">Prerequisites</span></span>

<span data-ttu-id="e85ef-111">tooconfigure integracji z usługą Azure AD z Kintone należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e85ef-111">tooconfigure Azure AD integration with Kintone, you need hello following items:</span></span>

- <span data-ttu-id="e85ef-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e85ef-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e85ef-113">Kintone logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e85ef-113">A Kintone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e85ef-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e85ef-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e85ef-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="e85ef-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e85ef-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e85ef-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e85ef-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e85ef-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e85ef-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="e85ef-118">Scenario description</span></span>
<span data-ttu-id="e85ef-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="e85ef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e85ef-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="e85ef-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e85ef-121">Dodawanie Kintone z galerii hello</span><span class="sxs-lookup"><span data-stu-id="e85ef-121">Adding Kintone from hello gallery</span></span>
2. <span data-ttu-id="e85ef-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e85ef-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kintone-from-hello-gallery"></a><span data-ttu-id="e85ef-123">Dodawanie Kintone z galerii hello</span><span class="sxs-lookup"><span data-stu-id="e85ef-123">Adding Kintone from hello gallery</span></span>
<span data-ttu-id="e85ef-124">tooconfigure hello integracji Kintone do usługi Azure AD, należy tooadd Kintone z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="e85ef-124">tooconfigure hello integration of Kintone into Azure AD, you need tooadd Kintone from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e85ef-125">**tooadd Kintone z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e85ef-125">**tooadd Kintone from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e85ef-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e85ef-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="e85ef-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e85ef-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e85ef-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e85ef-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="e85ef-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e85ef-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="e85ef-133">W polu wyszukiwania hello wpisz **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="e85ef-133">In hello search box, type **Kintone**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_search.png)

5. <span data-ttu-id="e85ef-135">W panelu wyników hello zaznacz **Kintone**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="e85ef-135">In hello results panel, select **Kintone**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e85ef-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e85ef-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e85ef-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Kintone w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="e85ef-138">In this section, you configure and test Azure AD single sign-on with Kintone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e85ef-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Kintone jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e85ef-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kintone is tooa user in Azure AD.</span></span> <span data-ttu-id="e85ef-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Kintone musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="e85ef-140">In other words, a link relationship between an Azure AD user and hello related user in Kintone needs toobe established.</span></span>

<span data-ttu-id="e85ef-141">W Kintone, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="e85ef-141">In Kintone, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e85ef-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Kintone, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="e85ef-142">tooconfigure and test Azure AD single sign-on with Kintone, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e85ef-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e85ef-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e85ef-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e85ef-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e85ef-145">**[Tworzenie użytkownika testowego Kintone](#creating-a-kintone-test-user)**  -toohave odpowiednikiem Simona Britta w Kintone, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e85ef-145">**[Creating a Kintone test user](#creating-a-kintone-test-user)** - toohave a counterpart of Britta Simon in Kintone that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e85ef-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e85ef-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e85ef-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="e85ef-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e85ef-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e85ef-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e85ef-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Kintone.</span><span class="sxs-lookup"><span data-stu-id="e85ef-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kintone application.</span></span>

<span data-ttu-id="e85ef-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Kintone, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e85ef-150">**tooconfigure Azure AD single sign-on with Kintone, perform hello following steps:**</span></span>

1. <span data-ttu-id="e85ef-151">W portalu Azure na powitania hello **Kintone** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e85ef-151">In hello Azure portal, on hello **Kintone** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="e85ef-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e85ef-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_samlbase.png)

3. <span data-ttu-id="e85ef-155">Na powitania **Kintone domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="e85ef-155">On hello **Kintone Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_url.png)

    <span data-ttu-id="e85ef-157">a.</span><span class="sxs-lookup"><span data-stu-id="e85ef-157">a.</span></span> <span data-ttu-id="e85ef-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.kintone.com`</span><span class="sxs-lookup"><span data-stu-id="e85ef-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.kintone.com`</span></span>

    <span data-ttu-id="e85ef-159">b.</span><span class="sxs-lookup"><span data-stu-id="e85ef-159">b.</span></span> <span data-ttu-id="e85ef-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="e85ef-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.cybozu.com`|
    | `https://<companyname>.kintone.com`|

    > [!NOTE] 
    > <span data-ttu-id="e85ef-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="e85ef-161">These values are not real.</span></span> <span data-ttu-id="e85ef-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="e85ef-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e85ef-163">Skontaktuj się z [zespołem pomocy technicznej klienta Kintone](https://www.kintone.com/contact/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="e85ef-163">Contact [Kintone Client support team](https://www.kintone.com/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="e85ef-164">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e85ef-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_certificate.png) 

5. <span data-ttu-id="e85ef-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e85ef-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kintone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e85ef-168">Na powitania **konfiguracji Kintone** kliknij **skonfigurować Kintone** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="e85ef-168">On hello **Kintone Configuration** section, click **Configure Kintone** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e85ef-169">Witaj kopii **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="e85ef-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_configure.png) 

7. <span data-ttu-id="e85ef-171">W oknie przeglądarki innej witryny sieci web, zaloguj się do Twojego **Kintone** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e85ef-171">In a different web browser window, log into your **Kintone** company site as an administrator.</span></span>

8. <span data-ttu-id="e85ef-172">Kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="e85ef-172">Click **Settings**.</span></span>
   
    <span data-ttu-id="e85ef-173">![Ustawienia](./media/active-directory-saas-kintone-tutorial/ic785879.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="e85ef-173">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

9. <span data-ttu-id="e85ef-174">Kliknij przycisk **użytkownicy i administrowanie systemem**.</span><span class="sxs-lookup"><span data-stu-id="e85ef-174">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="e85ef-175">![Użytkownicy i administrowanie systemem](./media/active-directory-saas-kintone-tutorial/ic785880.png "użytkowników & administracji systemu")</span><span class="sxs-lookup"><span data-stu-id="e85ef-175">![Users & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "Users & System Administration")</span></span>

10. <span data-ttu-id="e85ef-176">W obszarze **Administracja systemu \> zabezpieczeń** kliknij **logowania**.</span><span class="sxs-lookup"><span data-stu-id="e85ef-176">Under **System Administration \> Security** click **Login**.</span></span>
   
    <span data-ttu-id="e85ef-177">![Logowania](./media/active-directory-saas-kintone-tutorial/ic785881.png "logowania")</span><span class="sxs-lookup"><span data-stu-id="e85ef-177">![Login](./media/active-directory-saas-kintone-tutorial/ic785881.png "Login")</span></span>

11. <span data-ttu-id="e85ef-178">Kliknij przycisk **uwierzytelnianie Włącz SAML**.</span><span class="sxs-lookup"><span data-stu-id="e85ef-178">Click **Enable SAML authentication**.</span></span>
   
    <span data-ttu-id="e85ef-179">![Uwierzytelnianie SAML](./media/active-directory-saas-kintone-tutorial/ic785882.png "uwierzytelnianie SAML")</span><span class="sxs-lookup"><span data-stu-id="e85ef-179">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML Authentication")</span></span>

12. <span data-ttu-id="e85ef-180">W sekcji uwierzytelnianie SAML hello wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e85ef-180">In hello SAML Authentication section, perform hello following steps:</span></span>
    
    <span data-ttu-id="e85ef-181">![Uwierzytelnianie SAML](./media/active-directory-saas-kintone-tutorial/ic785883.png "uwierzytelnianie SAML")</span><span class="sxs-lookup"><span data-stu-id="e85ef-181">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML Authentication")</span></span>
    
    <span data-ttu-id="e85ef-182">a.</span><span class="sxs-lookup"><span data-stu-id="e85ef-182">a.</span></span> <span data-ttu-id="e85ef-183">W hello **adres URL logowania** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e85ef-183">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="e85ef-184">b.</span><span class="sxs-lookup"><span data-stu-id="e85ef-184">b.</span></span> <span data-ttu-id="e85ef-185">W hello **adresu URL wylogowania** pole tekstowe, Wklej wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e85ef-185">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="e85ef-186">c.</span><span class="sxs-lookup"><span data-stu-id="e85ef-186">c.</span></span> <span data-ttu-id="e85ef-187">Kliknij przycisk **Przeglądaj** tooupload pobranego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="e85ef-187">Click **Browse** tooupload your downloaded certificate.</span></span>
    
    <span data-ttu-id="e85ef-188">d.</span><span class="sxs-lookup"><span data-stu-id="e85ef-188">d.</span></span> <span data-ttu-id="e85ef-189">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="e85ef-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="e85ef-190">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="e85ef-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e85ef-191">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="e85ef-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e85ef-192">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e85ef-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e85ef-193">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e85ef-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="e85ef-194">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="e85ef-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="e85ef-196">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e85ef-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e85ef-197">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e85ef-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e85ef-199">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="e85ef-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e85ef-201">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e85ef-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e85ef-203">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e85ef-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e85ef-205">a.</span><span class="sxs-lookup"><span data-stu-id="e85ef-205">a.</span></span> <span data-ttu-id="e85ef-206">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e85ef-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e85ef-207">b.</span><span class="sxs-lookup"><span data-stu-id="e85ef-207">b.</span></span> <span data-ttu-id="e85ef-208">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e85ef-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e85ef-209">c.</span><span class="sxs-lookup"><span data-stu-id="e85ef-209">c.</span></span> <span data-ttu-id="e85ef-210">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="e85ef-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e85ef-211">d.</span><span class="sxs-lookup"><span data-stu-id="e85ef-211">d.</span></span> <span data-ttu-id="e85ef-212">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e85ef-212">Click **Create**.</span></span>
 
### <a name="creating-a-kintone-test-user"></a><span data-ttu-id="e85ef-213">Tworzenie użytkownika testowego Kintone</span><span class="sxs-lookup"><span data-stu-id="e85ef-213">Creating a Kintone test user</span></span>

<span data-ttu-id="e85ef-214">toolog użytkowników tooenable usługi Azure AD w tooKintone, muszą mieć przydzielone do Kintone.</span><span class="sxs-lookup"><span data-stu-id="e85ef-214">tooenable Azure AD users toolog in tooKintone, they must be provisioned into Kintone.</span></span>  
<span data-ttu-id="e85ef-215">W przypadku hello Kintone Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="e85ef-215">In hello case of Kintone, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="e85ef-216">tooprovision konta użytkownika, należy wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e85ef-216">tooprovision a user account, perform hello following steps:</span></span>

1. <span data-ttu-id="e85ef-217">Zaloguj się za tooyour **Kintone** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e85ef-217">Log in tooyour **Kintone** company site as an administrator.</span></span>

2. <span data-ttu-id="e85ef-218">Kliknij przycisk **ustawienie**.</span><span class="sxs-lookup"><span data-stu-id="e85ef-218">Click **Setting**.</span></span>
   
    <span data-ttu-id="e85ef-219">![Ustawienia](./media/active-directory-saas-kintone-tutorial/ic785879.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="e85ef-219">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

3. <span data-ttu-id="e85ef-220">Kliknij przycisk **użytkownicy i administrowanie systemem**.</span><span class="sxs-lookup"><span data-stu-id="e85ef-220">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="e85ef-221">![Administracja systemu & użytkownika](./media/active-directory-saas-kintone-tutorial/ic785880.png "Administracja systemu & użytkownika")</span><span class="sxs-lookup"><span data-stu-id="e85ef-221">![User & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "User & System Administration")</span></span>

4. <span data-ttu-id="e85ef-222">W obszarze **Administracja użytkownikami**, kliknij przycisk **działów i użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="e85ef-222">Under **User Administration**, click **Departments & Users**.</span></span>
   
    <span data-ttu-id="e85ef-223">![Dział & użytkowników](./media/active-directory-saas-kintone-tutorial/ic785888.png "działu & użytkowników")</span><span class="sxs-lookup"><span data-stu-id="e85ef-223">![Department & Users](./media/active-directory-saas-kintone-tutorial/ic785888.png "Department & Users")</span></span>

5. <span data-ttu-id="e85ef-224">Kliknij przycisk **nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="e85ef-224">Click **New User**.</span></span>
   
    <span data-ttu-id="e85ef-225">![Nowi użytkownicy](./media/active-directory-saas-kintone-tutorial/ic785889.png "nowych użytkowników")</span><span class="sxs-lookup"><span data-stu-id="e85ef-225">![New Users](./media/active-directory-saas-kintone-tutorial/ic785889.png "New Users")</span></span>

6. <span data-ttu-id="e85ef-226">W hello **nowego użytkownika** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="e85ef-226">In hello **New User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="e85ef-227">![Nowi użytkownicy](./media/active-directory-saas-kintone-tutorial/ic785890.png "nowych użytkowników")</span><span class="sxs-lookup"><span data-stu-id="e85ef-227">![New Users](./media/active-directory-saas-kintone-tutorial/ic785890.png "New Users")</span></span>
   
    <span data-ttu-id="e85ef-228">a.</span><span class="sxs-lookup"><span data-stu-id="e85ef-228">a.</span></span> <span data-ttu-id="e85ef-229">Wpisz **Nazwa wyświetlana**, **nazwa logowania**, **nowe hasło**, **Potwierdź hasło**, **adres E-mail**, i inne szczegóły prawidłowego konta usługi AAD, które chcesz tooprovision do hello pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="e85ef-229">Type a **Display Name**, **Login Name**, **New Password**, **Confirm Password**, **E-mail Address**, and other details of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
 
    <span data-ttu-id="e85ef-230">b.</span><span class="sxs-lookup"><span data-stu-id="e85ef-230">b.</span></span> <span data-ttu-id="e85ef-231">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="e85ef-231">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="e85ef-232">Możesz użyć innych Kintone użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Kintone tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="e85ef-232">You can use any other Kintone user account creation tools or APIs provided by Kintone tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e85ef-233">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e85ef-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e85ef-234">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooKintone.</span><span class="sxs-lookup"><span data-stu-id="e85ef-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKintone.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="e85ef-236">**tooassign tooKintone Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e85ef-236">**tooassign Britta Simon tooKintone, perform hello following steps:**</span></span>

1. <span data-ttu-id="e85ef-237">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e85ef-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="e85ef-239">Z listy aplikacji hello wybierz **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="e85ef-239">In hello applications list, select **Kintone**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_app.png) 

3. <span data-ttu-id="e85ef-241">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e85ef-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="e85ef-243">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e85ef-243">Click **Add** button.</span></span> <span data-ttu-id="e85ef-244">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e85ef-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="e85ef-246">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e85ef-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e85ef-247">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e85ef-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e85ef-248">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e85ef-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e85ef-249">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e85ef-249">Testing single sign-on</span></span>

<span data-ttu-id="e85ef-250">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="e85ef-250">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e85ef-251">Po kliknięciu kafelka Kintone hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Kintone aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e85ef-251">When you click hello Kintone tile in hello Access Panel, you should get automatically signed-on tooyour Kintone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e85ef-252">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e85ef-252">Additional resources</span></span>

* [<span data-ttu-id="e85ef-253">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e85ef-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e85ef-254">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e85ef-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_203.png

