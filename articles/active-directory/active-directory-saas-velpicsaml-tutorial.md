---
title: 'Samouczek: Integracji Azure Active Directory z Velpic SAML | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Velpic SAML."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 613947d8fe95113382a2cdc0f79ce9eda85a0127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a><span data-ttu-id="0f8f9-103">Samouczek: Integracji Azure Active Directory z Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="0f8f9-103">Tutorial: Azure Active Directory integration with Velpic SAML</span></span>

<span data-ttu-id="0f8f9-104">Z tego samouczka, dowiesz się, jak toointegrate SAML Velpic w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0f8f9-104">In this tutorial, you learn how toointegrate Velpic SAML with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0f8f9-105">Integrację Velpic SAML z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="0f8f9-105">Integrating Velpic SAML with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0f8f9-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooVelpic SAML</span><span class="sxs-lookup"><span data-stu-id="0f8f9-106">You can control in Azure AD who has access tooVelpic SAML</span></span>
- <span data-ttu-id="0f8f9-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooVelpic SAML (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f8f9-107">You can enable your users tooautomatically get signed-on tooVelpic SAML (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0f8f9-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="0f8f9-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="0f8f9-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0f8f9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f8f9-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0f8f9-110">Prerequisites</span></span>

<span data-ttu-id="0f8f9-111">tooconfigure integracji usługi Azure AD z Velpic SAML należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="0f8f9-111">tooconfigure Azure AD integration with Velpic SAML, you need hello following items:</span></span>

- <span data-ttu-id="0f8f9-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f8f9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0f8f9-113">Velpic SAML jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="0f8f9-113">A Velpic SAML single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0f8f9-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0f8f9-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="0f8f9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0f8f9-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="0f8f9-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0f8f9-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0f8f9-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="0f8f9-118">Scenario description</span></span>
<span data-ttu-id="0f8f9-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0f8f9-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="0f8f9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0f8f9-121">Dodawanie Velpic SAML z galerii hello</span><span class="sxs-lookup"><span data-stu-id="0f8f9-121">Adding Velpic SAML from hello gallery</span></span>
2. <span data-ttu-id="0f8f9-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="0f8f9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-velpic-saml-from-hello-gallery"></a><span data-ttu-id="0f8f9-123">Dodawanie Velpic SAML z galerii hello</span><span class="sxs-lookup"><span data-stu-id="0f8f9-123">Adding Velpic SAML from hello gallery</span></span>
<span data-ttu-id="0f8f9-124">tooconfigure hello integrację Velpic SAML usługi Azure AD, należy tooadd Velpic SAML z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-124">tooconfigure hello integration of Velpic SAML into Azure AD, you need tooadd Velpic SAML from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0f8f9-125">**tooadd SAML Velpic z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="0f8f9-125">**tooadd Velpic SAML from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0f8f9-126">W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="0f8f9-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0f8f9-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="0f8f9-131">Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="0f8f9-133">W polu wyszukiwania hello wpisz **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-133">In hello search box, type **Velpic SAML**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. <span data-ttu-id="0f8f9-135">W panelu wyników hello, wybierz **Velpic SAML**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-135">In hello results panel, select **Velpic SAML**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0f8f9-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="0f8f9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0f8f9-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z Velpic SAML w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-138">In this section, you configure and test Azure AD single sign-on with Velpic SAML based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0f8f9-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Velpic SAML jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Velpic SAML is tooa user in Azure AD.</span></span> <span data-ttu-id="0f8f9-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Velpic SAML musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-140">In other words, a link relationship between an Azure AD user and hello related user in Velpic SAML needs toobe established.</span></span>

<span data-ttu-id="0f8f9-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Velpic SAML.</span></span>

<span data-ttu-id="0f8f9-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Velpic SAML, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="0f8f9-142">tooconfigure and test Azure AD single sign-on with Velpic SAML, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0f8f9-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0f8f9-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0f8f9-145">**[Tworzenie użytkownika testowego Velpic SAML](#creating-a-velpic-saml-test-user)**  -toohave odpowiednikiem Simona Britta w SAML Velpic, że jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-145">**[Creating a Velpic SAML test user](#creating-a-velpic-saml-test-user)** - toohave a counterpart of Britta Simon in Velpic SAML that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="0f8f9-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0f8f9-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0f8f9-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0f8f9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0f8f9-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w aplikacji Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Velpic SAML application.</span></span>

<span data-ttu-id="0f8f9-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Velpic SAML wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="0f8f9-150">**tooconfigure Azure AD single sign-on with Velpic SAML, perform hello following steps:**</span></span>

1. <span data-ttu-id="0f8f9-151">W portalu zarządzania Azure hello na powitania **Velpic SAML** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-151">In hello Azure Management portal, on hello **Velpic SAML** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="0f8f9-153">Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. <span data-ttu-id="0f8f9-155">Wprowadź szczegóły hello w hello **Velpic SAML domeny i adres URL** sekcji -</span><span class="sxs-lookup"><span data-stu-id="0f8f9-155">Enter hello details in hello **Velpic SAML Domain and URLs** section-</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    <span data-ttu-id="0f8f9-157">a.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-157">a.</span></span> <span data-ttu-id="0f8f9-158">W hello **adres URL logowania** pole tekstowe, wartość hello typu jako:`https://<sub-domain>.velpicsaml.net`</span><span class="sxs-lookup"><span data-stu-id="0f8f9-158">In hello **Sign-on URL** textbox, type hello value as: `https://<sub-domain>.velpicsaml.net`</span></span>

    <span data-ttu-id="0f8f9-159">b.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-159">b.</span></span> <span data-ttu-id="0f8f9-160">W hello **identyfikator** pole tekstowe, Wklej hello **"Rejestracja jednokrotna w adresie URL"** wartość`https://auth.velpic.com/saml/v2/<entity-id>/login`</span><span class="sxs-lookup"><span data-stu-id="0f8f9-160">In hello **Identifier** textbox, paste hello **‘Single sign on URL’** value `https://auth.velpic.com/saml/v2/<entity-id>/login`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="0f8f9-161">Należy pamiętać, że hello znaku w adresie URL, które będą udostępniane przez hello Velpic SAML zespołu i wartość identyfikatora będzie dostępna po skonfigurowaniu hello wtyczki logowania jednokrotnego Velpic SAML strony.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-161">Please note that hello Sign on URL will be provided by hello Velpic SAML team and Identifier value will be available when you configure hello SSO Plugin on Velpic SAML side.</span></span> <span data-ttu-id="0f8f9-162">Należy toocopy, który ze strony aplikacji Velpic SAML i wklej ją tutaj.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-162">You need toocopy that value from Velpic SAML application  page and paste it here.</span></span>

4. <span data-ttu-id="0f8f9-163">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. <span data-ttu-id="0f8f9-165">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-165">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0f8f9-167">W sekcji konfiguracji SAML Velpic hello kliknij polecenie skonfigurować SAML Velpic tooopen Konfigurowanie logowania jednokrotnego okna.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-167">On hello Velpic SAML Configuration section, click Configure Velpic SAML tooopen Configure sign-on window.</span></span> <span data-ttu-id="0f8f9-168">Skopiuj hello identyfikator jednostki SAML z hello sekcji krótkimi opisami.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-168">Copy hello SAML Entity ID from hello Quick Reference section.</span></span>

7. <span data-ttu-id="0f8f9-169">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Velpic SAML jako administrator.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-169">In a different web browser window, log into your Velpic SAML company site as an administrator.</span></span>

8. <span data-ttu-id="0f8f9-170">Polecenie **Zarządzaj** karcie i przejść za**integracji** sekcji, w którym należy tooclick na **wtyczek** przycisk toocreate nowej wtyczki dla logowania.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-170">Click on **Manage** tab and go too**Integration** section where you need tooclick on **Plugins** button toocreate new plugin for Sign-In.</span></span>

    ![Wtyczki](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. <span data-ttu-id="0f8f9-172">Polecenie hello **"Dodawanie wtyczki"** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-172">Click on hello **‘Add plugin’** button.</span></span>
    
    ![Wtyczki](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. <span data-ttu-id="0f8f9-174">Polecenie hello **SAML** kafelka w hello strona Dodawanie wtyczek.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-174">Click on hello **SAML** tile in hello Add Plugin page.</span></span>
    
    ![Wtyczki](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. <span data-ttu-id="0f8f9-176">Wprowadź nazwę nowej wtyczki SAML hello hello, a następnie kliknij przycisk hello **"Dodaj"** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-176">Enter hello name of hello new SAML plugin and click hello **‘Add’** button.</span></span>

    ![Wtyczki](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. <span data-ttu-id="0f8f9-178">Wprowadź szczegóły hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="0f8f9-178">Enter hello details as follows:</span></span>

    ![Wtyczki](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    <span data-ttu-id="0f8f9-180">a.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-180">a.</span></span> <span data-ttu-id="0f8f9-181">W hello **nazwa** pole tekstowe, nazwa typu hello wtyczki SAML.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-181">In hello **Name** textbox, type hello name of SAML plugin.</span></span>

    <span data-ttu-id="0f8f9-182">b.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-182">b.</span></span> <span data-ttu-id="0f8f9-183">W hello **adres URL wystawcy** pole tekstowe, Wklej hello **identyfikator jednostki SAML** skopiowany z hello **Konfigurowanie logowania jednokrotnego** okna hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-183">In hello **Issuer URL** textbox, paste hello **SAML Entity ID** you copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

    <span data-ttu-id="0f8f9-184">c.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-184">c.</span></span> <span data-ttu-id="0f8f9-185">W hello **dostawcy metadanych konfiguracji** przekazać hello pliku XML metadanych, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-185">In hello **Provider Metadata Config** upload hello Metadata XML file which you downloaded from Azure portal.</span></span>

    <span data-ttu-id="0f8f9-186">d.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-186">d.</span></span> <span data-ttu-id="0f8f9-187">Możesz również tooenable SAML tylko w czasie inicjowania obsługi administracyjnej, należy włączyć hello **"Automatyczne tworzenie nowych użytkowników"** pola wyboru.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-187">You can also choose tooenable SAML just in time provisioning by enabling hello **‘Auto create new users’** checkbox.</span></span> <span data-ttu-id="0f8f9-188">Jeśli użytkownik nie istnieje w Velpic i ta flaga nie jest włączona, hello logowania z platformy Azure nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-188">If a user doesn’t exist in Velpic and this flag is not enabled, hello login from Azure will fail.</span></span> <span data-ttu-id="0f8f9-189">Jeśli flaga hello jest automatycznie włączone hello użytkownika zostanie zainicjowana w Velpic w czasie hello nazwy logowania.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-189">If hello flag is enabled hello user will automatically be provisioned into Velpic at hello time of login.</span></span> 

    <span data-ttu-id="0f8f9-190">e.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-190">e.</span></span> <span data-ttu-id="0f8f9-191">Kopiuj hello **Rejestracja jednokrotna w adresie URL** z pola tekstowego hello i wklej go w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-191">Copy hello **Single sign on URL** from hello text box and paste it in hello Azure portal.</span></span>
    
    <span data-ttu-id="0f8f9-192">f.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-192">f.</span></span> <span data-ttu-id="0f8f9-193">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-193">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0f8f9-194">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f8f9-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="0f8f9-195">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-195">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="0f8f9-197">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0f8f9-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0f8f9-198">W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-198">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0f8f9-200">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-200">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0f8f9-202">U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-202">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0f8f9-204">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0f8f9-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0f8f9-206">a.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-206">a.</span></span> <span data-ttu-id="0f8f9-207">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0f8f9-208">b.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-208">b.</span></span> <span data-ttu-id="0f8f9-209">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0f8f9-210">c.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-210">c.</span></span> <span data-ttu-id="0f8f9-211">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0f8f9-212">d.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-212">d.</span></span> <span data-ttu-id="0f8f9-213">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-213">Click **Create**.</span></span>
 
### <a name="creating-a-velpic-saml-test-user"></a><span data-ttu-id="0f8f9-214">Tworzenie użytkownika testowego Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="0f8f9-214">Creating a Velpic SAML test user</span></span>

<span data-ttu-id="0f8f9-215">Ten krok zazwyczaj nie jest wymagane jako aplikacji hello obsługuje tylko w czasie Inicjowanie obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-215">This step is usually not required as hello application supports just in time user provisioning.</span></span> <span data-ttu-id="0f8f9-216">Jeśli nie włączono hello użytkownika automatycznego inicjowania obsługi administracyjnej tworzenie ręczne użytkownika można wykonać zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-216">If hello automatic user provisioning is not enabled then manual user creation can be done as described below.</span></span>

<span data-ttu-id="0f8f9-217">Zaloguj się do witryny firmy Velpic SAML jako administrator i wykonać następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0f8f9-217">Log into your Velpic SAML company site as an administrator and perform following steps:</span></span>
    
1. <span data-ttu-id="0f8f9-218">Kliknij na karcie Zarządzanie przejdź do sekcji tooUsers, a następnie kliknij nowy przycisk tooadd użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-218">Click on Manage tab and go tooUsers section, then click on New button tooadd users.</span></span>

    ![Dodaj użytkownika](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. <span data-ttu-id="0f8f9-220">Na powitania **"Tworzenie nowego użytkownika"** okna dialogowego wykonaj następujące kroki hello.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-220">On hello **“Create New User”** dialog page, perform hello following steps.</span></span>

    ![Użytkownika](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    <span data-ttu-id="0f8f9-222">a.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-222">a.</span></span> <span data-ttu-id="0f8f9-223">W hello **imię** pole tekstowe, typ hello imię Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-223">In hello **First Name** textbox, type hello first name of Britta Simon.</span></span>

    <span data-ttu-id="0f8f9-224">b.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-224">b.</span></span> <span data-ttu-id="0f8f9-225">W hello **nazwisko** pole tekstowe, typ hello nazwisko Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-225">In hello **Last Name** textbox, type hello last name of Britta Simon.</span></span>

    <span data-ttu-id="0f8f9-226">c.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-226">c.</span></span> <span data-ttu-id="0f8f9-227">W hello **nazwy użytkownika** pole tekstowe, nazwę użytkownika hello typu Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-227">In hello **User Name** textbox, type hello user name of Britta Simon.</span></span>

    <span data-ttu-id="0f8f9-228">d.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-228">d.</span></span> <span data-ttu-id="0f8f9-229">W hello **E-mail** pole tekstowe, adres e-mail hello typu Simona Britta konta.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-229">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="0f8f9-230">e.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-230">e.</span></span> <span data-ttu-id="0f8f9-231">Pozostałe informacje hello jest opcjonalny, możesz wpisać ją w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-231">Rest of hello information is optional, you can fill it if needed.</span></span>
    
    <span data-ttu-id="0f8f9-232">f.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-232">f.</span></span> <span data-ttu-id="0f8f9-233">Kliknij przycisk **SAVE** (Zapisz).</span><span class="sxs-lookup"><span data-stu-id="0f8f9-233">Click **SAVE**.</span></span>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0f8f9-234">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0f8f9-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0f8f9-235">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooVelpic dostępu SAML.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooVelpic SAML.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="0f8f9-237">**tooassign tooVelpic Simona Britta SAML, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0f8f9-237">**tooassign Britta Simon tooVelpic SAML, perform hello following steps:**</span></span>

1. <span data-ttu-id="0f8f9-238">W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-238">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="0f8f9-240">Z listy aplikacji hello wybierz **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-240">In hello applications list, select **Velpic SAML**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. <span data-ttu-id="0f8f9-242">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="0f8f9-244">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-244">Click **Add** button.</span></span> <span data-ttu-id="0f8f9-245">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="0f8f9-247">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0f8f9-248">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0f8f9-249">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0f8f9-250">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0f8f9-250">Testing single sign-on</span></span>

<span data-ttu-id="0f8f9-251">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-251">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="0f8f9-252">Po kliknięciu hello Velpic SAML kafelka w hello Panel dostępu, należy pobrać strony logowania Velpic SAML aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-252">When you click hello Velpic SAML tile in hello Access Panel, you should get login page of Velpic SAML application.</span></span> <span data-ttu-id="0f8f9-253">Powinny pojawić się hello **"Zaloguj się za pomocą usługi Azure AD"** przycisk na powitania stronę logowania.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-253">You should see hello **‘Log In With Azure AD’** button on hello sign in page.</span></span>

    ![Wtyczki](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. <span data-ttu-id="0f8f9-255">Polecenie hello **"Zaloguj się za pomocą usługi Azure AD"** toolog przycisk w tooVelpic przy użyciu konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f8f9-255">Click on hello **‘Log In With Azure AD’** button toolog in tooVelpic using your Azure AD account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0f8f9-256">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="0f8f9-256">Additional resources</span></span>

* [<span data-ttu-id="0f8f9-257">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f8f9-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0f8f9-258">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0f8f9-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

