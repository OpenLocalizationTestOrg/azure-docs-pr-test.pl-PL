---
title: "Samouczek: Integracji usługi Azure Active Directory z Dowiedz się, tablica | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Tablica Dowiedz się więcej."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b8ca505-61ea-487c-9a3e-fa50c936df0c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jeedes
ms.openlocfilehash: c2b7638e99fa46ff41a7f2202bdf0e7a2b017c19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn"></a><span data-ttu-id="454e7-103">Samouczek: Integracji Azure Active Directory z tablica Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="454e7-103">Tutorial: Azure Active Directory integration with Blackboard Learn</span></span>

<span data-ttu-id="454e7-104">Z tego samouczka dowiesz się integrowanie tablica Dowiedz się więcej o usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="454e7-104">In this tutorial, you learn how to integrate Blackboard Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="454e7-105">Integrowanie tablica Dowiedz się więcej o usłudze Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="454e7-105">Integrating Blackboard Learn with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="454e7-106">Można kontrolować w usłudze Azure AD, który ma dostęp do informacji tablica</span><span class="sxs-lookup"><span data-stu-id="454e7-106">You can control in Azure AD who has access to Blackboard Learn</span></span>
- <span data-ttu-id="454e7-107">Umożliwia użytkownikom automatycznie pobrać zalogowane tablica informacji (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="454e7-107">You can enable your users to automatically get signed-on to Blackboard Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="454e7-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="454e7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="454e7-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="454e7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="454e7-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="454e7-110">Prerequisites</span></span>

<span data-ttu-id="454e7-111">Aby skonfigurować integrację usługi Azure AD z tablica Dowiedz się, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="454e7-111">To configure Azure AD integration with Blackboard Learn, you need the following items:</span></span>

- <span data-ttu-id="454e7-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="454e7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="454e7-113">Dowiedz się, tablica logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="454e7-113">A Blackboard Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="454e7-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="454e7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="454e7-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="454e7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="454e7-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="454e7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="454e7-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="454e7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="454e7-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="454e7-118">Scenario description</span></span>
<span data-ttu-id="454e7-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="454e7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="454e7-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="454e7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="454e7-121">Dodawanie informacji tablica z galerii</span><span class="sxs-lookup"><span data-stu-id="454e7-121">Adding Blackboard Learn from the gallery</span></span>
2. <span data-ttu-id="454e7-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="454e7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn-from-the-gallery"></a><span data-ttu-id="454e7-123">Dodawanie informacji tablica z galerii</span><span class="sxs-lookup"><span data-stu-id="454e7-123">Adding Blackboard Learn from the gallery</span></span>
<span data-ttu-id="454e7-124">Aby skonfigurować integrację tablica informacje do usługi Azure AD, należy dodać informacje tablica z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="454e7-124">To configure the integration of Blackboard Learn into Azure AD, you need to add Blackboard Learn from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="454e7-125">**Aby dodać informacje tablica z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="454e7-125">**To add Blackboard Learn from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="454e7-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="454e7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="454e7-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="454e7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="454e7-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="454e7-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="454e7-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="454e7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="454e7-133">W polu wyszukiwania wpisz **Dowiedz się, tablica**.</span><span class="sxs-lookup"><span data-stu-id="454e7-133">In the search box, type **Blackboard Learn**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_search.png)

5. <span data-ttu-id="454e7-135">W panelu wyników wybierz **Dowiedz się, tablica**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="454e7-135">In the results panel, select **Blackboard Learn**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="454e7-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="454e7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="454e7-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z tablica Dowiedz się na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="454e7-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="454e7-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednikiem w Dowiedz się, tablica jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="454e7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Blackboard Learn is to a user in Azure AD.</span></span> <span data-ttu-id="454e7-140">Innymi słowy łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w tablica Dowiedz się potrzeba ustanowienia.</span><span class="sxs-lookup"><span data-stu-id="454e7-140">In other words, a link relationship between an Azure AD user and the related user in Blackboard Learn needs to be established.</span></span>

<span data-ttu-id="454e7-141">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w tablica Dowiedz się więcej.</span><span class="sxs-lookup"><span data-stu-id="454e7-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Blackboard Learn.</span></span>

<span data-ttu-id="454e7-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z tablica Dowiedz się więcej, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="454e7-142">To configure and test Azure AD single sign-on with Blackboard Learn, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="454e7-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="454e7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="454e7-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="454e7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="454e7-145">**[Tworzenie użytkownika testowego Dowiedz się, tablica](#creating-a-blackboard-learn-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta tablica informacje połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="454e7-145">**[Creating a Blackboard Learn test user](#creating-a-blackboard-learn-test-user)** - to have a counterpart of Britta Simon in Blackboard Learn that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="454e7-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="454e7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="454e7-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="454e7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="454e7-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="454e7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="454e7-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji tablica Dowiedz się więcej.</span><span class="sxs-lookup"><span data-stu-id="454e7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Blackboard Learn application.</span></span>

<span data-ttu-id="454e7-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z tablica Dowiedz się, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="454e7-150">**To configure Azure AD single sign-on with Blackboard Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="454e7-151">W portalu Azure na **Dowiedz się, tablica** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="454e7-151">In the Azure portal, on the **Blackboard Learn** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="454e7-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="454e7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_samlbase.png)

3. <span data-ttu-id="454e7-155">Na **tablica Dowiedz się, domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="454e7-155">On the **Blackboard Learn Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_url.png)

    <span data-ttu-id="454e7-157">a.</span><span class="sxs-lookup"><span data-stu-id="454e7-157">a.</span></span> <span data-ttu-id="454e7-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.blackboard.com/`</span><span class="sxs-lookup"><span data-stu-id="454e7-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.blackboard.com/`</span></span>

    <span data-ttu-id="454e7-159">b.</span><span class="sxs-lookup"><span data-stu-id="454e7-159">b.</span></span> <span data-ttu-id="454e7-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span><span class="sxs-lookup"><span data-stu-id="454e7-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="454e7-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="454e7-161">These values are not real.</span></span> <span data-ttu-id="454e7-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="454e7-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="454e7-163">Skontaktuj się z [tablica klienta Dowiedz się z pomocą techniczną](https://www.blackboard.com/support/index.aspx) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="454e7-163">Contact [Blackboard Learn Client support team](https://www.blackboard.com/support/index.aspx) to get these values.</span></span> 

4. <span data-ttu-id="454e7-164">Tablica Dowiedz się więcej aplikacji oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="454e7-164">Blackboard Learn application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="454e7-165">Skonfiguruj następujące oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="454e7-165">Configure the following claims for this application.</span></span> <span data-ttu-id="454e7-166">Możesz zarządzać wartości tych atrybutów z **atrybuty użytkownika** sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="454e7-166">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span>
 <span data-ttu-id="454e7-167">Poniższy zrzut ekranu przedstawia przykład informacji na ten temat.</span><span class="sxs-lookup"><span data-stu-id="454e7-167">The following screenshot shows an example about it.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="454e7-169">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybuty tokenu SAML, jak pokazano w obrazie i wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="454e7-169">In the **User Attributes** section on **Single sign-on** dialog, configure SAML token attributes as shown in the image and perform the following steps.</span></span> <span data-ttu-id="454e7-170">Firma Microsoft zamapowaniu Userprincipalname jako atrybut unikatowego użytkownika w tym miejscu, ale mapowany na odpowiednią wartość, która odróżnia jednoznacznie użytkownik w organizacji i która jest mapowana na pole username tablica Dowiedz się.</span><span class="sxs-lookup"><span data-stu-id="454e7-170">We have mapped the Userprincipalname as the unique user attribute here but you can map it to the appropriate value, which uniquely distinguishes the user in the organization and that maps to Blackboard Learn username field.</span></span>
           
    | <span data-ttu-id="454e7-171">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="454e7-171">Attribute Name</span></span> | <span data-ttu-id="454e7-172">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="454e7-172">Attribute Value</span></span> |   
    | ---------------| ----------------|
    | <span data-ttu-id="454e7-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span><span class="sxs-lookup"><span data-stu-id="454e7-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span></span> |<span data-ttu-id="454e7-174">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="454e7-174">user.userprincipalname</span></span> |

    <span data-ttu-id="454e7-175">a.</span><span class="sxs-lookup"><span data-stu-id="454e7-175">a.</span></span> <span data-ttu-id="454e7-176">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="454e7-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_04.png)
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="454e7-179">b.</span><span class="sxs-lookup"><span data-stu-id="454e7-179">b.</span></span> <span data-ttu-id="454e7-180">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="454e7-180">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="454e7-181">c.</span><span class="sxs-lookup"><span data-stu-id="454e7-181">c.</span></span> <span data-ttu-id="454e7-182">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="454e7-182">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="454e7-183">d.</span><span class="sxs-lookup"><span data-stu-id="454e7-183">d.</span></span> <span data-ttu-id="454e7-184">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="454e7-184">Click **Ok**.</span></span>

4. <span data-ttu-id="454e7-185">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="454e7-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_certificate.png)

7. <span data-ttu-id="454e7-187">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="454e7-187">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="454e7-189">Na **tablica informacje konfiguracji** , kliknij przycisk **skonfigurować tablica Dowiedz się,** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="454e7-189">On the **Blackboard Learn Configuration** section, click **Configure Blackboard Learn** to open **Configure sign-on** window.</span></span> <span data-ttu-id="454e7-190">Kopiuj **identyfikator jednostki SAML** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="454e7-190">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_configure.png) 

9. <span data-ttu-id="454e7-192">Skonfigurować logowanie jednokrotne w **tablica Dowiedz się** stronie, musisz wysłać pobrany **XML metadanych** i **identyfikator jednostki SAML** do [tablica Dowiedz się więcej obsługuje](https://www.blackboard.com/support/index.aspx).</span><span class="sxs-lookup"><span data-stu-id="454e7-192">To configure single sign-on on **Blackboard Learn** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID** to [Blackboard Learn support](https://www.blackboard.com/support/index.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="454e7-193">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="454e7-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="454e7-194">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="454e7-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="454e7-195">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="454e7-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="454e7-196">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="454e7-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="454e7-197">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="454e7-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="454e7-199">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="454e7-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="454e7-200">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="454e7-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="454e7-202">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="454e7-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="454e7-204">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="454e7-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="454e7-206">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="454e7-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="454e7-208">a.</span><span class="sxs-lookup"><span data-stu-id="454e7-208">a.</span></span> <span data-ttu-id="454e7-209">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="454e7-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="454e7-210">b.</span><span class="sxs-lookup"><span data-stu-id="454e7-210">b.</span></span> <span data-ttu-id="454e7-211">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="454e7-211">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="454e7-212">c.</span><span class="sxs-lookup"><span data-stu-id="454e7-212">c.</span></span> <span data-ttu-id="454e7-213">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="454e7-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="454e7-214">d.</span><span class="sxs-lookup"><span data-stu-id="454e7-214">d.</span></span> <span data-ttu-id="454e7-215">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="454e7-215">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn-test-user"></a><span data-ttu-id="454e7-216">Tworzenie użytkownika testowego tablica Dowiedz się więcej.</span><span class="sxs-lookup"><span data-stu-id="454e7-216">Creating a Blackboard Learn test user</span></span>
<span data-ttu-id="454e7-217">W tej sekcji można utworzyć użytkownika o nazwie Simona Britta w tablica Dowiedz się więcej.</span><span class="sxs-lookup"><span data-stu-id="454e7-217">In this section, you create a user called Britta Simon in Blackboard Learn.</span></span> 

<span data-ttu-id="454e7-218">Tablica Dowiedz się aplikacja obsługuje tylko w czasie Inicjowanie obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="454e7-218">Blackboard Learn application support just in time user provisioning.</span></span> <span data-ttu-id="454e7-219">Upewnij się, że skonfigurowano oświadczenia zgodnie z opisem w sekcji  **[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**</span><span class="sxs-lookup"><span data-stu-id="454e7-219">Make sure that you have configured the claims as described in the section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span></span>
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="454e7-220">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="454e7-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="454e7-221">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu, aby dowiedzieć się, tablica.</span><span class="sxs-lookup"><span data-stu-id="454e7-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Blackboard Learn.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="454e7-223">**Aby przypisać Simona Britta tablica Dowiedz się, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="454e7-223">**To assign Britta Simon to Blackboard Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="454e7-224">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="454e7-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="454e7-226">Na liście aplikacji zaznacz **Dowiedz się, tablica**.</span><span class="sxs-lookup"><span data-stu-id="454e7-226">In the applications list, select **Blackboard Learn**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_app.png) 

3. <span data-ttu-id="454e7-228">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="454e7-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="454e7-230">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="454e7-230">Click **Add** button.</span></span> <span data-ttu-id="454e7-231">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="454e7-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="454e7-233">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="454e7-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="454e7-234">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="454e7-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="454e7-235">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="454e7-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="454e7-236">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="454e7-236">Testing single sign-on</span></span>

<span data-ttu-id="454e7-237">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="454e7-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="454e7-238">Po kliknięciu kafelka tablica Dowiedz się, w panelu dostępu należy należy pobrać automatycznie zalogowane do aplikacji tablica Dowiedz się więcej.</span><span class="sxs-lookup"><span data-stu-id="454e7-238">When you click the Blackboard Learn tile in the Access Panel, you should get automatically signed-on to your Blackboard Learn application.</span></span> <span data-ttu-id="454e7-239">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="454e7-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="454e7-240">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="454e7-240">Additional resources</span></span>

* [<span data-ttu-id="454e7-241">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="454e7-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="454e7-242">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="454e7-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_203.png

