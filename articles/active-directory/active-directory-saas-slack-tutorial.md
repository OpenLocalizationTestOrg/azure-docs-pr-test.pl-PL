---
title: 'Samouczek: Integracji Azure Active Directory z zapas czasu | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i zapas czasu."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 7f0151401af4dc63d2f714d4b4f66380c4b51e0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a><span data-ttu-id="08238-103">Samouczek: Integracji Azure Active Directory z zapas czasu</span><span class="sxs-lookup"><span data-stu-id="08238-103">Tutorial: Azure Active Directory integration with Slack</span></span>

<span data-ttu-id="08238-104">Z tego samouczka, dowiesz się, jak toointegrate Slack z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="08238-104">In this tutorial, you learn how toointegrate Slack with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="08238-105">Integrowanie zapas czasu z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="08238-105">Integrating Slack with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="08238-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooSlack</span><span class="sxs-lookup"><span data-stu-id="08238-106">You can control in Azure AD who has access tooSlack</span></span>
- <span data-ttu-id="08238-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSlack (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="08238-107">You can enable your users tooautomatically get signed-on tooSlack (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="08238-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="08238-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="08238-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="08238-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08238-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="08238-110">Prerequisites</span></span>

<span data-ttu-id="08238-111">tooconfigure integracji usługi Azure AD z zapas czasu, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="08238-111">tooconfigure Azure AD integration with Slack, you need hello following items:</span></span>

- <span data-ttu-id="08238-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="08238-112">An Azure AD subscription</span></span>
- <span data-ttu-id="08238-113">Slack logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="08238-113">A Slack single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="08238-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="08238-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="08238-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="08238-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="08238-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="08238-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="08238-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="08238-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="08238-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="08238-118">Scenario description</span></span>
<span data-ttu-id="08238-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="08238-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="08238-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="08238-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="08238-121">Dodawanie zapas czasu z galerii hello</span><span class="sxs-lookup"><span data-stu-id="08238-121">Adding Slack from hello gallery</span></span>
2. <span data-ttu-id="08238-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="08238-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-slack-from-hello-gallery"></a><span data-ttu-id="08238-123">Dodawanie zapas czasu z galerii hello</span><span class="sxs-lookup"><span data-stu-id="08238-123">Adding Slack from hello gallery</span></span>
<span data-ttu-id="08238-124">integracji hello tooconfigure zapas czasu w usłudze Azure Active Directory, należy tooadd zapas czasu z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="08238-124">tooconfigure hello integration of Slack into Azure AD, you need tooadd Slack from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="08238-125">**tooadd zapas czasu z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="08238-125">**tooadd Slack from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="08238-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="08238-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="08238-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="08238-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="08238-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="08238-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="08238-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="08238-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="08238-133">W polu wyszukiwania hello wpisz **Slack**.</span><span class="sxs-lookup"><span data-stu-id="08238-133">In hello search box, type **Slack**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. <span data-ttu-id="08238-135">W panelu wyników hello zaznacz **zapas czasu**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="08238-135">In hello results panel, select **Slack**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="08238-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="08238-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="08238-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z zapas czasu, w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="08238-138">In this section, you configure and test Azure AD single sign-on with Slack based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="08238-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w zapas czasu jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="08238-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Slack is tooa user in Azure AD.</span></span> <span data-ttu-id="08238-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w zapas czasu musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="08238-140">In other words, a link relationship between an Azure AD user and hello related user in Slack needs toobe established.</span></span>

<span data-ttu-id="08238-141">W zapas czasu, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="08238-141">In Slack, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="08238-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z zapas czasu, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="08238-142">tooconfigure and test Azure AD single sign-on with Slack, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="08238-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="08238-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="08238-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="08238-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="08238-145">**[Tworzenie użytkownika testowego Slack](#creating-a-slack-test-user)**  -toohave odpowiednikiem Simona Britta w zapas czasu, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="08238-145">**[Creating a Slack test user](#creating-a-slack-test-user)** - toohave a counterpart of Britta Simon in Slack that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="08238-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="08238-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="08238-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="08238-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="08238-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="08238-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="08238-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne Slack aplikacji.</span><span class="sxs-lookup"><span data-stu-id="08238-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Slack application.</span></span>

<span data-ttu-id="08238-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z zapas czasu, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="08238-150">**tooconfigure Azure AD single sign-on with Slack, perform hello following steps:**</span></span>

1. <span data-ttu-id="08238-151">W portalu Azure na powitania hello **Slack** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="08238-151">In hello Azure portal, on hello **Slack** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="08238-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="08238-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. <span data-ttu-id="08238-155">Na powitania **domeny zapas czasu i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="08238-155">On hello **Slack Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    <span data-ttu-id="08238-157">a.</span><span class="sxs-lookup"><span data-stu-id="08238-157">a.</span></span> <span data-ttu-id="08238-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.slack.com`</span><span class="sxs-lookup"><span data-stu-id="08238-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.slack.com`</span></span>

    <span data-ttu-id="08238-159">b.</span><span class="sxs-lookup"><span data-stu-id="08238-159">b.</span></span> <span data-ttu-id="08238-160">W hello **identyfikator** pole tekstowe, wprowadź adres URL hello:`https://slack.com`</span><span class="sxs-lookup"><span data-stu-id="08238-160">In hello **Identifier** textbox, type hello URL: `https://slack.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="08238-161">wartość Hello nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="08238-161">hello value is not real.</span></span> <span data-ttu-id="08238-162">Masz tooupdate hello wartości z hello rzeczywiste na adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="08238-162">You have tooupdate hello value with hello actual Sign On URL.</span></span> <span data-ttu-id="08238-163">Skontaktuj się z [zespołem pomocy technicznej Slack](https://slack.com/help/contact) tooget hello wartość</span><span class="sxs-lookup"><span data-stu-id="08238-163">Contact [Slack support team](https://slack.com/help/contact) tooget hello value</span></span>
     
4. <span data-ttu-id="08238-164">Slack aplikacji oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="08238-164">Slack application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="08238-165">Skonfiguruj powitania po oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="08238-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="08238-166">Można zarządzać hello wartości tych atrybutów z hello "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="08238-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="08238-167">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="08238-167">hello following screenshot shows an example for this.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. <span data-ttu-id="08238-169">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **user.mail** jako **identyfikator użytkownika** i dla każdego wiersza wyświetlany w poniższej tabeli hello wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="08238-169">In hello **User Attributes** section on hello **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in hello table below, perform hello following steps:</span></span>
    
    | <span data-ttu-id="08238-170">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="08238-170">Attribute Name</span></span> | <span data-ttu-id="08238-171">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="08238-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="08238-172">Imię</span><span class="sxs-lookup"><span data-stu-id="08238-172">first_name</span></span> | <span data-ttu-id="08238-173">User.givenName</span><span class="sxs-lookup"><span data-stu-id="08238-173">user.givenname</span></span> |
    | <span data-ttu-id="08238-174">nazwisko</span><span class="sxs-lookup"><span data-stu-id="08238-174">last_name</span></span> | <span data-ttu-id="08238-175">User.surname</span><span class="sxs-lookup"><span data-stu-id="08238-175">user.surname</span></span> |
    | <span data-ttu-id="08238-176">User.Email</span><span class="sxs-lookup"><span data-stu-id="08238-176">User.Email</span></span> | <span data-ttu-id="08238-177">User.mail</span><span class="sxs-lookup"><span data-stu-id="08238-177">user.mail</span></span> |  
    | <span data-ttu-id="08238-178">User.Username</span><span class="sxs-lookup"><span data-stu-id="08238-178">User.Username</span></span> | <span data-ttu-id="08238-179">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="08238-179">user.userprincipalname</span></span> |

    <span data-ttu-id="08238-180">a.</span><span class="sxs-lookup"><span data-stu-id="08238-180">a.</span></span> <span data-ttu-id="08238-181">Polecenie **atrybutu** tooopen **atrybutu Edytuj** okna dialogowego pole i wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="08238-181">Click on **Attribute** tooopen **Edit Attribute** dialog box and perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    <span data-ttu-id="08238-183">a.</span><span class="sxs-lookup"><span data-stu-id="08238-183">a.</span></span> <span data-ttu-id="08238-184">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="08238-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="08238-185">b.</span><span class="sxs-lookup"><span data-stu-id="08238-185">b.</span></span> <span data-ttu-id="08238-186">Z hello **wartość** lista, hello wybierz atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="08238-186">From hello **Value** list, select hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="08238-187">c.</span><span class="sxs-lookup"><span data-stu-id="08238-187">c.</span></span> <span data-ttu-id="08238-188">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="08238-188">Click **OK**</span></span>

6. <span data-ttu-id="08238-189">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="08238-189">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. <span data-ttu-id="08238-191">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="08238-191">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="08238-193">Na powitania **konfiguracji zapas czasu** kliknij **skonfigurować zapas czasu** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="08238-193">On hello **Slack Configuration** section, click **Configure Slack** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="08238-194">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="08238-194">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  <span data-ttu-id="08238-196">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy Slack tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="08238-196">In a different web browser window, log in tooyour Slack company site as an administrator.</span></span>

10.  <span data-ttu-id="08238-197">Przejdź za**usługi Microsoft Azure AD** Przejdź zbyt**ustawień zespołu**.</span><span class="sxs-lookup"><span data-stu-id="08238-197">Navigate too**Microsoft Azure AD** then go too**Team Settings**.</span></span>

     ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  <span data-ttu-id="08238-199">W hello **ustawień zespołu** kliknij hello **uwierzytelniania** , a następnie kliknij pozycję **Zmień ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="08238-199">In hello **Team Settings** section, click hello **Authentication** tab, and then click **Change Settings**.</span></span>

     ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. <span data-ttu-id="08238-201">Na powitania **ustawienia uwierzytelniania SAML** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="08238-201">On hello **SAML Authentication Settings** dialog, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    <span data-ttu-id="08238-203">a.</span><span class="sxs-lookup"><span data-stu-id="08238-203">a.</span></span>  <span data-ttu-id="08238-204">W hello **SAML 2.0 punktu końcowego (HTTP)** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="08238-204">In hello **SAML 2.0 Endpoint (HTTP)** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="08238-205">b.</span><span class="sxs-lookup"><span data-stu-id="08238-205">b.</span></span>  <span data-ttu-id="08238-206">W hello **wystawcy dostawcy tożsamości** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="08238-206">In hello **Identity Provider Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="08238-207">c.</span><span class="sxs-lookup"><span data-stu-id="08238-207">c.</span></span>  <span data-ttu-id="08238-208">Otwórz plik certyfikatu pobrane w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu publicznego** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="08238-208">Open your downloaded certificate file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Public Certificate** textbox.</span></span>

    <span data-ttu-id="08238-209">d.</span><span class="sxs-lookup"><span data-stu-id="08238-209">d.</span></span> <span data-ttu-id="08238-210">Skonfiguruj hello powyżej trzy ustawienia odpowiednie dla swojego zespołu Slack.</span><span class="sxs-lookup"><span data-stu-id="08238-210">Configure hello above three settings as appropriate for your Slack team.</span></span> <span data-ttu-id="08238-211">Aby uzyskać więcej informacji na temat ustawień hello Znajdź hello **Przewodnik po konfiguracji logowania jednokrotnego zapas czasu jego** tutaj.</span><span class="sxs-lookup"><span data-stu-id="08238-211">For more information about hello settings, please find hello **Slack's SSO configuration guide** here.</span></span> `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    <span data-ttu-id="08238-212">e.</span><span class="sxs-lookup"><span data-stu-id="08238-212">e.</span></span>  <span data-ttu-id="08238-213">Kliknij przycisk **Zapisz konfigurację**.</span><span class="sxs-lookup"><span data-stu-id="08238-213">Click **Save Configuration**.</span></span>
     
    <!-- Deselect **Allow users toochange their email address**.

    e.  Select **Allow users toochoose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> <span data-ttu-id="08238-214">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="08238-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="08238-215">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="08238-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="08238-216">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="08238-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="08238-217">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="08238-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="08238-218">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="08238-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="08238-220">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="08238-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="08238-221">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="08238-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="08238-223">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="08238-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="08238-225">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="08238-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="08238-227">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="08238-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="08238-229">a.</span><span class="sxs-lookup"><span data-stu-id="08238-229">a.</span></span> <span data-ttu-id="08238-230">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="08238-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="08238-231">b.</span><span class="sxs-lookup"><span data-stu-id="08238-231">b.</span></span> <span data-ttu-id="08238-232">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="08238-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="08238-233">c.</span><span class="sxs-lookup"><span data-stu-id="08238-233">c.</span></span> <span data-ttu-id="08238-234">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="08238-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="08238-235">d.</span><span class="sxs-lookup"><span data-stu-id="08238-235">d.</span></span> <span data-ttu-id="08238-236">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="08238-236">Click **Create**.</span></span>
 
### <a name="creating-a-slack-test-user"></a><span data-ttu-id="08238-237">Tworzenie użytkownika testowego Slack</span><span class="sxs-lookup"><span data-stu-id="08238-237">Creating a Slack test user</span></span>

<span data-ttu-id="08238-238">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Slack.</span><span class="sxs-lookup"><span data-stu-id="08238-238">hello objective of this section is toocreate a user called Britta Simon in Slack.</span></span> <span data-ttu-id="08238-239">Zapas czasu obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="08238-239">Slack supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="08238-240">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="08238-240">There is no action item for you in this section.</span></span> <span data-ttu-id="08238-241">Nowy użytkownik został utworzony podczas tooaccess próba zapas czasu, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="08238-241">A new user is created during an attempt tooaccess Slack if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="08238-242">Jeśli potrzebujesz ręcznie toocreate użytkownika, należy tooContact [zespołem pomocy technicznej Slack](https://slack.com/help/contact).</span><span class="sxs-lookup"><span data-stu-id="08238-242">If you need toocreate a user manually, you need tooContact [Slack support team](https://slack.com/help/contact).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="08238-243">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="08238-243">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="08238-244">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSlack.</span><span class="sxs-lookup"><span data-stu-id="08238-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSlack.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="08238-246">**tooassign tooSlack Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="08238-246">**tooassign Britta Simon tooSlack, perform hello following steps:**</span></span>

1. <span data-ttu-id="08238-247">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="08238-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="08238-249">Z listy aplikacji hello wybierz **Slack**.</span><span class="sxs-lookup"><span data-stu-id="08238-249">In hello applications list, select **Slack**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. <span data-ttu-id="08238-251">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="08238-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="08238-253">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="08238-253">Click **Add** button.</span></span> <span data-ttu-id="08238-254">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="08238-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="08238-256">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="08238-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="08238-257">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="08238-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="08238-258">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="08238-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="08238-259">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="08238-259">Testing single sign-on</span></span>

<span data-ttu-id="08238-260">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="08238-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="08238-261">Po kliknięciu kafelka Slack hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Slack aplikacji.</span><span class="sxs-lookup"><span data-stu-id="08238-261">When you click hello Slack tile in hello Access Panel, you should get automatically signed-on tooyour Slack application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="08238-262">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="08238-262">Additional resources</span></span>

* [<span data-ttu-id="08238-263">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="08238-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="08238-264">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="08238-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

