---
title: 'Samouczek: Integracji Azure Active Directory z Moxtra | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Moxtra."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 82e2fcc390ba508e86a3992ec1c81d0a0ffed96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a><span data-ttu-id="eb74d-103">Samouczek: Integracji Azure Active Directory z Moxtra</span><span class="sxs-lookup"><span data-stu-id="eb74d-103">Tutorial: Azure Active Directory integration with Moxtra</span></span>

<span data-ttu-id="eb74d-104">Z tego samouczka, dowiesz się, jak toointegrate Moxtra w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eb74d-104">In this tutorial, you learn how toointegrate Moxtra with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eb74d-105">Integracja z usługą Azure AD Moxtra zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="eb74d-105">Integrating Moxtra with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eb74d-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooMoxtra</span><span class="sxs-lookup"><span data-stu-id="eb74d-106">You can control in Azure AD who has access tooMoxtra</span></span>
- <span data-ttu-id="eb74d-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooMoxtra (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb74d-107">You can enable your users tooautomatically get signed-on tooMoxtra (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eb74d-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="eb74d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="eb74d-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eb74d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb74d-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="eb74d-110">Prerequisites</span></span>

<span data-ttu-id="eb74d-111">tooconfigure integracji z usługą Azure AD z Moxtra należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="eb74d-111">tooconfigure Azure AD integration with Moxtra, you need hello following items:</span></span>

- <span data-ttu-id="eb74d-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb74d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eb74d-113">Moxtra logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="eb74d-113">A Moxtra single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eb74d-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="eb74d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eb74d-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="eb74d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eb74d-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="eb74d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eb74d-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eb74d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eb74d-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="eb74d-118">Scenario description</span></span>
<span data-ttu-id="eb74d-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="eb74d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eb74d-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="eb74d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eb74d-121">Dodawanie Moxtra z galerii hello</span><span class="sxs-lookup"><span data-stu-id="eb74d-121">Adding Moxtra from hello gallery</span></span>
2. <span data-ttu-id="eb74d-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="eb74d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moxtra-from-hello-gallery"></a><span data-ttu-id="eb74d-123">Dodawanie Moxtra z galerii hello</span><span class="sxs-lookup"><span data-stu-id="eb74d-123">Adding Moxtra from hello gallery</span></span>
<span data-ttu-id="eb74d-124">tooconfigure hello integracji Moxtra do usługi Azure AD, należy tooadd Moxtra z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="eb74d-124">tooconfigure hello integration of Moxtra into Azure AD, you need tooadd Moxtra from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eb74d-125">**tooadd Moxtra z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="eb74d-125">**tooadd Moxtra from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb74d-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="eb74d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="eb74d-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="eb74d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eb74d-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="eb74d-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="eb74d-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eb74d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="eb74d-133">W polu wyszukiwania hello wpisz **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="eb74d-133">In hello search box, type **Moxtra**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. <span data-ttu-id="eb74d-135">W panelu wyników hello zaznacz **Moxtra**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="eb74d-135">In hello results panel, select **Moxtra**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eb74d-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="eb74d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eb74d-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Moxtra w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="eb74d-138">In this section, you configure and test Azure AD single sign-on with Moxtra based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="eb74d-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Moxtra jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb74d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Moxtra is tooa user in Azure AD.</span></span> <span data-ttu-id="eb74d-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Moxtra musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="eb74d-140">In other words, a link relationship between an Azure AD user and hello related user in Moxtra needs toobe established.</span></span>

<span data-ttu-id="eb74d-141">W Moxtra, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="eb74d-141">In Moxtra, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="eb74d-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Moxtra, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="eb74d-142">tooconfigure and test Azure AD single sign-on with Moxtra, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eb74d-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="eb74d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eb74d-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="eb74d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eb74d-145">**[Tworzenie użytkownika testowego Moxtra](#creating-a-moxtra-test-user)**  -toohave odpowiednikiem Simona Britta w Moxtra, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="eb74d-145">**[Creating a Moxtra test user](#creating-a-moxtra-test-user)** - toohave a counterpart of Britta Simon in Moxtra that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="eb74d-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="eb74d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eb74d-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="eb74d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eb74d-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="eb74d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eb74d-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Moxtra.</span><span class="sxs-lookup"><span data-stu-id="eb74d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Moxtra application.</span></span>

<span data-ttu-id="eb74d-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Moxtra, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="eb74d-150">**tooconfigure Azure AD single sign-on with Moxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb74d-151">W portalu Azure na powitania hello **Moxtra** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="eb74d-151">In hello Azure portal, on hello **Moxtra** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="eb74d-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="eb74d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. <span data-ttu-id="eb74d-155">Na powitania **Moxtra domeny i adres URL** sekcji, wykonaj powitania po kroku:</span><span class="sxs-lookup"><span data-stu-id="eb74d-155">On hello **Moxtra Domain and URLs** section, perform hello following step:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    <span data-ttu-id="eb74d-157">W hello **adres URL logowania** tekstowym, wpisz adres URL jako:`https://www.moxtra.com/service/#login`</span><span class="sxs-lookup"><span data-stu-id="eb74d-157">In hello **Sign-on URL** textbox, type a URL as: `https://www.moxtra.com/service/#login`</span></span>

4. <span data-ttu-id="eb74d-158">Aplikacja Moxtra oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="eb74d-158">Moxtra application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="eb74d-159">Skonfiguruj powitania po oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eb74d-159">Configure hello following claims for this application.</span></span> <span data-ttu-id="eb74d-160">Można zarządzać hello wartości tych atrybutów z hello "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eb74d-160">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="eb74d-161">powitania po zrzut ekranu przedstawia przykład dla tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="eb74d-161">hello following screenshot shows an example for this configuration.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. <span data-ttu-id="eb74d-163">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie hello i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="eb74d-163">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="eb74d-164">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="eb74d-164">Attribute Name</span></span> | <span data-ttu-id="eb74d-165">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="eb74d-165">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="eb74d-166">Imię</span><span class="sxs-lookup"><span data-stu-id="eb74d-166">firstname</span></span> | <span data-ttu-id="eb74d-167">User.givenName</span><span class="sxs-lookup"><span data-stu-id="eb74d-167">user.givenname</span></span> |
    | <span data-ttu-id="eb74d-168">nazwisko</span><span class="sxs-lookup"><span data-stu-id="eb74d-168">lastname</span></span> | <span data-ttu-id="eb74d-169">User.surname</span><span class="sxs-lookup"><span data-stu-id="eb74d-169">user.surname</span></span> |
    | <span data-ttu-id="eb74d-170">idpid</span><span class="sxs-lookup"><span data-stu-id="eb74d-170">idpid</span></span>    | <span data-ttu-id="eb74d-171">< Identyfikator jednostki SAML ></span><span class="sxs-lookup"><span data-stu-id="eb74d-171">< SAML Entity ID ></span></span> 

    > [!Note]
    > <span data-ttu-id="eb74d-172">Witaj wartość **idpid** atrybut nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="eb74d-172">hello value of **idpid** attribute is not real.</span></span> <span data-ttu-id="eb74d-173">Można uzyskać wartość rzeczywista hello z **krótkimi opisami** w obszarze **Moxtra konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="eb74d-173">You can get hello actual value from **Quick reference** section under **Moxtra Configuration**.</span></span>
    
    <span data-ttu-id="eb74d-174">a.</span><span class="sxs-lookup"><span data-stu-id="eb74d-174">a.</span></span> <span data-ttu-id="eb74d-175">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eb74d-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="eb74d-177">b.</span><span class="sxs-lookup"><span data-stu-id="eb74d-177">b.</span></span> <span data-ttu-id="eb74d-178">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="eb74d-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="eb74d-180">c.</span><span class="sxs-lookup"><span data-stu-id="eb74d-180">c.</span></span> <span data-ttu-id="eb74d-181">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="eb74d-181">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="eb74d-182">d.</span><span class="sxs-lookup"><span data-stu-id="eb74d-182">d.</span></span> <span data-ttu-id="eb74d-183">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="eb74d-183">Click **Ok**.</span></span>
    
5. <span data-ttu-id="eb74d-184">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="eb74d-184">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. <span data-ttu-id="eb74d-186">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="eb74d-186">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="eb74d-188">Na powitania **konfiguracji Moxtra** kliknij **skonfigurować Moxtra** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="eb74d-188">On hello **Moxtra Configuration** section, click **Configure Moxtra** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="eb74d-189">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="eb74d-189">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. <span data-ttu-id="eb74d-191">W innym oknie przeglądarki Zaloguj się w witrynie firmy Moxtra tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="eb74d-191">In another browser window, sign on tooyour Moxtra company site as an administrator.</span></span>

9. <span data-ttu-id="eb74d-192">Na powitania narzędzi po lewej stronie powitania kliknij **konsoli administracyjnej > SAML logowania jednokrotnego**, a następnie kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="eb74d-192">In hello toolbar on hello left, click **Admin Console > SAML Single Sign-on**, and then click **New**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. <span data-ttu-id="eb74d-194">Na powitania **SAML** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="eb74d-194">On hello **SAML** page, perform hello following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    <span data-ttu-id="eb74d-196">a.</span><span class="sxs-lookup"><span data-stu-id="eb74d-196">a.</span></span> <span data-ttu-id="eb74d-197">W hello **nazwa** tekstowym, wpisz nazwę konfiguracji (np.: *SAML*).</span><span class="sxs-lookup"><span data-stu-id="eb74d-197">In hello **Name** textbox, type a name for your configuration (e.g.: *SAML*).</span></span> 
  
    <span data-ttu-id="eb74d-198">b.</span><span class="sxs-lookup"><span data-stu-id="eb74d-198">b.</span></span> <span data-ttu-id="eb74d-199">W hello **identyfikator jednostki IdP** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="eb74d-199">In hello **IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="eb74d-200">c.</span><span class="sxs-lookup"><span data-stu-id="eb74d-200">c.</span></span> <span data-ttu-id="eb74d-201">W **adres URL logowania** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="eb74d-201">In **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="eb74d-202">d.</span><span class="sxs-lookup"><span data-stu-id="eb74d-202">d.</span></span> <span data-ttu-id="eb74d-203">W hello **AuthnContextClassRef** pole tekstowe, typ **urn: oasis: nazwy: tc: SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="eb74d-203">In hello **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span> 
 
    <span data-ttu-id="eb74d-204">e.</span><span class="sxs-lookup"><span data-stu-id="eb74d-204">e.</span></span> <span data-ttu-id="eb74d-205">W hello **NameID Format** pole tekstowe, typ **urn: oasis: nazwy: tc: SAML:1.1:nameid-format: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="eb74d-205">In hello **NameID Format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span> 
 
    <span data-ttu-id="eb74d-206">f.</span><span class="sxs-lookup"><span data-stu-id="eb74d-206">f.</span></span> <span data-ttu-id="eb74d-207">Otwórz certyfikat, który został pobrany z portalu Azure w programie Notatnik, skopiuj zawartość hello i wkleić go do hello **certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="eb74d-207">Open certificate which you have downloaded from Azure portal in notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span>    
 
    <span data-ttu-id="eb74d-208">g.</span><span class="sxs-lookup"><span data-stu-id="eb74d-208">g.</span></span> <span data-ttu-id="eb74d-209">W hello SAML e-mail domeny tekstowym wpisz domenę poczty e-mail SAML.</span><span class="sxs-lookup"><span data-stu-id="eb74d-209">In hello SAML email domain textbox, type your SAML email domain.</span></span>    
  
    >[!NOTE]
    ><span data-ttu-id="eb74d-210">toosee hello kroki tooverify hello domeny, kliknij przycisk hello "**i**" poniżej.</span><span class="sxs-lookup"><span data-stu-id="eb74d-210">toosee hello steps tooverify hello domain, click hello "**i**" below.</span></span>

    <span data-ttu-id="eb74d-211">h.</span><span class="sxs-lookup"><span data-stu-id="eb74d-211">h.</span></span> <span data-ttu-id="eb74d-212">Kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="eb74d-212">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="eb74d-213">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="eb74d-213">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="eb74d-214">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="eb74d-214">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="eb74d-215">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eb74d-215">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eb74d-216">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb74d-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="eb74d-217">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="eb74d-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="eb74d-219">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="eb74d-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb74d-220">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="eb74d-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eb74d-222">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="eb74d-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eb74d-224">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eb74d-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eb74d-226">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="eb74d-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eb74d-228">a.</span><span class="sxs-lookup"><span data-stu-id="eb74d-228">a.</span></span> <span data-ttu-id="eb74d-229">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eb74d-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eb74d-230">b.</span><span class="sxs-lookup"><span data-stu-id="eb74d-230">b.</span></span> <span data-ttu-id="eb74d-231">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eb74d-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eb74d-232">c.</span><span class="sxs-lookup"><span data-stu-id="eb74d-232">c.</span></span> <span data-ttu-id="eb74d-233">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="eb74d-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="eb74d-234">d.</span><span class="sxs-lookup"><span data-stu-id="eb74d-234">d.</span></span> <span data-ttu-id="eb74d-235">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="eb74d-235">Click **Create**.</span></span>
 
### <a name="creating-a-moxtra-test-user"></a><span data-ttu-id="eb74d-236">Tworzenie użytkownika testowego Moxtra</span><span class="sxs-lookup"><span data-stu-id="eb74d-236">Creating a Moxtra test user</span></span>

<span data-ttu-id="eb74d-237">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Moxtra.</span><span class="sxs-lookup"><span data-stu-id="eb74d-237">hello objective of this section is toocreate a user called Britta Simon in Moxtra.</span></span>

<span data-ttu-id="eb74d-238">**toocreate użytkownika o nazwie Simona Britta w Moxtra, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="eb74d-238">**toocreate a user called Britta Simon in Moxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb74d-239">Rejestracja tooyour Moxtra witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="eb74d-239">Sign on tooyour Moxtra company site as an administrator.</span></span>

2. <span data-ttu-id="eb74d-240">Na powitania narzędzi po lewej stronie powitania kliknij **konsoli administracyjnej > Zarządzanie użytkownikami**, a następnie **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="eb74d-240">In hello toolbar on hello left, click **Admin Console > User Management**, and then **Add User**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. <span data-ttu-id="eb74d-242">Na powitania **Dodaj użytkownika** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="eb74d-242">On hello **Add User** dialog, perform hello following steps:</span></span>
  
    <span data-ttu-id="eb74d-243">a.</span><span class="sxs-lookup"><span data-stu-id="eb74d-243">a.</span></span> <span data-ttu-id="eb74d-244">W hello **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="eb74d-244">In hello **First Name** textbox, type **Britta**.</span></span>
  
    <span data-ttu-id="eb74d-245">b.</span><span class="sxs-lookup"><span data-stu-id="eb74d-245">b.</span></span> <span data-ttu-id="eb74d-246">W hello **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="eb74d-246">In hello **Last Name** textbox, type **Simon**.</span></span>
  
    <span data-ttu-id="eb74d-247">c.</span><span class="sxs-lookup"><span data-stu-id="eb74d-247">c.</span></span> <span data-ttu-id="eb74d-248">W hello **E-mail** tekstowym, wpisz adres e-mail firmy Britta identyczny z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="eb74d-248">In hello **Email** textbox, type Britta's email address same as on Azure portal.</span></span>
  
    <span data-ttu-id="eb74d-249">d.</span><span class="sxs-lookup"><span data-stu-id="eb74d-249">d.</span></span> <span data-ttu-id="eb74d-250">W hello **dzielenia** pole tekstowe, typ **deweloperów**.</span><span class="sxs-lookup"><span data-stu-id="eb74d-250">In hello **Division** textbox, type **Dev**.</span></span>
  
    <span data-ttu-id="eb74d-251">e.</span><span class="sxs-lookup"><span data-stu-id="eb74d-251">e.</span></span> <span data-ttu-id="eb74d-252">W hello **działu** pole tekstowe, typ **IT**.</span><span class="sxs-lookup"><span data-stu-id="eb74d-252">In hello **Department** textbox, type **IT**.</span></span>
  
    <span data-ttu-id="eb74d-253">f.</span><span class="sxs-lookup"><span data-stu-id="eb74d-253">f.</span></span> <span data-ttu-id="eb74d-254">Wybierz **administratora**.</span><span class="sxs-lookup"><span data-stu-id="eb74d-254">Select **Administrator**.</span></span>
  
    <span data-ttu-id="eb74d-255">g.</span><span class="sxs-lookup"><span data-stu-id="eb74d-255">g.</span></span> <span data-ttu-id="eb74d-256">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="eb74d-256">Click **Add**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="eb74d-257">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb74d-257">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="eb74d-258">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooMoxtra.</span><span class="sxs-lookup"><span data-stu-id="eb74d-258">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMoxtra.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="eb74d-260">**tooassign tooMoxtra Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="eb74d-260">**tooassign Britta Simon tooMoxtra, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb74d-261">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="eb74d-261">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="eb74d-263">Z listy aplikacji hello wybierz **Moxtra**.</span><span class="sxs-lookup"><span data-stu-id="eb74d-263">In hello applications list, select **Moxtra**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. <span data-ttu-id="eb74d-265">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="eb74d-265">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="eb74d-267">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="eb74d-267">Click **Add** button.</span></span> <span data-ttu-id="eb74d-268">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eb74d-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="eb74d-270">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="eb74d-270">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eb74d-271">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eb74d-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eb74d-272">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eb74d-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eb74d-273">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="eb74d-273">Testing single sign-on</span></span>

<span data-ttu-id="eb74d-274">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="eb74d-274">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="eb74d-275">Po kliknięciu kafelka Moxtra hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Moxtra aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eb74d-275">When you click hello Moxtra tile in hello Access Panel, you should get automatically signed-on tooyour Moxtra application.</span></span>
<span data-ttu-id="eb74d-276">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="eb74d-276">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eb74d-277">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="eb74d-277">Additional resources</span></span>

* [<span data-ttu-id="eb74d-278">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eb74d-278">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eb74d-279">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="eb74d-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

