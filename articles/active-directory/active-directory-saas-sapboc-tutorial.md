---
title: 'Samouczek: Integracji Azure Active Directory z SAP Business obiektu chmury | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i SAP Business obiektu chmury."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: a3e9bd93897271531f91bcbc50cd361e8a20551e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a><span data-ttu-id="f6326-103">Samouczek: Integracji Azure Active Directory z SAP Business obiektu chmury</span><span class="sxs-lookup"><span data-stu-id="f6326-103">Tutorial: Azure Active Directory integration with SAP Business Object Cloud</span></span>

<span data-ttu-id="f6326-104">Z tego samouczka, dowiesz się, jak toointegrate SAP Business obiektu chmury z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f6326-104">In this tutorial, you learn how toointegrate SAP Business Object Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f6326-105">Możesz uzyskać hello następujące korzyści podczas integracji z usługą Azure AD SAP Business obiektu chmury:</span><span class="sxs-lookup"><span data-stu-id="f6326-105">You get hello following benefits when you integrate SAP Business Object Cloud with Azure AD:</span></span>

- <span data-ttu-id="f6326-106">W usłudze Azure AD można kontrolować, kto ma dostęp tooSAP firm obiektu chmury.</span><span class="sxs-lookup"><span data-stu-id="f6326-106">In Azure AD, you can control who has access tooSAP Business Object Cloud.</span></span>
- <span data-ttu-id="f6326-107">TooSAP Twojego użytkowników biznesowych obiektu chmury mogą automatycznie zaloguj przy użyciu rejestracji jednokrotnej i konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6326-107">You can automatically sign in your users tooSAP Business Object Cloud by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="f6326-108">Możesz zarządzać kont w jednej, centralnej lokalizacji, hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f6326-108">You can manage your accounts in one, central location, hello Azure portal.</span></span>

<span data-ttu-id="f6326-109">toolearn więcej informacji na temat oprogramowania jako usługa (SaaS) integracji aplikacji z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f6326-109">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6326-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f6326-110">Prerequisites</span></span>

<span data-ttu-id="f6326-111">tooset się integracji usługi Azure AD z SAP Business obiektu chmury, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="f6326-111">tooset up Azure AD integration with SAP Business Object Cloud, you need hello following items:</span></span>

- <span data-ttu-id="f6326-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6326-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f6326-113">Chmura obiektu SAP Business, z logowanie jednokrotne włączone</span><span class="sxs-lookup"><span data-stu-id="f6326-113">An SAP Business Object Cloud, with single sign-on turned on</span></span>

> [!NOTE]
> <span data-ttu-id="f6326-114">W przypadku testowania czynności hello w tym samouczku, zaleca się nie przetestować ich w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="f6326-114">If you test hello steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="f6326-115">Zalecenia dotyczące testowania czynności hello w tym samouczku:</span><span class="sxs-lookup"><span data-stu-id="f6326-115">Recommendations for testing hello steps in this tutorial:</span></span>

- <span data-ttu-id="f6326-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="f6326-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="f6326-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [Pobierz bezpłatną wersję próbną miesięcznego](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f6326-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f6326-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="f6326-118">Scenario description</span></span>
<span data-ttu-id="f6326-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="f6326-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="f6326-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="f6326-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f6326-121">Dodaj SAP Business obiektu chmury z galerii hello.</span><span class="sxs-lookup"><span data-stu-id="f6326-121">Add SAP Business Object Cloud from hello gallery.</span></span>
2. <span data-ttu-id="f6326-122">Instalowanie i testowanie usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f6326-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-sap-business-object-cloud-from-hello-gallery"></a><span data-ttu-id="f6326-123">Dodaj SAP Business obiektu chmury z galerii hello</span><span class="sxs-lookup"><span data-stu-id="f6326-123">Add SAP Business Object Cloud from hello gallery</span></span>
<span data-ttu-id="f6326-124">tooset się integracji hello SAP Business obiektu chmury z usługą Azure AD w galerii hello Dodaj SAP Business obiektu chmury tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="f6326-124">tooset up hello integration of SAP Business Object Cloud with Azure AD, in hello gallery, add SAP Business Object Cloud tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f6326-125">tooadd SAP Business obiektu chmury z galerii hello:</span><span class="sxs-lookup"><span data-stu-id="f6326-125">tooadd SAP Business Object Cloud from hello gallery:</span></span>

1. <span data-ttu-id="f6326-126">W hello [portalu Azure](https://portal.azure.com), w menu po lewej stronie Witaj, wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f6326-126">In hello [Azure portal](https://portal.azure.com), in hello left menu, select **Azure Active Directory**.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="f6326-128">Wybierz **aplikacje dla przedsiębiorstw**, a następnie wybierz **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f6326-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Strona aplikacji Hello Enterprise][2]
    
3. <span data-ttu-id="f6326-130">tooadd nowej aplikacji, wybierz **nowej aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="f6326-130">tooadd a new application, select **New application**.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="f6326-132">W polu wyszukiwania hello wpisz **SAP Business obiektu chmury**.</span><span class="sxs-lookup"><span data-stu-id="f6326-132">In hello search box, enter **SAP Business Object Cloud**.</span></span>

    ![pole wyszukiwania Hello](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. <span data-ttu-id="f6326-134">W panelu wyników hello zaznacz **SAP Business obiektu chmury**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="f6326-134">In hello results panel, select **SAP Business Object Cloud**, and then select **Add**.</span></span>

    ![SAP Business obiektu chmury hello listy wyników](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f6326-136">Instalowanie i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f6326-136">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="f6326-137">W tej sekcji możesz zdefiniować i test usługi Azure AD rejestracji jednokrotnej z SAP Business obiektu chmury w oparciu o nazwie użytkownika testowego *Simona Britta*.</span><span class="sxs-lookup"><span data-stu-id="f6326-137">In this section, you set up and test Azure AD single sign-on with SAP Business Object Cloud based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="f6326-138">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi użytkownika odpowiednikiem tooknow hello Azure AD w chmurze programu SAP Business obiektu.</span><span class="sxs-lookup"><span data-stu-id="f6326-138">For single sign-on toowork, Azure AD needs tooknow hello Azure AD counterpart user in SAP Business Object Cloud.</span></span> <span data-ttu-id="f6326-139">Należy ustanowić relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w chmurze programu SAP Business obiektu.</span><span class="sxs-lookup"><span data-stu-id="f6326-139">A link relationship between an Azure AD user and hello related user in SAP Business Object Cloud must be established.</span></span>

<span data-ttu-id="f6326-140">tooestablish hello połączyć relacji w SAP Business obiektu chmury, **Username**, przypisz wartość hello hello **nazwy użytkownika** w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6326-140">tooestablish hello link relationship, in SAP Business Object Cloud, for **Username**, assign hello value of hello **user name** in Azure AD.</span></span>

<span data-ttu-id="f6326-141">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z chmurą obiektu SAP Business, pełną hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="f6326-141">tooconfigure and test Azure AD single sign-on with SAP Business Object Cloud, complete hello following tasks:</span></span>

1. <span data-ttu-id="f6326-142">[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="f6326-142">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="f6326-143">Konfiguruje toouse użytkownika tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="f6326-143">Sets up a user toouse this feature.</span></span>
2. <span data-ttu-id="f6326-144">[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="f6326-144">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="f6326-145">Testy usługi Azure AD rejestracji jednokrotnej z użytkownikiem hello Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="f6326-145">Tests Azure AD single sign-on with hello user Britta Simon.</span></span>
3. <span data-ttu-id="f6326-146">[Tworzenie użytkownika testowego SAP Business obiektu chmury](#create-an-sap-business-object-cloud-test-user).</span><span class="sxs-lookup"><span data-stu-id="f6326-146">[Create an SAP Business Object Cloud test user](#create-an-sap-business-object-cloud-test-user).</span></span> <span data-ttu-id="f6326-147">Tworzy odpowiednikiem Simona Britta SAP Business obiektu chmurze, który jest połączony toohello reprezentacja hello użytkownika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6326-147">Creates a counterpart of Britta Simon in SAP Business Object Cloud that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="f6326-148">[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="f6326-148">[Assign hello Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="f6326-149">Konfiguruje toouse Simona Britta usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="f6326-149">Sets up Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f6326-150">[Test rejestracji jednokrotnej](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="f6326-150">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="f6326-151">Sprawdza, czy konfiguracja tego hello działa.</span><span class="sxs-lookup"><span data-stu-id="f6326-151">Verifies that hello configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="f6326-152">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f6326-152">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="f6326-153">W tej sekcji należy włączyć usługi Azure AD pojedynczego logowania jednokrotnego w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f6326-153">In this section, you turn on Azure AD single sign-on in hello Azure portal.</span></span> <span data-ttu-id="f6326-154">Następnie skonfigurowaniu rejestracji jednokrotnej w aplikacji SAP Business obiektu chmury.</span><span class="sxs-lookup"><span data-stu-id="f6326-154">Then, you set up single sign-on in your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="f6326-155">tooset się usługi Azure AD rejestracji jednokrotnej z SAP Business obiektu chmury:</span><span class="sxs-lookup"><span data-stu-id="f6326-155">tooset up Azure AD single sign-on with SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="f6326-156">W portalu Azure na powitania hello **SAP Business obiektu chmury** strona integracji aplikacji, wybierz opcję **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="f6326-156">In hello Azure portal, on hello **SAP Business Object Cloud** application integration page, select **Single sign-on**.</span></span>

    ![Wybierz rejestracji jednokrotnej][4]

2. <span data-ttu-id="f6326-158">Na powitania **logowanie jednokrotne** strony, dla **tryb**, wybierz pozycję **na języku SAML logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="f6326-158">On hello **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Wybierz na języku SAML logowania jednokrotnego](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. <span data-ttu-id="f6326-160">W obszarze **adresy URL i SAP Business obiektu chmury domeny**pełnego hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f6326-160">Under **SAP Business Object Cloud Domain and URLs**, complete hello following steps:</span></span>

    1. <span data-ttu-id="f6326-161">W hello **adres URL logowania** wprowadź adres URL, który ma hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="f6326-161">In hello **Sign-on URL** box, enter a URL that has hello following pattern:</span></span> 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. <span data-ttu-id="f6326-162">W hello **identyfikator** wprowadź adres URL, który ma hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="f6326-162">In hello **Identifier** box, enter a URL that has hello following pattern:</span></span>
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![Adresy URL i SAP Business obiektu chmury domeny adresów URL stron](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > <span data-ttu-id="f6326-164">wartości Hello w tych adresów URL dotyczą tylko pokaz.</span><span class="sxs-lookup"><span data-stu-id="f6326-164">hello values in these URLs are for demonstration only.</span></span> <span data-ttu-id="f6326-165">Aktualizacja hello wartościami hello rzeczywiste logowania jednokrotnego adres URL adresu URL i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="f6326-165">Update hello values with hello actual sign-on URL and identifier URL.</span></span> <span data-ttu-id="f6326-166">tooget hello adres URL logowania, skontaktuj się z pomocą hello [zespołem pomocy technicznej SAP Business obiektu chmury klienta](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span><span class="sxs-lookup"><span data-stu-id="f6326-166">tooget hello sign-on URL, contact hello [SAP Business Object Cloud Client support team](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span></span> <span data-ttu-id="f6326-167">Adres URL identyfikatora hello można uzyskać, pobierając hello SAP Business obiektu chmury metadanych z konsoli administracyjnej hello.</span><span class="sxs-lookup"><span data-stu-id="f6326-167">You can get hello identifier URL by downloading hello SAP Business Object Cloud metadata from hello admin console.</span></span> <span data-ttu-id="f6326-168">Wyjaśnienie jest zawarte w dalszej części samouczka hello.</span><span class="sxs-lookup"><span data-stu-id="f6326-168">This is explained later in hello tutorial.</span></span> 

4. <span data-ttu-id="f6326-169">W obszarze **certyfikat podpisywania SAML**, wybierz pozycję **XML metadanych**.</span><span class="sxs-lookup"><span data-stu-id="f6326-169">Under **SAML Signing Certificate**, select **Metadata XML**.</span></span> <span data-ttu-id="f6326-170">Następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="f6326-170">Then, save hello metadata file on your computer.</span></span>

    ![Wybierz XML metadanych](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. <span data-ttu-id="f6326-172">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="f6326-172">Select **Save**.</span></span>

    ![Wybierz opcję Zapisz](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f6326-174">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy SAP Business obiektu chmury tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="f6326-174">In a different web browser window, sign in tooyour SAP Business Object Cloud company site as an administrator.</span></span>

7. <span data-ttu-id="f6326-175">Wybierz **Menu** > **systemu** > **administracji**.</span><span class="sxs-lookup"><span data-stu-id="f6326-175">Select **Menu** > **System** > **Administration**.</span></span>
    
    ![Wybierz Menu, a następnie systemu, a następnie administracji](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. <span data-ttu-id="f6326-177">Na powitania **zabezpieczeń** kartę, zaznacz hello **Edytuj** ikona (pióra).</span><span class="sxs-lookup"><span data-stu-id="f6326-177">On hello **Security** tab, select hello **Edit** (pen) icon.</span></span>
    
    ![Na karcie Zabezpieczenia hello wybierz ikonę edycji hello](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. <span data-ttu-id="f6326-179">Aby uzyskać **metodę uwierzytelniania**, wybierz pozycję **SAML pojedynczego logowania jednokrotnego (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="f6326-179">For **Authentication Method**, select **SAML Single Sign-On (SSO)**.</span></span>

    ![Wybierz SAML logowania jednokrotnego dla metod uwierzytelniania hello](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. <span data-ttu-id="f6326-181">toodownload hello dostawcy metadanych usługi (krok 1), wybierz opcję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="f6326-181">toodownload hello service provider metadata (Step 1), select **Download**.</span></span> <span data-ttu-id="f6326-182">W pliku metadanych hello, należy znaleźć i skopiować hello **entityID** wartości.</span><span class="sxs-lookup"><span data-stu-id="f6326-182">In hello metadata file, find and copy hello **entityID** value.</span></span> <span data-ttu-id="f6326-183">W hello Azure portalu, w obszarze **adresy URL i SAP Business obiektu chmury domeny**, Wklej wartość hello hello **identyfikator** pole.</span><span class="sxs-lookup"><span data-stu-id="f6326-183">In hello Azure portal, under **SAP Business Object Cloud Domain and URLs**, paste hello value in hello **Identifier** box.</span></span>

    ![Skopiuj i Wklej hello entityID wartość](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. <span data-ttu-id="f6326-185">w obszarze hello tooupload hello dostawcy metadanych usługi (krok 2) w pliku hello, który został pobrany z portalu Azure, **metadanych Przekaż dostawcy tożsamości**, wybierz pozycję **przekazać**.</span><span class="sxs-lookup"><span data-stu-id="f6326-185">tooupload hello service provider metadata (Step 2) in hello file that you downloaded from hello Azure portal, under **Upload Identity Provider metadata**, select **Upload**.</span></span>  

    ![W obszarze metadanych Przekaż dostawcy tożsamości wybierz przekazywania](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. <span data-ttu-id="f6326-187">W hello **atrybut użytkownika** listy, wybierz hello atrybut użytkownika (krok 3) mają toouse implementacji.</span><span class="sxs-lookup"><span data-stu-id="f6326-187">In hello **User Attribute** list, select hello user attribute (Step 3) that you want toouse for your implementation.</span></span> <span data-ttu-id="f6326-188">Ten atrybut użytkownika mapuje toohello dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="f6326-188">This user attribute maps toohello identity provider.</span></span> <span data-ttu-id="f6326-189">Atrybut niestandardowy na stronie powitania użytkownika, użyj hello tooenter **niestandardowe mapowanie SAML** opcji.</span><span class="sxs-lookup"><span data-stu-id="f6326-189">tooenter a custom attribute on hello user's page, use hello **Custom SAML Mapping** option.</span></span> <span data-ttu-id="f6326-190">Lub użytkownik może wybrać jedną **E-mail** lub **identyfikator użytkownika** jako atrybut użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="f6326-190">Or, you can select either **Email** or **USER ID** as hello user attribute.</span></span> <span data-ttu-id="f6326-191">W naszym przykładzie wybrano **E-mail** możemy mapowane hello oświadczenia identyfikatora użytkownika z hello **userprincipalname** atrybutu w hello **atrybuty użytkownika** części hello Portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f6326-191">In our example, we selected **Email** because we mapped hello user identifier claim with hello **userprincipalname** attribute in hello **User Attributes** section in hello Azure portal.</span></span> <span data-ttu-id="f6326-192">Zapewnia to adres e-mail użytkownika unikatowy, który jest wysyłany toohello aplikacji w chmurze programu SAP Business obiektu w każdym pomyślnym odpowiedzi SAML.</span><span class="sxs-lookup"><span data-stu-id="f6326-192">This provides a unique user email, which is sent toohello SAP Business Object Cloud application in every successful SAML response.</span></span>

    ![Wybierz atrybut użytkownika](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. <span data-ttu-id="f6326-194">Konto hello tooverify z hello dostawcy tożsamości (krok 4) w hello **poświadczeń logowania (Poczta E-mail)** wprowadź adres e-mail użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="f6326-194">tooverify hello account with hello identity provider (Step 4), in hello **Login Credential (Email)** box, enter hello user's email address.</span></span> <span data-ttu-id="f6326-195">Następnie wybierz opcję **Sprawdź konto**.</span><span class="sxs-lookup"><span data-stu-id="f6326-195">Then, select **Verify Account**.</span></span> <span data-ttu-id="f6326-196">Hello system dodaje konto użytkownika toohello poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="f6326-196">hello system adds sign-in credentials toohello user account.</span></span>

    ![Wprowadź adres e-mail, a następnie wybierz zweryfikować konta](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. <span data-ttu-id="f6326-198">Wybierz hello **zapisać** ikony.</span><span class="sxs-lookup"><span data-stu-id="f6326-198">Select hello **Save** icon.</span></span>

    ![Zapisz](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="f6326-200">Możesz przeczytać zwięzły wersji tych instrukcji w hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="f6326-200">You can read a concise version of these instructions in hello [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="f6326-201">Po dodaniu aplikacji hello wybierając **usługi Active Directory** > **aplikacje dla przedsiębiorstw**, wybierz pozycję hello **rejestracji jednokrotnej** kartę. Dostęp można uzyskać dokumentację hello osadzone w hello **konfiguracji** sekcji u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="f6326-201">After you add hello app by selecting **Active Directory** > **Enterprise Applications**, select hello **Single Sign-On** tab. You can access hello embedded documentation in hello **Configuration** section, at hello bottom of hello page.</span></span> <span data-ttu-id="f6326-202">Aby uzyskać więcej informacji, zobacz [usługi Azure AD osadzonych dokumentacji]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="f6326-202">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f6326-203">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6326-203">Create an Azure AD test user</span></span>
<span data-ttu-id="f6326-204">W tej sekcji utworzysz użytkownika testu o nazwie Simona Britta w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f6326-204">In this section, you create a test user named Britta Simon in hello Azure portal.</span></span>

<span data-ttu-id="f6326-205">toocreate użytkownika testowego w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="f6326-205">toocreate a test user in Azure AD:</span></span>

1. <span data-ttu-id="f6326-206">W portalu Azure, w menu po lewej stronie powitania hello wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f6326-206">In hello Azure portal, in hello left menu, select **Azure Active Directory**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f6326-208">toodisplay hello listę użytkowników, wybierz opcję **użytkowników i grup**, a następnie wybierz **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="f6326-208">toodisplay hello list of users, select **Users and groups**, and then select **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f6326-210">Witaj tooopen **użytkownika** okno dialogowe, wybierz opcję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="f6326-210">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f6326-212">W hello **użytkownika** okno dialogowe, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f6326-212">In hello **User** dialog box, complete hello following steps:</span></span>
 
    1. <span data-ttu-id="f6326-213">W hello **nazwa** wprowadź **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f6326-213">In hello **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="f6326-214">W hello **nazwy użytkownika** wprowadź adres e-mail użytkownika hello Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="f6326-214">In hello **User name** box, enter hello email address of hello user Britta Simon.</span></span>

    3. <span data-ttu-id="f6326-215">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="f6326-215">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    4. <span data-ttu-id="f6326-216">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f6326-216">Select **Create**.</span></span>

        ![okno dialogowe Hello użytkownika](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![Tworzenie użytkowników usługi Azure AD][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a><span data-ttu-id="f6326-219">Tworzenie użytkownika testowego SAP Business obiektu chmury</span><span class="sxs-lookup"><span data-stu-id="f6326-219">Create an SAP Business Object Cloud test user</span></span>

<span data-ttu-id="f6326-220">Użytkownicy usługi Azure AD należy udostępnić w chmurze programu SAP Business obiektu przed móc zalogować się tooSAP firm obiektu chmury.</span><span class="sxs-lookup"><span data-stu-id="f6326-220">Azure AD users must be provisioned in SAP Business Object Cloud before they can sign in tooSAP Business Object Cloud.</span></span> <span data-ttu-id="f6326-221">W chmurze obiektu biznesowych SAP Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="f6326-221">In SAP Business Object Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="f6326-222">tooprovision konto użytkownika:</span><span class="sxs-lookup"><span data-stu-id="f6326-222">tooprovision a user account:</span></span>

1. <span data-ttu-id="f6326-223">Zaloguj się tooyour SAP Business obiektu chmury witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="f6326-223">Sign in tooyour SAP Business Object Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="f6326-224">Wybierz **Menu** > **zabezpieczeń** > **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="f6326-224">Select **Menu** > **Security** > **Users**.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. <span data-ttu-id="f6326-226">Na powitania **użytkowników** , tooadd nowe szczegóły użytkownika, wybierz  **+** .</span><span class="sxs-lookup"><span data-stu-id="f6326-226">On hello **Users** page, tooadd new user details, select **+**.</span></span> 

    ![Strona dodawania użytkowników](./media/active-directory-saas-sapboc-tutorial/user4.png)

    <span data-ttu-id="f6326-228">Następnie należy wykonać następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="f6326-228">Then, complete hello following steps:</span></span>

    1. <span data-ttu-id="f6326-229">W hello **identyfikator użytkownika** wprowadź identyfikator użytkownika hello hello użytkownika, takie jak **Britta**.</span><span class="sxs-lookup"><span data-stu-id="f6326-229">In hello **USER ID** box, enter hello user ID of hello user, like **Britta**.</span></span>

    2. <span data-ttu-id="f6326-230">W hello **imię** tak samo, jak wprowadź hello imię użytkownika hello **Britta**.</span><span class="sxs-lookup"><span data-stu-id="f6326-230">In hello **FIRST NAME** box, enter hello first name of hello user, like **Britta**.</span></span>

    3. <span data-ttu-id="f6326-231">W hello **nazwisko** tak samo, jak wprowadź hello nazwisko użytkownika hello **Simona**.</span><span class="sxs-lookup"><span data-stu-id="f6326-231">In hello **LAST NAME** box, enter hello last name of hello user, like **Simon**.</span></span>

    4. <span data-ttu-id="f6326-232">W hello **nazwa WYŚWIETLANA** wpisz pełną nazwę użytkownika hello hello tak samo, jak **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="f6326-232">In hello **DISPLAY NAME** box, enter hello full name of hello user, like **Britta Simon**.</span></span>

    5. <span data-ttu-id="f6326-233">W hello **E-MAIL** tak samo, jak wprowadź adres e-mail użytkownika hello hello  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="f6326-233">In hello **E-MAIL** box, enter hello email address of hello user, like **brittasimon@contoso.com**.</span></span>

    6. <span data-ttu-id="f6326-234">Na powitania **Wybieranie ról** wybierz hello odpowiednią rolę dla użytkownika hello, a następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="f6326-234">On hello **Select Roles** page, select hello appropriate role for hello user, and then select **OK**.</span></span>

      ![Wybór roli](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. <span data-ttu-id="f6326-236">Wybierz hello **zapisać** ikony.</span><span class="sxs-lookup"><span data-stu-id="f6326-236">Select hello **Save** icon.</span></span>  


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="f6326-237">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f6326-237">Assign hello Azure AD test user</span></span>

<span data-ttu-id="f6326-238">W tej sekcji możesz Zezwalaj użytkownikowi hello Simona Britta toouse usługi Azure AD rejestracji jednokrotnej, przyznając hello użytkownika konta dostępu tooSAP firm obiektu chmury.</span><span class="sxs-lookup"><span data-stu-id="f6326-238">In this section, you allow hello user Britta Simon toouse Azure AD single sign-on by granting hello user account access tooSAP Business Object Cloud.</span></span>

<span data-ttu-id="f6326-239">tooassign tooSAP Simona Britta firm obiektu chmury:</span><span class="sxs-lookup"><span data-stu-id="f6326-239">tooassign Britta Simon tooSAP Business Object Cloud:</span></span>

1. <span data-ttu-id="f6326-240">W portalu Azure hello Otwórz widok aplikacji hello, a następnie przejdź toohello widok katalogu.</span><span class="sxs-lookup"><span data-stu-id="f6326-240">In hello Azure portal, open hello applications view, and then go toohello directory view.</span></span> <span data-ttu-id="f6326-241">Wybierz **aplikacje dla przedsiębiorstw**, a następnie wybierz **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="f6326-241">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="f6326-243">Z listy aplikacji hello wybierz **SAP Business obiektu chmury**.</span><span class="sxs-lookup"><span data-stu-id="f6326-243">In hello applications list, select **SAP Business Object Cloud**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. <span data-ttu-id="f6326-245">W menu po lewej stronie powitania wybierz **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="f6326-245">In hello left menu, select **Users and groups**.</span></span>

    ![Wybierz użytkowników i grup][202] 

4. <span data-ttu-id="f6326-247">Wybierz pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="f6326-247">Select **Add**.</span></span> <span data-ttu-id="f6326-248">Następnie na powitania **Dodaj przydziału** wybierz pozycję **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="f6326-248">Then, on hello **Add Assignment** page, select **Users and groups**.</span></span>

    ![Strona Dodawanie przypisanie Hello][203]

5. <span data-ttu-id="f6326-250">Na powitania **użytkowników i grup** strony w hello listę użytkowników, wybierz opcję **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="f6326-250">On hello **Users and groups** page, in hello list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="f6326-251">Na powitania **użytkowników i grup** wybierz pozycję **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="f6326-251">On hello **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="f6326-252">Na powitania **Dodaj przydziału** wybierz pozycję **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="f6326-252">On hello **Add Assignment** page, select **Assign**.</span></span>

![Przypisanie roli użytkownika hello][200] 
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f6326-254">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="f6326-254">Test single sign-on</span></span>

<span data-ttu-id="f6326-255">W tej sekcji można przetestować przy użyciu panelu dostępu hello konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="f6326-255">In this section, you test your Azure AD single sign-on configuration by using hello access panel.</span></span>

<span data-ttu-id="f6326-256">Po wybraniu kafelka SAP Business obiektu chmury hello w panelu dostępu hello powinny być automatycznie zalogowano tooyour aplikacji SAP Business obiektu chmury.</span><span class="sxs-lookup"><span data-stu-id="f6326-256">When you select hello SAP Business Object Cloud tile in hello access panel, you should be automatically signed in tooyour SAP Business Object Cloud application.</span></span>

<span data-ttu-id="f6326-257">Aby uzyskać więcej informacji na temat hello panel dostępu, zobacz [panelu dostępu toohello wprowadzenie](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f6326-257">For more information about hello access panel, see [Introduction toohello access panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f6326-258">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="f6326-258">Additional resources</span></span>

* [<span data-ttu-id="f6326-259">Lista samouczków dotyczących toointegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f6326-259">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f6326-260">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f6326-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_203.png

