---
title: "Samouczek: Integracji Azure Active Directory z chmurą Atlassian | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i w chmurze Atlassian."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: f679e8b3306bf0efb9373d8baa0cfe095b760aaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a><span data-ttu-id="cb1a1-103">Samouczek: Integracji Azure Active Directory z chmurą Atlassian</span><span class="sxs-lookup"><span data-stu-id="cb1a1-103">Tutorial: Azure Active Directory integration with Atlassian Cloud</span></span>

<span data-ttu-id="cb1a1-104">Z tego samouczka, dowiesz się, jak toointegrate Atlassian chmury w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cb1a1-104">In this tutorial, you learn how toointegrate Atlassian Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cb1a1-105">Integracja z usługą Azure AD Atlassian chmury udostępnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="cb1a1-105">Integrating Atlassian Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cb1a1-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooAtlassian chmury</span><span class="sxs-lookup"><span data-stu-id="cb1a1-106">You can control in Azure AD who has access tooAtlassian Cloud</span></span>
- <span data-ttu-id="cb1a1-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAtlassian chmury (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb1a1-107">You can enable your users tooautomatically get signed-on tooAtlassian Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cb1a1-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="cb1a1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="cb1a1-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cb1a1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb1a1-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cb1a1-110">Prerequisites</span></span>

<span data-ttu-id="cb1a1-111">tooconfigure integracji usługi Azure AD z chmurą Atlassian należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="cb1a1-111">tooconfigure Azure AD integration with Atlassian Cloud, you need hello following items:</span></span>

- <span data-ttu-id="cb1a1-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb1a1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cb1a1-113">Chmura Atlassian logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="cb1a1-113">An Atlassian Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cb1a1-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cb1a1-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="cb1a1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cb1a1-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cb1a1-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cb1a1-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cb1a1-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="cb1a1-118">Scenario description</span></span>
<span data-ttu-id="cb1a1-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cb1a1-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="cb1a1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cb1a1-121">Dodawanie Atlassian chmury z galerii hello</span><span class="sxs-lookup"><span data-stu-id="cb1a1-121">Adding Atlassian Cloud from hello gallery</span></span>
2. <span data-ttu-id="cb1a1-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="cb1a1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atlassian-cloud-from-hello-gallery"></a><span data-ttu-id="cb1a1-123">Dodawanie Atlassian chmury z galerii hello</span><span class="sxs-lookup"><span data-stu-id="cb1a1-123">Adding Atlassian Cloud from hello gallery</span></span>
<span data-ttu-id="cb1a1-124">tooconfigure hello integracji Atlassian chmury do usługi Azure AD, należy tooadd Atlassian chmury z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-124">tooconfigure hello integration of Atlassian Cloud into Azure AD, you need tooadd Atlassian Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cb1a1-125">**tooadd Atlassian chmury z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="cb1a1-125">**tooadd Atlassian Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb1a1-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="cb1a1-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cb1a1-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="cb1a1-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="cb1a1-133">W polu wyszukiwania hello wpisz **chmury Atlassian**.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-133">In hello search box, type **Atlassian Cloud**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_search.png)

5. <span data-ttu-id="cb1a1-135">W panelu wyników hello, wybierz **chmury Atlassian**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-135">In hello results panel, select **Atlassian Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cb1a1-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="cb1a1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cb1a1-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z chmurą Atlassian oparte na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="cb1a1-138">In this section, you configure and test Azure AD single sign-on with Atlassian Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cb1a1-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w chmurze Atlassian jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Atlassian Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="cb1a1-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w chmurze Atlassian musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-140">In other words, a link relationship between an Azure AD user and hello related user in Atlassian Cloud needs toobe established.</span></span>

<span data-ttu-id="cb1a1-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w chmurze Atlassian.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Atlassian Cloud.</span></span>

<span data-ttu-id="cb1a1-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z chmurą Atlassian, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="cb1a1-142">tooconfigure and test Azure AD single sign-on with Atlassian Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cb1a1-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cb1a1-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cb1a1-145">**[Tworzenie użytkownika testowego chmury Atlassian](#creating-an-atlassian-cloud-test-user)**  -toohave odpowiednikiem Simona Britta w chmurze Atlassian, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-145">**[Creating an Atlassian Cloud test user](#creating-an-atlassian-cloud-test-user)** - toohave a counterpart of Britta Simon in Atlassian Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="cb1a1-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cb1a1-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cb1a1-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="cb1a1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cb1a1-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w chmurze Atlassian aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Atlassian Cloud application.</span></span>

<span data-ttu-id="cb1a1-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z chmurą Atlassian wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="cb1a1-150">**tooconfigure Azure AD single sign-on with Atlassian Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb1a1-151">W portalu Azure na powitania hello **chmury Atlassian** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-151">In hello Azure portal, on hello **Atlassian Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="cb1a1-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. <span data-ttu-id="cb1a1-155">Na powitania **adresy URL i domenę chmury Atlassian** sekcji, wykonaj następujące kroki, jeśli chcesz, aby aplikacja hello tooconfigure w hello **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="cb1a1-155">On hello **Atlassian Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)

    <span data-ttu-id="cb1a1-157">a.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-157">a.</span></span> <span data-ttu-id="cb1a1-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<instancename>.atlassian.net/admin/saml/edit`</span><span class="sxs-lookup"><span data-stu-id="cb1a1-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.atlassian.net/admin/saml/edit`</span></span>

    <span data-ttu-id="cb1a1-159">b.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-159">b.</span></span> <span data-ttu-id="cb1a1-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL jako:`https://id.atlassian.com/login/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="cb1a1-160">In hello **Reply URL** textbox, type a URL as: `https://id.atlassian.com/login/saml/acs`</span></span>

4. <span data-ttu-id="cb1a1-161">Sprawdź **Pokaż zaawansowane ustawienia adresu URL** i wykonywać powitania po kroku, jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="cb1a1-161">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    <span data-ttu-id="cb1a1-163">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<instancename>.atlassian.net`</span><span class="sxs-lookup"><span data-stu-id="cb1a1-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.atlassian.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cb1a1-164">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-164">These values are not real.</span></span> <span data-ttu-id="cb1a1-165">Zaktualizować te wartości z hello rzeczywisty identyfikator i adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-165">Update these values with hello actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="cb1a1-166">Możesz uzyskać dokładne wartości hello z ekranu konfiguracji SAML chmury Atlassian.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-166">You can get hello exact values from Atlassian Cloud SAML Configuration screen.</span></span>
 
5. <span data-ttu-id="cb1a1-167">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-167">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png) 

6. <span data-ttu-id="cb1a1-169">Na powitania **konfiguracji chmury Atlassian** , kliknij przycisk **Konfigurowanie chmury Atlassian** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-169">On hello **Atlassian Cloud Configuration** section, click **Configure Atlassian Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="cb1a1-170">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="cb1a1-170">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png) 

7. <span data-ttu-id="cb1a1-172">tooget logowania jednokrotnego skonfigurowane dla aplikacji, toohello logowania portalu Atlassian za pomocą hello uprawnienia administratora.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-172">tooget SSO configured for your application, login toohello Atlassian Portal using hello administrator rights.</span></span>

8. <span data-ttu-id="cb1a1-173">W sekcji uwierzytelnianie hello hello lewy pasek nawigacyjny kliknij **domen**.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-173">In hello Authentication section of hello left navigation click **Domains**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)

    <span data-ttu-id="cb1a1-175">a.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-175">a.</span></span> <span data-ttu-id="cb1a1-176">W polu tekstowym hello, wpisz nazwę domeny, a następnie kliknij przycisk **Dodaj domenę**.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-176">In hello textbox, type your domain name, and then click **Add domain**.</span></span>
        
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_07.png)

    <span data-ttu-id="cb1a1-178">b.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-178">b.</span></span> <span data-ttu-id="cb1a1-179">tooverify hello domeny, kliknij przycisk **Sprawdź**.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-179">tooverify hello domain, click **Verify**.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_08.png)

    <span data-ttu-id="cb1a1-181">c.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-181">c.</span></span> <span data-ttu-id="cb1a1-182">Pobierz plik html weryfikacji domeny hello, Prześlij go toohello folder główny witryny sieci Web w danej domenie, a następnie kliknij **weryfikowanie domeny**.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-182">Download hello domain verification html file, upload it toohello root folder of your domain's website, and then click **Verify domain**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_09.png)

    <span data-ttu-id="cb1a1-184">d.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-184">d.</span></span> <span data-ttu-id="cb1a1-185">Po zweryfikowaniu domeny hello hello wartość hello **stan** pole jest **zweryfikowano**.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-185">Once hello domain is verified, hello value of hello **Status** field is **Verified**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_10.png)

9. <span data-ttu-id="cb1a1-187">Na pasku nawigacyjnym po lewej stronie powitania kliknij **SAML**.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-187">In hello left navigation bar, click **SAML**.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

10. <span data-ttu-id="cb1a1-189">Utwórz Konfiguracja SAML i Dodaj hello tożsamości dostawcy konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-189">Create a SAML Configuration and add hello Identity provider configuration.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    <span data-ttu-id="cb1a1-191">a.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-191">a.</span></span> <span data-ttu-id="cb1a1-192">W hello **dostawcy tożsamości identyfikator jednostki** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-192">In hello **Identity provider Entity ID** text box, paste hello value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cb1a1-193">b.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-193">b.</span></span> <span data-ttu-id="cb1a1-194">W hello **dostawcy tożsamości adresu URL logowania jednokrotnego** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-194">In hello **Identity provider SSO URL** text box, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="cb1a1-195">c.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-195">c.</span></span> <span data-ttu-id="cb1a1-196">Otwórz certyfikat hello pobrane z Azure portal i skopiuj wartości hello bez hello Begin i na końcu wiersza i wklej go w hello **X509 publicznego certyfikatu** pole.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-196">Open hello downloaded certificate from Azure portal and copy hello values without hello Begin and End lines and paste it in hello **Public X509 certificate** box.</span></span>
    
    <span data-ttu-id="cb1a1-197">d.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-197">d.</span></span> <span data-ttu-id="cb1a1-198">Kliknij przycisk **Zapisz konfigurację** tooSave hello ustawienia.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-198">Click **Save Configuration**  tooSave hello settings.</span></span>
     
11. <span data-ttu-id="cb1a1-199">Zaktualizuj toomake ustawienia usługi Azure AD hello upewnić się, że Instalator hello, popraw adres URL identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-199">Update hello Azure AD settings toomake sure that you have setup hello correct Identifier URL.</span></span>
  
    <span data-ttu-id="cb1a1-200">a.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-200">a.</span></span> <span data-ttu-id="cb1a1-201">Kopiuj hello **Identyfikatora tożsamości SP** z hello SAML ekranu i wklej go w usłudze Azure AD jako hello **identyfikator** wartość.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-201">Copy hello **SP Identity ID** from hello SAML screen and paste it in Azure AD as hello **Identifier** value.</span></span>

    <span data-ttu-id="cb1a1-202">b.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-202">b.</span></span> <span data-ttu-id="cb1a1-203">Zaloguj się na adres URL jest adres URL dzierżawy hello Atlassian chmury.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-203">Sign On URL is hello tenant URL of your Atlassian Cloud.</span></span>     

     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)
    
12. <span data-ttu-id="cb1a1-205">W portalu Azure hello, kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-205">In hello Azure portal, Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="cb1a1-207">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="cb1a1-207">You can now read a concise version of these instructions inside hello [Azure  portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="cb1a1-208">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-208">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="cb1a1-209">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cb1a1-209">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cb1a1-210">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb1a1-210">Creating an Azure AD test user</span></span>
<span data-ttu-id="cb1a1-211">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-211">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="cb1a1-213">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="cb1a1-213">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb1a1-214">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-214">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cb1a1-216">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-216">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cb1a1-218">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-218">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cb1a1-220">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="cb1a1-220">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cb1a1-222">a.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-222">a.</span></span> <span data-ttu-id="cb1a1-223">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-223">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cb1a1-224">b.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-224">b.</span></span> <span data-ttu-id="cb1a1-225">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-225">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cb1a1-226">c.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-226">c.</span></span> <span data-ttu-id="cb1a1-227">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-227">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cb1a1-228">d.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-228">d.</span></span> <span data-ttu-id="cb1a1-229">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-229">Click **Create**.</span></span>
 
### <a name="creating-an-atlassian-cloud-test-user"></a><span data-ttu-id="cb1a1-230">Tworzenie użytkownika testowego Atlassian chmury</span><span class="sxs-lookup"><span data-stu-id="cb1a1-230">Creating an Atlassian Cloud test user</span></span>

<span data-ttu-id="cb1a1-231">toolog użytkowników tooenable usługi Azure AD w tooAtlassian chmurze muszą mieć przydzielone do Atlassian chmury.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-231">tooenable Azure AD users toolog in tooAtlassian Cloud, they must be provisioned into Atlassian Cloud.</span></span>  
<span data-ttu-id="cb1a1-232">W przypadku Atlassian chmury Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-232">In case of Atlassian Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="cb1a1-233">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="cb1a1-233">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb1a1-234">W sekcji Administracja witryny hello, kliknij przycisk hello **użytkowników** przycisku</span><span class="sxs-lookup"><span data-stu-id="cb1a1-234">In hello Site administration section, click hello **Users** button</span></span>

    ![Utwórz użytkownika Atlassian chmury](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. <span data-ttu-id="cb1a1-236">Kliknij przycisk hello **Tworzenie użytkownika** toocreate przycisk użytkownika w chmurze Atlassian hello</span><span class="sxs-lookup"><span data-stu-id="cb1a1-236">Click hello **Create User** button toocreate a user in hello Atlassian Cloud</span></span>

    ![Utwórz użytkownika Atlassian chmury](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. <span data-ttu-id="cb1a1-238">Wprowadź nazwę użytkownika hello **adres E-mail**, **Username**, i **Pełna nazwa** i przypisz hello dostęp do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-238">Enter hello user's **Email address**, **Username**, and **Full Name** and assign hello application access.</span></span> 

    ![Utwórz użytkownika Atlassian chmury](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. <span data-ttu-id="cb1a1-240">Kliknij przycisk **tworzenia użytkownika** przycisku, wysyła hello e-mail zaproszenia toohello użytkownika i po zaakceptowaniu hello zaproszenia hello użytkownika będzie aktywny w systemie hello.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-240">Click **Create user** button, it will send hello email invitation toohello user and after accepting hello invitation hello user will be active in hello system.</span></span> 

>[!NOTE] 
><span data-ttu-id="cb1a1-241">Można również utworzyć hello zbiorczego użytkowników, klikając hello **Tworzenie zbiorczego** przycisk w sekcji użytkownicy hello.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-241">You can also create hello bulk users by clicking hello **Bulk Create** button in hello Users section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cb1a1-242">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb1a1-242">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cb1a1-243">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooAtlassian chmury.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-243">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAtlassian Cloud.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="cb1a1-245">**tooassign tooAtlassian Simona Britta chmury, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="cb1a1-245">**tooassign Britta Simon tooAtlassian Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="cb1a1-246">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-246">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="cb1a1-248">Z listy aplikacji hello wybierz **chmury Atlassian**.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-248">In hello applications list, select **Atlassian Cloud**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png) 

3. <span data-ttu-id="cb1a1-250">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-250">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="cb1a1-252">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-252">Click **Add** button.</span></span> <span data-ttu-id="cb1a1-253">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-253">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="cb1a1-255">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-255">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cb1a1-256">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-256">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cb1a1-257">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-257">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cb1a1-258">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="cb1a1-258">Testing single sign-on</span></span>

<span data-ttu-id="cb1a1-259">W tej sekcji można przetestować konfigurację usługi Azure AD z logowania jednokrotnego za pomocą hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-259">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="cb1a1-260">Po kliknięciu hello chmury Atlassian kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour aplikacji w chmurze Atlassian.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-260">When you click hello Atlassian Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Atlassian Cloud application.</span></span> <span data-ttu-id="cb1a1-261">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cb1a1-261">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cb1a1-262">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="cb1a1-262">Additional resources</span></span>

* [<span data-ttu-id="cb1a1-263">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb1a1-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cb1a1-264">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cb1a1-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png

