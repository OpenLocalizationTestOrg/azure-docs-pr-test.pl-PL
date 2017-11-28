---
title: 'Samouczek: Integracji Azure Active Directory z Cisco Spark | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Cisco Spark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c47894b1-f5df-4755-845d-f12f4c602dc4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 386c4fd816095e1c61de01dd1dee1bbd00311a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-spark"></a><span data-ttu-id="5a681-103">Samouczek: Integracji Azure Active Directory z Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="5a681-103">Tutorial: Azure Active Directory integration with Cisco Spark</span></span>

<span data-ttu-id="5a681-104">Z tego samouczka, dowiesz się, jak toointegrate Cisco Spark w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5a681-104">In this tutorial, you learn how toointegrate Cisco Spark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5a681-105">Integracja z usługą Azure AD Cisco Spark zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5a681-105">Integrating Cisco Spark with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5a681-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooCisco Spark</span><span class="sxs-lookup"><span data-stu-id="5a681-106">You can control in Azure AD who has access tooCisco Spark</span></span>
- <span data-ttu-id="5a681-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooCisco Spark (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a681-107">You can enable your users tooautomatically get signed-on tooCisco Spark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5a681-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5a681-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5a681-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5a681-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a681-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5a681-110">Prerequisites</span></span>

<span data-ttu-id="5a681-111">tooconfigure integracji usługi Azure AD z Cisco Spark należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5a681-111">tooconfigure Azure AD integration with Cisco Spark, you need hello following items:</span></span>

- <span data-ttu-id="5a681-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a681-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5a681-113">Cisco Spark logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5a681-113">A Cisco Spark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5a681-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5a681-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5a681-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5a681-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5a681-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5a681-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5a681-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5a681-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5a681-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5a681-118">Scenario description</span></span>
<span data-ttu-id="5a681-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5a681-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5a681-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5a681-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5a681-121">Dodawanie Cisco Spark z galerii hello</span><span class="sxs-lookup"><span data-stu-id="5a681-121">Adding Cisco Spark from hello gallery</span></span>
2. <span data-ttu-id="5a681-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5a681-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cisco-spark-from-hello-gallery"></a><span data-ttu-id="5a681-123">Dodawanie Cisco Spark z galerii hello</span><span class="sxs-lookup"><span data-stu-id="5a681-123">Adding Cisco Spark from hello gallery</span></span>
<span data-ttu-id="5a681-124">tooconfigure hello integracji Cisco Spark w usłudze Azure Active Directory, należy tooadd Cisco Spark z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5a681-124">tooconfigure hello integration of Cisco Spark into Azure AD, you need tooadd Cisco Spark from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5a681-125">**tooadd Spark Cisco z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5a681-125">**tooadd Cisco Spark from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a681-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5a681-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="5a681-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5a681-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5a681-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5a681-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="5a681-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5a681-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="5a681-133">W polu wyszukiwania hello wpisz **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="5a681-133">In hello search box, type **Cisco Spark**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_search.png)

5. <span data-ttu-id="5a681-135">W panelu wyników hello, wybierz **Cisco Spark**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5a681-135">In hello results panel, select **Cisco Spark**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5a681-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5a681-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5a681-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Cisco Spark oparty na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="5a681-138">In this section, you configure and test Azure AD single sign-on with Cisco Spark based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5a681-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Cisco Spark jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a681-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cisco Spark is tooa user in Azure AD.</span></span> <span data-ttu-id="5a681-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w łączniku Spark Cisco musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="5a681-140">In other words, a link relationship between an Azure AD user and hello related user in Cisco Spark needs toobe established.</span></span>

<span data-ttu-id="5a681-141">W łączniku Spark Cisco, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="5a681-141">In Cisco Spark, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5a681-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Cisco Spark, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="5a681-142">tooconfigure and test Azure AD single sign-on with Cisco Spark, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5a681-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5a681-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5a681-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5a681-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5a681-145">**[Tworzenie użytkownika testowego Cisco Spark](#creating-a-cisco-spark-test-user)**  -toohave odpowiednikiem Simona Britta w łączniku Spark Cisco, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5a681-145">**[Creating a Cisco Spark test user](#creating-a-cisco-spark-test-user)** - toohave a counterpart of Britta Simon in Cisco Spark that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5a681-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5a681-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5a681-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="5a681-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5a681-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5a681-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5a681-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="5a681-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cisco Spark application.</span></span>

<span data-ttu-id="5a681-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Cisco Spark wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5a681-150">**tooconfigure Azure AD single sign-on with Cisco Spark, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a681-151">W portalu Azure na powitania hello **Cisco Spark** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="5a681-151">In hello Azure portal, on hello **Cisco Spark** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="5a681-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5a681-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_samlbase.png)

3. <span data-ttu-id="5a681-155">Na powitania **Cisco Spark domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="5a681-155">On hello **Cisco Spark Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_url.png)

    <span data-ttu-id="5a681-157">a.</span><span class="sxs-lookup"><span data-stu-id="5a681-157">a.</span></span> <span data-ttu-id="5a681-158">W hello **adres URL logowania** tekstowym, wpisz adres URL jako:`https://web.ciscospark.com/#/signin`</span><span class="sxs-lookup"><span data-stu-id="5a681-158">In hello **Sign-on URL** textbox, type a URL as: `https://web.ciscospark.com/#/signin`</span></span>

    <span data-ttu-id="5a681-159">b.</span><span class="sxs-lookup"><span data-stu-id="5a681-159">b.</span></span> <span data-ttu-id="5a681-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://idbroker.webex.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="5a681-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://idbroker.webex.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5a681-161">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="5a681-161">This value is not real.</span></span> <span data-ttu-id="5a681-162">Zaktualizuj tę wartość z hello rzeczywisty identyfikator.</span><span class="sxs-lookup"><span data-stu-id="5a681-162">Update this value with hello actual Identifier.</span></span> <span data-ttu-id="5a681-163">Skontaktuj się z [zespołem pomocy technicznej klienta Spark Cisco](https://support.ciscospark.com/) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="5a681-163">Contact [Cisco Spark Client support team](https://support.ciscospark.com/) tooget this value.</span></span> 
 
4. <span data-ttu-id="5a681-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5a681-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_certificate.png) 

5. <span data-ttu-id="5a681-166">Aplikacji Spark Cisco oczekuje hello SAML potwierdzenia toocontain określonych atrybutów.</span><span class="sxs-lookup"><span data-stu-id="5a681-166">Cisco Spark application expects hello SAML assertions toocontain specific attributes.</span></span> <span data-ttu-id="5a681-167">Skonfiguruj hello następujące atrybuty dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5a681-167">Configure hello following attributes  for this application.</span></span> <span data-ttu-id="5a681-168">Można zarządzać hello wartości tych atrybutów z hello **atrybuty użytkownika** sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5a681-168">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span> <span data-ttu-id="5a681-169">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="5a681-169">hello following screenshot shows an example for this.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_07.png) 

6. <span data-ttu-id="5a681-171">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w powyższy obraz powitania i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5a681-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="5a681-172">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="5a681-172">Attribute Name</span></span>  | <span data-ttu-id="5a681-173">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="5a681-173">Attribute Value</span></span> |
    | --------------- | -------------------- |    
    |   <span data-ttu-id="5a681-174">Identyfikator UID</span><span class="sxs-lookup"><span data-stu-id="5a681-174">uid</span></span>    | <span data-ttu-id="5a681-175">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="5a681-175">user.userprincipalname</span></span> |   

    <span data-ttu-id="5a681-176">a.</span><span class="sxs-lookup"><span data-stu-id="5a681-176">a.</span></span> <span data-ttu-id="5a681-177">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5a681-177">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-spark-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="5a681-180">b.</span><span class="sxs-lookup"><span data-stu-id="5a681-180">b.</span></span> <span data-ttu-id="5a681-181">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="5a681-181">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="5a681-182">c.</span><span class="sxs-lookup"><span data-stu-id="5a681-182">c.</span></span> <span data-ttu-id="5a681-183">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="5a681-183">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="5a681-184">d.</span><span class="sxs-lookup"><span data-stu-id="5a681-184">d.</span></span> <span data-ttu-id="5a681-185">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="5a681-185">Click **Ok**.</span></span>

7. <span data-ttu-id="5a681-186">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5a681-186">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="5a681-188">Zaloguj się za[zarządzania współpracy chmury Cisco](https://admin.ciscospark.com/) przy użyciu poświadczeń administratora pełnego.</span><span class="sxs-lookup"><span data-stu-id="5a681-188">Sign in too[Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

9. <span data-ttu-id="5a681-189">Wybierz **ustawienia** i w obszarze hello **uwierzytelniania** kliknij **Modyfikuj**.</span><span class="sxs-lookup"><span data-stu-id="5a681-189">Select **Settings** and under hello **Authentication** section, click **Modify**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_10.png)
    
10. <span data-ttu-id="5a681-191">Wybierz **dostawcy tożsamości firm 3rd integracji. (Zaawansowane)**  i toohello Przejdź dalej ekranu.</span><span class="sxs-lookup"><span data-stu-id="5a681-191">Select **Integrate a 3rd-party identity provider. (Advanced)** and go toohello next screen.</span></span>

11. <span data-ttu-id="5a681-192">Na powitania **Importowanie metadanych Idp** strony albo przeciągania i upuszczania pliku metadanych hello Azure AD na stronę hello lub hello pliku przeglądarki opcja toolocate i przekazać plik metadanych hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a681-192">On hello **Import Idp Metadata** page, either drag and drop hello Azure AD metadata file onto hello page or use hello file browser option toolocate and upload hello Azure AD metadata file.</span></span> <span data-ttu-id="5a681-193">Następnie wybierz opcję **wymagają certyfikatu podpisanego przez urząd certyfikacji w metadanych (bardziej bezpieczny)** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="5a681-193">Then, select **Require certificate signed by a certificate authority in Metadata (more secure)** and click **Next**.</span></span> 
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_11.png)

12. <span data-ttu-id="5a681-195">Wybierz **Test rejestracji Jednokrotnej połączenia**i po otwarciu nowej karty przeglądarki uwierzytelniania za pomocą usługi Azure AD logując się.</span><span class="sxs-lookup"><span data-stu-id="5a681-195">Select **Test SSO Connection**, and when a new browser tab opens, authenticate with Azure AD by signing in.</span></span>

13. <span data-ttu-id="5a681-196">Zwraca toohello **zarządzania współpracy chmury Cisco** karty przeglądarki. Jeśli hello test zakończyło się pomyślnie, wybierz **ten test zakończyła się pomyślnie. Włącz opcję logowania jednokrotnego** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="5a681-196">Return toohello **Cisco Cloud Collaboration Management** browser tab. If hello test was successful, select **This test was successful. Enable Single Sign-On option** and click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="5a681-197">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="5a681-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5a681-198">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="5a681-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5a681-199">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5a681-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5a681-200">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a681-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="5a681-201">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="5a681-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="5a681-203">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5a681-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a681-204">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5a681-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5a681-206">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="5a681-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5a681-208">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5a681-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5a681-210">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5a681-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cisco-spark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5a681-212">a.</span><span class="sxs-lookup"><span data-stu-id="5a681-212">a.</span></span> <span data-ttu-id="5a681-213">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5a681-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5a681-214">b.</span><span class="sxs-lookup"><span data-stu-id="5a681-214">b.</span></span> <span data-ttu-id="5a681-215">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5a681-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5a681-216">c.</span><span class="sxs-lookup"><span data-stu-id="5a681-216">c.</span></span> <span data-ttu-id="5a681-217">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="5a681-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5a681-218">d.</span><span class="sxs-lookup"><span data-stu-id="5a681-218">d.</span></span> <span data-ttu-id="5a681-219">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5a681-219">Click **Create**.</span></span>
 
### <a name="creating-a-cisco-spark-test-user"></a><span data-ttu-id="5a681-220">Tworzenie użytkownika testowego Cisco Spark</span><span class="sxs-lookup"><span data-stu-id="5a681-220">Creating a Cisco Spark test user</span></span>

<span data-ttu-id="5a681-221">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="5a681-221">In this section, you create a user called Britta Simon in Cisco Spark.</span></span> <span data-ttu-id="5a681-222">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Cisco Spark.</span><span class="sxs-lookup"><span data-stu-id="5a681-222">In this section, you create a user called Britta Simon in Cisco Spark.</span></span>

1. <span data-ttu-id="5a681-223">Przejdź toohello [zarządzania współpracy chmury Cisco](https://admin.ciscospark.com/) przy użyciu poświadczeń administratora pełnego.</span><span class="sxs-lookup"><span data-stu-id="5a681-223">Go toohello [Cisco Cloud Collaboration Management](https://admin.ciscospark.com/) with your full administrator credentials.</span></span>

2. <span data-ttu-id="5a681-224">Kliknij przycisk **użytkowników** , a następnie **Zarządzanie użytkownikami**.</span><span class="sxs-lookup"><span data-stu-id="5a681-224">Click **Users** and then **Manage Users**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_12.png) 

3. <span data-ttu-id="5a681-226">W hello **zarządzania użytkownika** wybierz **ręcznego dodawania lub modyfikowania użytkowników** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="5a681-226">In hello **Manage User** window, select **Manually add or modify users** and click **Next**.</span></span>

4. <span data-ttu-id="5a681-227">Wybierz **nazwy i adresu E-mail**.</span><span class="sxs-lookup"><span data-stu-id="5a681-227">Select **Names and Email address**.</span></span> <span data-ttu-id="5a681-228">Następnie wypełnij pole tekstowe hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="5a681-228">Then, fill out hello textbox as follows:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-spark-tutorial/tutorial_cisco_spark_13.png) 
    
    <span data-ttu-id="5a681-230">a.</span><span class="sxs-lookup"><span data-stu-id="5a681-230">a.</span></span> <span data-ttu-id="5a681-231">W hello **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="5a681-231">In hello **First Name** textbox, type **Britta**.</span></span> 
    
    <span data-ttu-id="5a681-232">b.</span><span class="sxs-lookup"><span data-stu-id="5a681-232">b.</span></span> <span data-ttu-id="5a681-233">W hello **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="5a681-233">In hello **Last Name** textbox, type **Simon**.</span></span>
    
    <span data-ttu-id="5a681-234">c.</span><span class="sxs-lookup"><span data-stu-id="5a681-234">c.</span></span> <span data-ttu-id="5a681-235">W hello **adres E-mail** pole tekstowe, typ  **britta.simon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="5a681-235">In hello **Email address** textbox, type **britta.simon@contoso.com**.</span></span>

5. <span data-ttu-id="5a681-236">Kliknij przycisk hello oraz zarejestrować tooadd Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5a681-236">Click hello plus sign tooadd Britta Simon.</span></span> <span data-ttu-id="5a681-237">Następnie kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="5a681-237">Then, click **Next**.</span></span>

6. <span data-ttu-id="5a681-238">W hello **Dodaj usługi dla użytkowników** okna, kliknij przycisk **zapisać** , a następnie **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="5a681-238">In hello **Add Services for Users** window, click **Save** and then **Finish**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5a681-239">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5a681-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5a681-240">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooCisco Spark.</span><span class="sxs-lookup"><span data-stu-id="5a681-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCisco Spark.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="5a681-242">**tooassign tooCisco Simona Britta Spark, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5a681-242">**tooassign Britta Simon tooCisco Spark, perform hello following steps:**</span></span>

1. <span data-ttu-id="5a681-243">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5a681-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5a681-245">Z listy aplikacji hello wybierz **Cisco Spark**.</span><span class="sxs-lookup"><span data-stu-id="5a681-245">In hello applications list, select **Cisco Spark**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cisco-spark-tutorial/tutorial_ciscospark_app.png) 

3. <span data-ttu-id="5a681-247">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5a681-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="5a681-249">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5a681-249">Click **Add** button.</span></span> <span data-ttu-id="5a681-250">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5a681-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="5a681-252">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5a681-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5a681-253">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5a681-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5a681-254">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5a681-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5a681-255">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5a681-255">Testing single sign-on</span></span>

<span data-ttu-id="5a681-256">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5a681-256">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="5a681-257">Po kliknięciu kafelka Cisco Spark hello w hello Panel dostępu, należy pobrać aplikacji Cisco Spark tooyour zalogowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="5a681-257">When you click hello Cisco Spark tile in hello Access Panel, you should get automatically signed-on tooyour Cisco Spark application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5a681-258">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5a681-258">Additional resources</span></span>

* [<span data-ttu-id="5a681-259">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5a681-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5a681-260">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5a681-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_060.png
[100]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cisco-spark-tutorial/tutorial_general_203.png

