---
title: "Samouczek: Integracji usługi Azure Active Directory z logowania jednokrotnego Procore | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Procore logowania jednokrotnego."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: bb918617f18ba3f44ddde469e6fc411977752f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a><span data-ttu-id="796cc-103">Samouczek: Integracji Azure Active Directory z Procore logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="796cc-103">Tutorial: Azure Active Directory integration with Procore SSO</span></span>

<span data-ttu-id="796cc-104">Z tego samouczka, dowiesz się, jak toointegrate Procore logowania jednokrotnego w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="796cc-104">In this tutorial, you learn how toointegrate Procore SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="796cc-105">Integracja z usługą Azure AD Procore logowania jednokrotnego zawiera hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="796cc-105">Integrating Procore SSO with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="796cc-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooProcore logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="796cc-106">You can control in Azure AD who has access tooProcore SSO</span></span>
- <span data-ttu-id="796cc-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooProcore SSO (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="796cc-107">You can enable your users tooautomatically get signed-on tooProcore SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="796cc-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="796cc-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="796cc-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="796cc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Procore SSO, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="796cc-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="796cc-110">Prerequisites</span></span>

<span data-ttu-id="796cc-111">tooconfigure integracji usługi Azure AD z Procore logowania jednokrotnego należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="796cc-111">tooconfigure Azure AD integration with Procore SSO, you need hello following items:</span></span>

- <span data-ttu-id="796cc-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="796cc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="796cc-113">Procore logowania jednokrotnego jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="796cc-113">A Procore SSO single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="796cc-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="796cc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="796cc-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="796cc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="796cc-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="796cc-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="796cc-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="796cc-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="796cc-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="796cc-118">Scenario description</span></span>
<span data-ttu-id="796cc-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="796cc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="796cc-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="796cc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="796cc-121">Dodawanie Procore rejestracji Jednokrotnej z galerii hello</span><span class="sxs-lookup"><span data-stu-id="796cc-121">Adding Procore SSO from hello gallery</span></span>
2. <span data-ttu-id="796cc-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="796cc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-procore-sso-from-hello-gallery"></a><span data-ttu-id="796cc-123">Dodawanie Procore rejestracji Jednokrotnej z galerii hello</span><span class="sxs-lookup"><span data-stu-id="796cc-123">Adding Procore SSO from hello gallery</span></span>
<span data-ttu-id="796cc-124">tooconfigure hello integracji Procore logowania jednokrotnego do usługi Azure AD, należy tooadd Procore rejestracji Jednokrotnej z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="796cc-124">tooconfigure hello integration of Procore SSO into Azure AD, you need tooadd Procore SSO from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="796cc-125">**tooadd Procore rejestracji Jednokrotnej z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="796cc-125">**tooadd Procore SSO from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="796cc-126">W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="796cc-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="796cc-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="796cc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="796cc-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="796cc-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="796cc-131">Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="796cc-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="796cc-133">W polu wyszukiwania hello wpisz **Procore logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="796cc-133">In hello search box, type **Procore SSO**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. <span data-ttu-id="796cc-135">W panelu wyników hello, wybierz **Procore logowania jednokrotnego**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="796cc-135">In hello results panel, select **Procore SSO**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="796cc-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="796cc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="796cc-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej Procore logowaniem jednokrotnym w oparciu o użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="796cc-138">In this section, you configure and test Azure AD single sign-on with Procore SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="796cc-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Procore rejestracji Jednokrotnej jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="796cc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Procore SSO is tooa user in Azure AD.</span></span> <span data-ttu-id="796cc-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Procore logowania jednokrotnego musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="796cc-140">In other words, a link relationship between an Azure AD user and hello related user in Procore SSO needs toobe established.</span></span>

<span data-ttu-id="796cc-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Procore logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="796cc-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Procore SSO.</span></span>

<span data-ttu-id="796cc-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Procore logowania jednokrotnego, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="796cc-142">tooconfigure and test Azure AD single sign-on with Procore SSO, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="796cc-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="796cc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="796cc-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="796cc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="796cc-145">**[Tworzenie użytkownika testowego Procore logowania jednokrotnego](#creating-a-procore-sso-test-user)**  -toohave odpowiednikiem Simona Britta w Procore logowania jednokrotnego, że jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="796cc-145">**[Creating a Procore SSO test user](#creating-a-procore-sso-test-user)** - toohave a counterpart of Britta Simon in Procore SSO that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="796cc-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="796cc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="796cc-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="796cc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="796cc-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="796cc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="796cc-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w aplikacji Procore logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="796cc-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Procore SSO application.</span></span>

<span data-ttu-id="796cc-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Procore logowanie Jednokrotne, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="796cc-150">**tooconfigure Azure AD single sign-on with Procore SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="796cc-151">W portalu zarządzania Azure hello na powitania **Procore logowania jednokrotnego** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="796cc-151">In hello Azure Management portal, on hello **Procore SSO** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="796cc-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="796cc-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. <span data-ttu-id="796cc-155">Na powitania **Procore domena logowania jednokrotnego i adresy URL** sekcji, hello użytkownik nie ma tooperform wszystkie kroki jako aplikacji hello już jest wstępna Integracja z usługą Azure.</span><span class="sxs-lookup"><span data-stu-id="796cc-155">On hello **Procore SSO Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. <span data-ttu-id="796cc-157">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="796cc-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. <span data-ttu-id="796cc-159">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="796cc-159">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="796cc-161">Na powitania **Procore konfiguracji logowania jednokrotnego** kliknij **Konfigurowanie logowania jednokrotnego Procore** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="796cc-161">On hello **Procore SSO Configuration** section, click **Configure Procore SSO** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="796cc-162">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="796cc-162">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. <span data-ttu-id="796cc-164">tooconfigure rejestracji jednokrotnej w **Procore logowania jednokrotnego** strona, witryny firmy procore tooyour logowania jako administrator.</span><span class="sxs-lookup"><span data-stu-id="796cc-164">tooconfigure single sign-on on **Procore SSO** side, login tooyour procore company site as an administrator.</span></span>

8. <span data-ttu-id="796cc-165">Z listy przybornika hello w dół, kliknij pozycję **Admin** tooopen hello logowania jednokrotnego ustawienia strony.</span><span class="sxs-lookup"><span data-stu-id="796cc-165">From hello toolbox drop down, click on **Admin** tooopen hello SSO settings page.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. <span data-ttu-id="796cc-167">Wklej hello wartości w polach hello opisane poniżej-</span><span class="sxs-lookup"><span data-stu-id="796cc-167">Paste hello values in hello boxes as described below-</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    <span data-ttu-id="796cc-169">a.</span><span class="sxs-lookup"><span data-stu-id="796cc-169">a.</span></span> <span data-ttu-id="796cc-170">W hello **pojedynczy znak na adres URL wystawcy** Wklej hello identyfikator jednostki SAML skopiowanych z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="796cc-170">In hello **Single Sign On Issuer URL** box, paste hello SAML Entity ID copied from hello Azure portal.</span></span>

    <span data-ttu-id="796cc-171">b.</span><span class="sxs-lookup"><span data-stu-id="796cc-171">b.</span></span> <span data-ttu-id="796cc-172">W hello **SAML logowania na docelowy adres URL** Wklej hello SAML pojedynczy znak na adres URL usługi skopiowanych z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="796cc-172">In hello **SAML Sign On Target URL** box, paste hello SAML Single Sign-On Service URL copied from hello Azure portal.</span></span>

    <span data-ttu-id="796cc-173">c.</span><span class="sxs-lookup"><span data-stu-id="796cc-173">c.</span></span> <span data-ttu-id="796cc-174">Teraz Otwórz hello **XML metadanych** pobranego wcześniej z hello portalu Azure i certyfikat hello kopiowania w tagu hello o nazwie **X509Certificate**.</span><span class="sxs-lookup"><span data-stu-id="796cc-174">Now open hello **Metadata XML** downloaded above from hello Azure portal and copy hello certficate in hello tag named **X509Certificate**.</span></span> <span data-ttu-id="796cc-175">Witaj Wklej skopiowane wartości do hello **certyfikatu rejestracji jednokrotnej x509** pole.</span><span class="sxs-lookup"><span data-stu-id="796cc-175">Paste hello copied value into hello **Single Sign On x509 Certificate** box.</span></span>

10. <span data-ttu-id="796cc-176">Polecenie **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="796cc-176">Click on **Save Changes**.</span></span>

11. <span data-ttu-id="796cc-177">Po tych ustawień wymaga toosend hello **nazwy domeny** (np. **contoso.com**) za pomocą którego logujesz się do Procore toohello [zespołem pomocy technicznej Procore](https://support.procore.com/) i zostaną one Aktywacja z federacyjną rejestracją Jednokrotną dla tej domeny.</span><span class="sxs-lookup"><span data-stu-id="796cc-177">After these settings, you needs toosend hello **domain name** (e.g **contoso.com**) through which you are logging into Procore toohello [Procore Support team](https://support.procore.com/) and they will activate federated SSO for that domain.</span></span>

<!--### Next steps

tooensure users can sign-in tooProcore SSO after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooProcore SSO in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="796cc-178">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="796cc-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="796cc-179">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="796cc-179">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="796cc-181">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="796cc-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="796cc-182">W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="796cc-182">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="796cc-184">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="796cc-184">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="796cc-186">U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="796cc-186">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="796cc-188">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="796cc-188">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="796cc-190">a.</span><span class="sxs-lookup"><span data-stu-id="796cc-190">a.</span></span> <span data-ttu-id="796cc-191">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="796cc-191">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="796cc-192">b.</span><span class="sxs-lookup"><span data-stu-id="796cc-192">b.</span></span> <span data-ttu-id="796cc-193">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="796cc-193">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="796cc-194">c.</span><span class="sxs-lookup"><span data-stu-id="796cc-194">c.</span></span> <span data-ttu-id="796cc-195">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="796cc-195">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="796cc-196">d.</span><span class="sxs-lookup"><span data-stu-id="796cc-196">d.</span></span> <span data-ttu-id="796cc-197">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="796cc-197">Click **Create**.</span></span>
 
### <a name="creating-a-procore-sso-test-user"></a><span data-ttu-id="796cc-198">Tworzenie użytkownika testowego Procore logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="796cc-198">Creating a Procore SSO test user</span></span>

<span data-ttu-id="796cc-199">Wykonaj hello poniżej toocreate czynności użytkownika testowego Procore w bok.</span><span class="sxs-lookup"><span data-stu-id="796cc-199">Please follow hello below steps toocreate a Procore test user on their side.</span></span>

1. <span data-ttu-id="796cc-200">Logowania z witryny firmy procore tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="796cc-200">Login tooyour procore company site as an administrator.</span></span>  

2. <span data-ttu-id="796cc-201">Z listy przybornika hello w dół, kliknij pozycję **katalogu** tooopen hello firmy katalogu strony.</span><span class="sxs-lookup"><span data-stu-id="796cc-201">From hello toolbox drop down, click on **Directory** tooopen hello company directory page.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. <span data-ttu-id="796cc-203">Polecenie **dodać osobę** opcję tooopen hello formularz i wprowadzić wykonaj następujące opcje —</span><span class="sxs-lookup"><span data-stu-id="796cc-203">Click on **Add a Person** option tooopen hello form and enter perform following options -</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    <span data-ttu-id="796cc-205">a.</span><span class="sxs-lookup"><span data-stu-id="796cc-205">a.</span></span> <span data-ttu-id="796cc-206">W hello **imię** pole tekstowe, imię użytkownika typu, takich jak **Britta**.</span><span class="sxs-lookup"><span data-stu-id="796cc-206">In hello **First Name** textbox, type user's first name like **Britta**.</span></span>

    <span data-ttu-id="796cc-207">b.</span><span class="sxs-lookup"><span data-stu-id="796cc-207">b.</span></span> <span data-ttu-id="796cc-208">W hello **nazwisko** pole tekstowe, nazwisko użytkownika typu, takich jak **Simona**.</span><span class="sxs-lookup"><span data-stu-id="796cc-208">In hello **Last name** textbox, type user's last name like **Simon**.</span></span>

    <span data-ttu-id="796cc-209">c.</span><span class="sxs-lookup"><span data-stu-id="796cc-209">c.</span></span> <span data-ttu-id="796cc-210">W hello **adres E-mail** , adres e-mail użytkownika typu pole tekstowe, takich jak  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="796cc-210">In hello **Email Address** textbox, type user's email address like **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="796cc-211">d.</span><span class="sxs-lookup"><span data-stu-id="796cc-211">d.</span></span> <span data-ttu-id="796cc-212">Wybierz **szablon uprawnień** jako **później Zastosuj szablon uprawnień**.</span><span class="sxs-lookup"><span data-stu-id="796cc-212">Select **Permission Template** as **Apply Permission Template Later**.</span></span>

    <span data-ttu-id="796cc-213">e.</span><span class="sxs-lookup"><span data-stu-id="796cc-213">e.</span></span> <span data-ttu-id="796cc-214">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="796cc-214">Click **Create**.</span></span>

4. <span data-ttu-id="796cc-215">Sprawdź i zaktualizuj szczegóły hello, dla hello nowo dodany kontakt.</span><span class="sxs-lookup"><span data-stu-id="796cc-215">Check and update hello details for hello newly added contact.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. <span data-ttu-id="796cc-217">Polecenie **zapisywanie i wysyłanie Invitiation** (Jeśli wymagane jest zaproszenia pocztą) lub **zapisać** (Zapisz bezpośrednio) toocomplete hello użytkownika rejestracji.</span><span class="sxs-lookup"><span data-stu-id="796cc-217">Click on **Save and Send Invitiation** (if an invite through mail is required) or **Save** (Save directly) toocomplete hello user registration.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="796cc-219">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="796cc-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="796cc-220">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooProcore dostępu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="796cc-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooProcore SSO.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="796cc-222">**tooassign tooProcore Simona Britta logowanie Jednokrotne, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="796cc-222">**tooassign Britta Simon tooProcore SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="796cc-223">W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="796cc-223">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="796cc-225">Z listy aplikacji hello wybierz **Procore logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="796cc-225">In hello applications list, select **Procore SSO**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. <span data-ttu-id="796cc-227">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="796cc-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="796cc-229">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="796cc-229">Click **Add** button.</span></span> <span data-ttu-id="796cc-230">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="796cc-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="796cc-232">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="796cc-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="796cc-233">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="796cc-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="796cc-234">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="796cc-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="796cc-235">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="796cc-235">Testing single sign-on</span></span>

<span data-ttu-id="796cc-236">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="796cc-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="796cc-237">Jeśli chcesz przetestować jednego ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="796cc-237">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="796cc-238">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="796cc-238">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> <span data-ttu-id="796cc-239">Po kliknięciu kafelka Procore logowania jednokrotnego hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Procore logowania jednokrotnego aplikacji.</span><span class="sxs-lookup"><span data-stu-id="796cc-239">When you click hello Procore SSO tile in hello Access Panel, you should get automatically signed-on tooyour Procore SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="796cc-240">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="796cc-240">Additional resources</span></span>

* [<span data-ttu-id="796cc-241">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="796cc-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="796cc-242">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="796cc-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

