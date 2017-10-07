---
title: "Samouczek: Integracji Azure Active Directory z chmurą SAP dla klienta | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i w chmurze SAP dla klienta."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 0525ea81122458ab3ac24a5bdb0b5f628405dd05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a><span data-ttu-id="00ce9-103">Samouczek: Integracji Azure Active Directory z chmurą SAP dla klienta</span><span class="sxs-lookup"><span data-stu-id="00ce9-103">Tutorial: Azure Active Directory integration with SAP Cloud for Customer</span></span>

<span data-ttu-id="00ce9-104">Z tego samouczka, dowiesz się, jak SAP toointegrate chmury dla klienta w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="00ce9-104">In this tutorial, you learn how toointegrate SAP Cloud for Customer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="00ce9-105">Integrowanie SAP chmury dla klienta z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="00ce9-105">Integrating SAP Cloud for Customer with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="00ce9-106">Można kontrolować w usłudze Azure AD mającego dostęp tooSAP chmury dla klienta</span><span class="sxs-lookup"><span data-stu-id="00ce9-106">You can control in Azure AD who has access tooSAP Cloud for Customer</span></span>
- <span data-ttu-id="00ce9-107">Twoje użytkowników tooautomatically get zalogowane tooSAP chmury można włączyć dla klienta (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="00ce9-107">You can enable your users tooautomatically get signed-on tooSAP Cloud for Customer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="00ce9-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="00ce9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="00ce9-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="00ce9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00ce9-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="00ce9-110">Prerequisites</span></span>

<span data-ttu-id="00ce9-111">tooconfigure integracji usługi Azure AD z chmurą SAP dla klienta, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="00ce9-111">tooconfigure Azure AD integration with SAP Cloud for Customer, you need hello following items:</span></span>

- <span data-ttu-id="00ce9-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="00ce9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="00ce9-113">Chmurę SAP do klienta logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="00ce9-113">A SAP Cloud for Customer single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="00ce9-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="00ce9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="00ce9-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="00ce9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="00ce9-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="00ce9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="00ce9-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="00ce9-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="00ce9-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="00ce9-118">Scenario description</span></span>
<span data-ttu-id="00ce9-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="00ce9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="00ce9-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="00ce9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="00ce9-121">Dodawanie SAP chmury dla klienta z galerii hello</span><span class="sxs-lookup"><span data-stu-id="00ce9-121">Adding SAP Cloud for Customer from hello gallery</span></span>
2. <span data-ttu-id="00ce9-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="00ce9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-cloud-for-customer-from-hello-gallery"></a><span data-ttu-id="00ce9-123">Dodawanie SAP chmury dla klienta z galerii hello</span><span class="sxs-lookup"><span data-stu-id="00ce9-123">Adding SAP Cloud for Customer from hello gallery</span></span>
<span data-ttu-id="00ce9-124">tooconfigure hello integracji SAP chmury dla klienta do usługi Azure AD, należy tooadd SAP chmury dla klienta z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="00ce9-124">tooconfigure hello integration of SAP Cloud for Customer into Azure AD, you need tooadd SAP Cloud for Customer from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="00ce9-125">**tooadd chmurę SAP do klienta z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="00ce9-125">**tooadd SAP Cloud for Customer from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="00ce9-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="00ce9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="00ce9-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="00ce9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="00ce9-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="00ce9-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="00ce9-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="00ce9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="00ce9-133">W polu wyszukiwania hello wpisz **SAP chmury dla klienta**.</span><span class="sxs-lookup"><span data-stu-id="00ce9-133">In hello search box, type **SAP Cloud for Customer**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. <span data-ttu-id="00ce9-135">W panelu wyników hello, wybierz **SAP chmury dla klienta**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="00ce9-135">In hello results panel, select **SAP Cloud for Customer**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="00ce9-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="00ce9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="00ce9-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z chmurą SAP dla klienta w oparciu o użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="00ce9-138">In this section, you configure and test Azure AD single sign-on with SAP Cloud for Customer based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="00ce9-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w chmurze SAP dla klienta jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00ce9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP Cloud for Customer is tooa user in Azure AD.</span></span> <span data-ttu-id="00ce9-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w chmurze SAP dla klienta musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="00ce9-140">In other words, a link relationship between an Azure AD user and hello related user in SAP Cloud for Customer needs toobe established.</span></span>

<span data-ttu-id="00ce9-141">W chmurze SAP dla klienta, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="00ce9-141">In SAP Cloud for Customer, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="00ce9-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z chmurą SAP dla klienta, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="00ce9-142">tooconfigure and test Azure AD single sign-on with SAP Cloud for Customer, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="00ce9-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="00ce9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="00ce9-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="00ce9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="00ce9-145">**[Tworzenie chmury SAP dla użytkownika testowego klienta](#creating-a-sap-cloud-for-customer-test-user)**  -toohave odpowiednikiem Simona Britta w chmurze SAP dla klienta, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="00ce9-145">**[Creating a SAP Cloud for Customer test user](#creating-a-sap-cloud-for-customer-test-user)** - toohave a counterpart of Britta Simon in SAP Cloud for Customer that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="00ce9-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="00ce9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="00ce9-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="00ce9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="00ce9-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="00ce9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="00ce9-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w chmurze SAP dla aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="00ce9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP Cloud for Customer application.</span></span>

<span data-ttu-id="00ce9-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z chmurą SAP dla klienta, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="00ce9-150">**tooconfigure Azure AD single sign-on with SAP Cloud for Customer, perform hello following steps:**</span></span>

1. <span data-ttu-id="00ce9-151">W portalu Azure na powitania hello **SAP chmury dla klienta** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="00ce9-151">In hello Azure portal, on hello **SAP Cloud for Customer** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="00ce9-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="00ce9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. <span data-ttu-id="00ce9-155">Na powitania **chmury SAP do domeny klienta i adresy URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="00ce9-155">On hello **SAP Cloud for Customer Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    <span data-ttu-id="00ce9-157">a.</span><span class="sxs-lookup"><span data-stu-id="00ce9-157">a.</span></span> <span data-ttu-id="00ce9-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="00ce9-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    <span data-ttu-id="00ce9-159">b.</span><span class="sxs-lookup"><span data-stu-id="00ce9-159">b.</span></span> <span data-ttu-id="00ce9-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="00ce9-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="00ce9-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="00ce9-161">These values are not real.</span></span> <span data-ttu-id="00ce9-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="00ce9-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="00ce9-163">Skontaktuj się z [chmurę SAP do zespołu pomocy technicznej klienta klienta](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="00ce9-163">Contact [SAP Cloud for Customer Client support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget these values.</span></span> 

4. <span data-ttu-id="00ce9-164">Na powitania **atrybuty użytkownika** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="00ce9-164">On hello **User Attributes** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    <span data-ttu-id="00ce9-166">a.</span><span class="sxs-lookup"><span data-stu-id="00ce9-166">a.</span></span> <span data-ttu-id="00ce9-167">W **identyfikator użytkownika** listy, wybierz opcję hello **ExtractMailPrefix()** funkcji.</span><span class="sxs-lookup"><span data-stu-id="00ce9-167">In **User Identifier** list, select hello **ExtractMailPrefix()** function.</span></span>

    <span data-ttu-id="00ce9-168">b.</span><span class="sxs-lookup"><span data-stu-id="00ce9-168">b.</span></span> <span data-ttu-id="00ce9-169">Z hello **poczty** listy, wybierz hello atrybut użytkownika ma toouse implementacji.</span><span class="sxs-lookup"><span data-stu-id="00ce9-169">From hello **Mail** list, select hello user attribute you want toouse for your implementation.</span></span>
    <span data-ttu-id="00ce9-170">Na przykład jeśli wartość atrybutu hello są przechowywane w hello ExtensionAttribute2 ma hello toouse identyfikator pracownika jako identyfikator unikatowy użytkownika, wybierz user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="00ce9-170">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select user.extensionattribute2.</span></span>  

5. <span data-ttu-id="00ce9-171">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="00ce9-171">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. <span data-ttu-id="00ce9-173">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="00ce9-173">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="00ce9-175">Na powitania **SAP chmury dla konfiguracji klienta** kliknij **skonfigurować chmurę SAP do klienta** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="00ce9-175">On hello **SAP Cloud for Customer Configuration** section, click **Configure SAP Cloud for Customer** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="00ce9-176">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="00ce9-176">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. <span data-ttu-id="00ce9-178">tooget logowania jednokrotnego skonfigurowane, wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="00ce9-178">tooget SSO configured, perform hello following steps:</span></span>
   
    <span data-ttu-id="00ce9-179">a.</span><span class="sxs-lookup"><span data-stu-id="00ce9-179">a.</span></span> <span data-ttu-id="00ce9-180">Zaloguj się w chmurze SAP do portalu klienta z prawami administratora.</span><span class="sxs-lookup"><span data-stu-id="00ce9-180">Login into SAP Cloud for Customer portal with administrator rights.</span></span>
   
    <span data-ttu-id="00ce9-181">b.</span><span class="sxs-lookup"><span data-stu-id="00ce9-181">b.</span></span> <span data-ttu-id="00ce9-182">Przejdź toohello **aplikacji i typowych zadań zarządzania użytkownika** i kliknij przycisk hello **dostawcy tożsamości** kartę.</span><span class="sxs-lookup"><span data-stu-id="00ce9-182">Navigate toohello **Application and User Management Common Task** and click hello **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="00ce9-183">c.</span><span class="sxs-lookup"><span data-stu-id="00ce9-183">c.</span></span> <span data-ttu-id="00ce9-184">Kliknij przycisk **nowego dostawcy tożsamości** i pliku XML metadanych hello wybierz zostały pobrane z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="00ce9-184">Click **New Identity Provider** and select hello metadata XML file you have downloaded from hello Azure portal.</span></span> <span data-ttu-id="00ce9-185">Importując hello metadanych systemu hello automatyczne przekazywanie hello wymagany podpis certyfikatu i certyfikat szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="00ce9-185">By importing hello metadata, hello system automatically uploads hello required signature certificate and encryption certificate.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    <span data-ttu-id="00ce9-187">d.</span><span class="sxs-lookup"><span data-stu-id="00ce9-187">d.</span></span> <span data-ttu-id="00ce9-188">Element hello adres URL usługi klienta potwierdzenia w żądaniu SAML hello wymaga usługi Azure Active Directory, dlatego wybierz hello **zawierają potwierdzenie konsumenta adres URL usługi** wyboru.</span><span class="sxs-lookup"><span data-stu-id="00ce9-188">Azure Active Directory requires hello element Assertion Consumer Service URL in hello SAML request, so select hello **Include Assertion Consumer Service URL** checkbox.</span></span>
   
    <span data-ttu-id="00ce9-189">e.</span><span class="sxs-lookup"><span data-stu-id="00ce9-189">e.</span></span> <span data-ttu-id="00ce9-190">Kliknij przycisk **aktywacji rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="00ce9-190">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="00ce9-191">f.</span><span class="sxs-lookup"><span data-stu-id="00ce9-191">f.</span></span> <span data-ttu-id="00ce9-192">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="00ce9-192">Save your changes.</span></span>
   
    <span data-ttu-id="00ce9-193">g.</span><span class="sxs-lookup"><span data-stu-id="00ce9-193">g.</span></span> <span data-ttu-id="00ce9-194">Kliknij przycisk hello **systemie** kartę.</span><span class="sxs-lookup"><span data-stu-id="00ce9-194">Click hello **My System** tab.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    <span data-ttu-id="00ce9-196">h.</span><span class="sxs-lookup"><span data-stu-id="00ce9-196">h.</span></span> <span data-ttu-id="00ce9-197">W **Azure AD znaku w adresie URL** pole tekstowe, Wklej **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="00ce9-197">In **Azure AD Sign On URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    <span data-ttu-id="00ce9-199">i.</span><span class="sxs-lookup"><span data-stu-id="00ce9-199">i.</span></span> <span data-ttu-id="00ce9-200">Określ, czy pracownika hello ręcznie wybrać między zalogowanie się przy użyciu Identyfikatora użytkownika i hasła lub logowania jednokrotnego, wybierając hello **wybór dostawcy tożsamości ręcznego**.</span><span class="sxs-lookup"><span data-stu-id="00ce9-200">Specify whether hello employee can manually choose between logging on with user ID and password or SSO by selecting hello **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="00ce9-201">j.</span><span class="sxs-lookup"><span data-stu-id="00ce9-201">j.</span></span> <span data-ttu-id="00ce9-202">W hello **adres URL logowania jednokrotnego** sekcji, podaj adres URL hello, które mają być używane przez użytkownika toosign pracowników w systemie toohello.</span><span class="sxs-lookup"><span data-stu-id="00ce9-202">In hello **SSO URL** section, specify hello URL that should be used by your employees toosign on toohello system.</span></span> 
    <span data-ttu-id="00ce9-203">W hello **wysyłane na adres URL tooEmployee** listy, możesz wybrać hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="00ce9-203">In hello **URL Sent tooEmployee** list, you can choose between hello following options:</span></span>
   
    <span data-ttu-id="00ce9-204">**Adres URL — Usługa rejestracji Jednokrotnej**</span><span class="sxs-lookup"><span data-stu-id="00ce9-204">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="00ce9-205">Hello system wysyła tylko hello system normalny adres URL toohello pracownika.</span><span class="sxs-lookup"><span data-stu-id="00ce9-205">hello system sends only hello normal system URL toohello employee.</span></span> <span data-ttu-id="00ce9-206">pracowników Hello nie może zalogować się przy użyciu logowania jednokrotnego i musi użyć hasła lub zamiast tego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="00ce9-206">hello employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="00ce9-207">**ADRES URL LOGOWANIA JEDNOKROTNEGO**</span><span class="sxs-lookup"><span data-stu-id="00ce9-207">**SSO URL**</span></span> 
   
    <span data-ttu-id="00ce9-208">Hello system wysyła tylko hello pracownika toohello adres URL logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="00ce9-208">hello system sends only hello SSO URL toohello employee.</span></span> <span data-ttu-id="00ce9-209">Pracownik Hello można zalogować się przy użyciu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="00ce9-209">hello employee can log on using SSO.</span></span> <span data-ttu-id="00ce9-210">Za pomocą hello IdP kierowane jest żądanie uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="00ce9-210">Authentication request is redirected through hello IdP.</span></span>
   
    <span data-ttu-id="00ce9-211">**Automatyczne wybieranie**</span><span class="sxs-lookup"><span data-stu-id="00ce9-211">**Automatic Selection**</span></span>
   
    <span data-ttu-id="00ce9-212">Jeśli logowania jednokrotnego nie jest aktywne, hello system wysyła hello system normalny adres URL toohello pracownika.</span><span class="sxs-lookup"><span data-stu-id="00ce9-212">If SSO is not active, hello system sends hello normal system URL toohello employee.</span></span> <span data-ttu-id="00ce9-213">Jeśli rejestracji Jednokrotnej jest aktywny, hello system sprawdza, czy hello pracownik ma hasło.</span><span class="sxs-lookup"><span data-stu-id="00ce9-213">If SSO is active, hello system checks whether hello employee has a password.</span></span> <span data-ttu-id="00ce9-214">Jeśli hasło jest dostępny, zarówno adres URL logowania jednokrotnego i adres URL logowania jednokrotnego nie są wysyłane toohello pracownika.</span><span class="sxs-lookup"><span data-stu-id="00ce9-214">If a password is available, both SSO URL and Non-SSO URL are sent toohello employee.</span></span> <span data-ttu-id="00ce9-215">Jednak jeśli pracownik hello nie ma hasła, hello adres URL logowania jednokrotnego są wysyłane toohello pracownika.</span><span class="sxs-lookup"><span data-stu-id="00ce9-215">However, if hello employee has no password, only hello SSO URL is sent toohello employee.</span></span>
   
    <span data-ttu-id="00ce9-216">k.</span><span class="sxs-lookup"><span data-stu-id="00ce9-216">k.</span></span> <span data-ttu-id="00ce9-217">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="00ce9-217">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="00ce9-218">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="00ce9-218">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="00ce9-219">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="00ce9-219">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="00ce9-220">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="00ce9-220">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="00ce9-221">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="00ce9-221">Creating an Azure AD test user</span></span>
<span data-ttu-id="00ce9-222">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="00ce9-222">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="00ce9-224">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="00ce9-224">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="00ce9-225">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="00ce9-225">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="00ce9-227">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="00ce9-227">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="00ce9-229">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="00ce9-229">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="00ce9-231">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="00ce9-231">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="00ce9-233">a.</span><span class="sxs-lookup"><span data-stu-id="00ce9-233">a.</span></span> <span data-ttu-id="00ce9-234">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="00ce9-234">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="00ce9-235">b.</span><span class="sxs-lookup"><span data-stu-id="00ce9-235">b.</span></span> <span data-ttu-id="00ce9-236">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="00ce9-236">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="00ce9-237">c.</span><span class="sxs-lookup"><span data-stu-id="00ce9-237">c.</span></span> <span data-ttu-id="00ce9-238">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="00ce9-238">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="00ce9-239">d.</span><span class="sxs-lookup"><span data-stu-id="00ce9-239">d.</span></span> <span data-ttu-id="00ce9-240">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="00ce9-240">Click **Create**.</span></span>
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a><span data-ttu-id="00ce9-241">Tworzenie chmury SAP dla użytkownika testowego klienta</span><span class="sxs-lookup"><span data-stu-id="00ce9-241">Creating a SAP Cloud for Customer test user</span></span>

<span data-ttu-id="00ce9-242">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w chmurze SAP dla klienta.</span><span class="sxs-lookup"><span data-stu-id="00ce9-242">In this section, you create a user called Britta Simon in SAP Cloud for Customer.</span></span> <span data-ttu-id="00ce9-243">We współpracy z [SAP chmury zespół obsługi klienta](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooadd hello użytkowników w hello SAP chmurze dla platformy klienta.</span><span class="sxs-lookup"><span data-stu-id="00ce9-243">Please work with [SAP Cloud for Customer support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooadd hello users in hello SAP Cloud for Customer platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="00ce9-244">Upewnij się, wartość NameID powinny być zgodne z pole username hello w hello SAP chmurze dla platformy klienta.</span><span class="sxs-lookup"><span data-stu-id="00ce9-244">Please make sure that NameID value should match with hello username field in hello SAP Cloud for Customer platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="00ce9-245">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="00ce9-245">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="00ce9-246">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSAP chmury dla klienta.</span><span class="sxs-lookup"><span data-stu-id="00ce9-246">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP Cloud for Customer.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="00ce9-248">**tooassign tooSAP Simona Britta chmury dla klienta, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="00ce9-248">**tooassign Britta Simon tooSAP Cloud for Customer, perform hello following steps:**</span></span>

1. <span data-ttu-id="00ce9-249">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="00ce9-249">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="00ce9-251">Z listy aplikacji hello wybierz **SAP chmury dla klienta**.</span><span class="sxs-lookup"><span data-stu-id="00ce9-251">In hello applications list, select **SAP Cloud for Customer**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. <span data-ttu-id="00ce9-253">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="00ce9-253">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="00ce9-255">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="00ce9-255">Click **Add** button.</span></span> <span data-ttu-id="00ce9-256">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="00ce9-256">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="00ce9-258">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="00ce9-258">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="00ce9-259">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="00ce9-259">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="00ce9-260">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="00ce9-260">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="00ce9-261">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="00ce9-261">Testing single sign-on</span></span>

<span data-ttu-id="00ce9-262">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="00ce9-262">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="00ce9-263">Po kliknięciu hello SAP chmury dla klienta kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour SAP chmury dla aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="00ce9-263">When you click hello SAP Cloud for Customer tile in hello Access Panel, you should get automatically signed-on tooyour SAP Cloud for Customer application.</span></span>
<span data-ttu-id="00ce9-264">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="00ce9-264">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="00ce9-265">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="00ce9-265">Additional resources</span></span>

* [<span data-ttu-id="00ce9-266">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="00ce9-266">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="00ce9-267">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="00ce9-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png

