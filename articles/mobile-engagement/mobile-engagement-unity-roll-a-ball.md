---
title: "Wycofaj Unity samouczek piłka"
description: "Kroki, aby utworzyć klasycznego Unity Przywróć gra w piłkę, czyli jako warunek wstępny dla wszystkich samouczków Unity usługi Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0afd0eca-f74a-43aa-bba8-436a0265c312
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 6392d1f780b1bc2348fee5947550b05e86ea4de2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="730b5-103"><a id="unity-roll-a-ball"></a>Utwórz Przywróć Unity grę piłka</span><span class="sxs-lookup"><span data-stu-id="730b5-103"><a id="unity-roll-a-ball"></a>Create Unity Roll a Ball game</span></span>
<span data-ttu-id="730b5-104">Ten samouczek przedstawia kroki głównego nieco zmodyfikowany [Unity Przywróć samouczek piłka](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span><span class="sxs-lookup"><span data-stu-id="730b5-104">This tutorial walks through the main steps for a slightly modified [Unity Roll a Ball tutorial](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span></span> <span data-ttu-id="730b5-105">Gry próbki składa się z obiektu kulistego player, który jest kontrolowany przez użytkownika aplikacji i celem gry jest "zbieranie" kolekcjonowanych obiektów przez kolizji obiektu player z tymi obiektami kolekcjonowanych.</span><span class="sxs-lookup"><span data-stu-id="730b5-105">This sample game consists of a spherical 'player' object which is controlled by the app user and the objective of the game is to 'collect' collectible objects by colliding the player object with these collectible objects.</span></span> <span data-ttu-id="730b5-106">Przy założeniu, podstawowa znajomość środowiska Edytor platformy Unity.</span><span class="sxs-lookup"><span data-stu-id="730b5-106">This assumes basic familiarity with Unity editor environment.</span></span> <span data-ttu-id="730b5-107">Jeśli wystąpiły problemy powinien zapoznaj się z samouczkiem pełna.</span><span class="sxs-lookup"><span data-stu-id="730b5-107">If you run into any issues then you should refer to the full tutorial.</span></span> 

### <a name="setting-up-the-game"></a><span data-ttu-id="730b5-108">Konfigurowanie gry</span><span class="sxs-lookup"><span data-stu-id="730b5-108">Setting up the game</span></span>
<span data-ttu-id="730b5-109">Poniższe kroki są z [samouczek Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="730b5-109">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span></span>

1. <span data-ttu-id="730b5-110">Otwórz **Edytor platformy Unity** i kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="730b5-110">Open **Unity Editor** and click **New**.</span></span> 
   
    ![][51] 
2. <span data-ttu-id="730b5-111">Podaj **Nazwa projektu** & **lokalizacji**, wybierz pozycję **3D** i kliknij przycisk **Tworzenie projektu**.</span><span class="sxs-lookup"><span data-stu-id="730b5-111">Provide a **Project name** & **Location**, select **3D** and click **Create project**.</span></span>
   
    ![][52]
3. <span data-ttu-id="730b5-112">Zapisz sceny domyślne właśnie utworzony jako część nowego projektu jako o nazwie **MiniGame** w ramach nowej  **\_sceny** folder **zasoby** folderu:</span><span class="sxs-lookup"><span data-stu-id="730b5-112">Save the default scene just created as part of the new project as with the name **MiniGame** within a new **\_Scenes** folder under **Assets** folder:</span></span>
   
    ![][53]
4. <span data-ttu-id="730b5-113">Utwórz **obiektu 3D -> płaszczyzny** jako odtwarzanie i zmienić nazwę tego obiektu płaszczyzny jako **podstaw**</span><span class="sxs-lookup"><span data-stu-id="730b5-113">Create a **3D Object -> Plane** as the playing field and rename this plane object as **Ground**</span></span>
   
    ![][1]
5. <span data-ttu-id="730b5-114">Resetuj składnika transformacji dla tego **podstaw** obiekt tak, aby w źródle.</span><span class="sxs-lookup"><span data-stu-id="730b5-114">Reset the transform component for this **Ground** object so that it is at the Origin.</span></span> 
   
    ![][3]
6. <span data-ttu-id="730b5-115">Usuń zaznaczenie pola wyboru **Pokaż siatkę** z **Gizmos menu** dla **podstaw** obiektu.</span><span class="sxs-lookup"><span data-stu-id="730b5-115">Uncheck **Show Grid** from **Gizmos menu** for the **Ground** object.</span></span>
   
    ![][4]
7. <span data-ttu-id="730b5-116">Aktualizacja **skali** składnik **podstaw** być obiekt [X = 2, T = 1, Z = 2].</span><span class="sxs-lookup"><span data-stu-id="730b5-116">Update the **Scale** component for the **Ground** object to be [X = 2,Y = 1, Z = 2].</span></span> 
   
    ![][5]
8. <span data-ttu-id="730b5-117">Dodaj nową **obiektu 3D -> kuli** do projektu i Zmień nazwę tego kuli obiekt jako **Player**.</span><span class="sxs-lookup"><span data-stu-id="730b5-117">Add a new **3D Object -> Sphere** to the project and rename this sphere object as **Player**.</span></span> 
   
    ![][6]
9. <span data-ttu-id="730b5-118">Wybierz **Player** obiekt i kliknij przycisk **zresetować przekształcenie** podobny do obiektu płaszczyzny.</span><span class="sxs-lookup"><span data-stu-id="730b5-118">Select the **Player** object and click **Reset Transform** similar to the Plane object.</span></span> 
10. <span data-ttu-id="730b5-119">Aktualizacja **Transform -> pozycji -> współrzędną Y** składnika y Player jako 0,5.</span><span class="sxs-lookup"><span data-stu-id="730b5-119">Update **Transform -> Position -> Y Coordinate** component for the Player Y as 0.5.</span></span>  
    
    ![][7]
11. <span data-ttu-id="730b5-120">Utwórz nowy folder o nazwie **materiałów** w projekcie, gdzie utworzymy materiały do odtwarzacza kolorów.</span><span class="sxs-lookup"><span data-stu-id="730b5-120">Create a new folder called **Materials** in the project where we will create the material to color the player.</span></span> 
12. <span data-ttu-id="730b5-121">Utwórz nową **materiału** o nazwie **tła** w tym folderze.</span><span class="sxs-lookup"><span data-stu-id="730b5-121">Create a new **Material** called **Background** in this folder.</span></span> 
    
    ![][8]
13. <span data-ttu-id="730b5-122">Zaktualizuj kolor materiałów, aktualizując **Albedo** jego właściwości.</span><span class="sxs-lookup"><span data-stu-id="730b5-122">Update the color of the material by updating the **Albedo** property of it.</span></span> <span data-ttu-id="730b5-123">Można wybrać wartości RGB [0,32,64].</span><span class="sxs-lookup"><span data-stu-id="730b5-123">You can select the RGB values of [0,32,64].</span></span> 
    
    ![][9]
14. <span data-ttu-id="730b5-124">Przeciągnij w tym materiale do widoku sceny umożliwia stosowanie koloru do **podstaw** obiektu.</span><span class="sxs-lookup"><span data-stu-id="730b5-124">Drag this material into the scene view to apply color to the **Ground** object.</span></span> 
    
    ![][10]
15. <span data-ttu-id="730b5-125">Na koniec zaktualizuj **Transform -> Obrót -> Y** do 60 obiektu światła dla uzyskania przejrzystości.</span><span class="sxs-lookup"><span data-stu-id="730b5-125">Finally update the **Transform -> Rotation -> Y** to 60 on the Directional Light object for clarity.</span></span> 
    
    ![][12]

### <a name="moving-the-player"></a><span data-ttu-id="730b5-126">Przenoszenie Windows Media player</span><span class="sxs-lookup"><span data-stu-id="730b5-126">Moving the player</span></span>
<span data-ttu-id="730b5-127">Poniższe kroki są z [samouczek Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="730b5-127">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span></span>

1. <span data-ttu-id="730b5-128">Dodaj **RigidBody** składnika do **Player** obiektu.</span><span class="sxs-lookup"><span data-stu-id="730b5-128">Add a **RigidBody** component to the **Player** object.</span></span> 
   
    ![][13]
2. <span data-ttu-id="730b5-129">Utwórz nowy folder o nazwie **skryptów** w projekcie.</span><span class="sxs-lookup"><span data-stu-id="730b5-129">Create a new folder called **Scripts** in the Project.</span></span> 
3. <span data-ttu-id="730b5-130">Kliknij przycisk **Dodaj składnik -> Nowy skrypt -> C# skrypt**.</span><span class="sxs-lookup"><span data-stu-id="730b5-130">Click **Add Component-> New Script -> C# Script**.</span></span> <span data-ttu-id="730b5-131">Nadaj mu nazwę **PlayerController**i kliknij przycisk **Utwórz i Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="730b5-131">Name it **PlayerController**, and click **Create and Add**.</span></span> <span data-ttu-id="730b5-132">Spowoduje to utworzenie i Dołącz skrypt do obiektu Player.</span><span class="sxs-lookup"><span data-stu-id="730b5-132">This will create and attach a script to the Player object.</span></span>  
   
    ![][14]
4. <span data-ttu-id="730b5-133">Przenieś ten skrypt, w obszarze **skryptów** folderu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="730b5-133">Move this script under the **Scripts** folder in the project.</span></span> 
5. <span data-ttu-id="730b5-134">Otwórz skrypt do edycji w Edytorze skryptów Ulubione, zaktualizuj kod skryptu z następującym kodem i zapisz go.</span><span class="sxs-lookup"><span data-stu-id="730b5-134">Open the script for editing in your favorite script editor, update the script code with the following code and save it.</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour 
        {
            public float speed;
            private Rigidbody rb;
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
                rb.AddForce (movement * speed);
            }
        }
6. <span data-ttu-id="730b5-135">Należy pamiętać, że skrypt powyżej używa **szybkości** właściwości.</span><span class="sxs-lookup"><span data-stu-id="730b5-135">Note that the script above uses a **Speed** property.</span></span> <span data-ttu-id="730b5-136">W edytorze Unity zaktualizuj właściwość szybkości do 10.</span><span class="sxs-lookup"><span data-stu-id="730b5-136">In the Unity editor, update the speed property to 10.</span></span>  
   
    ![][15]
7. <span data-ttu-id="730b5-137">Trafienia **odtwarzanie** Edytor platformy Unity.</span><span class="sxs-lookup"><span data-stu-id="730b5-137">Hit **Play** in the Unity Editor.</span></span> <span data-ttu-id="730b5-138">Teraz powinno być możliwe do kontrolowania piłka przy użyciu klawiatury i powinna obracania i przenoszenia.</span><span class="sxs-lookup"><span data-stu-id="730b5-138">Now you should be able to control the ball using the keyboard and it should rotate and move around.</span></span> 

### <a name="moving-the-camera"></a><span data-ttu-id="730b5-139">Przenoszenie aparatu</span><span class="sxs-lookup"><span data-stu-id="730b5-139">Moving the camera</span></span>
<span data-ttu-id="730b5-140">Poniższe kroki są z [samouczek Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) i będzie powiązać **głównego aparatu** do **Player** obiektu.</span><span class="sxs-lookup"><span data-stu-id="730b5-140">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) and will tie the **Main Camera** to the **Player** object.</span></span> 

1. <span data-ttu-id="730b5-141">Aktualizacja **Transform.Position** jako X = 0, Y = 10.5, Z =-10.</span><span class="sxs-lookup"><span data-stu-id="730b5-141">Update the **Transform.Position** to be X = 0,  Y = 10.5, Z=-10.</span></span>  
2. <span data-ttu-id="730b5-142">Aktualizacja **Transform.Rotation** jako X = 45, Y = 0, Z = 0.</span><span class="sxs-lookup"><span data-stu-id="730b5-142">Update the **Transform.Rotation** to be X = 45, Y = 0, Z = 0.</span></span>  
   
    ![][16]
3. <span data-ttu-id="730b5-143">Dodaj nowy skrypt o nazwie **CameraController** do **MainCamera** i umieści ją w folderze skryptów.</span><span class="sxs-lookup"><span data-stu-id="730b5-143">Add a new script called **CameraController** to the **MainCamera** and move it under the Scripts folder.</span></span> 
   
    ![][17]
4. <span data-ttu-id="730b5-144">Otwarcie skryptu do edycji i Dodaj następujący kod w tym:</span><span class="sxs-lookup"><span data-stu-id="730b5-144">Open up the script for editing and add the following code in it:</span></span>
   
        using UnityEngine;
        using System.Collections;
   
        public class CameraController : MonoBehaviour {
   
            public GameObject player;
   
            private Vector3 offset;
   
            void Start ()
            {
                offset = transform.position - player.transform.position;
            }
   
            void LateUpdate ()
            {
                transform.position = player.transform.position + offset;
            }
        }
5. <span data-ttu-id="730b5-145">W środowisku Unity — przeciągnij zmiennej Player w gnieździe odtwarzacza dla obiektu głównego aparatu tak, aby dwa są skojarzone ze sobą.</span><span class="sxs-lookup"><span data-stu-id="730b5-145">In Unity environment - drag the Player variable into the Player slot for the Main Camera object so that the two are associated with one another.</span></span> 
   
    ![][18]
6. <span data-ttu-id="730b5-146">Jeśli naciśnij pozycję Odtwórz w edytorze Unity i obrót obiektu Player piłka następnie zostanie wyświetlone aparatu w ruchu.</span><span class="sxs-lookup"><span data-stu-id="730b5-146">Now if you hit Play in the Unity editor and rotate the Player Ball object then you will see the Camera following it in the movement.</span></span>  

### <a name="setting-up-the-play-area"></a><span data-ttu-id="730b5-147">Konfigurowanie obszaru odtwarzania</span><span class="sxs-lookup"><span data-stu-id="730b5-147">Setting up the Play area</span></span>
<span data-ttu-id="730b5-148">Poniższe kroki są z [samouczek Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="730b5-148">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span></span> <span data-ttu-id="730b5-149">Utworzymy ściany otaczającego podstaw, dzięki czemu obiektu Player piłka nie pozostawienia obszaru odtwarzania w ruchu.</span><span class="sxs-lookup"><span data-stu-id="730b5-149">We will create the Walls surrounding the Ground so that the Player Ball object doesn't drop off the play area in its movement.</span></span> 

1. <span data-ttu-id="730b5-150">Kliknij przycisk **Utwórz -> Utwórz pusty -> obiekt gry** i nadaj mu nazwę **ściany**</span><span class="sxs-lookup"><span data-stu-id="730b5-150">Click **Create -> Create Empty -> Game Object** and name it **Walls**</span></span>
   
    ![][19]
2. <span data-ttu-id="730b5-151">W tym obiektu ściany — Utwórz nową **obiektu 3D -> modułu** i nadaj jej nazwę na "Zachodnie tablicy".</span><span class="sxs-lookup"><span data-stu-id="730b5-151">Under this Walls object - create a new **3D Object -> Cube** and name it "West wall".</span></span> 
   
    ![][20]
3. <span data-ttu-id="730b5-152">Aktualizacji **Transform -> pozycji** i **Transform -> skali** dla tego obiektu zachodnie tablicy.</span><span class="sxs-lookup"><span data-stu-id="730b5-152">Update the **Transform -> Position** and **Transform -> Scale** for this West Wall object.</span></span> 
   
    ![][21]
4. <span data-ttu-id="730b5-153">Zduplikowana wall Zachodnia, aby utworzyć **wall wschód** z zaktualizowanego przekształcenie położenie i Skala.</span><span class="sxs-lookup"><span data-stu-id="730b5-153">Duplicate the West wall to create an **East wall** with the updated transform position and scale.</span></span> 
   
    ![][22]
5. <span data-ttu-id="730b5-154">Zduplikowana tablicy Wschodnia, aby utworzyć **wall Północna** z zaktualizowanego przekształcenie pozycji & skali.</span><span class="sxs-lookup"><span data-stu-id="730b5-154">Duplicate the East wall to create a **North wall** with the updated transform position & scale.</span></span> 
   
    ![][23]
6. <span data-ttu-id="730b5-155">Zduplikowana wall Północna i Utwórz **wall Południowa** z zaktualizowanego przekształcenie pozycji & skali.</span><span class="sxs-lookup"><span data-stu-id="730b5-155">Duplicate the North wall and create a **South wall** with the updated transform position & scale.</span></span> 
   
    ![][24]

### <a name="creating-collectible-objects"></a><span data-ttu-id="730b5-156">Tworzenie obiektów kolekcjonowanych</span><span class="sxs-lookup"><span data-stu-id="730b5-156">Creating Collectible objects</span></span>
<span data-ttu-id="730b5-157">Poniższe kroki są z [samouczek Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="730b5-157">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span></span> <span data-ttu-id="730b5-158">Utworzymy niektórych atrakcyjne obiektów wyglądającej stanowiące zestawu kolekcjonowanego obiektów, które obiekt piłka Player musi zebrać przez kolizji z nich.</span><span class="sxs-lookup"><span data-stu-id="730b5-158">We will create some attractive looking objects which will form the set of collectible objects which the Player Ball object needs to 'collect' by colliding with them.</span></span> 

1. <span data-ttu-id="730b5-159">Utwórz nową **3D obiektu modułu** i nadaj mu nazwę pobrania.</span><span class="sxs-lookup"><span data-stu-id="730b5-159">Create a new **3D Cube object** and name it Pickup.</span></span> 
2. <span data-ttu-id="730b5-160">Dostosuj **Transform -> Obrót** & **Transform -> skali** podnoszenia obiektu.</span><span class="sxs-lookup"><span data-stu-id="730b5-160">Adjust the **Transform -> Rotation** & **Transform -> Scale** of the Pickup object.</span></span> 
   
    ![][25]
3. <span data-ttu-id="730b5-161">Utwórz i Dołącz **nowego skryptu C#** o nazwie **Rotator** do pobrania obiektu.</span><span class="sxs-lookup"><span data-stu-id="730b5-161">Create and attach a **new C# Script** called **Rotator** to the Pickup object.</span></span> <span data-ttu-id="730b5-162">Upewnij się umieścić skrypt w folderze skryptów.</span><span class="sxs-lookup"><span data-stu-id="730b5-162">Make sure to put the script under the Scripts folder.</span></span> 
   
    ![][26]
4. <span data-ttu-id="730b5-163">Otwórz ten skrypt do edycji i zaktualizować go na następujący:</span><span class="sxs-lookup"><span data-stu-id="730b5-163">Open this script for editing and update it to be the following:</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. <span data-ttu-id="730b5-164">Teraz trafiony tryb gry w edytorze Unity i pokazu podnoszenia obiektu można obracanie na osi.</span><span class="sxs-lookup"><span data-stu-id="730b5-164">Now hit the Play mode in the Unity Editor and your Pickup object show be rotating on its axis.</span></span>
6. <span data-ttu-id="730b5-165">Utwórz nowy folder o nazwie **Prefabs**</span><span class="sxs-lookup"><span data-stu-id="730b5-165">Create a new folder called **Prefabs**</span></span> 
   
    ![][27]
7. <span data-ttu-id="730b5-166">Przeciągnij **podnoszenia** obiektu i umieść ją w folderze Prefabs.</span><span class="sxs-lookup"><span data-stu-id="730b5-166">Drag the **Pickup** object and put it in the Prefabs folder.</span></span>
   
    ![][28]
8. <span data-ttu-id="730b5-167">Utwórz nową **gry pusty obiekt** o nazwie **Pickups**.</span><span class="sxs-lookup"><span data-stu-id="730b5-167">Create a new **Empty Game object** called **Pickups**.</span></span> <span data-ttu-id="730b5-168">Resetowanie położenia do źródła, a następnie przeciągnij podnoszenia obiektu pod ten obiekt gier.</span><span class="sxs-lookup"><span data-stu-id="730b5-168">Reset its position to origin and then drag the Pickup object under this game object.</span></span>  
   
    ![][29]
9. <span data-ttu-id="730b5-169">Zduplikowana **podnoszenia** obiekt i utworzyć na **podstaw** obiekt wokół **Player** obiektu aktualizując **X & ZTransform.Positionw** odpowiednio wartości.</span><span class="sxs-lookup"><span data-stu-id="730b5-169">Duplicate the **Pickup** object and spread it on the **Ground** object around the **Player** object by updating the **Transform.Position's X & Z** values appropriately.</span></span> 
   
    ![][30]
10. <span data-ttu-id="730b5-170">Utwórz **nowe materiały** o nazwie **podnoszenia** i zaktualizować je będzie kolor czerwony, aktualizując **właściwości Albedo** podobnie jak robiliśmy dla obiekt podstaw aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="730b5-170">Create a **new material** called **Pickup** and update it to be Red in color by updating the **Albedo property** similar to what we did for updating the Ground object.</span></span> 
    
    ![][31]
11. <span data-ttu-id="730b5-171">Zastosuj materiałów do 4 podnoszenia obiektów.</span><span class="sxs-lookup"><span data-stu-id="730b5-171">Apply the material to all the 4 pickup objects.</span></span>
    
    ![][32]

### <a name="collecting-the-pickup-objects"></a><span data-ttu-id="730b5-172">Zbieranie obiektów podnoszenia</span><span class="sxs-lookup"><span data-stu-id="730b5-172">Collecting the Pickup objects</span></span>
<span data-ttu-id="730b5-173">Poniższe kroki są z [samouczek Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="730b5-173">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span></span> <span data-ttu-id="730b5-174">Odtwarzacz będą aktualizowane tak, że jest w stanie "collect" podnoszenia obiektów przez kolizji z nich.</span><span class="sxs-lookup"><span data-stu-id="730b5-174">We will update the Player so that it is able to 'collect' the pickup objects by colliding with them.</span></span> 

1. <span data-ttu-id="730b5-175">Otwórz **PlayerController** skryptu dołączony do obiektu Player do edycji i zaktualizować ją do następującego:</span><span class="sxs-lookup"><span data-stu-id="730b5-175">Open up the **PlayerController** script attached to the Player object for editing and update it to the following:</span></span>  
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour {
   
            public float speed;
   
            private Rigidbody rb;
   
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
   
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
   
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
   
                rb.AddForce (movement * speed);
            }
   
            void OnTriggerEnter(Collider other) 
            {
                if (other.gameObject.CompareTag ("Pick Up"))
                {
                    other.gameObject.SetActive (false);
                }
            }
        }
2. <span data-ttu-id="730b5-176">Utwórz nową **Tag** o nazwie **wybierz się** (musi być zgodna nowości w skrypcie)</span><span class="sxs-lookup"><span data-stu-id="730b5-176">Create a new **Tag** called **Pick Up** (it must match what is in the script)</span></span>  
   
    ![][33]
   
    ![][34]
3. <span data-ttu-id="730b5-177">Zastosuj tę **Tag** do pobrania Prefab obiektu.</span><span class="sxs-lookup"><span data-stu-id="730b5-177">Apply this **Tag** to the Prefab Pickup object.</span></span> 
   
    ![][35]
4. <span data-ttu-id="730b5-178">Włącz **IsTrigger** wyboru dla obiekt Prefab.</span><span class="sxs-lookup"><span data-stu-id="730b5-178">Enable **IsTrigger** checkbox for the Prefab object.</span></span>
   
    ![][36]
5. <span data-ttu-id="730b5-179">Dodaj treść sztywne do pobrania Prefab obiektu.</span><span class="sxs-lookup"><span data-stu-id="730b5-179">Add a Rigid body to Pickup Prefab object.</span></span> <span data-ttu-id="730b5-180">Aby zoptymalizować wydajność modyfikacjom collider statycznych, które zostały użyte do dynamicznego collider.</span><span class="sxs-lookup"><span data-stu-id="730b5-180">For performance optimization we will update the static collider that we used to a Dynamic collider.</span></span> 
   
    ![][37]
6. <span data-ttu-id="730b5-181">Na koniec sprawdź **IsKinematic** właściwość prefab obiektu.</span><span class="sxs-lookup"><span data-stu-id="730b5-181">Finally check the **IsKinematic** property for the prefab object.</span></span> 
   
    ![][38]
7. <span data-ttu-id="730b5-182">Trafienia **odtwarzanie** w jednolitości edytora i będzie można odtworzyć ten **Przywróć piłka** gier za pomocą przenoszenia obiektu Player przy użyciu kluczy klawiatury dla kierunku danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="730b5-182">Hit **Play** in the Unity editor and you will be able to play this **Roll a Ball** game by moving the Player object using your keyboard keys for direction input.</span></span> 

### <a name="updating-the-game-for-mobile-play"></a><span data-ttu-id="730b5-183">Aktualizowanie gry dla przenośnych play</span><span class="sxs-lookup"><span data-stu-id="730b5-183">Updating the game for mobile play</span></span>
<span data-ttu-id="730b5-184">Powyżej zawartych podstawowy samouczek z Unity.</span><span class="sxs-lookup"><span data-stu-id="730b5-184">The sections above concluded the basic tutorial from Unity.</span></span> <span data-ttu-id="730b5-185">Firma Microsoft będzie teraz zmodyfikować grę, aby była urządzenia przenośnego przyjazną.</span><span class="sxs-lookup"><span data-stu-id="730b5-185">Now we will modify the game to make it mobile device friendly.</span></span> <span data-ttu-id="730b5-186">Należy zwrócić uwagę na to, My używamy danych wprowadzonych z klawiatury w grze wykonanej do tej pory do testowania.</span><span class="sxs-lookup"><span data-stu-id="730b5-186">Note that we used keyboard input for the game so far for testing.</span></span> <span data-ttu-id="730b5-187">Obecnie firma Microsoft będzie zmodyfikuj go, aby odtwarzacz można sterować przy użyciu ruchu telefonu, tj.</span><span class="sxs-lookup"><span data-stu-id="730b5-187">Now we will modify it so that we can control the player by using the motion of the phone i.e.</span></span> <span data-ttu-id="730b5-188">przy użyciu przyspieszeniomierza jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="730b5-188">using Accelerometer as the input.</span></span> 

<span data-ttu-id="730b5-189">Otwórz **PlayerController** skryptów do edycji i aktualizacji **FixedUpdate** metodę ruchu z przyspieszeniomierza przeniesienie obiektu Player.</span><span class="sxs-lookup"><span data-stu-id="730b5-189">Open up the **PlayerController** script for editing and update the **FixedUpdate** method to use the motion from the accelerometer to move the Player object.</span></span> 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

<span data-ttu-id="730b5-190">Ten samouczek zawiera podstawowe tworzenia gier z Unity i wdrażać ją na urządzeniu wybranym grę.</span><span class="sxs-lookup"><span data-stu-id="730b5-190">This tutorial concludes a basic game creation with Unity and you can deploy this on a device of your choice to play the game.</span></span> 

<!-- Images -->
[1]: ./media/mobile-engagement-unity-roll-a-ball/1.png    
[2]: ./media/mobile-engagement-unity-roll-a-ball/2.png
[3]: ./media/mobile-engagement-unity-roll-a-ball/3.png
[4]: ./media/mobile-engagement-unity-roll-a-ball/4.png
[5]: ./media/mobile-engagement-unity-roll-a-ball/5.png
[6]: ./media/mobile-engagement-unity-roll-a-ball/6.png
[7]: ./media/mobile-engagement-unity-roll-a-ball/7.png
[8]: ./media/mobile-engagement-unity-roll-a-ball/8.png
[9]: ./media/mobile-engagement-unity-roll-a-ball/9.png    
[10]: ./media/mobile-engagement-unity-roll-a-ball/10.png    
[11]: ./media/mobile-engagement-unity-roll-a-ball/11.png    
[12]: ./media/mobile-engagement-unity-roll-a-ball/12.png
[13]: ./media/mobile-engagement-unity-roll-a-ball/13.png
[14]: ./media/mobile-engagement-unity-roll-a-ball/14.png
[15]: ./media/mobile-engagement-unity-roll-a-ball/15.png
[16]: ./media/mobile-engagement-unity-roll-a-ball/16.png
[17]: ./media/mobile-engagement-unity-roll-a-ball/17.png
[18]: ./media/mobile-engagement-unity-roll-a-ball/18.png
[19]: ./media/mobile-engagement-unity-roll-a-ball/19.png    
[20]: ./media/mobile-engagement-unity-roll-a-ball/20.png    
[21]: ./media/mobile-engagement-unity-roll-a-ball/21.png    
[22]: ./media/mobile-engagement-unity-roll-a-ball/22.png    
[23]: ./media/mobile-engagement-unity-roll-a-ball/23.png    
[24]: ./media/mobile-engagement-unity-roll-a-ball/24.png    
[25]: ./media/mobile-engagement-unity-roll-a-ball/25.png    
[26]: ./media/mobile-engagement-unity-roll-a-ball/26.png    
[27]: ./media/mobile-engagement-unity-roll-a-ball/27.png    
[28]: ./media/mobile-engagement-unity-roll-a-ball/28.png    
[29]: ./media/mobile-engagement-unity-roll-a-ball/29.png    
[30]: ./media/mobile-engagement-unity-roll-a-ball/30.png    
[31]: ./media/mobile-engagement-unity-roll-a-ball/31.png    
[32]: ./media/mobile-engagement-unity-roll-a-ball/32.png    
[33]: ./media/mobile-engagement-unity-roll-a-ball/33.png    
[34]: ./media/mobile-engagement-unity-roll-a-ball/34.png    
[35]: ./media/mobile-engagement-unity-roll-a-ball/35.png    
[36]: ./media/mobile-engagement-unity-roll-a-ball/36.png    
[37]: ./media/mobile-engagement-unity-roll-a-ball/37.png    
[38]: ./media/mobile-engagement-unity-roll-a-ball/38.png    
[51]: ./media/mobile-engagement-unity-roll-a-ball/new-project.png
[52]: ./media/mobile-engagement-unity-roll-a-ball/new-project-properties.png
[53]: ./media/mobile-engagement-unity-roll-a-ball/save-scene.png













