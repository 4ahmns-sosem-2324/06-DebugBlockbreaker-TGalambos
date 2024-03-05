# 06-DebugBlockbreaker-TGalambos

```mermaid
classDiagram
    MonoBehaviour <|-- Ball
    MonoBehaviour <|-- Block
    MonoBehaviour <|-- GameSession
    MonoBehaviour <|-- Level
    MonoBehaviour <|-- LoseCollider
    MonoBehaviour <|-- Paddle
    MonoBehaviour <|-- SceneManager

    class Ball
    {
        + Paddle paddle1
        + float xPush = 2f
        + float yPush = 15f
        + AudioClip[] ballSounds
        + float randomFactor = 0.2f
   
        - Vector2 paddleToBallVector
        - bool hasStarted = false

        - AudioSource myAudioSource
        - Rigidbody2D myRigidBody2D

        - void Start ()
        - void Update ()
        - void LaunchOnMouseClick()
        - void LockBallToPaddle()
        - void OnCollisionEnter2D(Collision2D collision)
    }
    
    class Block
    {
        - const string BREAKABLE = "Breakable"
        - const string UNBREAKABLE = "UnBreakable"
    
        + AudioClip breakSound
        + GameObject blockSparklesVFX
        + Sprite[] hitSprites
    
        - Level level
        - GameSession gameStatus
        - [SerializeField] int timesHit
    
        - void Start()
        - void CountBreakableBlocks()
        - void OnCollisionEnter2D(Collision2D collision)
        - void HandleHit()
        - void ShowNextHitSprite()
        - void DestroyBlock()
        - void PlayBlockDestroySFX()
        - void TriggerSparkleVFX()
    }
    
    class GameSession
    {
        [Range(0.1f, 10f)] + float gameSpeed = 1f
        + int pointsPerBlockDestroyed = 83
        + TextMeshProUGUI scoreText
        + bool isAutoPlayEnabled
    
        + int currentScore = 0
        - void Awake()
        - void Start()
        - void Update () 
        + void AddToScore()
        + void ResetGame()
        + bool IsAutoPlayEnabled()
    }
    class Level
    {
        - [SerializeField] int breakableBlocks
    
        - SceneLoader sceneLoader
    
        - void Start()
        - void CountBlocks()
        - void BlockDestroyed()
        - void LoadEndScreen()
    }
    
    class LoseCollider
    {
        + GameObject loader
        - SceneLoader sceneLoader
    
        - void Start ()
       - void OnTriggerEnter2D (Collider2D collision)
    }
    
    class Paddle 
    {
        + float minX = 1f
        + float maxX = 15f
        + float screenWidthInUnits = 16f
    
        - GameSession theGameSession
        - Ball theBall
    
    	- void Start ()
    	- void Update ()
      - float GetXPosition()
        
    }
    class SceneLoader
    {
        - const string GAMEOVERSCREEN = "GameOver"
        - const string CONGRATSSCREEN = "Congrats"
        - const string LEVEL5 = "Level5"
    
        + void LoadNextScene()
        + void LoadWelcome()
        + void LoadGameOver()
        + void LoadCongrats()
        + bool IsLastPlayScene()
    }


```
