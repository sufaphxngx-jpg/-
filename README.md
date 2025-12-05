# -
Can kill 
using UnityEngine;

public class ScytheWeapon : MonoBehaviour
{
    public float damage = 40f;
    public float range = 2f;
    public LayerMask enemyLayer;

    // ถ้าใช้ SphereCast หรือ OverlapSphere
    public void TryHit()
    {
        // ทำ PlayParticle / Sound ถ้าต้องการ
        Collider[] hits = Physics.OverlapSphere(transform.position + transform.forward * (range/2f), range, enemyLayer);
        foreach (var c in hits)
        {
            EnemyHealth eh = c.GetComponent<EnemyHealth>();
            if (eh != null)
            {
                eh.TakeDamage(damage);
            }
        }
    }

    void OnDrawGizmosSelected()
    {
        Gizmos.color = Color.red;
        Gizmos.DrawWireSphere(transform.position + transform.forward * (range/2f), range);
    }
}
