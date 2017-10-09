---
title: 'Samouczek: Integracji Azure Active Directory z Lesson.ly | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Lesson.ly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c9dc6e6-5d85-4553-8a35-c7137064b928
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 23b339dcc26471b42aaa7e1baadcb42500d6b7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lessonly"></a><span data-ttu-id="19747-103">Samouczek: Integracji Azure Active Directory z Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="19747-103">Tutorial: Azure Active Directory integration with Lesson.ly</span></span>

<span data-ttu-id="19747-104">Z tego samouczka, dowiesz się, jak toointegrate Lesson.ly w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="19747-104">In this tutorial, you learn how toointegrate Lesson.ly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="19747-105">Integracja z usługą Azure AD Lesson.ly zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="19747-105">Integrating Lesson.ly with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="19747-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooLesson.ly</span><span class="sxs-lookup"><span data-stu-id="19747-106">You can control in Azure AD who has access tooLesson.ly</span></span>
- <span data-ttu-id="19747-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooLesson.ly (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="19747-107">You can enable your users tooautomatically get signed-on tooLesson.ly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="19747-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="19747-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="19747-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="19747-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19747-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="19747-110">Prerequisites</span></span>

<span data-ttu-id="19747-111">tooconfigure integracji z usługą Azure AD z Lesson.ly należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="19747-111">tooconfigure Azure AD integration with Lesson.ly, you need hello following items:</span></span>

- <span data-ttu-id="19747-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="19747-112">An Azure AD subscription</span></span>
- <span data-ttu-id="19747-113">Lesson.ly logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="19747-113">A Lesson.ly single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="19747-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="19747-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="19747-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="19747-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="19747-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="19747-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="19747-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="19747-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="19747-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="19747-118">Scenario description</span></span>
<span data-ttu-id="19747-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="19747-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="19747-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="19747-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="19747-121">Dodawanie Lesson.ly z galerii hello</span><span class="sxs-lookup"><span data-stu-id="19747-121">Adding Lesson.ly from hello gallery</span></span>
2. <span data-ttu-id="19747-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="19747-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lessonly-from-hello-gallery"></a><span data-ttu-id="19747-123">Dodawanie Lesson.ly z galerii hello</span><span class="sxs-lookup"><span data-stu-id="19747-123">Adding Lesson.ly from hello gallery</span></span>
<span data-ttu-id="19747-124">tooconfigure hello integracji Lesson.ly do usługi Azure AD, należy tooadd Lesson.ly z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="19747-124">tooconfigure hello integration of Lesson.ly into Azure AD, you need tooadd Lesson.ly from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="19747-125">**tooadd Lesson.ly z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="19747-125">**tooadd Lesson.ly from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="19747-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="19747-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="19747-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="19747-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="19747-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="19747-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="19747-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="19747-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="19747-133">W polu wyszukiwania hello wpisz **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="19747-133">In hello search box, type **Lesson.ly**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_search.png)

5. <span data-ttu-id="19747-135">W panelu wyników hello zaznacz **Lesson.ly**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="19747-135">In hello results panel, select **Lesson.ly**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="19747-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="19747-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="19747-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Lesson.ly w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="19747-138">In this section, you configure and test Azure AD single sign-on with Lesson.ly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="19747-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Lesson.ly jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19747-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lesson.ly is tooa user in Azure AD.</span></span> <span data-ttu-id="19747-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Lesson.ly musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="19747-140">In other words, a link relationship between an Azure AD user and hello related user in Lesson.ly needs toobe established.</span></span>

<span data-ttu-id="19747-141">W Lesson.ly, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="19747-141">In Lesson.ly, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="19747-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Lesson.ly, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="19747-142">tooconfigure and test Azure AD single sign-on with Lesson.ly, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="19747-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="19747-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="19747-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="19747-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="19747-145">**[Tworzenie użytkownika testowego Lesson.ly](#creating-a-lessonly-test-user)**  -toohave odpowiednikiem Simona Britta w Lesson.ly, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="19747-145">**[Creating a Lesson.ly test user](#creating-a-lessonly-test-user)** - toohave a counterpart of Britta Simon in Lesson.ly that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="19747-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="19747-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="19747-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="19747-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="19747-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="19747-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="19747-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="19747-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lesson.ly application.</span></span>

<span data-ttu-id="19747-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Lesson.ly, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="19747-150">**tooconfigure Azure AD single sign-on with Lesson.ly, perform hello following steps:**</span></span>

1. <span data-ttu-id="19747-151">W portalu Azure na powitania hello **Lesson.ly** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="19747-151">In hello Azure portal, on hello **Lesson.ly** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="19747-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="19747-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_samlbase.png)

3. <span data-ttu-id="19747-155">Na powitania **Lesson.ly domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="19747-155">On hello **Lesson.ly Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_url.png)

    <span data-ttu-id="19747-157">a.</span><span class="sxs-lookup"><span data-stu-id="19747-157">a.</span></span> <span data-ttu-id="19747-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="19747-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/signin`|
    | `https://<companyname>.lessonly.com/signin`|

    >[!NOTE]
    ><span data-ttu-id="19747-159">Gdy odwołanie do ogólnego nazw, które **NazwaFirmy** musi toobe zastępuje rzeczywistą nazwą.</span><span class="sxs-lookup"><span data-stu-id="19747-159">When referencing a generic name that **companyname** needs toobe replaced by an actual name.</span></span>
    
    <span data-ttu-id="19747-160">b.</span><span class="sxs-lookup"><span data-stu-id="19747-160">b.</span></span> <span data-ttu-id="19747-161">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="19747-161">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.lesson.ly/auth/saml/metadata`|
    | `https://<companyname>.lessonly.com/auth/saml/metadata`|

    > [!NOTE] 
    > <span data-ttu-id="19747-162">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="19747-162">These values are not real.</span></span> <span data-ttu-id="19747-163">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="19747-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="19747-164">Skontaktuj się z [zespołem pomocy technicznej klienta Lesson.ly](mailto:dev@lessonly.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="19747-164">Contact [Lesson.ly Client support team](mailto:dev@lessonly.com) tooget these values.</span></span> 

4. <span data-ttu-id="19747-165">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="19747-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_certificate.png)

5. <span data-ttu-id="19747-167">Lesson.ly aplikacji Hello oczekuje potwierdzenia SAML hello w określonym formacie wymaga tooyour mapowań atrybutów niestandardowych tooadd **atrybuty tokenu SAML** configuration.hello po zrzut ekranu przedstawia przykład Ta.</span><span class="sxs-lookup"><span data-stu-id="19747-167">hello Lesson.ly application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.hello following screenshot shows an example for this.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lessonly-tutorial/tutorial_lessonly_06.png)
           
6. <span data-ttu-id="19747-169">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, Konfigurowanie atrybutu tokenu SAML, jak pokazano w hello poprzedzających obrazu i wykonywanie hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="19747-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>

    | <span data-ttu-id="19747-170">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="19747-170">Attribute Name</span></span>   | <span data-ttu-id="19747-171">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="19747-171">Attribute Value</span></span> |
    | ---------------  | ----------------|
    | <span data-ttu-id="19747-172">urn: oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="19747-172">urn:oid:2.5.4.42</span></span> |<span data-ttu-id="19747-173">User.givenName</span><span class="sxs-lookup"><span data-stu-id="19747-173">user.givenname</span></span> |
    | <span data-ttu-id="19747-174">urn: oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="19747-174">urn:oid:2.5.4.4</span></span>  |<span data-ttu-id="19747-175">User.surname</span><span class="sxs-lookup"><span data-stu-id="19747-175">user.surname</span></span> |
    | <span data-ttu-id="19747-176">urn: oid:0.9.2342.19200300.1001.3</span><span class="sxs-lookup"><span data-stu-id="19747-176">urn:oid:0.9.2342.19200300.1001.3</span></span> |<span data-ttu-id="19747-177">User.mail</span><span class="sxs-lookup"><span data-stu-id="19747-177">user.mail</span></span> |

    <span data-ttu-id="19747-178">a.</span><span class="sxs-lookup"><span data-stu-id="19747-178">a.</span></span> <span data-ttu-id="19747-179">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="19747-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lessonly-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="19747-182">b.</span><span class="sxs-lookup"><span data-stu-id="19747-182">b.</span></span> <span data-ttu-id="19747-183">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="19747-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="19747-184">c.</span><span class="sxs-lookup"><span data-stu-id="19747-184">c.</span></span> <span data-ttu-id="19747-185">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="19747-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="19747-186">d.</span><span class="sxs-lookup"><span data-stu-id="19747-186">d.</span></span> <span data-ttu-id="19747-187">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="19747-187">Click **Ok**.</span></span>     

7. <span data-ttu-id="19747-188">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="19747-188">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lessonly-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="19747-190">Na powitania **konfiguracji Lesson.ly** kliknij **skonfigurować Lesson.ly** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="19747-190">On hello **Lesson.ly Configuration** section, click **Configure Lesson.ly** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="19747-191">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="19747-191">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_configure.png)

9. <span data-ttu-id="19747-193">tooconfigure rejestracji jednokrotnej w **Lesson.ly** strony, należy pobrać hello toosend **Certificate(Base64)** i **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** za[zespołem pomocy technicznej Lesson.ly](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="19747-193">tooconfigure single sign-on on **Lesson.ly** side, you need toosend hello downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

> [!TIP]
> <span data-ttu-id="19747-194">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="19747-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="19747-195">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="19747-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="19747-196">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="19747-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="19747-197">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="19747-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="19747-198">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="19747-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="19747-200">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="19747-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="19747-201">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="19747-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="19747-203">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="19747-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="19747-205">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="19747-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="19747-207">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="19747-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-lessonly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="19747-209">a.</span><span class="sxs-lookup"><span data-stu-id="19747-209">a.</span></span> <span data-ttu-id="19747-210">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="19747-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="19747-211">b.</span><span class="sxs-lookup"><span data-stu-id="19747-211">b.</span></span> <span data-ttu-id="19747-212">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="19747-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="19747-213">c.</span><span class="sxs-lookup"><span data-stu-id="19747-213">c.</span></span> <span data-ttu-id="19747-214">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="19747-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="19747-215">d.</span><span class="sxs-lookup"><span data-stu-id="19747-215">d.</span></span> <span data-ttu-id="19747-216">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="19747-216">Click **Create**.</span></span>
 
### <a name="creating-a-lessonly-test-user"></a><span data-ttu-id="19747-217">Tworzenie użytkownika testowego Lesson.ly</span><span class="sxs-lookup"><span data-stu-id="19747-217">Creating a Lesson.ly test user</span></span>

<span data-ttu-id="19747-218">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Lesson.ly.</span><span class="sxs-lookup"><span data-stu-id="19747-218">hello objective of this section is toocreate a user called Britta Simon in Lesson.ly.</span></span> <span data-ttu-id="19747-219">Lesson.LY obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="19747-219">Lesson.ly supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="19747-220">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="19747-220">There is no action item for you in this section.</span></span> <span data-ttu-id="19747-221">Nowy użytkownik zostanie utworzony podczas próby tooaccess Lesson.ly, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="19747-221">A new user will be created during an attempt tooaccess Lesson.ly if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="19747-222">Jeśli potrzebujesz ręcznie toocreate użytkownika, należy toocontact hello [zespołem pomocy technicznej Lesson.ly](mailto:dev@lessonly.com).</span><span class="sxs-lookup"><span data-stu-id="19747-222">If you need toocreate an user manually, you need toocontact hello [Lesson.ly support team](mailto:dev@lessonly.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="19747-223">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="19747-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="19747-224">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooLesson.ly.</span><span class="sxs-lookup"><span data-stu-id="19747-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLesson.ly.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="19747-226">**tooassign tooLesson.ly Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="19747-226">**tooassign Britta Simon tooLesson.ly, perform hello following steps:**</span></span>

1. <span data-ttu-id="19747-227">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="19747-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="19747-229">Z listy aplikacji hello wybierz **Lesson.ly**.</span><span class="sxs-lookup"><span data-stu-id="19747-229">In hello applications list, select **Lesson.ly**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-lessonly-tutorial/tutorial_lesson.ly_app.png) 

3. <span data-ttu-id="19747-231">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="19747-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="19747-233">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="19747-233">Click **Add** button.</span></span> <span data-ttu-id="19747-234">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="19747-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="19747-236">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="19747-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="19747-237">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="19747-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="19747-238">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="19747-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="19747-239">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="19747-239">Testing single sign-on</span></span>

<span data-ttu-id="19747-240">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="19747-240">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="19747-241">Po kliknięciu kafelka Lesson.ly hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Lesson.ly aplikacji.</span><span class="sxs-lookup"><span data-stu-id="19747-241">When you click hello Lesson.ly tile in hello Access Panel, you should get automatically signed-on tooyour Lesson.ly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="19747-242">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="19747-242">Additional resources</span></span>

* [<span data-ttu-id="19747-243">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="19747-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="19747-244">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="19747-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lessonly-tutorial/tutorial_general_203.png

