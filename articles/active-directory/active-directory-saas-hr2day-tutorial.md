---
title: 'Samouczek: Integracji Azure Active Directory z HR2day przez Merces | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i HR2day przez Merces."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 257233767e1fddbaf115878cb0455acf61b2f5f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a><span data-ttu-id="dffb9-103">Samouczek: Integracji Azure Active Directory z HR2day przez Merces</span><span class="sxs-lookup"><span data-stu-id="dffb9-103">Tutorial: Azure Active Directory integration with HR2day by Merces</span></span>

<span data-ttu-id="dffb9-104">Z tego samouczka, dowiesz się, jak toointegrate HR2day przez Merces w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dffb9-104">In this tutorial, you learn how toointegrate HR2day by Merces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dffb9-105">Integracja z usługą Azure AD HR2day przez Merces zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="dffb9-105">Integrating HR2day by Merces with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dffb9-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooHR2day przez Merces.</span><span class="sxs-lookup"><span data-stu-id="dffb9-106">You can control in Azure AD who has access tooHR2day by Merces.</span></span>
- <span data-ttu-id="dffb9-107">Umożliwia użytkownikom tooautomatically uzyskać zalogowany tooHR2day przez Merces z konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dffb9-107">You can enable your users tooautomatically get signed in tooHR2day by Merces with their Azure AD accounts.</span></span>
- <span data-ttu-id="dffb9-108">Możesz zarządzać kont w jednej centralnej lokalizacji — Witaj portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="dffb9-108">You can manage your accounts in one central location--hello Azure portal.</span></span>

<span data-ttu-id="dffb9-109">Aby uzyskać więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dffb9-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dffb9-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dffb9-110">Prerequisites</span></span>

<span data-ttu-id="dffb9-111">tooconfigure integracji usługi Azure AD z HR2day przez Merces należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="dffb9-111">tooconfigure Azure AD integration with HR2day by Merces, you need hello following items:</span></span>

- <span data-ttu-id="dffb9-112">Subskrypcja usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dffb9-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="dffb9-113">HR2day przez Merces logowanie jednokrotne włączone subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="dffb9-113">An HR2day by Merces single sign-on enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="dffb9-114">Nie zaleca się, że przy użyciu hello tootest środowiska produkcyjnego kroków w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="dffb9-114">We don't recommend using a production environment tootest hello steps in this tutorial.</span></span>

<span data-ttu-id="dffb9-115">kroki hello tootest w tym samouczku, wykonaj te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="dffb9-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="dffb9-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="dffb9-116">Don't use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="dffb9-117">Pobierz [miesięczna bezpłatna wersja próbna usługi Azure AD](https://azure.microsoft.com/pricing/free-trial/) Jeśli jeszcze nie masz.</span><span class="sxs-lookup"><span data-stu-id="dffb9-117">Get a [one-month free trial of Azure AD](https://azure.microsoft.com/pricing/free-trial/) if you don't already have it.</span></span>  

## <a name="scenario-description"></a><span data-ttu-id="dffb9-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="dffb9-118">Scenario description</span></span>
<span data-ttu-id="dffb9-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="dffb9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dffb9-120">Scenariusz Hello jest opisana w tym temacie składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="dffb9-120">hello scenario that's outlined here consists of two main building blocks:</span></span>

1. <span data-ttu-id="dffb9-121">Dodawanie HR2day przez Merces z galerii hello.</span><span class="sxs-lookup"><span data-stu-id="dffb9-121">Adding HR2day by Merces from hello gallery.</span></span>
2. <span data-ttu-id="dffb9-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="dffb9-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-hr2day-by-merces-from-hello-gallery"></a><span data-ttu-id="dffb9-123">Dodaj HR2day przez Merces z galerii hello</span><span class="sxs-lookup"><span data-stu-id="dffb9-123">Add HR2day by Merces from hello gallery</span></span>
<span data-ttu-id="dffb9-124">tooconfigure hello integracji HR2day przez Merces do usługi Azure AD, Dodaj HR2day przez Merces hello galerii tooyour listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="dffb9-124">tooconfigure hello integration of HR2day by Merces into Azure AD, add HR2day by Merces from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dffb9-125">**tooadd HR2day przez Merces z galerii hello hello wykonaj następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="dffb9-125">**tooadd HR2day by Merces from hello gallery, take hello following steps:**</span></span>

1. <span data-ttu-id="dffb9-126">W hello [portalu Azure](https://portal.azure.com)na temat hello w lewym okienku nawigacji, wybierz hello **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="dffb9-126">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="dffb9-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="dffb9-128">Go too**Enterprise applications**.</span></span> <span data-ttu-id="dffb9-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="dffb9-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="dffb9-131">tooadd nowej aplikacji, wybierz opcję hello **nowej aplikacji** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dffb9-131">tooadd a new application, select hello **New application** button on hello top of hello dialog box.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="dffb9-133">W polu wyszukiwania hello wpisz **HR2day przez Merces**.</span><span class="sxs-lookup"><span data-stu-id="dffb9-133">In hello search box, type **HR2day by Merces**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. <span data-ttu-id="dffb9-135">W panelu wyników hello, wybierz **HR2day przez Merces**, a następnie wybierz hello **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="dffb9-135">In hello results panel, select **HR2day by Merces**, and then select hello **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="dffb9-137">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="dffb9-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="dffb9-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z HR2day przez Merces oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="dffb9-138">In this section, you configure and test Azure AD single sign-on with HR2day by Merces based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="dffb9-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow, który użytkownik odpowiednikiem hello w HR2day przez Merces jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dffb9-139">For single sign-on toowork, Azure AD needs tooknow who hello counterpart user in HR2day by Merces is tooa user in Azure AD.</span></span> <span data-ttu-id="dffb9-140">Innymi słowy należy tooestablish łącza między użytkownika usługi Azure AD i hello użytkownikowi w HR2day przez Merces.</span><span class="sxs-lookup"><span data-stu-id="dffb9-140">In other words, you need tooestablish a link between an Azure AD user and hello related user in HR2day by Merces.</span></span>

<span data-ttu-id="dffb9-141">HR2day przez Merces, przypisywanie hello **nazwy użytkownika** w usłudze Azure AD za **Username** tooestablish hello relacji.</span><span class="sxs-lookup"><span data-stu-id="dffb9-141">In HR2day by Merces, assign hello **user name** in Azure AD too **Username** tooestablish hello relationship.</span></span>

<span data-ttu-id="dffb9-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z HR2day przez Merces, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="dffb9-142">tooconfigure and test Azure AD single sign-on with HR2day by Merces, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dffb9-143">[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on): Włącz toouse Twojego użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="dffb9-143">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on): Enable your users toouse this feature.</span></span>
2. <span data-ttu-id="dffb9-144">[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user): Test usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="dffb9-144">[Create an Azure AD test user](#creating-an-azure-ad-test-user): Test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dffb9-145">[Utwórz HR2day przez użytkownika testowego Merces](#creating-an-hr2day-by-merces-test-user): tworzenie odpowiednikiem Simona Britta w HR2day przez Merces, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="dffb9-145">[Create an HR2day by Merces test user](#creating-an-hr2day-by-merces-test-user): Create a counterpart of Britta Simon in HR2day by Merces that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dffb9-146">[Przypisz użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user): Włącz Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="dffb9-146">[Assign hello Azure AD test user](#assigning-the-azure-ad-test-user): Enable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dffb9-147">[Test rejestracji jednokrotnej](#testing-single-sign-on): Sprawdź, czy konfiguracja hello działa.</span><span class="sxs-lookup"><span data-stu-id="dffb9-147">[Test single sign-on](#testing-single-sign-on): Verify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="dffb9-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="dffb9-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="dffb9-149">W tej sekcji włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w sieci HR2day przez aplikację Merces.</span><span class="sxs-lookup"><span data-stu-id="dffb9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HR2day by Merces application.</span></span>

<span data-ttu-id="dffb9-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z HR2day przez Merces, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="dffb9-150">**tooconfigure Azure AD single sign-on with HR2day by Merces, take hello following steps:**</span></span>

1. <span data-ttu-id="dffb9-151">W portalu Azure na powitania hello **HR2day przez Merces** strona integracji aplikacji, wybierz opcję **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="dffb9-151">In hello Azure portal, on hello **HR2day by Merces** application integration page, select **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="dffb9-153">tooenable logowanie jednokrotne, w hello **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="dffb9-153">tooenable single sign-on, in hello **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. <span data-ttu-id="dffb9-155">W hello **HR2day Merces domeny i adresy URL** sekcji, podjąć hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="dffb9-155">In hello **HR2day by Merces Domain and URLs** section, take hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    <span data-ttu-id="dffb9-157">a.</span><span class="sxs-lookup"><span data-stu-id="dffb9-157">a.</span></span> <span data-ttu-id="dffb9-158">W hello **adres URL logowania** wpisz adres URL przy użyciu hello następującego wzorca: `https://<tenantname>.force.com/<instancename>`.</span><span class="sxs-lookup"><span data-stu-id="dffb9-158">In hello **Sign-on URL** box, type a URL by using hello following pattern: `https://<tenantname>.force.com/<instancename>`.</span></span>

    <span data-ttu-id="dffb9-159">b.</span><span class="sxs-lookup"><span data-stu-id="dffb9-159">b.</span></span> <span data-ttu-id="dffb9-160">W hello **identyfikator** wpisz adres URL przy użyciu hello następującego wzorca: `https://hr2day.force.com/<companyname>`.</span><span class="sxs-lookup"><span data-stu-id="dffb9-160">In hello **Identifier** box, type a URL by using hello following pattern: `https://hr2day.force.com/<companyname>`.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dffb9-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="dffb9-161">These values are not real.</span></span> <span data-ttu-id="dffb9-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="dffb9-162">Update these values with hello actual sign-on URL and identifier.</span></span> <span data-ttu-id="dffb9-163">Skontaktuj się z pomocą hello [HR2day przez zespół pomocy technicznej klienta Merces](mailto:servicedesk@merces.nl) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="dffb9-163">Contact hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl) tooget these values.</span></span> 
 


4. <span data-ttu-id="dffb9-164">Na powitania **certyfikat podpisywania SAML** wybierz opcję **Certificate(Base64)**, a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="dffb9-164">On hello **SAML Signing Certificate** section, select **Certificate(Base64)**, and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. <span data-ttu-id="dffb9-166">W tej sekcji opisano sposób tooenable użytkowników tooauthenticate tooHR2day przez Merces do swojego konta w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dffb9-166">This section describes how tooenable users tooauthenticate tooHR2day by Merces with their account in Azure AD.</span></span> <span data-ttu-id="dffb9-167">One to robić przy użyciu Federacji opartego na powitania protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="dffb9-167">They do this by using federation that's based on hello SAML protocol.</span></span>

    <span data-ttu-id="dffb9-168">Twoje HR2day przez aplikację Merces oczekuje potwierdzenia SAML hello w określonym formacie, który wymaga tokenu SAML tooyour tooadd atrybutu niestandardowego mapowania.</span><span class="sxs-lookup"><span data-stu-id="dffb9-168">Your HR2day by Merces application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token.</span></span> <span data-ttu-id="dffb9-169">powitania po zrzut ekranu przedstawia przykład.</span><span class="sxs-lookup"><span data-stu-id="dffb9-169">hello following screenshot shows an example of this.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    <span data-ttu-id="dffb9-171">Aby można było skonfigurować potwierdzenia języka SAML hello, musisz skontaktować się z hello [HR2day przez zespół pomocy technicznej klienta Merces](mailto:servicedesk@merces.nl) i zażądać hello wartość hello atrybut identyfikator unikatowy dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="dffb9-171">Before you can configure hello SAML assertion, you must contact hello [HR2day by Merces Client support team](mailto:servicedesk@merces.nl) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="dffb9-172">Należy to wartość toocomplete hello kroki opisane w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="dffb9-172">You need this value toocomplete hello steps in hello next section.</span></span> 

6. <span data-ttu-id="dffb9-173">W hello **logowanie jednokrotne** okno dialogowe, w hello **atrybuty użytkownika** skonfiguruj atrybut tokenu SAML hello, jak pokazano w powitania po obrazu.</span><span class="sxs-lookup"><span data-stu-id="dffb9-173">In hello **Single sign-on** dialog box, in hello **User Attributes** section, configure hello SAML token attribute as shown in hello following image.</span></span> <span data-ttu-id="dffb9-174">Wykonaj następujące kroki hello.</span><span class="sxs-lookup"><span data-stu-id="dffb9-174">Then take hello following steps.</span></span>
    
      | <span data-ttu-id="dffb9-175">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="dffb9-175">Attribute name</span></span>    |   <span data-ttu-id="dffb9-176">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="dffb9-176">Attribute value</span></span> |  
    | ------------------- | -------------------- |    
    | <span data-ttu-id="dffb9-177">ATTR_LOGINCLAIM</span><span class="sxs-lookup"><span data-stu-id="dffb9-177">ATTR_LOGINCLAIM</span></span> | <span data-ttu-id="dffb9-178">sprzężenia ([poczty] "102938475Z", "@"</span><span class="sxs-lookup"><span data-stu-id="dffb9-178">join([mail],"102938475Z","@"</span></span> |
    
      <span data-ttu-id="dffb9-179">a.</span><span class="sxs-lookup"><span data-stu-id="dffb9-179">a.</span></span> <span data-ttu-id="dffb9-180">Witaj tooopen **Dodawanie atrybutu** okno dialogowe, wybierz opcję **Dodaj atrybut**.</span><span class="sxs-lookup"><span data-stu-id="dffb9-180">tooopen hello **Add Attribute** dialog, select **Add attribute**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="dffb9-183">b.</span><span class="sxs-lookup"><span data-stu-id="dffb9-183">b.</span></span> <span data-ttu-id="dffb9-184">W hello **nazwa** wpisz **ATTR_LOGINCLAIM**.</span><span class="sxs-lookup"><span data-stu-id="dffb9-184">In hello **Name** box, type **ATTR_LOGINCLAIM**.</span></span>

    <span data-ttu-id="dffb9-185">c.</span><span class="sxs-lookup"><span data-stu-id="dffb9-185">c.</span></span> <span data-ttu-id="dffb9-186">Z hello **wartość** listy, wybierz **Join()**.</span><span class="sxs-lookup"><span data-stu-id="dffb9-186">From hello **Value** list, select **Join()**.</span></span>

    <span data-ttu-id="dffb9-187">d.</span><span class="sxs-lookup"><span data-stu-id="dffb9-187">d.</span></span> <span data-ttu-id="dffb9-188">Z hello **ciąg1** listy, wybierz **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="dffb9-188">From hello **String1** list, select **user.mail**.</span></span>

    <span data-ttu-id="dffb9-189">e.</span><span class="sxs-lookup"><span data-stu-id="dffb9-189">e.</span></span> <span data-ttu-id="dffb9-190">Aby uzyskać **ciąg2**, hello unikatowego identyfikatora dostarczonego przez zespół HR2day.</span><span class="sxs-lookup"><span data-stu-id="dffb9-190">For **String2**, type hello unique identifier that's provided by your HR2day team.</span></span>

    <span data-ttu-id="dffb9-191">f.</span><span class="sxs-lookup"><span data-stu-id="dffb9-191">f.</span></span> <span data-ttu-id="dffb9-192">W hello **separatora** wpisz  **@** .</span><span class="sxs-lookup"><span data-stu-id="dffb9-192">In hello **Separator** box, type **@**.</span></span>
    
    <span data-ttu-id="dffb9-193">g.</span><span class="sxs-lookup"><span data-stu-id="dffb9-193">g.</span></span> <span data-ttu-id="dffb9-194">Wybierz **Ok**.</span><span class="sxs-lookup"><span data-stu-id="dffb9-194">Select **Ok**.</span></span>

7. <span data-ttu-id="dffb9-195">Wybierz hello **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="dffb9-195">Select hello **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="dffb9-197">W hello **HR2day przez konfigurację Merces** zaznacz **skonfigurować HR2day przez Merces** tooopen hello **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="dffb9-197">In hello **HR2day by Merces Configuration** section, select **Configure HR2day by Merces** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="dffb9-198">Kopiuj hello **Sign-Out adres URL**, **SAML identyfikator jednostki**, i **SAML pojedynczy znak na adres URL usługi** z hello **krótki przewodnik** sekcji.</span><span class="sxs-lookup"><span data-stu-id="dffb9-198">Copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** from hello **Quick Reference** section.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. <span data-ttu-id="dffb9-200">tooconfigure logowania jednokrotnego dla twojej aplikacji, skontaktuj się z hello [HR2day przez zespół pomocy technicznej klienta Merces](mailTo:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="dffb9-200">tooconfigure SSO  for your application, contact hello [HR2day by Merces client support team](mailTo:servicedesk@merces.nl).</span></span> <span data-ttu-id="dffb9-201">Dołącz hello pobrane **Certificate(Base64)** pliku tooyour wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="dffb9-201">Attach hello downloaded **Certificate(Base64)** file tooyour email.</span></span> <span data-ttu-id="dffb9-202">Udostępniają hello **Sign-Out URL**, **identyfikator jednostki SAML**, i **SAML pojedynczy znak na adres URL usługi** tak, aby można je skonfigurować integracji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="dffb9-202">Also provide hello **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** so that they can be configured for SSO integration.</span></span>

    > [!NOTE]
    ><span data-ttu-id="dffb9-203">Wspomina toohello Merces zespół, który wymaga tej integracji hello toobe identyfikator jednostki ustawiony za pomocą wzorca hello **https://hr2day.force.com/INSTANCENAME**.</span><span class="sxs-lookup"><span data-stu-id="dffb9-203">Mention toohello Merces team that this integration needs hello Entity ID toobe set with hello pattern **https://hr2day.force.com/INSTANCENAME**.</span></span>

    > [!TIP]
    ><span data-ttu-id="dffb9-204">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="dffb9-204">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dffb9-205">Po dodaniu tej aplikacji z hello **usługi Active Directory** > **aplikacje dla przedsiębiorstw** sekcji, wybierz hello **rejestracji jednokrotnej** kartę. Witaj dostęp osadzone dokumentacji za pośrednictwem hello **konfiguracji** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="dffb9-205">After you add this app from hello **Active Directory** > **Enterprise Applications** section, select hello **Single Sign-On** tab. Then access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dffb9-206">Więcej o hello osadzonych dokumentacji funkcji w hello [usługi Azure AD osadzonych dokumentacji]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="dffb9-206">You can read more about hello embedded documentation feature in hello [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="dffb9-207">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="dffb9-207">Create an Azure AD test user</span></span>
<span data-ttu-id="dffb9-208">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="dffb9-208">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="dffb9-210">**toocreate użytkownika testowego w usłudze Azure AD, hello wykonaj następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="dffb9-210">**toocreate a test user in Azure AD, take hello following steps:**</span></span>

1. <span data-ttu-id="dffb9-211">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, wybierz hello **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="dffb9-211">In hello **Azure portal**, on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dffb9-213">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie wybierz **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="dffb9-213">toodisplay hello list of users, go too**Users and groups**, and then select **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dffb9-215">Witaj tooopen **użytkownika** wybierz pozycję **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dffb9-215">tooopen hello **User** dialog box, select **Add** on hello top of hello dialog box.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dffb9-217">W hello **użytkownika** okno dialogowe, hello wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="dffb9-217">In hello **User** dialog box, take hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dffb9-219">a.</span><span class="sxs-lookup"><span data-stu-id="dffb9-219">a.</span></span> <span data-ttu-id="dffb9-220">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dffb9-220">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dffb9-221">b.</span><span class="sxs-lookup"><span data-stu-id="dffb9-221">b.</span></span> <span data-ttu-id="dffb9-222">W hello **nazwy użytkownika** okno, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dffb9-222">In hello **User name** box, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dffb9-223">c.</span><span class="sxs-lookup"><span data-stu-id="dffb9-223">c.</span></span> <span data-ttu-id="dffb9-224">Wybierz **Pokaż hasło**, a następnie Zapisz hasło hello.</span><span class="sxs-lookup"><span data-stu-id="dffb9-224">Select **Show Password**, and then write down hello password.</span></span>

    <span data-ttu-id="dffb9-225">d.</span><span class="sxs-lookup"><span data-stu-id="dffb9-225">d.</span></span> <span data-ttu-id="dffb9-226">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="dffb9-226">Select **Create**.</span></span>
 
### <a name="create-an-hr2day-by-merces-test-user"></a><span data-ttu-id="dffb9-227">Utwórz HR2day przez Merces użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="dffb9-227">Create an HR2day by Merces test user</span></span>

<span data-ttu-id="dffb9-228">Celem Hello w tej sekcji jest toocreate użytkownik wywołał Simona Britta w HR2day Merces.</span><span class="sxs-lookup"><span data-stu-id="dffb9-228">hello objective of this section is toocreate a user called Britta Simon in HR2day by Merces.</span></span> <span data-ttu-id="dffb9-229">Użytkownicy hello tooadd na koncie hello HR2day pracować z hello [HR2day przez zespół pomocy technicznej klienta Merces](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="dffb9-229">tooadd hello users in hello HR2day account, work with hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span> 

> [!NOTE]
> <span data-ttu-id="dffb9-230">Toocreate użytkownik ręcznie, należy skontaktować się z hello [HR2day przez zespół pomocy technicznej klienta Merces](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="dffb9-230">If you need toocreate a user manually, contact hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="dffb9-231">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="dffb9-231">Assign hello Azure AD test user</span></span>

<span data-ttu-id="dffb9-232">W tej sekcji zostanie włączone, przyznając jej tooHR2day dostępu przez Merces toouse Simona Britta Azure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="dffb9-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooHR2day by Merces.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="dffb9-234">**tooassign tooHR2day Simona Britta przez Merces, hello wykonaj następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="dffb9-234">**tooassign Britta Simon tooHR2day by Merces, take hello following steps:**</span></span>

1. <span data-ttu-id="dffb9-235">W hello Azure aplikacji hello portalu, otwórz wyświetlić, przejdź do widoku katalogu toohello, a następnie przejdź zbyt**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="dffb9-235">In hello Azure portal, open hello applications view, go toohello directory view, and then go too**Enterprise applications**.</span></span> <span data-ttu-id="dffb9-236">Następnie wybierz pozycję **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="dffb9-236">Next, select **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="dffb9-238">Z listy aplikacji hello wybierz **HR2day przez Merces**.</span><span class="sxs-lookup"><span data-stu-id="dffb9-238">In hello applications list, select **HR2day by Merces**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. <span data-ttu-id="dffb9-240">W menu hello powitania po lewej stronie wybierz **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="dffb9-240">In hello menu on hello left, select **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="dffb9-242">Wybierz hello **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="dffb9-242">Select hello **Add** button.</span></span> <span data-ttu-id="dffb9-243">Następnie w hello **Dodaj przydziału** okno dialogowe, wybierz opcję **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="dffb9-243">Then, in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="dffb9-245">W hello **użytkowników i grup** okno dialogowe, w hello **użytkowników** listy, wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="dffb9-245">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="dffb9-246">Kliknij przycisk hello **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="dffb9-246">Click hello **Select** button.</span></span>

7. <span data-ttu-id="dffb9-247">W hello **Dodaj przydziału** okno dialogowe, wybierz opcję **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="dffb9-247">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="dffb9-248">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="dffb9-248">Test single sign-on</span></span>

<span data-ttu-id="dffb9-249">Witaj celem tej sekcji jest tootest konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="dffb9-249">hello objective of this section is tootest your Azure AD single sign-on configuration by using hello Access Panel.</span></span>  

<span data-ttu-id="dffb9-250">Po wybraniu hello HR2day przez Kafelek Merces w panelu dostępu hello automatycznie pobrać zalogowano tooyour HR2day przez aplikację Merces.</span><span class="sxs-lookup"><span data-stu-id="dffb9-250">When you select hello HR2day by Merces tile in hello Access Panel, you automatically get signed in  tooyour HR2day by Merces application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dffb9-251">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="dffb9-251">Additional resources</span></span>

* [<span data-ttu-id="dffb9-252">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dffb9-252">List of tutorials about how tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dffb9-253">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dffb9-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

