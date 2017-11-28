---
title: 'Samouczek: Integracji Azure Active Directory z Pluralsight | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Pluralsight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4c3f07d2-4e1f-4ea3-9025-c663f1f2b7b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c8394eed79f21fb889816d8dafe2d71187be72b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pluralsight"></a><span data-ttu-id="24baa-103">Samouczek: Integracji Azure Active Directory z Pluralsight</span><span class="sxs-lookup"><span data-stu-id="24baa-103">Tutorial: Azure Active Directory integration with Pluralsight</span></span>

<span data-ttu-id="24baa-104">Z tego samouczka, dowiesz się, jak toointegrate Pluralsight w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="24baa-104">In this tutorial, you learn how toointegrate Pluralsight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="24baa-105">Integracja z usługą Azure AD Pluralsight zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="24baa-105">Integrating Pluralsight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="24baa-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooPluralsight</span><span class="sxs-lookup"><span data-stu-id="24baa-106">You can control in Azure AD who has access tooPluralsight</span></span>
- <span data-ttu-id="24baa-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooPluralsight (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="24baa-107">You can enable your users tooautomatically get signed-on tooPluralsight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="24baa-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="24baa-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="24baa-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="24baa-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24baa-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="24baa-110">Prerequisites</span></span>

<span data-ttu-id="24baa-111">tooconfigure integracji z usługą Azure AD z Pluralsight należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="24baa-111">tooconfigure Azure AD integration with Pluralsight, you need hello following items:</span></span>

- <span data-ttu-id="24baa-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="24baa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="24baa-113">Pluralsight logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="24baa-113">A Pluralsight single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="24baa-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="24baa-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="24baa-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="24baa-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="24baa-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="24baa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="24baa-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="24baa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="24baa-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="24baa-118">Scenario description</span></span>
<span data-ttu-id="24baa-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="24baa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="24baa-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="24baa-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="24baa-121">Dodawanie Pluralsight z galerii hello</span><span class="sxs-lookup"><span data-stu-id="24baa-121">Adding Pluralsight from hello gallery</span></span>
2. <span data-ttu-id="24baa-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="24baa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pluralsight-from-hello-gallery"></a><span data-ttu-id="24baa-123">Dodawanie Pluralsight z galerii hello</span><span class="sxs-lookup"><span data-stu-id="24baa-123">Adding Pluralsight from hello gallery</span></span>
<span data-ttu-id="24baa-124">tooconfigure hello integracji Pluralsight do usługi Azure AD, należy tooadd Pluralsight z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="24baa-124">tooconfigure hello integration of Pluralsight into Azure AD, you need tooadd Pluralsight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="24baa-125">**tooadd Pluralsight z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="24baa-125">**tooadd Pluralsight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="24baa-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="24baa-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="24baa-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="24baa-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="24baa-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="24baa-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="24baa-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="24baa-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="24baa-133">W polu wyszukiwania hello wpisz **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="24baa-133">In hello search box, type **Pluralsight**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_search.png)

5. <span data-ttu-id="24baa-135">W panelu wyników hello zaznacz **Pluralsight**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="24baa-135">In hello results panel, select **Pluralsight**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="24baa-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="24baa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="24baa-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Pluralsight w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="24baa-138">In this section, you configure and test Azure AD single sign-on with Pluralsight based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="24baa-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Pluralsight jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24baa-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pluralsight is tooa user in Azure AD.</span></span> <span data-ttu-id="24baa-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Pluralsight musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="24baa-140">In other words, a link relationship between an Azure AD user and hello related user in Pluralsight needs toobe established.</span></span>

<span data-ttu-id="24baa-141">W Pluralsight, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="24baa-141">In Pluralsight, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="24baa-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Pluralsight, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="24baa-142">tooconfigure and test Azure AD single sign-on with Pluralsight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="24baa-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="24baa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="24baa-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="24baa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="24baa-145">**[Tworzenie użytkownika testowego Pluralsight](#creating-a-pluralsight-test-user)**  -toohave odpowiednikiem Simona Britta w Pluralsight, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="24baa-145">**[Creating a Pluralsight test user](#creating-a-pluralsight-test-user)** - toohave a counterpart of Britta Simon in Pluralsight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="24baa-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="24baa-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="24baa-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="24baa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="24baa-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="24baa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="24baa-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="24baa-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Pluralsight application.</span></span>

<span data-ttu-id="24baa-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Pluralsight, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="24baa-150">**tooconfigure Azure AD single sign-on with Pluralsight, perform hello following steps:**</span></span>

1. <span data-ttu-id="24baa-151">W portalu Azure na powitania hello **Pluralsight** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="24baa-151">In hello Azure portal, on hello **Pluralsight** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="24baa-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="24baa-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_samlbase.png)

3. <span data-ttu-id="24baa-155">Na powitania **Pluralsight domeny i adres URL** sekcji, wykonaj następujące hello:</span><span class="sxs-lookup"><span data-stu-id="24baa-155">On hello **Pluralsight Domain and URLs** section, perform hello following:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_url.png)

    <span data-ttu-id="24baa-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<instance name>.pluralsight.com/sso/<company name>`</span><span class="sxs-lookup"><span data-stu-id="24baa-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instance name>.pluralsight.com/sso/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="24baa-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="24baa-158">This value is not real.</span></span> <span data-ttu-id="24baa-159">Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="24baa-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="24baa-160">Skontaktuj się z [zespołem pomocy technicznej klienta Pluralsight](mailto:support@pluralsight.com) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="24baa-160">Contact [Pluralsight Client support team](mailto:support@pluralsight.com) tooget this value.</span></span> 
 


4. <span data-ttu-id="24baa-161">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="24baa-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_certificate.png) 

5. <span data-ttu-id="24baa-163">Celem Hello w tej sekcji jest tooenable usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i tooconfigure logowania jednokrotnego w hello Pluralsight aplikacji.</span><span class="sxs-lookup"><span data-stu-id="24baa-163">hello objective of this section is tooenable Azure AD single sign-on in hello Azure portal and tooconfigure SSO in hello Pluralsight application.</span></span>

    <span data-ttu-id="24baa-164">Witaj Pluralsight aplikacji oczekuje potwierdzenia SAML hello w określonym formacie wymaga możesz tooadd atrybutu niestandardowego mapowania tooyour SAML tokenu atrybuty konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="24baa-164">hello Pluralsight application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="24baa-165">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="24baa-165">hello following screenshot shows an example for this.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_attribute.png)

    >[!NOTE]
    ><span data-ttu-id="24baa-167">Możesz także dodać hello **"Unikatowy identyfikator"** atrybut o hello wartości odpowiednich jak identyfikator pracownika lub inny element, który jest odpowiedni dla Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="24baa-167">You can also add hello **"Unique ID"** attribute with hello appropriate value like EmployeeID or something else which suits for your organization.</span></span> <span data-ttu-id="24baa-168">Należy również zauważyć, że nie jest wymagany atrybut hello; jednak ją dodać za zidentyfikować hello unikatowego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="24baa-168">Also note that this is not hello required attribute; however, you can add it too identify hello unique user.</span></span> 

6. <span data-ttu-id="24baa-169">wymagane hello tooadd **atrybuty tokenu SAML**, dla każdego wiersza poniższą tabelą hello wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="24baa-169">tooadd hello required **SAML token attributes**, for each row shown in hello table below, perform hello following steps:</span></span>
   
   | <span data-ttu-id="24baa-170">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="24baa-170">Attribute Name</span></span> | <span data-ttu-id="24baa-171">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="24baa-171">Attribute Value</span></span> |
   | ---| --- |
   | <span data-ttu-id="24baa-172">Imię</span><span class="sxs-lookup"><span data-stu-id="24baa-172">First Name</span></span> |<span data-ttu-id="24baa-173">User.givenName</span><span class="sxs-lookup"><span data-stu-id="24baa-173">user.givenname</span></span> |
   | <span data-ttu-id="24baa-174">Nazwisko</span><span class="sxs-lookup"><span data-stu-id="24baa-174">Last Name</span></span> |<span data-ttu-id="24baa-175">User.surname</span><span class="sxs-lookup"><span data-stu-id="24baa-175">user.surname</span></span> |
   | <span data-ttu-id="24baa-176">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="24baa-176">Email</span></span> |<span data-ttu-id="24baa-177">User.mail</span><span class="sxs-lookup"><span data-stu-id="24baa-177">user.mail</span></span> |
   
   <span data-ttu-id="24baa-178">a.</span><span class="sxs-lookup"><span data-stu-id="24baa-178">a.</span></span> <span data-ttu-id="24baa-179">Kliknij przycisk **Dodaj atrybut użytkownika** tooopen hello **Dodaj użytkownika Attribure** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="24baa-179">Click **add user attribute** tooopen hello **Add User Attribure** dialog.</span></span>
    
     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_addattribute.png)
  
   <span data-ttu-id="24baa-181">b.</span><span class="sxs-lookup"><span data-stu-id="24baa-181">b.</span></span> <span data-ttu-id="24baa-182">W hello **nazwa atrybutu** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="24baa-182">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
  
   <span data-ttu-id="24baa-183">c.</span><span class="sxs-lookup"><span data-stu-id="24baa-183">c.</span></span> <span data-ttu-id="24baa-184">Z hello **wartość atrybutu** lista, hello wybierz atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="24baa-184">From hello **Attribute Value** list, select hello attribute value shown for that row.</span></span>
  
   <span data-ttu-id="24baa-185">d.</span><span class="sxs-lookup"><span data-stu-id="24baa-185">d.</span></span> <span data-ttu-id="24baa-186">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="24baa-186">Click **Ok**.</span></span>    

7. <span data-ttu-id="24baa-187">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="24baa-187">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pluralsight-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="24baa-189">tooget logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z [Pluralsight Professional usług](mailTo:professionalservices@pluralsight.com) zespołu i podaj hello metadanych pobranego pliku.</span><span class="sxs-lookup"><span data-stu-id="24baa-189">tooget SSO configured for your application, contact [Pluralsight Professional Services](mailTo:professionalservices@pluralsight.com) team and provide hello downloaded metadata file.</span></span>

> [!TIP]
> <span data-ttu-id="24baa-190">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="24baa-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="24baa-191">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="24baa-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="24baa-192">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="24baa-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="24baa-193">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="24baa-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="24baa-194">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="24baa-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="24baa-196">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="24baa-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="24baa-197">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="24baa-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="24baa-199">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="24baa-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="24baa-201">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="24baa-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="24baa-203">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="24baa-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-pluralsight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="24baa-205">a.</span><span class="sxs-lookup"><span data-stu-id="24baa-205">a.</span></span> <span data-ttu-id="24baa-206">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="24baa-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="24baa-207">b.</span><span class="sxs-lookup"><span data-stu-id="24baa-207">b.</span></span> <span data-ttu-id="24baa-208">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="24baa-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="24baa-209">c.</span><span class="sxs-lookup"><span data-stu-id="24baa-209">c.</span></span> <span data-ttu-id="24baa-210">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="24baa-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="24baa-211">d.</span><span class="sxs-lookup"><span data-stu-id="24baa-211">d.</span></span> <span data-ttu-id="24baa-212">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="24baa-212">Click **Create**.</span></span>
 
### <a name="creating-a-pluralsight-test-user"></a><span data-ttu-id="24baa-213">Tworzenie użytkownika testowego Pluralsight</span><span class="sxs-lookup"><span data-stu-id="24baa-213">Creating a Pluralsight test user</span></span>

<span data-ttu-id="24baa-214">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Pluralsight.</span><span class="sxs-lookup"><span data-stu-id="24baa-214">hello objective of this section is toocreate a user called Britta Simon in Pluralsight.</span></span> <span data-ttu-id="24baa-215">We współpracy z [zespołem pomocy technicznej klienta Pluralsight](mailto:support@pluralsight.com) tooadd hello użytkowników w hello Pluralsight konta.</span><span class="sxs-lookup"><span data-stu-id="24baa-215">Please work with [Pluralsight Client support team](mailto:support@pluralsight.com) tooadd hello users in hello Pluralsight account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="24baa-216">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="24baa-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="24baa-217">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooPluralsight.</span><span class="sxs-lookup"><span data-stu-id="24baa-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPluralsight.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="24baa-219">**tooassign tooPluralsight Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="24baa-219">**tooassign Britta Simon tooPluralsight, perform hello following steps:**</span></span>

1. <span data-ttu-id="24baa-220">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="24baa-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="24baa-222">Z listy aplikacji hello wybierz **Pluralsight**.</span><span class="sxs-lookup"><span data-stu-id="24baa-222">In hello applications list, select **Pluralsight**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-pluralsight-tutorial/tutorial_pluralsight_app.png) 

3. <span data-ttu-id="24baa-224">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="24baa-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="24baa-226">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="24baa-226">Click **Add** button.</span></span> <span data-ttu-id="24baa-227">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="24baa-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="24baa-229">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="24baa-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="24baa-230">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="24baa-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="24baa-231">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="24baa-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="24baa-232">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="24baa-232">Testing single sign-on</span></span>

<span data-ttu-id="24baa-233">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="24baa-233">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="24baa-234">Po kliknięciu kafelka Pluralsight hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Pluralsight aplikacji.</span><span class="sxs-lookup"><span data-stu-id="24baa-234">When you click hello Pluralsight tile in hello Access Panel, you should get automatically signed-on tooyour Pluralsight application.</span></span> <span data-ttu-id="24baa-235">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="24baa-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="24baa-236">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="24baa-236">Additional resources</span></span>

* [<span data-ttu-id="24baa-237">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="24baa-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="24baa-238">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="24baa-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pluralsight-tutorial/tutorial_general_203.png

