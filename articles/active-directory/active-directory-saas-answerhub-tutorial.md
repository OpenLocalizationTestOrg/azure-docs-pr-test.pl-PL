---
title: 'Samouczek: Integracji Azure Active Directory z AnswerHub | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i AnswerHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 818b91d7-01df-4b36-9706-f167c710a73c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 90b530da31abe7e6f18bfa2c5409f8ff1d4f1063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-answerhub"></a><span data-ttu-id="ee574-103">Samouczek: Integracji Azure Active Directory z AnswerHub</span><span class="sxs-lookup"><span data-stu-id="ee574-103">Tutorial: Azure Active Directory integration with AnswerHub</span></span>

<span data-ttu-id="ee574-104">Z tego samouczka, dowiesz się, jak toointegrate AnswerHub w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ee574-104">In this tutorial, you learn how toointegrate AnswerHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ee574-105">Integracja z usługą Azure AD AnswerHub zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ee574-105">Integrating AnswerHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ee574-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooAnswerHub</span><span class="sxs-lookup"><span data-stu-id="ee574-106">You can control in Azure AD who has access tooAnswerHub</span></span>
- <span data-ttu-id="ee574-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAnswerHub (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee574-107">You can enable your users tooautomatically get signed-on tooAnswerHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ee574-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ee574-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ee574-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ee574-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee574-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ee574-110">Prerequisites</span></span>

<span data-ttu-id="ee574-111">tooconfigure integracji z usługą Azure AD z AnswerHub należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ee574-111">tooconfigure Azure AD integration with AnswerHub, you need hello following items:</span></span>

- <span data-ttu-id="ee574-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee574-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ee574-113">AnswerHub logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ee574-113">An AnswerHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ee574-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ee574-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ee574-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ee574-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ee574-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ee574-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ee574-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ee574-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ee574-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ee574-118">Scenario description</span></span>
<span data-ttu-id="ee574-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ee574-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ee574-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ee574-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ee574-121">Dodawanie AnswerHub z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ee574-121">Adding AnswerHub from hello gallery</span></span>
2. <span data-ttu-id="ee574-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ee574-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-answerhub-from-hello-gallery"></a><span data-ttu-id="ee574-123">Dodawanie AnswerHub z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ee574-123">Adding AnswerHub from hello gallery</span></span>
<span data-ttu-id="ee574-124">tooconfigure hello integracji AnswerHub do usługi Azure AD, należy tooadd AnswerHub z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ee574-124">tooconfigure hello integration of AnswerHub into Azure AD, you need tooadd AnswerHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ee574-125">**tooadd AnswerHub z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ee574-125">**tooadd AnswerHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee574-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ee574-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="ee574-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ee574-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ee574-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ee574-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ee574-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ee574-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ee574-133">W polu wyszukiwania hello wpisz **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="ee574-133">In hello search box, type **AnswerHub**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_search.png)

5. <span data-ttu-id="ee574-135">W panelu wyników hello zaznacz **AnswerHub**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ee574-135">In hello results panel, select **AnswerHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ee574-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ee574-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ee574-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z AnswerHub w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="ee574-138">In this section, you configure and test Azure AD single sign-on with AnswerHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ee574-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w AnswerHub jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ee574-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AnswerHub is tooa user in Azure AD.</span></span> <span data-ttu-id="ee574-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w AnswerHub musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="ee574-140">In other words, a link relationship between an Azure AD user and hello related user in AnswerHub needs toobe established.</span></span>

<span data-ttu-id="ee574-141">W AnswerHub, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="ee574-141">In AnswerHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ee574-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z AnswerHub, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ee574-142">tooconfigure and test Azure AD single sign-on with AnswerHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ee574-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ee574-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ee574-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ee574-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ee574-145">**[Tworzenie użytkownika testowego AnswerHub](#creating-an-answerhub-test-user)**  -toohave odpowiednikiem Simona Britta w AnswerHub, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ee574-145">**[Creating an AnswerHub test user](#creating-an-answerhub-test-user)** - toohave a counterpart of Britta Simon in AnswerHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ee574-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ee574-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ee574-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="ee574-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ee574-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ee574-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ee574-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="ee574-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AnswerHub application.</span></span>

<span data-ttu-id="ee574-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z AnswerHub, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ee574-150">**tooconfigure Azure AD single sign-on with AnswerHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee574-151">W portalu Azure na powitania hello **AnswerHub** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ee574-151">In hello Azure portal, on hello **AnswerHub** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="ee574-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ee574-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_samlbase.png)

3. <span data-ttu-id="ee574-155">Na powitania **AnswerHub domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ee574-155">On hello **AnswerHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_url.png)

    <span data-ttu-id="ee574-157">a.</span><span class="sxs-lookup"><span data-stu-id="ee574-157">a.</span></span> <span data-ttu-id="ee574-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="ee574-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.answerhub.com`</span></span>

    <span data-ttu-id="ee574-159">b.</span><span class="sxs-lookup"><span data-stu-id="ee574-159">b.</span></span> <span data-ttu-id="ee574-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="ee574-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company>.answerhub.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ee574-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="ee574-161">These values are not real.</span></span> <span data-ttu-id="ee574-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="ee574-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ee574-163">Skontaktuj się z [zespołem pomocy technicznej klienta AnswerHub](mailto:success@answerhub.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="ee574-163">Contact [AnswerHub Client support team](mailto:success@answerhub.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="ee574-164">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ee574-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_certificate.png) 

5. <span data-ttu-id="ee574-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ee574-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-answerhub-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ee574-168">Na powitania **konfiguracji AnswerHub** kliknij **skonfigurować AnswerHub** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="ee574-168">On hello **AnswerHub Configuration** section, click **Configure AnswerHub** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ee574-169">Witaj kopii **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="ee574-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_configure.png) 

7. <span data-ttu-id="ee574-171">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy AnswerHub jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ee574-171">In a different web browser window, log into your AnswerHub company site as an administrator.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="ee574-172">Jeśli potrzebujesz pomocy przy konfigurowaniu AnswerHub, skontaktuj się z [zespołem pomocy technicznej firmy AnswerHub](mailto:success@answerhub.com.).</span><span class="sxs-lookup"><span data-stu-id="ee574-172">If you need help configuring AnswerHub, contact [AnswerHub's support team](mailto:success@answerhub.com.).</span></span>
   
8. <span data-ttu-id="ee574-173">Przejdź za**administracji**.</span><span class="sxs-lookup"><span data-stu-id="ee574-173">Go too**Administration**.</span></span>

9. <span data-ttu-id="ee574-174">Kliknij przycisk hello **użytkowników i grup** kartę.</span><span class="sxs-lookup"><span data-stu-id="ee574-174">Click hello **User and Group** tab.</span></span>

10. <span data-ttu-id="ee574-175">W okienku nawigacji hello na powitania po lewej stronie, w hello **społecznościowych ustawienia** , kliknij przycisk **Instalatora SAML**.</span><span class="sxs-lookup"><span data-stu-id="ee574-175">In hello navigation pane on hello left side, in hello **Social Settings** section, click **SAML Setup**.</span></span>

11. <span data-ttu-id="ee574-176">Kliknij przycisk **IDP Config** kartę.</span><span class="sxs-lookup"><span data-stu-id="ee574-176">Click **IDP Config** tab.</span></span>

12. <span data-ttu-id="ee574-177">Na powitania **IDP Config** karcie, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ee574-177">On hello **IDP Config** tab, perform hello following steps:</span></span>

     <span data-ttu-id="ee574-178">![Instalator SAML](./media/active-directory-saas-answerhub-tutorial/ic785172.png "Instalatora SAML")</span><span class="sxs-lookup"><span data-stu-id="ee574-178">![SAML Setup](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML Setup")</span></span>  
  
     <span data-ttu-id="ee574-179">a.</span><span class="sxs-lookup"><span data-stu-id="ee574-179">a.</span></span> <span data-ttu-id="ee574-180">W **adres URL logowania IDP** pole tekstowe, Wklej **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ee574-180">In **IDP Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
     <span data-ttu-id="ee574-181">b.</span><span class="sxs-lookup"><span data-stu-id="ee574-181">b.</span></span> <span data-ttu-id="ee574-182">W **adresu URL wylogowania IDP** pole tekstowe, Wklej **Sign-Out URL** wartość, która została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ee574-182">In **IDP Logout URL** textbox, paste **Sign-Out URL** value which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="ee574-183">c.</span><span class="sxs-lookup"><span data-stu-id="ee574-183">c.</span></span> <span data-ttu-id="ee574-184">W **Format identyfikatora nazwy IDP** pole tekstowe, wprowadź nazwę użytkownika hello identyfikator wartość sam jako wybrane w portalu Azure w **atrybuty użytkownika** sekcji.</span><span class="sxs-lookup"><span data-stu-id="ee574-184">In **IDP Name Identifier Format** textbox, enter hello user Identifier value same as selected in Azure portal in **User Attributes** section.</span></span>
  
     <span data-ttu-id="ee574-185">d.</span><span class="sxs-lookup"><span data-stu-id="ee574-185">d.</span></span> <span data-ttu-id="ee574-186">Kliknij przycisk **klucze i certyfikaty**.</span><span class="sxs-lookup"><span data-stu-id="ee574-186">Click **Keys and Certificates**.</span></span>

13. <span data-ttu-id="ee574-187">Na karcie klucze i certyfikaty hello wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ee574-187">On hello Keys and Certificates tab, perform hello following steps:</span></span>
    
     <span data-ttu-id="ee574-188">![Klucze i certyfikaty](./media/active-directory-saas-answerhub-tutorial/ic785173.png "klucze i certyfikaty")</span><span class="sxs-lookup"><span data-stu-id="ee574-188">![Keys and Certificates](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Keys and Certificates")</span></span>  
 
     <span data-ttu-id="ee574-189">a.</span><span class="sxs-lookup"><span data-stu-id="ee574-189">a.</span></span> <span data-ttu-id="ee574-190">Otwórz z zakodowanego certyfikatu base-64, który został pobrany z portalu Azure w programie Notatnik hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **IDP klucza publicznego (x 509 Format)** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="ee574-190">Open your base-64 encoded certificate which you have downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **IDP Public Key (x509 Format)** textbox.</span></span>
  
     <span data-ttu-id="ee574-191">b.</span><span class="sxs-lookup"><span data-stu-id="ee574-191">b.</span></span> <span data-ttu-id="ee574-192">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ee574-192">Click **Save**.</span></span>

14. <span data-ttu-id="ee574-193">Na powitania **IDP Config** , kliknij pozycję **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="ee574-193">On hello **IDP Config** tab, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="ee574-194">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="ee574-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ee574-195">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="ee574-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ee574-196">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ee574-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ee574-197">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee574-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="ee574-198">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="ee574-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="ee574-200">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ee574-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee574-201">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ee574-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ee574-203">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ee574-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ee574-205">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ee574-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ee574-207">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ee574-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ee574-209">a.</span><span class="sxs-lookup"><span data-stu-id="ee574-209">a.</span></span> <span data-ttu-id="ee574-210">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ee574-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ee574-211">b.</span><span class="sxs-lookup"><span data-stu-id="ee574-211">b.</span></span> <span data-ttu-id="ee574-212">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ee574-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ee574-213">c.</span><span class="sxs-lookup"><span data-stu-id="ee574-213">c.</span></span> <span data-ttu-id="ee574-214">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="ee574-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ee574-215">d.</span><span class="sxs-lookup"><span data-stu-id="ee574-215">d.</span></span> <span data-ttu-id="ee574-216">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ee574-216">Click **Create**.</span></span>
 
### <a name="creating-an-answerhub-test-user"></a><span data-ttu-id="ee574-217">Tworzenie użytkownika testowego AnswerHub</span><span class="sxs-lookup"><span data-stu-id="ee574-217">Creating an AnswerHub test user</span></span>

<span data-ttu-id="ee574-218">toolog użytkowników tooenable usługi Azure AD w tooAnswerHub, muszą mieć przydzielone do AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="ee574-218">tooenable Azure AD users toolog in tooAnswerHub, they must be provisioned into AnswerHub.</span></span>  
<span data-ttu-id="ee574-219">W przypadku hello AnswerHub Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="ee574-219">In hello case of AnswerHub, provisioning is a manual task.</span></span>

<span data-ttu-id="ee574-220">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ee574-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee574-221">Zaloguj się za tooyour **AnswerHub** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ee574-221">Log in tooyour **AnswerHub** company site as administrator.</span></span>

2. <span data-ttu-id="ee574-222">Przejdź za**administracji**.</span><span class="sxs-lookup"><span data-stu-id="ee574-222">Go too**Administration**.</span></span>

3. <span data-ttu-id="ee574-223">Kliknij przycisk hello **użytkownicy i grupy** kartę.</span><span class="sxs-lookup"><span data-stu-id="ee574-223">Click hello **Users & Groups** tab.</span></span>

4. <span data-ttu-id="ee574-224">W okienku nawigacji hello na powitania po lewej stronie, w hello **Zarządzanie użytkownikami** kliknij **Tworzenie lub importowanie użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="ee574-224">In hello navigation pane on hello left side, in hello **Manage Users** section, click **Create or import users**.</span></span>
   
   <span data-ttu-id="ee574-225">![Użytkownicy i grupy](./media/active-directory-saas-answerhub-tutorial/ic785175.png "użytkownicy i grupy")</span><span class="sxs-lookup"><span data-stu-id="ee574-225">![Users & Groups](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Users & Groups")</span></span>

5. <span data-ttu-id="ee574-226">Typ hello **adres E-mail**, **Username** i **hasło** prawidłowy Azure powiązane pola tekstowe mają tooprovision w hello konta usługi Active Directory, a następnie kliknij  **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ee574-226">Type hello **Email address**, **Username** and **Password** of a valid Azure Active Directory account you want tooprovision into hello related textboxes, and then click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="ee574-227">Możesz użyć innych AnswerHub użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez AnswerHub tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="ee574-227">You can use any other AnswerHub user account creation tools or APIs provided by AnswerHub tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ee574-228">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee574-228">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ee574-229">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooAnswerHub.</span><span class="sxs-lookup"><span data-stu-id="ee574-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAnswerHub.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="ee574-231">**tooassign tooAnswerHub Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ee574-231">**tooassign Britta Simon tooAnswerHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="ee574-232">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ee574-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ee574-234">Z listy aplikacji hello wybierz **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="ee574-234">In hello applications list, select **AnswerHub**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_app.png) 

3. <span data-ttu-id="ee574-236">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ee574-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="ee574-238">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ee574-238">Click **Add** button.</span></span> <span data-ttu-id="ee574-239">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ee574-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="ee574-241">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ee574-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ee574-242">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ee574-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ee574-243">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ee574-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ee574-244">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ee574-244">Testing single sign-on</span></span>

<span data-ttu-id="ee574-245">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ee574-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ee574-246">Po kliknięciu kafelka AnswerHub hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour AnswerHub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ee574-246">When you click hello AnswerHub tile in hello Access Panel, you should get automatically signed-on tooyour AnswerHub application.</span></span>
<span data-ttu-id="ee574-247">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ee574-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ee574-248">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ee574-248">Additional resources</span></span>

* [<span data-ttu-id="ee574-249">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ee574-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ee574-250">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ee574-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_203.png

