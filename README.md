Here is a set of questions aimed at assessing the basic understanding of clustering, including fundamental concepts like resources, clusters, and their components. Each question is assigned points to help evaluate the interviewee's grasp of basic clustering principles.

### Basic Understanding Questions and Points

1. **What is a cluster in the context of computing?**  
   **Points:** 5  
   *Expected Answer:*  
   - A cluster is a group of interconnected computers that work together as a single system to ensure high availability, scalability, and reliability.

2. **Define a resource in the context of failover clustering.**  
   **Points:** 5  
   *Expected Answer:*  
   - A resource is any hardware, software, or service managed by the cluster to provide a specific function, such as a virtual machine, disk, or network service.

3. **What is the primary purpose of failover clustering?**  
   **Points:** 5  
   *Expected Answer:*  
   - To provide high availability and reliability by ensuring that services and applications continue to run even if one or more components fail.

4. **Explain the role of the cluster service in failover clustering.**  
   **Points:** 10  
   *Expected Answer:*  
   - The cluster service manages the cluster configuration, monitors the health of resources, and facilitates failover and recovery processes.

5. **What are the main components of a failover cluster?**  
   **Points:** 10  
   *Expected Answer:*  
   - Nodes (servers), shared storage, network infrastructure, and the cluster service software.

6. **Describe what a node is in a cluster.**  
   **Points:** 5  
   *Expected Answer:*  
   - A node is an individual server that is part of a cluster, contributing its resources to the cluster's overall capacity.

7. **What is a quorum in the context of failover clustering?**  
   **Points:** 10  
   *Expected Answer:*  
   - Quorum is a voting mechanism used to ensure that the cluster has enough votes to remain operational, preventing split-brain scenarios.

8. **How does a failover process work in a cluster?**  
   **Points:** 10  
   *Expected Answer:*  
   - If a node or resource fails, the cluster service detects the failure and automatically transfers the workload to another healthy node, ensuring continuous availability.

9. **What is the purpose of a cluster shared volume (CSV)?**  
   **Points:** 10  
   *Expected Answer:*  
   - CSVs provide a shared storage area accessible by all nodes in the cluster, allowing multiple nodes to read and write to the same disk simultaneously.

10. **What are the benefits of using a failover cluster?**  
    **Points:** 10  
    *Expected Answer:*  
    - High availability, improved reliability, load balancing, and scalability.

11. **What is the role of a witness disk or file share in a cluster quorum?**  
    **Points:** 10  
    *Expected Answer:*  
    - A witness disk or file share acts as an additional vote in the quorum to help the cluster maintain majority and remain operational, especially in scenarios with an even number of nodes.

12. **Explain the concept of 'failback' in failover clustering.**  
    **Points:** 5  
    *Expected Answer:*  
    - Failback is the process of returning services to their original node once it becomes available again after a failure.

13. **What is cluster validation, and why is it important?**  
    **Points:** 10  
    *Expected Answer:*  
    - Cluster validation is a set of tests that verify the hardware and software configurations are suitable for a failover cluster, ensuring reliability and supportability.

14. **Describe the difference between active-passive and active-active clustering.**  
    **Points:** 10  
    *Expected Answer:*  
    - Active-passive: One node is active while the other(s) are on standby.
    - Active-active: All nodes are active and share the workload, providing better resource utilization.

15. **What is the purpose of heartbeat communication in a cluster?**  
    **Points:** 5  
    *Expected Answer:*  
    - Heartbeat communication is used by cluster nodes to monitor each other's health and status, ensuring timely detection of node failures.

16. **What does the term 'split-brain' mean in the context of clustering?**  
    **Points:** 10  
    *Expected Answer:*  
    - Split-brain occurs when there is a communication failure between cluster nodes, causing them to operate independently and potentially leading to data inconsistencies.

17. **What is a cluster-aware application, and why is it important?**  
    **Points:** 10  
    *Expected Answer:*  
    - A cluster-aware application is designed to work seamlessly within a clustered environment, supporting failover and recovery mechanisms to ensure high availability.

18. **How do you add a new node to an existing cluster?**  
    **Points:** 10  
    *Expected Answer:*  
    - Use the Failover Cluster Manager or PowerShell cmdlets to add the new node, then validate and configure it to join the existing cluster.

19. **What is the significance of cluster nodes having access to shared storage?**  
    **Points:** 10  
    *Expected Answer:*  
    - Shared storage ensures that all nodes can access the same data, which is essential for maintaining data consistency and supporting failover processes.

20. **How does the cluster service handle network partition scenarios?**  
    **Points:** 10  
    *Expected Answer:*  
    - The cluster service uses quorum and heartbeats to determine node availability and prevent split-brain scenarios by ensuring only a majority of nodes can operate the cluster resources.

### Total Points: 200

These questions cover fundamental clustering concepts, ensuring that the interviewee has a solid basic understanding of what clusters are, how they function, and why they are important in providing high availability and reliability in IT environments.

Here is a set of questions to assess the interviewee's understanding of the article on how Failover Clustering recovers from unresponsive resources. Each question is assigned points based on its complexity and depth of understanding required.

### Questions and Points

1. **Describe the roles of the 'LooksAlive' and 'IsAlive' checks in Failover Clustering.**  
   **Points:** 10  
   *Expected Answer:*  
   - LooksAlive: A quick, lightweight health check performed every 5 seconds by default to see if the resource appears to be functioning.
   - IsAlive: A more comprehensive health check performed every 60 seconds by default to confirm the resource is indeed functioning properly.

2. **What happens when a resource fails the 'LooksAlive' check?**  
   **Points:** 10  
   *Expected Answer:*  
   - RHS performs a more comprehensive 'IsAlive' check immediately to verify the resource's health.

3. **Explain what the 'DeadlockTimeout' property is and how it is used in Failover Clustering.**  
   **Points:** 15  
   *Expected Answer:*  
   - DeadlockTimeout is the period RHS waits for a resource to respond to an entry point call before taking recovery action. The default is 5 minutes (300,000 milliseconds). It can be modified using PowerShell commands.

4. **What are the steps Failover Clustering takes when a resource becomes unresponsive and doesn't respond within the DeadlockTimeout period?**  
   **Points:** 20  
   *Expected Answer:*  
   - RHS waits for the DeadlockTimeout period.
   - If no response, Cluster Service terminates the RHS process.
   - Cluster Service waits for DeadlockTimeout x 4 for RHS to terminate.
   - If RHS does not terminate, NetFT bugchecks the node to force failover and recovery.

5. **How does Failover Clustering manage the impact of terminating the RHS process when multiple resources share the same RHS process?**  
   **Points:** 15  
   *Expected Answer:*  
   - If one resource causes an RHS crash, all resources in that RHS process are restarted.
   - The misbehaving resource is marked with SeparateMonitor to run in its own RHS process to prevent future issues.

6. **What improvements were introduced in Windows Server 2012 to mitigate the impact of non-responsive resource recovery?**  
   **Points:** 20  
   *Expected Answer:*  
   - Resource Re-attach: Allows healthy resources to re-attach to the new RHS process without being restarted.
   - Isolation of Core Resources: Segments resources into multiple RHS processes to prevent application resource deadlocks from impacting core cluster functionality.

7. **Detail the steps you would take to troubleshoot an RHS recovery event.**  
   **Points:** 20  
   *Expected Answer:*  
   - Open Event Viewer and look for Event ID 1230.
   - Identify the date/time, resource name, and resource type.
   - Generate the cluster log with Get-ClusterLog cmdlet.
   - Open the Cluster.log file and find the point of failure.
   - Identify the entry point being called and understand what it was attempting to do.
   - Investigate the underlying component causing the issue.

8. **What is the impact of enabling the SeparateMonitor property for a resource?**  
   **Points:** 10  
   *Expected Answer:*  
   - Resources run in their own dedicated RHS process, which consumes more system resources but isolates misbehaving resources to prevent them from affecting others.

9. **Explain the role of the 'Get-ClusterLog –UseLocalTime' cmdlet in troubleshooting Failover Clustering issues.**  
   **Points:** 5  
   *Expected Answer:*  
   - It generates the cluster log in local time, making it easier to correlate with event logs for troubleshooting.

10. **What does Event ID 1146 signify in the context of RHS recovery?**  
    **Points:** 5  
    *Expected Answer:*  
    - Indicates that the RHS process stopped unexpectedly, usually associated with the recovery of a crashed or deadlocked resource.

### Total Points: 130

The points system helps gauge the depth of the interviewee's understanding and their ability to explain complex concepts clearly.

Here are additional questions to further assess the interviewee's knowledge of failover clustering, specifically focusing on deeper technical understanding and real-world application of concepts:

### Additional Questions and Points

1. **Explain the difference between 'Physical Disk' resources and 'Virtual Machine' resources in the context of failover clustering.**  
   **Points:** 10  
   *Expected Answer:*  
   - Physical Disk resources manage storage volumes used by the cluster, ensuring data availability and redundancy.
   - Virtual Machine resources control clustered VMs, managing their start, stop, and health checks.

2. **How would you manually configure a resource to run in its own dedicated RHS process? Provide the PowerShell command and explain its impact.**  
   **Points:** 10  
   *Expected Answer:*  
   - Use the command `(Get-ClusterResource "Resource Name").SeparateMonitor = 1`.
   - This isolates the resource in its own RHS process, reducing the risk of it affecting other resources if it becomes unresponsive.

3. **What are the implications of setting a very short DeadlockTimeout value for a critical resource?**  
   **Points:** 10  
   *Expected Answer:*  
   - A very short DeadlockTimeout might cause the RHS process to terminate too quickly, leading to unnecessary resource restarts and potential instability in the cluster.

4. **Describe the steps the cluster service takes if the RHS process does not terminate within the extended DeadlockTimeout period (20 minutes).**  
   **Points:** 10  
   *Expected Answer:*  
   - The cluster service will call NetFT to bugcheck the node, forcing a failover and recovery to ensure overall cluster health.

5. **What are some common causes for a resource to fail an 'IsAlive' check, and how would you troubleshoot them?**  
   **Points:** 15  
   *Expected Answer:*  
   - Causes: Network issues, storage I/O problems, resource DLL bugs.
   - Troubleshooting: Check network connectivity, verify storage health, review event logs and cluster logs for errors, and analyze user-mode dumps if necessary.

6. **How does the 'Resource Re-attach' feature in Windows Server 2012 improve failover clustering behavior compared to earlier versions?**  
   **Points:** 15  
   *Expected Answer:*  
   - Allows healthy resources to re-attach to a new RHS process without being restarted, minimizing the impact on cluster services and reducing downtime.

7. **What is the role of NetFT in failover clustering, and how does it interact with the cluster service during a node bugcheck?**  
   **Points:** 10  
   *Expected Answer:*  
   - NetFT (Network Fault Tolerant) handles network communications and failover decisions. During a bugcheck, it forces a node to failover to ensure cluster continuity.

8. **Explain how the 'Get-ClusterLog' cmdlet is used in diagnosing cluster issues and provide an example command with the '-UseLocalTime' option.**  
   **Points:** 10  
   *Expected Answer:*  
   - The cmdlet generates detailed logs of cluster activity, useful for troubleshooting. Example: `Get-ClusterLog -UseLocalTime`.

9. **What would be your approach to investigating a recurring unresponsive resource issue in a cluster?**  
   **Points:** 15  
   *Expected Answer:*  
   - Review event logs for patterns.
   - Generate and analyze cluster logs.
   - Isolate the resource using SeparateMonitor.
   - Update or patch resource DLLs.
   - Consult Microsoft support if necessary.

10. **Describe how the isolation of core resources in multiple RHS processes enhances cluster stability.**  
    **Points:** 10  
    *Expected Answer:*  
    - Segregates critical resources into separate RHS processes, ensuring that application resource issues do not impact core cluster services, enhancing overall stability.

11. **What is the significance of the STOP 0x9E bugcheck code in the context of failover clustering, and how should it be handled?**  
    **Points:** 10  
    *Expected Answer:*  
    - Indicates a severe issue with the RHS process failing to terminate. Handle by investigating resource health, reviewing logs, and potentially involving hardware checks or vendor support.

12. **How can you configure debugging for the RHS process to generate more detailed information during a deadlock? Provide the relevant registry keys and values.**  
    **Points:** 15  
    *Expected Answer:*  
    - Configure by setting the registry DWORD `HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Failover Clusters\DebugBreakOnDeadlock` to `3`.
    - For Windows Server 2012 R2 and later: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\ClusSvc\Parameters\DebugBreakOnDeadlock` to `3`.

13. **Discuss the importance of resource DLLs in failover clustering and what actions you would take if a resource DLL is suspected to be the cause of a resource failure.**  
    **Points:** 10  
    *Expected Answer:*  
    - Resource DLLs manage the interactions between the cluster service and resources. If suspected, review logs, update or patch the DLL, and potentially replace or reconfigure the resource.

14. **What are the potential risks of manually modifying cluster resource properties, and how can you mitigate them?**  
    **Points:** 10  
    *Expected Answer:*  
    - Risks include resource instability, unintended failovers, and cluster downtime. Mitigate by thoroughly testing changes in a staging environment, documenting modifications, and applying changes during maintenance windows.

### Total Points for Additional Questions: 180

These additional questions aim to deepen the interviewee's understanding of failover clustering, focusing on practical application, troubleshooting, and advanced configuration.

