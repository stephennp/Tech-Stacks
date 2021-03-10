# Intro

- A new adventure for game programming

# Escape Dungeon

- Create background and scrolling - Create 3D-> Quad - Create Material -> Naming `Background` -> Mode to Quad - Edit Quad -> Choose `Background` -> Convert `Standard` -> `Unlit/Texture`
- Add a script

  ```csharp
  public class BackgroundScroll : MonoBehaviour
  {
  public float ScrollSpeed { get; set; } = 0.298f;

      private MeshRenderer meshRenderer;

      void Awake()
      {
          meshRenderer = GetComponent<MeshRenderer>();
      }

      // Update is called once per frame
      void Update()
      {
          ScrollHandler();
      }

      void ScrollHandler()
      {

          Vector2 offset = meshRenderer.sharedMaterial.GetTextureOffset("_MainTex");
          offset.y += Time.deltaTime * ScrollSpeed;

          meshRenderer.sharedMaterial.SetTextureOffset("_MainTex", offset);
      }

  }
  ```

- Edit Bg -> Wrap Mode ->`Repeat`

## Add Platform

- Using for effect of falling down when scroll up
- Create an image like platform
- Update `Order in layer`
- Add `Box Collider 2D` ->
- Add ``Rigid body 2d` -> Update BodyType `Kinematic` ( that no affected by gravity(dynamic), instead of velocity)

## Add animation

- Duplicate above `Platfom`
- Create `Animation` folder -> Choose `Animation controller` -> move to `Break Platform`
- Go `Animation` tab -> create -> naming `Idle` -> create `A new clip` -> naming `Break`
- Drag animation imgs to `Break`
- View `Animator` -> Set default `Break` -> Update `Speed` -> Double Click -> Uncheck `loop time`

## Add blade

- set `layer order` = 1
- add `Box Collider` -> Is Trigger : checked
- add `rigid body` -> body type `Kitenamic`

## Set speed left arrow

- drag and drop to `scene`
- create new animation -> move to `animation` folder
- add `rigid body` -> body type `Kitenamic`

## Set speed left arrow

- Duplicate `left arrow`
- Sprite Renderer -> Flip check `X`

## Add platform script

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Platform : MonoBehaviour
{
    public float moveSpeed = 1.98f;
    public float boudY = 5.55f;
    public bool movingPlatFormLeft,
                movingPlatFormRight,
                isBreakable,
                isBlade,
                isPlatform;

    private Animator anim;
    private void Awake()
    {
       if(isBreakable)
        {
            anim = GetComponent<Animator>();
        }
    }

    // Update is called once per frame
    void Update()
    {
        Move();
    }

   void Move()
    {
        Vector2 temp = transform.position;
        temp.y += moveSpeed * Time.deltaTime;
        transform.position = temp;
    }
}

```
- Move the script to every platform
- Check every platform with flat respectively. Such as breakPlatform with `isBreakable`
## Add preface
- Move all platforms to this folder

## Spawner platform
- Create a spanwer platform by `create empty object`
- Add spawner platform script
```csharp
 void Spawn()
    {
        currentPlatformSpawnerTime += Time.deltaTime;

        if (currentPlatformSpawnerTime >= platformSpawnerTime)
        {
            platformSpawnCount++;
            Vector3 temp = transform.position;
            temp.y = Random.Range(minX, maxX);

            GameObject newPlatform = null;
            if (platformSpawnCount < 2)
            {
                newPlatform = Instantiate(platformPrefab, temp, Quaternion.identity);

            }
            else if (platformSpawnCount == 2)
            {
                if (Random.Range(0, 2) > 0)
                {
                    newPlatform = Instantiate(platformPrefab, temp, Quaternion.identity);
                }
                else
                {
                    newPlatform = Instantiate(movingPlatForms[Random.Range(0, movingPlatForms.Length)],
                                             temp,
                                             Quaternion.identity);
                }
            }
            else if(platformSpawnCount == 3)
            {
                if (Random.Range(0, 2) > 0)
                {
                    newPlatform = Instantiate(platformPrefab, temp, Quaternion.identity);
                }
                else
                {
                    newPlatform = Instantiate(blazePrefab, temp, Quaternion.identity);
                }
            }
            else if (platformSpawnCount == 4)
            {
                if (Random.Range(0, 2) > 0)
                {
                    newPlatform = Instantiate(platformPrefab, temp, Quaternion.identity);
                }
                else
                {
                    newPlatform = Instantiate(breakPlatform, temp, Quaternion.identity);
                }

                platformSpawnCount = 0;
            }
        }
    }
```
- drag and drop blaze,break and platform to script 

## Add bound platform script to Creature

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class CreatureBound : MonoBehaviour
{
    public float minX = -2.6f, maxX = 2.6f, minY = -5.6f;
    private bool outOfBound;
    // Update is called once per frame
    void Update()
    {
        boundHandler();
    }

    void boundHandler()
    {
        Vector2 temp = transform.position;
        if(temp.x > maxX)
        {
            temp.x = maxX;
        }

        if (temp.x < minX)
        {
            temp.x = minX;
        }

        transform.position = temp;

        if(temp.y <= minY)
        {
            if (!outOfBound)
            {
                outOfBound = true;
                

                // SoundManager.instance.DeathSound();
                // GameManager.instance.RestartGame();
            }
        }
    }
}

```

## Create top spike tag
- Create `empty object` -> Add a tag -> Add `Box Coliider 2D  `
- Add functions to platform
```csharp
    void BreakDeactive()
    {
        Invoke("DeactiveGameObject", 0.29f);
    }

    void DeactiveGameObject()
    {
        gameObject.SetActive(false);
    }
```
- Move to `Breakable platform` -> final animation -> add an event -> select `BreakDeactive()`

- Create a tag for `creature` spike


## Create game manager 
- File -> Build settings -> `Add open scenes`
- create `Empty object`

## Create score
-> Create `UI` -> `Text` -> Rename `Score`

# Up EscapeDungeon to google play
- Update `Player setting`
    - Package name `io.Stephen.EscapeDungeon`
    - compnay Name `stephen`
    - version `0.1`
    - buldle version `2`
    - Other settings:
        - Backend scrippting : switch `Momo` -> `IL2CPP` -> checked `ARM64`
        - Update `Android SDK API 29`
    - Publish settings:
        - add key store 
            - password: 8158**
            - alias: steve
            - organization: Stephen