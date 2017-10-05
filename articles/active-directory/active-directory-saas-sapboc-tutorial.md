---
title: 'Samouczek: Integracji Azure Active Directory z SAP Business obiektu chmury | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i SAP Business obiektu chmury."
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
ms.openlocfilehash: 6d517c5e302ac36e5bba2053998c75f8f4d42683
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a><span data-ttu-id="46a82-103">Samouczek: Integracji Azure Active Directory z SAP Business obiektu chmury</span><span class="sxs-lookup"><span data-stu-id="46a82-103">Tutorial: Azure Active Directory integration with SAP Business Object Cloud</span></span>

<span data-ttu-id="46a82-104">Z tego samouczka dowiesz się integrowanie SAP Business obiektu chmury w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="46a82-104">In this tutorial, you learn how to integrate SAP Business Object Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="46a82-105">Po zintegrowaniu z usługą Azure AD SAP Business obiektu chmury można uzyskać następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="46a82-105">You get the following benefits when you integrate SAP Business Object Cloud with Azure AD:</span></span>

- <span data-ttu-id="46a82-106">W usłudze Azure AD można kontrolować, kto ma dostęp do programu SAP Business obiektu chmury.</span><span class="sxs-lookup"><span data-stu-id="46a82-106">In Azure AD, you can control who has access to SAP Business Object Cloud.</span></span>
- <span data-ttu-id="46a82-107">Użytkownikom programu SAP Business obiektu chmury mogą automatycznie zaloguj przy użyciu rejestracji jednokrotnej i konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="46a82-107">You can automatically sign in your users to SAP Business Object Cloud by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="46a82-108">Możesz zarządzać kont w jednej, centralnej lokalizacji, portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="46a82-108">You can manage your accounts in one, central location, the Azure portal.</span></span>

<span data-ttu-id="46a82-109">Aby dowiedzieć się więcej na temat oprogramowania jako usługa (SaaS) integracji aplikacji z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="46a82-109">To learn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46a82-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="46a82-110">Prerequisites</span></span>

<span data-ttu-id="46a82-111">Aby skonfigurować integrację usługi Azure AD z SAP Business obiektu chmury, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="46a82-111">To set up Azure AD integration with SAP Business Object Cloud, you need the following items:</span></span>

- <span data-ttu-id="46a82-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="46a82-112">An Azure AD subscription</span></span>
- <span data-ttu-id="46a82-113">Chmura obiektu SAP Business, z logowanie jednokrotne włączone</span><span class="sxs-lookup"><span data-stu-id="46a82-113">An SAP Business Object Cloud, with single sign-on turned on</span></span>

> [!NOTE]
> <span data-ttu-id="46a82-114">W przypadku testowania czynności w tym samouczku, zaleca się nie przetestować ich w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="46a82-114">If you test the steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="46a82-115">Zalecenia dotyczące testowania czynności w tym samouczku:</span><span class="sxs-lookup"><span data-stu-id="46a82-115">Recommendations for testing the steps in this tutorial:</span></span>

- <span data-ttu-id="46a82-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="46a82-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="46a82-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [Pobierz bezpłatną wersję próbną miesięcznego](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="46a82-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="46a82-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="46a82-118">Scenario description</span></span>
<span data-ttu-id="46a82-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="46a82-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="46a82-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="46a82-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="46a82-121">Dodaj SAP Business obiektu chmury z galerii.</span><span class="sxs-lookup"><span data-stu-id="46a82-121">Add SAP Business Object Cloud from the gallery.</span></span>
2. <span data-ttu-id="46a82-122">Instalowanie i testowanie usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="46a82-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-sap-business-object-cloud-from-the-gallery"></a><span data-ttu-id="46a82-123">Dodaj SAP Business obiektu chmury z galerii</span><span class="sxs-lookup"><span data-stu-id="46a82-123">Add SAP Business Object Cloud from the gallery</span></span>
<span data-ttu-id="46a82-124">Aby skonfigurować integrację SAP Business obiektu chmury z usługą Azure AD w galerii, należy dodać SAP Business obiektu chmury do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="46a82-124">To set up the integration of SAP Business Object Cloud with Azure AD, in the gallery, add SAP Business Object Cloud to your list of managed SaaS apps.</span></span>

<span data-ttu-id="46a82-125">Aby dodać SAP Business obiektu chmury z galerii:</span><span class="sxs-lookup"><span data-stu-id="46a82-125">To add SAP Business Object Cloud from the gallery:</span></span>

1. <span data-ttu-id="46a82-126">W [portalu Azure](https://portal.azure.com), w menu po lewej stronie wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46a82-126">In the [Azure portal](https://portal.azure.com), in the left menu, select **Azure Active Directory**.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="46a82-128">Wybierz **aplikacje dla przedsiębiorstw**, a następnie wybierz **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="46a82-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Strona aplikacji przedsiębiorstwa][2]
    
3. <span data-ttu-id="46a82-130">Aby dodać nową aplikację, zaznacz **nowej aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="46a82-130">To add a new application, select **New application**.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="46a82-132">W polu wyszukiwania wprowadź **SAP Business obiektu chmury**.</span><span class="sxs-lookup"><span data-stu-id="46a82-132">In the search box, enter **SAP Business Object Cloud**.</span></span>

    ![Pole wyszukiwania](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. <span data-ttu-id="46a82-134">W panelu wyników wybierz **SAP Business obiektu chmury**, a następnie wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="46a82-134">In the results panel, select **SAP Business Object Cloud**, and then select **Add**.</span></span>

    ![SAP Business obiektu chmury na liście wyników](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="46a82-136">Instalowanie i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="46a82-136">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="46a82-137">W tej sekcji możesz zdefiniować i test usługi Azure AD rejestracji jednokrotnej z SAP Business obiektu chmury w oparciu o nazwie użytkownika testowego *Simona Britta*.</span><span class="sxs-lookup"><span data-stu-id="46a82-137">In this section, you set up and test Azure AD single sign-on with SAP Business Object Cloud based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="46a82-138">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi znać użytkownika odpowiednikiem usługi Azure AD w chmurze programu SAP Business obiektu.</span><span class="sxs-lookup"><span data-stu-id="46a82-138">For single sign-on to work, Azure AD needs to know the Azure AD counterpart user in SAP Business Object Cloud.</span></span> <span data-ttu-id="46a82-139">Należy ustanowić relację łącza między użytkownika usługi Azure AD i powiązanych użytkowników w chmurze programu SAP Business obiektu.</span><span class="sxs-lookup"><span data-stu-id="46a82-139">A link relationship between an Azure AD user and the related user in SAP Business Object Cloud must be established.</span></span>

<span data-ttu-id="46a82-140">Ustanowienie relacji link, w chmurze obiektu biznesowych SAP, dla **Username**, przypisz wartość **nazwy użytkownika** w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="46a82-140">To establish the link relationship, in SAP Business Object Cloud, for **Username**, assign the value of the **user name** in Azure AD.</span></span>

<span data-ttu-id="46a82-141">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SAP Business obiektu chmury, należy wykonać następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="46a82-141">To configure and test Azure AD single sign-on with SAP Business Object Cloud, complete the following tasks:</span></span>

1. <span data-ttu-id="46a82-142">[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="46a82-142">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="46a82-143">Ustawia użytkownika, aby użyć tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="46a82-143">Sets up a user to use this feature.</span></span>
2. <span data-ttu-id="46a82-144">[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="46a82-144">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="46a82-145">Testy usługi Azure AD rejestracji jednokrotnej z użytkownikiem Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="46a82-145">Tests Azure AD single sign-on with the user Britta Simon.</span></span>
3. <span data-ttu-id="46a82-146">[Tworzenie użytkownika testowego SAP Business obiektu chmury](#create-an-sap-business-object-cloud-test-user).</span><span class="sxs-lookup"><span data-stu-id="46a82-146">[Create an SAP Business Object Cloud test user](#create-an-sap-business-object-cloud-test-user).</span></span> <span data-ttu-id="46a82-147">Tworzy odpowiednikiem Simona Britta SAP Business obiektu chmury połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="46a82-147">Creates a counterpart of Britta Simon in SAP Business Object Cloud that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="46a82-148">[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="46a82-148">[Assign the Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="46a82-149">Konfiguruje Simona Britta przy użyciu usługi Azure AD logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="46a82-149">Sets up Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="46a82-150">[Test rejestracji jednokrotnej](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="46a82-150">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="46a82-151">Sprawdza, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="46a82-151">Verifies that the configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="46a82-152">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="46a82-152">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="46a82-153">W tej sekcji możesz włączyć usługi Azure AD pojedynczego logowania w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="46a82-153">In this section, you turn on Azure AD single sign-on in the Azure portal.</span></span> <span data-ttu-id="46a82-154">Następnie skonfigurowaniu rejestracji jednokrotnej w aplikacji SAP Business obiektu chmury.</span><span class="sxs-lookup"><span data-stu-id="46a82-154">Then, you set up single sign-on in your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="46a82-155">Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z SAP Business obiektu chmury:</span><span class="sxs-lookup"><span data-stu-id="46a82-155">To set up Azure AD single sign-on with SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="46a82-156">W portalu Azure na **SAP Business obiektu chmury** strona integracji aplikacji, wybierz opcję **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="46a82-156">In the Azure portal, on the **SAP Business Object Cloud** application integration page, select **Single sign-on**.</span></span>

    ![Wybierz rejestracji jednokrotnej][4]

2. <span data-ttu-id="46a82-158">Na **logowanie jednokrotne** strony, dla **tryb**, wybierz pozycję **na języku SAML logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="46a82-158">On the **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Wybierz na języku SAML logowania jednokrotnego](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. <span data-ttu-id="46a82-160">W obszarze **SAP Business obiektu chmury domeny i adres URL**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="46a82-160">Under **SAP Business Object Cloud Domain and URLs**, complete the following steps:</span></span>

    1. <span data-ttu-id="46a82-161">W **adres URL logowania** wprowadź adres URL, który ma następujący wzór:</span><span class="sxs-lookup"><span data-stu-id="46a82-161">In the **Sign-on URL** box, enter a URL that has the following pattern:</span></span> 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. <span data-ttu-id="46a82-162">W **identyfikator** wprowadź adres URL, który ma następujący wzór:</span><span class="sxs-lookup"><span data-stu-id="46a82-162">In the **Identifier** box, enter a URL that has the following pattern:</span></span>
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![Adresy URL i SAP Business obiektu chmury domeny adresów URL stron](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > <span data-ttu-id="46a82-164">Wartości te adresy URL są do pokazania tylko.</span><span class="sxs-lookup"><span data-stu-id="46a82-164">The values in these URLs are for demonstration only.</span></span> <span data-ttu-id="46a82-165">Zaktualizuj wartości z rzeczywisty adres URL logowania i adres URL identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="46a82-165">Update the values with the actual sign-on URL and identifier URL.</span></span> <span data-ttu-id="46a82-166">Aby uzyskać adres URL logowania, skontaktuj się z [zespołem pomocy technicznej SAP Business obiektu chmury klienta](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span><span class="sxs-lookup"><span data-stu-id="46a82-166">To get the sign-on URL, contact the [SAP Business Object Cloud Client support team](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span></span> <span data-ttu-id="46a82-167">Adres URL identyfikatora można uzyskać, pobierając metadanych SAP Business obiektu chmury z poziomu konsoli administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="46a82-167">You can get the identifier URL by downloading the SAP Business Object Cloud metadata from the admin console.</span></span> <span data-ttu-id="46a82-168">Wyjaśnienie jest zawarte w dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="46a82-168">This is explained later in the tutorial.</span></span> 

4. <span data-ttu-id="46a82-169">W obszarze **certyfikat podpisywania SAML**, wybierz pozycję **XML metadanych**.</span><span class="sxs-lookup"><span data-stu-id="46a82-169">Under **SAML Signing Certificate**, select **Metadata XML**.</span></span> <span data-ttu-id="46a82-170">Następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="46a82-170">Then, save the metadata file on your computer.</span></span>

    ![Wybierz XML metadanych](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. <span data-ttu-id="46a82-172">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="46a82-172">Select **Save**.</span></span>

    ![Wybierz opcję Zapisz](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="46a82-174">W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy SAP Business obiektu chmury.</span><span class="sxs-lookup"><span data-stu-id="46a82-174">In a different web browser window, sign in to your SAP Business Object Cloud company site as an administrator.</span></span>

7. <span data-ttu-id="46a82-175">Wybierz **Menu** > **systemu** > **administracji**.</span><span class="sxs-lookup"><span data-stu-id="46a82-175">Select **Menu** > **System** > **Administration**.</span></span>
    
    ![Wybierz Menu, a następnie systemu, a następnie administracji](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. <span data-ttu-id="46a82-177">Na **zabezpieczeń** wybierz opcję **Edytuj** ikona (pióra).</span><span class="sxs-lookup"><span data-stu-id="46a82-177">On the **Security** tab, select the **Edit** (pen) icon.</span></span>
    
    ![Na karcie Zabezpieczenia wybierz ikonę edycji](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. <span data-ttu-id="46a82-179">Aby uzyskać **metodę uwierzytelniania**, wybierz pozycję **SAML pojedynczego logowania jednokrotnego (SSO)**.</span><span class="sxs-lookup"><span data-stu-id="46a82-179">For **Authentication Method**, select **SAML Single Sign-On (SSO)**.</span></span>

    ![Wybierz SAML logowania jednokrotnego dla metody uwierzytelniania](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. <span data-ttu-id="46a82-181">Aby pobrać metadane dostawcy usługi (krok 1), wybierz **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="46a82-181">To download the service provider metadata (Step 1), select **Download**.</span></span> <span data-ttu-id="46a82-182">W pliku metadanych, należy znaleźć i skopiować **entityID** wartości.</span><span class="sxs-lookup"><span data-stu-id="46a82-182">In the metadata file, find and copy the **entityID** value.</span></span> <span data-ttu-id="46a82-183">W portalu Azure w obszarze **adresy URL i SAP Business obiektu chmury domeny**, Wklej wartość **identyfikator** pole.</span><span class="sxs-lookup"><span data-stu-id="46a82-183">In the Azure portal, under **SAP Business Object Cloud Domain and URLs**, paste the value in the **Identifier** box.</span></span>

    ![Skopiuj i Wklej wartość identyfikator jednostki](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. <span data-ttu-id="46a82-185">Aby przekazać metadane dostawcy usługi (krok 2) w pliku, który został pobrany z portalu Azure w obszarze **metadanych Przekaż dostawcy tożsamości**, wybierz pozycję **przekazać**.</span><span class="sxs-lookup"><span data-stu-id="46a82-185">To upload the service provider metadata (Step 2) in the file that you downloaded from the Azure portal, under **Upload Identity Provider metadata**, select **Upload**.</span></span>  

    ![W obszarze metadanych Przekaż dostawcy tożsamości wybierz przekazywania](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. <span data-ttu-id="46a82-187">W **atrybut użytkownika** wybierz atrybut użytkownika (krok 3), który ma być używany dla implementacji.</span><span class="sxs-lookup"><span data-stu-id="46a82-187">In the **User Attribute** list, select the user attribute (Step 3) that you want to use for your implementation.</span></span> <span data-ttu-id="46a82-188">Ten atrybut użytkownika mapuje dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="46a82-188">This user attribute maps to the identity provider.</span></span> <span data-ttu-id="46a82-189">Aby wprowadzić atrybutów niestandardowych na stronie użytkownika, należy użyć **niestandardowe mapowanie SAML** opcji.</span><span class="sxs-lookup"><span data-stu-id="46a82-189">To enter a custom attribute on the user's page, use the **Custom SAML Mapping** option.</span></span> <span data-ttu-id="46a82-190">Alternatywnie można wybrać **poczty E-mail** lub **identyfikator użytkownika** jako atrybut użytkownika.</span><span class="sxs-lookup"><span data-stu-id="46a82-190">Or, you can select either **Email** or **USER ID** as the user attribute.</span></span> <span data-ttu-id="46a82-191">W naszym przykładzie wybrano **E-mail** możemy mapowane oświadczenia identyfikatora użytkownika z **userprincipalname** atrybutu w **atrybuty użytkownika** części platformy Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="46a82-191">In our example, we selected **Email** because we mapped the user identifier claim with the **userprincipalname** attribute in the **User Attributes** section in the Azure portal.</span></span> <span data-ttu-id="46a82-192">Zapewnia to adres e-mail użytkownika unikatowy, który jest wysyłany do aplikacji SAP Business obiektu chmury w każdym pomyślnym odpowiedzi SAML.</span><span class="sxs-lookup"><span data-stu-id="46a82-192">This provides a unique user email, which is sent to the SAP Business Object Cloud application in every successful SAML response.</span></span>

    ![Wybierz atrybut użytkownika](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. <span data-ttu-id="46a82-194">Aby zweryfikować konto z dostawcy tożsamości (krok 4) w **poświadczeń logowania (Poczta E-mail)** wprowadź adres e-mail użytkownika.</span><span class="sxs-lookup"><span data-stu-id="46a82-194">To verify the account with the identity provider (Step 4), in the **Login Credential (Email)** box, enter the user's email address.</span></span> <span data-ttu-id="46a82-195">Następnie wybierz opcję **Sprawdź konto**.</span><span class="sxs-lookup"><span data-stu-id="46a82-195">Then, select **Verify Account**.</span></span> <span data-ttu-id="46a82-196">System dodaje poświadczenia logowania do konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="46a82-196">The system adds sign-in credentials to the user account.</span></span>

    ![Wprowadź adres e-mail, a następnie wybierz zweryfikować konta](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. <span data-ttu-id="46a82-198">Wybierz **zapisać** ikony.</span><span class="sxs-lookup"><span data-stu-id="46a82-198">Select the **Save** icon.</span></span>

    ![Zapisz](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="46a82-200">Możesz przeczytać zwięzły wersji tych instrukcji w [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="46a82-200">You can read a concise version of these instructions in the [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="46a82-201">Po dodaniu aplikacji przez wybranie **usługi Active Directory** > **aplikacje dla przedsiębiorstw**, wybierz pozycję **rejestracji jednokrotnej** kartę. Są dostępne w dokumentacji osadzony w **konfiguracji** sekcji w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="46a82-201">After you add the app by selecting **Active Directory** > **Enterprise Applications**, select the **Single Sign-On** tab. You can access the embedded documentation in the **Configuration** section, at the bottom of the page.</span></span> <span data-ttu-id="46a82-202">Aby uzyskać więcej informacji, zobacz [usługi Azure AD osadzonych dokumentacji]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="46a82-202">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="46a82-203">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="46a82-203">Create an Azure AD test user</span></span>
<span data-ttu-id="46a82-204">W tej sekcji utworzysz użytkownika testu o nazwie Simona Britta w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="46a82-204">In this section, you create a test user named Britta Simon in the Azure portal.</span></span>

<span data-ttu-id="46a82-205">Aby utworzyć użytkownika testowego w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="46a82-205">To create a test user in Azure AD:</span></span>

1. <span data-ttu-id="46a82-206">W portalu Azure, w menu po lewej stronie wybierz **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46a82-206">In the Azure portal, in the left menu, select **Azure Active Directory**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="46a82-208">Aby wyświetlić listę użytkowników, wybierz **użytkowników i grup**, a następnie wybierz **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="46a82-208">To display the list of users, select **Users and groups**, and then select **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="46a82-210">Aby otworzyć **użytkownika** okno dialogowe, wybierz opcję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="46a82-210">To open the **User** dialog box, select **Add**.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="46a82-212">W **użytkownika** okna dialogowego należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="46a82-212">In the **User** dialog box, complete the following steps:</span></span>
 
    1. <span data-ttu-id="46a82-213">W **nazwa** wprowadź **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="46a82-213">In the **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="46a82-214">W **nazwy użytkownika** wprowadź adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="46a82-214">In the **User name** box, enter the email address of the user Britta Simon.</span></span>

    3. <span data-ttu-id="46a82-215">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="46a82-215">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    4. <span data-ttu-id="46a82-216">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="46a82-216">Select **Create**.</span></span>

        ![Okno dialogowe użytkownika](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![Tworzenie użytkowników usługi Azure AD][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a><span data-ttu-id="46a82-219">Tworzenie użytkownika testowego SAP Business obiektu chmury</span><span class="sxs-lookup"><span data-stu-id="46a82-219">Create an SAP Business Object Cloud test user</span></span>

<span data-ttu-id="46a82-220">Użytkownicy usługi Azure AD należy udostępnić w chmurze programu SAP Business obiektu, aby móc zalogować się do programu SAP Business obiektu chmury.</span><span class="sxs-lookup"><span data-stu-id="46a82-220">Azure AD users must be provisioned in SAP Business Object Cloud before they can sign in to SAP Business Object Cloud.</span></span> <span data-ttu-id="46a82-221">W chmurze obiektu biznesowych SAP Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="46a82-221">In SAP Business Object Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="46a82-222">Aby udostępnić konta użytkownika:</span><span class="sxs-lookup"><span data-stu-id="46a82-222">To provision a user account:</span></span>

1. <span data-ttu-id="46a82-223">Zaloguj się do witryny firmy SAP Business obiektu chmury jako administrator.</span><span class="sxs-lookup"><span data-stu-id="46a82-223">Sign in to your SAP Business Object Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="46a82-224">Wybierz **Menu** > **zabezpieczeń** > **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="46a82-224">Select **Menu** > **Security** > **Users**.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. <span data-ttu-id="46a82-226">Na **użytkowników** , aby dodać nowe szczegóły użytkownika, wybierz  **+** .</span><span class="sxs-lookup"><span data-stu-id="46a82-226">On the **Users** page, to add new user details, select **+**.</span></span> 

    ![Strona dodawania użytkowników](./media/active-directory-saas-sapboc-tutorial/user4.png)

    <span data-ttu-id="46a82-228">Następnie należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="46a82-228">Then, complete the following steps:</span></span>

    1. <span data-ttu-id="46a82-229">W **identyfikator użytkownika** wprowadź identyfikator użytkownika, nazwa użytkownika, takie jak **Britta**.</span><span class="sxs-lookup"><span data-stu-id="46a82-229">In the **USER ID** box, enter the user ID of the user, like **Britta**.</span></span>

    2. <span data-ttu-id="46a82-230">W **imię** Wprowadź imię użytkownika, takie jak **Britta**.</span><span class="sxs-lookup"><span data-stu-id="46a82-230">In the **FIRST NAME** box, enter the first name of the user, like **Britta**.</span></span>

    3. <span data-ttu-id="46a82-231">W **nazwisko** wprowadź nazwisko użytkownika, takie jak **Simona**.</span><span class="sxs-lookup"><span data-stu-id="46a82-231">In the **LAST NAME** box, enter the last name of the user, like **Simon**.</span></span>

    4. <span data-ttu-id="46a82-232">W **nazwa WYŚWIETLANA** wpisz pełną nazwę użytkownika, takie jak **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="46a82-232">In the **DISPLAY NAME** box, enter the full name of the user, like **Britta Simon**.</span></span>

    5. <span data-ttu-id="46a82-233">W **E-MAIL** wprowadź adres e-mail użytkownika, takie jak  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="46a82-233">In the **E-MAIL** box, enter the email address of the user, like **brittasimon@contoso.com**.</span></span>

    6. <span data-ttu-id="46a82-234">Na **Wybieranie ról** , wybierz odpowiednią rolę dla użytkownika, a następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="46a82-234">On the **Select Roles** page, select the appropriate role for the user, and then select **OK**.</span></span>

      ![Wybór roli](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. <span data-ttu-id="46a82-236">Wybierz **zapisać** ikony.</span><span class="sxs-lookup"><span data-stu-id="46a82-236">Select the **Save** icon.</span></span>    


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="46a82-237">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="46a82-237">Assign the Azure AD test user</span></span>

<span data-ttu-id="46a82-238">W tej sekcji musisz zezwolić na użytkownika Simona Britta na przyznanie dostępu kontu użytkownika SAP Business obiektu chmury za pomocą usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="46a82-238">In this section, you allow the user Britta Simon to use Azure AD single sign-on by granting the user account access to SAP Business Object Cloud.</span></span>

<span data-ttu-id="46a82-239">Aby przypisać Simona Britta SAP Business obiektu chmury:</span><span class="sxs-lookup"><span data-stu-id="46a82-239">To assign Britta Simon to SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="46a82-240">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu.</span><span class="sxs-lookup"><span data-stu-id="46a82-240">In the Azure portal, open the applications view, and then go to the directory view.</span></span> <span data-ttu-id="46a82-241">Wybierz **aplikacje dla przedsiębiorstw**, a następnie wybierz **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="46a82-241">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="46a82-243">Na liście aplikacji zaznacz **SAP Business obiektu chmury**.</span><span class="sxs-lookup"><span data-stu-id="46a82-243">In the applications list, select **SAP Business Object Cloud**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. <span data-ttu-id="46a82-245">W menu po lewej stronie wybierz **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="46a82-245">In the left menu, select **Users and groups**.</span></span>

    ![Wybierz użytkowników i grup][202] 

4. <span data-ttu-id="46a82-247">Wybierz pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="46a82-247">Select **Add**.</span></span> <span data-ttu-id="46a82-248">Następnie na **Dodaj przydziału** wybierz pozycję **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="46a82-248">Then, on the **Add Assignment** page, select **Users and groups**.</span></span>

    ![Strona Dodawanie przypisania][203]

5. <span data-ttu-id="46a82-250">Na **użytkowników i grup** strony, na liście użytkowników, wybierz opcję **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="46a82-250">On the **Users and groups** page, in the list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="46a82-251">Na **użytkowników i grup** wybierz pozycję **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="46a82-251">On the **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="46a82-252">Na **Dodaj przydziału** wybierz pozycję **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="46a82-252">On the **Add Assignment** page, select **Assign**.</span></span>

![Przypisanie roli użytkownika][200] 
    
### <a name="test-single-sign-on"></a><span data-ttu-id="46a82-254">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="46a82-254">Test single sign-on</span></span>

<span data-ttu-id="46a82-255">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="46a82-255">In this section, you test your Azure AD single sign-on configuration by using the access panel.</span></span>

<span data-ttu-id="46a82-256">Po wybraniu kafelka SAP Business obiektu chmury w panelu dostępu należy powinny być automatycznie zalogowany do aplikacji SAP Business obiektu chmury.</span><span class="sxs-lookup"><span data-stu-id="46a82-256">When you select the SAP Business Object Cloud tile in the access panel, you should be automatically signed in to your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="46a82-257">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="46a82-257">For more information about the access panel, see [Introduction to the access panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="46a82-258">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="46a82-258">Additional resources</span></span>

* [<span data-ttu-id="46a82-259">Lista samouczków dotyczących sposobów integracji aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="46a82-259">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="46a82-260">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="46a82-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


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

