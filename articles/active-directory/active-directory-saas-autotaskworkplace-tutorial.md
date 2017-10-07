---
title: 'Samouczek: Integracji Azure Active Directory z miejsca pracy Autotask | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Autotask w miejscu pracy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a9a7ff71-c389-4169-aafd-d7a505244797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 7f820f24e8e9493fa2e1c075f2ef61d7eaa84f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-autotask-workplace"></a><span data-ttu-id="47aab-103">Samouczek: Integracji Azure Active Directory z Autotask w miejscu pracy</span><span class="sxs-lookup"><span data-stu-id="47aab-103">Tutorial: Azure Active Directory integration with Autotask Workplace</span></span>

<span data-ttu-id="47aab-104">Z tego samouczka, dowiesz się, jak toointegrate Autotask pracy z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="47aab-104">In this tutorial, you learn how toointegrate Autotask Workplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="47aab-105">Integrowanie Autotask miejsca pracy z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="47aab-105">Integrating Autotask Workplace with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="47aab-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooAutotask miejsca pracy</span><span class="sxs-lookup"><span data-stu-id="47aab-106">You can control in Azure AD who has access tooAutotask Workplace</span></span>
- <span data-ttu-id="47aab-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAutotask pracy (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="47aab-107">You can enable your users tooautomatically get signed-on tooAutotask Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="47aab-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="47aab-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="47aab-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="47aab-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47aab-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="47aab-110">Prerequisites</span></span>

<span data-ttu-id="47aab-111">tooconfigure integracji usługi Azure AD z miejsca pracy Autotask należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="47aab-111">tooconfigure Azure AD integration with Autotask Workplace, you need hello following items:</span></span>

- <span data-ttu-id="47aab-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="47aab-112">An Azure AD subscription</span></span>
- <span data-ttu-id="47aab-113">Obszar roboczy Autotask jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="47aab-113">An Autotask Workplace single-sign on enabled subscription</span></span>
- <span data-ttu-id="47aab-114">Musi być administratora lub administratora administrator w miejscu pracy.</span><span class="sxs-lookup"><span data-stu-id="47aab-114">You must be an administrator or super administrator in Workplace.</span></span>
- <span data-ttu-id="47aab-115">Musi mieć konto administratora w hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47aab-115">You must have an administrator account in hello Azure AD.</span></span>
- <span data-ttu-id="47aab-116">Witaj użytkowników, którzy będą korzystać z tej funkcji, muszą mieć konta w miejscu pracy i hello Azure AD, a ich adresów e-mail, oba muszą być zgodne.</span><span class="sxs-lookup"><span data-stu-id="47aab-116">hello users that will utilize this feature must have accounts within Workplace and hello Azure AD, and their email addresses for both must match.</span></span>

> [!NOTE]
> <span data-ttu-id="47aab-117">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="47aab-117">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="47aab-118">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="47aab-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="47aab-119">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="47aab-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="47aab-120">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="47aab-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="47aab-121">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="47aab-121">Scenario description</span></span>
<span data-ttu-id="47aab-122">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="47aab-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="47aab-123">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="47aab-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="47aab-124">Dodawanie miejsca pracy Autotask z galerii hello</span><span class="sxs-lookup"><span data-stu-id="47aab-124">Adding Autotask Workplace from hello gallery</span></span>
2. <span data-ttu-id="47aab-125">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="47aab-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-autotask-workplace-from-hello-gallery"></a><span data-ttu-id="47aab-126">Dodawanie miejsca pracy Autotask z galerii hello</span><span class="sxs-lookup"><span data-stu-id="47aab-126">Adding Autotask Workplace from hello gallery</span></span>
<span data-ttu-id="47aab-127">tooconfigure hello integracji Autotask dołączanie do usługi Azure AD, należy tooadd Autotask miejsca pracy z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="47aab-127">tooconfigure hello integration of Autotask Workplace into Azure AD, you need tooadd Autotask Workplace from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="47aab-128">**tooadd Autotask w miejscu pracy na powitania galerii, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="47aab-128">**tooadd Autotask Workplace from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="47aab-129">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="47aab-129">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="47aab-131">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="47aab-131">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="47aab-132">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="47aab-132">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="47aab-134">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="47aab-134">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="47aab-136">W polu wyszukiwania hello wpisz **Autotask w miejscu pracy**, wybierz pozycję **Autotask w miejscu pracy** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="47aab-136">In hello search box, type **Autotask Workplace**, select  **Autotask Workplace**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Obszar roboczy Autotask w hello liście wyników](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="47aab-138">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="47aab-138">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="47aab-139">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z miejsca pracy Autotask oparte na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="47aab-139">In this section, you configure and test Azure AD single sign-on with Autotask Workplace based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="47aab-140">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w miejscu pracy Autotask jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47aab-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Autotask Workplace is tooa user in Azure AD.</span></span> <span data-ttu-id="47aab-141">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w miejscu pracy Autotask musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="47aab-141">In other words, a link relationship between an Azure AD user and hello related user in Autotask Workplace needs toobe established.</span></span>

<span data-ttu-id="47aab-142">W obszarze roboczym Autotask, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="47aab-142">In Autotask Workplace, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="47aab-143">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Autotask w miejscu pracy, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="47aab-143">tooconfigure and test Azure AD single sign-on with Autotask Workplace, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="47aab-144">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="47aab-144">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="47aab-145">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="47aab-145">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="47aab-146">**[Tworzenie użytkownika testowego pracy Autotask](#create-an-autotask-workplace-test-user)**  -toohave odpowiednikiem Simona Britta w pracy Autotask, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="47aab-146">**[Create an Autotask Workplace test user](#create-an-autotask-workplace-test-user)** - toohave a counterpart of Britta Simon in Autotask Workplace that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="47aab-147">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="47aab-147">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="47aab-148">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="47aab-148">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="47aab-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="47aab-149">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="47aab-150">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w miejscu pracy Autotask aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47aab-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Autotask Workplace application.</span></span>

<span data-ttu-id="47aab-151">**tooconfigure usługi Azure AD rejestracji jednokrotnej z miejsca pracy Autotask, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="47aab-151">**tooconfigure Azure AD single sign-on with Autotask Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="47aab-152">W portalu Azure na powitania hello **pracy Autotask** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="47aab-152">In hello Azure portal, on hello **Autotask Workplace** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="47aab-154">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="47aab-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_samlbase.png)

3. <span data-ttu-id="47aab-156">Jeśli chcesz, aby aplikacja hello tooconfigure w **IDP** inicjowane tryb, wykonaj następujące kroki na powitania hello **Autotask Dołączanie domeny i adres URL** sekcji:</span><span class="sxs-lookup"><span data-stu-id="47aab-156">If you wish tooconfigure hello application in **IDP** initiated mode, perform hello following steps on hello **Autotask Workplace Domain and URLs** section:</span></span>

    ![Dołączanie Autotask domeny i adres URL pojedynczego logowania jednokrotnego informacje dotyczące IDP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url.png)

    <span data-ttu-id="47aab-158">a.</span><span class="sxs-lookup"><span data-stu-id="47aab-158">a.</span></span> <span data-ttu-id="47aab-159">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="47aab-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`</span></span>

    <span data-ttu-id="47aab-160">b.</span><span class="sxs-lookup"><span data-stu-id="47aab-160">b.</span></span> <span data-ttu-id="47aab-161">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="47aab-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`</span></span>

4. <span data-ttu-id="47aab-162">Jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane trybie wyboru **Pokaż zaawansowane ustawienia adresu URL** i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="47aab-162">If you wish tooconfigure hello application in **SP** initiated mode, check **Show advanced URL settings** and perform hello following steps:</span></span>

    ![Dołączanie Autotask domeny i adres URL pojedynczego logowania jednokrotnego informacje dotyczące SP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url1.png)

    <span data-ttu-id="47aab-164">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.awp.autotask.net/loginsso`</span><span class="sxs-lookup"><span data-stu-id="47aab-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awp.autotask.net/loginsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="47aab-165">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="47aab-165">These values are not real.</span></span> <span data-ttu-id="47aab-166">Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="47aab-166">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="47aab-167">Skontaktuj się z [zespołem pomocy technicznej Autotask miejsca pracy klienta](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="47aab-167">Contact [Autotask Workplace Client support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget these values.</span></span> 

5. <span data-ttu-id="47aab-168">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="47aab-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_certificate.png) 

6. <span data-ttu-id="47aab-170">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="47aab-170">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="47aab-172">W oknie przeglądarki innej witryny sieci web logowanie się za pomocą Online tooWorkplace hello poświadczenia administratora.</span><span class="sxs-lookup"><span data-stu-id="47aab-172">In a different web browser window, Log in tooWorkplace Online using hello administrator credentials.</span></span>

    >[!Note]
    ><span data-ttu-id="47aab-173">Konfigurując hello IdP poddomeny należy toobe określony.</span><span class="sxs-lookup"><span data-stu-id="47aab-173">When configuring hello IdP, a subdomain will need toobe specified.</span></span> <span data-ttu-id="47aab-174">tooconfirm hello poprawne poddomeny, tooWorkplace logowania w trybie Online.</span><span class="sxs-lookup"><span data-stu-id="47aab-174">tooconfirm hello correct subdomain, login tooWorkplace Online.</span></span> <span data-ttu-id="47aab-175">Po zalogowaniu, dokonaj poddomeny toohello Uwaga hello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="47aab-175">Once logged in, make note toohello subdomain in hello URL.</span></span>
    ><span data-ttu-id="47aab-176">poddomeny Hello wchodzi powitania "hello"https://"i".awp.autotask.net/"i powinien być nam, Europa, urząd certyfikacji lub Australia.</span><span class="sxs-lookup"><span data-stu-id="47aab-176">hello subdomain is hello part between hello “https://“ and “.awp.autotask.net/“ and should be us, eu, ca, or au.</span></span>

8. <span data-ttu-id="47aab-177">Przejdź za**konfiguracji** > **rejestracji jednokrotnej** i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="47aab-177">Go too**Configuration** > **Single Sign-On** and perform hello following steps:</span></span>

    ![Jednym Autotask logowania jednokrotnego konfiguracji](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig1.png)
 
    <span data-ttu-id="47aab-179">a.</span><span class="sxs-lookup"><span data-stu-id="47aab-179">a.</span></span> <span data-ttu-id="47aab-180">Wybierz hello **pliku metadanych XML** opcji, a następnie przekaż hello **XML metadanych** pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="47aab-180">Select hello **XML Metadata File** option, and then upload hello **Metadata XML** downloaded from Azure portal.</span></span>

    <span data-ttu-id="47aab-181">b.</span><span class="sxs-lookup"><span data-stu-id="47aab-181">b.</span></span> <span data-ttu-id="47aab-182">Kliknij przycisk **włączenia funkcji logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="47aab-182">Click **Enable SSO**.</span></span>
    
    ![Autotask jednokrotnej Zatwierdzanie konfiguracji](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig2.png)

    <span data-ttu-id="47aab-184">c.</span><span class="sxs-lookup"><span data-stu-id="47aab-184">c.</span></span> <span data-ttu-id="47aab-185">Wybierz hello **potwierdzam, te informacje są poprawne i można zaufać tym IdP** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="47aab-185">Select hello **I confirm this information is correct and I trust this IdP** check box.</span></span>

    <span data-ttu-id="47aab-186">d.</span><span class="sxs-lookup"><span data-stu-id="47aab-186">d.</span></span> <span data-ttu-id="47aab-187">Kliknij przycisk **zatwierdzić**.</span><span class="sxs-lookup"><span data-stu-id="47aab-187">Click **Approve**.</span></span>
     
>[!Note]
><span data-ttu-id="47aab-188">Jeśli potrzebujesz pomocy przy konfigurowaniu Autotask w miejscu pracy, zobacz [tej strony](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget pomocy z konta firmowego.</span><span class="sxs-lookup"><span data-stu-id="47aab-188">If you require assistance with configuring Autotask Workplace, please see [this page](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget assistance with your Workplace account.</span></span>

> [!TIP]
> <span data-ttu-id="47aab-189">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="47aab-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="47aab-190">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="47aab-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="47aab-191">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="47aab-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="47aab-192">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="47aab-192">Create an Azure AD test user</span></span>

<span data-ttu-id="47aab-193">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="47aab-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="47aab-195">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="47aab-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="47aab-196">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="47aab-196">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="47aab-198">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="47aab-198">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="47aab-200">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="47aab-200">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="47aab-202">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="47aab-202">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="47aab-204">a.</span><span class="sxs-lookup"><span data-stu-id="47aab-204">a.</span></span> <span data-ttu-id="47aab-205">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="47aab-205">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="47aab-206">b.</span><span class="sxs-lookup"><span data-stu-id="47aab-206">b.</span></span> <span data-ttu-id="47aab-207">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="47aab-207">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="47aab-208">c.</span><span class="sxs-lookup"><span data-stu-id="47aab-208">c.</span></span> <span data-ttu-id="47aab-209">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="47aab-209">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="47aab-210">d.</span><span class="sxs-lookup"><span data-stu-id="47aab-210">d.</span></span> <span data-ttu-id="47aab-211">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="47aab-211">Click **Create**.</span></span>

### <a name="create-an-autotask-workplace-test-user"></a><span data-ttu-id="47aab-212">Tworzenie użytkownika testowego Autotask w miejscu pracy</span><span class="sxs-lookup"><span data-stu-id="47aab-212">Create an Autotask Workplace test user</span></span>

<span data-ttu-id="47aab-213">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Autotask.</span><span class="sxs-lookup"><span data-stu-id="47aab-213">In this section, you create a user called Britta Simon in Autotask.</span></span> <span data-ttu-id="47aab-214">We współpracy z [Autotask pracy zespołu pomocy technicznej](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooadd hello użytkowników w hello platformy Autotask w miejscu pracy.</span><span class="sxs-lookup"><span data-stu-id="47aab-214">Please work with [Autotask Workplace support team](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooadd hello users in hello Autotask Workplace platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="47aab-215">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="47aab-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="47aab-216">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooAutotask miejsca pracy.</span><span class="sxs-lookup"><span data-stu-id="47aab-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAutotask Workplace.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="47aab-218">**tooassign tooAutotask Simona Britta miejsca pracy, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="47aab-218">**tooassign Britta Simon tooAutotask Workplace, perform hello following steps:**</span></span>

1. <span data-ttu-id="47aab-219">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="47aab-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="47aab-221">Z listy aplikacji hello wybierz **pracy Autotask**.</span><span class="sxs-lookup"><span data-stu-id="47aab-221">In hello applications list, select **Autotask Workplace**.</span></span>

    ![Witaj łącze Autotask w miejscu pracy na liście aplikacji hello](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_app.png) 

3. <span data-ttu-id="47aab-223">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="47aab-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="47aab-225">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="47aab-225">Click **Add** button.</span></span> <span data-ttu-id="47aab-226">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="47aab-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="47aab-228">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="47aab-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="47aab-229">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="47aab-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="47aab-230">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="47aab-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="47aab-231">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="47aab-231">Test single sign-on</span></span>

<span data-ttu-id="47aab-232">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="47aab-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="47aab-233">Po kliknięciu hello pracy Autotask kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Autotask pracy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47aab-233">When you click hello Autotask Workplace tile in hello Access Panel, you should get automatically signed-on tooyour Autotask Workplace application.</span></span>
<span data-ttu-id="47aab-234">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="47aab-234">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="47aab-235">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="47aab-235">Additional resources</span></span>

* [<span data-ttu-id="47aab-236">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="47aab-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="47aab-237">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="47aab-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_203.png

