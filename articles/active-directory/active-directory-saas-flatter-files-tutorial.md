---
title: "Samouczek: Integracji Azure Active Directory z plikami płaska | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i płaska plików."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f86fe5e3-0e91-40d6-869c-3df6912d27ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 73ca2613b7bbaf9992ecf624ff5defabaa44f7a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-flatter-files"></a><span data-ttu-id="5f260-103">Samouczek: Integracji Azure Active Directory z plikami płaska</span><span class="sxs-lookup"><span data-stu-id="5f260-103">Tutorial: Azure Active Directory integration with Flatter Files</span></span>

<span data-ttu-id="5f260-104">Z tego samouczka, dowiesz się, jak toointegrate płaska plików w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5f260-104">In this tutorial, you learn how toointegrate Flatter Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5f260-105">Integrowanie płaska pliki z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5f260-105">Integrating Flatter Files with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5f260-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do plików tooFlatter</span><span class="sxs-lookup"><span data-stu-id="5f260-106">You can control in Azure AD who has access tooFlatter Files</span></span>
- <span data-ttu-id="5f260-107">Można włączyć tooautomatically Twojego użytkownikom pobieranie plików zalogowane tooFlatter (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f260-107">You can enable your users tooautomatically get signed-on tooFlatter Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5f260-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5f260-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5f260-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5f260-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f260-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5f260-110">Prerequisites</span></span>

<span data-ttu-id="5f260-111">tooconfigure integracji usługi Azure AD z plikami płaska należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5f260-111">tooconfigure Azure AD integration with Flatter Files, you need hello following items:</span></span>

- <span data-ttu-id="5f260-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f260-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5f260-113">Pliki płaska logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5f260-113">A Flatter Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5f260-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5f260-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5f260-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5f260-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5f260-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5f260-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5f260-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5f260-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5f260-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5f260-118">Scenario description</span></span>
<span data-ttu-id="5f260-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5f260-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5f260-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5f260-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5f260-121">Dodawanie plików płaska z galerii hello</span><span class="sxs-lookup"><span data-stu-id="5f260-121">Adding Flatter Files from hello gallery</span></span>
2. <span data-ttu-id="5f260-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5f260-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-flatter-files-from-hello-gallery"></a><span data-ttu-id="5f260-123">Dodawanie plików płaska z galerii hello</span><span class="sxs-lookup"><span data-stu-id="5f260-123">Adding Flatter Files from hello gallery</span></span>
<span data-ttu-id="5f260-124">tooconfigure hello integracji płaska plików do usługi Azure AD, należy tooadd płaska plików z listy tooyour galerii hello zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5f260-124">tooconfigure hello integration of Flatter Files into Azure AD, you need tooadd Flatter Files from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5f260-125">**tooadd płaska pliki z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5f260-125">**tooadd Flatter Files from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f260-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5f260-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="5f260-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5f260-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5f260-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5f260-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="5f260-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5f260-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="5f260-133">W polu wyszukiwania hello wpisz **płaska pliki**.</span><span class="sxs-lookup"><span data-stu-id="5f260-133">In hello search box, type **Flatter Files**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_search.png)

5. <span data-ttu-id="5f260-135">W panelu wyników hello, wybierz **płaska pliki**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5f260-135">In hello results panel, select **Flatter Files**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5f260-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5f260-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5f260-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z plikami płaska w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="5f260-138">In this section, you configure and test Azure AD single sign-on with Flatter Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5f260-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w plikach płaska jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5f260-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Flatter Files is tooa user in Azure AD.</span></span> <span data-ttu-id="5f260-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w plikach płaska musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="5f260-140">In other words, a link relationship between an Azure AD user and hello related user in Flatter Files needs toobe established.</span></span>

<span data-ttu-id="5f260-141">W plikach płaska, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="5f260-141">In Flatter Files, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5f260-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z plikami płaska, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="5f260-142">tooconfigure and test Azure AD single sign-on with Flatter Files, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5f260-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5f260-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5f260-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5f260-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5f260-145">**[Tworzenie użytkownika testowego płaska pliki](#creating-a-flatter-files-test-user)**  -toohave odpowiednikiem Simona Britta płaska plików, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5f260-145">**[Creating a Flatter Files test user](#creating-a-flatter-files-test-user)** - toohave a counterpart of Britta Simon in Flatter Files that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5f260-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5f260-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5f260-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="5f260-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5f260-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5f260-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5f260-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji płaska plików.</span><span class="sxs-lookup"><span data-stu-id="5f260-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Flatter Files application.</span></span>

<span data-ttu-id="5f260-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z plikami płaska wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5f260-150">**tooconfigure Azure AD single sign-on with Flatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f260-151">W portalu Azure na powitania hello **płaska pliki** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="5f260-151">In hello Azure portal, on hello **Flatter Files** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="5f260-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5f260-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_samlbase.png)

3. <span data-ttu-id="5f260-155">Na powitania **płaska domeny plików i adresy URL** sekcji, hello użytkownik nie ma tooperform wszystkie kroki jako aplikacji hello już jest wstępna Integracja z usługą Azure.</span><span class="sxs-lookup"><span data-stu-id="5f260-155">On hello **Flatter Files Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_url.png)
 
4. <span data-ttu-id="5f260-157">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5f260-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_certificate.png) 

5. <span data-ttu-id="5f260-159">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5f260-159">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-flatter-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5f260-161">Na powitania **płaska pliki konfiguracji** kliknij **skonfigurować płaska pliki** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="5f260-161">On hello **Flatter Files Configuration** section, click **Configure Flatter Files** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5f260-162">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="5f260-162">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_configure.png) 

7. <span data-ttu-id="5f260-164">Zaloguj się na tooyour płaska pliki aplikacji jako administrator.</span><span class="sxs-lookup"><span data-stu-id="5f260-164">Sign-on tooyour Flatter Files application as an administrator.</span></span>

8. <span data-ttu-id="5f260-165">Kliknij przycisk **pulpitu NAWIGACYJNEGO**.</span><span class="sxs-lookup"><span data-stu-id="5f260-165">Click **DASHBOARD**.</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_05.png)  

9. <span data-ttu-id="5f260-167">Kliknij przycisk **ustawienia**, a następnie wykonaj następujące kroki na powitania hello **firmy** karty:</span><span class="sxs-lookup"><span data-stu-id="5f260-167">Click **Settings**, and then perform hello following steps on hello **Company** tab:</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_06.png)  
    
    <span data-ttu-id="5f260-169">a.</span><span class="sxs-lookup"><span data-stu-id="5f260-169">a.</span></span> <span data-ttu-id="5f260-170">Wybierz **SAML 2.0 jest używany do uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="5f260-170">Select **Use SAML 2.0 for Authentication**.</span></span>
    
    <span data-ttu-id="5f260-171">b.</span><span class="sxs-lookup"><span data-stu-id="5f260-171">b.</span></span> <span data-ttu-id="5f260-172">Kliknij przycisk **skonfigurować SAML**.</span><span class="sxs-lookup"><span data-stu-id="5f260-172">Click **Configure SAML**.</span></span>

8. <span data-ttu-id="5f260-173">Na powitania **Konfiguracja SAML** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="5f260-173">On hello **SAML Configuration** dialog, perform hello following steps:</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_08.png)  
   
    <span data-ttu-id="5f260-175">a.</span><span class="sxs-lookup"><span data-stu-id="5f260-175">a.</span></span> <span data-ttu-id="5f260-176">W hello **domeny** tekstowym, wpisz domenę zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="5f260-176">In hello **Domain** textbox, type your registered domain.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="5f260-177">Jeśli użytkownik nie ma zarejestrowanej domeny jeszcze, skontaktuj się z bardziej płaski plików obsługuje zespołu za pomocą [ support@flatterfiles.com ](mailto:support@flatterfiles.com).</span><span class="sxs-lookup"><span data-stu-id="5f260-177">If you don't have a registered domain yet, contact your Flatter Files support team via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span></span> 
    
    <span data-ttu-id="5f260-178">b.</span><span class="sxs-lookup"><span data-stu-id="5f260-178">b.</span></span> <span data-ttu-id="5f260-179">W **adres URL dostawcy tożsamości** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana tworzą portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5f260-179">In **Identity Provider URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied form Azure portal.</span></span>
   
    <span data-ttu-id="5f260-180">c.</span><span class="sxs-lookup"><span data-stu-id="5f260-180">c.</span></span>  <span data-ttu-id="5f260-181">Otwieranie certyfikatu zakodowanego base-64 w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikat dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5f260-181">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="5f260-182">d.</span><span class="sxs-lookup"><span data-stu-id="5f260-182">d.</span></span> <span data-ttu-id="5f260-183">Kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="5f260-183">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="5f260-184">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="5f260-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5f260-185">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="5f260-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5f260-186">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5f260-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5f260-187">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f260-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="5f260-188">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="5f260-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="5f260-190">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5f260-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f260-191">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5f260-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5f260-193">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="5f260-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5f260-195">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5f260-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5f260-197">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5f260-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5f260-199">a.</span><span class="sxs-lookup"><span data-stu-id="5f260-199">a.</span></span> <span data-ttu-id="5f260-200">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5f260-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5f260-201">b.</span><span class="sxs-lookup"><span data-stu-id="5f260-201">b.</span></span> <span data-ttu-id="5f260-202">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5f260-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5f260-203">c.</span><span class="sxs-lookup"><span data-stu-id="5f260-203">c.</span></span> <span data-ttu-id="5f260-204">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="5f260-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5f260-205">d.</span><span class="sxs-lookup"><span data-stu-id="5f260-205">d.</span></span> <span data-ttu-id="5f260-206">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5f260-206">Click **Create**.</span></span>
 
### <a name="creating-a-flatter-files-test-user"></a><span data-ttu-id="5f260-207">Tworzenie użytkownika testowego płaska plików</span><span class="sxs-lookup"><span data-stu-id="5f260-207">Creating a Flatter Files test user</span></span>

<span data-ttu-id="5f260-208">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w płaska plików.</span><span class="sxs-lookup"><span data-stu-id="5f260-208">hello objective of this section is toocreate a user called Britta Simon in Flatter Files.</span></span>

<span data-ttu-id="5f260-209">**toocreate użytkownika o nazwie Simona Britta w plikach płaska wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5f260-209">**toocreate a user called Britta Simon in Flatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f260-210">Zaloguj się na tooyour **płaska pliki** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="5f260-210">Sign on tooyour **Flatter Files** company site as administrator.</span></span>

2. <span data-ttu-id="5f260-211">W okienku nawigacji hello po lewej stronie powitania kliknij **ustawienia**, a następnie kliknij przycisk hello **użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="5f260-211">In hello navigation pane on hello left, click **Settings**, and then click hello **Users** tab.</span></span>
   
    ![Utwórz użytkownika płaska plików](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_09.png)

3. <span data-ttu-id="5f260-213">Kliknij przycisk **dodać użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="5f260-213">Click **Add User**.</span></span> 

4. <span data-ttu-id="5f260-214">Na powitania **Dodaj użytkownika** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="5f260-214">On hello **Add User** dialog, perform hello following steps:</span></span>
   
    ![Utwórz użytkownika płaska plików](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_10.png)

    <span data-ttu-id="5f260-216">a.</span><span class="sxs-lookup"><span data-stu-id="5f260-216">a.</span></span> <span data-ttu-id="5f260-217">W hello **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="5f260-217">In hello **First Name** textbox, type **Britta**.</span></span>
   
    <span data-ttu-id="5f260-218">b.</span><span class="sxs-lookup"><span data-stu-id="5f260-218">b.</span></span> <span data-ttu-id="5f260-219">W hello **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="5f260-219">In hello **Last Name** textbox, type **Simon**.</span></span> 
   
    <span data-ttu-id="5f260-220">c.</span><span class="sxs-lookup"><span data-stu-id="5f260-220">c.</span></span> <span data-ttu-id="5f260-221">W hello **adres E-mail** tekstowym, wpisz adres e-mail firmy Britta hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5f260-221">In hello **Email Address** textbox, type Britta's email address in hello Azure portal.</span></span>
   
    <span data-ttu-id="5f260-222">d.</span><span class="sxs-lookup"><span data-stu-id="5f260-222">d.</span></span> <span data-ttu-id="5f260-223">Kliknij przycisk **przesłać**.</span><span class="sxs-lookup"><span data-stu-id="5f260-223">Click **Submit**.</span></span>   


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5f260-224">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f260-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5f260-225">W tej sekcji, musisz włączyć Simona Britta toouse Azure logowania jednokrotnego za udzielanie dostępu do plików tooFlatter.</span><span class="sxs-lookup"><span data-stu-id="5f260-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFlatter Files.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="5f260-227">**tooassign Simona Britta tooFlatter pliki, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5f260-227">**tooassign Britta Simon tooFlatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f260-228">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5f260-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5f260-230">Z listy aplikacji hello wybierz **płaska pliki**.</span><span class="sxs-lookup"><span data-stu-id="5f260-230">In hello applications list, select **Flatter Files**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_app.png) 

3. <span data-ttu-id="5f260-232">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5f260-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="5f260-234">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5f260-234">Click **Add** button.</span></span> <span data-ttu-id="5f260-235">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5f260-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="5f260-237">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5f260-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5f260-238">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5f260-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5f260-239">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5f260-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5f260-240">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5f260-240">Testing single sign-on</span></span>

<span data-ttu-id="5f260-241">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5f260-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5f260-242">Po kliknięciu powitalne płaska pliki kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour płaska pliki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5f260-242">When you click hello Flatter Files tile in hello Access Panel, you should get automatically signed-on tooyour Flatter Files application.</span></span>
<span data-ttu-id="5f260-243">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5f260-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5f260-244">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5f260-244">Additional resources</span></span>

* [<span data-ttu-id="5f260-245">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5f260-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5f260-246">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5f260-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_203.png

