---
title: 'Samouczek: Integracji Azure Active Directory z Printix | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Printix."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4aea7320-b2d5-49e0-9b63-aeaff0f6fe66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 654810116091eb52912b377cc97afef803ee816e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-printix"></a><span data-ttu-id="96f3b-103">Samouczek: Integracji Azure Active Directory z Printix</span><span class="sxs-lookup"><span data-stu-id="96f3b-103">Tutorial: Azure Active Directory integration with Printix</span></span>

<span data-ttu-id="96f3b-104">Z tego samouczka, dowiesz się, jak toointegrate Printix w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="96f3b-104">In this tutorial, you learn how toointegrate Printix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="96f3b-105">Integracja z usługą Azure AD Printix zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="96f3b-105">Integrating Printix with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="96f3b-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooPrintix</span><span class="sxs-lookup"><span data-stu-id="96f3b-106">You can control in Azure AD who has access tooPrintix</span></span>
- <span data-ttu-id="96f3b-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooPrintix (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="96f3b-107">You can enable your users tooautomatically get signed-on tooPrintix (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="96f3b-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="96f3b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="96f3b-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="96f3b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96f3b-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="96f3b-110">Prerequisites</span></span>

<span data-ttu-id="96f3b-111">tooconfigure integracji z usługą Azure AD z Printix należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="96f3b-111">tooconfigure Azure AD integration with Printix, you need hello following items:</span></span>

- <span data-ttu-id="96f3b-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="96f3b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="96f3b-113">Printix logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="96f3b-113">A Printix single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="96f3b-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="96f3b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="96f3b-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="96f3b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="96f3b-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="96f3b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="96f3b-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="96f3b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="96f3b-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="96f3b-118">Scenario description</span></span>
<span data-ttu-id="96f3b-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="96f3b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="96f3b-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="96f3b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="96f3b-121">Dodawanie Printix z galerii hello</span><span class="sxs-lookup"><span data-stu-id="96f3b-121">Adding Printix from hello gallery</span></span>
2. <span data-ttu-id="96f3b-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="96f3b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-printix-from-hello-gallery"></a><span data-ttu-id="96f3b-123">Dodawanie Printix z galerii hello</span><span class="sxs-lookup"><span data-stu-id="96f3b-123">Adding Printix from hello gallery</span></span>
<span data-ttu-id="96f3b-124">tooconfigure hello integracji Printix do usługi Azure AD, należy tooadd Printix z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="96f3b-124">tooconfigure hello integration of Printix into Azure AD, you need tooadd Printix from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="96f3b-125">**tooadd Printix z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="96f3b-125">**tooadd Printix from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="96f3b-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="96f3b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="96f3b-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="96f3b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="96f3b-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="96f3b-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="96f3b-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="96f3b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="96f3b-133">W polu wyszukiwania hello wpisz **Printix**.</span><span class="sxs-lookup"><span data-stu-id="96f3b-133">In hello search box, type **Printix**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-printix-tutorial/tutorial_printix_search.png)

5. <span data-ttu-id="96f3b-135">W panelu wyników hello zaznacz **Printix**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="96f3b-135">In hello results panel, select **Printix**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-printix-tutorial/tutorial_printix_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="96f3b-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="96f3b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="96f3b-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Printix w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="96f3b-138">In this section, you configure and test Azure AD single sign-on with Printix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="96f3b-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Printix jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96f3b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Printix is tooa user in Azure AD.</span></span> <span data-ttu-id="96f3b-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Printix musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="96f3b-140">In other words, a link relationship between an Azure AD user and hello related user in Printix needs toobe established.</span></span>

<span data-ttu-id="96f3b-141">W Printix, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="96f3b-141">In Printix, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="96f3b-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Printix, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="96f3b-142">tooconfigure and test Azure AD single sign-on with Printix, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="96f3b-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="96f3b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="96f3b-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="96f3b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="96f3b-145">**[Tworzenie użytkownika testowego Printix](#creating-a-printix-test-user)**  -toohave odpowiednikiem Simona Britta w Printix, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="96f3b-145">**[Creating a Printix test user](#creating-a-printix-test-user)** - toohave a counterpart of Britta Simon in Printix that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="96f3b-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="96f3b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="96f3b-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="96f3b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="96f3b-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="96f3b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="96f3b-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Printix.</span><span class="sxs-lookup"><span data-stu-id="96f3b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Printix application.</span></span>

<span data-ttu-id="96f3b-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Printix, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="96f3b-150">**tooconfigure Azure AD single sign-on with Printix, perform hello following steps:**</span></span>

1. <span data-ttu-id="96f3b-151">W portalu Azure na powitania hello **Printix** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="96f3b-151">In hello Azure portal, on hello **Printix** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="96f3b-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="96f3b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-printix-tutorial/tutorial_printix_samlbase.png)

3. <span data-ttu-id="96f3b-155">Na powitania **Printix domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="96f3b-155">On hello **Printix Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-printix-tutorial/tutorial_printix_url.png)

    <span data-ttu-id="96f3b-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<subdomain>.printix.net`</span><span class="sxs-lookup"><span data-stu-id="96f3b-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.printix.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="96f3b-158">wartość Hello nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="96f3b-158">hello value is not real.</span></span> <span data-ttu-id="96f3b-159">Wartość hello aktualizacji z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="96f3b-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="96f3b-160">Skontaktuj się z [zespołem pomocy technicznej klienta Printix](mailto:support@printix.net) tooget hello wartość.</span><span class="sxs-lookup"><span data-stu-id="96f3b-160">Contact [Printix Client support team](mailto:support@printix.net) tooget hello value.</span></span> 
 
4. <span data-ttu-id="96f3b-161">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="96f3b-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-printix-tutorial/tutorial_printix_certificate.png) 

5. <span data-ttu-id="96f3b-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="96f3b-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-printix-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="96f3b-165">Dzierżawca Printix tooyour logowania jako administrator.</span><span class="sxs-lookup"><span data-stu-id="96f3b-165">Sign-on tooyour Printix tenant as an administrator.</span></span>

7. <span data-ttu-id="96f3b-166">W menu hello na górze hello, kliknij ikonę hello w prawym górnym rogu hello i wybierz "**uwierzytelniania**".</span><span class="sxs-lookup"><span data-stu-id="96f3b-166">In hello menu on hello top, click hello icon at hello upper right corner and select "**Authentication**".</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-printix-tutorial/tutorial_printix_06.png)

8. <span data-ttu-id="96f3b-168">Na powitania **Instalator** wybierz opcję **uwierzytelniania Włącz Azure/Office 365**</span><span class="sxs-lookup"><span data-stu-id="96f3b-168">On hello **Setup** tab, select **Enable Azure/Office 365 authentication**</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-printix-tutorial/tutorial_printix_07.png)

9. <span data-ttu-id="96f3b-170">Na powitania **Azure** karcie pole tekstowe toohello adres URL metadanych Federacji wejściowych z "**dokument metadanych usług federacyjnych**".</span><span class="sxs-lookup"><span data-stu-id="96f3b-170">On hello **Azure** tab, input federation metadata URL toohello textbox of "**Federation metadata document**".</span></span> 

    <span data-ttu-id="96f3b-171">Dołącz plik xml metadanych hello, który został pobrany z usługi Azure AD za[zespołem pomocy technicznej Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="96f3b-171">Attach hello metadata xml file which you downloaded from Azure AD too[Printix support team](mailto:support@printix.net).</span></span> <span data-ttu-id="96f3b-172">Następnie przekaż plik xml hello i wprowadzić adres URL metadanych federacji.</span><span class="sxs-lookup"><span data-stu-id="96f3b-172">Then they upload hello xml file and provide a federation metadata URL.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-printix-tutorial/tutorial_printix_08.png)
   
10. <span data-ttu-id="96f3b-174">Kliknij przycisk hello "**Test**"przycisk i kliknij przycisk"**OK**" przycisku, jeśli hello test zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="96f3b-174">Click hello "**Test**" button and click "**OK**" button if hello test was successful.</span></span>
   
     <span data-ttu-id="96f3b-175">Strona usługi Azure active directory zostaną wyświetlone po kliknięciu hello **test** przycisku.</span><span class="sxs-lookup"><span data-stu-id="96f3b-175">Azure active directory page will show after clicking hello **test** button.</span></span> <span data-ttu-id="96f3b-176">"powiodło się testu hello" w tym miejscu oznacza, że po wprowadzeniu poświadczeń hello konta Azure testu, który będzie punktu obecności komunikat "Ustawienia sprawdzona". Następnie kliknij przycisk hello **OK** przycisku.</span><span class="sxs-lookup"><span data-stu-id="96f3b-176">"hello test was successful" here means after entering hello credentials of your Azure test account it will pop up a message "Settings tested OK".Then click hello **OK** button.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-printix-tutorial/tutorial_printix_09.png)

11. <span data-ttu-id="96f3b-178">Kliknij przycisk hello **zapisać** znajdującego się na "**uwierzytelniania**" strony.</span><span class="sxs-lookup"><span data-stu-id="96f3b-178">Click hello **Save** button on "**Authentication**" page.</span></span>


> [!TIP]
> <span data-ttu-id="96f3b-179">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="96f3b-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="96f3b-180">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="96f3b-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="96f3b-181">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="96f3b-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="96f3b-182">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="96f3b-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="96f3b-183">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="96f3b-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="96f3b-185">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="96f3b-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="96f3b-186">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="96f3b-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="96f3b-188">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="96f3b-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="96f3b-190">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="96f3b-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="96f3b-192">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="96f3b-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="96f3b-194">a.</span><span class="sxs-lookup"><span data-stu-id="96f3b-194">a.</span></span> <span data-ttu-id="96f3b-195">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="96f3b-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="96f3b-196">b.</span><span class="sxs-lookup"><span data-stu-id="96f3b-196">b.</span></span> <span data-ttu-id="96f3b-197">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="96f3b-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="96f3b-198">c.</span><span class="sxs-lookup"><span data-stu-id="96f3b-198">c.</span></span> <span data-ttu-id="96f3b-199">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="96f3b-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="96f3b-200">d.</span><span class="sxs-lookup"><span data-stu-id="96f3b-200">d.</span></span> <span data-ttu-id="96f3b-201">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="96f3b-201">Click **Create**.</span></span>
 
### <a name="creating-a-printix-test-user"></a><span data-ttu-id="96f3b-202">Tworzenie użytkownika testowego Printix</span><span class="sxs-lookup"><span data-stu-id="96f3b-202">Creating a Printix test user</span></span>

<span data-ttu-id="96f3b-203">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Printix.</span><span class="sxs-lookup"><span data-stu-id="96f3b-203">hello objective of this section is toocreate a user called Britta Simon in Printix.</span></span> <span data-ttu-id="96f3b-204">Printix obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="96f3b-204">Printix supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="96f3b-205">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="96f3b-205">There is no action item for you in this section.</span></span> <span data-ttu-id="96f3b-206">Nowy użytkownik jest tworzona podczas próby tooaccess Printix, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="96f3b-206">A new user is created during an attempt tooaccess Printix if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="96f3b-207">Jeśli potrzebujesz ręcznie toocreate użytkownika, należy toocontact hello [zespołem pomocy technicznej Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="96f3b-207">If you need toocreate a user manually, you need toocontact hello [Printix support team](mailto:support@printix.net).</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="96f3b-208">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="96f3b-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="96f3b-209">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooPrintix.</span><span class="sxs-lookup"><span data-stu-id="96f3b-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPrintix.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="96f3b-211">**tooassign tooPrintix Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="96f3b-211">**tooassign Britta Simon tooPrintix, perform hello following steps:**</span></span>

1. <span data-ttu-id="96f3b-212">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="96f3b-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="96f3b-214">Z listy aplikacji hello wybierz **Printix**.</span><span class="sxs-lookup"><span data-stu-id="96f3b-214">In hello applications list, select **Printix**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-printix-tutorial/tutorial_printix_app.png) 

3. <span data-ttu-id="96f3b-216">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="96f3b-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="96f3b-218">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="96f3b-218">Click **Add** button.</span></span> <span data-ttu-id="96f3b-219">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="96f3b-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="96f3b-221">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="96f3b-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="96f3b-222">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="96f3b-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="96f3b-223">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="96f3b-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="96f3b-224">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="96f3b-224">Testing single sign-on</span></span>

<span data-ttu-id="96f3b-225">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="96f3b-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="96f3b-226">Po kliknięciu kafelka Printix hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Printix aplikacji.</span><span class="sxs-lookup"><span data-stu-id="96f3b-226">When you click hello Printix tile in hello Access Panel, you should get automatically signed-on tooyour Printix application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="96f3b-227">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="96f3b-227">Additional resources</span></span>

* [<span data-ttu-id="96f3b-228">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="96f3b-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="96f3b-229">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="96f3b-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-printix-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-printix-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-printix-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-printix-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-printix-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-printix-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-printix-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-printix-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-printix-tutorial/tutorial_general_203.png

