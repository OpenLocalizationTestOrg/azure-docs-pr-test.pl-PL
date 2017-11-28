---
title: 'Samouczek: Integracji Azure Active Directory z Litmos | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Litmos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: jeedes
ms.assetid: cfaae4bb-e8e5-41d1-ac88-8cc369653036
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ef1b5860ba0a406022bbd11afb366d14bee2c57d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-litmos"></a><span data-ttu-id="d1723-103">Samouczek: Integracji Azure Active Directory z Litmos</span><span class="sxs-lookup"><span data-stu-id="d1723-103">Tutorial: Azure Active Directory integration with Litmos</span></span>

<span data-ttu-id="d1723-104">Z tego samouczka dowiesz się integrowanie Litmos z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d1723-104">In this tutorial, you learn how to integrate Litmos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d1723-105">Integracja z usługą Azure AD Litmos zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d1723-105">Integrating Litmos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d1723-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Litmos.</span><span class="sxs-lookup"><span data-stu-id="d1723-106">You can control in Azure AD who has access to Litmos.</span></span>
- <span data-ttu-id="d1723-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Litmos (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1723-107">You can enable your users to automatically get signed-on to Litmos (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d1723-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d1723-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="d1723-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d1723-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1723-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d1723-110">Prerequisites</span></span>

<span data-ttu-id="d1723-111">Aby skonfigurować integrację usługi Azure AD z Litmos, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d1723-111">To configure Azure AD integration with Litmos, you need the following items:</span></span>

- <span data-ttu-id="d1723-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1723-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d1723-113">Litmos logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d1723-113">A Litmos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d1723-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d1723-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d1723-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d1723-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d1723-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d1723-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d1723-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d1723-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d1723-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d1723-118">Scenario description</span></span>
<span data-ttu-id="d1723-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d1723-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d1723-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d1723-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d1723-121">Dodawanie Litmos z galerii</span><span class="sxs-lookup"><span data-stu-id="d1723-121">Adding Litmos from the gallery</span></span>
2. <span data-ttu-id="d1723-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d1723-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-litmos-from-the-gallery"></a><span data-ttu-id="d1723-123">Dodawanie Litmos z galerii</span><span class="sxs-lookup"><span data-stu-id="d1723-123">Adding Litmos from the gallery</span></span>
<span data-ttu-id="d1723-124">Aby skonfigurować integrację usługi Azure AD Litmos, należy dodać Litmos z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d1723-124">To configure the integration of Litmos into Azure AD, you need to add Litmos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d1723-125">**Aby dodać Litmos z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d1723-125">**To add Litmos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d1723-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d1723-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="d1723-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="d1723-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d1723-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d1723-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="d1723-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d1723-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="d1723-133">W polu wyszukiwania wpisz **Litmos**, wybierz pozycję **Litmos** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="d1723-133">In the search box, type **Litmos**, select **Litmos** from result panel then click **Add** button to add the application.</span></span>

    ![Litmos na liście wyników](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d1723-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d1723-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d1723-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Litmos w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="d1723-136">In this section, you configure and test Azure AD single sign-on with Litmos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d1723-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Litmos jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1723-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Litmos is to a user in Azure AD.</span></span> <span data-ttu-id="d1723-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Litmos musi się.</span><span class="sxs-lookup"><span data-stu-id="d1723-138">In other words, a link relationship between an Azure AD user and the related user in Litmos needs to be established.</span></span>

<span data-ttu-id="d1723-139">W Litmos, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="d1723-139">In Litmos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d1723-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Litmos, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="d1723-140">To configure and test Azure AD single sign-on with Litmos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d1723-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d1723-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d1723-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d1723-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d1723-143">**[Tworzenie użytkownika testowego Litmos](#create-a-litmos-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Litmos połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d1723-143">**[Create a Litmos test user](#create-a-litmos-test-user)** - to have a counterpart of Britta Simon in Litmos that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d1723-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d1723-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d1723-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="d1723-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d1723-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d1723-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d1723-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Litmos.</span><span class="sxs-lookup"><span data-stu-id="d1723-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Litmos application.</span></span>

<span data-ttu-id="d1723-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Litmos, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d1723-148">**To configure Azure AD single sign-on with Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="d1723-149">W portalu Azure na **Litmos** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="d1723-149">In the Azure portal, on the **Litmos** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="d1723-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="d1723-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_samlbase.png)

3. <span data-ttu-id="d1723-153">Na **Litmos domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d1723-153">On the **Litmos Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i domeny Litmos pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_url.png)

    <span data-ttu-id="d1723-155">a.</span><span class="sxs-lookup"><span data-stu-id="d1723-155">a.</span></span> <span data-ttu-id="d1723-156">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.litmos.com/account/Login`</span><span class="sxs-lookup"><span data-stu-id="d1723-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.litmos.com/account/Login`</span></span>

    <span data-ttu-id="d1723-157">b.</span><span class="sxs-lookup"><span data-stu-id="d1723-157">b.</span></span> <span data-ttu-id="d1723-158">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<companyname>.litmos.com/integration/samllogin`</span><span class="sxs-lookup"><span data-stu-id="d1723-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.litmos.com/integration/samllogin`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d1723-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="d1723-159">These values are not real.</span></span> <span data-ttu-id="d1723-160">Zaktualizować te wartości z rzeczywistego identyfikatora i adres URL odpowiedzi, które opisano szczegółowo w dalszej części samouczka lub skontaktuj się z [Litmos obsługuje zespołu](https://www.litmos.com/contact-us/) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="d1723-160">Update these values with the actual Identifier and Reply URL, which are explained later in tutorial or contact [Litmos support team](https://www.litmos.com/contact-us/) to get these values.</span></span>

4. <span data-ttu-id="d1723-161">Na **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d1723-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_certificate.png)

5. <span data-ttu-id="d1723-163">W ramach konfiguracji, musisz dostosować **atrybuty tokenu SAML** Litmos aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d1723-163">As part of the configuration, you need to customize the **SAML Token Attributes** for your Litmos application.</span></span>

    ![Atrybut sekcji](./media/active-directory-saas-litmos-tutorial/tutorial_attribute.png)
           
    | <span data-ttu-id="d1723-165">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="d1723-165">Attribute Name</span></span>   | <span data-ttu-id="d1723-166">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="d1723-166">Attribute Value</span></span> |   
    | ---------------  | ----------------|
    | <span data-ttu-id="d1723-167">Imię</span><span class="sxs-lookup"><span data-stu-id="d1723-167">FirstName</span></span> |<span data-ttu-id="d1723-168">User.givenName</span><span class="sxs-lookup"><span data-stu-id="d1723-168">user.givenname</span></span> |
    | <span data-ttu-id="d1723-169">Nazwisko</span><span class="sxs-lookup"><span data-stu-id="d1723-169">LastName</span></span>  |<span data-ttu-id="d1723-170">User.surname</span><span class="sxs-lookup"><span data-stu-id="d1723-170">user.surname</span></span> |
    | <span data-ttu-id="d1723-171">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="d1723-171">Email</span></span> |<span data-ttu-id="d1723-172">User.mail</span><span class="sxs-lookup"><span data-stu-id="d1723-172">user.mail</span></span> |

    <span data-ttu-id="d1723-173">a.</span><span class="sxs-lookup"><span data-stu-id="d1723-173">a.</span></span> <span data-ttu-id="d1723-174">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d1723-174">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Dodaj atrybut](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_04.png)

    ![Dodaj atrybut Dailog](./media/active-directory-saas-litmos-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="d1723-177">b.</span><span class="sxs-lookup"><span data-stu-id="d1723-177">b.</span></span> <span data-ttu-id="d1723-178">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="d1723-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="d1723-179">c.</span><span class="sxs-lookup"><span data-stu-id="d1723-179">c.</span></span> <span data-ttu-id="d1723-180">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="d1723-180">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="d1723-181">d.</span><span class="sxs-lookup"><span data-stu-id="d1723-181">d.</span></span> <span data-ttu-id="d1723-182">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d1723-182">Click **Ok**.</span></span>     

6. <span data-ttu-id="d1723-183">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d1723-183">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-litmos-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="d1723-185">W oknie innej przeglądarki logowania do witryny firmy Litmos jako administrator.</span><span class="sxs-lookup"><span data-stu-id="d1723-185">In a different browser window, sign-on to your Litmos company site as administrator.</span></span>

8. <span data-ttu-id="d1723-186">Na pasku nawigacyjnym po lewej stronie kliknij **kont**.</span><span class="sxs-lookup"><span data-stu-id="d1723-186">In the navigation bar on the left side, click **Accounts**.</span></span>
   
    ![Sekcja kont na stronie aplikacji][22] 

9. <span data-ttu-id="d1723-188">Kliknij przycisk **integracji** kartę.</span><span class="sxs-lookup"><span data-stu-id="d1723-188">Click the **Integrations** tab.</span></span>
   
    ![Karta Integracja][23] 

10. <span data-ttu-id="d1723-190">Na **integracji** karcie, przewiń w dół do **3 integracji strona**, a następnie kliknij przycisk **SAML 2.0** kartę.</span><span class="sxs-lookup"><span data-stu-id="d1723-190">On the **Integrations** tab, scroll down to **3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0 sekcji][24] 

11. <span data-ttu-id="d1723-192">Skopiuj wartość w obszarze **jest SAML punktu końcowego litmos:** i wklej ją do **adres URL odpowiedzi służący** textbox w **Litmos domeny i adres URL** sekcji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d1723-192">Copy the value under **The SAML endpoint for litmos is:** and paste it into the **Reply URL** textbox in the **Litmos Domain and URLs** section in Azure portal.</span></span> 
   
    ![Punkt końcowy SAML][26] 

12. <span data-ttu-id="d1723-194">W Twojej **Litmos** aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d1723-194">In your **Litmos** application, perform the following steps:</span></span>
    
     ![Litmos aplikacji][25] 
     
     <span data-ttu-id="d1723-196">a.</span><span class="sxs-lookup"><span data-stu-id="d1723-196">a.</span></span> <span data-ttu-id="d1723-197">Kliknij przycisk **Włącz SAML**.</span><span class="sxs-lookup"><span data-stu-id="d1723-197">Click **Enable SAML**.</span></span>
    
     <span data-ttu-id="d1723-198">b.</span><span class="sxs-lookup"><span data-stu-id="d1723-198">b.</span></span> <span data-ttu-id="d1723-199">Otwórz w Notatniku certyfikatu zakodowanego base-64, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikatu X.509 SAML** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="d1723-199">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **SAML X.509 Certificate** textbox.</span></span>
     
     <span data-ttu-id="d1723-200">c.</span><span class="sxs-lookup"><span data-stu-id="d1723-200">c.</span></span> <span data-ttu-id="d1723-201">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="d1723-201">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="d1723-202">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="d1723-202">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d1723-203">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="d1723-203">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d1723-204">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d1723-204">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d1723-205">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1723-205">Create an Azure AD test user</span></span>

<span data-ttu-id="d1723-206">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d1723-206">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="d1723-208">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d1723-208">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d1723-209">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d1723-209">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-litmos-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="d1723-211">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d1723-211">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-litmos-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="d1723-213">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="d1723-213">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-litmos-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="d1723-215">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d1723-215">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-litmos-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d1723-217">a.</span><span class="sxs-lookup"><span data-stu-id="d1723-217">a.</span></span> <span data-ttu-id="d1723-218">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d1723-218">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d1723-219">b.</span><span class="sxs-lookup"><span data-stu-id="d1723-219">b.</span></span> <span data-ttu-id="d1723-220">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d1723-220">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="d1723-221">c.</span><span class="sxs-lookup"><span data-stu-id="d1723-221">c.</span></span> <span data-ttu-id="d1723-222">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="d1723-222">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="d1723-223">d.</span><span class="sxs-lookup"><span data-stu-id="d1723-223">d.</span></span> <span data-ttu-id="d1723-224">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d1723-224">Click **Create**.</span></span>
  
### <a name="create-a-litmos-test-user"></a><span data-ttu-id="d1723-225">Tworzenie użytkownika testowego Litmos</span><span class="sxs-lookup"><span data-stu-id="d1723-225">Create a Litmos test user</span></span>

<span data-ttu-id="d1723-226">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Litmos.</span><span class="sxs-lookup"><span data-stu-id="d1723-226">The objective of this section is to create a user called Britta Simon in Litmos.</span></span>  
<span data-ttu-id="d1723-227">Aplikacja Litmos obsługuje Just in Time inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="d1723-227">The Litmos application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="d1723-228">Oznacza to konto użytkownika jest tworzone automatycznie w razie potrzeby podczas próby uzyskania dostępu do aplikacji za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d1723-228">This means, a user account is automatically created if necessary during an attempt to access the application using the Access Panel.</span></span>

<span data-ttu-id="d1723-229">**Aby utworzyć użytkownika o nazwie Simona Britta w Litmos, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d1723-229">**To create a user called Britta Simon in Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="d1723-230">W oknie innej przeglądarki logowania do witryny firmy Litmos jako administrator.</span><span class="sxs-lookup"><span data-stu-id="d1723-230">In a different browser window, sign-on to your Litmos company site as administrator.</span></span>

2. <span data-ttu-id="d1723-231">Na pasku nawigacyjnym po lewej stronie kliknij **kont**.</span><span class="sxs-lookup"><span data-stu-id="d1723-231">In the navigation bar on the left side, click **Accounts**.</span></span>
   
    ![Sekcja kont na stronie aplikacji][22] 

3. <span data-ttu-id="d1723-233">Kliknij przycisk **integracji** kartę.</span><span class="sxs-lookup"><span data-stu-id="d1723-233">Click the **Integrations** tab.</span></span>
   
    ![Karta integracji][23] 

4. <span data-ttu-id="d1723-235">Na **integracji** karcie, przewiń w dół do **3 integracji strona**, a następnie kliknij przycisk **SAML 2.0** kartę.</span><span class="sxs-lookup"><span data-stu-id="d1723-235">On the **Integrations** tab, scroll down to **3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0][24] 
    
5. <span data-ttu-id="d1723-237">Wybierz **Autogenerate użytkowników**</span><span class="sxs-lookup"><span data-stu-id="d1723-237">Select **Autogenerate Users**</span></span>
   
    ![Automatyczne generowanie użytkowników][27] 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d1723-239">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1723-239">Assign the Azure AD test user</span></span>

<span data-ttu-id="d1723-240">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu Litmos.</span><span class="sxs-lookup"><span data-stu-id="d1723-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Litmos.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="d1723-242">**Aby przypisać Simona Britta Litmos, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d1723-242">**To assign Britta Simon to Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="d1723-243">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d1723-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d1723-245">Na liście aplikacji zaznacz **Litmos**.</span><span class="sxs-lookup"><span data-stu-id="d1723-245">In the applications list, select **Litmos**.</span></span>

    ![Łącze Litmos na liście aplikacji](./media/active-directory-saas-litmos-tutorial/tutorial_litmos_app.png)  

3. <span data-ttu-id="d1723-247">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d1723-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="d1723-249">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d1723-249">Click **Add** button.</span></span> <span data-ttu-id="d1723-250">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d1723-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="d1723-252">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="d1723-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d1723-253">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d1723-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d1723-254">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d1723-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d1723-255">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d1723-255">Test single sign-on</span></span>

<span data-ttu-id="d1723-256">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d1723-256">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="d1723-257">Po kliknięciu kafelka Litmos w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Litmos.</span><span class="sxs-lookup"><span data-stu-id="d1723-257">When you click the Litmos tile in the Access Panel, you should get automatically signed-on to your Litmos application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d1723-258">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d1723-258">Additional resources</span></span>

* [<span data-ttu-id="d1723-259">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d1723-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d1723-260">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d1723-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_04.png
[21]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_60.png
[22]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_61.png
[23]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_62.png
[24]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_63.png
[25]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_64.png
[26]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_65.png
[27]: ./media/active-directory-saas-litmos-tutorial/tutorial_litmos_66.png

[100]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-litmos-tutorial/tutorial_general_203.png

