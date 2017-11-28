---
title: 'Samouczek: Integracji Azure Active Directory z myPolicies | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i myPolicies."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bf79e858-1dfb-4ab3-a6df-74b2d5a878d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: jeedes
ms.openlocfilehash: d8890457ebdb1b80e0d3126d4210e6265ae7f1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mypolicies"></a><span data-ttu-id="ce4ee-103">Samouczek: Integracji Azure Active Directory z myPolicies</span><span class="sxs-lookup"><span data-stu-id="ce4ee-103">Tutorial: Azure Active Directory integration with myPolicies</span></span>

<span data-ttu-id="ce4ee-104">Z tego samouczka, dowiesz się, jak myPolicies toointegrate w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ce4ee-104">In this tutorial, you learn how toointegrate myPolicies with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ce4ee-105">Integracja z usługą Azure AD myPolicies zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ce4ee-105">Integrating myPolicies with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ce4ee-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do toomyPolicies</span><span class="sxs-lookup"><span data-stu-id="ce4ee-106">You can control in Azure AD who has access toomyPolicies</span></span>
- <span data-ttu-id="ce4ee-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane toomyPolicies (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce4ee-107">You can enable your users tooautomatically get signed-on toomyPolicies (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ce4ee-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ce4ee-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ce4ee-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ce4ee-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce4ee-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ce4ee-110">Prerequisites</span></span>

<span data-ttu-id="ce4ee-111">tooconfigure integracji z usługą Azure AD z myPolicies należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ce4ee-111">tooconfigure Azure AD integration with myPolicies, you need hello following items:</span></span>

- <span data-ttu-id="ce4ee-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce4ee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ce4ee-113">MyPolicies logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ce4ee-113">A myPolicies single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ce4ee-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ce4ee-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ce4ee-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ce4ee-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ce4ee-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ce4ee-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ce4ee-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ce4ee-118">Scenario description</span></span>
<span data-ttu-id="ce4ee-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ce4ee-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ce4ee-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ce4ee-121">Dodawanie myPolicies z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ce4ee-121">Adding myPolicies from hello gallery</span></span>
2. <span data-ttu-id="ce4ee-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ce4ee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mypolicies-from-hello-gallery"></a><span data-ttu-id="ce4ee-123">Dodawanie myPolicies z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ce4ee-123">Adding myPolicies from hello gallery</span></span>
<span data-ttu-id="ce4ee-124">tooconfigure hello integracji myPolicies do usługi Azure AD, należy myPolicies tooadd z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-124">tooconfigure hello integration of myPolicies into Azure AD, you need tooadd myPolicies from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ce4ee-125">**myPolicies tooadd z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ce4ee-125">**tooadd myPolicies from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce4ee-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="ce4ee-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ce4ee-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ce4ee-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ce4ee-133">W polu wyszukiwania hello wpisz **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-133">In hello search box, type **myPolicies**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_search.png)

5. <span data-ttu-id="ce4ee-135">W panelu wyników hello zaznacz **myPolicies**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-135">In hello results panel, select **myPolicies**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ce4ee-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ce4ee-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ce4ee-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z myPolicies w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-138">In this section, you configure and test Azure AD single sign-on with myPolicies based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ce4ee-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w myPolicies jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in myPolicies is tooa user in Azure AD.</span></span> <span data-ttu-id="ce4ee-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w myPolicies musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-140">In other words, a link relationship between an Azure AD user and hello related user in myPolicies needs toobe established.</span></span>

<span data-ttu-id="ce4ee-141">W myPolicies, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-141">In myPolicies, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ce4ee-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z myPolicies, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ce4ee-142">tooconfigure and test Azure AD single sign-on with myPolicies, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ce4ee-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ce4ee-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ce4ee-145">**[Tworzenie użytkownika testowego myPolicies](#creating-a-mypolicies-test-user)**  -toohave odpowiednikiem Simona Britta w myPolicies, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-145">**[Creating a myPolicies test user](#creating-a-mypolicies-test-user)** - toohave a counterpart of Britta Simon in myPolicies that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ce4ee-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ce4ee-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ce4ee-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ce4ee-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ce4ee-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji myPolicies.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your myPolicies application.</span></span>

<span data-ttu-id="ce4ee-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z myPolicies, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ce4ee-150">**tooconfigure Azure AD single sign-on with myPolicies, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce4ee-151">W portalu Azure na powitania hello **myPolicies** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-151">In hello Azure portal, on hello **myPolicies** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="ce4ee-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_samlbase.png)

3. <span data-ttu-id="ce4ee-155">Na powitania **myPolicies domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ce4ee-155">On hello **myPolicies Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_url.png)

    <span data-ttu-id="ce4ee-157">a.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-157">a.</span></span> <span data-ttu-id="ce4ee-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenantname>.mypolicies.com/`</span><span class="sxs-lookup"><span data-stu-id="ce4ee-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.mypolicies.com/`</span></span>

    <span data-ttu-id="ce4ee-159">b.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-159">b.</span></span> <span data-ttu-id="ce4ee-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="ce4ee-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ce4ee-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-161">These values are not real.</span></span> <span data-ttu-id="ce4ee-162">Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="ce4ee-163">Skontaktuj się z [myPolicies obsługuje zespołu](mailto:support@mypolicies.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-163">Contact [myPolicies support team](mailto:support@mypolicies.com) tooget these values.</span></span>

4. <span data-ttu-id="ce4ee-164">Witaj myPolicies aplikacji oczekuje potwierdzenia SAML hello w określonym formacie wymaga możesz tooadd atrybutu niestandardowego mapowania tooyour SAML tokenu atrybuty konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-164">hello myPolicies application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="ce4ee-165">Skonfiguruj powitania po oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="ce4ee-166">Można zarządzać hello wartości tych atrybutów z hello "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="ce4ee-167">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-167">hello following screenshot shows an example for this.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_attribute.png)

5. <span data-ttu-id="ce4ee-169">Kliknij przycisk **widoku i edytować wszystkie atrybuty użytkowników** checkbox w hello **atrybuty użytkownika** sekcji tooexpand hello atrybutów.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-169">Click **View and edit all other user attributes** checkbox in hello **User Attributes** section tooexpand hello attributes.</span></span> <span data-ttu-id="ce4ee-170">Wykonaj następujące kroki na każdym z atrybutów hello wyświetlane - hello</span><span class="sxs-lookup"><span data-stu-id="ce4ee-170">Perform hello following steps on each of hello displayed attributes-</span></span>

    | <span data-ttu-id="ce4ee-171">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="ce4ee-171">Attribute Name</span></span> | <span data-ttu-id="ce4ee-172">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="ce4ee-172">Attribute Value</span></span> |
    | ------------------- | ---------- |
    | <span data-ttu-id="ce4ee-173">Imię</span><span class="sxs-lookup"><span data-stu-id="ce4ee-173">givenname</span></span> | <span data-ttu-id="ce4ee-174">User.givenName</span><span class="sxs-lookup"><span data-stu-id="ce4ee-174">user.givenname</span></span> |
    | <span data-ttu-id="ce4ee-175">nazwisko</span><span class="sxs-lookup"><span data-stu-id="ce4ee-175">surname</span></span> | <span data-ttu-id="ce4ee-176">User.surname</span><span class="sxs-lookup"><span data-stu-id="ce4ee-176">user.surname</span></span> |
    | <span data-ttu-id="ce4ee-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="ce4ee-177">emailaddress</span></span> | <span data-ttu-id="ce4ee-178">User.mail</span><span class="sxs-lookup"><span data-stu-id="ce4ee-178">user.mail</span></span> |
    | <span data-ttu-id="ce4ee-179">name</span><span class="sxs-lookup"><span data-stu-id="ce4ee-179">name</span></span> | <span data-ttu-id="ce4ee-180">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="ce4ee-180">user.userprincipalname</span></span> |
    
    <span data-ttu-id="ce4ee-181">a.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-181">a.</span></span> <span data-ttu-id="ce4ee-182">Polecenie hello atrybutu tooopen hello **atrybutu Edytuj** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-182">Click on hello attribute tooopen hello **Edit Attribute** dialog.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mypolicies-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="ce4ee-184">b.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-184">b.</span></span> <span data-ttu-id="ce4ee-185">Usuń wartość adresu URL hello z hello **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-185">Delete hello URL value from hello **Namespace**.</span></span>
    
    <span data-ttu-id="ce4ee-186">c.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-186">c.</span></span> <span data-ttu-id="ce4ee-187">Kliknij przycisk **Ok** toosave hello ustawienie.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-187">Click **Ok** toosave hello setting.</span></span>
    
6. <span data-ttu-id="ce4ee-188">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-188">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_certificate.png) 

7. <span data-ttu-id="ce4ee-190">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-190">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mypolicies-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ce4ee-192">Na powitania **myPolicies konfiguracji** kliknij **skonfigurować myPolicies** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-192">On hello **myPolicies Configuration** section, click **Configure myPolicies** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ce4ee-193">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="ce4ee-193">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_configure.png) 

9. <span data-ttu-id="ce4ee-195">tooconfigure rejestracji jednokrotnej w **myPolicies** strony, należy pobrać hello toosend **Certificate(Base64)** i **SAML pojedynczy znak na adres URL usługi** za[zespołu obsługi myPolicies](mailto:support@mypolicies.com).</span><span class="sxs-lookup"><span data-stu-id="ce4ee-195">tooconfigure single sign-on on **myPolicies** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** too[myPolicies support team](mailto:support@mypolicies.com).</span></span> 

> [!TIP]
> <span data-ttu-id="ce4ee-196">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="ce4ee-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ce4ee-197">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ce4ee-198">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ce4ee-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ce4ee-199">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce4ee-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="ce4ee-200">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="ce4ee-202">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ce4ee-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce4ee-203">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ce4ee-205">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ce4ee-207">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ce4ee-209">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ce4ee-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-mypolicies-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ce4ee-211">a.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-211">a.</span></span> <span data-ttu-id="ce4ee-212">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ce4ee-213">b.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-213">b.</span></span> <span data-ttu-id="ce4ee-214">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ce4ee-215">c.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-215">c.</span></span> <span data-ttu-id="ce4ee-216">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ce4ee-217">d.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-217">d.</span></span> <span data-ttu-id="ce4ee-218">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-218">Click **Create**.</span></span>
 
### <a name="creating-a-mypolicies-test-user"></a><span data-ttu-id="ce4ee-219">Tworzenie użytkownika testowego myPolicies</span><span class="sxs-lookup"><span data-stu-id="ce4ee-219">Creating a myPolicies test user</span></span>

<span data-ttu-id="ce4ee-220">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w myPolicies.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-220">In this section, you create a user called Britta Simon in myPolicies.</span></span> <span data-ttu-id="ce4ee-221">Praca z [myPolicies obsługuje zespołu](mailto:support@mypolicies.com) do dodawania użytkowników hello hello myPolicies platformy.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-221">Work with [myPolicies support team](mailto:support@mypolicies.com) to add hello users in hello myPolicies platform.</span></span> <span data-ttu-id="ce4ee-222">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-222">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ce4ee-223">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ce4ee-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ce4ee-224">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu toomyPolicies.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access toomyPolicies.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="ce4ee-226">**tooassign toomyPolicies Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ce4ee-226">**tooassign Britta Simon toomyPolicies, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce4ee-227">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ce4ee-229">Z listy aplikacji hello wybierz **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-229">In hello applications list, select **myPolicies**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-mypolicies-tutorial/tutorial_mypolicies_app.png) 

3. <span data-ttu-id="ce4ee-231">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="ce4ee-233">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-233">Click **Add** button.</span></span> <span data-ttu-id="ce4ee-234">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="ce4ee-236">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ce4ee-237">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ce4ee-238">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ce4ee-239">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ce4ee-239">Testing single sign-on</span></span>

<span data-ttu-id="ce4ee-240">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ce4ee-241">Po kliknięciu powitalne myPolicies kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour myPolicies aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ce4ee-241">When you click hello myPolicies tile in hello Access Panel, you should get automatically signed-on tooyour myPolicies application.</span></span>
<span data-ttu-id="ce4ee-242">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ce4ee-242">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ce4ee-243">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ce4ee-243">Additional resources</span></span>

* [<span data-ttu-id="ce4ee-244">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ce4ee-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ce4ee-245">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ce4ee-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mypolicies-tutorial/tutorial_general_203.png

