---
title: 'Samouczek: Integracji Azure Active Directory z BenefitHub | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i BenefitHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4069fe32-a452-463f-973e-7aa0baa4c2fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 8df9c0d8443d6685253207ed1915c780275014fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefithub"></a><span data-ttu-id="5bb76-103">Samouczek: Integracji Azure Active Directory z BenefitHub</span><span class="sxs-lookup"><span data-stu-id="5bb76-103">Tutorial: Azure Active Directory integration with BenefitHub</span></span>

<span data-ttu-id="5bb76-104">Z tego samouczka dowiesz się integrowanie BenefitHub z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5bb76-104">In this tutorial, you learn how to integrate BenefitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5bb76-105">Integracja z usługą Azure AD BenefitHub zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5bb76-105">Integrating BenefitHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5bb76-106">Można kontrolować w usłudze Azure AD, który ma dostęp do BenefitHub</span><span class="sxs-lookup"><span data-stu-id="5bb76-106">You can control in Azure AD who has access to BenefitHub</span></span>
- <span data-ttu-id="5bb76-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do BenefitHub (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bb76-107">You can enable your users to automatically get signed-on to BenefitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5bb76-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5bb76-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5bb76-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5bb76-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bb76-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5bb76-110">Prerequisites</span></span>

<span data-ttu-id="5bb76-111">Aby skonfigurować integrację usługi Azure AD z BenefitHub, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5bb76-111">To configure Azure AD integration with BenefitHub, you need the following items:</span></span>

- <span data-ttu-id="5bb76-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bb76-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5bb76-113">BenefitHub jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5bb76-113">A BenefitHub single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5bb76-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5bb76-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5bb76-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5bb76-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5bb76-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5bb76-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5bb76-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5bb76-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5bb76-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5bb76-118">Scenario description</span></span>
<span data-ttu-id="5bb76-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5bb76-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5bb76-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5bb76-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5bb76-121">Dodawanie BenefitHub z galerii</span><span class="sxs-lookup"><span data-stu-id="5bb76-121">Adding BenefitHub from the gallery</span></span>
2. <span data-ttu-id="5bb76-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5bb76-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benefithub-from-the-gallery"></a><span data-ttu-id="5bb76-123">Dodawanie BenefitHub z galerii</span><span class="sxs-lookup"><span data-stu-id="5bb76-123">Adding BenefitHub from the gallery</span></span>
<span data-ttu-id="5bb76-124">Aby skonfigurować integrację usługi Azure AD BenefitHub, należy dodać BenefitHub z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5bb76-124">To configure the integration of BenefitHub into Azure AD, you need to add BenefitHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5bb76-125">**Aby dodać BenefitHub z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5bb76-125">**To add BenefitHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5bb76-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5bb76-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="5bb76-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5bb76-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5bb76-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5bb76-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="5bb76-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bb76-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="5bb76-133">W polu wyszukiwania wpisz **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="5bb76-133">In the search box, type **BenefitHub**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_search.png)

5. <span data-ttu-id="5bb76-135">W panelu wyników wybierz **BenefitHub**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="5bb76-135">In the results panel, select **BenefitHub**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5bb76-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5bb76-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5bb76-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z BenefitHub na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="5bb76-138">In this section, you configure and test Azure AD single sign-on with BenefitHub based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5bb76-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w BenefitHub jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bb76-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BenefitHub is to a user in Azure AD.</span></span> <span data-ttu-id="5bb76-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w BenefitHub musi się.</span><span class="sxs-lookup"><span data-stu-id="5bb76-140">In other words, a link relationship between an Azure AD user and the related user in BenefitHub needs to be established.</span></span>

<span data-ttu-id="5bb76-141">W BenefitHub, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="5bb76-141">In BenefitHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5bb76-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z BenefitHub, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="5bb76-142">To configure and test Azure AD single sign-on with BenefitHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5bb76-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5bb76-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5bb76-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5bb76-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5bb76-145">**[Tworzenie użytkownika testowego BenefitHub](#creating-a-benefithub-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta BenefitHub połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5bb76-145">**[Creating a BenefitHub test user](#creating-a-benefithub-test-user)** - to have a counterpart of Britta Simon in BenefitHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5bb76-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5bb76-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5bb76-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="5bb76-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5bb76-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5bb76-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5bb76-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="5bb76-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BenefitHub application.</span></span>

<span data-ttu-id="5bb76-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z BenefitHub, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5bb76-150">**To configure Azure AD single sign-on with BenefitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="5bb76-151">W portalu Azure na **BenefitHub** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="5bb76-151">In the Azure portal, on the **BenefitHub** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="5bb76-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="5bb76-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_samlbase.png)

3. <span data-ttu-id="5bb76-155">Na **BenefitHub domeny i adres URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5bb76-155">On the **BenefitHub Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_url1.png)
  
    <span data-ttu-id="5bb76-157">a.</span><span class="sxs-lookup"><span data-stu-id="5bb76-157">a.</span></span> <span data-ttu-id="5bb76-158">W **identyfikator** tekstowym, wpisz:`urn:benefithub:passport`</span><span class="sxs-lookup"><span data-stu-id="5bb76-158">In the **Identifier** textbox, type: `urn:benefithub:passport`</span></span>
    
    <span data-ttu-id="5bb76-159">b.</span><span class="sxs-lookup"><span data-stu-id="5bb76-159">b.</span></span> <span data-ttu-id="5bb76-160">W **adres URL odpowiedzi** tekstowym, wpisz:`https://passport.benefithub.info/saml/post/ac`</span><span class="sxs-lookup"><span data-stu-id="5bb76-160">In the **Reply URL** textbox, type: `https://passport.benefithub.info/saml/post/ac`</span></span>

4. <span data-ttu-id="5bb76-161">Aplikacja BenefitHub oczekuje potwierdzenia języka SAML w określonym formacie, musisz dodać mapowania atrybutu niestandardowego do konfiguracji atrybuty tokenu SAML.</span><span class="sxs-lookup"><span data-stu-id="5bb76-161">The BenefitHub application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="5bb76-162">Skonfiguruj następujące oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5bb76-162">Configure the following claims for this application.</span></span> <span data-ttu-id="5bb76-163">Możesz zarządzać wartości tych atrybutów z "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5bb76-163">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_attribute.png)

5. <span data-ttu-id="5bb76-165">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano na powyższej ilustracji i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5bb76-165">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the preceding image and perform the following steps:</span></span>
    
    | <span data-ttu-id="5bb76-166">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="5bb76-166">Attribute Name</span></span> | <span data-ttu-id="5bb76-167">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="5bb76-167">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="5bb76-168">identyfikatora organizacji</span><span class="sxs-lookup"><span data-stu-id="5bb76-168">organizationid</span></span> | <span data-ttu-id="5bb76-169">< identyfikatora organizacji ></span><span class="sxs-lookup"><span data-stu-id="5bb76-169">< organizationid ></span></span> |

    > [!NOTE]
    > <span data-ttu-id="5bb76-170">Ta wartość atrybutu nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="5bb76-170">This attribute value is not real.</span></span> <span data-ttu-id="5bb76-171">Zaktualizuj tę wartość z rzeczywistego identyfikatora organizacji.</span><span class="sxs-lookup"><span data-stu-id="5bb76-171">Update this value with actual organizationid.</span></span> <span data-ttu-id="5bb76-172">Skontaktuj się z [zespołem pomocy technicznej BenefitHub](https://www.benefithub.com/Home/ContactUs) Aby uzyskać rzeczywiste identyfikatora organizacji.</span><span class="sxs-lookup"><span data-stu-id="5bb76-172">Contact [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to get the actual organizationid.</span></span>
    
    <span data-ttu-id="5bb76-173">a.</span><span class="sxs-lookup"><span data-stu-id="5bb76-173">a.</span></span> <span data-ttu-id="5bb76-174">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bb76-174">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="5bb76-177">b.</span><span class="sxs-lookup"><span data-stu-id="5bb76-177">b.</span></span> <span data-ttu-id="5bb76-178">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="5bb76-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>
    
    <span data-ttu-id="5bb76-179">c.</span><span class="sxs-lookup"><span data-stu-id="5bb76-179">c.</span></span> <span data-ttu-id="5bb76-180">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="5bb76-180">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="5bb76-181">d.</span><span class="sxs-lookup"><span data-stu-id="5bb76-181">d.</span></span> <span data-ttu-id="5bb76-182">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="5bb76-182">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5bb76-183">Aby można było skonfigurować potwierdzenia języka SAML, należy skontaktować się z [BenefitHub pomocy technicznej](https://www.benefithub.com/Home/ContactUs) i zażądać wartość atrybutu Unikatowy identyfikator dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="5bb76-183">Before you can configure the SAML assertion, you need to contact your [BenefitHub support](https://www.benefithub.com/Home/ContactUs) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="5bb76-184">Należy tę wartość, aby skonfigurować niestandardowe oświadczeń dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5bb76-184">You need this value to configure the custom claim for your application.</span></span>

6. <span data-ttu-id="5bb76-185">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5bb76-185">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_certificate.png) 

7. <span data-ttu-id="5bb76-187">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5bb76-187">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benefithub-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="5bb76-189">Skonfigurować logowanie jednokrotne w **BenefitHub** stronie, musisz wysłać pobrany **XML metadanych** do [zespołem pomocy technicznej BenefitHub](https://www.benefithub.com/Home/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="5bb76-189">To configure single sign-on on **BenefitHub** side, you need to send the downloaded **Metadata XML** to [BenefitHub support team](https://www.benefithub.com/Home/ContactUs).</span></span> <span data-ttu-id="5bb76-190">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="5bb76-190">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="5bb76-191">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="5bb76-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5bb76-192">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="5bb76-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5bb76-193">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5bb76-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5bb76-194">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bb76-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="5bb76-195">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5bb76-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="5bb76-197">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5bb76-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5bb76-198">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5bb76-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5bb76-200">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="5bb76-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5bb76-202">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bb76-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5bb76-204">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5bb76-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5bb76-206">a.</span><span class="sxs-lookup"><span data-stu-id="5bb76-206">a.</span></span> <span data-ttu-id="5bb76-207">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5bb76-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5bb76-208">b.</span><span class="sxs-lookup"><span data-stu-id="5bb76-208">b.</span></span> <span data-ttu-id="5bb76-209">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5bb76-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5bb76-210">c.</span><span class="sxs-lookup"><span data-stu-id="5bb76-210">c.</span></span> <span data-ttu-id="5bb76-211">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="5bb76-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5bb76-212">d.</span><span class="sxs-lookup"><span data-stu-id="5bb76-212">d.</span></span> <span data-ttu-id="5bb76-213">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5bb76-213">Click **Create**.</span></span>
 
### <a name="creating-a-benefithub-test-user"></a><span data-ttu-id="5bb76-214">Tworzenie użytkownika testowego BenefitHub</span><span class="sxs-lookup"><span data-stu-id="5bb76-214">Creating a BenefitHub test user</span></span>

<span data-ttu-id="5bb76-215">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="5bb76-215">In this section, you create a user called Britta Simon in BenefitHub.</span></span> <span data-ttu-id="5bb76-216">Praca z [zespołem pomocy technicznej BenefitHub](https://www.benefithub.com/Home/ContactUs) Aby dodać użytkowników do platformy BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="5bb76-216">Work with [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to add the users in the BenefitHub platform.</span></span> <span data-ttu-id="5bb76-217">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5bb76-217">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5bb76-218">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bb76-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5bb76-219">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="5bb76-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BenefitHub.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="5bb76-221">**Aby przypisać Simona Britta BenefitHub, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5bb76-221">**To assign Britta Simon to BenefitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="5bb76-222">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5bb76-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5bb76-224">Na liście aplikacji zaznacz **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="5bb76-224">In the applications list, select **BenefitHub**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_app.png) 

3. <span data-ttu-id="5bb76-226">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5bb76-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="5bb76-228">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5bb76-228">Click **Add** button.</span></span> <span data-ttu-id="5bb76-229">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bb76-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="5bb76-231">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="5bb76-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5bb76-232">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bb76-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5bb76-233">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5bb76-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5bb76-234">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5bb76-234">Testing single sign-on</span></span>

<span data-ttu-id="5bb76-235">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5bb76-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5bb76-236">Po kliknięciu kafelka BenefitHub w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="5bb76-236">When you click the BenefitHub tile in the Access Panel, you should get automatically signed-on to your BenefitHub application.</span></span>
<span data-ttu-id="5bb76-237">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="5bb76-237">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5bb76-238">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5bb76-238">Additional resources</span></span>

* [<span data-ttu-id="5bb76-239">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5bb76-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5bb76-240">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5bb76-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_203.png

