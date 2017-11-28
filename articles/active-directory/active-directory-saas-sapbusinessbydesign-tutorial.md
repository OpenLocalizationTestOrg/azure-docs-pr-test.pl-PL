---
title: 'Samouczek: Integracji Azure Active Directory z SAP Business ByDesign | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i SAP Business ByDesign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: c14714fd27f8d7fc555f25c7be83fad2b0d7f333
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a><span data-ttu-id="cc620-103">Samouczek: integracja usługi Azure Active Directory z oprogramowaniem SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="cc620-103">Tutorial: Azure Active Directory integration with SAP Business ByDesign</span></span>

<span data-ttu-id="cc620-104">Z tego samouczka, dowiesz się, jak SAP toointegrate ByDesign firm z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc620-104">In this tutorial, you learn how toointegrate SAP Business ByDesign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cc620-105">Integrowanie SAP Business ByDesign z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="cc620-105">Integrating SAP Business ByDesign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cc620-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooSAP ByDesign biznesowych.</span><span class="sxs-lookup"><span data-stu-id="cc620-106">You can control in Azure AD who has access tooSAP Business ByDesign.</span></span>
- <span data-ttu-id="cc620-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSAP ByDesign Business (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc620-107">You can enable your users tooautomatically get signed-on tooSAP Business ByDesign (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="cc620-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cc620-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="cc620-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cc620-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc620-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cc620-110">Prerequisites</span></span>

<span data-ttu-id="cc620-111">tooconfigure integracji usługi Azure AD z SAP Business ByDesign należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="cc620-111">tooconfigure Azure AD integration with SAP Business ByDesign, you need hello following items:</span></span>

- <span data-ttu-id="cc620-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc620-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cc620-113">SAP Business ByDesign logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="cc620-113">An SAP Business ByDesign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cc620-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="cc620-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cc620-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="cc620-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cc620-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="cc620-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cc620-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc620-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cc620-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="cc620-118">Scenario description</span></span>
<span data-ttu-id="cc620-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="cc620-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cc620-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="cc620-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cc620-121">Dodawanie SAP Business ByDesign z galerii hello</span><span class="sxs-lookup"><span data-stu-id="cc620-121">Adding SAP Business ByDesign from hello gallery</span></span>
2. <span data-ttu-id="cc620-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="cc620-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-business-bydesign-from-hello-gallery"></a><span data-ttu-id="cc620-123">Dodawanie SAP Business ByDesign z galerii hello</span><span class="sxs-lookup"><span data-stu-id="cc620-123">Adding SAP Business ByDesign from hello gallery</span></span>
<span data-ttu-id="cc620-124">tooconfigure hello integracji SAP Business ByDesign do usługi Azure AD, należy tooadd SAP Business ByDesign z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="cc620-124">tooconfigure hello integration of SAP Business ByDesign into Azure AD, you need tooadd SAP Business ByDesign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cc620-125">**tooadd SAP Business ByDesign z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="cc620-125">**tooadd SAP Business ByDesign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc620-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="cc620-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="cc620-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="cc620-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cc620-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="cc620-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="cc620-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cc620-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="cc620-133">W polu wyszukiwania hello wpisz **SAP Business ByDesign**, wybierz pozycję **SAP Business ByDesign** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="cc620-133">In hello search box, type **SAP Business ByDesign**, select **SAP Business ByDesign** from result panel then click **Add** button tooadd hello application.</span></span>

    ![SAP Business ByDesign hello listy wyników](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="cc620-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="cc620-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="cc620-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SAP Business ByDesign w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="cc620-136">In this section, you configure and test Azure AD single sign-on with SAP Business ByDesign based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cc620-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w SAP Business ByDesign jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc620-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP Business ByDesign is tooa user in Azure AD.</span></span> <span data-ttu-id="cc620-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w SAP Business ByDesign musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="cc620-138">In other words, a link relationship between an Azure AD user and hello related user in SAP Business ByDesign needs toobe established.</span></span>

<span data-ttu-id="cc620-139">W SAP Business ByDesign, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="cc620-139">In SAP Business ByDesign, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="cc620-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z SAP Business ByDesign, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="cc620-140">tooconfigure and test Azure AD single sign-on with SAP Business ByDesign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cc620-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="cc620-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cc620-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="cc620-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cc620-143">**[Tworzenie użytkownika testowego SAP Business ByDesign](#create-an-sap-business-bydesign-test-user)**  -toohave odpowiednikiem Simona Britta w SAP Business ByDesign, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cc620-143">**[Create an SAP Business ByDesign test user](#create-an-sap-business-bydesign-test-user)** - toohave a counterpart of Britta Simon in SAP Business ByDesign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cc620-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="cc620-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cc620-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="cc620-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="cc620-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="cc620-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="cc620-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="cc620-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP Business ByDesign application.</span></span>

<span data-ttu-id="cc620-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z SAP Business ByDesign, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="cc620-148">**tooconfigure Azure AD single sign-on with SAP Business ByDesign, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc620-149">W portalu Azure na powitania hello **SAP Business ByDesign** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="cc620-149">In hello Azure portal, on hello **SAP Business ByDesign** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="cc620-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="cc620-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. <span data-ttu-id="cc620-153">Na powitania **adresy URL i SAP Business ByDesign domeny** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="cc620-153">On hello **SAP Business ByDesign Domain and URLs** section, perform hello following steps:</span></span>

    ![Adresy URL i SAP Business ByDesign domeny pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    <span data-ttu-id="cc620-155">a.</span><span class="sxs-lookup"><span data-stu-id="cc620-155">a.</span></span> <span data-ttu-id="cc620-156">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="cc620-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<servername>.sapbydesign.com`</span></span>

    <span data-ttu-id="cc620-157">b.</span><span class="sxs-lookup"><span data-stu-id="cc620-157">b.</span></span> <span data-ttu-id="cc620-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="cc620-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<servername>.sapbydesign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cc620-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="cc620-159">These values are not real.</span></span> <span data-ttu-id="cc620-160">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="cc620-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="cc620-161">Skontaktuj się z [zespołem pomocy technicznej SAP Business ByDesign klienta](https://www.sap.com/products/cloud-analytics.support.html) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="cc620-161">Contact [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) tooget these values.</span></span>

4. <span data-ttu-id="cc620-162">Na powitania **atrybuty użytkownika** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="cc620-162">On hello **User Attributes** section, perform hello following steps:</span></span>

    ![SAP Business ByDesign atrybutów sekcji](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    <span data-ttu-id="cc620-164">a.</span><span class="sxs-lookup"><span data-stu-id="cc620-164">a.</span></span> <span data-ttu-id="cc620-165">W **identyfikator użytkownika** listy, wybierz opcję hello **ExtractMailPrefix()** funkcji.</span><span class="sxs-lookup"><span data-stu-id="cc620-165">In **User Identifier** list, select hello **ExtractMailPrefix()** function.</span></span>
    
    <span data-ttu-id="cc620-166">b.</span><span class="sxs-lookup"><span data-stu-id="cc620-166">b.</span></span> <span data-ttu-id="cc620-167">Z hello **poczty** listy, wybierz hello atrybut użytkownika ma toouse implementacji.</span><span class="sxs-lookup"><span data-stu-id="cc620-167">From hello **Mail** list, select hello user attribute you want toouse for your implementation.</span></span> <span data-ttu-id="cc620-168">Na przykład jeśli wartość atrybutu hello są przechowywane w hello ExtensionAttribute2 ma hello toouse identyfikator pracownika jako identyfikator unikatowy użytkownika, wybierz user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="cc620-168">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select user.extensionattribute2.</span></span>   

5. <span data-ttu-id="cc620-169">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="cc620-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. <span data-ttu-id="cc620-171">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="cc620-171">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="cc620-173">Na powitania **SAP Business ByDesign konfiguracji** kliknij **skonfigurować SAP Business ByDesign** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="cc620-173">On hello **SAP Business ByDesign Configuration** section, click **Configure SAP Business ByDesign** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cc620-174">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="cc620-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![SAP Business ByDesign konfiguracji](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. <span data-ttu-id="cc620-176">tooget logowania jednokrotnego skonfigurowane dla aplikacji, należy wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="cc620-176">tooget SSO configured for your application, perform hello following steps:</span></span>
   
    <span data-ttu-id="cc620-177">a.</span><span class="sxs-lookup"><span data-stu-id="cc620-177">a.</span></span> <span data-ttu-id="cc620-178">Zaloguj się w portalu SAP Business ByDesign tooyour z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="cc620-178">Sign on tooyour SAP Business ByDesign portal with administrator rights.</span></span>
   
    <span data-ttu-id="cc620-179">b.</span><span class="sxs-lookup"><span data-stu-id="cc620-179">b.</span></span> <span data-ttu-id="cc620-180">Przejdź za**aplikacji i typowych zadań zarządzania użytkownika** i kliknij przycisk hello **dostawcy tożsamości** kartę.</span><span class="sxs-lookup"><span data-stu-id="cc620-180">Navigate too**Application and User Management Common Task** and click hello **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="cc620-181">c.</span><span class="sxs-lookup"><span data-stu-id="cc620-181">c.</span></span> <span data-ttu-id="cc620-182">Kliknij przycisk **nowego dostawcy tożsamości** i pliku XML metadanych wybierz hello pobranego z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cc620-182">Click **New Identity Provider** and select hello metadata XML file that you have downloaded from hello Azure portal.</span></span> <span data-ttu-id="cc620-183">Importując hello metadanych systemu hello automatyczne przekazywanie hello wymagany podpis certyfikatu i certyfikat szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="cc620-183">By importing hello metadata, hello system automatically uploads hello required signature certificate and encryption certificate.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    <span data-ttu-id="cc620-185">d.</span><span class="sxs-lookup"><span data-stu-id="cc620-185">d.</span></span> <span data-ttu-id="cc620-186">Witaj tooinclude **adres URL usługi klienta potwierdzenia** do żądania SAML hello, wybierz **zawierają potwierdzenie konsumenta adres URL usługi**.</span><span class="sxs-lookup"><span data-stu-id="cc620-186">tooinclude hello **Assertion Consumer Service URL** into hello SAML request, select **Include Assertion Consumer Service URL**.</span></span>
   
    <span data-ttu-id="cc620-187">e.</span><span class="sxs-lookup"><span data-stu-id="cc620-187">e.</span></span> <span data-ttu-id="cc620-188">Kliknij przycisk **aktywacji rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="cc620-188">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="cc620-189">f.</span><span class="sxs-lookup"><span data-stu-id="cc620-189">f.</span></span> <span data-ttu-id="cc620-190">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="cc620-190">Save your changes.</span></span>
   
    <span data-ttu-id="cc620-191">g.</span><span class="sxs-lookup"><span data-stu-id="cc620-191">g.</span></span> <span data-ttu-id="cc620-192">Kliknij przycisk hello **systemie** kartę.</span><span class="sxs-lookup"><span data-stu-id="cc620-192">Click hello **My System** tab.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    <span data-ttu-id="cc620-194">h.</span><span class="sxs-lookup"><span data-stu-id="cc620-194">h.</span></span> <span data-ttu-id="cc620-195">Wklej **SAML pojedynczy znak na adres URL usługi**, która została skopiowana z portalu Azure hello go do hello **Azure AD znaku w adresie URL** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="cc620-195">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal it into hello **Azure AD Sign On URL** textbox.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    <span data-ttu-id="cc620-197">i.</span><span class="sxs-lookup"><span data-stu-id="cc620-197">i.</span></span> <span data-ttu-id="cc620-198">Określ, czy pracownika hello ręcznie wybrać między zalogowanie się przy użyciu Identyfikatora użytkownika i hasła lub logowania jednokrotnego, wybierając **wybór dostawcy tożsamości ręcznego**.</span><span class="sxs-lookup"><span data-stu-id="cc620-198">Specify whether hello employee can manually choose between logging on with user ID and password or SSO by selecting **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="cc620-199">j.</span><span class="sxs-lookup"><span data-stu-id="cc620-199">j.</span></span> <span data-ttu-id="cc620-200">W hello **adres URL logowania jednokrotnego** sekcji, podaj adres URL hello, które mają być używane przez system toohello toologon pracownika hello.</span><span class="sxs-lookup"><span data-stu-id="cc620-200">In hello **SSO URL** section, specify hello URL that should be used by hello employee toologon toohello system.</span></span> 
    <span data-ttu-id="cc620-201">Witaj wysyłane na adres URL tooEmployee listy rozwijanej można wybrać hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="cc620-201">In hello URL Sent tooEmployee dropdown list, you can choose between hello following options:</span></span>
   
    <span data-ttu-id="cc620-202">**Adres URL — Usługa rejestracji Jednokrotnej**</span><span class="sxs-lookup"><span data-stu-id="cc620-202">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="cc620-203">Hello system wysyła tylko hello system normalny adres URL toohello pracownika.</span><span class="sxs-lookup"><span data-stu-id="cc620-203">hello system sends only hello normal system URL toohello employee.</span></span> <span data-ttu-id="cc620-204">pracowników Hello nie może zalogować się przy użyciu logowania jednokrotnego i musi użyć hasła lub zamiast tego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="cc620-204">hello employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="cc620-205">**ADRES URL LOGOWANIA JEDNOKROTNEGO**</span><span class="sxs-lookup"><span data-stu-id="cc620-205">**SSO URL**</span></span> 
   
    <span data-ttu-id="cc620-206">Hello system wysyła tylko hello pracownika toohello adres URL logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="cc620-206">hello system sends only hello SSO URL toohello employee.</span></span> <span data-ttu-id="cc620-207">Pracownik Hello można zalogować się przy użyciu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="cc620-207">hello employee can log on using SSO.</span></span> <span data-ttu-id="cc620-208">Za pomocą hello IdP kierowane jest żądanie uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="cc620-208">Authentication request is redirected through hello IdP.</span></span>
   
    <span data-ttu-id="cc620-209">**Automatyczne wybieranie**</span><span class="sxs-lookup"><span data-stu-id="cc620-209">**Automatic Selection**</span></span>
   
    <span data-ttu-id="cc620-210">Jeśli logowania jednokrotnego nie jest aktywne, hello system wysyła hello system normalny adres URL toohello pracownika.</span><span class="sxs-lookup"><span data-stu-id="cc620-210">If SSO is not active, hello system sends hello normal system URL toohello employee.</span></span> <span data-ttu-id="cc620-211">Jeśli rejestracji Jednokrotnej jest aktywny, hello system sprawdza, czy hello pracownik ma hasło.</span><span class="sxs-lookup"><span data-stu-id="cc620-211">If SSO is active, hello system checks whether hello employee has a password.</span></span> <span data-ttu-id="cc620-212">Jeśli hasło jest dostępny, zarówno adres URL logowania jednokrotnego i adres URL logowania jednokrotnego nie są wysyłane toohello pracownika.</span><span class="sxs-lookup"><span data-stu-id="cc620-212">If a password is available, both SSO URL and Non-SSO URL are sent toohello employee.</span></span> <span data-ttu-id="cc620-213">Jednak jeśli pracownik hello nie ma hasła, hello adres URL logowania jednokrotnego są wysyłane toohello pracownika.</span><span class="sxs-lookup"><span data-stu-id="cc620-213">However, if hello employee has no password, only hello SSO URL is sent toohello employee.</span></span>
   
    <span data-ttu-id="cc620-214">k.</span><span class="sxs-lookup"><span data-stu-id="cc620-214">k.</span></span> <span data-ttu-id="cc620-215">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="cc620-215">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="cc620-216">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="cc620-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cc620-217">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="cc620-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cc620-218">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cc620-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="cc620-219">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc620-219">Create an Azure AD test user</span></span>

<span data-ttu-id="cc620-220">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="cc620-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="cc620-222">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="cc620-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc620-223">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="cc620-223">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="cc620-225">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="cc620-225">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="cc620-227">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="cc620-227">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="cc620-229">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="cc620-229">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    <span data-ttu-id="cc620-231">a.</span><span class="sxs-lookup"><span data-stu-id="cc620-231">a.</span></span> <span data-ttu-id="cc620-232">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cc620-232">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cc620-233">b.</span><span class="sxs-lookup"><span data-stu-id="cc620-233">b.</span></span> <span data-ttu-id="cc620-234">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="cc620-234">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="cc620-235">c.</span><span class="sxs-lookup"><span data-stu-id="cc620-235">c.</span></span> <span data-ttu-id="cc620-236">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="cc620-236">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="cc620-237">d.</span><span class="sxs-lookup"><span data-stu-id="cc620-237">d.</span></span> <span data-ttu-id="cc620-238">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="cc620-238">Click **Create**.</span></span>
 
### <a name="create-an-sap-business-bydesign-test-user"></a><span data-ttu-id="cc620-239">Tworzenie użytkownika testowego SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="cc620-239">Create an SAP Business ByDesign test user</span></span>

<span data-ttu-id="cc620-240">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="cc620-240">In this section, you create a user called Britta Simon in SAP Business ByDesign.</span></span> <span data-ttu-id="cc620-241">We współpracy z [zespołem pomocy technicznej SAP Business ByDesign klienta](https://www.sap.com/products/cloud-analytics.support.html) użytkowników hello tooadd hello SAP Business ByDesign platformy.</span><span class="sxs-lookup"><span data-stu-id="cc620-241">Please work with [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) tooadd hello users in hello SAP Business ByDesign platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="cc620-242">Upewnij się, że NameID wartość powinno być zgodne z pola Nazwa użytkownika hello hello SAP Business ByDesign platformy.</span><span class="sxs-lookup"><span data-stu-id="cc620-242">Please make sure that NameID value should match with hello username field in hello SAP Business ByDesign platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="cc620-243">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc620-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="cc620-244">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSAP ByDesign biznesowych.</span><span class="sxs-lookup"><span data-stu-id="cc620-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP Business ByDesign.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="cc620-246">**tooassign tooSAP Simona Britta ByDesign biznesowych, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="cc620-246">**tooassign Britta Simon tooSAP Business ByDesign, perform hello following steps:**</span></span>

1. <span data-ttu-id="cc620-247">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="cc620-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="cc620-249">Z listy aplikacji hello wybierz **SAP Business ByDesign**.</span><span class="sxs-lookup"><span data-stu-id="cc620-249">In hello applications list, select **SAP Business ByDesign**.</span></span>

    ![łącze SAP Business ByDesign Hello na liście aplikacji hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. <span data-ttu-id="cc620-251">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="cc620-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="cc620-253">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="cc620-253">Click **Add** button.</span></span> <span data-ttu-id="cc620-254">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cc620-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="cc620-256">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="cc620-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cc620-257">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cc620-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cc620-258">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cc620-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="cc620-259">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="cc620-259">Test single sign-on</span></span>

<span data-ttu-id="cc620-260">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="cc620-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cc620-261">Po kliknięciu kafelka SAP Business ByDesign hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour SAP Business ByDesign aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cc620-261">When you click hello SAP Business ByDesign tile in hello Access Panel, you should get automatically signed-on tooyour SAP Business ByDesign application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cc620-262">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="cc620-262">Additional resources</span></span>

* [<span data-ttu-id="cc620-263">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc620-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cc620-264">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cc620-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png

