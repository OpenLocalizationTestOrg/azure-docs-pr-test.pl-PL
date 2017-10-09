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
# <a id="unity-roll-a-ball"></a>Utwórz Przywróć Unity grę piłka
Ten samouczek przedstawia hello główne kroki dla nieco zmodyfikowany [Unity Przywróć samouczek piłka](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial). Gry próbki składa się z obiektu kulistego player, który jest kontrolowany przez użytkownika aplikacji hello i celem hello gry hello jest too'collect "kolekcjonowanych obiekty według kolizji obiektu player hello z tymi obiektami kolekcjonowanych. Przy założeniu, podstawowa znajomość środowiska Edytor platformy Unity. Jeśli wystąpiły problemy należy zapoznać się toohello pełne samouczka. 

### <a name="setting-up-hello-game"></a>Konfigurowanie hello gry
Poniższe kroki Hello pochodzą z hello [samouczek Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)

1. Otwórz **Edytor platformy Unity** i kliknij przycisk **nowy**. 
   
    ![][51] 
2. Podaj **Nazwa projektu** & **lokalizacji**, wybierz pozycję **3D** i kliknij przycisk **Tworzenie projektu**.
   
    ![][52]
3. Zapisz sceny domyślne hello właśnie utworzony jako część nowego projektu hello zgodnie z nazwą hello **MiniGame** w ramach nowej  **\_sceny** folder **zasoby** folderu:
   
    ![][53]
4. Utwórz **obiektu 3D -> płaszczyzny** jako hello odtwarzanie i zmienić nazwę tego obiektu płaszczyzny jako **podstaw**
   
    ![][1]
5. Resetowanie hello przekształcenia składników dla tego **podstaw** obiekt tak, aby na powitania pochodzenia. 
   
    ![][3]
6. Usuń zaznaczenie pola wyboru **Pokaż siatkę** z **Gizmos menu** dla hello **podstaw** obiektu.
   
    ![][4]
7. Aktualizacja hello **skali** składnik hello **podstaw** obiekt toobe [X = 2, T = 1, Z = 2]. 
   
    ![][5]
8. Dodaj nową **obiektu 3D -> kuli** toohello projektu i Zmień nazwę tego kuli obiekt jako **Player**. 
   
    ![][6]
9. Wybierz hello **Player** obiekt i kliknij przycisk **zresetować przekształcenie** podobne toohello płaszczyzny obiektu. 
10. Aktualizacja **Transform -> pozycji -> współrzędną Y** składnik hello Player Y jako 0,5.  
    
    ![][7]
11. Utwórz nowy folder o nazwie **materiałów** w projekcie hello gdzie utworzymy hello materiału toocolor hello player. 
12. Utwórz nową **materiału** o nazwie **tła** w tym folderze. 
    
    ![][8]
13. Zaktualizuj kolor hello materiału hello aktualizując hello **Albedo** jego właściwości. Można wybrać wartości RGB hello [0,32,64]. 
    
    ![][9]
14. Przeciągnij w tym materiale hello sceny widoku tooapply kolor toohello **podstaw** obiektu. 
    
    ![][10]
15. Na koniec zaktualizuj hello **Transform -> Obrót -> Y** too60 hello światło kierunkowe obiektu dla uzyskania przejrzystości. 
    
    ![][12]

### <a name="moving-hello-player"></a>Przenoszenie hello player
Poniższe kroki Hello pochodzą z hello [samouczek Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)

1. Dodaj **RigidBody** toohello składnika **Player** obiektu. 
   
    ![][13]
2. Utwórz nowy folder o nazwie **skryptów** w hello projektu. 
3. Kliknij przycisk **Dodaj składnik -> Nowy skrypt -> C# skrypt**. Nadaj mu nazwę **PlayerController**i kliknij przycisk **Utwórz i Dodaj**. Spowoduje to utworzenie i dołączyć obiektu Player toohello skryptu.  
   
    ![][14]
4. Przenieś ten skrypt, w obszarze hello **skryptów** folderu w projekcie hello. 
5. Otwórz hello skryptu do edycji w Edytorze skryptów Ulubione, zaktualizuj kod skryptu hello z hello następującego kodu i zapisz go. 
   
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
6. Należy zwrócić uwagę tego skryptu hello powyżej używa **szybkości** właściwości. W edytorze Unity hello zaktualizuj hello szybkości właściwości too10.  
   
    ![][15]
7. Trafienia **odtwarzanie** w hello Edytor platformy Unity. Teraz powinny być piłka hello stanie toocontrol za pomocą klawiatury hello i powinna obracania i przenoszenia. 

### <a name="moving-hello-camera"></a>Przenoszenie hello aparat fotograficzny
Poniższe kroki Hello pochodzą z hello [samouczek platformy Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) i będzie powiązać hello **głównego aparatu** toohello **Player** obiektu. 

1. Aktualizacja hello **Transform.Position** toobe X = 0, Y = 10.5, Z =-10.  
2. Aktualizacja hello **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.  
   
    ![][16]
3. Dodaj nowy skrypt o nazwie **CameraController** toohello **MainCamera** i umieści ją w folderze skryptów hello. 
   
    ![][17]
4. Otwarcie hello skryptu do edycji, a następnie dodaj powitania po w niej kodu:
   
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
5. W środowisku Unity — przeciągnij hello Player zmiennej w gnieździe Player hello obiektu głównego aparatu hello tak, aby hello dwóch skojarzonych ze sobą. 
   
    ![][18]
6. Jeśli Edytor platformy Unity hello i Obróć hello obiektu Player piłka naciśnij pozycję Odtwórz następnie zostanie wyświetlone hello aparatu w hello przepływu.  

### <a name="setting-up-hello-play-area"></a>Konfigurowanie hello obszar odtwarzania
Poniższe kroki Hello pochodzą z hello [samouczek Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141). Utworzymy ściany hello otaczającego hello podstaw, dzięki czemu hello obiektu Player piłka nie pozostawienia obszar odtwarzania hello w ruchu. 

1. Kliknij przycisk **Utwórz -> Utwórz pusty -> obiekt gry** i nadaj mu nazwę **ściany**
   
    ![][19]
2. W tym obiektu ściany — Utwórz nową **obiektu 3D -> modułu** i nadaj jej nazwę na "Zachodnie tablicy". 
   
    ![][20]
3. Hello aktualizacji **Transform -> pozycji** i **Transform -> skali** dla tego obiektu zachodnie tablicy. 
   
    ![][21]
4. Zduplikowana hello zachodnie wall toocreate **wall wschód** z hello zaktualizowane przekształcenie położenie i Skala. 
   
    ![][22]
5. Zduplikowana hello wschód wall toocreate **wall Północna** z hello zaktualizowane przekształcenie pozycji & skali. 
   
    ![][23]
6. Zduplikowana wall Północna hello i Utwórz **wall Południowa** z hello zaktualizowane przekształcenie pozycji & skali. 
   
    ![][24]

### <a name="creating-collectible-objects"></a>Tworzenie obiektów kolekcjonowanych
Poniższe kroki Hello pochodzą z hello [samouczek Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141). Utworzymy niektóre atrakcyjne wyszukiwania obiektów, stanowiące hello zestaw obiektów kolekcjonowanych obiektu Player piłka hello musi too'collect "przez kolizji z nich. 

1. Utwórz nową **3D obiektu modułu** i nadaj mu nazwę pobrania. 
2. Dostosuj hello **Transform -> Obrót** & **Transform -> skali** hello podnoszenia obiektu. 
   
    ![][25]
3. Utwórz i Dołącz **nowego skryptu C#** o nazwie **Rotator** toohello obiektu poczty. Upewnij się, że skrypt hello tooput w folderze skryptów hello. 
   
    ![][26]
4. Otwórz ten skrypt do edycji i zaktualizować go hello toobe następujące: 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. Teraz trybu odtwarzania trafień hello hello Edytor platformy Unity i pokazu podnoszenia obiektu można obracanie na osi.
6. Utwórz nowy folder o nazwie **Prefabs** 
   
    ![][27]
7. Przeciągnij hello **podnoszenia** obiektu i umieszcza je w folderze Prefabs hello.
   
    ![][28]
8. Utwórz nową **gry pusty obiekt** o nazwie **Pickups**. Resetuj jego tooorigin pozycji, a następnie przeciągnij hello podnoszenia obiektu pod ten obiekt gier.  
   
    ![][29]
9. Zduplikowane hello **podnoszenia** obiekt i utworzyć na powitania **podstaw** obiekt wokół hello **Player** obiektu aktualizując hello **X Transform.Position w & Z**  odpowiednio wartości. 
   
    ![][30]
10. Utwórz **nowe materiały** o nazwie **podnoszenia** i zaktualizować go toobe czerwony w kolorze, aktualizując hello **Albedo właściwości** podobne toowhat firma Microsoft hello podstaw aktualizacji obiektu. 
    
    ![][31]
11. Zastosuj hello materiału tooall hello 4 podnoszenia obiektów.
    
    ![][32]

### <a name="collecting-hello-pickup-objects"></a>Zbieranie obiektów podnoszenia hello
Poniższe kroki Hello pochodzą z hello [samouczek Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141). Witaj Player będą aktualizowane tak, aby mogli too'collect "hello podnoszenia obiektów przez kolizji z nich. 

1. Otwórz hello **PlayerController** skryptów obiektu Player toohello dołączone do edycji i zaktualizować je toohello następujące:  
   
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
2. Utwórz nową **Tag** o nazwie **wybierz się** (musi być zgodna nowości w skrypcie hello)  
   
    ![][33]
   
    ![][34]
3. Zastosuj tę **Tag** toohello Prefab pobrania obiektu. 
   
    ![][35]
4. Włącz **IsTrigger** wyboru dla obiekt Prefab hello.
   
    ![][36]
5. Dodaj obiekt Prefab tooPickup sztywne treści. Do optymalizacji wydajności będą aktualizowane hello collider statyczne czy użyliśmy tooa collider dynamicznych. 
   
    ![][37]
6. Na koniec sprawdź hello **IsKinematic** dla obiektu prefab hello. 
   
    ![][38]
7. Trafienia **odtwarzanie** w hello Edytor platformy Unity i będą mogli tooplay to **Przywróć piłka** grę, przenosząc hello obiektu Player przy użyciu kluczy klawiatury dla kierunku danych wejściowych. 

### <a name="updating-hello-game-for-mobile-play"></a>Aktualizowanie hello gier dla przenośnych play
sekcje Hello powyżej hello zawartego podstawowy samouczek z Unity. Teraz możemy zmodyfikuje hello gier toomake go przyjazną urządzenia przenośnego. Pamiętaj, że firma Microsoft stosowane wprowadzanie z klawiatury dla hello gier do tej pory do testowania. Obecnie firma Microsoft będzie zmodyfikuj go, aby firma Microsoft może kontrolować player hello przy użyciu ruchu hello hello telefonu, np. przy użyciu przyspieszeniomierza jako dane wejściowe hello. 

Otwórz hello **PlayerController** skryptu do edycji i aktualizacji hello **FixedUpdate** metody toouse hello ruchu z hello przyspieszeniomierza toomove hello Player obiektu. 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

Ten samouczek zawiera podstawowe tworzenia gier z Unity i wdrażać ją na urządzeniu gry hello tooplay wybór. 

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













