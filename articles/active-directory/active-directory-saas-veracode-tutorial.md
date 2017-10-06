---
title: 'Samouczek: Integracji Azure Active Directory z Veracode | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Veracode."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d17307b3864b7df8ee55f569d8f962e2e315b936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a><span data-ttu-id="0a605-103">Samouczek: Integracji Azure Active Directory z Veracode</span><span class="sxs-lookup"><span data-stu-id="0a605-103">Tutorial: Azure Active Directory integration with Veracode</span></span>

<span data-ttu-id="0a605-104">Z tego samouczka, dowiesz się, jak toointegrate Veracode w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0a605-104">In this tutorial, you learn how toointegrate Veracode with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0a605-105">Integracja z usługą Azure AD Veracode zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="0a605-105">Integrating Veracode with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0a605-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooVeracode.</span><span class="sxs-lookup"><span data-stu-id="0a605-106">You can control in Azure AD who has access tooVeracode.</span></span>
- <span data-ttu-id="0a605-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooVeracode (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a605-107">You can enable your users tooautomatically get signed-on tooVeracode (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0a605-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0a605-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="0a605-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0a605-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a605-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0a605-110">Prerequisites</span></span>

<span data-ttu-id="0a605-111">tooconfigure integracji z usługą Azure AD z Veracode należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="0a605-111">tooconfigure Azure AD integration with Veracode, you need hello following items:</span></span>

- <span data-ttu-id="0a605-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a605-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0a605-113">Veracode logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="0a605-113">A Veracode single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0a605-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="0a605-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0a605-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="0a605-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0a605-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="0a605-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0a605-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0a605-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0a605-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="0a605-118">Scenario description</span></span>
<span data-ttu-id="0a605-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="0a605-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0a605-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="0a605-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0a605-121">Dodaj Veracode z galerii hello</span><span class="sxs-lookup"><span data-stu-id="0a605-121">Add Veracode from hello gallery</span></span>
2. <span data-ttu-id="0a605-122">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0a605-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-veracode-from-hello-gallery"></a><span data-ttu-id="0a605-123">Dodaj Veracode z galerii hello</span><span class="sxs-lookup"><span data-stu-id="0a605-123">Add Veracode from hello gallery</span></span>
<span data-ttu-id="0a605-124">tooconfigure hello integracji Veracode do usługi Azure AD, należy tooadd Veracode z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="0a605-124">tooconfigure hello integration of Veracode into Azure AD, you need tooadd Veracode from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0a605-125">**tooadd Veracode z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0a605-125">**tooadd Veracode from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a605-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0a605-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="0a605-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="0a605-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0a605-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0a605-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="0a605-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0a605-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="0a605-133">W polu wyszukiwania hello wpisz **Veracode**, wybierz pozycję **Veracode** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="0a605-133">In hello search box, type **Veracode**, select  **Veracode** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Veracode hello listy wyników](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0a605-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0a605-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0a605-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Veracode w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="0a605-136">In this section, you configure and test Azure AD single sign-on with Veracode based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0a605-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Veracode jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a605-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Veracode is tooa user in Azure AD.</span></span> <span data-ttu-id="0a605-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Veracode musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="0a605-138">In other words, a link relationship between an Azure AD user and hello related user in Veracode needs toobe established.</span></span>

<span data-ttu-id="0a605-139">W Veracode, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="0a605-139">In Veracode, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0a605-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Veracode, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="0a605-140">tooconfigure and test Azure AD single sign-on with Veracode, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0a605-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="0a605-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0a605-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0a605-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0a605-143">**[Tworzenie użytkownika testowego Veracode](#create-a-veracode-test-user)**  -toohave odpowiednikiem Simona Britta w Veracode, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0a605-143">**[Create a Veracode test user](#create-a-veracode-test-user)** - toohave a counterpart of Britta Simon in Veracode that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0a605-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="0a605-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0a605-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="0a605-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0a605-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0a605-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0a605-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Veracode.</span><span class="sxs-lookup"><span data-stu-id="0a605-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Veracode application.</span></span>

<span data-ttu-id="0a605-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Veracode, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0a605-148">**tooconfigure Azure AD single sign-on with Veracode, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a605-149">W portalu Azure na powitania hello **Veracode** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="0a605-149">In hello Azure portal, on hello **Veracode** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="0a605-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="0a605-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. <span data-ttu-id="0a605-153">Na powitania **Veracode domeny i adres URL** sekcji, użytkownik nie ma tooperform wszystkie kroki jako aplikacji hello już jest wstępna Integracja z usługą Azure.</span><span class="sxs-lookup"><span data-stu-id="0a605-153">On hello **Veracode Domain and URLs** section, the user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. <span data-ttu-id="0a605-155">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="0a605-155">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. <span data-ttu-id="0a605-157">Celem Hello w tej sekcji jest toooutline jak tooenable użytkowników tooauthenticate tooVeracode do swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="0a605-157">hello objective of this section is toooutline how tooenable users tooauthenticate tooVeracode with their account in Azure AD using federation based on hello SAML protocol.</span></span>

    <span data-ttu-id="0a605-158">Aplikacja Veracode oczekuje potwierdzenia SAML hello w określonym formacie wymaga tooyour mapowań atrybutów niestandardowych tooadd **atrybuty tokenu saml** konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0a605-158">Your Veracode application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **saml token attributes** configuration.</span></span> <span data-ttu-id="0a605-159">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="0a605-159">hello following screenshot shows an example for this.</span></span>
    
    <span data-ttu-id="0a605-160">![Atrybuty](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "atrybutów")</span><span class="sxs-lookup"><span data-stu-id="0a605-160">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Attributes")</span></span>

6. <span data-ttu-id="0a605-161">Mapowanie atrybutów hello wymagane tooadd, wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0a605-161">tooadd hello required attribute mappings, perform hello following steps:</span></span>

    | <span data-ttu-id="0a605-162">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="0a605-162">Attribute Name</span></span> | <span data-ttu-id="0a605-163">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="0a605-163">Attribute Value</span></span> |
    |--- |--- |
    | <span data-ttu-id="0a605-164">Imię</span><span class="sxs-lookup"><span data-stu-id="0a605-164">firstname</span></span> |<span data-ttu-id="0a605-165">User.givenName</span><span class="sxs-lookup"><span data-stu-id="0a605-165">User.givenname</span></span> |
    | <span data-ttu-id="0a605-166">nazwisko</span><span class="sxs-lookup"><span data-stu-id="0a605-166">lastname</span></span> |<span data-ttu-id="0a605-167">User.surname</span><span class="sxs-lookup"><span data-stu-id="0a605-167">User.surname</span></span> |
    | <span data-ttu-id="0a605-168">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="0a605-168">email</span></span> |<span data-ttu-id="0a605-169">User.mail</span><span class="sxs-lookup"><span data-stu-id="0a605-169">User.mail</span></span> |
    
    <span data-ttu-id="0a605-170">a.</span><span class="sxs-lookup"><span data-stu-id="0a605-170">a.</span></span> <span data-ttu-id="0a605-171">Dla każdego wiersza danych w powyższej tabeli powitania kliknij **Dodaj atrybut użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="0a605-171">For each data row in hello table above, click **add user attribute**.</span></span>
    
    <span data-ttu-id="0a605-172">![Atrybuty](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "atrybutów")</span><span class="sxs-lookup"><span data-stu-id="0a605-172">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Attributes")</span></span>
    
    <span data-ttu-id="0a605-173">![Atrybuty](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "atrybutów")</span><span class="sxs-lookup"><span data-stu-id="0a605-173">![Attributes](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Attributes")</span></span>
    
    <span data-ttu-id="0a605-174">b.</span><span class="sxs-lookup"><span data-stu-id="0a605-174">b.</span></span> <span data-ttu-id="0a605-175">W hello **nazwa atrybutu** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="0a605-175">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="0a605-176">c.</span><span class="sxs-lookup"><span data-stu-id="0a605-176">c.</span></span> <span data-ttu-id="0a605-177">W hello **wartość atrybutu** pole tekstowe, wartość atrybutu hello wybierz wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="0a605-177">In hello **Attribute Value** textbox, select hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="0a605-178">d.</span><span class="sxs-lookup"><span data-stu-id="0a605-178">d.</span></span> <span data-ttu-id="0a605-179">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="0a605-179">Click **Ok**.</span></span>

7. <span data-ttu-id="0a605-180">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0a605-180">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="0a605-182">Na powitania **konfiguracji Veracode** kliknij **skonfigurować Veracode** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="0a605-182">On hello **Veracode Configuration** section, click **Configure Veracode** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0a605-183">Kopiuj hello **SAML identyfikator jednostki** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="0a605-183">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Konfiguracja Veracode](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. <span data-ttu-id="0a605-185">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Veracode jako administrator.</span><span class="sxs-lookup"><span data-stu-id="0a605-185">In a different web browser window, log into your Veracode company site as an administrator.</span></span>

10. <span data-ttu-id="0a605-186">W menu hello na górze hello, kliknij przycisk **ustawienia**, a następnie kliknij przycisk **administratora**.</span><span class="sxs-lookup"><span data-stu-id="0a605-186">In hello menu on hello top, click **Settings**, and then click **Admin**.</span></span>
   
    <span data-ttu-id="0a605-187">![Administracja](./media/active-directory-saas-veracode-tutorial/ic802911.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="0a605-187">![Administration](./media/active-directory-saas-veracode-tutorial/ic802911.png "Administration")</span></span>

11. <span data-ttu-id="0a605-188">Kliknij przycisk hello **SAML** kartę.</span><span class="sxs-lookup"><span data-stu-id="0a605-188">Click hello **SAML** tab.</span></span>

12. <span data-ttu-id="0a605-189">W hello **ustawienia SAML organizacji** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="0a605-189">In hello **Organization SAML Settings** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="0a605-190">![Administracja](./media/active-directory-saas-veracode-tutorial/ic802912.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="0a605-190">![Administration](./media/active-directory-saas-veracode-tutorial/ic802912.png "Administration")</span></span>
   
    <span data-ttu-id="0a605-191">a.</span><span class="sxs-lookup"><span data-stu-id="0a605-191">a.</span></span>  <span data-ttu-id="0a605-192">W **wystawcy** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0a605-192">In  **Issuer** textbox, paste hello value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="0a605-193">b.</span><span class="sxs-lookup"><span data-stu-id="0a605-193">b.</span></span> <span data-ttu-id="0a605-194">Kliknij certyfikat pobrany z portalu Azure, tooupload **wybierz plik**.</span><span class="sxs-lookup"><span data-stu-id="0a605-194">tooupload your downloaded certificate from Azure portal, click **Choose File**.</span></span>
   
    <span data-ttu-id="0a605-195">c.</span><span class="sxs-lookup"><span data-stu-id="0a605-195">c.</span></span> <span data-ttu-id="0a605-196">Wybierz **umożliwić samodzielną rejestrację**.</span><span class="sxs-lookup"><span data-stu-id="0a605-196">Select **Enable Self Registration**.</span></span>

13. <span data-ttu-id="0a605-197">W hello **ustawień rejestracji samoobsługowego** sekcji, wykonaj następujące kroki hello, a następnie kliknij przycisk **zapisać**:</span><span class="sxs-lookup"><span data-stu-id="0a605-197">In hello **Self Registration Settings** section, perform hello following steps, and then click **Save**:</span></span>
   
    <span data-ttu-id="0a605-198">![Administracja](./media/active-directory-saas-veracode-tutorial/ic802913.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="0a605-198">![Administration](./media/active-directory-saas-veracode-tutorial/ic802913.png "Administration")</span></span>
   
    <span data-ttu-id="0a605-199">a.</span><span class="sxs-lookup"><span data-stu-id="0a605-199">a.</span></span> <span data-ttu-id="0a605-200">Jako **nowe Aktywacja użytkownika**, wybierz pozycję **wymagane uaktywnienie nr**.</span><span class="sxs-lookup"><span data-stu-id="0a605-200">As **New User Activation**, select **No Activation Required**.</span></span>
   
    <span data-ttu-id="0a605-201">b.</span><span class="sxs-lookup"><span data-stu-id="0a605-201">b.</span></span> <span data-ttu-id="0a605-202">Jako **aktualizacje danych użytkownika**, wybierz pozycję **dane użytkownika Veracode preferencji**.</span><span class="sxs-lookup"><span data-stu-id="0a605-202">As **User Data Updates**, select **Preference Veracode User Data**.</span></span>
   
    <span data-ttu-id="0a605-203">c.</span><span class="sxs-lookup"><span data-stu-id="0a605-203">c.</span></span> <span data-ttu-id="0a605-204">Dla **szczegółów atrybutów SAML**, hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0a605-204">For **SAML Attribute Details**, select hello following:</span></span>
      * <span data-ttu-id="0a605-205">**Role użytkowników**</span><span class="sxs-lookup"><span data-stu-id="0a605-205">**User Roles**</span></span>
      * <span data-ttu-id="0a605-206">**Administrator zasad**</span><span class="sxs-lookup"><span data-stu-id="0a605-206">**Policy Administrator**</span></span>
      * <span data-ttu-id="0a605-207">**Osoba dokonująca przeglądu**</span><span class="sxs-lookup"><span data-stu-id="0a605-207">**Reviewer**</span></span>
      * <span data-ttu-id="0a605-208">**Realizacji zabezpieczeń**</span><span class="sxs-lookup"><span data-stu-id="0a605-208">**Security Lead**</span></span>
      * <span data-ttu-id="0a605-209">**Główna programu SMS**</span><span class="sxs-lookup"><span data-stu-id="0a605-209">**Executive**</span></span>
      * <span data-ttu-id="0a605-210">**Obiekt przesyłający**</span><span class="sxs-lookup"><span data-stu-id="0a605-210">**Submitter**</span></span>
      * <span data-ttu-id="0a605-211">**Twórcy**</span><span class="sxs-lookup"><span data-stu-id="0a605-211">**Creator**</span></span>
      * <span data-ttu-id="0a605-212">**Wszystkie typy skanowania**</span><span class="sxs-lookup"><span data-stu-id="0a605-212">**All Scan Types**</span></span>
      * <span data-ttu-id="0a605-213">**Członkostwo zespołu**</span><span class="sxs-lookup"><span data-stu-id="0a605-213">**Team Memberships**</span></span>
      * <span data-ttu-id="0a605-214">**Domyślny zespół**</span><span class="sxs-lookup"><span data-stu-id="0a605-214">**Default Team**</span></span>

> [!TIP]
> <span data-ttu-id="0a605-215">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="0a605-215">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0a605-216">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="0a605-216">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0a605-217">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0a605-217">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0a605-218">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a605-218">Create an Azure AD test user</span></span>

<span data-ttu-id="0a605-219">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="0a605-219">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="0a605-221">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0a605-221">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a605-222">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0a605-222">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="0a605-224">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="0a605-224">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="0a605-226">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="0a605-226">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="0a605-228">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0a605-228">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    <span data-ttu-id="0a605-230">a.</span><span class="sxs-lookup"><span data-stu-id="0a605-230">a.</span></span> <span data-ttu-id="0a605-231">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0a605-231">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0a605-232">b.</span><span class="sxs-lookup"><span data-stu-id="0a605-232">b.</span></span> <span data-ttu-id="0a605-233">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0a605-233">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="0a605-234">c.</span><span class="sxs-lookup"><span data-stu-id="0a605-234">c.</span></span> <span data-ttu-id="0a605-235">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="0a605-235">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="0a605-236">d.</span><span class="sxs-lookup"><span data-stu-id="0a605-236">d.</span></span> <span data-ttu-id="0a605-237">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0a605-237">Click **Create**.</span></span>
 
### <a name="create-a-veracode-test-user"></a><span data-ttu-id="0a605-238">Tworzenie użytkownika testowego Veracode</span><span class="sxs-lookup"><span data-stu-id="0a605-238">Create a Veracode test user</span></span>
<span data-ttu-id="0a605-239">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do Veracode muszą mieć przydzielone do Veracode.</span><span class="sxs-lookup"><span data-stu-id="0a605-239">In order tooenable Azure AD users toolog into Veracode, they must be provisioned into Veracode.</span></span> <span data-ttu-id="0a605-240">W przypadku hello Veracode Inicjowanie obsługi to zadanie automatyczne.</span><span class="sxs-lookup"><span data-stu-id="0a605-240">In hello case of Veracode, provisioning is an automated task.</span></span> <span data-ttu-id="0a605-241">Nie ma elementu akcji dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="0a605-241">There is no action item for you.</span></span> <span data-ttu-id="0a605-242">Użytkownicy są tworzone automatycznie w razie potrzeby podczas hello pierwszej pojedynczego logowania jednokrotnego próby.</span><span class="sxs-lookup"><span data-stu-id="0a605-242">Users are automatically created if necessary during hello first single sign-on attempt.</span></span>

> [!NOTE]
> <span data-ttu-id="0a605-243">Możesz użyć innych Veracode użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Veracode tooprovision kont użytkowników usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a605-243">You can use any other Veracode user account creation tools or APIs provided by Veracode tooprovision Azure AD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="0a605-244">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a605-244">Assign hello Azure AD test user</span></span>

<span data-ttu-id="0a605-245">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooVeracode.</span><span class="sxs-lookup"><span data-stu-id="0a605-245">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooVeracode.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="0a605-247">**tooassign tooVeracode Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="0a605-247">**tooassign Britta Simon tooVeracode, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a605-248">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0a605-248">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="0a605-250">Z listy aplikacji hello wybierz **Veracode**.</span><span class="sxs-lookup"><span data-stu-id="0a605-250">In hello applications list, select **Veracode**.</span></span>

    ![łącze Veracode Hello na liście aplikacji hello](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. <span data-ttu-id="0a605-252">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="0a605-252">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="0a605-254">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0a605-254">Click **Add** button.</span></span> <span data-ttu-id="0a605-255">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0a605-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="0a605-257">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0a605-257">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0a605-258">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0a605-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0a605-259">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0a605-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0a605-260">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0a605-260">Test single sign-on</span></span>

<span data-ttu-id="0a605-261">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="0a605-261">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0a605-262">Po kliknięciu kafelka Veracode hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Veracode aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0a605-262">When you click hello Veracode tile in hello Access Panel, you should get automatically signed-on tooyour Veracode application.</span></span>
<span data-ttu-id="0a605-263">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0a605-263">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0a605-264">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="0a605-264">Additional resources</span></span>

* [<span data-ttu-id="0a605-265">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a605-265">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0a605-266">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0a605-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png

