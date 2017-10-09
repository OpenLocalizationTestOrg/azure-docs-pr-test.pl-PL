---
title: "Samouczek: Integracji Azure Active Directory z usługi Google Apps w usłudze Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i usługi Google Apps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2093b5ab605ec0d7bbefe7a78e1eede34d756f53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a><span data-ttu-id="08ae4-103">Samouczek: Integracji Azure Active Directory z usługi Google Apps</span><span class="sxs-lookup"><span data-stu-id="08ae4-103">Tutorial: Azure Active Directory integration with Google Apps</span></span>

<span data-ttu-id="08ae4-104">Z tego samouczka, dowiesz się, jak toointegrate usługi Google Apps w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="08ae4-104">In this tutorial, you learn how toointegrate Google Apps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="08ae4-105">Integrowanie usługi Google Apps z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="08ae4-105">Integrating Google Apps with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="08ae4-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooGoogle aplikacji</span><span class="sxs-lookup"><span data-stu-id="08ae4-106">You can control in Azure AD who has access tooGoogle Apps</span></span>
- <span data-ttu-id="08ae4-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooGoogle aplikacji (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="08ae4-107">You can enable your users tooautomatically get signed-on tooGoogle Apps (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="08ae4-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="08ae4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="08ae4-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="08ae4-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08ae4-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="08ae4-110">Prerequisites</span></span>

<span data-ttu-id="08ae4-111">tooconfigure integracji z usługą Azure AD z usługi Google Apps należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="08ae4-111">tooconfigure Azure AD integration with Google Apps, you need hello following items:</span></span>

- <span data-ttu-id="08ae4-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="08ae4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="08ae4-113">Usługi Google Apps logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="08ae4-113">A Google Apps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="08ae4-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="08ae4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="08ae4-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="08ae4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="08ae4-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="08ae4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="08ae4-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="08ae4-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="08ae4-118">Samouczek wideo</span><span class="sxs-lookup"><span data-stu-id="08ae4-118">Video tutorial</span></span>
<span data-ttu-id="08ae4-119">Jak tooEnable rejestracji jednokrotnej tooGoogle aplikacji w ciągu 2 minut:</span><span class="sxs-lookup"><span data-stu-id="08ae4-119">How tooEnable Single Sign-On tooGoogle Apps in 2 Minutes:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a><span data-ttu-id="08ae4-120">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="08ae4-120">Frequently Asked Questions</span></span>
1. <span data-ttu-id="08ae4-121">**Pytanie: czy Chromebooks i innych urządzeniach Chrome zgodne z usługą Azure AD rejestracji jednokrotnej?**</span><span class="sxs-lookup"><span data-stu-id="08ae4-121">**Q: Are Chromebooks and other Chrome devices compatible with Azure AD single sign-on?**</span></span>
   
    <span data-ttu-id="08ae4-122">A: tak, użytkownicy będą mogli toosign do swoich urządzeń Chromebook przy użyciu swoich poświadczeń usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="08ae4-122">A: Yes, users are able toosign into their Chromebook devices using their Azure AD credentials.</span></span> <span data-ttu-id="08ae4-123">Zobacz to [usługi Google Apps obsługuje artykułu](https://support.google.com/chrome/a/answer/6060880) informacji o tym, dlaczego użytkownicy mogą się monit o poświadczenia dwa razy.</span><span class="sxs-lookup"><span data-stu-id="08ae4-123">See this [Google Apps support article](https://support.google.com/chrome/a/answer/6060880) for information on why users may get prompted for credentials twice.</span></span>

2. <span data-ttu-id="08ae4-124">**Pytanie: czy włączyć logowanie jednokrotne, użytkownicy będą się mogli toouse ich toosign poświadczeń usługi Azure AD do żadnego produktu Google, takich jak klasy Google, GMail, dysk Google, YouTube itd.?**</span><span class="sxs-lookup"><span data-stu-id="08ae4-124">**Q: If I enable single sign-on, will users be able toouse their Azure AD credentials toosign into any Google product, such as Google Classroom, GMail, Google Drive, YouTube, and so on?**</span></span>
   
    <span data-ttu-id="08ae4-125">Odpowiedź: tak, w zależności od [aplikacje, które Google](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) wybierz tooenable lub wyłączenia dla Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="08ae4-125">A: Yes, depending on [which Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) you choose tooenable or disable for your organization.</span></span>

3. <span data-ttu-id="08ae4-126">**Pytanie: czy można włączyć logowanie jednokrotne dla tylko podzestaw użytkowników usługi Google Apps?**</span><span class="sxs-lookup"><span data-stu-id="08ae4-126">**Q: Can I enable single sign-on for only a subset of my Google Apps users?**</span></span>
   
    <span data-ttu-id="08ae4-127">A: wymaga włączenia logowania jednokrotnego natychmiast nie wszystkie Twoje aplikacje Google użytkowników tooauthenticate przy użyciu poświadczeń usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="08ae4-127">A: No, turning on single sign-on immediately requires all your Google Apps users tooauthenticate with their Azure AD credentials.</span></span> <span data-ttu-id="08ae4-128">Ponieważ usługi Google Apps nie obsługuje posiadanie wielu dostawców tożsamości, hello dostawcy tożsamości w danym środowisku usługi Google Apps można usługi Azure AD lub Google —, ale nie oba na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="08ae4-128">Because Google Apps doesn't support having multiple identity providers, hello identity provider for your Google Apps environment can either be Azure AD or Google -- but not both at hello same time.</span></span>

4. <span data-ttu-id="08ae4-129">**Pytanie: czy użytkownik jest zalogowany przy użyciu systemu Windows, czy na pewno uwierzytelniają automatycznie tooGoogle aplikacji bez pobierania zostanie wyświetlony monit o podanie hasła?**</span><span class="sxs-lookup"><span data-stu-id="08ae4-129">**Q: If a user is signed in through Windows, are they automatically authenticate tooGoogle Apps without getting prompted for a password?**</span></span>
   
    <span data-ttu-id="08ae4-130">Odpowiedź: istnieją dwie opcje dotyczące włączania tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="08ae4-130">A: There are two options for enabling this scenario.</span></span> <span data-ttu-id="08ae4-131">Najpierw użytkownicy mogą zalogować się do urządzeń z systemem Windows 10 za pomocą [usługi Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="08ae4-131">First, users could sign into Windows 10 devices via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span> <span data-ttu-id="08ae4-132">Alternatywnie użytkownicy mogą zalogować się do urządzeń z systemem Windows, które są przyłączone do domeny tooan lokalnej usługi Active Directory została włączona dla pojedynczego logowania jednokrotnego tooAzure AD za pomocą [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="08ae4-132">Alternatively, users could sign into Windows devices that are domain-joined tooan on-premises Active Directory that has been enabled for single sign-on tooAzure AD via an [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) deployment.</span></span> <span data-ttu-id="08ae4-133">Obie te opcje wymagają tooperform hello etapami powitania po tooenable samouczka rejestracji jednokrotnej między usługą Azure AD i usługi Google Apps.</span><span class="sxs-lookup"><span data-stu-id="08ae4-133">Both options require you tooperform hello steps in hello following tutorial tooenable single sign-on between Azure AD and Google Apps.</span></span>

## <a name="scenario-description"></a><span data-ttu-id="08ae4-134">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="08ae4-134">Scenario description</span></span>
<span data-ttu-id="08ae4-135">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="08ae4-135">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="08ae4-136">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="08ae4-136">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="08ae4-137">Dodawanie usługi Google Apps z galerii hello</span><span class="sxs-lookup"><span data-stu-id="08ae4-137">Adding Google Apps from hello gallery</span></span>
2. <span data-ttu-id="08ae4-138">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="08ae4-138">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-google-apps-from-hello-gallery"></a><span data-ttu-id="08ae4-139">Dodawanie usługi Google Apps z galerii hello</span><span class="sxs-lookup"><span data-stu-id="08ae4-139">Adding Google Apps from hello gallery</span></span>
<span data-ttu-id="08ae4-140">tooconfigure hello integracji usługi Google Apps w usłudze Azure Active Directory, należy tooadd usługi Google Apps z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="08ae4-140">tooconfigure hello integration of Google Apps into Azure AD, you need tooadd Google Apps from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="08ae4-141">**tooadd usługi Google Apps z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="08ae4-141">**tooadd Google Apps from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="08ae4-142">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="08ae4-142">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="08ae4-144">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="08ae4-144">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="08ae4-145">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="08ae4-145">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="08ae4-147">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="08ae4-147">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="08ae4-149">W polu wyszukiwania hello wpisz **usługi Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="08ae4-149">In hello search box, type **Google Apps**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. <span data-ttu-id="08ae4-151">W panelu wyników hello, wybierz **usługi Google Apps**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="08ae4-151">In hello results panel, select **Google Apps**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="08ae4-153">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="08ae4-153">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="08ae4-154">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługi Google Apps oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="08ae4-154">In this section, you configure and test Azure AD single sign-on with Google Apps based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="08ae4-155">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w usługi Google Apps jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="08ae4-155">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Google Apps is tooa user in Azure AD.</span></span> <span data-ttu-id="08ae4-156">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w usługi Google Apps musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="08ae4-156">In other words, a link relationship between an Azure AD user and hello related user in Google Apps needs toobe established.</span></span>

<span data-ttu-id="08ae4-157">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w usługi Google Apps.</span><span class="sxs-lookup"><span data-stu-id="08ae4-157">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Google Apps.</span></span>

<span data-ttu-id="08ae4-158">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z usługi Google Apps, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="08ae4-158">tooconfigure and test Azure AD single sign-on with Google Apps, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="08ae4-159">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="08ae4-159">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="08ae4-160">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="08ae4-160">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="08ae4-161">**[Tworzenie użytkownika testowego usługi Google Apps](#creating-a-google-apps-test-user)**  -toohave odpowiednikiem Simona Britta w usługi Google Apps, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="08ae4-161">**[Creating a Google Apps test user](#creating-a-google-apps-test-user)** - toohave a counterpart of Britta Simon in Google Apps that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="08ae4-162">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="08ae4-162">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="08ae4-163">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="08ae4-163">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="08ae4-164">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="08ae4-164">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="08ae4-165">W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne do aplikacji Google Apps.</span><span class="sxs-lookup"><span data-stu-id="08ae4-165">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Google Apps application.</span></span>

<span data-ttu-id="08ae4-166">**tooconfigure usługi Azure AD rejestracji jednokrotnej z usługi Google Apps, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="08ae4-166">**tooconfigure Azure AD single sign-on with Google Apps, perform hello following steps:**</span></span>

1. <span data-ttu-id="08ae4-167">W portalu Azure na powitania hello **usługi Google Apps** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="08ae4-167">In hello Azure portal, on hello **Google Apps** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="08ae4-169">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="08ae4-169">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. <span data-ttu-id="08ae4-171">Na powitania **domenę usługi Google Apps i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="08ae4-171">On hello **Google Apps Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    <span data-ttu-id="08ae4-173">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://mail.google.com/a/<yourdomain>`</span><span class="sxs-lookup"><span data-stu-id="08ae4-173">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://mail.google.com/a/<yourdomain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="08ae4-174">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="08ae4-174">This value is not real.</span></span> <span data-ttu-id="08ae4-175">Zaktualizuj wartość hello z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="08ae4-175">Update hello value with hello actual Sign-on URL.</span></span> <span data-ttu-id="08ae4-176">Skontaktuj się z hello [zespołem pomocy technicznej usługi Google](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="08ae4-176">contact hello [Google support team](https://www.google.com/contact/).</span></span>
 
4. <span data-ttu-id="08ae4-177">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu** , a następnie Zapisz certyfikat hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="08ae4-177">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. <span data-ttu-id="08ae4-179">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="08ae4-179">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="08ae4-181">Na powitania **Google Apps konfiguracji** kliknij **Konfigurowanie usługi Google Apps** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="08ae4-181">On hello **Google Apps Configuration** section, click **Configure Google Apps** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="08ae4-182">Kopiuj hello **Sign-Out adres URL, SAML pojedynczy znak na adres URL usługi i zmień adres URL hasła** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="08ae4-182">Copy hello **Sign-Out URL, SAML Single Sign-On Service URL and Change password URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. <span data-ttu-id="08ae4-184">Otwórz nową kartę w przeglądarce i zaloguj się do hello [konsoli administracyjnej usługi Google Apps](http://admin.google.com/) przy użyciu konta administratora.</span><span class="sxs-lookup"><span data-stu-id="08ae4-184">Open a new tab in your browser, and sign into hello [Google Apps Admin Console](http://admin.google.com/) using your administrator account.</span></span>

8. <span data-ttu-id="08ae4-185">Kliknij przycisk **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="08ae4-185">Click **Security**.</span></span> <span data-ttu-id="08ae4-186">Jeśli nie widzisz hello łącza może być ukryty w obszarze hello **więcej formantów** menu u dołu hello hello ekranu.</span><span class="sxs-lookup"><span data-stu-id="08ae4-186">If you don't see hello link, it may be hidden under hello **More Controls** menu at hello bottom of hello screen.</span></span>
   
    ![Kliknij pozycję Zabezpieczenia.][10]

9. <span data-ttu-id="08ae4-188">Na powitania **zabezpieczeń** kliknij przycisk **Konfigurowanie rejestracji jednokrotnej (SSO).**</span><span class="sxs-lookup"><span data-stu-id="08ae4-188">On hello **Security** page, click **Set up single sign-on (SSO).**</span></span>
   
    ![Kliknij przycisk logowania jednokrotnego.][11]

10. <span data-ttu-id="08ae4-190">Wykonaj hello następujące zmiany w konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="08ae4-190">Perform hello following configuration changes:</span></span>
   
    ![Konfigurowanie logowania jednokrotnego][12]
   
    <span data-ttu-id="08ae4-192">a.</span><span class="sxs-lookup"><span data-stu-id="08ae4-192">a.</span></span> <span data-ttu-id="08ae4-193">Wybierz **Instalatora Usługa rejestracji Jednokrotnej z dostawcy tożsamości innych firm**.</span><span class="sxs-lookup"><span data-stu-id="08ae4-193">Select **Setup SSO with third-party identity provider**.</span></span>

    <span data-ttu-id="08ae4-194">b.</span><span class="sxs-lookup"><span data-stu-id="08ae4-194">b.</span></span> <span data-ttu-id="08ae4-195">W **adres URL logowania strony** pola w usługi Google Apps, Wklej wartość hello **pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="08ae4-195">In the **Sign-in page URL** field in Google Apps, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="08ae4-196">c.</span><span class="sxs-lookup"><span data-stu-id="08ae4-196">c.</span></span> <span data-ttu-id="08ae4-197">W hello **adres URL strony wylogowania** pola w usługi Google Apps, Wklej wartość hello **Sign-Out adres URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="08ae4-197">In hello **Sign-out page URL** field in Google Apps, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="08ae4-198">d.</span><span class="sxs-lookup"><span data-stu-id="08ae4-198">d.</span></span> <span data-ttu-id="08ae4-199">W hello **zmienić adres URL hasła** pola w usługi Google Apps, Wklej wartość hello **zmienić adres URL hasła**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="08ae4-199">In hello **Change password URL** field in Google Apps, paste hello value of **Change password URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="08ae4-200">e.</span><span class="sxs-lookup"><span data-stu-id="08ae4-200">e.</span></span> <span data-ttu-id="08ae4-201">W usłudze Google Apps dla hello **certyfikatu weryfikacji**, Przekaż hello certyfikatu, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="08ae4-201">In Google Apps, for hello **Verification certificate**, upload hello certificate that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="08ae4-202">f.</span><span class="sxs-lookup"><span data-stu-id="08ae4-202">f.</span></span> <span data-ttu-id="08ae4-203">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="08ae4-203">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="08ae4-204">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="08ae4-204">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="08ae4-205">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="08ae4-205">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="08ae4-206">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="08ae4-206">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="08ae4-207">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="08ae4-207">Creating an Azure AD test user</span></span>
<span data-ttu-id="08ae4-208">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="08ae4-208">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="08ae4-210">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="08ae4-210">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="08ae4-211">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="08ae4-211">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="08ae4-213">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="08ae4-213">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="08ae4-215">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="08ae4-215">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="08ae4-217">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="08ae4-217">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="08ae4-219">a.</span><span class="sxs-lookup"><span data-stu-id="08ae4-219">a.</span></span> <span data-ttu-id="08ae4-220">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="08ae4-220">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="08ae4-221">b.</span><span class="sxs-lookup"><span data-stu-id="08ae4-221">b.</span></span> <span data-ttu-id="08ae4-222">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="08ae4-222">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="08ae4-223">c.</span><span class="sxs-lookup"><span data-stu-id="08ae4-223">c.</span></span> <span data-ttu-id="08ae4-224">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="08ae4-224">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="08ae4-225">d.</span><span class="sxs-lookup"><span data-stu-id="08ae4-225">d.</span></span> <span data-ttu-id="08ae4-226">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="08ae4-226">Click **Create**.</span></span>
 
### <a name="creating-a-google-apps-test-user"></a><span data-ttu-id="08ae4-227">Tworzenie użytkownika testowego usługi Google Apps</span><span class="sxs-lookup"><span data-stu-id="08ae4-227">Creating a Google Apps test user</span></span>

<span data-ttu-id="08ae4-228">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Google Apps oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="08ae4-228">hello objective of this section is toocreate a user called Britta Simon in Google Apps Software.</span></span> <span data-ttu-id="08ae4-229">Usługi Google Apps obsługuje automatyczne Inicjowanie obsługi, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="08ae4-229">Google Apps supports auto provisioning, which is by default enabled.</span></span> <span data-ttu-id="08ae4-230">Brak akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="08ae4-230">There is no action for you in this section.</span></span> <span data-ttu-id="08ae4-231">Jeśli użytkownik nie istnieje w oprogramowaniu do aplikacji Google, nowy jest tworzony podczas próby tooaccess Google Apps oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="08ae4-231">If a user doesn't already exist in Google Apps Software, a new one is created when you attempt tooaccess Google Apps Software.</span></span>

>[!NOTE] 
><span data-ttu-id="08ae4-232">Toocreate użytkownik ręcznie, należy skontaktować się z hello [zespołem pomocy technicznej usługi Google](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="08ae4-232">If you need toocreate a user manually, contact hello [Google support team](https://www.google.com/contact/).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="08ae4-233">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="08ae4-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="08ae4-234">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooGoogle aplikacji.</span><span class="sxs-lookup"><span data-stu-id="08ae4-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGoogle Apps.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="08ae4-236">**tooassign Simona Britta tooGoogle aplikacji, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="08ae4-236">**tooassign Britta Simon tooGoogle Apps, perform hello following steps:**</span></span>

1. <span data-ttu-id="08ae4-237">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="08ae4-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="08ae4-239">Z listy aplikacji hello wybierz **usługi Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="08ae4-239">In hello applications list, select **Google Apps**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. <span data-ttu-id="08ae4-241">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="08ae4-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="08ae4-243">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="08ae4-243">Click **Add** button.</span></span> <span data-ttu-id="08ae4-244">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="08ae4-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="08ae4-246">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="08ae4-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="08ae4-247">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="08ae4-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="08ae4-248">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="08ae4-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="08ae4-249">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="08ae4-249">Testing single sign-on</span></span>

<span data-ttu-id="08ae4-250">W tej sekcji tootest pojedynczego logowania jednokrotnego ustawienia, otwórz hello panelu dostępu pod adresem [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), następnie zaloguj się do konta testowego hello i kliknij przycisk **usługi Google Apps** kafelka w hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="08ae4-250">In this section, tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), then sign into hello test account, and click **Google Apps** tile in hello Access Panel.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="08ae4-251">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="08ae4-251">Additional resources</span></span>

* [<span data-ttu-id="08ae4-252">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="08ae4-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="08ae4-253">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="08ae4-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="08ae4-254">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="08ae4-254">Configure User Provisioning</span></span>](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png