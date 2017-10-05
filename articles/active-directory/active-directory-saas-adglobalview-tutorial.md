---
title: 'Samouczek: Integracji Azure Active Directory z ADP Globalview | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i ADP Globalview."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffb6464f-714d-41a9-869a-2b7e5ae9f125
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: e9a5e65c484dfb98d1a7bc63d55f6ef92039554b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-globalview"></a><span data-ttu-id="6e85f-103">Samouczek: Integracji Azure Active Directory z ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="6e85f-103">Tutorial: Azure Active Directory integration with ADP Globalview</span></span>

<span data-ttu-id="6e85f-104">Z tego samouczka dowiesz się integrowanie ADP Globalview w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6e85f-104">In this tutorial, you learn how to integrate ADP Globalview with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6e85f-105">Integracja z usługą Azure AD ADP Globalview zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="6e85f-105">Integrating ADP Globalview with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6e85f-106">Można kontrolować w usłudze Azure AD, który ma dostęp do ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="6e85f-106">You can control in Azure AD who has access to ADP Globalview</span></span>
- <span data-ttu-id="6e85f-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do ADP Globalview (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e85f-107">You can enable your users to automatically get signed-on to ADP Globalview (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6e85f-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6e85f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6e85f-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6e85f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e85f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6e85f-110">Prerequisites</span></span>

<span data-ttu-id="6e85f-111">Aby skonfigurować integrację usługi Azure AD z ADP Globalview, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6e85f-111">To configure Azure AD integration with ADP Globalview, you need the following items:</span></span>

- <span data-ttu-id="6e85f-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e85f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6e85f-113">ADP Globalview logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6e85f-113">An ADP Globalview single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6e85f-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="6e85f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6e85f-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="6e85f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6e85f-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="6e85f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6e85f-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6e85f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6e85f-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="6e85f-118">Scenario description</span></span>
<span data-ttu-id="6e85f-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="6e85f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6e85f-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="6e85f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6e85f-121">Dodawanie ADP Globalview z galerii</span><span class="sxs-lookup"><span data-stu-id="6e85f-121">Adding ADP Globalview from the gallery</span></span>
2. <span data-ttu-id="6e85f-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6e85f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-globalview-from-the-gallery"></a><span data-ttu-id="6e85f-123">Dodawanie ADP Globalview z galerii</span><span class="sxs-lookup"><span data-stu-id="6e85f-123">Adding ADP Globalview from the gallery</span></span>
<span data-ttu-id="6e85f-124">Aby skonfigurować integrację usługi Azure AD ADP Globalview, należy dodać ADP Globalview z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="6e85f-124">To configure the integration of ADP Globalview into Azure AD, you need to add ADP Globalview from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6e85f-125">**Aby dodać ADP Globalview z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6e85f-125">**To add ADP Globalview from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6e85f-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6e85f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="6e85f-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="6e85f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6e85f-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6e85f-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="6e85f-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6e85f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="6e85f-133">W polu wyszukiwania wpisz **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="6e85f-133">In the search box, type **ADP Globalview**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_search.png)

5. <span data-ttu-id="6e85f-135">W panelu wyników wybierz **ADP Globalview**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="6e85f-135">In the results panel, select **ADP Globalview**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6e85f-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6e85f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6e85f-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z ADP Globalview oparte na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="6e85f-138">In this section, you configure and test Azure AD single sign-on with ADP Globalview based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6e85f-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w ADP Globalview jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e85f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ADP Globalview is to a user in Azure AD.</span></span> <span data-ttu-id="6e85f-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w ADP Globalview musi się.</span><span class="sxs-lookup"><span data-stu-id="6e85f-140">In other words, a link relationship between an Azure AD user and the related user in ADP Globalview needs to be established.</span></span>

<span data-ttu-id="6e85f-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="6e85f-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ADP Globalview.</span></span>

<span data-ttu-id="6e85f-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ADP Globalview, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="6e85f-142">To configure and test Azure AD single sign-on with ADP Globalview, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6e85f-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="6e85f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6e85f-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6e85f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6e85f-145">**[Tworzenie użytkownika testowego ADP Globalview](#creating-an-adp-globalview-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta ADP Globalview, połączonej z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6e85f-145">**[Creating an ADP Globalview test user](#creating-an-adp-globalview-test-user)** - to have a counterpart of Britta Simon in ADP Globalview that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6e85f-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6e85f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6e85f-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="6e85f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6e85f-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6e85f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6e85f-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="6e85f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ADP Globalview application.</span></span>

<span data-ttu-id="6e85f-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z ADP Globalview, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6e85f-150">**To configure Azure AD single sign-on with ADP Globalview, perform the following steps:**</span></span>

1. <span data-ttu-id="6e85f-151">W portalu Azure na **ADP Globalview** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="6e85f-151">In the Azure portal, on the **ADP Globalview** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="6e85f-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="6e85f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_samlbase.png)

3. <span data-ttu-id="6e85f-155">Na **ADP Globalview domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6e85f-155">On the **ADP Globalview Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_url.png)

     <span data-ttu-id="6e85f-157">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca: `https://<subdomain>.globalview.adp.com/federate` lub`https://<subdomain>.globalview.adp.com/federate2`</span><span class="sxs-lookup"><span data-stu-id="6e85f-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.globalview.adp.com/federate` or `https://<subdomain>.globalview.adp.com/federate2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6e85f-158">Wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="6e85f-158">The value is not real.</span></span> <span data-ttu-id="6e85f-159">Zaktualizuj tę wartość z rzeczywistego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="6e85f-159">Update the value with the actual Identifier.</span></span> <span data-ttu-id="6e85f-160">Skontaktuj się z [Obsługa ADP Globalview](https://www.adp.com/contact-us/overview.aspx) można uzyskać wartość.</span><span class="sxs-lookup"><span data-stu-id="6e85f-160">Contact [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) to get the value.</span></span>
 
4. <span data-ttu-id="6e85f-161">Na **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="6e85f-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_certificate.png) 

5. <span data-ttu-id="6e85f-163">Aplikacja ADP GlobalView oczekuje potwierdzenia języka SAML w określonym formacie, musisz dodać mapowania atrybutu niestandardowego do konfiguracji atrybuty tokenu SAML.</span><span class="sxs-lookup"><span data-stu-id="6e85f-163">The ADP GlobalView application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> 

6. <span data-ttu-id="6e85f-164">Poniższy zrzut ekranu przedstawia przykład dla niego.</span><span class="sxs-lookup"><span data-stu-id="6e85f-164">The following screenshot shows an example for it.</span></span> <span data-ttu-id="6e85f-165">Nazwy oświadczenia zawsze być **"PersonImmutableID"** i wartości, których firma Microsoft zamapowaniu ExtensionAttribute2, który zawiera identyfikator pracownika użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6e85f-165">The claim names always be **"PersonImmutableID"** and the value of which we have mapped to ExtensionAttribute2, which contains the EmployeeID of the user.</span></span> <span data-ttu-id="6e85f-166">Tutaj mapowanie użytkownika z usługi Azure AD do ADP GlobalView jest wykonywana na identyfikatorem EmployeeID, ale można go mapować na inną wartość, jak również oparte na ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6e85f-166">Here the user mapping from Azure AD to ADP GlobalView is done on the EmployeeID but you can map it to a different value also based on your application settings.</span></span> <span data-ttu-id="6e85f-167">Może współpracować z zespołem ADP GlobalView najpierw do używania prawidłowy identyfikator użytkownika i zmapować tę wartość z **"PersonImmutableID"** oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="6e85f-167">You can work with the ADP GlobalView team first to use the correct identifier of a user and map that value with the **"PersonImmutableID"** claim.</span></span> <span data-ttu-id="6e85f-168">Można również mapować oświadczenia poczty E-mail i identyfikator użytkownika, jak pokazano na rysunku.</span><span class="sxs-lookup"><span data-stu-id="6e85f-168">You can also map the Email and UserID claim as shown in the picture.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_attribute.png)

7. <span data-ttu-id="6e85f-170">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6e85f-170">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="6e85f-171">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="6e85f-171">Attribute Name</span></span> | <span data-ttu-id="6e85f-172">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="6e85f-172">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="6e85f-173">personalimmutableid</span><span class="sxs-lookup"><span data-stu-id="6e85f-173">personalimmutableid</span></span> | <span data-ttu-id="6e85f-174">User.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="6e85f-174">user.extensionattribute2</span></span> |
    | <span data-ttu-id="6e85f-175">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="6e85f-175">email</span></span>               | <span data-ttu-id="6e85f-176">User.mail</span><span class="sxs-lookup"><span data-stu-id="6e85f-176">user.mail</span></span> |
    | <span data-ttu-id="6e85f-177">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="6e85f-177">userid</span></span>              | <span data-ttu-id="6e85f-178">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="6e85f-178">user.userprincipalname</span></span>|
    
    <span data-ttu-id="6e85f-179">a.</span><span class="sxs-lookup"><span data-stu-id="6e85f-179">a.</span></span> <span data-ttu-id="6e85f-180">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6e85f-180">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="6e85f-183">b.</span><span class="sxs-lookup"><span data-stu-id="6e85f-183">b.</span></span> <span data-ttu-id="6e85f-184">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="6e85f-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="6e85f-185">c.</span><span class="sxs-lookup"><span data-stu-id="6e85f-185">c.</span></span> <span data-ttu-id="6e85f-186">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="6e85f-186">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="6e85f-187">d.</span><span class="sxs-lookup"><span data-stu-id="6e85f-187">d.</span></span> <span data-ttu-id="6e85f-188">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="6e85f-188">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6e85f-189">Aby można było skonfigurować potwierdzenia języka SAML, należy skontaktować się z [ADP Globalview pomocy technicznej](https://www.adp.com/contact-us/overview.aspx) i zażądać wartość atrybutu Unikatowy identyfikator dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="6e85f-189">Before you can configure the SAML assertion, you need to contact your [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="6e85f-190">Należy tę wartość, aby skonfigurować niestandardowe oświadczeń dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6e85f-190">You need this value to configure the custom claim for your application.</span></span> 

8. <span data-ttu-id="6e85f-191">Na **ADP Globalview konfiguracji** kliknij **skonfigurować ADP Globalview** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="6e85f-191">On the **ADP Globalview Configuration** section, click **Configure ADP Globalview** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6e85f-192">Kopiuj **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="6e85f-192">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_configure.png) 

9. <span data-ttu-id="6e85f-194">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6e85f-194">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adglobalview-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="6e85f-196">Skonfigurować logowanie jednokrotne w **ADP Globalview** stronie, musisz wysłać pobrany **certyfikatu (Base64)**, **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** do [Obsługa ADP Globalview](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="6e85f-196">To configure single sign-on on **ADP Globalview** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="6e85f-197">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="6e85f-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6e85f-198">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="6e85f-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6e85f-199">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6e85f-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6e85f-200">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e85f-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="6e85f-201">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6e85f-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="6e85f-203">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6e85f-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6e85f-204">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6e85f-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="6e85f-206">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="6e85f-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6e85f-208">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6e85f-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6e85f-210">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6e85f-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6e85f-212">a.</span><span class="sxs-lookup"><span data-stu-id="6e85f-212">a.</span></span> <span data-ttu-id="6e85f-213">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6e85f-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6e85f-214">b.</span><span class="sxs-lookup"><span data-stu-id="6e85f-214">b.</span></span> <span data-ttu-id="6e85f-215">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6e85f-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6e85f-216">c.</span><span class="sxs-lookup"><span data-stu-id="6e85f-216">c.</span></span> <span data-ttu-id="6e85f-217">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="6e85f-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6e85f-218">d.</span><span class="sxs-lookup"><span data-stu-id="6e85f-218">d.</span></span> <span data-ttu-id="6e85f-219">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6e85f-219">Click **Create**.</span></span>
 
### <a name="creating-an-adp-globalview-test-user"></a><span data-ttu-id="6e85f-220">Tworzenie użytkownika testowego ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="6e85f-220">Creating an ADP Globalview test user</span></span>

<span data-ttu-id="6e85f-221">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="6e85f-221">The objective of this section is to create a user called Britta Simon in ADP GlobalView.</span></span> <span data-ttu-id="6e85f-222">Praca z [Obsługa ADP Globalview](https://www.adp.com/contact-us/overview.aspx) Aby dodać użytkowników w ramach konta ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="6e85f-222">Work with [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) to add the users in the ADP GlobalView account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6e85f-223">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6e85f-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6e85f-224">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="6e85f-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ADP Globalview.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="6e85f-226">**Aby przypisać Simona Britta ADP Globalview, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="6e85f-226">**To assign Britta Simon to ADP Globalview, perform the following steps:**</span></span>

1. <span data-ttu-id="6e85f-227">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6e85f-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="6e85f-229">Na liście aplikacji zaznacz **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="6e85f-229">In the applications list, select **ADP Globalview**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_app.png) 

3. <span data-ttu-id="6e85f-231">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="6e85f-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="6e85f-233">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6e85f-233">Click **Add** button.</span></span> <span data-ttu-id="6e85f-234">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6e85f-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="6e85f-236">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="6e85f-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6e85f-237">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6e85f-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6e85f-238">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6e85f-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6e85f-239">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6e85f-239">Testing single sign-on</span></span>

<span data-ttu-id="6e85f-240">Celem tej sekcji służy do testowania konfigurację usługi Azure AD z logowania jednokrotnego za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="6e85f-240">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="6e85f-241">Po kliknięciu kafelka ADP GlobalView w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="6e85f-241">When you click the ADP GlobalView tile in the Access Panel, you should get automatically signed-on to your ADP GlobalView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6e85f-242">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="6e85f-242">Additional resources</span></span>

* [<span data-ttu-id="6e85f-243">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6e85f-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6e85f-244">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6e85f-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_203.png

