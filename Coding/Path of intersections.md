# Path of intersections
To implement a system where the ship checks for intersections and occasionally makes turns, we need to extend the movement logic. Specifically, we'll:
- Detect possible paths at intersections using raycasts in multiple directions.
- Randomly decide whether the ship should continue moving straight or make a turn when it reaches an intersection.

### Extended Code:

```csharp
using UnityEngine;

public class MazeGhostShip : MonoBehaviour
{
    public float moveSpeed = 2f;
    public float rotationSpeed = 5f;
    public float checkDistance = 1f;
    public float turnProbability = 0.3f;  // Probability of turning at intersections
    public LayerMask obstacleLayer;
    public GameObject cursorPrefab;

    private Vector3 movementDirection;
    private GameObject cursorInstance;
    private Rigidbody rb;   // Rigidbody reference

    void Start()
    {
        rb = GetComponent<Rigidbody>();
        if (rb == null)
        {
            rb = gameObject.AddComponent<Rigidbody>();
        }
        rb.isKinematic = true;   // Make sure the ship is not affected by physics forces

        ChooseRandomDirection();

        if (cursorPrefab != null)
        {
            cursorInstance = Instantiate(cursorPrefab);
            cursorInstance.SetActive(false);
        }
    }

    void Update()
    {
        MoveShip();
        AlignToMovement();
    }

    void MoveShip()
    {
        RaycastHit hit;
        Vector3 raycastStart = transform.position + movementDirection * 0.5f;

        // Check for obstacles in the current direction
        if (!Physics.Raycast(raycastStart, movementDirection, out hit, checkDistance, obstacleLayer))
        {
            // If there's no obstacle, check if there are possible turns at an intersection
            if (IsAtIntersection())
            {
                // Randomly decide whether to turn or continue straight
                if (Random.value < turnProbability)
                {
                    ChooseRandomDirection();
                }
            }

            // Move the ship using Rigidbody's MovePosition for smooth movement
            rb.MovePosition(transform.position + movementDirection * moveSpeed * Time.deltaTime);
        }
        else
        {
            // If an obstacle is detected, choose a new random direction
            ChooseRandomDirection();

            if (cursorInstance != null)
            {
                cursorInstance.transform.position = hit.point;
                cursorInstance.SetActive(true);
            }
        }
    }

    void AlignToMovement()
    {
        if (movementDirection != Vector3.zero)
        {
            Quaternion targetRotation = Quaternion.LookRotation(movementDirection);
            transform.rotation = Quaternion.Slerp(transform.rotation, targetRotation, rotationSpeed * Time.deltaTime);
        }
    }

    void ChooseRandomDirection()
    {
        int random = Random.Range(0, 4);
        switch (random)
        {
            case 0: movementDirection = Vector3.forward; break;
            case 1: movementDirection = Vector3.back; break;
            case 2: movementDirection = Vector3.right; break;
            case 3: movementDirection = Vector3.left; break;
        }
    }

    // Check for possible turns (intersection detection)
    bool IsAtIntersection()
    {
        // Check left and right directions for open paths
        bool canTurnLeft = !Physics.Raycast(transform.position, Vector3.left, checkDistance, obstacleLayer);
        bool canTurnRight = !Physics.Raycast(transform.position, Vector3.right, checkDistance, obstacleLayer);
        bool canTurnForward = !Physics.Raycast(transform.position, Vector3.forward, checkDistance, obstacleLayer);
        bool canTurnBackward = !Physics.Raycast(transform.position, Vector3.back, checkDistance, obstacleLayer);

        // If there's an open path in any direction other than straight, it's an intersection
        return canTurnLeft || canTurnRight || canTurnForward || canTurnBackward;
    }
}
```

### Explanation:
1. **Intersection Detection (`IsAtIntersection`)**:  
   - This method checks for open paths (without obstacles) in the left, right, forward, and backward directions using raycasts.
   - If there are multiple possible directions, it means the ship is at an intersection.

2. **Turning at Intersections**:
   - When the ship reaches an intersection, it has a chance to turn. This probability is controlled by `turnProbability` (e.g., 30% chance to turn).
   - If the ship decides to turn, it chooses a new random direction.

3. **Movement**:
   - The ship moves forward until an obstacle is detected, at which point it picks a new direction.
   - It checks for intersections regularly and occasionally turns based on the random chance.

With this setup, the ship will dynamically move through the maze, detecting intersections and making occasional turns for more varied movement.
