---
title: 'Samouczek: Integracji Azure Active Directory z SkyDesk poczty E-mail | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i SkyDesk wiadomości E-mail."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9d0bbcb-ddb5-473f-a4aa-028ae88ced1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 19c670a60f581a2be55b74eacdb5393a36e38be3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skydesk-email"></a><span data-ttu-id="571db-103">Samouczek: Integracji Azure Active Directory z SkyDesk poczty E-mail</span><span class="sxs-lookup"><span data-stu-id="571db-103">Tutorial: Azure Active Directory integration with SkyDesk Email</span></span>

<span data-ttu-id="571db-104">Z tego samouczka, dowiesz się, jak toointegrate SkyDesk poczty E-mail w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="571db-104">In this tutorial, you learn how toointegrate SkyDesk Email with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="571db-105">Integrowanie SkyDesk wiadomości E-mail z usługi Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="571db-105">Integrating SkyDesk Email with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="571db-106">Można kontrolować w usłudze Azure AD mającego tooSkyDesk dostępu do poczty E-mail</span><span class="sxs-lookup"><span data-stu-id="571db-106">You can control in Azure AD who has access tooSkyDesk Email</span></span>
- <span data-ttu-id="571db-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSkyDesk poczty E-mail (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="571db-107">You can enable your users tooautomatically get signed-on tooSkyDesk Email (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="571db-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="571db-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="571db-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="571db-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="571db-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="571db-110">Prerequisites</span></span>

<span data-ttu-id="571db-111">tooconfigure integracji usługi Azure AD z SkyDesk poczty E-mail, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="571db-111">tooconfigure Azure AD integration with SkyDesk Email, you need hello following items:</span></span>

- <span data-ttu-id="571db-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="571db-112">An Azure AD subscription</span></span>
- <span data-ttu-id="571db-113">E-mail SkyDesk logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="571db-113">A SkyDesk Email single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="571db-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="571db-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="571db-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="571db-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="571db-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="571db-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="571db-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="571db-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="571db-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="571db-118">Scenario description</span></span>
<span data-ttu-id="571db-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="571db-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="571db-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="571db-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="571db-121">Dodawanie SkyDesk wiadomości E-mail z galerii hello</span><span class="sxs-lookup"><span data-stu-id="571db-121">Adding SkyDesk Email from hello gallery</span></span>
2. <span data-ttu-id="571db-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="571db-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skydesk-email-from-hello-gallery"></a><span data-ttu-id="571db-123">Dodawanie SkyDesk wiadomości E-mail z galerii hello</span><span class="sxs-lookup"><span data-stu-id="571db-123">Adding SkyDesk Email from hello gallery</span></span>
<span data-ttu-id="571db-124">tooconfigure hello integracji SkyDesk poczty E-mail w usłudze Azure Active Directory, należy tooadd SkyDesk wiadomości E-mail z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="571db-124">tooconfigure hello integration of SkyDesk Email into Azure AD, you need tooadd SkyDesk Email from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="571db-125">**tooadd E-mail SkyDesk z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="571db-125">**tooadd SkyDesk Email from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="571db-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="571db-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="571db-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="571db-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="571db-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="571db-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="571db-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="571db-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="571db-133">W polu wyszukiwania hello wpisz **E-mail SkyDesk**.</span><span class="sxs-lookup"><span data-stu-id="571db-133">In hello search box, type **SkyDesk Email**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_search.png)

5. <span data-ttu-id="571db-135">W panelu wyników hello, wybierz **E-mail SkyDesk**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="571db-135">In hello results panel, select **SkyDesk Email**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="571db-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="571db-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="571db-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z SkyDesk poczty E-mail w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="571db-138">In this section, you configure and test Azure AD single sign-on with SkyDesk Email based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="571db-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow hello odpowiednikiem użytkownika w wiadomości E-mail SkyDesk jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="571db-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SkyDesk Email is tooa user in Azure AD.</span></span> <span data-ttu-id="571db-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w wiadomości E-mail SkyDesk musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="571db-140">In other words, a link relationship between an Azure AD user and hello related user in SkyDesk Email needs toobe established.</span></span>

<span data-ttu-id="571db-141">W wiadomości E-mail SkyDesk, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="571db-141">In SkyDesk Email, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="571db-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z SkyDesk poczty E-mail, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="571db-142">tooconfigure and test Azure AD single sign-on with SkyDesk Email, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="571db-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="571db-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="571db-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="571db-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="571db-145">**[Tworzenie użytkownika testowego E-mail SkyDesk](#creating-a-skydesk-email-test-user)**  -toohave odpowiednikiem Simona Britta w SkyDesk wiadomości E-mail, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="571db-145">**[Creating a SkyDesk Email test user](#creating-a-skydesk-email-test-user)** - toohave a counterpart of Britta Simon in SkyDesk Email that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="571db-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="571db-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="571db-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="571db-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="571db-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="571db-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="571db-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji poczty E-mail SkyDesk.</span><span class="sxs-lookup"><span data-stu-id="571db-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SkyDesk Email application.</span></span>

<span data-ttu-id="571db-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z SkyDesk poczty E-mail, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="571db-150">**tooconfigure Azure AD single sign-on with SkyDesk Email, perform hello following steps:**</span></span>

1. <span data-ttu-id="571db-151">W portalu Azure na powitania hello **E-mail SkyDesk** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="571db-151">In hello Azure portal, on hello **SkyDesk Email** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="571db-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="571db-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_samlbase.png)

3. <span data-ttu-id="571db-155">Na powitania **SkyDesk domenę poczty E-mail i adresów URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="571db-155">On hello **SkyDesk Email Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_url.png)

    <span data-ttu-id="571db-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://mail.skydesk.jp/portal/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="571db-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://mail.skydesk.jp/portal/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="571db-158">wartość Hello nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="571db-158">hello value is not real.</span></span> <span data-ttu-id="571db-159">Wartość hello aktualizacji z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="571db-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="571db-160">Skontaktuj się z [zespołem pomocy technicznej klienta poczty E-mail SkyDesk](https://www.skydesk.sg/support/) tooget hello wartość.</span><span class="sxs-lookup"><span data-stu-id="571db-160">Contact [SkyDesk Email Client support team](https://www.skydesk.sg/support/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="571db-161">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="571db-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_certificate.png) 

5. <span data-ttu-id="571db-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="571db-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="571db-165">Na powitania **konfiguracji poczty E-mail SkyDesk** , kliknij przycisk **konfigurowanie poczty E-mail SkyDesk** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="571db-165">On hello **SkyDesk Email Configuration** section, click **Configure SkyDesk Email** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="571db-166">Witaj kopii **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="571db-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_configure.png) 

7. <span data-ttu-id="571db-168">tooenable logowania jednokrotnego w **E-mail SkyDesk**, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="571db-168">tooenable SSO in **SkyDesk Email**, perform hello following steps:</span></span>

    <span data-ttu-id="571db-169">a.</span><span class="sxs-lookup"><span data-stu-id="571db-169">a.</span></span> <span data-ttu-id="571db-170">Zaloguj się na tooyour konta E-mail SkyDesk jako administrator.</span><span class="sxs-lookup"><span data-stu-id="571db-170">Sign-on tooyour SkyDesk Email account as administrator.</span></span>

    <span data-ttu-id="571db-171">b.</span><span class="sxs-lookup"><span data-stu-id="571db-171">b.</span></span> <span data-ttu-id="571db-172">W menu hello na górze hello, kliknij przycisk **Instalator**i wybierz **organizacji**.</span><span class="sxs-lookup"><span data-stu-id="571db-172">In hello menu on hello top, click **Setup**, and select **Org**.</span></span> 
    
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_51.png)
  
    <span data-ttu-id="571db-174">c.</span><span class="sxs-lookup"><span data-stu-id="571db-174">c.</span></span> <span data-ttu-id="571db-175">Polecenie **domen** z hello lewego panelu.</span><span class="sxs-lookup"><span data-stu-id="571db-175">Click on **Domains** from hello left panel.</span></span>
    
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_53.png)

    <span data-ttu-id="571db-177">d.</span><span class="sxs-lookup"><span data-stu-id="571db-177">d.</span></span> <span data-ttu-id="571db-178">Polecenie **Dodawanie domeny**.</span><span class="sxs-lookup"><span data-stu-id="571db-178">Click on **Add Domain**.</span></span>
    
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_54.png)

    <span data-ttu-id="571db-180">e.</span><span class="sxs-lookup"><span data-stu-id="571db-180">e.</span></span> <span data-ttu-id="571db-181">Wpisz nazwę domeny, a następnie sprawdź hello domeny.</span><span class="sxs-lookup"><span data-stu-id="571db-181">Enter your Domain name, and then verify hello Domain.</span></span>
    
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_55.png)

    <span data-ttu-id="571db-183">f.</span><span class="sxs-lookup"><span data-stu-id="571db-183">f.</span></span> <span data-ttu-id="571db-184">Polecenie **uwierzytelnianie SAML** z hello lewego panelu.</span><span class="sxs-lookup"><span data-stu-id="571db-184">Click on **SAML Authentication** from hello left panel.</span></span>
    
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_52.png)

8. <span data-ttu-id="571db-186">Na powitania **uwierzytelnianie SAML** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="571db-186">On hello **SAML Authentication** dialog page, perform hello following steps:</span></span>
   
      ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_56.png)
   
    >[!NOTE]
    ><span data-ttu-id="571db-188">Uwierzytelnianie na podstawie toouse SAML, użytkownik powinien mieć **zweryfikowaną domeną** lub **portal adresu URL** Instalatora.</span><span class="sxs-lookup"><span data-stu-id="571db-188">toouse SAML based authentication, you should either have **verified domain** or **portal URL** setup.</span></span> <span data-ttu-id="571db-189">Hello portal można ustawić adres URL z hello unikatową nazwę.</span><span class="sxs-lookup"><span data-stu-id="571db-189">You can set hello portal URL with hello unique name.</span></span>
    > 
    > 
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_57.png)

    <span data-ttu-id="571db-191">a.</span><span class="sxs-lookup"><span data-stu-id="571db-191">a.</span></span> <span data-ttu-id="571db-192">W hello **adres URL logowania** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="571db-192">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="571db-193">b.</span><span class="sxs-lookup"><span data-stu-id="571db-193">b.</span></span> <span data-ttu-id="571db-194">W hello **wylogowania** pole tekstowe adresu URL, wartości hello Wklej **Sign-Out URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="571db-194">In hello **Logout** URL textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="571db-195">c.</span><span class="sxs-lookup"><span data-stu-id="571db-195">c.</span></span> <span data-ttu-id="571db-196">**Zmień adres URL hasła** jest opcjonalny, dlatego pozostaw to pole puste.</span><span class="sxs-lookup"><span data-stu-id="571db-196">**Change Password URL** is optional so leave it blank.</span></span>

    <span data-ttu-id="571db-197">d.</span><span class="sxs-lookup"><span data-stu-id="571db-197">d.</span></span> <span data-ttu-id="571db-198">Polecenie **uzyskać klucz z pliku** tooselect certyfikat pobrany z portalu Azure, a następnie kliknij przycisk **Otwórz** tooupload hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="571db-198">Click on **Get Key From File** tooselect your downloaded certificate from Azure portal, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="571db-199">e.</span><span class="sxs-lookup"><span data-stu-id="571db-199">e.</span></span> <span data-ttu-id="571db-200">Jako **algorytm**, wybierz pozycję **RSA**.</span><span class="sxs-lookup"><span data-stu-id="571db-200">As **Algorithm**, select **RSA**.</span></span>

    <span data-ttu-id="571db-201">f.</span><span class="sxs-lookup"><span data-stu-id="571db-201">f.</span></span> <span data-ttu-id="571db-202">Kliknij przycisk **Ok** toosave hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="571db-202">Click **Ok** toosave hello changes.</span></span>

> [!TIP]
> <span data-ttu-id="571db-203">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="571db-203">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="571db-204">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="571db-204">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="571db-205">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="571db-205">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="571db-206">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="571db-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="571db-207">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="571db-207">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="571db-209">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="571db-209">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="571db-210">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="571db-210">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="571db-212">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="571db-212">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="571db-214">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="571db-214">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="571db-216">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="571db-216">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="571db-218">a.</span><span class="sxs-lookup"><span data-stu-id="571db-218">a.</span></span> <span data-ttu-id="571db-219">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="571db-219">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="571db-220">b.</span><span class="sxs-lookup"><span data-stu-id="571db-220">b.</span></span> <span data-ttu-id="571db-221">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="571db-221">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="571db-222">c.</span><span class="sxs-lookup"><span data-stu-id="571db-222">c.</span></span> <span data-ttu-id="571db-223">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="571db-223">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="571db-224">d.</span><span class="sxs-lookup"><span data-stu-id="571db-224">d.</span></span> <span data-ttu-id="571db-225">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="571db-225">Click **Create**.</span></span>
 
### <a name="creating-a-skydesk-email-test-user"></a><span data-ttu-id="571db-226">Tworzenie użytkownika testowego SkyDesk poczty E-mail</span><span class="sxs-lookup"><span data-stu-id="571db-226">Creating a SkyDesk Email test user</span></span>

<span data-ttu-id="571db-227">W tej sekcji utworzysz użytkownika o nazwie Simona Britta w SkyDesk wiadomości E-mail.</span><span class="sxs-lookup"><span data-stu-id="571db-227">In this section, you create a user called Britta Simon in SkyDesk Email.</span></span>

1. <span data-ttu-id="571db-228">Polecenie **dostępu użytkownika** z pozostałych hello panelu w SkyDesk wiadomości E-mail, a następnie wprowadź nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="571db-228">Click on **User Access** from hello left panel in SkyDesk Email and then enter your username.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_58.png)

>[!NOTE] 
><span data-ttu-id="571db-230">Jeśli potrzebujesz toocreate zbiorczego użytkowników, należy toocontact hello [zespołem pomocy technicznej klienta poczty E-mail SkyDesk](https://www.skydesk.sg/support/).</span><span class="sxs-lookup"><span data-stu-id="571db-230">If you need toocreate bulk users, you need toocontact hello [SkyDesk Email Client support team](https://www.skydesk.sg/support/).</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="571db-231">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="571db-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="571db-232">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie tooSkyDesk dostępu do poczty E-mail.</span><span class="sxs-lookup"><span data-stu-id="571db-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSkyDesk Email.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="571db-234">**tooassign tooSkyDesk Simona Britta poczty E-mail, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="571db-234">**tooassign Britta Simon tooSkyDesk Email, perform hello following steps:**</span></span>

1. <span data-ttu-id="571db-235">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="571db-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="571db-237">Z listy aplikacji hello wybierz **E-mail SkyDesk**.</span><span class="sxs-lookup"><span data-stu-id="571db-237">In hello applications list, select **SkyDesk Email**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_app.png) 

3. <span data-ttu-id="571db-239">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="571db-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="571db-241">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="571db-241">Click **Add** button.</span></span> <span data-ttu-id="571db-242">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="571db-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="571db-244">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="571db-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="571db-245">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="571db-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="571db-246">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="571db-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="571db-247">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="571db-247">Testing single sign-on</span></span>

<span data-ttu-id="571db-248">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="571db-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="571db-249">Po kliknięciu hello E-mail SkyDesk kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour aplikacji SkyDesk poczty E-mail.</span><span class="sxs-lookup"><span data-stu-id="571db-249">When you click hello SkyDesk Email tile in hello Access Panel, you should get automatically signed-on tooyour SkyDesk Email application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="571db-250">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="571db-250">Additional resources</span></span>

* [<span data-ttu-id="571db-251">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="571db-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="571db-252">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="571db-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_203.png

