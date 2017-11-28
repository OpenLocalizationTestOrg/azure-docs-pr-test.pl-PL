---
title: 'Samouczek: Azure Active Directory integracji z oprogramowaniem OfficeSpace | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między oprogramowaniem OfficeSpace i Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 95d8413f-db98-4e2c-8097-9142ef1af823
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: b53afb648b8a6057c32c782d857e34c06e152c67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-officespace-software"></a><span data-ttu-id="81950-103">Samouczek: Azure Active Directory integracji z oprogramowaniem OfficeSpace</span><span class="sxs-lookup"><span data-stu-id="81950-103">Tutorial: Azure Active Directory integration with OfficeSpace Software</span></span>

<span data-ttu-id="81950-104">Z tego samouczka, dowiesz się, jak toointegrate OfficeSpace oprogramowania w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="81950-104">In this tutorial, you learn how toointegrate OfficeSpace Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="81950-105">Integracja oprogramowania OfficeSpace z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="81950-105">Integrating OfficeSpace Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="81950-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooOfficeSpace oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="81950-106">You can control in Azure AD who has access tooOfficeSpace Software.</span></span>
- <span data-ttu-id="81950-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooOfficeSpace oprogramowania (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81950-107">You can enable your users tooautomatically get signed-on tooOfficeSpace Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="81950-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="81950-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="81950-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="81950-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81950-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="81950-110">Prerequisites</span></span>

<span data-ttu-id="81950-111">tooconfigure integracji usługi Azure AD z oprogramowaniem OfficeSpace należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="81950-111">tooconfigure Azure AD integration with OfficeSpace Software, you need hello following items:</span></span>

- <span data-ttu-id="81950-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="81950-112">An Azure AD subscription</span></span>
- <span data-ttu-id="81950-113">Oprogramowanie OfficeSpace logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="81950-113">A OfficeSpace Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="81950-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="81950-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="81950-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="81950-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="81950-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="81950-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="81950-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="81950-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="81950-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="81950-118">Scenario description</span></span>
<span data-ttu-id="81950-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="81950-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="81950-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="81950-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="81950-121">Dodawanie oprogramowania OfficeSpace z galerii hello</span><span class="sxs-lookup"><span data-stu-id="81950-121">Adding OfficeSpace Software from hello gallery</span></span>
2. <span data-ttu-id="81950-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="81950-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-officespace-software-from-hello-gallery"></a><span data-ttu-id="81950-123">Dodawanie oprogramowania OfficeSpace z galerii hello</span><span class="sxs-lookup"><span data-stu-id="81950-123">Adding OfficeSpace Software from hello gallery</span></span>
<span data-ttu-id="81950-124">tooconfigure hello integracji OfficeSpace oprogramowania do usługi Azure AD, należy tooadd OfficeSpace oprogramowania z listy tooyour galerii hello zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="81950-124">tooconfigure hello integration of OfficeSpace Software into Azure AD, you need tooadd OfficeSpace Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="81950-125">**tooadd OfficeSpace oprogramowania z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="81950-125">**tooadd OfficeSpace Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="81950-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="81950-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="81950-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="81950-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="81950-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="81950-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="81950-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="81950-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="81950-133">W polu wyszukiwania hello wpisz **OfficeSpace oprogramowania**, wybierz pozycję **OfficeSpace oprogramowania** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="81950-133">In hello search box, type **OfficeSpace Software**, select **OfficeSpace Software** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Oprogramowanie OfficeSpace w hello liście wyników](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="81950-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="81950-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="81950-136">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z oprogramowaniem OfficeSpace w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="81950-136">In this section, you configure and test Azure AD single sign-on with OfficeSpace Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="81950-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w oprogramowaniu OfficeSpace jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81950-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in OfficeSpace Software is tooa user in Azure AD.</span></span> <span data-ttu-id="81950-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w oprogramowaniu OfficeSpace musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="81950-138">In other words, a link relationship between an Azure AD user and hello related user in OfficeSpace Software needs toobe established.</span></span>

<span data-ttu-id="81950-139">W oprogramowaniu OfficeSpace, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="81950-139">In OfficeSpace Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="81950-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z oprogramowaniem OfficeSpace, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="81950-140">tooconfigure and test Azure AD single sign-on with OfficeSpace Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="81950-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="81950-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="81950-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="81950-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="81950-143">**[Tworzenie użytkownika testowego oprogramowania OfficeSpace](#create-a-officespace-software-test-user)**  -toohave odpowiednikiem Simona Britta OfficeSpace oprogramowania, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="81950-143">**[Create a OfficeSpace Software test user](#create-a-officespace-software-test-user)** - toohave a counterpart of Britta Simon in OfficeSpace Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="81950-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="81950-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="81950-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="81950-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="81950-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="81950-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="81950-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w używanej aplikacji OfficeSpace.</span><span class="sxs-lookup"><span data-stu-id="81950-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your OfficeSpace Software application.</span></span>

<span data-ttu-id="81950-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z oprogramowaniem OfficeSpace wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="81950-148">**tooconfigure Azure AD single sign-on with OfficeSpace Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="81950-149">W portalu Azure na powitania hello **oprogramowania OfficeSpace** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="81950-149">In hello Azure portal, on hello **OfficeSpace Software** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="81950-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="81950-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_samlbase.png)

3. <span data-ttu-id="81950-153">Na powitania **OfficeSpace oprogramowania domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="81950-153">On hello **OfficeSpace Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Adresy URL i domeny oprogramowania OfficeSpace pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_url.png)

    <span data-ttu-id="81950-155">a.</span><span class="sxs-lookup"><span data-stu-id="81950-155">a.</span></span> <span data-ttu-id="81950-156">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.officespacesoftware.com/users/sign_in/saml`</span><span class="sxs-lookup"><span data-stu-id="81950-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.officespacesoftware.com/users/sign_in/saml`</span></span>

    <span data-ttu-id="81950-157">b.</span><span class="sxs-lookup"><span data-stu-id="81950-157">b.</span></span> <span data-ttu-id="81950-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`<company name>.officespacesoftware.com`</span><span class="sxs-lookup"><span data-stu-id="81950-158">In hello **Identifier** textbox, type a URL using hello following pattern: `<company name>.officespacesoftware.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="81950-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="81950-159">These values are not real.</span></span> <span data-ttu-id="81950-160">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="81950-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="81950-161">Skontaktuj się z [zespołem pomocy technicznej klienta oprogramowania OfficeSpace](mailto:support@officespacesoftware.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="81950-161">Contact [OfficeSpace Software Client support team](mailto:support@officespacesoftware.com) tooget these values.</span></span> 

4. <span data-ttu-id="81950-162">Aplikacja OfficeSpace oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="81950-162">OfficeSpace Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="81950-163">Skonfiguruj powitania po oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="81950-163">Please configure hello following claims for this application.</span></span> <span data-ttu-id="81950-164">Można zarządzać hello wartości tych atrybutów z hello "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="81950-164">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="81950-165">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="81950-165">hello following screenshot shows an example for this.</span></span>
    
    ![Konfigurowanie atrybutów](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_attribute.png)

5. <span data-ttu-id="81950-167">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **user.mail** jako **identyfikator użytkownika** i dla każdego wiersza wyświetlany w poniższej tabeli hello wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="81950-167">In hello **User Attributes** section on hello **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in hello table below, perform hello following steps:</span></span>
    
    | <span data-ttu-id="81950-168">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="81950-168">Attribute Name</span></span> | <span data-ttu-id="81950-169">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="81950-169">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="81950-170">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="81950-170">email</span></span> | <span data-ttu-id="81950-171">User.mail</span><span class="sxs-lookup"><span data-stu-id="81950-171">user.mail</span></span> |
    | <span data-ttu-id="81950-172">name</span><span class="sxs-lookup"><span data-stu-id="81950-172">name</span></span> | <span data-ttu-id="81950-173">User.DisplayName</span><span class="sxs-lookup"><span data-stu-id="81950-173">user.displayname</span></span> |
    | <span data-ttu-id="81950-174">Imię</span><span class="sxs-lookup"><span data-stu-id="81950-174">first_name</span></span> | <span data-ttu-id="81950-175">User.givenName</span><span class="sxs-lookup"><span data-stu-id="81950-175">user.givenname</span></span> |
    | <span data-ttu-id="81950-176">nazwisko</span><span class="sxs-lookup"><span data-stu-id="81950-176">last_name</span></span> | <span data-ttu-id="81950-177">User.surname</span><span class="sxs-lookup"><span data-stu-id="81950-177">user.surname</span></span> |

    <span data-ttu-id="81950-178">a.</span><span class="sxs-lookup"><span data-stu-id="81950-178">a.</span></span> <span data-ttu-id="81950-179">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="81950-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![<span data-ttu-id="81950-180">Skonfiguruj Dodaj</span><span class="sxs-lookup"><span data-stu-id="81950-180">Configure Add</span></span> ](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_04.png)

    ![Konfigurowanie atrybutów](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="81950-182">b.</span><span class="sxs-lookup"><span data-stu-id="81950-182">b.</span></span> <span data-ttu-id="81950-183">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="81950-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="81950-184">c.</span><span class="sxs-lookup"><span data-stu-id="81950-184">c.</span></span> <span data-ttu-id="81950-185">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="81950-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="81950-186">d.</span><span class="sxs-lookup"><span data-stu-id="81950-186">d.</span></span> <span data-ttu-id="81950-187">Kliknij przycisk **Ok**</span><span class="sxs-lookup"><span data-stu-id="81950-187">Click **Ok**</span></span>
 
6. <span data-ttu-id="81950-188">Na powitania **certyfikat podpisywania SAML** hello kopiowania, sekcji **odcisk PALCA** wartość hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="81950-188">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of hello certificate.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_certificate.png) 

7. <span data-ttu-id="81950-190">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="81950-190">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-officespace-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="81950-192">Na powitania **konfiguracji oprogramowania OfficeSpace** kliknij **Konfigurowanie oprogramowania OfficeSpace** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="81950-192">On hello **OfficeSpace Software Configuration** section, click **Configure OfficeSpace Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="81950-193">Witaj kopii **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="81950-193">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfiguracja oprogramowania OfficeSpace](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_configure.png) 

9. <span data-ttu-id="81950-195">W oknie przeglądarki innej witryny sieci web Zaloguj się do dzierżawy OfficeSpace oprogramowania jako administrator.</span><span class="sxs-lookup"><span data-stu-id="81950-195">In a different web browser window, log into your OfficeSpace Software tenant as an administrator.</span></span>

10. <span data-ttu-id="81950-196">Przejdź za**ustawienia** i kliknij przycisk **łączniki**.</span><span class="sxs-lookup"><span data-stu-id="81950-196">Go too**Settings** and click **Connectors**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_002.png)

11. <span data-ttu-id="81950-198">Kliknij przycisk **uwierzytelnianie SAML**.</span><span class="sxs-lookup"><span data-stu-id="81950-198">Click **SAML Authentication**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_003.png)

12. <span data-ttu-id="81950-200">W hello **uwierzytelnianie SAML** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="81950-200">In hello **SAML Authentication** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_004.png)

    <span data-ttu-id="81950-202">a.</span><span class="sxs-lookup"><span data-stu-id="81950-202">a.</span></span> <span data-ttu-id="81950-203">W hello **adres url wylogowania dostawcy** pole tekstowe, Wklej wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="81950-203">In hello **Logout provider url** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="81950-204">b.</span><span class="sxs-lookup"><span data-stu-id="81950-204">b.</span></span> <span data-ttu-id="81950-205">W hello **klienta idp docelowy adres url** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="81950-205">In hello **Client idp target url** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="81950-206">c.</span><span class="sxs-lookup"><span data-stu-id="81950-206">c.</span></span> <span data-ttu-id="81950-207">Wklej hello **odcisk palca** wartość, która została skopiowana z portalu Azure do hello **odcisk palca certyfikatu klienta IDP** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="81950-207">Paste hello **Thumbprint** value which you have copied from Azure portal, into hello **Client IDP certificate fingerprint** textbox.</span></span> 

    <span data-ttu-id="81950-208">d.</span><span class="sxs-lookup"><span data-stu-id="81950-208">d.</span></span> <span data-ttu-id="81950-209">Kliknij przycisk **Zapisz ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="81950-209">Click **Save Settings**.</span></span>


> [!TIP]
> <span data-ttu-id="81950-210">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="81950-210">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="81950-211">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="81950-211">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="81950-212">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="81950-212">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="81950-213">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="81950-213">Create an Azure AD test user</span></span>

<span data-ttu-id="81950-214">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="81950-214">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="81950-216">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="81950-216">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="81950-217">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="81950-217">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-officespace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="81950-219">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="81950-219">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-officespace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="81950-221">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="81950-221">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-officespace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="81950-223">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="81950-223">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-officespace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="81950-225">a.</span><span class="sxs-lookup"><span data-stu-id="81950-225">a.</span></span> <span data-ttu-id="81950-226">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="81950-226">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="81950-227">b.</span><span class="sxs-lookup"><span data-stu-id="81950-227">b.</span></span> <span data-ttu-id="81950-228">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="81950-228">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="81950-229">c.</span><span class="sxs-lookup"><span data-stu-id="81950-229">c.</span></span> <span data-ttu-id="81950-230">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="81950-230">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="81950-231">d.</span><span class="sxs-lookup"><span data-stu-id="81950-231">d.</span></span> <span data-ttu-id="81950-232">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="81950-232">Click **Create**.</span></span>
 
### <a name="create-a-officespace-software-test-user"></a><span data-ttu-id="81950-233">Tworzenie użytkownika testowego OfficeSpace oprogramowania</span><span class="sxs-lookup"><span data-stu-id="81950-233">Create a OfficeSpace Software test user</span></span>

<span data-ttu-id="81950-234">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta OfficeSpace oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="81950-234">hello objective of this section is toocreate a user called Britta Simon in OfficeSpace Software.</span></span> <span data-ttu-id="81950-235">Oprogramowanie OfficeSpace obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="81950-235">OfficeSpace Software supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="81950-236">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="81950-236">There is no action item for you in this section.</span></span> <span data-ttu-id="81950-237">Nowy użytkownik zostanie utworzony podczas próby tooaccess OfficeSpace oprogramowania, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="81950-237">A new user will be created during an attempt tooaccess OfficeSpace Software if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="81950-238">Jeśli potrzebujesz ręcznie toocreate użytkownika, należy tooContact [zespołem pomocy technicznej oprogramowania OfficeSpace](mailto:support@officespacesoftware.com).</span><span class="sxs-lookup"><span data-stu-id="81950-238">If you need toocreate an user manually, you need tooContact [OfficeSpace Software support team](mailto:support@officespacesoftware.com).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="81950-239">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="81950-239">Assign hello Azure AD test user</span></span>

<span data-ttu-id="81950-240">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooOfficeSpace oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="81950-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOfficeSpace Software.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="81950-242">**tooassign tooOfficeSpace Simona Britta oprogramowania, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="81950-242">**tooassign Britta Simon tooOfficeSpace Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="81950-243">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="81950-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="81950-245">Z listy aplikacji hello wybierz **oprogramowania OfficeSpace**.</span><span class="sxs-lookup"><span data-stu-id="81950-245">In hello applications list, select **OfficeSpace Software**.</span></span>

    ![Witaj oprogramowania OfficeSpace łącza na liście aplikacji hello](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_app.png)  

3. <span data-ttu-id="81950-247">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="81950-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="81950-249">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="81950-249">Click **Add** button.</span></span> <span data-ttu-id="81950-250">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="81950-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="81950-252">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="81950-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="81950-253">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="81950-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="81950-254">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="81950-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="81950-255">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="81950-255">Test single sign-on</span></span>

<span data-ttu-id="81950-256">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="81950-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="81950-257">Po kliknięciu hello oprogramowania OfficeSpace kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour OfficeSpace aplikacji.</span><span class="sxs-lookup"><span data-stu-id="81950-257">When you click hello OfficeSpace Software tile in hello Access Panel, you should get automatically signed-on tooyour OfficeSpace Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="81950-258">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="81950-258">Additional resources</span></span>

* [<span data-ttu-id="81950-259">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="81950-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="81950-260">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="81950-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_203.png

