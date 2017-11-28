---
title: "Samouczek: Integracji Azure Active Directory z przyjęcia LMS | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i przyjęcia LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: a140a78a3a9474a6372a3ad4fb8251bd2452c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a><span data-ttu-id="8ba8b-103">Samouczek: Integracji Azure Active Directory z przyjęcia LMS</span><span class="sxs-lookup"><span data-stu-id="8ba8b-103">Tutorial: Azure Active Directory integration with Absorb LMS</span></span>

<span data-ttu-id="8ba8b-104">Z tego samouczka, dowiesz się, jak toointegrate Absorb LMS w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8ba8b-104">In this tutorial, you learn how toointegrate Absorb LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8ba8b-105">Integracja z usługą Azure AD przyjęcia LMS zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="8ba8b-105">Integrating Absorb LMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8ba8b-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooAbsorb LMS</span><span class="sxs-lookup"><span data-stu-id="8ba8b-106">You can control in Azure AD who has access tooAbsorb LMS</span></span>
- <span data-ttu-id="8ba8b-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAbsorb LMS (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ba8b-107">You can enable your users tooautomatically get signed-on tooAbsorb LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8ba8b-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8ba8b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8ba8b-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="8ba8b-110">[Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8ba8b-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ba8b-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8ba8b-111">Prerequisites</span></span>

<span data-ttu-id="8ba8b-112">tooconfigure integracji usługi Azure AD z przyjęcia LMS należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8ba8b-112">tooconfigure Azure AD integration with Absorb LMS, you need hello following items:</span></span>

- <span data-ttu-id="8ba8b-113">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ba8b-113">An Azure AD subscription</span></span>
- <span data-ttu-id="8ba8b-114">Przyjęcia LMS jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8ba8b-114">An Absorb LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8ba8b-115">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8ba8b-116">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="8ba8b-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8ba8b-117">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8ba8b-118">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ba8b-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8ba8b-119">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="8ba8b-119">Scenario description</span></span>
<span data-ttu-id="8ba8b-120">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8ba8b-121">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="8ba8b-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8ba8b-122">Dodawanie przyjęcia LMS z galerii hello</span><span class="sxs-lookup"><span data-stu-id="8ba8b-122">Adding Absorb LMS from hello gallery</span></span>
2. <span data-ttu-id="8ba8b-123">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8ba8b-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-absorb-lms-from-hello-gallery"></a><span data-ttu-id="8ba8b-124">Dodawanie przyjęcia LMS z galerii hello</span><span class="sxs-lookup"><span data-stu-id="8ba8b-124">Adding Absorb LMS from hello gallery</span></span>
<span data-ttu-id="8ba8b-125">tooconfigure hello integracji LMS przyjęcia w tooAzure AD, należy tooadd Absorb LMS z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-125">tooconfigure hello integration of Absorb LMS in tooAzure AD, you need tooadd Absorb LMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8ba8b-126">**tooadd Absorb LMS z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8ba8b-126">**tooadd Absorb LMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ba8b-127">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="8ba8b-129">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8ba8b-130">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-130">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="8ba8b-132">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="8ba8b-134">W polu wyszukiwania hello wpisz **przyjęcia LMS**, wybierz pozycję **przyjęcia LMS** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-134">In hello search box, type **Absorb LMS**, select **Absorb LMS** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Przyjęcia LMS hello listy wyników](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8ba8b-136">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8ba8b-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8ba8b-137">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z przyjęcia LMS oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="8ba8b-137">In this section, you configure and test Azure AD single sign-on with Absorb LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8ba8b-138">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w przyjęcia LMS jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Absorb LMS is tooa user in Azure AD.</span></span> <span data-ttu-id="8ba8b-139">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w przyjęcia LMS musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-139">In other words, a link relationship between an Azure AD user and hello related user in Absorb LMS needs toobe established.</span></span>

<span data-ttu-id="8ba8b-140">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w LMS przyjęcia.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Absorb LMS.</span></span>

<span data-ttu-id="8ba8b-141">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z przyjęcia LMS, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8ba8b-141">tooconfigure and test Azure AD single sign-on with Absorb LMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8ba8b-142">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-142">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8ba8b-143">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-143">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8ba8b-144">**[Tworzenie użytkownika testowego przyjęcia LMS](#create-an-absorb-lms-test-user)**  -toohave odpowiednikiem Simona Britta w przyjęcia LMS, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-144">**[Create an Absorb LMS test user](#create-an-absorb-lms-test-user)** - toohave a counterpart of Britta Simon in Absorb LMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8ba8b-145">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-145">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8ba8b-146">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-146">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8ba8b-147">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8ba8b-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8ba8b-148">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji przyjęcia LMS.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Absorb LMS application.</span></span>

<span data-ttu-id="8ba8b-149">**tooconfigure usługi Azure AD rejestracji jednokrotnej z przyjęcia LMS, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8ba8b-149">**tooconfigure Azure AD single sign-on with Absorb LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ba8b-150">W portalu Azure na powitania hello **przyjęcia LMS** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-150">In hello Azure portal, on hello **Absorb LMS** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="8ba8b-152">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. <span data-ttu-id="8ba8b-154">Na powitania **adresy URL i przyjęcia domeny LMS** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8ba8b-154">On hello **Absorb LMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Przyjęcia LMS domeny i adres URL pojedynczego logowania jednokrotnego informacji](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    <span data-ttu-id="8ba8b-156">a.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-156">a.</span></span> <span data-ttu-id="8ba8b-157">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="8ba8b-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>

    <span data-ttu-id="8ba8b-158">b.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-158">b.</span></span> <span data-ttu-id="8ba8b-159">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="8ba8b-159">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="8ba8b-160">Wartości te nie są hello prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-160">These values are not hello real.</span></span> <span data-ttu-id="8ba8b-161">Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-161">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="8ba8b-162">Skontaktuj się z [zespołem pomocy technicznej klienta LMS przyjęcia](https://www.absorblms.com/support) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-162">Contact [Absorb LMS Client support team](https://www.absorblms.com/support) tooget these values.</span></span> 

4. <span data-ttu-id="8ba8b-163">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. <span data-ttu-id="8ba8b-165">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-165">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="8ba8b-167">Na powitania **przyjęcia konfiguracji LMS** kliknij **skonfigurować LMS przyjęcia** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-167">On hello **Absorb LMS Configuration** section, click **Configure Absorb LMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8ba8b-168">Kopiuj hello **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="8ba8b-168">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Przyjęcia LMS konfiguracji](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. <span data-ttu-id="8ba8b-170">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy przyjęcia LMS tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-170">In a different web browser window, log in tooyour Absorb LMS company site as an administrator.</span></span>

9. <span data-ttu-id="8ba8b-171">Kliknij przycisk hello **ikonę konta** na powitania interfejsu administracyjnego.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-171">Click hello **Account Icon** on hello admin interface.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-absorblms-tutorial/1.png)

10. <span data-ttu-id="8ba8b-173">Kliknij przycisk **ustawienia portalu**.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-173">Click **Portal Settings**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. <span data-ttu-id="8ba8b-175">Kliknij przycisk hello **użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-175">Click hello **Users** tab.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-absorblms-tutorial/3.png)

12. <span data-ttu-id="8ba8b-177">Wykonaj następujące kroki tooaccess hello rejestracji jednokrotnej pola konfiguracji hello:</span><span class="sxs-lookup"><span data-stu-id="8ba8b-177">Perform hello following steps tooaccess hello Single Sign-On configuration fields:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-absorblms-tutorial/4.png)

    <span data-ttu-id="8ba8b-179">a.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-179">a.</span></span> <span data-ttu-id="8ba8b-180">Wybierz odpowiednie hello **tryb**.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-180">Select hello appropriate **Mode**.</span></span>

    <span data-ttu-id="8ba8b-181">b.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-181">b.</span></span> <span data-ttu-id="8ba8b-182">Otwórz hello certyfikatu, który został pobrany z portalu Azure w programie Notatnik hello Usuń hello **---BEGIN CERTIFICATE---** i **---END CERTIFICATE---** tag, a następnie wklej hello pozostała zawartość Witaj **klucza** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-182">Open hello Certificate that you have downloaded from hello Azure portal in notepad, remove hello **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste hello remaining content in hello **Key** textbox.</span></span>
    
    <span data-ttu-id="8ba8b-183">c.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-183">c.</span></span> <span data-ttu-id="8ba8b-184">W hello **właściwość identyfikatora**, wybierz hello odpowiedni atrybut, który został skonfigurowany jako hello identyfikatora użytkownika w hello Azure AD (na przykład, jeśli wybrano hello userprinciplename w usłudze Azure AD, a następnie zaznaczony tutaj nazwę użytkownika.)</span><span class="sxs-lookup"><span data-stu-id="8ba8b-184">In hello **Id Property**, select hello appropriate attribute which you have configured as hello user identifier in hello Azure AD (For example, If hello userprinciplename is selected in Azure AD, then Username would be selected here.)</span></span>

    <span data-ttu-id="8ba8b-185">d.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-185">d.</span></span> <span data-ttu-id="8ba8b-186">W hello **adres URL logowania**, Wklej hello **"SAML pojedynczy znak na adres URL usługi"** wartość została skopiowana z hello **Konfigurowanie logowania jednokrotnego** okna hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-186">In hello **Login URL**, paste hello **“SAML Single Sign-On Service URL”** value you have copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

    <span data-ttu-id="8ba8b-187">e.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-187">e.</span></span> <span data-ttu-id="8ba8b-188">W hello **adresu URL wylogowania**, Wklej hello **"Adres URL Sign-Out"** wartość została skopiowana z hello **Konfigurowanie logowania jednokrotnego** okna hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-188">In hello **Logout URL**, paste hello **“Sign-Out URL”** value you have copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

13. <span data-ttu-id="8ba8b-189">Włącz **"Zezwalaj tylko na logowanie SSO"**.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-189">Enable **‘Only Allow SSO Login’**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-absorblms-tutorial/5.png)

14. <span data-ttu-id="8ba8b-191">Kliknij przycisk **"Zapisz".**</span><span class="sxs-lookup"><span data-stu-id="8ba8b-191">Click **"Save."**</span></span>

> [!TIP]
> <span data-ttu-id="8ba8b-192">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="8ba8b-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8ba8b-193">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8ba8b-194">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8ba8b-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8ba8b-195">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ba8b-195">Create an Azure AD test user</span></span>

<span data-ttu-id="8ba8b-196">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="8ba8b-198">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8ba8b-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ba8b-199">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8ba8b-201">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8ba8b-203">U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-203">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![przycisk Dodaj Hello](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8ba8b-205">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8ba8b-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8ba8b-207">a.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-207">a.</span></span> <span data-ttu-id="8ba8b-208">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8ba8b-209">b.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-209">b.</span></span> <span data-ttu-id="8ba8b-210">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8ba8b-211">c.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-211">c.</span></span> <span data-ttu-id="8ba8b-212">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8ba8b-213">d.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-213">d.</span></span> <span data-ttu-id="8ba8b-214">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-214">Click **Create**.</span></span>

### <a name="create-an-absorb-lms-test-user"></a><span data-ttu-id="8ba8b-215">Tworzenie użytkownika testowego przyjęcia LMS</span><span class="sxs-lookup"><span data-stu-id="8ba8b-215">Create an Absorb LMS test user</span></span>

<span data-ttu-id="8ba8b-216">toolog użytkowników tooenable usługi Azure AD w tooAbsorb LMS, muszą mieć przydzielone w tooAbsorb LMS.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-216">tooenable Azure AD users toolog in tooAbsorb LMS, they must be provisioned in tooAbsorb LMS.</span></span>  
<span data-ttu-id="8ba8b-217">W przypadku przyjęcia LMS inicjowania obsługi administracyjnej jest zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-217">For Absorb LMS, provisioning is a manual task.</span></span>

<span data-ttu-id="8ba8b-218">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="8ba8b-218">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ba8b-219">Zaloguj się za tooyour przyjęcia LMS witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-219">Log in tooyour Absorb LMS company site as an administrator.</span></span>

2. <span data-ttu-id="8ba8b-220">Kliknij przycisk **użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-220">Click **Users** tab.</span></span>

    ![Zaproś inne osoby](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. <span data-ttu-id="8ba8b-222">Kliknij przycisk **użytkowników** w obszarze hello **użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-222">Click **Users** under hello **Users** tab.</span></span>

    ![Zaproś inne osoby](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  <span data-ttu-id="8ba8b-224">Wybierz **użytkownika** z **Dodaj nowy** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-224">Select **User** from **Add New** drop-down.</span></span>

    ![Zaproś inne osoby](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. <span data-ttu-id="8ba8b-226">Na powitania **Dodaj użytkownika** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8ba8b-226">On hello **Add User** page, perform hello following steps:</span></span>

    ![Zaproś inne osoby](./media/active-directory-saas-absorblms-tutorial/user.png)

    <span data-ttu-id="8ba8b-228">a.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-228">a.</span></span> <span data-ttu-id="8ba8b-229">W hello **imię** pole tekstowe, typ hello imię jak Britta.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-229">In hello **First Name** textbox, type hello first name like Britta.</span></span>

    <span data-ttu-id="8ba8b-230">b.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-230">b.</span></span> <span data-ttu-id="8ba8b-231">W hello **nazwisko** pole tekstowe, typ hello nazwisko jak Simona.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-231">In hello **Last Name** textbox, type hello last name like Simon.</span></span>
    
    <span data-ttu-id="8ba8b-232">c.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-232">c.</span></span> <span data-ttu-id="8ba8b-233">W hello **Username** tekstowym, wpisz nazwę użytkownika hello jak Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-233">In hello **Username** textbox, type hello user name like Britta Simon.</span></span>

    <span data-ttu-id="8ba8b-234">d.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-234">d.</span></span> <span data-ttu-id="8ba8b-235">W hello **hasło** tekstowym, wpisz hasło hello Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-235">In hello **Password** textbox, type hello password of Britta Simon.</span></span>

    <span data-ttu-id="8ba8b-236">e.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-236">e.</span></span> <span data-ttu-id="8ba8b-237">W hello **Potwierdź hasło** pole tekstowe, hello typu tego samego hasła.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-237">In hello **Confirm Password** textbox, type hello same password.</span></span>
    
    <span data-ttu-id="8ba8b-238">f.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-238">f.</span></span> <span data-ttu-id="8ba8b-239">Należy go jako **ACTIVE**.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-239">Make it as **ACTIVE**.</span></span>   

6. <span data-ttu-id="8ba8b-240">Kliknij przycisk **"Zapisz".**</span><span class="sxs-lookup"><span data-stu-id="8ba8b-240">Click **"Save."**</span></span>
 
### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="8ba8b-241">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ba8b-241">Assign hello Azure AD test user</span></span>

<span data-ttu-id="8ba8b-242">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooAbsorb LMS.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAbsorb LMS.</span></span>

![Przypisanie roli użytkownika hello][200]

<span data-ttu-id="8ba8b-244">**tooassign tooAbsorb Simona Britta LMS, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8ba8b-244">**tooassign Britta Simon tooAbsorb LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ba8b-245">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="8ba8b-247">Z listy aplikacji hello wybierz **przyjęcia LMS**.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-247">In hello applications list, select **Absorb LMS**.</span></span>

    ![łącze przyjęcia LMS Hello na liście aplikacji hello](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. <span data-ttu-id="8ba8b-249">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202] 

4. <span data-ttu-id="8ba8b-251">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-251">Click **Add** button.</span></span> <span data-ttu-id="8ba8b-252">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="8ba8b-254">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8ba8b-255">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8ba8b-256">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8ba8b-257">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8ba8b-257">Test single sign-on</span></span>

<span data-ttu-id="8ba8b-258">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8ba8b-259">Kliknij przycisk hello przyjęcia LMS kafelka w hello panelu dostępu otrzymasz automatycznie zalogowane tooyour przyjęcia LMS aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ba8b-259">Click hello Absorb LMS tile in hello Access Panel, you will get automatically signed-on tooyour Absorb LMS application.</span></span> <span data-ttu-id="8ba8b-260">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="8ba8b-260">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8ba8b-261">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8ba8b-261">Additional resources</span></span>

* [<span data-ttu-id="8ba8b-262">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ba8b-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8ba8b-263">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8ba8b-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

