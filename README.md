# Zombie-shooter
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    public float speed = 5f;
    public float rotationSpeed = 5f;
    public GameObject bulletPrefab;
    public Transform firePoint;

    void Update()
    {
        float moveX = Input.GetAxis("Horizontal") * speed * Time.deltaTime;
        float moveZ = Input.GetAxis("Vertical") * speed * Time.deltaTime;
        transform.Translate(moveX, 0, moveZ);

        if (Input.GetMouseButtonDown(0)) // Left click to shoot
        {
            Shoot();
        }
    }

    void Shoot()
    {
        Instantiate(bulletPrefab, firePoint.position, firePoint.rotation);
    }
}
using UnityEngine;
using UnityEngine.AI;

public class Zombie : MonoBehaviour
{
    public int health = 100;
    public float speed = 2f;
    public Transform target;
    private NavMeshAgent agent;

    void Start()
    {
        agent = GetComponent<NavMeshAgent>();
        target = GameObject.FindGameObjectWithTag("Player").transform;
        agent.speed = speed;
    }

    void Update()
    {
        if (target != null)
            agent.SetDestination(target.position);
    }

    public void TakeDamage(int damage)
    {
        health -= damage;
        if (health <= 0)
            Destroy(gameObject);
    }
}
