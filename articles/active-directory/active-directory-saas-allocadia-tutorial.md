---
title: 'Samouczek: Integracji Azure Active Directory z Allocadia | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Allocadia."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c415fc55-6dc1-49f2-a8a2-2fc6e3790d65
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: jeedes
ms.openlocfilehash: 9a01c232f9dc50e690dd348430899db9c13f1564
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-allocadia"></a><span data-ttu-id="2b2fd-103">Samouczek: Integracji Azure Active Directory z Allocadia</span><span class="sxs-lookup"><span data-stu-id="2b2fd-103">Tutorial: Azure Active Directory integration with Allocadia</span></span>

<span data-ttu-id="2b2fd-104">Z tego samouczka, dowiesz się, jak toointegrate Allocadia w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2b2fd-104">In this tutorial, you learn how toointegrate Allocadia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2b2fd-105">Integracja z usługą Azure AD Allocadia zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="2b2fd-105">Integrating Allocadia with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2b2fd-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooAllocadia</span><span class="sxs-lookup"><span data-stu-id="2b2fd-106">You can control in Azure AD who has access tooAllocadia</span></span>
- <span data-ttu-id="2b2fd-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAllocadia (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b2fd-107">You can enable your users tooautomatically get signed-on tooAllocadia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2b2fd-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="2b2fd-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2b2fd-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2b2fd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b2fd-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2b2fd-110">Prerequisites</span></span>

<span data-ttu-id="2b2fd-111">tooconfigure integracji z usługą Azure AD z Allocadia należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="2b2fd-111">tooconfigure Azure AD integration with Allocadia, you need hello following items:</span></span>

- <span data-ttu-id="2b2fd-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b2fd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2b2fd-113">Allocadia jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2b2fd-113">An Allocadia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2b2fd-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2b2fd-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="2b2fd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2b2fd-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2b2fd-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2b2fd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2b2fd-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="2b2fd-118">Scenario description</span></span>
<span data-ttu-id="2b2fd-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2b2fd-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="2b2fd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2b2fd-121">Dodawanie Allocadia z galerii hello</span><span class="sxs-lookup"><span data-stu-id="2b2fd-121">Adding Allocadia from hello gallery</span></span>
2. <span data-ttu-id="2b2fd-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="2b2fd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-allocadia-from-hello-gallery"></a><span data-ttu-id="2b2fd-123">Dodawanie Allocadia z galerii hello</span><span class="sxs-lookup"><span data-stu-id="2b2fd-123">Adding Allocadia from hello gallery</span></span>
<span data-ttu-id="2b2fd-124">tooconfigure hello integracji Allocadia do usługi Azure AD, należy tooadd Allocadia z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-124">tooconfigure hello integration of Allocadia into Azure AD, you need tooadd Allocadia from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2b2fd-125">**tooadd Allocadia z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="2b2fd-125">**tooadd Allocadia from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b2fd-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="2b2fd-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2b2fd-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="2b2fd-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="2b2fd-133">W polu wyszukiwania hello wpisz **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-133">In hello search box, type **Allocadia**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_search.png)

5. <span data-ttu-id="2b2fd-135">W panelu wyników hello zaznacz **Allocadia**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-135">In hello results panel, select **Allocadia**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2b2fd-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="2b2fd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2b2fd-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Allocadia na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="2b2fd-138">In this section, you configure and test Azure AD single sign-on with Allocadia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2b2fd-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Allocadia jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Allocadia is tooa user in Azure AD.</span></span> <span data-ttu-id="2b2fd-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Allocadia musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-140">In other words, a link relationship between an Azure AD user and hello related user in Allocadia needs toobe established.</span></span>

<span data-ttu-id="2b2fd-141">W Allocadia, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-141">In Allocadia, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2b2fd-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Allocadia, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="2b2fd-142">tooconfigure and test Azure AD single sign-on with Allocadia, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2b2fd-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2b2fd-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2b2fd-145">**[Tworzenie użytkownika testowego Allocadia](#creating-an-allocadia-test-user)**  -toohave odpowiednikiem Simona Britta w Allocadia, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-145">**[Creating an Allocadia test user](#creating-an-allocadia-test-user)** - toohave a counterpart of Britta Simon in Allocadia that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2b2fd-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2b2fd-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2b2fd-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2b2fd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2b2fd-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Allocadia.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Allocadia application.</span></span>

<span data-ttu-id="2b2fd-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Allocadia, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="2b2fd-150">**tooconfigure Azure AD single sign-on with Allocadia, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b2fd-151">W portalu Azure na powitania hello **Allocadia** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-151">In hello Azure portal, on hello **Allocadia** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="2b2fd-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_samlbase.png)

3. <span data-ttu-id="2b2fd-155">Na powitania **Allocadia domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="2b2fd-155">On hello **Allocadia Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_url.png)

    <span data-ttu-id="2b2fd-157">a.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-157">a.</span></span> <span data-ttu-id="2b2fd-158">W hello **identyfikator** tekstowym, wpisz adres URL przy użyciu następującego hello wzorców:</span><span class="sxs-lookup"><span data-stu-id="2b2fd-158">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
       
     <span data-ttu-id="2b2fd-159">Dla środowiska testowego-`https://na2standby.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="2b2fd-159">For test environment -  `https://na2standby.allocadia.com`</span></span>
    
     <span data-ttu-id="2b2fd-160">W środowisku produkcyjnym —`https://na2.allocadia.com`</span><span class="sxs-lookup"><span data-stu-id="2b2fd-160">For production environment - `https://na2.allocadia.com`</span></span>

    <span data-ttu-id="2b2fd-161">b.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-161">b.</span></span> <span data-ttu-id="2b2fd-162">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL przy użyciu następującego hello wzorców:</span><span class="sxs-lookup"><span data-stu-id="2b2fd-162">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 
    
     <span data-ttu-id="2b2fd-163">Dla środowiska testowego-`https://na2standby.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="2b2fd-163">For test environment - `https://na2standby.allocadia.com/allocadia/saml/SSO`</span></span>
    
     <span data-ttu-id="2b2fd-164">W środowisku produkcyjnym —`https://na2.allocadia.com/allocadia/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="2b2fd-164">For production environment - `https://na2.allocadia.com/allocadia/saml/SSO`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2b2fd-165">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-165">These values are not real.</span></span> <span data-ttu-id="2b2fd-166">Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-166">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="2b2fd-167">Skontaktuj się z [zespołem pomocy technicznej Allocadia](mailTo:support@allocadia.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-167">Contact [Allocadia support team](mailTo:support@allocadia.com) tooget these values.</span></span>

4. <span data-ttu-id="2b2fd-168">Aplikacja Allocadia oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-168">Allocadia application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="2b2fd-169">Skonfiguruj powitania po oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-169">Configure hello following claims for this application.</span></span> <span data-ttu-id="2b2fd-170">Można zarządzać hello wartości tych atrybutów z hello "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-170">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="2b2fd-171">powitania po zrzut ekranu przedstawia przykład dla tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-171">hello following screenshot shows an example for this configuration.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_attributes.png)
    
5. <span data-ttu-id="2b2fd-173">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie hello i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="2b2fd-173">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="2b2fd-174">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="2b2fd-174">Attribute Name</span></span> | <span data-ttu-id="2b2fd-175">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="2b2fd-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="2b2fd-176">Imię</span><span class="sxs-lookup"><span data-stu-id="2b2fd-176">firstname</span></span> | <span data-ttu-id="2b2fd-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="2b2fd-177">user.givenname</span></span> |
    | <span data-ttu-id="2b2fd-178">nazwisko</span><span class="sxs-lookup"><span data-stu-id="2b2fd-178">lastname</span></span> | <span data-ttu-id="2b2fd-179">User.surname</span><span class="sxs-lookup"><span data-stu-id="2b2fd-179">user.surname</span></span> |
    | <span data-ttu-id="2b2fd-180">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="2b2fd-180">email</span></span> | <span data-ttu-id="2b2fd-181">User.mail</span><span class="sxs-lookup"><span data-stu-id="2b2fd-181">user.mail</span></span> |
    
    <span data-ttu-id="2b2fd-182">a.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-182">a.</span></span> <span data-ttu-id="2b2fd-183">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-183">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="2b2fd-185">b.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-185">b.</span></span> <span data-ttu-id="2b2fd-186">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-186">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-allocadia-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="2b2fd-188">c.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-188">c.</span></span> <span data-ttu-id="2b2fd-189">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-189">From hello **Value** list, type hello attribute value shown for that row.</span></span>
 
    <span data-ttu-id="2b2fd-190">d.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-190">d.</span></span> <span data-ttu-id="2b2fd-191">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-191">Click **Ok**.</span></span>



6. <span data-ttu-id="2b2fd-192">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-192">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_certificate.png) 


7. <span data-ttu-id="2b2fd-194">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-194">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-allocadia-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="2b2fd-196">tooconfigure rejestracji jednokrotnej w **Allocadia** strony, należy pobrać hello toosend **XML metadanych** za[zespołem pomocy technicznej Allocadia](mailTo:support@allocadia.com).</span><span class="sxs-lookup"><span data-stu-id="2b2fd-196">tooconfigure single sign-on on **Allocadia** side, you need toosend hello downloaded **Metadata XML** too[Allocadia support team](mailTo:support@allocadia.com).</span></span> <span data-ttu-id="2b2fd-197">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-197">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="2b2fd-198">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="2b2fd-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2b2fd-199">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2b2fd-200">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2b2fd-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2b2fd-201">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b2fd-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="2b2fd-202">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="2b2fd-204">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="2b2fd-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b2fd-205">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2b2fd-207">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2b2fd-209">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2b2fd-211">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="2b2fd-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-allocadia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2b2fd-213">a.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-213">a.</span></span> <span data-ttu-id="2b2fd-214">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2b2fd-215">b.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-215">b.</span></span> <span data-ttu-id="2b2fd-216">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2b2fd-217">c.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-217">c.</span></span> <span data-ttu-id="2b2fd-218">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2b2fd-219">d.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-219">d.</span></span> <span data-ttu-id="2b2fd-220">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-220">Click **Create**.</span></span>
 
### <a name="creating-an-allocadia-test-user"></a><span data-ttu-id="2b2fd-221">Tworzenie użytkownika testowego Allocadia</span><span class="sxs-lookup"><span data-stu-id="2b2fd-221">Creating an Allocadia test user</span></span>

<span data-ttu-id="2b2fd-222">Aplikacja obsługuje tylko w czasie Inicjowanie obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-222">Application supports Just in time user provisioning.</span></span> <span data-ttu-id="2b2fd-223">Po uwierzytelnieniu użytkownicy są automatycznie tworzone w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-223">After authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2b2fd-224">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b2fd-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2b2fd-225">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooAllocadia.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAllocadia.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="2b2fd-227">**tooassign tooAllocadia Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="2b2fd-227">**tooassign Britta Simon tooAllocadia, perform hello following steps:**</span></span>

1. <span data-ttu-id="2b2fd-228">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="2b2fd-230">Z listy aplikacji hello wybierz **Allocadia**.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-230">In hello applications list, select **Allocadia**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-allocadia-tutorial/tutorial_allocadia_app.png) 

3. <span data-ttu-id="2b2fd-232">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="2b2fd-234">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-234">Click **Add** button.</span></span> <span data-ttu-id="2b2fd-235">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="2b2fd-237">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2b2fd-238">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2b2fd-239">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2b2fd-240">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="2b2fd-240">Testing single sign-on</span></span>

<span data-ttu-id="2b2fd-241">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2b2fd-242">Po kliknięciu kafelka Allocadia hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Allocadia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2b2fd-242">When you click hello Allocadia tile in hello Access Panel, you should get automatically signed-on tooyour Allocadia application.</span></span>
<span data-ttu-id="2b2fd-243">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="2b2fd-243">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2b2fd-244">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="2b2fd-244">Additional resources</span></span>

* [<span data-ttu-id="2b2fd-245">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b2fd-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2b2fd-246">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2b2fd-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-allocadia-tutorial/tutorial_general_203.png

