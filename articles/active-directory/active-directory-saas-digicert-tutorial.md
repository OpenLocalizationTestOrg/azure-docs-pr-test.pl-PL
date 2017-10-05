---
title: 'Samouczek: Integracji Azure Active Directory z DigiCert | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i DigiCert."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 646f3129-aa67-4875-9073-1d0b6a3173d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 2ceb3c0833edcd4ecd875c5e8006961ed7216c66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-digicert"></a><span data-ttu-id="7fb00-103">Samouczek: Integracji Azure Active Directory z DigiCert</span><span class="sxs-lookup"><span data-stu-id="7fb00-103">Tutorial: Azure Active Directory integration with DigiCert</span></span>

<span data-ttu-id="7fb00-104">Z tego samouczka dowiesz się integrowanie DigiCert z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7fb00-104">In this tutorial, you learn how to integrate DigiCert with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7fb00-105">Integracja z usługą Azure AD DigiCert zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="7fb00-105">Integrating DigiCert with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7fb00-106">Można kontrolować w usłudze Azure AD, który ma dostęp do DigiCert</span><span class="sxs-lookup"><span data-stu-id="7fb00-106">You can control in Azure AD who has access to DigiCert</span></span>
- <span data-ttu-id="7fb00-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do DigiCert (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fb00-107">You can enable your users to automatically get signed-on to DigiCert (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7fb00-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="7fb00-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7fb00-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7fb00-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7fb00-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7fb00-110">Prerequisites</span></span>

<span data-ttu-id="7fb00-111">Aby skonfigurować integrację usługi Azure AD z DigiCert, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="7fb00-111">To configure Azure AD integration with DigiCert, you need the following items:</span></span>

- <span data-ttu-id="7fb00-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fb00-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7fb00-113">DigiCert logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7fb00-113">A DigiCert single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7fb00-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="7fb00-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7fb00-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="7fb00-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7fb00-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="7fb00-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7fb00-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7fb00-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7fb00-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="7fb00-118">Scenario description</span></span>
<span data-ttu-id="7fb00-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="7fb00-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7fb00-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="7fb00-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7fb00-121">Dodawanie DigiCert z galerii</span><span class="sxs-lookup"><span data-stu-id="7fb00-121">Adding DigiCert from the gallery</span></span>
2. <span data-ttu-id="7fb00-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="7fb00-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-digicert-from-the-gallery"></a><span data-ttu-id="7fb00-123">Dodawanie DigiCert z galerii</span><span class="sxs-lookup"><span data-stu-id="7fb00-123">Adding DigiCert from the gallery</span></span>
<span data-ttu-id="7fb00-124">Aby skonfigurować integrację usługi Azure AD DigiCert, należy dodać DigiCert z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="7fb00-124">To configure the integration of DigiCert into Azure AD, you need to add DigiCert from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7fb00-125">**Aby dodać DigiCert z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7fb00-125">**To add DigiCert from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7fb00-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="7fb00-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="7fb00-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="7fb00-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7fb00-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7fb00-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="7fb00-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7fb00-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="7fb00-133">W polu wyszukiwania wpisz **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="7fb00-133">In the search box, type **DigiCert**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_search.png)

5. <span data-ttu-id="7fb00-135">W panelu wyników wybierz **DigiCert**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="7fb00-135">In the results panel, select **DigiCert**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7fb00-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="7fb00-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7fb00-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z DigiCert na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="7fb00-138">In this section, you configure and test Azure AD single sign-on with DigiCert based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7fb00-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w DigiCert jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7fb00-139">For single sign-on to work, Azure AD needs to know what the counterpart user in DigiCert is to a user in Azure AD.</span></span> <span data-ttu-id="7fb00-140">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w DigiCert musi się.</span><span class="sxs-lookup"><span data-stu-id="7fb00-140">In other words, a link relationship between an Azure AD user and the related user in DigiCert needs to be established.</span></span>

<span data-ttu-id="7fb00-141">W DigiCert, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="7fb00-141">In DigiCert, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7fb00-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z DigiCert, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="7fb00-142">To configure and test Azure AD single sign-on with DigiCert, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7fb00-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="7fb00-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7fb00-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7fb00-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7fb00-145">**[Tworzenie użytkownika testowego DigiCert](#creating-a-digicert-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta DigiCert połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7fb00-145">**[Creating a DigiCert test user](#creating-a-digicert-test-user)** - to have a counterpart of Britta Simon in DigiCert that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7fb00-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="7fb00-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7fb00-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="7fb00-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7fb00-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7fb00-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7fb00-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w aplikacji DigiCert.</span><span class="sxs-lookup"><span data-stu-id="7fb00-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your DigiCert application.</span></span>

<span data-ttu-id="7fb00-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z DigiCert, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7fb00-150">**To configure Azure AD single sign-on with DigiCert, perform the following steps:**</span></span>

1. <span data-ttu-id="7fb00-151">W portalu Azure na **DigiCert** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="7fb00-151">In the Azure portal, on the **DigiCert** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="7fb00-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="7fb00-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_samlbase.png)

3. <span data-ttu-id="7fb00-155">Na **DigiCert domeny i adres URL** sekcji, użytkownik nie trzeba wykonywać żadnych czynności, jak aplikacja już jest wstępna Integracja z usługą Azure.</span><span class="sxs-lookup"><span data-stu-id="7fb00-155">On the **DigiCert Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_url.png)

4. <span data-ttu-id="7fb00-157">Aplikacja firmy DigiCert oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="7fb00-157">DigiCert application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="7fb00-158">Skonfiguruj następujące oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7fb00-158">Configure the following claims for this application.</span></span> <span data-ttu-id="7fb00-159">Możesz zarządzać wartości tych atrybutów z "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7fb00-159">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="7fb00-160">Poniższy zrzut ekranu przedstawia przykład dla tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="7fb00-160">The following screenshot shows an example for this configuration.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_attributes.png)
    
5. <span data-ttu-id="7fb00-162">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie i wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7fb00-162">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="7fb00-163">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="7fb00-163">Attribute Name</span></span> | <span data-ttu-id="7fb00-164">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="7fb00-164">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="7fb00-165">Firmy</span><span class="sxs-lookup"><span data-stu-id="7fb00-165">company</span></span> | <span data-ttu-id="7fb00-166">< companycode ></span><span class="sxs-lookup"><span data-stu-id="7fb00-166">< companycode ></span></span> |
    | <span data-ttu-id="7fb00-167">digicertrole</span><span class="sxs-lookup"><span data-stu-id="7fb00-167">digicertrole</span></span> | <span data-ttu-id="7fb00-168">CanAccessCertCentral</span><span class="sxs-lookup"><span data-stu-id="7fb00-168">CanAccessCertCentral</span></span> |

    > [!Note]
    > <span data-ttu-id="7fb00-169">Wartość **firmy** atrybut nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="7fb00-169">The value of **company** attribute is not real.</span></span> <span data-ttu-id="7fb00-170">Zaktualizuj tę wartość z kodem rzeczywiste firmy.</span><span class="sxs-lookup"><span data-stu-id="7fb00-170">Update this value with actual company code.</span></span> <span data-ttu-id="7fb00-171">Aby uzyskać wartość **firmy** atrybutu skontaktuj się z [zespołem pomocy technicznej firmy DigiCert](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="7fb00-171">To get the value of **company** attribute contact [DigiCert support team](mailto:support@digicert.com).</span></span>

    <span data-ttu-id="7fb00-172">a.</span><span class="sxs-lookup"><span data-stu-id="7fb00-172">a.</span></span> <span data-ttu-id="7fb00-173">Kliknij przycisk **Dodaj atrybut** otworzyć **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7fb00-173">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-digicert-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="7fb00-176">b.</span><span class="sxs-lookup"><span data-stu-id="7fb00-176">b.</span></span> <span data-ttu-id="7fb00-177">W **nazwa** tekstowym, wpisz nazwę atrybut wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="7fb00-177">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="7fb00-178">c.</span><span class="sxs-lookup"><span data-stu-id="7fb00-178">c.</span></span> <span data-ttu-id="7fb00-179">Z **wartość** listy, wpisz wartość atrybutu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="7fb00-179">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="7fb00-180">d.</span><span class="sxs-lookup"><span data-stu-id="7fb00-180">d.</span></span> <span data-ttu-id="7fb00-181">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="7fb00-181">Click **Ok**.</span></span> 

6. <span data-ttu-id="7fb00-182">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="7fb00-182">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_certificate.png) 

7. <span data-ttu-id="7fb00-184">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7fb00-184">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-digicert-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="7fb00-186">Do konfigurowania rejestracji jednokrotnej na **DigiCert** stronie, musisz wysłać pobrany **XML metadanych** do [zespołem pomocy technicznej firmy DigiCert](mailto:support@digicert.com).</span><span class="sxs-lookup"><span data-stu-id="7fb00-186">To configure single sign-on on **DigiCert** side, you need to send the downloaded **Metadata XML** to [DigiCert support team](mailto:support@digicert.com).</span></span> <span data-ttu-id="7fb00-187">To ustawienie, aby były prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one wartość.</span><span class="sxs-lookup"><span data-stu-id="7fb00-187">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="7fb00-188">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="7fb00-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7fb00-189">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="7fb00-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7fb00-190">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7fb00-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7fb00-191">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fb00-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="7fb00-192">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7fb00-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="7fb00-194">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7fb00-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7fb00-195">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="7fb00-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7fb00-197">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="7fb00-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7fb00-199">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7fb00-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7fb00-201">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7fb00-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-digicert-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7fb00-203">a.</span><span class="sxs-lookup"><span data-stu-id="7fb00-203">a.</span></span> <span data-ttu-id="7fb00-204">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7fb00-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7fb00-205">b.</span><span class="sxs-lookup"><span data-stu-id="7fb00-205">b.</span></span> <span data-ttu-id="7fb00-206">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7fb00-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7fb00-207">c.</span><span class="sxs-lookup"><span data-stu-id="7fb00-207">c.</span></span> <span data-ttu-id="7fb00-208">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="7fb00-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7fb00-209">d.</span><span class="sxs-lookup"><span data-stu-id="7fb00-209">d.</span></span> <span data-ttu-id="7fb00-210">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7fb00-210">Click **Create**.</span></span>
 
### <a name="creating-a-digicert-test-user"></a><span data-ttu-id="7fb00-211">Tworzenie użytkownika testowego DigiCert</span><span class="sxs-lookup"><span data-stu-id="7fb00-211">Creating a DigiCert test user</span></span>

<span data-ttu-id="7fb00-212">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w DigiCert.</span><span class="sxs-lookup"><span data-stu-id="7fb00-212">In this section, you create a user called Britta Simon in DigiCert.</span></span> <span data-ttu-id="7fb00-213">We współpracy z [zespołem pomocy technicznej firmy DigiCert](mailto:support@digicert.com) Aby dodać użytkowników w DigiCert.</span><span class="sxs-lookup"><span data-stu-id="7fb00-213">Please work with [DigiCert support team](mailto:support@digicert.com) to add the users in DigiCert.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7fb00-214">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7fb00-214">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7fb00-215">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do firmy DigiCert.</span><span class="sxs-lookup"><span data-stu-id="7fb00-215">In this section, you enable Britta Simon to use Azure single sign-on by granting access to DigiCert.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="7fb00-217">**Aby przypisać Simona Britta DigiCert, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7fb00-217">**To assign Britta Simon to DigiCert, perform the following steps:**</span></span>

1. <span data-ttu-id="7fb00-218">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7fb00-218">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="7fb00-220">Na liście aplikacji zaznacz **DigiCert**.</span><span class="sxs-lookup"><span data-stu-id="7fb00-220">In the applications list, select **DigiCert**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-digicert-tutorial/tutorial_digicert_app.png) 

3. <span data-ttu-id="7fb00-222">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="7fb00-222">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="7fb00-224">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7fb00-224">Click **Add** button.</span></span> <span data-ttu-id="7fb00-225">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7fb00-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="7fb00-227">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="7fb00-227">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7fb00-228">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7fb00-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7fb00-229">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7fb00-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7fb00-230">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7fb00-230">Testing single sign-on</span></span>

<span data-ttu-id="7fb00-231">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="7fb00-231">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7fb00-232">Po kliknięciu kafelka DigiCert w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji DeigiCert.</span><span class="sxs-lookup"><span data-stu-id="7fb00-232">When you click the DigiCert tile in the Access Panel, you should get automatically signed-on to your DeigiCert application.</span></span>
<span data-ttu-id="7fb00-233">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7fb00-233">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7fb00-234">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="7fb00-234">Additional resources</span></span>

* [<span data-ttu-id="7fb00-235">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7fb00-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7fb00-236">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7fb00-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-digicert-tutorial/tutorial_general_203.png

