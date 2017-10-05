---
title: 'Samouczek: Integracji Azure Active Directory z ADP eTime | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i ADP eTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 31fed307a32e629d00aab7cc9d5167ee16d83936
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a><span data-ttu-id="5257e-103">Samouczek: Integracji Azure Active Directory z ADP eTime</span><span class="sxs-lookup"><span data-stu-id="5257e-103">Tutorial: Azure Active Directory integration with ADP eTime</span></span>

<span data-ttu-id="5257e-104">Z tego samouczka dowiesz się integrowanie ADP eTime w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5257e-104">In this tutorial, you learn how to integrate ADP eTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5257e-105">Integracja z usługą Azure AD ADP eTime zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5257e-105">Integrating ADP eTime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5257e-106">Można kontrolować w usłudze Azure AD, który ma dostęp do ADP eTime</span><span class="sxs-lookup"><span data-stu-id="5257e-106">You can control in Azure AD who has access to ADP eTime</span></span>
- <span data-ttu-id="5257e-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do eTime ADP (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5257e-107">You can enable your users to automatically get signed-on to ADP eTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5257e-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5257e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5257e-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5257e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5257e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5257e-110">Prerequisites</span></span>

<span data-ttu-id="5257e-111">Aby skonfigurować integrację usługi Azure AD z ADP eTime, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5257e-111">To configure Azure AD integration with ADP eTime, you need the following items:</span></span>

- <span data-ttu-id="5257e-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5257e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5257e-113">ADP eTime logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5257e-113">An ADP eTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5257e-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5257e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5257e-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5257e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5257e-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5257e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5257e-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5257e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5257e-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5257e-118">Scenario description</span></span>
<span data-ttu-id="5257e-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5257e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5257e-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5257e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5257e-121">Dodawanie ADP eTime z galerii</span><span class="sxs-lookup"><span data-stu-id="5257e-121">Adding ADP eTime from the gallery</span></span>
2. <span data-ttu-id="5257e-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5257e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-etime-from-the-gallery"></a><span data-ttu-id="5257e-123">Dodawanie ADP eTime z galerii</span><span class="sxs-lookup"><span data-stu-id="5257e-123">Adding ADP eTime from the gallery</span></span>
<span data-ttu-id="5257e-124">Aby skonfigurować integrację usługi Azure AD ADP eTime, należy dodać ADP eTime z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5257e-124">To configure the integration of ADP eTime into Azure AD, you need to add ADP eTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5257e-125">**Aby dodać ADP eTime z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5257e-125">**To add ADP eTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5257e-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5257e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="5257e-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5257e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5257e-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5257e-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="5257e-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5257e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="5257e-133">W polu wyszukiwania wpisz **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="5257e-133">In the search box, type **ADP eTime**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_search.png)

5. <span data-ttu-id="5257e-135">W panelu wyników wybierz **ADP eTime**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="5257e-135">In the results panel, select **ADP eTime**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5257e-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5257e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5257e-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z eTime ADP oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="5257e-138">In this section, you configure and test Azure AD single sign-on with ADP eTime based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5257e-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w ADP eTime jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5257e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ADP eTime is to a user in Azure AD.</span></span> <span data-ttu-id="5257e-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w ADP eTime musi się.</span><span class="sxs-lookup"><span data-stu-id="5257e-140">In other words, a link relationship between an Azure AD user and the related user in ADP eTime needs to be established.</span></span>

<span data-ttu-id="5257e-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="5257e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ADP eTime.</span></span>

<span data-ttu-id="5257e-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ADP eTime, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="5257e-142">To configure and test Azure AD single sign-on with ADP eTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5257e-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5257e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5257e-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5257e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5257e-145">**[Tworzenie użytkownika testowego eTime ADP](#creating-an-adp-etime-test-user)**  — mają odpowiednika Simona Britta w eTime ADP, połączonej z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5257e-145">**[Creating an ADP eTime test user](#creating-an-adp-etime-test-user)** - to have a counterpart of Britta Simon in ADP eTime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5257e-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5257e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5257e-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="5257e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5257e-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5257e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5257e-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji eTime ADP.</span><span class="sxs-lookup"><span data-stu-id="5257e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ADP eTime application.</span></span>

<span data-ttu-id="5257e-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z ADP eTime, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5257e-150">**To configure Azure AD single sign-on with ADP eTime, perform the following steps:**</span></span>

1. <span data-ttu-id="5257e-151">W portalu Azure na **ADP eTime** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="5257e-151">In the Azure portal, on the **ADP eTime** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="5257e-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="5257e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_samlbase.png)

3. <span data-ttu-id="5257e-155">Na **eTime ADP domeny i adres URL** sekcji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5257e-155">On the **ADP eTime Domain and URLs** section, perform the following step:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_url.png)

    <span data-ttu-id="5257e-157">a.</span><span class="sxs-lookup"><span data-stu-id="5257e-157">a.</span></span> <span data-ttu-id="5257e-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<servername>.adp.com`</span><span class="sxs-lookup"><span data-stu-id="5257e-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<servername>.adp.com`</span></span>

    <span data-ttu-id="5257e-159">b.</span><span class="sxs-lookup"><span data-stu-id="5257e-159">b.</span></span> <span data-ttu-id="5257e-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="5257e-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span></span> 
 
    > [!NOTE] 
    > <span data-ttu-id="5257e-161">Wartości te nie są rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="5257e-161">These values are not the real.</span></span> <span data-ttu-id="5257e-162">Rzeczywisty adres URL odpowiedzi i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="5257e-162">Update these values with the actual Reply URL and Identifier.</span></span> <span data-ttu-id="5257e-163">Skontaktuj się z [zespołem pomocy technicznej eTime ADP](https://www.adp.com/contact-us/overview.aspx) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="5257e-163">Contact [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) to get these values.</span></span>

4. <span data-ttu-id="5257e-164">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5257e-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_certificate.png) 

5. <span data-ttu-id="5257e-166">Aplikacja eTime ADP oczekuje potwierdzenia języka SAML w określonym formacie, musisz dodać mapowania atrybutu niestandardowego do konfiguracji atrybuty tokenu SAML.</span><span class="sxs-lookup"><span data-stu-id="5257e-166">The ADP eTime application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="5257e-167">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="5257e-167">The following screenshot shows an example for this.</span></span> <span data-ttu-id="5257e-168">Nazwa oświadczenia będą zawsze miały **"PersonImmutableID"** i wartości, których firma Microsoft zamapowaniu ExtensionAttribute2, który zawiera identyfikator pracownika użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5257e-168">The claim name will always be **"PersonImmutableID"** and the value of which we have mapped to ExtensionAttribute2 which contains the EmployeeID of the user.</span></span> 

    <span data-ttu-id="5257e-169">W tym miejscu będzie można przeprowadzić mapowanie użytkownika z usługi Azure AD do ADP eTime identyfikatorem EmployeeID, ale to można mapować na inną wartość, jak również oparte na ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5257e-169">Here the user mapping from Azure AD to ADP eTime will be done on the EmployeeID but you can map this to a different value also based on your application settings.</span></span> <span data-ttu-id="5257e-170">Pracy, dlatego należy z [zespołem pomocy technicznej eTime ADP](https://www.adp.com/contact-us/overview.aspx) najpierw do używania prawidłowy identyfikator użytkownika i zmapować tę wartość z **"PersonImmutableID"** oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="5257e-170">So please work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_attribute.png)

6. <span data-ttu-id="5257e-172">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5257e-172">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="5257e-173">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="5257e-173">Attribute Name</span></span> | <span data-ttu-id="5257e-174">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="5257e-174">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="5257e-175">PersonImmutableID</span><span class="sxs-lookup"><span data-stu-id="5257e-175">PersonImmutableID</span></span> | <span data-ttu-id="5257e-176">User.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="5257e-176">user.extensionattribute2</span></span> |
    
    <span data-ttu-id="5257e-177">a.</span><span class="sxs-lookup"><span data-stu-id="5257e-177">a.</span></span> <span data-ttu-id="5257e-178">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5257e-178">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="5257e-181">b.</span><span class="sxs-lookup"><span data-stu-id="5257e-181">b.</span></span> <span data-ttu-id="5257e-182">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="5257e-182">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="5257e-183">c.</span><span class="sxs-lookup"><span data-stu-id="5257e-183">c.</span></span> <span data-ttu-id="5257e-184">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="5257e-184">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="5257e-185">d.</span><span class="sxs-lookup"><span data-stu-id="5257e-185">d.</span></span> <span data-ttu-id="5257e-186">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="5257e-186">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5257e-187">Aby można było skonfigurować potwierdzenia języka SAML, należy skontaktować się z [zespołem pomocy technicznej eTime ADP](https://www.adp.com/contact-us/overview.aspx) i zażądać wartość atrybutu Unikatowy identyfikator dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="5257e-187">Before you can configure the SAML assertion, you need to contact your [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="5257e-188">Należy tę wartość, aby skonfigurować niestandardowe oświadczeń dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5257e-188">You need this value to configure the custom claim for your application.</span></span> 

7. <span data-ttu-id="5257e-189">Na **eTime ADP konfiguracji** , kliknij przycisk **eTime skonfigurować ADP** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="5257e-189">On the **ADP eTime Configuration** section, click **Configure ADP eTime** to open **Configure sign-on** window.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_configure.png) 

8. <span data-ttu-id="5257e-191">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5257e-191">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adpetime-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="5257e-193">Skonfigurować logowanie jednokrotne w **ADP eTime** stronie, musisz wysłać pobrany **XML metadanych** do [zespołem pomocy technicznej eTime ADP](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="5257e-193">To configure single sign-on on **ADP eTime** side, you need to send the downloaded **Metadata XML** to [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="5257e-194">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="5257e-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5257e-195">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="5257e-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5257e-196">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5257e-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5257e-197">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5257e-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="5257e-198">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5257e-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="5257e-200">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5257e-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5257e-201">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5257e-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5257e-203">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="5257e-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5257e-205">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5257e-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5257e-207">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5257e-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5257e-209">a.</span><span class="sxs-lookup"><span data-stu-id="5257e-209">a.</span></span> <span data-ttu-id="5257e-210">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5257e-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5257e-211">b.</span><span class="sxs-lookup"><span data-stu-id="5257e-211">b.</span></span> <span data-ttu-id="5257e-212">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5257e-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5257e-213">c.</span><span class="sxs-lookup"><span data-stu-id="5257e-213">c.</span></span> <span data-ttu-id="5257e-214">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="5257e-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5257e-215">d.</span><span class="sxs-lookup"><span data-stu-id="5257e-215">d.</span></span> <span data-ttu-id="5257e-216">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5257e-216">Click **Create**.</span></span>
 
### <a name="creating-an-adp-etime-test-user"></a><span data-ttu-id="5257e-217">Tworzenie użytkownika testowego eTime ADP</span><span class="sxs-lookup"><span data-stu-id="5257e-217">Creating an ADP eTime test user</span></span>

<span data-ttu-id="5257e-218">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="5257e-218">The objective of this section is to create a user called Britta Simon in ADP eTime.</span></span> <span data-ttu-id="5257e-219">Praca z [zespołem pomocy technicznej eTime ADP](https://www.adp.com/contact-us/overview.aspx) Aby dodać użytkowników w ramach konta eTime ADP.</span><span class="sxs-lookup"><span data-stu-id="5257e-219">Work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) to add the users in the ADP eTime account.</span></span> 
   
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5257e-220">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5257e-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5257e-221">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="5257e-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ADP eTime.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="5257e-223">**Aby przypisać Simona Britta ADP eTime, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5257e-223">**To assign Britta Simon to ADP eTime, perform the following steps:**</span></span>

1. <span data-ttu-id="5257e-224">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5257e-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5257e-226">Na liście aplikacji zaznacz **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="5257e-226">In the applications list, select **ADP eTime**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_app.png) 

3. <span data-ttu-id="5257e-228">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5257e-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="5257e-230">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5257e-230">Click **Add** button.</span></span> <span data-ttu-id="5257e-231">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5257e-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="5257e-233">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="5257e-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5257e-234">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5257e-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5257e-235">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5257e-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5257e-236">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5257e-236">Testing single sign-on</span></span>

<span data-ttu-id="5257e-237">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5257e-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5257e-238">Po kliknięciu kafelka eTime ADP w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji eTime ADP.</span><span class="sxs-lookup"><span data-stu-id="5257e-238">When you click the ADP eTime tile in the Access Panel, you should get automatically signed-on to your ADP eTime application.</span></span>
<span data-ttu-id="5257e-239">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5257e-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5257e-240">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5257e-240">Additional resources</span></span>

* [<span data-ttu-id="5257e-241">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5257e-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5257e-242">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5257e-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png

