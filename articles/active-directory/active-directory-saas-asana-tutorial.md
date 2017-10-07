---
title: 'Samouczek: Integracji Azure Active Directory z Asana | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Asana."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 837e38fe-8f55-475c-87f4-6394dc1fee2b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: jeedes
ms.openlocfilehash: 9ac35dedc809b2b3dfb461d92a5afb066ccdedde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asana"></a><span data-ttu-id="ce596-103">Samouczek: Integracji Azure Active Directory z Asana</span><span class="sxs-lookup"><span data-stu-id="ce596-103">Tutorial: Azure Active Directory integration with Asana</span></span>

<span data-ttu-id="ce596-104">Z tego samouczka, dowiesz się, jak toointegrate Asana w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ce596-104">In this tutorial, you learn how toointegrate Asana with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ce596-105">Integracja z usługą Azure AD Asana zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ce596-105">Integrating Asana with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ce596-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooAsana</span><span class="sxs-lookup"><span data-stu-id="ce596-106">You can control in Azure AD who has access tooAsana</span></span>
- <span data-ttu-id="ce596-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAsana (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce596-107">You can enable your users tooautomatically get signed-on tooAsana (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ce596-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ce596-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ce596-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ce596-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce596-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ce596-110">Prerequisites</span></span>

<span data-ttu-id="ce596-111">tooconfigure integracji z usługą Azure AD z Asana należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ce596-111">tooconfigure Azure AD integration with Asana, you need hello following items:</span></span>

- <span data-ttu-id="ce596-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce596-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ce596-113">Asana jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ce596-113">An Asana single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ce596-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ce596-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ce596-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ce596-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ce596-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ce596-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ce596-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ce596-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ce596-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ce596-118">Scenario description</span></span>
<span data-ttu-id="ce596-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ce596-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ce596-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ce596-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ce596-121">Dodawanie Asana z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ce596-121">Adding Asana from hello gallery</span></span>
2. <span data-ttu-id="ce596-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ce596-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asana-from-hello-gallery"></a><span data-ttu-id="ce596-123">Dodawanie Asana z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ce596-123">Adding Asana from hello gallery</span></span>
<span data-ttu-id="ce596-124">tooconfigure hello integracji Asana do usługi Azure AD, należy tooadd Asana z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ce596-124">tooconfigure hello integration of Asana into Azure AD, you need tooadd Asana from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ce596-125">**tooadd Asana z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ce596-125">**tooadd Asana from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce596-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ce596-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="ce596-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ce596-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ce596-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ce596-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="ce596-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ce596-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="ce596-133">W polu wyszukiwania hello wpisz **Asana**, wybierz pozycję **Asana** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ce596-133">In hello search box, type **Asana**, select **Asana** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-asana-tutorial/tutorial_asana_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ce596-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ce596-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="ce596-136">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Asana na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="ce596-136">In this section, you configure and test Azure AD single sign-on with Asana based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ce596-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Asana jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce596-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Asana is tooa user in Azure AD.</span></span> <span data-ttu-id="ce596-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Asana musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="ce596-138">In other words, a link relationship between an Azure AD user and hello related user in Asana needs toobe established.</span></span>

<span data-ttu-id="ce596-139">W Asana, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="ce596-139">In Asana, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ce596-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Asana, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ce596-140">tooconfigure and test Azure AD single sign-on with Asana, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ce596-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ce596-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ce596-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ce596-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ce596-143">**[Tworzenie użytkownika testowego Asana](#create-an-asana-test-user)**  -toohave odpowiednikiem Simona Britta w Asana, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ce596-143">**[Create an Asana test user](#create-an-asana-test-user)** - toohave a counterpart of Britta Simon in Asana that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ce596-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ce596-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ce596-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="ce596-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ce596-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ce596-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ce596-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Asana.</span><span class="sxs-lookup"><span data-stu-id="ce596-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Asana application.</span></span>

<span data-ttu-id="ce596-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Asana, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ce596-148">**tooconfigure Azure AD single sign-on with Asana, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce596-149">W portalu Azure na powitania hello **Asana** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ce596-149">In hello Azure portal, on hello **Asana** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="ce596-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ce596-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-asana-tutorial/tutorial_asana_samlbase.png)

3. <span data-ttu-id="ce596-153">Na powitania **Asana domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ce596-153">On hello **Asana Domain and URLs** section, perform hello following steps:</span></span>

    ![Adresy URL i domeny Asana pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-asana-tutorial/tutorial_asana_url.png)

    <span data-ttu-id="ce596-155">a.</span><span class="sxs-lookup"><span data-stu-id="ce596-155">a.</span></span> <span data-ttu-id="ce596-156">W hello **adres URL logowania** pole tekstowe, wprowadź adres URL:`https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="ce596-156">In hello **Sign-on URL** textbox, type URL: `https://app.asana.com/`</span></span>

    <span data-ttu-id="ce596-157">b.</span><span class="sxs-lookup"><span data-stu-id="ce596-157">b.</span></span> <span data-ttu-id="ce596-158">W hello **identyfikator** pole tekstowe, wartość typu:`https://app.asana.com/`</span><span class="sxs-lookup"><span data-stu-id="ce596-158">In hello **Identifier** textbox, type value: `https://app.asana.com/`</span></span>
 
4. <span data-ttu-id="ce596-159">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ce596-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-asana-tutorial/tutorial_asana_certificate.png)
    
5. <span data-ttu-id="ce596-161">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ce596-161">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-asana-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ce596-163">Na powitania **konfiguracji Asana** kliknij **skonfigurować Asana** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="ce596-163">On hello **Asana Configuration** section, click **Configure Asana** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ce596-164">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="ce596-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfiguracja Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_configure.png) 

7. <span data-ttu-id="ce596-166">W oknie innej przeglądarki, logowania jednokrotnego tooyour Asana aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ce596-166">In a different browser window, sign-on tooyour Asana application.</span></span> <span data-ttu-id="ce596-167">Logowanie Jednokrotne w Asana, ustawień dostępu hello obszaru roboczego, klikając nazwę obszaru roboczego hello na powitania prawym górnym rogu ekranu hello tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="ce596-167">tooconfigure SSO in Asana, access hello workspace settings by clicking hello workspace name on hello top right corner of hello screen.</span></span> <span data-ttu-id="ce596-168">Następnie kliknij  **\<nazwa obszaru roboczego\> ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="ce596-168">Then, click on **\<your workspace name\> Settings**.</span></span> 
   
    ![Ustawienia logowania jednokrotnego Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_09.png)

8. <span data-ttu-id="ce596-170">Na powitania **ustawienia organizacji** okna, kliknij przycisk **administracji**.</span><span class="sxs-lookup"><span data-stu-id="ce596-170">On hello **Organization settings** window, click **Administration**.</span></span> <span data-ttu-id="ce596-171">Następnie kliknij przycisk **elementów członkowskich należy zalogować się za pośrednictwem SAML** tooenable hello logowania jednokrotnego konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ce596-171">Then, click **Members must log in via SAML** tooenable hello SSO configuration.</span></span> <span data-ttu-id="ce596-172">Witaj wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ce596-172">hello perform hello following steps:</span></span>
   
    ![Skonfiguruj ustawienia organizacji rejestracji jednokrotnej](./media/active-directory-saas-asana-tutorial/tutorial_asana_10.png)  

     <span data-ttu-id="ce596-174">a.</span><span class="sxs-lookup"><span data-stu-id="ce596-174">a.</span></span> <span data-ttu-id="ce596-175">W hello **adres URL logowania strony** pole tekstowe, Wklej hello **SAML pojedynczy znak na adres URL usługi**.</span><span class="sxs-lookup"><span data-stu-id="ce596-175">In hello **Sign-in page URL** textbox, paste hello **SAML Single Sign-On Service URL**.</span></span>

     <span data-ttu-id="ce596-176">b.</span><span class="sxs-lookup"><span data-stu-id="ce596-176">b.</span></span> <span data-ttu-id="ce596-177">Kliknij prawym przyciskiem myszy certyfikat hello pobrany z portalu Azure, a następnie otwórz plik certyfikatu hello Notatniku lub w edytorze tekstów preferowany.</span><span class="sxs-lookup"><span data-stu-id="ce596-177">Right click hello certificate downloaded from Azure portal, then open hello certificate file using Notepad or your preferred text editor.</span></span> <span data-ttu-id="ce596-178">Kopiowanie zawartości hello między hello begin i hello zakończenia certyfikatów tytułu i wklej go w hello **certyfikatu X.509** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="ce596-178">Copy hello content between hello begin and hello end certificate title and paste it in hello **X.509 Certificate** textbox.</span></span>

9. <span data-ttu-id="ce596-179">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ce596-179">Click **Save**.</span></span> <span data-ttu-id="ce596-180">Przejdź za[Asana przewodnik konfigurowania rejestracji Jednokrotnej](https://asana.com/guide/help/premium/authentication#gl-saml) Jeœli potrzebujesz dodatkowej pomocy.</span><span class="sxs-lookup"><span data-stu-id="ce596-180">Go too[Asana guide for setting up SSO](https://asana.com/guide/help/premium/authentication#gl-saml) if you need further assistance.</span></span>

> [!TIP]
> <span data-ttu-id="ce596-181">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="ce596-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ce596-182">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="ce596-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ce596-183">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ce596-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ce596-184">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce596-184">Create an Azure AD test user</span></span>

<span data-ttu-id="ce596-185">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="ce596-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="ce596-187">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ce596-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce596-188">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ce596-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-asana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ce596-190">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ce596-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-asana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ce596-192">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ce596-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-asana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ce596-194">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ce596-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![przycisk Dodaj Hello](./media/active-directory-saas-asana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ce596-196">a.</span><span class="sxs-lookup"><span data-stu-id="ce596-196">a.</span></span> <span data-ttu-id="ce596-197">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ce596-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ce596-198">b.</span><span class="sxs-lookup"><span data-stu-id="ce596-198">b.</span></span> <span data-ttu-id="ce596-199">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ce596-199">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ce596-200">c.</span><span class="sxs-lookup"><span data-stu-id="ce596-200">c.</span></span> <span data-ttu-id="ce596-201">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="ce596-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ce596-202">d.</span><span class="sxs-lookup"><span data-stu-id="ce596-202">d.</span></span> <span data-ttu-id="ce596-203">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ce596-203">Click **Create**.</span></span>
 
### <a name="create-an-asana-test-user"></a><span data-ttu-id="ce596-204">Tworzenie użytkownika testowego Asana</span><span class="sxs-lookup"><span data-stu-id="ce596-204">Create an Asana test user</span></span>

<span data-ttu-id="ce596-205">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Asana.</span><span class="sxs-lookup"><span data-stu-id="ce596-205">In this section, you create a user called Britta Simon in Asana.</span></span>

1. <span data-ttu-id="ce596-206">Na **Asana**, przejdź toohello **zespołów** sekcji na powitania lewego panelu.</span><span class="sxs-lookup"><span data-stu-id="ce596-206">On **Asana**, go toohello **Teams** section on hello left panel.</span></span> <span data-ttu-id="ce596-207">Kliknij przycisk hello oraz przycisk Zaloguj.</span><span class="sxs-lookup"><span data-stu-id="ce596-207">Click hello plus sign button.</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-asana-tutorial/tutorial_asana_12.png) 

2. <span data-ttu-id="ce596-209">Wpisz wiadomość hello e-mail britta.simon@contoso.com w hello pola tekstowego, a następnie wybierz **zaprosić**.</span><span class="sxs-lookup"><span data-stu-id="ce596-209">Type hello email britta.simon@contoso.com in hello text box and then select **Invite**.</span></span>

3. <span data-ttu-id="ce596-210">Kliknij przycisk **wysłać zaproszenie**.</span><span class="sxs-lookup"><span data-stu-id="ce596-210">Click **Send Invite**.</span></span> <span data-ttu-id="ce596-211">Witaj nowy użytkownik otrzyma wiadomość e-mail na swoje konto e-mail.</span><span class="sxs-lookup"><span data-stu-id="ce596-211">hello new user will receive an email into her email account.</span></span> <span data-ttu-id="ce596-212">Użytkownik należy toocreate a sprawdzania hello konta.</span><span class="sxs-lookup"><span data-stu-id="ce596-212">She will need toocreate and validate hello account.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ce596-213">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce596-213">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ce596-214">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooAsana.</span><span class="sxs-lookup"><span data-stu-id="ce596-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAsana.</span></span>

![Przypisanie roli użytkownika hello][200]

<span data-ttu-id="ce596-216">**tooassign tooAsana Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ce596-216">**tooassign Britta Simon tooAsana, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce596-217">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ce596-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ce596-219">Z listy aplikacji hello wybierz **Asana**.</span><span class="sxs-lookup"><span data-stu-id="ce596-219">In hello applications list, select **Asana**.</span></span>

    ![łącze Asana Hello na liście aplikacji hello](./media/active-directory-saas-asana-tutorial/tutorial_asana_app.png) 

3. <span data-ttu-id="ce596-221">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ce596-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="ce596-223">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ce596-223">Click **Add** button.</span></span> <span data-ttu-id="ce596-224">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ce596-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="ce596-226">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ce596-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ce596-227">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ce596-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ce596-228">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ce596-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ce596-229">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ce596-229">Test single sign-on</span></span>

<span data-ttu-id="ce596-230">Celem Hello w tej sekcji jest tootest programu Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ce596-230">hello objective of this section is tootest your Azure AD single sign-on.</span></span>

<span data-ttu-id="ce596-231">Przejdź na stronę logowania tooAsana.</span><span class="sxs-lookup"><span data-stu-id="ce596-231">Go tooAsana login page.</span></span> <span data-ttu-id="ce596-232">W polu tekstowym Adres E-mail hello, Wstaw adres e-mail hello britta.simon@contoso.com. Pozostaw pole tekstowe hasła hello w puste, a następnie kliknij przycisk **dziennika w**.</span><span class="sxs-lookup"><span data-stu-id="ce596-232">In hello Email address textbox, insert hello email address britta.simon@contoso.com. Leave hello password textbox in blank and then click **Log In**.</span></span> <span data-ttu-id="ce596-233">Będzie przekierowany tooAzure AD strony logowania.</span><span class="sxs-lookup"><span data-stu-id="ce596-233">You will be redirected tooAzure AD login page.</span></span> <span data-ttu-id="ce596-234">Ukończ poświadczeń usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce596-234">Complete your Azure AD credentials.</span></span> <span data-ttu-id="ce596-235">Teraz użytkownik jest zalogowany na Asana.</span><span class="sxs-lookup"><span data-stu-id="ce596-235">Now, you are logged in on Asana.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ce596-236">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ce596-236">Additional resources</span></span>

* [<span data-ttu-id="ce596-237">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ce596-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ce596-238">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ce596-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-asana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asana-tutorial/tutorial_general_203.png
[10]: ./media/active-directory-saas-asana-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-asana-tutorial/tutorial_general_070.png
