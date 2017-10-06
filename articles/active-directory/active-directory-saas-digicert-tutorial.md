---
title: 'Samouczek: Integracji Azure Active Directory z DigiCert | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i DigiCert."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 646f3129-aa67-4875-9073-1d0b6a3173d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 861039d00533b3aeb361d04e45c4460c6fc8cef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-digicert"></a><span data-ttu-id="18817-103">Samouczek: Integracji Azure Active Directory z DigiCert</span><span class="sxs-lookup"><span data-stu-id="18817-103">Tutorial: Azure Active Directory integration with DigiCert</span></span>

<span data-ttu-id="18817-104">Z tego samouczka, dowiesz się, jak toointegrate DigiCert w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="18817-104">In this tutorial, you learn how toointegrate DigiCert with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="18817-105">Integracja z usługą Azure AD DigiCert zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="18817-105">Integrating DigiCert with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="18817-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooDigiCert</span><span class="sxs-lookup"><span data-stu-id="18817-106">You can control in Azure AD who has access tooDigiCert</span></span>
- <span data-ttu-id="18817-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooDigiCert (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="18817-107">You can enable your users tooautomatically get signed-on tooDigiCert (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="18817-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="18817-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="18817-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="18817-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18817-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="18817-110">Prerequisites</span></span>

<span data-ttu-id="18817-111">tooconfigure integracji usługi Azure AD z DigiCert należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="18817-111">tooconfigure Azure AD integration with DigiCert, you need hello following items:</span></span>

- <span data-ttu-id="18817-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="18817-112">An Azure AD subscription</span></span>
- <span data-ttu-id="18817-113">DigiCert logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="18817-113">A DigiCert single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="18817-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="18817-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="18817-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="18817-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="18817-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="18817-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="18817-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="18817-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="18817-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="18817-118">Scenario description</span></span>
<span data-ttu-id="18817-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="18817-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="18817-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="18817-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="18817-121">Dodawanie DigiCert z galerii hello</span><span class="sxs-lookup"><span data-stu-id="18817-121">Adding DigiCert from hello gallery</span></span>
2. <span data-ttu-id="18817-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="18817-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-digicert-from-hello-gallery"></a><span data-ttu-id="18817-123">Dodawanie DigiCert z galerii hello</span><span class="sxs-lookup"><span data-stu-id="18817-123">Adding DigiCert from hello gallery</span></span>
<span data-ttu-id="18817-124">tooconfigure hello integracji DigiCert do usługi Azure AD, należy tooadd DigiCert z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="18817-124">tooconfigure hello integration of DigiCert into Azure AD, you need tooadd DigiCert from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="18817-125">**tooadd DigiCert z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="18817-125">**tooadd DigiCert from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="18817-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="18817-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="18817-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="18817-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="18817-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="18817-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="18817-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="18817-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="18817-133">W polu wyszukiwania hello wpisz **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="18817-133">In hello search box, type **DigiCert**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_search.png)

5. <span data-ttu-id="18817-135">W panelu wyników hello, wybierz **DigiCert**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="18817-135">In hello results panel, select **DigiCert**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="18817-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="18817-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="18817-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z DigiCert na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="18817-138">In this section, you configure and test Azure AD single sign-on with DigiCert based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="18817-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w DigiCert jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="18817-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in DigiCert is tooa user in Azure AD.</span></span> <span data-ttu-id="18817-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w DigiCert musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="18817-140">In other words, a link relationship between an Azure AD user and hello related user in DigiCert needs toobe established.</span></span>

<span data-ttu-id="18817-141">W DigiCert, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="18817-141">In DigiCert, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="18817-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z DigiCert, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="18817-142">tooconfigure and test Azure AD single sign-on with DigiCert, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="18817-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="18817-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="18817-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="18817-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="18817-145">**[Tworzenie użytkownika testowego DigiCert](#creating-a-digicert-test-user)**  -toohave odpowiednikiem Simona Britta w DigiCert, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="18817-145">**[Creating a DigiCert test user](#creating-a-digicert-test-user)** - toohave a counterpart of Britta Simon in DigiCert that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="18817-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="18817-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="18817-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="18817-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="18817-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="18817-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="18817-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji DigiCert.</span><span class="sxs-lookup"><span data-stu-id="18817-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your DigiCert application.</span></span>

<span data-ttu-id="18817-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z DigiCert, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="18817-150">**tooconfigure Azure AD single sign-on with DigiCert, perform hello following steps:**</span></span>

1. <span data-ttu-id="18817-151">W portalu Azure na powitania hello **DigiCert** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="18817-151">In hello Azure portal, on hello **DigiCert** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="18817-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="18817-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_samlbase.png)

3. <span data-ttu-id="18817-155">Na powitania **DigiCert domeny i adres URL** sekcji, hello użytkownik nie ma tooperform wszystkie kroki jako aplikacji hello już jest wstępna Integracja z usługą Azure.</span><span class="sxs-lookup"><span data-stu-id="18817-155">On hello **DigiCert Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_url.png)

4. <span data-ttu-id="18817-157">Aplikacja firmy DigiCert oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="18817-157">DigiCert application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="18817-158">Skonfiguruj powitania po oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="18817-158">Configure hello following claims for this application.</span></span> <span data-ttu-id="18817-159">Można zarządzać hello wartości tych atrybutów z hello "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="18817-159">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="18817-160">powitania po zrzut ekranu przedstawia przykład dla tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="18817-160">hello following screenshot shows an example for this configuration.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_attributes.png)
    
5. <span data-ttu-id="18817-162">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie hello i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="18817-162">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="18817-163">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="18817-163">Attribute Name</span></span> | <span data-ttu-id="18817-164">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="18817-164">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="18817-165">Firmy</span><span class="sxs-lookup"><span data-stu-id="18817-165">company</span></span> | <span data-ttu-id="18817-166">< companycode ></span><span class="sxs-lookup"><span data-stu-id="18817-166">< companycode ></span></span> |
    | <span data-ttu-id="18817-167">digicertrole</span><span class="sxs-lookup"><span data-stu-id="18817-167">digicertrole</span></span> | <span data-ttu-id="18817-168">CanAccessCertCentral</span><span class="sxs-lookup"><span data-stu-id="18817-168">CanAccessCertCentral</span></span> |

    > [!Note]
    > <span data-ttu-id="18817-169">Witaj wartość **firmy** atrybut nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="18817-169">hello value of **company** attribute is not real.</span></span> <span data-ttu-id="18817-170">Zaktualizuj tę wartość z kodem rzeczywiste firmy.</span><span class="sxs-lookup"><span data-stu-id="18817-170">Update this value with actual company code.</span></span> <span data-ttu-id="18817-171">wartość hello tooget **firmy** atrybutu skontaktuj się z [zespołem pomocy technicznej firmy DigiCert](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="18817-171">tooget hello value of **company** attribute contact [DigiCert support team](mailto:support@digicert.com).</span></span>

    <span data-ttu-id="18817-172">a.</span><span class="sxs-lookup"><span data-stu-id="18817-172">a.</span></span> <span data-ttu-id="18817-173">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="18817-173">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="18817-176">b.</span><span class="sxs-lookup"><span data-stu-id="18817-176">b.</span></span> <span data-ttu-id="18817-177">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="18817-177">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="18817-178">c.</span><span class="sxs-lookup"><span data-stu-id="18817-178">c.</span></span> <span data-ttu-id="18817-179">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="18817-179">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="18817-180">d.</span><span class="sxs-lookup"><span data-stu-id="18817-180">d.</span></span> <span data-ttu-id="18817-181">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="18817-181">Click **Ok**.</span></span> 

6. <span data-ttu-id="18817-182">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="18817-182">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_certificate.png) 

7. <span data-ttu-id="18817-184">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="18817-184">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-digicert-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="18817-186">tooconfigure rejestracji jednokrotnej w **DigiCert** strony, należy pobrać hello toosend **XML metadanych** za[zespołem pomocy technicznej firmy DigiCert](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="18817-186">tooconfigure single sign-on on **DigiCert** side, you need toosend hello downloaded **Metadata XML** too[DigiCert support team](mailto:support@digicert.com).</span></span> <span data-ttu-id="18817-187">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="18817-187">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="18817-188">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="18817-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="18817-189">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="18817-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="18817-190">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="18817-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="18817-191">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="18817-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="18817-192">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="18817-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="18817-194">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="18817-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="18817-195">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="18817-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="18817-197">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="18817-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="18817-199">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="18817-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="18817-201">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="18817-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="18817-203">a.</span><span class="sxs-lookup"><span data-stu-id="18817-203">a.</span></span> <span data-ttu-id="18817-204">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="18817-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="18817-205">b.</span><span class="sxs-lookup"><span data-stu-id="18817-205">b.</span></span> <span data-ttu-id="18817-206">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="18817-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="18817-207">c.</span><span class="sxs-lookup"><span data-stu-id="18817-207">c.</span></span> <span data-ttu-id="18817-208">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="18817-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="18817-209">d.</span><span class="sxs-lookup"><span data-stu-id="18817-209">d.</span></span> <span data-ttu-id="18817-210">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="18817-210">Click **Create**.</span></span>
 
### <a name="creating-a-digicert-test-user"></a><span data-ttu-id="18817-211">Tworzenie użytkownika testowego DigiCert</span><span class="sxs-lookup"><span data-stu-id="18817-211">Creating a DigiCert test user</span></span>

<span data-ttu-id="18817-212">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w DigiCert.</span><span class="sxs-lookup"><span data-stu-id="18817-212">In this section, you create a user called Britta Simon in DigiCert.</span></span> <span data-ttu-id="18817-213">We współpracy z [zespołem pomocy technicznej firmy DigiCert](mailto:support@digicert.com) tooadd hello użytkowników w DigiCert.</span><span class="sxs-lookup"><span data-stu-id="18817-213">Please work with [DigiCert support team](mailto:support@digicert.com) tooadd hello users in DigiCert.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="18817-214">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="18817-214">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="18817-215">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooDigiCert.</span><span class="sxs-lookup"><span data-stu-id="18817-215">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDigiCert.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="18817-217">**tooassign tooDigiCert Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="18817-217">**tooassign Britta Simon tooDigiCert, perform hello following steps:**</span></span>

1. <span data-ttu-id="18817-218">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="18817-218">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="18817-220">Z listy aplikacji hello wybierz **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="18817-220">In hello applications list, select **DigiCert**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_app.png) 

3. <span data-ttu-id="18817-222">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="18817-222">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="18817-224">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="18817-224">Click **Add** button.</span></span> <span data-ttu-id="18817-225">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="18817-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="18817-227">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="18817-227">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="18817-228">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="18817-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="18817-229">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="18817-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="18817-230">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="18817-230">Testing single sign-on</span></span>

<span data-ttu-id="18817-231">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="18817-231">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="18817-232">Po kliknięciu kafelka DigiCert hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour DeigiCert aplikacji.</span><span class="sxs-lookup"><span data-stu-id="18817-232">When you click hello DigiCert tile in hello Access Panel, you should get automatically signed-on tooyour DeigiCert application.</span></span>
<span data-ttu-id="18817-233">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="18817-233">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="18817-234">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="18817-234">Additional resources</span></span>

* [<span data-ttu-id="18817-235">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="18817-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="18817-236">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="18817-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_203.png

