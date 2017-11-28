---
title: 'Samouczek: Hello integracji Azure Active Directory z portalu fundusze | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i hello fundusze portalu."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4663cc8a-976a-4c6c-b3b4-1e5df9b66744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 9f4329e02f91eb6d8034f17646ac7d15afe503e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hello-funding-portal"></a><span data-ttu-id="d70f9-103">Samouczek: Integracji Azure Active Directory z hello fundusze portalu</span><span class="sxs-lookup"><span data-stu-id="d70f9-103">Tutorial: Azure Active Directory integration with hello Funding Portal</span></span>

<span data-ttu-id="d70f9-104">Z tego samouczka dowiesz się, jak toointegrate hello fundusze Portal za pomocą usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d70f9-104">In this tutorial, you learn how toointegrate hello Funding Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d70f9-105">Integrowanie hello fundusze portalu z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d70f9-105">Integrating hello Funding Portal with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d70f9-106">Można kontrolować w usłudze Azure AD, kto ma dostęp toohello fundusze portalu</span><span class="sxs-lookup"><span data-stu-id="d70f9-106">You can control in Azure AD who has access toohello Funding Portal</span></span>
- <span data-ttu-id="d70f9-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane toohello fundusze Portal (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d70f9-107">You can enable your users tooautomatically get signed-on toohello Funding Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d70f9-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d70f9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d70f9-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d70f9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d70f9-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d70f9-110">Prerequisites</span></span>

<span data-ttu-id="d70f9-111">Integracja tooconfigure usługi Azure AD z hello fundusze portalu, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d70f9-111">tooconfigure Azure AD integration with hello Funding Portal, you need hello following items:</span></span>

- <span data-ttu-id="d70f9-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d70f9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d70f9-113">Witaj fundusze portalu rejestracji jednokrotnej włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d70f9-113">A hello Funding Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d70f9-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d70f9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d70f9-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d70f9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d70f9-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d70f9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d70f9-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d70f9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d70f9-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d70f9-118">Scenario description</span></span>
<span data-ttu-id="d70f9-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d70f9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d70f9-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d70f9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d70f9-121">Dodawanie hello portalu fundusze z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d70f9-121">Adding hello Funding Portal from hello gallery</span></span>
2. <span data-ttu-id="d70f9-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d70f9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hello-funding-portal-from-hello-gallery"></a><span data-ttu-id="d70f9-123">Dodawanie hello portalu fundusze z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d70f9-123">Adding hello Funding Portal from hello gallery</span></span>
<span data-ttu-id="d70f9-124">tooconfigure hello integracji hello fundusze portalu usługi Azure AD, należy tooadd hello portalu fundusze na powitania galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d70f9-124">tooconfigure hello integration of hello Funding Portal into Azure AD, you need tooadd hello Funding Portal from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d70f9-125">**tooadd hello fundusze portalu z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d70f9-125">**tooadd hello Funding Portal from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d70f9-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d70f9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="d70f9-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="d70f9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d70f9-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d70f9-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="d70f9-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d70f9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="d70f9-133">W polu wyszukiwania hello wpisz **hello fundusze Portal**.</span><span class="sxs-lookup"><span data-stu-id="d70f9-133">In hello search box, type **hello Funding Portal**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_search.png)

5. <span data-ttu-id="d70f9-135">W panelu wyników hello, wybierz **hello fundusze portalu**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d70f9-135">In hello results panel, select **hello Funding Portal**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d70f9-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d70f9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d70f9-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z powitalne fundusze portalu w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="d70f9-138">In this section, you configure and test Azure AD single sign-on with hello Funding Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d70f9-139">Dla pojedynczego logowania jednokrotnego toowork, usługi Azure AD wymaga tooknow użytkownika odpowiednikiem hello w hello fundusze Portal jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d70f9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in hello Funding Portal is tooa user in Azure AD.</span></span> <span data-ttu-id="d70f9-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w hello fundusze portalu musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="d70f9-140">In other words, a link relationship between an Azure AD user and hello related user in hello Funding Portal needs toobe established.</span></span>

<span data-ttu-id="d70f9-141">W hello fundusze portalu, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="d70f9-141">In hello Funding Portal, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d70f9-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z hello fundusze portalu, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d70f9-142">tooconfigure and test Azure AD single sign-on with hello Funding Portal, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d70f9-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d70f9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d70f9-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d70f9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d70f9-145">**[Tworzenie użytkownika testowego fundusze portalu hello](#creating-the-funding-portal-test-user)**  -toohave odpowiednikiem Simona Britta w hello fundusze Portal, który jest odpowiednikiem połączonych toohello usługi Azure AD użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d70f9-145">**[Creating hello Funding Portal test user](#creating-the-funding-portal-test-user)** - toohave a counterpart of Britta Simon in hello Funding Portal that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d70f9-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d70f9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d70f9-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="d70f9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d70f9-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d70f9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d70f9-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w Twojej aplikacji portalu fundusze hello.</span><span class="sxs-lookup"><span data-stu-id="d70f9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your hello Funding Portal application.</span></span>

<span data-ttu-id="d70f9-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z hello fundusze portalu, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d70f9-150">**tooconfigure Azure AD single sign-on with hello Funding Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="d70f9-151">W portalu Azure na powitania hello **hello fundusze portalu** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="d70f9-151">In hello Azure portal, on hello **hello Funding Portal** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="d70f9-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d70f9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_samlbase.png)

3. <span data-ttu-id="d70f9-155">Na powitania **hello fundusze domeny portalu i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d70f9-155">On hello **hello Funding Portal Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_url.png)

    <span data-ttu-id="d70f9-157">a.</span><span class="sxs-lookup"><span data-stu-id="d70f9-157">a.</span></span> <span data-ttu-id="d70f9-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.regenteducation.net/`</span><span class="sxs-lookup"><span data-stu-id="d70f9-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.regenteducation.net/`</span></span>

    <span data-ttu-id="d70f9-159">b.</span><span class="sxs-lookup"><span data-stu-id="d70f9-159">b.</span></span> <span data-ttu-id="d70f9-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.regenteducation.net`</span><span class="sxs-lookup"><span data-stu-id="d70f9-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.regenteducation.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d70f9-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="d70f9-161">These values are not real.</span></span> <span data-ttu-id="d70f9-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="d70f9-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d70f9-163">Skontaktuj się z [hello zespołem pomocy technicznej fundusze portalu klienta](mailto:info@regenteducation.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="d70f9-163">Contact [hello Funding Portal Client support team](mailto:info@regenteducation.com) tooget these values.</span></span> 

4. <span data-ttu-id="d70f9-164">Portal fundusze aplikacji Hello oczekuje hello SAML potwierdzenia toocontain atrybut o nazwie "externalId1".</span><span class="sxs-lookup"><span data-stu-id="d70f9-164">hello Funding Portal application expects hello SAML assertions toocontain an attribute named "externalId1".</span></span> <span data-ttu-id="d70f9-165">wartość Hello "externalId1" powinna być rozpoznawanym studentID.</span><span class="sxs-lookup"><span data-stu-id="d70f9-165">hello value of "externalId1" should be a recognized studentID.</span></span> <span data-ttu-id="d70f9-166">Skonfiguruj oświadczenia hello "externalId1" dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d70f9-166">Configure hello "externalId1" claim for this application.</span></span> <span data-ttu-id="d70f9-167">Można zarządzać hello wartości tych atrybutów z hello **atrybuty użytkownika** aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d70f9-167">You can manage hello values of these attributes from hello **User Attributes** of hello application.</span></span> <span data-ttu-id="d70f9-168">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="d70f9-168">hello following screenshot shows an example for this.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_attribute.png)

5. <span data-ttu-id="d70f9-170">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie hello i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d70f9-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>

    | <span data-ttu-id="d70f9-171">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="d70f9-171">Attribute Name</span></span> | <span data-ttu-id="d70f9-172">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="d70f9-172">Attribute Value</span></span> |
    | ------------------- | ---------------- |
    | <span data-ttu-id="d70f9-173">externalId1</span><span class="sxs-lookup"><span data-stu-id="d70f9-173">externalId1</span></span> | <span data-ttu-id="d70f9-174">User.extensionattribute1</span><span class="sxs-lookup"><span data-stu-id="d70f9-174">user.extensionattribute1</span></span> |

    <span data-ttu-id="d70f9-175">a.</span><span class="sxs-lookup"><span data-stu-id="d70f9-175">a.</span></span> <span data-ttu-id="d70f9-176">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d70f9-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thefundingportal-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="d70f9-179">b.</span><span class="sxs-lookup"><span data-stu-id="d70f9-179">b.</span></span> <span data-ttu-id="d70f9-180">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="d70f9-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="d70f9-181">c.</span><span class="sxs-lookup"><span data-stu-id="d70f9-181">c.</span></span> <span data-ttu-id="d70f9-182">Z hello **wartość atrybutu** listy, wybierz hello atrybut ma toouse implementacji.</span><span class="sxs-lookup"><span data-stu-id="d70f9-182">From hello **Attribute Value** list, select hello attribute you want toouse for your implementation.</span></span> <span data-ttu-id="d70f9-183">Na przykład jeśli hello StudentID wartość przechowywanych w hello ExtensionAttribute1, wybierz user.extensionattribute1.</span><span class="sxs-lookup"><span data-stu-id="d70f9-183">For example, if you have stored hello StudentID value in hello ExtensionAttribute1, then select user.extensionattribute1.</span></span>
    
    <span data-ttu-id="d70f9-184">d.</span><span class="sxs-lookup"><span data-stu-id="d70f9-184">d.</span></span> <span data-ttu-id="d70f9-185">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d70f9-185">Click **Ok**.</span></span>
 
6. <span data-ttu-id="d70f9-186">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d70f9-186">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_certificate.png) 

7. <span data-ttu-id="d70f9-188">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d70f9-188">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="d70f9-190">tooconfigure rejestracji jednokrotnej w **hello fundusze portalu** strony, należy pobrać hello toosend **XML metadanych** za[hello zespołem pomocy technicznej fundusze Portal](mailto:info@regenteducation.com).</span><span class="sxs-lookup"><span data-stu-id="d70f9-190">tooconfigure single sign-on on **hello Funding Portal** side, you need toosend hello downloaded **Metadata XML** too[hello Funding Portal support team](mailto:info@regenteducation.com).</span></span> <span data-ttu-id="d70f9-191">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="d70f9-191">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d70f9-192">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="d70f9-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d70f9-193">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="d70f9-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d70f9-194">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d70f9-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d70f9-195">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d70f9-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="d70f9-196">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="d70f9-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="d70f9-198">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d70f9-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d70f9-199">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d70f9-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d70f9-201">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d70f9-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d70f9-203">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d70f9-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d70f9-205">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d70f9-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-thefundingportal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d70f9-207">a.</span><span class="sxs-lookup"><span data-stu-id="d70f9-207">a.</span></span> <span data-ttu-id="d70f9-208">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d70f9-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d70f9-209">b.</span><span class="sxs-lookup"><span data-stu-id="d70f9-209">b.</span></span> <span data-ttu-id="d70f9-210">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d70f9-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d70f9-211">c.</span><span class="sxs-lookup"><span data-stu-id="d70f9-211">c.</span></span> <span data-ttu-id="d70f9-212">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="d70f9-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d70f9-213">d.</span><span class="sxs-lookup"><span data-stu-id="d70f9-213">d.</span></span> <span data-ttu-id="d70f9-214">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d70f9-214">Click **Create**.</span></span>
 
### <a name="creating-hello-funding-portal-test-user"></a><span data-ttu-id="d70f9-215">Tworzenie użytkownika testowego hello fundusze portalu</span><span class="sxs-lookup"><span data-stu-id="d70f9-215">Creating hello Funding Portal test user</span></span>

<span data-ttu-id="d70f9-216">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w hello fundusze portalu.</span><span class="sxs-lookup"><span data-stu-id="d70f9-216">In this section, you create a user called Britta Simon in hello Funding Portal.</span></span> <span data-ttu-id="d70f9-217">Praca z [hello zespołem pomocy technicznej fundusze portalu](mailto:info@regenteducation.com) tooadd hello użytkownika testowego i włączenia funkcji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="d70f9-217">Work with [hello Funding Portal support team](mailto:info@regenteducation.com) tooadd hello test user and enable SSO.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d70f9-218">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d70f9-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d70f9-219">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu toohello fundusze portalu.</span><span class="sxs-lookup"><span data-stu-id="d70f9-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access toohello Funding Portal.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="d70f9-221">**tooassign toohello Simona Britta fundusze portalu, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d70f9-221">**tooassign Britta Simon toohello Funding Portal, perform hello following steps:**</span></span>

1. <span data-ttu-id="d70f9-222">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d70f9-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d70f9-224">Z listy aplikacji hello wybierz **hello fundusze Portal**.</span><span class="sxs-lookup"><span data-stu-id="d70f9-224">In hello applications list, select **hello Funding Portal**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-thefundingportal-tutorial/tutorial_thefundingportal_app.png) 

3. <span data-ttu-id="d70f9-226">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d70f9-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="d70f9-228">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d70f9-228">Click **Add** button.</span></span> <span data-ttu-id="d70f9-229">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d70f9-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="d70f9-231">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d70f9-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d70f9-232">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d70f9-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d70f9-233">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d70f9-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d70f9-234">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d70f9-234">Testing single sign-on</span></span>

<span data-ttu-id="d70f9-235">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d70f9-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d70f9-236">Po kliknięciu kafelka fundusze portalu hello hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour hello fundusze portalu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d70f9-236">When you click hello hello Funding Portal tile in hello Access Panel, you should get automatically signed-on tooyour hello Funding Portal application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d70f9-237">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d70f9-237">Additional resources</span></span>

* [<span data-ttu-id="d70f9-238">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d70f9-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d70f9-239">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d70f9-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thefundingportal-tutorial/tutorial_general_203.png

