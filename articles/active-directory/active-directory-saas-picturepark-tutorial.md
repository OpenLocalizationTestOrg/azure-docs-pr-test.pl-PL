---
title: 'Samouczek: Integracji Azure Active Directory z Picturepark | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Picturepark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 3d826d3f73aad2f0d123f8697c6caafad7bc926a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a><span data-ttu-id="a4b64-103">Samouczek: Integracji Azure Active Directory z Picturepark</span><span class="sxs-lookup"><span data-stu-id="a4b64-103">Tutorial: Azure Active Directory integration with Picturepark</span></span>

<span data-ttu-id="a4b64-104">Z tego samouczka, dowiesz się, jak toointegrate Picturepark w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a4b64-104">In this tutorial, you learn how toointegrate Picturepark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a4b64-105">Integracja z usługą Azure AD Picturepark zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="a4b64-105">Integrating Picturepark with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a4b64-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooPicturepark</span><span class="sxs-lookup"><span data-stu-id="a4b64-106">You can control in Azure AD who has access tooPicturepark</span></span>
- <span data-ttu-id="a4b64-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooPicturepark (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4b64-107">You can enable your users tooautomatically get signed-on tooPicturepark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a4b64-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a4b64-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a4b64-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a4b64-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4b64-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a4b64-110">Prerequisites</span></span>

<span data-ttu-id="a4b64-111">tooconfigure integracji z usługą Azure AD z Picturepark należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a4b64-111">tooconfigure Azure AD integration with Picturepark, you need hello following items:</span></span>

- <span data-ttu-id="a4b64-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4b64-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a4b64-113">Picturepark logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a4b64-113">A Picturepark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a4b64-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="a4b64-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a4b64-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="a4b64-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a4b64-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="a4b64-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a4b64-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a4b64-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a4b64-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="a4b64-118">Scenario description</span></span>
<span data-ttu-id="a4b64-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="a4b64-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a4b64-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="a4b64-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a4b64-121">Dodawanie Picturepark z galerii hello</span><span class="sxs-lookup"><span data-stu-id="a4b64-121">Adding Picturepark from hello gallery</span></span>
2. <span data-ttu-id="a4b64-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a4b64-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-picturepark-from-hello-gallery"></a><span data-ttu-id="a4b64-123">Dodawanie Picturepark z galerii hello</span><span class="sxs-lookup"><span data-stu-id="a4b64-123">Adding Picturepark from hello gallery</span></span>
<span data-ttu-id="a4b64-124">tooconfigure hello integracji Picturepark do usługi Azure AD, należy tooadd Picturepark z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="a4b64-124">tooconfigure hello integration of Picturepark into Azure AD, you need tooadd Picturepark from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a4b64-125">**tooadd Picturepark z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="a4b64-125">**tooadd Picturepark from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4b64-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a4b64-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="a4b64-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="a4b64-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a4b64-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a4b64-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="a4b64-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a4b64-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="a4b64-133">W polu wyszukiwania hello wpisz **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="a4b64-133">In hello search box, type **Picturepark**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. <span data-ttu-id="a4b64-135">W panelu wyników hello zaznacz **Picturepark**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="a4b64-135">In hello results panel, select **Picturepark**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a4b64-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a4b64-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a4b64-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Picturepark w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="a4b64-138">In this section, you configure and test Azure AD single sign-on with Picturepark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a4b64-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Picturepark jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4b64-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Picturepark is tooa user in Azure AD.</span></span> <span data-ttu-id="a4b64-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Picturepark musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="a4b64-140">In other words, a link relationship between an Azure AD user and hello related user in Picturepark needs toobe established.</span></span>

<span data-ttu-id="a4b64-141">W Picturepark, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="a4b64-141">In Picturepark, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a4b64-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Picturepark, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a4b64-142">tooconfigure and test Azure AD single sign-on with Picturepark, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a4b64-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="a4b64-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a4b64-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a4b64-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a4b64-145">**[Tworzenie użytkownika testowego Picturepark](#creating-a-picturepark-test-user)**  -toohave odpowiednikiem Simona Britta w Picturepark, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a4b64-145">**[Creating a Picturepark test user](#creating-a-picturepark-test-user)** - toohave a counterpart of Britta Simon in Picturepark that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a4b64-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a4b64-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a4b64-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="a4b64-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a4b64-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a4b64-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a4b64-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Picturepark.</span><span class="sxs-lookup"><span data-stu-id="a4b64-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Picturepark application.</span></span>

<span data-ttu-id="a4b64-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Picturepark, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="a4b64-150">**tooconfigure Azure AD single sign-on with Picturepark, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4b64-151">W portalu Azure na powitania hello **Picturepark** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="a4b64-151">In hello Azure portal, on hello **Picturepark** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="a4b64-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a4b64-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. <span data-ttu-id="a4b64-155">Na powitania **Picturepark domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="a4b64-155">On hello **Picturepark Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    <span data-ttu-id="a4b64-157">a.</span><span class="sxs-lookup"><span data-stu-id="a4b64-157">a.</span></span> <span data-ttu-id="a4b64-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.picturepark.com`</span><span class="sxs-lookup"><span data-stu-id="a4b64-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.picturepark.com`</span></span>

    <span data-ttu-id="a4b64-159">b.</span><span class="sxs-lookup"><span data-stu-id="a4b64-159">b.</span></span> <span data-ttu-id="a4b64-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="a4b64-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span> 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > <span data-ttu-id="a4b64-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="a4b64-161">These values are not real.</span></span> <span data-ttu-id="a4b64-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="a4b64-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a4b64-163">Skontaktuj się z [zespołem pomocy technicznej klienta Picturepark](https://picturepark.com/about/contact/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="a4b64-163">Contact [Picturepark Client support team](https://picturepark.com/about/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="a4b64-164">Na powitania **certyfikat podpisywania SAML** hello kopiowania, sekcji **odcisk PALCA** wartości certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="a4b64-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. <span data-ttu-id="a4b64-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a4b64-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a4b64-168">Na powitania **konfiguracji Picturepark** kliknij **skonfigurować Picturepark** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="a4b64-168">On hello **Picturepark Configuration** section, click **Configure Picturepark** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a4b64-169">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="a4b64-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. <span data-ttu-id="a4b64-171">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Picturepark jako administrator.</span><span class="sxs-lookup"><span data-stu-id="a4b64-171">In a different web browser window, log into your Picturepark company site as an administrator.</span></span>

8. <span data-ttu-id="a4b64-172">Witaj pasku narzędzi u góry hello, kliknij przycisk **narzędzia administracyjne**, a następnie kliknij przycisk **konsoli zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="a4b64-172">In hello toolbar on hello top, click **Administrative tools**, and then click **Management Console**.</span></span>
   
    <span data-ttu-id="a4b64-173">![Konsola zarządzania](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Konsola zarządzania")</span><span class="sxs-lookup"><span data-stu-id="a4b64-173">![Management Console](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Management Console")</span></span>

9. <span data-ttu-id="a4b64-174">Kliknij przycisk **uwierzytelniania**, a następnie kliknij przycisk **dostawców tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="a4b64-174">Click **Authentication**, and then click **Identity providers**.</span></span>
   
    <span data-ttu-id="a4b64-175">![Uwierzytelnianie](./media/active-directory-saas-picturepark-tutorial/ic795063.png "uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="a4b64-175">![Authentication](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Authentication")</span></span>

10. <span data-ttu-id="a4b64-176">W hello **konfiguracji dostawcy tożsamości** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="a4b64-176">In hello **Identity provider configuration** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="a4b64-177">![Konfiguracja dostawcy tożsamości](./media/active-directory-saas-picturepark-tutorial/ic795064.png "konfiguracji dostawcy tożsamości")</span><span class="sxs-lookup"><span data-stu-id="a4b64-177">![Identity provider configuration](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Identity provider configuration")</span></span>
   
    <span data-ttu-id="a4b64-178">a.</span><span class="sxs-lookup"><span data-stu-id="a4b64-178">a.</span></span> <span data-ttu-id="a4b64-179">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a4b64-179">Click **Add**.</span></span>
  
    <span data-ttu-id="a4b64-180">b.</span><span class="sxs-lookup"><span data-stu-id="a4b64-180">b.</span></span> <span data-ttu-id="a4b64-181">Wpisz nazwę dla danej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a4b64-181">Type a name for your configuration.</span></span>
   
    <span data-ttu-id="a4b64-182">c.</span><span class="sxs-lookup"><span data-stu-id="a4b64-182">c.</span></span> <span data-ttu-id="a4b64-183">Wybierz **Ustaw jako domyślny**.</span><span class="sxs-lookup"><span data-stu-id="a4b64-183">Select **Set as default**.</span></span>
   
    <span data-ttu-id="a4b64-184">d.</span><span class="sxs-lookup"><span data-stu-id="a4b64-184">d.</span></span> <span data-ttu-id="a4b64-185">W **URI wystawcy** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a4b64-185">In **Issuer URI** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="a4b64-186">e.</span><span class="sxs-lookup"><span data-stu-id="a4b64-186">e.</span></span> <span data-ttu-id="a4b64-187">W **zaufanego wystawcy miniatury** pole tekstowe, Wklej wartość hello **odcisk palca** , które zostały skopiowane z **certyfikat podpisywania SAML** sekcji.</span><span class="sxs-lookup"><span data-stu-id="a4b64-187">In **Trusted Issuer Thumb Print** textbox, paste hello value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span> 

11. <span data-ttu-id="a4b64-188">Kliknij przycisk **JoinDefaultUsersGroup**.</span><span class="sxs-lookup"><span data-stu-id="a4b64-188">Click **JoinDefaultUsersGroup**.</span></span>

12. <span data-ttu-id="a4b64-189">tooset hello **Emailaddress** atrybutu w hello **oświadczeń** pole tekstowe, typ `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="a4b64-189">tooset hello **Emailaddress** attribute in hello **Claim** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` and click **Save**.</span></span>

      <span data-ttu-id="a4b64-190">![Konfiguracja](./media/active-directory-saas-picturepark-tutorial/ic795065.png "konfiguracji")</span><span class="sxs-lookup"><span data-stu-id="a4b64-190">![Configuration](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuration")</span></span>

> [!TIP]
> <span data-ttu-id="a4b64-191">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="a4b64-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a4b64-192">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="a4b64-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a4b64-193">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a4b64-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a4b64-194">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4b64-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="a4b64-195">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="a4b64-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="a4b64-197">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="a4b64-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4b64-198">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a4b64-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a4b64-200">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="a4b64-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a4b64-202">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a4b64-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a4b64-204">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="a4b64-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a4b64-206">a.</span><span class="sxs-lookup"><span data-stu-id="a4b64-206">a.</span></span> <span data-ttu-id="a4b64-207">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a4b64-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a4b64-208">b.</span><span class="sxs-lookup"><span data-stu-id="a4b64-208">b.</span></span> <span data-ttu-id="a4b64-209">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a4b64-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a4b64-210">c.</span><span class="sxs-lookup"><span data-stu-id="a4b64-210">c.</span></span> <span data-ttu-id="a4b64-211">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="a4b64-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a4b64-212">d.</span><span class="sxs-lookup"><span data-stu-id="a4b64-212">d.</span></span> <span data-ttu-id="a4b64-213">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a4b64-213">Click **Create**.</span></span>
 
### <a name="creating-a-picturepark-test-user"></a><span data-ttu-id="a4b64-214">Tworzenie użytkownika testowego Picturepark</span><span class="sxs-lookup"><span data-stu-id="a4b64-214">Creating a Picturepark test user</span></span>

<span data-ttu-id="a4b64-215">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do Picturepark muszą mieć przydzielone do Picturepark.</span><span class="sxs-lookup"><span data-stu-id="a4b64-215">In order tooenable Azure AD users toolog into Picturepark, they must be provisioned into Picturepark.</span></span> <span data-ttu-id="a4b64-216">W przypadku hello Picturepark Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="a4b64-216">In hello case of Picturepark, provisioning is a manual task.</span></span>

<span data-ttu-id="a4b64-217">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="a4b64-217">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4b64-218">Zaloguj się za tooyour **Picturepark** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="a4b64-218">Log in tooyour **Picturepark** tenant.</span></span>

2. <span data-ttu-id="a4b64-219">Witaj pasku narzędzi u góry hello, kliknij przycisk **narzędzia administracyjne**, a następnie kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="a4b64-219">In hello toolbar on hello top, click **Administrative tools**, and then click **Users**.</span></span>
   
    <span data-ttu-id="a4b64-220">![Użytkownicy](./media/active-directory-saas-picturepark-tutorial/ic795067.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="a4b64-220">![Users](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Users")</span></span>

3. <span data-ttu-id="a4b64-221">W hello **Przegląd użytkowników** , kliknij pozycję **nowy**.</span><span class="sxs-lookup"><span data-stu-id="a4b64-221">In hello **Users overview** tab, click **New**.</span></span>
   
    <span data-ttu-id="a4b64-222">![Zarządzanie użytkownikami](./media/active-directory-saas-picturepark-tutorial/ic795068.png "Zarządzanie użytkownikami")</span><span class="sxs-lookup"><span data-stu-id="a4b64-222">![User management](./media/active-directory-saas-picturepark-tutorial/ic795068.png "User management")</span></span>

4. <span data-ttu-id="a4b64-223">Na powitania **Tworzenie użytkownika** okna dialogowego, hello wykonaj następujące kroki prawidłowego Azure Active Directory użytkownika ma tooprovision:</span><span class="sxs-lookup"><span data-stu-id="a4b64-223">On hello **Create User** dialog, perform hello following steps of a valid Azure Active Directory User you want tooprovision:</span></span>
   
    <span data-ttu-id="a4b64-224">![Utwórz użytkownika](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Tworzenie użytkownika")</span><span class="sxs-lookup"><span data-stu-id="a4b64-224">![Create User](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Create User")</span></span>
   
    <span data-ttu-id="a4b64-225">a.</span><span class="sxs-lookup"><span data-stu-id="a4b64-225">a.</span></span> <span data-ttu-id="a4b64-226">W hello **adres E-mail** pole tekstowe, hello typu **adres e-mail** użytkownika hello  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="a4b64-226">In hello **Email Address** textbox, type hello **email address** of hello user **BrittaSimon@contoso.com**.</span></span>  
   
    <span data-ttu-id="a4b64-227">b.</span><span class="sxs-lookup"><span data-stu-id="a4b64-227">b.</span></span> <span data-ttu-id="a4b64-228">W hello **hasło** i **Potwierdź hasło** pól tekstowych, hello typu **hasło** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a4b64-228">In hello **Password** and **Confirm Password** textboxes, type hello **password** of BrittaSimon.</span></span> 
   
    <span data-ttu-id="a4b64-229">c.</span><span class="sxs-lookup"><span data-stu-id="a4b64-229">c.</span></span> <span data-ttu-id="a4b64-230">W hello **imię** pole tekstowe, hello typu **imię** użytkownika hello **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a4b64-230">In hello **First Name** textbox, type hello **First Name** of hello user **Britta**.</span></span> 
   
    <span data-ttu-id="a4b64-231">d.</span><span class="sxs-lookup"><span data-stu-id="a4b64-231">d.</span></span> <span data-ttu-id="a4b64-232">W hello **nazwisko** pole tekstowe, hello typu **nazwisko** użytkownika hello **Simona**.</span><span class="sxs-lookup"><span data-stu-id="a4b64-232">In hello **Last Name** textbox, type hello **Last Name** of hello user **Simon**.</span></span>
   
    <span data-ttu-id="a4b64-233">e.</span><span class="sxs-lookup"><span data-stu-id="a4b64-233">e.</span></span> <span data-ttu-id="a4b64-234">W hello **firmy** pole tekstowe, hello typu **nazwa firmy** hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a4b64-234">In hello **Company** textbox, type hello **Company name** of hello user.</span></span> 
   
    <span data-ttu-id="a4b64-235">f.</span><span class="sxs-lookup"><span data-stu-id="a4b64-235">f.</span></span> <span data-ttu-id="a4b64-236">W hello **kraju** pole tekstowe, wybierz hello **kraju** hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a4b64-236">In hello **Country** textbox, select hello **Country** of hello user.</span></span>
  
    <span data-ttu-id="a4b64-237">g.</span><span class="sxs-lookup"><span data-stu-id="a4b64-237">g.</span></span> <span data-ttu-id="a4b64-238">W hello **ZIP** pole tekstowe, hello typu **kod POCZTOWY** hello miasta.</span><span class="sxs-lookup"><span data-stu-id="a4b64-238">In hello **ZIP** textbox, type hello **ZIP code** of hello city.</span></span>
   
    <span data-ttu-id="a4b64-239">h.</span><span class="sxs-lookup"><span data-stu-id="a4b64-239">h.</span></span> <span data-ttu-id="a4b64-240">W hello **miasta** pole tekstowe, hello typu **nazwę miejscowości** hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a4b64-240">In hello **City** textbox, type hello **City name** of hello user.</span></span>

    <span data-ttu-id="a4b64-241">i.</span><span class="sxs-lookup"><span data-stu-id="a4b64-241">i.</span></span> <span data-ttu-id="a4b64-242">Wybierz **języka**.</span><span class="sxs-lookup"><span data-stu-id="a4b64-242">Select a **Language**.</span></span>
   
    <span data-ttu-id="a4b64-243">j.</span><span class="sxs-lookup"><span data-stu-id="a4b64-243">j.</span></span> <span data-ttu-id="a4b64-244">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a4b64-244">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="a4b64-245">Możesz użyć innych Picturepark użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Picturepark tooprovision kont użytkowników usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a4b64-245">You can use any other Picturepark user account creation tools or APIs provided by Picturepark tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a4b64-246">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a4b64-246">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a4b64-247">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooPicturepark.</span><span class="sxs-lookup"><span data-stu-id="a4b64-247">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPicturepark.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="a4b64-249">**tooassign tooPicturepark Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="a4b64-249">**tooassign Britta Simon tooPicturepark, perform hello following steps:**</span></span>

1. <span data-ttu-id="a4b64-250">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a4b64-250">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="a4b64-252">Z listy aplikacji hello wybierz **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="a4b64-252">In hello applications list, select **Picturepark**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. <span data-ttu-id="a4b64-254">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="a4b64-254">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="a4b64-256">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a4b64-256">Click **Add** button.</span></span> <span data-ttu-id="a4b64-257">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a4b64-257">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="a4b64-259">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a4b64-259">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a4b64-260">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a4b64-260">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a4b64-261">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a4b64-261">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a4b64-262">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a4b64-262">Testing single sign-on</span></span>

<span data-ttu-id="a4b64-263">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a4b64-263">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a4b64-264">Po kliknięciu kafelka Picturepark hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Picturepark aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a4b64-264">When you click hello Picturepark tile in hello Access Panel, you should get automatically signed-on tooyour Picturepark application.</span></span> <span data-ttu-id="a4b64-265">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a4b64-265">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a4b64-266">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="a4b64-266">Additional resources</span></span>

* [<span data-ttu-id="a4b64-267">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a4b64-267">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a4b64-268">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a4b64-268">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

