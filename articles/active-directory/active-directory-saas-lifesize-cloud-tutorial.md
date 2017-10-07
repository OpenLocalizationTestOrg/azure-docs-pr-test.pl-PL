---
title: "Samouczek: Integracji Azure Active Directory z chmurą Lifesize | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i w chmurze Lifesize."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ae599907e872571b3220de7122006c7db8db4a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a><span data-ttu-id="49fd8-103">Samouczek: Integracji Azure Active Directory z chmurą Lifesize</span><span class="sxs-lookup"><span data-stu-id="49fd8-103">Tutorial: Azure Active Directory integration with Lifesize Cloud</span></span>

<span data-ttu-id="49fd8-104">Z tego samouczka, dowiesz się, jak toointegrate Lifesize chmury w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="49fd8-104">In this tutorial, you learn how toointegrate Lifesize Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="49fd8-105">Integracja z usługą Azure AD Lifesize chmury udostępnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="49fd8-105">Integrating Lifesize Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="49fd8-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooLifesize chmury</span><span class="sxs-lookup"><span data-stu-id="49fd8-106">You can control in Azure AD who has access tooLifesize Cloud</span></span>
- <span data-ttu-id="49fd8-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooLifesize chmury (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="49fd8-107">You can enable your users tooautomatically get signed-on tooLifesize Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="49fd8-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="49fd8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="49fd8-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="49fd8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49fd8-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="49fd8-110">Prerequisites</span></span>

<span data-ttu-id="49fd8-111">tooconfigure integracji usługi Azure AD z chmurą Lifesize należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="49fd8-111">tooconfigure Azure AD integration with Lifesize Cloud, you need hello following items:</span></span>

- <span data-ttu-id="49fd8-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="49fd8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="49fd8-113">Chmura Lifesize logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="49fd8-113">A Lifesize Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="49fd8-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="49fd8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="49fd8-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="49fd8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="49fd8-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="49fd8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="49fd8-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="49fd8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="49fd8-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="49fd8-118">Scenario description</span></span>
<span data-ttu-id="49fd8-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="49fd8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="49fd8-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="49fd8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="49fd8-121">Dodawanie Lifesize chmury z galerii hello</span><span class="sxs-lookup"><span data-stu-id="49fd8-121">Adding Lifesize Cloud from hello gallery</span></span>
2. <span data-ttu-id="49fd8-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="49fd8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lifesize-cloud-from-hello-gallery"></a><span data-ttu-id="49fd8-123">Dodawanie Lifesize chmury z galerii hello</span><span class="sxs-lookup"><span data-stu-id="49fd8-123">Adding Lifesize Cloud from hello gallery</span></span>
<span data-ttu-id="49fd8-124">tooconfigure hello integracji Lifesize chmury do usługi Azure AD, należy tooadd Lifesize chmury z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="49fd8-124">tooconfigure hello integration of Lifesize Cloud into Azure AD, you need tooadd Lifesize Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="49fd8-125">**tooadd Lifesize chmury z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="49fd8-125">**tooadd Lifesize Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="49fd8-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="49fd8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="49fd8-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="49fd8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="49fd8-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="49fd8-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="49fd8-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="49fd8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="49fd8-133">W polu wyszukiwania hello wpisz **chmury Lifesize**.</span><span class="sxs-lookup"><span data-stu-id="49fd8-133">In hello search box, type **Lifesize Cloud**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_search.png)

5. <span data-ttu-id="49fd8-135">W panelu wyników hello, wybierz **chmury Lifesize**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="49fd8-135">In hello results panel, select **Lifesize Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="49fd8-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="49fd8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="49fd8-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z chmurą Lifesize w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="49fd8-138">In this section, you configure and test Azure AD single sign-on with Lifesize Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="49fd8-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w chmurze Lifesize jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49fd8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lifesize Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="49fd8-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w chmurze Lifesize musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="49fd8-140">In other words, a link relationship between an Azure AD user and hello related user in Lifesize Cloud needs toobe established.</span></span>

<span data-ttu-id="49fd8-141">W chmurze Lifesize przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="49fd8-141">In Lifesize Cloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="49fd8-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z chmurą Lifesize, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="49fd8-142">tooconfigure and test Azure AD single sign-on with Lifesize Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="49fd8-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="49fd8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="49fd8-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="49fd8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="49fd8-145">**[Tworzenie użytkownika testowego chmury Lifesize](#creating-a-lifesize-cloud-test-user)**  -toohave odpowiednikiem Simona Britta w chmurze Lifesize, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="49fd8-145">**[Creating a Lifesize Cloud test user](#creating-a-lifesize-cloud-test-user)** - toohave a counterpart of Britta Simon in Lifesize Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="49fd8-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="49fd8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="49fd8-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="49fd8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="49fd8-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="49fd8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="49fd8-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w chmurze Lifesize aplikacji.</span><span class="sxs-lookup"><span data-stu-id="49fd8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lifesize Cloud application.</span></span>

<span data-ttu-id="49fd8-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z chmurą Lifesize wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="49fd8-150">**tooconfigure Azure AD single sign-on with Lifesize Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="49fd8-151">W portalu Azure na powitania hello **chmury Lifesize** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="49fd8-151">In hello Azure portal, on hello **Lifesize Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="49fd8-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="49fd8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_samlbase.png)

3. <span data-ttu-id="49fd8-155">Na powitania **adresy URL i domenę chmury Lifesize** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="49fd8-155">On hello **Lifesize Cloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url.png)

    <span data-ttu-id="49fd8-157">a.</span><span class="sxs-lookup"><span data-stu-id="49fd8-157">a.</span></span> <span data-ttu-id="49fd8-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://login.lifesizecloud.com/ls/?acs`</span><span class="sxs-lookup"><span data-stu-id="49fd8-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://login.lifesizecloud.com/ls/?acs`</span></span>

    <span data-ttu-id="49fd8-159">b.</span><span class="sxs-lookup"><span data-stu-id="49fd8-159">b.</span></span> <span data-ttu-id="49fd8-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://login.lifesizecloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="49fd8-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://login.lifesizecloud.com/<companyname>`</span></span>

     
4. <span data-ttu-id="49fd8-161">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, wykonaj powitania po kroku:</span><span class="sxs-lookup"><span data-stu-id="49fd8-161">Check **Show advanced URL settings**, perform hello following step:</span></span>  
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_url1.png)

    <span data-ttu-id="49fd8-163">W hello **przekazywania stanu** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://webapp.lifesizecloud.com/?ent=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="49fd8-163">In hello **Relay state** textbox, type a URL using hello following pattern: `https://webapp.lifesizecloud.com/?ent=<identifier>`</span></span>
   
   > [!NOTE] 
   ><span data-ttu-id="49fd8-164">Należy pamiętać, że nie są one hello wartości rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="49fd8-164">Please note that these are not hello real values.</span></span> <span data-ttu-id="49fd8-165">masz tooupdate tych wartości za pomocą hello rzeczywisty adres URL logowania, stan przekazywania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="49fd8-165">you have tooupdate these values with hello actual Sign-On URL, Relay State, and Identifier.</span></span> <span data-ttu-id="49fd8-166">Skontaktuj się z [zespołem pomocy technicznej klienta chmury Lifesize](https://www.lifesize.com/support) tooget adres URL logowania, a wartości identyfikatora i można uzyskać stanu przekazywania wartości z konfiguracji logowania jednokrotnego, który znajduje się w dalszej części samouczka hello.</span><span class="sxs-lookup"><span data-stu-id="49fd8-166">Contact [Lifesize Cloud Client support team](https://www.lifesize.com/support) tooget Sign-On URL, and Identifier values and you can get Relay State  value from SSO Configuration that is explained later in hello tutorial.</span></span>

4. <span data-ttu-id="49fd8-167">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="49fd8-167">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_certificate.png) 

5. <span data-ttu-id="49fd8-169">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="49fd8-169">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="49fd8-171">Na powitania **konfiguracji chmury Lifesize** , kliknij przycisk **Konfigurowanie chmury Lifesize** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="49fd8-171">On hello **Lifesize Cloud Configuration** section, click **Configure Lifesize Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="49fd8-172">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="49fd8-172">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_configure.png) 

7. <span data-ttu-id="49fd8-174">tooget logowania jednokrotnego skonfigurowane dla danej aplikacji, zaloguj się do hello aplikacji w chmurze Lifesize z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="49fd8-174">tooget SSO configured for your application, login into hello Lifesize Cloud application with Admin privileges.</span></span>

8. <span data-ttu-id="49fd8-175">W hello prawym górnym rogu kliknij swoją nazwę, a następnie kliknij polecenie hello **ustawienia zaawansowane**.</span><span class="sxs-lookup"><span data-stu-id="49fd8-175">In hello top right corner click on your name and then click on hello **Advance Settings**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)

9. <span data-ttu-id="49fd8-177">W powitania kliknij przycisk na powitania ustawienia zaawansowane **konfiguracji logowania jednokrotnego** łącza.</span><span class="sxs-lookup"><span data-stu-id="49fd8-177">In hello Advance Settings now click on hello **SSO Configuration** link.</span></span> <span data-ttu-id="49fd8-178">Zostanie otwarty hello strony konfiguracji logowania jednokrotnego dla swojego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="49fd8-178">It will open hello SSO Configuration page for your instance.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)

10. <span data-ttu-id="49fd8-180">Teraz skonfigurować hello następujące wartości w konfiguracji logowania jednokrotnego hello interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="49fd8-180">Now configure hello following values in hello SSO configuration UI.</span></span>    
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
    
    <span data-ttu-id="49fd8-182">a.</span><span class="sxs-lookup"><span data-stu-id="49fd8-182">a.</span></span> <span data-ttu-id="49fd8-183">W **wystawcy dostawcy tożsamości** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="49fd8-183">In **Identity Provider Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="49fd8-184">b.</span><span class="sxs-lookup"><span data-stu-id="49fd8-184">b.</span></span>  <span data-ttu-id="49fd8-185">W **adres URL logowania** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="49fd8-185">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="49fd8-186">c.</span><span class="sxs-lookup"><span data-stu-id="49fd8-186">c.</span></span> <span data-ttu-id="49fd8-187">Otwieranie certyfikatu zakodowanego base-64 w Notatniku pobrany z portalu Azure, hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu X.509** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="49fd8-187">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="49fd8-188">d.</span><span class="sxs-lookup"><span data-stu-id="49fd8-188">d.</span></span> <span data-ttu-id="49fd8-189">W hello SAML atrybutu mapowania dla pola tekstowego imię hello wprowadź wartość hello jako **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span><span class="sxs-lookup"><span data-stu-id="49fd8-189">In hello SAML Attribute mappings for hello First Name text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**</span></span>
    
    <span data-ttu-id="49fd8-190">e.</span><span class="sxs-lookup"><span data-stu-id="49fd8-190">e.</span></span> <span data-ttu-id="49fd8-191">Mapowanie atrybutu SAML powitania dla hello **nazwisko** polu tekstowym wprowadź wartość hello jako **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span><span class="sxs-lookup"><span data-stu-id="49fd8-191">In hello SAML Attribute mapping for hello **Last Name** text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**</span></span>
    
    <span data-ttu-id="49fd8-192">f.</span><span class="sxs-lookup"><span data-stu-id="49fd8-192">f.</span></span> <span data-ttu-id="49fd8-193">Mapowanie atrybutu SAML powitania dla hello **E-mail** polu tekstowym wprowadź wartość hello jako **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span><span class="sxs-lookup"><span data-stu-id="49fd8-193">In hello SAML Attribute mapping for hello **Email** text box enter hello value as **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**</span></span>

11. <span data-ttu-id="49fd8-194">Możesz kliknąć hello konfiguracji hello toocheck **testu** przycisku.</span><span class="sxs-lookup"><span data-stu-id="49fd8-194">toocheck hello configuration you can click on hello **Test** button.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="49fd8-195">Pomyślne testowania muszą Kreatora konfiguracji hello toocomplete w usłudze Azure AD, a także podać toousers dostępu lub grupy, które można wykonać hello test.</span><span class="sxs-lookup"><span data-stu-id="49fd8-195">For successful testing you need toocomplete hello configuration wizard in Azure AD and also provide access toousers or groups who can perform hello test.</span></span>

12. <span data-ttu-id="49fd8-196">Włącz hello logowania jednokrotnego, sprawdzając na powitania **włączenia logowania jednokrotnego** przycisku.</span><span class="sxs-lookup"><span data-stu-id="49fd8-196">Enable hello SSO by checking on hello **Enable SSO** button.</span></span>

13. <span data-ttu-id="49fd8-197">Teraz kliknij hello **aktualizacji** przycisk Tak, aby wszystkie ustawienia hello są zapisywane.</span><span class="sxs-lookup"><span data-stu-id="49fd8-197">Now click on hello **Update** button so that all hello settings are saved.</span></span> <span data-ttu-id="49fd8-198">Spowoduje to wygenerowanie hello RelayState wartość.</span><span class="sxs-lookup"><span data-stu-id="49fd8-198">This will generate hello RelayState value.</span></span> <span data-ttu-id="49fd8-199">Kopia hello RelayState wartość, która jest generowana w polu tekstowym hello, wklej go w hello **stan przekazywania** pole tekstowe, w obszarze **Lifesize chmury domeny i adres URL** sekcji.</span><span class="sxs-lookup"><span data-stu-id="49fd8-199">Copy hello RelayState value, which is generated in hello text box, paste it in hello **Relay State** textbox under **Lifesize Cloud Domain and URLs** section.</span></span> 

> [!TIP]
> <span data-ttu-id="49fd8-200">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="49fd8-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="49fd8-201">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="49fd8-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="49fd8-202">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="49fd8-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="49fd8-203">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="49fd8-203">Creating an Azure AD test user</span></span>

<span data-ttu-id="49fd8-204">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="49fd8-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="49fd8-206">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="49fd8-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="49fd8-207">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="49fd8-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="49fd8-209">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="49fd8-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="49fd8-211">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="49fd8-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="49fd8-213">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="49fd8-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="49fd8-215">a.</span><span class="sxs-lookup"><span data-stu-id="49fd8-215">a.</span></span> <span data-ttu-id="49fd8-216">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="49fd8-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="49fd8-217">b.</span><span class="sxs-lookup"><span data-stu-id="49fd8-217">b.</span></span> <span data-ttu-id="49fd8-218">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="49fd8-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="49fd8-219">c.</span><span class="sxs-lookup"><span data-stu-id="49fd8-219">c.</span></span> <span data-ttu-id="49fd8-220">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="49fd8-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="49fd8-221">d.</span><span class="sxs-lookup"><span data-stu-id="49fd8-221">d.</span></span> <span data-ttu-id="49fd8-222">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="49fd8-222">Click **Create**.</span></span>
 
### <a name="creating-a-lifesize-cloud-test-user"></a><span data-ttu-id="49fd8-223">Tworzenie użytkownika testowego Lifesize chmury</span><span class="sxs-lookup"><span data-stu-id="49fd8-223">Creating a Lifesize Cloud test user</span></span>

<span data-ttu-id="49fd8-224">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w chmurze Lifesize.</span><span class="sxs-lookup"><span data-stu-id="49fd8-224">In this section, you create a user called Britta Simon in Lifesize Cloud.</span></span> <span data-ttu-id="49fd8-225">Chmura Lifesize obsługę użytkowników.</span><span class="sxs-lookup"><span data-stu-id="49fd8-225">Lifesize cloud does support automatic user provisioning.</span></span> <span data-ttu-id="49fd8-226">Po pomyślnym uwierzytelnieniu w usłudze Azure AD hello użytkownika będą automatycznie udostępniane w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="49fd8-226">After successful authentication at Azure AD, hello user will be automatically provisioned in hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="49fd8-227">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="49fd8-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="49fd8-228">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooLifesize chmury.</span><span class="sxs-lookup"><span data-stu-id="49fd8-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLifesize Cloud.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="49fd8-230">**tooassign tooLifesize Simona Britta chmury, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="49fd8-230">**tooassign Britta Simon tooLifesize Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="49fd8-231">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="49fd8-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="49fd8-233">Z listy aplikacji hello wybierz **chmury Lifesize**.</span><span class="sxs-lookup"><span data-stu-id="49fd8-233">In hello applications list, select **Lifesize Cloud**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesize-cloud_app.png) 

3. <span data-ttu-id="49fd8-235">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="49fd8-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="49fd8-237">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="49fd8-237">Click **Add** button.</span></span> <span data-ttu-id="49fd8-238">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="49fd8-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="49fd8-240">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="49fd8-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="49fd8-241">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="49fd8-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="49fd8-242">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="49fd8-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="49fd8-243">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="49fd8-243">Testing single sign-on</span></span>

<span data-ttu-id="49fd8-244">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="49fd8-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="49fd8-245">Po kliknięciu hello chmury Lifesize kafelka w hello Panel dostępu, należy pobrać stronę logowania w chmurze Lifesize aplikacji.</span><span class="sxs-lookup"><span data-stu-id="49fd8-245">When you click hello Lifesize Cloud tile in hello Access Panel, you should get login page of Lifesize Cloud application.</span></span>
<span data-ttu-id="49fd8-246">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="49fd8-246">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="49fd8-247">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="49fd8-247">Additional resources</span></span>

* [<span data-ttu-id="49fd8-248">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="49fd8-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="49fd8-249">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="49fd8-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png

