---
title: "Samouczek: Integracji Azure Active Directory z ulepszeniami małych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między ulepszenia małe i Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 59c8a112-41e1-4337-9ef3-3d7029780d61
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33213fe4b61f5005cf78bee2c05b2b1e5e71ae8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-small-improvements"></a><span data-ttu-id="a2b73-103">Samouczek: Integracji Azure Active Directory z ulepszeniami małe</span><span class="sxs-lookup"><span data-stu-id="a2b73-103">Tutorial: Azure Active Directory integration with Small Improvements</span></span>

<span data-ttu-id="a2b73-104">Z tego samouczka, dowiesz się, jak toointegrate małych ulepszenia w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a2b73-104">In this tutorial, you learn how toointegrate Small Improvements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a2b73-105">Integracja z usługą Azure AD małych ulepszenia zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="a2b73-105">Integrating Small Improvements with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a2b73-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooSmall ulepszenia</span><span class="sxs-lookup"><span data-stu-id="a2b73-106">You can control in Azure AD who has access tooSmall Improvements</span></span>
- <span data-ttu-id="a2b73-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSmall ulepszenia (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2b73-107">You can enable your users tooautomatically get signed-on tooSmall Improvements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a2b73-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a2b73-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a2b73-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a2b73-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2b73-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a2b73-110">Prerequisites</span></span>

<span data-ttu-id="a2b73-111">tooconfigure integracji usługi Azure AD z ulepszeniami małych należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a2b73-111">tooconfigure Azure AD integration with Small Improvements, you need hello following items:</span></span>

- <span data-ttu-id="a2b73-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2b73-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a2b73-113">Ulepszenia małych logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a2b73-113">A Small Improvements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a2b73-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="a2b73-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a2b73-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="a2b73-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a2b73-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="a2b73-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a2b73-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a2b73-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a2b73-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="a2b73-118">Scenario description</span></span>
<span data-ttu-id="a2b73-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="a2b73-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a2b73-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="a2b73-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a2b73-121">Dodawanie małych ulepszenia z galerii hello</span><span class="sxs-lookup"><span data-stu-id="a2b73-121">Adding Small Improvements from hello gallery</span></span>
2. <span data-ttu-id="a2b73-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a2b73-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-small-improvements-from-hello-gallery"></a><span data-ttu-id="a2b73-123">Dodawanie małych ulepszenia z galerii hello</span><span class="sxs-lookup"><span data-stu-id="a2b73-123">Adding Small Improvements from hello gallery</span></span>
<span data-ttu-id="a2b73-124">tooconfigure hello integracji małych ulepszeń do usługi Azure AD, należy tooadd małych ulepszenia z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="a2b73-124">tooconfigure hello integration of Small Improvements into Azure AD, you need tooadd Small Improvements from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a2b73-125">**tooadd małych ulepszenia z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="a2b73-125">**tooadd Small Improvements from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2b73-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a2b73-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="a2b73-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="a2b73-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a2b73-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a2b73-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="a2b73-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a2b73-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="a2b73-133">W polu wyszukiwania hello wpisz **ulepszenia małych**.</span><span class="sxs-lookup"><span data-stu-id="a2b73-133">In hello search box, type **Small Improvements**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_search.png)

5. <span data-ttu-id="a2b73-135">W panelu wyników hello, wybierz **ulepszenia małych**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="a2b73-135">In hello results panel, select **Small Improvements**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a2b73-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a2b73-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a2b73-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z małych ulepszeń w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="a2b73-138">In this section, you configure and test Azure AD single sign-on with Small Improvements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a2b73-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w małych ulepszenia jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2b73-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Small Improvements is tooa user in Azure AD.</span></span> <span data-ttu-id="a2b73-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w małych ulepszenia musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="a2b73-140">In other words, a link relationship between an Azure AD user and hello related user in Small Improvements needs toobe established.</span></span>

<span data-ttu-id="a2b73-141">W małych ulepszenia, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="a2b73-141">In Small Improvements, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a2b73-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z ulepszeniami małych, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a2b73-142">tooconfigure and test Azure AD single sign-on with Small Improvements, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a2b73-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="a2b73-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a2b73-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a2b73-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a2b73-145">**[Tworzenie użytkownika testowego ulepszenia małych](#creating-a-small-improvements-test-user)**  -toohave odpowiednikiem Simona Britta w małych ulepszenia, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a2b73-145">**[Creating a Small Improvements test user](#creating-a-small-improvements-test-user)** - toohave a counterpart of Britta Simon in Small Improvements that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a2b73-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a2b73-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a2b73-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="a2b73-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a2b73-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a2b73-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a2b73-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji małych ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="a2b73-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Small Improvements application.</span></span>

<span data-ttu-id="a2b73-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z małych ulepszeń, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="a2b73-150">**tooconfigure Azure AD single sign-on with Small Improvements, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2b73-151">W portalu Azure na powitania hello **ulepszenia małych** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="a2b73-151">In hello Azure portal, on hello **Small Improvements** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="a2b73-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a2b73-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_samlbase.png)

3. <span data-ttu-id="a2b73-155">Na powitania **adresy URL i małej domeny ulepszenia** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="a2b73-155">On hello **Small Improvements Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_url.png)

    <span data-ttu-id="a2b73-157">a.</span><span class="sxs-lookup"><span data-stu-id="a2b73-157">a.</span></span> <span data-ttu-id="a2b73-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="a2b73-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    <span data-ttu-id="a2b73-159">b.</span><span class="sxs-lookup"><span data-stu-id="a2b73-159">b.</span></span> <span data-ttu-id="a2b73-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.small-improvements.com`</span><span class="sxs-lookup"><span data-stu-id="a2b73-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.small-improvements.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a2b73-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="a2b73-161">These values are not real.</span></span> <span data-ttu-id="a2b73-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="a2b73-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a2b73-163">Skontaktuj się z [zespołem pomocy technicznej klienta ulepszenia małych](mailto:support@small-improvements.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="a2b73-163">Contact [Small Improvements Client support team](mailto:support@small-improvements.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="a2b73-164">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="a2b73-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_certificate.png) 

5. <span data-ttu-id="a2b73-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a2b73-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a2b73-168">Na powitania **małych konfiguracji ulepszenia** , kliknij przycisk **skonfigurować małych ulepszenia** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="a2b73-168">On hello **Small Improvements Configuration** section, click **Configure Small Improvements** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a2b73-169">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="a2b73-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_configure.png) 

7. <span data-ttu-id="a2b73-171">W innym oknie przeglądarki Zaloguj się w witrynie tooyour ulepszenia małe firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="a2b73-171">In another browser window, sign on tooyour Small Improvements company site as an administrator.</span></span>

8. <span data-ttu-id="a2b73-172">Witaj strony głównej pulpitu nawigacyjnego, kliknij **administracji** przycisku po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="a2b73-172">From hello main dashboard page, click **Administration** button on hello left.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_06.png) 

9. <span data-ttu-id="a2b73-174">Kliknij przycisk hello **logowania jednokrotnego SAML** przycisk z **integracji** sekcji.</span><span class="sxs-lookup"><span data-stu-id="a2b73-174">Click hello **SAML SSO** button from **Integrations** section.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_07.png) 

10. <span data-ttu-id="a2b73-176">Na stronie Ustawienia logowania jednokrotnego hello wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="a2b73-176">On hello SSO Setup page, perform hello following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_08.png)  

    <span data-ttu-id="a2b73-178">a.</span><span class="sxs-lookup"><span data-stu-id="a2b73-178">a.</span></span> <span data-ttu-id="a2b73-179">W hello **punkt końcowy HTTP** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a2b73-179">In hello **HTTP Endpoint** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a2b73-180">b.</span><span class="sxs-lookup"><span data-stu-id="a2b73-180">b.</span></span> <span data-ttu-id="a2b73-181">Otwórz pobrany certyfikat w Notatniku, hello kopiowania zawartości, a następnie wklej go do hello **x509 certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a2b73-181">Open your downloaded certificate in Notepad, copy hello content, and then paste it into hello **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="a2b73-182">c.</span><span class="sxs-lookup"><span data-stu-id="a2b73-182">c.</span></span> <span data-ttu-id="a2b73-183">W razie potrzeby toohave logowania jednokrotnego i logowania formularza opcję uwierzytelniania dostępne dla użytkowników, a następnie sprawdź hello **włączyć dostęp za pomocą nazwy logowania i hasła zbyt** opcji.</span><span class="sxs-lookup"><span data-stu-id="a2b73-183">If you wish toohave SSO and Login form authentication option available for users, then check hello **Enable access via login/password too** option.</span></span>  

    <span data-ttu-id="a2b73-184">d.</span><span class="sxs-lookup"><span data-stu-id="a2b73-184">d.</span></span> <span data-ttu-id="a2b73-185">Wprowadź hello odpowiednią wartość tooName hello logowania jednokrotnego logowania przycisku w hello **SAML monitu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a2b73-185">Enter hello appropriate value tooName hello SSO Login button in hello **SAML Prompt** textbox.</span></span>  

    <span data-ttu-id="a2b73-186">e.</span><span class="sxs-lookup"><span data-stu-id="a2b73-186">e.</span></span> <span data-ttu-id="a2b73-187">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a2b73-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="a2b73-188">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="a2b73-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a2b73-189">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="a2b73-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a2b73-190">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a2b73-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a2b73-191">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2b73-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="a2b73-192">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="a2b73-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="a2b73-194">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="a2b73-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2b73-195">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="a2b73-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a2b73-197">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="a2b73-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a2b73-199">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a2b73-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a2b73-201">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="a2b73-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a2b73-203">a.</span><span class="sxs-lookup"><span data-stu-id="a2b73-203">a.</span></span> <span data-ttu-id="a2b73-204">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a2b73-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a2b73-205">b.</span><span class="sxs-lookup"><span data-stu-id="a2b73-205">b.</span></span> <span data-ttu-id="a2b73-206">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a2b73-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a2b73-207">c.</span><span class="sxs-lookup"><span data-stu-id="a2b73-207">c.</span></span> <span data-ttu-id="a2b73-208">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="a2b73-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a2b73-209">d.</span><span class="sxs-lookup"><span data-stu-id="a2b73-209">d.</span></span> <span data-ttu-id="a2b73-210">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a2b73-210">Click **Create**.</span></span>
 
### <a name="creating-a-small-improvements-test-user"></a><span data-ttu-id="a2b73-211">Tworzenie użytkownika testowego małych ulepszenia</span><span class="sxs-lookup"><span data-stu-id="a2b73-211">Creating a Small Improvements test user</span></span>

<span data-ttu-id="a2b73-212">toolog użytkowników tooenable usługi Azure AD w tooSmall ulepszenia, muszą mieć przydzielone do ulepszenia mała.</span><span class="sxs-lookup"><span data-stu-id="a2b73-212">tooenable Azure AD users toolog in tooSmall Improvements, they must be provisioned into Small Improvements.</span></span> <span data-ttu-id="a2b73-213">W przypadku hello małych ulepszenia Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="a2b73-213">In hello case of Small Improvements, provisioning is a manual task.</span></span>

<span data-ttu-id="a2b73-214">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="a2b73-214">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2b73-215">Logowania jednokrotnego tooyour małych ulepszenia witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="a2b73-215">Sign-on tooyour Small Improvements company site as an administrator.</span></span>

2. <span data-ttu-id="a2b73-216">Na stronie głównej hello toohello menu Przejdź na powitania po lewej, kliknij przycisk **administracji**.</span><span class="sxs-lookup"><span data-stu-id="a2b73-216">From hello Home page, go toohello menu on hello left, click **Administration**.</span></span>

3. <span data-ttu-id="a2b73-217">Kliknij przycisk hello **katalogu użytkownika** przycisk z sekcji Zarządzanie użytkownikami.</span><span class="sxs-lookup"><span data-stu-id="a2b73-217">Click hello **User Directory** button from User Management section.</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_10.png) 

4. <span data-ttu-id="a2b73-219">Kliknij przycisk **dodawania użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="a2b73-219">Click **Add users**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_11.png) 

5. <span data-ttu-id="a2b73-221">Na powitania **Dodaj użytkowników** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="a2b73-221">On hello **Add Users** dialog, perform hello following steps:</span></span> 

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_12.png)
    
    <span data-ttu-id="a2b73-223">a.</span><span class="sxs-lookup"><span data-stu-id="a2b73-223">a.</span></span> <span data-ttu-id="a2b73-224">Wprowadź hello **imię** użytkownika, takich jak **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a2b73-224">Enter hello **first name** of user like **Britta**.</span></span>

    <span data-ttu-id="a2b73-225">b.</span><span class="sxs-lookup"><span data-stu-id="a2b73-225">b.</span></span> <span data-ttu-id="a2b73-226">Wprowadź hello **nazwisko** użytkownika, takich jak **Simona**.</span><span class="sxs-lookup"><span data-stu-id="a2b73-226">Enter hello **Last name** of user like **Simon**.</span></span>

    <span data-ttu-id="a2b73-227">c.</span><span class="sxs-lookup"><span data-stu-id="a2b73-227">c.</span></span> <span data-ttu-id="a2b73-228">Wprowadź hello **E-mail** użytkownika, takich jak  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="a2b73-228">Enter hello **Email** of user like **brittasimon@contoso.com**.</span></span> 

    <span data-ttu-id="a2b73-229">d.</span><span class="sxs-lookup"><span data-stu-id="a2b73-229">d.</span></span> <span data-ttu-id="a2b73-230">Możesz również osobistą wiadomość hello tooenter w hello **wysłać wiadomość e-mail z powiadomieniem** pole.</span><span class="sxs-lookup"><span data-stu-id="a2b73-230">You can also choose tooenter hello personal message in hello **Send notification email** box.</span></span> <span data-ttu-id="a2b73-231">Jeśli nie chcesz, aby toosend hello powiadomienia, usuń zaznaczenie tego pola wyboru.</span><span class="sxs-lookup"><span data-stu-id="a2b73-231">If you do not wish toosend hello notification, then uncheck this checkbox.</span></span>

    <span data-ttu-id="a2b73-232">e.</span><span class="sxs-lookup"><span data-stu-id="a2b73-232">e.</span></span> <span data-ttu-id="a2b73-233">Kliknij przycisk **tworzenie użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="a2b73-233">Click **Create Users**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a2b73-234">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2b73-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a2b73-235">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSmall ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="a2b73-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSmall Improvements.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="a2b73-237">**tooassign Simona Britta tooSmall ulepszenia, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="a2b73-237">**tooassign Britta Simon tooSmall Improvements, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2b73-238">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="a2b73-238">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="a2b73-240">Z listy aplikacji hello wybierz **ulepszenia małych**.</span><span class="sxs-lookup"><span data-stu-id="a2b73-240">In hello applications list, select **Small Improvements**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_app.png) 

3. <span data-ttu-id="a2b73-242">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="a2b73-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="a2b73-244">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a2b73-244">Click **Add** button.</span></span> <span data-ttu-id="a2b73-245">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a2b73-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="a2b73-247">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a2b73-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a2b73-248">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a2b73-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a2b73-249">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a2b73-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a2b73-250">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a2b73-250">Testing single sign-on</span></span>

<span data-ttu-id="a2b73-251">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a2b73-251">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="a2b73-252">Po kliknięciu powitalne małych ulepszenia kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour ulepszenia małych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a2b73-252">When you click hello Small Improvements tile in hello Access Panel, you should get automatically signed-on tooyour Small Improvements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a2b73-253">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="a2b73-253">Additional resources</span></span>

* [<span data-ttu-id="a2b73-254">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2b73-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a2b73-255">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a2b73-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_203.png

