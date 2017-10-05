---
title: 'Samouczek: Integracji Azure Active Directory z eKincare | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i eKincare."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 57f56d14-83cf-4cbb-b342-fac4fc60078f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 014eaff14974bb6cd551b6fe53409ede6a6dfea1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ekincare"></a><span data-ttu-id="cc198-103">Samouczek: Integracji Azure Active Directory z eKincare</span><span class="sxs-lookup"><span data-stu-id="cc198-103">Tutorial: Azure Active Directory integration with eKincare</span></span>

<span data-ttu-id="cc198-104">Z tego samouczka dowiesz się integrowanie eKincare z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc198-104">In this tutorial, you learn how to integrate eKincare with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cc198-105">Integracja z usługą Azure AD eKincare zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="cc198-105">Integrating eKincare with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cc198-106">Można kontrolować w usłudze Azure AD, który ma dostęp do eKincare</span><span class="sxs-lookup"><span data-stu-id="cc198-106">You can control in Azure AD who has access to eKincare</span></span>
- <span data-ttu-id="cc198-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do eKincare (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc198-107">You can enable your users to automatically get signed-on to eKincare (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cc198-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="cc198-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cc198-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cc198-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc198-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cc198-110">Prerequisites</span></span>

<span data-ttu-id="cc198-111">Aby skonfigurować integrację usługi Azure AD z eKincare, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="cc198-111">To configure Azure AD integration with eKincare, you need the following items:</span></span>

- <span data-ttu-id="cc198-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc198-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cc198-113">EKincare jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="cc198-113">A eKincare single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cc198-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="cc198-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cc198-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="cc198-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cc198-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="cc198-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cc198-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc198-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cc198-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="cc198-118">Scenario description</span></span>
<span data-ttu-id="cc198-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="cc198-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cc198-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="cc198-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cc198-121">Dodawanie eKincare z galerii</span><span class="sxs-lookup"><span data-stu-id="cc198-121">Adding eKincare from the gallery</span></span>
2. <span data-ttu-id="cc198-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="cc198-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ekincare-from-the-gallery"></a><span data-ttu-id="cc198-123">Dodawanie eKincare z galerii</span><span class="sxs-lookup"><span data-stu-id="cc198-123">Adding eKincare from the gallery</span></span>
<span data-ttu-id="cc198-124">Aby skonfigurować integrację usługi Azure AD eKincare, należy dodać eKincare z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="cc198-124">To configure the integration of eKincare into Azure AD, you need to add eKincare from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cc198-125">**Aby dodać eKincare z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="cc198-125">**To add eKincare from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cc198-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="cc198-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="cc198-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="cc198-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cc198-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="cc198-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="cc198-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cc198-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="cc198-133">W polu wyszukiwania wpisz **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="cc198-133">In the search box, type **eKincare**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_search.png)

5. <span data-ttu-id="cc198-135">W panelu wyników wybierz **eKincare**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="cc198-135">In the results panel, select **eKincare**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cc198-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="cc198-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cc198-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z eKincare na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="cc198-138">In this section, you configure and test Azure AD single sign-on with eKincare based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cc198-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w eKincare jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc198-139">For single sign-on to work, Azure AD needs to know what the counterpart user in eKincare is to a user in Azure AD.</span></span> <span data-ttu-id="cc198-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w eKincare musi się.</span><span class="sxs-lookup"><span data-stu-id="cc198-140">In other words, a link relationship between an Azure AD user and the related user in eKincare needs to be established.</span></span>

<span data-ttu-id="cc198-141">W eKincare, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="cc198-141">In eKincare, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cc198-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z eKincare, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="cc198-142">To configure and test Azure AD single sign-on with eKincare, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cc198-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="cc198-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cc198-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="cc198-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cc198-145">**[Tworzenie użytkownika testowego eKincare](#creating-a-ekincare-test-user)**  — mają odpowiednika Simona Britta w eKincare połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cc198-145">**[Creating a eKincare test user](#creating-a-ekincare-test-user)** - to have a counterpart of Britta Simon in eKincare that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cc198-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="cc198-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cc198-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="cc198-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cc198-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="cc198-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cc198-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji eKincare.</span><span class="sxs-lookup"><span data-stu-id="cc198-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your eKincare application.</span></span>

<span data-ttu-id="cc198-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z eKincare, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="cc198-150">**To configure Azure AD single sign-on with eKincare, perform the following steps:**</span></span>

1. <span data-ttu-id="cc198-151">W portalu Azure na **eKincare** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="cc198-151">In the Azure portal, on the **eKincare** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="cc198-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="cc198-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_samlbase.png)

3. <span data-ttu-id="cc198-155">Na **eKincare domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cc198-155">On the **eKincare Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_url.png)

    <span data-ttu-id="cc198-157">a.</span><span class="sxs-lookup"><span data-stu-id="cc198-157">a.</span></span> <span data-ttu-id="cc198-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<instancename>.ekincare.com/`</span><span class="sxs-lookup"><span data-stu-id="cc198-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.ekincare.com/`</span></span>

    <span data-ttu-id="cc198-159">b.</span><span class="sxs-lookup"><span data-stu-id="cc198-159">b.</span></span> <span data-ttu-id="cc198-160">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<instancename>.ekincare.com/hul/saml`</span><span class="sxs-lookup"><span data-stu-id="cc198-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<instancename>.ekincare.com/hul/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cc198-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="cc198-161">These values are not real.</span></span> <span data-ttu-id="cc198-162">Rzeczywisty identyfikator i adres URL odpowiedzi, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="cc198-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="cc198-163">Skontaktuj się z [zespołem pomocy technicznej eKincare](mailto:tech@ekincare.com) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="cc198-163">Contact [eKincare support team](mailto:tech@ekincare.com) to get these values.</span></span>
 
4. <span data-ttu-id="cc198-164">Aplikacja eKincare oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="cc198-164">eKincare application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="cc198-165">Skonfiguruj następujące oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cc198-165">Configure the following claims for this application.</span></span> <span data-ttu-id="cc198-166">Możesz zarządzać wartości tych atrybutów z "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cc198-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="cc198-167">Poniższy zrzut ekranu przedstawia przykład dla tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="cc198-167">The following screenshot shows an example for this configuration.</span></span>

    <span data-ttu-id="cc198-168">Nazwa oświadczenia będą zawsze miały **"identyfikator pracownika"** i wartości, których firma Microsoft zamapowaniu user.extensionattribute1, który zawiera identyfikator pracownika użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cc198-168">The claim name will always be **"employeeid"** and the value of which we have mapped to user.extensionattribute1, that contains the employeeid of the user.</span></span> <span data-ttu-id="cc198-169">Tj nazwy innych dwa oświadczenia</span><span class="sxs-lookup"><span data-stu-id="cc198-169">The other two claims' name i.e</span></span> <span data-ttu-id="cc198-170">**"identyfikatora organizacji"** i **"nazwa_organizacji"** jest zawsze tej samej i ich wartości zawierają odpowiednio szczegóły organizacji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cc198-170">**"organizationid"** and **"organizationname"** will always be same and their values contain the details of the organization of the user respectively.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ekincare-tutorial/attribute.png)
    
5. <span data-ttu-id="cc198-172">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano na ilustracji powyżej i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cc198-172">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image above and perform the following steps:</span></span>
    
    | <span data-ttu-id="cc198-173">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="cc198-173">Attribute Name</span></span> | <span data-ttu-id="cc198-174">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="cc198-174">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="cc198-175">Identyfikator pracownika</span><span class="sxs-lookup"><span data-stu-id="cc198-175">employeeid</span></span> | <span data-ttu-id="cc198-176">*User.extensionattribute1*</span><span class="sxs-lookup"><span data-stu-id="cc198-176">*user.extensionattribute1*</span></span> |
    | <span data-ttu-id="cc198-177">identyfikatora organizacji</span><span class="sxs-lookup"><span data-stu-id="cc198-177">organizationid</span></span> | <span data-ttu-id="cc198-178">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="cc198-178">*"uniquevalue"*</span></span> |
    | <span data-ttu-id="cc198-179">nazwa_organizacji</span><span class="sxs-lookup"><span data-stu-id="cc198-179">organizationname</span></span> | <span data-ttu-id="cc198-180">*User.CompanyName*</span><span class="sxs-lookup"><span data-stu-id="cc198-180">*user.companyname*</span></span> |

    <span data-ttu-id="cc198-181">a.</span><span class="sxs-lookup"><span data-stu-id="cc198-181">a.</span></span> <span data-ttu-id="cc198-182">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cc198-182">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ekincare-tutorial/04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ekincare-tutorial/05.png)
    
    <span data-ttu-id="cc198-185">b.</span><span class="sxs-lookup"><span data-stu-id="cc198-185">b.</span></span> <span data-ttu-id="cc198-186">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="cc198-186">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="cc198-187">c.</span><span class="sxs-lookup"><span data-stu-id="cc198-187">c.</span></span> <span data-ttu-id="cc198-188">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="cc198-188">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="cc198-189">d.</span><span class="sxs-lookup"><span data-stu-id="cc198-189">d.</span></span> <span data-ttu-id="cc198-190">Kliknij przycisk **Ok**</span><span class="sxs-lookup"><span data-stu-id="cc198-190">Click **Ok**</span></span>

6. <span data-ttu-id="cc198-191">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="cc198-191">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_certificate.png) 

7. <span data-ttu-id="cc198-193">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="cc198-193">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ekincare-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="cc198-195">Skonfigurować logowanie jednokrotne w **eKincare** stronie, musisz wysłać pobrany **XML metadanych** do [zespołem pomocy technicznej eKincare](mailto:tech@ekincare.com).</span><span class="sxs-lookup"><span data-stu-id="cc198-195">To configure single sign-on on **eKincare** side, you need to send the downloaded **Metadata XML** to [eKincare support team](mailto:tech@ekincare.com).</span></span> <span data-ttu-id="cc198-196">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="cc198-196">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="cc198-197">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="cc198-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cc198-198">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="cc198-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cc198-199">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cc198-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cc198-200">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc198-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="cc198-201">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="cc198-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="cc198-203">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="cc198-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cc198-204">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="cc198-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cc198-206">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="cc198-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cc198-208">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cc198-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cc198-210">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cc198-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cc198-212">a.</span><span class="sxs-lookup"><span data-stu-id="cc198-212">a.</span></span> <span data-ttu-id="cc198-213">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cc198-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cc198-214">b.</span><span class="sxs-lookup"><span data-stu-id="cc198-214">b.</span></span> <span data-ttu-id="cc198-215">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cc198-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cc198-216">c.</span><span class="sxs-lookup"><span data-stu-id="cc198-216">c.</span></span> <span data-ttu-id="cc198-217">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="cc198-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cc198-218">d.</span><span class="sxs-lookup"><span data-stu-id="cc198-218">d.</span></span> <span data-ttu-id="cc198-219">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="cc198-219">Click **Create**.</span></span>
 
### <a name="creating-a-ekincare-test-user"></a><span data-ttu-id="cc198-220">Tworzenie użytkownika testowego eKincare</span><span class="sxs-lookup"><span data-stu-id="cc198-220">Creating a eKincare test user</span></span>

<span data-ttu-id="cc198-221">Aplikacja obsługuje tylko w czasie Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników są tworzone automatycznie w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cc198-221">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cc198-222">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc198-222">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cc198-223">W tej sekcji musisz włączyć Simona Britta do użycia usługi Azure logowania jednokrotnego za udzielanie dostępu do eKincare.</span><span class="sxs-lookup"><span data-stu-id="cc198-223">In this section, you enable Britta Simon to use Azure single sign-on by granting access to eKincare.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="cc198-225">**Aby przypisać Simona Britta eKincare, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="cc198-225">**To assign Britta Simon to eKincare, perform the following steps:**</span></span>

1. <span data-ttu-id="cc198-226">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="cc198-226">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="cc198-228">Na liście aplikacji zaznacz **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="cc198-228">In the applications list, select **eKincare**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_app.png) 

3. <span data-ttu-id="cc198-230">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="cc198-230">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="cc198-232">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="cc198-232">Click **Add** button.</span></span> <span data-ttu-id="cc198-233">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cc198-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="cc198-235">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="cc198-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cc198-236">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cc198-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cc198-237">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cc198-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cc198-238">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="cc198-238">Testing single sign-on</span></span>

<span data-ttu-id="cc198-239">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="cc198-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cc198-240">Po kliknięciu kafelka eKincare w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji eKincare.</span><span class="sxs-lookup"><span data-stu-id="cc198-240">When you click the eKincare tile in the Access Panel, you should get automatically signed-on to your eKincare application.</span></span>
<span data-ttu-id="cc198-241">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="cc198-241">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cc198-242">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="cc198-242">Additional resources</span></span>

* [<span data-ttu-id="cc198-243">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc198-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cc198-244">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cc198-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_203.png

