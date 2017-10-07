---
title: 'Samouczek: Integracji Azure Active Directory z SuccessFactors | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak toouse SuccessFactors z usługą Azure Active Directory tooenable pojedynczy logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 3f7895d7d5e26fda27f555ae2f14a1645b50dcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a><span data-ttu-id="c84bc-103">Samouczek: Integracji Azure Active Directory z SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="c84bc-103">Tutorial: Azure Active Directory integration with SuccessFactors</span></span>
<span data-ttu-id="c84bc-104">Celem Hello tego samouczka jest tooshow należy jak toointegrate SuccessFactors w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c84bc-104">hello objective of this tutorial is tooshow you how toointegrate SuccessFactors with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c84bc-105">Integracja z usługą Azure AD SuccessFactors zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="c84bc-105">Integrating SuccessFactors with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="c84bc-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooSuccessFactors</span><span class="sxs-lookup"><span data-stu-id="c84bc-106">You can control in Azure AD who has access tooSuccessFactors</span></span>
* <span data-ttu-id="c84bc-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSuccessFactors (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c84bc-107">You can enable your users tooautomatically get signed-on tooSuccessFactors (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="c84bc-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c84bc-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="c84bc-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c84bc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c84bc-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c84bc-110">Prerequisites</span></span>
<span data-ttu-id="c84bc-111">tooconfigure integracji z usługą Azure AD z SuccessFactors należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="c84bc-111">tooconfigure Azure AD integration with SuccessFactors, you need hello following items:</span></span>

* <span data-ttu-id="c84bc-112">Ważnej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c84bc-112">A valid Azure subscription</span></span>
* <span data-ttu-id="c84bc-113">Dzierżawcy w SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="c84bc-113">A tenant in SuccessFactors</span></span>

> [!NOTE]
> <span data-ttu-id="c84bc-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="c84bc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="c84bc-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="c84bc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="c84bc-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="c84bc-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="c84bc-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c84bc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c84bc-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="c84bc-118">Scenario description</span></span>
<span data-ttu-id="c84bc-119">Celem Hello tego samouczka jest tooenable możesz tootest usługi Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="c84bc-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="c84bc-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="c84bc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c84bc-121">Dodawanie SuccessFactors z galerii hello</span><span class="sxs-lookup"><span data-stu-id="c84bc-121">Adding SuccessFactors from hello gallery</span></span>
2. <span data-ttu-id="c84bc-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c84bc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-successfactors-from-hello-gallery"></a><span data-ttu-id="c84bc-123">Dodawanie SuccessFactors z galerii hello</span><span class="sxs-lookup"><span data-stu-id="c84bc-123">Adding SuccessFactors from hello gallery</span></span>
<span data-ttu-id="c84bc-124">tooconfigure hello integracji SuccessFactors do usługi Azure AD, należy tooadd SuccessFactors z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="c84bc-124">tooconfigure hello integration of SuccessFactors into Azure AD, you need tooadd SuccessFactors from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c84bc-125">**tooadd SuccessFactors z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c84bc-125">**tooadd SuccessFactors from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c84bc-126">W hello klasycznego portalu Azure, na panelu nawigacyjnym po lewej stronie powitania kliknij **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-126">In hello Azure classic portal, on hello left navigation panel, click **Active Directory**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][1]
2. <span data-ttu-id="c84bc-128">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="c84bc-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="c84bc-129">Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="c84bc-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][2]
4. <span data-ttu-id="c84bc-131">Kliknij przycisk **Dodaj** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="c84bc-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Aplikacje][3]
5. <span data-ttu-id="c84bc-133">Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][4]
6. <span data-ttu-id="c84bc-135">W hello **pole wyszukiwania**, typ **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-135">In hello **search box**, type **SuccessFactors**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][5]
7. <span data-ttu-id="c84bc-137">W panelu wyników hello, wybierz **SuccessFactors**, a następnie kliknij przycisk **Complete** tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c84bc-137">In hello results panel, select **SuccessFactors**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c84bc-139">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="c84bc-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c84bc-140">Celem Hello w tej sekcji jest tooshow użytkownika jak tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z SuccessFactors na podstawie użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="c84bc-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with SuccessFactors based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c84bc-141">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow jest odpowiednikiem hello użytkownika w SuccessFactors tooan użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c84bc-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SuccessFactors tooan user in Azure AD is.</span></span> <span data-ttu-id="c84bc-142">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w SuccessFactors musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="c84bc-142">In other words, a link relationship between an Azure AD user and hello related user in SuccessFactors needs toobe established.</span></span>

<span data-ttu-id="c84bc-143">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="c84bc-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SuccessFactors.</span></span>

<span data-ttu-id="c84bc-144">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z SuccessFactors, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="c84bc-144">tooconfigure and test Azure AD single sign-on with SuccessFactors, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c84bc-145">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="c84bc-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c84bc-146">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c84bc-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c84bc-147">**[Tworzenie użytkownika testowego SuccessFactors](#creating-a-successfactors-test-user)**  -toohave odpowiednikiem Simona Britta w SuccessFactors, że jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c84bc-147">**[Creating a SuccessFactors test user](#creating-a-successfactors-test-user)** - toohave a counterpart of Britta Simon in SuccessFactors that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="c84bc-148">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="c84bc-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c84bc-149">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="c84bc-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c84bc-150">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c84bc-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="c84bc-151">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu klasycznym hello i skonfigurować logowanie jednokrotne w aplikacji SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="c84bc-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your SuccessFactors application.</span></span>

<span data-ttu-id="c84bc-152">**tooconfigure usługi Azure AD rejestracji jednokrotnej z SuccessFactors, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c84bc-152">**tooconfigure Azure AD single sign-on with SuccessFactors, perform hello following steps:**</span></span>

1. <span data-ttu-id="c84bc-153">W hello klasycznego portalu Azure na powitania **SuccessFactors** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować rejestrację jednokrotną** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="c84bc-153">In hello Azure classic portal, on hello **SuccessFactors** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][7]
2. <span data-ttu-id="c84bc-155">Na powitania **jak ma toosign użytkowników na tooSuccessFactors** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-155">On hello **How would you like users toosign on tooSuccessFactors** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][8]
3. <span data-ttu-id="c84bc-157">Na powitania **Konfigurowanie adresu URL aplikacji** , wykonaj następujące kroki hello, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-157">On hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][9]
   
    <span data-ttu-id="c84bc-159">a.</span><span class="sxs-lookup"><span data-stu-id="c84bc-159">a.</span></span> <span data-ttu-id="c84bc-160">W hello **na adres URL logowania** tekstowym, wpisz adres URL przy użyciu jednej z powitania po wzorców:</span><span class="sxs-lookup"><span data-stu-id="c84bc-160">In hello **Sign On URL** textbox, type a URL using one of hello following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    <span data-ttu-id="c84bc-161">b.</span><span class="sxs-lookup"><span data-stu-id="c84bc-161">b.</span></span> <span data-ttu-id="c84bc-162">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL przy użyciu jednej z powitania po wzorców:</span><span class="sxs-lookup"><span data-stu-id="c84bc-162">In hello **Reply URL** textbox, type a URL using one of hello following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    <span data-ttu-id="c84bc-163">c.</span><span class="sxs-lookup"><span data-stu-id="c84bc-163">c.</span></span> <span data-ttu-id="c84bc-164">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-164">Click **Next**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="c84bc-165">Należy pamiętać, że nie są one hello wartości rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="c84bc-165">Please note that these are not hello real values.</span></span> <span data-ttu-id="c84bc-166">Masz tooupdate tych wartości za pomocą hello rzeczywiste na adres URL logowania i odpowiedzi adresu URL.</span><span class="sxs-lookup"><span data-stu-id="c84bc-166">You have tooupdate these values with hello actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="c84bc-167">Skontaktuj się z tych wartości, tooget [SuccessFactors obsługuje zespołu](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="c84bc-167">tooget these values, contact [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

1. <span data-ttu-id="c84bc-168">Na powitania **skonfigurować logowanie jednokrotne w SuccessFactors** kliknij przycisk **pobierania certyfikatu**, a następnie zapisz plik certyfikatu hello lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="c84bc-168">On hello **Configure single sign-on at SuccessFactors** page, click **Download certificate**, and then save hello certificate file locally on your computer.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][10]

2. <span data-ttu-id="c84bc-170">W oknie przeglądarki innej witryny sieci web, zaloguj się do Twojego **portalu administracyjnego SuccessFactors** jako administrator.</span><span class="sxs-lookup"><span data-stu-id="c84bc-170">In a different web browser window, log into your **SuccessFactors admin portal** as an administrator.</span></span>

3. <span data-ttu-id="c84bc-171">Odwiedź stronę **zabezpieczeń aplikacji** i natywne zbyt**pojedynczy znak w funkcji**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-171">Visit **Application Security** and native too**Single Sign On Feature**.</span></span> 

4. <span data-ttu-id="c84bc-172">Umieść wszystkie wartości w hello **zresetować tokenu** i kliknij przycisk **zapisać tokenu** tooenable logowania jednokrotnego SAML.</span><span class="sxs-lookup"><span data-stu-id="c84bc-172">Place any value in hello **Reset Token** and click **Save Token** tooenable SAML SSO.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji][11]

    > [!NOTE] 
    > <span data-ttu-id="c84bc-174">Ta wartość jest używana tylko jako hello wyłącznik.</span><span class="sxs-lookup"><span data-stu-id="c84bc-174">This value is just used as hello on/off switch.</span></span> <span data-ttu-id="c84bc-175">Po zapisaniu wartości hello logowania jednokrotnego SAML jest włączone.</span><span class="sxs-lookup"><span data-stu-id="c84bc-175">If any value is saved, hello SAML SSO is ON.</span></span> <span data-ttu-id="c84bc-176">Po zapisaniu pustego hello logowania jednokrotnego SAML został WYŁĄCZONY.</span><span class="sxs-lookup"><span data-stu-id="c84bc-176">If a blank value is saved hello SAML SSO is OFF.</span></span>

1. <span data-ttu-id="c84bc-177">Zrzut ekranu toobelow macierzystego i wykonaj następujące akcje hello.</span><span class="sxs-lookup"><span data-stu-id="c84bc-177">Native toobelow screenshot and perform hello following actions.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji][12]
   
    <span data-ttu-id="c84bc-179">a.</span><span class="sxs-lookup"><span data-stu-id="c84bc-179">a.</span></span> <span data-ttu-id="c84bc-180">Wybierz hello **logowania jednokrotnego SAML v2** przycisku radiowego</span><span class="sxs-lookup"><span data-stu-id="c84bc-180">Select hello **SAML v2 SSO** Radio Button</span></span>
   
    <span data-ttu-id="c84bc-181">b.</span><span class="sxs-lookup"><span data-stu-id="c84bc-181">b.</span></span> <span data-ttu-id="c84bc-182">Ustaw hello Name(e.g. SAml issuer + company name) strona zostanie SAML.</span><span class="sxs-lookup"><span data-stu-id="c84bc-182">Set hello SAML Asserting Party Name(e.g. SAml issuer + company name).</span></span>
   
    <span data-ttu-id="c84bc-183">c.</span><span class="sxs-lookup"><span data-stu-id="c84bc-183">c.</span></span> <span data-ttu-id="c84bc-184">W hello **wystawcy SAML** pole tekstowe umieścić wartość hello **adres URL wystawcy** z Kreatora konfiguracji aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c84bc-184">In hello **SAML Issuer** textbox put hello value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="c84bc-185">d.</span><span class="sxs-lookup"><span data-stu-id="c84bc-185">d.</span></span> <span data-ttu-id="c84bc-186">Wybierz **odpowiedzi (odbiorcy wygenerowanych/IdP/AP)** jako **wymagają podpisu obowiązkowe**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-186">Select **Response(Customer Generated/IdP/AP)** as **Require Mandatory Signature**.</span></span>
   
    <span data-ttu-id="c84bc-187">e.</span><span class="sxs-lookup"><span data-stu-id="c84bc-187">e.</span></span> <span data-ttu-id="c84bc-188">Wybierz **włączone** jako **Włącz flagę SAML**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-188">Select **Enabled** as **Enable SAML Flag**.</span></span>
   
    <span data-ttu-id="c84bc-189">f.</span><span class="sxs-lookup"><span data-stu-id="c84bc-189">f.</span></span> <span data-ttu-id="c84bc-190">Wybierz **nr** jako **podpisu żądania logowania (rz wygenerowanych/SP/RP)**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-190">Select **No** as **Login Request Signature(SF Generated/SP/RP)**.</span></span>
   
    <span data-ttu-id="c84bc-191">g.</span><span class="sxs-lookup"><span data-stu-id="c84bc-191">g.</span></span> <span data-ttu-id="c84bc-192">Wybierz **profilu przeglądarki lub używanego po** jako **profilu SAML**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-192">Select **Browser/Post Profile** as **SAML Profile**.</span></span>
   
    <span data-ttu-id="c84bc-193">h.</span><span class="sxs-lookup"><span data-stu-id="c84bc-193">h.</span></span> <span data-ttu-id="c84bc-194">Wybierz **nr** jako **wymusić nieprawidłowy okres certyfikatu**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-194">Select **No** as **Enforce Certificate Valid Period**.</span></span>
   
    <span data-ttu-id="c84bc-195">i.</span><span class="sxs-lookup"><span data-stu-id="c84bc-195">i.</span></span> <span data-ttu-id="c84bc-196">Kopiowanie zawartości hello hello pliku pobranego certyfikatu, a następnie wklej go do hello **certyfikatu weryfikacji SAML** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="c84bc-196">Copy hello content of hello downloaded certificate file, and then paste it into hello **SAML Verifying Certificate** textbox.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c84bc-197">zawartość certyfikatu Hello musi mieć rozpocząć certyfikatu i na końcu tagi certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="c84bc-197">hello certificate content must have begin certificate and end certificate tags.</span></span>

1. <span data-ttu-id="c84bc-198">Przejdź tooSAML V2, a następnie wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="c84bc-198">Navigate tooSAML V2, and then perform hello following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji][13]
   
    <span data-ttu-id="c84bc-200">a.</span><span class="sxs-lookup"><span data-stu-id="c84bc-200">a.</span></span> <span data-ttu-id="c84bc-201">Wybierz **tak** jako **inicjowane SP wylogowania globalnego obsługują**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-201">Select **Yes** as **Support SP-initiated Global Logout**.</span></span>
   
    <span data-ttu-id="c84bc-202">b.</span><span class="sxs-lookup"><span data-stu-id="c84bc-202">b.</span></span> <span data-ttu-id="c84bc-203">W hello **globalne wylogowania adres URL usługi (LogoutRequest docelowy)** pole tekstowe umieścić wartość hello **zdalnego adresu URL wylogowania** z Kreatora konfiguracji aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c84bc-203">In hello **Global Logout Service URL (LogoutRequest destination)** textbox put hello value of **Remote Logout URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="c84bc-204">c.</span><span class="sxs-lookup"><span data-stu-id="c84bc-204">c.</span></span> <span data-ttu-id="c84bc-205">Wybierz **nr** jako **wymagają sp należy szyfrować wszystkie element NameID**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-205">Select **No** as **Require sp must encrypt all NameID element**.</span></span>
   
    <span data-ttu-id="c84bc-206">d.</span><span class="sxs-lookup"><span data-stu-id="c84bc-206">d.</span></span> <span data-ttu-id="c84bc-207">Wybierz **nieokreślony** jako **NameID Format**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-207">Select **unspecified** as **NameID Format**.</span></span>
   
    <span data-ttu-id="c84bc-208">e.</span><span class="sxs-lookup"><span data-stu-id="c84bc-208">e.</span></span> <span data-ttu-id="c84bc-209">Wybierz **tak** jako **Włącz sp zainicjował logowania (AuthnRequest)**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-209">Select **Yes** as **Enable sp initiated login (AuthnRequest)**.</span></span>
   
    <span data-ttu-id="c84bc-210">f.</span><span class="sxs-lookup"><span data-stu-id="c84bc-210">f.</span></span> <span data-ttu-id="c84bc-211">W hello **żądanie wysłania jako wystawca firmie** pole tekstowe umieścić wartość hello **zdalnego adresu URL logowania** z Kreatora konfiguracji aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c84bc-211">In hello **Send request as Company-Wide issuer** textbox put hello value of **Remote Login URL** from Azure AD application configuration wizard.</span></span>
2. <span data-ttu-id="c84bc-212">Wykonaj następujące kroki, jeśli chcesz, aby toomake hello logowania użytkowników bez uwzględniania wielkości liter,.</span><span class="sxs-lookup"><span data-stu-id="c84bc-212">Perform these steps if you want toomake hello login usernames Case Insensitive, .</span></span>
   
    <span data-ttu-id="c84bc-213">a.</span><span class="sxs-lookup"><span data-stu-id="c84bc-213">a.</span></span> <span data-ttu-id="c84bc-214">Odwiedź stronę **ustawienia firmy**(dolnej hello).</span><span class="sxs-lookup"><span data-stu-id="c84bc-214">Visit **Company Settings**(near hello bottom).</span></span>
   
    <span data-ttu-id="c84bc-215">b.</span><span class="sxs-lookup"><span data-stu-id="c84bc-215">b.</span></span> <span data-ttu-id="c84bc-216">Zaznacz pole wyboru obok **włączyć Username Non-uwzględniana wielkość liter**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-216">select checkbox near **Enable Non-Case-Sensitive Username**.</span></span>
   
    <span data-ttu-id="c84bc-217">c.Click **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-217">c.Click **Save**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][29]

    > [!NOTE] 
    > <span data-ttu-id="c84bc-219">Jeśli spróbujesz tooenable to, hello system sprawdza, czy spowoduje utworzenie zduplikowanej nazwy logowania SAML.</span><span class="sxs-lookup"><span data-stu-id="c84bc-219">If you try tooenable this, hello system checks if it will create a duplicate SAML login name.</span></span> <span data-ttu-id="c84bc-220">Na przykład nazwy użytkowników Użytkownik1 i Użytkownik1 ma powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="c84bc-220">For example if hello customer has usernames User1 and user1.</span></span> <span data-ttu-id="c84bc-221">Zdjęciu uwzględniana wielkość liter powoduje, że te duplikaty.</span><span class="sxs-lookup"><span data-stu-id="c84bc-221">Taking away case sensitivity makes these duplicates.</span></span> <span data-ttu-id="c84bc-222">Hello system otrzymasz komunikat o błędzie i nie dają hello funkcji.</span><span class="sxs-lookup"><span data-stu-id="c84bc-222">hello system will give you an error message and will not enable hello feature.</span></span> <span data-ttu-id="c84bc-223">powitania klienta należy toochange jedną z nazw użytkowników hello tak faktycznie Pisownia jest inny.</span><span class="sxs-lookup"><span data-stu-id="c84bc-223">hello customer will need toochange one of hello usernames so it’s actually spelled different.</span></span> 

1. <span data-ttu-id="c84bc-224">Na powitania klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **Complete** tooclose hello **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="c84bc-224">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    ![Aplikacje][14]
2. <span data-ttu-id="c84bc-226">Na powitania **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-226">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    ![Aplikacje][15]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c84bc-228">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="c84bc-228">Creating an Azure AD test user</span></span>
<span data-ttu-id="c84bc-229">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu klasycznym hello o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="c84bc-229">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][16]

<span data-ttu-id="c84bc-231">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="c84bc-231">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c84bc-232">W hello **klasycznego portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-232">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD][17]
2. <span data-ttu-id="c84bc-234">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="c84bc-234">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="c84bc-235">Kliknij toodisplay hello listę użytkowników, w menu hello na górze hello **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-235">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD][18]
4. <span data-ttu-id="c84bc-237">Witaj tooopen **Dodaj użytkownika** kliknij okno dialogowe narzędzi hello na dole hello **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-237">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD][19]
5. <span data-ttu-id="c84bc-239">Na powitania **Poinformuj nas o tym użytkowniku** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c84bc-239">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD][20]
   
    <span data-ttu-id="c84bc-241">a.</span><span class="sxs-lookup"><span data-stu-id="c84bc-241">a.</span></span> <span data-ttu-id="c84bc-242">Jako typ użytkownika wybierz nowego użytkownika w organizacji.</span><span class="sxs-lookup"><span data-stu-id="c84bc-242">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="c84bc-243">b.</span><span class="sxs-lookup"><span data-stu-id="c84bc-243">b.</span></span> <span data-ttu-id="c84bc-244">W hello nazwy użytkownika **pole tekstowe**, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-244">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="c84bc-245">c.</span><span class="sxs-lookup"><span data-stu-id="c84bc-245">c.</span></span> <span data-ttu-id="c84bc-246">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-246">Click **Next**.</span></span>
6. <span data-ttu-id="c84bc-247">Na powitania **profilu użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c84bc-247">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD][21]
   
    <span data-ttu-id="c84bc-249">a.</span><span class="sxs-lookup"><span data-stu-id="c84bc-249">a.</span></span> <span data-ttu-id="c84bc-250">W hello **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-250">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="c84bc-251">b.</span><span class="sxs-lookup"><span data-stu-id="c84bc-251">b.</span></span> <span data-ttu-id="c84bc-252">W hello **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-252">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="c84bc-253">c.</span><span class="sxs-lookup"><span data-stu-id="c84bc-253">c.</span></span> <span data-ttu-id="c84bc-254">W hello **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-254">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="c84bc-255">d.</span><span class="sxs-lookup"><span data-stu-id="c84bc-255">d.</span></span> <span data-ttu-id="c84bc-256">W hello **roli** listy, wybierz **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-256">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="c84bc-257">e.</span><span class="sxs-lookup"><span data-stu-id="c84bc-257">e.</span></span> <span data-ttu-id="c84bc-258">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-258">Click **Next**.</span></span>
7. <span data-ttu-id="c84bc-259">Na powitania **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-259">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD][22]
8. <span data-ttu-id="c84bc-261">Na powitania **Uzyskaj hasło tymczasowe** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c84bc-261">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD][23]
   
    <span data-ttu-id="c84bc-263">a.</span><span class="sxs-lookup"><span data-stu-id="c84bc-263">a.</span></span> <span data-ttu-id="c84bc-264">Zanotuj wartość hello hello **nowe hasło**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-264">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="c84bc-265">b.</span><span class="sxs-lookup"><span data-stu-id="c84bc-265">b.</span></span> <span data-ttu-id="c84bc-266">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="c84bc-266">Click **Complete**.</span></span>  

### <a name="creating-a-successfactors-test-user"></a><span data-ttu-id="c84bc-267">Tworzenie użytkownika testowego SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="c84bc-267">Creating a SuccessFactors test user</span></span>
<span data-ttu-id="c84bc-268">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do SuccessFactors muszą mieć przydzielone do SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="c84bc-268">In order tooenable Azure AD users toolog into SuccessFactors, they must be provisioned into SuccessFactors.</span></span>  
<span data-ttu-id="c84bc-269">W przypadku hello SuccessFactors Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="c84bc-269">In hello case of SuccessFactors, provisioning is a manual task.</span></span>

<span data-ttu-id="c84bc-270">Użytkownicy tooget utworzone w SuccessFactors, potrzebujesz toocontact hello [SuccessFactors obsługuje zespołu](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="c84bc-270">tooget users created in SuccessFactors, you need toocontact hello [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c84bc-271">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c84bc-271">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="c84bc-272">Celem Hello w tej sekcji jest tooenabling toouse Simona Britta Azure rejestracji jednokrotnej, przyznając jej tooSuccessFactors dostępu.</span><span class="sxs-lookup"><span data-stu-id="c84bc-272">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSuccessFactors.</span></span>

![Przypisz użytkownika][24]

<span data-ttu-id="c84bc-274">**tooassign tooSuccessFactors Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="c84bc-274">**tooassign Britta Simon tooSuccessFactors, perform hello following steps:**</span></span>

1. <span data-ttu-id="c84bc-275">W portalu klasycznym hello, kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="c84bc-275">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Przypisz użytkownika][25]
2. <span data-ttu-id="c84bc-277">Z listy aplikacji hello wybierz **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-277">In hello applications list, select **SuccessFactors**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][26]
3. <span data-ttu-id="c84bc-279">W menu hello na górze hello, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-279">In hello menu on hello top, click **Users**.</span></span>
   
    ![Przypisz użytkownika][27]
4. <span data-ttu-id="c84bc-281">Na liście hello użytkowników, wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-281">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="c84bc-282">W narzędzi hello na dole powitania kliknij **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="c84bc-282">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Przypisz użytkownika][28]

### <a name="testing-single-sign-on"></a><span data-ttu-id="c84bc-284">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="c84bc-284">Testing single sign-on</span></span>
<span data-ttu-id="c84bc-285">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="c84bc-285">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c84bc-286">Po kliknięciu powitalne SuccessFactors kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour SuccessFactors aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c84bc-286">When you click hello SuccessFactors tile in hello Access Panel, you should get automatically signed-on tooyour SuccessFactors application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c84bc-287">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="c84bc-287">Additional resources</span></span>
* [<span data-ttu-id="c84bc-288">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c84bc-288">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c84bc-289">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c84bc-289">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
