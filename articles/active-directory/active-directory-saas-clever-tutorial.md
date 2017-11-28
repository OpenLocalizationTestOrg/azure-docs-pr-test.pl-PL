---
title: 'Samouczek: Integracji Azure Active Directory z Clever | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Clever."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 069ff13a-310e-4366-a147-d6ec5cca12a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 24430e1e6c750efa5787561aa151201b1fe7d428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clever"></a><span data-ttu-id="d0ab2-103">Samouczek: Integracji Azure Active Directory z Clever</span><span class="sxs-lookup"><span data-stu-id="d0ab2-103">Tutorial: Azure Active Directory integration with Clever</span></span>

<span data-ttu-id="d0ab2-104">Z tego samouczka, dowiesz się, jak toointegrate Clever w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d0ab2-104">In this tutorial, you learn how toointegrate Clever with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d0ab2-105">Integracja z usługą Azure AD Clever zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d0ab2-105">Integrating Clever with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d0ab2-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooClever.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-106">You can control in Azure AD who has access tooClever.</span></span>
- <span data-ttu-id="d0ab2-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooClever (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-107">You can enable your users tooautomatically get signed-on tooClever (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d0ab2-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="d0ab2-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d0ab2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0ab2-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d0ab2-110">Prerequisites</span></span>

<span data-ttu-id="d0ab2-111">tooconfigure integracji z usługą Azure AD z Clever należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d0ab2-111">tooconfigure Azure AD integration with Clever, you need hello following items:</span></span>

- <span data-ttu-id="d0ab2-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0ab2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d0ab2-113">Inteligentne logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d0ab2-113">A Clever single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d0ab2-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d0ab2-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d0ab2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d0ab2-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d0ab2-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d0ab2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d0ab2-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d0ab2-118">Scenario description</span></span>
<span data-ttu-id="d0ab2-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d0ab2-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d0ab2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d0ab2-121">Dodawanie Clever z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d0ab2-121">Adding Clever from hello gallery</span></span>
2. <span data-ttu-id="d0ab2-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d0ab2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clever-from-hello-gallery"></a><span data-ttu-id="d0ab2-123">Dodawanie Clever z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d0ab2-123">Adding Clever from hello gallery</span></span>
<span data-ttu-id="d0ab2-124">tooconfigure hello integracji Clever do usługi Azure AD, należy tooadd Clever z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-124">tooconfigure hello integration of Clever into Azure AD, you need tooadd Clever from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d0ab2-125">**tooadd Clever z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d0ab2-125">**tooadd Clever from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0ab2-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="d0ab2-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d0ab2-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="d0ab2-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="d0ab2-133">W polu wyszukiwania hello wpisz **Clever**, wybierz pozycję **Clever** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-133">In hello search box, type **Clever**, select **Clever** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Inteligentne hello listy wyników](./media/active-directory-saas-clever-tutorial/tutorial_clever_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d0ab2-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d0ab2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d0ab2-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Clever w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-136">In this section, you configure and test Azure AD single sign-on with Clever based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d0ab2-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Clever jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Clever is tooa user in Azure AD.</span></span> <span data-ttu-id="d0ab2-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Clever musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-138">In other words, a link relationship between an Azure AD user and hello related user in Clever needs toobe established.</span></span>

<span data-ttu-id="d0ab2-139">W Clever, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-139">In Clever, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d0ab2-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Clever, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d0ab2-140">tooconfigure and test Azure AD single sign-on with Clever, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d0ab2-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d0ab2-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d0ab2-143">**[Tworzenie użytkownika testowego inteligentne](#create-a-clever-test-user)**  -toohave odpowiednikiem Simona Britta w Clever, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-143">**[Create a Clever test user](#create-a-clever-test-user)** - toohave a counterpart of Britta Simon in Clever that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d0ab2-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d0ab2-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d0ab2-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d0ab2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d0ab2-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w inteligentne aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Clever application.</span></span>

<span data-ttu-id="d0ab2-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Clever, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d0ab2-148">**tooconfigure Azure AD single sign-on with Clever, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0ab2-149">W portalu Azure na powitania hello **Clever** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-149">In hello Azure portal, on hello **Clever** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="d0ab2-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-clever-tutorial/tutorial_clever_samlbase.png)

3. <span data-ttu-id="d0ab2-153">Na powitania **inteligentne domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d0ab2-153">On hello **Clever Domain and URLs** section, perform hello following steps:</span></span>

    ![Inteligentne domeny i adresów URL jednym informacje logowania jednokrotnego](./media/active-directory-saas-clever-tutorial/tutorial_clever_url.png)

    <span data-ttu-id="d0ab2-155">a.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-155">a.</span></span> <span data-ttu-id="d0ab2-156">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://clever.com/in/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="d0ab2-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://clever.com/in/<companyname>`</span></span>

    <span data-ttu-id="d0ab2-157">b.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-157">b.</span></span> <span data-ttu-id="d0ab2-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://clever.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="d0ab2-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://clever.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d0ab2-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-159">These values are not real.</span></span> <span data-ttu-id="d0ab2-160">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d0ab2-161">Skontaktuj się z [zespołem pomocy technicznej klienta inteligentne](https://clever.com/about/contact/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-161">Contact [Clever Client support team](https://clever.com/about/contact/) tooget these values.</span></span>

4. <span data-ttu-id="d0ab2-162">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-clever-tutorial/tutorial_clever_certificate.png)

5. <span data-ttu-id="d0ab2-164">Inteligentne aplikacji Hello oczekuje potwierdzenia SAML hello w określonym formacie wymaga tooyour mapowań atrybutów niestandardowych tooadd **atrybuty tokenu SAML** konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-164">hello Clever application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span>

    <span data-ttu-id="d0ab2-165">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-165">hello following screenshot shows an example for this.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-clever-tutorial/tutorial_clever_07.png) 

6. <span data-ttu-id="d0ab2-167">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w powyższy obraz powitania i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d0ab2-167">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="d0ab2-168">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="d0ab2-168">Attribute Name</span></span>  | <span data-ttu-id="d0ab2-169">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="d0ab2-169">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    | <span data-ttu-id="d0ab2-170">clever.student.Credentials.District\_nazwy użytkownika</span><span class="sxs-lookup"><span data-stu-id="d0ab2-170">clever.student.credentials.district\_username</span></span>  | <span data-ttu-id="d0ab2-171">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="d0ab2-171">user.userprincipalname</span></span> |
    | <span data-ttu-id="d0ab2-172">Imię</span><span class="sxs-lookup"><span data-stu-id="d0ab2-172">Firstname</span></span>  | <span data-ttu-id="d0ab2-173">User.givenName</span><span class="sxs-lookup"><span data-stu-id="d0ab2-173">user.givenname</span></span> |
    | <span data-ttu-id="d0ab2-174">nazwisko</span><span class="sxs-lookup"><span data-stu-id="d0ab2-174">Lastname</span></span>  | <span data-ttu-id="d0ab2-175">User.surname</span><span class="sxs-lookup"><span data-stu-id="d0ab2-175">user.surname</span></span> |    

    <span data-ttu-id="d0ab2-176">a.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-176">a.</span></span> <span data-ttu-id="d0ab2-177">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-clever-tutorial/tutorial_attribute_04.png)
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-clever-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="d0ab2-180">b.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-180">b.</span></span> <span data-ttu-id="d0ab2-181">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="d0ab2-182">c.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-182">c.</span></span> <span data-ttu-id="d0ab2-183">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="d0ab2-184">d.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-184">d.</span></span> <span data-ttu-id="d0ab2-185">Pozostaw hello **Namespace** puste pole tekstowe.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-185">Leave hello **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="d0ab2-186">d.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-186">d.</span></span> <span data-ttu-id="d0ab2-187">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-187">Click **Ok**.</span></span>     

5. <span data-ttu-id="d0ab2-188">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-188">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-clever-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="d0ab2-190">Witaj toogenerate **metadanych** adres url, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d0ab2-190">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="d0ab2-191">a.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-191">a.</span></span> <span data-ttu-id="d0ab2-192">Kliknij przycisk **rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-192">Click **App registrations**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-clever-tutorial/tutorial_clever_appregistrations.png)
   
    <span data-ttu-id="d0ab2-194">b.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-194">b.</span></span> <span data-ttu-id="d0ab2-195">Kliknij przycisk **punkty końcowe** tooopen **punkty końcowe** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-195">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpointicon.png)

    <span data-ttu-id="d0ab2-197">c.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-197">c.</span></span> <span data-ttu-id="d0ab2-198">Kliknij przycisk toocopy przycisku Kopiuj hello **dokument METADANYCH usług FEDERACYJNYCH** adresu url i wklej go do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-198">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpoint.png)
     
    <span data-ttu-id="d0ab2-200">d.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-200">d.</span></span> <span data-ttu-id="d0ab2-201">Teraz przejdź strony właściwości toohello **Clever** i kopiowania hello **identyfikator aplikacji** przy użyciu **kopiowania** przycisk i wklej go do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-201">Now go toohello property page of **Clever** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-clever-tutorial/tutorial_clever_appid.png)

    <span data-ttu-id="d0ab2-203">e.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-203">e.</span></span> <span data-ttu-id="d0ab2-204">Generowanie hello **adres URL metadanych** przy użyciu hello następującego wzorca:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="d0ab2-204">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>   

9. <span data-ttu-id="d0ab2-205">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy inteligentne tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-205">In a different web browser window, log in tooyour Clever company site as an administrator.</span></span>

10. <span data-ttu-id="d0ab2-206">Witaj pasku narzędzi, kliknij przycisk **błyskawicznych logowania**.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-206">In hello toolbar, click **Instant Login**.</span></span>

    <span data-ttu-id="d0ab2-207">![Logowania błyskawicznych](./media/active-directory-saas-clever-tutorial/ic798984.png "błyskawicznych logowania")</span><span class="sxs-lookup"><span data-stu-id="d0ab2-207">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798984.png "Instant Login")</span></span>

11. <span data-ttu-id="d0ab2-208">Na powitania **błyskawicznych logowania** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d0ab2-208">On hello **Instant Login** page, perform hello following steps:</span></span>
      
      <span data-ttu-id="d0ab2-209">![Logowania błyskawicznych](./media/active-directory-saas-clever-tutorial/ic798985.png "błyskawicznych logowania")</span><span class="sxs-lookup"><span data-stu-id="d0ab2-209">![Instant Login](./media/active-directory-saas-clever-tutorial/ic798985.png "Instant Login")</span></span>
      
      <span data-ttu-id="d0ab2-210">a.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-210">a.</span></span> <span data-ttu-id="d0ab2-211">Typ hello **adres URL logowania**.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-211">Type hello **Login URL**.</span></span>
      
      >[!NOTE]
      ><span data-ttu-id="d0ab2-212">Witaj **adres URL logowania** jest niestandardowa wartość.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-212">hello **Login URL** is a custom value.</span></span> <span data-ttu-id="d0ab2-213">Skontaktuj się z [zespołem pomocy technicznej klienta inteligentne](https://clever.com/about/contact/) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-213">Contact [Clever Client support team](https://clever.com/about/contact/) tooget this value.</span></span>
      
      <span data-ttu-id="d0ab2-214">b.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-214">b.</span></span> <span data-ttu-id="d0ab2-215">Jako **systemu tożsamości**, wybierz pozycję **usług AD FS**.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-215">As **Identity System**, select **ADFS**.</span></span>

      <span data-ttu-id="d0ab2-216">c.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-216">c.</span></span> <span data-ttu-id="d0ab2-217">Typ hello **adres URL metadanych** w hello **adres URL metadanych** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-217">Type hello **Metadata URL** in hello **Metadata URL** textbox.</span></span>
      
      <span data-ttu-id="d0ab2-218">d.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-218">d.</span></span> <span data-ttu-id="d0ab2-219">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-219">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d0ab2-220">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="d0ab2-220">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d0ab2-221">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-221">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d0ab2-222">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d0ab2-222">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d0ab2-223">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0ab2-223">Create an Azure AD test user</span></span>

<span data-ttu-id="d0ab2-224">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-224">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="d0ab2-226">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d0ab2-226">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0ab2-227">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-227">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-clever-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="d0ab2-229">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-229">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-clever-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="d0ab2-231">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-231">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-clever-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="d0ab2-233">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d0ab2-233">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-clever-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d0ab2-235">a.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-235">a.</span></span> <span data-ttu-id="d0ab2-236">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-236">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d0ab2-237">b.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-237">b.</span></span> <span data-ttu-id="d0ab2-238">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-238">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="d0ab2-239">c.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-239">c.</span></span> <span data-ttu-id="d0ab2-240">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-240">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="d0ab2-241">d.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-241">d.</span></span> <span data-ttu-id="d0ab2-242">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-242">Click **Create**.</span></span>
 
### <a name="create-a-clever-test-user"></a><span data-ttu-id="d0ab2-243">Tworzenie użytkownika testowego inteligentne</span><span class="sxs-lookup"><span data-stu-id="d0ab2-243">Create a Clever test user</span></span>

<span data-ttu-id="d0ab2-244">toolog użytkowników tooenable usługi Azure AD w tooClever, muszą mieć przydzielone do Clever.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-244">tooenable Azure AD users toolog in tooClever, they must be provisioned into Clever.</span></span>

<span data-ttu-id="d0ab2-245">W przypadku Clever, Praca z [zespołem pomocy technicznej klienta inteligentne](https://clever.com/about/contact/) do dodawania użytkowników hello hello inteligentne platformy.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-245">In case of Clever, Work with [Clever Client support team](https://clever.com/about/contact/) to add hello users in hello Clever platform.</span></span> <span data-ttu-id="d0ab2-246">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-246">Users must be created and activated before you use single sign-on.</span></span> 

>[!NOTE]
><span data-ttu-id="d0ab2-247">Możesz użyć innych inteligentne użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision inteligentne kont użytkowników usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-247">You can use any other Clever user account creation tools or APIs provided by Clever tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="d0ab2-248">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d0ab2-248">Assign hello Azure AD test user</span></span>

<span data-ttu-id="d0ab2-249">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooClever.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-249">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooClever.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="d0ab2-251">**tooassign tooClever Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d0ab2-251">**tooassign Britta Simon tooClever, perform hello following steps:**</span></span>

1. <span data-ttu-id="d0ab2-252">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-252">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d0ab2-254">Z listy aplikacji hello wybierz **Clever**.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-254">In hello applications list, select **Clever**.</span></span>

    ![Witaj Clever łącza na liście aplikacji hello](./media/active-directory-saas-clever-tutorial/tutorial_clever_app.png)  

3. <span data-ttu-id="d0ab2-256">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-256">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="d0ab2-258">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-258">Click **Add** button.</span></span> <span data-ttu-id="d0ab2-259">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-259">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="d0ab2-261">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-261">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d0ab2-262">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-262">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d0ab2-263">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-263">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d0ab2-264">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d0ab2-264">Test single sign-on</span></span>

<span data-ttu-id="d0ab2-265">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-265">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d0ab2-266">Po kliknięciu kafelka inteligentne hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour inteligentne aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d0ab2-266">When you click hello Clever tile in hello Access Panel, you should get automatically signed-on tooyour Clever application.</span></span>
<span data-ttu-id="d0ab2-267">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d0ab2-267">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d0ab2-268">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d0ab2-268">Additional resources</span></span>

* [<span data-ttu-id="d0ab2-269">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0ab2-269">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d0ab2-270">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d0ab2-270">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clever-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clever-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clever-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clever-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clever-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clever-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clever-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clever-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clever-tutorial/tutorial_general_203.png

