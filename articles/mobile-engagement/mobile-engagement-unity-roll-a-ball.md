---
title: "Samouczek piłka Przywróć aaaUnity"
description: "Kroki toocreate hello klasycznego Przywróć Unity gra w piłkę, czyli jako warunek wstępny dla wszystkich samouczków Unity usługi Mobile Engagement"
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
ms.openlocfilehash: 10d923682432961207594886b08e5db60cf60d9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="1ac0e-103"><a id="unity-roll-a-ball"></a>Utwórz Przywróć Unity grę piłka</span><span class="sxs-lookup"><span data-stu-id="1ac0e-103"><a id="unity-roll-a-ball"></a>Create Unity Roll a Ball game</span></span>
<span data-ttu-id="1ac0e-104">Ten samouczek przedstawia hello główne kroki dla nieco zmodyfikowany [Unity Przywróć samouczek piłka](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span><span class="sxs-lookup"><span data-stu-id="1ac0e-104">This tutorial walks through hello main steps for a slightly modified [Unity Roll a Ball tutorial](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span></span> <span data-ttu-id="1ac0e-105">Gry próbki składa się z obiektu kulistego player, który jest kontrolowany przez użytkownika aplikacji hello i celem hello gry hello jest too'collect "kolekcjonowanych obiekty według kolizji obiektu player hello z tymi obiektami kolekcjonowanych.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-105">This sample game consists of a spherical 'player' object which is controlled by hello app user and hello objective of hello game is too'collect' collectible objects by colliding hello player object with these collectible objects.</span></span> <span data-ttu-id="1ac0e-106">Przy założeniu, podstawowa znajomość środowiska Edytor platformy Unity.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-106">This assumes basic familiarity with Unity editor environment.</span></span> <span data-ttu-id="1ac0e-107">Jeśli wystąpiły problemy należy zapoznać się toohello pełne samouczka.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-107">If you run into any issues then you should refer toohello full tutorial.</span></span> 

### <a name="setting-up-hello-game"></a><span data-ttu-id="1ac0e-108">Konfigurowanie hello gry</span><span class="sxs-lookup"><span data-stu-id="1ac0e-108">Setting up hello game</span></span>
<span data-ttu-id="1ac0e-109">Poniższe kroki Hello pochodzą z hello [samouczek Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="1ac0e-109">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span></span>

1. <span data-ttu-id="1ac0e-110">Otwórz **Edytor platformy Unity** i kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-110">Open **Unity Editor** and click **New**.</span></span> 
   
    ![][51] 
2. <span data-ttu-id="1ac0e-111">Podaj **Nazwa projektu** & **lokalizacji**, wybierz pozycję **3D** i kliknij przycisk **Tworzenie projektu**.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-111">Provide a **Project name** & **Location**, select **3D** and click **Create project**.</span></span>
   
    ![][52]
3. <span data-ttu-id="1ac0e-112">Zapisz sceny domyślne hello właśnie utworzony jako część nowego projektu hello zgodnie z nazwą hello **MiniGame** w ramach nowej  **\_sceny** folder **zasoby** folderu:</span><span class="sxs-lookup"><span data-stu-id="1ac0e-112">Save hello default scene just created as part of hello new project as with hello name **MiniGame** within a new **\_Scenes** folder under **Assets** folder:</span></span>
   
    ![][53]
4. <span data-ttu-id="1ac0e-113">Utwórz **obiektu 3D -> płaszczyzny** jako hello odtwarzanie i zmienić nazwę tego obiektu płaszczyzny jako **podstaw**</span><span class="sxs-lookup"><span data-stu-id="1ac0e-113">Create a **3D Object -> Plane** as hello playing field and rename this plane object as **Ground**</span></span>
   
    ![][1]
5. <span data-ttu-id="1ac0e-114">Resetowanie hello przekształcenia składników dla tego **podstaw** obiekt tak, aby na powitania pochodzenia.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-114">Reset hello transform component for this **Ground** object so that it is at hello Origin.</span></span> 
   
    ![][3]
6. <span data-ttu-id="1ac0e-115">Usuń zaznaczenie pola wyboru **Pokaż siatkę** z **Gizmos menu** dla hello **podstaw** obiektu.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-115">Uncheck **Show Grid** from **Gizmos menu** for hello **Ground** object.</span></span>
   
    ![][4]
7. <span data-ttu-id="1ac0e-116">Aktualizacja hello **skali** składnik hello **podstaw** obiekt toobe [X = 2, T = 1, Z = 2].</span><span class="sxs-lookup"><span data-stu-id="1ac0e-116">Update hello **Scale** component for hello **Ground** object toobe [X = 2,Y = 1, Z = 2].</span></span> 
   
    ![][5]
8. <span data-ttu-id="1ac0e-117">Dodaj nową **obiektu 3D -> kuli** toohello projektu i Zmień nazwę tego kuli obiekt jako **Player**.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-117">Add a new **3D Object -> Sphere** toohello project and rename this sphere object as **Player**.</span></span> 
   
    ![][6]
9. <span data-ttu-id="1ac0e-118">Wybierz hello **Player** obiekt i kliknij przycisk **zresetować przekształcenie** podobne toohello płaszczyzny obiektu.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-118">Select hello **Player** object and click **Reset Transform** similar toohello Plane object.</span></span> 
10. <span data-ttu-id="1ac0e-119">Aktualizacja **Transform -> pozycji -> współrzędną Y** składnik hello Player Y jako 0,5.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-119">Update **Transform -> Position -> Y Coordinate** component for hello Player Y as 0.5.</span></span>  
    
    ![][7]
11. <span data-ttu-id="1ac0e-120">Utwórz nowy folder o nazwie **materiałów** w projekcie hello gdzie utworzymy hello materiału toocolor hello player.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-120">Create a new folder called **Materials** in hello project where we will create hello material toocolor hello player.</span></span> 
12. <span data-ttu-id="1ac0e-121">Utwórz nową **materiału** o nazwie **tła** w tym folderze.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-121">Create a new **Material** called **Background** in this folder.</span></span> 
    
    ![][8]
13. <span data-ttu-id="1ac0e-122">Zaktualizuj kolor hello materiału hello aktualizując hello **Albedo** jego właściwości.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-122">Update hello color of hello material by updating hello **Albedo** property of it.</span></span> <span data-ttu-id="1ac0e-123">Można wybrać wartości RGB hello [0,32,64].</span><span class="sxs-lookup"><span data-stu-id="1ac0e-123">You can select hello RGB values of [0,32,64].</span></span> 
    
    ![][9]
14. <span data-ttu-id="1ac0e-124">Przeciągnij w tym materiale hello sceny widoku tooapply kolor toohello **podstaw** obiektu.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-124">Drag this material into hello scene view tooapply color toohello **Ground** object.</span></span> 
    
    ![][10]
15. <span data-ttu-id="1ac0e-125">Na koniec zaktualizuj hello **Transform -> Obrót -> Y** too60 hello światło kierunkowe obiektu dla uzyskania przejrzystości.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-125">Finally update hello **Transform -> Rotation -> Y** too60 on hello Directional Light object for clarity.</span></span> 
    
    ![][12]

### <a name="moving-hello-player"></a><span data-ttu-id="1ac0e-126">Przenoszenie hello player</span><span class="sxs-lookup"><span data-stu-id="1ac0e-126">Moving hello player</span></span>
<span data-ttu-id="1ac0e-127">Poniższe kroki Hello pochodzą z hello [samouczek Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="1ac0e-127">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span></span>

1. <span data-ttu-id="1ac0e-128">Dodaj **RigidBody** toohello składnika **Player** obiektu.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-128">Add a **RigidBody** component toohello **Player** object.</span></span> 
   
    ![][13]
2. <span data-ttu-id="1ac0e-129">Utwórz nowy folder o nazwie **skryptów** w hello projektu.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-129">Create a new folder called **Scripts** in hello Project.</span></span> 
3. <span data-ttu-id="1ac0e-130">Kliknij przycisk **Dodaj składnik -> Nowy skrypt -> C# skrypt**.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-130">Click **Add Component-> New Script -> C# Script**.</span></span> <span data-ttu-id="1ac0e-131">Nadaj mu nazwę **PlayerController**i kliknij przycisk **Utwórz i Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-131">Name it **PlayerController**, and click **Create and Add**.</span></span> <span data-ttu-id="1ac0e-132">Spowoduje to utworzenie i dołączyć obiektu Player toohello skryptu.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-132">This will create and attach a script toohello Player object.</span></span>  
   
    ![][14]
4. <span data-ttu-id="1ac0e-133">Przenieś ten skrypt, w obszarze hello **skryptów** folderu w projekcie hello.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-133">Move this script under hello **Scripts** folder in hello project.</span></span> 
5. <span data-ttu-id="1ac0e-134">Otwórz hello skryptu do edycji w Edytorze skryptów Ulubione, zaktualizuj kod skryptu hello z hello następującego kodu i zapisz go.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-134">Open hello script for editing in your favorite script editor, update hello script code with hello following code and save it.</span></span> 
   
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
6. <span data-ttu-id="1ac0e-135">Należy zwrócić uwagę tego skryptu hello powyżej używa **szybkości** właściwości.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-135">Note that hello script above uses a **Speed** property.</span></span> <span data-ttu-id="1ac0e-136">W edytorze Unity hello zaktualizuj hello szybkości właściwości too10.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-136">In hello Unity editor, update hello speed property too10.</span></span>  
   
    ![][15]
7. <span data-ttu-id="1ac0e-137">Trafienia **odtwarzanie** w hello Edytor platformy Unity.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-137">Hit **Play** in hello Unity Editor.</span></span> <span data-ttu-id="1ac0e-138">Teraz powinny być piłka hello stanie toocontrol za pomocą klawiatury hello i powinna obracania i przenoszenia.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-138">Now you should be able toocontrol hello ball using hello keyboard and it should rotate and move around.</span></span> 

### <a name="moving-hello-camera"></a><span data-ttu-id="1ac0e-139">Przenoszenie hello aparat fotograficzny</span><span class="sxs-lookup"><span data-stu-id="1ac0e-139">Moving hello camera</span></span>
<span data-ttu-id="1ac0e-140">Poniższe kroki Hello pochodzą z hello [samouczek platformy Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) i będzie powiązać hello **głównego aparatu** toohello **Player** obiektu.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-140">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) and will tie hello **Main Camera** toohello **Player** object.</span></span> 

1. <span data-ttu-id="1ac0e-141">Aktualizacja hello **Transform.Position** toobe X = 0, Y = 10.5, Z =-10.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-141">Update hello **Transform.Position** toobe X = 0,  Y = 10.5, Z=-10.</span></span>  
2. <span data-ttu-id="1ac0e-142">Aktualizacja hello **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-142">Update hello **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.</span></span>  
   
    ![][16]
3. <span data-ttu-id="1ac0e-143">Dodaj nowy skrypt o nazwie **CameraController** toohello **MainCamera** i umieści ją w folderze skryptów hello.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-143">Add a new script called **CameraController** toohello **MainCamera** and move it under hello Scripts folder.</span></span> 
   
    ![][17]
4. <span data-ttu-id="1ac0e-144">Otwarcie hello skryptu do edycji, a następnie dodaj powitania po w niej kodu:</span><span class="sxs-lookup"><span data-stu-id="1ac0e-144">Open up hello script for editing and add hello following code in it:</span></span>
   
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
5. <span data-ttu-id="1ac0e-145">W środowisku Unity — przeciągnij hello Player zmiennej w gnieździe Player hello obiektu głównego aparatu hello tak, aby hello dwóch skojarzonych ze sobą.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-145">In Unity environment - drag hello Player variable into hello Player slot for hello Main Camera object so that hello two are associated with one another.</span></span> 
   
    ![][18]
6. <span data-ttu-id="1ac0e-146">Jeśli Edytor platformy Unity hello i Obróć hello obiektu Player piłka naciśnij pozycję Odtwórz następnie zostanie wyświetlone hello aparatu w hello przepływu.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-146">Now if you hit Play in hello Unity editor and rotate hello Player Ball object then you will see hello Camera following it in hello movement.</span></span>  

### <a name="setting-up-hello-play-area"></a><span data-ttu-id="1ac0e-147">Konfigurowanie hello obszar odtwarzania</span><span class="sxs-lookup"><span data-stu-id="1ac0e-147">Setting up hello Play area</span></span>
<span data-ttu-id="1ac0e-148">Poniższe kroki Hello pochodzą z hello [samouczek Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="1ac0e-148">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span></span> <span data-ttu-id="1ac0e-149">Utworzymy ściany hello otaczającego hello podstaw, dzięki czemu hello obiektu Player piłka nie pozostawienia obszar odtwarzania hello w ruchu.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-149">We will create hello Walls surrounding hello Ground so that hello Player Ball object doesn't drop off hello play area in its movement.</span></span> 

1. <span data-ttu-id="1ac0e-150">Kliknij przycisk **Utwórz -> Utwórz pusty -> obiekt gry** i nadaj mu nazwę **ściany**</span><span class="sxs-lookup"><span data-stu-id="1ac0e-150">Click **Create -> Create Empty -> Game Object** and name it **Walls**</span></span>
   
    ![][19]
2. <span data-ttu-id="1ac0e-151">W tym obiektu ściany — Utwórz nową **obiektu 3D -> modułu** i nadaj jej nazwę na "Zachodnie tablicy".</span><span class="sxs-lookup"><span data-stu-id="1ac0e-151">Under this Walls object - create a new **3D Object -> Cube** and name it "West wall".</span></span> 
   
    ![][20]
3. <span data-ttu-id="1ac0e-152">Hello aktualizacji **Transform -> pozycji** i **Transform -> skali** dla tego obiektu zachodnie tablicy.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-152">Update hello **Transform -> Position** and **Transform -> Scale** for this West Wall object.</span></span> 
   
    ![][21]
4. <span data-ttu-id="1ac0e-153">Zduplikowana hello zachodnie wall toocreate **wall wschód** z hello zaktualizowane przekształcenie położenie i Skala.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-153">Duplicate hello West wall toocreate an **East wall** with hello updated transform position and scale.</span></span> 
   
    ![][22]
5. <span data-ttu-id="1ac0e-154">Zduplikowana hello wschód wall toocreate **wall Północna** z hello zaktualizowane przekształcenie pozycji & skali.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-154">Duplicate hello East wall toocreate a **North wall** with hello updated transform position & scale.</span></span> 
   
    ![][23]
6. <span data-ttu-id="1ac0e-155">Zduplikowana wall Północna hello i Utwórz **wall Południowa** z hello zaktualizowane przekształcenie pozycji & skali.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-155">Duplicate hello North wall and create a **South wall** with hello updated transform position & scale.</span></span> 
   
    ![][24]

### <a name="creating-collectible-objects"></a><span data-ttu-id="1ac0e-156">Tworzenie obiektów kolekcjonowanych</span><span class="sxs-lookup"><span data-stu-id="1ac0e-156">Creating Collectible objects</span></span>
<span data-ttu-id="1ac0e-157">Poniższe kroki Hello pochodzą z hello [samouczek Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="1ac0e-157">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span></span> <span data-ttu-id="1ac0e-158">Utworzymy niektóre atrakcyjne wyszukiwania obiektów, stanowiące hello zestaw obiektów kolekcjonowanych obiektu Player piłka hello musi too'collect "przez kolizji z nich.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-158">We will create some attractive looking objects which will form hello set of collectible objects which hello Player Ball object needs too'collect' by colliding with them.</span></span> 

1. <span data-ttu-id="1ac0e-159">Utwórz nową **3D obiektu modułu** i nadaj mu nazwę pobrania.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-159">Create a new **3D Cube object** and name it Pickup.</span></span> 
2. <span data-ttu-id="1ac0e-160">Dostosuj hello **Transform -> Obrót** & **Transform -> skali** hello podnoszenia obiektu.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-160">Adjust hello **Transform -> Rotation** & **Transform -> Scale** of hello Pickup object.</span></span> 
   
    ![][25]
3. <span data-ttu-id="1ac0e-161">Utwórz i Dołącz **nowego skryptu C#** o nazwie **Rotator** toohello obiektu poczty.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-161">Create and attach a **new C# Script** called **Rotator** toohello Pickup object.</span></span> <span data-ttu-id="1ac0e-162">Upewnij się, że skrypt hello tooput w folderze skryptów hello.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-162">Make sure tooput hello script under hello Scripts folder.</span></span> 
   
    ![][26]
4. <span data-ttu-id="1ac0e-163">Otwórz ten skrypt do edycji i zaktualizować go hello toobe następujące:</span><span class="sxs-lookup"><span data-stu-id="1ac0e-163">Open this script for editing and update it toobe hello following:</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. <span data-ttu-id="1ac0e-164">Teraz trybu odtwarzania trafień hello hello Edytor platformy Unity i pokazu podnoszenia obiektu można obracanie na osi.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-164">Now hit hello Play mode in hello Unity Editor and your Pickup object show be rotating on its axis.</span></span>
6. <span data-ttu-id="1ac0e-165">Utwórz nowy folder o nazwie **Prefabs**</span><span class="sxs-lookup"><span data-stu-id="1ac0e-165">Create a new folder called **Prefabs**</span></span> 
   
    ![][27]
7. <span data-ttu-id="1ac0e-166">Przeciągnij hello **podnoszenia** obiektu i umieszcza je w folderze Prefabs hello.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-166">Drag hello **Pickup** object and put it in hello Prefabs folder.</span></span>
   
    ![][28]
8. <span data-ttu-id="1ac0e-167">Utwórz nową **gry pusty obiekt** o nazwie **Pickups**.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-167">Create a new **Empty Game object** called **Pickups**.</span></span> <span data-ttu-id="1ac0e-168">Resetuj jego tooorigin pozycji, a następnie przeciągnij hello podnoszenia obiektu pod ten obiekt gier.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-168">Reset its position tooorigin and then drag hello Pickup object under this game object.</span></span>  
   
    ![][29]
9. <span data-ttu-id="1ac0e-169">Zduplikowane hello **podnoszenia** obiekt i utworzyć na powitania **podstaw** obiekt wokół hello **Player** obiektu aktualizując hello **X Transform.Position w & Z**  odpowiednio wartości.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-169">Duplicate hello **Pickup** object and spread it on hello **Ground** object around hello **Player** object by updating hello **Transform.Position's X & Z** values appropriately.</span></span> 
   
    ![][30]
10. <span data-ttu-id="1ac0e-170">Utwórz **nowe materiały** o nazwie **podnoszenia** i zaktualizować go toobe czerwony w kolorze, aktualizując hello **Albedo właściwości** podobne toowhat firma Microsoft hello podstaw aktualizacji obiektu.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-170">Create a **new material** called **Pickup** and update it toobe Red in color by updating hello **Albedo property** similar toowhat we did for updating hello Ground object.</span></span> 
    
    ![][31]
11. <span data-ttu-id="1ac0e-171">Zastosuj hello materiału tooall hello 4 podnoszenia obiektów.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-171">Apply hello material tooall hello 4 pickup objects.</span></span>
    
    ![][32]

### <a name="collecting-hello-pickup-objects"></a><span data-ttu-id="1ac0e-172">Zbieranie obiektów podnoszenia hello</span><span class="sxs-lookup"><span data-stu-id="1ac0e-172">Collecting hello Pickup objects</span></span>
<span data-ttu-id="1ac0e-173">Poniższe kroki Hello pochodzą z hello [samouczek Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="1ac0e-173">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span></span> <span data-ttu-id="1ac0e-174">Witaj Player będą aktualizowane tak, aby mogli too'collect "hello podnoszenia obiektów przez kolizji z nich.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-174">We will update hello Player so that it is able too'collect' hello pickup objects by colliding with them.</span></span> 

1. <span data-ttu-id="1ac0e-175">Otwórz hello **PlayerController** skryptów obiektu Player toohello dołączone do edycji i zaktualizować je toohello następujące:</span><span class="sxs-lookup"><span data-stu-id="1ac0e-175">Open up hello **PlayerController** script attached toohello Player object for editing and update it toohello following:</span></span>  
   
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
2. <span data-ttu-id="1ac0e-176">Utwórz nową **Tag** o nazwie **wybierz się** (musi być zgodna nowości w skrypcie hello)</span><span class="sxs-lookup"><span data-stu-id="1ac0e-176">Create a new **Tag** called **Pick Up** (it must match what is in hello script)</span></span>  
   
    ![][33]
   
    ![][34]
3. <span data-ttu-id="1ac0e-177">Zastosuj tę **Tag** toohello Prefab pobrania obiektu.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-177">Apply this **Tag** toohello Prefab Pickup object.</span></span> 
   
    ![][35]
4. <span data-ttu-id="1ac0e-178">Włącz **IsTrigger** wyboru dla obiekt Prefab hello.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-178">Enable **IsTrigger** checkbox for hello Prefab object.</span></span>
   
    ![][36]
5. <span data-ttu-id="1ac0e-179">Dodaj obiekt Prefab tooPickup sztywne treści.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-179">Add a Rigid body tooPickup Prefab object.</span></span> <span data-ttu-id="1ac0e-180">Do optymalizacji wydajności będą aktualizowane hello collider statyczne czy użyliśmy tooa collider dynamicznych.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-180">For performance optimization we will update hello static collider that we used tooa Dynamic collider.</span></span> 
   
    ![][37]
6. <span data-ttu-id="1ac0e-181">Na koniec sprawdź hello **IsKinematic** dla obiektu prefab hello.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-181">Finally check hello **IsKinematic** property for hello prefab object.</span></span> 
   
    ![][38]
7. <span data-ttu-id="1ac0e-182">Trafienia **odtwarzanie** w hello Edytor platformy Unity i będą mogli tooplay to **Przywróć piłka** grę, przenosząc hello obiektu Player przy użyciu kluczy klawiatury dla kierunku danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-182">Hit **Play** in hello Unity editor and you will be able tooplay this **Roll a Ball** game by moving hello Player object using your keyboard keys for direction input.</span></span> 

### <a name="updating-hello-game-for-mobile-play"></a><span data-ttu-id="1ac0e-183">Aktualizowanie hello gier dla przenośnych play</span><span class="sxs-lookup"><span data-stu-id="1ac0e-183">Updating hello game for mobile play</span></span>
<span data-ttu-id="1ac0e-184">sekcje Hello powyżej hello zawartego podstawowy samouczek z Unity.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-184">hello sections above concluded hello basic tutorial from Unity.</span></span> <span data-ttu-id="1ac0e-185">Teraz możemy zmodyfikuje hello gier toomake go przyjazną urządzenia przenośnego.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-185">Now we will modify hello game toomake it mobile device friendly.</span></span> <span data-ttu-id="1ac0e-186">Pamiętaj, że firma Microsoft stosowane wprowadzanie z klawiatury dla hello gier do tej pory do testowania.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-186">Note that we used keyboard input for hello game so far for testing.</span></span> <span data-ttu-id="1ac0e-187">Obecnie firma Microsoft będzie zmodyfikuj go, aby firma Microsoft może kontrolować player hello przy użyciu ruchu hello hello telefonu, np. przy użyciu przyspieszeniomierza jako dane wejściowe hello.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-187">Now we will modify it so that we can control hello player by using hello motion of hello phone i.e. using Accelerometer as hello input.</span></span> 

<span data-ttu-id="1ac0e-188">Otwórz hello **PlayerController** skryptu do edycji i aktualizacji hello **FixedUpdate** metody toouse hello ruchu z hello przyspieszeniomierza toomove hello Player obiektu.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-188">Open up hello **PlayerController** script for editing and update hello **FixedUpdate** method toouse hello motion from hello accelerometer toomove hello Player object.</span></span> 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

<span data-ttu-id="1ac0e-189">Ten samouczek zawiera podstawowe tworzenia gier z Unity i wdrażać ją na urządzeniu gry hello tooplay wybór.</span><span class="sxs-lookup"><span data-stu-id="1ac0e-189">This tutorial concludes a basic game creation with Unity and you can deploy this on a device of your choice tooplay hello game.</span></span> 

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













