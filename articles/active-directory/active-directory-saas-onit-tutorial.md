---
title: 'Samouczek: Integracji Azure Active Directory z Onit | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Onit."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: bc479a28-8fcd-493f-ac53-681975a5149c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 9e12449e5bf7f169b3cadfaa12438ac5d52ed8f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-onit"></a><span data-ttu-id="e8e19-103">Samouczek: Integracji Azure Active Directory z Onit</span><span class="sxs-lookup"><span data-stu-id="e8e19-103">Tutorial: Azure Active Directory integration with Onit</span></span>

<span data-ttu-id="e8e19-104">Z tego samouczka, dowiesz się, jak toointegrate Onit w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e8e19-104">In this tutorial, you learn how toointegrate Onit with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e8e19-105">Integracja z usługą Azure AD Onit zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e8e19-105">Integrating Onit with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e8e19-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooOnit.</span><span class="sxs-lookup"><span data-stu-id="e8e19-106">You can control in Azure AD who has access tooOnit.</span></span>
- <span data-ttu-id="e8e19-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooOnit (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8e19-107">You can enable your users tooautomatically get signed-on tooOnit (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e8e19-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e8e19-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="e8e19-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e8e19-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8e19-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e8e19-110">Prerequisites</span></span>

<span data-ttu-id="e8e19-111">tooconfigure integracji z usługą Azure AD z Onit należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e8e19-111">tooconfigure Azure AD integration with Onit, you need hello following items:</span></span>

- <span data-ttu-id="e8e19-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8e19-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e8e19-113">Onit logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e8e19-113">An Onit single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e8e19-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e8e19-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e8e19-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="e8e19-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e8e19-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e8e19-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e8e19-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e8e19-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e8e19-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="e8e19-118">Scenario description</span></span>

<span data-ttu-id="e8e19-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="e8e19-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e8e19-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="e8e19-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e8e19-121">Dodawanie Onit z galerii hello</span><span class="sxs-lookup"><span data-stu-id="e8e19-121">Adding Onit from hello gallery</span></span>
2. <span data-ttu-id="e8e19-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e8e19-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-onit-from-hello-gallery"></a><span data-ttu-id="e8e19-123">Dodawanie Onit z galerii hello</span><span class="sxs-lookup"><span data-stu-id="e8e19-123">Adding Onit from hello gallery</span></span>
<span data-ttu-id="e8e19-124">tooconfigure hello integracji Onit do usługi Azure AD, należy tooadd Onit z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="e8e19-124">tooconfigure hello integration of Onit into Azure AD, you need tooadd Onit from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e8e19-125">**tooadd Onit z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e8e19-125">**tooadd Onit from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8e19-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e8e19-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="e8e19-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e8e19-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e8e19-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e8e19-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="e8e19-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e8e19-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="e8e19-133">W polu wyszukiwania hello wpisz **Onit**, wybierz pozycję **Onit** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="e8e19-133">In hello search box, type **Onit**, select **Onit** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Onit hello listy wyników](./media/active-directory-saas-onit-tutorial/tutorial_onit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e8e19-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e8e19-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e8e19-136">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Onit na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="e8e19-136">In this section, you configure and test Azure AD single sign-on with Onit based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e8e19-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Onit jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8e19-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Onit is tooa user in Azure AD.</span></span> <span data-ttu-id="e8e19-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Onit musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="e8e19-138">In other words, a link relationship between an Azure AD user and hello related user in Onit needs toobe established.</span></span>

<span data-ttu-id="e8e19-139">W Onit, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="e8e19-139">In Onit, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e8e19-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Onit, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="e8e19-140">tooconfigure and test Azure AD single sign-on with Onit, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e8e19-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e8e19-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e8e19-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e8e19-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e8e19-143">**[Tworzenie użytkownika testowego Onit](#create-an-onit-test-user)**  -toohave odpowiednikiem Simona Britta w Onit, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e8e19-143">**[Create an Onit test user](#create-an-onit-test-user)** - toohave a counterpart of Britta Simon in Onit that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e8e19-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e8e19-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e8e19-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="e8e19-145">**[Test single sign-on](#test-single-sign-on)** tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e8e19-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e8e19-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e8e19-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Onit.</span><span class="sxs-lookup"><span data-stu-id="e8e19-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Onit application.</span></span>

<span data-ttu-id="e8e19-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Onit, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e8e19-148">**tooconfigure Azure AD single sign-on with Onit, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8e19-149">W portalu Azure na powitania hello **Onit** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e8e19-149">In hello Azure portal, on hello **Onit** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="e8e19-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e8e19-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-onit-tutorial/tutorial_onit_samlbase.png)

3. <span data-ttu-id="e8e19-153">Na powitania **Onit domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="e8e19-153">On hello **Onit Domain and URLs** section, perform hello following steps:</span></span>

    ![Adresy URL i domeny onit pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-onit-tutorial/tutorial_onit_url.png)

    <span data-ttu-id="e8e19-155">a.</span><span class="sxs-lookup"><span data-stu-id="e8e19-155">a.</span></span> <span data-ttu-id="e8e19-156">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="e8e19-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<sub-domain>.onit.com`</span></span>

    <span data-ttu-id="e8e19-157">b.</span><span class="sxs-lookup"><span data-stu-id="e8e19-157">b.</span></span> <span data-ttu-id="e8e19-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<sub-domain>.onit.com`</span><span class="sxs-lookup"><span data-stu-id="e8e19-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<sub-domain>.onit.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e8e19-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="e8e19-159">These values are not real.</span></span> <span data-ttu-id="e8e19-160">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="e8e19-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e8e19-161">Skontaktuj się z [zespołem pomocy technicznej klienta Onit](https://www.onit.com/support) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="e8e19-161">Contact [Onit Client support team](https://www.onit.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="e8e19-162">Na powitania **certyfikat podpisywania SAML** hello kopiowania, sekcji **odcisk PALCA** wartości certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="e8e19-162">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-onit-tutorial/tutorial_onit_certificate.png) 

5. <span data-ttu-id="e8e19-164">Aplikacja onit oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="e8e19-164">Onit application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="e8e19-165">Skonfiguruj powitania po oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e8e19-165">Please configure hello following claims for this application.</span></span> <span data-ttu-id="e8e19-166">Można zarządzać hello wartości tych atrybutów z hello **"Atrribute"** kartę aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e8e19-166">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="e8e19-167">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="e8e19-167">hello following screenshot shows an example for this.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-onit-tutorial/tutorial_onit_attribute.png) 

6. <span data-ttu-id="e8e19-169">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie hello i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e8e19-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="e8e19-170">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="e8e19-170">Attribute Name</span></span> | <span data-ttu-id="e8e19-171">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="e8e19-171">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="e8e19-172">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="e8e19-172">email</span></span> | <span data-ttu-id="e8e19-173">User.mail</span><span class="sxs-lookup"><span data-stu-id="e8e19-173">user.mail</span></span> |
    
    <span data-ttu-id="e8e19-174">a.</span><span class="sxs-lookup"><span data-stu-id="e8e19-174">a.</span></span> <span data-ttu-id="e8e19-175">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e8e19-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-onit-tutorial/tutorial_attribute_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-onit-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="e8e19-178">b.</span><span class="sxs-lookup"><span data-stu-id="e8e19-178">b.</span></span> <span data-ttu-id="e8e19-179">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="e8e19-179">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="e8e19-180">c.</span><span class="sxs-lookup"><span data-stu-id="e8e19-180">c.</span></span> <span data-ttu-id="e8e19-181">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="e8e19-181">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="e8e19-182">d.</span><span class="sxs-lookup"><span data-stu-id="e8e19-182">d.</span></span> <span data-ttu-id="e8e19-183">Pozostaw hello **Namespace** puste.</span><span class="sxs-lookup"><span data-stu-id="e8e19-183">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="e8e19-184">e.</span><span class="sxs-lookup"><span data-stu-id="e8e19-184">e.</span></span> <span data-ttu-id="e8e19-185">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8e19-185">Click **Ok**.</span></span>

7. <span data-ttu-id="e8e19-186">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e8e19-186">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-onit-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="e8e19-188">Na powitania **konfiguracji Onit** kliknij **skonfigurować Onit** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="e8e19-188">On hello **Onit Configuration** section, click **Configure Onit** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e8e19-189">Kopiuj hello **Sign-Out adres URL, SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="e8e19-189">Copy hello **Sign-Out URL, SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfiguracja onit](./media/active-directory-saas-onit-tutorial/tutorial_onit_configure.png)

9. <span data-ttu-id="e8e19-191">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Onit jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e8e19-191">In a different web browser window, log into your Onit company site as an administrator.</span></span>

10. <span data-ttu-id="e8e19-192">W menu hello na górze hello, kliknij przycisk **administracji**.</span><span class="sxs-lookup"><span data-stu-id="e8e19-192">In hello menu on hello top, click **Administration**.</span></span>
   
   <span data-ttu-id="e8e19-193">![Administracja](./media/active-directory-saas-onit-tutorial/IC791174.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="e8e19-193">![Administration](./media/active-directory-saas-onit-tutorial/IC791174.png "Administration")</span></span>
11. <span data-ttu-id="e8e19-194">Kliknij przycisk **Corporation edycji**.</span><span class="sxs-lookup"><span data-stu-id="e8e19-194">Click **Edit Corporation**.</span></span>
   
   <span data-ttu-id="e8e19-195">![Edytuj Corporation](./media/active-directory-saas-onit-tutorial/IC791175.png "Corporation edycji")</span><span class="sxs-lookup"><span data-stu-id="e8e19-195">![Edit Corporation](./media/active-directory-saas-onit-tutorial/IC791175.png "Edit Corporation")</span></span>
   
12. <span data-ttu-id="e8e19-196">Kliknij przycisk hello **zabezpieczeń** kartę.</span><span class="sxs-lookup"><span data-stu-id="e8e19-196">Click hello **Security** tab.</span></span>
    
    <span data-ttu-id="e8e19-197">![Informacje o firmie edycji](./media/active-directory-saas-onit-tutorial/IC791176.png "informacji o firmie edycji")</span><span class="sxs-lookup"><span data-stu-id="e8e19-197">![Edit Company Information](./media/active-directory-saas-onit-tutorial/IC791176.png "Edit Company Information")</span></span>

13. <span data-ttu-id="e8e19-198">Na powitania **zabezpieczeń** karcie, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="e8e19-198">On hello **Security** tab, perform hello following steps:</span></span>

    <span data-ttu-id="e8e19-199">![Logowanie jednokrotne](./media/active-directory-saas-onit-tutorial/IC791177.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="e8e19-199">![Single Sign-On](./media/active-directory-saas-onit-tutorial/IC791177.png "Single Sign-On")</span></span>

    <span data-ttu-id="e8e19-200">a.</span><span class="sxs-lookup"><span data-stu-id="e8e19-200">a.</span></span> <span data-ttu-id="e8e19-201">Jako **strategii uwierzytelniania**, wybierz pozycję **rejestracji jednokrotnej i hasło**.</span><span class="sxs-lookup"><span data-stu-id="e8e19-201">As **Authentication Strategy**, select **Single Sign On and Password**.</span></span>
    
    <span data-ttu-id="e8e19-202">b.</span><span class="sxs-lookup"><span data-stu-id="e8e19-202">b.</span></span> <span data-ttu-id="e8e19-203">W **Idp docelowy adres URL** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e8e19-203">In **Idp Target URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e8e19-204">c.</span><span class="sxs-lookup"><span data-stu-id="e8e19-204">c.</span></span> <span data-ttu-id="e8e19-205">W **adresu URL wylogowania Idp** pole tekstowe, Wklej hello wartość **Sign-Out URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e8e19-205">In **Idp logout URL** textbox, paste hello value of  **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e8e19-206">d.</span><span class="sxs-lookup"><span data-stu-id="e8e19-206">d.</span></span> <span data-ttu-id="e8e19-207">W **odcisk palca certyfikatu Idp (SHA1)** pole tekstowe, Wklej hello **odcisk palca** wartość certyfikatów, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e8e19-207">In **Idp Cert Fingerprint (SHA1)** textbox, paste hello  **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="e8e19-208">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="e8e19-208">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e8e19-209">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="e8e19-209">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e8e19-210">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e8e19-210">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e8e19-211">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8e19-211">Create an Azure AD test user</span></span>

<span data-ttu-id="e8e19-212">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="e8e19-212">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="e8e19-214">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e8e19-214">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8e19-215">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e8e19-215">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-onit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e8e19-217">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="e8e19-217">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-onit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e8e19-219">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="e8e19-219">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-onit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e8e19-221">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e8e19-221">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-onit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e8e19-223">a.</span><span class="sxs-lookup"><span data-stu-id="e8e19-223">a.</span></span> <span data-ttu-id="e8e19-224">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e8e19-224">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e8e19-225">b.</span><span class="sxs-lookup"><span data-stu-id="e8e19-225">b.</span></span> <span data-ttu-id="e8e19-226">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e8e19-226">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="e8e19-227">c.</span><span class="sxs-lookup"><span data-stu-id="e8e19-227">c.</span></span> <span data-ttu-id="e8e19-228">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="e8e19-228">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="e8e19-229">d.</span><span class="sxs-lookup"><span data-stu-id="e8e19-229">d.</span></span> <span data-ttu-id="e8e19-230">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e8e19-230">Click **Create**.</span></span>
 
### <a name="create-an-onit-test-user"></a><span data-ttu-id="e8e19-231">Tworzenie użytkownika testowego Onit</span><span class="sxs-lookup"><span data-stu-id="e8e19-231">Create an Onit test user</span></span>

<span data-ttu-id="e8e19-232">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do Onit muszą mieć przydzielone do Onit.</span><span class="sxs-lookup"><span data-stu-id="e8e19-232">In order tooenable Azure AD users toolog into Onit, they must be provisioned into Onit.</span></span>  

<span data-ttu-id="e8e19-233">W przypadku hello Onit Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="e8e19-233">In hello case of Onit, provisioning is a manual task.</span></span>

<span data-ttu-id="e8e19-234">**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e8e19-234">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8e19-235">Zaloguj się na tooyour **Onit** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e8e19-235">Sign on tooyour **Onit** company site as an administrator.</span></span>
2. <span data-ttu-id="e8e19-236">Kliknij przycisk **dodać użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="e8e19-236">Click **Add User**.</span></span>
   
   <span data-ttu-id="e8e19-237">![Administracja](./media/active-directory-saas-onit-tutorial/IC791180.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="e8e19-237">![Administration](./media/active-directory-saas-onit-tutorial/IC791180.png "Administration")</span></span>
3. <span data-ttu-id="e8e19-238">Na powitania **Dodaj użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e8e19-238">On hello **Add User** dialog page, perform hello following steps:</span></span>
   
   <span data-ttu-id="e8e19-239">![Dodaj użytkownika](./media/active-directory-saas-onit-tutorial/IC791181.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="e8e19-239">![Add User](./media/active-directory-saas-onit-tutorial/IC791181.png "Add User")</span></span>
   
  1. <span data-ttu-id="e8e19-240">Hello typu **nazwa** i hello **adres E-mail** prawidłowy Azure AD konta tooprovision do hello związane z pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="e8e19-240">Type hello **Name** and hello **Email Address** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span>
  2. <span data-ttu-id="e8e19-241">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e8e19-241">Click **Create**.</span></span>    
   
 > [!NOTE]
 > <span data-ttu-id="e8e19-242">Właściciel konta usługi Azure Active Directory Hello otrzymuje wiadomość e-mail i następuje tooconfirm łącze swojego konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="e8e19-242">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e8e19-243">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8e19-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e8e19-244">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooOnit.</span><span class="sxs-lookup"><span data-stu-id="e8e19-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOnit.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="e8e19-246">**tooassign tooOnit Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e8e19-246">**tooassign Britta Simon tooOnit, perform hello following steps:**</span></span>

1. <span data-ttu-id="e8e19-247">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e8e19-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="e8e19-249">Z listy aplikacji hello wybierz **Onit**.</span><span class="sxs-lookup"><span data-stu-id="e8e19-249">In hello applications list, select **Onit**.</span></span>

    ![łącze Onit Hello na liście aplikacji hello](./media/active-directory-saas-onit-tutorial/tutorial_onit_app.png)  

3. <span data-ttu-id="e8e19-251">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e8e19-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="e8e19-253">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e8e19-253">Click **Add** button.</span></span> <span data-ttu-id="e8e19-254">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e8e19-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="e8e19-256">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e8e19-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e8e19-257">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e8e19-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e8e19-258">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e8e19-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e8e19-259">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e8e19-259">Test single sign-on</span></span>

<span data-ttu-id="e8e19-260">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="e8e19-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e8e19-261">Po kliknięciu kafelka Onit hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Onit aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e8e19-261">When you click hello Onit tile in hello Access Panel, you should get automatically signed-on tooyour Onit application.</span></span>
<span data-ttu-id="e8e19-262">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e8e19-262">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e8e19-263">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e8e19-263">Additional resources</span></span>

* [<span data-ttu-id="e8e19-264">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e8e19-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e8e19-265">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e8e19-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-onit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-onit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-onit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-onit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-onit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-onit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-onit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-onit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-onit-tutorial/tutorial_general_203.png

