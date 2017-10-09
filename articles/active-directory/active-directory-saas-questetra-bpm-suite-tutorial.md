---
title: 'Samouczek: Azure Active Directory integracji z pakietem BPM Questetra | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Questetra BPM Suite."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 4907e3b5751cd79f994fbd2ebcb7faec4eac34e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a><span data-ttu-id="a99fb-103">Samouczek: Azure Active Directory integracji z pakietem BPM Questetra</span><span class="sxs-lookup"><span data-stu-id="a99fb-103">Tutorial: Azure Active Directory integration with Questetra BPM Suite</span></span>
<span data-ttu-id="a99fb-104">Celem Hello tego samouczka jest tooshow należy jak toointegrate Suite BPM Questetra w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a99fb-104">hello objective of this tutorial is tooshow you how toointegrate Questetra BPM Suite with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="a99fb-105">Integracja z usługą Azure AD Questetra BPM Suite udostępnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="a99fb-105">Integrating Questetra BPM Suite with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="a99fb-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooQuestetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="a99fb-106">You can control in Azure AD who has access tooQuestetra BPM Suite</span></span> 
* <span data-ttu-id="a99fb-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooQuestetra Suite BPM (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a99fb-107">You can enable your users tooautomatically get signed-on tooQuestetra BPM Suite (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="a99fb-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a99fb-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="a99fb-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a99fb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a99fb-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a99fb-110">Prerequisites</span></span>
<span data-ttu-id="a99fb-111">tooconfigure integracji usługi Azure AD z pakietem BPM Questetra należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a99fb-111">tooconfigure Azure AD integration with Questetra BPM Suite, you need hello following items:</span></span>

* <span data-ttu-id="a99fb-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a99fb-112">An Azure AD subscription</span></span>
* <span data-ttu-id="a99fb-113">[Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="a99fb-113">An [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a99fb-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="a99fb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="a99fb-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="a99fb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="a99fb-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="a99fb-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="a99fb-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a99fb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="a99fb-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="a99fb-118">Scenario Description</span></span>
<span data-ttu-id="a99fb-119">Celem Hello tego samouczka jest tooenable możesz tootest usługi Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="a99fb-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="a99fb-120">Scenariusz Hello opisane w tym samouczku składa się z trzech głównych bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="a99fb-120">hello scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="a99fb-121">Dodawanie pakietu BPM Questetra z galerii hello</span><span class="sxs-lookup"><span data-stu-id="a99fb-121">Adding Questetra BPM Suite from hello gallery</span></span> 
2. <span data-ttu-id="a99fb-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a99fb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-questetra-bpm-suite-from-hello-gallery"></a><span data-ttu-id="a99fb-123">Dodawanie pakietu BPM Questetra z galerii hello</span><span class="sxs-lookup"><span data-stu-id="a99fb-123">Adding Questetra BPM Suite from hello gallery</span></span>
<span data-ttu-id="a99fb-124">tooconfigure hello integracji pakietu BPM Questetra do usługi Azure AD, należy tooadd Questetra BPM pakiet z listy tooyour galerii hello zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="a99fb-124">tooconfigure hello integration of Questetra BPM Suite into Azure AD, you need tooadd Questetra BPM Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a99fb-125">**tooadd Questetra BPM pakiet z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="a99fb-125">**tooadd Questetra BPM Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a99fb-126">W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Usługa Active Directory][1]

2. <span data-ttu-id="a99fb-128">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="a99fb-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="a99fb-129">Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="a99fb-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Aplikacje][2]

4. <span data-ttu-id="a99fb-131">Kliknij przycisk **Dodaj** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="a99fb-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplikacje][3]

5. <span data-ttu-id="a99fb-133">Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Aplikacje][4]

6. <span data-ttu-id="a99fb-135">W polu wyszukiwania hello wpisz **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-135">In hello search box, type **Questetra BPM Suite**.</span></span>
   
    ![Aplikacje][5]

7. <span data-ttu-id="a99fb-137">W okienku wyników hello, wybierz **Questetra BPM Suite**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="a99fb-137">In hello results pane, select **Questetra BPM Suite**, and then click **Complete** tooadd hello application.</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a99fb-138">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="a99fb-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a99fb-139">Celem Hello w tej sekcji jest tooshow użytkownika jak tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z pakietem BPM Questetra na podstawie użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="a99fb-139">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with Questetra BPM Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a99fb-140">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow jest odpowiednikiem hello użytkownika w pakiet BPM Questetra tooan użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a99fb-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Questetra BPM Suite tooan user in Azure AD is.</span></span> <span data-ttu-id="a99fb-141">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi pakietu BPM Questetra musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="a99fb-141">In other words, a link relationship between an Azure AD user and hello related user in Questetra BPM Suite needs toobe established.</span></span>  
<span data-ttu-id="a99fb-142">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** pakietu BPM Questetra.</span><span class="sxs-lookup"><span data-stu-id="a99fb-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Questetra BPM Suite.</span></span>

<span data-ttu-id="a99fb-143">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z pakietem BPM Questetra, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="a99fb-143">tooconfigure and test Azure AD single sign-on with Questetra BPM Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a99fb-144">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="a99fb-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a99fb-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a99fb-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a99fb-146">**[Tworzenie użytkownika testowego zestawu BPM Questetra](#creating-a-questetra-bpm-suite-test-user)**  -toohave odpowiednikiem Simona Britta pakietu BPM Questetra, że jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a99fb-146">**[Creating a Questetra BPM Suite test user](#creating-a-questetra-bpm-suite-test-user)** - toohave a counterpart of Britta Simon in Questetra BPM Suite that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="a99fb-147">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a99fb-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a99fb-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="a99fb-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a99fb-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a99fb-149">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="a99fb-150">Celem Hello w tej sekcji jest tooenable usługi Azure AD rejestracji jednokrotnej w hello klasycznego portalu Azure i tooconfigure rejestracji jednokrotnej w Questetra BPM pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a99fb-150">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your Questetra BPM Suite application.</span></span>

<span data-ttu-id="a99fb-151">**tooconfigure usługi Azure AD rejestracji jednokrotnej z pakietem BPM Questetra, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="a99fb-151">**tooconfigure Azure AD single sign-on with Questetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="a99fb-152">W hello klasycznego portalu Azure na powitania **Questetra BPM Suite** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować logowanie jednokrotne**  okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="a99fb-152">In hello Azure classic portal, on hello **Questetra BPM Suite** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][8]

2. <span data-ttu-id="a99fb-154">Na powitania **jak ma toosign użytkowników na tooQuestetra BPM Suite** wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-154">On hello **How would you like users toosign on tooQuestetra BPM Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD rejestracji jednokrotnej][9]

3. <span data-ttu-id="a99fb-156">W oknie przeglądarki innej witryny sieci web, zaloguj się do Twojego **Questetra BPM Suite** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="a99fb-156">In a different web browser window, log into your **Questetra BPM Suite** company site as an administrator.</span></span>

4. <span data-ttu-id="a99fb-157">W menu hello na górze hello, kliknij przycisk **ustawienia systemu**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-157">In hello menu on hello top, click **System Settings**.</span></span> 
   
    ![Azure AD rejestracji jednokrotnej][10]

5. <span data-ttu-id="a99fb-159">Witaj tooopen **SingleSignOnSAML** kliknij przycisk **logowania jednokrotnego (SAML)**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-159">tooopen hello **SingleSignOnSAML** page, click **SSO (SAML)**.</span></span> 
   
    ![Azure AD rejestracji jednokrotnej][11]

6. <span data-ttu-id="a99fb-161">W hello klasycznego portalu Azure na powitania **Konfigurowanie ustawień aplikacji** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="a99fb-161">In hello Azure classic portal, on hello **Configure App Settings** dialog page, perform hello following steps:</span></span> 
   
    ![Konfiguruj ustawienia aplikacji][13]
   
    <span data-ttu-id="a99fb-163">a.</span><span class="sxs-lookup"><span data-stu-id="a99fb-163">a.</span></span> <span data-ttu-id="a99fb-164">W przypadku **Questetra BPM Suite** witryna firmy, w sekcji informacji SP hello, hello kopiowania **adres URL usługi ACS**, a następnie wklej go do hello **na adres URL logowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a99fb-164">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **ACS URL**, and then paste it into hello **Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="a99fb-165">b.</span><span class="sxs-lookup"><span data-stu-id="a99fb-165">b.</span></span> <span data-ttu-id="a99fb-166">W przypadku **Questetra BPM Suite** witryna firmy, w sekcji informacji SP hello, hello kopiowania **identyfikator jednostki**i wklej go do hello **adres URL wystawcy** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a99fb-166">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **Entity ID**, and then paste it into hello **Issuer URL** textbox.</span></span>
   
    <span data-ttu-id="a99fb-167">c.</span><span class="sxs-lookup"><span data-stu-id="a99fb-167">c.</span></span> <span data-ttu-id="a99fb-168">W przypadku **Questetra BPM Suite** witryna firmy, w sekcji informacji SP hello, hello kopii **adres URL usługi ACS**, a następnie wklej go do hello **adres URL odpowiedzi** pole tekstowe.</span><span class="sxs-lookup"><span data-stu-id="a99fb-168">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **ACS URL**, and then paste it into hello **Reply URL** textbox.</span></span>
   
    <span data-ttu-id="a99fb-169">d.</span><span class="sxs-lookup"><span data-stu-id="a99fb-169">d.</span></span> <span data-ttu-id="a99fb-170">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-170">Click **Next**.</span></span>

7. <span data-ttu-id="a99fb-171">Na powitania **skonfigurować logowanie jednokrotne w pakiet BPM Questetra** kliknij przycisk **pobierania certyfikatu**, a następnie zapisz plik certyfikatu hello lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="a99fb-171">On hello **Configure single sign-on at Questetra BPM Suite** page, click **Download certificate**, and then save hello certificate file locally on your computer.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][14]

8. <span data-ttu-id="a99fb-173">W przypadku **Questetra BPM Suite** firmy, witryny, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="a99fb-173">On you **Questetra BPM Suite** company site, perform hello following steps:</span></span> 
   
    ![Konfigurowanie rejestracji jednokrotnej][15]
   
    <span data-ttu-id="a99fb-175">a.</span><span class="sxs-lookup"><span data-stu-id="a99fb-175">a.</span></span> <span data-ttu-id="a99fb-176">Wybierz **Włącz rejestrację jednokrotną**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-176">Select **Enable Single Sign-On**.</span></span>
   
    <span data-ttu-id="a99fb-177">b.</span><span class="sxs-lookup"><span data-stu-id="a99fb-177">b.</span></span> <span data-ttu-id="a99fb-178">Na powitania klasycznego portalu Azure, skopiuj hello **adres URL wystawcy** wartość, a następnie wklej go do hello **identyfikator jednostki** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a99fb-178">On hello Azure classic portal, copy hello **Issuer URL** value, and then paste it into hello **Entity ID** textbox.</span></span>
   
    <span data-ttu-id="a99fb-179">c.</span><span class="sxs-lookup"><span data-stu-id="a99fb-179">c.</span></span> <span data-ttu-id="a99fb-180">Na powitania klasycznego portalu Azure, skopiuj hello **pojedynczy znak na adres URL usługi** wartość, a następnie wklej go do hello **adres URL logowania strony** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a99fb-180">On hello Azure classic portal, copy hello **Single Sign-On Service URL** value, and then paste it into hello **Sign-in page URL** textbox.</span></span>
   
    <span data-ttu-id="a99fb-181">d.</span><span class="sxs-lookup"><span data-stu-id="a99fb-181">d.</span></span> <span data-ttu-id="a99fb-182">Na powitania klasycznego portalu Azure, skopiuj hello **pojedynczy adres URL usługi Sign-Out** wartość, a następnie wklej go do hello **adres URL strony wylogowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a99fb-182">On hello Azure classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Sign-out page URL** textbox.</span></span>
   
    <span data-ttu-id="a99fb-183">e.</span><span class="sxs-lookup"><span data-stu-id="a99fb-183">e.</span></span> <span data-ttu-id="a99fb-184">W hello **NameID format** pole tekstowe, typ **urn: oasis: nazwy: tc: SAML:1.1:nameid-format: emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-184">In hello **NameID format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="a99fb-185">f.</span><span class="sxs-lookup"><span data-stu-id="a99fb-185">f.</span></span> <span data-ttu-id="a99fb-186">Utwórz plik zakodowany base-64 z pobranego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="a99fb-186">Create a base-64 encoded file from your downloaded certificate.</span></span> 

    >[!TIP] 
    ><span data-ttu-id="a99fb-187">Aby uzyskać więcej informacji, zobacz [jak tooconvert pliku binarnego certyfikatu do pliku tekstowego](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="a99fb-187">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

    <span data-ttu-id="a99fb-188">g.</span><span class="sxs-lookup"><span data-stu-id="a99fb-188">g.</span></span> <span data-ttu-id="a99fb-189">Otwórz certyfikatu zakodowanego base-64 w Notatniku, hello kopiowania zawartości go do Schowka, a następnie wklej go do hello **certyfikatu weryfikacji** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="a99fb-189">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it into hello **Validation certificate** textbox.</span></span> 

    <span data-ttu-id="a99fb-190">h.</span><span class="sxs-lookup"><span data-stu-id="a99fb-190">h.</span></span> <span data-ttu-id="a99fb-191">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-191">Click **Save**.</span></span>

1. <span data-ttu-id="a99fb-192">Na powitania klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-192">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Co to jest program Azure AD Connect][17]

2. <span data-ttu-id="a99fb-194">Na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-194">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Co to jest program Azure AD Connect][18]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a99fb-196">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a99fb-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="a99fb-197">Celem Hello w tej sekcji jest toocreate użytkownika testowego w hello klasycznego portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a99fb-197">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="a99fb-198">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="a99fb-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a99fb-199">W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-199">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD][100] 

2. <span data-ttu-id="a99fb-201">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="a99fb-201">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="a99fb-202">Kliknij toodisplay hello listę użytkowników, w menu hello na górze hello **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-202">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD][101] 

4. <span data-ttu-id="a99fb-204">Witaj tooopen **Dodaj użytkownika** kliknij okno dialogowe narzędzi hello na dole hello **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-204">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD][102] 

5. <span data-ttu-id="a99fb-206">Na powitania **Poinformuj nas o tym użytkowniku** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="a99fb-206">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD][103]
   
    <span data-ttu-id="a99fb-208">a.</span><span class="sxs-lookup"><span data-stu-id="a99fb-208">a.</span></span> <span data-ttu-id="a99fb-209">Jako **typ użytkownika**, wybierz pozycję **nowy użytkownik w organizacji**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-209">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="a99fb-210">b.</span><span class="sxs-lookup"><span data-stu-id="a99fb-210">b.</span></span> <span data-ttu-id="a99fb-211">W hello nazwy użytkownika **pole tekstowe**, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-211">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="a99fb-212">c.</span><span class="sxs-lookup"><span data-stu-id="a99fb-212">c.</span></span> <span data-ttu-id="a99fb-213">Kliknij przycisk Dalej.</span><span class="sxs-lookup"><span data-stu-id="a99fb-213">Click Next.</span></span>

6. <span data-ttu-id="a99fb-214">Na powitania **profilu użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="a99fb-214">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD][104] 
   
    <span data-ttu-id="a99fb-216">a.</span><span class="sxs-lookup"><span data-stu-id="a99fb-216">a.</span></span> <span data-ttu-id="a99fb-217">W hello **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-217">In hello **First Name** textbox, type **Britta**.</span></span> 
   
    <span data-ttu-id="a99fb-218">b.</span><span class="sxs-lookup"><span data-stu-id="a99fb-218">b.</span></span> <span data-ttu-id="a99fb-219">W hello **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-219">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="a99fb-220">c.</span><span class="sxs-lookup"><span data-stu-id="a99fb-220">c.</span></span> <span data-ttu-id="a99fb-221">W hello **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-221">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="a99fb-222">d.</span><span class="sxs-lookup"><span data-stu-id="a99fb-222">d.</span></span> <span data-ttu-id="a99fb-223">W hello **roli** listy, wybierz **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-223">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="a99fb-224">e.</span><span class="sxs-lookup"><span data-stu-id="a99fb-224">e.</span></span> <span data-ttu-id="a99fb-225">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-225">Click **Next**.</span></span>

7. <span data-ttu-id="a99fb-226">Na powitania **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-226">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD][105]  

8. <span data-ttu-id="a99fb-228">Na powitania **Uzyskaj hasło tymczasowe** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="a99fb-228">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD][106]   
   
    <span data-ttu-id="a99fb-230">a.</span><span class="sxs-lookup"><span data-stu-id="a99fb-230">a.</span></span> <span data-ttu-id="a99fb-231">Zanotuj wartość hello hello **nowe hasło**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-231">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="a99fb-232">b.</span><span class="sxs-lookup"><span data-stu-id="a99fb-232">b.</span></span> <span data-ttu-id="a99fb-233">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="a99fb-233">Click **Complete**.</span></span>   

### <a name="creating-a-questetra-bpm-suite-test-user"></a><span data-ttu-id="a99fb-234">Tworzenie użytkownika testowego Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="a99fb-234">Creating a Questetra BPM Suite test user</span></span>
<span data-ttu-id="a99fb-235">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta Questetra BPM pakietu.</span><span class="sxs-lookup"><span data-stu-id="a99fb-235">hello objective of this section is toocreate a user called Britta Simon in Questetra BPM Suite.</span></span>

<span data-ttu-id="a99fb-236">**Użytkownik o nazwie Simona Britta pakietu BPM Questetra toocreate wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="a99fb-236">**toocreate a user called Britta Simon in Questetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="a99fb-237">Logowania jednokrotnego tooyour Questetra BPM Suite witryna firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="a99fb-237">Sign-on tooyour Questetra BPM Suite company site as an administrator.</span></span>
2. <span data-ttu-id="a99fb-238">Przejdź za**ustawienia systemu > listy użytkowników > Nowy użytkownik**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-238">Go too**System Settings > User List > New User**.</span></span> 
3. <span data-ttu-id="a99fb-239">W oknie dialogowym Nowy użytkownik hello wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="a99fb-239">On hello New User dialog, perform hello following steps:</span></span> 
   
    ![Tworzenie użytkownika testowego][300] 
   
    <span data-ttu-id="a99fb-241">a.</span><span class="sxs-lookup"><span data-stu-id="a99fb-241">a.</span></span> <span data-ttu-id="a99fb-242">W hello **nazwa** tekstowym, wpisz nazwę użytkownika w Britta w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a99fb-242">In hello **Name** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="a99fb-243">b.</span><span class="sxs-lookup"><span data-stu-id="a99fb-243">b.</span></span> <span data-ttu-id="a99fb-244">W hello **E-mail** tekstowym, wpisz nazwę użytkownika w Britta w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a99fb-244">In hello **Email** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="a99fb-245">c.</span><span class="sxs-lookup"><span data-stu-id="a99fb-245">c.</span></span> <span data-ttu-id="a99fb-246">W hello **hasło** tekstowym, wpisz hasło.</span><span class="sxs-lookup"><span data-stu-id="a99fb-246">In hello **Password** textbox, type a password.</span></span>

4. <span data-ttu-id="a99fb-247">Kliknij przycisk **Dodaj nowego użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-247">Click **Add new user**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a99fb-248">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a99fb-248">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="a99fb-249">Celem Hello w tej sekcji jest tooenabling toouse Simona Britta Azure rejestracji jednokrotnej, przyznając jej tooQuestetra dostępu BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="a99fb-249">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooQuestetra BPM Suite.</span></span>

![Co to jest program Azure AD Connect][200]

<span data-ttu-id="a99fb-251">**tooassign tooQuestetra Simona Britta BPM Suite wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="a99fb-251">**tooassign Britta Simon tooQuestetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="a99fb-252">Na hello Azure kliknij klasycznego portalu, widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="a99fb-252">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Co to jest program Azure AD Connect][201]
2. <span data-ttu-id="a99fb-254">Z listy aplikacji hello wybierz **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-254">In hello applications list, select **Questetra BPM Suite**.</span></span>
   
    ![Co to jest program Azure AD Connect][205]
3. <span data-ttu-id="a99fb-256">W menu hello na górze hello, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-256">In hello menu on hello top, click **Users**.</span></span>
   
    ![Co to jest program Azure AD Connect][202]
4. <span data-ttu-id="a99fb-258">Na liście hello użytkowników, wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-258">In hello Users list, select **Britta Simon**.</span></span>
   
    ![Co to jest program Azure AD Connect][203]
5. <span data-ttu-id="a99fb-260">W narzędzi hello na dole powitania kliknij **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="a99fb-260">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Co to jest program Azure AD Connect][204]

### <a name="testing-single-sign-on"></a><span data-ttu-id="a99fb-262">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a99fb-262">Testing Single Sign-On</span></span>
<span data-ttu-id="a99fb-263">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a99fb-263">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="a99fb-264">Po kliknięciu kafelka Questetra BPM Suite hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Questetra BPM pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a99fb-264">When you click hello Questetra BPM Suite tile in hello Access Panel, you should get automatically signed-on tooyour Questetra BPM Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a99fb-265">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="a99fb-265">Additional Resources</span></span>
* [<span data-ttu-id="a99fb-266">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a99fb-266">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a99fb-267">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a99fb-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
